---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: 액세스 제어 개요
description: Adobe Experience Platform에 대한 액세스 제어는 Adobe Admin Console을 통해 제공됩니다. 이 기능은 Admin Console의 제품 프로필을 활용하므로 사용자에게 사용 권한 및 샌드박스를 연결합니다.
translation-type: tm+mt
source-git-commit: ccb7286e47aa4cf6356d22f84111b0c0fb30dfa8
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 3%

---


# 액세스 제어 개요

액세스 제어 [!DNL Experience Platform] 는 [Adobe Admin Console을 통해 제공됩니다](https://adminconsole.adobe.com). 이 기능은 사용 권한 및 샌드박스 [!DNL Admin Console]와 사용자를 연결하는 제품 프로필을 활용합니다.

## 액세스 제어 계층 구조 및 워크플로우

에 대한 액세스 제어를 구성하려면 [!DNL Experience Platform]제품 통합이 있는 조직에 대한 관리자 권한이 있어야 [!DNL Experience Platform] 합니다. 권한을 부여하거나 해지하는 최소 역할은 제품 프로필 관리자입니다. 권한을 관리할 수 있는 다른 관리자 역할은 제품 관리자(제품 내의 모든 프로필을 관리할 수 있음)와 시스템 관리자입니다(제한 없음). 자세한 내용은 [관리자 역할에](https://helpx.adobe.com/enterprise/using/admin-roles.html) 대한 Adobe Help Center 문서를 참조하십시오.

>[!NOTE]
>
>이 시점부터 이 문서의 &quot;관리자&quot;에 대한 모든 언급 내용은 제품 프로필 관리자 이상(위에 설명된 대로)을 참조합니다.

액세스 권한을 획득하고 할당하는 고급 작업 과정은 다음과 같이 요약할 수 있습니다.

- Adobe Experience Platform 또는 Experience Platform을 사용하는 응용 프로그램/응용 프로그램 서비스에 라이선스를 부여하면 라이선스 동안 지정된 관리자에게 이메일이 전송됩니다.
- 관리자는 [Adobe Admin Console](#adobe-admin-console) 에 로그인하여 개요 페이지의 제품 목록에서 **Adobe Experience Platform** 를 선택합니다.
- 관리자는 기본 [제품 프로필을](#product-profiles) 보거나 필요에 따라 새 고객 제품 프로필을 만들 수 있습니다.
- 관리자는 기존 제품 프로필에 대한 권한 및 사용자를 편집할 수 있습니다.
- 제품 프로필을 만들거나 편집할 때 관리자는 **[!UICONTROL 사용자]** 탭을 사용하여 프로필에 사용자를 추가하고 권한 탭에 액세스하여 이러한 사용자(&quot;[!UICONTROL 데이터 세트]읽기[!UICONTROL &quot; 또는 &quot;스키마]관리 **[!UICONTROL &quot;와 같은)에게]** 권한탭에 액세스하여 권한을 부여합니다. 마찬가지로 관리자는 동일한 권한 탭을 사용하여 샌드박스에 대한 액세스 권한을 할당할 수 있습니다.
- 사용자가 [!DNL Experience Platform] 사용자 인터페이스에 로그인하면 기능에 대한 [!DNL Platform] 액세스 권한은 2단계에서 사용자에게 부여된 권한에 의해 결정됩니다. 예를 들어 사용자에게 &quot;데이터 집합[!UICONTROL 보기]&quot; 권한이 없는 경우, 측면 메뉴의 **[!UICONTROL 데이터 집합]** 탭이 해당 사용자에게 표시되지 않습니다.

액세스 제어 관리 방법에 대한 자세한 단계 [!DNL Experience Platform]는 [액세스 제어 사용 안내서를 참조하십시오](./ui/overview.md).

API에 대한 모든 [!DNL Experience Platform] 호출은 권한에 대해 유효성이 검사되며, 현재 사용자 컨텍스트에서 적절한 권한이 없으면 오류를 반환합니다. UI 내에서 요소는 현재 사용자에게 부여된 권한에 따라 숨겨지거나 변경됩니다.

## Adobe Admin Console

Adobe Admin Console은 Adobe 제품 이용 권한 및 조직의 이용 권한을 중앙에서 관리할 수 있습니다. 콘솔을 통해 &quot;데이터 세트 [!DNL Platform] 관리&quot;, &quot;데이터 세트[!UICONTROL 보기&quot;, &quot;]프로필[!UICONTROL 관리&quot;와 같은 다양한 기능에 대한 액세스 권한을 사용자 그룹에 부여할 수]있습니다.

### 제품 프로필

에서 [!DNL Admin Console]는 제품 프로필 사용을 통해 사용자에게 권한이 할당됩니다. 제품 프로필을 사용하면 한 명 또는 여러 사용자에게 권한을 부여할 수 있으며 제품 프로필을 통해 사용자에게 할당된 샌드박스 범위에 대한 액세스 권한을 포함할 수 있습니다. 사용자를 조직에 속한 하나 이상의 제품 프로필에 할당할 수 있습니다.

### 기본 제품 프로필

[!DNL Experience Platform] 에는 두 개의 사전 구성된 기본 제품 프로필이 포함되어 있습니다. 다음 표에서는 해당 샌드박스의 범위에서 부여하는 권한 및 액세스 권한을 부여하는 샌드박스를 비롯하여 각 기본 프로파일에서 제공되는 사항에 대해 설명합니다.

| 제품 프로필 | 샌드박스 액세스 | 권한 |
| --- | --- | --- |
| 기본 프로덕션 - 모든 액세스 | 프로덕션 | Sandbox 관리 권한을 [!DNL Experience Platform]제외한 모든 권한 |
| 기본 샌드박스 관리 | N/A | 샌드박스 관리 권한에 대해서만 액세스를 제공합니다. |

## 샌드박스 및 권한

비프로덕션 샌드박스는 다른 샌드박스에서 데이터를 격리할 수 있는 데이터 가상화의 한 형태이며 일반적으로 개발 실험, 테스트 또는 시험버전에 사용됩니다. 제품 프로필의 권한은 프로파일의 사용자에게 액세스 권한이 부여된 샌드박스 환경 내의 기능에 대한 액세스 권한을 부여합니다. [!DNL Platform] 기본 Experience Platform 라이선스는 5개의 샌드박스(1개의 프로덕션과 4개의 비프로덕션)를 제공합니다. 비프로덕션 샌드박스 10개 팩을 총 75개의 샌드박스에 추가할 수 있습니다. 자세한 내용은 IMS 조직 관리자 또는 Adobe 영업 담당자에게 문의하십시오.

샌드박스에 대한 자세한 내용 [!DNL Experience Platform]은 [샌드박스 개요를 참조하십시오](../sandboxes/home.md).

### 샌드박스 액세스

샌드박스 액세스는 제품 프로필을 통해 관리됩니다. 제품 프로필의 샌드박스에 대한 액세스를 활성화하는 방법에 대한 자세한 내용은 [액세스 제어 사용 안내서를 참조하십시오](./ui/overview.md).

사용자는 제품 프로필 내에서 하나 이상의 샌드박스에 대한 액세스 권한을 부여할 수 있습니다. 한 사용자가 두 개 이상의 제품 프로필에 포함되어 있는 경우 해당 사용자는 해당 프로필에 포함된 모든 샌드박스에 액세스할 수 있습니다.

&quot;샌드박스 관리&quot; 권한을 사용하면 샌드박스를 관리, 보기 또는 재설정할 수 있습니다.

### 권한

제품 프로필 내의 권한 탭에는 해당 프로필에 대해 활성화된 샌드박스 및 권한이 표시됩니다.

![permissions-overview](./images/permissions-overview.png)

여러 가지 하위 수준 기능에 대한 액세스 권한을 부여하는 일부 권한과 함께, 이 [!DNL Admin Console] 를 통해 부여된 권한은 범주별로 정렬됩니다.

다음 표에서는 액세스 권한을 부여하는 특정 기능 [!DNL Experience Platform] 에 대한 사용 가능한 권한에 [!DNL Admin Console]대해 설명하고 [!DNL Platform] 있습니다. 제품 프로필에 권한을 추가하는 방법에 대한 자세한 내용은 [액세스 제어 사용 안내서를 참조하십시오](./ui/overview.md).

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 스키마 관리] | 스키마 및 관련 리소스를 읽고, 생성, 편집 및 삭제할 수 있습니다. |
| [!DNL Data Modeling] | [!UICONTROL 스키마 보기] | 스키마 및 관련 리소스에 대한 읽기 전용 액세스 |
| [!DNL Data Modeling] | [!UICONTROL 관계 관리] | 스키마 관계를 읽기, 생성, 편집 및 삭제할 수 있는 액세스 권한 |
| [!DNL Data Modeling] | [!UICONTROL ID 메타데이터 관리] | 스키마에 대한 ID 메타데이터를 읽고 생성, 편집 및 삭제할 수 있는 액세스 권한 |
| [!DNL Data Management] | [!UICONTROL 데이터 세트 관리] | 데이터 세트를 읽고, 생성, 편집 및 삭제할 수 있습니다. 스키마에 대한 읽기 전용 액세스 |
| [!DNL Data Management] | [!UICONTROL 데이터 세트 보기] | 데이터 집합 및 스키마에 대한 읽기 전용 액세스 |
| [!DNL Data Management] | [!UICONTROL 데이터 모니터링] | 데이터 세트 및 스트림 모니터링을 위한 읽기 전용 액세스 |
| [!DNL Profile Management] | [!UICONTROL 프로필 관리] | 고객 프로파일에 사용되는 데이터 세트를 읽고, 작성하고, 편집하고, 삭제할 수 있습니다. 사용 가능한 프로파일에 대한 읽기 전용 액세스 |
| [!DNL Profile Management] | [!UICONTROL 프로필 보기] | 사용 가능한 프로파일에 대한 읽기 전용 액세스 |
| [!DNL Profile Management] | [!UICONTROL 세그먼트 관리] | 세그먼트를 읽고, 만들고, 편집하고, 삭제할 수 있습니다. |
| [!DNL Profile Management] | [!UICONTROL 세그먼트 보기] | 사용 가능한 세그먼트에 대한 읽기 전용 액세스. |
| [!DNL Profile Management] | [!UICONTROL 병합 정책 관리] | 병합 정책을 읽고, 만들고, 편집하고, 삭제할 수 있습니다. |
| [!DNL Profile Management] | [!UICONTROL 병합 정책 보기] | 사용 가능한 병합 정책에 대한 읽기 전용 액세스 |
| [!DNL Profile Management] | [!UICONTROL 세그먼트에 대한 대상 내보내기] | 평가된 대상 세그먼트를 데이터 세트로 내보내는 기능 |
| [!DNL Profile Management] | [!UICONTROL 대상에 세그먼트 평가] | 세그먼트 정의를 평가하여 대상에 대한 프로파일을 생성하는 기능 |
| [!DNL Identities] | [!UICONTROL ID 네임스페이스 관리] | ID 네임스페이스를 읽고, 만들고, 편집하고, 삭제할 수 있습니다. |
| [!DNL Identities] | [!UICONTROL ID 네임스페이스 보기] | ID 네임스페이스에 대한 읽기 전용 액세스 |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 관리] | 샌드박스를 읽고, 만들고, 편집하고, 삭제할 수 있습니다. |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 보기] | 조직에 속하는 샌드박스에 대한 읽기 전용 액세스 |
| [!DNL Sandbox Administration] | [!UICONTROL 샌드박스 재설정] | 샌드박스를 재설정하는 기능 |
| [!DNL Destinations] | [!UICONTROL 대상 관리] | 대상을 읽고, 만들고, 편집하고, 비활성화하는 액세스 권한* |
| [!DNL Destinations] | [!UICONTROL 대상 보기] | [카탈로그] 탭 및 [찾아보기] 탭 **[!UICONTROL 의 인증된 대상]** 및 사용 가능한 대상에 대한 읽기 전용 **[!UICONTROL 액세스]** .* |
| [!DNL Destinations] | [!UICONTROL 대상 활성화] | 활성화된 대상에 데이터를 활성화하는 기능 이 권한을 사용하려면 대상을 활성화할 사용자에게 &quot;대상 보기&quot; 또는 &quot; [!UICONTROL 대상] 관리&quot;가 부여되어야 합니다.* |
| [!DNL Data Ingestion] | [!UICONTROL 소스 관리] | 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있습니다. |
| [!DNL Data Ingestion] | [!UICONTROL 소스 보기] | [카탈로그] 탭의 사용 가능한 소스 및 [ **[!UICONTROL 찾아보기]** ] **[!UICONTROL 탭의 인증된 소스에 대한 읽기 전용]** 액세스. |
| [!DNL Data Science Workspace] | [!UICONTROL 데이터 과학 작업 공간 관리] | 액세스 권한을 사용하여 내용을 읽고, 만들고, 편집하고, 삭제할 수 [!DNL Data Science Workspace]있습니다. |
| [!DNL Data Governance] | [!UICONTROL 데이터 사용 레이블 적용] | 사용 레이블을 읽고, 만들고, 삭제할 수 있습니다. |
| [!DNL Data Governance] | [!UICONTROL 데이터 사용 정책 관리] | 데이터 사용 정책을 읽고, 작성하고, 편집하고, 삭제할 수 있는 액세스 권한 |
| [!DNL Data Governance] | [!UICONTROL 데이터 사용 정책 보기] | 조직에 속하는 데이터 사용 정책에 대한 읽기 전용 액세스 |
| [!DNL Query Service] | [!UICONTROL 쿼리 관리] | 플랫폼 데이터에 대한 구조화된 SQL 쿼리를 읽고, 작성하고, 편집하고, 삭제할 수 있는 액세스 권한 |

_(*) 이 권한을 사용하려면 [!DNL Real-time Customer Data Platform] 실시간 CDP에 대한 자세한 내용은 [실시간 CDP 개요를 읽어 보시기 바랍니다](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)._

## 다음 단계

이 가이드를 읽고 액세스 제어의 주요 원칙을 소개했습니다 [!DNL Experience Platform]. 이제 액세스 제어 사용 [가이드로](./ui/overview.md) 계속 이동하여 제품 프로필을 만들고 사용 권한을 할당하는 방법에 대한 자세한 단계를 [!DNL Admin Console] 수행할 수 [!DNL Platform]있습니다.