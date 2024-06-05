<h2 id="🧐-nextjs에서의-csr-왜-사용할까">🧐 Next.js에서의 CSR, 왜 사용할까?</h2>
<ul>
<li>React의 CSR에서, 브라우저는 최소한의 HTML 파일과 페이지에 필요한 최소한의 JS 코드만을 다운로드 받는다.</li>
<li>그 후 클라이언트는 JS를 사용하여 DOM을 업데이트하고, 페이지를 렌더링한다.</li>
<li>애플리케이션이 처음 로드되었을 때, 사용자는 그들이 전체 페이지를 보기 전에 약간의 지연을 겪게 된다.<ul>
<li>이는 모든 JS 코드가 다운로드 되어 파싱되고, 실행되기 전까지 페이지가 렌더링되지 않기 때문이다.</li>
</ul>
</li>
<li>대신 CSR 방식을 사용하는 경우 페이지가 처음 로드된 이후에 같은 웹 사이트 내 다른 페이지로의 이동이 다른 방식에 비해 일반적으로 더 빠르다.<ul>
<li>필요한 데이터만 fetching하면 되고, JS는 전체 페이지를 새로고침하지 않고도 페이지의 일부를 리렌더링할 수 있기 때문이다.</li>
</ul>
</li>
</ul>
<pre><code>👩‍🏫 이제 Next.js에서 공식적으로 알려주는 두 가지 CSR 구현 방법을 알아봅시다!</code></pre><h2 id="🪄-codeuseeffectcode-사용하기">🪄 <code>useEffect()</code> 사용하기</h2>
<h3 id="🌟-ssr-메소드-대신-codeuseeffectcode-훅을-페이지-내부에-사용한다">🌟 SSR 메소드 대신 <code>useEffect()</code> 훅을 페이지 내부에 사용한다.</h3>
<pre><code class="language-js">import React, { useState, useEffect } from &quot;react&quot;;

export function Page() {
  const [data, setData] = useState(null);

  useEffect(() =&gt; {
    const fetchData = async () =&gt; {
      const response = await fetch(&quot;https://api.example.com/data&quot;);
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      const result = await response.json();
      setData(result);
    };

    fetchData().catch((e) =&gt; {
      // handle the error as needed
      console.error(&quot;An error occurred while fetching the data: &quot;, e);
    });
  }, []);

  return &lt;p&gt;{data ? `Your data: ${data}` : &quot;Loading...&quot;}&lt;/p&gt;;
}</code></pre>
<ol>
<li>컴포넌트는 <code>Loading...</code>을 보여주면서 렌더링 과정을 시작한다.</li>
<li>데이터가 fetch 되면, 컴포넌트는 리렌더링 되면서 데이터를 보여준다.</li>
</ol>
<h2 id="💼-data-fetching-라이브러리-사용하기">💼 Data-Fetching 라이브러리 사용하기</h2>
<ul>
<li>클라이언트가 데이터를 fetch할 수 있도록 <code>SWR</code>과 같은 data-fetching 라이브러리를 사용한다.</li>
</ul>
<pre><code>👩‍🏫 공식적으로 권장되는 방식입니다!</code></pre><h3 id="swr"><a href="https://swr.vercel.app/ko">SWR</a></h3>
<img src="https://github.com/JeongwooHam/FE_Study_Logs/assets/123251211/24802325-cf73-4247-8dcd-3dc6cd857299" width="50%" />

<ul>
<li>Stale-While-Revalidate</li>
<li>데이터를 가져오기 위한 React 훅 함수</li>
<li>Vercel에서 만든, 데이터를 가져오기 위한 모듈이다.</li>
<li>백그라운드에서 캐시에 대한 fetch 요청(revalidate)을 하는 동안 신선하지 않은 상태의 캐시 데이터를 사용하여 화면을 렌더링하다가 최종적으로는 최신화된 신선한 데이터를 반환한다.</li>
<li>도중에 에러를 반환하더라도 기존 캐시 데이터를 사용할 수 있게 하여 불필요한 API Call과 렌더링을 최소화할 수 있게 한다.</li>
<li><code>npm i swr</code>로 설치하여 사용할 수 있다.</li>
</ul>
<h3 id="codeuseswrcode"><code>useSWR</code></h3>
<pre><code class="language-js">import useSWR from &quot;swr&quot;;

const fetcher = (url: string) =&gt; axios.get(url);

function Profile() {
  const { data, error, isLoading } = useSWR(&quot;/api/url&quot;, fetcher, {// option});

  if (error) return &lt;div&gt;failed to load&lt;/div&gt;;
  if (isLoading) return &lt;div&gt;loading...&lt;/div&gt;;
  return &lt;div&gt;hello {data.name}!&lt;/div&gt;;
}</code></pre>
<ul>
<li><code>useSWR(key, fetcher)</code><ul>
<li>key(string): 데이터의 고유한 식별자 (일반적으로 API URL)</li>
<li>fetcher(function): 데이터를 반환하는 비동기 함수 (axios, fetch 등)</li>
</ul>
</li>
<li>요청의 상태에 따라 <code>{data, isLoading, error}</code> 값을 반환한다.<ul>
<li>data: 요청에 에러가 없는 경우 가져오는 데이터</li>
<li>error: 요청에 에러가 있는 경우 발생한 오류</li>
</ul>
</li>
<li>세 번째 인자인 option 객체에 <code>revalidate, mutate, initialData</code> 등의 값을 넣어줄 수 있다.</li>
</ul>
<h3 id="🌟-codeuseswrcode과-함께-nextjs에서-csr-구현하기">🌟 <code>useSWR</code>과 함께 Next.js에서 CSR 구현하기</h3>
<pre><code class="language-js">import useSWR from &quot;swr&quot;;

export function Page() {
  const { data, error, isLoading } = useSWR(
    &quot;https://api.example.com/data&quot;,
    fetcher
  );

  if (error) return &lt;p&gt;Failed to load.&lt;/p&gt;;
  if (isLoading) return &lt;p&gt;Loading...&lt;/p&gt;;

  return &lt;p&gt;Your Data: {data}&lt;/p&gt;;
}</code></pre>
<ul>
<li>Next.js 공식문서에서는 성능이나 캐싱, 낙관적 업데이트 등의 측면에서 data-fetching 라이브러리를 사용하는 것을 권장한다.</li>
<li>SWR은 자동으로 데이터를 캐싱하고 만약 데이터가 신선하지 않은 상태가 된다면 해당 데이터에 대해 <code>revalidate</code>를 진행한다.</li>
</ul>
<blockquote>
<p>🤔 어떻게 동작하나요?</p>
</blockquote>
<ol>
<li>useSWR은 초기에 props로 넘어온 데이터를 SWR 캐시에 저장한다.</li>
<li>SWR는 캐시 데이터가 있으므로, 컴포넌트 최초 렌더링 시 요청을 보내지 않는다.</li>
<li>대신 다른 화면을 갔다와서 다시 포커싱 되거나, 네트워가 끊겼다가 다시 복구되는 등의 상황 또는 사용자의 설정에 따라 원하는 순간에 revalidate 값을 설정하면 SWR은 데이터를 재요청한다.</li>
<li>만약 새로 불러온 값이 기존의 캐시 데이터와 같다면 따로 리렌더링을 발생시키지 않고, 다른 경우 리렌더링을 진행한다.</li>
</ol>
<h2 id="📢-그럼에도-잊지-말아야-할-것">📢 그럼에도 잊지 말아야 할 것</h2>
<ul>
<li>몇몇 검색 엔진의 크롤러들은 JS를 실행하지 못하여 CSR 방식을 사용할 경우 초기의 빈 화면이나 로딩 중인 상태만을 보게 될 수 있다.</li>
<li>또한 사용자들은 그들이 전체 페이지를 보기 전 모든 JS 코드가 로드되고 실행되는 것을 기다려야 하므로 인터넷이나 기기의 연결이 다른 방식을 사용할 때보다 더 느리다고 생각할 수 있다.</li>
<li>Next.js는 CSR 뿐만 아니라 SSR, SSG 방식을 각 페이지의 필요에 따라 혼용할 수 있도록 만들어져 있으므로, 무조건 한 방식만을 채택하기 보다는 각 페이지에 적합한 방식이 무엇인지를 고민하여 사용하면 좋다!</li>
</ul>
<h2 id="🔎-references">🔎 References</h2>
<details>
참고 자료 모음
<div>

<ul>
<li><a href="https://nextjs.org/docs/pages/building-your-application/rendering/client-side-rendering">Client-side Rendering (CSR)</a></li>
<li><a href="https://nextjs.org/docs/pages/building-your-application/data-fetching/client-side#client-side-data-fetching-with-useeffect">Client-side Fetching</a></li>
<li><a href="https://velog.io/@sinclairr/next-swr-1">Next.js에서 SWR을 사용해 보자 - 1 (Fetch)</a></li>
<li><a href="https://velog.io/@denmark-banana/Nextjs-PreRendering-useSWR">Next.js 에서 Pre-rendering (SSG, SSR)과 useSWR(CSR) 잘 융합하기</a></li>
<li><a href="https://jjongsk.tistory.com/entry/useSWR%EC%9D%98-3%EA%B0%80%EC%A7%80-hook%EB%93%A4%EA%B3%BC-%EC%82%AC%EC%9A%A9%EB%B2%95">useSWR의 3가지 hook들과 사용법</a></li>
</ul>
</div>
</details>