---
title: UI에서 브레이즈 데이터에 대한 데이터 흐름 만들기
description: Adobe Experience Platform UI를 사용하여 Braze 계정의 데이터 흐름을 만드는 방법을 알아봅니다.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 92d3a7143edc81cc5266ef5a33a8c53dcfdf1074
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# 만들기 [!DNL Braze] UI의 소스 연결

>[!NOTE]
>
>다음 [!DNL Braze] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

[!DNL Braze] 는 실시간으로 소비자와 브랜드 간의 고객 중심 상호 작용을 강화합니다. [!DNL Braze Currents] 는 Braze 플랫폼의 참여 이벤트에 대한 실시간 데이터 스트림으로, 에서 가장 강력하면서도 세부적인 내보내기입니다. [!DNL Braze] 플랫폼.

에서 참여 이벤트 데이터를 가져오는 방법을 알아보려면 다음 튜토리얼을 참조하십시오. [!DNL Braze] UI에서 Adobe Experience Platform에 계정을 추가합니다.

## 전제 조건

이 안내서의 단계를 완료하려면 다음이 필요합니다.

* 에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 새 스트리밍 소스 연결을 만들 수 있는 권한입니다.
* 에 대한 로그인 [[!DNL Braze] 대시보드](https://dashboard.braze.com/sign_in), 사용되지 않음 [Current Connector 라이선스](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)및 커넥터를 만들 수 있는 권한. 자세한 내용은 [설정 요구 사항 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이 자습서에서는 또한 의 작업 이해를 필요로 합니다 [[!DNL Braze] 전류](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

이미 다음 항목이 있는 경우: [!DNL Braze] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/marketing-automation.md).

## 연결 [!DNL Braze] Experience Platform 계정

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 *마케팅 자동화* 범주, 선택 **[!UICONTROL 브레이즈]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![브레이즈 전류 소스가 선택된 Experience Platform UI의 소스 카탈로그.](../../../../images/tutorials/create/braze/catalog.png)

그런 다음 제공된 을 업로드합니다 [브레이즈 커런츠 샘플 파일](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). 이 파일에는 브레이즈가 이벤트의 일부로 보낼 수 있는 모든 필드가 포함되어 있습니다.

![&quot;데이터 추가&quot; 화면.](../../../../images/tutorials/create/braze/select-data.png)

파일이 업로드되면 매핑할 데이터 세트 및 스키마에 대한 정보를 포함하여 데이터 흐름 세부 정보를 제공해야 합니다.
![&quot;데이터 세트 세부 정보&quot;가 강조 표시된 &quot;데이터 흐름 세부 정보&quot; 화면.](../../../../images/tutorials/create/braze/dataflow-detail.png)

그런 다음 매핑 인터페이스를 사용하여 데이터에 대한 매핑을 구성합니다.

![&quot;매핑&quot; 화면.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>브레이즈 타임스탬프는 밀리초로 표시되지 않고, 초 단위로 표시됩니다. Experience Platform의 타임스탬프를 정확하게 반영하려면 계산된 필드를 밀리초 단위로 만들어야 합니다. &quot;시간 * 1000&quot;의 계산은 Experience Platform 내의 타임스탬프 필드에 매핑하는 데 적합한 밀리초로 적절히 변환됩니다.
>
>![타임스탬프에 대한 계산된 필드 만들기 ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### 필요한 자격 증명 수집

연결이 생성되면 다음 자격 증명 값을 수집해야 합니다. 그런 다음 동기화 대시보드에서 입력하여 데이터를으로 전송합니다 [!DNL Platform]. 자세한 내용은 [!DNL Braze] [Current로 이동하는 방법 안내](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| 필드 | 설명 |
| ---------- | ----------- |
| `Client ID` | 와 연결된 클라이언트 ID [!DNL Platform] 소스. |
| `Client Secret` | 와(과) 연결된 클라이언트 암호 [!DNL Platform] 소스. |
| `Tenant ID` | 와 연결된 테넌트 ID [!DNL Platform] 소스. |
| `Sandbox Name` | 와 연계된 샌드박스 [!DNL Platform] 소스. |
| `Dataflow ID` | 와 연결된 데이터 흐름 ID [!DNL Platform] 소스. |
| `Streaming Endpoint` | 와 연결된 스트리밍 엔드포인트 [!DNL Platform] 소스. 브레이즈는 이 문자열을 일괄 처리 스트리밍 끝점으로 자동 변환합니다. |

### 구성 [!DNL Braze Currents] 데이터를 데이터 소스로 스트리밍하려면

다음 범위 내 [!DNL Braze Dashboard], Partner Integration으로 이동합니다. **->** 데이터 내보내기에서 다음을 선택합니다. **[!DNL Create New Current]**. 커넥터의 이름, 커넥터에 대한 알림에 대한 연락처 정보 및 위에 나열된 자격 증명을 제공하라는 메시지가 표시됩니다. 수신하려는 이벤트를 선택하고 원하는 필드 제외/변환을 선택적으로 구성한 다음 을 선택합니다 **[!DNL Launch Current]**.

## 다음 단계

이 자습서를 따라 [!DNL Braze] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [marketing automation 시스템 데이터를 로 가져오기 위한 데이터 흐름 구성 [!DNL Platform]](../../dataflow/marketing-automation.md).