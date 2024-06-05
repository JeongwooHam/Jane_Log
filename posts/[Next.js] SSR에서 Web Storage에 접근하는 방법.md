<h2 id="🚨-referenceerror-localstorage-is-not-defined">🚨 ReferenceError: <a href="https://github.com/vercel/next.js/discussions/19911">localStorage is not defined</a></h2>
<pre><code class="language-js">import { useState } from &quot;react&quot;;

export default function Home() {
  let value;

  value = localStorage.getItem(&quot;pw&quot;) || &quot;&quot;;

  const [pw, setPw] = useState(value);

  const saveToLocalStorage = (e) =&gt; {
    e.preventDefault();
    localStorage.setItem(&quot;password&quot;, pw);
  };

  return (
    &lt;div&gt;
      &lt;label htmlFor=&quot;pw&quot;&gt;Write your password here.&lt;/label&gt;
      &lt;form onSubmit={saveToLocalStorage}&gt;
        &lt;input
          id=&quot;pw&quot;
          type=&quot;password&quot;
          value={pw}
          onChange={(e) =&gt; setPw(e.target.value)}
        /&gt;
        &lt;button type=&quot;submit&quot;&gt;&lt;/button&gt;
      &lt;/form&gt;
    &lt;/div&gt;
  );
}</code></pre>
<p>위와 같이 비밀번호를 localStorage에 저장하는 코드를 Next.js 프로젝트에서 작성했다고 가정해보자.
그리고 이 코드를 실행시키면,</p>
<pre><code>ReferenceError: localStorage is not defined</code></pre><p>이러한 에러가 발생한다.</p>
<h3 id="🤔-왜-발생하는-에러일까">🤔 왜 발생하는 에러일까?</h3>
<ol>
<li>Next.js는 Client-Side를 렌더링하기 전 Server-Side 렌더링을 수행한다.</li>
<li>Next.js에서 제공하는 SSR에서는 window, document와 같은 브라우저 전역 객체를 사용할 수 없다.</li>
<li>window 객체는 Client-Side에만 존재한다.<ul>
<li>WebStorage는 window의 객체이다.</li>
<li>페이지가 클라이언트에 로드되고, window 객체가 정의되기 전까지는 <code>window.localStorage</code>에 접근할 수 없다.</li>
</ul>
</li>
<li>따라서 코드가 서버에서 컴파일 될 때, localStorage 객체가 존재하지 않아 에러가 발생하는 것이다.</li>
</ol>
<h3 id="🧐-어떻게-해결할-수-있을까">🧐 어떻게 해결할 수 있을까?</h3>
<ul>
<li>이러한 에러를 해결하기 위해서는 localStorage에 접근하기 전에 클라이언트 측에 페이지가 마운트 될 떄까지 기다려야 한다.</li>
</ul>
<blockquote>
<p><code>typeof window !== 'undefined'</code></p>
</blockquote>
<ul>
<li>window 객체가 정의되었는지 확인하는 방법</li>
</ul>
<pre><code class="language-js">if (typeof window !== &quot;undefined&quot;) {
  // localStorage 관련 작업 수행 코드
  value = localStorage.getItem(&quot;pw&quot;) || &quot;&quot;;
}</code></pre>
<ul>
<li>페이지가 Client-Side에 마운트 될 때까지 기다렸다가 localStorage에 접근한다.</li>
<li>window 객체가 참조되지 않을 경우 undefined를 반환한다.<ul>
<li>localStorage는 window 객체 내부의 객체이므로 window 객체가 정의되지 않은 서버에서는 localStorage 관련 코드가 실행되지 않을 것이다.</li>
</ul>
</li>
<li>이를 통해 localStorage에 접근하기 전 localStorage가 정의된 상태라는 것을 보장한다.</li>
</ul>
<blockquote>
<p>typeof의 확장; class로 만들어서 사용하기</p>
</blockquote>
<pre><code class="language-js">class LocalStorage {
  constructor() {}

  static setItem(key: string, item: string) {
    if (typeof window !== &quot;undefined&quot;) {
      localStorage.setItem(key, item);
    }
  }

  static getItem(key: string) {
    if (typeof window !== &quot;undefined&quot;) {
      return localStorage.getItem(key);
    }
    return null;
  }

  static removeItem(key: string) {
    if (typeof window !== &quot;undefined&quot;) {
      localStorage.removeItem(key);
    }
  }
}

export default LocalStorage;</code></pre>
<ul>
<li>위와 같이 localStorage 관련 메서드를 클래스로 선언하여 사용할 수 있다.</li>
</ul>
<pre><code class="language-js">// 사용방법
import LocalStorage from &quot;../&quot;;

const saveToLocalStorage = (e) =&gt; {
  if (!e.target.value) return;
  e.preventDefault();
  LocalStorage.setItem(&quot;password&quot;, pw);
};</code></pre>
<blockquote>
<p><code>try-catch</code> 문 사용하기</p>
</blockquote>
<pre><code class="language-js">try {
  value = localStorage.getItem(&quot;pw&quot;) || &quot;&quot;;
} catch (error) {}</code></pre>
<ul>
<li>단순하게 try catch 블록으로 localStorage 접근 코드를 감쌀 수 있다.</li>
</ul>
<blockquote>
<p>🌟 <code>useEffect</code></p>
</blockquote>
<pre><code>👩‍🏫 위의 방식들보다 더 &quot;React&quot;스러운 해결책입니다.</code></pre><pre><code class="language-js">import { useEffect } from &quot;react&quot;;

useEffect(() =&gt; {
  // localStorage 관련 작업 수행 코드
  value = localStorage.getItem(&quot;pw&quot;) || &quot;&quot;;
}, []);</code></pre>
<ul>
<li>useEffect는 마운트 되었을 때 실행되기 때문에 CSR 전용 훅 함수이다.<ul>
<li>이 때문에 브라우저라는 확신을 줄 수 있고, <strong><em>not defined</em></strong>라는 에러에 대한 우려 없이 사용할 수 있다.</li>
</ul>
</li>
<li>useEffect는 렌더링 시 실행되므로 초기 서버 빌드 시에 useEffect 내부에 위치한 코드는 실행되지 않는다.</li>
<li>useEffect는 Client-Side에서만 실행되므로 localStorage에 안전하게 접근할 수 있다.</li>
</ul>
<h2 id="🔎-references">🔎 References</h2>
<details>
참고 자료 모음
<div>

<ul>
<li><a href="https://velog.io/@dngur9801/Next.js-localStorage-%EC%9D%B4%EC%8A%88">[Next.js] localStorage 이슈</a></li>
<li><a href="https://developer.school/snippets/react/localstorage-is-not-defined-nextjs#scenario">How to Fix &quot;localStorage is not defined&quot; in Next.js</a></li>
<li><a href="https://all-dev-kang.tistory.com/entry/Next-localstorage%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95">[Next] localstorage를 사용하는 방법 #1</a></li>
<li><a href="https://chunho.tistory.com/60">[nextJS] localStorage 사용하기</a></li>
<li><a href="https://dev.to/collegewap/how-to-use-local-storage-in-nextjs-2l2j">How to use Local Storage in Next.js</a></li>
<li><a href="https://stackoverflow.com/questions/63312727/how-to-deal-with-local-storage-and-ssr">How to deal with local storage and SSR?</a></li>
<li><a href="https://stackoverflow.com/questions/76070793/localstorage-is-not-defined-in-next-js">localStorage is not defined in next js</a></div>
</details>
</li>
</ul>