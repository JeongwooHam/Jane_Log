<pre><code>👩‍🏫 트랜스파일러 Babel과 SWC에 대해 알아보기 전, 
트랜스파일러가 무엇인지부터 알고 갑시다!</code></pre><h2 id="🌟-트랜스파일러-알아보기">🌟 트랜스파일러 알아보기</h2>
<h3 id="👾-컴파일러">👾 컴파일러</h3>
<ul>
<li>트랜스파일러를 이해하기 위해서는 컴파일러에 대한 이해가 선행되어야 한다.</li>
</ul>
<img src="https://github.com/JeongwooHam/FE_Study_Logs/assets/123251211/8a09ce0a-7081-4068-9643-70ca0fa0007e" width="70%" />

<p><a href="https://hpc-wiki.info/hpc/Compiler">이미지 출처</a></p>
<ul>
<li>컴퓨터는 0과 1로 작성된 기계어만을 이해할 수 있음에도 불구하고, 프로그램을 작성할 때에는 JS나 Java와 같은 프로그래밍 언어를 사용한다.</li>
</ul>
<pre><code>🤔 어떻게 가능한 것인가요?</code></pre><blockquote>
<p>고급 프로그래밍 언어</p>
</blockquote>
<ul>
<li>사람이 실제로 사용하는 언어를 기준으로 하여 사람이 이해하기 쉬운 단어와 문법을 통해 프로그램을 작성하도록 설계된 대부분의 프로그래밍 언어</li>
<li>사람이 이해하기 쉬울 정도로 추상화가 고수준으로 진행되어 있기 때문에 <strong><em>고급</em></strong></li>
<li>고급 프로그래밍 언어로 작성된 코드를 컴퓨터에 바로 집어넣으면 컴퓨터는 이 코드를 이해하고 실행하지 못한다.</li>
</ul>
<blockquote>
<p>저급 프로그래밍 언어</p>
</blockquote>
<ul>
<li>컴퓨터가 이해하는 기계어와 1대 1로 대응하는 언어로, <code>어셈블리어</code>라고도 부른다.</li>
</ul>
<blockquote>
<p>컴파일러</p>
</blockquote>
<ul>
<li>프로그래밍의 영역에서 고급 프로그래밍 언어와 저급 프로그래밍 언어 간의 변환을 담당하는 도구</li>
<li>꼭 고급 ➡️ 저급이 아니더라도 한 언어로 작성된 코드를 동일한 기능을 제공하는 다른 언어의 코드로 변환해주는 역할을 제공하는 도구의 통칭이다.</li>
<li>예: 영어 ➡️ 한국어</li>
</ul>
<h3 id="🤖-트랜스파일러">🤖 트랜스파일러</h3>
<img src="https://github.com/JeongwooHam/FE_Study_Logs/assets/123251211/d4e234e3-77a1-4947-a6ef-52959fbe0146" width="70%" />

<p><a href="https://devopedia.org/transpiler">이미지 출처</a></p>
<ul>
<li>컴파일러의 하위 분류이다.</li>
<li>언어를 변환해주는 기능을 제공하는 소프트웨어라는 점에서 일반 컴파일러들과 동일하다.</li>
<li>하지만 완전히 다른 두 언어 간이 아닌 <strong>유사한</strong> 두 언어 사이의 변환을 하는 한정된 역할을 제공하는 소프트웨어라는 점에서 차이를 갖는다.</li>
<li>예: 고대 국어 ➡️ 현대 국어</li>
</ul>
<h3 id="🧐-트랜스파일러는-왜-필요한가">🧐 트랜스파일러는 왜 필요한가?</h3>
<pre><code>물론 프로젝트가 ES3와 같이 대부분 지원되는 JS 버전을 사용하는 간단한 규모라거나,
화살표 함수와 같은 JS 최신 버전 기능에 의존하지만
지원이 필요한 브라우저 또한
해당 기능을 지원하는 Chrome 최신 버전 등으로 한정되어 있는 경우에는
트랜스파일러를 굳이 필요로 하지 않는다.</code></pre><blockquote>
<p>🚨 하지만 대부분의 경우 트랜스파일러가 필요합니다!</p>
</blockquote>
<ul>
<li>브라우저는 V8(Chrome), SpiderMonkey(FireFox), Chakra(IE) 등 다양한 JS 엔진을 사용한다.</li>
<li>이는 곧 여러 브라우저들 간에 지원하는 ES 표준에 광범위한 차이가 존재할수도 있음을 의미한다.</li>
<li>FE는 빠르게 발전하고, 최신 브라우저조차 지원하지 못하는 여러 문법과 기술들이 등장한다.<ul>
<li>이 상황에서도 많은 사용자들은 예전 브라우저 OS를 사용하고 있다.</li>
</ul>
</li>
<li>이때 ESNext의 새로운 기능을 사용하면서도 브라우저마다 지원되는 기능을 동일하게 하고 일관적으로 실행되는 서비스를 구축하기 위해서 필요한 것이 바로 트랜스파일러이다.</li>
<li>트랜스파일러는 단순히 ES6나 TypeScript를 ES5로 변환하는 것에 그치지 않고 ES2019 등 다양한 JS 버전으로의 전환을 가능케 하여 하위 호환성을 보장한다.</li>
</ul>
<h2 id="babel"><a href="https://babeljs.io/">Babel</a></h2>
<img src="https://github.com/JeongwooHam/FE_Study_Logs/assets/123251211/aa5acb19-5d04-4f72-a329-1839b9353ce2" width="25%" />

<h3 id="🧐-babel이란-무엇인가">🧐 Babel이란 무엇인가?</h3>
<ul>
<li>JS 트랜스파일러</li>
<li>JS로 프로그램 작성 시 ES6 이상의 최신 문법이 일부 환경에서 작동하지 않거나, 모든 환경에서 작동하기 위해 원치 않는 ES5 이하의 방식만을 사용하게 되는 문제점을 해결할 수 있다.</li>
<li>Babel을 통해 ES6 이상의 최신 문법으로 작성한 JS 코드를 ES5 이하의 예전 문법으로 작성한 것처럼 소스 코드 내의 문법의 형태를 변경할 수 있다.<ul>
<li>이렇게 변경된 소스 코드는 최신 문법을 지원하는 환경 뿐 아니라 최신 문법이 적용되지 않은 실행 환경에서도 문제 없이 동작한다.</li>
</ul>
</li>
</ul>
<pre><code>👩‍🏫 그렇다면 Babel은 왜 트랜스파일러로 분류될까요?</code></pre><ul>
<li>위의 <code>고대 국어 ➡️ 현대 국어</code> 예시를 통해 이해했듯, Babel은 최신 JS 문법으로 작성된 코드를 구 버전 브라우저에서도 이해할 수 있는 수준의 오래된 JS 코드로 변환해주는 소프트웨어이기 때문이다.</li>
<li>Babel은 유사한 두 언어 사이에서의 변환 기능을 제공한다.</li>
<li>Babel은 단순히 ES6 문법만을 변환하는 것이 아니라 ECMAScript 2020까지의 기능들을 별도의 세팅 없이도 자체적으로 지원하고, 별도의 플러그인 사용 시 ECMAScript 2021의 기능까지도 지원하게 할 수 있다.</li>
</ul>
<h3 id="🧩-babel-polyfill">🧩 Babel-Polyfill</h3>
<blockquote>
<p>polyfill</p>
</blockquote>
<ul>
<li>개발자가 특정 기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드 조각이나 플러그인</li>
<li>브라우저에서 지원하지 않는 기능들에 대한 호환성 작업을 채워넣을 수 있게 한다.</li>
</ul>
<blockquote>
<p>Babel-Polyfill</p>
</blockquote>
<ul>
<li>Babel은 문법을 변환하여 JS로 변환하는 트랜스파일러로써의 역할만 할 뿐, Babel을 사용한다고 해서 바로 최신 함수를 사용할 수 있는 것은 아니다.</li>
<li>대신 Babel은 Polyfill 기능을 지원하여 프로그램이 처음 시작될 때 지원하지 않는 기능들을 추가할 수 있게 한다.<ul>
<li>Babel은 컴파일 시 실행되고, Babel-Polyfill은 런타임 시 실행된다.</li>
</ul>
</li>
</ul>
<h3 id="⚠️-babel의-한계점">⚠️ Babel의 한계점</h3>
<ol>
<li>Babel은 코드 변환 시 코드의 문법을 변경한다.</li>
</ol>
<ul>
<li>따라서 배포 뒤 개발자들이 Babel이 변경한 코드를 이해하기 어려울 수 있다.</li>
</ul>
<ol start="2">
<li>변환 후후 코드의 크기가 증가한다.</li>
<li>Polyfill을 통해 Babel이 지원하지 않는 범위까지 변환해주어야 한다.</li>
<li>다른 컴파일러보다 시간이 오래 걸린다.</li>
</ol>
<h2 id="swc"><a href="https://swc.rs/">SWC</a></h2>
<img src="https://github.com/JeongwooHam/FE_Study_Logs/assets/123251211/30540c81-b790-4c89-b0a5-f383129dfab2" width="25%" />

<ul>
<li>Speedy Web Compiler</li>
<li>SWC는 저급 프로그래밍 언어인 Rust로 작성된 컴파일러로, 매우 빠른 웹 컴파일러의 기능을 제공하는 빌드 툴이다.</li>
<li>프로젝트의 컴파일과 번들링 모두에 사용될 수 있다.</li>
</ul>
<h3 id="🤠-nextjs는-12버전부터-내장-컴파일러에-swc를-활용합니다">🤠 Next.js는 12버전부터 내장 컴파일러에 SWC를 활용합니다!</h3>
<ul>
<li>Next.js 12에서는 기존 빌드에 활용하던 Babel(트랜스파일링)과 Terser(코드 경량화)를 SWC를 기반으로 개발한 컴파일러로 대체하였다.</li>
</ul>
<pre><code>👩‍🏫 어떤 이유에서 Babel 대신 SWC를 사용하게 되었을까요?</code></pre><h3 id="1-빠른-빌드-타임">1. 빠른 빌드 타임</h3>
<img src="https://github.com/JeongwooHam/FE_Study_Logs/assets/123251211/0023b35f-4e01-4b4f-a23d-a9ccee84d224" width="80%" />

<ul>
<li><p>놀랍게도 SWC 공식문서에 적힌 내용이다.</p>
</li>
<li><p>SWC 기반 컴파일러로 교체하면서, 트랜스파일링이 무려 17배나 빨라졌다고 보고된다.</p>
 <img src="https://github.com/JeongwooHam/FE_Study_Logs/assets/123251211/e26e5105-a0ff-42f9-a532-8aebd37a11db" width="50%" />
</li>
<li><p>또한 Next.js 공식 블로그에서 밝힌 결과에 따르면, SWC로 구축된 새로운 컴파일러로 Next.js 프로젝트 빌드 시 빌드 타임이 최대 5배까지 빨라졌다고 한다.</p>
</li>
</ul>
<pre><code>🤔  SWC는 왜 이렇게 빠른가요?</code></pre><blockquote>
<p>Rust는 병렬 처리를 고려하여 설계된 언어</p>
</blockquote>
<ul>
<li>이유는 RUST가 이벤트 루프 기반의 싱글 스레드 언어인 JS와 달리 <code>병렬 처리를 고려해서 설계</code>된 언어이기 때문이다.</li>
<li>JS는 이벤트 루프 기반의 싱글 스레드 언어이기 때문에 하나의 작업이 끝나야 다음 작업을 시작한다.<ul>
<li>컴퓨터는 멀티 태스킹이 가능해야하고, 이는 곧 Babel이나 Terser로 프로젝트를 빌드할 때 의존성이 없는 파일들은 동시에 변환되고 있어야 함을 의미한다.</li>
<li>하지만 JS는 한 개의 스레드만을 사용하는 언어이기 때문에 Babel과 Terser은 한 번에 한 개의 파일만 변환할 수 있다.</li>
</ul>
</li>
<li>하지만 Rust는 병렬 처리가 가능하도록 설계되어 있다.<ul>
<li>이 때문에 SWC는 의존성이 없는 파일들을 동시에 변환할 수 있다.</li>
<li>만약 컴퓨터가 최대 5개의 작업을 동시에 진행할 수 있다면, SWC를 사용한 빌드 속도는 Babel이나 Terser로 빌드했을 때보다 최대 5배까지 빨라질 수 있는 것이다.</li>
</ul>
</li>
<li>또한 SWC의 <a href="https://swc.rs/docs/benchmarks">벤치마크 결과</a>에 따르면 SWC는 싱글 스레드 환경에서도 Babel보다 20배나 빠르다고 한다.<ul>
<li>여기서 우리는 SWC가 단순히 여러 작업을 동시에 할 수 있다는 이유만으로 Babel보다 빠른 것은 아님을 알 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>Rust의 가비지 컬렉션 수행 방식</p>
</blockquote>
<ul>
<li>가비지 컬렉션은 더이상 사용되지 않는 데이터 객체들에 의해 사용되는 메모리 리소스들을 버림으로써 메모리를 관리하는 방식을 의미한다.</li>
<li>Rust는 컴파일 시점에 더이상 필요하지 않은 메모리 리소스가 무엇인지 파악하고 그 이후에는 가비지 컬렉션을 지속하지 않기 때문에 수행 시간이 빨라진다.</li>
</ul>
<h3 id="2-확장성">2. 확장성</h3>
<ul>
<li>라이브러리를 fork 해오거나 설계에 대한 제약 조건 없이 Next.js에 미리 설치된 SWC를 사용할 수 있다.</li>
<li>SWC의 확장 가능한 특성 덕분에 별도로 라이브러리를 추가하지 않고도 Next.js 12에 사전 구축된 컴파일러를 사용할 수 있다.</li>
</ul>
<h3 id="3-webassembly">3. <a href="https://developer.mozilla.org/ko/docs/WebAssembly/Concepts">WebAssembly</a></h3>
<ul>
<li>최신 웹 브라우저에서 실행할 수 있는 새로운 유형의 코드</li>
<li>웹에서 실행되는 클라이언트 응용 프로그램을 사용해 어려 언어로 작성된 웹 코드를 네이티브에 가까운 속도로 실행할 수 있게 한다.</li>
<li>Rust가 WASM(WebAssembly)을 지원하기 때문에 어떤 종류의 플랫폼에서도 Next.js 개발이 가능하다.</li>
</ul>
<h3 id="4-커뮤니티">4. 커뮤니티</h3>
<ul>
<li>Rust의 커뮤니티와 생태계는 엄청나다🤸‍♀️</li>
</ul>
<h3 id="⚙️-swc-적용하기">⚙️ SWC 적용하기</h3>
<ul>
<li>SWC가 Next.js에 내장되어 있으므로 별도로 설치할 필요는 없다.</li>
</ul>
<blockquote>
<p>새로운 프로젝트에 적용하기</p>
</blockquote>
<pre><code>npx create-react-app@latest

npx create-next-app@latest --typescript</code></pre><blockquote>
<p>기존 프로젝트에 적용하기</p>
</blockquote>
<ul>
<li>Next.js 12 이전 버전을 사용 중이라면 업데이트가 필요하다.</li>
</ul>
<pre><code>npm install next@12</code></pre><ul>
<li>이미 babel configuration이 존재하는 경우 Next.js가 Babel을 인식하게 되므로 해당 파일을 지워주어야 한다.<ul>
<li><code>.babelrc</code> 또는 <code>babel.config.js</code> 파일을 지워준다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>추가 세팅; 최적화 옵션 적용하기</p>
</blockquote>
<pre><code>module.exports = {
  swcMinify: true,
}</code></pre><blockquote>
<p>추가 세팅; console call 제거하기</p>
</blockquote>
<pre><code>module.exports = {
  compiler: {
    removeConsole: true,
    // 몇몇 콘솔 기능을 제외하고 싶은 경우
    {
      exclude: ['log'], // console.log를 제외한 모든 console 제거
    },
    },
}</code></pre><h2 id="🔎-references">🔎 References</h2>
<details>
참고 자료 모음
<div>

<ul>
<li><a href="https://nextjs.org/docs/architecture/nextjs-compiler">Next.js Compiler</a></li>
<li><a href="https://nextjs.org/blog/next-12">Next.js 12</a></li>
<li><a href="https://bravenamme.github.io/2020/02/12/what-is-babel/">babel 이란 무엇인가?</a></li>
<li><a href="https://www.daleseo.com/js-babel/">바벨(Babel 7) 기본 사용법</a></li>
<li><a href="https://fe-developers.kakaoent.com/2022/220217-learn-babel-terser-swc/?ref=codenary">초보 웹 개발자를 위한 자바스크립트 빌드 툴과 SWC</a></li>
<li><a href="https://im-developer.tistory.com/230">[Kasra Khosravi] Why you should use SWC (and not Babel) 한글 번역</a></li>
<li><a href="https://velog.io/@kwonhygge/Next-JS%EA%B0%80-Babel%EC%9D%84-SWC%EB%A1%9C-%EB%8C%80%EC%B2%B4%ED%95%9C-%EC%9D%B4%EC%9C%A0">Next JS가 Babel을 SWC로 대체한 이유</a></li>
<li><a href="https://blog.logrocket.com/why-you-should-use-swc/#:~:text=In%20general%2C%20we%20see%20a,multi%2Dcore%20async%20operation%20process">Why you should use SWC (and not Babel)</a></li>
<li><a href="https://blog.bitsrc.io/why-you-should-replace-babel-with-swc-in-next-js-7d47510d0e0d">Why You Should Replace Babel with SWC in Next.js</a></li>
<li><a href="https://dev.to/this-is-learning/what-is-babel-and-swc-49cp">What is Babel? And SWC?</a></li>
</ul>
</div>
</details>