## Next Blog getting started
1. Vercel (https://vercel.com/templates/starter)
2. 마음에 드는 tmeplate 선택 후 cmd를 이용해 설치
3. 
4. 


## Deploying
1. Static Exports 문서 활용(https://nextjs.org/docs/pages/building-your-application/deploying/static-exports)
2. next.config.js(해당 파일은 Next.js 프레임워크에서 사용되며, 애플리케이션의 환경 설정을 구성하는 역할을 합니다. )
```
/**
 * @type {import('next').NextConfig}
 */

const isProd = process.env.NODE_ENV === 'production'
const nextConfig = {
    basePath: isProd ? '/next-blog-test' : '',
    output: 'export',
    distDir: 'dist',
    images: {
        unoptimized: true,
    }
}

module.exports = nextConfig
```
`isProd`라는 변수는 process.env.NODE_ENV 환경 변수가 'production'인지 확인하여 불리언 값을 할당합니다. 이는 애플리케이션이 개발 환경인지 아니면 프로덕션 환경인지를 구분하기 위한 용도로 사용됩니다.
`nextConfig`라는 객체는 Next.js 애플리케이션의 구성 옵션을 정의합니다.
`basePath`: isProd 값이 true인 경우 '/next-blog-test'로 설정되고, 그렇지 않은 경우 빈 문자열('')로 설정됩니다. basePath는 애플리케이션의 라우팅 경로에 접두사를 추가하는 옵션입니다.
`output`: 'export'로 설정되어 있습니다. 이는 Next.js의 정적 사이트 생성(Static Site Generation) 기능을 사용하여 정적 파일을 내보내는 옵션입니다.
`distDir`: 'dist'로 설정되어 있습니다. 이는 Next.js 애플리케이션의 빌드 결과물이 생성될 디렉토리를 지정하는 옵션입니다.
`images`: 다양한 이미지 처리 옵션을 설정하는 객체입니다. 현재는 unoptimized: true로 설정되어 있어, 이미지 최적화를 비활성화합니다.
`module.exports = nextConfig` 구문은 nextConfig 객체를 외부에서 사용할 수 있도록 모듈로 내보내는 역할을 합니다.
3. `npm run build` -> 명령 이후에 빌드 결과물인 dist폴더 생성
4. git의 저장소를 만들어 설정
5. git 저장소의 settings - pages에서 Build and deployment (https://docs.github.com/ko/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)
6. next.js.yml파일을 만들어 저장하고 코드를 고쳐 다시 rebuild(https://docs.github.com/ko/actions)
** 저장소 GitHub Actions으로 yml파일을 만들고 편집기로 `git pull`로 저장소 데이터를 가져와 파일 변경
- `path: ./out` -> `path: ./dist` 로 변경

- run: ${{ steps.detect-package-manager.outputs.runner }} next build
  name: Static HTML export with Next.js -> 삭제 (왜???)

** YAML(YAML Ain't Markup Language)은 인간이 쉽게 읽고 작성할 수 있는 데이터 직렬화 형식입니다. 주로 설정 파일이나 데이터 구조를 표현하는 용도로 사용됩니다. GitHub에서는 YAML 파일을 사용하여 워크플로우(workflow)를 정의하고 빌드 및 배포 과정을 자동화할 수 있습니다.

GitHub의 워크플로우는 ".github/workflows" 디렉토리에 YAML 파일을 작성하여 정의됩니다. 이 파일은 특정 이벤트(예: 코드 푸시, Pull Request 등)가 발생했을 때 실행되는 작업들을 선언하는 역할을 합니다. 이러한 작업들은 순차적이거나 병렬적으로 실행될 수 있으며, 각 작업은 특정한 스크립트 또는 명령어를 실행하는 것일 수 있습니다.

YAML 파일은 일반적으로 다음과 같은 구조를 가지게 됩니다:
```
name: Workflow 이름

on:
  이벤트: [이벤트 조건]

jobs:
  작업_이름:
    runs-on: 실행_환경
    steps:
      - name: 단계_이름
        uses: 액션_사용
        with:
          매개변수: 값
      - name: 단계_이름
        run: 실행할_스크립트_또는_명령어
```

7. 이렇게 하고 git 저장소에 올리고 `npx serve ./dist` 명령으로 서버 실행


## Image
상황: config.js 설정을 하고 build를 한 후 yml파일을 고쳐 서버를 실행했지만 이미지가 안나오는 오류 존재

1. `_posts` 폴더 설정 필요

"_posts" 폴더의 역할은 다음과 같습니다:

글 게시물 저장: "_posts" 폴더는 블로그 포스트나 글 게시물에 해당하는 파일들을 저장하는 곳입니다. 각각의 파일은 하나의 글 게시물을 나타내며, 파일 이름은 일반적으로 날짜와 제목을 포함합니다. 예를 들어, "2022-01-17-my-blog-post.md"와 같은 형식을 가질 수 있습니다.
마크다운 또는 텍스트 파일 형식: "_posts" 폴더에 저장되는 글 게시물은 주로 마크다운(Markdown) 또는 텍스트 파일 형식으로 작성됩니다. 이러한 파일 형식은 글 게시물의 내용과 형식을 구조화하고 서식을 적용하는 데 사용됩니다. 마크다운을 사용하면 글 게시물을 쉽게 작성하고 포맷팅할 수 있습니다.
자동 변환과 렌더링: 정적 사이트 생성기는 "_posts" 폴더에 저장된 글 게시물을 자동으로 변환하고 렌더링하여 웹 사이트에 표시합니다. 이를 통해 블로그 페이지나 글 목록을 생성하고, 글 게시물을 템플릿에 맞게 출력할 수 있습니다.
정렬과 카테고리화: 글 게시물은 파일 이름의 날짜 정보를 기준으로 정렬되고, 필요에 따라 카테고리화되어 웹 사이트의 블로그 페이지에 표시될 수 있습니다. 이를 통해 사용자는 원하는 카테고리의 글 게시물을 찾거나 정렬된 순서로 확인할 수 있습니다.

```
title: "Preview Mode for Static Generation"
excerpt: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Praesent elementum facilisis leo vel fringilla est ullamcorper eget. At imperdiet dui accumsan sit amet nulla facilities morbi tempus."
coverImage: "${basePath}/assets/blog/preview/cover.jpg"
date: "2020-03-16T05:35:07.322Z"
author:
  name: Joe Haddad
  picture: "${basePath}/assets/blog/authors/joe.jpeg"
ogImage:
  url: "${basePath}/assets/blog/preview/cover.jpg"
```

2. `_posts`의 모든 파일에서 Image 파일의 path를 변경



## write
Next.js로 만든 블로그에 글을 작성하는 방법은 다음과 같습니다:

1. "_posts" 폴더 생성: 우선, Next.js 프로젝트의 루트 디렉토리에 "_posts" 폴더를 생성합니다. 이 폴더는 글 게시물을 저장할 공간으로 사용됩니다.
2. 글 게시물 파일 생성: "_posts" 폴더에 새로운 글 게시물 파일을 생성합니다. 일반적으로 파일 이름은 날짜와 제목을 포함한 형식을 따르는 것이 좋습니다. 예를 들어, "2022-01-17-my-blog-post.md"와 같은 형식을 사용할 수 있습니다.
3. 글 게시물 작성: 생성한 글 게시물 파일을 열고 마크다운 또는 텍스트 형식으로 글 내용을 작성합니다. 마크다운을 사용하면 글을 구조화하고 서식을 적용할 수 있습니다. 글 게시물에는 제목, 내용, 작성자 등의 정보를 포함할 수 있습니다.
4. 블로그에 게시: 작성한 글 게시물 파일을 저장한 후, Next.js 프로젝트를 빌드하거나 개발 서버를 실행하여 변경 사항을 적용합니다. 이후 블로그 페이지에서 작성한 글이 표시됩니다.
5. 추가 기능 구현 (선택 사항): 필요에 따라 블로그에 추가 기능을 구현할 수 있습니다. 예를 들어, 글 목록 페이지, 카테고리 분류, 태그 기능, 댓글 기능 등을 추가할 수 있습니다. 이는 Next.js 프로젝트의 설정과 개발자의 요구에 따라 다를 수 있습니다.




