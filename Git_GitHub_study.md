# Git & GitHub 학습 정리

## 1. 왜 Git과 GitHub를 사용해야 할까?

### 버전 관리
- Git은 코드의 변경 이력을 기록·추적할 수 있게 해준다.
- 실수로 코드를 잘못 수정해도 이전 버전으로 쉽게 되돌릴 수 있다.

### 협업 용이
- 여러 명이 각자의 브랜치(branch)에서 동시에 작업한 후 병합(merge)할 수 있다.
- 팀원 간 코드 리뷰가 가능해 서로의 코드를 확인하고 피드백을 주고받을 수 있다.

### 백업 및 중앙 집중화 (GitHub)
- GitHub는 클라우드 기반의 중앙 저장소 역할을 한다.
- 로컬 컴퓨터가 고장나도 GitHub에 저장된 코드로 데이터 손실을 방지할 수 있다.

### 오픈소스 및 공개 협업
- 누구나 오픈소스 프로젝트에 기여하거나 자신의 프로젝트를 공개해 피드백을 받을 수 있다.

### CI/CD 및 자동화 지원
- 코드를 push하면 자동으로 테스트·배포하는 등의 작업을 자동화할 수 있다.

### 문서화 및 프로젝트 관리
- README 파일로 프로젝트 개요를 문서화할 수 있고, 이슈 추적 기능으로 작업 항목을 체계적으로 관리할 수 있다.

---

## 2. Git이란?

프로젝트의 모든 변경 사항을 기록·관리하고, 여러 사람이 동시에 작업할 수 있게 하는 **분산형 버전 관리 시스템**.

- **버전 관리**: 파일과 폴더의 변경 사항을 "커밋(commit)" 단위로 기록하여 과거 시점으로 되돌아갈 수 있다.
- **분산형 시스템**: 각 사용자가 자신의 컴퓨터에 전체 프로젝트의 복사본을 가지고 작업 → 중앙 서버와 연결이 끊겨도 작업 지속 가능.
- **브랜치(branch) 기능**: 독립적인 작업을 위한 브랜치를 만들고, 완성되면 다시 병합(merge) 가능.
- **협업**: 여러 사람의 작업을 효과적으로 병합하고, 충돌 발생 시 해결 기능 제공.

## 3. GitHub란?

개발자들이 효율적으로 협업하고 프로젝트를 체계적으로 관리하도록 돕는 **웹 기반 플랫폼**.

- **원격 저장소**: Git으로 관리되는 프로젝트를 인터넷 상에 호스팅.
- **협업 도구**: 변경 사항을 올리면 다른 사람이 검토하고 병합 가능.
- **오픈소스와 커뮤니티**: 전 세계 개발자가 오픈소스 프로젝트를 공유·기여하는 플랫폼.

---

## 4. 개발 환경 준비

### 터미널 열기
- Mac: `Command + Space` → "Terminal" 검색 → 실행
- Windows: 검색창에 `cmd` 입력 또는 `윈도우 키 + R` → `cmd` 입력

### Homebrew 설치 (Mac 전용)
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
설치 완료 확인:
```bash
brew --version
brew list
```

### Git 설치 (Mac, brew 이용)
```bash
brew install git
git --version
```
Windows는 공식 Git 설치 가이드를 통해 설치.

### Git 전역 설정 (최초 1회)
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
git config --list   # 설정 확인
```

> `dquote>` 프롬프트가 계속 뜨면 `ctrl + g`로 빠져나온 뒤, 따옴표 오류인지(짝이 안 맞는지) 확인하고 아래처럼 설정을 지운 후 다시 시도한다.
> ```bash
> git config --global --unset user.name
> git config --global --unset user.email
> ```

---

## 5. Repository 생성 & 원격 저장소 연결

### 방법 1 — 로컬에서 시작 후 원격 연결
1. 작업 디렉토리 생성
   ```bash
   pwd
   cd Desktop
   mkdir oz_assignment
   cd oz_assignment
   ```
2. GitHub에서 새 레포지토리 생성 (Repository name: `oz_assignment`, 공개 여부: Public)
3. 터미널에서 Git 초기화 및 원격 저장소 연결
   ```bash
   echo "# oz_assignment" >> README.md
   git init
   git add README.md
   git commit -m "first commit"
   git branch -M main
   git remote add origin <URL>
   git push -u origin main
   ```

### 방법 2 — Git Clone으로 시작
1. GitHub에서 레포지토리 생성 (Public)
2. 원하는 디렉토리로 이동 후 clone
   ```bash
   cd Desktop
   git clone <본인 레포지토리 URL>
   ```

### `.git` 폴더
- Git 저장소의 핵심. 모든 커밋, 브랜치, 태그, 메타데이터가 저장되는 숨겨진 디렉토리.
- **절대 삭제 금지**. 최상위 폴더에 하나만 존재해야 하며, 하위 폴더에 중복 생성 시 충돌 원인이 된다.

---

## 6. VSC에서 add / commit / push 3종 세트

1. VSC에서 `oz_assignment` 디렉토리 열기
2. 작업 후 저장 (`Command + S`)
3. VSC 터미널 열기 (`Command + J`)
4. 상태 확인
   ```bash
   git status
   ```
5. 스테이징
   ```bash
   git add day_1     # 특정 폴더만
   git add .         # 전체 파일
   ```
6. 커밋
   ```bash
   git commit -m "커밋 메시지"
   ```
7. 푸시
   ```bash
   git push origin main
   ```
8. GitHub에서 반영 확인

> 주의: 같은 작업 폴더에서 `git init`은 **한 번만** 진행한다.

---

## 7. 과제 폴더 구조 추천

폴더/파일명은 띄어쓰기 대신 언더바(`_`) 사용.

```
oz_assignment/
├── PYTHON/
│   ├── day_1/
│   ├── day_2/
│   └── day_3/
├── HTML/
│   ├── day_1/
│   └── day_2/
├── JS/
│   ├── day_1/
│   ├── day_2/
│   ├── day_3/
│   ├── day_4/
│   └── day_5/
└── FLASK/
    ├── day_1/
    └── day_2/
```

---

## 8. 간단 요약 — 새 폴더를 GitHub에 업로드하는 전체 흐름

```bash
git init                              # 최초 1회
git remote add origin "레포지토리 주소"
git remote -v                         # 연결 확인
git branch -M main                    # master → main 변경 (필요 시)
git add .
git commit -m "커밋 메세지"
git push origin main
```

---

## 오늘의 핵심 요약

- Git = 로컬에서 변경 이력을 관리하는 **분산 버전 관리 시스템**
- GitHub = Git 저장소를 온라인에 호스팅하고 협업을 돕는 **플랫폼**
- 핵심 워크플로우: `git add` → `git commit` → `git push`
- 레포지토리 연결 방법은 크게 두 가지: (1) 로컬 초기화 후 원격 연결, (2) `git clone`으로 시작
- `.git` 폴더는 버전 관리의 핵심이므로 절대 삭제하지 않는다
