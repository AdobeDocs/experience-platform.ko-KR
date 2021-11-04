---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api;데이터 사용 레이블 개요
solution: Experience Platform
title: 데이터 사용 레이블 개요
topic-legacy: labels
description: Adobe Experience Platform 데이터 거버넌스를 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 데이터 사용 정책에 따라 각 데이터를 분류할 수 있습니다. 이 문서에서는 Experience Platform의 데이터 사용 레이블에 대한 개요를 제공합니다.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 데이터 사용 레이블 개요

Adobe Experience Platform 데이터 거버넌스를 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 데이터 사용 정책에 따라 각 데이터를 분류할 수 있습니다.

이 문서에서는 [!DNL Experience Platform]. 이 안내서를 읽기 전에 [데이터 거버넌스 개요](../home.md) 를 참조하십시오.

## 데이터 사용 레이블 이해

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블을 언제든지 적용할 수 있으므로 데이터를 관리하는 방법을 유연하게 선택할 수 있습니다. 우수 사례에서는 데이터를 수집하자마자 레이블 지정을 권장합니다. [!DNL Experience Platform]또는 에서 데이터를 사용할 수 있게 되는 즉시 [!DNL Platform].

데이터 세트 수준에서 적용되는 데이터 사용 레이블은 데이터 세트 내의 모든 필드에 전파됩니다. 전달하지 않고 데이터 집합의 개별 필드(열 헤더)에 직접 레이블을 적용할 수도 있습니다.

[!DNL Platform] 에서는 데이터 거버넌스에 적용되는 다양한 일반적인 제한 사항을 다루는 몇 가지 &quot;핵심&quot; 데이터 사용 레이블을 기본적으로 제공합니다. 이러한 레이블 및 해당 레이블이 나타내는 사용 정책에 대한 자세한 내용은 [코어 데이터 사용 레이블](reference.md).

Adobe에서 제공하는 레이블 외에도 조직을 위한 고유한 사용자 지정 레이블을 정의할 수 있습니다. 의 섹션을 참조하십시오. [레이블 관리](#manage-labels) 추가 정보.

## 대상 세그먼트의 레이블 상속

에 의해 만들어진 모든 대상 세그먼트 [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md) 해당 데이터 세트의 사용 레이블을 상속합니다. 세그먼트를 대상에 활성화할 때 Experience Platform이 자동 데이터 사용 정책 적용을 제공할 수 있습니다.

데이터 세트 수준 레이블을 상속하는 것 외에도 세그먼트는 기본적으로 연결된 데이터 세트에서 모든 필드 수준 레이블을 상속합니다. 따라서 세그먼트에서 제외해야 하는 특성을 보다 쉽게 식별하고, 이러한 특성이 제외된 필드에서 레이블을 상속하지 못하도록 할 수 있습니다.

Platform에서 자동 적용 작동 방식에 대한 자세한 내용은 [자동 정책 적용](../enforcement/auto-enforcement.md).

### Adobe Audience Manager 데이터 내보내기 컨트롤에서 상속

[!DNL Experience Platform] 는 Adobe Audience Manager과 세그먼트를 공유할 수 있는 기능을 갖추고 있습니다. Audience Manager 세그먼트에 적용된 모든 데이터 내보내기 컨트롤은 해당 레이블 및 마케팅 작업에서 인식하는 것으로 변환됩니다 [!DNL Experience Platform] 데이터 거버넌스.

특정 데이터 내보내기 컨트롤이 의 데이터 사용 레이블에 매핑되는 방법에 대한 참조 [!DNL Platform]을(를) 참조하십시오. [Audience Manager 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 에서 데이터 사용 레이블 관리 [!DNL Experience Platform] {#manage-labels}

다음을 사용하여 데이터 사용 레이블을 관리할 수 있습니다 [!DNL Experience Platform] API 또는 사용자 인터페이스. 각각에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### UI 사용

다음 **[!UICONTROL 정책]** 작업 영역 [!DNL Experience Platform] UI를 통해 조직의 코어 및 사용자 지정 레이블을 보고 관리할 수 있습니다. 다음 **[!DNL Datasets]** 작업 공간을 사용하면 데이터 세트 및 필드에 레이블을 적용할 수 있습니다. 자세한 내용은 [레이블 사용 안내서](user-guide.md).

### API 사용

다음 `/labels` 의 엔드포인트 [정책 서비스 API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 사용자 지정 레이블 만들기를 포함하여 데이터 사용 레이블을 프로그래밍 방식으로 관리할 수 있습니다. 자세한 내용은 [레이블 끝점 안내서](../api/labels.md) 추가 정보.

다음 [데이터 집합 서비스 API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 는 데이터 세트 및 필드에 대한 레이블을 관리하는 데 사용됩니다. 다음 안내서를 참조하십시오. [데이터 세트 레이블 관리](./dataset-api.md) 추가 정보.

## 다음 단계

이 문서에서는 데이터 거버넌스 프레임워크 내의 데이터 사용 레이블 및 해당 역할에 대해 소개합니다. 에서 레이블을 관리하는 방법에 대한 자세한 내용은 이 안내서 전체에서 연결된 설명서 를 참조하십시오 [!DNL Experience Platform].
