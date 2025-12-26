# 🇧🇷 Olist 브라질 이커머스 데이터 분석 (SQL)

## 1. 프로젝트 개요 (Overview)
**SQL을 활용한 이커머스 핵심 지표 추출 및 비즈니스 현황 진단**  
브라질의 실제 커머스 데이터(9.9만 건)를 활용하여 현업의 모호한 비즈니스 질문을 명확한 SQL 쿼리로 변환하고, **매출 성장 둔화의 원인**을 데이터 기반으로 규명했습니다.

## 2. 문제 정의 (Problem Statement)
이커머스 운영 현장에서는 "매출이 정말 늘고 있는가?", "충성 고객은 얼마나 되는가?"와 같은 질문이 끊임없이 발생합니다.  
하지만 단순한 매출 합계만으로는 **재구매율(Retention), 객단가(AOV), 배송 지연 영향** 등 비즈니스의 구조적 문제를 파악하기 어렵습니다.  
따라서 본 프로젝트는 **추상적인 비즈니스 요구사항을 명확한 지표(KPI)로 정의**하고, 이를 검증 가능한 **SQL 쿼리로 구현**하는 데 초점을 맞추었습니다.

## 3. 데이터 및 분석 방법 (Data & Approach)
*   **Data Source**: [Kaggle Olist Brazilian E-Commerce Dataset](https://www.kaggle.com/datasets/terencicp/e-commerce-dataset-by-olist-as-an-sqlite-database)
*   **Scale**: 주문 9.9만 건, 고객 9.9만 명, 셀러 3천 명 (2016.09 ~ 2018.10)
*   **Analysis Flow**:
    1.  **Metric Definition**: GMV, AOV, 재구매율 등 지표의 분자/분모를 명확히 정의
    2.  **Query Engineering**: `Window Function`과 `CTE`를 활용하여 성장률(MoM) 및 재구매 주기 산출
    3.  **Verification**: Python(Pandas)을 활용한 쿼리 결과 정합성 교차 검증

## 4. 핵심 발견 (Key Findings)
*   **📉 성장세 둔화**: 2017년 블랙프라이데이에 최고 매출을 기록했으나, 이후 성장률(MoM)이 정체되는 경향을 확인했습니다.
*   **🧴 카테고리 쏠림**: 'Bed_Bath_Table', 'Health_Beauty' 등 상위 10개 카테고리가 전체 매출의 60% 이상을 견인합니다.
*   **⚠️ 낮은 재구매율**: 전체 고객 중 재구매 비중이 **약 3%**에 불과하여, 신규 유입에 대한 의존도가 비정상적으로 높습니다. (CRM 마케팅 시급)
*   **💳 할부 의존도**: 고가 상품일수록 신용카드 할부(평균 3.5개월) 결제 비중이 뚜렷하게 증가합니다.

## 5. 산출물 (Deliverables)
분석 결과와 코드는 아래 링크에서 상세히 확인할 수 있습니다.

*   [📊 **분석 결과 시각화 (Composite Snapshot)**](../assets/olist_result.png)
    *   매출 추이, 카테고리 점유율, 결제 수단 분포를 **한눈에 요약한 대시보드 이미지**입니다.
*   [📁 **SQL 쿼리셋 (GitHub)**](https://github.com/esoyeon/olist-sql-data-analysis/tree/main/sql)
    *   비즈니스 질문별로 최적화된 SQL 파일들이 정리되어 있습니다.
*   [📓 **데이터 검증 노트 (EDA Notebook)**](https://github.com/esoyeon/olist-sql-data-analysis/blob/main/notebooks/eda_olist.ipynb)
    *   SQL 분석 전 데이터 구조를 파악하고 정합성을 검증한 Python Notebook입니다.

## 6. 한계점 및 추후 과제 (Limitations & Next Steps)
*   **외부 요인 데이터 부재**: 마케팅 프로모션 및 광고비 데이터가 없어 매출 변동의 인과관계를 완벽히 규명하기 어렵습니다.
*   **최신 성 비반영**: 2018년 이후 데이터가 부재하여 현재 시점의 트렌드와 다를 수 있습니다.
*   **Next Steps**: RFM 분석을 통한 **고객 세분화(Segmentation)** 및 타겟 마케팅 전략 수립이 필요합니다.
