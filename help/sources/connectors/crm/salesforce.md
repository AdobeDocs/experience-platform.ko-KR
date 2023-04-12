---
keywords: Experience Platform;홈;인기 항목;crm 스키마;crm;CRM;salesforce;Salesforce
solution: Experience Platform
title: Salesforce 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# [!DNL Salesforce] 커넥터

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 CRM 시스템에서 데이터 섭취를 지원합니다. CRM 공급자를 지원하는 기능은 다음과 같습니다 [!DNL Salesforce].

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 필드 매핑 위치 [!DNL Salesforce] XDM으로

소스 연결을 설정하려면 [!DNL Salesforce] 및 플랫폼, [!DNL Salesforce] 소스 데이터 필드를 Platform으로 수집하기 전에 적절한 대상 XDM 필드에 매핑해야 합니다.

필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하십시오 [!DNL Salesforce] 데이터 세트 및 플랫폼:

- [연락처](../adobe-applications/mapping/salesforce.md#contact)
- [리드](../adobe-applications/mapping/salesforce.md#lead)
- [계정](../adobe-applications/mapping/salesforce.md#account)
- [기회](../adobe-applications/mapping/salesforce.md#opportunity)
- [기회 연락처 역할](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [캠페인](../adobe-applications/mapping/salesforce.md#campaign)
- [캠페인 구성원](../adobe-applications/mapping/salesforce.md#campaign-member)
- [계정 연락처 관계](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## 설정 [!DNL Salesforce] 네임스페이스 및 스키마 자동 생성 유틸리티

를 사용하려면 [!DNL Salesforce] 의 일부로 소스 [!DNL B2B-CDP], 먼저 [!DNL Postman] 자동 생성 유틸리티 [!DNL Salesforce] 네임스페이스 및 스키마. 다음 설명서에서는 [!DNL Postman] 유틸리티:

- 여기에서 네임스페이스 및 스키마 자동 생성 유틸리티 컬렉션 및 환경을 다운로드할 수 있습니다 [GitHub 리포지토리](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 필수 헤더에 대한 값을 수집하고 샘플 API 호출을 읽는 방법에 대한 자세한 내용을 포함하여 플랫폼 API 사용에 대한 자세한 내용은 다음 안내서를 참조하십시오 [플랫폼 API 시작](../../../landing/api-guide.md).
- Platform API용 자격 증명을 생성하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md).
- 설정 방법에 대한 자세한 내용 [!DNL Postman] 플랫폼 API의 경우 다음 위치에서 자습서를 참조하십시오. [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md).

플랫폼 개발자 콘솔 사용 및 [!DNL Postman] 을 설정하고, 이제 적절한 환경 값을 [!DNL Postman] 환경.

다음 표에는 예제 값과 [!DNL Postman] 환경:

| 변수 | 설명 | 예 |
| --- | --- | --- |
| `CLIENT_SECRET` | 를 생성하는 데 사용되는 고유 식별자입니다 `{ACCESS_TOKEN}`. 다음에서 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 을 검색하는 방법에 대한 자세한 내용은 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON 웹 토큰(JWT)은 {ACCESS_TOKEN}을 생성하는 데 사용되는 인증 자격 증명입니다. 다음에서 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 를 생성하는 방법에 대한 자세한 내용을 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Experience Platform API에 대한 호출을 인증하는 데 사용되는 고유 식별자입니다. 다음에서 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 을 검색하는 방법에 대한 자세한 내용은 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰. 다음에서 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 을 검색하는 방법에 대한 자세한 내용은 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 와 관련하여 [!DNL Marketo]로 설정되면 이 값은 고정되며 항상 다음으로 설정됩니다. `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 다음 `global` 컨테이너에는 모든 표준 Adobe 및 Experience Platform 파트너가 제공하는 클래스, 스키마 필드 그룹, 데이터 유형 및 스키마가 있습니다. 와 관련하여 [!DNL Marketo]이면 이 값이 고정되고 항상 로 설정됩니다 `global`. | `global` |
| `PRIVATE_KEY` | 인증을 위해 사용되는 자격 증명 [!DNL Postman] Experience Platform API에 대한 인스턴스. 개발자 콘솔 설정에 대한 튜토리얼 및 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md) {PRIVATE_KEY}을(를) 검색하는 방법에 대한 지침은 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Adobe I/O에 통합하는 데 사용되는 자격 증명입니다. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | IMS(Identity Management 시스템)는 Adobe 서비스에 대한 인증을 위한 프레임워크를 제공합니다. 와 관련하여 [!DNL Marketo]로 설정되면 이 값은 고정되며 항상 다음으로 설정됩니다. `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 제품 및 서비스를 소유하거나 라이센스를 부여하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인. 다음에서 자습서를 참조하십시오. [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md) 을 검색하는 방법에 대한 지침 `{ORG_ID}` 정보. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 사용 중인 가상 샌드박스 파티션의 이름입니다. | `prod` |
| `TENANT_ID` | 사용자가 만드는 리소스가 제대로 식별되고 조직 내에 포함되어 있는지 확인하는 데 사용되는 ID입니다. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | API를 호출하는 URL 끝점입니다. 이 값은 고정되며 항상 다음으로 설정됩니다. `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | 에 대한 고유 ID입니다 [!DNL Marketo] 계정이 필요합니다. 다음에서 자습서를 참조하십시오. [인증 [!DNL Marketo] 인스턴스](../adobe-applications/marketo/marketo-auth.md) 을 검색하는 방법에 대한 자세한 내용은 `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | 조직의 조직 ID입니다 [!DNL Salesforce] 계정이 필요합니다. 다음을 참조하십시오 [[!DNL Salesforce] 안내서](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) 자세한 내용은 [!DNL Salesforce] 조직 ID. | `00D4W000000FgYJUA0` |
| `has_abm` | 구독 여부를 나타내는 부울 값 [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | 이 등록 여부를 나타내는 부울 값 [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### 스크립트 실행

사용 [!DNL Postman] 이제 를 통해 스크립트를 실행할 수 있습니다 [!DNL Postman] 인터페이스.

에서 [!DNL Postman] 인터페이스를 사용하여 자동 생성 유틸리티의 루트 폴더를 선택한 다음 **[!DNL Run]** 상단 헤더에서

![루트 폴더](../../images/tutorials/create/salesforce/root-folder.png)

다음 [!DNL Runner] 인터페이스가 표시됩니다. 여기에서 모든 확인란을 선택한 다음 선택합니다 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![실행 생성기](../../images/tutorials/create/salesforce/run-generator.png)

요청이 성공하면 베타 사양에 따라 B2B 네임스페이스 및 스키마를 만듭니다.

## Connect [!DNL Salesforce] API를 사용하여 플랫폼 구현

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Salesforce] API 또는 사용자 인터페이스를 사용하여 플랫폼:

- [Flow Service API를 사용하여 Salesforce 기본 연결 만들기](../../tutorials/api/create/crm/salesforce.md)
- [Flow Service API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [Flow Service API를 사용하여 CRM 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)

## Connect [!DNL Salesforce] UI를 사용하여 플랫폼 구현

- [UI에서 Salesforce 소스 연결 만들기](../../tutorials/ui/create/crm/salesforce.md)
- [UI에서 CRM 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
