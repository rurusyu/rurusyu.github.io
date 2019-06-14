---
title: "[Gatsby.js] 개츠비로 블로그 만들기"
date: "2019-06-14T16:02:11.121Z"
template: "post"
draft: false
slug: "/posts/Create-blogging-with-Gatsby/"
category: "React"
tags:
  - "gatsby.js"
  - "Create blogging with Gatsby.js"
description: "리액트 라이브러리의 한 종류 인 gatsby.js.로 블로그 만들기"
---

### 리액트 라이브러리는 프론트 엔드 3대장 중 하나이며,  

#### CRA(create-react-app), Gatsby.js, Next.js 로 실행할 수 있다.  

이번에는 그 중에서 Gatsby를 이용해서 블로그를 만들어 보려고 한다.  

# Gatsby JS 란 무엇인가  

Gatsby JS 는 정적 HTML 생성기 이다.

일반적인 단순한 페이지는 하나의 HTML 로 만들어 질 수 있다.

사이트가 커지고 페이지 별로 HTML 이 생성되어야 한다면, 페이지에 접근할때 마다 DB 에서 정보를 받아와서 HTML 을 만들어 내는 SSR 방식,  

API 로 해당 페이지 정보를 받아와서 HTML 페이지를 만들어내는 CSR 방식, 그리고, 그때마다 페이지를 만들어 내는것이 아닌 페이지를 원하는  

시점 빌드 시점마다 만들어내는 방식이 있을 수 있다.  

Gatsby JS 는 가공할 정보를 GraphQL 에서 가져와서 빌드 시점에 정적 페이지를 만들어내는 방식을 취하고 있다.  

이미 배포할때 각 페이지 정보들이 모두 배포시점에 만들어져지므로, 따로 앱서버가 필요하지 않다는 장점이 있다.  

#### Flow는 아래와 같이 진행된다.  
```
1. yarn을 이용해서 설치
2. gatsby  설치
3. 원하는 폴더로 이동후 : gatsby new 하위폴더명 블로그테플릿주소
3. config.js에서  주소를 실제 올릴 주소로 변경. url: 'https://XXXX.github.io/',
4. package.json deploy : 
   1) ~에서 : "yarn run clean && gatsby build --prefix-paths && gh-pages -d public", 
   2) ~으로 : "yarn run clean && gatsby build  && gh-pages -d public -b master",

5. git add remote 함.
6. 수정 후 git add . / git commit  / git push 브랜치명 / checkout 브랜치명 / 수정 후 / yarn deploy
```
  
```
1. npm install -g yarn
2. 블로그 폴더 만들고 이동
3. gatsby new blogithub https://github.com/alxshelepenok/gatsby-starter-lumen   //나는 루멘이용
4. 설치완료 후 vscode를 이용해서 package.json 파일에서 deploy 수정
5. 깃에 원격 저장소 추가함. git add remote https://github.com/rurusyu/rurusyu.github.io.git 
6. 수정 깃에 저장. 
7. 다른 사용자도 공유하기 위해서 배포해야함. yarn deploy한다.

```


