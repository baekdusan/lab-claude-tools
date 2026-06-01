# lab-claude-tools

연구실에서 쓰는 Claude Code 플러그인 모음 (마켓플레이스).

수록 플러그인:
- **research-toolkit** — 연구 워크플로우 도구 모음 (스킬 2종)
  - `paper-summary` — 학술 논문을 CPR 프레임으로 요약
  - `make-slides` — 기존 .pptx 템플릿 양식을 유지하며 발표자료 생성

## 설치

Claude Code에서:

```
/plugin marketplace add baekdusan/lab-claude-tools
/plugin install research-toolkit@lab-claude-tools
```

업데이트:

```
/plugin marketplace update lab-claude-tools
```

---

## 스킬 1 — paper-summary

학술 논문을 **CPR(Context-Problem-Response) 프레임**으로 요약합니다.

*The Craft of Research* (Booth, Colomb, Williams)의 수사적 논증 구조를 그대로 따라, 단순 섹션 나열이 아니라 저자의 논증을 복원하는 방식으로 정리합니다.

### 출력 구조

- **한 줄 요약**
- **Context** — 받아들여진 사실 + 의존하는 선행 연구
- **Problem** — Condition(무엇이 불완전한가) + Cost(So what? — 안 풀면 누가 어떤 손해를 보는가)
- **Response** — Claim → How(방법) → Evidence(근거)
- **한계 및 열린 질문** — 저자 인정 vs 리뷰어 의문 구분
- **우리 연구와의 관련성**

### 입력 형태

- 로컬 PDF 파일 경로 (`~/Downloads/paper.pdf`)
- arXiv URL (`https://arxiv.org/abs/2401.12345`)
- 학회/저널 URL (ACL Anthology, OpenReview, IEEE 등)
- DOI 또는 제목

### 사용 예

```
이 논문 요약해줘: https://arxiv.org/abs/2401.12345
```

---

## 스킬 2 — make-slides

**`.pptx` 템플릿의 양식(레이아웃·폰트·색·로고)을 그대로 유지**하면서, 텍스트·마크다운·논문 요약 내용을 채워 발표용 `.pptx`를 생성합니다. [python-pptx](https://python-pptx.readthedocs.io/)로 템플릿을 열어 레이아웃 플레이스홀더에 내용만 넣으므로 마스터 슬라이드가 보존됩니다.

**연구실 공용 템플릿이 번들되어 있어**(`skills/make-slides/assets/template.pptx`), 따로 지정하지 않아도 누구나 같은 양식으로 발표자료가 나옵니다. 다른 템플릿을 쓰고 싶으면 `.pptx` 경로를 주면 대체됩니다.

### 동작 흐름

1. **템플릿 스캔** — `scripts/inspect_template.py`로 레이아웃·플레이스홀더 인덱스 파악
2. **아웃라인 합의** — 청중·시간·목적에 맞춰 슬라이드 구조를 먼저 텍스트로 제시
3. **빌드** — 기존 슬라이드는 비우고(레이아웃만 차용) 내용을 새로 채워 `.pptx` 생성
4. **검증 안내**

`paper-summary`의 CPR 요약을 그대로 발표 슬라이드로 매핑하는 표를 내장하고 있어, **논문 → CPR 요약 → 발표자료** 워크플로우로 이어집니다.

### 사용 예

```
이 내용으로 발표자료 만들어줘            # 번들 공용 템플릿 사용
이 논문 발표자료로 만들어줘: paper.pdf   # 논문 → CPR → 슬라이드
이 템플릿으로 만들어줘: ./other.pptx     # 다른 템플릿으로 대체
```

### 의존성

- Python 3
- `python-pptx` (`pip3 install python-pptx`)

---

## 기여

연구실 동료가 개선 제안이 있다면 PR 또는 이슈로 알려주세요.
