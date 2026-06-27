# 재무 데이터 획득 및 교차 검증 규범

정확하고 신뢰할 수 있는 재무 데이터를 확보하고, AI 암산 오류와 출처 단일화 위험을 방지하기 위한 표준 작업 흐름.

## 핵심 원칙

1. **최소 2개 독립 출처**: 모든 핵심 숫자는 최소 2개 서로 다른 데이터 소스에서 확인해야 함
2. **도구 검증 강제**: 중요한 계산은 반드시 `tools/financial_rigor.py`를 사용. LLM 암산 금지
3. **오차 >1% 경고**: 두 출처 간 차이가 1%를 초과하면 명확히 표시하고 원인을 조사
4. **단위 명확화**: "억"의 기준(홍콩달러? 위안? 달러?), 주식수 단위(만 주? 억 주?)를 반드시 명시

## 데이터 소스 매트릭스 (2026년 기준)

### 미국 주식 (NYSE / NASDAQ)
- **주**: macrotrends.net
- **부**: stockanalysis.com 또는 Yahoo Finance
- 재무제표(손익계산서, 재무상태표, 현금흐름표): macrotrends를 기본으로 하고 stockanalysis로 교차 확인

### 홍콩 주식 (HKEX)
- **주**: aastocks.com
- **부**: macrotrends ADR 페이지 또는 회사 IR 공시
- 재무제표는 aastocks의 "재무 분석" 섹션 사용. 연간/분기 모두 확인

### A주 (상하이/선전)
- **주**: 동방재부 (eastmoney.com)
- **부**: 거조자신망 (cninfo.com.cn) — 상장사 공시 원본
- 가능하면 Wind 또는 Bloomberg 터미널 데이터로 3차 확인

## 필수 검증 단계 (반드시 실행)

### 1. 시가총액 수작업 검산
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap \
  --price 510 \
  --shares 9.11e9 \
  --reported 4.65e12 \
  --currency HKD
```

### 2. 밸류에이션 지표 정확 계산
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price 510 --eps 27.5 --bvps 180 --fcf-per-share 22 --dividend 3.5
```

### 3. 다중 출처 교차 검증
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py cross-validate \
  --field "revenue_2024" \
  --values '{"eastmoney": 4521.2, "cninfo": 4518.9}' \
  --unit "억 위안"
```

### 4. 3시나리오 밸류에이션 (선택)
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario \
  --price 120 --eps 8.5 --shares 62 \
  --growth 0.18 0.12 0.06 \
  --pe 22 18 14 \
  --currency HKD
```

## 일반적인 함정과 대책

- **시가총액 단위 오류**: 홍콩달러 억 vs 위안 억 — 항상 통화를 명시하고 손으로 계산
- **주식수 단위 오류**: "만 주"와 "억 주" 혼동 — 반드시 억 단위로 통일
- **FCF 정의 차이**: 리스, 인수, 자본화 비용 포함 여부 — 출처별 정의를 확인
- **ADR vs 원주**: 미국 ADR 보고서의 숫자는 원주와 다를 수 있음 — 조정 계수 확인
- **연결 vs 별도 재무제표**: 중국 회사에서 흔한 함정 — 일관되게 연결 재무제표 사용

## 보고서 내 표기 규칙

- 모든 숫자 뒤에 출처를 괄호로 표기: `매출 4,521억 위안 (동방재부 2025-03-25)`
- 두 출처 간 오차가 있으면: `매출 4,521억 / 4,519억 위안 (오차 0.04%)`
- 추정치인 경우: `추정 매출 ≈ 5,200억 위안 (신뢰도 중)`
- 모든 계산 결과는 도구 출력 원문을 "부록: 핵심 데이터 교차 검증 기록"에 첨부

## 예시: 텐센트 분석 시 데이터 수집 흐름

1. aastocks에서 최신 재무제표 다운로드
2. macrotrends ADR 페이지에서 동일 기간 숫자 비교
3. 주가 × 발행주식수로 시총 검산 (HKD 단위)
4. financial_rigor.py로 주요 지표 재계산
5. 결과가 일치하면 보고서 본문에 사용, 불일치 시 "데이터 불일치 주의" 명시

이 규범을 철저히 지키는 것이 AI Berkshire의 데이터 신뢰성의 기반입니다.