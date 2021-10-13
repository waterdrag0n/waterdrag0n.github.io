---
title: '[배포] NCloud 서버로 배포 준비하기'
excerpt: '배포 직전까지의 기본 설정'

categories:
  - 배포
tags:
  - [배포, Ncloud, Ubuntu]
last_modified_at: 2021-10-13
toc: true  
toc_sticky: true
---

## 회원가입/로그인

- ncloud 회원가입/로그인 후, 우측 상단의 [콘솔] 클릭
    - 2021-10-13 기준, 회원가입 후 결제수단을 등록하면 10만원 크레딧 제공

![Untitled](https://user-images.githubusercontent.com/70019911/137104769-0572972c-e540-4deb-9289-2523ee78f982.png)

## ACG 생성

- [Products & Services] → [Server] 클릭

![Untitled 1](https://user-images.githubusercontent.com/70019911/137104735-aff4600f-9498-4550-aa88-b655a2b9a8dc.png)

- ACG 클릭

![Untitled 2](https://user-images.githubusercontent.com/70019911/137104738-8d401a34-2bc7-4446-8dfa-e43224d45469.png)

- [ACG 생성] 혹은 [ncloude-default-acg] 클릭 후 [ACG 설정] 클릭

![Untitled 3](https://user-images.githubusercontent.com/70019911/137104739-6a48e6e5-dea7-4f6c-8c6e-c2ab0588af46.png)

- 필요한 포트를 추가
    - ssh 접속을 위해 [TCP, 0.0.0.0/0, 22] 추가
    - React 프로젝트를 배포할 거라 [TCP, 0.0.0.0/0, 3000] 추가

![Untitled 4](https://user-images.githubusercontent.com/70019911/137104741-46eaae91-1576-4620-86fc-04a5cea031b0.png)

- [적용] 클릭하기! 적용 눌러야 저장됨!
![Untitled 5](https://user-images.githubusercontent.com/70019911/137104742-f1b50b60-dfb0-4953-b751-9746a20e4e38.png)

## 서버 생성

- 아래의 [서버 생성] 클릭

![Untitled 6](https://user-images.githubusercontent.com/70019911/137104745-a49f3bb7-c589-40b0-bf01-60107c37df23.png)

- [ubuntu 18.04] 선택

![Untitled 7](https://user-images.githubusercontent.com/70019911/137104746-ef4c5862-93bc-48da-97f8-e03a2409e2be.png)

- 원하는 크기의 서버 타입 선택
- 반납 보호를 [설정]하면 실수로 서버를 삭제하는 불상사를 방지할 수 있다.

![Untitled 8](https://user-images.githubusercontent.com/70019911/137104748-bc905a35-49bb-461d-bc2b-df1de0d19495.png)

- 원하는 이름으로 인증키를 생성하고 잘 보관. 경로를 잘 기억하기!

![Untitled 9](https://user-images.githubusercontent.com/70019911/137104749-d246b343-5221-4b45-8ae5-470023a3d810.png)

- 아까 생성한 ACG를 연결

![Untitled 10](https://user-images.githubusercontent.com/70019911/137104750-37209738-eb4b-400e-b692-a1728428f97d.png)

- 최종 확인 후 [서버 생성] 클릭!

![Untitled 11](https://user-images.githubusercontent.com/70019911/137104751-9b25c750-3e5d-4238-8aec-f31db8712ecc.png)

## 서버 설정

### 관리자 비밀번호 확인

- 서버 오른쪽 클릭 - [관리자 비밀번호 확인]

![Untitled 12](https://user-images.githubusercontent.com/70019911/137104752-ab78ac88-43fd-455e-a5ad-f420d0d1b7df.png)

- 인증키 드래그 후 [비밀번호 확인] 클릭 - 비밀번호 잘 기억하기! (곧 바꿀 예정)

![Untitled 13](https://user-images.githubusercontent.com/70019911/137104754-31437cb3-4233-4c85-a13d-73f1a3ba3b3c.png)

### 공인 IP 신청

- Server - [Public IP] 클릭

![Untitled 14](https://user-images.githubusercontent.com/70019911/137104755-77d5db98-6400-43b7-b71c-a479f71e7d28.png)

- [공인 IP 신청] - 적용서버 선택에 아까 만든 서버 선택 - [다음] 클릭

![Untitled 15](https://user-images.githubusercontent.com/70019911/137104756-735e4780-2679-4119-8b73-d6dc648d436d.png)

- [생성] 클릭

![Untitled 16](https://user-images.githubusercontent.com/70019911/137104757-5c1c12c9-b36b-482a-9123-1c827459ab4b.png)

### 포트 포워딩 설정

- 서버 - 만든 서버 클릭 후 [포트 포워딩 설정] 클릭

![Untitled 17](https://user-images.githubusercontent.com/70019911/137104760-d09fc67a-2754-4dc9-a212-c95bd5fb49df.png)

- 외부 포트 열어주기 (2020 포트 개방)

![Untitled 18](https://user-images.githubusercontent.com/70019911/137104763-e48ff3d3-e780-4cdb-8508-faf3f0edd514.png)

## 접속

- pem키가 있는 디렉토리에서 콘솔을 켜서 접속하기

```bash
ssh root@{서버 접속용 공인 IP} -p {포트포워딩 포트}
```

![Untitled 19](https://user-images.githubusercontent.com/70019911/137104764-2c45ea97-e1e6-48dd-9c88-e624992abd00.png)

## 패키지 설치

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install curl
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
apt-get install nodejs

// node, npm 잘 설치되었는지 버전 확인
node -v
npm -v
```

![Untitled 20](https://user-images.githubusercontent.com/70019911/137104765-452a8782-57c7-439d-80db-8ce71a616a7b.png)

최소한으로 필요한 패키지들을 설치하며 기본 설정을 마무리하게 되었다.

추가로 git 등을 설치할 수 있다.

- 참고

[https://kjwsx23.tistory.com/353](https://kjwsx23.tistory.com/353)

[https://velog.io/@youn_22/React-Express-2.-배포-NCP](https://velog.io/@youn_22/React-Express-2.-%EB%B0%B0%ED%8F%AC-NCP)