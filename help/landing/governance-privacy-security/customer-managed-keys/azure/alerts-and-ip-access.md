---
title: Azure CMK에 대한 경고 및 IP 허용 목록 구성
description: Azure에서 Adobe Vault의 고정 IP 주소를 Experience Platform 하는 방법에 대해 알아보고 허용 목록에 추가하다 경고가 고객 관리 키 액세스 문제를 감지하고 해결하는 방법을 이해합니다.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# [!DNL Azure] CMK에 대한 경고 및 IP 허용 목록 구성

Adobe에서는 투명도를 향상시키기 위해 주요 자격 증명 모음의 액세스 상태를 확인하고 문제가 발생할 경우 경고를 트리거하는 [모니터링 서비스](../../../../observability/alerts/ui.md){target="_blank"}를 제공합니다. 이러한 경고를 통해 신속하게 대응하고 서비스 중단을 방지할 수 있습니다. 허용 목록에 추가하다 이 서비스를 활성화하려면 Adobe의 고정 IP 주소를 테스트하십시오.

>[!IMPORTANT]
>
>공개 네트워크 액세스를 사용하지 않도록 설정하거나 선택한 네트워크만 허용하도록 [!DNL Azure] Key Vault를 구성한 경우 Adobe의 정적 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 이 지침이 없으면 Experience Platform 인스턴스에 영향을 줄 수 있는 액세스 문제에 대한 알림을 받지 못할 수 있습니다.

## 허용 목록에 추가하다 [!DNL Azure] 키 자격 증명 모음의 Adobe {#add-adobe-static-ip}

네트워크 제한을 유지하면서 이러한 경고를 활성화하려면 **[!DNL Azure Key Vault]** > **[!DNL Networking settings]**(으)로 이동하십시오. **[!DNL Firewalls and virtual networks]** 탭에서 **[!DNL Allow public access from specific virtual networks and IP addresses]**&#x200B;을(를) 선택합니다.

Adobe의 고정 IP 주소를 추가할 위치와 액세스 허용 옵션을 강조 표시한 ![[!DNL Azure] 주요 자격 증명 모음 네트워킹 설정 화면입니다.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Adobe의 고정 IP 주소

>[!IMPORTANT]
>
>Adobe에서 제공한 고정 IP 주소: `20.88.123.53`.

그런 다음 **[!DNL Firewall]** 섹션에서 **[!DNL Add your current IP address]**&#x200B;을(를) 선택하고 Adobe의 고정 IP 주소로 바꿉니다. 모든 아웃바운드 연결은 프로덕션 환경으로 처리되므로 제한된 네트워크 구성에서 키 저장소에 중단 없이 액세스하려면 이 고정 IP 주소를 허용 목록에추가된으로 사용해야 합니다.

>[!NOTE]
>
>[!DNL Azure] Key Vault 설정에서 고정 IP 주소를 추가하거나 업데이트한 후 변경 사항이 적용되도록 최대 10분 허용하십시오. IP가 추가되면 CMK 앱은 주요 저장소에 액세스하여 권한을 확인합니다.

Adobe의 고정 IP를 허용 목록에 추가 한 후 Experience Platform은 주요 자격 증명 모음에 대한 액세스를 모니터링하고 문제가 발생하는 경우 경고를 트리거할 수 있습니다. 이러한 경고는 조기 경고를 제공하므로 서비스가 영향을 받기 전에 조치를 취할 수 있습니다. 다음 섹션에서는 수신할 수 있는 경고 유형과 응답 방법에 대해 자세히 설명합니다.

## 경고 모니터링 {#monitor-alerts}

플랫폼 경고는 **[!UICONTROL 키 액세스 실패]** 또는 **[!UICONTROL 키 비활성화]**&#x200B;와 같이 키 액세스를 차단할 수 있는 문제를 알려줍니다. 이러한 경고는 제거된 고정 IP 또는 잘못 구성된 방화벽과 같은 문제를 빠르게 식별하는 데 도움이 됩니다. 액세스를 복원하려면 [!DNL Azure] 방화벽 설정을 검토하고 필요한 IP 주소를 다시 추가하십시오.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Adobe I/O 이벤트 알림을 구독하면 모니터링 도구에서 실시간 알림을 받을 수 있습니다. 설치 지침은 [Adobe I/O 이벤트 알림 구독](../../../../observability/alerts/subscribe.md)을 참조하세요. 또한 [경고 UI 안내서](../../../../observability/alerts/ui.md)를 참조하여 Experience Platform 내에서 경고를 보고 관리하는 방법을 배울 수 있습니다.

## 다음 단계

이제 [!DNL Azure] 키 자격 증명 모음에 대해 IP 허용 목록에 추가 및 경고 모니터링을 구성했습니다. [!DNL Azure]에서 고객 관리 키 설정을 완료하려면 다음 구성 안내서를 따르십시오.

- [Key Vault 구성 [!DNL Azure] 2}](./azure-key-vault-config.md)
- [API를 사용하여 CMK 설정](./api-set-up.md)
- [UI를 사용하여 CMK 설정](./ui-set-up.md)
