---
audience: user
user-guide-title: Adobe Experience Platform ID 서비스
breadcrumb-title: Platform Identity Service 안내서
user-guide-description: 다양한 디바이스와 시스템에서 고객 ID를 연결하여 개인화된 디지털 경험을 전달할 수 있습니다.
feature: Identities
role: Admin,Developer
source-git-commit: cbdfa76d546be631a8c1fa588896648835d2a159
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 30%

---


# Adobe Experience Platform ID 서비스 {#identity}

- [ID 서비스 개요](home.md)
- [ID 서비스 및 실시간 고객 프로필](identity-and-profile.md)
- 기능 {#features}
   - [ID 네임스페이스](./features/namespaces.md)
   - [ID 연결 논리](./features/identity-linking-logic.md)
   - [ID 그래프 뷰어](./features/identity-graph-viewer.md)
   - [ID 서비스에서 삭제](./features/deletion.md)
   - ID 그래프 연결 규칙 {#identity-graph-linking-rules}
      - [기능 개요](./identity-graph-linking-rules/overview.md)
      - [ID 최적화 알고리즘](./identity-graph-linking-rules/identity-optimization-algorithm.md)
      - [ID 그래프 연결 규칙에 대한 구현 안내서](./identity-graph-linking-rules/implementation-guide.md)
      - [그래프 구성 예](./identity-graph-linking-rules/example-configurations.md)
      - [ID 그래프 연결 규칙 문제 해결](./identity-graph-linking-rules/troubleshooting.md)
      - [네임스페이스 우선순위](./identity-graph-linking-rules/namespace-priority.md)
      - [그래프 시뮬레이션 UI](./identity-graph-linking-rules/graph-simulation.md)
      - [ID 설정 UI](./identity-graph-linking-rules/identity-settings-ui.md)
   - [ECID 개요](./features/ecid.md)
- [구현 안내서](implementation.md)
- [ID 데이터 보호](guardrails.md)
- ID 서비스 API {#api}
   - [시작하기](api/getting-started.md)
   - [필드에 ID 레이블 지정](api/label-identities.md)
   - [클러스터 ID 나열](api/list-cluster-identites.md)
   - [ID 클러스터 내역 나열](api/list-cluster-history.md)
   - [목록 ID 매핑](api/list-identity-mappings.md)
   - [사용 가능한 네임스페이스 나열](api/list-namespaces.md)
   - [사용자 지정 네임스페이스 만들기](api/create-custom-namespace.md)
   - [ID에 대한 기본 ID 나열](api/list-native-id.md)
   - [API 참조](https://www.adobe.io/experience-platform-apis/references/identity-service)
- [UI에서 ID 필드 정의](label-identities.md)
- [개인 정보 보호 요청 처리](privacy.md)
- [문제 해결 안내서](troubleshooting-guide.md)
- [플랫폼 릴리스 정보](https://experienceleague.adobe.com/ko/docs/experience-platform/release-notes/latest)