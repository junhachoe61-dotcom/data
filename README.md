# DataTrust-Light

**금융권용 초경량 데이터 신뢰성 확보 체계**

서버리스 및 오픈소스 기반으로 데이터 품질 검증(Quality)과 흐름 추적(Lineage)을 자동화하는 프레임워크

## 🎯 프로젝트 목표

- **비용 효율성**: 상용 솔루션 대비 90% 비용 절감
- **데이터 신뢰성**: 품질 검증 통과율 99.9% 유지
- **빠른 장애 대응**: 데이터 사고 인지 시간(MTTD) 80% 단축
- **확장 가능성**: 표준 기반 설계로 엔터프라이즈 확장 용이

## 🏗️ 아키텍처

```
Data Sources → GitHub Actions → Soda Core (Quality) → OpenLineage (Lineage)
                                        ↓
                                   S3 + DuckDB
                                        ↓
                                Marquez + Grafana
```

## 🛠️ 기술 스택

- **Orchestration**: GitHub Actions
- **Quality Check**: Soda Core
- **Lineage**: OpenLineage + Marquez
- **Storage**: AWS S3
- **Analysis**: DuckDB
- **Monitoring**: Grafana + Prometheus

## 📚 문서

- [PRD (Product Requirements Document)](docs/PRD.md)
- [TechStack](docs/TechStack.md)
- [Ideation](docs/Ideation.md)

## 🚀 빠른 시작

```bash
# 1. 저장소 클론
git clone https://github.com/junhachoe61-dotcom/datatrust-light.git
cd datatrust-light

# 2. 환경 설정
cp .env.example .env
# .env 파일에 AWS 자격증명 및 설정 입력

# 3. 의존성 설치
pip install -r requirements.txt

# 4. Marquez 서버 시작
docker-compose up -d

# 5. 샘플 파이프라인 실행
python examples/sample_pipeline.py
```

## 💡 핵심 기능

### 1. 선제적 품질 가드레일
```yaml
# checks/transactions.yml
checks for transactions:
  - row_count > 0
  - missing_count(user_id) = 0
  - invalid_percent(amount) < 1%
```

### 2. 자동 데이터 리니지
- 데이터 생성부터 소비까지 전체 경로 추적
- 변경 영향도 분석
- 감사 대응 시간 단축

### 3. Circuit Breaker
- 품질 미달 시 하위 파이프라인 자동 차단
- Slack 실시간 알림

## 📊 성공 지표

| 지표 | 목표 |
|------|------|
| 데이터 사고 인지 시간 (MTTD) | 80% 단축 |
| 인프라 운영 비용 | 90% 절감 |
| 데이터 신뢰도 | 99.9% 유지 |

## 🗺️ 로드맵

- [x] Phase 1: MVP (2주) - 핵심 품질 검증 및 리니지
- [ ] Phase 2: 확장 (2주) - 다중 소스 및 고급 기능
- [ ] Phase 3: 프로덕션 (1주) - 모니터링 및 문서화

## 📄 라이선스

MIT License

## 👤 Author

Junha Choe - Portfolio Project for Toss Bank Data Engineering Department Leader Position
