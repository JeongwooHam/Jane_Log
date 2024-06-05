<ul>
<li><p>HTML 요소는 HTML 문서와 웹 페이지를 구성한다.</p>
</li>
<li><p>일반적인 요소는 여는 태그와 몇 가지 특성, 내용과 닫는 태그로 구성된다.</p>
</li>
</ul>
<h2 id="🦴-anatomy-of-an-html-elements">🦴 Anatomy of an HTML elements</h2>
<img src="https://velog.velcdn.com/images/hamjw0122/post/e8f18621-fa18-4398-a20c-8057a3e574af/image.png" width="60%" />

<ul>
<li>요소는 데이터 항목, 텍스트, 이미지 등 다양한 콘텐츠를 담을 수 있고, 아무것도 담지 않는 것도 가능하다.</li>
</ul>
<h3 id="🌠-여는닫는-태그-openingclosing-tag">🌠 여는/닫는 태그 (Opening/Closing Tag)</h3>
<ul>
<li><p>HTML 요소를 만들 때 사용되는 태그는 요소 이름과 이를 둘러싸는 꺾쇠괄호(&lt;&gt;)로 이루어진다.</p>
</li>
<li><p>닫는 태그의 경우 슬래시(/)를 넣어 시작 태그와 구별한다.</p>
</li>
<li><p>하지만 모든 요소가 여는 태그, 내용, 닫는 태그의 구조로 이루어져 있는 것은 아니다.</p>
<ul>
<li>빈 태그(Void Elements로도 불림)는 시작 태그로만 있는 단일 태그 구성을 가진다.</li>
<li>이미지를 삽입하기 위해 사용되는 <strong>img</strong> 요소 등이 이에 해당한다.</li>
</ul>
</li>
<li><p>위의 구조도를 통해서도 알 수 있듯, 요소와 태그는 같지 않다.</p>
<ul>
<li>태그: 소스 코드에서 요소의 시작과 끝을 '표시'하는 역할을</li>
<li>요소: 브라우저가 페이지를 표시할 때 사용하는 문서 모델인 DOM의 일부</li>
</ul>
</li>
<li><p>Java에서 메서드를 이용할 때 대소문자의 구분이 중요한 것과는 다르게, HTML 요소는 대소문자를 구분하지 않는다.</p>
<ul>
<li><strong>title</strong> 요소는 <strong>Title</strong>, <strong>TITLE</strong>, <strong>TiTlE</strong> 등으로 사용해도 오류가 아니다.</li>
<li>다만, 일반적으로는 가독성 등을 위해 소문자로 작성한다.</li>
</ul>
</li>
</ul>
<h3 id="🌠-내용-content">🌠 내용 (Content)</h3>
<ul>
<li>요소의 내용에는 단순한 텍스트가 올 수 있다.</li>
</ul>
<h3 id="🌠-속성-attribute">🌠 속성 (Attribute)</h3>
<ul>
<li><p>속성은 요소에 실제론 나타내고 싶지 않지만 추가적인 내용을 담고 싶을 때 사용한다.</p>
</li>
<li><p>태그를 확장해 동작 방식을 바꾸거나 메타데이터를 제공한다.</p>
</li>
</ul>
<blockquote>
<p><strong>🤖 Metadata</strong> : 데이터에 대한 데이터. 원시데이터를 구조화/표준화한 정보)</p>
</blockquote>
<ul>
<li><p>특성은 <strong><em>속성명(name) = &quot;속성값(value)&quot;</em></strong>의 형태를 가진다.</p>
</li>
<li><p>다만 위의 예시처럼 속성이 별도로 지정된 경우가 아니라면, 기본값이 사용된다.</p>
</li>
<li><p>속성을 사용할 때 주의해야 할 세 가지 규칙</p>
</li>
</ul>
<pre><code>1️⃣ 요소 이름과 속성명 사이, 하나 이상의 속성들이 있는 경우 속성 사이에는 공백이 있어야 한다.

2️⃣속성명 다음엔 등호(=)가 붙어야 한다.

3️⃣ 속성값은 열고 닫는 따옴표로 감싸야 한다.

    예) &lt;inputVtype=&quot;radio&quot;Vname=&quot;gender&quot;Vvalue=&quot;0&quot;/&gt;

    V: 띄어쓰기 표시
</code></pre><h2 id="block-level-🤼-inline-elements">Block Level 🤼 Inline Elements</h2>
<pre><code>👩‍🏫 HTML에는 두 가지 종류의 요소가 있습니다.</code></pre><h3 id="😶-블록-레벨-요소block-level-elements">😶 블록 레벨 요소(Block-level elements)</h3>
<img src="https://velog.velcdn.com/images/hamjw0122/post/62fb2425-4b5c-4f99-b192-2ed821dc43bf/image.png" />

<ul>
<li>블록 레벨 요소인 <strong>p</strong> 요소는 화면 너비 전체를 차지한다.</li>
<li>웹페이지 상에 블록(Block)을 만드는 요소이다.</li>
<li>블록 레벨 요소는 항상 새로운 줄에서 시작하며, 좌우 양쪽으로 모두 확장되어 화면 상 가능한 모든 너비를 차지한다.</li>
</ul>
<h3 id="🫥-인라인-요소inline-elements">🫥 인라인 요소(Inline elements)</h3>
<img src="https://velog.velcdn.com/images/hamjw0122/post/2ae86202-0109-480d-9702-7515d0cf7d9a/image.png" width="50%" />

<ul>
<li>인라인 요소는 문서의 한 단락 같은 큰 범위에는 적용될 수 없고 문장, 단어 같은 작은 부분에 대해서만 적용 가능하므로 항상 블록 레벨 요소 내에 포함되어 있다.</li>
<li>다시 말해, 인라인 요소는 새로운 줄(Line)을 만들지 않는다.</li>
<li>따라서 무조건 줄바꿈 되어 다음 줄에서부터 시작되는 블록 레벨 요소와 달리, 인라인 요소는 줄의 어느 곳에서나 시작할 수 있다.</li>
</ul>
<hr />

<ul>
<li>블록 레벨 요소가 다른 블록 레벨 요소에 중첩되는 것은 가능하다.</li>
<li>블록 레벨 요소가 인라인 요소 안에 중첩되는 것은 불가능하다.</li>
<li>대표적 블록 레벨/인라인 요소인 <strong>div</strong> 요소와 <strong>span</strong> 요소로 예를 들어보자.<ul>
<li><strong>div</strong> 요소에 <strong>span</strong> 요소를 중첩시키는 것은 가능하다.</li>
<li><strong>div</strong> 요소에 <strong>div</strong> 요소를 중첩시키는 것도 가능하다.</li>
<li><strong>span</strong> 요소 안에 <strong>div</strong> 요소를 중첩시키는 것은 불가능하다.</li>
</ul>
</li>
<li>블록 레벨 요소와 인라인 요소의 개별적 예시들은 다음 게시글 'HTML의 요소 이해하기 (2)'에서 다루도록 하겠다.</li>
</ul>
<p><a href="https://developer.mozilla.org/ko/docs/Web/HTML">참조 문서</a></p>