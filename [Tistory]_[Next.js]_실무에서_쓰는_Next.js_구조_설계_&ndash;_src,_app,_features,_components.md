**Date**  
2025. 7. 1. 15:11

**Blog**  
Tistory

**Summary**  
<p data-ke-size="size16"><span>프로젝트가 커질수록 이런 경험, 한 번쯤은 해봤을 것이다.</span></p>
<p data-ke-size="size16"><br /><span>app/,<span>&nbsp;</span>components/,<span>&nbsp;</span>utils/<span>&nbsp;</span>안에 파일이 정체 불명의(name.conflict)처럼 쌓이다 보니 "이걸 어디에 넣어야 하지?" 며 5분을 검색하게 된다. 누구나 겪는 이 문제는 단순한 디렉토리 정리가 아니다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="237" data-start="123" data-ke-size="size16"><span>Next.js 공식 문서는 &ldquo;폴더와 파일 구조는 자유지만, 제대로 설계하면 유지보수와 협업에 큰 도움이 된다&rdquo;고 조언한다.</span><span>&nbsp;</span><span>실제 개발자들도 공감하는데, 다음은 Reddit에서 나온 이야기다:</span></p>
<blockquote data-end="316" data-start="239" data-ke-style="style3">
<p data-end="316" data-start="241" data-ke-size="size16"><i>&ldquo;I use a feature‑based folder structure to keep things organized and scalable.&rdquo;</i></p>
</blockquote>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="color: #666666; text-align: start;">커뮤니티 한 회원은 기능 단위로 폴더를 나누는 구조 덕분에 &ldquo;집중해서 개발하고, 나중에 확장하기도 쉬워졌다&rdquo;고 평가했다. 이런 배경 안에서 이 글은</span><span style="color: #666666; text-align: start;">&nbsp;</span><b>실무 환경에서 확장성과 협업을 고려한 Next.js + TypeScript + Tailwind 기반 구조 설계 전략</b><span style="color: #666666; text-align: start;">을 단계별로 제시하고자 한다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">1.&nbsp;src&nbsp;및&nbsp;app&nbsp;디렉토리 구조</blockquote>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">Next.js 13 이상에서는<span>&nbsp;</span>app/<span>&nbsp;</span>폴더를 사용하여 라우팅 구조를 정의하고,<span>&nbsp;</span>src/<span>&nbsp;</span>내부에서 애플리케이션 코드를 관리하는 패턴이 권장된다.<br />공식 문서에서는 아래와 같은 구조를 제안한다 (<a href="https://nextjs.org/docs/app/getting-started/project-structure?utm_source=chatgpt.com">nextjs.org</a>,<span>&nbsp;</span><a href="https://sentry.io/answers/next-js-directory-organisation-best-practices/?utm_source=chatgpt.com">sentry.io</a>):</p>
<pre class="crystal" style="color: #000000; text-align: start;"><code>src/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   └── ...
├── components/
├── lib/
├── utils/
├── hooks/
├── types/
└── styles/
</code></pre>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">2.&nbsp;app/&nbsp;내부 구조 설계</blockquote>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li>폴더 이름이 URL 경로가 된다.</li>
<li>(group)/<span>&nbsp;</span>형식의<span>&nbsp;</span><b>Route Group</b>을 사용하면 URL 경로에 영향을 주지 않고 기능별 묶음 가능 (<a href="https://nextjs.org/docs/app/getting-started/project-structure?utm_source=chatgpt.com">nextjs.org</a>).</li>
<li>_private/<span>&nbsp;</span><u>언더스코어</u> 폴더를 사용하면 라우팅에서 제외되는<span>&nbsp;</span><b>Private Folder</b><span>&nbsp;</span>역할 수행 (<a href="https://nextjs.org/docs/app/getting-started/project-structure?utm_source=chatgpt.com">nextjs.org</a>).<br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><i><span style="color: #000000; text-align: start;">Next.js의<span>&nbsp;</span></span>app/<span style="color: #000000; text-align: start;"><span>&nbsp;</span>디렉토리 구조에서는 언더스코어(</span>_<span style="color: #000000; text-align: start;">)로 시작하는 폴더를 라우팅에서<span>&nbsp;</span></span><b>자동으로 제외</b><span style="color: #000000; text-align: start;">한다. 즉,&nbsp;</span>app/_components/<span style="color: #000000; text-align: start;">처럼 폴더명을<span>&nbsp;</span></span>_<span style="color: #000000; text-align: start;">로 시작하면<span>&nbsp;</span></span><b>URL 경로에는 포함되지 않고</b><span style="color: #000000; text-align: start;">, 해당 경로를 내부적으로만 사용할 수 있다.</span></i></li>
<li><i><span style="color: #000000; text-align: start;">간단히 말해,<span>&nbsp;</span></span>_components<span style="color: #000000; text-align: start;">,<span>&nbsp;</span></span>_lib<span style="color: #000000; text-align: start;">,<span>&nbsp;</span></span>_layouts<span style="color: #000000; text-align: start;"><span>&nbsp;</span>같은 폴더는<span>&nbsp;</span></span><b>클린한 라우팅 구조</b><span style="color: #000000; text-align: start;">를 유지하면서도<span>&nbsp;</span></span><b>기능별 정리</b><span style="color: #000000; text-align: start;">를 가능하게 해주는 유용한 구조이다.</span></i></li>
</ul>
</li>
</ul>
<pre class="stylus" style="color: #000000; text-align: start;"><code>app/
├── layout.tsx
├── page.tsx
├── (dashboard)/
│   ├── page.tsx
│   └── _components/
└── blog/
    ├── page.tsx
    ├── [slug]/
    │   └── page.tsx
    └── metadata.ts
</code></pre>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">3. 기능(feature)-기반 모듈 구조</blockquote>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">대형 프로젝트에서는<span>&nbsp;</span><b>Feature 기반 구조</b>를 사용하는 것이 유지보수와 확장성 측면에서 유리하다 (<a href="https://www.reddit.com/r/nextjs/comments/1e4juvk/how_do_you_structure_files_and_directories_in/?utm_source=chatgpt.com">reddit.com</a>).</p>
<pre class="typescript" style="color: #000000; text-align: start;" data-ke-language="typescript"><code>예시:

src/features/
└── cart/
    ├── Cart.tsx
    ├── CartItem.tsx
    ├── useCart.ts
    └── cart.types.ts</code></pre>
<p style="color: #000000; text-align: start;" data-ke-size="size16">Reddit 실무자들은 다음과 같이 평가했다:</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">4. 재사용 UI 컴포넌트 분리</blockquote>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li>components/ui/: 버튼, 모달, 입력 등 범용 컴포넌트 저장</li>
<li>components/features/: 특정 feature에 종속된 UI 저장</li>
<li>UI와 로직은 철저히 분리하여 모듈화 (<a href="https://www.wisp.blog/blog/the-ultimate-guide-to-organizing-your-nextjs-15-project-structure?utm_source=chatgpt.com">wisp.blog</a>,<span>&nbsp;</span><a href="https://www.robinwieruch.de/react-folder-structure/?utm_source=chatgpt.com">robinwieruch.de</a>)</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">5. 훅, 라이브러리, 유틸, 상태관리 분리</blockquote>
<ul style="list-style-type: disc; color: #000000; text-align: start;" data-ke-list-type="disc">
<li>hooks/: 커스텀 훅 (useForm, useAuth 등)</li>
<li>lib/: API 호출, 외부 서비스 래퍼, DB 연결</li>
<li>utils/: 날짜&middot;문자열 포맷, 도우미 함수</li>
<li>store/: Zustand, Redux 등의 전역 상태관리 로직</li>
<li>types/: 공통 TypeScript 타입 정의 (<a href="https://dev.to/bajrayejoon/best-practices-for-organizing-your-nextjs-15-2025-53ji?utm_source=chatgpt.com">dev.to</a>,<span>&nbsp;</span><a href="https://www.wisp.blog/blog/the-ultimate-guide-to-organizing-your-nextjs-15-project-structure?utm_source=chatgpt.com">wisp.blog</a>,<span>&nbsp;</span><a href="https://nextjsstarter.com/blog/nextjs-14-project-structure-best-practices/?utm_source=chatgpt.com">nextjsstarter.com</a>)</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">6. 실제 예시 구조 (중대형 프로젝트)</blockquote>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">다음은 실무에 바로 적용 가능한 예시 구조이다:</p>
<pre class="stylus" style="color: #000000; text-align: start;"><code>src/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   ├── (auth)/
│   │   ├── login/page.tsx
│   │   └── register/page.tsx
│   └── dashboard/
│       ├── layout.tsx
│       ├── page.tsx
│       └── settings/page.tsx
├── components/
│   ├── ui/
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   ├── Button.test.tsx
│   │   │   └── index.ts
│   │   └── Modal/
│   └── features/
│       └── blog/
│           ├── PostCard/
│           └── CategoryList/
├── features/
│   └── cart/
│       ├── Cart.tsx
│       ├── cart.types.ts
│       └── useCart.ts
├── hooks/
│   ├── useForm.ts
│   └── useMediaQuery.ts
├── lib/
│   └── api/
│       └── getBlogPosts.ts
├── utils/
│   └── formatting.ts
├── store/
│   └── authStore.ts
├── types/
│   └── blog.types.ts
└── styles/
    └── globals.css
</code></pre>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">해당 예시는 &ldquo;The Ultimate Guide to Organizing Your Next.js 15 Project Structure&rdquo;에서 제시된 중대형 구조를 참고한 것이다 (<a href="https://www.wisp.blog/blog/the-ultimate-guide-to-organizing-your-nextjs-15-project-structure?utm_source=chatgpt.com">wisp.blog</a>).</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">7. 깊이 및 colocaton 원칙</blockquote>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>1) 컴포넌트 깊이 3~4레벨 이내 유지 권장 .</b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">프로젝트가 커질수록 폴더 안에 폴더, 또 그 안에 폴더&hellip; 이렇게<span>&nbsp;</span><b>너무 깊게 구조화되면</b><span>&nbsp;</span>오히려 찾기도 어렵고, import 경로도 복잡해진다.</p>
<p style="color: #000000; text-align: start;" data-end="238" data-start="211" data-ke-size="size16">예를 들어 이런 경로는<span>&nbsp;</span><b>좋지 않은 예</b>이다:</p>
<div>
<pre id="code_1751349975623" class="typescript" data-ke-language="typescript" data-ke-type="codeblock"><code>src/components/ui/buttons/primary/desktop/variant1/Button.tsx</code></pre>
</div>
<p style="color: #000000; text-align: start;" data-end="380" data-start="311" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="380" data-start="311" data-ke-size="size16">이처럼 5단계 이상 깊어지면 유지보수가 어려워지므로, 일반적으로는<span>&nbsp;</span><b>3~4단계 이내로</b><span>&nbsp;</span>폴더 깊이를 제한하는 것이 좋다:</p>
<div>
<div>
<pre id="code_1751349986126" class="typescript" data-ke-language="typescript" data-ke-type="codeblock"><code>src/components/Button/Button.tsx ✅ src/features/blog/PostCard.tsx ✅</code></pre>
</div>
<div>&nbsp;</div>
<div><span style="color: #000000; letter-spacing: 0px;">즉,</span><span style="color: #000000; letter-spacing: 0px;">&nbsp;</span><b>찾기 쉽고, import 경로가 짧을수록 좋다.</b></div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>2) Colocation 원칙: 관련된 파일은 가까이 두자</b></p>
</div>
<p style="color: #000000; text-align: start;" data-end="630" data-start="542" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="630" data-start="542" data-ke-size="size16">Colocation(콜로케이션)이란,<span>&nbsp;</span><b>서로 연관된 코드끼리 같은 폴더에 배치</b>하는 것을 의미한다. 이를 통해<span>&nbsp;</span><b>이해와 관리가 훨씬 쉬워진다.</b></p>
<p style="color: #000000; text-align: start;" data-end="683" data-start="632" data-ke-size="size16">예를 들어, 특정 컴포넌트에만 사용하는 스타일, 타입, 훅이 있다면 이렇게 정리할 수 있다:</p>
<div>
<div>
<pre id="code_1751350013702" class="typescript" data-ke-language="typescript" data-ke-type="codeblock"><code>src/components/PostCard/
├── PostCard.tsx
├── PostCard.module.css
├── usePostCard.ts
└── postCard.types.ts</code></pre>
<p data-ke-size="size16">&nbsp;</p>
</div>
<div>&nbsp;</div>
<div><span style="color: #000000; letter-spacing: 0px;">이렇게 하면 PostCard 컴포넌트에 관련된 모든 파일이 한눈에 들어오고,</span><span style="color: #000000; letter-spacing: 0px;">&nbsp;</span><b>다른 곳에 영향 없이 유지보수할 수 있다.</b></div>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">8. Barrel 파일 (index.ts) 활용</blockquote>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">components/ui/Button/index.ts처럼 index 파일을 활용하면 import 경로를 간단하게 정리할 수 있다 .</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>1) Barrel 파일이란?</b></p>
<p style="color: #000000; text-align: start;" data-end="235" data-start="125" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="235" data-start="125" data-ke-size="size16">index.ts<span>&nbsp;</span>파일은<span>&nbsp;</span><b>하나의 폴더 안에서 여러 파일을 한꺼번에 export</b>할 수 있도록 도와주는 역할을 한다.<br />이런 방식은<span>&nbsp;</span><b>import 경로를 깔끔하게 줄여주는 효과</b>가 있다.</p>
<p style="color: #000000; text-align: start;" data-end="235" data-start="125" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="235" data-start="125" data-ke-size="size16"><b>2) ❌ 일반적인 import 방식 (Barrel 파일 없이)</b></p>
<div>
<pre id="code_1751350069853" class="typescript" data-ke-language="typescript" data-ke-type="codeblock"><code>import { Button } from '@/components/ui/Button/Button'; import { ButtonIcon } from '@/components/ui/Button/ButtonIcon';</code></pre>
</div>
<p style="color: #000000; text-align: start;" data-end="444" data-start="406" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="444" data-start="406" data-ke-size="size16">파일마다 경로를 직접 작성해야 하니,<span>&nbsp;</span><b>경로가 길고 반복적이다.</b></p>
<p style="color: #000000; text-align: start;" data-end="444" data-start="406" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="444" data-start="406" data-ke-size="size16"><b>3) ✅ Barrel 파일을 사용하는 방식 (index.ts 활용)</b></p>
<pre id="code_1751350096261" class="typescript" data-ke-language="typescript" data-ke-type="codeblock"><code>// components/ui/Button/index.ts export * from './Button'; export * from './ButtonIcon';</code></pre>
<p style="color: #000000; text-align: start;" data-end="639" data-start="593" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="639" data-start="593" data-ke-size="size16">이렇게 export만 정리해두면, 다음과 같이<span>&nbsp;</span><b>경로가 훨씬 짧고 간단</b>해진다:</p>
<p style="color: #000000; text-align: start;" data-end="639" data-start="593" data-ke-size="size16">&nbsp;</p>
<pre id="code_1751350105546" class="typescript" data-ke-language="typescript" data-ke-type="codeblock"><code>import { Button, ButtonIcon } from '@/components/ui/Button';</code></pre>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>4)   구조 예시</b></p>
<pre id="code_1751350122220" class="typescript" data-ke-language="typescript" data-ke-type="codeblock"><code>components/
└── ui/
    └── Button/
        ├── Button.tsx
        ├── ButtonIcon.tsx
        └── index.ts   &larr; 여기서 export 처리</code></pre>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">9. README에 구조 문서화</blockquote>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">프로젝트 최상위에<span>&nbsp;</span>README.md를 작성하여 폴더 구조, 네이밍 규칙, alias 사용법 등을 명시하고 팀원과 공유하자.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<blockquote data-ke-style="style2">마무리 제안</blockquote>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">폴더 구조는 프로젝트의 규모, 팀 구성, 목적에 따라 유동적으로 변화해야 한다. 위에서 소개한 구조는 중대형 규모의 Next.js 실무 환경에서 검증된 방식이지만, 모든 프로젝트에 정답이 될 수는 없다. 중요한 것은 팀이 함께 이해하고 유지할 수 있는 구조를 만드는 것이다.</p>
<p style="color: #000000; text-align: start;" data-ke-size="size16">&nbsp;</p>
<p style="color: #000000; text-align: start;" data-end="275" data-start="207" data-ke-size="size16">처음부터 완벽할 필요는 없다. 명확한 기준과 일관된 구조를 갖추는 것만으로도 협업 효율과 생산성은 놀랄 만큼 향상된다.</p>

**Link**  
https://pangil-log.tistory.com/362