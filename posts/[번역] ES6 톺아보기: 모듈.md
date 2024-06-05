<p>구현하는 프로젝트의 규모가 점점 커지고, 심지어는 모노레포 형태의 프로젝트도 경험해보면서 점점 더 코드를 효율적으로 구성하고 관리해야 할 필요성을 느꼈고, 그 중에서도 모듈 시스템에 대한 학습을 해보고 싶다는 생각을 했다. 
기존에도 모듈 시스템을 사용하면 코드 재사용 및 유지보수가 쉬워진다는 것은 알고 있었지만 지금까지 JavaScript의 모듈 시스템에 대해 제대로 이해하고 있지는 못했다는 생각이 들었기 때문이다.
그러던 중 마침 모듈에 관련된 좋은 아티클을 추천받게 되어 이를 번역하면서 학습해보고자 한다.</p>
<blockquote>
<p><strong>원문 보러가기</strong>
<a href="https://hacks.mozilla.org/2015/08/es6-in-depth-modules/">ES6 In Depth: Modules</a></p>
</blockquote>
<p>2007년에 Mozilla의 JavaScript 팀에 입사했을 때, 일반적인 JavaScript 프로그램의 길이는 한 줄이라는 농담이 있었습니다.</p>
<p>이때는 Google 지도가 출시된 지 2년이 지난 시점이었습니다. 그 전까지 JavaScript의 주된 사용처는 form 유효성 검증이었고, 당신이 평균적으로 사용했을 <code>&lt;input onchange=&gt;</code> 핸들러는 확실히... 한 줄의 코드였을 겁니다.</p>
<p>하지만 상황이 바뀌었습니다. JavaScript 프로젝트는 입이 떡 벌어질 정도의 규모로 성장했고, JavaScript 커뮤니티 또한 그 규모에 맞게 작업할 수 있는 도구를 개발했습니다. 당신이 가장 필요로 하는 것 중 하나는 모듈 시스템일텐데, 이는 당신의 작업을 다양한 파일과 디렉토리에 분산시키면서도 여전히 당신의 모든 코드 조각들이 서로 필요할 때마다 접근 가능하도록 만들 뿐만 아니라 모든 코드를 효율적으로 로드할 수 있도록 하는 방법입니다. 따라서 자연스럽게, JavaScript는 모듈 시스템을 가지고 있습니다. 사실은, 여러 가지를 가지고 있죠. 또한 다양한 패키지 매니저도 있는데, 이는 모든 소프트웨어를 설치하고 높은 수준의 종속성에 대처할 수 있도록 해주는 도구입니다. 당신은  새로운 모듈 구문을 사용하는 ES6가 다소 늦었다고 생각할 수도 있습니다.</p>
<p>그래서 오늘 우리는 ES6가 이런 기존 시스템에 무언가를 추가할지, 그리고 추후 표준과 도구가 이 시스템을 기반으로 구축될 수 있을지에 대해 살펴볼 예정입니다. 하지만 그 전에 먼저, ES6 모듈이 어떻게 생겼는지부터 알아봅시다.</p>
<h2 id="모듈의-기본">모듈의 기본</h2>
<p>ES6 모듈은 JS 코드를 포함하는 파일입니다. 특별한 <code>module</code> 키워드는 존재하지 않습니다; 모듈은 대부분 스크립트와 비슷하게 읽히지만, 두 개의 차이점이 존재합니다.</p>
<ul>
<li>ES6 모듈은 당신이 <code>use strict</code>를 내부에 작성하지 않더라도 자동으로 strict-mode가 적용된 코드입니다.</li>
<li>당신은 모듈에 <code>import</code>와 <code>export</code>를 사용할 수 있습니다.</li>
</ul>
<p><code>export</code>에 대해 먼저 이야기해봅시다. 기본적으로, 모듈 내에서 선언된 모든 것은 해당 모듈 내에서만 local로 처리됩니다. 만약 당신이 모듈 내부에서 무언가가 public하게 선언되어 다른 모듈도 그것을 사용할 수 있기를 원한다면, 당신은 반드시 그 기능을 <code>export</code> 해주어야 합니다. 여기 이를 수행할 수 있는 몇 가지의 방법이 있습니다. 가장 단순한 방법은 <code>export</code> 키워드를 추가하는 것입니다.</p>
<blockquote>
<p>kittydar.js</p>
</blockquote>
<ul>
<li>이미지에서 모든 고양이의 위치를 찾아줍니다.</li>
<li><a href="https://api.velog.io/rss/%22https:/harthur.github.io/kittydar/%22">Heather Arthur는 이 라이브러리를 실제로 작성했습니다.</a></li>
<li>하지만 이때는 2013년이었기 때문에, 그녀는 모듈을 사용하지 않았습니다.</li>
</ul>
<pre><code class="language-js">export function detectCats(canvas, options) {
var kittydar = new Kittydar(options);
return kittydar.detectCats(canvas);
}

export class Kittydar {
... several methods doing image processing ...
}

// 이 헬퍼 함수는 export 되지 않았습니다.
function resizeCanvas() {
...
}
...</code></pre>
<p>당신은 최상위 함수, 클래스, <code>var</code>, <code>let</code>, 또는 <code>const</code>를 <code>export</code>할 수 있습니다.</p>
<p>그리고 이것이 당신이 모듈을 작성하기 위해 알아야 하는 전부입니다! 모든 것을 <a href="https://en.wikipedia.org/wiki/Immediately-invoked_function_expression">IIFE</a>나 콜백 함수 안에 넣을 필요는 없습니다. 그냥 필요한 모든 것을 선언하세요. 코드가 스크립트가 아닌 모듈이기 때문에 모든 선언은 전체 스트립트와 모듈에서 전역적으로 표시되는 것이 아니라, 해당 모듈로 범위가 지정됩니다. 모듈의 공용 API를 구성하는 선언을 내보내면 완료됩니다.</p>
<p>내보내기(<code>exports</code>)를 제외하면, 모듈 내부의 코드는 거의 일반적인 코드와 동일합니다. 이는 <code>Object</code>나 <code>Array</code>와 같은 전역 변수를 사용할 수 있습니다. 웹 브라우저에서 모듈이 실행된다면, <code>document</code>와 <code>XMLHttpRequest</code>를 사용할 수 있습니다.</p>
<p>분리된 파일에서, 우리는 <code>detectCats()</code> 함수를 import 해와서 사용할 수 있습니다.</p>
<pre><code class="language-js">// demo.js - Kittydar demo program

import {detectCats} from &quot;kittydar.js&quot;;

function go() {
var canvas = document.getElementById(&quot;catpix&quot;);
var cats = detectCats(canvas);
drawRectangles(canvas, cats);
}</code></pre>
<p>모듈에서 다양한 것들을 import 해오기 위해서, 당신은 다음과 같이 작성해야 합니다:</p>
<pre><code class="language-js">import {detectCats, Kittydar} from &quot;kittydar.js&quot;;</code></pre>
<p><code>import</code> 선언을 포함하는 모듈을 실행한다면 먼저 가져온 모듈이 로드되고, 그 뒤에는 의존성 그래프의 깊이 우선 탐색을 통해 각 모듈 본문이 실행되어 이미 실행된 것은 건너 뛰면서 순환을 피하게 됩니다.</p>
<p>그리고 이것이 모듈의 기본 사항입니다. 정말 간단하죠? ;-)</p>
<h2 id="내보내기-목록">내보내기 목록</h2>
<p>내보낼 각각의 기능에 태그를 붙이는 대신, 내보내고자 하는 모든 이름들을 중괄호로 묶은 단일 목록을 작성할 수 있습니다.</p>
<pre><code class="language-js">export {detectCats, Kittydar};

// 여기서는 export 키워드가 필요하지 않습니다.
function detectCats(canvas, options) { ... }
class Kittydar { ... }</code></pre>
<p><code>export</code> 목록이 파일의 첫 부분일 필요는 없습니다. 모듈 파일의 최상단 범위 내의 어디든 표시할 수 있습니다. 당신은 이름을 두 번 이상 내보내지 않는 한 여러 개의 <code>export</code> 목록을 가지거나 다른 <code>export</code> 선언들과 <code>export</code> 목록들을 섞을 수도 있습니다.</p>
<h2 id="imports와-exports의-이름-변경하기">imports와 exports의 이름 변경하기</h2>
<p>가끔씩 가져온 이름이 사용해야 하는 어떤 이름과 충돌하는 경우가 있습니다. 그래서 ES6은 무언가를 가져올 때 이름을 변경할 수 있도록 해줍니다:</p>
<pre><code class="language-js">// suburbia.js

// 두 개의 모듈은 모두 `flip`이라는 이름을 가진 무언가를 내보냈습니다.
// 두 개를 모두 가져오기 위해, 우리는 최소 하나의 이름을 변경해야 합니다.
import {flip as flipOmelet} from &quot;eggs.js&quot;;
import {flip as flipHouse} from &quot;real-estate.js&quot;;</code></pre>
<p>비슷하게, 내보낼 때에도 이름을 변경할 수 있습니다. 이 기능은 가끔 발생할 수도 있는 상황인, 동일한 값을 두 개의 다른 이름으로 내보내기를 원할 때 유용합니다.</p>
<pre><code class="language-js">// unlicensed_nuclear_accelerator.js
// drm(디지털 권리 관리)이 없는 미디어 스트리밍 사이트
// 실제 라이브러리는 아니지만, 아마 라이브러리가 될 수도 있습니다. 

function v1() { ... }
function v2() { ... }

export {
v1 as streamV1,
v2 as streamV2,
v2 as streamLatestVersion
};</code></pre>
<h2 id="기본-내보내기-default-export">기본 내보내기 (Default Export)</h2>
<p>새로운 표준은 기존 CommonJS와 AMD 모듈과 상호 운용이 가능하도록 설계되었습니다. 당신이 Node 프로젝트를 가지고 있고 <code>npm install lodash</code>를 수행했다고 가정해보겠습니다. 당신의 ES6 코드는 Lodash에서 개별적인 함수들을 가져올 수 있습니다:</p>
<pre><code class="language-js">import {each, map} from &quot;lodash&quot;;

each([3, 2, 1], x =&gt; console.log(x));</code></pre>
<p>하지만 아마 당신은 <code>each</code> 보다는 <code>_.each</code>를 보는 것에 더 익숙해져서 여전히 그러한 방식으로 작성하는 것을 원할 수도 있습니다. 또는 <a href="https://lodash.com/docs#_">이것이 Lodash에서 유용한 기능</a>이기 때문에 <code>_</code>를 함수로 사용하고 싶을 수도 있습니다. </p>
<p>이를 위해서, 당신은 약간 다른 구문을 사용할 수 있습니다: 중괄호 없이 모듈을 가져오세요.</p>
<pre><code class="language-js">import _ from &quot;lodash&quot;;</code></pre>
<p>이 약어는 <code>import {default as _} from 'lodash'</code>와 같습니다. 모든 CommonJS와 AMD 모듈은 ES6에 <code>default</code> export를 가지고 있는 것으로 표시되며, 이는 해당 모듈에 대해 <code>require()</code>, 즉 <code>exports</code> 객체를 요청하면 얻게 되는 것과 동일합니다.</p>
<p>ES6 모듈은 여러 개의 항목을 내보낼 수 있도록 설계되었지만, 기존의 CommonJS 모듈에서는 기본 내보내기가 유일한 방법입니다. 예를 들어, 이 글을 작성하고 있는 지금 유명한 <a href="https://github.com/Marak/colors.js">colors</a> 패키지는 제가 말씀드릴 수 있는 한 특별한 ES6 지원이 없습니다. 이것은 대부분의 npm 패키지와 마찬가지로 CommonJS 모듈의 컬렉션입니다. 그러나 이를 바로 ES6 코드로 가져올 수 있습니다.</p>
<pre><code class="language-js">// ES6에서 `var colors = require(&quot;colors/safe&quot;);`와 동일합니다.
import colors from &quot;colors/safe&quot;;</code></pre>
<p>만약 자체 ESE6 모듈에 기본 내보내기를 사용하려 한다면, 매우 쉽게 할 수 있습니다. 기본 내보내기에 특별한 것은 없습니다; <code>default</code>라고 이름 붙여진 것만 제외한다면 다른 내보내기들과 동일합니다. 우리가 이미 이야기를 나눴던 이름 바꾸기 구문을 사용할 수도 있습니다:</p>
<pre><code class="language-js">let myObject = {
field1: value1,
field2: value2
};
export {myObject as default};</code></pre>
<p>또는 이 약어를 사용하는 것이 더 좋습니다:</p>
<pre><code class="language-js">export default {
field1: value1,
field2: value2
};</code></pre>
<p><code>export default</code> 키워드 다음에는 함수, 클래스, 객체 리터럴 등 당신이 이름을 지정하는 어떤 값이든 올 수 있습니다.</p>
<h2 id="모듈-객체">모듈 객체</h2>
<p>글이 너무 길어져 죄송합니다. 하지만 JavaScript만 이런 것은 아닙니다: 어떤 이유에서인지, 모든 언어의 모듈 시스템은 개별적으로 작고 지루한 기능들을 가지고 있는 편입니다. 다행히도, 이제 하나 밖에 남지 않았습니다. 사실, 두 개네요.</p>
<pre><code class="language-js">import * as cows from &quot;cows&quot;;</code></pre>
<p>당신이 <code>import *</code>를 할 때 가져오는 것은 <em>모듈 네임스페이스 객체</em>입니다. 이 객체의 속성들은 해당 모듈들이 내보낸 것들입니다. 따라서 만약 'cows' 모듈이 <code>moo()</code>라는 이름의 함수를 내보냈다면 위와 같은 방식으로 'cows'를 가져온 뒤 <code>cows.moo()</code>와 같이 작성할 수 있습니다.</p>
<h2 id="모듈-집합하기">모듈 집합하기</h2>
<p>때때로 패키지의 메인 모듈은 패키지의 다른 모듈들을 모두 가져와서 통합된 방식으로 내보내는 것에 불과합니다. 이러한 종류의 코드를 단순화하기 위해, 모든 것을 한 번에 가져와서 내보낼 수 있는 단축된 방법이 있습니다:</p>
<pre><code class="language-js">// world-foods.js - 모든 곳에서 좋은 것들 

// &quot;sri-lanka&quot;를 import 해와서 그 중 몇 개를 다시 export 합니다.
export {Tea, Cinnamon} from &quot;sri-lanka&quot;;

// &quot;equatorial-guinea&quot;를 import 해와서 그 중 몇 개를 다시 export 합니다.
export {Coffee, Cocoa} from &quot;equatorial-guinea&quot;;

// &quot;singapore&quot;를 import 해와서 전체를 다시 export 합니다.
export * from &quot;singapore&quot;;</code></pre>
<p>각각의 <code>export-from</code> 구문은 <code>import-from</code> 구문 뒤에 <code>export</code>가 이어지는 것과 유사합니다. 실제 <code>import</code>와는 다르게, 이것은 다시 내보낸 바인딩을 스코프에 추가하지 않습니다. 따라서 <code>Tea</code>를 사용하는 <code>world-foo.js</code>에 코드를 작성할 계획이 있다면 이 축약형을 사용하지 마세요. 그 곳에 없다는 것을 알게 될 것입니다.</p>
<p>만약 'singapore'에 의해 내보내진 어떤 이름이 다른 내보내기와 충돌한다면, 오류가 발생할 것이므로 <code>export *</code>를 사용할 때는 주의가 필요합니다.</p>
<p>휴! 이제 문법에 대한 설명이 끝났네요! 이제 흥미로운 부분으로 넘어가봅시다.</p>
<h2 id="import는-실제로-어떤-역할을-할까"><code>import</code>는 실제로 어떤 역할을 할까?</h2>
<p>아무 역할도 하지 않는다면... 믿을 수 있나요?</p>
<p>물론, 당신은 그렇게 순진하지 않겠죠. 하지만 <code>import</code>가 정확히 무엇을 하는지 대부분 명시되어 있지 않다면 믿어지나요? 그리고 이것이 좋은 일이라는 것도 믿으시나요?</p>
<p>ES6는 모듈 로딩의 세부적인 사항들을 <a href="https://262.ecma-international.org/6.0/#sec-hostresolveimportedmodule">구현에 완전히 맡기고</a> 있습니다. 모듈 실행의 나머지 부분들은 <a href="https://262.ecma-international.org/6.0/#sec-toplevelmoduleevaluationjob">세부적으로 지정</a>되어 있습니다.</p>
<p>대략적으로 말하자면, JS 엔진에게 모듈을 실행하도록 지시하면 다음 네 가지의 단계가 발생하는 것처럼 동작해야 합니다: </p>
<ol>
<li><p>파싱: 구현체는 모듈의 소스 코드를 읽고 구문 오류를 확인합니다.</p>
</li>
<li><p>로딩: 구현체는 가져온 모든 모듈을 (재귀적으로) 로드합니다. 이 부분은 아직 표준화되지 않았습니다.</p>
</li>
<li><p>링킹: 새롭게 로드된 각각의 모듈들에 대해 구현체는 모듈 스코프를 생성하고, 다른 모듈들에서 가져온 것들을 포함하여 해당 모듈 내부에 선언된 모든 바인딩을 채웁니다.</p>
<p>만약 <code>import {cake} from 'paleo</code>를 시도했으나 'paleo' 모듈이 실제로는 <code>cake</code>라는 이름으로 아무것도 내보내지 않고 있다면 이 부분에서 에러가 발생한다. 그리고 이는 일부 JS 코드를 실제로 실행할 수 있을 뻔했으니, 매우 안타까운 일입니다. 심지어는 케이크도 가질 수 있었는데요!</p>
</li>
<li><p>런타임: 마지막으로, 구현체는 새로 로드된 각 모듈의 본문에 있는 구문들을 실행합니다. 이 시점에는 이미 <code>import</code> 처리가 완료되었으므로 <code>import</code> 선언이 있는 코드 라인에 실행이 도달한다면... 아무 일도 발생하지 않습니다!</p>
</li>
</ol>
<p>보이시나요? 제가 정답은 '아무 역할도 하지 않는다'라고 말씀드렸죠? 저는 프로그래밍 언어에 관해서 거짓말을 하지 않는답니다.</p>
<p>하지만 이제 우리는 이 시스템의 재미있는 부분에 도착했습니다. 멋진 트릭이 있습니다. 시스템은 로딩 작업이 어떻게 수행되는지를 명시하지 않고, 당신이 소스코드의 <code>import</code> 선언을 보고 모든 종속성을 미리 파악할 수 있기 때문에 ES6의 구현체는 모든 작업을 컴파일 타임에 수행하고 모든 모듈을 하나의 파일에 번들링해 네트워크로 그것들을 전달할 수 있습니다! 그러면 webpack과 같은 도구들이 실제로 이 작업을 수행합니다.</p>
<p>네트워크를 통해 스크립트를 로드하는 데에는 시간이 소요되며, 하나씩 가져올 때마다 수십 개를 더 로드해와야 하는 <code>import</code> 선언을 포함할 수 있으므로, 이것은 큰 문제입니다. 순진한 로더는 많은 네트워크 왕복 시간이 필요합니다. 하지만 webpack을 사용하면 오늘날의 ES6 모듈을 사용할 뿐만 아니라 실행 시 런타임 성능 저하 없이 모든 소프트웨어 엔지니어링의 이점을 얻을 수 있습니다.</p>
<p>ES6 모듈 로딩에 대한 세부적인 사양은 원래 계획되었고 - 구축되었습니다. 이것이 최종 표준에 포함되지 않은 이유 중 하나는 이 번들링 기능을 어떻게 달성할지에 대한 합의가 없었기 때문입니다. 우리가 본 것처럼, 모듈 로딩은 실제로 표준화가 되어야 하고 번들링은 포기하기에는 너무 좋은 방법이므로 누군가 이 문제를 해결했으면 좋겠습니다.</p>
<blockquote>
<p><strong><em>조금 더 의역하자면..!</em></strong></p>
</blockquote>
<ul>
<li>ES6 모듈 시스템은 모듈 간의 의존성을 정의하고 모듈을 로드하는 방법을 정의하며, 네트워크 상에서 모듈을 로드할 때의 성능 문제를 해결해야 한다.</li>
<li>모듈 간의 의존성이 많을 경우 네트워크 왕복이 많이 발생하여 성능이 저하될 수 있다.</li>
<li>webpack과 같은 도구는 ES6 모듈 시스템을 사용하여 소스 코드를 번들링하고 하나의 파일로 만들어 네트워크에서 로드할 때의 성능을 향상시킨다. ➡️ 이를 통해 네트워크 왕복 시간을 줄이고 모든 모듈을 하나의 요청으로 처리할 수 있다.</li>
<li>하지만 ES6의 모듈 로딩에 대한 자세한 명세는 초기에는 계획되었지만 모듈을 번들링하는 기능에 대한 합의가 이루어지지 않았기 때문에 최종 표준에는 포함되지 않았다. 그러나 모듈 로딩에 대한 표준화가 필요하며, 번들링은 포기하기에는 너무 유용한 기능이다.</li>
</ul>
<h2 id="정적-vs-동적-또는-규칙과-그것을-어기는-방법">정적 vs 동적, 또는: 규칙과 그것을 어기는 방법</h2>
<p>JavaScript는 동적인 언어로서는 놀라울 정도로 정적인 모듈 시스템을 갖추고 있습니다.</p>
<ul>
<li><p>모든 종류의 <code>import</code>와 <code>export</code>는 모듈의 최상위 수준에서만 허용됩니다. 조건부 <code>import</code>와 <code>export</code>는 존재하지 않고 <code>import</code>를 함수 스코프에서 사용할 수 없습니다.</p>
</li>
<li><p><code>export</code> 된 모든 식별자는 소스 코드에서 이름으로써 명시적으로 내보내져야 합니다. 프로그래밍적으로 배열을 반복하여 데이터 주도적으로 이름을 내보내는 방식은 사용할 수 없습니다.</p>
</li>
<li><p>모듈 객체는 동결됩니다. 폴리필 스타일로 모듈 객체에 새로운 기능을 추가할 방법은 없습니다.</p>
</li>
<li><p>모듈의 <em>모든</em> 종속성은 모듈 코드가 실행되기 전에 열심히 로드되고, 파싱되며 링크됩니다. 필요에 따라 lazy-load 될 수 있는 <code>import</code> 구문은 존재하지 않습니다.</p>
</li>
<li><p><code>import</code> 오류에 대한 오류 회복 기능이 없습니다. 애플리케이션은 수백 개의 모듈을 가질 수 있으며 그 중 하나라도 로드나 링크에 실패한다면, 아무것도 실행되지 않습니다. <code>import</code>를 <code>try/catch</code> 블록 안에서 사용할 수 없습니다. (이 부분의 장점은 시스템이 너무 정적이기 때문에 webpack이 컴파일 타임에 오류를 감지할 수 있다는 것입니다.)</p>
</li>
<li><p>모듈의 종속성이 로드되기 전에 일부 코드를 실행할 수 있도록 하는 hook이 없습니다. 이것은 모듈이 자신의 종속성이 로드되는 방식을 제어할 수 없음을 의미합니다.</p>
</li>
</ul>
<p>정적인 용도로만 사용하고자 한다면 이 시스템은 매우 훌륭합니다. 하지만 가끔은 약간의 해킹도 필요하잖아요?</p>
<p>그리고 이것이 어떤 어떤 모듈 로딩 시스템을 사용하더라도 ES6의 정적인 <code>import/export</code> 구문과 함께 사용할 수 있는 프로그래밍 API가 존재하는 이유입니다. 예를 들어, webpack에는 <a href="https://webpack.js.org/guides/code-splitting/#root">'code splitting'</a>을 위해 사용할 수 있는 API가 있어서, 몇 개의 모듈 번들을 필요에 따라 늦게 로드해올 수 있습니다. 동일한 API를 사용하면 위에 나열되어 있는 대부분의 다른 규칙들을 위반할 수 있습니다.</p>
<p>ES6 모듈의 <em>구문</em>은 매우 정적이며, 좋은 점에 해당합니다 - 이는 강력한 컴파일 타임 도구의 형태로 나타나고 있습니다. 하지만 정적인 구문은 풍부한 동적, 프로그래밍 로더 API와 함께 작동하도록 설계되었습니다.</p>
<h2 id="언제-es6-모듈을-사용할-수-있을까">언제 ES6 모듈을 사용할 수 있을까?</h2>
<p>오늘날 모듈을 사용하기 위해서는 <a href="https://github.com/google/traceur-compiler#what-is-traceur">Traceur</a>나 <a href="https://babeljs.io/">Babel</a>과 같은 컴파일러가 필요합니다. 이 시리즈의 초반에, Gastón I. Silva는 웹을 위해 ES6 코드를 컴파일하려면 <a href="https://hacks.mozilla.org/2015/06/es6-in-depth-babel-and-broccoli/">Babel과 Broccoli를 어떻게 사용해야 하는지 보여주었습니다</a>; 이 기사를 기반으로, Gastón은 <a href="https://github.com/givanse/broccoli-babel-examples/tree/master/es6-modules">ES6 모듈을 지원하면서 작동하는 예시</a>를 제공합니다. <a href="https://2ality.com/2015/04/webpack-es6.html">Axel Rauschmayer의 이 포스팅</a>은 Babel과 webpack을 사용하는 예제를 포함하고 있습니다.</p>
<p>ES6 모듈 시스템은 Dave Herman과 Sam Tobin-Hochstadt가 주로 설계했습니다. 이들은 몇 년에 걸친 논쟁을 통해 (저를 포함한) 모든 대항자들로부터 시스템의 정적인 부분을 방어했습니다. Jon Coppeard는 Firefox에서 모듈을 구현하고 있습니다. <a href="https://github.com/whatwg/loader">JavaScript 로더 표준</a>에 대한 추가적인 작업은 진행 중에 있습니다. HTML에 <code>&lt;script type=module&gt;</code>과 같은 내용을 추가하는 작업이 이어질 것으로 예상됩니다.</p>
<p>그리고 이것이 바로 ES6입니다.</p>
<p>너무 재미있어서 글을 끝내고 싶지가 않네요. 아마도 한 에피소드를 더 다뤄야 할 것 같아요. 우리는 ES6 사양에서 자체적인 기사로 다룰 만큼 중요하지는 않은 자질구레한 것들에 대해 이야기해볼 수 있을 것 같습니다. 그리고 미래에는 어떤 일이 일어날지에 대해서도 조금은 이야기해볼 수 있을지도 모르겠습니다. 다음주 ES6 심층 분석의 놀라운 결론을 함께해주세요.</p>
<hr />

<blockquote>
<p><strong><em>✨ 본문에는 없는 추가 탐구 사항</em></strong></p>
</blockquote>
<ul>
<li><p><a href="https://developer.mozilla.org/ko/docs/Glossary/Binding">바인딩</a></p>
<ul>
<li>두 데이터 혹은 정보의 소스를 일치시키는 기법</li>
<li>값과 식별자 사이의 연관 관계</li>
<li>변수 뿐만 아니라 함수 매개변수와 <code>catch</code> 코드 블록 등 변수가 아닌 것들을 포함한다.</li>
<li>JavaScript에서의 <code>this</code>나 <code>new.target</code>의 경우 언어에 의해 암시적으로 생성된다.</li>
<li>재할당이 가능하면 mutable, 아니면 immutable로 취급하나 이것이 보유한 값의 불변성까지 보장하지는 않는다.</li>
<li>JavaScript의 경우 바인딩을 만드는 데 사용된 구문에 따라 스코프 내에서 바인딩을 재선언할 수 있는지 여부가 결정된다. </li>
</ul>
</li>
<li><p><a href="https://developer.mozilla.org/ko/docs/Glossary/Round_Trip_Time">왕복 시간 (Round Trip Time, RTT)</a></p>
<ul>
<li>데이터 패킷이 대상으로 전송되는 데 걸리는 시간과 해당 패킷에 대한 승인이 원본에서 다시 수신되는 데 걸리는 시간을 더한 것</li>
<li>네트워크와 서버 간의 RTT는 <code>ping</code> 명령을 사용하여 확인할 수 있다.</li>
</ul>
</li>
</ul>