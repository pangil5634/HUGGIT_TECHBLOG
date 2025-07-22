**Date**  
2025. 7. 22. 22:36

**Blog**  
Tistory

**Summary**  
<blockquote style="background-color: #fcfcfc; color: #666666; text-align: left;" data-ke-style="style3">문제 링크 :<span><span>&nbsp;</span><a href="https://www.acmicpc.net/problem/2644">https://www.acmicpc.net/problem/2644</a></span></blockquote>
<p><figure class="imageblock alignCenter" data-ke-mobileStyle="widthOrigin" data-origin-width="1190" data-origin-height="1548"><span data-url="https://blog.kakaocdn.net/dn/cmbBzD/btsPsX8w3Zp/Nac73P6CJSERG6EM7mTii0/img.png" data-phocus="https://blog.kakaocdn.net/dn/cmbBzD/btsPsX8w3Zp/Nac73P6CJSERG6EM7mTii0/img.png"><img src="https://blog.kakaocdn.net/dn/cmbBzD/btsPsX8w3Zp/Nac73P6CJSERG6EM7mTii0/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmbBzD%2FbtsPsX8w3Zp%2FNac73P6CJSERG6EM7mTii0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" loading="lazy" width="1190" height="1548" data-origin-width="1190" data-origin-height="1548"/></span></figure>
</p>
<p style="color: #333333; text-align: start;" data-ke-size="size16">&nbsp;</p>
<blockquote style="color: #666666; text-align: left;" data-ke-style="style2">문제 탐색하기</blockquote>
<p style="color: #333333; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #333333; text-align: start;" data-ke-size="size16"><b>1) 문제 분석</b></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li style="color: #000000;" data-end="132" data-start="114"><span>line1 : 전체 사람의 수 : n<span>&nbsp;</span></span><span>&nbsp; &nbsp;<span>&nbsp;</span></span></li>
<li style="color: #000000;" data-end="132" data-start="114"><span>line2 : 촌수 계산 인원 : a, b<span>&nbsp;</span></span><span>&nbsp; &nbsp;<span>&nbsp;</span></span></li>
<li style="color: #000000;" data-end="132" data-start="114"><span>line3 : 부모자식 관계의 수 : m<span>&nbsp;</span></span><span>&nbsp; &nbsp;<span>&nbsp;</span></span></li>
<li style="color: #000000;" data-end="132" data-start="114"><span>line4 : 부모 번호, 자식 번호<span>&nbsp;</span></span><span>&nbsp; &nbsp;<span>&nbsp;</span></span></li>
<li style="color: #000000;" data-end="132" data-start="114"><span>각 사람의 부모는 최대 한 명<span>&nbsp;</span></span><span>&nbsp; &nbsp;<span>&nbsp;</span></span></li>
<li style="color: #000000;" data-end="132" data-start="114"><span>친척 관계가 없는 경우 -1을 출력</span></li>
</ul>
<p style="color: #333333; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #333333; text-align: start;" data-end="77" data-start="61" data-ke-size="size16"><b>2) 가능한 시간복잡도</b></p>
<p style="color: #333333; text-align: start;" data-end="77" data-start="61" data-ke-size="size16"><span style="font-family: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', 'Apple SD Gothic Neo', Arial, sans-serif; letter-spacing: 0px;">(1) 입력 처리</span></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li style="color: #000000;" data-end="269" data-start="232">첫 번째 줄 ~ 세 번째 줄 입력 처리 : O(1) * 3 = O(1)</li>
<li style="color: #000000;" data-end="269" data-start="232">네 번째 줄 처리 : O(m)</li>
</ul>
<p style="color: #333333; text-align: start;" data-end="200" data-start="185" data-ke-size="size16">(2) 부모자식관계 추출 -&gt; O(<span style="color: #000000; text-align: left;">m</span>)</p>
<p style="color: #333333; text-align: start;" data-end="200" data-start="185" data-ke-size="size16">(3) 방문 여부 기록, 인접 리스트 배열 선언 -&gt; O(n)</p>
<p style="color: #333333; text-align: start;" data-end="200" data-start="185" data-ke-size="size16">(4) 인접 리스트 배열 삽입 -&gt; O(<span style="color: #000000; text-align: left;">m</span>)</p>
<p style="color: #333333; text-align: start;" data-end="200" data-start="185" data-ke-size="size16">(5) 탐색 -&gt; O(n + m)</p>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li>최악의 경우,<span>&nbsp;</span><span><b>노드 수 n</b></span>개의 노드를 모두 방문하고,</li>
<li>각 노드에서 연결된 간선을 모두 확인 (총 간선 m개 확인)</li>
</ul>
<p style="color: #333333; text-align: start;" data-end="200" data-start="185" data-ke-size="size16">(6) 출력 -&gt; O(1)</p>
<p style="color: #333333; text-align: start;" data-end="414" data-start="395" data-ke-size="size16">(7) 전체 시간복잡도</p>
<ul style="list-style-type: disc;" data-end="489" data-start="415" data-ke-list-type="disc">
<li data-start="365" data-end="393">입력 처리 : O(1)</li>
<li data-start="365" data-end="393">부모자식관계 추출 : O(m)</li>
<li data-start="365" data-end="393">배열 선언<span>&nbsp;</span>: O(m)</li>
<li data-start="365" data-end="393">배열 삽입<span>&nbsp;</span>: O(m)</li>
<li data-start="365" data-end="393">탐색<span>&nbsp;</span>: O(n + m)</li>
<li data-start="365" data-end="393">출력<span style="color: #333333; text-align: left;"><span>&nbsp;</span>: O(1)</span><br />-&gt; 총합 : O(n + m)</li>
</ul>
<p style="color: #333333; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #333333; text-align: start;" data-end="513" data-start="496" data-ke-size="size16"><b>3) 알고리즘 선택 이유</b></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>이 문제는 두 사람 사이의 <b>촌수(최단 거리)</b>를 계산해야 한다. <span style="color: #000000; letter-spacing: 0px;">사람들 사이의 관계는</span><span style="color: #000000; letter-spacing: 0px;">&nbsp;</span><span style="color: #000000; letter-spacing: 0px;"><b>부모-자식 관계</b></span><span style="color: #000000; letter-spacing: 0px;">로 구성된</span><span style="color: #000000; letter-spacing: 0px;">&nbsp;</span><span style="color: #000000; letter-spacing: 0px;"><b>그래프 형태</b></span><span style="color: #000000; letter-spacing: 0px;">이며, </span><span style="color: #000000; letter-spacing: 0px;">특정 두 노드(사람) 사이의 가장 짧은 경로를 찾아야 한다.</span></li>
<li><span style="color: #000000; letter-spacing: 0px;">따라서</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람들 간의 관계는<span>&nbsp;</span><span><b>무방향 그래프</b></span>로 구성하고,</li>
<li><b>BFS(너비 우선 탐색)</b>을 사용하여 두 사람 사이의 최단 경로(촌수)를 계산하는 방식이 가장 적합하다.</li>
</ul>
</li>
<li>BFS는 그래프 내에서&nbsp;최단 거리를 구할 때 가장 효율적인 방법이다.</li>
<li><span style="color: #000000; letter-spacing: 0px;">관계의 개수(m)와 사람 수(n)가 비교적 작고 트리 구조가 아닌 일반적인 그래프 형태이기 때문에,</span></li>
<li><b>BFS 탐색 O(n + m)</b><span style="color: #000000; letter-spacing: 0px;">으로 충분히 빠르게 문제를 해결할 수 있다.<br /></span><span style="color: #000000; letter-spacing: 0px;">-&gt; </span><b>즉, 이 문제는 BFS(너비 우선 탐색) 기반으로 해결하는 것이 가장 직관적이고 효율적인 선택이다.</b></li>
</ul>
<blockquote style="background-color: #fcfcfc; color: #666666; text-align: left;" data-ke-style="style3">잠깐!<span> <span style="background-color: #fcfcfc; color: #006dd7; text-align: left;">그래프, BFS/DFS</span></span>에 대한 간단한 설명, 그리고 관련 예시 문제는<span>&nbsp;</span><a href="https://pangil-log.tistory.com/430" target="_blank" rel="noopener">여기</a>를 참고하자.</blockquote>
<p style="color: #333333; text-align: start;" data-ke-size="size16">&nbsp;</p>
<blockquote style="color: #666666; text-align: left;" data-ke-style="style2">코드 설계하기</blockquote>
<p style="color: #333333; text-align: start;" data-ke-size="size16"><b>1. 실행 구조</b></p>
<p style="color: #333333; text-align: start;" data-ke-size="size16">1) 사용자 입력</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>전체 사람 수(n), 촌수를 계산할 두 사람(a, b), 부모-자식 관계 수(m), 그리고 m개의 부모-자식 관계 데이터를 입력받는다.</li>
<li>각 데이터를 공백 기준으로 나눈 후 숫자로 변환하여 사용한다.</li>
</ul>
<p data-ke-size="size16">2) <span style="letter-spacing: 0px;">그래프 초기화</span></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람들 사이의 부모-자식 관계를 양방향으로 연결하여 인접 리스트 형태의 그래프를 생성한다.</li>
<li>방문 여부를 확인하기 위한 visited 배열도 함께 초기화한다.</li>
</ul>
<p data-ke-size="size16">3) BFS 탐색 함수 구현</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>BFS(너비 우선 탐색) 방식을 사용하여 시작 사람(a)으로부터 목표 사람(b)까지 이동하며 촌수를 계산한다.</li>
<li>큐(queue)를 이용하여 현재 사람과 촌수를 함께 저장하고, 큐에서 꺼낼 때마다 목표 사람인지 확인한다.</li>
<li>부모, 자식으로 연결된 사람들을 모두 탐색하며, 이미 방문한 사람은 다시 방문하지 않도록 한다.</li>
</ul>
<p data-ke-size="size16">4) 탐색 및 출력</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>BFS를 실행하여 두 사람 사이의 촌수를 계산하고, 결과를 출력한다.</li>
<li>만약 두 사람 사이에 연결된 경로가 없다면 -1을 출력한다.</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p style="color: #333333; text-align: start;" data-ke-size="size16"><b>2. 고민이 되었던 부분</b></p>
<p style="color: #333333; text-align: start;" data-ke-size="size16">: 두 사람이 서로 얼마나 가까운지(촌수)를 구하기 위해 어떤 알고리즘을 사용할지 고민하게 되었다. 결국 이 문제는 사람들 간의 관계를 그래프로 구성한 후, 두 사람 사이의 최단 경로를 찾는 문제라는 점을 인식했다. 따라서 다음 두 가지 전제를 세웠다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">첫 번째, 부모-자식 관계는 한 방향이 아니라 양방향으로 연결된 관계로 이해해야 했다. 부모에서 자식으로만 이동할 수 있는 게 아니라, 자식에서 부모로도 이동할 수 있기 때문에 인접 리스트를 무조건 양방향으로 구성해야 했다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">두 번째, 최단 거리 탐색을 위해 BFS(너비 우선 탐색)를 선택했다. BFS는 시작 노드로부터 인접한 노드를 모두 순서대로 탐색하면서 최단 경로를 찾는 데 가장 적합한 알고리즘이다. 따라서 큐를 이용한 BFS를 통해 촌수를 자연스럽게 계산할 수 있도록 구현했다. 큐에는 현재 사람 번호와 촌수를 함께 저장해 촌수를 따로 관리할 수 있도록 구성했다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">이렇게 함으로써, 두 사람이 서로 연결된 경우 최단 촌수를 바로 구할 수 있고, 연결되지 않은 경우 -1을 반환할 수 있는 구조를 완성할 수 있었다.</p>
<p style="color: #333333; text-align: start;" data-ke-size="size16"><br /><br /></p>
<blockquote style="color: #666666; text-align: left;" data-ke-style="style2">정답 코드</blockquote>
<pre id="code_1753175118200" style="background-color: #f8f8f8; color: #383a42; text-align: start;" data-ke-language="javascript" data-ke-type="codeblock"><code>// 사용 언어 : Javascript

// 입력 처리
const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().trim().split("\n");

// 첫 번째 줄 : n(전체 사람의 수)
const n = Number(input[0]);
input.shift();

// 두 번째 줄 : a, b(촌수 계산 인원)
const [a, b] = input[0].split(" ").map(Number);
input.shift();

// 세 번째 줄 : m(부모자식 관계의 수)
const m = Number(input[0]);
input.shift();

// 부모자식 관계 정보 추출
const edges = [];
input.forEach(edge =&gt; edges.push(edge.split(" ").map(Number)));

// 방문 여부 기록 배열
const visited = new Array(n + 1).fill(false);

// 인접 리스트 형태로 그래프 초기화
const graph = Array.from({ length: n + 1 }, () =&gt; []);

// 무방향 그래프 : 서로 연결된 관계 추가
for (let [u, v] of edges) {
    graph[u].push(v);
    graph[v].push(u);
}

// BFS 함수 : 시작 노드(start)에서 목표 노드(target)까지 몇 촌인지 계산하는 함수
function bfs(start, target) {

    // 큐(queue)에 시작 노드와 현재 촌수를 넣음
    // 큐에는 [사람 번호, 지금까지 센 촌수] 형태로 저장됨
    const queue = [[start, 0]];

    // 시작 노드는 방문 처리 (자기 자신은 다시 방문하지 않도록)
    visited[start] = true;

    // 큐가 빌 때까지 반복 (탐색 계속)
    while (queue.length) {

        // 큐에서 하나 꺼내기 : 현재 사람과 지금까지의 촌수
        const [current, count] = queue.shift();

        // 만약 목표 사람을 찾았다면? -&gt; 지금까지의 촌수를 바로 반환
        if (current === target) {
            return count;
        }

        // 현재 사람과 연결된 모든 사람을 하나씩 확인
        graph[current].forEach(next =&gt; {

            // 아직 방문하지 않은 사람이라면
            if (!visited[next]) {
                visited[next] = true;              // 방문 처리
                queue.push([next, count + 1]);     // 큐에 추가 (촌수 1 증가시켜서)
            }

        });
    }

    // 큐를 다 돌았는데도 목표 사람을 찾지 못했다면 -&gt; 서로 연결되지 않은 상태
    return -1;
}

const result = bfs(a, b);
console.log(result);</code></pre>
<p style="color: #333333; text-align: start;" data-ke-size="size16">&nbsp;</p>
<blockquote style="color: #666666; text-align: left;" data-ke-style="style2">마무리하며</blockquote>
<p style="color: #333333; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-is-only-node="" data-is-last-node="" data-end="819" data-start="615" data-ke-size="size16">어제 따로 공부했던<span>&nbsp;</span><span><b>BFS</b></span>,<span>&nbsp;</span><span><b>DFS</b></span>, 그리고<span>&nbsp;</span><span><b>그래프</b></span><span>&nbsp;</span>개념이 오늘 이 문제를 풀면서 확실히 도움이 되었다는 걸 실감했다. 단순히 개념으로만 이해했을 때는 그냥 노드와 간선을 돌면서 탐색하는 방식 정도로 생각했는데, 오늘 이 문제를 통해 그게 실제로 &lsquo;사람들의 관계&rsquo;를 탐색하는 데 적용될 수 있다는 걸 몸으로 느낀 것 같다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">특히<span>&nbsp;</span><span><b>BFS</b></span>가 왜 &lsquo;최단 거리&rsquo;를 찾는 데 적합한지, 이론으로는 알았지만 직접 큐를 이용해 촌수를 하나씩 세어가며 구현하면서 훨씬 더 명확하게 이해할 수 있었다. 단순히 깊게 파고들기보단 넓게 펼치면서 탐색하는 과정 속에서 자연스럽게 거리를 계산할 수 있다는 걸 코드로 경험한 게 큰 도움이 되었다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">또한,<span>&nbsp;</span><span><b>부모-자식 관계를 그래프로 표현</b></span>하고, 그것을 양방향으로 처리하는 것 역시 어제 공부했던 그래프의 구조가 떠올랐기에 바로 적용할 수 있었다. 만약 이런 개념을 미리 공부하지 않았다면 단방향 관계로만 생각해서 문제를 계속 꼬이게 풀었을 것 같다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">이번 문제를 통해 단순히 개념을 아는 것과, 실제 문제에 적용할 수 있는 것은 다르다는 것을 다시 배웠다. 알고리즘을 외우는 게 아니라 &lsquo;언제 써야 하는지&rsquo;, &lsquo;왜 써야 하는지&rsquo;를 이해하는 게 중요하다는 걸 실감했다. 앞으로도 문제를 풀 때, 개념이 어떻게 실전에서 쓰이는지를 하나씩 체감해 가고 싶다. 어제 공부한 내용이 단순한 지식이 아니라, 오늘 실전에서 무기가 되어준 느낌이었다.</p>

**Link**  
https://pangil-log.tistory.com/431