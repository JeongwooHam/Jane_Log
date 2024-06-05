<pre><code>👩‍🏫 &lt;form&gt; 태그 또한 앞서 설명했던 블록 레벨 요소에 속하지만, 
다루어야 할 내용이 많아 별도의 문서에서 설명하려 합니다.
덧붙여, &lt;form&gt;과 관련된 다양한 요소들 또한
앞의 두 문서에서 구분하여 여기서 자세히 알아봅시다!</code></pre><h2 id="🧐-form-태그란-무엇인가">🧐 form 태그란 무엇인가!</h2>
<ul>
<li><strong>form</strong> 태그는 정보를 제출하기 위한 대화형 컨트롤을 포함하는 문서 구획을 나타낸다.</li>
<li>사용자가 의견이나 정보를 입력하고 제출 버튼을 누르면 해당 데이터를 백엔드 서버로 전송한다.</li>
<li>웹 서버는 해당 데이터를 처리하고, 결과에 따른 다른 웹 페이지를 보여준다.</li>
</ul>
<blockquote>
<p><strong>조금 더 구체적인 form 요소의 동작 방법</strong></p>
</blockquote>
<pre><code>1️⃣ &lt;form&gt;이 포함된 웹 페이지에서 &lt;form&gt;에 대응하는 값을 입력한다.

2️⃣ 웹 브라우저는 입력된 데이터를 모두 웹 서버로 보낸다.

3️⃣ 웹 서버는 이 값을 웹 프로그램으로 넘겨 처리하도록 한다.

4️⃣ 웹 프로그램은 처리한 결과에 따른 새로운 HTML 페이지를 웹 서버로 보낸다.

5️⃣ 웹 서버는 받은 HTML 페이지를 웹 브라우저로 보낸다.

6️⃣ 웹 브라우저는 받은 HTML 페이지를 화면에 보여준다.
</code></pre><ul>
<li><strong>form</strong> 태그는 다양한 속성을 가지는데, 우리는 이를 통해 입력 받은 정보를 어디로 어떻게 전송할지 설정할 수 있다.</li>
<li>그 중 중요한 두 속성 action과 method에 대해 알아보자.</li>
</ul>
<h2 id="💡-action과-method">💡 action과 method</h2>
<h3 id="🛠️-action">🛠️ action</h3>
<ul>
<li><p>form이 submit 되었을 때 데이터가 향하는 주소, 경로를 의미한다.</p>
</li>
<li><p>양식 데이터를 처리할 프로그램의 URL을 입력한다.</p>
</li>
</ul>
<h3 id="🛠️-method">🛠️ method</h3>
<ul>
<li><p>데이터를 서버에 전송할 때 사용할 HTTP 방식을 정의한다.</p>
</li>
<li><p>메소드는 웹 브라우저로부터 form 데이터를 가져와 웹 서버로 보내는 기능을 수행한다.</p>
</li>
</ul>
<p>-메소드에는 get, post 두 종류가 있는데 전달 방식에 차이가 있다.</p>
<h4 id="✨-get">✨ GET</h4>
<ul>
<li><p>주소에 데이터를 실어서 전달하는 방식으로 action URL과 ? 뒤에 데이터를 이어 붙여서 전송한다.</p>
</li>
<li><p>데이터가 Header에 위치한다.</p>
</li>
<li><p>post 방식과 달리 body가 별도로 존재하지 않고 
URL 끝에 데이터를 직접 붙여 전송하므로 데이터가 외부에 노출되어 보안에 취약하다.</p>
</li>
<li><p>예) 백엔드 서버 주소가 <a href="http://www.jw.com/api/user/signup%EC%9D%BC%EB%95%8C">www.jw.com/api/user/signup일때</a></p>
</li>
</ul>
<blockquote>
<p><a href="http://www.jw.com/api/user/signup?user_email=a@naver.com&amp;user_password=1234">www.jw.com/api/user/signup?user_email=a@naver.com&amp;user_password=1234</a></p>
</blockquote>
<ul>
<li><p>user_email이라는 key에 <a href="mailto:a@naver.com">a@naver.com</a>이라는 value, user_password라는 key에 1234라는 value를 담고, 보내야 할 key와 value가 여러 개인 경우 단순히 &amp;를 사용해 이어주기 때문에 ID와 비밀번호라는 중요한 개인정보가 노출될 가능성이 높다.</p>
</li>
<li><p>따라서 get 방식은 지정된 리소스로부터 정보를 읽어올 때 주로 사용한다.</p>
</li>
<li><p>보안이 필요 없는 상품 정보 조회 등이 그 예시이다.</p>
<ul>
<li>예) <a href="http://www.shoppingmall.com/cloth?color=red">www.shoppingmall.com/cloth?color=red</a></li>
<li>의류 쇼핑몰 웹 브라우저가 빨간 색 옷들의 정보를 조회하는 경우</li>
</ul>
</li>
</ul>
<h4 id="✨-post">✨ POST</h4>
<ul>
<li><p>http request message의 body 안에 데이터를 실어 전달하는 방식이다.</p>
</li>
<li><p>데이터가 Body에 존재한다.</p>
</li>
<li><p>예) 백엔드 서버 주소가 <a href="http://www.jw.com/api/user/signup%EC%9D%BC%EB%95%8C">www.jw.com/api/user/signup일때</a></p>
</li>
</ul>
<blockquote>
<p><a href="http://www.jw.com/api/user/signup">www.jw.com/api/user/signup</a></p>
</blockquote>
<ul>
<li>데이터가 보이지 않도록 내부적으로 전송하므로 저장 시 많이 사용한다.</li>
</ul>
<hr />

<ul>
<li><p>백엔드에 데이터를 요청할 수 있는 다양한 라이브러리 등의 등장으로 JSP와 같은 서블릿이 아니라면 action과 method는 거의 사용하지 않는 속성이 되었다.</p>
</li>
<li><p>그럼에도 <strong>form</strong> 태그가 사용되는 주된 이유는 submit 이벤트 발생 시 <strong>form</strong> 내부 <strong>input</strong>의 값을 가져올 수 있고, enter 키를 누르면 submit 이벤트를 자동으로 실행시키기 때문이다.</p>
</li>
<li><p>따라서 enter 키를 누르면 알림 창을 노출시키는 등의 이벤트를 발생시키기 위해 <strong>form</strong> 태그가 자주 사용된다.</p>
</li>
<li><p>더 나아가 <strong>form</strong> 요소를 구성하는 다양한 요소들이 존재한다.</p>
</li>
</ul>
<h2 id="🤖-form을-구성하는-다양한-요소들">🤖 form을 구성하는 다양한 요소들</h2>
<h3 id="✨-input">✨ input</h3>
<ul>
<li>사용자가 입력할 수 있는 다양한 공간을 만들어주는 인라인 요소이다.</li>
</ul>
<blockquote>
<p><strong>input</strong>에 사용할 수 있는 다양한 속성들</p>
</blockquote>
<h4 id="💡-type">💡 type</h4>
<ul>
<li><p>태그 모양을 다양하게 변경할 수 있다.</p>
<ul>
<li>radio, button, submit checkbox, text, password, email, number, ...</li>
<li>radio: 단일 선택만 가능 / checkbox: 다중 선택 가능</li>
</ul>
</li>
<li><p>이 속성을 통해 해당 input이 어떠한 기능을 하고 있는 태그인지 명확히 명시해 줄 수 있다.</p>
<ul>
<li>default value: &quot;text&quot;</li>
</ul>
</li>
<li><p>단일속성으로 자식을 가질 수 없다.</p>
</li>
</ul>
<h4 id="💡-name">💡 name</h4>
<ul>
<li>태그 이름을 지정한다.</li>
</ul>
<h4 id="💡-maxlength">💡 maxlength</h4>
<ul>
<li>해당 태그의 최대 글자 수를 지정한다.</li>
</ul>
<h4 id="💡-required">💡 required</h4>
<ul>
<li><p>해당 태그를 필수태그로 지정한다.</p>
</li>
<li><p>해당 태그에 대한 값을 입력하지 않고 submit 버튼을 누르면 에러 메세지가 화면에 출력된다.</p>
</li>
</ul>
<h4 id="💡-placeholder">💡 placeholder</h4>
<ul>
<li>태그에 입력할 값에 대한 힌트를 준다.</li>
</ul>
<h3 id="✨-button">✨ button</h3>
<ul>
<li><p>클릭 가능한 버튼을 나타내는 인라인 요소이다.</p>
</li>
<li><p>default type = &quot;submit&quot;</p>
<ul>
<li>백엔드로 데이터를 전송하는 액션을 일으켜야 할 때 주로 사용한다.</li>
</ul>
</li>
<li><p><strong>button</strong>의 type을 submit 액션이 일어나지 않는 'button'으로 지정할 수 있다.</p>
<pre><code class="language-html">&lt;button type=&quot;button&quot;&gt;버튼&lt;/button&gt;</code></pre>
</li>
</ul>
<p>1) </p>
<pre><code class="language-html">&lt;button&gt;...&lt;/button&gt; (type=&quot;submit&quot;)</code></pre>
<ul>
<li><strong>button</strong>의 기본값으로, 버튼이 서버로 양식 데이터를 제출한다.</li>
</ul>
<p>2) </p>
<pre><code class="language-html">&lt;button type=&quot;button&quot;&gt;...&lt;/button&gt;</code></pre>
<ul>
<li>클릭하더라도 아무 액션이 발생하지 않는다.</li>
</ul>
<p>3) </p>
<pre><code class="language-html">&lt;input type=&quot;button&quot;/&gt;</code></pre>
<ul>
<li><p><strong>button</strong> 태그가 존재하지 않았던 HTML 4.0 표준 이전에 사용된 방식이다.</p>
</li>
<li><p><strong>button</strong>은 이 코드가 하던 역할을 이어 받아 나중에 탄생한 태그이다.</p>
</li>
<li><p><strong>button</strong>을 사용한 버튼과 <strong>input</strong>을 사용한 버튼의 기능은 동일하지만 활용성 측면에서 <strong>button</strong>이 더 우월하다.</p>
<ul>
<li><strong>input</strong>은 열린 태그라 자식을 가질 수 없는 반면 <strong>button</strong>은 자식을 가질 수 있고 CSS에서 가상 선택자로 꾸며주는 것도 가능하다.</li>
<li>즉, <strong>button</strong>을 통해 다양한 이미지와 텍스트가 포함된 버튼을 생성할 수 있다.</li>
</ul>
</li>
</ul>
<h3 id="✨-label">✨ label</h3>
<ul>
<li><p>사용자 인터페이스 요소들의 설명을 정의할 때 사용하는 인라인 요소이다.</p>
</li>
<li><p>for 속성을 사용하여 다른 요소와 결합할 수 있다.</p>
<ul>
<li>이때 <strong>label</strong>의 for 속성값이 결합하고자 하는 요소의 id 속성값과 같아야 한다.</li>
<li>이 경우 사용자가 해당 텍스트만 클릭하더라도 <strong>label</strong> 요소와 연결된 요소를 곧바로 클릭하는 것과 같은 효과를 준다.</li>
</ul>
</li>
</ul>
<pre><code class="language-html">&lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;0&quot;/&gt; 남성
&lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;1&quot; id=&quot;female&quot;/&gt;
     &lt;label for=&quot;female&quot;&gt; 여성 &lt;/label&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/99cae87f-dbe6-463e-9dc3-18c6e3eaebdd/image.png" /></p>
<ul>
<li><p>이러한 특성을 사용하여, checkbox의 속성을 그대로 유지하되 모양만 바꾸려 할 때 해당 체크박스가 보이지 않게 CSS 로 설정한 후 해당 위치에 <strong>label</strong> 태그를 두어 별도로 설정한 다른 이미지 영역을 클릭해도 <strong>label</strong>과 연결된 기존의 checkbox가 클릭되는 효과가 나게 할 수 있다.</p>
</li>
<li><p>또는 <strong>label</strong> 요소를 결합하고자 하는 요소 내부에 위치시키면 for 속성 없이도 해당 요소와 결합시킬 수 있다.</p>
</li>
</ul>
<h3 id="✨-fieldset-legend">✨ fieldset, legend</h3>
<h4 id="💡-fieldset">💡 fieldset</h4>
<ul>
<li><p>웹 양식의 여러 컨트롤과 <strong>label</strong>을 묶을 때 사용하는 블록 레벨 요소이다.</p>
</li>
<li><p><strong>form</strong> 안에서 <strong>form</strong>의 요소들을 그룹화할 때 사용한다.</p>
</li>
</ul>
<h4 id="💡-legend">💡 legend</h4>
<ul>
<li><strong>fieldset</strong> 하위에서 그룹화한 <strong>form</strong> 요소들에 대해 목적에 맞는 이름을 지정한다.</li>
</ul>
<pre><code class="language-html">&lt;form&gt;
    &lt;fieldset&gt;
      &lt;legend&gt;Your Favorite Sports&lt;/legend&gt; 
      &lt;input type=&quot;radio&quot; id=&quot;soccer&quot; name=&quot;sports&quot; value=&quot;0&quot;/&gt;
      &lt;label for=&quot;soccer&quot;&gt;soccer&lt;/label&gt; &lt;br&gt;
      &lt;input type=&quot;radio&quot; id=&quot;baseball&quot; name=&quot;sports&quot; value=&quot;1&quot;/&gt;
      &lt;label for=&quot;baseball&quot;&gt;baseball&lt;/label&gt; &lt;br&gt;
      &lt;input type=&quot;radio&quot; id=&quot;basketball&quot; name=&quot;sports&quot; value=&quot;2&quot;/&gt;
      &lt;label for=&quot;basketball&quot;&gt;basketball&lt;/label&gt; &lt;br&gt;
    &lt;/fieldset&gt;
  &lt;/form&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/26e767b0-03d4-4287-8f67-d201fdc5bf6f/image.png" /></p>
<h3 id="✨-select-option-optgroup">✨ select, option, optgroup</h3>
<h4 id="💡-select">💡 select</h4>
<ul>
<li><p>항목을 선택할 수 있는 드롭다운 메뉴를 정의하는 인라인 요소이다.</p>
</li>
<li><p>선택됐을 때 값으로써 사용할 value라는 속성을 가진다.</p>
</li>
<li><p>지정된 value 값이 없는 경우 안의 텍스트를 값으로 사용한다.</p>
</li>
<li><p>예) 이메일 회원가입 시 이메일을 선택하는 드롭다운 메뉴</p>
</li>
</ul>
<h4 id="💡-option">💡 option</h4>
<ul>
<li><strong>select</strong>, <strong>optgroup</strong>, <strong>datalist</strong> 요소의 항목을 정의한다.</li>
</ul>
<h4 id="💡-optgroup">💡 optgroup</h4>
<ul>
<li><p><strong>select</strong> 태그 안의 목록들을 그룹화할 때 사용한다.</p>
</li>
<li><p><strong>optgroup</strong> 하위에 <strong>option</strong> 요소들이 포함된다.</p>
</li>
</ul>
<pre><code class="language-html">&lt;div&gt;
      취미:
      &lt;select&gt;
          &lt;option value=&quot;0&quot;&gt;농구&lt;/option&gt;
          &lt;option value=&quot;1&quot;&gt;축구&lt;/option&gt;
          &lt;option value=&quot;2&quot;&gt;야구&lt;/option&gt;
      &lt;/select&gt;
&lt;/div&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/1b2de0fa-a2ba-4f06-b996-0e20d9c2923f/image.png" /></p>
<h3 id="✨-textarea">✨ textarea</h3>
<ul>
<li><p>여러 줄을 입력받기 위해 사용하는 인라인 요소이다.</p>
</li>
<li><p>rows 속성으로 줄을, cols 속성으로 한 줄에 입력받을 크기를 설정한다.</p>
</li>
</ul>
<pre><code class="language-html">&lt;textarea placeholder=&quot;작성해주세요&quot; cols=&quot;50&quot; rows=&quot;50&quot;&gt;
    &lt;!--엔터 친 만큼 textarea 안에 빈칸으로 표시--&gt;
    반갑습니다.
    &lt;!--엔터 친 만큼 textarea 안에 빈칸으로 표시--&gt;
&lt;/textarea&gt;</code></pre>
<ul>
<li>기본 화면에서 보여질 텍스트를 설정할 수 있다. 입력된 여백(tab, enter)이 그대로 보여진다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/dd316b2f-f035-429e-9730-53e9fa474d8e/image.png" /></p>
<ul>
<li>위의 텍스트를 지우면 미리 설정해둔 placeholder 속성값이 보여진다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/f3fb287e-7c23-4558-8a45-e26258be17a2/image.png" /></p>
<h3 id="✨-datalist">✨ datalist</h3>
<ul>
<li><p>검색이 가능한 (미리보기가 가능한) input(사용자 입력) 태그이다. (인라인 요소)</p>
</li>
<li><p>텍스트 상자에 입력할 값 후보 목록을 설정해둘 수 있다.</p>
</li>
</ul>
<pre><code class="language-html">// list = datalist 태그의 id 속성값
&lt;input type=&quot;text&quot; list=&quot;data&quot; /&gt;

// id = 속성값
&lt;datalist id=&quot;data&quot;&gt;
     &lt;option&gt;축구&lt;/option&gt;
     &lt;option&gt;농구&lt;/option&gt;
     &lt;option&gt;야구&lt;/option&gt;
&lt;/datalist&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/5a407feb-5cb4-428a-8b06-82b5f738109a/image.png" /></p>
<h3 id="✨-dialog-대화-상자-요소">✨ dialog: 대화 상자 요소</h3>
<ul>
<li><p>닫을 수 있는 경고창, 대화 상자 등 상호작용 가능한 요소를 만들기 위해 사용하는 블록 레벨 요소이다.</p>
</li>
<li><p><strong>dialog</strong>를 사용하여 웹 페이지 상에 팝업 창을 만들 수 있다.</p>
</li>
<li><p>open 속성을 통해 해당 요소가 활성화 상태이고 상호작용이 가능함을 나타낸다.</p>
<ul>
<li>open 속성이 없을 경우 해당 요소가 사용자에게 보여지지 않는다.</li>
</ul>
</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://www.nextree.co.kr/p8428/">HTML: 폼의 이해</a></li>
<li><a href="https://nykim.work/96">버튼에 타입을 쓰는 이유</a></li>
</ul>