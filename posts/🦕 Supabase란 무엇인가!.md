<p>이번 유기동물 공고 관련 토이 프로젝트를 진행하면서,
사용자 관련 데이터 로직을 Supabase를 통해 구현하였다.
그런데 여기서 Supabase는 정확히 어떤 역할을 하는 걸까?</p>
<h2 id="🖥️-baas">🖥️ BaaS</h2>
<ul>
<li>Backend as a Service; 서비스형 백엔드</li>
<li>프론트엔드 애플리케이션에 백엔드 서비스를 제공하기 위해 사용하는 모델이다.</li>
<li>백엔드 측면 개발을 자동화시키고 클라우드 인프라를 다루는 플랫폼이다.</li>
<li>BaaS의 예시<ul>
<li>Firebase</li>
<li>Supabase</li>
<li>AWS Amplify</li>
<li>Game Sparks</li>
</ul>
</li>
<li>BaaS 공급업체는 확장성 및 보안 보장을 위해 클라우드 및 서버리스 환경을 제공한다.</li>
<li>BaaS를 통해 개발자는 편리하게 최상의 UI/UX를 제공할 수 있게 되며, 모든 백엔드 코드를 BaaS 공급업체에 아웃소싱 할 수 있다.<ul>
<li>다시 말해 개발자는 제3자에게 서버 운영 및 관리에 대한 책임을 위탁하고 프론트엔드 및 사용자 측면 개발에 초점을 맞출 수 있다.</li>
</ul>
</li>
<li>또한 BaaS는 백엔드 코드를 만들고 DX를 향상시킬 수 있는 도구들을 제공한다.<ul>
<li>API를 통해 DB에 대한 접근을 보장하고, 사용자 인증, 파일 저장, 푸시 알림, 자동화된 테스트 솔루션 등의 서비스가 포함되어 있다.</li>
<li>이로써 개발 프로세스 속도가 향상되며 최종 사용자는 가능한 한 빠르게 서비스에 접근할 수 있게 된다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>BaaS VS. Custom Backend</p>
</blockquote>
<ul>
<li>백엔드를 직접 커스텀할 경우 직접 백엔드 영역을 구축하고 인프라를 다뤄야 한다.<ul>
<li>장점: 유연성 및 맞춤화 기능</li>
<li>단점: 더 높은 개발 비용과 시간 소모</li>
</ul>
</li>
<li>BaaS를 사용할 경우 만들어진 블록과 코드 생성 도구를 이용할 수 있다.<ul>
<li>장점: 빠른 개발 속도, 개발 비용 절약, 클라우드 인프라 관리 위탁 </li>
<li>단점: 유연성이 낮고 표준화된 구조를 따르게 된다.</li>
</ul>
</li>
</ul>
<h2 id="🔥-firebase-대신-supabase를-사용하는-이유">🔥 Firebase 대신 Supabase를 사용하는 이유</h2>
<blockquote>
<p>Firebase 장점</p>
</blockquote>
<ul>
<li>웹소켓과 SSE(Server-Sent-Event)가 대중화 되기 전까지 혁신적인 실시간 DB를 제공했다.</li>
<li>RTSP(Real-Time-Stream-Protocol) 방식의 DB를 지원하여 실시간 데이터 동기화 기능을 무료로 제공해준다.</li>
<li>최신 데이터에 관련된 클라이언트 상태 관리 문제점이 해결된다.</li>
<li>서버 관리자 페이지, 원격 구성 및 사용자 통계 정보를 제공한다.</li>
</ul>
<blockquote>
<p>Firebase 단점</p>
</blockquote>
<ul>
<li>서버가 해외에 위치하여 서버의 응답 처리 속도가 느려질 때가 있다.</li>
<li>NoSQL 기반의 DB이므로 쿼리가 빈약해 데이터 검색이 어렵다.</li>
<li>로컬에서의 완벽한 실행이 불가능하며 인덱스 생성이 더디다.</li>
<li>오픈소스가 아니라 지속적일 것이라는 보장이 없고, CLI(명령줄 인터페이스)가 폐쇄적이다.</li>
<li>Cloud Function CI/CD(지속적 통합/지속적 배포)가 나빠졌다.</li>
</ul>
<blockquote>
<p>그래서, Supabase</p>
</blockquote>
<ul>
<li>Supabase는 PostgreSQL 기반의 SQL DB 기능과 REST API, 이벤트 처리 등의 고유한 기능을 오픈소스로 제공한다.</li>
<li>Firebase처럼 편리하며 Firebase에서는 제공하지 못하는 RDB를 제공한다.<ul>
<li>RDB(Relational-DataBase): 엑셀 시트처럼 빈 칸에 내용을 채워가는 DB 방식</li>
</ul>
</li>
<li>편리한 사용창<ul>
<li>SQL Editor: SQL 쿼리를 웹페이지에서 작성, 저장, 실행 가능하게 해준다. 테이블 스키마를 쉽게 생성할 수 있다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/0bfbce99-b6da-46e1-aa3a-391bf4c89ea8/image.png" /></li>
<li>Table Editor: DB 내부의 데이터를 스프레드시트(엑셀)처럼 볼 수 있다.
<img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/31340ea7-b001-4c66-99ef-f7b0b526ac88/image.png" /></li>
</ul>
</li>
<li>클라이언트, 서버 환경 두 곳에서 동일한 방식의 작업이 가능하도록 <strong>isomorphic JavaScript</strong> 라이브러리를 제공한다.<ul>
<li>isomorphic: 동형 사상. 서로 구조가 같은 두 대상 사이에 모든 구조를 보존하는 사상</li>
</ul>
</li>
</ul>
<h2 id="🤓-supabase-이렇게-사용합시다">🤓 Supabase, 이렇게 사용합시다!</h2>
<h3 id="프로젝트-생성하기">프로젝트 생성하기</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/e747f8ba-3881-423a-8da2-cd5a8cd523a8/image.png" /></p>
<ul>
<li>위의 버튼을 클릭해 프로젝트 생성 시 해당 프로젝트에서 사용할 서버 인스턴스와 PostgreSQL DB가 자동으로 생성된다.</li>
<li><a href="https://supabase.com/docs/guides/getting-started/quickstarts/nextjs">Next.js 프로젝트에 Supabase 적용하기</a></li>
</ul>
<h3 id="소셜-로그인-구현하기">소셜 로그인 구현하기</h3>
<pre><code class="language-javascript">const { data, error } = await supabase.auth.signUp({
  email: &quot;example@email.com&quot;,
  password: &quot;example-password&quot;,
});</code></pre>
<ul>
<li><code>supabase.auth.signup</code>를 호출해 Supabase의 서버에 저장될 새로운 유저를 생성할 수 있다.</li>
<li>이러한 사용자에 대한 로그인을 구현하려면<ul>
<li>단순 ID/password 로그인: <code>supabase.auth.signInWithPassword</code></li>
<li>로그인 된 유저 정보 확인: <code>supabase.auth.getUser()</code> (세션이 로컬 쿠키에 저장됨)</li>
</ul>
</li>
</ul>
<blockquote>
<p>소셜 로그인 구현하기</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/16cb5fda-cc8e-4d84-9c75-9b5b0f963239/image.png" /></p>
<ul>
<li>Supabase는 10개 이상의 주요 소셜 로그인 프로바이더를 구현하고 있어서 간편하게 코드 몇 줄만 입력하면 소셜 로그인 기능을 사용할 수 있다.</li>
</ul>
<pre><code class="language-javascript">async function signInWithGoogle() {
  const { data, error } = await supabase.auth.signInWithOAuth({
    provider: &quot;google&quot;, // kakao도 가능하다!
  });
}</code></pre>
<h3 id="db-생성하기">DB 생성하기</h3>
<ul>
<li>Supabase 프로젝트 생성 시 같이 만들어진 PostgreSQL DB는 Supabase 페이지의 대시보드에서 간편하게 관리할 수 있다.</li>
<li>테이블을 새로 추가하려 한다면 아래의 창에 이름을 부여하여 생성할 수 있다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/660c84df-77aa-44bb-a47c-3bfaff3150ba/image.png" /></p>
<ul>
<li>각 데이터의 key와 value의 type 등도 편리하게 설정할 수 있다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/89eb6a16-7e59-47ed-99aa-5135d8a4887a/image.png" /></p>
<ul>
<li>이처럼 테이블을 생성하면 이에 접근하기 위한 REST API가 자동 생성되고, 클라이언트 측에서는 SDK를 사용하여 쉽게 접근할 수 있다.<ul>
<li>SDK (Software Development Kit): 소프트웨어 개발 도구 모음</li>
<li>프론트엔드에서 DB 쿼리를 필요에 따라 직접 작성해 실행할 수 있으므로 단순 CRUD를 위해 백엔드에서 별도의 API를 구현할 필요가 없다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>RLS (Row-Level-Security)</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/2a4bad67-4aad-4732-939e-bf55453d6a7c/image.png" /></p>
<ul>
<li>행 수준 보안</li>
<li>'자신의 데이터만 가져올 수 있다'를 구현할 수 있는 보안 정책 설정이 가능하다.</li>
<li>프론트엔드 측에서 필요한 DB 쿼리를 직접 실행하기 위해 필요하다.</li>
<li>PostgreSQL의 Row Level Security 기능을 통해 Supabase에 구현되어 있다.</li>
<li>예: Supabase 대시보드를 사용해 특정 테이블에 대해 본인의 Row만 조회 가능하다는 정책 추가하기 <ul>
<li>이때 Supabase는 암묵적으로 이 정책에 기반하여 사용자가 실행하는 쿼리에 대한 필터링 조건을 자동으로 추가해준다.</li>
</ul>
</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://dlwocks31.me/blog/supabase/">Supabase - 쉽고 빠른 모바일/웹 개발을 위한 백엔드 서비스</a></li>
<li><a href="https://develop-const.tistory.com/16">Supabase란?</a></li>
<li><a href="https://velog.io/@racoon/supabase-%ED%8F%BC-%EB%AF%B8%EC%B3%A4%EB%8B%A4">supabase 폼 미쳤다</a></li>
<li><a href="https://psvm.kr/posts/tutorials/supabase/what-is-supabase">오픈소스 Firebase, Supabase는 뭐니?</a></li>
<li><a href="https://news.hada.io/topic?id=7615">우리가 Firebase에서 Supabase로 변경한 이유</a></li>
<li><a href="https://www.happyteam.io/blog/supabase-open-source-baas-can-it-work/">Supabase – open source BaaS, can it work?</a></li>
<li><a href="https://blog.back4app.com/ko/%EC%84%9C%EB%B9%84%EC%8A%A4-%ED%98%95-%EB%B0%B1%EC%95%A4%EB%93%9Cbackend-as-a-service-baas%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94/">서비스 형 백앤드(Backend as a Service)- Baas는 무엇인가요?</a></li>
</ul>