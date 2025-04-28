
# 📝 프로젝트 요구사항 정리 (Draft)

## 1. 프로젝트 개요
- **프로젝트명**: 홈서버 기반 Java 웹 서비스 및 GIF 변환 AI 시스템 구축
- **목적**:  
  - 사용자가 웹을 통해 PDF 업로드 → AI 모델이 이를 분석해 GIF 변환 → 결과를 조회 및 관리할 수 있도록 한다.
  - 모든 인프라는 **사용자 소유 홈서버(Ubuntu)** 위에 자체 구축 및 운영한다.

## 2. 시스템 구성
| 구성 요소 | 설명 |
|:--|:--|
| Java 웹 서버 (Spring Boot) | - Admin UI/API 제공<br>- AI 모델 제어 API 호출 |
| AI 모델 서버 (Python 기반) | - PDF → GIF 변환 수행<br>- Web API 형태로 동작 |
| 데이터베이스 (MySQL 예상) | - PDF 업로드 경로, 변환된 GIF 경로 저장<br>- 변환 기록, 사용자 평가 기록 저장 |
| 스토리지 (Local Disk) | - PDF, GIF 파일 저장 |
| 네트워크/보안 | - SSL 통신 적용<br>- 외부에서 접속 가능하도록 홈서버 네트워크 설정 |

## 3. 주요 기능 요구사항
- Admin UI
- Java API 서버
- AI 모델 서버

## 4. 비기능 요구사항 (NFR)
| 항목 | 요구사항 |
|:--|:--|
| 성능 | - 1건 변환당 1~5분 이내 완료 |
| 보안 | - HTTPS 통신 적용<br>- 인증 및 접근제어 추가 예정 |
| 가용성 | - 홈서버 구동 상태 모니터링 수단 마련 |
| 백업 | - 변환된 GIF 및 원본 PDF 주기적 백업 스크립트 마련 |
| 유지보수성 | - 서비스 재기동 시 자동 복구 가능한 구조 설계 (Docker 고려 가능) |

## 5. 개발 환경
| 항목 | 환경 |
|:--|:--|
| 서버 OS | Ubuntu (홈서버) |
| Java 버전 | Java 17 이상 |
| Spring Boot 버전 | 3.x 권장 |
| Python 버전 | Python 3.11 이상 |
| DB | MySQL 8.x |
| 프론트엔드 | Admin: Thymeleaf or React(추후 결정) |
| API 통신 | REST API (JSON 기반) |
| 기타 툴 | Jenkins (CI/CD 예정), Docker (선택사항) |

# 📝 API 명세서 (Draft)

## 1. API 개요
- 서버: Spring Boot 기반 Java API 서버
- 통신 방식: REST API (JSON 포맷)

## 2. API 상세 목록
- PDF 업로드
- PDF 목록 조회
- PDF 삭제
- GIF 변환 요청
- 변환 상태 조회
- GIF 평가/피드백 입력

# 🗄️ DB 테이블 설계 (초안)

## 1. 주요 테이블
- pdf
- gif
- convert_history
- feedback

## 2. ERD 요약
- pdf 1 --- * gif
- pdf 1 --- * convert_history
- gif 1 --- * feedback
