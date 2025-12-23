# TechStack: DataTrust-Light

## 핵심 기술 스택

### 1. Orchestration
- **GitHub Actions**
  - 서버리스 워크플로우 실행
  - 무료 티어: 2,000분/월
  - 코드와 파이프라인 통합 관리

### 2. Data Quality
- **Soda Core**
  - YAML 기반 품질 규칙 정의
  - 다중 데이터 소스 지원 (PostgreSQL, S3, Snowflake)
  - 오픈소스 무료

### 3. Data Lineage
- **OpenLineage**
  - 업계 표준 메타데이터 스펙
  - 벤더 중립적
- **Marquez**
  - OpenLineage 네이티브 지원
  - 리니지 시각화 UI
  - Docker 경량 배포

### 4. Storage & Analysis
- **AWS S3**
  - 데이터 레이크 스토리지
  - Parquet 포맷
- **DuckDB**
  - 인메모리 OLAP 엔진
  - 별도 서버 불필요
  - S3 직접 쿼리 가능

### 5. Monitoring & Alerts
- **Grafana + Prometheus**
  - 품질 메트릭 시각화
  - 알림 규칙 설정
- **Slack API**
  - 실시간 알림

---

## 데이터 흐름

```
Source (PostgreSQL/S3/API)
    ↓
GitHub Actions Trigger
    ↓
Soda Core Quality Check ──→ [FAIL] → Slack Alert + Block
    ↓ [PASS]
Data Pipeline Execution
    ↓
OpenLineage Event Emission
    ↓
Marquez Metadata Store
    ↓
S3 Data Lake (Parquet)
    ↓
DuckDB Analysis
    ↓
Grafana Dashboard
```

---

## 비용 구조

| 항목 | 월 비용 | 비고 |
|------|---------|------|
| GitHub Actions | $0 | 무료 티어 |
| AWS S3 | $100 | 1TB 데이터 |
| EC2 (Marquez) | $50 | t3.small |
| Grafana Cloud | $0 | 무료 티어 |
| **합계** | **$150** | 기존 대비 97% 절감 |

---

## 확장 경로

### 현재 (MVP)
- GitHub Actions + Soda Core + Marquez
- 소규모 팀 (< 10명)
- 파이프라인 < 50개

### 중기 (6개월)
- Self-hosted Airflow (필요시)
- Great Expectations 추가
- 파이프라인 < 200개

### 장기 (12개월+)
- Datahub / Amundsen 마이그레이션
- 엔터프라이즈 규모
- OpenLineage 표준 덕분에 코드 변경 최소화

---

## 기술 선정 이유

| 기술 | 선정 이유 |
|------|-----------|
| GitHub Actions | 서버리스, 무료, CI/CD 통합 |
| Soda Core | 선언적 규칙, 학습 곡선 낮음 |
| OpenLineage | 표준 준수, 향후 확장성 |
| DuckDB | 서버 불필요, SQL 지원 |
| S3 | 저비용, 높은 내구성 |
