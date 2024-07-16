---
title: Salesforce Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# [!DNL Salesforce]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 CRM 시스템에서 데이터 수집을 지원합니다. CRM 공급자에 대한 지원에는 [!DNL Salesforce]이(가) 포함됩니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## [!DNL Salesforce]에서 XDM으로 필드 매핑

[!DNL Salesforce]과(와) 플랫폼 간에 소스 연결을 설정하려면 [!DNL Salesforce] 소스 데이터 필드를 플랫폼으로 수집하기 전에 해당 대상 XDM 필드에 매핑해야 합니다.

[!DNL Salesforce] 데이터 세트와 플랫폼 간의 필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하세요.

- [연락처](../adobe-applications/mapping/salesforce.md#contact)
- [잠재 고객](../adobe-applications/mapping/salesforce.md#lead)
- [계정](../adobe-applications/mapping/salesforce.md#account)
- [기회](../adobe-applications/mapping/salesforce.md#opportunity)
- [영업 기회 연락처 역할](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [캠페인](../adobe-applications/mapping/salesforce.md#campaign)
- [캠페인 멤버](../adobe-applications/mapping/salesforce.md#campaign-member)
- [계정 연락처 관계](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## [!DNL Salesforce] 네임스페이스 및 스키마 자동 생성 유틸리티 설정

[!DNL Salesforce] 소스를 [!DNL B2B-CDP]의 일부로 사용하려면 먼저 [!DNL Postman] 유틸리티를 설정하여 [!DNL Salesforce] 네임스페이스 및 스키마를 자동 생성해야 합니다. 다음 설명서는 [!DNL Postman] 유틸리티 설정에 대한 추가 정보를 제공합니다.

- 이 [GitHub 저장소](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)에서 네임스페이스와 스키마 자동 생성 유틸리티 컬렉션 및 환경을 다운로드할 수 있습니다.
- 필요한 헤더에 대한 값을 수집하고 샘플 API 호출을 읽는 방법에 대한 세부 정보를 포함하여 Platform API 사용에 대한 자세한 내용은 [Platform API 시작하기](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.
- Platform API에 대한 자격 증명을 생성하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오.
- 플랫폼 API용 [!DNL Postman]을(를) 설정하는 방법에 대한 자세한 내용은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md)에 대한 자습서를 참조하십시오.

Platform 개발자 콘솔과 [!DNL Postman]을(를) 설정하면 이제 [!DNL Postman] 환경에 적절한 환경 값을 적용할 수 있습니다.

다음 표에는 예제 값과 [!DNL Postman] 환경 채우기에 대한 추가 정보가 포함되어 있습니다.

| 변수 | 설명 | 예 |
| --- | --- | --- |
| `CLIENT_SECRET` | `{ACCESS_TOKEN}`을(를) 생성하는 데 사용되는 고유 식별자입니다. `{CLIENT_SECRET}`을(를) 검색하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON 웹 토큰(JWT)은 {ACCESS_TOKEN}을(를) 생성하는 데 사용되는 인증 자격 증명입니다. `{JWT_TOKEN}`을(를) 생성하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `{JWT_TOKEN}` |
| `API_KEY` | Experience Platform API 호출을 인증하는 데 사용되는 고유 식별자입니다. `{API_KEY}`을(를) 검색하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰입니다. `{ACCESS_TOKEN}`을(를) 검색하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | [!DNL Marketo]과(와) 관련하여 이 값은 고정되어 있으며 항상 `ent_dataservices_sdk`(으)로 설정되어 있습니다. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | `global` 컨테이너에는 모든 표준 Adobe 및 Experience Platform 파트너가 제공한 클래스, 스키마 필드 그룹, 데이터 형식 및 스키마가 들어 있습니다. [!DNL Marketo]과(와) 관련하여 이 값은 고정되어 있으며 항상 `global`(으)로 설정됩니다. | `global` |
| `PRIVATE_KEY` | Experience Platform API에 대한 [!DNL Postman] 인스턴스를 인증하는 데 사용되는 자격 증명입니다. {PRIVATE_KEY}을(를) 검색하는 방법에 대한 지침은 개발자 콘솔 설정 및 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md)에 대한 자습서를 참조하십시오. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Adobe I/O에 통합하는 데 사용되는 자격 증명입니다. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | IMS(Identity Management System)는 Adobe 서비스에 인증을 위한 프레임워크를 제공합니다. [!DNL Marketo]과(와) 관련하여 이 값은 고정되어 있으며 항상 `ims-na1.adobelogin.com`(으)로 설정됩니다. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 제품 및 서비스를 소유하거나 라이선스를 부여하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인 엔티티입니다. `{ORG_ID}` 정보를 검색하는 방법에 대한 지침은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md)에 대한 자습서를 참조하십시오. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 사용 중인 가상 샌드박스 파티션의 이름입니다. | `prod` |
| `TENANT_ID` | 만든 리소스의 이름 간격이 제대로 지정되고 조직 내에 포함되어 있는지 확인하는 데 사용되는 ID입니다. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | API 호출을 수행하는 URL 엔드포인트. 이 값은 고정되어 있으며 항상 `http://platform.adobe.io/`(으)로 설정됩니다. | `http://platform.adobe.io/` |
| `munchkinId` | [!DNL Marketo] 계정의 고유 ID입니다. `munchkinId`을(를) 검색하는 방법에 대한 자세한 내용은 [인스턴스 인증 [!DNL Marketo] 에 대한 자습서를 참조하십시오.](../adobe-applications/marketo/marketo-auth.md) | `123-ABC-456` |
| `sfdc_org_id` | [!DNL Salesforce] 계정의 조직 ID입니다. [!DNL Salesforce] 조직 ID를 가져오는 방법에 대한 자세한 내용은 다음 [[!DNL Salesforce] 안내서](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)를 참조하십시오. | `00D4W000000FgYJUA0` |
| `has_abm` | [!DNL Marketo Account-Based Marketing]을(를) 구독하는지 여부를 나타내는 부울 값입니다. | `false` |
| `has_msi` | [!DNL Marketo Sales Insight]에 가입되어 있는지 여부를 나타내는 부울 값입니다. | `false` |

{style="table-layout:auto"}

### 스크립트 실행

[!DNL Postman] 컬렉션 및 환경이 설정되면 이제 [!DNL Postman] 인터페이스를 통해 스크립트를 실행할 수 있습니다.

[!DNL Postman] 인터페이스에서 자동 생성기 유틸리티의 루트 폴더를 선택한 다음 상단 헤더에서 **[!DNL Run]**&#x200B;을(를) 선택합니다.

![루트 폴더](../../images/tutorials/create/salesforce/root-folder.png)

[!DNL Runner] 인터페이스가 나타납니다. 여기에서 모든 확인란이 선택되었는지 확인한 다음 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**&#x200B;을(를) 선택하십시오.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

요청이 성공하면 Beta 사양에 따라 B2B 네임스페이스 및 스키마가 만들어집니다.

## API를 사용하여 [!DNL Salesforce]을(를) 플랫폼에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Salesforce]을(를) 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.

- [흐름 서비스 API를 사용하여 Salesforce 기본 연결 만들기](../../tutorials/api/create/crm/salesforce.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 CRM 소스의 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)

## UI를 사용하여 [!DNL Salesforce]을(를) 플랫폼에 연결

- [UI에서 Salesforce 소스 연결 만들기](../../tutorials/ui/create/crm/salesforce.md)
- [UI에서 CRM 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
