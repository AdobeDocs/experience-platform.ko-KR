---
title: Adobe Experience Platform 릴리스 노트 2021년 10월
description: Adobe Experience Platform의 2021년 10월 릴리스 정보.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 10월 27일**

## Experience Platform 업데이트

Experience Platform 업데이트.

### 사용자 인터페이스 {#ui}

사용자 인터페이스가 다음과 같은 변경 사항으로 업데이트되었습니다.

| 기능 | 설명 |
| --- | --- |
| 어두운 테마 | Platform 인터페이스의 밝은 테마와 어두운 테마 사이를 전환하려면 어두운 테마 스위치를 사용하십시오. 스위치는 사용자 이름 및 이메일 아래의 사용자 프로필에 있습니다. |
| 왼쪽 탐색 전환 | 애플리케이션 헤더 상단에 있는 향상된 탐색 토글을 사용하여 Experience Platform 기능을 표시하는 메뉴를 표시하거나 숨깁니다. 시스템은 마지막 선택을 기억하고 액세스 권한이 있는 기능만 표시합니다. |
| 액세스 가시성 | 왼쪽 탐색 모음에는 액세스할 수 있는 기능만 표시됩니다. 이전 버전의 Adobe Experience Platform에서는 액세스할 수 없는 경우에도 사용할 수 없는 항목이 표시되었습니다. |

다음을 참조하십시오. [Platform UI 안내서](../../landing/ui-guide.md) 자세히 알아보십시오.

## 기존 기능 업데이트

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [소스](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어를 통해 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| `contains_key` 함수 위에 있어야 합니다 | 다음 `contains_key` 소스 내에 개체가 있는지 확인할 수 있는 함수가 도입되었습니다. 이 함수는 `is_set` 함수, 이제 더 이상 사용되지 않습니다. |
| 오류 메시지 | 에서 반환한 오류 메시지 `/mappingSets/preview` 이제 데이터 준비 API의 끝점이 런타임 중에 생성되는 오류 메시지와 일치합니다. |

다음을 참조하십시오. [[!DNL Data Prep] 개요](../../data-prep/home.md) 을(를) 참조하십시오.

### 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| [!DNL Amazon S3] 소스 개선 사항 | 이제 다음을 사용할 수 있습니다. `s3SessionToken` 연결할 매개 변수 [!DNL Amazon S3] 임시 보안 자격 증명을 사용하여 Platform에 연결합니다. 이 토큰을 사용하면 에 대한 단기, 임시 액세스를 제공할 수 있습니다. [!DNL Amazon S3] 신뢰할 수 없는 환경의 사용자에게 리소스를 제공합니다. 자세한 내용은 [[!DNL Amazon S3] 설명서](../../sources/connectors/cloud-storage/s3.md#prerequisites)를 참조하십시오. |
| [!DNL Generic REST API] (베타) | 이제 다음을 만들 수 있습니다 [!DNL Generic REST API] 를 사용한 소스 연결 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 일반 REST 응용 프로그램에서 플랫폼으로 데이터를 가져옵니다. 다음을 참조하십시오. [[!DNL Generic REST API] 개요](../../sources/connectors/protocols/generic-rest.md) 추가 정보. |
| [!DNL Zoho CRM] (베타) | 이제 다음을 만들 수 있습니다 [!DNL Zoho CRM] 를 사용한 소스 연결 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 또는 [사용자 인터페이스](../../sources/tutorials/ui/create/crm/zoho.md) 에서 데이터를 가져오려면 [!DNL Zoho CRM] 계정을 플랫폼에 추가합니다. 다음을 참조하십시오. [[!DNL Zoho CRM] 개요](../../sources/connectors/crm/zoho.md) 추가 정보. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
