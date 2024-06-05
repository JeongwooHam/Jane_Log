<p>리액트를 공부하면서 <code>👥 리액트의 특징이 무엇인가요?</code>라고 물어보면 <code>🙋‍♀️ 가상 DOM을 사용하여 렌더링 성능을 향상시킵니다.</code> 라고 대답해왔는데 막상 <code>👥 가상 DOM을 어떻게 사용하는데요?</code> 라는 질문을 받으면</p>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/6c0a4c3e-9ff8-4cfa-8153-67aa882998d9/image.png" /></p>
<p><code>🤔 ... 그러게요..?</code> </p>
<p>정확히 답변을 할 수 없다는 생각이 들었다. 이러한 계기로 공식문서와 아티클들을 이것저것 찾아보면서 생각보다도 훨씬 깊고 심오한 리액트의 세계를 보게 되었고 이를 정리해보고자 이번 포스팅을 작성하게 되었다.</p>
<h2 id="💡-dom이란">💡 DOM이란?</h2>
<blockquote>
<p>React 가상 DOM 관련 원문
<a href="https://www.geeksforgeeks.org/reactjs-virtual-dom/">ReactJS Virtual DOM</a></p>
</blockquote>
<ul>
<li>Document Object Model</li>
<li>웹 페이지 또는 웹 앱에 표시되는 HTML 요소들의 구조화된 표현으로, 애플리케이션의 전체 UI를 나타낸다.</li>
<li>DOM은 트리 구조로 표현되며 웹 문서의 각각의 UI가 하나의 노드가 된다.</li>
<li>웹 개발자들로 하여금 JavaScript를 통해 콘텐츠를 수정할 수 있도록 해준다. 또한 구조화된 형식으로 되어 있기 때문에 특정 대상을 선택할 수 있고 모든 코드에 대한 작업을 더욱 수월하게 할 수 있어 유용하다. </li>
</ul>
<h3 id="🚨-실제-dom의-단점">🚨 실제 DOM의 단점</h3>
<ul>
<li><p>DOM이 업데이트 될 때마다 페이지의 UI를 업데이트하기 위해 업데이트 된 요소 뿐만 아니라 그 자식 요소들까지 다시 렌더링 되어야 한다.</p>
</li>
<li><p>예를 들어 아래와 같은 코드가 있다고 가정해보자.</p>
</li>
</ul>
<pre><code class="language-js">// 간단한 getElementById() 메서드
document.getElementById('some-id').innerValue = '업데이트 된 값';</code></pre>
<ul>
<li>이 코드로 인해 아래와 같은 상황이 발생한다.<ul>
<li>브라우저는 <code>some-id</code>라는 id를 가지는 노드를 찾기 위해 HTML을 파싱한다.</li>
<li>특정 요소에서 자식 요소들을 제거한다.</li>
<li>DOM 요소를 <code>'업데이트 된 값'</code>으로 업데이트한다.</li>
<li>부모, 자식 노드에 대한 CSS를 다시 계산한다.</li>
<li>레이아웃을 업데이트한다.</li>
<li>마지막으로, 트리를 가로지르며 화면(브라우저) 디스플레이에 이를 페인트한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>파싱, 레이아웃, 페인팅 등 <strong>브라우저 렌더링</strong> 관련 용어가 궁금하다면?
<a href="https://developer.mozilla.org/ko/docs/Web/Performance/How_browsers_work">MDN 공식문서: 브라우저는 어떻게 동작하는가</a></p>
</blockquote>
<ul>
<li>CSS를 다시 계산하고 레이아웃을 변경하는 것은 복잡한 알고리즘을 수반하고 이는 성능에도 영향을 미치게 된다.</li>
<li>따라서 리액트는 이를 해결하기 위해 가상 DOM으로 알려진 새로운 접근을 시도했다.</li>
</ul>
<h2 id="💡-가상-dom이란">💡 가상 DOM이란?</h2>
<ul>
<li>Virtual DOM(VDOM): UI의 이상적인 또는 <strong>가상</strong> 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리를 통해 <strong>실제</strong> DOM과 동기화하는 프로그래밍 개념</li>
<li>원본 DOM에 존재하는 모든 객체들이 리액트 가상 DOM에도 존재한다.<ul>
<li>이 객체들은 완전히 동일하지만 문서의 레이아웃을 직접 변경할 수는 없다.</li>
</ul>
</li>
<li><strong>DOM을 조작하는 것은 느리지만 가상 DOM을 조작하는 것은 빠르다.</strong> 이는 화면에 아무것도 그려지지 않기 때문인데, 이 때문에 애플리케이션의 상태에 변화가 있으면 가상 DOM은 실제 DOM보다 먼저 업데이트 된다.</li>
</ul>
<h3 id="🧐-가상-dom은-무엇을-어떻게-빠르게-만들까">🧐 가상 DOM은 무엇을 어떻게 빠르게 만들까?</h3>
<ul>
<li>무언가 애플리케이션에 추가되면 가상 DOM이 생성되고 트리 구조로 나타내진다.<ul>
<li>각각의 요소들은 트리의 노드로 표현된다.</li>
</ul>
</li>
<li>가상 DOM 트리는 이전의 가상 DOM 트리와 비교되고, 변화를 기록한다. 그리고 나서 이것을 실제 DOM에 반영할 최적의 방법을 찾아낸다.</li>
<li>이제 업데이트 된 요소들만 페이지에 다시 렌더링 된다.</li>
</ul>
<h3 id="🧐-가상-dom은-리액트에게-어떤-식으로-도움이-될까">🧐 가상 DOM은 리액트에게 어떤 식으로 도움이 될까?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/4e01aed5-d4d9-4b18-85e2-094ebe2d5702/image.png" /></p>
<ul>
<li>리액트에서 모든 것은 컴포넌트로 취급되고, 이는 상태를 포함할 수 있다.</li>
<li>컴포넌트의 상태가 변경될 때마다 리액트는 가상 DOM 트리를 업데이트한다.<ul>
<li>가상 DOM을 업데이트하는 데는 많은 시간이 소요되지 않아 비용이 그다지 많이 들지 않고, 비효율적이지 않다.</li>
</ul>
</li>
<li>리액트는 매번 두 개의 가상 DOM을 유지하는데, 하나는 업데이트 된 가상 DOM, 다른 하나는 업데이트 이전의 가상 DOM이다. <ul>
<li>두 가상 DOM을 비교해 정확히 DOM에서 무엇이 변경되었는지를 찾아낸다.</li>
<li>아래에서 더 자세히 다루겠지만, 현재의 가상 DOM을 이전의 가상 DOM과 비교하는 이 과정을 <strong>diffing</strong>이라고 부른다.</li>
<li>리액트는 무엇이 변경되었는지를 정확하게 찾아내어 실제 DOM에서 오직 이 객체들만 업데이트한다.</li>
</ul>
</li>
<li>리액트는 실제 DOM을 업데이트하기 위해 <strong>배치 업데이트</strong>를 사용한다.<ul>
<li>이는 컴포넌트 상태에 대한 모든 변화에 대한 업데이트를 전송하는 대신 실제 DOM에 대한 변경 사항이 <a href="https://en.wikipedia.org/wiki/Batch_processing">배치</a>로 전송된다는 것을 의미한다.</li>
</ul>
</li>
<li>UI의 리렌더링은 가장 비용이 많이 드는 부분이다. <ul>
<li>따라서 리액트는 UI를 리렌더링하기 위해 실제 DOM에 배치 업데이트가 적용되는 것을 보장함으로써 이를 효율적으로 관리한다. </li>
<li>➡️ 이 과정이 바로 <strong>재조정*(Reconciliation)</strong> 이다. (아래에서 더 자세히 다룰 예정)</li>
</ul>
</li>
</ul>
<h3 id="✨-가상-dom에-대한-주요-개념">✨ 가상 DOM에 대한 주요 개념</h3>
<ul>
<li>가상 DOM은 실제 DOM을 가상으로 표현한 것이다.</li>
<li>리액트는 가상 DOM의 상태 변경을 먼저 업데이트한 후 실제 DOM과 동기화한다.</li>
<li>가상 DOM은 기계의 청사진과 같아서, 청사진을 변경하는 것은 가능하지만 이것이 직접 기계에 반영되는 것과 동일하다.</li>
<li>가상 DOM은 ReactDOM과 같은 라이브러리에 의해 &quot;실제 DOM&quot;과 동기화 된 가상의 UI 표현이 메모리에 유지되는 프로그래밍 개념으로, 이 과정을 <strong>재조정(Reconciliation)</strong> 이라고 부른다.</li>
<li>가상 DOM은 성능을 더 빠르게 만든다. 하지만 이것은 처리 자체의 시간이 짧아지기 때문은 아니고, 정보의 양이 변경되었기 때문이다. 가상 DOM을 통해 전체 페이지를 업데이트하는 데 시간을 낭비하지 않고 작은 요소와 상호작용으로 세분화할 수 있다.</li>
</ul>
<h3 id="💫-가상-dom과-실제-dom의-차이점">💫 가상 DOM과 실제 DOM의 차이점</h3>
<table>
<thead>
<tr>
<th align="left">가상 DOM</th>
<th align="left">실제 DOM</th>
</tr>
</thead>
<tbody><tr>
<td align="left">원본 DOM의 경량 복사본</td>
<td align="left">HTML 요소들을 트리 구조로 표현한 것</td>
</tr>
<tr>
<td align="left">JavaScript 라이브러리에 의해 유지관리된다.</td>
<td align="left">HTML 요소들을 파싱한 이후 브라우저에 의해 유지관리된다.</td>
</tr>
<tr>
<td align="left">조작 후 변경된 요소들만 리렌더링한다.</td>
<td align="left">조작 후 전체 DOM을 리렌더링한다.</td>
</tr>
<tr>
<td align="left">가벼운 업데이트</td>
<td align="left">무거운 업데이트</td>
</tr>
<tr>
<td align="left">빠른 성능과 최적화된 UX</td>
<td align="left">느린 성능과 품질이 떨어지는 UX</td>
</tr>
<tr>
<td align="left">배치 업데이트를 수행하여 매우 효율적이다.</td>
<td align="left">각각의 업데이트 이후 DOM을 리렌더링하여 덜 효율적이다.</td>
</tr>
</tbody></table>
<blockquote>
<p>재조정 관련 React 공식 문서
<a href="https://legacy.reactjs.org/docs/reconciliation.html">Reconciliation</a></p>
</blockquote>
<h2 id="💡-재조정reconciliation이란">💡 재조정(Reconciliation)이란?</h2>
<ul>
<li>리액트가 브라우저 DOM을 업데이트하는 과정으로, 리액트에서의 DOM 업데이트가 더 빨라지게 한다.</li>
<li>가상 DOM을 먼저 업데이트 한 뒤 diffing 알고리즘을 통해 실제 DOM에 대해 효율적이고 최적화된 업데이트를 수행한다.</li>
</ul>
<h3 id="✨-가상-dom과-재조정">✨ 가상 DOM과 재조정</h3>
<ol>
<li>리액트는 브라우저 DOM에 JSX 컴포넌트를 렌더링하지만 실제 DOM의 <strong>복사본</strong>인 <strong>가상 DOM</strong>은 자체적으로 보관한다.</li>
<li>우리가 <strong>데이터를 변경하거나 추가</strong>할 때, 리액트는 <strong>새로운 가상 DOM</strong>을 생성하고 <strong>이전</strong>의 것과 비교한다.</li>
<li>비교는 <strong>Diffing 알고리즘</strong>에 의해 수행된다. 이때 모든 비교는 <strong>메모리에서</strong> 수행되며 브라우저는 아직 아무것도 변경되지 않는다.</li>
<li>비교가 끝나면 리액트는 <strong>변경 사항이 포함된 새로운 가상 DOM</strong>을 생성한다. 이때 1초에 최대 200,000개의 가상 DOM 노드를 생성할 수 있다.</li>
<li>이후 전체 DOM을 다시 렌더링하는 것이 <strong>아니라</strong> 가능한 <strong>최소한의 변경 사항</strong>으로 <strong>브라우저 DOM을 업데이트</strong>한다. (아래 사진 참조) 이를 통해 애플리케이션의 효율성이 엄청나게 향상된다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/607a9666-543c-49a7-82f5-1d77fe46535c/image.png" /></p>
<ul>
<li><p>가상 DOM이 이전 구조와 새 구조를 비교하여 변경 사항이 없다면 브라우저에 아무것도 렌더링되지 않는다. ➡️ 이러한 방식으로 가상 DOM은 브라우저 성능 향상에 도움을 주는 것!</p>
</li>
<li><p>재조정에 관해서는 <a href="https://ko.legacy.reactjs.org/docs/reconciliation.html">리액트 공식 문서</a>에도 잘 정리되어 있으니 추가로 확인해봐도 좋을 것 같다.</p>
</li>
</ul>
<h3 id="💫-재조정-vs-렌더링">💫 재조정 vs. 렌더링</h3>
<ul>
<li>DOM은 리엑트가 렌더링할 수 있는 <strong>렌더링 환경 중 하나</strong>이다. React Native를 통한 네이티브 iOS, Android 뷰 또한 그 대상이 될 수 있다. (이것이 &quot;가상 DOM&quot;이 살작 잘못된 명칭인 이유이다.)</li>
<li>이렇게 여러 종류를 지원할 수 있는 이유는 리액트가 재조정과 렌더링을 별도의 단계로 설계했기 때문이다.<ul>
<li>리액트 Reconciler는 트리의 어떤 부분이 변경되었는지 계산하는 작업을 한다.</li>
<li>리액트 Renderer는 이후 해당 정보를 사용하여 실제로 렌더링 된 앱을 업데이트한다.</li>
</ul>
</li>
<li>이 분리는 다시 말해 리액트 DOM과 리액트 네이티브가 리액트 코어에서 제공하는 동일한 Reconciler를 사용하면서 별도로 그들만의 Renderer를 사용할 수 있다는 것을 의미한다.</li>
<li>아래에서 다루게 될 리액트 Fiber에서는 이 Reconciler를 다시 구현한다.<ul>
<li>이는 렌더링과는 원론적으로 관련이 없지만, Renderer는 새로운 아키텍쳐를 지원(및 활용)하기 위해 변경되어야 한다.</li>
</ul>
</li>
</ul>
<h2 id="💡-diffing-알고리즘이란">💡 Diffing 알고리즘이란?</h2>
<blockquote>
<p>Diffing 알고리즘 관련 원문
<a href="https://www.geeksforgeeks.org/what-is-diffing-algorithm/?source=post_page-----5faa9531175--------------------------------">What is Diffing Algorithm?</a></p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/8daabae6-0942-4088-9e46-f6d0d971e332/image.png" /></p>
<h3 id="🧐-리액트에서의-diffing-알고리즘이란">🧐 리액트에서의 Diffing 알고리즘이란?</h3>
<ul>
<li>Differences Algorithm의 줄임말</li>
<li>DOM 트리를 효율적으로 비교하여 업데이트하기 위해 사용된다.</li>
<li>리액트는 Diffing 알고리즘을 사용하여 변경이 이루어진 후 새로 생성 된 가상 DOM과 이전 버전과의 차이점을 식별한다.</li>
</ul>
<h3 id="🧐-diffing-알고리즘은-어떻게-동작할까">🧐 Diffing 알고리즘은 어떻게 동작할까?</h3>
<ol>
<li>웹페이지에 콘텐츠가 렌더링되고 DOM 트리가 생성된다.</li>
<li>사용자 상호작용 또는 API에서 전달된 데이터의 변경으로 콘텐츠에 변화가 생기면 리액트는 관측 가능한 패턴에 따라 작동한다. 따라서 상태에 변화가 생기면 가상 DOM의 노드를 업데이트한다.</li>
<li>재조정 과정에서 이전 트리는 가장 최근의 버전과 비교되고 업데이트가 필요한 변경 사항의 개수를 판별한다.</li>
<li>변경사항을 결정한 후에 실제 DOM에서 구현할 수 있도록 최적화된 최소한의 명령어 집합이 생성된다.</li>
<li>이러한 변경사항들이 구현된 후 변경된 콘텐츠들만 웹 페이지에서 리렌더링 된다.</li>
</ol>
<h3 id="🤓-diffing-알고리즘에-대한-추정">🤓 Diffing 알고리즘에 대한 추정</h3>
<ul>
<li>리액트는 아래의 가정에 기반하여 Diffing 알고리즘이라는 <strong>휴리스틱 알고리즘</strong>을 사용한다.<ul>
<li><strong>다른 타입</strong>의 요소들은 <strong>다른 트리</strong>를 생성한다.</li>
<li>우리는 어떤 요소가 정적이고 확인할 필요가 없는지 <strong>설정할 수 있다</strong>.</li>
<li><strong>너비 우선 탐색 (BFS)</strong> 이 적용된다. 이는 깊이 우선 탐색으로 접근할 경우 변경된 노드에 대해 <strong>전체 하위 트리를 리렌더링</strong> 하게 되어 최적화된 방식이 아니기 때문이다.</li>
<li><strong>동일한 타입의 두 요소</strong>를 비교할 때, <strong>기본 노드를 동일하게 유지</strong>하고 속성이나 스타일 같은 변경 사항만 업데이트한다.</li>
<li>React는 이 알고리즘을 사용하여 <strong>O(N)의 시간 복잡도</strong>로 차이 계산을 최적화한다.</li>
</ul>
</li>
<li>리액트는 루트 요소에서만 변경 사항을 확인하고, 업데이트는 루트 요소의 유형에 따라 달라진다.<ul>
<li><strong>다른 타입의 요소</strong>: 루트에서 요소의 유형이 변경될 때마다 리액트는 이전 트리를 폐기하고 새로운 트리를 빌드한다.</li>
<li><strong>동일한 타입의 요소</strong>: 변경된 요소의 타입이 같다면 리액트는 각각의 버전의 속성을 확인하고 트리의 변경 없이 변경이 있는 노드만 업데이트한다. 컴포넌트는 다음 라이프사이클 호출 시에 업데이트 된다.</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/2db5ecd8-bff9-4877-9412-4dd86ed4a10c/image.png" /></p>
<blockquote>
<p><strong>참고</strong></p>
</blockquote>
<ul>
<li>이것이 우리가 각 요소들에 <strong>고유한 키</strong>를 사용해야 하는 이유이다.</li>
<li>이를 통해 리액트는 요소의 변경 사항을 쉽게 확인할 수 있다.</li>
</ul>
<h3 id="✨-diffing-알고리즘의-장점">✨ Diffing 알고리즘의 장점</h3>
<ul>
<li>효율적인 업데이트를 가능하게 하고 변경 사항을 반영하기 위해 필요한 작업을 줄여준다.</li>
<li>필요한 컴포넌트 / 노드들만 업데이트하여 성능을 향상시킨다.</li>
<li>불필요한 리렌더링을 줄임으로써 변경 사항 발생 시 더 빠르게 대응할 수 있다.</li>
</ul>
<h2 id="💡-리액트-scheduling">💡 리액트 Scheduling</h2>
<blockquote>
<p><strong>Scheduling</strong>
: 작업을 언제 수행해야 하는지 결정하는 프로세스</p>
</blockquote>
<blockquote>
<p><strong>Work</strong>
: 수행해야 하는 모든 계산. 일반적으로 업데이트(예: <code>setState</code>)의 결과에 해당한다.</p>
</blockquote>
<h3 id="✨-stack-reconciler">✨ Stack Reconciler</h3>
<ul>
<li>JavaScript의 실행 컨텍스트는 함수가 호출되면 콜 스택에 쌓이게 된다.</li>
<li>이때 <strong>Stack Reconciler</strong>는 아래와 같은 과정을 거쳐 리렌더링을 처리한다.<ol>
<li>모든 DOM 트리 상단에서부터 재귀 형식으로 컴포넌트를 만날 때마다 <code>.render( )</code> 호출</li>
<li>트리의 변경 사항, 업데이트가 필요한 컴포넌트를 확인하고 해당 컴포넌트 자식들의 업데이트 필요 여부 확인</li>
<li>각각의 컴포넌트 업데이트</li>
</ol>
</li>
<li><code>1번</code>에서 중요한 것은 <strong>순서</strong>이다.<ul>
<li>순차적으로 만나는 컴포넌트들을 스택에 담아두고 <code>.render( )</code>을 호출한다. ➡️ <strong>Stack(FIFO)</strong></li>
</ul>
</li>
</ul>
<h3 id="🚨-stack-reconciler의-문제점">🚨 Stack Reconciler의 문제점</h3>
<ul>
<li>UI에서는 모든 업데이트를 즉시 적용하지 않아도 된다. <ul>
<li>변경사항이 발생할 때마다 업데이트를 반영하는 것은 리소스 낭비여서 프레임 드랍이 발생할 수 있고, 이는 곧 <strong>사용자 경험 저하</strong>로 이어질 수 있다.</li>
</ul>
</li>
<li>다른 타입의 업데이트는 다른 우선순위를 가진다.<ul>
<li>예를 들어 애니메이션 업데이트의 경우 데이터 저장소의 업데이트보다 더 빨리 완료되어야 한다.</li>
</ul>
</li>
<li><code>push</code> 기반 접근 방식에서는 앱(프로그래머)가 이 스케쥴이 어떻게 동작하는지를 결정해야 한다.   <ul>
<li>반면 <code>pull</code> 기반 접근의 경우 프레임워크(리액트)가 현명하게 이런 결정을 대신 해주는 것을 허용한다.</li>
</ul>
</li>
</ul>
<h3 id="🧐-프레임-드랍은-어떤-문제가-있을까">🧐 프레임 드랍은 어떤 문제가 있을까?</h3>
<ul>
<li>일반적인 모니터는 초당 60FPS 정도로 화면을 재생한다.<ul>
<li>1/60(16.67)ms 간격으로 새 프레임이 나타난다.</li>
<li>⚠️ 만약 리액트가 16ms보다 빠르게 리렌더를 하지 않으면 사용자는 <strong>버벅거리는 화면</strong>을 보게될 수 있다.</li>
</ul>
</li>
<li>단순 텍스트가 아닌 애니메이션의 경우 재조정 알고리즘의 업데이트가 있을 떄마다 리액트 내 트리를 모두 순회하고 렌더링을 하는 데 16ms 이상의 시간이 소요된다면 <strong>프레임이 드랍</strong>되고 사용자는 <strong>버벅거리는 애니메이션</strong>을 보게 된다.</li>
</ul>
<pre><code>👩‍🏫 이러한 문제를 해결하기 위해 React Fiber Reconcilation 알고리즘이 탄생했습니다! </code></pre><h2 id="💡-fiber">💡 Fiber</h2>
<blockquote>
<p>React Fiber 관련 공식 문서
<a href="https://github.com/acdlite/react-fiber-architecture?tab=readme-ov-file">React Fiber Architecture</a></p>
</blockquote>
<ul>
<li>개발자가 일반적으로 생각하는 것보다 훨씬 낮은 수준의 추상화이다.</li>
<li>리액트 팀에서 스케줄링의 이점을 취할 수 있도록 설정한 리액트 Fiber의 핵심 목표는 아래와 같다.<ol>
<li>작업을 멈춘 후 나중에 다시 돌아온다.</li>
<li>각 작업들의 타입 마다 우선순위를 부여한다.</li>
<li>이전에 완료된 작업을 다시 사용한다.</li>
<li>더이상 필요로 하지 않는 작업의 경우 중단한다.</li>
</ol>
</li>
</ul>
<h3 id="🤠-fiber는-작업의-단위입니다">🤠 Fiber는 작업의 단위입니다!</h3>
<ul>
<li>위의 목표 작업들을 수행하기 위해서는 작업을 <strong>단위로 세분화</strong>할 수 있는 방법이 필요하다.<ul>
<li>➡️ 이것이 바로 <strong><em>FIBER</em></strong>!</li>
</ul>
</li>
</ul>
<blockquote>
<p>더 자세한 이해를 위해 <strong>데이터의 함수로서의 리액트 컴포넌트</strong>의 개념을 더 자세히 알아보자.</p>
</blockquote>
<pre><code class="language-js">v = f(d)</code></pre>
<ul>
<li>리액트 앱을 렌더링하는 것은 내부에 다른 함수를 호출하는 로직을 포함하는 것과 비슷하다.</li>
<li>컴퓨터가 일반적으로 프로그램의 실행을 추적하는 방식은 <a href="https://ko.wikipedia.org/wiki/%EC%BD%9C_%EC%8A%A4%ED%83%9D"><strong>콜스택</strong></a>을 사용하는 것이다.<ul>
<li>함수가 실행되면 콜 스택에 새로운 <strong>스택 프레임</strong>이 추가된다.</li>
<li>스택 프레임: 스택 영역에 차례대로 저장되는 함수의 호출 정보. 해당 함수가 수행한 작업을 나타낸다.</li>
</ul>
</li>
<li>UI를 다룰 때 한 번에 너무 많은 작업을 실행하면 <strong>애니메이션이 버벅거릴 수 있다</strong>는 문제가 있다.<ul>
<li>또한 최신 업데이트로 인해 일부 작업이 불필요해질 수도 있다.</li>
</ul>
</li>
<li>최신 브라우저(와 React Native)는 이 문제를 해결할 때 도움이 되는 API를 구현한다.<ul>
<li><code>requestIdleCallback</code>: 쉬고 있는 기간에 낮은 우선순위의 함수가 호출되도록 예약한다.</li>
<li><code>requestAnimationFrame</code>: 다음 애니메이션 프레임에 높은 우선순위의 함수가 호출되도록 예약한다.</li>
<li>⚠️ 이러한 API를 사용하려면 렌더링 작업을 점진적 단위로 분할하는 방법이 필요하다.</li>
<li>콜 스택에만 의존할 경우 스택이 비워질 때까지 계속 작업이 수행되기 때문이다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>🤔 UI 렌더링을 최적화할 수 있게 콜 스택을 임의로 중단하고 스택 프레임을 수동으로 조작 가능하게 커스터마이징할 수 없을까?</p>
</blockquote>
<h3 id="🤠-이러한-이유로-fiber가-탄생했습니다">🤠 이러한 이유로 FIber가 탄생했습니다!</h3>
<ul>
<li>Fiber는 React16에서 스택을 재구현한 것으로 리액트 컴포넌트에 특화되어 있다.</li>
<li>하나의 Fiber를 하나의 <strong>가상 스택 프레임</strong>으로 생각하면 된다.</li>
<li>스택을 재구성하여 스택 프레임을 메모리에 보관하고 언제든 원할 때 실행하는 것이 가능해졌다.<ul>
<li>➡️ 리액트 <strong>스케줄링</strong>의 목표 달성에 용이하다.</li>
</ul>
</li>
<li>그 외에도 스택 프레임을 수동으로 처리하면 <strong>동시성</strong> 및 <strong>에러 바운더리</strong> 등을 효과적으로 처리할 수 있게 된다.</li>
</ul>
<h2 id="🛠️-fiber의-구조">🛠️ Fiber의 구조</h2>
<ul>
<li>Fiber란 컴포넌트, 입력, 출력에 대한 정보를 담고 있는 JavaScript 객체이다.</li>
<li>Fiber은 스택 프레임이자 컴포넌트의 인스턴스이다.</li>
</ul>
<h3 id="✨-fiber의-주요-필드">✨ Fiber의 주요 필드</h3>
<blockquote>
<p><code>type</code>과 <code>key</code></p>
</blockquote>
<ul>
<li>리액트 요소에서 사용될 때와 동일한 용도로 사용된다.<ul>
<li>리액트 요소에서 Fiber가 생성될 때 실제로 두 필드가 직접 복사된다.</li>
</ul>
</li>
<li><code>type</code><ul>
<li>Fiber가 해당하는 컴포넌트를 설명한다.</li>
<li><strong>복합</strong> 컴포넌트: 함수, 클래스 컴포넌트 자체</li>
<li><strong>호스트</strong> 컴포넌트 (<code>div</code>, <code>span</code> 등): 문자열 </li>
<li><code>type</code>이란 스택 프레임이 실행을 추적하는 함수(<code>v = f(d)</code>에서처럼)이다.</li>
</ul>
</li>
<li><code>key</code><ul>
<li>재조정 기간 동안 Fiber가 재사용될 수 있는지를 판단하기 위해 사용된다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><code>child</code>와 <code>sibling</code></p>
</blockquote>
<ul>
<li>다른 Fiber를 나타내며, Fiber의 재귀적 트리 구조를 설명한다.</li>
<li><code>child</code> Fiber는 컴포넌트의 <code>render( )</code> 메서드가 반환한 값에 해당한다.<pre><code class="language-js"> function Parent( ){
   return &lt;Child/&gt;
 }</code></pre>
</li>
<li><code>sibling</code>은 Fiber의 새로운 기능으로, <code>render( )</code> 메서드가 여러 자식을 반환하는 경우를 설명한다.<pre><code class="language-js"> function Parent( ){
   return [&lt;Child1/&gt;, &lt;Child2/&gt;]
 }</code></pre>
<ul>
<li>이 예제에서 <code>&lt;Child1/&gt;</code>은 <code>child</code>, <code>&lt;Child2/&gt;</code>는 <code>sibling</code>에 해당한다.</li>
<li>이는 <code>child</code> Fiber가 단일 연결 목록을 형성하기 때문이다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><code>return</code></p>
</blockquote>
<ul>
<li><code>return</code> Fiber는 프로그램이 현재 Fiber를 처리한 후 반환해야 하는 Fiber이다. 개념적으로는 스택 프레임의 주소와 동일하며, 부모 Fiber라고 생각할 수도 있다.</li>
<li>만약 Fiber이 다수의 자식 Fiber를 가지고 있다면 각각의 자식 Fiber들은 부모 Fiber를 반환할 것이다. <pre><code class="language-js"> function Parent( ){
   return [&lt;Child1/&gt;, &lt;Child2/&gt;]
 }</code></pre>
<ul>
<li>➡️ 이 예제에서 <code>&lt;Child1/&gt;</code>과 <code>&lt;Child2/&gt;</code>의 <code>return</code> Fiber는 <code>Parent</code>이다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><code>pendingProps</code>와 <code>memoizedProps</code></p>
</blockquote>
<ul>
<li>여기서 props는 개념상 함수의 인자이다. </li>
<li>Fiber의 <code>pendingProps</code>는 함수 실행 초반에 설정되고 <code>memoizedProps</code>는 끝에 설정된다.</li>
<li>들어온 <code>pendingProps</code>가 <code>memoizedProps</code>와 동일하다면 Fiber의 이전 산출물이 재사용되었음을 알려주어 불필요한 작업을 방지하게 한다.</li>
</ul>
<blockquote>
<p><code>pendingWorkPriority</code></p>
</blockquote>
<ul>
<li>Fiber가 나타내는 작업의 우선순위를 보여주는 숫자</li>
<li><code>ReactPriorityLevel</code> 모듈이 다양한 우선 순위 수준과 그들이 나타내는 내용들을 나열한다.</li>
<li>0을 의미하는 <code>NoWork</code>를 제외하면 숫자가 클수록 낮은 우선순위를 의미한다.<pre><code class="language-js">// Fiber의 우선순위가 지정된 수준보다 높은지 확인하는 함수
// ⚠️ 실제 React 코드 베이스에 포함되는 함수는 아니다!
function matchesPriority(fiber, priority) {
  return fiber.pendingWorkPriority !== 0 &amp;&amp; fiber.pendingWorkPriority &lt;= priority
}</code></pre>
</li>
<li>리액트 스케쥴러는 우선순위 필드를 통해 수행할 다음 작업 단위를 탐색한다.</li>
</ul>
<blockquote>
<p><code>alternate</code></p>
</blockquote>
<ul>
<li>컴포넌트 인스턴스는 최대 두 개의 Fiber를 가진다.<table>
<thead>
<tr>
<th align="center"><strong><em>flush</em></strong></th>
<th align="center"><strong><em>work-in-progress</em></strong></th>
</tr>
</thead>
<tbody><tr>
<td align="center">해당 출력을 화면에 렌더링한다.</td>
<td align="center">아직 완료되지 않은 Fiber <br /> (아직 반환되지 않은 스택 프레임)</td>
</tr>
</tbody></table>
</li>
<li>현재 Fiber와 <code>work-in-progress</code>는 서로 대체된다.<ul>
<li>Fiber의 대체물은 <code>cloneFiber</code> 함수를 사용해 <strong>게으르게</strong> 생성된다.</li>
<li>매번 새로운 객체를 생성하는 대신 <code>cloneFiber</code>는 대체물이 이미 존재하는 경우 이를 재사용함으로써 할당을 최소화하기 위해 노력한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><code>output</code></p>
</blockquote>
<ul>
<li><p>개념적으로 Fiber의 출력은 함수의 반환값이다.</p>
<table>
<thead>
<tr>
<th align="left"><strong><em>host component</em></strong></th>
</tr>
</thead>
<tbody><tr>
<td align="left">- 리액트 애플리케이션의 리프 노드(자식 노드가 없는 노드) <br /> - 브라우저 앱의 <code>div</code>, <code>span</code>과 같은 렌더링 환경에 특화되어 있다. <br /> - JSX에서는 소문자 태그명을 사용해 표시된다.</td>
</tr>
</tbody></table>
</li>
<li><p>모든 Fiber은 궁극적으로 출력이 있지만, 이는 <strong>host component</strong>에 의해 리프 노드에서만 생성된다.</p>
<ul>
<li>➡️ 이후 출력은 트리 위로 전송된다.</li>
</ul>
</li>
<li><p>출력은 최종적으로 렌더러에게 전달되어 렌더링 환경에서 변화를 flush할 수 있게 한다.</p>
<ul>
<li>출력이 어떻게 생성되고 업데이트되는지를 정의하는 것은 렌더러의 책임이다. </li>
<li><strong>렌더러</strong>: 리액트에서 가상 DOM을 실제 DOM으로 변환하고 업데이트를 처리해 사용자 인터페이스를 브라우저나 모바일 디바이스에 렌더링하는 모듈이나 라이브러리</li>
</ul>
</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://www.geeksforgeeks.org/reactjs-virtual-dom/">ReactJS Virtual DOM</a></li>
<li><a href="https://legacy.reactjs.org/docs/faq-internals.html">Virtual DOM and Internals</a></li>
<li><a href="https://legacy.reactjs.org/docs/reconciliation.html">Reconciliation</a></li>
<li><a href="https://www.geeksforgeeks.org/what-is-diffing-algorithm/?source=post_page-----5faa9531175--------------------------------">What is Diffing Algorithm ?</a></li>
<li><a href="https://github.com/acdlite/react-fiber-architecture?tab=readme-ov-file">React Fiber Architecture</a></li>
<li><a href="https://m.blog.naver.com/dlaxodud2388/223195103660">[React] Fiber 아키텍처의 개념과 Fiber Reconcilation 이해하기</a></li>
<li><a href="https://react.dev/reference/react/Component#reference">Component</a></li>
<li><a href="https://www.alibabacloud.com/blog/a-closer-look-at-react-fiber_598138">A Closer Look at React Fiber</a></li>
<li><a href="https://www.developerway.com/posts/react-re-renders-guide">React re-renders guide: everything, all at once</a></li>
<li><a href="https://www.zhenghao.io/posts/react-rerender">When Does React Render Your Component?</a></li>
<li><a href="https://www.joshwcomeau.com/react/why-react-re-renders/#profiling-with-the-react-devtools-5">Why React Re-Renders</a></li>
</ul>