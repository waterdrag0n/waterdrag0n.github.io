---
title: '[CS] Boilerplate'
excerpt: 'Boilerplate의 개념'

categories:
  - CS
tags:
  - [CS]
last_modified_at: 2021-09-23
toc: true  
toc_sticky: true
---

## 보일러플레이트란

개발을 하다 보면 매번 해야 하는, 하지만 반복적이어서 귀찮은 작업들이 (많이) 있다.

처음엔 이게 무엇인지도 모르고 쓰다가, 나중에 알게 되더라도 기계적으로 작성하게 되는 코드가 있는데, 이런 단순노동을 줄여주는 것을 보일러플레이트라고 한다.




보일러플레이트는 원래 변경 없이 재사용할 수 있는 저작품을 뜻하는데, 프로그래밍에서도 같은 의미로 사용되는 것이다.



예를 들어, 새로운 리액트 프로젝트를 시작할 때 create-react-app을 사용할 수 없다고 생각해보자.

기본 폴더구조를 만들고, webpack, babel을 설정하는 등 귀찮고 반복적인 일들이 쌓여있어 무언가를 만들기도 전에 진이 빠질 것이다.

이런 과정을 create-react-app으로 해결하고 개발자는 실제 원하는 기능을 개발할 수 있도록 보일러플레이트가 도와준다.



최근 Node.js 토이 프로젝트를 할 때 express-generator를 사용해 기본적인 설정을 완료하였는데, 이 또한 보일러플레이트를 활용한 것으로 볼 수 있다.

express-generator를 활용하면 기본적인 폴더 구조와 원하는 template engine까지 설정이 된 채로 개발을 시작할 수 있다.



작업 시 자신이 자주 사용하는 정해진 형식의 코드가 있다면 재사용 가능하도록 미리 제작하여 놓는 것도 좋은 방법일 수 있을 것이다.



추가로 대표적인 보일러플레이트의 활용을 몇가지 소개하면서 마치도록 하겠다.



### create-react-app으로 React.js 프로젝트 시작하기

```java
npx create-react-app app-name
cd app-name
npm start
```

### express-generator로 Node.js 프로젝트 시작하기

```java
npm i express-generator
express app-name // 기본 template engine - jade
express app-name --view=pug //tempate engine - pug
cd app-name
npm start
```