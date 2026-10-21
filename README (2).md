# STUDIO 상상 | 영상 제작 스튜디오 웹사이트

> 상상을 넘어 장면이 되다

영상 제작 서비스와 제작 사례를 소개하고, 제작 문의와 예상 견적 확인으로 연결하는 포트폴리오 웹사이트입니다.

## 프로젝트 소개

브랜드 소개 → 서비스 이해 → 포트폴리오 탐색 → 제작 문의로 이어지는 정보 구조를 갖춘 정적 웹사이트입니다. HTML, CSS, JavaScript를 사용하며 별도의 패키지 설치나 빌드 과정 없이 실행됩니다.

## 디자인 방향

| 요소 | 스타일 |
| --- | --- |
| 배경 | 화이트 `#FFFFFF` |
| 텍스트 | 블랙 `#000000` |
| 포인트 1 | 라임 `#E0FF4F` — 주요 문구·메뉴 강조 |
| 포인트 2 | 블루 `#1647FF` — 구분선·그래픽 포인트 |

## 핵심 구성

- **브랜드 소개**: 스튜디오의 서비스와 방향을 전달합니다.
- **작업물 탐색**: 제작 사례 이미지와 영상으로 결과물을 보여줍니다.
- **문의 연결**: 개인·기업 제작 문의 및 예상 견적 확인을 제공합니다.
- **화면 이동**: 마우스 휠과 터치 기반 장면 이동을 지원합니다.

---

## 주요 페이지

- **ABOUT US**: 스튜디오 소개, 서비스, 협력 브랜드
- **AI VIDEO**: AI 영상 제작 서비스 소개
- **PORTFOLIO**: 제작 사례 이미지 및 영상
- **CONTACT**: 개인·기업 제작 문의와 예상 견적 확인

## 폴더 구조

```text
.
├─ index.html              # main/index.html로 이동하는 시작 페이지
├─ reset.css               # 공통 CSS 초기화
├─ site-header.css         # 공통 헤더 및 푸터 스타일
├─ site-header.js          # 공통 헤더, 푸터, 페이지 이동
├─ scene-scroll.js         # 화면 단위 스크롤과 터치 이동
├─ site-enhancements.js    # TOP 버튼 및 페이지별 보조 기능
├─ main/                   # ABOUT US 메인 페이지와 이미지
├─ ai-video/               # AI VIDEO 페이지, 영상, 이미지, 폰트
├─ portfolio/              # 포트폴리오 페이지, 상세 이미지와 영상
├─ contact/                # 문의 페이지, 견적 계산 로직과 미디어
└─ social/                 # SNS 이미지
```

폴더와 파일의 상대 경로를 사용하므로 배포하거나 전달할 때 전체 구조를 그대로 유지해야 합니다.

## 실행 방법

가장 간단한 방법은 루트의 `index.html`을 Chrome 또는 Edge로 여는 것입니다.

로컬 서버로 확인하려면 프로젝트 폴더에서 다음 명령을 실행합니다.

```bash
python -m http.server 8000
```

그다음 브라우저에서 `http://localhost:8000`으로 접속합니다.

## 문의 페이지 설정

문의 페이지의 연락처, 상담 시간, 상품, 옵션, 가격은 `contact/inquiry-config.js`에서 관리합니다.

실제 문의 접수를 연동하려면 아래 항목을 운영 환경에 맞게 설정해야 합니다.

- `contacts.email`: 문의 이메일 주소
- `contacts.kakao`: 카카오톡 상담 주소
- `inquiryEndpoint`: 문의 내용을 받을 서버 API 주소
- `privacy`: 개인정보 수집 목적 및 보유 기간

`inquiryEndpoint`가 비어 있으면 문의 내용을 실제 서버로 전송할 수 없습니다.

## GitHub Pages 배포

1. 이 폴더의 전체 파일을 GitHub 저장소 루트에 업로드합니다.
2. 저장소의 **Settings → Pages**로 이동합니다.
3. 배포 소스를 **Deploy from a branch**로 선택합니다.
4. 사용할 브랜치와 `/(root)` 폴더를 선택한 뒤 저장합니다.
5. 배포가 완료되면 안내된 Pages 주소로 접속합니다.

### 용량 최적화 및 업로드

포트폴리오 HTML에 내장되어 있던 이미지를 `portfolio/optimized-images/`의 WebP 파일로 분리했습니다. 이 폴더도 함께 업로드해야 합니다.

영상은 H.264 MP4로 압축하고 웹에서 재생을 빨리 시작할 수 있도록 `faststart`를 적용했습니다. 영상의 전체 길이와 오디오는 유지하며, 큰 사진·포스터는 WebP로 변환했습니다. 원본 자료는 배포 폴더 밖에 따로 백업했습니다.

GitHub는 일반 Git 저장소에서 파일 하나가 100 MiB를 넘으면 업로드를 차단합니다. 브라우저의 파일 업로드는 25 MiB 제한이 있으므로, 이 프로젝트는 Git 명령으로 업로드하세요. [GitHub 파일 용량 안내](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)

**압축 전 파일을 이미 로컬에서 커밋했다면**, 파일을 바꾸고 새 커밋만 추가해도 이전 기록에 큰 파일이 남습니다. 아직 푸시하지 않은 최초 커밋 하나만 있는 경우 다음 명령으로 그 커밋을 최적화된 파일로 갱신할 수 있습니다.

```bash
git add -A
git commit --amend --no-edit
git branch -M main
git push -u origin main
```

이미 다른 사람과 공유하거나 원격 저장소에 푸시한 기록에는 위의 커밋 수정 명령을 그대로 적용하지 마세요.

## 수정 가이드

- 공통 메뉴와 푸터: `site-header.js`, `site-header.css`
- 메인 페이지: `main/index.html`
- AI VIDEO 페이지: `ai-video/index.html`, `ai-video/css_*.css`, `ai-video/js_*.js`
- 포트폴리오: `portfolio/index.html`, `portfolio/project-details.css`, `portfolio/project-details.js`
- 문의 및 견적: `contact/index.html`, `contact/inquiry.css`, `contact/inquiry.js`, `contact/inquiry-pricing.js`

이미지나 영상을 교체할 때는 기존 파일명과 경로를 유지하거나, 해당 HTML·CSS·JavaScript의 참조 경로를 함께 변경해야 합니다.

## 기술 구성

- HTML5
- CSS3
- Vanilla JavaScript
- 반응형 레이아웃
- 마우스 휠 및 터치 기반 장면 이동

## 브라우저 권장 환경

최신 버전의 Chrome, Edge, Safari, Firefox를 권장합니다.

## 문서 기준

첨부된 README를 기반으로 재구성했습니다. 실제 소스 코드·화면·배포 상태는 별도로 검증하지 않았습니다.
