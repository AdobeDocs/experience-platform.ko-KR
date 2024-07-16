---
title: 새 대상 연결 만들기
type: Tutorial
description: Adobe Experience Platform에서 대상에 연결하고, 경고를 활성화하고, 연결된 대상에 대한 마케팅 작업을 설정하는 방법을 알아봅니다.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---

# 새 대상 연결 만들기

>[!IMPORTANT]
> 
>* 대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* 데이터 세트 내보내기를 지원하는 대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 데이터 세트 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

## 개요 {#overview}

대상 데이터를 대상으로 보내려면 먼저 대상 플랫폼에 대한 연결을 설정해야 합니다. 이 문서에서는 새 대상 연결을 설정하는 방법을 보여 줍니다. 그러면 Adobe Experience Platform 사용자 인터페이스를 사용하여 대상을 활성화하거나 데이터 세트를 내보낼 수 있습니다.

## 카탈로그에서 원하는 대상 찾기 {#setup}

1. **[!UICONTROL 연결]** > **[!UICONTROL 대상]**(으)로 이동한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다.

   대상 카탈로그 페이지를 표시하는 Experience Platform UI의 ![스크린샷입니다.](../assets/ui/connect-destinations/catalog.png)

2. 대상에 대한 기존 연결 여부와 대상이 대상자 활성화, 데이터 세트 내보내기 또는 두 가지 모두를 지원하는지 여부에 따라 카탈로그의 대상 카드에 다른 작업 컨트롤이 있을 수 있습니다. 대상 카드에 대해 다음 컨트롤이 표시될 수 있습니다.

   * **[!UICONTROL 설정]**. 대상을 활성화하거나 데이터 세트를 내보내려면 먼저 이 대상에 연결을 설정해야 합니다.
   * **[!UICONTROL 활성화]**. 이 대상에 대한 연결이 이미 설정되었습니다. 이 대상은 대상 활성화 및 데이터 세트 내보내기를 지원합니다.
   * **[!UICONTROL 대상자 활성화]**. 이 대상에 대한 연결이 이미 설정되었습니다. 이 대상은 대상자 활성화만 지원합니다.

   이러한 컨트롤의 차이점에 대한 자세한 내용은 대상 작업 영역 설명서의 [카탈로그](../ui/destinations-workspace.md#catalog) 섹션도 참조하십시오.

   사용 가능한 제어에 따라 **[!UICONTROL 설정]**, **[!UICONTROL 활성화]** 또는 **[!UICONTROL 대상자 활성화]**&#x200B;를 선택하십시오.

   [설정] 컨트롤이 강조 표시된 대상 카탈로그 페이지를 표시하는 Experience Platform UI의 ![스크린샷입니다.](../assets/ui/connect-destinations/set-up.png)

   대상자 활성화 컨트롤이 강조 표시된 대상 카탈로그 페이지를 표시하는 Experience Platform UI의 ![스크린샷입니다.](../assets/ui/connect-destinations/activate-segments.png)

3. **[!UICONTROL 설정]**&#x200B;을 선택한 경우 다음 단계로 건너뛰고 대상에 대해 [인증](#authenticate)합니다.

   **[!UICONTROL 활성화]**, **[!UICONTROL 대상자 활성화]** 또는 **[!UICONTROL 데이터 세트 내보내기]**&#x200B;를 선택한 경우 이제 기존 대상 연결 목록을 볼 수 있습니다.

   대상에 대한 새 연결을 설정하려면 **[!UICONTROL 새 대상 구성]**&#x200B;을 선택하십시오.

   사용 가능한 대상 목록과 새 대상 구성 컨트롤이 강조 표시된 Experience Platform UI의 ![스크린샷입니다.](../assets/ui/connect-destinations/configure-new-destination.png)

## 대상으로 인증 {#authenticate}

대상에 연결하는 첫 번째 단계는 대상 플랫폼에 인증하는 것입니다.

연결 중인 대상에 따라 대상 파트너의 페이지로 이동하여 인증하거나 플랫폼 워크플로에서 직접 인증 자격 증명을 입력하라는 메시지가 표시될 수 있습니다. 다음은 [!DNL Amazon S3] 대상을 인증하는 데 필요한 입력의 예입니다. 필요한 입력에 대한 자세한 지침은 각 대상 설명서 페이지에 제공됩니다(예: [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) 및 [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)의 인증 섹션 참조).

필수 및 선택적 인증 매개 변수 **[!DNL Amazon S3]개**

![Amazon S3 대상에 인증할 때 필수 입력 매개 변수와 선택적 입력 매개 변수를 보여 주는 이미지입니다.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## 연결 매개 변수 설정 {#set-up-connection-parameters}

대상에 대한 인증을 이미 설정한 경우 기존 계정을 계속 사용하거나 새 계정을 설정할 수 있습니다.

연결할 대상에 따라 다른 유형의 연결 매개 변수를 입력하라는 메시지가 표시될 수 있습니다. 예를 들어 [!DNL Amazon S3] 대상에 연결할 때 파일이 저장될 [!DNL Amazon S3] 버킷 이름 및 폴더 경로에 대한 세부 정보를 입력하라는 메시지가 표시됩니다. 다음은 [!DNL Amazon S3] 대상 및 [!DNL Trade Desk] 대상에 대한 두 가지 필수 입력 예입니다. 필요한 입력에 대한 자세한 지침은 각 대상 설명서 페이지에 나와 있습니다.

>[!IMPORTANT]
>
>아래 이미지는 설명 목적으로만 사용됩니다. 대상 연결 세부 사항은 대상마다 다릅니다. 대상의 연결 세부 정보에 대한 자세한 내용을 보려면 각 [대상 카탈로그](../catalog/overview.md) 페이지의 **대상에 연결** 섹션(예: [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect) 또는 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details))을 읽어 보십시오.

필수 및 선택적 입력 매개 변수 **[!DNL Amazon S3]개**

![Amazon S3 대상에 연결할 때 필수 및 선택적 입력 매개 변수를 표시하는 이미지입니다.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

필수 및 선택적 입력 매개 변수 **[!DNL The Trade Desk]개**

![Trade Desk 대상에 연결할 때 필수 및 선택적 입력 매개 변수를 표시하는 이미지입니다.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### 내보낸 파일에 대한 파일 서식 옵션 설정 {#file-formatting-and-compression-options}

파일 기반 대상의 경우 내보낸 파일의 형식 지정 및 압축 방법과 관련된 다양한 설정을 구성할 수 있습니다. 사용 가능한 모든 서식 및 압축 옵션에 대한 자세한 내용은 [파일 기반 대상에 대한 파일 서식 옵션 구성 자습서](/help/destinations/ui/batch-destinations-file-formatting-options.md)를 참조하십시오.

![CSV 파일에 대한 파일 형식 선택 및 다양한 옵션을 보여 주는 이미지입니다.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### 대상 활성화, 계정 활성화, 잠재 고객 활성화 또는 데이터 세트 내보내기에 대한 대상 연결을 설정합니다 {#segment-activation-or-dataset-exports}

일부 파일 기반 대상은 알려진 고객, 계정 고객 또는 잠재 고객에 대한 대상 활성화와 데이터 세트 내보내기를 지원합니다. 이러한 대상의 경우 연결을 만들어 [대상 활성화](/help/destinations/ui/activate-batch-profile-destinations.md), [계정](/help/destinations/ui/activate-account-audiences.md), [잠재 고객](/help/destinations/ui/activate-prospect-audiences.md) 또는 [데이터 세트 내보내기](/help/destinations/ui/export-datasets.md)를 사용할 수 있도록 할지 여부를 선택할 수 있습니다.

>[!WARNING]
>
>데이터 세트를 내보낼 때 JSON 파일로 내보내기는 압축 모드에서만 지원됩니다. [!DNL Parquet] 파일로 내보내기는 압축 및 압축 해제 모드에서 지원됩니다.

![사용자가 대상 활성화와 데이터 집합 내보내기 중 하나를 선택할 수 있는 데이터 형식 선택 컨트롤을 보여 주는 이미지](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### 대상 경고 활성화 {#enable-alerts}

1. (선택 사항) 구독하려는 대상 데이터 흐름 경고를 선택합니다. 데이터 흐름을 만들 때 경고를 구독하여 흐름 실행의 상태, 성공 또는 실패와 관련된 경고 메시지를 받을 수 있습니다. 사용 가능한 경고는 연결 중인 대상 유형(파일 기반 또는 스트리밍)에 따라 다릅니다. 대상 데이터 흐름 경고에 대한 자세한 내용은 [컨텍스트 내 대상 경고 구독](alerts.md)을 참조하십시오.

   ![컨텍스트 내 대상 경고 구독 옵션이 강조 표시된 새 대상 구성 대화 상자.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. **[!UICONTROL 다음]**&#x200B;을 선택합니다.

   ![다음 컨트롤이 강조 표시된 새 대상 구성 대화 상자를 사용하여 사용자가 워크플로우의 다음 단계로 진행할 수 있습니다.](../assets/ui/connect-destinations/next.png)

## 마케팅 액션 선택 {#select-marketing-actions}

1. 대상으로 내보낼 데이터에 적용할 수 있는 마케팅 작업을 선택합니다. 마케팅 액션은 데이터를 대상으로 내보내는 의도를 나타냅니다. Adobe 정의 마케팅 액션에서 선택하거나 고유한 마케팅 액션을 만들 수 있습니다. 마케팅 액션에 대한 자세한 내용은 [데이터 사용 정책 개요](../../data-governance/policies/overview.md) 페이지를 참조하세요.

   ![사용 가능한 마케팅 작업이 강조 표시된 새 대상 구성 대화 상자 대상에 연결 워크플로를 완료하는 데 사용할 수 있는 컨트롤도 강조 표시됩니다.](../assets/ui/connect-destinations/governance.png)

2. 대상 구성을 저장하려면 **[!UICONTROL 저장 및 종료]**&#x200B;를 선택하고 대상 데이터 [활성화 흐름](activation-overview.md)으로 진행하려면 **[!UICONTROL 다음]**&#x200B;을 선택하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽고 Experience Platform UI를 사용하여 대상에 대한 연결을 설정하는 방법에 대해 알아보았습니다. 다시 말해서 사용 가능한 연결 매개 변수와 필요한 연결 매개 변수는 대상마다 다릅니다. 대상 유형별 필수 입력 및 사용 가능한 옵션에 대한 특정 정보는 [대상 카탈로그](/help/destinations/catalog/overview.md)의 대상 설명서 페이지를 참조하십시오.

다음으로 [대상 활성화](/help/destinations/ui/activation-overview.md) 또는 [데이터 세트 내보내기](/help/destinations/ui/export-datasets.md)를 대상으로 진행할 수 있습니다.