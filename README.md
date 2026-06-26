<div align="center">

# 📊 정보자원 통합 만족도 — 일일 보고서 자동 생성기

**구글 폼 응답 CSV 한 장이면, 매일 똑같은 디자인의 인포그래픽 + 발표 PPT가 자동으로.**

경기도교육청 「정보자원 통합 성과 및 시스템 이전·통합 만족도 조사」 전용
일일 보고 자동화 도구 — *형식은 고정, 데이터만 매일 교체.*

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?logo=python&logoColor=white)
![Node](https://img.shields.io/badge/Node.js-16+-339933?logo=node.js&logoColor=white)
![pptxgenjs](https://img.shields.io/badge/PPT-pptxgenjs-E08A1E)
![License](https://img.shields.io/badge/License-MIT-13294B)

<img src="docs/preview.png" alt="보고서 미리보기" width="820">

</div>

---

## ✨ 무엇을 만드나요

CSV를 넣으면 동일한 형식의 산출물 2종이 나옵니다.

| 산출물 | 설명 |
| :-- | :-- |
| 📄 **`index.html`** | 화면용 인포그래픽. 웹서버에 그대로 올리면 바로 서비스됩니다. |
| 📑 **`report.pptx`** | 발표용 8슬라이드 PPT. 그대로 보고에 사용 가능합니다. |

> 디자인: 네이비 `#13294B` · 틸 `#0AA6A0` · 앰버 `#E08A1E` / 8개 섹션 고정 구성.

---

## 🚀 빠른 시작

```bash
# 0) 최초 1회 — Node 의존성 설치 (Python 3는 표준 라이브러리만 사용)
npm install

# 1) 구글 폼 → 응답 → ⋮ → 응답 다운로드(.csv)
# 2) 한 줄 실행
bash run_daily.sh sample/sample_responses.csv
```

→ `output/index.html`, `output/report.pptx` 완성 ✔

개별 실행도 가능합니다.

```bash
python3 generate.py <응답.csv> output                         # → index.html + report_data.json
node     build_ppt.js output/report_data.json output/report.pptx   # → report.pptx
```

---

## 🗂 저장소 구성

```
.
├─ generate.py                # CSV 분석 → index.html + report_data.json
├─ build_ppt.js               # report_data.json → report.pptx (8슬라이드)
├─ run_daily.sh               # 위 두 단계 원클릭 실행
├─ package.json               # Node 의존성 (pptxgenjs)
├─ docs/
│  └─ preview.png             # 산출물 미리보기
└─ sample/
   └─ sample_responses.csv    # 형식 기준 예시 데이터
```

---

## 📈 보고서 8개 섹션

1. **핵심 지표 요약** — 응답수 · 인지율 · 전반 만족도 · 전환 인지율
2. **응답자 구성** — 기관 / 직군 / 직급 분포 (+ 표본 대표성 점검)
3. **전환·통합 만족도** — TRN / MSA / CMS 영역별 (소표본 자동 표기)
4. **기대효과 · 우선순위** — 복수선택 집계 + 우선순위 ‘상’ 비율
5. **현장 자유의견** — 형식적 응답 자동 제외 후 발췌
6. **관점별 종합 진단** — 사업관리 · 기술 · 비즈니스
7. **결론 재점검 · 리스크** — 수치 과잉해석 경계 / 빠진 데이터 점검

## ⚙️ 자동으로 계산되는 값

집계일·응답기간·응답수(타임스탬프 기준) · 기관/직군/직급 분포 · 사업·전환 인지율 ·
전반 만족도(평균·인원·매우만족/만족/불만족) · 기대효과 선택수 · 우선순위 ‘상’ 비율 ·
최우선 기대효과 · TRN/MSA/CMS 만족도(평균·인원, **10명 미만은 ‘참고치’ 자동 표기**) ·
자유의견 발췌 · 관점별 진단/리스크 문구의 수치까지 — 전부 데이터에서 재계산됩니다.

---

## ⚠️ 전제 / 주의사항

- **CSV 열 구조(32열)가 동일해야 합니다.** 설문 문항을 추가·삭제하면
  `generate.py` 상단의 열 번호 매핑을 그에 맞게 수정하세요.
- 척도 표기 기준 — 전반 만족도 `매우 만족 / 만족 / 보통 / 불만족 / 매우 불만족`, 영역별 `1~5`.
- 글꼴은 외부 CDN(Pretendard)을 사용 → **외부망에서만** 의도한 글꼴로 표시됩니다.
  폐쇄망 서비스 시 폰트 내장본이 필요합니다.

## 🔐 개인정보 / 보안

`sample/sample_responses.csv`는 **실제 설문 응답**입니다. 직접 식별자(이름·이메일·연락처)는
없지만 기관·직급·자유의견이 포함된 내부 자료입니다.

- **공개(public) 저장소**로 운영한다면 이 파일을 커밋하지 마세요
  → `.gitignore`의 해당 줄을 활성화하거나 합성(가짜) 샘플로 교체.
- 실데이터를 보관해야 한다면 **비공개(private) 저장소**를 사용하세요.

---

## 📦 요구 사항

- Python ≥ 3.8 (표준 라이브러리만 사용)
- Node.js ≥ 16 + `pptxgenjs` (`npm install`)

## 📄 라이선스

MIT — 자유롭게 사용·수정하세요.

<div align="center">

*형식 버전 **v1** · 2026-06-25 기준 · 경기도교육청 교육정보기록원*

</div>
