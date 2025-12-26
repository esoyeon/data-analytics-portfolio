# 🧴 올리브영 썬크림 리뷰 분석: 미충족 니즈(Unmet Needs) 발굴

## Overview
**LLM을 활용한 방대한 고객 리뷰 분석 및 제품 기회 발굴 프로젝트**  
수만 건의 리뷰 텍스트에서 단순 긍/부정이 아닌 '소비자가 기대했으나 충족되지 않은' 패턴을 찾아내어, 신제품 기획자가 즉시 활용 가능한 포인트를 도출했습니다.

## Problem
화장품 시장, 특히 썬크림은 이미 레드오션으로 상향 평준화되어 차별화가 어렵습니다. 기존의 정량적 별점 데이터나 단순 키워드 빈도 분석으로는 "왜 4점을 줬는지", "좋지만 무엇이 아쉬운지"에 대한 **Expectation-Experience Gap(기대와 경험의 차이)**을 파악하기 어렵습니다.

## Data
*   **Source**: 올리브영 온라인몰 썬크림 카테고리
*   **Scale**: 주요 148개 제품, **총 11,528건 리뷰** (Helpful, Newest, Low/High Rating 기반 층화 추출)
*   **Preprocessing**:
    *   체험단/단답형 노이즈 제거
    *   Domain Dictionary 기반 태깅 (계절, 피부타입, 상황 등)

## Approach
**Human-in-the-loop AI Pipeline**을 구축하여 분석의 깊이와 효율성을 확보했습니다.
1.  **Collection**: Playwright를 활용한 동적 크롤링
2.  **Structuring**: **Gemini 2.0 Flash**를 활용하여 비정형 텍스트를 구조화된 데이터(Aspect-Sentiment Pair)로 변환
3.  **Analysis**: 속성별 만족/불만/조건부만족 비율 분석 및 Opportunity Map 시각화
4.  **Reporting**: Plotly 대시보드 및 PDF 리포트 자동 생성

## Key Findings
*   **자극/트러블의 역설**: '순한 성분'을 강조한 제품일수록 소비자의 기대치가 높아 미세한 자극에도 민감하게 반응하여 불만율이 급증함.
*   **유수분 밸런스(Oiliness vs Dryness)**: '촉촉함'과 '기름짐' 사이의 모호한 경계에서 복합성 피부 소비자들의 불만이 집중됨.
*   **메이크업 궁합(Compatibility)**: 단독 사용 시 만족도가 높아도, 파운데이션과의 밀림 현상이 발생하면 재구매 의사가 급락함.
*   **톤업의 구체성**: 단순 '하얘짐'이 아닌 '맑은 상아빛', '균일한 톤' 등 톤업에 대한 소비자 기준이 매우 구체적임.

## Deliverables
*   **Deliverables**:
    *   [GitHub Repository](https://github.com/esoyeon/sunscreen-review-unmet-needs)
    *   [📄 **Final Report (PDF)**](../docs/sunscreen_report.pdf)


## Reproducibility
**Environment**: Python 3.10+, Google Gemini API Key 필요
1.  레포지토리 클론 및 의존성 설치: `pip install -r requirements.txt`
2.  Playwright 브라우저 설치: `playwright install`
3.  통합 파이프라인 스크립트 실행:
    ```bash
    chmod +x run_pipeline.sh
    ./run_pipeline.sh
    ```
    *수집부터 리포트 생성까지 전 과정이 자동 실행됩니다.*

## Limitations & Next Steps
**Limitations**
*   **Sampling Bias**: 전체 리뷰 모집단이 아닌 샘플 데이터로, 실제 시장 전체의 통계와는 오차가 있을 수 있음.
*   **LLM Hallucination**: Gemini 2.0 모델의 구조화 과정에서 미세한 오분류 가능성 존재 (자체 검증 정확도 약 94%).
*   **Seasonality**: 수집 시점에 따라 계절성 키워드(여름/겨울) 빈도에 차이가 발생할 수 있음.

**Next Steps**
*   **카테고리 확장**: 썬크림 외 '앰플', '크림' 등 타 카테고리로 파이프라인 확장 적용.
*   **실시간 모니터링**: 신제품 출시 직후 리뷰를 실시간으로 수집하여 초기 반응 대시보드화.
*   **감성 사전 고도화**: LLM이 분류한 데이터를 기반으로 도메인 특화 감성 사전을 반자동으로 구축하여 비용 절감.
