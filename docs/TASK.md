# 프로젝트 태스크 (DataTrust-Light)

이 문서는 [PRD](./PRD.md)의 구현 로드맵을 기반으로 작성된 작업 목록입니다.

## Phase 1: MVP (2주)
**목표**: 핵심 품질 검증 및 리니지 추적 기능 구현

- [ ] **기술 스택 선정 및 초기 설정**
  - [ ] 프로젝트 리포지토리 생성 및 설정
  - [ ] GitHub Actions 환경 구성
  - [ ] Python, Soda Core, OpenLineage 라이브러리 의존성 정의
- [ ] **Soda Core 품질 검증 파이프라인 구축**
  - [ ] PostgreSQL 데이터베이스 연동 설정
  - [ ] 기본 품질 규칙(Quality Rules) 정의 (`checks.yml`)
    - [ ] `row_count > 0`
    - [ ] `schema` 검증
    - [ ] `freshness` (최신성) 검사
  - [ ] Slack 알림 연동 (검증 실패 시 알림)
- [ ] **OpenLineage + Marquez 설정**
  - [ ] Marquez 서버 Docker Compose 배포
  - [ ] ETL 파이프라인 코드에 OpenLineage 클라이언트 통합
  - [ ] 샘플 파이프라인 실행 및 리니지 추적 확인
- [ ] **GitHub Actions 워크플로우 구성**
  - [ ] 일일 배치 스케줄링 (`cron`)
  - [ ] 품질 검증 단계(Step) 추가
  - [ ] 검증 실패 시 파이프라인 중단 로직 확인

## Phase 2: 확장 (2주)
**목표**: 다양한 데이터 소스 및 고급 기능 추가

- [ ] **다중 데이터 소스 지원**
  - [ ] AWS S3 Parquet 파일 검증 로직 구현
  - [ ] Kafka 스트림 데이터 모니터링 연동
  - [ ] 외부 API 데이터 검증 추가
- [ ] **고급 품질 규칙 구현**
  - [ ] 통계적 이상 탐지 (Anomaly Detection) 설정
  - [ ] 비즈니스 도메인 규칙 (예: 금액 범위, 참조 무결성) 추가
  - [ ] 데이터 프로파일링 리포트 생성
- [ ] **DuckDB 분석 환경 구축**
  - [ ] S3 데이터에 대한 DuckDB 직접 쿼리 환경 구성
  - [ ] 품질 메트릭 추이 분석 쿼리 작성 (SQL)
- [ ] **Circuit Breaker 메커니즘**
  - [ ] 품질 검증 실패 시 하위(Downstream) 작업 자동 차단 구현
  - [ ] 일시적 오류에 대한 재시도(Retry) 정책 설정

## Phase 3: 프로덕션 준비 (1주)
**목표**: 모니터링, 문서화, 안정성 강화

- [ ] **모니터링 대시보드 구축**
  - [ ] Grafana 설치 및 데이터 소스 연결
  - [ ] 품질 메트릭 및 파이프라인 상태 시각화 대시보드 생성
  - [ ] 주요 지표에 대한 Alert Rule 설정
- [ ] **문서화 (Documentation)**
  - [ ] 사용자 가이드 (User Guide) 작성
  - [ ] 품질 규칙 작성 가이드 (How-to) 작성
  - [ ] 트러블슈팅(Troubleshooting) 가이드 작성
- [ ] **성능 최적화**
  - [ ] 대용량 데이터 처리 파티셔닝 전략 도입
  - [ ] 자주 조회되는 데이터 캐싱(Caching) 전략 수립
- [ ] **보안 강화**
  - [ ] 민감 정보(Credentials) GitHub Secrets로 이관
  - [ ] IAM 및 접근 제어 권한 검토 (Least Privilege)
