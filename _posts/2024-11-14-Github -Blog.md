---
title: GitHub를 이용한 Blog만들기 -1
       (Chirpy Theme)
author: soooyeon22
date: 2024-11-14 11:53:00 +0900
categories: [Github]
tags: [blog,Github]
---

연관 포스팅

🔗[GitHub를 이용한 blog만들기 -2](https://soooyeon22.github.io/posts/Github-Blog3/)

---

## Github blog(깃허브 블로그)란?

Github에는 여러가지 파일이 업로드,저장이 이루어집니다. 그 중, 저장된 html파일 같은 웹 문서들을 Github에서 무료로 호스팅을 제공해주는 서비스가 존재합니다. 바로 **Github Page**입니다. 이 Github Page를 이용하여 Blog를 만든것이 Github Blog(깃허브 블로그, 깃블로그)입니다

Github page를 이용해  Jekyll 기반 Github blog를 만들어 보겠습니다.

## Step 0.  사전준비 사항

---

- Windows 64bit
- Git 설치
- VS Code 설치
- Github 가입

## Step 1.  Github Page 생성

---

### step 1-1. Repository 생성

- github username이 suzy인 경우, repository name 을 suzy.github.io로 설정해주세요.
- Public 체크해 주세요.
- Add a REAME file 체크해 주세요.

![img1](https://soooyeon22.github.io/assets/img/favicons/img.png)

### Step 1-2. Github Page 설정

- 생성한 리포지토리로 이동하여, 상단 Settings 클릭하세요.
- 좌측 **Pages** 클릭하세요.
- **Source**를 Deploy from a branch로 설정하세요.
- 사이트 접속 확인하세요.  (예시: `https://suzy.github.io`)

### Step 1-3. VS Code 활용

리포지토리 클론

- 폴더를 로컬 디스크 (D:)에 저장하지 않게 주의하세요.
    
     (나중에 Start Command Prompt with Ruby 실행할 때 문제가 될 수 있음)
    
- VS Code 열기 → F1 키 입력 → git clone 검색 → Git: Clone 선택하세요.

![img2](https://soooyeon22.github.io/assets/img/favicons/img2.png)

- 리포지토리 주소 입력 → 클론할 위치 선택하세요.

![img3](https://soooyeon22.github.io/assets/img/favicons/img3.png)



- 이 때, 한글이 포함된 경로를 선택하지 않도록 주의하세요.

로컬 변경사항 적용

- 클론한 리포지토리 열어보세요. (REAME.md 파일 확인)
- index.html 파일 생성하세요.

```html
<html>
		<body>
				Hello! This is the first page!
		</body>
</html>
```

- 좌측 **Source Control** 메뉴 선택하세요.
- + 버튼을 클릭하여 변경사항 추가하세요.

![img4](https://soooyeon22.github.io/assets/img/favicons/img4.png)


- 커밋 메시지 입력, 커밋 & 푸시하세요.
- 사이트 반영 확인하세요. (예시:  `https://suzy.github.io`)

## Step 2. 로컬 개발 환경 구축

---

### step 2-1. Ruby 설치

- [공식 홈페이지](https://rubyinstaller.org/downloads/)에서 최신버전 다운로드 (Ruby+Devkit x.y.z-1 (x64)) 및 설치하세요.
- 시작(윈도우 키)메뉴에서 `Start Command Prompt with Ruby` 실행하세요.
- cd 명령어로 리포지토리가 있는 위치로 이동하세요.
- 리포지토리가 있는 폴더에서 오른쪽 버튼 클릭을 한 후 경로로 복사 클릭 후 붙혀넣기 가능합니다.

```
cd C:\Users\susy\Documents\suzy.github.io
```

- jekyll, bundler, webrick 설치하세요

```
gem install jekyll bundler
gem install webrick
```

- 설치 확인하세요.

```
ruby -v
jekyll -v
bundler -v
```

### Step 2-2. Jekyll 서버 구축

- jekyll 생성하세요.

```
jekyll new ./
# 또는
jekyll new ./ --force
```

- bundle install

```
bundle install
```

- jekyll 서버 실행하세요.

```
bundle exec jekyll serve
```

- http://127.0.0.1:4000/ 또는 http://localhost:4000/ 접속 확인하세요.

## Step 3. Jekyll 테마 적용

---

### Step 3-0. 테마 선택

- [http://jekyllthemes.org](http://jekyllthemes.org/)
- [https://jekyllthemes.io/free]
- [https://themes.jekyllrc.org](https://themes.jekyllrc.org/)
- [https://github.com/topics/jekyll-theme]

### Step 3-1. chirpy 테마 적용

- [공식 홈페이지](https://github.com/cotes2020/jekyll-theme-chirpy)에서 압축파일 다운로드하세요.
- 압축을 해제한 뒤, 모든 파일과 폴더를 로컬 리포지토리로 복사하세요.
- bundle install

```
bundle install
```

- jekyll 서버 실행하세요.

```
bundle exec jekyll serve
```

- http://127.0.0.1:4000/ 또는 http://localhost:4000/ 접속 확인하세요.
- 모든 변경사항 커밋 및 푸시하세요.

### Step 3-4. 테마 상세 설정

- `.gitignore` 파일 하단 수정하세요.

```html
# Misc
# _sass/dist
# assets/js/dist
```

- `_config.yml` 파일 수정하세요.

```html
timezone: Asia/Seoul

url: "https://suzy.github.io"

github:
  username: karina
```

- 모든 변경사항 커밋 및 푸시하세요.
- 커밋 메시지 주의하세요.
- 사이트 반영 확인하세요. (예시: `https://suzy.github.io`)

[https://jekyllthemes.io/free]: https://jekyllthemes.io/free
[https://github.com/topics/jekyll-theme]: https://github.com/topics/jekyll-theme`