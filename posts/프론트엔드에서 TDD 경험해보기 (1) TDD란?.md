<div align="center"><h3> 📝 TDD 목차 </h3>
<hr style="width: 50%;" />

<p><span style="background-color: rgba(250, 224, 56, 1);"><strong>1. TDD란?</strong></span>
2. 단위 테스트
3. 통합 테스트
4. 시각적 요소의 테스트
5. E2E 테스트</div></p>
<h2 id="📝-테스트와-tdd">📝 테스트와 TDD</h2>
<h3 id="🧐-테스트란-무엇인가">🧐 테스트란 무엇인가!</h3>
<ul>
<li>소프트웨어 관점에서의 테스트란 <strong>애플리케이션이 요구 사항에 맞게 동작하는지 검증하는 행위</strong>이다.</li>
</ul>
<h3 id="💡-테스트-유형">💡 테스트 유형</h3>
<blockquote>
<p><strong>정적 테스트</strong> (Static Test)</p>
</blockquote>
<ul>
<li>버그를 유발할 수 있는 코드를 미리 잡아줄 수 있다.</li>
<li>타입 오류, 린트 오류 체크 등이 해당한다.</li>
<li>예: TypeScript, ESLint</li>
</ul>
<blockquote>
<p><strong>단위 테스트</strong> (Unit Test)</p>
</blockquote>
<ul>
<li>프로그램의 기본 단위가 되는 모듈을 테스트하는 것을 의미한다.</li>
<li>다시 말해, 최소 단위의 util 함수, custom hook이나 하나의 컴포넌트 등 작은 단위를 전체 애플리케이션에서 떼어 내어 분리된 환경에서 테스트 한다.</li>
<li>개발한 모듈이 의도한 대로 동작하는 지에 초점을 둔다.</li>
<li>테스트 방식<ul>
<li>모듈 내의 데이터 흐름에 대한 예외 케이스를 작성하고 통과 여부를 확인한다.</li>
<li>필요 시 Mock 객체를 사용해 테스트를 진행한다.</li>
</ul>
</li>
<li>장점<ul>
<li>분리된 상태의 테스트이므로 하나의 모듈, 클래스에 대한 세밀한 테스트가 가능하다.</li>
<li>넓은 범위에서 테스트할 때보다 훨씬 빠르게 실행할 수 있다.</li>
</ul>
</li>
<li>단점<ul>
<li>의존성이 있는 모듈 제어를 위해 필연적으로 Mock(모의 객체)을 사용할 수밖에 없다.<ul>
<li>이 때 각 모듈이 실제로 잘 연결되어 상호작용하는지에 대해서는 검증할 수 없다.</li>
</ul>
</li>
<li>각 모듈의 사소한 API 변경에도 영향을 받으므로 작은 단위의 리팩터링에도 쉽게 문제가 생길 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>통합 테스트</strong> (Integration Test)</p>
</blockquote>
<ul>
<li>어플리케이션에서 여러 개의 요소를 함께 돌렸을 때의 동작을 테스트한다.</li>
<li>보통 두 개 이상의 모듈이 실제로 연결된 상태를 테스트한다.</li>
<li>단위 테스트가 끝난 모듈과 개발자가 변경할 수 없는 외부 라이브러리, DB 등의 모듈에 대해 함께 진행한다.</li>
<li>모듈 간 상호작용이 정상적으로 수행되는 지에 초점</li>
<li>장점<ul>
<li>여러 개의 모듈이 동시에 상호작용하는 것을 테스트하므로 단위 테스트에 비해 Mock의 사용이 적다.</li>
<li>모듈 간의 연결에서 발생하는 에러를 검증할 수 있다.</li>
<li>비교적 넓은 범위의 API 변경에만 영향을 받는다.<ul>
<li>단위 테스트에 비해 리팩토링 시 쉽게 깨지지 않는다.</li>
</ul>
</li>
</ul>
</li>
<li>단점<ul>
<li>단일 모듈이 복잡한 알고리즘이나 분기문을 가질 경우 단위 테스트에 비해 테스트가 어렵다.</li>
<li>테스트의 중복이 발생할 확률이 높다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>E2E 테스트</strong> (End-To-End Test)</p>
</blockquote>
<ul>
<li>사용자가 웹앱을 사용하는 것처럼 시뮬레이션한다.</li>
<li>서버, 인프라, 웹앱을 모두 테스트한다.</li>
<li>실제 사용자의 관점에서 테스트를 진행한다.<ul>
<li>내부 구조를 알고 있는 개발자의 관점에서 제품 일부분을 선택해 테스트하는 단위 테스트와 통합 테스트와는 차이가 있다.</li>
</ul>
</li>
<li>장점<ul>
<li>사용자의 실행 환경과 거의 동일한 환경에서 테스트를 진행한다.<ul>
<li>이 때문에 실제 상황에서 발생할 수 있는 에러를 사전에 발견할 수 있다.</li>
</ul>
</li>
<li>브라우저를 외부에서 직접 제어할 수 있어 JS의 API만으로는 제어할 수 없는 행위에 대한 테스트도 가능한다.<ul>
<li>예: 브라우저의 크기 변경, 실제 키보드 입력 등</li>
</ul>
</li>
<li>테스트 코드가 실제 코드 내부 구조에 영향을 받지 않는다.<ul>
<li>큰 범위의 리팩토링에도 깨지지 않으므로 자신감 있는 코드 개선이 가능해진다.</li>
</ul>
</li>
</ul>
</li>
<li>단점<ul>
<li>단위 테스트나 통합 테스트에 비해 실행 속도가 느리다.<ul>
<li>이 때문에 개발 단계에서 빠른 피드백을 받기 어렵다.</li>
</ul>
</li>
<li>세부 모듈들이 갖는 다양한 상황들의 조합을 고려해야 해서 테스트 작성이 어렵다.</li>
<li>큰 단위의 기능을 작은 기능으로 나누어 테스트할 수 없다.<ul>
<li>필연적으로 테스트 사이에 중복이 발생한다.</li>
</ul>
</li>
<li>통제된 샌드 박스 환경에서의 테스트가 아니다.<ul>
<li>테스트 실행 환경의 예상치 못한 문제들로 인해 테스트가 실패할 수 있다.</li>
<li>예: 네트워크 오류, 프로세스 대기로 인한 timeout</li>
<li>이 때문에 테스트를 완전히 신뢰하기 어려울 수 있다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>트레이드 오프 (Trade Off)</p>
</blockquote>
<ul>
<li>현실적으로 위의 모든 테스트를 완벽하게 작성하고 관리하는 것은 매우 어렵다.</li>
<li>정적 테스트에서 E2E 테스트로 올수록 테스트 비용이 증가한다.<ul>
<li>테스트를 진행하는 데 있어 실제 컴퓨팅 자원을 많이 사용한다.</li>
<li>테스트 코드 작성 및 유지보수에 더 많은 노력을 요한다.</li>
</ul>
</li>
<li>정적 테스트에서 E2E 테스트로 올수록 테스트 속도가 느려진다.<ul>
<li>E2E 테스트는 사용자의 실제 사용 흐름을 만들어야 하므로 느리다.</li>
</ul>
</li>
<li>정적 테스트에서 E2E 테스트로 올수록 신뢰도가 높아진다.<ul>
<li>단위 테스트를 많이 작성한다고 해도 합쳐졌을 때는 또 다른 결과를 낼 수 있다.</li>
<li>테스트가 사용자의 사용 방식과 유사할수록 테스트 결과에 대한 신뢰도가 높아진다.</li>
</ul>
</li>
</ul>
<pre><code>👩‍🏫 
이처럼 테스트 코드는 각 유형에 대해 트레이드 오프를 가지고 있으므로
팀의 상황에 따라 최적화된 테스트 전략을 세우기 위해 고민해야 합니다!</code></pre><h3 id="💡-좋은-테스트-코드-first">💡 좋은 테스트 코드, FIRST</h3>
<ul>
<li><strong><em>FIRST</em></strong> 란 <a href="https://www.yes24.com/Product/Goods/11681152">Clean Code</a>에서 제시한 좋은 테스트 코드 작성을 위한 원칙이다.</li>
</ul>
<blockquote>
<p><strong>F</strong>ast</p>
</blockquote>
<ul>
<li>테스트는 자주 실행시키기 부담스럽지 않을 정도로 빨라야 한다.</li>
</ul>
<blockquote>
<p><strong>I</strong>ndependent</p>
</blockquote>
<ul>
<li>각각의 테스트는 독립적이어야 한다.</li>
<li>의존성이 생길 경우 다른 테스트에도 영향을 미칠 수 있게 되기 때문이다.</li>
</ul>
<blockquote>
<p><strong>R</strong>epeatable</p>
</blockquote>
<ul>
<li>어떤 환경에서도 반복할 수 있어야 한다.</li>
<li>어떤 환경에서든 같은 결과값을 반환해야 신뢰성을 가질 수 있기 때문이다.</li>
</ul>
<blockquote>
<p><strong>S</strong>elf-Validating</p>
</blockquote>
<ul>
<li>테스트의 결과 값은 boolean 타입이어야 하고, 이 결과로 자체 검증이 가능해야 한다.</li>
<li>이를 통해 테스트 코드를 위한 불필요한 로그, 데이터 추적이 불필요해질 수 있다.</li>
</ul>
<blockquote>
<p><strong>T</strong>imely</p>
</blockquote>
<ul>
<li>테스트 코드는 적시(서비스 코드를 구현하기 전)에 작성되어야 한다.</li>
<li>TDD가 가능하려면 테스트 코드 작성이 선행되어야 하기 때문이다.</li>
</ul>
<h3 id="🧐-적절한-테스트-대상-right-bicep">🧐 적절한 테스트 대상, Right-BICEP</h3>
<ul>
<li><strong><em>Right-BICEP</em></strong> 란 무엇을 테스트해야 할지에 대한 가이드 용어이다.</li>
</ul>
<blockquote>
<p><strong>Right</strong></p>
</blockquote>
<ul>
<li>올바른 결과를 보여주는지</li>
<li>일어날 상황들에 대해서만 적절하게 테스트를 수행했는지를 의미한다.</li>
</ul>
<blockquote>
<p><strong>B</strong>oundary-conditions</p>
</blockquote>
<ul>
<li>아래의 경계 조건을 준수했는지를 의미한다.</li>
</ul>
<table>
<thead>
<tr>
<th align="center">경계 조건</th>
<th align="left">의미</th>
</tr>
</thead>
<tbody><tr>
<td align="center"><strong>C</strong>onformance</td>
<td align="left">값이 예상한 형식과 일치하는지</td>
</tr>
<tr>
<td align="center"><strong>O</strong>rdering</td>
<td align="left">값의 집합이 적절하게 정렬되거나 정렬되지 않았는지</td>
</tr>
<tr>
<td align="center"><strong>R</strong>ange</td>
<td align="left">값이 예상된 범위 내에 있는지</td>
</tr>
<tr>
<td align="center"><strong>R</strong>eference</td>
<td align="left">직접 제어할 수 없는 외부 항목을 참조하고 있진 않은지</td>
</tr>
<tr>
<td align="center"><strong>E</strong>xistance</td>
<td align="left">값이 존재하는지 (null check)</td>
</tr>
<tr>
<td align="center"><strong>C</strong>ardinality</td>
<td align="left">값이 없거나/하나이거나/엄청 많을 때의 수행을 확인했는지</td>
</tr>
<tr>
<td align="center"><strong>T</strong>ime</td>
<td align="left">모든 작업이 적시에 시간 순으로 수행되는지</td>
</tr>
</tbody></table>
<blockquote>
<p><strong>I</strong>nverse-relationships</p>
</blockquote>
<ul>
<li>역 관계 검사가 가능한지</li>
<li>테스트의 수행에 대해 역 방향으로도 검사할 수 있는지를 의미한다.<ul>
<li>예: 뺄셈 기능에 대해 반대로 더하면 다시 초기 값으로 돌아가는지</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>C</strong>ross-checking-using-other-means</p>
</blockquote>
<ul>
<li>다른 수단을 통한 교차 검증이 가능한지</li>
<li>라이브러리 또는 다른 테스트 코드를 사용해 해당 테스트 코드를 교차 검증할 수 있는지를 의미한다.</li>
</ul>
<blockquote>
<p><strong>E</strong>rror-conditions</p>
</blockquote>
<ul>
<li>오류 조건을 강제 발생시킬 수 있는지</li>
<li>테스트하려는 서비스 코드에서 발생하는 에러를 테스트 코드에서 강제로 발생시킬 수 있는지를 의미한다.</li>
</ul>
<blockquote>
<p><strong>P</strong>erformance-characteristics</p>
</blockquote>
<ul>
<li>성능 조건이 기준에 부합하는지</li>
<li>성능 측정에 대한 결과가 원하는 기준에 맞는지를 의미한다.</li>
</ul>
<h3 id="👓-프론트엔드-관점에서의-테스트-대상">👓 프론트엔드 관점에서의 테스트 대상</h3>
<blockquote>
<p>시각적 요소</p>
</blockquote>
<ul>
<li>FE 개발자는 디자이너로 전달받은 디자인을 HTML로 마크업한 뒤 CSS로 해당 컴포넌트에 스타일을 더하는 작업을 수행한다.</li>
<li>이때 디자인이 의도한 대로 잘 구현되었는지를 아래의 테스트를 통해 확인할 수 있다.</li>
<li>스냅샷 테스트<ul>
<li>HTML 구조가 의도한 대로 나타나는지를 테스트한다.</li>
<li>Jest를 통해 구현할 수 있다.</li>
</ul>
</li>
<li>시각적 회귀 테스트 (Visual Regression Test)<ul>
<li>HTML에 CSS를 덧입혀 컴포넌트가 실제로 브라우저에서 렌더링되는 모습이 의도한 모습과 같은지를 테스트한다.</li>
<li>Storybook에서 만든 <a href="https://www.chromatic.com/">Chomatic</a>을 통해 구현할 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>사용자 이벤트 처리</p>
</blockquote>
<ul>
<li>FE 개발자는 사용자의 입력 이벤트를 적절한 이벤트 핸들러로 처리한다.</li>
<li>JS API 또는 React 등에서 제공하는 테스트 유틸리티를 활용하여 이를 시뮬레이션 해볼 수 있다.<ul>
<li>Node.js에서 테스트하는 경우 React에서 권장하는 테스트 도구인 <strong>react-testing-library</strong> 패키지를 활용해 보다 효율적인 사용자 이벤트 시뮬레이션이 가능하다.</li>
</ul>
</li>
<li>또는 E2E 테스트를 통해 실제 브라우저 상에서 이벤트를 발생시켜 테스트할 수도 있다.</li>
</ul>
<blockquote>
<p>API 통신</p>
</blockquote>
<ul>
<li>FE 개발자는 브라우저 API 또는 라이브러리를 활용해 API 서버와 통신하고 애플리케이션 상태를 동기화한다.</li>
<li>아래의 방법을 통해 이렇게 구현한 API 서버와의 통신을 테스트할 수 있다.<ul>
<li>1) 실제 API 서버를 이용한다. ➡️ 주로 E2E 테스트에서 사용된다.</li>
<li>2) 테스트 API 서버를 구축하거나 API 클라이언트를 mocking한다.<ul>
<li>API 요청에 대한 응답을 원하는 대로 수정할 수 있어 다양한 상황에 대한 테스트가 가능하다.</li>
<li>Jest를 통해 모듈을 간단한 방법으로 mocking할 수 있다.</li>
<li>이 때문에 React 팀에서는 Jest를 테스트 도구로 활용할 것을 권장하고 있다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="🪆-test-double-테스트-대역">🪆 Test Double (테스트 대역)</h2>
<ul>
<li>테스트하려는 객체와 연관된 객체를 사용하기 어려울 때 대신해서 사용해줄 수 있는 객체를 의미한다.</li>
</ul>
<h3 id="💫-테스트-대역이-필요한-이유">💫 테스트 대역이 필요한 이유</h3>
<ul>
<li>테스트 대상에 의존성이 걸쳐 있어 테스트가 어려워지는 것을 막기 위해 사용한다.</li>
<li>테스트 작성 시 외부 요인이 필요한 사례<ul>
<li>테스트 대상에서 파일의 시스템을 사용할 때</li>
<li>테스트 대상이 DB로부터 데이터를 조회하거나 데이터를 추가할 때</li>
<li>테스트 대상에서 외부의 HTTP 서버와 통신할 때</li>
</ul>
</li>
<li>이처럼 외부 요인이 포함될 경우 테스트 작성이 어려워지고 테스트 결과 예측도 힘들어진다.<ul>
<li>예를 들어 연결된 API Key가 시간이 지나 만료된다면 테스트가 실패할 수 있다.</li>
<li>또한 API 서버에 일시적인 장애가 생기는 경우 테스트가 힘들어진다.</li>
</ul>
</li>
</ul>
<pre><code>👩‍🏫 이렇게 의존하는 요소로 인해 테스트가 어려워질 때 대역을 써서 테스트를 할 수 있습니다!</code></pre><ul>
<li>이처럼 테스트 대역을 사용하면 아래와 같은 상황을 피할 수 있다.<ul>
<li>로그인 테스트 시 인증 메일을 직접 메일함에서 확인한다.</li>
<li>API의 에러 상황 테스트를 위해 외부 API가 잘못된 응답을 할 때까지 기다린다.</li>
<li>테스트를 위해 필요한 연결된 작업이 완료될 떄까지 기다렸다가 함께 테스트한다.</li>
</ul>
</li>
<li>이는 대기 시간을 줄여주고, 개발 속도를 향상하는 데 도움이 된다.</li>
</ul>
<h3 id="💫-대역의-종류">💫 대역의 종류</h3>
<blockquote>
<p>Dummy</p>
</blockquote>
<ul>
<li>가장 기본적인 테스트 대역으로, 구현체만 필요하고 기능은 필요 없는 경우 사용한다.</li>
<li>일반적으로 매개 변수의 목록을 채우기 위해 사용한다.</li>
</ul>
<blockquote>
<p>Fake</p>
</blockquote>
<ul>
<li>동작은 하지만 실제 사용되는 객체처럼 정교하게 동작하지는 않는 객체를 의미한다.</li>
<li>예: 테스트 시 실제 DB를 연결해 테스트 하는 대신 Fake DB를 만들어 객체에 주입하여 실제 DB에 의존하지 않을 수 있게 하는 것</li>
<li>일반적인 production에는 적합하지 않다.</li>
</ul>
<blockquote>
<p>Stub</p>
</blockquote>
<ul>
<li><strong>상태 검증</strong> (State Verification) 사용<ul>
<li>메소드가 수행된 후 객체의 상태를 확인해 올바르게 동작했는지를 확인하는 검증법</li>
</ul>
</li>
<li>테스트 중 만들어진 호출에 대해 미리 준비된 답변을 제공한다.</li>
<li>Dummy 객체가 실제 동작하는 것처럼 보이게 만들어 놓은 객체이다.</li>
<li>보통 테스트를 위해 프로그래밍된 것 이외에는 전혀 응답하지 않는다.</li>
<li>실제 반환값이 변경될 경우 Stub 객체도 함께 수정해야 한다는 단점이 있다.</li>
<li>life cycle<pre><code>테스트 준비(setup) 
➡️ 테스트(exercise) 
➡️ 상태 검증(verify state) 
➡️ 리소스 정리(teardown)</code></pre></li>
</ul>
<blockquote>
<p>Spy</p>
</blockquote>
<ul>
<li>어떻게 호출 받았는지에 따라 일부 정보를 기록하는 stub이다.</li>
<li>테스트 대역으로 구현된 객체에 자기 자신이 호출되었을 때의 방법이나 과정처럼 추후 확인이 필요한 부분을 기록하도록 구현된 것이다.</li>
<li>함수가 실행될 때마다 그 응답값, argument 등을 기록한다.</li>
<li>특정 액션을 통해 원하는 함수가 실행되는지를 검사할 수 있다.</li>
<li>실제 객체처럼 동작시킬 수도 있고, 필요한 부분에서는 stub으로 만들어 동작을 지정하는 것도 가능하다.</li>
</ul>
<blockquote>
<p>Mock</p>
</blockquote>
<ul>
<li><strong>행위 검증</strong> (Behavior Verification) 사용<ul>
<li>메소드의 반환 값으로 판단할 수 없는 경우 특정 동작을 수행하는지를 확인하는 검증법</li>
</ul>
</li>
<li>예상되는 기대값으로 미리 프로그래밍한 객체이다.</li>
<li>호출 시 사전에 정의된 대로 결과를 반환하도록 미리 설정되어 있다.</li>
<li>테스트 작성을 위한 환경 구축이 어려울 때 테스트하고자 하는 코드와 엮인 객체들을 대체하여 사용할 수 있다.</li>
<li>예상치 못한 호출이 있을 경우 예외 값을 반환한다.<ul>
<li>이를 통해 예상된 호출이었는지를 판단할 수 있다.</li>
</ul>
</li>
<li>life cycle<pre><code>데이터 준비(setup data) 
➡️ 예상되는 결과 준비(setup expectations) 
➡️ 테스트(exercise) 
➡️ 예상 검증(verify expectations) 
➡️ 상태 검증(verify state) 
➡️ 리소스 정리(teardown)</code></pre></li>
</ul>
<h2 id="💻-tdd">💻 TDD</h2>
<h3 id="🎞️-tdd의-의미와-도입-배경">🎞️ TDD의 의미와 도입 배경</h3>
<ul>
<li>TDD (Test Driven Development)<ul>
<li>테스트 주도 개발</li>
<li>테스트를 먼저 만든 뒤 테스트를 통과하기 위한 코드를 짜는 개발 방식</li>
<li>개발 과정에서 테스트를 먼저 작성하고 이를 통과하는 코드를 구현하는 방식으로 동작 여부에 대한 피드백을 적극적으로 받는 것이다.</li>
</ul>
</li>
<li>TDD란 결정과 피드백 사이의 GAP에 대한 인식이자 GAP을 조절하기 위한 기술이다.<ul>
<li>by <a href="https://www.yes24.com/Product/Goods/12246033">테스트 주도 개발</a>의 저자 Kent Beck</li>
<li>결정<ul>
<li>프로그램 구현 시 어떠한 방식으로, 무엇을 이용해서 코드를 작성할지에 대한 것들을 정하는 것</li>
</ul>
</li>
<li>피드백<ul>
<li>코드의 성공과 실패(error!)</li>
<li>프로그램을 실행한 결과</li>
</ul>
</li>
<li>이 둘 사이의 GAP을 인식하고 있다면 TDD를 하고 있는 것이다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>TDD의 도입 배경</p>
</blockquote>
<ul>
<li>보통 테스트란 개발과 별도의 영역으로 분류되어 QA(Quality Assuarance) 과정에서 진행된다.</li>
<li>하지만 2000년대 이후 애자일 방법론과 <a href="https://itwiki.kr/w/%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%A6%BC_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D">익스트림 프로그래밍</a>에서 강조하는 TDD의 대중화로 테스트가 점점 개발 단계 중 하나로 받아들여지고 있는 추세이다.<ul>
<li>여기서의 테스트란 <strong>코드로 작성된 자동화 테스트</strong>를 의미한다.</li>
</ul>
</li>
</ul>
<h3 id="🔄️-tdd-개발-주기">🔄️ TDD 개발 주기</h3>
<img src="https://velog.velcdn.com/images/hamjw0122/post/93a69e51-92bc-4b0f-b369-a24f4489e3c5/image.png" width="50%" />

<p><a href="https://kentcdodds.com/blog/when-i-follow-tdd">이미지 출처</a></p>
<ul>
<li>TDD는 짧은 개발 주기의 반복에 의존하는 개발 프로세스이다.</li>
<li>Extreme Programming의 'Test-First' 개념에 기반을 둔 단순한 설계를 중시한다.</li>
</ul>
<blockquote>
<p>If we pull back to the minute by minute scale we see the micro-cycle that experienced TDDers follow. The Red/Green/Refactor cycle. - Robert C. Martin(Uncle Bob)</p>
</blockquote>
<p><span style="background-color: rgba(255, 137, 137, 1);"><strong>1. RED</strong></span></p>
<ul>
<li>실패하는 테스트 코드를 작성한다.</li>
</ul>
<p><span style="background-color: rgba(138, 218, 136, 1);"><strong>2. GREEN</strong></span></p>
<ul>
<li>테스트 코드를 성공시키기 위한 실제 코드를 작성한다.</li>
<li>이 과정에서는 테스트를 통과하기 위해 단순 복사하기+붙여넣기 또는 설계를 무시한 개발 등을 해도 된다.</li>
</ul>
<p><span style="background-color: rgba(166, 208, 221, 1);"><strong>3. REFACTOR</strong></span></p>
<ul>
<li>위의 과정에서 발생한 중복 코드 제거, 올바르지 못한 구조 해결, 일반화 등의 리팩토링을 수행한다.</li>
</ul>
<h4 id="⚠️-중요한-것">⚠️ <strong>중요한 것</strong></h4>
<blockquote>
<p>Write a test, make it run, make it right. To make it run, one is allowed to violate principles of good design. Making it right means to refactor it. - KentBeck</p>
</blockquote>
<ul>
<li>먼저 실패하는 테스트 코드를 작성한다.</li>
<li>컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 테스트 코드를 작성한다.</li>
<li>현재 실패하는 테스트 코드를 통과한 코드만 실제 코드에 작성한다.</li>
</ul>
<pre><code>👩‍🏫 우리는 이를 통해 실제 코드에 대해 기대하는 바를 명확하게 정의하여 
불필요한 설계 대신 정확한 요구 사항에 집중할 수 있습니다.</code></pre><h3 id="🙄-일반-개발-과정과의-비교">🙄 일반 개발 과정과의 비교</h3>
<img src="https://velog.velcdn.com/images/hamjw0122/post/150d4c89-52d1-4d84-b7dd-0487c7179807/image.png" width="50%" /> 

<ul>
<li>아래와 같은 형태의 개발 주기를 갖는다.<pre><code>1️⃣ 요구 사항 분석
2️⃣ 설계
3️⃣ 개발
4️⃣ 테스트
5️⃣ 배포</code></pre></li>
<li>프로젝트의 초기 설계가 무조건 완벽할 수는 없다.<ul>
<li>이 때문에 요구 사항, 오류 등 다양한 조건에 의한 재설계를 거쳐 프로그램은 완벽한 설계로 개선되는 것이다.</li>
<li>그리고 이러한 과정에서 불필요한 코드가 남거나 중복 처리를 하게 될 수 있다.</li>
</ul>
</li>
</ul>
<pre><code>👩‍🏫 결론적으로 이러한 코드들은 재사용이 어렵고, 유지보수하기도 힘듭니다.</code></pre><ul>
<li>작은 기능을 수정하더라도 모든 부분을 테스트해야 하므로 <strong>전체적인 버그 검출</strong>이 어렵다.<ul>
<li>따라서 자체 버그 검출 능력이 저하된다.</li>
<li>이는 곧 잘못된 코드까지 고치지 못하여 소스코드의 품질이 저하되는 결과를 야기할 수 있다.</li>
<li>또한 작은 수정에도 모든 기능을 다시 테스트해야 하므로 자체 테스트 비용도 증가한다.</li>
</ul>
</li>
</ul>
<img src="https://velog.velcdn.com/images/hamjw0122/post/79b32826-9df4-4c88-afe8-9577527ec17f/image.png" width="50%" /> 

<ul>
<li>TDD는 테스트 코드를 작성한 뒤 실제 코드를 작성한다.<ul>
<li>따라서 설계 단계에서 프로그래밍의 목적을 미리 정의해야 한다.</li>
<li>또한 무엇을 테스트해야 하는지도 미리 고민해 결정해야 한다. (테스트 케이스 작성)</li>
</ul>
</li>
<li>이렇게 테스트 코드를 작성하는 과정에서 발생하는 버그 등의 예외 사항은 테스트 케이스에 추가한 뒤 설계를 개선한다.</li>
<li>이후 테스트가 통과된 코드만을 코드 개발 단계에서 실제 코드로 사용한다.</li>
</ul>
<pre><code>👩‍🏫 이러한 단계가 반복적으로 진행되며 코드의 버그는 자연스럽게 줄고, 소스코드는 간결해집니다.
또한 테스트 케이스 작성을 통한 설계 개선으로 재설계 시간이 단축됩니다.</code></pre><h3 id="🟢-tdd의-장점">🟢 TDD의 장점</h3>
<blockquote>
<p>객체 지향적인 코드 구현</p>
</blockquote>
<ul>
<li>TDD로 개발 시 기능 별로 모듈화가 철저하게 이루어진다.<ul>
<li>TDD는 코드의 재사용을 보장하기 때문이다.</li>
</ul>
</li>
<li>이를 통해 종속성과 의존성이 낮은 모듈로 조합된 개발이 가능해진다.<ul>
<li>필요에 따라 추후 모듈을 추가하거나 제거하더라도 소프트웨어 전체 구조에 영향을 미치지 않는다.</li>
</ul>
</li>
<li>테스트 친화적인 코드를 작성하다보면 결국 좋은 코드를 설계할 수 있다.<ul>
<li>테스트하기 좋은 코드인 <strong>계산</strong> 형태의 코드를 작성하려고 하다 보면 값의 불변성이 보장되는 코드를 작성할 수 있다.</li>
<li>간략한 테스트 코드를 위해서는 구현하고자 하는 코드가 단순해져야 하므로 단일 책임 원칙(SRP)이 지켜진 코드를 작성할 수 있다.</li>
<li>테스트할 기능들이 서로에게 의존하지 않도록 하다보면 각각의 기능을 독립적으로 작성할 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>재설계 시간 단축</p>
</blockquote>
<ul>
<li>테스트 코드를 먼저 작성하므로 무엇을 해야 하는지 분명히 정의한 후 개발에 착수할 수 있다.</li>
<li>테스트 시나리오를 작성하며 예외 사항에 대해 고민해볼 수 있다.<ul>
<li>이를 통해 개발 중 소프트웨어의 전반적인 설계가 변경되지 않도록 예방할 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>디버깅 시간 단축</p>
</blockquote>
<ul>
<li>TDD의 경우 자동화된 유닛 테스트를 전제하므로 특정한 버그를 쉽게 찾아낼 수 있다.<ul>
<li>TDD가 아니라면 사용자의 데이터가 잘못 되었을 때 DB, 비즈니스 레이어, UI 중 문제가 있는 부분을 찾기 위해 모든 레이어에 대한 디버깅을 진행해야 한다.</li>
</ul>
</li>
<li>이는 특히 <strong>유닛 테스트</strong>의 이점에 해당한다.</li>
</ul>
<blockquote>
<p>추가 구현 시 용이함</p>
</blockquote>
<ul>
<li>TDD의 경우 자동화된 유닛 테스트를 전제하므로 테스트 시간을 획기적으로 단축할 수 있다.<ul>
<li>해당 기능이 기존 코드에 어떤 영향을 미칠 지 불안해하지 않아도 된다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>더 좋은 문서화 가능</p>
</blockquote>
<ul>
<li>잘 짜인 테스트 코드는 그 자체로 문서가 된다.</li>
<li>시스템이 어떻게 동작해야 하는지에 대한 문서를 자동으로, 최신 상태로 작성할 수 있다.</li>
</ul>
<blockquote>
<p>팀 내 커뮤니케이션 촉진</p>
</blockquote>
<ul>
<li>팀원들이 작성 중인 코드를 같은 시야에서 바라볼 수 있게 도와준다.</li>
<li>잘못된 의사소통으로 인한 오해나 오류를 예방할 수 있다.</li>
</ul>
<h3 id="🔴-tdd의-단점">🔴 TDD의 단점</h3>
<blockquote>
<p>생산성 저하</p>
</blockquote>
<ul>
<li>비즈니스 로직이 라이브러리에 의존할 경우 테스팅 방법이 일관적이지 않을 수 있다.</li>
<li>테스트 코드에 익숙하지 않으면 기능 구현보다도 시간을 오래 소요하게 될 수 있다.</li>
</ul>
<blockquote>
<p>러닝 커브</p>
</blockquote>
<ul>
<li>테스트 코드를 작성하고 TDD 개발 주기를 적용함에 있어 적응 기간이 필요하다.</li>
</ul>
<h3 id="🫠-tdd를-적절히-활용하기">🫠 TDD를 적절히 활용하기</h3>
<ul>
<li>TDD와 관련된 다양한 기술 활용하기<ul>
<li>적절한 Mock 프레임워크를 통해 자동화가 가능한 부분을 분리하여 활용해야 한다.</li>
</ul>
</li>
<li>TDD 개발 주기 속 'Refactor' 단계에서 다양한 리팩토링 기법 적용하기<ul>
<li>TDD는 이처럼 개별적이고 구체적인 예시로부터 리팩토링을 통해 코드를 일반화하며 완성된다고 볼 수 있다.</li>
</ul>
</li>
<li>다른 개발 프로세스의 활용 고려하기<ul>
<li>BDD(Behavior Driven Development)<ul>
<li>행위 주도 개발</li>
<li>개발자 관점에서의 기능의 동작에 중점을 둔다.</li>
<li>아직 존재하지 않는 코드에 대해 테스트를 작성하는 대신 비기술적 언어를 사용해 행위에 대한 명세를 작성한다.</li>
<li>구체적인 테스트 코드 작성 전 구조화되고 특화된 공통 언어를 통해 요구 사항을 시나리오 형태로 정의해 관리하는 개발 프로세스</li>
</ul>
</li>
<li>ATDD(Acceptance Test Driven Development)<ul>
<li>인수 테스트 주도 개발</li>
<li>인수 테스트: 사용자 입장에서 요구 사항을 충족하는지 검증하는 테스트</li>
<li>사용자 시나리오 관점에서 요구 사항을 정확히 캡쳐하는지에 중점을 둔다.</li>
<li>코드 구현 전 사용자, 테스터, 개발자가 Acceptance Criteria를 정의하고 이를 기반으로 모든 프로젝트 구성원이 수행할 작업과 요구 사항을 이해한다.</li>
</ul>
</li>
</ul>
</li>
<li>테스트의 기회비용 고려하기
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/3674d2ae-c519-455f-bb12-c14f6c9ca4d8/image.png" /><ul>
<li>TDD의 창시자인 Kent Back도 테스트에 대한 <a href="https://stackoverflow.com/questions/153234/how-deep-are-your-unit-tests/">StackOverflow의 질문</a>에 대해 위와 같이 대답하였다.</li>
<li>테스트 코드를 작성하고 유지 보수하는 데에는 비용이 들기 때문에 투입된 비용에 비해 얻을 수 있는 효과가 적다면 수동으로 테스트하는 것이 낫다.</li>
<li>테스트 coverage를 억지로 100%로 맞추려 한다거나, 중요한 로직이 없는 단순한 코드까지 테스트하려고 하고 있진 않은지 고민해보아야 한다.</li>
<li>또한 이미 작성되어 있는 코드 중에서도 불필요한 부분은 제거해주는 것이 유지 보수 비용 측면에서도 더 좋다.</li>
</ul>
</li>
</ul>
<h2 id="🗂️-테스트에-사용되는-용어들">🗂️ 테스트에 사용되는 용어들</h2>
<blockquote>
<p>Instrumentation</p>
</blockquote>
<ul>
<li>테스트 코드가 커버하는 범위를 계산할 때 전체 코드베이스에서 몇 줄이, 각 라인에서 몇 번 실행되는지 측정하기 위해 모든 파일을 감싸는 과정을 말한다.</li>
<li>보통 <a href="https://github.com/istanbuljs/babel-plugin-istanbul">istanbul</a>이라는 라이브러리를 사용해 babel 설정에서 수행한다.<ul>
<li>⚠️ production 환경에서 절대 사용하지 않도록 주의하자!</li>
</ul>
</li>
</ul>
<blockquote>
<p>Snapshot Test</p>
</blockquote>
<ul>
<li>특정 컴포넌트가 렌더링 시 어떤 아웃풋이 나오는지 파일로 기록한다.</li>
<li>코드 수정 후 렌더링 되는 결과물이 변경될 경우 테스트는 실패한다.<ul>
<li>로직만 수정했다고 생각했지만 DOM까지 건드리는 상황을 예방할 수 있다.</li>
</ul>
</li>
</ul>
<h3 id="💡-js-테스트-도구와-그-기능들">💡 JS 테스트 도구와 그 기능들</h3>
<ul>
<li>대표적인 테스팅 라이브러리는 아래와 같다.<ul>
<li><a href="https://jestjs.io/">jest</a></li>
<li><a href="https://mochajs.org/">mocha</a></li>
<li><a href="https://karma-runner.github.io/1.0/index.html">karma</a></li>
<li><a href="https://jasmine.github.io/">jasmine</a></li>
</ul>
</li>
<li>위의 테스팅 라이브러리들은 테스트를 위한 다양한 기능을 통합하여 제공하고 있다.<ul>
<li>이 중 무엇을 사용할지 선택하기 위해서는 제공되는 기능들이 무엇인지 아는 것이 필요하다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>테스트 러너</p>
</blockquote>
<ul>
<li>이전에는 JS를 브라우저에 한정하여 실행할 수 있었다.<ul>
<li>이때는 작성된 테스트 코드를 직접 브라우저에서 실행한 뒤 웹페이지나 브라우저 콘솔을 통해서 결과를 확인해야 했다.</li>
</ul>
</li>
<li>하지만 Node.js의 등장으로 브라우저 없이도 JS 코드를 손쉽게 실행할 수 있게 되었다.<ul>
<li>이 덕분에 <strong>테스트 러너</strong> 도구를 통해 이러한 과정을 자동화할 수 있다.</li>
</ul>
</li>
<li>제공하는 기능<ul>
<li>테스트 파일을 읽어들여 작성한 코드를 실행하고, 실행 결과를 특정 형식으로 출력한다.</li>
<li>Reporter을 지정해 수행 결과를 원하는 형태로 출력할 수 있다.</li>
<li>Watcher를 통해 테스트 코드나 소스 코드 변경 시 영향을 받는 테스트를 자동 재실행해줄 수도 있다 (부가적).</li>
</ul>
</li>
<li>지원하는 라이브러리<ul>
<li>브라우저 기반: Karma</li>
<li>Node.js 기반: Jest<ul>
<li>러너의 실행 환경과 코드의 실행 환경을 구분할 필요가 없으므로 대부분 테스트 프레임워크와 통합된 형태로 제공된다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>테스트 프레임워크</p>
</blockquote>
<ul>
<li>사용자가 테스트 코드를 작성할 수 있는 기반을 제공해준다.</li>
<li>프레임워크가 제공하는 함수를 사용해 테스트코드를 작성하면 프레임워크가 테스트코드를 자동으로 실행한 뒤 성공/실패에 대한 결과를 반환한다.</li>
<li>지원하는 라이브러리: Mocha, Jasmin, AVA, Jest</li>
</ul>
<blockquote>
<p>단언 라이브러리</p>
</blockquote>
<ul>
<li>테스트 코드는 주로 '테스트를 위한 초기화'와 '단언'으로 이루어진다.</li>
<li>단언(Assertion) <ul>
<li>원하는 결과를 받고 있는지 확인하기 위한 기능이다.</li>
<li>개별 테스트가 통과하기 위한 조건을 명확하게 기술하기 위해 사용된다.</li>
</ul>
</li>
<li>보통 테스트 프레임워크에서 다양한 방식의 단언 API를 기본 제공한다. (Mocha 제외)</li>
<li>초기의 단언 라이브러리들은 JUnit과 유사한 방식의 API를 많이 따랐다.<ul>
<li>JUnit: Java에서 독립된 단위테스트를 지원해주는 프레임워크</li>
</ul>
</li>
<li>최근 가장 많이 사용되는 Chai, Jasmine 등에서는 조금 더 자연어에 가까운 BDD 방식의 API가 사용된다.</li>
<li>대부분의 단언 라이브러리들은 사용자들이 필요에 따라 스스로 단언을 추가하여 사용할 수 있는 플러그인 확장 기능을 제공한다.</li>
</ul>
<blockquote>
<p>테스트 대역(더블) 라이브러리</p>
</blockquote>
<ul>
<li>위에서 설명한 테스트 대역을 더 쉽게 만들 수 있도록 도와주는 라이브러리를 의미한다.</li>
<li>대부분 단언과 마찬가지로 테스트 더블을 위한 함수들도 테스트 프레임워크에서 기본 제공된다. (Mocha 제외)</li>
<li>일반적으로 JS 객체 혹은 함수를 직접 변경하거나 생성하는 형태로 사용된다.<ul>
<li>Jest에서는 모듈 단위로 사용할 수 있는 기능도 제공한다.</li>
<li><a href="https://github.com/ctimmerm/axios-mock-adapter">Axios-mock-adapter</a>와 같이 별도로 구현된 Mock 라이브러리도 존재하므로 관련된 라이브러리를 먼저 찾아보는 것도 좋다.</li>
</ul>
</li>
</ul>
<h3 id="💡-컴포넌트-렌더링-라이브러리">💡 컴포넌트 렌더링 라이브러리</h3>
<ul>
<li>제공하는 기능<ul>
<li>컴포넌트를 렌더링한다.</li>
<li>렌더링된 컴포넌트에서 원하는 element를 찾을 수 있는 selector 기능을 제공한다.</li>
<li>element에서 onClick과 같은 다양한 이벤트를 호출할 수 있게 해준다.</li>
</ul>
</li>
<li>사용 가능한 라이브러리: <a href="https://testing-library.com/">@Testing Library</a>, <a href="https://enzymejs.github.io/enzyme/">enzyme</a>, <a href="https://www.npmjs.com/package/react-test-renderer">react-test-renderer</a>, <a href="https://test-utils.vuejs.org/">@vue/test-utils</a></li>
<li>Testing Library의 경우 <a href="https://testing-library.com/docs/react-testing-library/intro/">React</a> 외의 다른 프레임워크도 지원한다.</li>
</ul>
<h2 id="📝-테스트-실행-환경">📝 테스트 실행 환경</h2>
<ul>
<li>JS의 테스트는 브라우저와 Node.js 환경에서 모두 실행할 수 있다.</li>
<li>두 환경 모두 뚜렷한 장단점을 가지므로 상황에 맞게 적절한 테스트 러너를 선택해야 한다.</li>
</ul>
<h3 id="✨-브라우저">✨ 브라우저</h3>
<ul>
<li>실제 브라우저를 실행해서 테스트 코드를 실행하는 방식</li>
<li>현재는 Karma를 사용하는 것이 유일한 방법이다. (E2E 테스트 도구 제외)<ul>
<li>Karma는 테스트 러너 역할만 지원하므로 Jasmine과 같은 별도의 테스트 프레임워크가 필요하다.</li>
</ul>
</li>
<li>구동 방식<pre><code>0️⃣ command line에서 Karma를 실행한다.
1️⃣ Karma는 자체 웹서버를 구동한 후 테스트 실행을 위한 HTML 페이지를 만든다.
2️⃣ 작성된 테스트 코드 및 소스 코드 전부를 만들어진 페이지에 로드한다.
3️⃣ 브라우저를 직접 실행해서 해당 웹 페이지에 접속하면 로드된 코드가 실행된다.
4️⃣ 테스트의 실행 결과를 브라우저 콘솔에 출력한다.
5️⃣ Karma는 이 정보를 받아와 지정된 리포터를 통해 결과를 정리한 뒤 command line에 보여준다.</code></pre></li>
</ul>
<blockquote>
<p>장점</p>
</blockquote>
<ul>
<li>실제 브라우저 환경에서 테스트하므로 브라우저의 모든 기능을 활용해 테스트할 수 있다.</li>
<li><a href="https://www.selenium.dev/">Selenium</a> 등을 사용해 동일한 테스트 코드를 다양한 환경(운영체제, 브라우저)에서 실행하여 <strong>브라우저 호환성 및 기기 환경</strong>에 대한 테스트를 진행할 수 있다.<ul>
<li>Selenium: 웹 애플리케이션 자동화 및 테스트를 위한 포터블 프레임워크</li>
</ul>
</li>
</ul>
<blockquote>
<p>단점</p>
</blockquote>
<ul>
<li><p>프로세스가 Node.js의 프로세스보다 무거워 테스트의 초기 구동 속도가 더 느리다.</p>
</li>
<li><p><a href="https://karma-runner.github.io/3.0/config/browsers.html">브라우저 런처</a> 등을 추가로 설치해주어야 해서 번거롭다.</p>
<ul>
<li>브라우저라는 별도의 애플리케이션을 추가로 실행해야 하기 때문이다.</li>
</ul>
</li>
<li><p>크로스 브라우징 테스트 등을 위해 별도의 환경을 구축하고 유지보수하기 위한 코스트가 소요된다.</p>
</li>
<li><p>이를 극복하기 위해서는 개발 단계에서 헤드리스 브라우저를 통한 빠른 피드백이 가능하도록 하고, 개발 완료 혹은 배포 시에만 CI 서버와 통합해 크로스 브라우징 테스트를 하는 방식이 권장된다.</p>
<ul>
<li>CI(Continuous Integration)<ul>
<li>변경 내용을 뒤늦게 통합하는 데서 비롯되는 문제들을 방지하도록 설계된 DevOps 방식</li>
<li>모든 사람의 코드 변경 내용을 자동으로 커밋, 빌드, 테스트할 수 있다.</li>
<li>프로젝트 전체에 걸쳐 통합을 자주 해줌으로써 충돌을 최소화하고, 모든 사람의 변경 내용이 상호작용하는 방식을 확인하며 다른 기능들이 버그에 의존하기 전에 문제 해결이 가능해진다.</li>
</ul>
</li>
</ul>
</li>
<li><p><a href="https://www.browserstack.com/">Browser Stack</a> 등의 외부 서비스를 사용해 크로스 브라우징을 위한 환경 구축 없이도 Karma와 연동해 사용하는 것도 가능하다.</p>
</li>
</ul>
<h3 id="✨-nodejs">✨ node.js</h3>
<ul>
<li>Node.js 환경에서 테스트 코드를 실행하는 방식</li>
<li>최근에는 Jest와 Mocha가 가장 많이 사용된다.</li>
</ul>
<blockquote>
<p>장점</p>
</blockquote>
<ul>
<li>테스트 러너와 테스트 프레임워크가 통합되어 있어 설치 및 실행이 비교적 간단하다.</li>
<li>Node.js의 프로세스가 브라우저의 프로세스에 비해 훨씬 가벼우므로 실행 속도가 <strong>빠르다</strong>.</li>
<li>모듈 단위의 테스트 실행이 어려워 webpack 등의 번들러가 필요한 브라우저와 달리 개별 프로세스에서 <strong>원하는 모듈만 import</strong>해서 테스트할 수 있다.<ul>
<li>훨씬 간단하고 안전한 방식으로 테스트할 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>단점</p>
</blockquote>
<ul>
<li>브라우저의 모든 API를 제대로 활용할 수 없다.<ul>
<li>Node.js에는 브라우저에서 제공하는 DOM이나 BOM 등의 API가 없다.</li>
<li>렌더링 엔진이 없어 UI 요소의 레이아웃에 대한 테스트가 불가능하다.</li>
<li>네비게이션 관련 동작을 사용할 수 없다.</li>
</ul>
</li>
<li><a href="https://github.com/jsdom/jsdom">jsdom</a> 등의 라이브러리를 통해 브라우저 환경을 가상으로 구현할 수 있지만 실제 브라우저의 동작을 완전히 구현하지는 못한다.</li>
<li>크로스 브라우징 관련 테스트가 불가능하다.</li>
</ul>
<h3 id="🧐-어떤-환경을-선택해야-할까">🧐 어떤 환경을 선택해야 할까?</h3>
<ul>
<li><p>브라우저 환경 사용이 꼭 필요한 경우</p>
<ul>
<li>크로스 브라우징 테스트가 <strong>반드시</strong> 필요한 경우</li>
<li>브라우저의 실제 동작에 대한 테스트가 필요한 경우 (렌더링, 네트워크 IO, 네비게이션, ...)</li>
</ul>
</li>
<li><p>최근 들어 크로스 브라우징 테스트의 필요성이 많이 감소했다.</p>
<ul>
<li>최신 브라우저들 간 표준 명세 구현에 대한 차이가 거의 없어졌다.</li>
<li>최신 JS 문법에 대한 호환성 지원은 트랜스파일러 도구(babel 등)가 대신해준다.</li>
<li>DOM을 직접 조작하는 것도 프레임워크(React, Vue, ...)가 대신 해주는 경우가 많다.
➡️ 프로젝트가 지원해야하는 브라우저 범위, 사용하는 도구 등을 고려하여 필요성을 검토해볼 필요가 있다.</li>
</ul>
</li>
<li><p>TDD 관련 포스팅에서는 Jest를 사용하므로 Node.js 기반 환경에서의 테스팅을 진행할 예정이다.</p>
</li>
</ul>
<h2 id="🤖-tdd-in-react">🤖 TDD in React</h2>
<h3 id="🤠-cra에는-tdd를-위한-기본-내장-기능이-존재합니다">🤠 CRA에는 TDD를 위한 기본 내장 기능이 존재합니다!</h3>
<p>CRA를 통해 React 프로젝트를 구상하면 Jest와 React Testing Library가 기본 내장되어 있으므로, 별도의 설치가 필요하지 않다.</p>
<pre><code>🤔 둘 다 써야 하나요?
👩‍🏫 그렇습니다!</code></pre><h3 id="👢-jest">👢 Jest</h3>
<ul>
<li>페이스북에서 만든 오픈소스 테스트 프레임워크로 개발자가 JS와 TS 코드에 대한 테스트를 실행할 수 있게 해준다.</li>
<li>최근 안정성 및 성능이 눈에 띄게 좋아지며 FE 개발에서 가장 활발하게 사용되는 테스트 도구이다.</li>
<li>테스트 케이스 등을 작성할 수 있는 기능을 제공하며 테스트를 찾아서 실행하고 테스트가 통과하는지 검사한다.</li>
</ul>
<blockquote>
<p><strong><em>Jest의 파일 이름 규칙</em></strong></p>
</blockquote>
<ol>
<li><strong><strong>test</strong></strong> 폴더에 .js 접미사가 있는 파일</li>
<li><strong>.test.js</strong> 접미사가 있는 파일</li>
<li><strong>.spec.js</strong> 접미사가 있는 파일</li>
</ol>
<ul>
<li>Jest는 위의 파일들을 src 폴더 하위의 모든 depth에서 찾을 수 있다.</li>
<li>CRA 공식 페이지에서는 <strong>.test</strong> 파일을 테스트 중인 코드 옆에 배치할 것을 추천한다.<ul>
<li>같은 수준(동일한 경로)에 파일이 위치해 가져올 때 코드가 짧기 때문이다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>Jest의 장점</p>
</blockquote>
<p><strong>1. <u>설치와 실행이 쉽다.</u></strong></p>
<ul>
<li>테스트 러너의 기능 뿐 아니라 단언, 테스트 더블, 코드 커버리지 등 테스트에 필요한 모든 기능을 지원하므로 별도의 추가 설치가 필요하지 않다.</li>
</ul>
<p><strong>2. <u>jsdom을 내장하고 있다.</u></strong></p>
<ul>
<li>이를 통해 테스트를 실행할 때마다 필요한 환경들을 자동으로 설정해 제공한다.</li>
<li>별다른 추가 작업 없이 브라우저 환경인 것처럼 테스트 작성이 가능하다.</li>
</ul>
<p><strong>3. <u>스냅샷 테스트를 지원한다.</u></strong></p>
<p><strong>4. <u>테스트 파일 필터링 기능을 지원한다.</u></strong></p>
<ul>
<li>테스트 대상 파일을 구체적으로 지정할 수 있다.</li>
<li>Jest는 버전 관리 도구(Git 등)와 연동해 마지막 커밋 이후 변경 사항이 있는 파일만 테스트 대상에 포함한다.</li>
<li>이미 검증된 파일에 대한 불필요한 테스트를 막을 수 있다.</li>
<li>한 번 실행한 이후 추가 명령이 불가능한 보통의 러너들과 달리 Jest는 <span style="background-color: rgba(250, 224, 56, 1);"><strong>인터렉티브한 command line 인터페이스</strong></span>를 제공(이미지 참조)한다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/c9268c72-563f-4310-9c98-057d54995b3f/image.png" /></li>
<li>이를 통해 실행 이후에도 키 입력을 통해 테스트 대상 파일을 변경할 수 있다.<ul>
<li><strong>a</strong>를 통해 전체 파일 테스트, <strong>q</strong>를 통해 현재 진행 중인 테스트 취소, <strong>p</strong>를 통해 특정 파일명으로 필터링 등의 명령이 가능하다.</li>
</ul>
</li>
<li>또한 스냅샷 테스트 실패 시 결과 확인 후 바로 스냅샷을 갱신하도록 하는 것도 가능하다. </li>
</ul>
<p><strong>5. <u>샌드박스 병렬 테스트가 가능하다.</u></strong></p>
<ul>
<li>Node.js 환경에서의 테스트는 빠르다.<ul>
<li>Node.js 환경에서 테스트를 하는 것의 가장 큰 메리트는 브라우저의 프로세스보다 가벼운 프로세스 덕분에 초기 구동 속도가 빠르다는 것이다.</li>
</ul>
</li>
<li>Jest는 이러한 장점을 이용해 각각의 테스트 파일을 독립된 프로세스에서 실행한다.<ul>
<li>각각의 테스트가 사용하는 전역 객체나 모듈의 상태가 서로에게 영향을 미치지 않아 마치 샌드박스 내부에 있는 것처럼 안전한 테스트가 가능하다.</li>
<li>샌드박스<ul>
<li>아이를 모래밭 밖에서 놀게 하지 않는다는 말에서 유래했다.</li>
<li>애플리케이션 실행을 위해 엄격히 제어된 환경을 말한다.</li>
<li>외부 요인에 의해 문제가 발생하지 않도록 다른 파일이나 프로세스로부터 격리된 보호된 영역 내에서 프로그램을 동작시킨다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<pre><code>🤔 
테스트를 순차적으로 실행하면서 개별 테스트마다 별도의 자식 프로세스를 생성하게 되면
단일 프로세스에서 실행하는 것보다 오히려 느려지진 않나요?</code></pre><ul>
<li>Jest는 <span style="background-color: rgba(250, 224, 56, 1);"><strong>다수의 프로세스를 병렬로 실행</strong></span>하는 방식을 사용하여 속도를 향상시킨다.</li>
<li>또한 내부적으로 CPU 코어 수 등을 고려해 동시에 실행되는 프로세스의 개수를 적절하게 조절한다.</li>
<li>그리고 앞의 테스트 파일 필터링 기능을 통해 불필요한 테스트 실행을 방지할 수 있다.</li>
</ul>
<pre><code>👩‍🏫 
Jest는 이러한 방식을 사용해 테스트 실행을 최적화된 속도로 유지하면서도 
훨씬 더 안전한 테스트 환경을 제공합니다!</code></pre><h3 id="🐙-react-testing-library">🐙 React Testing Library</h3>
<blockquote>
<p>Testing Library</p>
</blockquote>
<ul>
<li>UI를 사용자 관점에서 테스트할 수 있도록 도와주는 라이브러리이다.</li>
<li>2018년에 처음 등장했으나 JS 생태계 설문 조사 행사인 <strong><em>State of JS</em></strong>에서 여러 테스트 라이브러리를 제치고 1위를 차지할 정도로 FE 테스트 환경에 큰 역할을 하고 있다.</li>
</ul>
<img src="https://velog.velcdn.com/images/hamjw0122/post/d116c8ac-c2c0-4e25-a5f0-16599b3cbb00/image.png" width="50%" />

<p><a href="https://2020.stateofjs.com/ko-KR/technologies/testing/">이미지 출처</a></p>
<ul>
<li>기존의 FE 테스트는 컴포넌트의 내부 상태 변경과 같은 상세한 구현을 테스트한다는 문제가 있었다.<ul>
<li>이렇게 테스트할 경우 리팩토링 시 기능이 아닌 구현을 수정할 때에도 테스트를 깨지게 만들었다.</li>
<li>이는 곧 개발 속도와 생산성 저하로 이어질 수 있다.</li>
</ul>
</li>
<li>Testing Library는 사용자가 소프트웨어를 사용하는 것과 비슷하게 개발자가 테스트할 수 있게 함으로써 자신감을 주는 것을 슬로건으로 내세우고 있다.<ul>
<li>사용자가 컴포넌트 내부의 상태가 어떻게 바뀌고 내부에서 메서드가 어떻게 호출되는지 전혀 모르는 것처럼 테스트 코드 작성 시에도 이러한 부분은 테스트하지 않고, 사용자가 관심을 가지는 부분에 대해서만 테스트를 진행한다는 의미이다.</li>
<li>이를 통해 개발자는 더 자신감을 가지고 리팩토링을 진행할 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>React Testing Library</p>
</blockquote>
<ul>
<li>React Component를 테스트하기 위해 특별히 제작된 JS 테스트 유틸리티이다.</li>
<li>각각의 구성요소에 대한 사용자 상호작용을 테스트하고, UI의 올바른 작동을 확인할 수 있다.<ul>
<li>예를 들어, 버튼 클릭 이벤트 발생 시 div 존재 여부 등을 테스트하기 위한 가상 DOM을 제공한다.</li>
</ul>
</li>
</ul>
<h3 id="🏃♀️-react에서-첫-테스트-해보기">🏃‍♀️ React에서 첫 테스트 해보기</h3>
<ul>
<li>물론 테스트 코드를 너무 간단한 기능에 적용하는 것은 지양하는 것이 좋아 보이지만, 테스트를 처음 배우는 것이어서 최대한 간단한 기능을 구현해보려 하였다.</li>
<li>양쪽에 +, - 버튼이 있어 화면에 보이는 숫자를 조정하고, on/off 버튼으로 기능의 활성화 여부를 설정할 수 있다.</li>
<li>전체 코드를 넣기에는 너무 길어질 것 같아 on/off 버튼에 관련된 부분에 대해서만 작성해보고자 한다.</li>
</ul>
<blockquote>
<p>애플리케이션 생성하기</p>
</blockquote>
<ul>
<li>CRA로 프로젝트를 생성해주면 자동으로 Jest와 RTL을 사용할 수 있다.<pre><code>npx create-react-app 프로젝트명</code></pre></li>
</ul>
<blockquote>
<p>Prettier와 ESLint 적용하기</p>
</blockquote>
<ul>
<li>Prettier와 ESLint를 테스트 코드에 적용함으로써 코드 품질을 향상시키고 오류를 사전에 방지할 수 있다.</li>
</ul>
<pre><code class="language-json">// .eslintrc.json 에 아래의 내용을 설정해주어야 한다.
{
    &quot;plugins&quot;: [&quot;testing-library&quot;, &quot;jest-dom&quot;],
    &quot;extends&quot;: [
        &quot;react-app&quot;,
        &quot;plugin:testing-library/react&quot;,
        &quot;plugin:jest-dom/recommended&quot;
    ]
}
</code></pre>
<blockquote>
<p>테스트할 컴포넌트 만들기</p>
</blockquote>
<ul>
<li>on/off 관련 비즈니스 로직은 useButton이라는 커스텀 훅으로 분리해주었다.</li>
</ul>
<pre><code class="language-js">import { useState } from 'react'

const useButton = () =&gt; {
    const [disabled, setDisabled] = useState(false)
    const handleActiveMode = () =&gt; setDisabled(prev =&gt; !prev)
    // ...
    return {
        disabled,
        handleActiveMode,
      // ...
    }
}

export default useButton</code></pre>
<ul>
<li>실제 Button 컴포넌트에는 뷰 관련 코드만 남아있게 하였다.</li>
</ul>
<pre><code class="language-js">import useButton from './_hooks/useButton'

const Button = () =&gt; {
    const { disabled, handleActiveMode } =
        useButton()

    return (
        &lt;div&gt;
            ...
            &lt;div&gt;
                &lt;button
                    data-testid=&quot;onoffBtn&quot;
                    style={{ backgroundColor: 'black', color: 'white' }}
                    onClick={handleActiveMode}
                &gt;
                    {cnt}
                &lt;/button&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    )
}

export default Button
</code></pre>
<blockquote>
<p>테스트 코드 작성하기</p>
</blockquote>
<ul>
<li>버튼 컴포넌트가 구현된 파일과 같은 depth에 <strong><em>Button.test.js</em></strong> 를 작성하였다.</li>
</ul>
<pre><code class="language-js">// onoff 버튼의 스타일 테스트
test('onoff button', () =&gt; {
  // 버튼 컴포넌트를 렌더링한다.
    render(&lt;Button /&gt;)
  // 화면에서 data-testid 사용하여 해당 값을 갖는 요소를 찾는다.
    const onoffBtnElement = screen.getByTestId('onoffBtn')
  // 해당 요소가 원하는 스타일을 가지는지 확인한다.
    expect(onoffBtnElement).toHaveStyle({
        backgroundColor: 'black',
        color: 'white',
    })
})</code></pre>
<ul>
<li><a href="https://testing-library.com/docs/dom-testing-library/api-events/">Jest 공식 문서</a>에서는 <code>user-event</code>를 사용할 것을 권장하고 있다.</li>
<li>하지만 <code>fireEvent</code>와 어떤 차이가 있는지 알아두면 좋을 것 같아 간단한 코드에는 <code>fireEvent</code>를 적용해보고, 뒤의 본격적인 기능 구현 시에는 <code>user-event</code>를 적용해본 뒤 둘을 비교해보고자 한다.</li>
</ul>
<pre><code class="language-js">// onoff 버튼의 클릭 이벤트 테스트
test('handle whether the button is disabled with the onoff button click', () =&gt; {
    render(&lt;Button /&gt;)
    const onoffBtnElement = screen.getByTestId('onoffBtn')
  // fireEvent를 사용해 버튼 클릭 이벤트를 테스트한다.
    fireEvent.click(onoffBtnElement)
    const plusBtnElement = screen.getByTestId('plusBtn')
    const minusBtnElement = screen.getByTestId('minusBtn')

    // 해당 값이 비활성화 상태인지 확인한다.
    expect(plusBtnElement).toBeDisabled()
    expect(minusBtnElement).toBeDisabled()
})</code></pre>
<blockquote>
<p>실행하기</p>
</blockquote>
<ul>
<li>테스트를 실행한다.</li>
</ul>
<pre><code>npm run test</code></pre><ul>
<li><strong>a</strong>를 입력하여 전체 파일을 테스트한다.</li>
<li>아래와 같은 결과를 받을 수 있다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/6bb98e88-5dcd-4124-b4e9-398085b6aafa/image.png" /></p>
<hr />

<p>여러 TDD 관련 아티클을 읽으면서 모든 경우의 수를 떠올려 통과할 수 있도록 테스트 코드를 작성하는 것보다는 적절한 수준에서 프로젝트에 꼭 필요한 기능이 무엇인지 파악하고, 테스트에 적합한 코드를 작성하여 결함이 없도록 구현하는 것이 더 중요할 것 같다는 생각이 들었다. 모든 요소를 100% 만족시키는 테스트를 작성하는 것이란 불가능한 것 같고, 프로젝트의 특성과 상황을 고려하고 여러 환경에서의 테스트를 실행해보면서 스스로 테스트 관련 전략을 세울 수 있게 되도록 연습해봐야겠다!</p>
<pre><code>다음 포스팅부터는 직접 프로젝트에 테스트 코드를 작성해보면서
각 테스트 유형에 대해 조금 더 세부적으로 공부해볼 예정이다!</code></pre><h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://medium.com/wantedjobs/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%9D%98-%EB%AA%A8%EB%93%A0-%EA%B2%83-48912486f72d">프론트엔드 테스트의 모든 것</a></li>
<li><a href="https://ui.toast.com/fe-guide/ko_TEST">테스트 | TOAST UI</a></li>
<li><a href="https://meetup.nhncloud.com/posts/174">실용적인 프론트엔드 테스트 전략 (1)</a></li>
<li><a href="https://blog.mathpresso.com/%EB%AA%A8%EB%8D%98-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%A0%84%EB%9E%B5-1%ED%8E%B8-841e87a613b2">모던 프론트엔드 테스트 전략 — 1편(Testing Overview)</a></li>
<li><a href="https://learntdd.in/react/">Learn TDD in React</a></li>
<li><a href="https://itchallenger.tistory.com/918">[번역] React TDD 기초</a></li>
<li><a href="https://gdsc-university-of-seoul.github.io/how-to-develop-frontend-using-TDD/">프론트엔드에서 TDD로 개발하기</a></li>
<li><a href="https://shorttrack.tistory.com/9">테스트도 전략이다</a></li>
<li><a href="https://shorttrack.tistory.com/3">TDD 는 코드 설계를 위한 도구이다.</a></li>
<li><a href="https://www.cckn.dev/frontend/frontend%EC%97%90%EC%84%9C-tdd%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EA%B2%AC%EA%B3%A0%ED%95%9C-js-%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4-%EB%A7%8C%EB%93%A4%EA%B8%B0/">Frontend에서 TDD를 이용해 견고한 JS 소프트웨어 만들기</a></li>
<li><a href="https://team.modusign.co.kr/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C%EC%97%90%EC%84%9C-%EC%9D%98%EB%AF%B8%EC%9E%88%EB%8A%94-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%BD%94%EB%93%9C-%EC%9E%91%EC%84%B1%ED%95%98%EA%B8%B0-4992409c7f2d">프론트엔드에서 의미있는 테스트 코드 작성하기</a></li>
<li><a href="https://tech.madup.com/front-test-tips/">프론트엔드 테스트 팁</a></li>
<li><a href="https://blog.barogo.io/%EA%B0%9C%EB%B0%9C%EC%9D%B8%ED%84%B4-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EB%B0%A9%EC%8B%9D%EC%97%90-%EB%8C%80%ED%95%9C-%EC%A0%81%EC%A0%88%EC%84%B1-%EB%B0%8F-%EA%B3%A0%EB%AF%BC-with-tdd-6e19d3fb32bd">[개발인턴] 테스트 방식에 대한 적절성 및 고민 (with TDD)</a></li>
<li><a href="https://musma.github.io/2023/07/24/front-end-test-code.html">프론트엔드 테스트 코드를 도입하며 느낀점</a></li>
<li><a href="https://yong-nyong.tistory.com/45">[React] Jest와 React testing library를 사용해서 간단한 React app 테스트 해보기 (feat.TDD)</a></li>
<li><a href="https://www.samsungsds.com/kr/insights/test-driven-development.html?referrer=https://wooaoe.tistory.com/33">코드 품질을 높여주는 테스트 주도 개발 알아보기</a></li>
<li><a href="https://gmlwjd9405.github.io/2018/06/03/agile-tdd.html">[Agile] TDD(테스트 주도 개발)란</a></li>
<li><a href="https://wooaoe.tistory.com/33">[기술면접] TDD(Test-Driven-Development) 방법론에 대해서</a></li>
<li><a href="https://gmoon92.github.io/test/2018/08/24/test-driven-development.html">TDD : Test-Driven Development</a></li>
<li><a href="https://azderica.github.io/00-test-mock-and-stub/">[Test] Mock 테스트와 Stub 테스트 차이</a></li>
<li><a href="https://beststar-1.tistory.com/29">테스트 대역(Test Double)</a></li>
<li><a href="https://velog.io/@suhongkim98/TDD-BDD-ATDD-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0">TDD, BDD, ATDD 알아보기</a></li>
<li><a href="https://www.jetbrains.com/ko-kr/teamcity/ci-cd-guide/ci-cd-tools/servers/">CI 서버란?</a></li>
</ul>