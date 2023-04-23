# Elastic Search

### 정의

> Apache Lucene(아파치 루씬) 기반의 java 오픈소스 분산 검색 엔진으로 방대한 데이터를 신속하고 거의 실시간으로 저장, 검색, 분석할 수 있습니다.
Elasticsearch는 검색을 위해 단독으로 사용되기도 하며, ELK( Elasticsearch / Logstatsh / Kibana )스택으로 사용되기도 합니다.
> 

### **ELK( Elasticsearch / Logstatsh / Kibana ) 스택**

- **ELK**는 분석 및 저장 기능을 담당하는 **ElasticSearch**, 수집 기능을 하는 **Logstash**, 이를 시각화하는 도구인 **Kibana**의 앞글자만 딴 단어입니다.
- ELK는 접근성과 용이성이 좋아 최근 가장 핫한 Log 및 데이터 분석 도구입니다.

**Elasticsearch :** Logstatsh로 부터 받은 데이터를 검색 및 집계를 하여 필요한 관심 있는 정보를 획득

**Logstatsh :** 다양한 소스(DB, csv파일 등)의 로그 또는 트랜잭션 데이터를 수집, 집계, 파싱하여 Elasticsearch 로 전달

**Kibana :** Elasticsearch의 빠른 검색을 통해 데이터를 시각화 및 모니터링

### 참고

[[Elasticsearch] 기본 개념잡기](https://victorydntmd.tistory.com/308)
