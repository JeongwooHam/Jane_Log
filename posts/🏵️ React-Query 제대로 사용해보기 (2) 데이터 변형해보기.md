<h2 id="🤔-찾아보게-된-계기">🤔 찾아보게 된 계기</h2>
<p>토이 프로젝트에서 Open API에서 불러온 데이터를 필터링하는 로직을 구현하게 되었다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/719c1a86-eb5f-4517-abf7-5521a87bb8bb/image.png" /></p>
<p>위와 같은 형태의 컴포넌트였는데, 어떻게 필터값을 반영해야 할 지에 대해 고민이 많았다.
물론 필터링 종류가 많아서도 맞지만, 가장 고민이었던 점은
Open API에서 값을 받아오기 때문에 원하는 필터 값을 프론트에서 직접 구현해야 한다는 점이었다.
어떻게 하면 클라이언트에서 필터링 되지 않은 채로 받은 응답 값을 정제할 때,
최소한의 API 요청과 최대한의 퍼포먼스를 낼 수 있을까?
이에 대해 react-query의 데이터를 변형하는 좋은 방법들이 있어서 정리해보고자 한다.</p>
<pre><code>👩‍💻 가능하다면 백엔드에서 처리하는 것도 좋은 방법입니다.!</code></pre><h2 id="데이터를-변형할-수-있는-방법들">데이터를 변형할 수 있는 방법들</h2>
<h3 id="🟠-queryfn에서-구현하기">🟠 queryFn에서 구현하기</h3>
<ul>
<li>queryFn<ul>
<li><code>useQuery</code>에 전달해야 하는 함수이다.</li>
<li>Promise 값을 반환할 것을 예상하며, 결과 값은 query cache에 저장된다.</li>
</ul>
</li>
<li>하지만 꼭 백엔드에서 전달되는 값 원형 그대로를 반환할 필요는 없으므로 queryFn을 통해서 값을 변형하는 것도 가능하다.<ul>
<li>이를 통해 프론트엔드에서는 마치 원래 백엔드에서 이 형태의 값을 전달받은 것처럼 사용할 수 있다.</li>
</ul>
</li>
</ul>
<pre><code>const fetchAnimalList = async (): Promise&lt;Animal[]&gt; =&gt; {
  const response = await axios.get('/animalList/Seoul')
  const data: Animal[] = response.data

  return data.map((animal) =&gt; animal.name.toUpperCase())
}

export const useGetAnimalList = () =&gt;
  useQuery({
    queryKey: ['animalList'],
    queryFn: fetchAnimalList,
  })
</code></pre><ul>
<li>위의 코드의 경우, 프론트엔드 측에서는 동물의 이름이 대문자가 아닌 데이터, 즉 원본 데이터에는 접근할 수 없다.<ul>
<li>react-query-devtools에서는 변형된 구조의 데이터만 볼 수 있다.</li>
<li>네트워크를 추적해야 원본 데이터 구조를 볼 수 있다.</li>
</ul>
</li>
<li>react-query가 최적화를 해줄 수 없다.<ul>
<li>데이터 fetching이 실행될 때마다 데이터 변형도 같이 동작한다.</li>
<li>이것은 과도한 코스트로 다른 대안을 찾아보아야 할 원인이 될 수 있다.</li>
</ul>
</li>
<li>데이터 fetching을 추상화하여 API를 공유하는 경우 이 수준의 데이터 변형에 대한 접근 권한이 없을 수도 있다.</li>
</ul>
<blockquote>
<p>⭕ 장점</p>
</blockquote>
<ul>
<li>백엔드에서 데이터를 받은 것처럼 사용할 수 있다.</li>
</ul>
<blockquote>
<p>❌ 단점</p>
</blockquote>
<ul>
<li>변형된 데이터가 cache에 저장되어 원본 데이터 구조에 접근할 수 없다.</li>
<li>모든 데이터 fetching에서 작동한다.</li>
<li>자유롭게 변경할 수 없는 공유 API를 가진 경우 실현 불가능하다.</li>
</ul>
<h3 id="🟡-렌더링-함수에서-구현하기">🟡 렌더링 함수에서 구현하기</h3>
<ul>
<li>custom hook을 사용하여 데이터 변형을 할 수도 있다.</li>
</ul>
<pre><code>const fetchAnimalList = async (): Promise&lt;Animal[]&gt; =&gt; {
  const response = await axios.get('/animalList/Seoul')
  return response.data
}

export const useGetAnimalList = () =&gt; {
  const queryInfo = useQuery({
    queryKey: ['animalList'],
    queryFn: fetchAnimalList,
  })

  return {
    ...queryInfo,
    data: queryInfo.data?.map((animal) =&gt; animal.name.toUpperCase()),
  }
}</code></pre><ul>
<li>이렇게 구현할 경우 모든 fetch 함수가 동작 시 뿐만 아니라 모든 렌더링 시 이 함수가 실행되게 된다.<ul>
<li>데이터 fetching을 포함하지 않는 렌더링에서도!</li>
</ul>
</li>
</ul>
<pre><code>👩‍💻 useMemo를 사용하여 이러한 문제를 해결해볼 수 있습니다.</code></pre><blockquote>
<p><code>useMemo</code>로 최적화하기</p>
</blockquote>
<ul>
<li><p>이때 주의할 점은, 종속성을 최대한 좁게 정의해야 한다는 것이다.</p>
<pre><code>  data: React.useMemo(
        () =&gt; queryInfo.data?.map((animal) =&gt; animal.name.toUpperCase()),
        [queryInfo]
  )</code></pre><ul>
<li>이런 식으로 사용할 경우 <code>useMemo</code>를 사용하는 의미가 없다.</li>
<li><code>queryInfo</code>를 의존성 배열에 추가할 경우 결국 매 렌더링마다 다시 변형이 동작하는 것은 동일하기 때문이다.</li>
</ul>
</li>
<li><p>아래와 같은 방식으로 구현해보자.</p>
</li>
</ul>
<pre><code>export const useGetAnimalList = () =&gt; {
  const queryInfo = useQuery({
    queryKey: ['animalList'],
    queryFn: fetchAnimalList,
  })

  return {
    ...queryInfo,
    data: React.useMemo(
      () =&gt; queryInfo.data?.map((animal) =&gt; animal.name.toUpperCase()),
      [queryInfo.data]
    ),
  }
}</code></pre><ul>
<li><code>queryInfo</code> 내부의 data는 무언가가 실제로 변하는 경우, 다시 말해 다시 데이터의 변형을 수행하고 싶은 상황이 아니라면 참조적으로 안전하다.</li>
</ul>
<ul>
<li><p>여기에 데이터 변형과 함께 추가로 사용하고 싶은 로직을 넣어주어도 좋다.</p>
<ul>
<li>하지만 데이터가 <code>undefined</code> 될 수 있으므로 옵셔널 체이닝을 꼭 같이 사용해주도록 하자.</li>
</ul>
</li>
<li><p>추가로, React Query가 v4부터 <code>Tracked Queries</code> 추가해서 위의 <code>...queryInfo</code>와 같은 구조분해할당 코드는 지양하는 추세가 되었음에 주의하자.</p>
</li>
</ul>
<blockquote>
<p>⭕ 장점</p>
</blockquote>
<ul>
<li><code>useMemo</code>를 사용하여 최적화할 수 있다.</li>
</ul>
<blockquote>
<p>❌ 단점</p>
</blockquote>
<ul>
<li>개발자도구에서 정확한 형태를 검사할 수 없다.</li>
<li>구조가 조금 더 복잡해진다.</li>
<li>데이터가 <code>undefined</code> 될 수 있다.</li>
<li>tracked queries와 함께 사용하는 것은 권장되지 않는다.</li>
</ul>
<h2 id="🤠-select-옵션을-사용해봅시다">🤠 Select 옵션을 사용해봅시다!</h2>
<h3 id="👾-select-옵션">👾 Select 옵션</h3>
<ul>
<li><p><code>select: (data: TData) => unknown</code></p>
</li>
<li><p>optional한 속성이다.</p>
</li>
<li><p>query 함수로 반환되는 데이터의 일부를 변형하거나 선택할 수 있다.</p>
</li>
<li><p>반환되는 데이터의 값에 영향을 미치지만 쿼리 cache에 저장되는 값에는 영향을 미치지 않는다.</p>
</li>
<li><p>데이터가 존재할 때에만 selector가 호출되므로 <code>undefined</code> 값에 대해 걱정하지 않아도 된다.</p>
</li>
<li><p>예를 들어, <strong>동물 구분</strong>이 <strong>'개'</strong> 에 해당하는 동물을 필터링한다고 가정해보자.</p>
<pre><code>const useGetAnimalList = (queryKeys, func, filterLogic) =&gt; useQuery(
  [queryKeys],
  () =&gt; func(),
  {
      select: (animals) =&gt; animals.filter(filterLogic)
  }
)</code></pre></li>
<li><p>filter로직에는 <code>(animal) => animal.category === '개'</code>가 들어갈 수 있을 것이고, <code>category</code>와 <code>'개'</code> 부분만 재사용이 가능하도록 다른 값으로 바꾼다면 편리하게 useQuery만 사용해서 필터링 로직을 구현할 수 있다.</p>
</li>
<li><p>useQuery의 cache 된 데이터를 건드리지 않으면서 필터링을 구현하므로 useQuery의 normalization(정규화, 데이터 중복 방지)에 대한 장점과 필터링 로직을 동시에 사용할 수 있게 된다.</p>
</li>
</ul>
<h3 id="💾-selector-memoization">💾 Selector Memoization</h3>
<ul>
<li>selector 함수를 위의 코드와 같이 인라인 함수로 정의할 경우 매 렌더링마다 해당 함수가 동작하게 된다.<ul>
<li>이는 과도한 코스트를 발생시킬 수 있으므로 함수를 memoize하자!</li>
</ul>
</li>
</ul>
<blockquote>
<p><code>useCallback</code> 사용하기</p>
</blockquote>
<pre><code>select: React.useCallback((animals) =&gt; animals.filter(filterLogic), [])</code></pre><blockquote>
<p>함수의 참조를 안정적으로 만들기</p>
</blockquote>
<pre><code>const transFormLogic = (data: Animal[], filterLogic) =&gt;
  data.map((animals) =&gt; animals.filter(filterLogic))

const useGetAnimalList = (queryKeys, func, filterLogic) =&gt; useQuery(
    [queryKeys],
    () =&gt; func(),
    {
        select: transFormLogic
    }
)</code></pre><h3 id="🧐-select해야-하는-값이-여러-종류라면">🧐 select해야 하는 값이 여러 종류라면?</h3>
<ul>
<li>select 옵션은 데이터의 일부만을 구독하기 위해 사용할 수도 있다.</li>
</ul>
<pre><code>export const useGetAnimalList = (select) =&gt;
  useQuery({
    queryKey: ['animalList'],
    queryFn: fetchAnimalList,
    select,
  })

export const useOnlyCategory = (targetCategory: string) =&gt;
  useGetAnimalList((data) =&gt; data.map((animal) =&gt; animal.category))

export const useFindAnimal = (targetName: string) =&gt;
  useGetAnimalList((data) =&gt; data.find((animal) =&gt; animal.name === targetName))</code></pre><ul>
<li>이렇게 <code>useGetAnimalList</code>에 커스텀 selector들을 넘겨줌으로써 원본 데이터에서 필요한 데이터만 받아 쓸 수 있다.<ul>
<li>이때 select 함수를 인자로 넘겨주지 않을 경우 cache 된 전체 데이터가 반환된다.</li>
<li>하지만 select 함수를 넘겨주면 해당 데이터만 확인할 수 있게 된다.</li>
</ul>
</li>
<li>만약 데이터에서 동물들의 이름이 바뀌었더라도 <code>useOnlyCategory</code>를 통해 카테고리 정보만 구독하고 있는 컴포넌트는 리렌더링되지 않는다.<ul>
<li>물론 React Query의 메타 데이터 중 <code>isFetching</code>의 상태 변화에 따라 두 번 렌더링 될 가능성은 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>⭕ 장점</p>
</blockquote>
<ul>
<li>최적화에 가장 적합하다.</li>
<li>부분적인 정보의 구독이 가능하다.</li>
</ul>
<blockquote>
<p>❌ 단점</p>
</blockquote>
<ul>
<li>데이터를 관찰하는 모든 부분에서 구조가 다를 수 있다.</li>
</ul>
<pre><code>👩‍💻 이처럼 여러 방식들을 찾아보면서 select 옵션이 원하는 로직의 구현에 가장 적합하다는 결론을 내렸다! </code></pre><h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://tanstack.com/query/v4/docs/react/reference/useQuery">TanStack Query 공식문서_useQuery</a></li>
<li><a href="https://sangcho.tistory.com/entry/React-query-data-filter">[React-query]데이터 filtering하기</a></li>
<li><a href="https://tkdodo.eu/blog/react-query-data-transformations">React Query Data Transformations</a></li>
</ul>