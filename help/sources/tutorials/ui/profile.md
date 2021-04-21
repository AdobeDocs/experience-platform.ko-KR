---
keywords: Experience Platform;홈;인기 항목;인바운드 데이터 활성화;프로필 채우기;rtcp 채우기;채워진 통합 프로필
solution: Experience Platform
title: 인바운드 소스 데이터를 활성화하여 UI에서 고객 프로필 채우기
topic-legacy: overview
type: Tutorial
description: 소스 커넥터의 인바운드 데이터를 사용하여 실시간 고객 프로필 데이터를 풍부하게 만들고 채울 수 있습니다.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 인바운드 소스 데이터를 활성화하여 고객 프로필 채우기

소스 커넥터의 인바운드 데이터를 사용하여 [!DNL Real-time Customer Profile] 데이터를 누름 및 채울 수 있습니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 자습서에서는 소스 커넥터를 만들고 구성해야 합니다.  UI에서 다른 커넥터를 만들기 위한 자습서 목록은 [소스 커넥터 개요](../../home.md)에서 찾을 수 있습니다.

## [!DNL Real-time Customer Profile] 데이터 채우기

고객 프로파일을 강화하려면 대상 데이터 세트의 소스 스키마가 [!DNL Real-time Customer Profile]에서 사용할 수 있어야 합니다. 호환되는 스키마는 다음 요구 사항을 충족합니다.

- 스키마에 ID 속성으로 지정된 속성이 하나 이상 있습니다.
- 스키마에 기본 ID로 정의된 ID 속성이 있습니다.
- 기본 ID가 대상 속성인 데이터 흐름 내의 매핑이 있습니다.

소스 작업 영역에서 **[!UICONTROL Browse]** 탭을 클릭하여 기본 연결을 나열합니다. 표시된 목록에서 프로필을 채울 데이터 흐름을 포함하는 연결을 찾습니다. 연결 이름을 클릭하여 세부 정보에 액세스합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

연결의 **[!UICONTROL Source activity]** 화면이 나타나 연결이 소스 데이터를 수집하는 데이터 집합을 표시합니다. [!DNL Profile]에 대해 활성화할 데이터 세트 이름을 클릭합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

**[!UICONTROL Dataset activity]** 화면이 나타납니다. 화면 오른쪽의 **[!UICONTROL Properties]** 열에는 데이터 세트에 대한 세부 정보가 표시되며, 데이터 세트에 적용되는 **[!UICONTROL Profile]** 스위치 및 스키마에 대한 링크가 포함됩니다. 스키마 이름을 클릭하여 해당 컴포지션을 봅니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

가운데 캔버스에 스키마 구조를 표시하는 **[!UICONTROL Schema Editor]**&#x200B;이 나타납니다. 캔버스 내에서 기본 ID로 설정할 필드를 선택합니다. 나타나는 **[!UICONTROL Field properties]** 탭에서 **[!UICONTROL Identity]** 확인란을 선택한 다음 **[!UICONTROL Primary identity]** 를 선택합니다. 마지막으로 적절한 **[!UICONTROL Identity namespace]**&#x200B;을 선택한 다음 **[!UICONTROL Apply]**&#x200B;을 클릭합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

스키마 구조의 최상위 객체를 클릭하면 **[!UICONTROL Schema properties]** 열이 나타납니다. **[!UICONTROL Profile]** 스위치를 전환하여 [!DNL Profile]에 대한 스키마를 활성화합니다. **[!UICONTROL Save]**&#x200B;을 클릭하여 변경 내용을 완료합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

스키마가 [!DNL Profile]에 대해 활성화되어 있으므로 **[!UICONTROL Dataset activity]** 화면으로 돌아가 **[!UICONTROL Properties]** 열 내에서 **[!UICONTROL Profile]** 전환을 클릭하여 [!DNL Profile]에 대한 데이터 세트를 활성화합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

[!DNL Profile]에 대해 스키마와 데이터 세트를 모두 활성화하면 해당 데이터 세트에 인제스트된 데이터도 이제 고객 프로필을 채웁니다.

>[!NOTE]
>
>최근에 활성화된 데이터 집합 내의 기존 데이터는 [!DNL Profile]에 의해 사용되지 않습니다.

## 다음 단계

이 튜토리얼을 따라 [!DNL Profile] 모집단용 인바운드 데이터를 활성화했습니다. 자세한 내용은 [[!DNL Real-time Customer Profile] 개요](../../../profile/home.md)를 참조하십시오.
