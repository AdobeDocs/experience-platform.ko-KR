---
title: Adobe Experience Platform의 고객 관리 키
description: Adobe Experience Platform에 저장된 데이터에 대한 자체 암호화 키를 설정하는 방법에 대해 알아봅니다.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 930c786db51063c55f731dc90f2ee66e98624555
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---

# Adobe Experience Platform의 고객 관리 키

Adobe Experience Platform에 저장된 데이터는 시스템 수준 키를 사용하여 사용하지 않을 때 암호화됩니다. 플랫폼 위에 구축된 애플리케이션을 사용하는 경우 자체 암호화 키를 대신 사용하도록 선택할 수 있으므로 데이터 보안을 보다 세밀하게 제어할 수 있습니다.

>[!NOTE]
>
>Adobe Experience Platform 데이터 레이크 및 프로필 저장소의 데이터는 CMK를 사용하여 암호화됩니다. 이는 기본 데이터 저장소로 간주됩니다.

이 문서에서는 Platform에서 CMK(고객 관리 키) 기능을 활성화하는 프로세스에 대한 높은 수준의 개요와 이러한 단계를 완료하는 데 필요한 사전 요구 사항 정보를 제공합니다.

>[!NOTE]
>
>Customer Journey Analytics 고객의 경우 [Customer Journey Analytics 설명서](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=en).

## 전제 조건

을(를) 보고 방문하려면 [!UICONTROL 암호화] Adobe Experience Platform의 섹션에서 역할을 만들고 [!UICONTROL 고객 관리 키 관리] 해당 역할에 대한 권한. 을(를) 가진 모든 사용자 [!UICONTROL 고객 관리 키 관리] 권한은 해당 조직에 대해 CMK를 활성화할 수 있습니다.

Experience Platform에서 역할 및 권한 할당에 대한 자세한 내용은 [권한 구성 설명서](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

CMK를 활성화하려면 [!DNL Azure] Key Vault는 다음 설정으로 구성해야 합니다.

* [제거 보호 활성화](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [일시 삭제 활성화](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [다음을 사용하여 액세스 구성 [!DNL Azure] 역할 기반 액세스 제어](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

프로세스를 더 잘 이해하려면 연결된 설명서를 읽어 보십시오.

## 프로세스 요약 {#process-summary}

CMK는 Adobe의 Healthcare Shield 및 Privacy and Security Shield 오퍼링에 포함되어 있습니다. 조직에서 이러한 서비스 중 하나에 대한 라이선스를 구입한 후 해당 기능을 설정하는 프로세스를 한 번 시작할 수 있습니다.

>[!WARNING]
>
>CMK를 설정한 후에는 시스템 관리 키로 되돌릴 수 없습니다. 키를 안전하게 관리하고 내에서 Key Vault, Key 및 CMK 앱에 대한 액세스 권한을 제공해야 합니다. [!DNL Azure] 데이터에 대한 액세스 권한을 잃지 않도록 합니다.

프로세스는 다음과 같습니다.

1. [구성 [!DNL Azure] 주요 자격 증명 모음](./azure-key-vault-config.md) 조직의 정책을 기반으로 다음을 수행합니다. [암호화 키 생성](./azure-key-vault-config.md#generate-a-key) 궁극적으로 Adobe과 공유됩니다.
1. 로 CMK 앱 설정 [!DNL Azure] 다음 중 하나를 통한 임차인 [API 호출](./api-set-up.md#register-app) 또는 [UI](./ui-set-up.md#register-app).
1. 암호화 키 ID를 Adobe에 보내고 기능 활성화 프로세스를 시작하십시오. [UI에서](./ui-set-up.md#send-to-adobe) 또는 [API 호출](./api-set-up.md#send-to-adobe).
1. 구성 상태를 확인하여 CMK가 활성화되었는지 확인합니다. [UI에서](./ui-set-up.md#check-status) 또는 [API 호출](./api-set-up.md#check-status).

설정 프로세스가 완료되면 모든 샌드박스에서 Platform에 온보딩된 모든 데이터는 [!DNL Azure] 키 설정. CMK를 사용하려면 [!DNL Microsoft Azure] 해당 기능에 속할 수 있는 기능 [공개 미리 보기 프로그램](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## 액세스 취소 {#revoke-access}

데이터에 대한 Platform 액세스를 취소하려는 경우 내의 키 저장소에서 애플리케이션과 연결된 사용자 역할을 제거할 수 있습니다 [!DNL Azure].

>[!WARNING]
>
>Key Vault, Key 또는 CMK 앱을 비활성화하면 변경 사항이 중단될 수 있습니다. Key Vault, Key 또는 CMK 앱이 비활성화되고 Platform에서 더 이상 데이터에 액세스할 수 없게 되면 해당 데이터와 관련된 모든 다운스트림 작업은 더 이상 수행할 수 없습니다. 구성을 변경하기 전에 키에 대한 플랫폼 액세스 취소의 다운스트림에 대한 영향을 이해해야 합니다.

키 액세스 제거 또는 키에서 비활성화/삭제 후 [!DNL Azure] 주요 자격 증명 모음: 이 구성이 기본 데이터 저장소로 전파되는 데 몇 분에서 24시간 정도 소요될 수 있습니다. 또한 Platform 워크플로에는 성능 및 핵심 애플리케이션 기능에 필요한 캐시된 임시 데이터 저장소가 포함되어 있습니다. 이러한 캐시된 임시 저장소를 통한 CMK 취소의 전파는 데이터 처리 워크플로우에 의해 결정된 대로 최대 7일이 소요될 수 있다. 예를 들어 프로필 대시보드는 캐시 데이터 저장소에서 데이터를 유지 및 표시하고 새로 고침 주기의 일부로 캐시 데이터 저장소에 보관된 데이터를 만료하는 데 7일이 소요됩니다. 애플리케이션에 대한 액세스를 다시 활성화할 때 데이터를 다시 사용할 수 있도록 동일한 시간 지연이 적용됩니다.

>[!NOTE]
>
>기본이 아닌(캐시된/임시) 데이터에 대한 7일 데이터 세트 만료에 대한 두 가지 사용 사례별 예외가 있습니다. 이러한 기능에 대한 자세한 내용은 해당 설명서 를 참조하십시오.<ul><li>[Adobe Journey Optimizer URL 단축기](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[가장자리 투영](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 다음 단계

프로세스를 시작하려면 다음 기한까지 시작: [구성 [!DNL Azure] 주요 자격 증명 모음](./azure-key-vault-config.md) 및 [암호화 키 생성](./azure-key-vault-config.md#generate-a-key) Adobe과 공유
