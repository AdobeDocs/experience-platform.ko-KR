---
title: Gen2로 데이터 레이크 마이그레이션
description: Data Lake를 Adobe Experience Platform의 Gen2로 마이그레이션하여 제공하는 새로운 기능에 대해 알아보십시오.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Gen2로 Adobe Experience Platform Data Lake 마이그레이션

Adobe Experience Platform은 Gen2 Data Lake로 마이그레이션하고 있습니다. 이는 지리적 영역 복제, RBAC(보다 세밀한 역할 기반 액세스 제어), 향상된 확장 기능 등 플랫폼 사용자에게 유용한 새로운 차원의 데이터 레이지입니다.

## 사용자 영향

Adobe이 Gen1에서 Gen 2로 Data Lake를 마이그레이션하는 동안 사용자는 데이터 레이크에서 **read**&#x200B;를 수행할 수 있지만, **write**&#x200B;가 Data Lake에 대한 모든 기능에 영향을 줍니다. 다음은 영향을 받는 기능 목록입니다.

- **소스**:소스 및 다양한 데이터 수집 워크플로우에서 들어오는 데이터는 지연됩니다. 마이그레이션이 완료되면 데이터가 표시됩니다.
- **쿼리 서비스**:사용자는 쿼리를 수행할 수 있지만 쿼리의 출력을 데이터 집합에 쓸 수 없습니다.
- **실시간 고객 프로필**:일괄 처리를 통해 프로필 저장소에  **** 수집된 데이터는 마이그레이션 중에 사용할 수 없습니다. 그러나 **스트리밍** 수집을 통해 수집된 데이터는 마이그레이션 중에 사용할 수 있습니다. 또한 마이그레이션 중에는 프로필 내보내기를 사용할 수 없습니다.
- **데이터 과학 작업 공간**:Data Science Workspace에서 쓴 내용은 실패합니다.
- **세분화 서비스**:마이그레이션 중에  **** 일괄 세그먼테이션에서 파생된 대상은 활성화할 수 없습니다. **스트리밍** 세그먼테이션에서 파생된 대상은 영향을 받지 않습니다.
- **Customer Journey Analytics**:배치가 Data Lake로 수집되지 않으므로 Customer Journey Analytics 보고서 데이터가 오래된 것일 수 있으며 마이그레이션 중에 새로 고쳐지지 않습니다.

## 플랫폼 사용자와의 통신

Adobe은 시스템 관리자에게 연락하여 마이그레이션의 영향을 자세히 설명하고 특정 IMS 조직의 마이그레이션 날짜 및 시간을 확인할 것입니다.
