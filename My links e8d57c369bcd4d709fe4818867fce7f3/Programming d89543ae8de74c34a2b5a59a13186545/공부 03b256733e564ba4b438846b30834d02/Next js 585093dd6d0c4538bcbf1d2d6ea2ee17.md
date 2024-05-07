# Next.js

Status: In progress
Assign: GenuineLukas
subject: FrontEnd

### SSR

- 클라이언트 대신 서버에서 페이지를 준비하는 원리
- 원래 리액트에서는 클라이언트 사이드 랜더링하기 때문에 서버에 영향을 미치지 않고, 서버에서 클라이언트로 응답해서 보낸 html도 거의 비어있다
    
    → 이 방식은 서버에서 데이터를 가져올 때 지연 시간 발생으로 UX 측면에서 좋지 않을 수 있다.
    
    → 검색 엔진에 검색 시 웹크롤링이 동작할 때 내용을 제대로 가져와 읽을 수 없기에 검색엔진 최적화에 문제가 된다.
    
    → Next.js에서는 서버 사이드 렌더링을 통해 사용자와색 엔진 크롤러에게 바로 렌더링 된 페이지를 전달할 수 있어서 검색엔진 최적화에 좋은 영향을 준다.
    
- nextjs file structure
    
    pages 
    
    - 이 폴더 안에 페이지들을 생성
    - index.tsx가 처음 “/” 페이지로 된다
    - app.tsx는 공통되는 레이아웃을 작성한다. 모든 페이지에공통으로 들어가는 걸 넣어주면 된다. (url)을 통해 특정 페이지에 진입하기 전 통과하는 인터셉터 페이지이다.
    - 만약 about 페이지를 만들려면 pages 폴더 안에 about.tsx를 생성해주면 된다.
    
    public
    
    - 이미지 같은 정적(static) 에셋들을 보관한다.
    
    styles
    
    - 말 그대로 스타일링 처리해주는 폴더
    - 모들(module) css는 컴포넌트 종속적으로 스타일링하기위한 것, 확장자 앞에 module을 붙여줘야함
    
    next.config.js
    
    - Next.js는 웹팩을 기본 번들러로 사용한다
    - 그래서 웹팩에관한 설정들을 이 파일에서 해줄 수 있다
- pre-rendering
    
    nextjs로 개발된 페이지를 보면 javascript를 disable시켜도 화면이 잘 나온다.
    
    반면 react로만 개발된 페이지를 보면 javascript를 disable시키면 you need to enable javascript to run this app. 이라는 메세지가 뜬다
    
    Pre-rendering (using Next.js)
    
    Initial Load:
    
    pre-rendered HTML displayed →JS loads
    
    NO Pre-rendering
    
    Initial Load:
    
    App is not rendered → JS loads
    
    Hydration: React components are initialized and  App becomes interactive
    
    Hydration: React components are initialized and App becomes interactive
    
- data-fetching
    
    nextjs에서 데이터를 가져오는방법은 여러가지가있다. 그래서 앱의 용도에 따라서 다른 방법을 사용해주면 된다. 보통 리액트에서는 데이터를 가져올 때 useEffect안에서 가져오지만 nextjs에서는 다른 방법을 사용해 가져온다
    
    ```jsx
    getStaticProps //Static Generation 으로 빌드할 때 데이터를 불러온다(미리 만들어줌)
    getStaticPaths //Static Generation으로 데이터에 기반하여 pre-render시 특정한 동적 라우팅 구현(pages/post/[id].js)
    getServerSideProps //Server Side Rendering으로 요청이 있을 때 데이터를 불러옴
    ```
    
    getStaticProps
    
    - getStaticProps 함수를 async로 export하면, getStaticProps에서 리턴되는 props를 가지고 페이지를 pre-render 한다. build time에 페이지를 렌더링 한다.
    
    ```jsx
    // posts will be populated at build time by getStaticProps()
    export default function Blog({ posts }) {
      return (
        <ul>
          {posts.map((post) => (
            <li>{post.title}</li>
          ))}
        </ul>
      )
    }
     
    // This function gets called at build time on server-side.
    // It won't be called on client-side, so you can even do
    // direct database queries.
    export async function getStaticProps() {
      // Call an external API endpoint to get posts.
      // You can use any data fetching library
      const res = await fetch('https://.../posts')
      const posts = await res.json()
     
      // By returning { props: { posts } }, the Blog component
      // will receive `posts` as a prop at build time
      return {
        props: {
          posts,
        },
      }
    }
    ```
    
    - 페이지를 렌더링 하는데 필요한 데이터는 사용자의 요청보다 먼저 build 시건에 필요한 데이터를 가져올 때
    - 데이터는 Headless CMS에서 데이터를 가져올 떄
    - 데이터를 공개적으로 캐시할 수 있을 때
    - 페이지는 미리 렌더링되어야 하고(SEO의경우) 매우 빨라야할 때. (getStaticProps는 성능을 위해 CDN에서 캐시할 수있는 HTML 및 JSON 파일을 생성)
    
    getStaticPaths
    
    - 동적 라우팅이 필요할 때 getStaticPaths로 경로 리스트를 정의 하고 HTML에 build시간에 렌더링 된다
    
    *paths*
    
    - 어떠한경로가 pre-render 될지를 결정
    - 아래와 같이 된다
        
        ```jsx
        returns {
        	paths: [
        		{params: {id: '1'}},
        		{params: {id: '2'}}
        	],
        	fallback: ...
        }
        ```
        
    
    *params*
    
    - 페이지 이름이pages/posts/[postId]/[commentId]라면, params는 postId와 commentId이다
    - 만약 메이지 이름이 pages/[…slug]와 같이 모든 경로를 사용한다면, params는 slug가 담긴 배열이어야한다. [’postId’, ‘commentId’]
    
    *fallback*
    
    - false라면 getStaticPaths로 리턴되지않는 것은 모두 404페이지가 된다
    - true라면 getStaticPaths로 리턴되지 않는것은 404가 뜨지 않고, fallback페이지가 뜨게 된다.
        
        ```jsx
        if(router.isFallback) {
        	return <div>Loading...</div>
        }
        
        --------
        
        function Post({post}){
        //Render posts...
        }
        
        export async function getStaticPath() {
        	const res = await fetch('https://...//posts')
        	const posts = await res.json()
        
        	const paths = posts.map((post)=> ({
        		params: {id: post.id},
        	})
        
        	return {paths, fallback: false}
        }
        
        export async function getStaticProps({params}) {
        	const res = await fetch(`https://.../posts/${params.id}`)
        	const post = await res.json()
        
        	return {props: {post}}
        }
        
        export default Post
        ```
        
    
    getServerSideProps
    
    - getServerSideProps함수를 async로 export하면, Next는 각 요청마다 리턴되는 데이터를 getServerSideProps로 pre-render한다.
        
        ```jsx
        function Page({data}) {
        	//Render data...
        }
        
        //This gets called on every request
        export async function getServerSideProps() {
        	//fetch data from external API
        	const res = await fetch(`https://.../data`)
        	const data = await res.json()
        
        	//pass data to the ape via props
        	return {props: {data}}
        }
        
        ```
        
        - 요청할 때 데이터를 가져와야하는 페이지를 미리 렌더해야 할 때 사용한다. 서버가 모든 요청에 대한 결과를 계산하고, 추가 구성없이 CDN에 의해 결과를 캐시할 수 없기 떄문에 첫번째 바이트까지의 시간은 getStaticProps보다 느리다.
- file-based navigation
    
    리액트에서는 route를 위해서 react-router라는 라이브러리를 사용하지만 Next.js에서는 페이지 개념을 기반으로 구축된 파일 시스템 기반 라우터가 있다. 파이일이 페이지 디렉토리에 추가되면 자동으로 경로로 사용할 수 있다. 페이지 디렉토리 내의 파일은 가장 일반적인 패턴을 정의하는 데 사용할 수 있다.
    
    pages/index.js → /
    
    pages/blog/index.js → /blog
    
    pages/blog/first-post.js → /blog/first-post
    
    pages/dashboard/settings/username.js→ /dashboard/settings/username
    
    pages/blog/[slug].js→/blog/:slug(/blog/hello-world)
    
    pages/[username]/settings.js→/:username/settings(/foo/settings)
    
    pages/posts/[…all].js→/post/(/post/2020/id/title)
    

### Server Actions

with Server Actions, you don’t need to manually create API endpoints. Instead, you define asynchronous server functions that can be called directly from your components.

Server Actions can be defined in Server Components or called from Client Components. Defining the action in a Server Component allows the form to function without JavaScript, providing progressive enhancement.

`npx create-next-app@latest ./`

since it is still beta,

in next.cofig.js,

set 

```cpp
const nextConfig = {
	experimental: {
			serverActions: true
	}
}
```

Server Actions can be defined in two places:

- inside the component that uses it (Server Components only).
    
    ```cpp
    export default function ServerComponent() {
      async function myAction() {
        "use server";
      }
      return (
          <div></div>
      );
    }
    ```
    
- In a separate file (Client and ServerComponents), for reusability. You can define multiple Server Actions in a single file.
    
    ```cpp
    import {myAction} from "@/lib/actions";
    import React from 'react';
    
    const ClientComponents = () => {
        return (
            <form action={myAction}>
                <button type={'submit'}>Add to Cart</button>
            </form>
        )
    }
    
    //actions.ts
    'use server'
    
    export async function myAction() {
    
    }
    ```
    

Server Actions can be called:

- using `action`: React’s `action` prop allows invoking a Server Action on a `<form>` element
- Using `formAction`: React’s `formAction` prop allows handling `<button>`, `<input type=’submit’>`, and `<input type=’image’>` elements in a `<form>`
- custom invocation with `startTransition`: Invoke Server Actions without using `action` or `formAction` by using `startTransition`. This method disables [Progressive enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement)

** `[revalidatePath()](https://nextjs.org/docs/app/api-reference/functions/revalidatePath)` : allows you to purge cached data on-demand for a specific path.

** useOptimistic : use this to optimistically update the UI before the Server Action finishes rather than waiting for the response

[Todo List](Next%20js%20585093dd6d0c4538bcbf1d2d6ea2ee17/Todo%20List%208460ae53668e487683b7f107039c702f.md)

[Pages router quiz app](Next%20js%20585093dd6d0c4538bcbf1d2d6ea2ee17/Pages%20router%20quiz%20app%20cbe42850eef74e2cbf7075b082b15345.md)

[next13 weather app](Next%20js%20585093dd6d0c4538bcbf1d2d6ea2ee17/next13%20weather%20app%20b415726354564ae2a34c76fcf97bf686.md)