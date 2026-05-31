# paper-cpr-summary

학술 논문을 **CPR(Context-Problem-Response) 프레임**으로 요약해주는 Claude Code 스킬입니다.

*The Craft of Research* (Booth, Colomb, Williams)의 수사적 논증 구조를 그대로 따라, 단순 섹션 나열이 아니라 저자의 논증을 복원하는 방식으로 정리합니다.

## 출력 구조

- **한 줄 요약**
- **Context** — 받아들여진 사실 + 의존하는 선행 연구
- **Problem**
  - Condition (무엇이 불완전한가)
  - Cost (So what? — 안 풀면 누가 어떤 손해를 보는가)
- **Response** — Claim → How (방법) → Evidence (근거)
- **한계 및 열린 질문** — 저자 인정 vs 리뷰어 의문 구분
- **우리 연구와의 관련성**

## 입력 형태

- 로컬 PDF 파일 경로 (`~/Downloads/paper.pdf`)
- arXiv URL (`https://arxiv.org/abs/2401.12345`)
- 학회/저널 URL (ACL Anthology, OpenReview, IEEE 등)
- DOI 또는 제목

## 설치 방법

Claude Code에서:

```
/plugin marketplace add baekdusan/paper-cpr-summary
/plugin install paper-cpr-summary@paper-cpr-summary
```

## 사용 방법

```
이 논문 요약해줘: https://arxiv.org/abs/2401.12345
```

또는 명시적으로:

```
/paper-cpr-summary:paper-summary ~/Downloads/paper.pdf
```

## 업데이트

스킬 내용을 수정한 뒤 push 하면, 사용자 측에서:

```
/plugin marketplace update paper-cpr-summary
```

## 기여

연구실 동료가 개선 제안이 있다면 PR 또는 이슈로 알려주세요.
