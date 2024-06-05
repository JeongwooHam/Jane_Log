<p>토이 프로젝트로 유기 동물 공고 관련 웹 페이지를 만들면서, </p>
<p><img alt="" src="https://velog.velcdn.com/images/hamjw0122/post/8e1063ae-7dd1-41c1-b8fd-859380171571/image.png" /></p>
<p>이 부분의 n일 전 로직을 구현하기 위해 날짜 계산 라이브러리를 사용하였다.
처음에는 코드가 간편하고 관련 문서가 찾기 쉽다는 이유로 <strong><em>Moment.js</em></strong>를 사용하였는데</p>
<blockquote>
<p>왜 Day.js 대신 사용을 지양하는 Moment.js를 사용하셨나요?</p>
</blockquote>
<p>라는 피드백을 받았다.
<img src="https://velog.velcdn.com/images/hamjw0122/post/31b140bb-fd7b-4b18-ab74-bdc432220bd5/image.png" width="60%" /></p>
<pre><code>지금까지 잘 써왔던 Moment.js가 레거시한 코드가 되었다니...?</code></pre><p><strong><em>Day.js</em></strong>로 코드를 마이그레이션 하면서 그 이유를 찾아보게 되었다.</p>
<h2 id="🫥-momentjs는-레거시-프로젝트가-되었습니다">🫥 Moment.js는 레거시 프로젝트가 되었습니다!</h2>
<h3 id="⏱️-momentjs로-구현한-코드">⏱️ Moment.js로 구현한 코드</h3>
<pre><code class="language-typescript">import moment from 'moment'
import 'moment/locale/ko' // 대한민국 로컬 시간 

const getPeriod = (date: string, type: string) =&gt; moment(date, type).fromNow()

export default getPeriod</code></pre>
<ul>
<li>위의 함수는 시작 일자를 넣으면 현재 시간과 비교하여 시간이 얼마나 지났는지에 대한 값(3일, 5달, 방금, ...)을 반환해준다.</li>
<li>이러한 기능 뿐만 아니라 'YYYY.MM.DD'의 형식으로 날짜를 나타내는 것을 JS의 Data 객체를 사용하여 직접 구현하려면 복잡하고 긴 코드를 작성해야 한다.</li>
<li>따라서 보통은 날짜 관련 라이브러리를 사용하여 해당 코드를 구현하며, Moment.js의 경우 코드가 간단할 뿐 아니라 <strong><em>ko</em></strong>처럼 각 국가에 대한 로컬 시간도 지원해 JS의 Date 객체에 대한 계산을 간편하게 처리할 수 있었다.</li>
</ul>
<h3 id="⚠️-momentjs의-문제점">⚠️ Moment.js의 문제점</h3>
<blockquote>
<p>Webpack</p>
</blockquote>
<ul>
<li>웹팩은 서로 관련된 웹 자원들의 의존 관계를 파악하고, 의존하는 것들끼리 합쳐서 img, CSS, JS와 같은 정적 자원으로 변환해주는 모듈 번들러를 의미한다.</li>
<li>이렇게 최적화된 자원들은 하나의 번들로 압축되고, 요청이 한 번만 발생하면 되므로 HTTP 요청의 수가 줄어든다는 장점을 가진다.</li>
<li>하지만 여러 JS 파일이 하나로 합쳐지다보니 번들의 크기가 과도하게 커졌다.<ul>
<li>특히 SPA의 등장과 CSS-in-JS와 같은 방법론의 도입으로 JS 코드의 크기는 더 거대해졌다.</li>
<li>이로 인해 번들을 다운로드하기 위한 시간이 증가할 경우 사용자가 페이지를 보는 시간이 더 지연되는 문제가 발생한다.</li>
</ul>
</li>
<li>따라서 번들의 경량화는 프론트엔드 성능 최적화를 위한 중요한 도구 중 하나가 되었다.
(자세한 내용은 웹팩 관련 포스트에서 더 구체적으로 다뤄볼 예정이다.)</li>
</ul>
<blockquote>
<p>그리고, Moment.js</p>
</blockquote>
<ul>
<li>Moment.js는 Date 객체에 대해 광범위한 연산을 지원하고, 따라서 번들에 포함된 내용 중 사용되는 부분보다 그렇지 않은 부분이 더 큰 상황이 발생한다.</li>
</ul>
<pre><code>👩‍🏫 사용되지 않는 기능 때문에 네트워크 코스트와 페이지 렌더링 시간이 증가하고, 다운로드 속도는 저하되는 거죠!</code></pre><ul>
<li><p>실제로 Moment.js의 용량은 2.24.0버전 기준으로 235.4KB로, react-dom의 약 2.3배, vue의 3.6배만큼 크다.</p>
<ul>
<li>이때문에 번들에서 Moment.js가 30%를 차지하지만 실제로 사용되는 부분도 30% 정도밖에 되지 않는 극단적인 예시 상황이 발생하기도 한다.</li>
</ul>
</li>
<li><p>또한 Moment.js 공식문서에서도 이 라이브러리를 레거시하다고 정의하고, 더 이상의 신규 개발 없이 유지보수만 하는 상태로 전환하며 앞으로의 계획을 다음과 같이 밝혔다.</p>
<ul>
<li>새로운 성능이나 기능을 추가하지 않을 예정이다.</li>
<li>tree-shaking, 번들 사이즈 등 관련 에러나 버그를 해결하지 않을 예정이다.</li>
<li>더 이상의 업데이트를 하지 않을 것이다.</li>
<li>국제화 로케일 파일에 대한 수정을 진행하지 않을 예정이다.</li>
</ul>
</li>
</ul>
<h2 id="🤠-대신-dayjs를-사용합시다">🤠 대신 Day.js를 사용합시다!</h2>
<ul>
<li>Day.js란, Moment.js와 호환되는 API를 가진 경량 라이브러리이다.</li>
</ul>
<h3 id="🤓-dayjs를-선택한-이유">🤓 Day.js를 선택한 이유</h3>
<ul>
<li><a href="https://momentjs.com/docs/#/-project-status/recommendations/">Moment.js 공식문서</a>에는 대체 라이브러리들이 소개되어 있다.</li>
<li><a href="https://moment.github.io/luxon/#/">Luxon</a>, <a href="https://date-fns.org/">Date-fns</a>, <a href="https://js-joda.github.io/js-joda/">js-Joda</a>도 소개되어 있지만 <a href="https://day.js.org">Day.js</a> 공식 문서에 소개된 장점들이 가장 매력적이라고 생각되어 Day.js를 사용하게 되었다.</li>
</ul>
<blockquote>
<p>사이즈가 매우 작다.</p>
</blockquote>
<ul>
<li>Day.js에는 일반적으로 사용될 기본적인 기능들만 포함되어 있고 이외의 기능은 <code>dayjs/plugin</code>를 통해 확장하여 사용할 수 있다.</li>
<li>Day.js의 용량은 7.1KB(gzipped: 2.9KB)로, Moment.js보다 무려 33배 가량 더 가볍다.</li>
<li>실제로 자료들을 찾아본 결과 번들의 4% 정도만 차지할 정도로 용량 최적화에 유의미한 영향을 줌을 알 수 있었다.</li>
</ul>
<blockquote>
<p>Moment.js와 사용 방법이 유사하다.</p>
</blockquote>
<ul>
<li>새로운 라이브러리를 도입할 때, 추가로 공부해야 할 양이 얼마나 많은지도 중요하게 고민하는 요소 중 하나인데 Day.js의 경우 공식 문서에 이미 이렇게 언급하고 있다.</li>
</ul>
<pre><code>If you use Moment.js, you already know how to use Day.js.</code></pre><blockquote>
<p>I18n</p>
</blockquote>
<ul>
<li>Day.js는 국제화 관련 기능도 지원하고 있다.</li>
<li>하지만 이 기능이 실제 사용되기 전까지는 포함되지 않으므로 용량 최적화에도 좋다.</li>
</ul>
<h3 id="👾-dayjs-사용-방법">👾 Day.js 사용 방법</h3>
<pre><code>npm install dayjs

yarn add dayjs</code></pre><blockquote>
<p>Day.js is immutable!</p>
</blockquote>
<p>Moment.js와 달리 변경이 불가능(immutable)하기 때문에 이미 변수에 Day.js 객체의 날짜를 메소드로 변경할 경우 변수에 재할당해주어야 한다.</p>
<pre><code class="language-javascript">// Moment.js
const dateWithMoment = moment('2023-11-02');
dateWithMoment.add(7, 'day'); // 1일 추가
console.log(dateWithMoment.formet('YYYY-MM-DD'); // '2023-11-09'

// Day.js
let dateWithDay = dayjs('2023-11-02');
dateWithDay.add(1, 'day') // 1일 추가
console.log(dateWithDay.format('YYYY-MM-DD')) // '2023-11-02' 그대로 출력
dateWithDay = dateWithDay.add(1, 'day') // 1일 추가 + 재할당
console.log(dateWithDay.format('YYYY-MM-DD')) // '2023-11-09'</code></pre>
<blockquote>
<p>날짜 표시하기</p>
</blockquote>
<ul>
<li>Moment.js와 동일한 API를 사용한다.</li>
</ul>
<pre><code class="language-javascript">import dayjs from 'dayjs'

const date = dayjs('2023-11-02T23:56:00+09:00')

console.log(date.year()) // 2023 (연도)
console.log(date.month()) // 11 (월)
console.log(date.date()) // 02 (일)
console.log(date.hour()) // 23 (시)
console.log(date.minute()) // 56 (분)
console.log(date.second()) // 0 (초)
console.log(date.format('YYYY.MM.DD (HH:mm)')) // '2023.11.02 (23:56)' </code></pre>
<blockquote>
<p>날짜 변경하기</p>
</blockquote>
<ul>
<li>set: 날짜를 변경할 수 있다.</li>
</ul>
<pre><code class="language-javascript">let date = dayjs('2023-11-02T23:56:00+09:00')
date = date
  .set('month', 12) // 12월로 달 변경
console.log(date.format('YYYY년 MM월 DD일')) // '2023년 12월 02일' </code></pre>
<ul>
<li>add: 날짜를 더해줄 수 있다.</li>
</ul>
<pre><code class="language-javascript">let date = dayjs('2023-11-02T23:56:00+09:00')
date = date
  .add('day', 12) // 12일 더하기
console.log(date.format('YYYY년 MM월 DD일')) // '2023년 11월 14일' </code></pre>
<ul>
<li>subtract: 날짜를 빼줄 수 있다.</li>
</ul>
<pre><code class="language-javascript">let date = dayjs('2023-11-02T23:56:00+09:00')
date = date
  .subtract('month', 6) // 6개월 빼기
console.log(date.format('YYYY년 MM월 DD일')) // '2023년 05월 02일' </code></pre>
<blockquote>
<p>I18n (국제화)</p>
</blockquote>
<pre><code class="language-javascript">import dayjs from 'dayjs'
import 'dayjs/locale/ko'

dayjs.locale('ko') // global로 한국어 locale 사용
const todayKor = dayjs('2023-11-02')
console.log(todayKor.format('ddd')) // '목요일'
const todayEng = dayjs('2023-11-02').locale('en') 
// todayEng 인스턴스에서만 영어 locale사용
console.log(date2.format('ddd')) // 'Thu'</code></pre>
<p>+) <a href="https://github.com/iamkun/dayjs/tree/dev/src/locale">지원하는 locale 목록</a></p>
<h3 id="🗓️-dayjs로-수정한-코드">🗓️ Day.js로 수정한 코드</h3>
<pre><code class="language-typescript">import dayjs from 'dayjs'
import duration from 'dayjs/plugin/duration'
dayjs.extend(duration)

export const getDiff = (date: string) =&gt; {
  const today = dayjs()
  const diff = dayjs.duration(today.diff(date))

  const yearDif: number = parseInt(diff.format('Y'))
  const monthDif: number = parseInt(diff.format('M'))
  const dateDif: number = parseInt(diff.format('D'))

  if (yearDif &gt; 0) {
    return `${yearDif}년`
  } else if (monthDif &gt; 0) {
    return `${monthDif}달`
  } else if (dateDif &gt; 0) {
    return `${dateDif}일`
  } else {
    return '하루'
  }
}</code></pre>
<ul>
<li>Moment.js에 비해서는 직접 구현해주어야 하는 코드가 있는 편이다.</li>
<li>하지만 이러한 기능이 모두 번들에 포함되는 대신 필요한 기능만 담아 가볍고, 안정성이 보장된다는 것을 고려했을 때 Day.js를 포기할 만큼 사용법이 복잡하지는 않아 앞으로는 Day.js를 사용할 것 같다!</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://momentjs.com/docs/#:~:text=We%20now%20generally%20consider%20Moment%20to%20be%20a%20legacy%20project%20in%20maintenance%20mode.%20It%20is%20not%20dead%2C%20but%20it%20is%20indeed%20done.">Moment.js Documentation</a></li>
<li><a href="https://blog.hoseung.me/2022-03-13-dayjs-instead-of-momentjs">Moment.js 대신 Day.js - 프론트엔드 번들 사이즈 줄이기</a></li>
<li><a href="https://medium.com/@sg1004you/day-js-vs-moment-js-971ebc1c9aad">day.js vs moment.js</a></li>
<li><a href="https://john015.netlify.app/moment-js%EB%A5%BC-day-js%EB%A1%9C-%EB%8C%80%EC%B2%B4%ED%95%98%EA%B8%B0">Moment.js를 Day.js로 대체하기</a></li>
</ul>