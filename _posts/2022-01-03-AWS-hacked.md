---
title: '[AWS] 해킹으로 인한 비용폭탄 해결기'
excerpt: '네 key를 털렸습니다.'

categories:
  - AWS
tags:
  - [AWS, Cloud]
last_modified_at: 2022-01-03
toc: true  
toc_sticky: true
---

> 미해결 상태입니다. 진전 있을 시 업데이트 예정

## 사건 개요
와빅 학기말 프로젝트로 ['데이터 파이프라인 구축 프로젝트'](https://github.com/kpsy20/GameBoard)를 진행했다.  
나도 많이 해본건 아니지만 6명 중 2명의 선배 기수 중 하나였고, 그나마 많이 접해본지라 카프카 브로커 운영, S3 버킷 운영을 맡아 하게 되었는데...  
카프카 브로커는 환경설정만 잘 하고 켜놓으면 되는 거라서 문제가 없었지만, 팀원들이 외부에서 S3 버킷에 접근해서 데이터를 가져가려면 내 access key와 secret key를 알아야 했다.  
IAM을 통해 발급받은 키를 카톡방에 뿌리면서 키를 외부에 업로드하면 중국 해커들한테 털려서 많은 요금이 나오게 되니 절대 올리지 말라고 경고를 했지만..  
팀원 중 한 명이 실수로 git으로 키가 들어있는 파일을 커밋했고, 처음에는 같은 장소에 있었기 때문에 바로 키를 파기하고 새로운 키를 파서 전달했는데 정작 프로젝트가 끝난 뒤 팀원들이 정리 겸 커밋한 내용에 대해서는 신경쓰지 못했다.  

![image](https://user-images.githubusercontent.com/70019911/147637698-01f11afb-15fd-494d-b64f-c87662f6dc38.png)
그리고 이 메일을 받게 된다.  

별 생각 없이 학회에서 지원금이 나와서 정산을 할 겸 billing management 페이지에 들어갔더니 어이없는 bill을 발견하게 되었다.  
![image](https://user-images.githubusercontent.com/70019911/147637833-53d85212-5f2a-4d21-a190-89e25227ad29.png)
> ??? (원래 1만원 예상함)

특히, Elastic Compute Cloud 부분을 보면, 우리는 모두 Asia region에서 인스턴스를 만들어서 프로젝트를 진행했는데 미국에서 많은 인스턴스가 만들어지고 요금이 부과된 것을 볼 수 있다.
<img width="775" alt="화면 캡처 2021-12-29 161525" src="https://user-images.githubusercontent.com/70019911/147638625-f8764954-af14-43fb-b8f9-daa87cd8c180.png">
다른 분들 블로그에서 본 것처럼 천문학적인 금액은 아니었지만 나에게는 큰 돈이라.. AWS에 도움을 요청했다.

## AWS support
새로운 case를 만들어 요청을 했는데, 기존에 나에게 메일로 보낸 케이스와 연관된 케이스이므로 이를 우선 합쳐주었다.  
![image](https://user-images.githubusercontent.com/70019911/147638413-62dfbd1d-6878-41cf-8b2d-e8af981ee14d.png)
그리고 내 징징대는 메일을 잘 받아주어서
![image](https://user-images.githubusercontent.com/70019911/147638366-b269ebfc-e606-4f1d-9578-f0df3a712673.png)
어떻게 진행해야 할지 친절하게 안내를 해주었다.
![image](https://user-images.githubusercontent.com/70019911/147638575-d9f04d20-eea3-44ae-84e6-22215ccb87ac.png)

### 2021-12-29
24시간 동안 문제가 없으면 billing team과 검토를 시작한다는 것 같다.
![image](https://user-images.githubusercontent.com/70019911/147639276-8722aa02-52b9-4e3e-8503-1cc4c9ef3f80.png)
### 2022-01-03
support 측에서 bill을 리뷰하기 전에 다시 이런 일이 생기지 않도록 예방책을 세우라고 요구했고,
이에 따라 root 계정에서 MFA 설정을 했고, EC2 인스턴스에 CloudWatch 알람을 걸어서 사용량이 일정 기준을 넘으면 자동으로 인스턴스가 중지되고 메일이 오도록 설정했다.
이제 돈 좀 돌려줬으면 좋겠다... 방금 출금됐다...


to be continued