---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
source-git-commit: f4e9750685d641c83b4ceed79af739de43343aef
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 9%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 10월 27일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [소스](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| `contains_key` 함수 위에 있어야 합니다 | 다음 `contains_key` 함수가 도입되어 개체가 소스 내에 있는지 확인할 수 있습니다. 이 함수는 `is_set` 함수 위에 있어야 합니다. |
| 오류 메시지 | 에서 반환한 오류 메시지 `/mappingSets/preview` 이제 데이터 준비 API의 엔드포인트는 런타임 중에 생성된 오류 메시지와 일치합니다. |

자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md) 이 서비스에 대해 자세히 알아보십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| [!DNL Amazon S3] 소스 개선 사항 | 이제 를 사용할 수 있습니다 `s3SessionToken` 연결할 매개 변수 [!DNL Amazon S3] 임시 보안 자격 증명을 사용하여 Platform에 계정을 설정합니다. 이 토큰을 사용하면 다음에 대한 단기 임시 액세스를 제공할 수 있습니다 [!DNL Amazon S3] 신뢰할 수 없는 환경의 사용자에게 리소스를 제공합니다. 자세한 내용은 [[!DNL Amazon S3] 설명서](../../sources/connectors/cloud-storage/s3.md#prerequisites) 추가 정보. |
| [!DNL Generic REST API] (베타) | 이제 다음을 만들 수 있습니다 [!DNL Generic REST API] 소스 연결 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 또는 [사용자 인터페이스](../../sources/tutorials/ui/create/protocols/generic-rest.md) 일반 REST 애플리케이션에서 플랫폼으로 데이터를 가져올 수 있습니다. 자세한 내용은 [[!DNL Generic REST API] 개요](../../sources/connectors/protocols/generic-rest.md) 추가 정보. |
| [!DNL Zoho CRM] (베타) | 이제 다음을 만들 수 있습니다 [!DNL Zoho CRM] 소스 연결 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 또는 [사용자 인터페이스](../../sources/tutorials/ui/create/crm/zoho.md) 데이터를에서 [!DNL Zoho CRM] Platform에 계정을 설정합니다. 자세한 내용은 [[!DNL Zoho CRM] 개요](../../sources/connectors/crm/zoho.md) 추가 정보. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
