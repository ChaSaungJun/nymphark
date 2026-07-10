# Handoff: NymphArk Welcome Banner

## Overview
"NymphArk"는 모바일 게임 **'승리의 여신: 니케 (Goddess of Victory: NIKKE)'** 팬사이트입니다. 이 핸드오프 패키지는 사이트 상단 히어로 영역에 배치될 **환영 배너(Welcome Banner)** 디자인을 담고 있습니다.

디자인 탐색 결과 **이미지 없이 CSS/SVG로만 완결되는 타이포그래피 중심 배너 방향**이 최종 선택되었습니다. 이 방향으로 3가지 변주(Classic Emblem / Calligraphic Script / Solid Gold Monogram)가 준비되어 있으며, 개발자는 이 중 하나(또는 조합)를 선택해 구현하시면 됩니다.

## About the Design Files
이 패키지에 포함된 HTML/CSS 파일은 **HTML로 제작된 디자인 레퍼런스**입니다 — 프로덕션 코드로 그대로 복사해서 배포할 대상이 아니라, 최종 룩앤필과 행동을 보여주는 프로토타입입니다.

개발자의 작업은 이 HTML 디자인을 **타겟 코드베이스의 기존 환경**(React, Vue, Next.js, Nuxt, SwiftUI, Flutter 등)에서 그곳의 관례와 라이브러리를 활용해 재현하는 것입니다. 아직 코드베이스가 없다면 프로젝트에 가장 적합한 프레임워크를 선택해 구현하시면 됩니다.

## Fidelity
**High-fidelity (하이파이).** 색상 · 타이포 · 여백 · 장식 위치가 모두 최종값입니다. 개발자는 아래 스펙을 그대로 재현하되, 목표 코드베이스의 컴포넌트/토큰 시스템에 맞춰 매핑해 구현해 주세요.

---

## Screens / Views

배너는 단일 뷰이며, **3가지 시각적 변주**가 있습니다. 프로젝트 매니저와 상의 후 하나를 선택해 구현하세요.

### 공통 스펙 (모든 변주 공통)

- **컨테이너 비율:** `16:9` (모바일 대응 시 최소 높이 유지 또는 재구성 필요)
- **기준 사이즈:** 1920 × 1080 (참고용; 실제 배포 시 100% 폭, `aspect-ratio: 16/9`)
- **border-radius:** `6px`
- **box-shadow:**
  ```
  0 30px 80px -30px rgba(0, 0, 0, 0.8),
  0 0 0 1px rgba(201, 161, 92, 0.15),
  inset 0 0 0 1px rgba(244, 232, 212, 0.04)
  ```

- **공통 배경 (banner-base):**
  ```css
  background:
    radial-gradient(ellipse at 30% 35%, rgba(155, 57, 72, 0.32) 0%, transparent 55%),
    radial-gradient(ellipse at 78% 68%, rgba(45, 114, 120, 0.24) 0%, transparent 52%),
    radial-gradient(ellipse at 50% 100%, rgba(201, 161, 92, 0.14) 0%, transparent 60%),
    linear-gradient(135deg, #2a1418 0%, #1a0d10 55%, #0f2225 100%);
  ```

- **공통 오버레이 레이어:**
  1. `.grain` — SVG fractalNoise 필터로 만든 그레인 텍스처. `mix-blend-mode: overlay`, `opacity: 0.3`. 파일 참조 (index.html 내 인라인 SVG data URL).
  2. `.warm-glow` — `radial-gradient(ellipse at 50% 45%, rgba(224, 196, 138, 0.10) 0%, transparent 55%)`
  3. `.particle` — 골드 파티클 6~8개, 위치 랜덤. 각 파티클: `background: #c9a15c; border-radius: 50%; box-shadow: 0 0 8px rgba(201, 161, 92, 0.8); opacity: 0.35~0.5; size: 2~3px`

- **공통 태그라인:**
  - 국문: "여왕을 꿰뚫는 검은 총알이 되어라." (사이트 방문 상시 노출용 서브 태그라인)
  - 영문: "Be the black bullet that pierces the queen."
  - 스타일: 이탤릭 세리프, 크림색 (`rgba(244, 232, 212, 0.85~0.9)`), 영문은 골드 (`rgba(201, 161, 92, 0.65~0.7)`)

- **"어서오세요" 문구는 사용하지 않습니다.** (사용자 요청)

---

### Variation 01 — Classic Emblem
클래식 로마 문장 감성. 좌우 대칭 · Cinzel 대문자 · 월계관 · 플러런.

**Layout (중앙 정렬 · 좌우 대칭):**

```
┌─ [코너 SVG]  ─────────────────  [코너 SVG] ─┐
│                                              │
│         [월계관] · N · A · [월계관]           │
│                                              │
│              N Y M P H A R K                 │  ← Cinzel 600, 132px
│           a sanctuary of victory             │  ← Cormorant Italic 22px
│                                              │
│         ────────── ❦ ──────────              │  ← Fleuron 디바이더
│                                              │
│      여왕을 꿰뚫는 검은 총알이 되어라.        │  ← 국문 태그라인
│  — Be the black bullet that pierces...       │  ← 영문 태그라인
│                                              │
└─ [코너 SVG]  ─────────────────  [코너 SVG] ─┘
```

**Components:**

| 요소 | 폰트 | 크기 | 색상 |
|---|---|---|---|
| Emblem top | Cinzel 400 | 11~14px, letter-spacing 0.5em | `#c9a15c` |
| Brand | **Cinzel 600** | `clamp(52px, 9vw, 132px)`, letter-spacing 0.02em | 그라디언트 (아래) |
| Brand sub italic | Cormorant Garamond Italic 400 | 16~22px, letter-spacing 0.08em | `rgba(244, 232, 212, 0.55)` |
| Divider | — | Fleuron `❦` 14~18px | `#c9a15c` |
| Tagline KR | Cormorant Garamond Italic 400 / Noto Serif KR | 16~23px | `rgba(244, 232, 212, 0.9)` |
| Tagline EN | Cormorant Garamond Italic 400 | 0.68em of parent | `rgba(201, 161, 92, 0.7)` |

**Brand 그라디언트 (Cinzel wordmark):**
```css
background: linear-gradient(180deg, #f4e8d4 0%, #e0c48a 45%, #a88547 100%);
-webkit-background-clip: text;
color: transparent;
text-shadow: 0 8px 40px rgba(201, 161, 92, 0.2);
```

**월계관 SVG (좌우 미러):** `index.html` `.laurel` SVG 그대로 사용. 크기 `clamp(28px, 3.5vw, 48px)`. 색상 `#c9a15c`.

**코너 장식 SVG:** 4개 코너에 배치. 크기 `clamp(48px, 5.5vw, 78px)`. 위치 상하좌우 각각 3.5%/2.5%. TR·BL·BR은 각각 scaleX(-1) / scaleY(-1) / scale(-1,-1)로 미러링.

---

### Variation 02 — Calligraphic Script
필기체(캘리그래피) 브랜드 · 우아한 손글씨 감성 · 유기적 스와시.

**Layout (중앙 정렬 · 스크립트 강조):**

```
┌────  [swash SVG 좌상단]  ─────────────────┐
│                                            │
│        ────  N Y M P H  A R K  ────       │  ← eyebrow (Cinzel)
│                                            │
│  [flourish]  NymphArk  [flourish]         │  ← Pinyon Script 180px
│                                            │
│         — Goddess of Victory · Nikke —     │
│                                            │
│      여왕을 꿰뚫는 검은 총알이 되어라        │
│    Be the black bullet that pierces...     │
│                                            │
└─────────────  [swash SVG 우하단]  ────────┘
```

**Components:**

| 요소 | 폰트 | 크기 | 색상 |
|---|---|---|---|
| Eyebrow | Cinzel 400 | 10~13px, letter-spacing 0.55em | `rgba(201, 161, 92, 0.75)` |
| **Brand script** | **Pinyon Script (Italianno 폴백)** | `clamp(72px, 12vw, 180px)` | 그라디언트 (아래) |
| Brand sub | Cinzel 400 | 11~14px, letter-spacing 0.6em | `#e8d9bd`, opacity 0.75 |
| Tagline KR | Cormorant Italic + Noto Serif KR | 15~22px | `rgba(244, 232, 212, 0.85)` |
| Tagline EN | Cormorant Italic | 0.7em of parent | `rgba(201, 161, 92, 0.65)` |

**Brand script 그라디언트:**
```css
background: linear-gradient(180deg, #f0d9a0 0%, #c9a15c 55%, #8b6b38 100%);
-webkit-background-clip: text;
color: transparent;
text-shadow: 0 6px 30px rgba(201, 161, 92, 0.22);
```

**Flourish SVG (양옆):** 스크립트 좌우에 절대 배치, `top:50%; transform: translateY(-50%);` 우측은 `scaleX(-1)`. 폭 `clamp(50px, 8vw, 120px)`. 색상 `#c9a15c`, opacity 0.55.

**Swash SVG (좌상단·우하단):** 곡선 스와시, 폭 `clamp(120px, 18vw, 280px)`, opacity 0.35. 우하단은 rotate(180deg).

---

### Variation 03 — Solid Gold Monogram
아르데코 스타일 · 좌측 N·A 원형 앰블럼 · **솔리드 골드 폼트(그라디언트 없음)**.

**Layout (좌우 2단 · 좌측 앰블럼 + 우측 텍스트):**

```
┌── [deco frame 이중 골드 라인]  ────────────────┐
│  ◇ (top diamond)                                │
│                                                 │
│    ┌─────────┐                                  │
│    │  [★]    │      N Y M P H A R K            │  ← Cinzel Deco 700 solid gold
│    │ [월계]  │      Nymph & Ark                 │  ← Cormorant Italic
│    │  N · A  │      ── ◆ ── Goddess of Victory  │
│    │ [리본]  │                                  │
│    └─────────┘      여왕을 꿰뚫는 검은 총알...  │
│                     — Be the black bullet...    │
│                                                 │
│  ◇ (bottom diamond)                             │
└─────────────────────────────────────────────────┘
```

**Components:**

| 요소 | 폰트 | 크기 | 색상 |
|---|---|---|---|
| **Brand line** | **Cinzel Decorative 700** (Cinzel 폴백) | `clamp(38px, 6.5vw, 96px)`, letter-spacing 0.04em | **`#d9b46e` solid** |
| Brand italic | Cormorant Garamond Italic 400 | 15~22px, letter-spacing 0.15em | `rgba(244, 232, 212, 0.6)` |
| Type divider (EST) | Cinzel 400 | 9~11px, letter-spacing 0.4em | `rgba(201, 161, 92, 0.7)` |
| Tagline KR | Cormorant Italic + Noto Serif KR | 15~22px | `rgba(244, 232, 212, 0.9)` |
| Tagline EN | Cormorant Italic | 0.68em of parent | `rgba(201, 161, 92, 0.65)` |

**Solid gold (그라디언트 없음) 처리:**
```css
color: #d9b46e;
text-shadow:
  0 2px 0 rgba(139, 107, 56, 0.4),   /* 두께감 */
  0 4px 30px rgba(201, 161, 92, 0.25); /* 부드러운 발광 */
```

**Monogram SVG (원형 앰블럼, 좌측 배치):** `index.html` 내 200×200 viewBox SVG 그대로 사용. 크기 `clamp(120px, 18vw, 220px)`. 구성:
- 외곽 이중 원 (`#c9a15c`, stroke 1.2 + 0.6)
- 4방위 diamond(rotate 45), 대각선 tick 4개
- 좌우 월계관 (ellipse 5개씩, rotate로 흩뿌림, opacity 0.65)
- 중앙 대문자 "N" + "A" (Cinzel Decorative 700, `#d9b46e`)
- 상단 5각 별
- 하단 리본 (사다리꼴 path, `#a88547`, 텍스트 "EST · MMXXVI")

**Deco frame (외곽 이중 골드 프레임):**
```css
.deco-frame {
  position: absolute; inset: 3.5%;
  border: 1px solid rgba(201, 161, 92, 0.28);
}
.deco-frame::before, .deco-frame::after {
  content: ''; position: absolute; left: 50%;
  width: 24px; height: 24px;
  transform: translateX(-50%) rotate(45deg);
  background: #1a0d10;
  border: 1px solid rgba(201, 161, 92, 0.5);
}
.deco-frame::before { top: -12px; }
.deco-frame::after { bottom: -12px; }
.deco-frame-inner {
  position: absolute; inset: 3.5%; margin: 8px;
  border: 1px solid rgba(201, 161, 92, 0.14);
}
```

---

## Interactions & Behavior

배너는 **정적** 요소입니다. 클릭 핸들러나 상태 전이가 없습니다.

- **Hover 상태:** 없음. 배너는 히어로 표시용.
- **애니메이션:** 없음 (선택 사항 — 파티클에 아주 은은한 float 애니메이션 추가 가능. 3~5초 주기 sine wave, `translateY(±4px)`, opacity 0.3↔0.6)
- **로딩 상태:** 웹폰트 로드 전에는 시스템 세리프로 폴백. `font-display: swap` 사용.
- **반응형:**
  - Desktop / Tablet: `aspect-ratio: 16 / 9` 유지, 폭 100%
  - Mobile (≤ 780px): 텍스트 크기는 `clamp()`로 자동 축소됨. V3는 좌측 앰블럼 + 우측 텍스트 → 세로 스택으로 재배치 (아래 CSS 참고):
    ```css
    @media (max-width: 780px) {
      .banner-v3 .lockup { flex-direction: column; gap: 20px; }
      .banner-v3 .type-block { text-align: center; }
      .banner-v3 .type-divider { justify-content: center; }
    }
    ```

## State Management
불필요 — 상태 없음.

---

## Design Tokens

### Colors

| Token | Hex | 사용처 |
|---|---|---|
| `--burgundy-950` | `#1a0d10` | 배경 최심 |
| `--burgundy-900` | `#2a1418` | 배경 |
| `--burgundy-800` | `#3d1a20` | 배경 하이라이트 |
| `--wine` | `#9b3948` | 액센트 (radial gradient) |
| `--teal-900` | `#0f2a2e` | 배경 티얼 딥 |
| `--teal-500` | `#2d7278` | 티얼 억양 |
| `--teal-400` | `#4a9ba1` | 티얼 하이라이트 |
| `--cream` | `#f4e8d4` | 메인 텍스트 |
| `--cream-soft` | `#e8d9bd` | 서브 텍스트 |
| `--gold` | `#c9a15c` | 액센트 골드 (라인, 코너) |
| `--gold-bright` | `#e0c48a` | 그라디언트 하이라이트 |
| `--gold-deep` | `#a88547` | 그라디언트 딥 |
| **`#d9b46e`** | `#d9b46e` | **V3 solid gold 브랜드 색** |

### Typography

| 폰트 | 용도 |
|---|---|
| **Cinzel** (400, 500, 600, 700) | 대문자 워드마크 (V1), eyebrow, 로마 라벨 |
| **Cinzel Decorative** (400, 700, 900) | V3 아르데코 브랜드 워드마크 |
| **Cormorant Garamond** (400, 500, 600, italic) | 이탤릭 서브 헤더, 태그라인 |
| **Pinyon Script** | V2 캘리그래피 브랜드 워드마크 |
| **Italianno** | V2 폴백 스크립트 |
| **Marcellus** | 예비 로마 세리프 (필요 시) |
| **Noto Serif KR** (300~700) | 국문 태그라인 |
| **Gowun Batang** (400, 700) | 국문 예비 세리프 |

모두 **Google Fonts**에서 로드:
```html
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400;1,500;1,600&family=Cinzel:wght@400;500;600;700&family=Cinzel+Decorative:wght@400;700;900&family=Marcellus&family=Italianno&family=Pinyon+Script&family=Noto+Serif+KR:wght@300;400;500;600;700&family=Gowun+Batang:wght@400;700&display=swap" rel="stylesheet">
```

### Spacing / Radius / Shadow

- **Border radius (배너):** `6px`
- **Container padding:** `5~8%` (반응형)
- **Corner ornament offset:** `3.5% / 2.5%` (top/side)
- **Main box shadow:** `0 30px 80px -30px rgba(0,0,0,0.8), 0 0 0 1px rgba(201,161,92,0.15), inset 0 0 0 1px rgba(244,232,212,0.04)`

---

## Assets

이 디자인은 **외부 이미지 자산 없이** CSS + 인라인 SVG만으로 구성됩니다. 별도 이미지 파일 다운로드 불필요.

인라인 SVG 요소 목록:
- `.laurel` (V1): 월계관 브랜치 (48×48 viewBox)
- 코너 장식 (V1): 곡선 + 잎사귀 (80×80 viewBox)
- `.flourish-left/right` (V2): 필기체 좌우 장식 (120×80 viewBox)
- `.swash-tl/br` (V2): 배경 스와시 (280×200 viewBox)
- `.monogram svg` (V3): 원형 앰블럼 (200×200 viewBox) — 가장 복잡한 SVG. index.html에서 그대로 복사.
- `.grain`: data URL SVG (fractalNoise 필터로 만든 노이즈 텍스처)

**PNG export (Optional):**
프로토타입은 각 배너를 1920×1080 PNG로 브라우저에서 다운로드하는 기능을 포함합니다 (`html2canvas` 사용). 실제 사이트 구현 시에는 불필요하지만, 마케팅용 정적 이미지가 필요하다면 프로토타입 페이지에서 미리 추출해 두면 됩니다.

---

## Implementation Notes for the Developer

1. **컴포넌트 구조 제안:**
   - `<WelcomeBanner variant="classic" | "script" | "monogram" />` 형태로 variant prop 하나로 3개 스타일 스위칭
   - 태그라인은 i18n 대응 필요 (국문/영문 분리)

2. **웹폰트 로딩 최적화:**
   - `font-display: swap` 필수
   - LCP에 영향 있으므로 위 두 폰트만 preload 고려: **Cinzel 600** (V1), **Pinyon Script 400** (V2)
   - 나머지는 lazy 로드 가능

3. **접근성:**
   - 배너는 장식용에 가까우므로 텍스트 콘텐츠는 실제 HTML 텍스트로 유지 (스크린 리더 접근)
   - `aria-label` 이나 landmark role은 `<header>` 요소로 감싸 처리
   - 색상 대비: 크림 텍스트 `#f4e8d4` on 버간디 배경 `#1a0d10` = 명암비 15:1 이상 ✅

4. **성능:**
   - SVG 인라인 그대로 사용 (HTTP 요청 절약)
   - 그레인 텍스처는 data URL SVG — 그대로 유지 권장
   - `mix-blend-mode`, `backdrop-filter`, `text-shadow`는 저사양 모바일에서 부하 있음. 필요시 미디어쿼리로 단순화

5. **개발 착수 시 살펴볼 것:**
   - 사이트 전체의 브랜드 컬러 토큰 시스템이 있다면, 위 색상 팔레트를 프로젝트 CSS 변수/토큰에 매핑
   - 히어로 영역 위/아래 페이지 여백과 조화 확인
   - 페이지 전체가 다크 모드 기반인지 확인 (배너는 다크 배경 전제)

---

## Files

이 폴더에 포함된 파일:
- `README.md` — 이 문서
- `banner_prototype.html` — 3개 변주가 모두 담긴 원본 프로토타입 (프로젝트 루트 `index.html` 사본)

프로토타입에서 브라우저로 열어 확인 후, 각 variation의 `<section class="option">` 블록 내부의 `.banner` 마크업 + CSS를 참고해 구현하세요.
