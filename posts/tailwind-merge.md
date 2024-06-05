<h2 id="🤔-무엇을-위한-것일까">🤔 무엇을 위한 것일까?</h2>
<ul>
<li><p>간단히 소개하자면, 스타일 충돌 없이 JS에서 Tailwind CSS 클래스들을 병합할 수 있게 해주는 유틸 함수이다.</p>
</li>
<li><p>Tailwind CSS를 React나 Vue 같은 컴포넌트 기반 라이브러리와 함께 사용할 때 아래와 같이 하나의 특정 케이스에서만 컴포넌트의 몇몇 스타일을 바꾸고 싶은 상황을 마주친 경험이 많다.</p>
</li>
</ul>
<pre><code class="language-js">function CommonInput(props) {
    const className = `border rounded px-2 py-1 ${props.className || ''}`
    return &lt;input {...props} className={className} /&gt;
}

function ExceptionalInput(props) {
    return (
        &lt;MyGenericInput
            {...props}
            className=&quot;p-3&quot; // ← Only want to change some padding
        /&gt;
    )
}</code></pre>
<ul>
<li><strong>ExceptionalInput</strong>이 렌더링 될 때, <code>border rounded px-2 py-1 p-3</code>이라는 className을 갖는 input이 생성된다.</li>
<li>하지만 CSS 캐스캐이딩의 작동 때문에 <strong>p-3</strong>은 무시될 것이다.<ul>
<li>CSS 캐스캐이딩(cascading)</li>
</ul>
</li>
<li>className에서 클래스명의 순서는 의미가 없기 때문에 <strong>p-3</strong>을 적용하기 위해서는 <strong>px-2</strong>와 <strong>py-1</strong>을 삭제해주어야 한다.</li>
</ul>
<pre><code>🤠 그래서 tailwind-merge가 등장했습니다!</code></pre><pre><code class="language-js">function MyGenericInput(props) {
    // 이제 `props.className`가 충돌하는 클래스 명을 덮어쓸 수 있습니다.
    const className = twMerge('border rounded px-2 py-1', props.className)
    return &lt;input {...props} className={className} /&gt;
}</code></pre>
<ul>
<li>tainwind-merge는 충돌하는 클래스 명만 덮어쓰고 다른 것들은 그대로 남겨둔다.<ul>
<li>위의 예시에서 <strong>ExceptionalInput</strong>은 <code>border rounded p-3</code>이라는 클래스와 함께 렌더링될 것이다.</li>
</ul>
</li>
</ul>
<h2 id="📂-api-reference">📂 API reference</h2>
<h3 id="✨-twmerge">✨ twMerge</h3>
<pre><code class="language-ts">function twMerge(
    ...classLists: Array&lt;string | undefined | null | false | 0 | typeof classLists&gt;
): string</code></pre>
<ul>
<li><p>기본 Tailwind config를 사용하고 있거나 기본값과 근사한 config 파일을 사용하고 있을 경우 사용하는 기본 함수이다.</p>
</li>
<li><p>twMerge가 적용되지 않는다면 <strong>extendTailwindMerge</strong>를 사용하여 커스텀 함수를 생성할 수 있다.</p>
</li>
</ul>
<h3 id="✨-twjoin">✨ twJoin</h3>
<pre><code class="language-ts">function twJoin(
    ...classLists: Array&lt;string | undefined | null | false | 0 | typeof classLists&gt;
): string</code></pre>
<p>충돌을 해결하지 않고 조건적으로 클래스명 문자열을 합성해주는 함수이다.
twJoin 사용 시 조금 더 빠르며 번들 사이즈를 줄일 수 있다.
아래와 같이 사용이 가능하다. </p>
<pre><code class="language-ts">twJoin(
    'border border-red-500',
    hasBackground &amp;&amp; 'bg-red-100',
    hasLargeText &amp;&amp; 'text-lg',
    hasLargeSpacing &amp;&amp; ['p-2', hasLargeText ? 'leading-8' : 'leading-7'],
)</code></pre>
<h2 id="🌟-특징">🌟 특징</h2>
<h3 id="merging-behavior">Merging behavior</h3>
<ul>
<li>tailwind-merge는 직관적으로 만들어졌기 때문에 아래의 규칙들을 통해 충돌이 있는 경우 어떤 클래스가 <strong>이기는</strong>지를 파악할 수 있다.</li>
</ul>
<h3 id="🟢-장점">🟢 장점</h3>
<blockquote>
<p>다양한 층위의 컴포넌트를 작성하기 쉽다.</p>
</blockquote>
<p>tailwind-merge는 디자인 시스템이나 UI 컴포넌트 라이브러리처럼 HOC에 적합하다.</p>
<ul>
<li>HOC(고차 컴포넌트): 컴포넌트를 가져와 새 컴포넌트를 반환하여 컴포넌트 로직을 재사용할 수 있게 한다.</li>
</ul>
<blockquote>
<p>빠른 개발과 반복 속도를 가능케 한다.</p>
</blockquote>
<p>tailwind-merge를 사용하면 컴포넌트 내에서 각각을 명시적으로 정의하지 않고도 다양한 범위의 스타일링을 지원할 수 있다. 
예를 들어, 버튼 컴포넌트의 너비, 글자 색상이나 위치를 명시적으로 정의하지 않더라도 하나의 <code>className</code>의 prop으로 커스텀한 width와 글자 색상, 위치를 변경시킬 수 있다.</p>
<blockquote>
<p>성급한 추상화를 방지한다.</p>
</blockquote>
<ul>
<li>여러 곳에서 사용되고 있는 버튼 컴포넌트에 대해 특정 상황에서만 <code>error</code>를 나타내도록 스타일을 변경하고 싶을 경우 버튼 컴포넌트에 특정 속성만 전달하여 구현할 수 있다.
이후 더 많은 곳에서 해당 스타일을 생성하고 싶은 경우 버튼 컴포넌트 내부를 수정할 수도 있다.</li>
</ul>
<h3 id="🔴-단점">🔴 단점</h3>
<blockquote>
<p>번들 사이즈가 증가한다.</p>
</blockquote>
<p>tailwind-merge의 경우 어떤 클래스들이 충돌하는지를 파악하기 위해 방대한 크기의 config에 의존한다. 
타이트한 번들 사이즈 제약 조건을 가질 경우 제한이 될 수 있다.</p>
<blockquote>
<p>컴포넌트 사용자에게 너무 많은 자율성을 부여할 수 있다.</p>
</blockquote>
<p>대규모 팀이나 공개적으로 사용 가능하게 만들어진 컴포넌트의 경우 컴포넌트 사용자가 컴포넌트가 허용하는 방식으로 컴포넌트의 API를 사용할수도, 사용하지 않을수도 있다. 이러한 상황에서 tailwind-merge는 컴포넌트 사용자에게 너무 많은 자유를 부여하여 시간이 지남에 따라 컴포넌트를 유지 관리하고 발전시키기가 더 어려워질 수 있다. tailwind-merge를 사용하려면 컴포넌트 스타일링의 완전한 통제는 포기해야 할 것이다.</p>
<blockquote>
<p>재사용 가능성이 높은 컴포넌트 리팩토링이 어려울 수 있다.</p>
</blockquote>
<p>컴포넌트에 임의의 클래스를 전달할 수 있도록 허용하면 컴포넌트의 내부 스타일을 리팩터링할 때 컴포넌트 사용자의 스타일이 손상될 수 있다. 만약 당신이 컴포넌트의 스타일을 자주 리팩토링할 수 있어야 한다면 이러한 스타일은 컴포넌트의 용도 또한 리팩토링할 예정이 아닌 한 props로 전달되는 스타일과 병합되지 말아야 한다.</p>
<blockquote>
<p>Tailwind CSS나 컴포넌트 합성을 사용하지 않을 경우 무용하다.</p>
</blockquote>
<p>tailwind-merge는 TailwindCSS과 컴포넌트 합성을 특정한 형태에서 함꼐 사용할 때에만 유용하다.</p>
<ul>
<li>컴포넌트 합성: 컴포넌트를 작은 단위로 분리하고 재조합하여 재사용성을 높이는 것</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://github.com/dcastil/tailwind-merge">tailwind-merge</a></li>
<li><a href="https://github.com/dcastil/tailwind-merge/blob/v2.1.0/docs/what-is-it-for.md">tailwind-merge | what is it for</a></li>
<li><a href="https://github.com/dcastil/tailwind-merge/blob/v2.1.0/docs/when-and-how-to-use-it.md">tailwind-merge | when and how to use it</a></li>
<li><a href="https://github.com/dcastil/tailwind-merge/blob/v2.1.0/docs/features.md">tailwind-merge | features</a></li>
<li><a href="https://velog.io/@wgnator/Components-Composition">Components Composition</a></li>
</ul>