# Azure DevOps 주요 구성 요소

Azure DevOps는 Microsoft에서 제공하는 개발 도구 모음으로, 팀이 작업을 계획하고, 코드 개발에 협업하며, 애플리케이션을 빌드 및 배포할 수 있도록 도와줍니다. 다음은 Azure DevOps의 주요 구성 요소에 대한 상세 설명입니다.

## 1. Azure Boards

Azure Boards는 애자일([[Agile]]) 방법론을 지원하는 작업 관리 도구입니다.

### 주요 기능:

- **작업 항목 추적(Work Item Tracking)**: 버그, 작업, 사용자 스토리, 이슈 등을 생성하고 관리
- **스프린트 계획(Sprint Planning)**: 스프린트 기간 동안 수행할 작업 항목을 계획하고 할당
- **칸반 보드(Kanban Boards)**: 작업 상태를 시각적으로 표시하고 워크플로우 관리
- **백로그 관리(Backlog Management)**: 제품 백로그 및 스프린트 백로그 관리
- **대시보드 및 보고서(Dashboards & Reports)**: 프로젝트 진행 상황에 대한 시각적 보고서 제공

### 지원하는 애자일 프레임워크:

- Scrum
- Kanban
- Scrumban
- 기본 프로세스
- CMMI(Capability Maturity Model Integration) 프로세스

## 2. Azure Repos

Azure Repos는 소스 코드 관리를 위한 버전 제어 시스템입니다.

### 주요 기능:

- **Git 리포지토리**: 분산형 버전 제어 시스템인 Git을 통한 코드 관리
- **TFVC(Team Foundation Version Control)**: 중앙 집중식 버전 제어 옵션 지원
- **Pull Request**: 코드 리뷰 및 병합 프로세스 지원
- **브랜치 정책(Branch Policies)**: 코드 품질 및 협업 프로세스 제어
- **코드 검색(Code Search)**: 리포지토리 내 코드 검색 기능
- **무제한 프라이빗 리포지토리**: 개인 또는 팀만 접근 가능한 프라이빗 리포지토리 무제한 생성

### 코드 관리 기능:

- 브랜치 생성 및 관리
- 코드 변경 이력 추적
- 코드 변경사항 비교
- 충돌 해결(Conflict Resolution)

## 3. Azure Pipelines

Azure Pipelines는 지속적 통합(CI) 및 지속적 배포(CD)를 위한 자동화 도구입니다.

### 주요 기능:

- **지속적 통합(Continuous Integration)**: 코드 변경사항을 자동으로 빌드하고 테스트
- **지속적 배포(Continuous Deployment)**: 자동화된 배포 파이프라인 구성
- **다양한 플랫폼 지원**: Windows, Linux, macOS 등 다양한 운영 체제 지원
- **컨테이너 지원**: Docker 및 Kubernetes와의 통합
- **YAML 파이프라인**: 코드로서의 파이프라인(Pipeline as Code) 구현
- **릴리스 관리(Release Management)**: 여러 환경(개발, 테스트, 프로덕션 등)에 대한 릴리스 관리

### 통합 가능한 환경:

- 클라우드 서비스(Azure, AWS, GCP)
- 온프레미스 서버
- 다양한 언어 및 프레임워크(Node.js, Python, Java, .NET, PHP, Go 등)
- 다양한 배포 대상(VM, 컨테이너, 서버리스 등)

## 4. Azure Test Plans

Azure Test Plans는 소프트웨어 품질 보증을 위한 테스트 관리 도구입니다.

### 주요 기능:

- **수동 테스트 계획 및 실행**: 테스트 케이스 생성, 관리 및 실행
- **탐색적 테스트(Exploratory Testing)**: 구조화되지 않은 테스트 수행
- **자동화된 테스트 통합**: Selenium, JUnit, NUnit 등의 자동화 테스트 도구와 통합
- **부하 테스트(Load Testing)**: 애플리케이션의 성능 및 확장성 테스트
- **테스트 피드백(Test Feedback)**: 테스트 결과에 대한 피드백 수집 및 관리
- **결함 추적(Bug Tracking)**: 버그 발견 시 Azure Boards와 연동

### 테스트 관리 기능:

- 테스트 계획(Test Plans)
- 테스트 스위트(Test Suites)
- 테스트 케이스(Test Cases)
- 테스트 결과 분석 및 보고서

## 5. Azure Artifacts

Azure Artifacts는 패키지 관리 도구로, 팀이 코드 종속성을 공유하고 관리할 수 있게 해줍니다.

### 주요 기능:

- **패키지 리포지토리**: 개인 또는 조직 내 패키지 저장 및 공유
- **다양한 패키지 형식 지원**:
    - NuGet (.NET)
    - npm (JavaScript)
    - Maven (Java)
    - Python (PyPI)
    - Universal Packages
- **패키지 버전 관리**: 패키지의 다양한 버전 관리
- **업스트림 소스(Upstream Sources)**: 공용 패키지 리포지토리와 통합
- **권한 관리**: 패키지 접근 권한 제어

### 이점:

- 종속성 관리 간소화
- 패키지 보안 강화
- 빌드 프로세스 일관성 유지
- 외부 리포지토리 종속성 감소

## Azure DevOps 통합 및 확장성

Azure DevOps의 각 구성 요소는 서로 긴밀하게 통합되어 있으며, 다음과 같은 추가 기능도 제공합니다:

### 주요 통합 기능:

- **Azure Active Directory 통합**: 사용자 인증 및 권한 관리
- **확장 마켓플레이스**: 다양한 확장 프로그램을 통한 기능 확장
- **API 지원**: RESTful API를 통한 프로그래밍 방식의 접근
- **타사 도구 통합**: Slack, Microsoft Teams, Jenkins, Trello 등 다양한 도구와 통합
- **IDE 통합**: Visual Studio, VS Code, Eclipse 등의 개발 환경과 통합

### 배포 옵션:

- **Azure DevOps Services**: 클라우드 호스팅 버전
- **Azure DevOps Server**: 온프레미스 설치 버전

## 시작하기

Azure DevOps를 시작하기 위한 일반적인 단계:

1. Azure DevOps 조직 또는 서버 설정
2. 프로젝트 생성
3. 팀원 초대 및 권한 설정
4. 작업 항목 생성 및 스프린트 계획
5. 리포지토리 설정 및 코드 커밋
6. CI/CD 파이프라인 구성
7. 테스트 계획 수립
8. 패키지 리포지토리 설정

## 결론

Azure DevOps는 소프트웨어 개발 라이프사이클의 모든 단계를 지원하는 종합적인 도구 세트를 제공합니다. 각 구성 요소는 독립적으로 사용할 수 있지만, 함께 사용할 때 최대의 효과를 발휘합니다. 이를 통해 팀은 더 효율적으로 협업하고, 고품질의 소프트웨어를 더 빠르게 제공할 수 있습니다.