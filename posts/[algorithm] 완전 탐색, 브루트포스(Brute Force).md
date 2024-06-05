<p><a href="https://school.programmers.co.kr/learn/challenges?tab=algorithm_practice_kit">프로그래머스 코딩테스트 고득점 Kit</a>를 풀이한 내용을 정리합니다.</p>
<h2 id="💡완전-탐색이란">💡완전 탐색이란?</h2>
<ul>
<li>발생 가능한 모든 경우의 수를 탐색하면서 조건에 맞는 답을 찾아내는 방법</li>
<li>Exhuastive Search, Brute Force</li>
</ul>
<blockquote>
<p><strong><em>Brute</em></strong> (무식한) + <strong><em>Force</em></strong> (힘) </p>
</blockquote>
<ul>
<li>무식하게 모든 경우의 수를 전부 탐색하므로 시간 복잡도가 매우 크다.</li>
<li>따라서 입력값의 크기가 작을 때 사용하면 좋다. </li>
</ul>
<h3 id="💫-완전-탐색의-종류">💫 완전 탐색의 종류</h3>
<blockquote>
<p><strong>단순 Brute Force</strong></p>
</blockquote>
<ul>
<li>단순히 반복문과 조건문으로 모든 경우의 수를 시도하여 답을 구하는 방법</li>
<li>예를 들어, 4자리의 암호를 찾을 때 0000부터 9999까지 모두 시도(최대 10,000번)해보는 방식이 해당한다. </li>
</ul>
<blockquote>
<p><strong>비트마스크</strong></p>
</blockquote>
<ul>
<li>2진수를 사용하는 컴퓨터의 연산을 이용하는 방식</li>
<li>나올 수 있는 모든 경우의 수가 '각각의 원소가 포함되거나, 포함되지 않는', 두 가지 선택으로 구성된 경우 유용하다.</li>
<li>예를 들어, 원소가 n개인 집합의 모든 부분 집합을 구할 때 각 원소가 포함되는지의 여부를 <code>0</code>과 <code>1</code>로 구분하여 체크할 수 있다.</li>
</ul>
<blockquote>
<p><strong>재귀함수</strong></p>
</blockquote>
<ul>
<li>자기 자신을 호출함으로써 반복되는 코드를 짧게 줄일 수 있게 해준다.</li>
<li>⚠️ 주의할 점<ul>
<li><strong>재귀 탈출 조건이 필요하다.</strong>: <ul>
<li>올바르게 설정하지 않으면 범위 초가 오류 또는 무한 루프 등 원치 않는 결과가 발생할 수 있다.</li>
</ul>
</li>
<li><strong>현재 함수의 상태를 저장하는 매개변수가 필요하다.</strong><ul>
<li><code>cur</code>, <code>cnt</code> 등의 변수로 선택한 값이나 개수를 저장하여 현재 함수의 상태를 저장해야 한다.</li>
<li>이를 활용해야 재귀 탈출 조건을 만들고 올바른 결과를 도출해낼 수 있게 된다.</li>
</ul>
</li>
<li><strong>정확한 return문을 만들어야 한다.</strong><ul>
<li>재귀를 통해 이후의 연산 결과를 반환하여 이전 연산에 대한 추가 연산을 수행해야 하는지 고민하여 정확한 반환문을 구현해야 한다. </li>
</ul>
</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>순열</strong></p>
</blockquote>
<ul>
<li>임의의 수열이 있을 때 그것을 다른 <strong>순서</strong>로 연산하는 방법</li>
<li><code>[1, 2, 3]</code>과 <code>[3, 2, 1]</code>은 다른 값으로 여겨진다.</li>
<li>N개의 서로 다른 데이터를 순열로 나타내면 전체 순열은 <code>N!</code>개의 경우의 수를 갖게 된다.</li>
<li>순열에 원소를 하나씩 채워가며 구할 수 있고, 재귀 함수를 이용할 수 있다.</li>
</ul>
<blockquote>
<p><strong>깊이 우선 탐색(DFS), 너비 우선 탐색(BFS)</strong></p>
</blockquote>
<ul>
<li>그래프 자료 구조에서 모든 정점을 탐색하기 위한 방법</li>
<li>깊이 우선 탐색 (DFS)<ul>
<li>그래프에서 깊은 부분을 우선적으로 탐색한다.</li>
</ul>
</li>
<li>너비 우선 탐색 (BFS)<ul>
<li>그래프에서 가장 인접한 부분을 우선적으로 탐색한다.</li>
</ul>
</li>
<li>깊이 우선 탐색과 너비 우선 탐색의 경우 별도의 포스팅으로 더 자세하게 다루어볼 예정이다.</li>
</ul>
<h2 id="🌱-프로그래머스-예제로-이해하기">🌱 프로그래머스 예제로 이해하기</h2>
<pre><code>풀이할 때마다 예제가 추가됩니다.</code></pre><h3 id="✨-최소-직사각형-level-1">✨ <a href="https://school.programmers.co.kr/learn/courses/30/lessons/86491">최소 직사각형</a> (Level 1)</h3>
<pre><code class="language-js">const solution = (sizes) =&gt; {
  const sortedArr = sizes.map((arr) =&gt; arr.sort((a, b) =&gt; b - a));
  let Max_Max = 0;
  let Min_Max = 0;

  // 배열 전체를 순회하며 현재까지 확인된 값 중 최대 너비와 최대 높이를 저장한다.
  for (const [w, h] of sortedArr) {
    Max_Max = Math.max(Max_Max, w);
    Min_Max = Math.max(Min_Max, h);
  }

  return Max_Max * Min_Max;
};</code></pre>
<ul>
<li><code>sizes</code> 배열을 받은 뒤 각 사이즈마다 너비와 높이를 내림차순으로 모두 정렬한다.</li>
<li>정렬된 배열에서 가장 큰 너비와 가장 큰 높이를 찾아 곱한 값을 반환한다. </li>
<li>배열을 정렬한 뒤 각 사각형의 너비와 높이를 모두 확인하는 완전 탐색 알고리즘을 사용한다.</li>
</ul>
<h3 id="✨-모의고사-level-1">✨ <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42840">모의고사</a> (Level 1)</h3>
<pre><code class="language-js">const solution = (answers) =&gt; {
    // 각 수포자들의 정답 패턴을 저장한다. 
    const s = [[1, 2, 3, 4, 5], [2, 1, 2, 3, 2, 4, 2, 5], [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]]
    // 각 수포자들의 정답 개수를 저장할 공간
    const sum = [0, 0, 0]
    // 각 수포자들의 정답 패턴의 길이를 저장하는 공간 
    const len = [s[0].length, s[1].length, s[2].length]

    // 주어진 답안 배열을 모두 순회하며 맞은 문제 수를 구한다. 
    for(let i = 0; i &lt; answers.length; i++){
        for(let j = 0; j &lt; sum.length; j++){
            sum[j] += answers[i] === s[j][i%len[j]]
        }
    }
    // 가장 높은 점수
    const max = Math.max(...sum)
    const result = [];
     // sum이 가장 높은 점수와 일치하는 참가자들의 번호를 반환한다.
    for(let i = 0; i &lt; sum.length; i++){
        if(sum[i] === max) result.push(i+1)
    }

    return result
}</code></pre>
<h3 id="✨-소수-찾기-level-2">✨ <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42839">소수 찾기</a> (Level 2)</h3>
<pre><code class="language-js">const getNumSet = (str) =&gt; {
    const set = new Set()
     const generateCombinations = (cur, rem) =&gt; {
        if (rem.length === 0) return;

        for (let i = 0; i &lt; rem.length; i++) {
            const nextDigit = rem[i];
            const newCurrent = cur + nextDigit;
          // 현재 선택된 숫자를 제외한 나머지 숫자들로 이루어진 문자열 
          // 다음 재귀 호출에서 숫자 조합 생성 시 사용된다. 
            const newRemaining = rem.slice(0, i) + rem.slice(i + 1);
            set.add(Number(newCurrent));
            generateCombinations(newCurrent, newRemaining);
        }
    }

    generateCombinations('', str);
    return set
}

const isDec = (n) =&gt; {
    if(n &lt; 2) return false
    for(let i = 2; i &lt;= Math.sqrt(n); i++){
        if(n%i === 0){
            return false
        }
    }
    return true
}

// 가능한 모든 조합을 생성한 뒤 소수인 경우만 필터링하여 개수를 반환한다. 
const solution = (numbers) =&gt; [...getNumSet(numbers)].filter((n) =&gt; isDec(n)).length;</code></pre>
<blockquote>
<p><code>getNumSet</code></p>
</blockquote>
<ul>
<li>주어진 숫자 문자열에서 가능한 모든 조합을 생성한다.</li>
<li>중복을 피하기 위해 Set을 사용한다.</li>
<li>조합을 생성하는 함수인 <code>generateCombinations</code>을 재귀적으로 호출하여 가능한 모든 조합을 생성한다.<ul>
<li>각 숫자를 선택하고 나머지 숫자들과 조합하여 새로운 숫자를 생성한다.</li>
</ul>
</li>
<li>새로운 숫자를 Set에 저장한다. </li>
</ul>
<blockquote>
<p><code>genereateCombinations(cur, rem)</code></p>
</blockquote>
<ul>
<li><code>cur</code><ul>
<li>현재까지 생성된 조합을 나타내는 매개변수</li>
</ul>
</li>
<li><code>rem</code><ul>
<li>아직 선택되지 않은 나머지 숫자들</li>
</ul>
</li>
<li>함수는 재귀적으로 호출될 때마다 <code>rem</code> 배열의 모든 숫자를 선택해 <code>cur</code>에 이어붙여 새로운 숫자를 생성한다.<ul>
<li>생성된 숫자는 Set에 저장하여 중복을 방지한다.</li>
</ul>
</li>
<li>모든 숫자가 선택될 때까지 재귀 호출이 진행된다.<ul>
<li><code>rem.length===0</code>: 선택할 숫자가 없으면 재귀 호출을 종료한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><code>isDec</code></p>
</blockquote>
<ul>
<li>주어진 숫자가 소수인지 판별하는 함수</li>
<li>숫자가 2보다 작으면 소수가 될 수 없으므로 early return</li>
<li>2부터 해당 숫자의 제곱근까지의 모든 수로 나누어 하나라도 0으로 나누어떨어지는 값이 있는지 확인하며 소수 여부를 판별한다. </li>
</ul>
<h3 id="✨-카펫-level-2">✨ <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42842">카펫</a> (Level 2)</h3>
<pre><code class="language-js">const solution = (brown, yellow) =&gt; {
    const sum = brown + yellow
    let x = y = 0;

    for(let i = 3; i &lt; brown; i++){
        if(sum%i === 0){
            const val = sum / i
            if(i + val === (brown/2+2)){
                x = Math.max(i, val)
                y = Math.min(i, val)
                break;
            }
        }
    }

    return [x, y]
}</code></pre>
<ul>
<li>반복문을 사용하여 가능한 모든 수를 탐색하면서 조건에 맞는 정답을 구한다.</li>
<li>아래의 두 규칙을 파악해야 문제를 제대로 풀이할 수 있다.<ul>
<li><code>x * y = brown + yellow</code></li>
<li><code>x + y = (brown)/2 + 2</code></li>
</ul>
</li>
</ul>
<h3 id="✨-피로도-level-2">✨ <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87946">피로도</a> (Level 2)</h3>
<pre><code class="language-js">const getPerm = (perm, rest, result) =&gt; {
    if(rest.length === 0) return result.push(perm)
    for(let i = 0; i &lt; rest.length; i++){
        const newRest = [...rest.slice(0,i), ...rest.slice(i+1)]
        getPerm([...perm,rest[i]], newRest, result);
    }
}

const solution = (k, dungeons) =&gt; {
  // 던전을 도는 순서를 나타내는 순열 목록 
    const perm = []
    let result = 0;
    getPerm([], dungeons, perm)
    for(let i = 0; i &lt; perm.length; i++){
        let fatigue = k
        let sum = 0;
        for(let j = 0; j &lt; dungeons.length; j++){
            const target = perm[i][j]
            // 체력이 부족하면 해당 던전을 통과하지 못하고 넘어간다.
            if(fatigue &lt; target[0]) continue;
            // 체력이 충분하면 플레이어의 체력을 감소시키고 sum++
            else{
                fatigue -= target[1]
                sum++
            }
            result = Math.max(sum, result)
        }  
    }
    return result
}</code></pre>
<blockquote>
<p><code>getPerm(perm, rest, result)</code></p>
</blockquote>
<ul>
<li>순열을 생성하는 재귀 함수이다.</li>
<li><code>perm</code>: 현재까지 생성된 순열들</li>
<li><code>rest</code>: 아직 방문하지 않은 던전 목록</li>
<li><code>result</code>: 모든 던전을 방문한 뒤 생성된 순열들을 담을 결과 배열 </li>
<li>주어진 던전 리스트인 <code>rest</code>에서 가능한 모든 순열을 찾는다.<ul>
<li><code>rest</code>에서 하나의 요소를 선택해 순열에 추가한 뒤 재귀적으로 호출한다.</li>
<li>선택한 요소를 <code>perm</code>에 추가한 새로운 배열과 선택한 요소를 제외한 나머지 요소들이 포함된 새로운 <code>rest</code>가 생성된 후 재귀 호출한다.</li>
</ul>
</li>
<li>모든 던전을 검사하여 남은 배열의 길이가 0이면 순열이 완성된다.<ul>
<li>현재의 순열 <code>perm</code>을 <code>result</code>에 추가하고 함수를 종료한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>조합 생성 함수와 순열 생성 함수의 비교</p>
</blockquote>
<ul>
<li><code>generateCombinations</code><ul>
<li>조합(combination)은 <strong>순서에 관계 없이</strong> 요소들을 선택하여 만들어지는 모든 가능한 부분 집합</li>
<li>재귀적으로 호출되면서 현재 선택된 요소를 제외한 나머지 요소들로 새로운 조합을 생성한다.</li>
</ul>
</li>
<li><code>getPerm</code><ul>
<li>순열(permutation)은 요소들의 <strong>순서를 고려하여</strong> 만들어지는 모든 가능한 순서쌍</li>
<li>재귀적으로 호출되면서 현재 선택된 요소를 순열에 추가하고 다음 요소를 선택해 순열을 만든다.</li>
</ul>
</li>
</ul>
<blockquote>
<p><code>solution(k, dungeons)</code></p>
</blockquote>
<ul>
<li>가능한 모든 순열을 구한 뒤 주어진 체력 <code>k</code>를 가지고 각 순열을 탐색한다.</li>
<li>던전을 탐색하면서 체력이 0보다 작아지지 않으면 던전을 클리어할 수 있는 것으로 간주하여 <code>sum</code>에 클리어한 던전의 수를 누적한다.</li>
<li>이후 최대 클리어 가능 던전 수인 <code>result</code>와 비교하여 최대값을 갱신한다.</li>
</ul>
<h3 id="✨-모음사전-level-2">✨ <a href="https://school.programmers.co.kr/learn/courses/30/lessons/84512">모음사전</a> (Level 2)</h3>
<pre><code class="language-js">const v = ['A', 'E', 'I', 'O', 'U']

function solution(word) {
  // 가능한 모든 단어를 담는 사전 배열 
   const d = [];
  // 가능한 모든 단어의 조합을 생성하는 재귀 함수
  // 단어의 길이가 5를 초과할 경우 종료한다. 
   const makeWord = (cnt, w) =&gt; {
       if(cnt &gt; 5) return;
       d.push(w);
       for(let i = 0; i &lt; v.length; i++) makeWord(cnt+1, w + v[i])
    }

   makeWord(0, &quot;&quot;)
  // 모든 단어를 생성한 뒤 알파벳 순으로 정렬한다.
  // 첫 번째 요소는 빈 문자열이므로 제거한다. 
   d.sort().shift()

  // 주어진 단어의 인덱스를 구한다. 
   return d.indexOf(word)+1
}</code></pre>
<ul>
<li>주어진 모음을 사용해 <strong>가능한 모든 단어를 생성</strong>한 뒤 해당 단어의 순서를 찾는다.</li>
</ul>
<hr />

<h4 id="🔎-references">🔎 References</h4>
<ul>
<li><a href="https://hongjw1938.tistory.com/78">알고리즘 - 완전탐색(Exhaustive Search)</a></li>
<li><a href="https://hstory0208.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%99%84%EC%A0%84%ED%83%90%EC%83%89Exhaustive-search%EC%9D%B4%EB%9E%80">[알고리즘] 완전탐색(Exhaustive search)이란?</a></li>
<li><a href="https://velog.io/@hyehyes/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%99%84%EC%A0%84%ED%83%90%EC%83%89">[알고리즘] 완전탐색</a></li>
</ul>