# Secretary Dashboard 프로젝트 가이드

**프로젝트 생성일:** 2026-05-06  
**저장소:** https://github.com/hoikyung/secretary-test  
**배포:** https://secretary-test-five.vercel.app/  
**계정:** hoikyung02@gmail.com

---

## 📋 프로젝트 개요

Secretary(비서) 업무를 지원하는 통합 대시보드 시스템으로, 다음 3가지 핵심 페이지로 구성됩니다:

| 페이지 | 파일 | 기능 | 상태 |
|--------|------|------|------|
| 📊 대시보드 | dashboard.html | 주간 일정, 할 일, 프로젝트 진행률, 매출 요약 | ✅ 완성 |
| 📈 매출 현황 | chart.html | 월별 매출 추이 및 제품별 판매량 분석 | ✅ 완성 |
| 📋 사이트 분석 | report.html | SubTrackr.kr 웹사이트 상세 분석 보고서 | ✅ 완성 |

---

## 🎨 디자인 시스템

### 색상 팔레트
```css
/* 다크 모드 (기본) */
배경: #0F1419 (매우 어두운 파랑)
카드: rgba(255,255,255,0.08) (투명한 흰색 오버레이)
텍스트: #FFFFFF

/* 라이트 모드 */
배경: #F5F5F5 (밝은 회색)
카드: rgba(255,255,255,0.9) (거의 불투명한 흰색)
텍스트: #1A1A1A (매우 어두운 회색)
```

### 스타일 특징
- **글래스모피즘**: `backdrop-filter: blur(10px)`으로 유리창 효과
- **그래디언트 배경**: 라디얼 그래디언트를 이용한 애니메이션 오브 효과
- **부드러운 그림자**: `box-shadow: 0 8px 32px rgba(0,0,0,0.1)`
- **애니메이션**: `cubic-bezier(0.4, 0.0, 0.2, 1)` 이징으로 부드러운 전환

### 네비게이션
모든 페이지에 동일한 sticky 네비게이션 바:
```html
<nav class="header-nav">
  <a class="nav-tab active" href="dashboard.html">📊 대시보드</a>
  <a class="nav-tab" href="chart.html">📈 매출 현황</a>
  <a class="nav-tab" href="report.html">📋 사이트 분석</a>
</nav>
```

---

## 📁 파일 구조

```
워크숍-실습/
├── dashboard.html          # 메인 대시보드 (진입점)
├── chart.html              # 매출 분석 차트
├── report.html             # 사이트 분석 보고서
├── index.html              # Vercel 진입점 (자동 리다이렉트)
├── vercel.json             # Vercel 배포 설정
├── .env                    # 로컬 환경변수 (GitHub 토큰)
├── .gitignore              # Git 무시 파일 목록
├── .git/                   # Git 저장소
│
├── 김비서-데이터/          # 원본 CSV 데이터 폴더
│   ├── 매출데이터.csv      # 월별/일별 매출 데이터
│   ├── 프로젝트현황.csv    # 프로젝트 진행 상태
│   ├── 업무목록.csv        # 업무 할 일 목록
│   ├── 주간일정.txt        # 주간 일정표
│   └── 회의록.txt          # 회의 기록
│
└── 정리해줘/               # 정리된 파일 폴더
    ├── 보고서/             # 보고서 문서들
    ├── 메모/               # 메모 및 아이디어
    ├── 업무/               # 업무 관련 문서
    └── 기타/               # 기타 파일

```

---

## 🎯 주요 기능 상세

### 1. Dashboard (dashboard.html)

#### 📊 구성 섹션 (4개)

**a) ✅ 할 일 목록 (Todo List)**
- CSV에서 읽은 데이터
- 우선순위별 색상 구분
  - 🔴 높음 (High): #FF6B6B
  - 🟠 중간 (Medium): #FFA500
  - 🟢 낮음 (Low): #4CAF50
- 완료 체크박스 기능

**b) 📅 이번 주 일정 (Weekly Schedule)**
- Mon-Fri 요일별 시간 슬롯
- 10:00-18:00 시간대 표시
- 현재 시간 하이라이트

**c) 🚀 프로젝트 진행률 (Project Progress)**
- 6개 프로젝트 진행 상황
- 진행률 바 (0-100%)
- 예산 정보 표시
- 색상: 파랑(진행중), 초록(완료), 주황(보류)

**d) 💰 매출 요약 (Sales Summary)**
- 주요 KPI 카드 (총 매출, 월 평균, 목표 달성률)
- 월별 비교 (전월 대비)
- 카테고리별 내역

#### 🌓 다크/라이트 모드
- localStorage에 선택 저장
- 토글 버튼 (🌙/☀️)
- CSS 변수로 전체 테마 변경

#### 📅 동적 날짜 배지
- 현재 날짜 표시
- 형식: "2026년 5월 6일 (화)"

---

### 2. Chart (chart.html)

#### 📈 차트 기술
- **기술**: Pure HTML5 Canvas API (외부 라이브러리 없음)
- **데이터 소스**: 매출데이터.csv (30개 거래)
- **기간**: 2026-01-05 ~ 2026-02-10

#### 차트 종류

**a) 월별 매출 추이 (Line Chart)**
- 파란색: 1월 (January)
- 초록색: 2월 (February)
- 일일 거래액 표시
- 마우스 호버 시 구체적 숫자 표시

**b) 제품별 비교 (Horizontal Bar Chart)**
- Electronics (파랑): 전자제품
- Lifestyle (초록): 생활용품
- 가로 막대로 금액 비교

#### 🎨 시각화 기능
- 부드러운 애니메이션 진입
- 마우스 호버 효과
- 숫자 포맷팅 (쉼표 추가: 1,234,567)
- 반응형 캔버스 (창 크기에 맞춤)

---

### 3. Report (report.html)

#### 📋 분석 대상
웹사이트: https://www.subtrac.kr/  
SubTrackr - 구독료 추적 서비스

#### 🔍 분석 섹션 (8개)

1. **서비스 개요**: KPI 카드 4개 (사용자, 구독, 절감액, 평점)
2. **사이트 구조**: 8단계 네비게이션 경로 분석
3. **디자인 분석**: 색상, 타이포그래피, 레이아웃 패턴
4. **주요 기능**: 9개 핵심 기능 설명
5. **잘한 점**: 7개 강점 분석
6. **개선점**: 7개 개선 영역
7. **종합 평가**: 별점 4.0/5.0

#### 🎨 설계
- 다크 테마 (배경: #141C2E)
- 카드 레이아웃으로 가독성 향상
- Sticky 네비게이션 바

---

## 💾 데이터 소스

### 김비서-데이터/ 폴더 내용

**매출데이터.csv** (주요)
```
날짜,금액,카테고리,상태
2026-01-05,250000,Electronics,완료
2026-01-08,180000,Lifestyle,완료
... (30개 거래)
```

**프로젝트현황.csv**
```
프로젝트명,진행률,예산,카테고리
신규 앱 개발,85,15000000,개발
마케팅 캠페인,60,5000000,마케팅
... (6개 프로젝트)
```

**업무목록.csv**
```
업무,우선순위,담당자,상태
분기 보고서 작성,높음,김비서,진행중
고객 미팅 준비,중간,영업팀,대기
... (할 일 리스트)
```

---

## 🔧 기술 스택

| 항목 | 기술 |
|------|------|
| 마크업 | HTML5 |
| 스타일 | CSS3 (CSS Variables, Grid, Flexbox) |
| 상호작용 | Vanilla JavaScript (외부 라이브러리 없음) |
| 차트 | Canvas API |
| 상태 관리 | localStorage (다크모드 선택) |
| 배포 | Vercel (자동 재배포) |
| 버전관리 | Git + GitHub |

---

## 🚀 배포 설정

### GitHub 저장소
```
URL: https://github.com/hoikyung/secretary-test
브랜치: main
공개: Public
```

### Vercel 배포
```
배포 URL: https://secretary-test-five.vercel.app/
자동 배포: main 브랜치 push 시 자동 재배포
설정: vercel.json (최소 정적 사이트 설정)
```

### vercel.json 설정
```json
{
  "version": 2,
  "cleanUrls": false,
  "trailingSlash": false
}
```

---

## 🔐 환경변수

### .env 파일
```
# GitHub Personal Access Token
GITHUB_TOKEN=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
```

⚠️ **보안**: .gitignore에 자동으로 무시됨 (커밋되지 않음)

---

## 📝 CSS 커스터마이징 팁

### 다크 모드 색상 변경
dashboard.html의 `:root` 섹션:
```css
:root {
  --bg-primary: #0F1419;      /* 배경색 */
  --bg-card: rgba(255,255,255,0.08);  /* 카드 배경 */
  --text-primary: #FFFFFF;     /* 텍스트색 */
  --accent: #f5a623;           /* 강조색 */
}
```

### 애니메이션 속도 조정
```css
transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
/* 0.3s → 0.5s로 변경하면 더 느려짐 */
```

---

## 🔄 향후 확장 방법

### 새로운 페이지 추가 시
1. HTML 파일 생성
2. 동일한 네비게이션 바 복사
3. 데이터 소스 준비 (CSV/JSON)
4. Git에 커밋 후 푸시
5. Vercel이 자동 재배포

### 데이터 업데이트
- CSV 파일 수정 → JavaScript에서 자동 읽음
- 페이지 새로고침하면 반영됨

### 스타일 통일
- CSS 변수 사용 (`:root`에 정의)
- 모든 페이지가 동일한 색상 시스템 사용
- 글래스모피즘 스타일 일관성 유지

---

## 📞 빠른 참조

| 작업 | 명령어 |
|------|--------|
| 로컬 변경사항 확인 | `git status` |
| 파일 추가 및 커밋 | `git add [파일]; git commit -m "메시지"` |
| GitHub에 푸시 | `git push origin main` |
| Git 로그 확인 | `git log --oneline` |

---

## 📌 주의사항

✅ **할 것:**
- 데이터 변경 후 GitHub에 푸시하기
- CSS 수정 시 라이트/다크 모드 모두 테스트
- 새로운 기능 추가 후 모든 페이지에서 네비게이션 테스트

❌ **하지 말 것:**
- `.env` 파일을 Git에 커밋하기
- CSS 변수 이름 변경 (전체 페이지에 영향)
- HTML 구조 대폭 변경 (JavaScript 호환성 확인 필수)

---

## 🎓 나중에 요청할 때 참고사항

이 문서를 읽고 다음과 같이 요청하면 빠르게 진행할 수 있습니다:

**예시 요청 1:** "대시보드에 새로운 '📧 메일함' 섹션을 추가해줘"  
→ 4개 섹션 구조를 참고하여 즉시 구현 가능

**예시 요청 2:** "report.html의 색상을 라이트 모드처럼 밝게 변경해줘"  
→ CSS 섹션의 색상 팔레트를 참고하여 구현

**예시 요청 3:** "새로운 차트 페이지를 만들어줘 (데이터: [파일명])"  
→ chart.html의 Canvas API 구현을 참고하여 확장

---

**최종 업데이트:** 2026-05-06  
**담당자:** hoikyung02@gmail.com  
**상태:** ✅ 배포 완료
