<pre><code>👩‍🏫 평소에는 아무 생각 없이 사용해왔던 웹 페이지들은 사실 모두 박스 형태의 구조를 가지고 있었습니다!</code></pre><img src="https://velog.velcdn.com/images/hamjw0122/post/80c24a64-c214-423a-946e-2a52377bf880/image.png" width="30%" />

<p>'개발자 창(F12) &gt; ctrl + shift + c'를 통해 보면, 일반적으로 우리가 보던 화면이 어떻게 구조화되어 있는지 알 수 있다.</p>
<p>그리고 이처럼 웹 페이지 상의 내용을 구조화하기 위해 사용하는 코드,</p>
<p>웹 페이지의 기초 틀을 만들 때 쓰는 언어가 바로</p>
<p><strong><em>HTML</em></strong>이다.</p>
<h2 id="🧐-what-is-hypertext-markup-language">🧐 What is HyperText Markup Language?</h2>
<h3 id="📑-hyper-text">📑 Hyper Text</h3>
<ul>
<li>단일 선형 플로(≒소설 속의 한 문장)와 대비되는 개념</li>
<li>사용자에게 비순차적인 검색을 할 수 있도록 제공되는 텍스트</li>
<li>문서 속의 특정 자료가 다른 자료나 데이터베이스와 연결되어 있어 현재 페이지의 글과 이미지 등을 초월하여 다른 웹 페이지의 자료들과 연결시켜주기 때문에 사용자는 여러 페이지를 넘나들며 원하는 정보를 얻을 수 있다.</li>
<li>하이퍼 텍스트 문서들은 주로 마우스 클릭, 스크린 터치 등으로 활성화되는 하이퍼링크를 통해 서로 연결되어 있다.</li>
<li>하이퍼 '텍스트'이기는 하지만 사실 이는 단순히 '글'에 국한된 개념이 아니라 하이퍼링크를 통해 통합되어 있는 표, 그림, 그리고 다른 표상적인 콘텐츠 형식들을 묘사할 때도 사용되는 용어이다.</li>
<li>웹 페이지에서 실행됨으로써, 하이퍼텍스트는 사용자들로 하여금 인터넷상에 사용하기 편한 정보를 공개할 수 있게 한다.</li>
</ul>
<h3 id="📑-markup-language">📑 Markup Language</h3>
<ul>
<li>태그 등을 이용하여 문서의 (문단과 같은) 논리적 구조를 보여주고 특히 인터넷상의 송신과 표현과 관련된 페이지의 레이아웃에 대한 설명을 제공하는 체계</li>
<li>원래 태그는 원고의 교정 부호와 주석을 표현하기 위해 텍스트와는 별도로 사용되었으나 용도의 확장으로 이제는 문서의 구조를 표현하는 역할을 하게 되었다.</li>
<li>쉽게 말해, 웹 페이지 상의 콘텐츠를 어떻게 표현할지 명령하는 언어라고 할 수 있다.</li>
</ul>
<pre><code>👩‍🏫 즉, HTML 이란 우리가 보는 웹페이지가 어떻게 구조화되어 있는지 
브라우저로 하여금 알 수 있도록 하는 마크업 언어입니다.

일반적으로 데이터를 기술하는 정도로만 사용되므로 사실 프로그래밍 언어는 아닙니다!

또한 웹 페이지의 기초 틀을 만들 때 사용되는 언어로, 꾸미는 역할(style sheet)을 하지는 않습니다.</code></pre><h2 id="🤖-visual-studio-code">🤖 Visual Studio Code</h2>
<p>HTML은 메모장이나 글을 작성할 수 있는 곳 어디에서든 사용이 가능하지만</p>
<p>다양한 기능을 제공하지 않고 투박한 GUI를 가지고 개발해야 하므로</p>
<p>자동완성, 자동줄 바꿈과 같은 다양한 플러그인을 제공하고 개발에 용이한 GUI를 제공하는 에디터 툴을 사용하는 것이 편리하다.</p>
<p>다양한 에디터 툴 중 내가 선택한 것은 VSCode로,</p>
<p>마이크로소프트에서 제작한 텍스트 에디터이다.</p>
<img src="https://velog.velcdn.com/images/hamjw0122/post/4f5630f0-bc4c-4f5d-beb7-a35e42ae8fed/image.png" width="50%" />


<p>홈페이지에서 내 운영체제에 맞는 버전을 다운로드한 후,</p>
<p>사용을 더 편하게 할 수 있도록 해주는 다양한 확장 플러그인을 설치하였다.</p>
<img src="https://velog.velcdn.com/images/hamjw0122/post/62dd8757-d678-4fe3-b2e9-f7a40d9bdb11/image.png" width="50%" />

<p>표시된 부분을 클릭하여 다양한 확장 플러그인을 설치할 수 있다.</p>
<h3 id="🌟-korean-language-pack">🌟 Korean Language Pack</h3>
<img src="https://velog.velcdn.com/images/hamjw0122/post/53043b51-c9a1-45c2-9a8f-92f6ee53fb0a/image.png" width="30%" />

<ul>
<li>직관적인 이름에서 바로 유추할 수 있듯 언어를 한글로 설정할 수 있게 해준다.</li>
</ul>
<h3 id="🌟-live-server">🌟 Live Server</h3>
<img src="https://velog.velcdn.com/images/hamjw0122/post/b077b1f3-b7ec-4435-b704-14277b8f82d1/image.png" width="30%" />

<p>대표사진 삭제
사진 설명을 입력하세요.</p>
<ul>
<li><p>작성한 코드를 실시간으로 수정 및 실행 가능하도록 하는 플러그인이다.</p>
</li>
<li><p>단축키: [alt + L + O]</p>
</li>
<li><p>프로그램이 실행되는 브라우저를 변경하는 방법은 아래와 같다. (예를 들면, Internet Explorer에서 Chrome으로)</p>
</li>
</ul>
<img src="https://velog.velcdn.com/images/hamjw0122/post/1d211bbf-4830-4d74-8cb3-9729744ba3aa/image.png" width="60%" />

<pre><code>설정 &gt; live server 검색 &gt; Custom Browser</code></pre><p>3) Auto Rename Tag</p>
<img src="https://velog.velcdn.com/images/hamjw0122/post/d7e2f271-b083-4080-8ac2-8b5be661b511/image.png" width="30%" />

<ul>
<li>다음 글에서 더 자세히 기술하겠지만 HTML은 아래와 같은 tag의 형태를 가진다.</li>
</ul>
<p><code><시작태그명> ... 내용물(content) </code></p>
<ul>
<li>해당 플러그인을 설치하면 시작태그명 변경 시 종료태그명이 자동으로 수정된다.</li>
</ul>
<p>4) Prettier-Code Formatter</p>
<img src="https://velog.velcdn.com/images/hamjw0122/post/dfa264c7-dfa7-4672-b9ff-6f203fd5de44/image.png" width="30%" />

<ul>
<li>코드의 모양을 규칙에 맞추어 예쁘게 바꿔주는 역할을 한다.</li>
</ul>
<p>; 자동 줄바꿈, 자동 여백, 코드 종료 문자 자동 입력, 코드의 통일성 유지</p>
<ul>
<li>이는 단순히 개인의 프로그래밍을 편리하게 해주는 것에서 더 나아가</li>
</ul>
<p>협업관계에 있어서 코드를 작성할 때 같은 코드 포맷팅을 할 수 있도록 도와주는 역할도 한다.</p>
<h2 id="🦴-the-structure-of-html">🦴 The Structure of HTML</h2>
<p>본격적으로 HTML 문서를 제작하기에 앞서,</p>
<p>HTML의 기본 소스인 기본 템플릿을 입력해주어야 한다.</p>
<p>모두 외워서 타이핑 할 필요 없이, !를 타이핑 후 Tab키를 눌러주면</p>
<img src="https://velog.velcdn.com/images/hamjw0122/post/e5615a29-f3a3-4193-858a-b77fdf56345f/image.png" width="50%" />

<p>아래와 같은 HTML 기본 템플릿이 자동생성된다.</p>
<img src="https://velog.velcdn.com/images/hamjw0122/post/c14f80f8-a1c7-4d47-ab12-3a8d6e66751b/image.png" width="50%" />

<p>이는 VSCode에서 Emmet이라는 기능을 지원하기 때문에 가능하다.</p>
<p>Emmet이란 특정 문자를 타이핑하면 자동으로 나머지 코드들을 알아서 생성해줌으로써</p>
<p>코딩을 훨씬 빠르게 할 수 있도록 하는 자동완성기능이다.</p>
<p>기본 템플릿 생성을 완료했다면, 먼저 템플릿 속 각각의 코드들이 어떤 의미를 가지는지 알아보도록 하자.</p>
<pre><code class="language-html">&lt;!DOCTYPE html&gt;</code></pre>
<h3 id="💡-문서-형식-선언document-type-declaration">💡 문서 형식 선언(Document Type Declaration)</h3>
<ul>
<li>DOCTYPE 선언은 HTML 태그는 아니지만, 선언된 페이지의 HTML 버전이 무엇인지를 웹 브라우저에 알려주는 역할을 하는 선언문이다.</li>
<li>해당 코드는 HTML 문서에서 <strong>html</strong> 태그를 정의하기 전, 가장 먼저 선언되어야 한다.</li>
<li>DOCTYPE이 선언을 하지 않았거나 오류가 있으면 웹 브라우저는 문서를 쿼크 모드(Quirks Mode)로 해석한다.</li>
<li>이 경우 같은 코드를 실행하더라도 웹 브라우저마다 서로 다르게 해석하므로 웹 브라우저마다 전혀 다른 결과물이 나온다는 문제점이 생긴다.</li>
<li>하지만 문서 형식 선언이 있는 경우, 웹 브라우저는 HTML 문서를 표준 모드로 렌더링한다.</li>
<li>문서 형식 선언을 해줌으로써 웹 페이지가 모든 웹 브라우저에서 같은 레이아웃으로 실행되도록 할 수 있다.</li>
</ul>
<pre><code class="language-html">&lt;html lang=&quot;en&quot;&gt;
&lt;/html&gt;</code></pre>
<h3 id="💡-html-태그">💡 HTML 태그</h3>
<ul>
<li>HTML 파일의 시작과 끝을 보여준다.</li>
</ul>
<h3 id="💡-lang-속성">💡 lang 속성</h3>
<ul>
<li>웹문서의 언어를 지정해주는 속성이다.</li>
<li>예시의 코드는 영어(en)를 사용하고 있다.</li>
<li>lang 속성은 전역 속성에 해당하여 위와 같이 문서의 시작에 정의하면 모든 요소에 공통으로 적용된다.</li>
<li>다만, <strong>body</strong> 태그 안에 개별적으로 다른 언어를 지정해줌으로써 해당 요소에만 별도로 적용하는 것도 가능하다.</li>
</ul>
<pre><code class="language-html">&lt;head&gt;
&lt;/head&gt;</code></pre>
<h3 id="💡-head-태그">💡 head 태그</h3>
<ul>
<li>파일에 대한 정보를 제공하는 부분</li>
<li><strong>html</strong> 태그와 <strong>body</strong> 태그 사이에 생성한다.</li>
<li>웹 페이지의 제목을 설정하는 <strong>title</strong> 태그를 필수적으로 포함해야 한다.</li>
<li>그 외에도 파일 전체의 요소 디자인에 관한 <strong>style</strong> 태그나 아래에서 다룰 <strong>meta</strong> 태그와 같은 태그들이 <strong>head</strong> 태그 안에 위치할 수 있다.</li>
</ul>
<pre><code class="language-html">&lt;meta charset=&quot;UTF-8&quot;&gt;</code></pre>
<h3 id="💡-meta-태그">💡 meta 태그</h3>
<ul>
<li>해당 문서에 대한 정보, 즉 메타데이터를 제공할 때 사용되는 태그이다.</li>
<li>메타데이터는 화면에 표시되지는 않지만, 웹 프라우저에게 HTML 웹 문서에 대한 필요한 정보를 제공한다.</li>
<li>메타데이터의 예시로는 웹 페이지에 대한 설명(description), 문서 저작자(author), 검색엔진에서 사용될 키워드 등이 있다.</li>
</ul>
<h3 id="💡-charset-속성">💡 charset 속성</h3>
<ul>
<li>해당 HTML 문서의 인코딩 방식을 정의하는 속성이다.</li>
<li>인코딩 방식을 정의함으로써 파일을 열었을 때 글자 깨짐 현상이 발생하는 것을 방지할 수 있다.</li>
<li>유니코드를 위한 문자셋인 UTF-8이 가장 많이 사용된다.</li>
</ul>
<blockquote>
<p><strong>🌐 유니코드</strong>
: 전 세계의 모든 문자를 담아 각 언어와 문자 체계에 따른 충돌 현상을 해결한 표준 문자 전산 처리 방식이다. 이를 통해 사용자는 한글, 히라가나, 간체자를 통일된 환경에서 문제없이 사용할 수 있게 되었다.</p>
</blockquote>
<pre><code class="language-html">&lt;meta http-equiv=&quot;X-UA-Compatible&quot; content=&quot;IE=edge&quot;&gt;</code></pre>
<h3 id="💡-http-equiv-속성">💡 http-equiv 속성</h3>
<ul>
<li>content 속성의 정보 및 값에 대한 HTTP 헤더를 제공하는 http-equiv 속성은 HTTP 응답 헤더를 시뮬레이션할 때 사용한다.</li>
<li>여기서 HTTP 헤더란 클라이언트와 서버가 요청 또는 응답으로 부가정보를 전달할 수 있게 하는 것이다.</li>
<li>이 속성이 명시되어 있다면 반드시 아래의 content 속성도 함께 명시되어야 한다.</li>
</ul>
<h3 id="💡-x-ua-compatible">💡 X-UA-Compatible</h3>
<ul>
<li>마이크로소프트에서 버전별로 보여지는 웹의 모습에 차이가 있는 단점을 보완하기 위해 해당 값을 사용하여 웹의 호환성을 지정할 수 있도록 한 것이다.</li>
<li>content 속성의 값으로 개발 환경을 입력하면, 웹 브라우저는 '호환성 보기'를 통해 웹 페이지를 그 버전으로 보여주게 된다.</li>
</ul>
<h3 id="💡-content-속성">💡 content 속성</h3>
<ul>
<li>name 속성이나 http-equiv 속성과 관련된 값(value)을 명시하기 위해 사용된다.</li>
</ul>
<h3 id="💡-ieedge">💡 IE=edge</h3>
<ul>
<li>최신 모드.</li>
<li>지정된 DOCTYPE에 관계 없이 IE8 이상의 버전에서 항상 최신 표준 모드로 렌더링된다.</li>
</ul>
<blockquote>
<p><strong>🖌️ 렌더링</strong>
: HTML과 같은 마크업 언어에서의 렌더링(Rendering)이라는 특성은 엔진이 작성된 마크업 언어를 해석하여 사람의 눈을 통해 볼 수 있는 형태로 그려주는 과정을 의미한다.</p>
</blockquote>
<pre><code class="language-html">&lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1.0&quot;&gt;
</code></pre>
<h3 id="💡-name-속성">💡 name 속성</h3>
<ul>
<li>메타데이터를 위한 이름을 명시한다.</li>
<li>http-equiv 속성과 마찬가지로 content 속성도 반드시 함께 명시되어야 한다.</li>
</ul>
<h3 id="💡-viewport">💡 viewport</h3>
<ul>
<li>웹 페이지에서 사용자가 볼 수 있는 영역인 뷰포트를 제어할 수 있도록 name 속성에 지정된 속성 값이다.</li>
</ul>
<h3 id="💡-width--device-width">💡 width = device-width</h3>
<ul>
<li>화면 너비 = 기기 너비</li>
</ul>
<h3 id="💡-initial-scale--10">💡 initial-scale = 1.0</h3>
<ul>
<li>기본 크기 = 100%</li>
</ul>
<pre><code class="language-html">&lt;title&gt;Document&lt;/title&gt;</code></pre>
<h3 id="💡-title-태그">💡 title 태그</h3>
<ul>
<li>웹 페이지의 제목을 설정하는 역할을 한다.</li>
</ul>
<img src="https://velog.velcdn.com/images/hamjw0122/post/8943d4c0-b700-46cb-847a-72427b6c933e/image.png" width="60%" />

<ul>
<li>해당 태그에서 설정한 제목은 웹 브라우저 상단 탭에서 보여진다.</li>
</ul>
<pre><code class="language-html">&lt;body&gt;
&lt;/body&gt;</code></pre>
<h3 id="💡-body-태그">💡 body 태그</h3>
<ul>
<li>문서의 모든 콘텐츠를 포함하는 영역을 정의할 때 사용되는 영역</li>
<li><strong>body</strong> 태그 내부의 모든 것들은 웹 페이지 상에 표시된다.</li>
<li>하나의 HTML 문서에는 하나의 <strong>body</strong> 요소만 존재할 수 있다.</li>
</ul>