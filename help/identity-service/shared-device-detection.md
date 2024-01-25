---
keywords: Experience Platform;홈;인기 항목;ID 서비스;ID 서비스;공유 장치;공유 장치
title: 공유 장치 개요(베타)
description: 공유 디바이스 감지는 동일한 디바이스의 서로 다른 인증된 사용자를 식별하므로 ID 그래프에서 고객 데이터를 보다 정확하게 표시할 수 있습니다
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: d7c7bed74d746aba2330ecba62f9f810fbaf0d63
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 공유 장치 감지 개요(베타)

>[!IMPORTANT]
>
>다음 [!DNL Shared Device Detection] 기능은 Beta 버전입니다. 기능 및 설명서는 변경될 수 있습니다.

Adobe Experience Platform [!DNL Identity Service] 은 디바이스와 시스템 간에 id를 연결하여 고객 및 고객 행동을 더 잘 파악할 수 있도록 하여 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

[!DNL Shared Device] 둘 이상의 개인이 사용하는 장치를 나타냅니다. 공유 장치의 예로는 태블릿, 라이브러리 컴퓨터 및 키오스크가 있습니다. 다음을 통해 [!DNL Shared Device Detection] 기능을 사용하면 동일한 장치의 다른 사용자가 단일 id로 병합되는 것을 방지할 수 있으므로 개인을 보다 정확하게 표현할 수 있습니다.

포함 [!DNL Shared Device Detection] 다음을 수행할 수 있습니다.

* 동일한 장치의 여러 사용자에 대해 별도의 ID 그래프를 만듭니다.
* 동일한 장치를 사용하여 서로 다른 개인의 데이터가 혼합되는 것을 방지합니다.
* 고객을 보다 깨끗하고 정확하게 파악할 수 있도록 합니다.

>[!TIP]
>
>구성 대상 [!DNL Shared Device Detection] 그래프가 생성된 후에서 설정을 더 이상 수정할 수 없으므로 데이터 세트에 대한 프로필을 활성화하기 전에 을 완료해야 합니다. [!DNL Identity Service].

## [!DNL Shared Device Detection] 시작하기

작업 [!DNL Shared Device Detection] 관련된 다양한 플랫폼 서비스에 대한 이해가 필요합니다. (으)로 작업을 시작하기 전에 [!DNL Shared Device Detection], 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Identity Service]](./home.md): 디바이스와 시스템 간에 ID를 연결하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
   * [ID 그래프 뷰어](./features/identity-graph-viewer.md): ID 그래프 뷰어를 시각화하고 상호 작용하여 고객 ID가 어떻게 서로 결합되는지 더 잘 이해할 수 있습니다.
   * [ID 네임스페이스](./features/namespaces.md): 정규화된 ID의 구성 요소 및 ID 네임스페이스를 통해 ID의 컨텍스트와 유형을 구분하는 방법을 확인하십시오.

## [!DNL Shared Device Detection] 이해 

를 사용할 때는 다음 용어를 이해하는 것이 중요합니다
[!DNL Shared Device Detection]. 이해하는 데 필수적인 용어 목록은 아래 표를 참조하십시오 [!DNL Shared Device Detection].

### 용어

| 용어 | 정의 |
| --- | --- |
| 공유 장치 | 공유 장치는 두 명 이상의 개인이 사용하는 장치입니다. 공유 장치의 예로는 태블릿, 라이브러리 컴퓨터 및 키오스크가 있습니다. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 는 동일한 장치의 다른 사용자의 데이터를 서로 분리할 수 있는 구성 설정을 나타냅니다. |
| 공유 ID 네임스페이스 | 공유 ID 네임스페이스는 여러 사용자가 사용할 수 있는 장치를 나타냅니다. 공유 ID 네임스페이스는 일반적으로 ECID이지만 다른 장치 ID로 설정할 수 있습니다. |
| 사용자 ID 네임스페이스 | 사용자 ID 네임스페이스는 공유 장치의 인증된(로그인된) 사용자를 나타냅니다. |
| 마지막으로 인증된 사용자 | 마지막 인증된 사용자는 장치가 여러 계정에 의해 로그온되어 있는 경우 장치에 마지막으로 로그인한 사용자를 나타냅니다. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] 는 두 개의 네임스페이스를 설정하여 작동합니다. **공유 ID 네임스페이스** 및 **사용자 ID 네임스페이스**.

* 공유 ID 네임스페이스는 여러 사용자가 사용할 수 있는 장치를 나타냅니다. Adobe은 고객이 ECID를 공유 장치 식별자로 사용할 것을 권장합니다.
* 사용자 ID 네임스페이스는 사용자의 로그인 ID에 해당하는 ID 네임스페이스에 매핑되며, 사용자의 CRM ID, 이메일 주소, 해시된 이메일 또는 전화번호일 수 있습니다.

태블릿과 같은 공유 장치에는 단일 **공유 ID 네임스페이스**. 반면, 공유 장치의 각 사용자는 지정된 고유한 값을 갖습니다 **사용자 ID 네임스페이스** 해당 로그인 ID에 해당합니다. 예를 들어, Kevin과 Nora가 전자상거래를 위해 공유하는 태블릿은 다음의 고유한 ECID를 가진다 `1234`, Kevin에는 자신의 ID 네임스페이스가 매핑되어 있음 `kevin@email.com` 계정과 노라는 자신의 사용자 ID 네임스페이스가 매핑되어 있습니다. `nora@email.com` 계정입니다.

[!DNL Shared Device Detection] 는 공유 id 네임스페이스(예: )를 연결하여 동일한 장치의 여러 사용자를 구분할 수 있습니다. ECID)를 마지막으로 인증된 사용자의 사용자 ID 네임스페이스(로그인 ID)와 함께 사용할 수 있습니다.

### ID 데이터를 ID 그래프로 보내는 방법

다음 예를 참고하여 방법을 이해할 수 있습니다 [!DNL Shared Device Detection] 작동:

>[!NOTE]
>
>이 다이어그램에서 공유 ID 네임스페이스는 ECID로 구성되고 사용자 ID 네임스페이스는 CRM ID로 구성됩니다.

![다이어그램](./images/shared-device/diagram.png)

* Kevin과 Nora는 전자상거래 웹사이트를 방문하는 태블릿을 공유한다. 그러나, 그들 둘 다 그들이 온라인으로 검색하고 쇼핑하기 위해 각각 사용하는 그들 자신의 독립적인 계정을 가지고 있습니다.
   * 공유 디바이스인 태블릿에는 태블릿의 웹 브라우저 쿠키 ID를 나타내는 해당 ECID가 있습니다.
* 케빈이 태블릿을 사용하고 **로그인** 헤드폰을 검색할 전자 상거래 계정에 대해 이는 Kevin의 CRM ID(**사용자 ID 네임스페이스**)가 이제 태블릿의 ECID( )와 연결됩니다.**공유 ID 네임스페이스**). 태블릿의 브라우징 데이터가 이제 케빈의 신분 그래프에 통합되었습니다.
   * 만약 케빈이라면 **로그아웃** 노라가 태블릿을 사용하고 **로그인** 이제 자신의 계정에 연결하고 카메라를 구입하면 CRM ID가 태블릿의 ECID에 연결됩니다. 따라서, 태블릿의 브라우징 데이터는 이제 노라의 신원 그래프와 통합된다.
   * If Nora **로그아웃하지 않음** 케빈이 태블릿을 쓰긴 하는데 **로그인하지 않음**: 태블릿의 검색 데이터는 여전히 Nora와 통합되어 있는데, 이는 그녀가 인증된 사용자로 남아 있고 그녀의 CRM ID가 여전히 태블릿의 ECID에 연결되어 있기 때문이다.
   * If Nora **로그아웃** 케빈이 태블릿을 쓰긴 하는데 **로그인하지 않음**, 태블릿의 검색 데이터는 여전히 Nora의 ID 그래프와 통합되어 있습니다. **마지막 인증된 사용자**, 그녀의 CRM ID는 태블릿의 ECID와 연결된 상태로 유지됩니다.
   * 만약 케빈이라면 **로그인** 다시 한 번 말하지만, 이제 그의 CRM ID가 태블릿의 ECID에 연결됩니다. 왜냐하면 그는 이제 마지막으로 인증된 사용자이고 태블릿의 브라우징 데이터는 이제 그의 ID 그래프와 통합되기 때문입니다.

### 방법 [!DNL Profile Service] 프로필 조각을 와 병합 [!DNL Shared Device Detection] 활성화됨

[!DNL Profile Service] 는 프로필 조각 및 병합된 프로필을 기록합니다. 각 개별 고객 프로필은 해당 고객에 대한 단일 보기를 형성하기 위해 병합된 여러 프로필 조각으로 구성됩니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 단일 고객과 관련된 여러 프로필 조각이 있습니다. 이러한 조각을 Platform에 수집하면 해당 고객을 위한 단일 프로필을 만들기 위해 함께 병합됩니다.

날짜 [!DNL Shared Device Detection] 이(가) 활성화되었습니다. [!DNL Profile] 경험 이벤트가 인증되었는지 여부에 따라 프로필 조각의 기본 id를 정의합니다

An **인증된 경험 이벤트** 는 장치에 로그인하는 동안 사용자가 완료한 작업입니다. 인증된 경험 이벤트의 경우 기본 ID는 **사용자 ID 네임스페이스** (로그인 ID). An **인증되지 않은 경험 이벤트** 는 장치에 로그인하지 않은 사용자가 완료한 작업입니다. 인증되지 않은 경험 이벤트의 경우 기본 ID는 **공유 ID 네임스페이스** (ECID).

자세한 내용은  [[!DNL Real-Time Customer Profile] 개요](../profile/home.md).

## 공유 장치 UI

Platform UI에서 를 선택합니다. **[!UICONTROL ID]** 왼쪽 탐색에서 을(를) 선택한 다음 **[!UICONTROL ID 설정]**.

![id-대시보드](./images/shared-device/identity-dashboard.png)

다음 [!UICONTROL 공유 장치 설정] 데이터에 대한 공유 장치 설정을 구성하는 인터페이스를 제공하는 페이지가 나타납니다. 공유 장치 설정은 기본적으로 비활성화되어 있습니다.

활성화된 경우 공유 장치 설정을 사용하면 동일한 장치의 다른 사용자의 데이터를 서로 분리할 수 있습니다. 이 구성 설정을 사용하면 동일한 장치의 사용자 ID가 함께 결합되지 않는 ID 그래프를 보다 깨끗하고 정확하게 표시할 수 있습니다.

선택 **[!UICONTROL 사용]** 을 클릭하여 공유 장치 설정 수정을 시작합니다.

![enable-shared-device](./images/shared-device/enable-shared-device.png)

다음 [!UICONTROL 공유 ID 네임스페이스] 및 [!UICONTROL 사용자 ID 네임스페이스] 구성 옵션이 표시되어 사용하려는 id 네임스페이스를 수정할 수 있습니다.

![set-namespace](./images/shared-device/set-namespaces.png)

[!UICONTROL 공유 ID 네임스페이스] 는 여러 다른 사용자가 사용하는 단일 디바이스를 나타냅니다. 이 네임스페이스는 항상 (으)로 설정됩니다. **[!UICONTROL ECID]** 모든 Platform 사용자가 **[!UICONTROL ECID]** 웹 브라우저 식별자로 사용됩니다.

![shared-identity-namespace](./images/shared-device/shared-identity-namespace.png)

다음 [!UICONTROL 사용자 ID 네임스페이스] 동일한 장치의 다른 사용자를 식별하고 데이터가 동일한 id 그래프에 결합되지 않도록 할 수 있습니다.

![user-identity-namespace](./images/shared-device/user-identity-namespace.png)

다음 항목 선택 **[!UICONTROL 사용자 ID 네임스페이스]** 검색 창에서 id 네임스페이스를 입력하거나 드롭다운 메뉴에서 id 네임스페이스를 선택합니다.

>[!TIP]
>
>다음 [!UICONTROL 사용자 ID 네임스페이스] 최종 사용자의 로그인 ID에 해당하는 id 네임스페이스에 매핑해야 합니다. 옵션에는 고객 ID, 이메일 및 해시된 이메일이 포함됩니다.

![이메일](./images/shared-device/emails.png)

을(를) 구성했으면 [!UICONTROL 공유 장치 설정], 선택 **[!UICONTROL 저장]**.

![저장](./images/shared-device/save.png)

선택 내용을 확인하는 팝업 창이 나타납니다. 선택 **[!UICONTROL 예]** 구성 설정을 완료합니다.

![확인](./images/shared-device/confirm.png)
