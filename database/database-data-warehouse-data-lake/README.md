# Database vs Data Warehouse vs Data Lake

## What is a database?

- 데이터베이스는 데이터나 정보의 집합을 의미한다.
- Online Transaction Processing(OLTP)를 지원하는 데 사용된다.
- 사용자나 애플리케이션은 데이터베이스 관리 체계(DBMS)를 통해 데이터베이스에 저장된 데이터에 접근한다.

### Database characteristics

- 데이터 보안 및 인증/인가
- ACID(Atomicity, Consistency, Isolation, Durability) 트랜잭션
- 질의 언어 및 API
- 인덱스
- 전문 검색(Full-text Search)

#### 관계형 데이터베이스

- 고정된 행(row)과 열(column)으로 데이터를 저장
- 정형화된 데이터 저장

#### 비관계형 데이터베이스(NoSQL)

- 다양한 데이터 구조로 데이터 저장
  - JSON
  - BSON
  - Key-Value
  - Column Oriented
  - Graph
- 비정형, 반정형 데이터 저장

## OLAP + data warehouses and data lakes

- OLTP에 특화된 데이터베이스와 달리, 데이터 웨어하우스와 데이터 레이크는 OLAP(Online Analytical Processing)에 특화되어 있다.
- OLAP 시스템은 다양한 데이터 소스로부터 데이터를 수집하고, 수집한 데이터를 분석하여 BI(Business Intelligence), 보고, 예측 등의 작업을 수행한다.

## What is a data warehouse?

- 데이터 웨어하우스는 다양한 원천으로부터 고도로 구조화된 데이터를 저장하는 시스템이다.
- 데이터 웨어하우스를 사용하는 이유는 서로 다른 여러개의 데이터 소스를 통하여 데이터를 분석하고, 인사이트를 발견하고, 미래를 예측하기 위함이다.

> Q. 그렇다면 데이터 웨어하우스도 데이터베이스인가?  
> A. 그렇다. 데이터 웨어하우스는 데이터 분석에 특화된 대규모 데이터베이스이다.

### Data warehouse characteristics

- 데이터 웨어하우스에 저장되는 데이터는 추출(Extract), 변형(Transform), 적재(Load)의 과정(ETL Process)을 거쳐 원천으로부터 저장된다.
- ETL Process는 매일, 혹은 매 시간 등 주기적으로 실행되므로, 데이터 웨어하우스에 저장된 데이터는 실시간성이 떨어진다.
- 데이터 분석가는 데이터 웨어하우스에 접근할 수 있고, 이를 BI 툴과 연동하여 데이터 분석과 인사이트 발견을 위한 보고서, 대시보드 등을 구성할 수 있다.

### Data warehouse examples

- Amazon Redshift
- Google BigQuery
- IBM Db2 Warehouse
- Microsoft Azure Synapse
- Oracle Autonomous Data Warehouse
- Snowflake
- Teradata Vantage

## What is a data lake?

- 데이터 레이크는 다양한 원천으로부터 원천 그대로의 상태로 데이터를 저장하는 시스템이다.
- 데이터 레이크는 데이터 웨어하우스와 다르게 다양한 원천에서 가져오는 데이터를 JSON, BSON, CSV, TSV 등의 다양한 형태 그대로 저장할 수 있다.

### Data lake characteristics

- 데이터 레이크는 대량의 정형, 반정형, 비정형 데이터를 저장할 수 있다.
- 데이터 웨어하우스와 달리 데이터를 정형화하는 ETL 과정을 필요로 하지 않는다.
- 데이터 레이크에 저장된 데이터 분석을 위해서는 데이터 분석가 이외의 데이터 사이언티스트, 데이터 엔지니어의 도움이 필요할 수 있다.
- 비용 효율적이며, 머신 러닝을 통한 분석과 예측적 분석을 지원한다.

### Data lake examples

- Amazon S3
- Azure Data Lake Storage Gen2
- Google Cloud Storage

## What are the key differences between a database, data warehouse, and data lake?

- 데이터베이스는 애플리케이션이 필요로 하는 현재 데이터를 저장한다.
- 데이터 웨어하우스는 데이터 분석을 목적으로 다양한 원천으로부터 과거 데이터와 현재 데이터를 정형화된 형태로 가공하여 저장한다.
- 데이터 레이크는 데이터 분석을 목적으로 다양한 원천으로부터 과거 데이터와 현재 데이터를 원천 데이터 형태 그대로 저장한다.

|          | 데이터베이스                | 데이터 웨어하우스              | 데이터 레이크                               |
|----------|-----------------------|------------------------|---------------------------------------|
| 워크로드     | Operational,<br>Transactional | Analytical             | Analytical                            |
| 데이터 형태   | 정형, 반정형               | 정형, 반정형                | 정형, 반정형, 비정형                          |
| 데이터 실시간성 | 실시간                   | 준실시간 or 비실시간           | 준실시간 or 비실시간                          |
|사용자| 애플리케이션 개발자            | 데이터 분석가,<br>데이터 사이언티스트 | 애플리케이션 개발자,<br>데이터 분석가,<br>데이터 사이언티스트 |
|장점|빠른 데이터 접근|구조화된 데이터로 분석에 용이|데이터 저장이 간편<br>데이터 분석에 용이<br>분산 저장 및 컴퓨팅|
|단점|제한된 데이터 분석 능력|스키마 설계와 변경의 어려움|데이터 구조화와 가공을 위한 별도의 관리 필요|

## Reference

- https://www.mongodb.com/databases/data-lake-vs-data-warehouse-vs-database