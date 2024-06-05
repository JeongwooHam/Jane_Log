<p>2022년 3월에 발표된 React 18은 성능 향상과 렌더링 엔진 개선에 초점이 맞춰져 있다.
React 18은 동시성(concurrent) React를 강조하며 여러 가지 새로운 기능들을 출시하였는데, 
프로젝트에 해당 기능들을 적용하기에 앞서 이 중 몇 가지 기능들을 자세히 알아보고자 한다.</p>
<h3 id="🤠-react-18의-새로운-기능-첫-번째-automatic-batching">🤠 React 18의 새로운 기능 첫 번째, Automatic Batching!</h3>
<pre><code>👩‍🏫 React 18은 애플리케이션이나 라이브러리 코드에 대한 
수동 배치(batch) 업데이트를 제거하였습니다.
그리고 이를 통해 우리는 별도의 설치나 구성 없이도 
바로 더 많은 Batching을 통해 성능의 개선을 경험할 수 있습니다.</code></pre><p align="center"><img src="https://velog.velcdn.com/images/hamjw0122/post/c9bbad2a-8b56-4032-932c-e9d2338b0eac/image.png" width="20%" /><span>그런데,, 여기서 말하는 배칭(Batching)이란 뭘까..?</span></p>



<h2 id="🤔-batching이란-무엇인가">🤔 Batching이란 무엇인가!</h2>
<blockquote>
<p>Batching</p>
</blockquote>
<ul>
<li>React가 더 나은 성능을 위해 다수의 상태 업데이트를 한 번의 리렌더링으로 묶는 것을 말한다.</li>
<li>하나의 클릭 이벤트에 두 개의 상태 업데이트가 엮여 있다고 가정해보자.<ul>
<li>이때 React는 항상 이 두 개의 업데이트를 하나의 리렌더링으로 Batching 한다.</li>
<li>클릭 이벤트가 발생할 때마다 두 개의 상태 업데이트를 설정해두어도 React는 오직 한 번의 렌더링만을 수행한다.</li>
</ul>
</li>
</ul>
<pre><code class="language-js">function App() {
  const [count, setCount] = useState(0);
  const [isOpen, setIsOpen] = useState(false);

  function handleClick() {
    setCount(prev =&gt; prev + 1); // 아직 리렌더링 되지 않음
    setIsOpen(prev =&gt; !prev); // 아직 리렌더링 되지 않음
    // React는 마지막에 한 번만 리렌더링한다!
  }

  return (
    &lt;div&gt;
      &lt;button onClick={handleClick}&gt;Next&lt;/button&gt;
      &lt;h1&gt;{isOpen ? &quot;열림&quot; : &quot;닫힘&quot;}&lt;/h1&gt;
      {isOpen &amp;&amp; &lt;Toggle Component/&gt;}
    &lt;/div&gt;
  );
}</code></pre>
<ul>
<li>클릭 당 한 번의 렌더링만 발생한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/6f4ffbc8-bbf0-464c-ad21-0f5ab6cb566f/image.png" /></li>
</ul>
<h3 id="👥-batching은-왜-좋을까">👥 Batching은 왜 좋을까?</h3>
<ol>
<li>불필요한 리렌더링을 피해서 성능에 좋다.</li>
<li>하나의 상태 변수만 업데이트 된 경우에 컴포넌트가 '반만 완료된' 상태를 렌더링해 버그를 야기할 수 있는 경우를 방지할 수 있다.</li>
</ol>
<pre><code>👩‍🏫 엘리베이터가 한 명이 탔다고 바로 출발하고 
각 탑승객마다 동일한 이동을 반복하는 것이 아니라 
타려는 사람이 모두 탑승한 이후 출발하는 모습을 상상해봅시다!</code></pre><h3 id="⚠️-기존-batching의-문제점">⚠️ 기존 Batching의 문제점</h3>
<ul>
<li>React에서 업데이트를 Batching하는 시점이 일관적이지 않았다.</li>
<li>예를 들어, 데이터 fetching을 한 뒤 클릭 이벤트 함수 내부의 상태가 업데이트 되도록 하는 상황을 가정해보자.<ul>
<li>이때 React는 업데이트를 Batching하지 않고 두 개의 독립적인 업데이트를 실행했다.</li>
<li>이는 React가 오직 브라우저 이벤트가 발생하는 <strong>동안</strong>에만 업데이트를 수행하고, 이벤트가 이미 핸들링 <strong>된 후</strong>에는 업데이트를 하지 않기 때문에 발생하는 상황이다.</li>
</ul>
</li>
</ul>
<pre><code class="language-js">function App() {
  const [count, setCount] = useState(0);
  const [flag, setFlag] = useState(false);

  function handleClick() {
    fetchSomething().then(() =&gt; {
      // callback 실행 이후에 동작하는 부분이므로
      // React 17 이전의 경우 이 부분은 Batching 되지 않음
      setCount(c =&gt; c + 1); // 리렌더링 발생
      setFlag(f =&gt; !f); // 리렌더링 발생
    });
  }

  return (
    &lt;div&gt;
      &lt;button onClick={handleClick}&gt;Next&lt;/button&gt;
      &lt;h1 style={{ color: flag ? &quot;blue&quot; : &quot;black&quot; }}&gt;{count}&lt;/h1&gt;
    &lt;/div&gt;
  );
}</code></pre>
<ul>
<li>클릭 할 때마다 두 개 모두에 대한 렌더링이 각각 발생한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/fc32816a-e0d8-4c21-aa5d-1f302a9fb93e/image.png" /></li>
</ul>
<pre><code>👩‍🏫 이러한 문제를 해결하기 위해 Automatic Batching이 등장했습니다!</code></pre><h2 id="🧐-automatic-batching은-무엇일까">🧐 Automatic Batching은 무엇일까?</h2>
<ul>
<li><p>Automatic Batching이 없을 때에는 Batching이 오직 React 이벤트 핸들러 내부에서만 동작했다.</p>
</li>
<li><p>아래와 같은 경우에는 React에서 Batching을 기본 값으로 적용하지 않았다.</p>
<ul>
<li><code>addEventListener()</code>과 같은 기존 DOM 이벤트 리스너</li>
<li>비동기 콜백 (<code>Promise</code>, <code>setTimeout()</code>, <code>setInterval()</code> 등)</li>
</ul>
</li>
<li><p>React 18을 <code>createRoot</code>와 함께 시작하면, 업데이트가 어디에 위치해있는지에 관계 없이 모두 자동 Batching 된다.</p>
<ul>
<li>이제 모든 이벤트 내부의 업데이트는 React 이벤트 내부와 동일한 방식으로 Batching 된다.</li>
<li>이를 통해 더 적은 빈도의 렌더링을 발생시키고, 애플리케이션의 성능을 개선할 수 있다.</li>
</ul>
</li>
</ul>
<pre><code class="language-js">// 이전: 오직 React 이벤트에서만 Batching 적용
setTimeout(() =&gt; {
  setCount(prev =&gt; prev + 1);
  setFlag(prev =&gt; !prev);
  // React는 각각의 상태 업데이트마다 렌더링 된다. (총 두 번)
}, 1000);

// 이후: timeouts, promises 등 모든 이벤트 내부에서 Batching 적용
setTimeout(() =&gt; {
  setCount(prev =&gt; prev + 1);
  setFlag(prev =&gt; !prev);
  // React는 마지막에 한 번만 리렌더링 된다.
}, 1000);</code></pre>
<ul>
<li><p>클릭 시 한 번의 렌더링만 발생한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/53a7a456-489b-4f96-90ef-d0a8aeca303b/image.png" /></p>
</li>
<li><p><code>createRoot</code>를 사용하지 않을 경우 17 이하 버전과 동일하게 동작하니 주의하자!
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/fd42c8e9-60a0-456f-9ac0-2018961690c2/image.png" /></p>
</li>
</ul>
<pre><code>🤔 예전의 동작이 아직 남아있는 이유는 무엇인가요?
👩‍🏫 이전 버전과 18 버전 모두를 사용해 수행 실험을 할 경우에 대비해 존재합니다. 
하지만 React 18 사용 시 createRoot를 사용하여 
automatic batching이 적용되도록 하는 것이 좋겠습니다. </code></pre><ul>
<li>이제 아래의 코드는 모두 동일한 동작을 수행하게 되었다.</li>
</ul>
<pre><code class="language-js">// (1) 클릭 이벤트
function handleClick() {
  setCount(c =&gt; c + 1);
  setFlag(f =&gt; !f);
  // 맨 마지막 부분에서만 리렌더링 발생
}

// (2) setTimeout
setTimeout(() =&gt; {
  setCount(c =&gt; c + 1);
  setFlag(f =&gt; !f);
  // 맨 마지막 부분에서만 리렌더링 발생
}, 1000);

// (3) Promise
fetch(/*...*/).then(() =&gt; {
  setCount(c =&gt; c + 1);
  setFlag(f =&gt; !f);
  // 맨 마지막 부분에서만 리렌더링 발생
})

// (4) DOM 이벤트 리스너
elm.addEventListener('click', () =&gt; {
  setCount(c =&gt; c + 1);
  setFlag(f =&gt; !f);
  // 맨 마지막 부분에서만 리렌더링 발생
});</code></pre>
<ul>
<li>React는 일반적으로 안전한 경우에만 업데이트를 Batching 한다.</li>
<li>예를 들어, React는 다음 이벤트가 발생하기 전 클릭, 키보드 이벤트처럼 사용자 시작 이벤트에 대한 DOM을 완전히 업데이트할 것을 보장한다.<ul>
<li>그리고 이것은 제출 시 비활성화 된 form이 두 번 제출될 수 없도록 하는 등의 효과를 준다.</li>
</ul>
</li>
</ul>
<h2 id="💡-faq">💡 FAQ</h2>
<h3 id="🤷♀️-batch를-원하지-않는다면">🤷‍♀️ Batch를 원하지 않는다면?</h3>
<ul>
<li>대부분의 경우 Batching이 안전하긴 하지만, 상태가 변화하자마자 DOM에서 무언가를 즉시 읽어와야 하는 코드가 있다면 Batching을 사용하지 말아야 할 것이다.</li>
<li>이럴 때는 <strong><em>ReactDOM.flushSync()</em></strong> 를 사용해 Batching을 해제할 수 있다.<ul>
<li>react가 아니라 'react-dom'에서 import 해와야 한다!</li>
</ul>
</li>
</ul>
<pre><code class="language-javascript">import { flushSync } from 'react-dom'; 

function handleClick() {
  flushSync(() =&gt; {
    setCounter(c =&gt; c + 1);
  });
  // 이때 React가 DOM을 업데이트 했다.
  flushSync(() =&gt; {
    setFlag(f =&gt; !f);
  });
  // 이때 React가 DOM을 업데이트 했다.
}</code></pre>
<h3 id="🤷♀️-훅-함수-사용에-문제가-생기진-않을까">🤷‍♀️ 훅 함수 사용에 문제가 생기진 않을까?</h3>
<pre><code>👩‍🏫 그렇습니다!</code></pre><ul>
<li>React 개발팀에서는 대부분의 경우에 automatic batcing이 '그냥 잘 작동'할 것이라고 예측한다. </li>
</ul>
<h3 id="🤷♀️-클래스-사용에-문제가-생기진-않을까">🤷‍♀️ 클래스 사용에 문제가 생기진 않을까?</h3>
<pre><code>👩‍🏫 문제가 생길 수 있는 예외 상황이 존재합니다!</code></pre><blockquote>
<p>17이하 버전에서의 클래스</p>
</blockquote>
<p>클래스에서는 <code>setState</code> 호출 중 <code>this.state</code>를 통해 상태값을 동기적으로 읽을 수 있었다. </p>
<pre><code class="language-js">// React 17 이하 버전
handleClick = () =&gt; {
  setTimeout(() =&gt; {
    this.setState(({ count }) =&gt; ({ count: count + 1 }));

    console.log(this.state); // { count: 1, isClicked: false }

    this.setState(({ isClicked }) =&gt; ({ isClicked: !isClicked }));
  });
};</code></pre>
<blockquote>
<p>18 버전의 클래스</p>
</blockquote>
<p>하지만 이는 React 18에서는 사용할 수 없는 방식이 되었다.
    - <code>setTimeout</code> 내부에 있는 업데이트들까지 모두 Batching되기 때문에 React는 더이상 <code>setState</code>의 결과를 동기적으로 렌더링하지 않게 되었기 때문이다!</p>
<ul>
<li>렌더링은 다음 번 브라우저 틱에서 발생하게 된다.<ul>
<li>틱: 실행되는 프로그램에서의 간격, 내부의 함수가 실행되는 간격</li>
</ul>
</li>
</ul>
<pre><code class="language-js">// 18 버전
handleClick = () =&gt; {
  setTimeout(() =&gt; {
    this.setState(({ count }) =&gt; ({ count: count + 1 }));

    console.log(this.state); // { count: 0, isClicked: false }

    this.setState(({ isClicked }) =&gt; ({ isClicked: !isClicked }));
  });
};</code></pre>
<ul>
<li>이러한 문제 때문에 18버전으로 업데이트를 못하고 있다면, 위에서 언급한 <code>ReactDOM.flushSync</code>를 사용하여 업데이트를 강제할 수 있긴 하다.
➡️ 하지만 <strong>사용을 지양하는 것</strong>을 추천한다고 한다.</li>
</ul>
<pre><code class="language-js">// 18 버전
handleClick = () =&gt; {
  setTimeout(() =&gt; {
    ReactDOM.flushSync(() =&gt; {
      this.setState(({ count }) =&gt; ({ count: count + 1 }));
    });

    console.log(this.state); // { count: 1, isClicked: false }

    this.setState(({ isClicked }) =&gt; ({ isClicked: !isClicked }));
  });
};</code></pre>
<ul>
<li><p>Hooks를 가진 함수형 컴포넌트는 이러한 문제에 영향을 받지 않는다.</p>
<ul>
<li>state 변경이 기존 값을 업데이트하지 않기 때문이다!</li>
</ul>
<pre><code class="language-js">function handleClick() {
  setTimeout(() =&gt; {
    console.log(count); // 0
    setCount(c =&gt; c + 1);
    setCount(c =&gt; c + 1);
    setCount(c =&gt; c + 1);
    console.log(count); // 0
  }, 1000)</code></pre>
</li>
<li><p><code>setCount</code> 함수는 이전 상태 값을 업데이트하는 함수를 인자로 받고, 이전 상태 값을 직접 참조하여 새로운 상태 값을 계산하는 <strong>함수형 업데이트</strong>를 수행한다.</p>
<ul>
<li>하지만 이러한 상태 업데이트 함수는 비동기적으로 동작한다.</li>
<li>따라서 <code>setCount</code> 함수 호출 시 기존 상태 값이 즉시 업데이트되는 것이 아니라 이벤트 루프를 통해 대기하다가 다음 렌더링 사이클에서 업데이트 된다.</li>
<li>따라서 <code>setTimeout</code> 함수 내부의 업데이트들은 아직 렌더링 사이클에서 처리되지 않아 두 번째 콘솔에도 이전 상태 값인 '0'이 출력된다.</li>
</ul>
</li>
<li><p>위의 코드에서 <code>setTimeout</code> 함수 종료 후 업데이트 된 값을 확인하고 싶다면 위의 방식으로 콜백 함수 내에서 직접 상태 값을 참조하는 것이 아니라, <code>useEffect</code> 훅을 사용하여 값이 변경될 때마다 콘솔에 값이 찍히는 방식으로 수정해야 할 것이다.</p>
</li>
</ul>
<h2 id="🫵-unstable_batchedupdates를-사용했다면-주목">🫵 unstable_batchedUpdates를 사용했다면 주목..!</h2>
<ul>
<li>몇몇 라이브러리의 경우 이벤트 핸들러 외부에서 <code>setState</code>를 강제하기 위해 아래와 같은 문서화되지도 않은 API를 사용하기도 했다.</li>
</ul>
<blockquote>
<p><code>unstable_batchedUpdates</code></p>
</blockquote>
<ul>
<li>앞에서 언급했듯, 17버전 이하 React에서는 onClick과 같은 브라우저 이벤트에만 Batching이 있고 아래와 같은 경우에서는 사용할 수 없었다.</li>
</ul>
<pre><code class="language-javascript">import { unstable_batchedUpdates } from 'react-dom';

const batchUpdate = unstable_batchedUpdates(() =&gt; {
  setCount((prev) =&gt; (prev) + 1);
  setFlag((prev) =&gt; !(prev));
});  

batchUpdate()</code></pre>
<ul>
<li>이 함수는 내부의 모든 상태 변화를 하나의 그룹으로 묶고 한 번의 리렌더링에서 모두 적용한다.</li>
</ul>
<h3 id="📢-이제는-보내줍시다">📢 이제는 보내줍시다!</h3>
<ul>
<li>이 API는 여전히 React 18 버전에 남아있지만 Batching이 자동으로 이루어지므로 더이상 필요하지 않다.</li>
<li>공식 Github에 따르면 18 버전까지는 해당 코드를 삭제하지 않을 예정이지만, 유명 라이브러리들이 이 기능에 더이상 의존하지 않게 된 다음 번의 주요 업데이트에서는 제거할 예정이라고 하니 되도록 사용을 지양하는 것이 좋겠다.</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://github.com/reactwg/react-18/discussions/21">Automatic batching for fewer renders in React 18 #21</a></li>
<li><a href="https://react.dev/blog/2022/03/29/react-v18#new-feature-automatic-batching">React v18.0_Automatic Batching</a></li>
<li><a href="https://react.dev/learn/queueing-a-series-of-state-updates">React.dev_Queueing a Series of State Updates</a></li>
<li><a href="https://immigration9.github.io/react/2021/06/12/automatic-batching-react.html">React 18: 렌더링 최적화를 위한 자동 배칭</a></li>
<li><a href="https://velog.io/@dbwjd5864/React-18-automatic-batching%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90?ref=codenary">React 18 automatic batching에 대해 알아보자</a></li>
<li><a href="https://www.freecodecamp.org/korean/news/riaegteu-18yi-singineung-dongsiseong-rendeoring-concurrent-rendering-jadong-ilgwal-ceori-automatic-batching-deung/">리액트 18의 신기능 - 동시성 렌더링(Concurrent Rendering), 자동 일괄 처리(Automatic Batching) 등</a></li>
<li><a href="https://dev.to/devmoustafa97/do-you-know-unstablebatchedupdates-in-react-enforce-batching-state-update-5cn2">React의 불안정한_배치업데이트(unstable_batchedUpdates)를 알고 계십니까? (일괄 처리 상태 업데이트 시행)</a></li>
</ul>