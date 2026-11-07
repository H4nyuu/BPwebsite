# 김시온 포트폴리오

전북대학교 컴퓨터인공지능학부 재학생 김시온의 자기소개와 이전 수업의 웹페이지 배포 실습을 소개하는 개인 포트폴리오입니다.

- **사이트:** https://h4nyuu.github.io/BPwebsite/
- **저장소:** https://github.com/H4nyuu/BPwebsite
- **이전 실습 결과:** https://h4nyuu.github.io/teamintro/

## 사이트 구성

- **첫 화면:** 이름, 재학 정보, 프로필 이미지
- **자기소개:** 게임 개발 관심 분야와 선택 이유, 학습 목표, 사용 도구
- **대표 활동:** 제공된 템플릿을 활용한 GitHub Pages 배포 실습의 목적·역할·과정·결과·회고

메뉴의 자기소개와 대표 활동은 같은 페이지의 해당 영역으로 이동합니다.

## 주요 파일과 수정 위치

실제 배포 소스는 **`site/` 폴더**입니다. 최상위 테마 파일이나 `exampleSite/`와 구분해야 합니다.

| 파일 | 역할 |
|---|---|
| `site/data/author.yaml` | 첫 화면 이름·소개 문구·프로필 이미지 설정 |
| `site/data/sections/about.yaml` | 자기소개 내용과 메뉴 설정 |
| `site/data/sections/activity.yaml` | 대표 활동 내용과 메뉴 설정 |
| `site/layouts/partials/sections/portfoliotext.html` | 자기소개·대표 활동 공통 표시 틀 |
| `site/layouts/partials/header.html` | 키보드 포커스 스타일과 메뉴·스크롤 동작 |
| `site/assets/images/prl.jpg` | 프로필 이미지 |
| `site/hugo.yaml` | 사이트 제목·설명·구독란 설정 |
| `.github/pages_build.py` | 의존성 준비·빌드·배포 경로 보정 |
| `.github/workflows/hugo-pages.yml` | GitHub Actions 자동 빌드·배포 |

YAML 수정 시 기존 들여쓰기를 유지합니다. 프로필 이미지 설정의 파일명·확장자·대소문자는 실제 파일과 일치해야 합니다.

## 도구와 버전

- **Git:** 저장소 복제·커밋·push
- **Python 3.9 이상:** 수업 제공 준비·빌드 스크립트 실행
- **Hugo Extended 0.163.0 이상:** 테마 요구 버전
  - 프로젝트의 Actions 빌드 로그에서 확인한 버전: **0.167.0**
- **추가 빌드 도구:** Node.js·npm 등. 설치 단계와 버전은 아래 워크플로 파일을 기준으로 확인합니다.
- **편집 도구:** Visual Studio Code

설치·실행 참고:

- Git: https://git-scm.com/downloads
- Python: https://www.python.org/downloads/
- Hugo: https://gohugo.io/installation/
- 실제 빌드 환경 설정: https://github.com/H4nyuu/BPwebsite/blob/main/.github/workflows/hugo-pages.yml

## 저장소 복제

Git 설치 후 터미널에서 실행합니다.

```bash
git clone https://github.com/H4nyuu/BPwebsite.git
cd BPwebsite
```

## 빌드 방법

### 검증에 사용한 방법: GitHub Actions

이 프로젝트는 **GitHub Actions에서 빌드·배포하고 공개 사이트에서 결과를 확인하는 방식**으로 작업했습니다. 로컬 미리보기 실행 성공을 주장하는 문서는 아닙니다.

워크플로는 필요한 도구를 준비한 뒤, 저장소 최상위에서 다음 명령으로 의존성 준비와 사이트 빌드를 수행합니다.

```bash
python .github/pages_build.py --dependencies
python .github/pages_build.py --build
```

- 위 명령은 워크플로에서 설치하는 Hugo 및 추가 도구가 준비된 환경을 전제로 합니다.
- 일반 PC에서 두 명령만 실행하면 모든 시스템 도구까지 자동 설치되는 것은 아닙니다.
- 상세 설치 순서와 버전은 `.github/workflows/hugo-pages.yml`을 확인합니다.
- 빌드 결과는 저장소 최상위의 `public/` 폴더에 생성됩니다.
- 이미 준비된 이 저장소에서는 `prepare_github_pages.py`를 다시 실행할 필요가 없습니다.

### 자동 빌드·배포 확인

1. `main`에 변경을 push합니다.
2. 저장소의 **Actions** 탭에서 해당 커밋의 실행을 엽니다.
3. 빌드와 GitHub Pages 배포가 모두 성공했는지 확인합니다.
4. 공개 사이트에서 수정한 화면과 링크를 직접 확인합니다.

GitHub Pages의 Source는 **GitHub Actions**를 사용합니다.

- Actions: https://github.com/H4nyuu/BPwebsite/actions
- 공개 사이트: https://h4nyuu.github.io/BPwebsite/

## 콘텐츠 수정과 재배포

1. `site/` 안의 해당 파일을 수정하고 저장합니다.
2. `git status`와 `git diff`로 의도한 변경인지 확인합니다.
3. 변경을 커밋하고 `main`에 push합니다.
4. Actions에서 새 실행의 성공 여부를 확인합니다.
5. 공개 사이트에서 결과를 재검증합니다.

예시 — 첫 화면 소개 수정:

```bash
git status
git diff -- site/data/author.yaml
git add site/data/author.yaml
git commit -m "docs: update homepage introduction"
git push origin main
```

작업 브랜치를 사용하는 경우에는 변경을 `main`에 병합해야 자동 배포됩니다. 빌드·배포가 실패하면 마지막으로 성공한 공개 화면이 유지될 수 있으므로, 커밋 성공과 사이트 반영을 구분해서 확인합니다.

## 직접 설정·수정한 내용

- 본인 이름·재학 정보·프로필 이미지 적용
- 자기소개·대표 활동 섹션과 메뉴 연결
- 타이핑 소개와 사용하지 않는 이메일 구독란 제거
- 사이트 제목·설명 설정
- 내비게이션 버튼·링크와 첫 화면 화살표의 키보드 포커스 표시 개선
- 작은 화면에서 메뉴 밖으로 포커스 이동 또는 메뉴 링크 실행 시 자동 접기
- 키보드로 상단 홈 링크·메뉴 버튼 선택 시 맨 위로 이동
- 배포 경로 보정 과정에서 발생한 JavaScript 손상 문제 수정
- 같은 도메인의 다른 프로젝트인 이전 실습 사이트 링크가 변경되지 않도록 수정

## 검증과 알려진 제한

- 화면 폭 **390px·768px·1440px**에서 본문·메뉴·이미지의 배치를 확인했습니다.
- 키보드의 **Tab·Shift+Tab·Enter**로 주요 메뉴와 링크를 확인했습니다.
- 삼단줄 버튼과 첫 화면 화살표의 포커스 표시, 상단 버튼 선택 시 최상단 이동을 수정 후 확인했습니다.
- 이전 실습 사이트로 연결되는 링크와 구독란 제거를 확인했습니다.
- 빌드·배포 성공은 모든 기능의 자동 검증을 의미하지 않습니다.
- 작업 중 Mulish 글꼴 파일의 404가 관찰되었습니다. 최종 해결 여부는 별도 재확인이 필요하며, 해결 완료로 간주하지 않습니다.
- 최종 제출 버전의 검사 시각·브라우저 버전·화면 근거·남은 문제는 제출 보고서에 기록합니다.

## 출처와 제작 범위

### Toha 테마

- 원본 저장소: https://github.com/hugo-themes/toha
- 원본 README: https://github.com/hugo-themes/toha/blob/main/README.md
- 라이선스: 저장소에 포함된 `LICENSE` 및 원본 파일별 고지를 확인합니다.
- 테마 전체를 직접 개발한 것이 아니라, 제공된 테마에 개인 콘텐츠와 설정·동작 수정을 적용했습니다.
- 원본 라이선스 파일과 필요한 저작권·라이선스 고지는 삭제하지 않습니다. 원본 README의 일반 사용 설명 대신 이 프로젝트의 실행 안내를 작성했습니다.

### 수업 제공 자료

- 준비·배포 스크립트: 전북대학교 2026학년도 2학기 초급프로젝트 수업 제공 자료
- 대표 활동의 템플릿: 같은 학기 초급프로젝트 1분반 수업 제공 자료
- 이전 실습은 제공된 HTML·CSS·JavaScript 템플릿의 저장소 등록·배포·동작 확인을 수행한 활동입니다. 템플릿 화면과 버튼 기능 자체를 직접 개발한 것으로 주장하지 않습니다.

### 본문·이미지·AI 활용

- 자기소개와 활동의 사실관계는 본인의 경험과 계획을 바탕으로 작성했습니다.
- BAZE Mindlogic Super Agent의 도움으로 문안 정리, 설정·코드 수정안 작성, 오류 분석과 검증 절차 안내를 받았습니다.
- 제안의 채택과 파일 반영, 커밋·push, 브라우저에서의 실제 확인은 본인이 수행했습니다.
- 프로필 이미지 `site/assets/images/prl.jpg`: 친구가 촬영한 본인 사진입니다. 외부 웹사이트에서 가져온 이미지가 아닙니다.
- 테마 기본 배경과 기타 테마 포함 자산은 원본 자료이며, 개별 파일에 별도 이용 조건이 있다면 해당 고지를 따릅니다.