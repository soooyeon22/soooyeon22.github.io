---
title: GitHub를 이용한 Blog만들기 -3
       (Google 검색 엔진에 노출하기)
author: soooyeon22
date: 2024-11-14 11:53:00 +0900
categories: [Github]
tags: [blog,Github,]
---
연관 포스팅

[GitHub를 이용한 Blog만들기 -1](https://soooyeon22.github.io/posts/Github-Blog/) --> 

## step 0. 사전준비 사항

---

- VS Code 설치
- Google 가입
- Github 가입

## Step 1. Google Serch Console에 블로그 등록

---

### 1-1.  [Google Search Console](https://search.google.com/search-console) 접속

Google Search Console은 말 그대로 google에서 검색을 하였을 때, 나의 사이트가 보여질 수 있도록 등록하는 서비스입니다.

- [Google Search Console](https://search.google.com/search-console) 사이트에 접속하세요.
- Google계정으로 로그인 후 “시작하기” 버튼을 누르세요.

### 1-2.  사이트 등록

- 접속하시면 이렇게 화면이 보입니다. [URL 접두어]를 선택하고 자신의 블로그 주소를 입력하세요.  (예시:  `https://suzy.github.io`)
- 도메인이 있으신 분들은 DNS 인증만 진행하면 된다고 하니, 조금 더 빠르게 가능하실 것 같습니다. 일단 저는 도메인이 없기 때문에 우측의 [URL 접두어]를 사용 할 것입니다.

![img5](https://soooyeon22.github.io/assets/img/favicons/img5.png)

## Step 2. 소유권 확인(중요해요!)

---

Google은 소유권을 확인하기 위해 여러가지 방법을 제공합니다.

간단한 HTML 메타 태그 추가 방식을 선택해 진행하겠습니다.

- HTML 파일 업로드
- HTML 메타 태그 추가
- Google Analytics 계정 연결

---

### 2-1. 소유권 확인 방법

- 다른 확인 방법 선택 → HTML 태그 선택→ 복사 (복사까지만 누르세요!!)

![img6](https://soooyeon22.github.io/assets/img/favicons/img6.png)


### 2-2. HTML 메타 태그 추가

- Google에서 제공된 HTML 태그를 복사하세요.
- 복사한 내용을 보면 이렇게 나옵니다.

```html
<meta name="google-site-verification" content="YOUR_CODE" />
```

- VS Code를 들어가서  _config.yml 파일에 들어갑니다.
- google: 옆에 “YOUR_CODE” 부분을 추가해주세요.

```html
# Site Verification Settings
webmaster_verifications:
  google: "YOUR_CODE"
  bing: # fill in your Bing verification code
  alexa: # fill in your Alexa verification code
  yandex: # fill in your Yandex verification code
  baidu: # fill in your Baidu verification code
  facebook: # fill in your Facebook verification cod
```

- 추가한 후 커밋과 푸시를 합니다. 잘 모르시는 분들은 [GitHub를 이용한 Blog만들기 -1](https://soooyeon22.github.io/posts/Github-Blog/)  을 참고해주세요.

### 2-3. 배포 완료 후 확인

- Github에서 변경된 것을 확인한 후, 이제 확인 버튼을 눌러주세요.

## Step 3. 사이트맵 제출하기

---

사이트 맵이란?

웹사이트의 페이지 구조를 검색 엔진에 알려주는 파일입니다. 웹사이트의 URL과 메타데이터(업데이트 날짜, 변경 빈도 등)를 포함하며, 검색 엔진 크롤러가 웹사이트를 효율적으로 탐색하고 색인 하도록 돕습니다.

---

### 3-1. 사이트맵 접속해보기

- sitemap.xml 파일은 루트 아래 있는데 안보일 경우, “블로그주소/sitemap.xml”에 접속하면 이미 만들어진 파일을 볼 수 있습니다. (예시:  `https://suzy.github.io/sitemap.xml`)

### 3-2. 사이트 맵 제출하기

- `sitemap.xml` 파일의 존재를 확인 했다면 아까  [Google Search Console](https://search.google.com/search-console) 로 이동해 Sitemaps로 들어가 주세요.

![img7](https://soooyeon22.github.io/assets/img/favicons/img7.png)


- Sitemaps 탭 → 새 사이트 맵 추가→ URL작성 → 제출

![img8](https://soooyeon22.github.io/assets/img/favicons/img8.png)


- ‘사이트 맵이 제출됨’ 이라는 문구가 뜨면 완료입니다.

## Step3. 결과확인

- Google에 검색

![img9](https://soooyeon22.github.io/assets/img/favicons/img9.png)


- 사이트 맵 제출 후 가져올 수 없음 이라는 문구가 뜨는 경우 화면상의 버그이고 실제로는 정상적으로 동작한다고 합니다. 단! 사이트 맵을 읽을 수 없음 이라고 나오면서 다른 메세지가 없어야 한다고 합니다. 시간이 지나면 검색 사이트에 뜨니 걱정하지 마세요.