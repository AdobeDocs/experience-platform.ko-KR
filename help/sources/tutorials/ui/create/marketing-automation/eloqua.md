---
title: UI에서 Oracle Eloqua(V2)를 Experience Platform에 연결
description: UI에서 Oracle Eloqua 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 1%

---

# UI에서 [!DNL Oracle Eloqua]&#x200B;(V2)을(를) Experience Platform에 연결

[!DNL Oracle Eloqua (V2)] 소스 커넥터를 사용하면 Oracle Eloqua 계정을 Adobe Experience Platform과 연결할 수 있으므로 연락처, 계정, 캠페인 및 참여 활동을 포함한 주요 B2B 마케팅 데이터의 자동 및 확장 가능한 수집을 가능하게 합니다.

이 소스 커넥터를 사용하여 보안 인증을 구성하고, 필요한 정확한 Eloqua 데이터 엔티티를 선택한 다음 표준화된 XDM(Experience Data Model) 스키마에 매핑합니다. 유연한 예약 옵션을 사용하면 초기 데이터 로드와 반복 증분 동기화를 모두 설정할 수 있으므로 마케팅 데이터가 최신 상태로 유지되며 실행 가능합니다.

Adobe의 엔터프라이즈 수집 프레임워크를 기반으로 구축된 [!DNL Oracle Eloqua (V2)] 소스 커넥터는 캠페인 최적화, 성능 측정 및 크로스 채널 개인화를 위한 안정적이고 확장 가능한 기반을 제공합니다.

Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용하여 [!DNL Oracle Eloqua] 계정을 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

### 필요한 자격 증명 수집 {#credentials}

인증에 대한 자세한 내용은 [[!DNL Eloqua] 개요](../../../../connectors/marketing-automation/eloqua.md)를 읽어 보십시오.

## 소스 카탈로그 탐색 {#catalog}

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL Sources]**&#x200B;을(를) 선택하여 *[!UICONTROL Sources]* 작업 영역에 액세스합니다. 카테고리를 선택하거나 검색 창을 사용하여 소스를 찾습니다.

[!DNL Eloqua]에 연결하려면 *[!UICONTROL Marketing Automation]* 범주로 이동하여 **[!UICONTROL (V2) Oracle Eloqua]** 원본 카드를 선택한 다음 **[!UICONTROL Set up]**&#x200B;을(를) 선택하십시오.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL Set up]** 옵션이 표시됩니다. 인증된 계정이 만들어지면 이 옵션이 **[!UICONTROL Add data]**(으)로 변경됩니다.

![설정 단추가 강조 표시된 소스 카탈로그의 Eloqua 소스 카드입니다.](../../../../images/tutorials/create/eloqua/catalog.png)

## 기존 계정 사용 {#existing}

기존 계정을 사용하려면 **[!UICONTROL Existing account]**&#x200B;을(를) 선택한 다음 사용할 [!DNL Eloqua] 계정을 선택하십시오.

![계정 만들기 인터페이스에서 기존 계정 옵션을 선택했습니다.](../../../../images/tutorials/create/eloqua/existing.png)

## 새 계정 만들기 {#new}

새 계정을 만들려면 **[!UICONTROL New account]**&#x200B;을(를) 선택하고 [!UICONTROL Source connection details] 아래에 이름과 설명을 입력하십시오. 그런 다음 [!UICONTROL Account authentication]에서 **클라이언트 ID**, **클라이언트 암호**, **사용자 이름**, **암호** 및 **기본 끝점**&#x200B;의 값을 제공하십시오. 자격 증명에 대한 자세한 내용은 [인증 가이드](../../../../connectors/marketing-automation/eloqua.md)를 참조하십시오. 완료되면 **[!UICONTROL Connect to source]**&#x200B;을(를) 선택하고 몇 초 동안 연결을 설정하십시오.

![원본 연결 세부 정보 및 인증 자격 증명에 대한 필드가 있는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/eloqua/new.png)

## 데이터 선택

데이터 선택 인터페이스를 사용하여 Experience Platform으로 수집할 [!DNL Eloqua] 엔터티를 선택합니다.

>[!TIP]
>
>데이터를 선택하면 캠페인을 제외한 다른 엔티티에 대표 샘플 데이터가 표시된다는 것을 알 수 있습니다. 이 방법을 사용하면 [!DNL Eloqua]개의 공개 API가 현재 캠페인에 대한 실제 데이터만 검색하므로 사용 가능한 필드와 구조를 미리 볼 수 있습니다. 나머지 엔터티의 경우 구성 워크플로를 지원하기 위해 샘플 데이터가 제공됩니다.

![사용 가능한 Eloqua 데이터 엔터티를 표시하는 데이터 선택 인터페이스입니다.](../../../../images/tutorials/create/eloqua/select-data.png)

## 데이터 세트 및 데이터 흐름 세부 정보 {#details}

그런 다음 데이터 세트 및 데이터 흐름에 대한 정보를 제공해야 합니다. 이 단계에서는 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다. 또한 이 단계 중에 실시간 고객 프로필에 수집하기 위한 데이터 세트를 선택적으로 활성화할 수 있습니다.

![데이터 집합 속성을 구성하는 옵션이 있는 데이터 집합 및 데이터 흐름 세부 정보 인터페이스입니다.](../../../../images/tutorials/create/eloqua/details.png)

## 매핑 {#mapping}

[!DNL Eloqua]에 대한 매핑은 네 가지 기본 엔터티 형식으로 구성됩니다.

* **계정** - [!DNL Eloqua]의 회사/조직 레코드입니다.
* **활동** - [!DNL Eloqua]의 마케팅 활동 및 참여 이벤트.
* **캠페인** - [!DNL Eloqua]의 마케팅 캠페인 레코드.
* **연락처** - [!DNL Eloqua]의 개별 개인 레코드입니다.

기본적으로 제공되는 필드 이상의 추가 필드에 액세스해야 하는 경우 Experience Platform의 데이터 준비 매핑 프로세스를 사용하여 이러한 필드를 추가할 수 있습니다. 기본(표준) 스키마가 필수 필드 일부를 지원하지 않는 경우 Experience Platform에서 사용자 지정 스키마를 정의할 수 있습니다. 이 기능을 사용하여 필요한 필드를 만들고 매핑하면 [!DNL Eloqua]에서 Experience Platform으로 모든 관련 데이터를 원활하게 수집할 수 있습니다.

다음 단계 요약:

* 통합에서 사용할 수 있는 기본 매핑된 필드를 검토합니다.
* 매핑 단계에서 [!DNL Eloqua]에서 필요한 추가 필드를 포함합니다.
* 새 필드가 표준 스키마에 없는 경우 이러한 필드를 포함하는 Experience Platform에서 사용자 지정 스키마를 확장하거나 만듭니다.
* 매핑을 완료하여 원하는 데이터가 모두 수집되도록 합니다.

외부 CRM 정보가 정확하게 반영되도록 하려면 데이터 준비에서 계산된 필드 함수를 사용하여 원본 데이터 필드의 특정 CRM 인스턴스 ID로 `{CRM_INSTANCE_ID}` 자리 표시자를 업데이트하면 됩니다. 이렇게 하면 조직의 고유한 설정에 맞게 통합을 조정할 수 있는 유연성을 제공합니다.

계산된 필드 편집기를 사용하려면 업데이트할 소스 필드를 선택합니다.

![계산된 필드가 있는 Eloqua 원본 필드입니다.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

[!DNL Salesforce] 사용자의 경우 계산된 필드 편집기를 사용하고 `{CRM_INSTANCE_ID}`을(를) 적절한 인스턴스 ID로 업데이트하십시오.

![Salesforce의 계산된 필드입니다.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

[!DNL Microsoft] 사용자의 경우 계산된 필드 편집기를 사용하고 `{CRM_INSTANCE_ID}`을(를) 적절한 인스턴스 ID로 업데이트하십시오.

![Dynamics에 대해 계산된 필드입니다.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

계산된 필드를 업데이트했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택하여 계속합니다.

![Eloqua 데이터 엔터티에 대한 필드 매핑을 보여 주는 매핑 인터페이스입니다.](../../../../images/tutorials/create/eloqua/mapping.png)

## 일정 조정

>[!NOTE]
>
>다음은 증분 데이터 로드를 위해 내부적으로 사용되는 델타 필드입니다.
>
>* **연락처:** `C_DateModified`
>* **계정:** `M_DateModified`
>* **활동:** `CreatedAt`
>* **사용자 지정 개체:** `UpdatedAt`
>* **캠페인:** `updatedAt`

이제 매핑이 완료되면 데이터 흐름에 대한 수집 일정을 구성할 수 있습니다. [!UICONTROL Frequency]을(를) `Once`(으)로 설정하여 일회성 수집 실행을 구성합니다. 증분 수집의 경우 [!UICONTROL Frequency]을(를) `Hour`, `Day` 또는 `Week`(으)로 설정할 수 있습니다. 증분 수집을 사용할 때는 수집 실행 사이에 발생하는 시간을 정의하도록 [!UICONTROL Interval]을(를) 구성해야 합니다. 예를 들어 수집 빈도를 `Day`(으)로 설정하고 간격을 `15`(으)로 설정하면 데이터 흐름이 15일마다 데이터를 수집하도록 예약됩니다.

[!DNL Eloqua] 원본에는 분당 수집 빈도를 사용할 수 없습니다. 선택할 수 있는 가장 빈번한 일정은 시간별입니다. 데이터 새로 고침 요구 사항과 일치하는 일정을 선택하십시오. 더 자주 일정을 선택하면 컴퓨팅 비용이 증가한다는 점을 명심하십시오.

![수집 빈도 및 간격을 구성할 수 있는 옵션이 있는 예약 인터페이스입니다.](../../../../images/tutorials/create/eloqua/scheduling.png)

## 검토

수집 일정을 구성한 상태에서 [!UICONTROL Review] 인터페이스를 사용하여 데이터 흐름의 세부 정보를 확인합니다. **[!UICONTROL Finish]**&#x200B;을(를) 선택하여 설정을 완료하고 데이터 흐름을 시작할 수 있도록 잠시 기다려 주십시오.

![완료 전 데이터 흐름 구성의 요약을 표시하는 검토 인터페이스입니다.](../../../../images/tutorials/create/eloqua/review.png)

## 모니터

데이터 흐름을 선택하면 지정된 일정에 따라 데이터의 일회성 채우기 및 후속 증분 동기화가 수행됩니다. 데이터 흐름으로 이동하여 동기화 상태를 모니터링할 수 있습니다. 자세한 내용은 [UI에서 원본 데이터 흐름 모니터링](../../../../../dataflows/ui/monitor-sources.md)에 대한 안내서를 참조하십시오.

## 다음 단계

이제 Experience Platform에서 [!DNL Eloqua] 소스의 설정 및 구성을 완료했습니다. 데이터 흐름이 설정되면 [!DNL Eloqua] 데이터가 선택한 일정에 따라 수집되고 표준 Experience Data Model(XDM) 스키마에 매핑됩니다. 데이터 흐름을 계속 모니터링하고 플랫폼 내에서 수집된 데이터를 탐색하여 통찰력을 얻고 마케팅 사용 사례를 활성화합니다. 고급 구성 및 문제 해결에 대한 자세한 내용은 관련 설명서를 참조하거나 Adobe 지원 리소스에 문의하십시오.

자세한 내용은 다음 설명서를 참조하십시오.

* [소스 개요](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
