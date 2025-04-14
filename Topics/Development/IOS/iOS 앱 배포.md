
## 배포 준비

### Apple Developer Program 가입

- Apple Developer Program(연회비 $99)에 가입해야 함
- 개인 또는 기업 계정으로 등록 가능 (기업 계정은 D-U-N-S 번호 필요)
- 가입 링크: [Apple Developer Program](https://developer.apple.com/programs/)

### 필수 사항 체크리스트

- 최종 앱 바이너리
- 앱 아이콘 (여러 크기)
- 스크린샷 (iPhone 및 iPad 해상도별)
- 앱 설명 및 키워드
- 개인정보 처리방침 URL
- 지원 URL (고객 지원)
- 연령 등급 정보
- 앱 가격 정보

## App Store Connect 설정

### 새 앱 등록

1. [App Store Connect](https://appstoreconnect.apple.com/)에 로그인
2. '내 앱' 섹션으로 이동
3. '+' 버튼 클릭하여 새 앱 등록
4. 플랫폼, 앱 이름, 기본 언어, 번들 ID, SKU 입력
5. 사용자 접근 권한 및 역할 설정

### 앱 정보 입력

1. 앱 정보 탭으로 이동하여 기본 정보 입력
2. 스크린샷 및 앱 아이콘 업로드
3. 설명, 키워드, 지원 URL 추가
4. 앱의 연령 등급 및 카테고리 선택
5. 가격 및 판매 지역 설정
6. 개인정보 처리방침 URL 추가

## 앱 빌드 및 아카이브

### 인증서 및 프로파일 설정

1. Apple Developer 사이트에서 배포용 인증서 생성
2. 배포용 프로비저닝 프로파일 생성
3. Xcode에 인증서 및 프로파일 설치

### 빌드 및 아카이브

1. Xcode에서 프로젝트 열기
2. 'Generic iOS Device' 또는 실제 기기 선택
3. 'Product' > 'Archive' 선택하여 앱 아카이브
4. 필요한 경우 앱 버전 및 빌드 번호 업데이트

### TestFlight를 통한 테스트 (선택 사항)

1. 아카이브된 빌드를 TestFlight에 업로드
2. 내부 및 외부 테스터 초대
3. 피드백 수집 및 이슈 수정

## App Store에 제출

### 비트코드 및 앱 시닝 설정

1. 비트코드 포함 여부 결정 (권장)
2. 앱 시닝 활성화 여부 확인 (권장)

### 빌드 업로드 방법

1. Xcode Organizer에서 직접 업로드
    - 아카이브 후 'Distribute App' 선택
    - 'App Store Connect' 옵션 선택
    - 단계별 지침에 따라 진행
2. Application Loader 사용 (이전 방식)
    - .ipa 파일 생성 후 업로드

### 제출 정보 확인

1. App Store Connect에서 업로드된 빌드 확인
2. '앱 심사 제출 준비' 섹션의 모든 항목 완료
3. 앱 심사 제출 전 최종 확인

## 심사 프로세스

### 심사 가이드라인

- [App Store 심사 가이드라인](https://developer.apple.com/app-store/review/guidelines/) 숙지
- 자주 거부되는 사유 확인

### 심사 과정 모니터링

1. App Store Connect에서 심사 상태 확인
2. 일반적인 심사 소요 시간: 1-3일
3. 거부된 경우 Resolution Center에서 상세 내용 확인

### 거부 대응 방법

1. 거부 사유 정확히 파악
2. 필요한 수정 사항 반영
3. 재제출 또는 이의 제기

## 앱 출시

### 출시 옵션

1. 즉시 출시 (심사 통과 즉시)
2. 수동 출시 (승인 후 직접 릴리스)
3. 특정 날짜에 출시 (예약 출시)
4. 단계적 출시 (Phased Release)

### 출시 후 모니터링

1. App Analytics를 통한 다운로드 및 사용 현황 확인
2. 사용자 리뷰 및 평점 모니터링
3. 크래시 리포트 확인

## 배포 후 관리

### 업데이트 관리

1. 정기적인 업데이트 계획 수립
2. 버그 수정 및 신규 기능 추가
3. 앱 버전 및 빌드 번호 관리

### 인앱 구매 관리 (해당시)

1. 구독 및 인앱 구매 상태 모니터링
2. 가격 정책 수정 및 프로모션

### 사용자 피드백 대응

1. 리뷰에 응답
2. 자주 요청되는 기능 파악 및 반영
3. 부정적 리뷰에 대한 대응 전략

## 문제 해결

### 자주 발생하는 문제

1. 인증서 만료 및 갱신 문제
2. 프로비저닝 프로파일 오류
3. 업로드 실패
4. 심사 거부

### 해결 방법

1. Apple Developer Forums 참고
2. 개발자 문서 검토
3. Apple Developer Support에 문의

### 유용한 도구 및 리소스

1. Apple Developer 문서
2. Xcode Instruments
3. Fastlane (자동화 도구)
4. App Store Connect API

---

이 문서는 iOS 앱 배포에 관한 기본적인 가이드라인입니다. Apple의 정책과 절차는 변경될 수 있으므로, 항상 최신 [Apple Developer 문서](https://developer.apple.com/documentation/)를 참조하시기 바랍니다.