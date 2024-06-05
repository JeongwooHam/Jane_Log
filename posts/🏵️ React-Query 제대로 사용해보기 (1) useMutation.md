<h3 id="🤔-usemutation이란">🤔 useMutation이란?</h3>
<ul>
<li>React-Query를 이용해 서버에 변경(insert, update, delete) 작업 요청 시 사용</li>
</ul>
<h3 id="🧐-어떻게-사용하는가">🧐 어떻게 사용하는가?</h3>
<blockquote>
<p>mutationFn</p>
</blockquote>
<ul>
<li>promise 처리가 이루어지는 mutation function</li>
<li>axios를 이용해 서버에 API를 요청하는 부분</li>
</ul>
<pre><code class="language-jsx">// 첫 번째 방법
const deleteData = useMutation(() =&gt; axios.delete(`api/delete/${id}`));

// 두 번째 방법
const deleteData = useMutation({
  mutationFn: (id) =&gt; axios.delete(`api/delete/${id}`)
})</code></pre>
<blockquote>
<p>mutate</p>
</blockquote>
<ul>
<li>useMutation을 이용해 작성한 내용들이 실제로 실행될 수 있도록 돕는 trigger 역할을 함</li>
<li>useMutation을 정의해준 후, 이벤트 발생 시 사용하는 것</li>
</ul>
<pre><code class="language-jsx">const { mutate } = () =&gt; deleteData()

const deleteFn = () =&gt; {
    deleteData.mutate(id)
}</code></pre>
<blockquote>
<p>onSuccess, onError, onSettled</p>
</blockquote>
<p><strong>async/await 만 사용했을 때</strong></p>
<pre><code class="language-jsx">const deleteData = async () =&gt; {
    try{
        const res = await axios.delete(`api/delete/${id}`)
        .then((res) =&gt; console.log(res.data))
    } catch(err) {
        console.error('error', err.message)
    } finally {
        console.log('어쨌든 실행되는 부분')
    }
}</code></pre>
<p><strong>useMutation 적용 시</strong></p>
<pre><code class="language-jsx">// fn key 값 생략된 버전
const deleteData = useMutation((id) =&gt; axios.delete(`api/delete/${id}`), {
    onSuccess: () =&gt; { console.log('요청 성공') },
      onError: () =&gt; { console.error('에러 발생') },
      onSettled: () =&gt; { console.log('결과에 관계 없이 무언가 실행됨') }
})

// fn key 값 명시된 버전
const deleteData = useMutation({
      mutationFn: (id) =&gt; axios.delete(`api/delete/${id}`),
    onSuccess: () =&gt; { console.log('요청 성공') },
      onError: () =&gt; { console.error('에러 발생') },
      onSettled: () =&gt; { console.log('결과에 관계 없이 무언가 실행됨') }
})</code></pre>
<ul>
<li>onSuccess, onError, onSettled는 useMutation 정의 시 뿐만 아니라 mutate에서도 사용 가능</li>
</ul>
<h3 id="💓-usemutation으로-낙관적-업데이트-하기">💓 useMutation으로 낙관적 업데이트 하기</h3>
<ul>
<li>React Query는 낙관적 업데이트를 지원하며, 서버의 데이터 업데이트가 성공하기 전에도 UI를 업데이트할 수 있게 함</li>
<li>서버와의 데이터 동기화를 신경쓰지 않고 먼저 사용자에게 성공 시 UI를 보여준 후, 요청의 결과가 오면 성공/실패 여부에 따라 UI 업데이트</li>
<li>사용자는 서버와의 통신 여부와 관계 없이 UI를 확인할 수 있게 됨</li>
<li>예: 인스타그램의 좋아요 기능, 카카오톡이 일단 전송된 후 성공, 취소/재전송 창이 나중에 뜨는 것</li>
</ul>
<blockquote>
<p>onMutate</p>
</blockquote>
<ul>
<li>React Query에서 낙관적 업데이트를 수행하는 방법</li>
<li>API Call 전에 실행되는 함수</li>
<li>성공 시 현재 데이터 캐시를 업데이트하거나 UI를 변경하고, 실패 시 사용할 수 있는 rollback 매커니즘도 제공함</li>
<li>onMutate callback 함수에서 UI를 업데이트하고, setQueryData 함수로 이전 데이터 업데이트</li>
<li>onError 콜백함수에서 에러 발생 시 이전 데이터로 rollback</li>
</ul>
<pre><code class="language-jsx">const queryClient = useQueryClient(() =&gt; axios.post(`api/like/${id}`), {
    onMutate: async (id) =&gt; {
      // 'queryKey'로 진행 중인 refetch 취소하여 낙관적 업데이트를 덮어쓰지 않도록 함
        await queryClient.cancleQueries({
            queryKey: ['queryKey]
        })

      // 이전 데이터를 받아옴
        const previousData = queryClient.getQueryData(['queryKey']);

      // 새로운 값으로 낙관적 업데이트
          queryClient.setQueryData(['queryKey'], (prev) =&gt; !prev)

          return { previousData }
    },
  // mutation이 실패한 경우
  onError: (err, newData, context) =&gt; {
    // onMutate로부터 반환된 context를 사용하여 rollback
    queryClient.setQueryData(['queryKey'], context.previousData)
  },
  onSettled: () =&gt; {
    // 성공, 실패 여부에 관계 없이 refetch
       queryClient.invalidateQueries({queryKey: ['queryKey']}) 
  }
});

const deleteData = useMutation({

})
</code></pre>
<h3 id="💡-usemutation으로-업데이트-된-데이터를-반영하려면">💡 useMutation으로 업데이트 된 데이터를 반영하려면?</h3>
<blockquote>
<p>invalidateQueries</p>
</blockquote>
<ul>
<li>useQuery에서 사용된 queryKey의 유효성을 제거해줄 목적으로 사용됨</li>
<li>queryKey의 유효성을 제거해주는 이유?<ul>
<li>서버로부터 데이터를 다시 조회해오기 위해서!</li>
</ul>
</li>
<li>useQuery에는 staleTime, cacheTime이 존재하여 업데이트 사항이 생겼더라도 해당 시간이 지나기 전까지는 동일한 데이터를 화면에 보여줌</li>
<li>invalidateQueries를 사용해 가지고 있던 queryKey의 유효성을 제거해줌으로써 캐싱되어 있던 데이터 대신 새로운 데이터를 서버에 요청</li>
</ul>
<pre><code class="language-jsx">const queryClient = useQueryClient(); // 등록된 queryClient를 가져옴

const deleteData = useMutation((id) =&gt; axios.delete(`api/delete/${id}`), {
    onSuccess: () =&gt; { 
      console.log('요청 성공');
      // 요청 성공 시 해당 queryKey 유효성 제거
      queryClient.invalidateQueries('queryKey')
    },
      onError: () =&gt; { console.error('에러 발생') },
      onSettled: () =&gt; { console.log('결과에 관계 없이 무언가 실행됨') }
})
</code></pre>
<h4 id="🌟-references">🌟 References</h4>
<p><a href="https://tanstack.com/query/v4/docs/react/reference/useMutation">공식 문서</a>
<a href="https://jforj.tistory.com/244">참조 블로그 1</a>
<a href="https://subtlething.tistory.com/127">참조 블로그 2</a></p>