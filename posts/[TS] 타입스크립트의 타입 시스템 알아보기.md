<h2 id="💫-타입이란">💫 타입이란?</h2>
<ul>
<li>프로그램의 '올바른 동작'이 무엇인지에 대한 프로그래머의 의도를 인코딩하는 역할</li>
<li>프로그래머의 의도를 효과적으로 전달할 수 있다.<ul>
<li>두 정수를 더하는 작업과 기계의 특정 메모리 주소로부터 어떤 값만큼 떨어진 주소를 찾는 작업의 경우 사용되는 목적은 전혀 다르다.</li>
<li>하지만 어셈블리 수준에서는 모두 '더하기'라는 동일한 연산으로 환원된다.</li>
</ul>
</li>
<li>타입은 프로그램의 실제 동작과 <strong>일정 수준 이상 동떨어질 수 없다</strong>는 것이 보장된다.<ul>
<li>주석과 변수명은 프로그램의 실제 동작과 직접 결합되지는 않는 추상적 정보이다.</li>
<li>타입의 경우 타입 정의와 다르게 동작하면 실행 자체가 불가능하다.</li>
</ul>
</li>
</ul>
<h2 id="💫-타입스크립트의-타입-시스템">💫 타입스크립트의 타입 시스템</h2>
<blockquote>
<p>타입 시스템이란?</p>
</blockquote>
<ul>
<li>프로그램 내에서 타입을 이용해 검사하기 위해 사용하는 것</li>
<li>타임 시스템이 엄밀하고 강력할수록 언어가 복잡해지고, 진입 장벽이 높아진다는 트레이드 오프가 발생할 수 있다.</li>
</ul>
<h3 id="명목적-서브타이핑">명목적 서브타이핑</h3>
<ul>
<li>Java, C# 등</li>
<li>타입의 구조가 아닌 타입의 이름만을 가지고 구별한다.<ul>
<li>두 변수는 같은 이름의 데이터 타입으로 선언된 경우에만 서로 호환된다.</li>
<li>구조가 같아도 이름이 다르면 다른 타입으로 취급한다.</li>
</ul>
</li>
<li>명확한 상속 관계(A - B)를 지향한다.<ul>
<li>타입 정의 시 상속 관계임을 명확히 명시한 경우에만 타입 호환을 허용하는 것</li>
<li>타입 오류 발생 가능성을 배제하고 개발자의 명확한 의도를 반영할 수 있다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>장점</p>
</blockquote>
<ul>
<li>타입의 동일성을 확인할 때 구조적 타이핑에 비해 안전하다.</li>
<li>개발자가 의도한 타입이 아니라면 변수에 타입을 명시할 때 에러를 방출한다.</li>
<li>객체의 속성을 다른 객체의 속성과 호환되지 않도록 하여 안전성을 추구한다.</li>
</ul>
<h3 id="🦆-덕-타이핑-duck-typing">🦆 덕 타이핑 (Duck Typing)</h3>
<blockquote>
<p>&quot;만약 어떤 새가 오리처럼 걷고, 헤엄치고, 꽥꽥거리는 소리를 낸다면 나는 그 새를 오리라고 부를 것이다.&quot;</p>
</blockquote>
<ul>
<li>객체의 변수, 메소드의 집합이 객체의 타입을 결정하는 것</li>
<li>어떤 타입에 부합하는 변수와 메서드를 가질 경우 해당 타입에 속하는 것으로 간주하는 방식</li>
<li>타입을 미리 정하는 것이 아니라 실행되었을 때 해당 메소드들을 확인하여 타입을 정한다.</li>
<li>런타임에 타입을 검사하며 주로 <code>동적</code> 타이핑에서 사용된다.</li>
</ul>
<pre><code class="language-ts">class Duck {
  chirping() {
    console.log('quack quack')
  }
}
class Pigeon {
  chirping() {
    console.log('coo coo')
  }
}

// Pigeon으로 생성했어도 에러 없이 실행된다.
// chirping이 없더라도 클래스 객체가 들어올 수는 있다. (런타임 상에서만 에러 발생)
function inTheForest(duck) {
  duck.chirping()
}

inTheForest(new Duck())
inTheForest(new Pigeon())</code></pre>
<blockquote>
<p>장점</p>
</blockquote>
<ul>
<li>타입에 대해 자유롭다.</li>
<li>당장 빠르게 개발할 수 있고 유연하게 작성할 수 있어 생산성을 높일 수 있다.</li>
<li>런타임 데이터를 기반으로 한 기능과 자료형을 도출할 수 있다.</li>
</ul>
<h3 id="🦴구조적-서브타이핑">🦴구조적 서브타이핑</h3>
<ul>
<li>구조적 타입 시스템 (Structural Type System)</li>
<li>실제 구조와 정의에 의해 결정되는 타입 시스템</li>
<li>상속 관계가 명시되어 있지 않더라도 객체의 프로퍼티에 기반하여 사용처에서 사용에 문제가 없다면 타입 호환을 허용하는 방식</li>
<li>컴파일 타임에 타입체커가 타입을 검사하며 주로 <code>정적</code> 타이핑에서 사용된다.<ul>
<li>덕 타이핑과 마찬가지로 객체의 변수, 메소드 같은 필드를 기반으로 타입을 체크할 수 있지만 타입을 체크하는 시점은 서로 다르다.</li>
</ul>
</li>
<li>집합으로 포함한다는 개념을 지향한다.</li>
</ul>
<blockquote>
<p>장점</p>
</blockquote>
<ul>
<li><strong>같은 속성의 타입이 있는지</strong>를 체크하기 때문에 중복되는 범위가 있다면 재사용 가능하다.</li>
<li>집합 단위로 타입을 체크하므로 중복되는 속성 혹은 메서드를 획기적으로 줄일 수 있다.</li>
</ul>
<blockquote>
<p>단점</p>
</blockquote>
<ul>
<li>동일한 타입을 가지는 경우 의도치 않게 동일한 유형으로 간주될 수 있다.</li>
</ul>
<pre><code>👩‍🏫 TS는 JS를 모델링한 언어이므로, TS의 타입 시스템은 구조적 서브타이핑을 기반으로 합니다!</code></pre><h2 id="💫-타입스크립트의-타입-호환성-type-compatibility">💫 타입스크립트의 타입 호환성 (Type Compatibility)</h2>
<h3 id="🧐-타입-호환성-왜-필요할까">🧐 타입 호환성, 왜 필요할까?</h3>
<pre><code class="language-ts">type BasicFood = {
  protein: number;
  carbohydrates: number;
  fat: number;
}

const calcCalorie = (food: BasicFood) =&gt; 
food.protein * 4 + food.carbohydrates * 4 + food.fat * 9

type Pizza = BasicFood &amp; {
  brand: string;
}</code></pre>
<ul>
<li>위의 <code>calcCalorie</code> 함수에 여러 타입의 객체가 전달될 경우<ul>
<li>타입 시스템(type checker)은 동일한 타입인 경우와 아예 칼로리 계산이 불가능한 경우를 판단한다.</li>
<li>하지만 <code>Pizza</code>처럼 기존 타입을 상속하여 계산에 필요한 모든 프로퍼티를 포함하고 있을 경우 런타임 상 정상적으로 동작할 수 있는 코드가 된다.</li>
</ul>
</li>
</ul>
<p>➡️ 개발자의 의도에 맞는 유연한 대응을 위해 타입 시스템은 부분적으로 <strong>타입 호환</strong>을 지원한다.</p>
<blockquote>
<p>명목적 서브타이핑일 경우</p>
</blockquote>
<pre><code class="language-ts">// 상속 관계가 명시되어 있다.
type Pizza = BasicFood &amp; {
  brand: string;
}

const pizza: Pizza = {
  protein: 30,
  carbohydrates: 50,
  fat: 15,
  brand: &quot;Domino&quot;
}

const calorie = calcCalorie(pizza) // 오류 없이 실행된다.</code></pre>
<blockquote>
<p>구조적 서브타이핑일 경우</p>
</blockquote>
<ul>
<li>타입 시스템이 객체의 프로퍼티를 체크해주므로 명목적 서브타이핑과 동일한 효과를 낼 수 있다.</li>
<li>개발자가 상속 관계를 명시해주지 않아도 되어 편리하다.</li>
</ul>
<pre><code class="language-ts">// 상속 관계를 명시하지 않았다.
// pizza는 BasicFood 타입의 프로퍼티를 모두 포함하고 있다.
const pizza = {
  protein: 30,
  carbohydrates: 50,
  fat: 15,
  brand: &quot;Domino&quot;
}

const calorie = calcCalorie(pizza) // 오류 없이 실행된다.</code></pre>
<h2 id="⚠️-타입-호환과-freshness">⚠️ 타입 호환과 <code>Freshness</code></h2>
<ul>
<li>아래 코드의 경우 타입 오류가 발생한다.</li>
</ul>
<pre><code class="language-ts">const calorie = calculateCalorie({
  protein: 30,
  carbohydrates: 50,
  fat: 15,
  brand: 'Domino'
})</code></pre>
<h3 id="🛠️-ts-컴파일러의-동작-방식">🛠️ TS 컴파일러의 동작 방식</h3>
<ol>
<li>TS 컴파일러는 TS 소스코드를 AST(Abstract Syntax Tree)로 변환한다. (<code>parser.ts</code>, <code>scanner.ts</code>)</li>
<li><code>binder.ts</code>, <code>checker.ts</code> 등에서 타입 검사를 수행하고 JS 소스코드로 변환한다.</li>
<li><code>emitter.ts</code>, <code>transformer.ts</code> 등에서 AST를 JS 소스코드로 변환한다.</li>
</ol>
<p>➡️ <code>checker.ts</code>의 <code>hasExcessProperties()</code> 함수에서 구조적 서브타이핑과 타입 호환에 관련된 부분을 처리한다.</p>
<pre><code class="language-ts">// 함수의 매개변수로 전달된 값이 FreshLiteral이라면 true
const isPerformingExcessPropertyChecks =
    getObjectFlags(source) &amp; ObjectFlags.FreshLiteral;

// FreshLiteral일 경우
if (isPerformingExcessPropertyChecks) {
    // hasExcessProperties() 함수는 excess property가 있는 경우 에러 반환
    // property가 정확히 일치하는 경우만 허용하는 것으로 타입 호환을 허용하지 않는 것과 같은 의미
    if (hasExcessProperties(source as FreshObjectLiteralType)) {
        reportError();
    }
}
// FreshLiteral이 아닌 경우 위 분기를 건너뛰고 타입 호환을 허용하게 된다.</code></pre>
<ul>
<li>함수의 인자로 들어온 값의 <code>FreshLiteral</code> 여부에 따라 조건 분기가 발생하고, 타입 호환 허용 여부가 결정된다.</li>
</ul>
<h3 id="🧐-freshliteral이란-왜-존재할까">🧐 <code>FreshLiteral</code>이란 왜 존재할까?</h3>
<blockquote>
<p>구조적 서브타이핑에 기반한 타입 호환의 단점</p>
</blockquote>
<pre><code class="language-ts">const calorie = calculateCalorie({
  protein: 30,
  carbohydrates: 50,
  fat: 15,
  brand: 'Domino'
})</code></pre>
<ul>
<li>협업 시 다른 개발자가 해당 함수는 <code>brand</code> 프로퍼티를 사용하는 것으로 오해할 수 있다.</li>
<li><code>brand</code>를 <code>br</code> 등으로 쓰는 것처럼 오타가 발생하더라도 excess property이르모 오류가 발견되지 않는다.</li>
</ul>
<blockquote>
<p>Freshness</p>
</blockquote>
<ul>
<li>모든 Object Literal은 초기에는 신선한 것으로 간주된다.<ul>
<li>타입 단언을 하거나 타입 추론으로 타입이 확장될 경우 신선도가 사라진다.</li>
<li>특정 변수에 Object Literal 할당 시 둘 중 하나의 경우가 발생하게 된다.</li>
<li>따라서 변수에 할당 시 freshness가 사라진 상태이다.</li>
</ul>
</li>
<li>함수에 인자로 Object Literal을 바로 전달할 경우 fresh한 상태로 전달된다.<ul>
<li>fresh object의 경우 예외적으로 타입 호환이 <strong>허용되지 않는다</strong>. (<a href="https://github.com/Microsoft/TypeScript/pull/3823">관련 PR</a>)</li>
</ul>
</li>
<li>함수에 인자로 전달된 Fresh Object는 특정한 변수에 할당되지 않아 <strong>해당 함수에서만 사용된다</strong>.<ul>
<li>타입 체커는 구조적 서브타이핑을 기반으로 타입 호환을 판단하되 Freshness에 따라 예외를 둔다.</li>
<li>타입 호환을 제공해서 얻는 이점이 거의 없는 fresh object에서는 호환성을 지원하지 않는 것으로 절충안을 도출하였다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>그럼에도 fresh object에 타입 호환을 허용하고 싶다면?</p>
</blockquote>
<ul>
<li>1) 함수의 매개변수 타입에 index signature을 포함시켜 명시적으로 타입 호환을 허용시킨다.<pre><code class="language-ts">type Food = {
protein: number;
carbohydrates: number;
fat: number;
// index signature</code></pre>
</li>
</ul>
<p>}</p>
<pre><code>
- 2) `tsconfig.json`에 `suppressExcessPropertyErrors`를 `true`로 설정한다.

&gt; 모든 경우에 타입 호환을 막아버리고 싶다면?

- ***Branded Type (Branding Type)*** 
  - 의도적으로 `__brand`와 같은 프로퍼티를 추가한다.
  - 이를 통해 개발자는 함수의 매개변수로 정의한 타입 외에는 호환이 될 수 없도록 강제할 수 있다.

```ts
type Brand&lt;K, T&gt; = K &amp; { __brand: T};
type Food = Brand&lt;{
  protein: number;
  carbohydrates: number;
  fat: number;
}, 'Food'&gt;

const pizza = {
  protein: 100,
  carbohydrates: 100,
  fat: 100,
  brand: 'Domino'
}

calculateCalorie(burger) // 오류 발생 (Property '__brand' is missing)</code></pre><ul>
<li>같은 타입이지만 서로 다른 의미를 가져 명시적인 구분이 필요한 경우 사용할 수 있다.</li>
</ul>
<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://www.typescriptlang.org/ko/docs/handbook/type-compatibility.html">Type Compatibility</a></li>
<li><a href="https://toss.tech/article/typescript-type-compatibility">TypeScript 타입 시스템 뜯어보기: 타입 호환성</a></li>
<li><a href="https://vallista.kr/%EB%8D%95-%ED%83%80%EC%9D%B4%ED%95%91%EA%B3%BC-%EA%B5%AC%EC%A1%B0%EC%A0%81-%ED%83%80%EC%9D%B4%ED%95%91/">덕 타이핑과 구조적 타이핑</a></li>
<li><a href="https://nesoy.github.io/articles/2018-02/Duck-Typing">덕 타이핑(Duck Typing)이란?</a></li>
<li><a href="https://ahnheejong.name/articles/types-intro/">타입과 타입 시스템 : 연재를 시작하며</a></li>
</ul>