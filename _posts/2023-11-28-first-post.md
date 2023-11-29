---
title: 첫 포스팅
author: haley
date: 2023-11-28 15:00:00 +0800
categories: [Logging, Thinking]
tags: [blah]
pin: true # 중요한 포스팅은 상단 고정 가능
---

## 본격 블로그 시작
매번 블로그해야지 다짐만 했던 나날들.. 공부한 내용들을 정리하면서 다양한 형태의 블로그를 만들어 보았었다.  
그 중 <kbd>notion</kbd>의 <kbd>database</kbd>를 활용하여 <kbd>vercel</kbd>을 통해 한 번만 deploy하면 이후 notion을 통해 편하게 블로그 관리를 할 수 있었던 [**morethan-log**](https://github.com/morethanmin/morethan-log)를 활용해왔다.  
장점은 markdown 문법을 신경 쓸 필요가 거의 없으므로 아이디어를 수시로 추가해서 private or public하게 관리할 수 있다는 점이였다.  
그런데 가끔 씩 sync가 안맞는 문제가 생겨서 은근히 불편하기도 하고, notion에 문제가 생기면 접근 불가능하다는 치명적 단점이 있었다.  
그리고 학부 졸업 이후 개발자스러운 코딩은 손에서 놓았기 때문에 front-end 개발은 사실상 불가능 해 customizing은 꿈도 못꿨다.  
그 언젠가 정말 할게 없다면 front-end 영역도 도전해보겠지만, 거의 해당사항 없는 일이라 최대한 원하는 디자인과 기능을 가진 <kbd>Jeklly Themes</kbd> 를 한참을 찾았다. 그러다가 Chirpy 테마를 발견하게 되었다.  
많은 방법을 시도했으나.. 결국엔 돌고 돌아 다시 github.io를 활용한 블로그 개설로 최종 방향을 정했다. 

## Chirpy theme 적용하기
여러 사이트([**블로그1**](https://www.irgroup.org/posts/jekyll-chirpy/),
[**블로그2**](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-3/))를 참조하면서 수십 번을 지웠다가 다시했다가 반복을 해보았지만..  
fork, clone 그 무엇을 해도 <kbd>gh-pages</kbd> branch는 자동 생성 안됨ㅠㅠ  
나 말고도 같은 오류로 안되는 사람들이 많은 듯 했다.  
[**블로그3**](https://ree31206.tistory.com/entry/github-pages-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-%ED%85%8C%EB%A7%88-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0Chirpy) 여기서 해답을 찾아서 드디어 deploy할 수 있었다(감격ㅠㅠ)  
이대로 따라하면 <kbd>jekyll.yml</kbd>이 생성되는데, 이게 결국 deploy를 자동으로 해주는 yml이였기에, 기존에 존재하던 <kbd>pages-deploy.yml</kbd> 은 삭제하면 된다.


## 이미지 삽입 테스트
Git의 <kbd>Issues</kbd>에서 이미지를 복사하고 붙여넣고 기다리면 자동으로 URL생성됨! 그대로 주소만 활용하면 된다.  
![image](https://github.com/hyay/hyay.github.io/assets/28091783/ce2ffd6f-45c1-4928-aed3-76b142a3c799)  
그런데 왜인지 모르겠는데 자꾸 이미지에 특수효과(?)가 생긴다..🧐 나중에 해결해 보자ㅠ


## Google Search Console, Google Analytics, Google Adsense 추가하기 
이것도 여유를 갖고 제대로 해보기.  
일단 뭔가 하기는 했는데 버그가 있는 것 같다. 따라하는 포스팅들이 몇년 전 버전이라 UI가 조금 씩 달라서 다시 해보아야 겠다.


## Utterances 추가하기
블로그 댓글 기능 추가하기.  
깔끔하게 잘 추가 된다! 😌


## Customizing
블로그 로고랑 디자인 등등 바꾸는 작업도 해야한다. 시간을 들여서 천천히 공사 해보자! 👷🏻‍♀️


## 기타
<kbd>date: 2023-11-28 15:00:00 +0800</kbd> 포스팅 본래 시간보다 먼 미래(ex. 1일 뒤)는 blog에 게시되지 않는 것 같다.  
localhost로 확인할 때에도 보이지 않는다. 미리 포스트를 작성하고 예약 업로드처럼 활용해도 좋을 듯 하다.

## 향후 계획
얼마나 열심히할지 모르겠지만, 기왕 블로그 하기로 마음먹은 것 공부했던 내용들이라도 차근차근 올려보려고 한다.  
일단 올해까지 기존에 정리해둔 내용들을 업로드하고, <kbd>obsidian</kbd>과 연동해서 생산성을 올리는데 집중하려고 한다.  
목표했던 <kbd>ADP</kbd>를 드디어 땄기 때문에 이제 한결 가벼운 마음으로 자기계발에 집중해야겠다! 👩🏻‍💻
