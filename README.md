# 🔮 오늘의 운세

매일 카드를 뽑아 **연애운 · 금전운 · 건강운**을 확인하는 모바일 웹앱입니다.

🌐 **[지금 운세 보기 →](https://songwookun.github.io/today-fortune/)**

---

## 주요 기능

| 기능 | 설명 |
|------|------|
| 🃏 카드 뽑기 | 3장의 카드를 뽑아 연애/금전/건강 운세 확인 (플립 애니메이션) |
| 🔒 하루 고정 결론 | 같은 날 여러 번 접속해도 핵심 메시지는 동일 (PRNG 기반) |
| 🔄 다시 뽑기 | 세부 문장과 행동 추천만 살짝 변동되어 재미 유지 |
| 📤 결과 공유 | 클립보드 링크 복사, 받는 사람도 동일 결과 재현 |
| 🃏 카드 도감 | 12종 아키타입 카드와 카테고리별 해석 열람 |
| 📋 심화 리포트 | 전체 세부 해석, 행운 요소(색/숫자/방향/시간), 종합 분석 |
| 💡 맞춤 추천 | 카드 결과 기반으로 추천 콘텐츠가 동적으로 변경 |

## 기술 스택

- **순수 HTML / CSS / JS** — 빌드 도구 없음, 정적 파일 3개로 동작
- **모바일 퍼스트** 반응형 디자인
- **CSS 3D 카드 플립** 애니메이션
- **Seeded PRNG** (Cyrb53 해시 + Mulberry32) — 서버 없이 일관된 결과
- **localStorage** 기반 상태 관리 (기기별 고유 ID)
- **base64url** 공유 링크 인코딩/디코딩

## 결과 결정 규칙

```
seed = hash(오늘 날짜 + deviceId)
       ↓
  PRNG 생성
       ↓
  연애/금전/건강 각각 base_result_id 결정 (당일 고정)
       ↓
  coreMessage → 고정
  details / do / dont → drawCount에 따라 선택 인덱스만 변동
```

- 날짜가 바뀌면 자동으로 새 결과 생성
- 공유 링크(`?share=`)가 있으면 localStorage보다 우선 적용

## 로컬 실행

```bash
# Mac / Linux
python3 -m http.server 8000

# Windows
python -m http.server 8000
```

브라우저에서 `http://localhost:8000` 접속

## 배포 (GitHub Pages)

이 레포지토리는 GitHub Pages로 자동 배포됩니다.

**Settings → Pages → Source**: `main` 브랜치, `/ (root)`

## 프로젝트 구조

```
├── index.html   # 메인 HTML (SEO, OG 메타, 접근성)
├── style.css    # 모바일 퍼스트 CSS, 카드 애니메이션
├── app.js       # PRNG, 운세 데이터 36종, 상태관리, 공유 로직
└── README.md
```

## 수익화 로드맵

| 단계 | 상태 | 내용 |
|------|------|------|
| 1단계 | 슬롯 확보 완료 | Google AdSense 광고 — 승인 후 적용 |
| 2단계 | 시스템 구현 완료 | 제휴 콘텐츠 — 카드 결과 기반 동적 추천, 실제 링크 연결 예정 |
| 3단계 | 무료 제공 중 | 심화 리포트 — 향후 프리미엄 콘텐츠 확장 예정 |

## 검색 노출 (SEO)

- `index.html`에 title / description / OG 메타 / canonical 포함
- Google Search Console: `<meta name="google-site-verification">` 주석 해제 후 값 입력
- 네이버 서치어드바이저: `<meta name="naver-site-verification">` 주석 해제 후 값 입력
- `robots.txt`, `sitemap.xml`은 필요 시 루트에 추가

## 라이선스

MIT
