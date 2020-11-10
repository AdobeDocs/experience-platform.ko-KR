---
keywords: Experience Platform;home;popular topics;activate inbound data;populate profile;populate rtcp;populated unified profile
solution: Experience Platform
title: 인바운드 소스 데이터를 활성화하여 고객 프로필 채우기
topic: overview
type: Tutorial
description: 소스 커넥터의 인바운드 데이터를 사용하여 실시간 고객 프로필 데이터를 향상시키고 채울 수 있습니다.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# 인바운드 소스 데이터를 활성화하여 고객 프로필 채우기

소스 커넥터의 인바운드 데이터를 [!DNL Real-time Customer Profile] 데이터 누락을 위해 사용할 수 있습니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 자습서에서는 소스 커넥터를 만들고 구성해야 합니다.  UI에서 다른 커넥터를 만들기 위한 자습서 목록은 [소스 커넥터 개요에 있습니다](../../home.md).

## 데이터 [!DNL Real-time Customer Profile] 채우기

고객 프로파일을 강화하려면 대상 데이터 세트의 소스 스키마가 에서 사용할 수 있도록 호환되어야 합니다 [!DNL Real-time Customer Profile]. 호환 스키마는 다음 요구 사항을 충족합니다.

- 스키마에 ID 속성으로 지정된 속성이 하나 이상 있습니다.
- 스키마에 기본 ID로 정의된 ID 속성이 있습니다.
- 기본 ID가 target 속성인 데이터 흐름 내의 매핑이 있습니다.

소스 작업 영역에서 찾아보기 **[!UICONTROL 탭을 클릭하여]** 기본 연결을 나열합니다. 표시된 목록에서 프로필을 채울 데이터 흐름을 포함하는 연결을 찾습니다. 연결 이름을 클릭하여 세부 정보에 액세스합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

연결의 **[!UICONTROL 소스 활동]** 화면이 나타나 연결이 소스 데이터를 수집하는 데이터 세트를 표시합니다. 활성화할 데이터 세트의 이름을 클릭합니다 [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

데이터 **[!UICONTROL 집합 활동]** 화면이 나타납니다. 화면 오른쪽의 **[!UICONTROL 속성]** 열에는 데이터 세트에 대한 세부 정보가 표시되고, **[!UICONTROL 프로필]** 전환 및 데이터 세트에서 준수하는 스키마에 대한 링크가 포함됩니다. 스키마 이름을 클릭하여 해당 컴포지션을 봅니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

스키마 **[!UICONTROL 편집기가]** 나타나고 중앙 캔버스에 스키마의 구조를 표시합니다. 캔버스 내에서 기본 ID로 설정할 필드를 선택합니다. 표시되는 **[!UICONTROL 필드 속성]** 탭 아래에서 **[!UICONTROL ID]** 확인란을 선택한 다음 **[!UICONTROL 기본 ID를 선택합니다]**. 마지막으로 적절한 ID 네임스페이스를 **[!UICONTROL 선택한]**&#x200B;다음 적용을 **[!UICONTROL 클릭합니다]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

스키마 구조의 최상위 객체를 클릭하면 스키마 **[!UICONTROL 속성]** 열이 나타납니다. 프로필 [!DNL Profile] 스위치 **[!UICONTROL 를 전환하여 스키마를]** 활성화합니다. 저장을 **[!UICONTROL 클릭하여]** 변경 사항을 완료합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

이제 스키마가 활성화되면 데이터 세트 활동 [!DNL Profile]화면 **[!UICONTROL 으로 돌아가 PropertiesColumn에서]** 프로필 [!DNL Profile] 전환 **[!UICONTROL 을 클릭하여 데이터 세트]** 를 **** 활성화합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

이제 스키마와 데이터 세트에 대한 데이터 [!DNL Profile]가 모두 활성화되면 해당 데이터 세트에 수집되는 데이터도 고객 프로필을 채웁니다.

>[!NOTE]
>
>최근에 활성화된 데이터 세트 내의 기존 데이터는 사용되지 않습니다 [!DNL Profile].

## 다음 단계

이 튜토리얼을 따라 모집단 관련 인바운드 데이터를 성공적으로 활성화했습니다 [!DNL Profile] . 자세한 내용은 [[!DNL Real-time Customer Profile] 개요를 참조하십시오](../../../profile/home.md).