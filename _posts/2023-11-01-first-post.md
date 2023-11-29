---
title: 첫 포스팅
author: haley
date: 2023-11-01 00:34:00 +0800
categories: [Blogging, Tutorial]
tags: [blah]
---

## 본격 블로그 시작
매번 블로그해야지 다짐만 했던 나날들.. 공부한 내용들을 정리하면서 다양한 형태의 블로그를 만들어 보았었다.  
그 중 <kbd>notion</kbd>의 <kbd>database</kbd>를 활용하여 <kbd>vercel</kbd>을 통해 한 번만 deploy하면 이후 notion을 통해 편하게 블로그 관리를 할 수 있었던 [**morethan-log**](https://github.com/morethanmin/morethan-log)를 활용해왔다.  
장점은 markdown 문법을 신경 쓸 필요가 거의 없으므로 아이디어를 수시로 추가해서 private or public하게 관리할 수 있다는 점이였다.  
그런데 가끔 씩 sync가 안맞는 문제가 생겨서 은근히 불편하기도 하고, notion에 문제가 생기면 접근 불가능하다는 치명적 단점이 있었다.  
그리고 학부 졸업 이후 개발자스러운 코딩은 손에서 놓았기 때문에 front-end 개발은 사실 상 불가능해 customizing은 꿈도 못꿨다.  
그 언젠가 정말 할게 없다면 front-end 영역도 도전해보겠지만, 거의 해당사항 없는 일이라 원하는 디자인과 기능을 가진 <kbd>Jeklly Themes</kbd> 를 한참을 찾았다. 그러다가 결국 Chirpy 테마를 발견하게 되었다.


## Chirpy theme 적용하기
여러 사이트([**블로그1**](https://www.irgroup.org/posts/jekyll-chirpy/),
[**블로그2**](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-3/))를 참조하면서 수십 번을 지웠다가 다시했다가 반복을 해보았지만..  
fork, clone 그 무엇을 해도 <kbd>gh-pages</kbd> branch는 자동 생성 안됨ㅠㅠ  
나 말고도 같은 오류로 안되는 사람들이 많은 듯 했다.  
[**블로그3**](https://ree31206.tistory.com/entry/github-pages-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-%ED%85%8C%EB%A7%88-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0Chirpy) 여기서 해답을 찾아서 드디어 deploy할 수 있었다(감격ㅠㅠ)  
이대로 따라하면 <kbd>jekyll.yml</kbd>이 생성되는데, 이게 결국 deploy를 자동으로 해주는 yml이였기에, 기존에 존재하던 <kbd>pages-deploy.yml</kbd> 은 삭제하면 된다.

![img1](/assets/img/posts/2023-11-01-first-post-img1.png)
<!-- {: w="700" h="400" } -->

## 향후 계획
얼마나 열심히할지 모르겠지만, 기왕 블로그 하기로 마음먹은 것 공부했던 내용들이라도 차근차근 올려보려고 한다.  
일단 올해까지 기존에 정리해둔 내용들을 업로드하고, <kbd>obsidian</kbd>과 연동해서 생산성을 올리는데 집중하려고 한다.
목표했던 ADP를 드디어 땄기 때문에 이제 한결 가벼운 마음으로 자기계발에 집중해야겠다!
