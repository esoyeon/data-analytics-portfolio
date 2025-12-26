# 🇧🇷 Olist 브라질 이커머스 데이터 분석 (SQL)

## Overview
**SQL을 활용한 이커머스 핵심 지표 추출 및 비즈니스 현황 진단 프로젝트**  
브라질의 실제 커머스 데이터(9.9만 건)를 활용하여 모호할 수 있는 비즈니스 질문을 명확한 SQL 쿼리로 변환하고, 데이터에 기반한 현황 파악을 수행했습니다.

## Problem
이커머스 운영에서는 "매출이 늘었는가?", "어떤 카테고리가 효자인가?"와 같은 질문이 끊임없이 발생합니다. 하지만 단순한 합계만으로는 **재구매율, 객단가(AOV), 배송 지연 영향** 등 입체적인 현상을 파악하기 어렵습니다. 또한 현업에서는 분석 요청이 추상적인 경우가 많아, 이를 **명확한 지표(KPI)로 정의하고 검증 가능한 쿼리로 구현**하는 능력이 필수적입니다.

## Data
*   **Source**: [Kaggle Olist Brazilian E-Commerce Dataset](https://www.kaggle.com/datasets/terencicp/e-commerce-dataset-by-olist-as-an-sqlite-database)
*   **Scale**: 2016년 9월 ~ 2018년 10월 주문 약 99,000건, 고객 99,000명, 셀러 3,000명
*   **Database**: SQLite (Relation: Orders, Items, Customers, Payments, Products 등 7개 테이블)

## Approach
**"Business Question → KPI Definition → SQL Querying → Insight"**의 단계적 접근을 취했습니다.
1.  **Metric Definition**: GMV, AOV, 재구매율 등 모호할 수 있는 용어의 분자/분모를 명확히 정의
2.  **Query Engineering**: `WITH`문(CTE)을 활용하여 가독성을 높이고, `Window Function`으로 성장률(MoM) 등 심화 지표 산출
3.  **Visualization**: Python(Matplotlib/Seaborn)을 이용해 쿼리 결과의 추세와 패턴 시각화
4.  **Verification**: 쿼리 결과의 정합성을 교차 검증

## Key Findings
*   **성장세와 계절성**: 2017년 블랙프라이데이 시즌(11월)에 최고 매출을 기록했으나, 이후 성장률이 둔화되는 패턴 확인.
*   **카테고리 집중도**: 'Bed_Bath_Table', 'Health_Beauty' 등 상위 10개 카테고리가 전체 매출의 상당 부분을 점유.
*   **재구매의 한계**: 전체 고객 중 재구매 고객 비중이 3% 수준으로 매우 낮아, 신규 유입 의존도가 높음을 확인 (CRM 마케팅 필요성 대두).
*   **결제 수단 선호**: 신용카드 이용 비중이 압도적이며, 할부 결제 패턴이 고가 상품군에서 뚜렷하게 나타남.

## Deliverables
*   **GitHub Repository**: [esoyeon/olist-sql-data-analysis](https://github.com/esoyeon/olist-sql-data-analysis)
*   **Deliverables**:
    *   [📂 **SQL Queries**: 비즈니스 질문별 쿼리셋 (GitHub)](https://github.com/esoyeon/olist-sql-data-analysis/tree/main/sql)
    *   [📊 **Result Snapshot**: 결과 시각화 예시](../assets/olist_result.png)
    *   [📄 **Summary Report (PDF)**](../docs/olist_report.pdf)
    *   [📓 **EDA Notebook**: 데이터 탐색 및 정합성 검증](../projects/olist-sql-data-analysis.md) <!-- Self-link replaced or point to actual repo -->
        *   *(Note: Link to EDA Notebook is usually best served by GitHub URL)*
        *   [📓 **EDA Notebook (GitHub)**](https://github.com/esoyeon/olist-sql-data-analysis/blob/main/notebooks/eda_olist.ipynb)

## Reproducibility
**Environment**: Python 3.x, Jupyter Notebook, SQLite 3.25+
1.  Kaggle에서 `olist.sqlite` 다운로드 후 `_data_analysis/olist-data-analysis/` 루트에 위치
2.  SQL 쿼리 실행: DB 클라이언트(DBeaver 등) 또는 Python Notebook에서 `sql/*.sql` 실행
3.  EDA 실행: `notebooks/eda_olist.ipynb` 실행

## Limitations & Next Steps
**Limitations**
*   **Context Missing**: 프로모션 정보, 마케팅 비용 등 외부 요인 데이터 부재로 매출 변동의 원인 추론에 한계.
*   **Data Period**: 2018년 이후 데이터 부재로 최근 트렌드 파악 불가.
*   **Correlation vs Causation**: 배송 지연과 리뷰 평점 간의 상관관계만 확인 가능하며, 인과관계 단정은 어려움.

**Next Steps**
*   **고객 세분화(Segmentation)**: RFM 분석을 통해 VIP 고객군 정의 및 타겟 마케팅 전략 도출.
*   **배송 예측 모델링**: 머신러닝을 활용한 예상 배송일(Estimated Delivery Date) 정확도 개선 모델 개발.
*   **외부 데이터 결합**: 브라질 공휴일 및 경제 지표 데이터를 결합하여 거시적 요인 분석.
