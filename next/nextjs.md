# Nextjs

### App Router

- App Router built on React Server Components
  -> supports shared layouts, nested routing, loading states, error handling

  -> inside `app` components are React Server Components.(can use Client Components)

`pages` -> after v13, `app`

- file-system based router

**_File convention_**

| filename  | meaning                 |
| --------- | ----------------------- |
| layout    |
| page      |
| loading   |
| not-found |
| error     | React Suspense boundary |
| route     |
| template  |
| default   |

**absolute import alias** <- is useful
https://www.typescriptlang.org/tsconfig#paths

### optimizing Fonts and Images

**CLS - Cumulative Layout Shift**

- core web vitals에 영향을 준다.
- 페이지 수명동안 발생하는 모든 예상치 못한 레이아웃 변경에 관한 가증 큰 버스트를 측정한 것.
- 좋은 CLS 점수 0.1이하 가장 좋고 0.25이상부터는 큰일난다.

  https://web.dev/articles/cls?hl=ko
  is a metric used by Google to evalutate ther performace and ux
  with fonts, layout shift happens when the browser initially renders text in a fallback

**`next/font`** 모듈을 사용하면 성능향상에 도움을 준다.

- 빌드타임에 폰트파일을 다운로드 -> on static assets. -> No 추가적 네트워크 요청

#### optimizing images `<Image>`

- 이미지 로딩중 layout shifting 방지?
- 이미지 리사이징 -> 작은 뷰포트에 큰 사진 방지
- 레이지 로딩
- WebP, AVIF 등 지원?

width와 height를 지정함으로써 aspect ration identical

### creating Layouts and Pages

- `layout.tsx`
  -> navigation 중에 layout은 리렌더링이 되지 않는다. -> partial rendering

- `root layout.tsx`
  -> 모든 페이지에 공유되는 ui 활용하자..

### 5. Navigating Btw Pages

- why optimize navigation
  -> just use <a> -> refresh full pages

- <Link> 클릭시 백그라운드 페이지 다운로드 시작
- Automatic code-splitting and prefetching
  [How Routing and Navigation Works](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#how-routing-and-navigation-works)

- `usePathname()` can get url

### 6. Set up DB (using PostgreSQL)

- 셋업에 관한 내용

### 7. Fetching Data

- ORMS, SQL, API
- feel Server Component

API Layers

API endpoints using Route Handlers

- React Server Components -> no need API layer

- React Server Compoents benefits
- - support promises `async/await` without using `useEffect`
- - executes on server so that fetching and some expensive logic.
- - no need additional API layer

when data requests there would be possible

### 8. static and Dynamic Rendering

- **static rendering** (on server, build time, when deploy or during revalidation)

- 데이터가 없거나, 자주 변하지 않는 데이터, 사용자 전체에 보여줄만한 것

- \*\* dynamic rendering (on server, each user at request time)

- 실시간으로 바뀌는 데이터, 개인 데이터, 시간정보가 중요한 데이터(쿠키)

`unable_noStore` : 서버 컴포넌트와 패칭 함수에서 사용 가능하며 정적 렌더링을 사용하지 않을 수 있음

### 9. Streaming

-> slowing data fetches -> imporove performacnces

#### what is streaming

- 데이터를 "chunk"로 쪼개서 준비되는 대로 보내기

-page level => `loading.tsx`

- specific components `<Suspense>`

**`Group Routes`**

- convention
- - (filename)
- usage cases
- - 하나의 폴더 아래 여러 레이아웃을 이용할 수 있다 => 페이지 단위로 렌더링이 아니라 거기서 더 나아가서 컴포넌트로 쪼갤때 유용할듯.

`<Suspense>` API는 정말 깔끔하네.

- page | compoent depends on app, if data are heavy, -> component?

### 10. Partial Rendering(experimental)

### 11. Adding Search and Pagination

`searchParams`,

`useSearchParams`, `useRouter`, `usePathname` - `next/navigation`

##### URLParams을 사용하는 이유

1. Bookmarkable and Shareable URLs
2. Server-Side Rendering and Initial Load
3. Analytics and Tracking

##### 제어, 비제어 컴포넌트

- 제어되는 컴포넌트(Controlled Component): React가 해당 컴포넌트 상태를 완전히 제어, 보통 value 속성을 사용하여 상태를 설정하고, onChange 이벤트 핸들러를 통해 사용자 입력을 처리합니다.

- 비제어 컴포넌트(Uncontrolled Component): React 관여 X, 일반적으로 defaultValue 속성 사용, 입력이 변경될 때마다 직접 DOM 요소 이용
- - -> 리액트 재조정에 패스 -> 장단점은?

### 12. Server Action

- React Server Component, `'use server'`(실험), form action

##### Reading dynamic routes

`/app/dashboard/invoices/[id]/edit/page.tsx`

```tsx
export default function Page({ params }: { params: { id: string } });
```

##### JS bind method

```js
const updateInvoiceWithId = updateInvoice.bind(null, invoice.id);
```

JS bind. This will ensure that any values passed to the Server Action are encoded.

- `revalidatePath` - to clear client cache and make a new request to server
- `redirect`

### 13. Handling Error

with `error.tsx` & `not-found.tsx`

#### error.js

- 'use client'
- catch all errors
- get props (error, reset)
- create ReactErrorBoundary auto

#### notFound() -> not-found.tsx

### 15. Adding Authentication
