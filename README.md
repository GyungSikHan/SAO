# SAO Project

AI가 세계관의 규칙과 플레이어의 행동을 바탕으로 NPC 대화, 퀘스트, 아이템 설명 및 사건을 생성하는 Unreal Engine 기반 액션 RPG 프로젝트입니다.

---

## 개발 환경

| 항목 | 버전 및 설정 |
|---|---|
| Unreal Engine | 5.5.4 |
| Visual Studio | Visual Studio 2022 17.14 |
| Visual Studio Code| |
| 기본 브랜치 | `main` |
| Git 대용량 파일 관리 | Git LFS |
| 게임 클라이언트 | Unreal Engine C++ / Blueprint |
| AI 서버 | Python / FastAPI 예정 |

> `Unreal Engine 5.5.4`는 프로젝트에서 실제로 사용하는 정확한 버전으로 수정해 주세요.

---

## 저장소 복제

### 1. Git LFS 설치

프로젝트의 `.uasset`, `.umap` 파일은 Git LFS로 관리합니다.

Git LFS가 설치되어 있는지 확인합니다.

```bash
git lfs version
```

Git LFS가 설치되어 있다면 다음 명령을 실행합니다.

```bash
git lfs install
```

### 2. 저장소 복제

```bash
git clone <REPOSITORY_HTTPS_URL>
cd SAO
```

`<REPOSITORY_HTTPS_URL>`에는 실제 저장소 HTTPS 주소를 입력합니다.

예시:

```bash
git clone https://github.com/username/repository.git
```

### 3. LFS 파일 다운로드 확인

일반적으로 저장소를 복제할 때 LFS 파일도 함께 다운로드됩니다.

에셋이 정상적으로 내려받아지지 않은 경우 다음 명령을 실행합니다.

```bash
git lfs pull
```

LFS로 관리되는 파일은 다음 명령으로 확인할 수 있습니다.

```bash
git lfs ls-files
```

---

## 프로젝트 실행

### 1. Unreal Engine 버전 확인

프로젝트에서 사용하는 Unreal Engine 버전과 동일한 버전을 설치합니다.

버전이 다르면 에셋 또는 C++ 코드 호환 문제가 발생할 수 있습니다.

### 2. Visual Studio 구성

Visual Studio Installer에서 다음 워크로드 및 구성 요소를 설치합니다.

- Desktop development with C++
- Game development with C++
- Visual Studio Tools for Unreal Engine
- Windows 10 SDK 또는 Windows 11 SDK

저장소에 `.vsconfig` 파일이 포함되어 있다면 Visual Studio Installer에서 해당 설정을 사용할 수 있습니다.

### 3. Visual Studio 프로젝트 파일 생성

`SAO.uproject` 파일을 우클릭한 뒤 다음 메뉴를 실행합니다.

```text
Generate Visual Studio project files
```

메뉴가 보이지 않으면 먼저 Unreal Engine을 설치하고 `.uproject` 파일 연결 상태를 확인합니다.

### 4. 프로젝트 빌드

생성된 Visual Studio 솔루션을 열고 다음 구성으로 빌드합니다.

```text
Configuration: Development Editor
Platform: Win64
```

빌드가 완료되면 `SAO.uproject`를 실행합니다.

프로젝트 실행 중 C++ 모듈을 다시 빌드하겠다는 메시지가 표시되면 빌드를 진행합니다.

---

## 환경변수와 API 키

API 키와 개인 환경설정은 Git에 올리지 않습니다.

다음 파일은 `.gitignore`에 포함되어 있습니다.

```text
.env
.env.*
```

팀원이 사용할 환경변수 목록은 `.env.example` 파일로 공유합니다.

예시:

```env
AI_API_KEY=your_api_key_here
AI_SERVER_URL=http://127.0.0.1:8000
```

실제 `.env` 파일은 각자 로컬 환경에서 생성합니다.

```text
.env.example
→ 복사
→ .env로 이름 변경
→ 개인 API 키 입력
```

> 실제 API 키를 GitHub, GitLab, Discord 또는 메신저에 그대로 올리지 마세요.

---

## Git 작업 규칙

### 작업 시작 전

```bash
git checkout main
git pull
```

기능 개발은 별도 브랜치에서 진행하는 것을 권장합니다.

```bash
git checkout -b feature/기능이름
```

예시:

```bash
git checkout -b feature/ai-npc-dialogue
git checkout -b feature/quest-system
git checkout -b fix/player-movement
```

### 변경사항 커밋

```bash
git add .
git commit -m "feat: add AI NPC dialogue"
```

### 원격 저장소에 업로드

```bash
git push -u origin feature/ai-npc-dialogue
```

작업 완료 후 Pull Request 또는 Merge Request를 생성합니다.

---

## 커밋 메시지 규칙

| 접두사 | 용도 |
|---|---|
| `feat` | 새로운 기능 |
| `fix` | 버그 수정 |
| `refactor` | 기능 변화 없는 코드 개선 |
| `chore` | 설정, 빌드, Git 관리 |
| `docs` | 문서 수정 |
| `asset` | 에셋 추가 또는 수정 |
| `test` | 테스트 코드 |

예시:

```text
feat: add quest generation API
fix: resolve NPC dialogue UI error
asset: add village environment assets
docs: update project setup guide
chore: configure Git LFS
```

---

## Git에 포함되는 주요 항목

```text
Config/
Content/
Source/
Plugins/          # 프로젝트 전용 플러그인이 있을 경우
SAO.uproject
.gitignore
.gitattributes
.vsconfig
README.md
```

다음 폴더는 Unreal Engine이 자동 생성하므로 Git에 올리지 않습니다.

```text
Binaries/
DerivedDataCache/
Intermediate/
Saved/
.vs/
```

---

## 주의사항

### Unreal 에셋 충돌

`.uasset`과 `.umap`은 일반 텍스트처럼 자동 병합하기 어렵습니다.

동일한 맵, Blueprint 또는 DataAsset을 두 명이 동시에 수정하지 않도록 작업 전에 담당 파일을 공유합니다.

특히 다음 파일은 동시 수정을 피합니다.

- 레벨 맵
- GameMode Blueprint
- Player Character Blueprint
- 공용 Widget Blueprint
- 공용 DataTable 또는 DataAsset

### 에셋 이동 및 이름 변경

Unreal Editor 밖의 Windows 탐색기에서 `.uasset` 파일을 직접 이동하거나 이름을 변경하지 않습니다.

에셋 이동과 이름 변경은 Unreal Editor의 Content Browser에서 진행합니다.

이동 후에는 폴더를 우클릭하고 다음 작업을 실행합니다.

```text
Fix Up Redirectors in Folder
```

### 엔진 버전 업그레이드

팀원 개인이 임의로 Unreal Engine 버전을 업그레이드하지 않습니다.

엔진 버전 변경은 팀원 간 합의 후 별도 브랜치에서 테스트합니다.

---

## 문제 해결

### 에셋 파일이 작거나 열리지 않는 경우

Git LFS 포인터만 내려받아졌을 수 있습니다.

```bash
git lfs pull
```

### Visual Studio 솔루션이 없는 경우

`.sln` 파일은 Git에서 관리하지 않습니다.

`SAO.uproject`를 우클릭하고 다음 작업을 실행합니다.

```text
Generate Visual Studio project files
```

### 빌드 오류가 발생하는 경우

다음 폴더를 삭제한 뒤 프로젝트 파일을 다시 생성합니다.

```text
Binaries/
Intermediate/
.vs/
```

그 후:

1. `SAO.uproject` 우클릭
2. `Generate Visual Studio project files`
3. Visual Studio에서 `Development Editor / Win64` 빌드

---

## 프로젝트 담당

### Unreal Engine 클라이언트

- 경식
- 전투 시스템
- 캐릭터 및 적 AI
- 레벨 및 UI
- 저장 시스템

### AI 및 서버

- 이용진
- Python / FastAPI
- LLM API 연동
- NPC 기억 관리
- 퀘스트 생성
- 생성 결과 검증
- 데이터베이스 관리
-  HTTP 및 JSON 연동
