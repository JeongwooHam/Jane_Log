<pre><code>👩‍🏫 HTML의 블록 레벨 요소들이 각각 어떠한 역할을 하는지 정리해봅시다.</code></pre><h2 id="😶-block-level-elements">😶 Block Level Elements</h2>
<h3 id="✨-div-콘텐츠-분할-요소">✨ div: 콘텐츠 분할 요소</h3>
<ul>
<li><p>가장 사용빈도가 높은 요소라고 할 수 있지만 순수 컨테이너로서 기능할 뿐 아무것도 표현하지 않는다.</p>
</li>
<li><p>하나의 구역, 비어있는 박스, 틀을 나누는 역할(division)만 하기 때문에 CSS로 꾸미기 전에는 콘텐츠나 레이아웃에 어떤 영향도 주지 않는다.</p>
</li>
<li><p>해당 요소를 통해 class나 id 속성으로 꾸미는 것을 편리하게 하고, 해당 요소에 lang 속성을 적용하면 문서의 특정 구역이 다른 언어임을 표시할 수 있다.</p>
</li>
</ul>
<pre><code class="language-html">&lt;div&gt;안녕하세요&lt;/div&gt;</code></pre>
<h3 id="✨-p">✨ p</h3>
<ul>
<li><p>하나의 문단(Paragraph)을 나타낸다.</p>
</li>
<li><p>자신의 닫는 태그 이전에 다른 블록 레벨 요소가 있으면 닫는 태그가 없더라도 자동으로 닫힌다.</p>
</li>
<li><p>문단을 구분할 때 위 아래 여백이 생기게 되는데, 보통은 css로 이런 기본 속성 값을 초기화시킨다.</p>
</li>
<li><p><strong>p</strong> 태그 안에는 <strong>div</strong> 태그를 사용할 수 없다.</p>
<ul>
<li>하지만 <strong>div</strong> 태그 안의 <strong>p</strong> 태그, <strong>div</strong> 태그 안의 <strong>div</strong> 태그는 가능하다.</li>
</ul>
</li>
</ul>
<pre><code class="language-html">&lt;p&gt;안녕하세요.&lt;/p&gt;</code></pre>
<hr />

<p>여기까지 공부하다보면 궁금증이 하나 생기기 마련이다.
<strong>div</strong> 태그와 <strong>p</strong> 태그 모두 문자를 출력할 수 있으며 블록 레벨 요소이기 때문에 자동 줄바꿈으로 단락을 형성한다.</p>
<img src="https://velog.velcdn.com/images/hamjw0122/post/2962af8b-c120-4cbf-b176-a88e109082e2/image.jpg" width="25%" />

<pre><code>그렇다면...
&lt;div&gt; 태그와 &lt;p&gt; 태그는 무슨 차이가 있는걸까?
왜 &lt;p&gt; 태그 안에는 &lt;div&gt; 태그를 사용할 수 없을까?</code></pre><h3 id="div-🤼-p">div 🤼 p</h3>
<ul>
<li><p><strong>p</strong> 태그는 문자 정보를 입력하는 단락을 구성한다.</p>
</li>
<li><p>단락을 표현하는 역할을 하므로 다음의 단락과 구분되게 하기 위해 한 줄을 강제로 비워 여백을 형성한다.</p>
</li>
<li><p><strong>p</strong> 태그 속 각 문장에 채색한 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/39f9d32b-2206-44e1-b688-11f39656eee8/image.png" /></p>
</li>
<li><p>이처럼 <strong>p</strong> 태그로 background가 채색된 문장 다섯 개를 구현하면 문장과 문장 사이게 비워져 채색되는 것을 확인할 수 있다.</p>
</li>
<li><p>이러한 이유로, <strong>p</strong> 태그 하위 부분에는 인라인 요소만 올 수 있다.</p>
</li>
</ul>
<ul>
<li><p>반대로, <strong>div</strong> 태그의 주된 역할은 엄밀히 말하면 '영역 구분'이다.</p>
</li>
<li><p>물론 <strong>p</strong> 태그처럼 문자 정보를 입력할 수 있기 때문에 비슷한 것처럼 사용되지만 <strong>div</strong>의 실제 용도는 HTML 문서를 영역별로 구분하여 웹 페이지의 레이아웃을 보여주는 데 있다.</p>
</li>
<li><p><strong>div</strong> 태그 속 각 문장에 채색한 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/821764f6-0c82-49bc-b678-37af3cf26af5/image.png" /></p>
</li>
<li><p><strong>p</strong> 태그로 구현한 결과와는 다르게 <strong>div</strong> 태그를 사용한 결과 단락 간의 여백 없이 채색되어 있는 것을 확인할 수 있다.</p>
</li>
<li><p>영역의 용도를 구분하는 데 사용되기 때문에 <strong>div</strong> 태그의 하위에는 인라인 요소 뿐만 아니라 다른 블록 요소들, 심지어는 또 다른 <strong>div</strong> 태그도 위치할 수 있는 것이다.</p>
</li>
<li><p><strong>div</strong> 태그 속 <strong>p</strong> 태그에 채색한 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/c38c56ac-fa71-4223-8935-c09c301faca3/image.png" /></p>
</li>
<li><p>이를 이용하여 <strong>div</strong> 태그 안에 <strong>p</strong> 태그들을 사용하면, <strong>p</strong> 태그는 단락을 구분하며 문장 간 한 줄 씩을 여백으로 설정해두었지만, <strong>div</strong> 태그는 전체를 하나의 영역으로 간주하여 해당 여백 부분까지 채색한 것을 확인할 수 있다.</p>
</li>
</ul>
<hr />

<ul>
<li>정리하자면, <strong>p</strong> 태그는 문자 정보들의 단락을 구분하는 역할, <strong>div</strong> 태그는 웹 페이지의 레이아웃을 계층으로 나누는 역할을 한다.</li>
<li>따라서 <strong>p</strong> 태그 내부에 <strong>div</strong> 태그를 사용하는 것은 불가능하나 <strong>div</strong> 태그에는 모든 요소들이 위치할 수 있다.</li>
</ul>
<h3 id="✨-h1---h6-html-구획-제목-요소">✨ h1 - h6: HTML 구획 제목 요소</h3>
<ul>
<li><p>총 6단계로 구성된 제목 요소로, 각 숫자마다 폰트 크기, 굵기, 여백 등이 다르다.</p>
</li>
<li><p>단계는 h1이 가장 높고 h6가 가장 낮다.</p>
</li>
<li><p>'제목' 요소이므로 단순히 글씨의 크기를 조절하기 위해서라면 CSS로 font-size를 조절하는 것이 낫다.</p>
</li>
<li><p>오류에 해당하지는 않지만, 한 페이지에는 하나의 <strong>h1</strong>을 사용하는 것이 좋다.</p>
</li>
</ul>
<pre><code class="language-html">    &lt;h1&gt;1단계&lt;/h1&gt;
    &lt;h2&gt;2단계&lt;/h2&gt;
    &lt;h3&gt;3단계&lt;/h3&gt;
    &lt;h4&gt;4단계&lt;/h4&gt;
    &lt;h5&gt;5단계&lt;/h5&gt;
    &lt;h6&gt;6단계&lt;/h6&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/a77f5309-947c-47ed-8e6c-7e87016ae6e0/image.png" /></p>
<h3 id="✨-hgroup">✨ hgroup</h3>
<ul>
<li><p>문서 구획의 다단계 제목을 나타낸다.</p>
</li>
<li><p>다수의 <strong>h1</strong>~<strong>h6</strong> 요소들을 묶을 때 사용한다.</p>
</li>
</ul>
<pre><code class="language-html">&lt;hgroup&gt;
        &lt;h1&gt;주요 제목&lt;/h1&gt;
        &lt;h2&gt;부제목&lt;/h2&gt;
        &lt;h3&gt;저자명&lt;/h3&gt;
&lt;/hgroup&gt;</code></pre>
<h3 id="✨-address">✨ address</h3>
<ul>
<li><p>사람/단체/조직 등의 연락처 정보를 나타낸다.</p>
</li>
<li><p>연락처가 가리키는 사람/단체/조직의 이름이 필수적으로 들어가야 하며 물리적 주소, URL, 이메일 주소, 전화번호, SNS 식별자, 좌표 등 어떠한 정보라도 포함할 수 있다.</p>
</li>
</ul>
<h2 id="🤖-semantic-web-tag">🤖 Semantic Web Tag</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/2d5b05a1-5ff2-40c9-944a-2824ed5a84d8/image.png" /></p>
<p><a href="https://www.w3schools.com/html/html5_semantic_elements.asp">사진 출처</a></p>
<ul>
<li>검색 엔진(Naver, Google...)은 크롤링 과정을 통해 전 세계 웹 사이트의 정보를 수집한다.</li>
<li>그리고 사이트 이용자가 검색할 만한 키워드를 선정하여 미리 이에 대한 색인을 생성하는데, 이 과정을 인덱싱이라 한다.</li>
<li>이 인덱싱 과정에서 사용되는 정보가 바로 HTML 코드이다.</li>
<li>시멘틱 웹 태그란 이 과정에서 검색 엔진이 해당 웹 사이트에 대한 정보를 더 쉽게 파악할 수 있도록 태그에 해당 태그의 역할을 통해 이름을 지어주는 것이다.</li>
<li>HTML 코드에 다양한 메타데이터를 부여함으로써 단순 데이터 집합이었던 웹 페이지가 '의미'와 '연관성'을 가지도록 한다.</li>
</ul>
<blockquote>
<p>주석으로 표시만 한 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/7ab702b5-4a49-48a5-a3f6-8630662d1615/image.png" /></p>
</blockquote>
<blockquote>
<p>semantic web 태그를 사용한 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/f5f414b9-a81a-4c9f-af59-51128448acf6/image.png" /></p>
</blockquote>
<ul>
<li>위의 두 코드는 동일하게 기능하지만, 전자는 기계의 입장에서 보았을 때 의미론적으로 뚜렷한 의미를 나타내지 못하는 반면 후자는 기계로 하여금 해당 요소들이 어떠한 역할을 하는지 해석할 수 있게 한다.</li>
<li>각각의 시멘틱 웹 태그들은 고유한 의미를 내포하므로 개발자가 의도한 요소의 의미가 명백히 드러나게 된다.<ul>
<li>이는 코드의 가독성을 높이고, 더 나아가 유지보수성 또한 향상시킨다.</li>
</ul>
</li>
<li>또한 시멘틱 웹 태그는 웹 접근성을 높인다.</li>
</ul>
<blockquote>
<p>💡 <strong>웹 접근성</strong>
: 웹 사이트를 사용하는 모든 이용자가 불편함 없이 평등하게 이용할 수 있도록 접근성 자체를 높이는 행위</p>
</blockquote>
<ul>
<li>제목을 의미하는 시멘틱 웹 태그가 사용되었다고 가정해보자.<ul>
<li>HTML 문서를 해석할 때 검색엔진은 해당 제목 요소 내의 내용을 중요한 것으로 인식하고 인덱스에 포함시킬 확률이 높다.</li>
<li>이는 다시 말해, 시멘틱 요소로 구성되어 있는 웹 페이지가 검색 엔진에 더욱 의미론적으로 문서의 정보를 전달할 수 있고, 검색 엔진은 이를 이용하여 보다 효과적으로 '크롤링 &gt; 인덱싱' 과정을 수행할 수 있게 됨을 의미한다.</li>
<li>시멘틱 웹 태그는 기계와 사람 모두에게 웹 페이지의 내용을 명확히 설명하고, 데이터가 더욱 정확히 사용될 수 있게 하므로 웹 접근성을 높인다고 볼 수 있는 것이다.</li>
</ul>
</li>
<li>그리고 이는 더 나아가 검색 엔진이 자신의 웹 사이트를 더욱 검색하기 용이한 구조로 웹 사이트를 조정하는 마케팅 도구인 <strong><em>검색 엔진 최적화(SEO, Search Engine Optimization)</em></strong> 를 가능케 한다.</li>
</ul>
<pre><code>👩‍🏫 시멘틱 웹 태그의 종류에는 아래와 같은 것들이 있습니다.</code></pre><h3 id="✨-header">✨ header</h3>
<ul>
<li><p>소개 및 탐색에 도움을 주는 콘텐츠</p>
</li>
<li><p>제목, 로고, 검색창, 사용자 정보(작성자 이름 등), 메뉴</p>
</li>
<li><p>구획을 생성하지 않는다. 주변의 구획 제목 요소(<strong>h1</strong>~<strong>h6</strong>)를 감싸기 위해 사용되나 필수적인 것은 아니다.</p>
</li>
</ul>
<h3 id="✨-main">✨ main</h3>
<ul>
<li><p>해당 웹 사이트 <strong>body</strong> 요소의 주된 컨텐츠를 나타낸다.</p>
</li>
<li><p><strong>main</strong> 요소의 콘텐츠는 문서의 유일한 내용이어야 한다.</p>
</li>
<li><p>따라서 문서에 하나보다 많은 <strong>main</strong> 요소가 존재하면 안 된다. (hidden 속성이 있는 경우 제외)</p>
</li>
<li><p>또한 페이지의 주요 기능인 경우가 아니라면 여러 페이지에 걸쳐 반복되는 콘텐츠가 포함되면 안 된다.</p>
</li>
<li><p>요소 개요에 영향을 주지 않는다.</p>
</li>
<li><p>페이지의 개념적 구조를 바꾸지 않으며, 오로지 의미론적인 정보 제공 목적으로 사용된다.</p>
</li>
</ul>
<h3 id="✨-footer">✨ footer</h3>
<ul>
<li><p>일반적으로 웹 페이지의 최하단에 위치하여 회사 정보나 저작권 정보 등을 나타낸다.</p>
</li>
<li><p>연락처 정보를 나타내는 <strong>address</strong> 요소를 이곳에 배치한다.</p>
</li>
<li><p><strong>header</strong>, <strong>main</strong>과 마찬가지로 새로운 구획을 생성하지 않는다.</p>
</li>
</ul>
<h3 id="✨-section">✨ section</h3>
<ul>
<li><p>한 문서의 독립적인 구역을 나타낸다.</p>
</li>
<li><p>더 적합한 의미를 가진 요소가 없을 때 사용하는 태그이다.</p>
</li>
</ul>
<h3 id="✨-article">✨ article</h3>
<ul>
<li><p>페이지, 문서, 사이트 등에서 독립적으로 구분하여 배포, 반복 및 재사용할수 있는 구간을 나타낸다.</p>
<ul>
<li>예) 상품 목록, 게시판의 글, 매거진이나 뉴스 기사 등</li>
</ul>
</li>
<li><p>하나의 문서가 여러 개의 <strong>article</strong>을 가질 수 있다.</p>
</li>
<li><p>스크롤을 내리면 계속해서 다음 글을 보여주는 이 블로그의 경우 각각의 글이 하나의 <strong>article</strong> 요소가 된다.</p>
</li>
<li><p><strong>article</strong>을 중첩하여 사용할 수 있다.</p>
<ul>
<li>예를 들어, 이 블로그 글의 댓글을 나타내는 <strong>article</strong>은 이 글을 나타내는 <strong>article</strong> 요소 내부에 위치할 수 있다.</li>
</ul>
</li>
</ul>
<hr />

<ul>
<li><strong>div</strong>, <strong>section</strong>, <strong>article</strong>은 모두 블록 레벨 요소에 속한다.<ul>
<li>따라서 <strong>section</strong>, <strong>article</strong>을 <strong>div</strong>로 바꾸어 사용해도 기능상으로는 문제가 생기지 않는다.</li>
</ul>
</li>
</ul>
<table>
<thead>
<tr>
<th align="center">태그</th>
<th align="center">역할</th>
</tr>
</thead>
<tbody><tr>
<td align="center"><strong>div</strong></td>
<td align="center">순수 컨테이너. 단순 스타일링 목적으로 논리적 연관이 없는 것들을 그룹화할 때 사용</td>
</tr>
<tr>
<td align="center"><strong>section</strong></td>
<td align="center">논리적으로 연관된 요소를 문서상에 분리하여 나타내기 위해 사용</td>
</tr>
<tr>
<td align="center"><strong>article</strong></td>
<td align="center"><strong>section</strong>과 달리 독립적으로 존재할 수 있고 재사용이 가능하다. <strong>section</strong> 보다 조금 더 구체적이다.</td>
</tr>
</tbody></table>
<pre><code class="language-html">&lt;div&gt;
        메인 페이지
        &lt;section&gt;
            스포츠 뉴스
            &lt;article&gt;야구 관련 기사&lt;/article&gt;
            &lt;article&gt;축구 관련 기사&lt;/article&gt;
            &lt;article&gt;농구 관련 기사&lt;/article&gt;
        &lt;/section&gt;

        &lt;section&gt;
            날씨 예보
            &lt;article&gt;오늘의 날씨&lt;/article&gt;
            &lt;article&gt;전국 날씨&lt;/article&gt;
            &lt;article&gt;기상 특보&lt;/article&gt;
        &lt;/section&gt;
&lt;/div&gt;</code></pre>
<h3 id="✨-nav">✨ nav</h3>
<ul>
<li><p>문서의 현재 페이지 내, 또는 다른 페이지로의 링크를 보여주는 구획을 나타낼 때 사용한다.</p>
</li>
<li><p>주로 메뉴, 목차, 색인에 사용된다.</p>
</li>
<li><p>주요 탐색 링크를 위한 요소로, 문서의 '모든' 링크가 <strong>nav</strong> 안에 포함되어 있을 필요는 없다.</p>
</li>
<li><p>하나의 문서가 여러 <strong>nav</strong> 태그를 가질 수 있다.</p>
</li>
<li><p>주로 header 태그 안에 nav 태그를 사용한다.</p>
</li>
</ul>
<h3 id="✨-aside-별도-구획-요소">✨ aside: 별도 구획 요소</h3>
<ul>
<li><p>주된 컨텐츠와 간접적으로만 연계되는 부분을 나타낸다.</p>
</li>
<li><p>주로 사이드 바, 사이드 메뉴, 콜아웃 박스로 표현한다.</p>
</li>
</ul>
<pre><code>인라인 요소인 &lt;img&gt;, &lt;video&gt;, &lt;audio&gt; 태그 또한 시멘틱 웹 태그에 해당한다.</code></pre><h3 id="✨-table">✨ table</h3>
<ul>
<li><p>여러 종류의 데이터를 구분하여 보기 쉽게 정리해주는 일종의 표를 나타내기 위해 사용한다.</p>
</li>
<li><p><strong>table</strong> 내부에는 다양한 콘텐츠가 위치할 수 있다.</p>
</li>
</ul>
<h4 id="💡-caption">💡 caption</h4>
<ul>
<li><p>표의 설명 또는 제목을 나타낸다.</p>
</li>
<li><p><strong>table</strong>의 첫번째 자식이어야 한다.</p>
</li>
</ul>
<h4 id="💡-colgroup">💡 colgroup</h4>
<ul>
<li>표의 열을 그룹화할 때 사용한다.</li>
</ul>
<h4 id="💡-thead-표-머릿글-요소">💡 thead: 표 머릿글 요소</h4>
<ul>
<li>표의 열의 머릿글인 행들의 집합</li>
</ul>
<pre><code class="language-html">&lt;thead&gt;
        &lt;tr&gt;
            &lt;th scope=&quot;col&quot;&gt;Items&lt;/th&gt;
            &lt;th scope=&quot;col&quot;&gt;Expenditure&lt;/th&gt;
        &lt;/tr&gt;
&lt;/thead&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/7b7ea5ff-a19c-4b59-8a47-7f2753fa9005/image.png" /></p>
<ul>
<li>위의 표에서 Items와 Expenditure이 <strong>thead</strong>에 해당한다.</li>
</ul>
<h4 id="💡-tbody-표-본문-요소">💡 tbody: 표 본문 요소</h4>
<ul>
<li><strong>tr</strong>로 나타내지는 표의 여러 행들을 묶어 표의 본문을 구성한다.</li>
</ul>
<h4 id="💡-tfoot">💡 tfoot</h4>
<ul>
<li><p>표의 열을 요약하는 행들의 집합이다.</p>
</li>
<li><p>주석, 색인, 참조, 계(sum) 등이 담기는 부분이다.</p>
</li>
</ul>
<h4 id="💡-tr">💡 tr</h4>
<ul>
<li><p>TableRow. 표의 '행'</p>
</li>
<li><p><strong>th</strong>와 <strong>td</strong>를 묶어 표의 가로줄, 즉 행을 구성한다.</p>
</li>
</ul>
<h4 id="💡-th">💡 th</h4>
<ul>
<li><p>TableHead(data)</p>
</li>
<li><p>해당 셀이 표의 <strong>thead</strong>에 속하는 셀임을 나타낸다.</p>
</li>
<li><p>하나의 칸(제목 열)을 나타내며 중앙정렬, 볼드처리 되어 보여진다.</p>
</li>
</ul>
<h4 id="💡-td">💡 td</h4>
<ul>
<li><p>TableData. 행의 내부를 채우는 '값'</p>
</li>
<li><p>하나의 칸(일반 열)을 나타내며 중앙정렬, 볼드처리 없이 보여진다.</p>
</li>
</ul>
<pre><code>👩‍🏫 또한 표를 나타내기 위해 태그와 함께 사용되는 다양한 속성들도 존재합니다.</code></pre><h4 id="📅-colspan">📅 colspan</h4>
<ul>
<li><p>Columnspan</p>
</li>
<li><p>colspan을 사용하면 정보가 세로(열)로 읽히게 되므로 셀이 왼쪽에서 오른쪽으로 병합된다.</p>
</li>
<li><p>이를 통해 정보를 위에서 아래로 읽을 수 있다.</p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/b218b185-3a34-4589-827c-dd82b2f7459d/image.png" /></p>
<pre><code class="language-html">&lt;td colspan=&quot;2&quot;&gt;ㄱ&lt;/td&gt;</code></pre>
<ul>
<li><p>예시의 상황에서 빈칸은 왼쪽의 'ㄱ'으로 채워진다.</p>
</li>
<li><p>만약 예시와 다르게 표에 빈칸이 없는 경우, 한 칸이 밀린 채로 표시된다.</p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/8a07e0ef-a3b6-4aa3-b521-aa27428981cc/image.png" /></p>
<h4 id="📅-rowspan">📅 rowspan</h4>
<ul>
<li><p>rowspan을 사용하면 정보가 가로(행)로 읽히게 되므로 셀이 위에서 아래로 병합된다.</p>
</li>
<li><p>이를 통해 정보를 왼쪽에서 오른쪽으로(옆으로) 읽을 수 있다.</p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/bb7a6667-f729-43c6-a325-71d8a84d189c/image.png" /></p>
<pre><code class="language-html">&lt;td rowspan=&quot;2&quot;&gt;3&lt;/td&gt;</code></pre>
<ul>
<li><p>예시의 상황에서 빈칸은 위의 '3'으로 채워진다.</p>
</li>
<li><p>만약 예시와 다르게 빈칸이 없는 경우, 한 칸이 밀려 표시된다.</p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/d9b2fc92-7d14-40d7-8518-96256ac7152d/image.png" /></p>
<ul>
<li><p>그리고 만약 &lt;표A&gt;의 색칠된 셀들에 colspan 속성을 주는 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/3f789b44-0019-4610-94f4-78acf280e922/image.png" /></p>
</li>
<li><p>&lt;표B&gt;의 색칠된 셀들에 rowspan 속성을 주는 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/295d9d0d-a0f3-41e0-9a91-22ceac7c508a/image.png" /></p>
</li>
</ul>
<p><strong>아무 변화도 일어나지 않는다.</strong></p>
<h4 id="📅-border">📅 border</h4>
<ul>
<li><p>표에 테두리를 만들어주는 속성이다.</p>
</li>
<li><p>기본값은 none &gt; 테두리가 없는 표</p>
</li>
<li><p>bordercolor 속성을 사용해 테두리의 색상을 지정해주는 것도 가능하다.</p>
</li>
<li><p>셀의 배경색을 바꿔주고 싶다면 bgcolor 속성을 사용하면 된다.</p>
</li>
</ul>
<h4 id="📅-width-height">📅 width, height</h4>
<ul>
<li><p>표의 너비와 높이를 지정해주는 속성이다.</p>
</li>
<li><p>다만, 표의 높이는 내부 값에 따라 자연스럽게 조정되기 때문에 잘 지정하지는 않는다.</p>
</li>
<li><p>width=&quot;50&quot;으로 설정한 경우, 해당 표의 셀 너비는 50px으로 지정된다.</p>
</li>
<li><p>width=&quot;50%&quot;로 설정한 경우, 해당 표는 부모 요소(브라우저 창)의 50%의 크기를 가진다.</p>
</li>
</ul>
<h4 id="📅-align">📅 align</h4>
<ul>
<li><p>값을 정렬하기 위해 사용한다.</p>
</li>
<li><p>align=&quot;center&quot;로 설정한 경우 해당 표의 값들은 중앙 정렬 되어 보여진다.</p>
</li>
</ul>
<h3 id="✨-ul-li">✨ ul, li</h3>
<ul>
<li><p>Unorder List. 순서가 없는 목록을 정의한다.</p>
</li>
<li><p>주로 메뉴 혹은 반복되는 아이템들을 하나로 묶기 위해 사용한다.</p>
</li>
<li><p><strong>ul</strong>의 요소에 해당하는 아이템들은 <strong>li</strong> 태그를 이용해 정의한다.</p>
</li>
</ul>
<pre><code class="language-html">음료
    &lt;ul&gt;
        &lt;li&gt;커피☕&lt;/li&gt;
            &lt;ul&gt;
                &lt;li&gt;아메리카노&lt;/li&gt;
                &lt;li&gt;카페라떼&lt;/li&gt;
                &lt;li&gt;카페모카&lt;/li&gt;
            &lt;/ul&gt;
        &lt;li&gt;차🫖&lt;/li&gt;
            &lt;ul&gt;
                &lt;li&gt;루이보스&lt;/li&gt;
                &lt;li&gt;얼그레이&lt;/li&gt;
                &lt;li&gt;페퍼민트&lt;/li&gt;
            &lt;/ul&gt;
    &lt;/ul&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/1136fd3f-1787-489a-b745-389d34d432bb/image.png" /></p>
<ul>
<li>목록은 기본적으로 불릿의 형태를 가진다. (예시 참조)</li>
</ul>
<blockquote>
<p>🔴 <strong>불릿</strong>: 텍스트 앞에 주의를 끌기 위해 붙이는 기호</p>
</blockquote>
<h3 id="✨-ol-li">✨ ol, li</h3>
<ul>
<li><p>Order List. 순서가 있는 목록을 정의한다. 보통 숫자 목록으로 표현한다.</p>
</li>
<li><p><strong>ol</strong> 요소에 대해 사용할 수 있는 속성들이 있다.</p>
</li>
</ul>
<h4 id="💡-type">💡 type</h4>
<ul>
<li><p>항목을 셀 때 사용할 마커를 지정한다.</p>
</li>
<li><p>기본값은 숫자로 설정되어 있으며, 알파벳 대소문자(&quot;A&quot;, &quot;a&quot;), 로마 숫자 대소문자(&quot;I&quot;, &quot;i&quot;)로 변경할 수 있다.</p>
</li>
<li><p>하위의 모든 <strong>li</strong> 요소들에게 적용되나, 개별 type이 지정된 <strong>li</strong>가 있다면 그 요소에는 해당 값이 사용된다.</p>
</li>
</ul>
<h4 id="💡-start">💡 start</h4>
<ul>
<li><p>항목을 셀 때 시작할 수를 지정한다.</p>
</li>
<li><p>아라비아 숫자로 나타낸 정수로만 지정 가능하므로, type을 바꾼 경우에도 숫자를 사용하여 지정해주어야 한다.</p>
</li>
</ul>
<h4 id="💡-reversed">💡 reversed</h4>
<ul>
<li><p>목록의 순서 역전 여부를 지정한다. (역순 배치 여부)</p>
</li>
<li><p><strong>ul</strong>과 <strong>ol</strong>은 서로 중첩 가능하다.</p>
</li>
</ul>
<h3 id="✨-dl-dt-dd">✨ dl, dt, dd</h3>
<h4 id="💡-dl">💡 dl</h4>
<ul>
<li><p>Description List. 제목과 설명이 있는 목록을 정의한다.</p>
</li>
<li><p>주로 용어 사전을 구현하거나 메타데이터(키-값 쌍의 목록)를 표현할 때 사용한다.</p>
</li>
</ul>
<h4 id="💡-dt">💡 dt</h4>
<ul>
<li><p>Definition Term. 설명/정의 목록에서 제목(용어)을 나타내기 위해 사용한다.</p>
</li>
<li><p>일반적으로는 <strong>dt</strong> 하단에 <strong>dd</strong>가 위치하지만 여러 개의 <strong>dt</strong> 요소를 연속해 배치하고 하나의 <strong>dd</strong>로 설명해주는 것도 가능하다.</p>
</li>
</ul>
<h4 id="💡-dd">💡 dd</h4>
<ul>
<li><strong>dt</strong>에 대한 설명, 정의 또는 값을 나타내기 위해 사용한다.</li>
</ul>
<h3 id="✨-figure-figcaption">✨ figure, figcaption</h3>
<h4 id="💡-figure">💡 figure</h4>
<ul>
<li><p>웹 페이지 내에 이미지, 삽화, 도표, 코드 조각 등을 삽입하기 위해 사용한다.</p>
</li>
<li><p>그림을 표현하기 위해 사용되기는 하지만 인라인 요소인 <strong>img</strong> 태그와는 차이가 있다.</p>
</li>
<li><p><strong>figure</strong>은 구획 요소이므로, 하나의 플로우 콘텐츠를 소개할 뿐 실제로 이미지를 렌더링해오지는 않는다.</p>
</li>
</ul>
<h4 id="💡-figcaption">💡 figcaption</h4>
<ul>
<li>부모 <strong>figure</strong> 요소가 포함하는 콘텐츠에 대한 설명을 나타낸다.</li>
</ul>
<pre><code class="language-html">&lt;figure&gt;
    &lt;img src=&quot;이미지 주소&quot; alt=&quot;이미지 대체 텍스트&quot;&gt;
    &lt;figcaption&gt;이것은 그림에 대한 설명입니다.&lt;/figcaption&gt;
&lt;/figure&gt;</code></pre>
<h3 id="✨-pre">✨ pre</h3>
<ul>
<li>미리 서식을 지정한 텍스트를 나타내며, HTML에 작성한 내용을 그대로 나타낸다.</li>
</ul>
<blockquote>
<p><strong>p</strong>를 사용한 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/22d516d0-9d5b-4ae3-aaf8-698bd889d398/image.png" /></p>
</blockquote>
<blockquote>
<p><strong>pre</strong>를 사용한 경우
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/2dc50d0f-d291-404d-a667-d6fa9c982600/image.png" /></p>
</blockquote>
<ul>
<li><strong>pre</strong>를 사용하면 예시와 같이 요소 내 공백문자(tab, enter)들이 그대로 표현된다.</li>
</ul>
<h3 id="✨-blockquote-인용-블록-요소">✨ blockquote: 인용 블록 요소</h3>
<ul>
<li><p>내부의 텍스트가 긴 인용문임을 나타내기 위해 사용한다.</p>
</li>
<li><p>주로 들여쓰기를 한 상태로 표현되고, CSS를 사용하여 외형을 바꾸어줄 수 있다.</p>
</li>
<li><p>cite 속성을 사용해 인용 URL을 나타내거나 <strong>cite</strong> 요소를 활용하여 출처 텍스트를 제공할 수 있다.</p>
</li>
</ul>
<pre><code class="language-html">&lt;p&gt;paragraph&lt;/p&gt;

&lt;blockquote&gt;
     &lt;p&gt;
            내가 표현하고 싶은 것은, 감상적이고 우울한 것이 아니라 뿌리 깊은 고뇌다. 
            내 그림을 본 사람들이, 이 화가는 정말 격렬하게 고뇌하고 있다고 말할 정도의 경지에 이르고 싶다.
            어쩌면 내 그림의 거친 특성 때문에 더 절실하게 감정을 전달할 수 있을지도 모른다.
            나의 모든 것을 바쳐서 그런 경지에 이르고 싶다.
            그것이 나의 야망이다.
     &lt;/p&gt;
&lt;/blockquote&gt;

&lt;p&gt;paragraph&lt;/p&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/d7aafa3f-dd9c-4aeb-bd84-7ed1c6afc985/image.png" /></p>
<h3 id="✨-details">✨ details</h3>
<ul>
<li><p>'열림' 상태일 때만 내부 정보를 보여주는 정보 공개 요소를 만들기 위해 사용한다.</p>
</li>
<li><p>보통 레이블 옆의 작은 삼각형을 클릭하면, 이것이 돌아가면서 열림/닫힘 상태를 나타낸다.</p>
</li>
<li><p><strong>summary</strong> 속성을 사용하여 열리지 않은 상태에서 보여질 요약이나 레이블을 설정할 수 있다.</p>
</li>
<li><p>false(보이지 않는 상태)를 기본값으로 가지며, open 속성을 사용하면 처음부터 열린 상태로 만들어 줄 수 있다.</p>
</li>
</ul>
<pre><code class="language-html">&lt;details&gt;
     &lt;summary&gt;details summary&lt;/summary&gt;
     details 내부 콘텐츠
&lt;/details&gt;</code></pre>
<blockquote>
<p>기본 상태
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/3e96502a-bf05-4fa8-b668-d5735dd15df6/image.png" /></p>
</blockquote>
<blockquote>
<p>open
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/cbf3a681-445c-44ea-adbe-26af2cdefc49/image.png" /></p>
</blockquote>
<h3 id="✨-hr">✨ hr</h3>
<ul>
<li>주제의 변경, 장면의 전환 등을 나타내기 위한 수평 가로선을 그을 때 사용한다.</li>
</ul>
<pre><code class="language-html">&lt;p&gt;
This is the first paragraph of text.
&lt;/p&gt;

&lt;hr&gt;

&lt;p&gt;
This is second paragraph of text.
&lt;/p&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/7452a550-50e6-4821-9dad-fe6aacd2a5f0/image.png" /></p>
<hr />

<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://developer.mozilla.org/ko/docs/Web/HTML/Element/">HTML 요소 참고서</a></li>
<li><a href="https://dasima.xyz/div-vs-span-vs-p-%EC%B0%A8%EC%9D%B4%EB%8A%94-%EB%B8%94%EB%A1%9D-%EC%9A%94%EC%86%8C%EC%99%80-%ED%8F%AC%ED%95%A8-%EC%9C%A0%EB%AC%B4/">div, span, p 차이</a></li>
<li><a href="https://poiemaweb.com/html5-semantic-web">Semantic Web</a></li>
</ul>