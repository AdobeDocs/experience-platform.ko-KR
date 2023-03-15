---
keywords: Experience Platform;홈;인기 항목;인바운드 데이터 활성화;프로필 채우기;rtcp 채우기;채워진 통합 프로필
solution: Experience Platform
title: 인바운드 소스 데이터를 활성화하여 UI에서 고객 프로필 채우기
type: Tutorial
description: 소스 커넥터의 인바운드 데이터를 사용하여 실시간 고객 프로필 데이터를 보강하고 채울 수 있습니다.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 인바운드 소스 데이터를 활성화하여 고객 프로필 채우기

소스 커넥터의 인바운드 데이터는 다음을 강화하고 채우는 데 사용할 수 있습니다. [!DNL Real-Time Customer Profile] 데이터.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   - [스키마 컴포지션 기본 사항](../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

또한 이 자습서에서는 이미 소스 커넥터를 만들고 구성했어야 합니다.  UI에서 다양한 커넥터를 만들기 위한 튜토리얼 목록은 [소스 커넥터 개요](../../home.md).

## 사용자 채우기 [!DNL Real-Time Customer Profile] 데이터

고객 프로필을 보강하려면 대상 데이터 세트의 소스 스키마가에서 사용할 수 있도록 호환되어야 합니다 [!DNL Real-Time Customer Profile]. 호환되는 스키마는 다음 요구 사항을 충족합니다.

- 스키마에 ID 속성으로 지정된 특성이 하나 이상 있습니다.
- 스키마에는 기본 ID로 정의된 ID 속성이 있습니다.
- 기본 ID가 대상 속성인 데이터 흐름 내의 매핑이 존재합니다.

소스 작업 영역에서 **[!UICONTROL 찾아보기]** 탭으로 기본 연결을 나열합니다. 표시된 목록에서 프로필을 채울 데이터 흐름이 포함된 연결을 찾습니다. 연결 이름을 클릭하여 세부 정보에 액세스합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

연결 **[!UICONTROL 소스 활동]** 연결이 소스 데이터를 수집하는 데이터 세트를 표시하는 화면이 나타납니다. 활성화하려는 데이터 세트의 이름을 클릭합니다 [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

다음 **[!UICONTROL 데이터 세트 활동]** 화면이 나타납니다. 다음 **[!UICONTROL 속성]** 화면 오른쪽의 열에는 데이터 세트의 세부 정보가 표시되며 **[!UICONTROL 프로필]** 전환 및 데이터 세트가 준수하는 스키마에 대한 링크. 스키마 이름을 클릭하여 해당 컴포지션을 확인합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

다음 **[!UICONTROL 스키마 편집기]** 중앙 캔버스에 스키마 구조를 보여 주는 가 나타납니다. 캔버스 내에서 기본 ID로 설정할 필드를 선택합니다. 아래 **[!UICONTROL 필드 속성]** 나타나는 탭에서 **[!UICONTROL 신원]** 확인란, 그런 다음 **[!UICONTROL 기본 ID]**. 마지막으로 적절한 을 선택합니다. **[!UICONTROL ID 네임스페이스]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 적용]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

스키마 구조의 최상위 객체를 누릅니다. **[!UICONTROL 스키마 속성]** 열이 나타납니다. 에 대한 스키마 활성화 [!DNL Profile] 을 토글하여 **[!UICONTROL 프로필]** 전환. 클릭 **[!UICONTROL 저장]** 을 눌러 변경 사항을 완료합니다.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

이제 스키마가 다음에 대해 활성화됩니다. [!DNL Profile]로 돌아갑니다. **[!UICONTROL 데이터 세트 활동]** 다음에 대한 데이터 세트 차단 및 활성화 [!DNL Profile] 을(를) 클릭하여 **[!UICONTROL 프로필]** 내에서 전환 **[!UICONTROL 속성]** 열.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

에 대해 스키마와 데이터 세트가 모두 활성화됨 [!DNL Profile], 해당 데이터 세트에 수집된 데이터도 이제 고객 프로필을 채웁니다.

>[!NOTE]
>
>최근에 활성화된 데이터 세트 내의 기존 데이터는에서 사용하지 않습니다. [!DNL Profile].

## 다음 단계

이 자습서에 따라 다음에 대한 인바운드 데이터를 성공적으로 활성화했습니다. [!DNL Profile] 모집단. 자세한 내용은 [[!DNL Real-Time Customer Profile] 개요](../../../profile/home.md).
