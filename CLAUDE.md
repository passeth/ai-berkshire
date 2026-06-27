# AI Berkshire — 프로젝트 지침 (한국어판)

## 프로젝트 개요

Claude Code 기반의 가치 투자 연구 Skill 모음. 4대 거장 프레임워크: 버핏, 멍거, 단용평, 리루.
GitHub: passeth/ai-berkshire (원본 xbtlin/ai-berkshire)

## 프로젝트 구조

```
skills/          — 투 research Skill 정의(.md), ~/.claude/commands/ 로 복사해 사용
tools/           — 보조 도구 (financial_rigor.py 정확 계산)
reports/         — 투자 연구 보고서 출력
assets/          — 이미지 등 정적 리소스
```

## 보고서 디렉토리 구조

모든 보고서는 **회사명**으로 폴더를 만들고, 해당 회사와 관련된 모든 보고서를 폴더 안에 배치:

```
reports/
├── AI산업연구/              — AI 가치사슬 전경 연구 (상단 고정)
│   ├── AI다섯겹케이크-산업전경연구-20260605.md
│   └── AI다섯겹케이크-공중계-20260605.md
├── 텐센트/                  — 텐센트 모든 연구 보고서
│   ├── 텐센트-research-20260408.md
│   ├── 텐센트-earnings-2025Q4.md
│   ├── 텐센트-management-20260409.md
│   └── 텐센트-thesis.md
├── 핀둬둬/                  — 핀둬둬 모든 연구 보고서
├── 버블마트/                — 버블마트 모든 연구 보고서
├── 원전-industry-20260409.md — 업계 보고서는 루트에 배치
├── AI컴퓨트-funnel-20260509.md  — 깔때기 선별 보고서는 루트에 배치
├── portfolio-latest.md       — 포트폴리오 보고서는 루트에 배치
└── 다중회사비교-checklist-20260408.md — 다중 회사 보고서는 루트에 배치
```

## 보고서 명명 규칙

| Skill | 파일 명명 형식 | 예시 |
|------|----------------|------|
| /investment-team | `{회사명}/` 폴더 안에 4개 관점 + 최종 보고서 | `reports/핀둬둬/최종보고서.md` |
| /investment-research | `{회사명}-research-{YYYYMMDD}.md` | `reports/텐센트/텐센트-research-20260408.md` |
| /investment-checklist | `{회사명}-checklist-{YYYYMMDD}.md` | `reports/텐센트/텐센트-checklist-20260408.md` |
| /industry-research | `{업종명}-industry-{YYYYMMDD}.md` (루트) | `reports/원전-industry-20260409.md` |
| /industry-funnel | `{업종명}-funnel-{YYYYMMDD}.md` (루트) | `reports/AI컴퓨트-funnel-20260509.md` |
| /private-company-research | `{회사명}-private-{YYYYMMDD}.md` | `reports/바이트댄스/바이트댄스-private-20260408.md` |
| /earnings-review | `{회사명}-earnings-{기간}.md` | `reports/텐센트/텐센트-earnings-2025Q4.md` |
| /earnings-team | `{회사명}/` 폴더 안에 4대 거장 관점 + 연구 초안 + 공중계 아티클 + 독자 리뷰 | `reports/텐센트/텐센트-earnings-2025Q4.md` (공중계 확정판) |
| /thesis-tracker | `{회사명}-thesis.md` (장기 유지) | `reports/텐센트/텐센트-thesis.md` |
| /portfolio-review | `portfolio-latest.md` (루트, 지속 업데이트) | `reports/portfolio-latest.md` |
| /management-deep-dive | `{회사명}-management-{YYYYMMDD}.md` | `reports/텐센트/텐센트-management-20260409.md` |

## /investment-team 파일 구조

```
reports/{회사명}/
├── README.md                         — 연구 프레임워크 개요 + 핵심 결론
├── 01-비즈니스모델분석-단용평관점.md
├── 02-재무평가분석-버핏관점.md
├── 03-업계경쟁분석-멍거관점.md
├── 04-리스크경영진평가-리루관점.md
└── 최종보고서.md                     — Team Lead 종합 보고서
```

## 투 research 분석 핵심 원칙 (최고 우선순위)

- **객관, 객관, 객관** — 모든 투 research 분석은 사실과 데이터에 기반해야 하며, 주관적 억측은 엄격히 금지
- "사실"과 "견해"를 엄격히 구분: 사실은 데이터로 뒷받침, 견해는 반드시 "견해" 또는 "추측"으로 명시
- **선입견 금지**: 매수 또는 매도 선입견 없이, 먼저 데이터를 나열하고, 논리를 추론한 후, 결론을 도출. 결론은 데이터에서 자연스럽게 나와야 함
- "내 생각에는", "내 느낌에는", "명백히" 등 주관적 표현 사용 금지. 대신 "데이터에 따르면", "증거가 보여준다", "XX 출처에 따르면" 사용
- **양면 제시**: 모든 핵심 판단에는 반대 논거를 반드시 첨부 ("그러나 다른 한편으로는..."), 독자가 스스로 저울질하게 함
- 불확실한 일에 대해서는 솔직히 "불확실" 또는 "데이터 부족"이라고 말하고, 추측으로 확실성을 채우지 말 것
- 모든 skill (investment-team, investment-research, earnings-review 등) 실행 시 위 원칙을 반드시 준수

## 보고서 언어와 스타일

- 모든 보고서는 **원본 중국어** 유지 (연구 원본의 무결성 보존)
- 스타일: 직설적, 날카로움, 군더더기 없음
- 데이터는 반드시 출처 표기, 핵심 데이터는 최소 2개 출처 교차 검증
- 추정치는 반드시 "추정"이라고 명시
- 평점은 ★ 기호 사용 (★1-5, 반별 없음)
- 버핏/멍거/단용평/리루의 명언 코멘트를 적절히 삽입

## GitHub 작업

- 로컬 클론 경로: `~/ai-berkshire/`
- 원격 저장소: `https://github.com/passeth/ai-berkshire.git` (포크된 경우)
- 푸시 전 반드시 `git pull --rebase origin main` (원격에 자주 새 커밋이 있음)
- commit message는 한국어 또는 중국어로 명확하게 무엇을 변경했는지 기술
- 중간 과정 파일(예: data_collection.md)은 푸시하지 말고, 최종 보고서만 푸시

## 자주 사용하는 명령

```bash
# 보고서를 GitHub에 푸시
cd ~/ai-berkshire
git add reports/
git commit -m "feat: 텐센트 2025Q4 earnings 분석 추가"
git push

# 새로운 스킬 설치 (로컬 테스트 후)
cp skills/new-skill.md ~/.claude/commands/
```

## 참고

- 이 한국어판 CLAUDE.md는 번역본입니다. 원본 논리는 CLAUDE_CN.md를 참조하세요.
- 실제 연구 보고서 생성 시 원칙은 변함없이 적용됩니다.
