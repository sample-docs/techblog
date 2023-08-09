# How to contribute to Tech Blog

이 가이드는 기고자가 직접 마크다운과 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 문서화 플랫폼을 사용하여 테크 블로그에 기고하는 방법을 안내합니다.

안내 범위는 기획안을 바탕으로한 [초안 템플릿 생성](#step-1-tw가-초안-템플릿-생성)부터 [초안 배포](#4-초안-확인)까지이며, 전체적인 기술 블로그 운영 프로세스는 [여기](https://docs.google.com/presentation/d/1Vj2fPxkv4lRkNK6vzrvJKexuQG6UPk0zQDtRaMcP8vs/edit#slide=id.g25a55c4c35b_0_14)를 참고하세요.

당신이 기고자인 경우, [Step 2](user-content-step-2-기고자가-초안-작성) 중심으로 확인하시기 바랍니다.

<br>

## Step 1: TW가 초안 템플릿 생성
TW가 feature 브랜치 생성 후 기고자가 작성한 기획안을 바탕으로 초안 템플릿을 작성합니다.

[Git Flow 모델](https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html)를 활용하여 develop 브랜치를 기준으로 feature 브랜치 생성 후 초안 템플릿 생성합니다.

```
git flow init

{Continue to Enter}

git flow feature start {feature branch}
```
feature 브랜치에 초안 템플릿 파일 `{카테고리}-{기고자명}-{생성날짜}.md`(예:Rnd-hojun-230804.md)을 생성합니다. 이후 기획안을 바탕으로 초안 작성을 위한 초안 템플릿을 작성합니다(목차 구성, 기본 단락, 소주제 구성 등)

작업한 초안템플릿이 존재하는 feature 브랜치를 원격에 공유합니다.

`git flow feature publish {feature branch}`

<br>

## Step 2: 기고자가 초안 작성 

### 1. 문서 작업 환경 구성
기고자의 로컬 환경에서 블로그와 동일한 사이트를 빌드하며 초안 작성을 할 수 있도록 아래와 같이 문서 작업 환경을 구성합니다.

> ⚠️ 아래의 명령 실행에 앞서, Github에 회사 계정으로 접속 후 Personal Access Token(PAT)을 발급해야 합니다.
> 발급 방법은 [여기](https://docs.github.com/ko/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic)를 참조하세요.
> 
> 발급받은 PAT로 하여금 [저희의 문서화 Private Repo](https://github.com/morai-techblog/mkdocs-material-insiders)에 대한 접근 권한이 있는지를 인증할 수 있습니다.

```
python.exe -m pip install --upgrade pip
python.exe -m pip install  mkdocs-material
python.exe -m pip install git+https://{PAT}@github.com/morai-techblog/mkdocs-material-insiders.git

pip install mkdocs-minify-plugin
pip install mkdocs-rss-plugin
```

### 2. 블로그 리포지터리 및 Feature branch 복사 
`git clone --branch {feature branch} https://github.com/morai-techblog/morai-techblog.github.io.git`

### 3. 초안 작성
초안 작성은 글을 잘 쓴다기 보다는 초안 템플릿의 주요 항목을 채운다는 개념으로 접근하면 쉽습니다.
또한 각 목차 및 단락 별 소주제에 맞는 내용을 작성하는 것이 중요함. 필요한 캡처, 표, 그림을 최대한 활용헙나다.

초안 작성 후 1차 맞춤법 검사 --> [다음 맞춤법 검사기](https://alldic.daum.net/grammar_checker.do)

### 4. 초안 확인
아래의 명령으로 앞에서 구성한 문서 작업 환경에서 사이트를 빌드하며 웹 형태로 작성된 초안을 검토합니다.
`mkdocs serve`
  
### 5. 초안 공유 
feature 브랜치에서 작성한 초안을 커밋하여 원격에 공유합니다.
```
git add .
git commit -am "초안 작성 완료"

git push origin {feature branch}
```
<br>

## Step 3: TW가 초안 수정 및 편집
TW가 초안을 수정 및 편집하며 feature 브랜치 업데이트

수정된 초안을 develope 브랜치에 머지하도록 PR 요청 (meta.draft: true 상태)

기고자가 머지 승인 및 머지 완료

<br>

## Step 4: 초안 완성 및 배포
TW가 메타 데이터 확정: 날짜, 작가, 제목, 설명, 카테고리 등(meta.draft: false로 변경), 최종 내용 검수

TW가 PR 요청: develop to main branch

Github Action으로 맞춤법 자동 검사 

PM이 코멘트 후 머지 승인, 머지 완료

TW가 gh-pages 브랜치에 초안 배포:
`mkdocs gh-deploy --config-file mkdocs.yml --remote-branch gh-pages`






