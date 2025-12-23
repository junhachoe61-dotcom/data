[PRD] 프로젝트명: DataTrust-Light (금융권용 초경량 데이터 신뢰성 확보 체계)
1. 프로젝트 배경 및 목적 (Context & Goals)
배경: 토스뱅크와 같은 금융 환경은 데이터 정합성이 비즈니스 의사결정과 규제 준수에 직결됨. 그러나 대규모 거버넌스 솔루션 도입은 초기 비용과 운영 부담이 큼.

목적: 서버리스 및 오픈소스 기반의 최소 비용으로 데이터 품질 검증(Quality)과 흐름 추적(Lineage)을 자동화하는 프레임워크 구축.

타겟: 데이터 기반 의사결정이 잦은 비즈니스 부서 및 기술 규제 대응이 필요한 엔지니어링 팀.

2. 핵심 기능 (Key Features)
선제적 품질 가드레일 (Data Quality Guardrail):

소스 데이터 적재 전/후에 Null 체크, 스키마 일치 여부, 값의 범위 등을 자동 검증.

품질 기준 미달 시 하위 파이프라인 실행을 중단하는 'Circuit Breaker' 기능.

자동화된 데이터 리니지 (Automated Lineage):

데이터의 생성부터 소비까지의 경로를 시각화하여 변경 영향도 분석 및 감사 대응 시간 단축.

운영 비용 최적화 (Cost Efficiency):

GitHub Actions와 Soda Core 등을 활용하여 별도의 상시 서버 운영비 없이 실행 환경 구축.

3. 기술 스택 (Tech Stack)
Orchestration: GitHub Actions (서버리스 워크플로우 제어)

Quality Check: Soda Core (선언적 YAML 기반 품질 검증)

Metadata/Lineage: OpenLineage & Marquez (메타데이터 표준 준수 및 시각화)

Storage/Engine: DuckDB & S3 (초경량 분석 엔진 및 데이터 레이크)

4. 사용자 여정 (User Journey)
데이터 엔지니어: 신규 파이프라인 개발 시 YAML 파일에 품질 규칙 정의.

시스템 자동 실행: 데이터가 유입되면 품질 검사 수행 후 메타데이터를 리니지 서버로 전송.

장애 알림: 검증 실패 시 즉시 Slack 알림 발송 및 하위 작업 차단.

분석가/리더: 시각화된 리니지 맵을 통해 데이터의 신뢰도 수치를 확인 후 의사결정에 활용.

5. 성공 지표 (Success Metrics)
데이터 사고 인지 시간(MTTD): 기존 수동 모니터링 대비 80% 이상 단축.

인프라 운영 비용: 상용 거버넌스 도구 대비 90% 이상의 비용 절감.

데이터 신뢰도: 전체 데이터셋 중 품질 검증 통과 비율 99.9% 유지.