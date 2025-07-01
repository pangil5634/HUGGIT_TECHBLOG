**Date**  
2025. 7. 1. 21:13

**Blog**  
Tistory

**Summary**  
<blockquote data-ke-style="style2">React.memo</blockquote>
<p data-ke-size="size16">: <b>컴포넌트 자체를 메모이제이션</b><span style="color: #000000; text-align: start;">하여 props가 바뀌지 않으면 다시 렌더링하지 않도록 한다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="color: #000000;"><span style="caret-color: #000000;">1) 사용하는 경우</span></span></b></p>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-end="435" data-start="370" data-ke-list-type="disc">
<li data-end="417" data-start="370">부모 컴포넌트가 자주 렌더링되는데, 자식 컴포넌트의 props가 변하지 않는 경우</li>
<li data-end="435" data-start="418">불필요한 리렌더링 방지 목적</li>
</ul>
<p data-ke-size="size16"><b>2) 예시</b></p>
<p data-ke-size="size16"><b>: </b>React.memo<span style="color: #000000; text-align: start;">를 사용해 부모 컴포넌트가 리렌더링되더라도 자식 컴포넌트의 props가 변하지 않으면 자식 컴포넌트의 렌더링을 생략하여 성능을 최적화한 예제</span></p>
<pre id="code_1751369499219" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>// Child.tsx
import React from 'react';

const Child = ({ value }: { value: number }) =&gt; {
  console.log('  자식 컴포넌트 렌더링');
  return &lt;div&gt;값: {value}&lt;/div&gt;;
};

// memo 적용이며, 이렇게 하면 다른 파일에서 import할 때 자동으로 memo된 최적화 버전이 import됨
export default React.memo(Child);</code></pre>
<pre id="code_1751369514832" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>// Parent.tsx
import React, { useState } from 'react';
import Child from './Child';

export default function Parent() {
  const [count, setCount] = useState(0);
  const [value, setValue] = useState(100);

  return (
    &lt;&gt;
      &lt;button onClick={() =&gt; setCount((c) =&gt; c + 1)}&gt;카운트 증가&lt;/button&gt;
      &lt;Child value={value} /&gt;
    &lt;/&gt;
  );
}</code></pre>
<p data-end="748" data-start="734" data-ke-size="size16">&nbsp;</p>
<p data-end="748" data-start="734" data-ke-size="size16"><b>(1) 최적화 포인트</b></p>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-end="838" data-start="749" data-ke-list-type="disc">
<li data-end="779" data-start="749">count가 바뀔 때마다 부모가 리렌더링되지만,</li>
<li data-end="838" data-start="780">value는 변하지 않기 때문에<span>&nbsp;</span>Child는<span>&nbsp;</span>React.memo로 렌더링을 막을 수 있다.</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">3) 결론</p>
<p data-ke-size="size16"><b>: 부모는 변했지만 자식한테 전달된 값은 그대로니까, 굳이 다시 그릴 필요가 없다</b><br /><span style="color: #000000; text-align: start;">&rarr; 그래서 React가 렌더링을 "스킵"해주는 거예요.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">useMemo</blockquote>
<p data-ke-size="size16">: <b>값(value)을 메모이제이션</b><span style="color: #000000; text-align: start;">한다.</span><span style="color: #000000; text-align: start;"> </span><span style="color: #000000; text-align: start;">즉, 특정 연산의 결과를<span>&nbsp;</span></span><b>캐싱</b><span style="color: #000000; text-align: start;">해서<span>&nbsp;</span></span><b>의존값이 바뀌지 않으면 연산을 다시 하지 않는다.&nbsp;</b></p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>0) 사용 방법</b></p>
<pre id="code_1751370426567" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>const memoizedValue = useMemo(() =&gt; 계산식, [의존성배열]);</code></pre>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>계산식: 복잡하거나 비용이 많이 드는 연산</li>
<li>의존성 배열: 값이 바뀌면 다시 계산 / 안 바뀌면 이전 결과 재사용</li>
</ul>
<p data-ke-size="size16"><b>1) 사용하는 경우</b></p>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li>렌더링 시 비용이 큰 연산(heavy computation)이 수행될 경우</li>
<li>연산 결과가 동일한데도 매번 계산하는<span>&nbsp;</span><b>불필요한 연산을 방지</b>하고 싶을 때</li>
<li>복잡한 계산이 많은 컴포넌트에서<span>&nbsp;</span><b>불필요한 성능 낭비 방지</b></li>
</ul>
<p data-ke-size="size16"><b>2) 예시</b></p>
<p data-ke-size="size16"><b>: </b>useMemo<span style="color: #000000; text-align: start;">를 사용해 </span>input<span style="color: #000000; text-align: start;">값이 바뀔 때만 무거운 계산을 실행하고, 그렇지 않으면 이전 계산 결과를 재사용하여 렌더링 성능을 최적화한 예제</span></p>
<pre class="javascript" style="color: #000000; text-align: start;" data-ke-language="javascript"><code>// Calculator.js
import React, { useState, useMemo } from 'react';

function heavyCalculation(num) {
  console.log('  계산 중...');
  let result = 0;
  for (let i = 0; i &lt; 100000000; i++) {
    result += i % num;
  }
  return result;
}

export default function Calculator() {
  const [count, setCount] = useState(0);
  const [input, setInput] = useState(5);

  // input이 바뀔 때만 계산이 다시 일어남
  const calculated = useMemo(() =&gt; heavyCalculation(input), [input]);

  return (
    &lt;&gt;
      &lt;input
        type="number"
        value={input}
        onChange={(e) =&gt; setInput(Number(e.target.value))}
      /&gt;
      &lt;p&gt;계산 결과: {calculated}&lt;/p&gt;
      &lt;button onClick={() =&gt; setCount((c) =&gt; c + 1)}&gt;카운트 증가&lt;/button&gt;
    &lt;/&gt;
  );
}</code></pre>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>(1) 최적화 포인트</b></p>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li>count는 계산과는 무관한 상태이지만, 값이 바뀌면<span>&nbsp;</span>Calculator<span>&nbsp;</span>컴포넌트가 리렌더링됨</li>
<li>useMemo를 쓰지 않으면<span>&nbsp;</span>heavyCalculation(input)이<span>&nbsp;</span><b>매번 다시 실행됨</b><span>&nbsp;</span>&rarr; 비효율 발생</li>
<li>useMemo를 쓰면<span>&nbsp;</span>input이 바뀌지 않으면<span>&nbsp;</span><b>이전 계산 결과를 재사용</b></li>
</ul>
<p data-ke-size="size16"><b>3) 결론</b></p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">: 계산 결과가 이전과 같다면 굳이 다시 계산할 필요가 없다<br />&rarr; 그래서<span>&nbsp;</span>useMemo가<span>&nbsp;</span><b>계산 결과를 기억하고 있다가</b><span>&nbsp;</span>그대로 써주는 것이다.<br />&rarr; 불필요한 계산 로드를 줄이고, 렌더링 시<span>&nbsp;</span><b>퍼포먼스를 지키는 전략이다.</b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">useCallback</blockquote>
<p data-ke-size="size16">: <b>함수(function)를 메모이제이션</b><span style="color: #000000; text-align: start;">한다.</span><span style="color: #000000; text-align: start;"> </span><span style="color: #000000; text-align: start;">매번 새로운 함수 객체가 생성되는 걸 막고,<span>&nbsp;</span></span><b>같은 참조를 유지</b><span style="color: #000000; text-align: start;">함.</span><span style="color: #000000; text-align: start;"></span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>0) 사용 방법</b></p>
<pre id="code_1751371754245" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>const memoizedCallback = useCallback(() =&gt; {
  // 실행할 함수 내용
}, [의존성배열]);</code></pre>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>1) 사용하는 경우</b></p>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li><b>자식 컴포넌트에 함수를 props로 전달할 때</b></li>
<li>부모 컴포넌트가 리렌더링되면서 함수 객체가 매번 새로 만들어지는 현상을 막고 싶을 때</li>
<li>React.memo와 함께 사용하면<span>&nbsp;</span><b>props 비교 시 참조값이 유지되기 때문에 리렌더링 방지</b>에 효과적</li>
</ul>
<p data-ke-size="size16"><b>2) 예시</b></p>
<p data-ke-size="size16"><b>:</b> useCallback<span style="color: #000000; text-align: start;">을 사용하여 함수의 참조값을 고정함으로써, 부모 컴포넌트가 리렌더링되어도</span>React.memo<span style="color: #000000; text-align: start;">로 감싼 자식 컴포넌트의 불필요한 렌더링을 방지하는 예시</span></p>
<pre class="javascript" style="color: #000000; text-align: start;" data-ke-language="javascript"><code>// Child.js
import React from 'react';

function Child({ onClick }) {
  console.log('  자식 렌더링');
  return &lt;button onClick={onClick}&gt;자식 버튼&lt;/button&gt;;
}

export default React.memo(Child); // memo 적용</code></pre>
<pre class="javascript" style="color: #000000; text-align: start;" data-ke-language="javascript"><code>// Parent.js
import React, { useState, useCallback } from 'react';
import Child from './Child';

export default function Parent() {
  const [count, setCount] = useState(0);

  // 매 렌더링마다 새로 만들어지는 함수 (비효율)
  // const handleClick = () =&gt; console.log('클릭됨');

  // useCallback 사용 &rarr; 참조 유지됨
  const handleClick = useCallback(() =&gt; {
    console.log('클릭됨');
  }, []);

  return (
    &lt;&gt;
      &lt;button onClick={() =&gt; setCount((c) =&gt; c + 1)}&gt;카운트 증가&lt;/button&gt;
      &lt;Child onClick={handleClick} /&gt;
    &lt;/&gt;
  );
}</code></pre>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>(1) 최적화 포인트</b></p>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li>Child<span>&nbsp;</span>컴포넌트는<span>&nbsp;</span>React.memo로 감싸져 있지만</li>
<li>부모가 리렌더링될 때마다<span>&nbsp;</span>handleClick<span>&nbsp;</span>함수가<span>&nbsp;</span><b>새로운 객체로 생성</b>되면, 자식도 리렌더링된다.</li>
<li>useCallback을 사용하면 함수의<span>&nbsp;</span><b>참조값이 유지</b>되어<span>&nbsp;</span>Child는<span>&nbsp;</span><b>렌더링을 건너뛴다.</b></li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>3) 결론</b></p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">: 함수 로직은 똑같은데, 매번 새로운 객체로 만들어지면 자식 컴포넌트 입장에서는 &ldquo;다른 함수&rdquo;로 인식한다.<br />&rarr; 그래서<span>&nbsp;</span>useCallback을 쓰면<span>&nbsp;</span><b>같은 참조를 유지해서</b><br /><b>React.memo와 함께 진짜로 바뀐 props만 감지하도록</b><span>&nbsp;</span>도와주는 것이다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>

**Link**  
https://pangil-log.tistory.com/373