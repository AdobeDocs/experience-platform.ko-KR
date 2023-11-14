---
keywords: 프로필 대상 활성화;대상 활성화;데이터 활성화; 이메일 마케팅 대상 활성화; 클라우드 스토리지 대상 활성화
title: 스트리밍 프로필 내보내기 대상에 대상자 활성화
type: Tutorial
description: 스트리밍 프로필 기반 대상으로 대상자를 전송하여 Adobe Experience Platform에 있는 대상자 데이터를 활성화하는 방법을 알아봅니다.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 5%

---


# 스트리밍 프로필 내보내기 대상에 대상자 활성화

>[!IMPORTANT]
> 
> * 데이터를 활성화하고 활성화하려면 [매핑 단계](#mapping) 워크플로의 경우 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions).
> * 을(를) 거치지 않고 데이터를 활성화하려면 [매핑 단계](#mapping) 워크플로의 경우 **[!UICONTROL 대상 관리]**, **[!UICONTROL 매핑 없이 세그먼트 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions).
> 
> 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

## 개요 {#overview}

이 문서에서는 Amazon Kinesis과 같은 Adobe Experience Platform 스트리밍 프로필 기반 대상에서 대상 데이터를 활성화하는 데 필요한 워크플로에 대해 설명합니다.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 가 정상적으로 작동해야 합니다. [대상에 연결됨](./connect-destination.md). 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)에서 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 대상 선택 {#select-destination}

1. 다음으로 이동 **[!UICONTROL 연결 > 대상]**&#x200B;을(를) 클릭하고 **[!UICONTROL 카탈로그]** 탭.

   ![대상 카탈로그 탭을 표시하는 이미지.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 선택 **[!UICONTROL 대상자 활성화]** 아래 이미지에 표시된 대로 대상을 활성화할 대상에 해당하는 카드에.

   ![대상 카탈로그 탭에서 대상 활성화 컨트롤을 강조 표시하는 이미지.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. 대상을 활성화하는 데 사용할 대상 연결을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

   ![연결할 수 있는 두 개의 대상 선택을 보여 주는 이미지입니다.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 다음 섹션으로 이동 [대상자 선택](#select-audiences).

## 대상자 선택 {#select-audiences}

대상에 대해 활성화할 대상을 선택하려면 대상 이름 왼쪽에 있는 확인란을 사용한 다음 을 선택합니다 **[!UICONTROL 다음]**.

출처에 따라 여러 유형의 대상 중에서 선택할 수 있습니다.

* **[!UICONTROL 세분화 서비스]**: 세분화 서비스에 의해 Experience Platform 내에서 생성된 대상자. 다음을 참조하십시오. [세그멘테이션 설명서](../../segmentation/ui/overview.md) 을 참조하십시오.
* **[!UICONTROL 사용자 정의 업로드]**: Experience Platform 외부에서 생성되어 CSV 파일로 플랫폼에 업로드된 대상자 외부 대상자에 대한 자세한 내용은 [대상자 가져오기](../../segmentation/ui/overview.md#import-audience).
* 다른 Adobe 솔루션에서 가져온 다른 유형의 대상, 예: [!DNL Audience Manager].

![활성화 워크플로의 대상자 선택 단계에서 확인란 선택을 강조 표시하는 이미지.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## 프로필 속성 선택 {#select-attributes}

다음에서 **[!UICONTROL 매핑]** 단계에서는 대상 대상으로 보낼 프로필 속성을 선택합니다.

1. 다음에서 **[!UICONTROL 속성 선택]** 페이지, 선택 **[!UICONTROL 새 필드 추가]**.

   ![매핑 단계에서 새 필드 추가 컨트롤을 강조 표시하는 이미지.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 오른쪽 화살표를 선택합니다. **[!UICONTROL 스키마 필드]** 입력.

   ![매핑 단계에서 소스 필드를 선택하는 방법을 강조 표시하는 이미지입니다.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 다음에서 **[!UICONTROL 필드 선택]** 페이지에서 대상으로 전송할 XDM 속성을 선택한 다음 를 선택합니다 **[!UICONTROL 선택]**.

   ![소스 필드로 선택할 수 있는 선택한 XDM 필드를 보여 주는 이미지입니다.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. 필드를 추가하려면 1~3단계를 반복한 다음 을 선택합니다. **[!UICONTROL 다음]**.

## 검토 {#review}

다음에서 **[!UICONTROL 리뷰]** 페이지에서 선택 사항의 요약을 볼 수 있습니다. 선택 **[!UICONTROL 취소]** 흐름을 끊으려면, **[!UICONTROL 뒤로]** 설정을 수정하려면 **[!UICONTROL 완료]** 을 클릭하여 선택 항목을 확인하고 데이터를 대상으로 보내기 시작합니다.

![검토 단계의 선택 요약입니다.](../assets/ui/activate-streaming-profile-destinations/review.png)

### 동의 정책 평가 {#consent-policy-evaluation}

조직에서 **Adobe Healthcare Shield** 또는 **Adobe Privacy &amp; Security Shield**&#x200B;를 구매한 경우 **[!UICONTROL 해당 동의 정책 보기]**&#x200B;를 선택하여 적용된 동의 정책을 조회하고 그 결과로 활성화에 포함된 프로필 수를 확인합니다. 읽어보기 [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 추가 정보.

### 데이터 사용 정책 확인 {#data-usage-policy-checks}

다음에서 **[!UICONTROL 리뷰]** 단계, Experience Platform은 데이터 사용 정책 위반도 확인합니다. 다음은 정책이 위반되는 예입니다. 위반을 해결할 때까지 대상 활성화 워크플로우를 완료할 수 없습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [데이터 사용 정책 위반](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) (데이터 거버넌스 설명서 섹션)

![데이터 정책 위반](../assets/common/data-policy-violation.png)

### 대상자 필터링 {#filter-audiences}

또한 이 단계에서는 페이지에서 사용 가능한 필터를 사용하여 이 워크플로우의 일부로 일정이나 매핑이 업데이트된 대상자만 표시할 수 있습니다.

![검토 단계에서 사용 가능한 대상 필터를 보여 주는 화면 기록입니다.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

선택에 만족하고 정책 위반이 감지되지 않은 경우 다음을 선택합니다. **[!UICONTROL 완료]** 을 클릭하여 선택 항목을 확인하고 데이터를 대상으로 보내기 시작합니다.

## 대상자 활성화 확인 {#verify}

내보냄 [!DNL Experience Platform] 데이터는 JSON 형식으로 대상 대상에 배치됩니다. 예를 들어 아래 이벤트에는 특정 대상에 대해 자격이 있고 다른 대상을 종료한 프로필의 이메일 주소 속성이 포함되어 있습니다. 이 잠재 고객의 ID는 다음과 같습니다 `ECID` 및 `email_lc_sha256`.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
