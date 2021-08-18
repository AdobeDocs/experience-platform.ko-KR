---
keywords: 프로필 대상 활성화;대상 활성화;데이터 활성화 이메일 마케팅 대상 활성화 클라우드 스토리지 대상 활성화
title: 스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화
type: Tutorial
seo-title: 스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화
description: 세그먼트를 스트리밍 프로필 기반 대상으로 보내 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
seo-description: 세그먼트를 스트리밍 프로필 기반 대상으로 보내 Adobe Experience Platform에서 보유한 대상 데이터를 활성화하는 방법을 알아봅니다.
source-git-commit: f0c854e1b6b89d499c720328fa5054611147772f
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# 스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화

## 개요 {#overview}

이 문서에서는 Amazon Kinesis과 같은 Adobe Experience Platform 스트리밍 프로필 기반 대상에서 대상 데이터를 활성화하는 데 필요한 워크플로우를 설명합니다.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 [이(가) 대상](./connect-destination.md)에 연결되어 있어야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

## 대상을 선택합니다 {#select-destination}

1. **[!UICONTROL 연결 > 대상]**&#x200B;으로 이동하고 **[!UICONTROL 찾아보기]** 탭을 선택합니다.

   ![대상 찾아보기 탭](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. 아래 그림과 같이 세그먼트를 활성화할 대상에 해당하는 **[!UICONTROL 세그먼트 추가]** 단추를 선택하십시오.

   ![단추 활성화](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

1. 다음 섹션으로 이동하여 [세그먼트 선택](#select-segments).

## 세그먼트 선택 {#select-segments}

세그먼트 이름의 왼쪽에 있는 확인란을 사용하여 대상으로 활성화할 세그먼트를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![세그먼트 선택](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## 프로필 속성 선택 {#select-attributes}

대상 대상으로 전송할 프로필 속성을 선택합니다.

>[!NOTE]
>
> Adobe Experience Platform은 스키마에서 일반적으로 사용되는 4가지 권장 속성으로 선택 사항을 미리 채웁니다. `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

파일 내보내기는 `segmentMembership.status` 선택 여부에 따라 다음과 같은 방식으로 달라집니다.
* `segmentMembership.status` 필드를 선택하면 내보낸 파일에는 초기 전체 스냅샷의 **[!UICONTROL Active]** 멤버와 후속 증분 내보내기의 **[!UICONTROL Active]** 및 **[!UICONTROL Expired]** 멤버가 포함됩니다.
* `segmentMembership.status` 필드를 선택하지 않으면 내보낸 파일에는 초기 전체 스냅샷과 후속 증분 내보내기에 **[!UICONTROL Active]** 멤버만 포함됩니다.

![권장 속성](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. **[!UICONTROL 속성 선택]** 페이지에서 **[!UICONTROL 새 필드 추가]**&#x200B;를 선택합니다.

   ![새 매핑 추가](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. **[!UICONTROL 스키마 필드]** 항목 오른쪽에 있는 화살표를 선택합니다.

   ![소스 필드 선택](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. **[!UICONTROL 필드 선택]** 페이지에서 대상으로 전송할 XDM 속성을 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 선택합니다.

   ![소스 필드 선택 페이지](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. 매핑을 더 추가하려면 1단계부터 3단계까지 반복한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 검토 {#review}

**[!UICONTROL 검토]** 페이지에서 선택 요약이 표시됩니다. **[!UICONTROL 취소]**&#x200B;를 선택하여 플로우를 분류하고, 설정을 수정하려면 **[!UICONTROL 뒤로]**&#x200B;를 선택하고, 선택 내용을 확인하고 데이터를 대상에 보내려면 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

>[!IMPORTANT]
>
>이 단계에서 Adobe Experience Platform은 데이터 사용 정책 위반을 확인합니다. 아래는 정책이 위반되는 예입니다. 위반을 해결해야 세그먼트 활성화 워크플로우를 완료할 수 있습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 설명서 섹션의 [정책 적용](../../rtcdp/privacy/data-governance-overview.md#enforcement)을 참조하십시오.

![데이터 정책 위반](../assets/common/data-policy-violation.png)

정책 위반이 감지되지 않은 경우 **[!UICONTROL 완료]**&#x200B;를 선택하여 선택 내용을 확인하고 데이터를 대상에 보냅니다.

![검토](../assets/ui/activate-streaming-profile-destinations/review.png)

## 세그먼트 활성화 확인 {#verify}

내보낸 [!DNL Experience Platform] 데이터가 JSON 형식으로 대상 대상에 배치됩니다. 예를 들어, 아래 이벤트는 특정 세그먼트에 대해 자격이 있고 다른 세그먼트를 종료한 대상의 이메일 주소 프로필 속성을 포함합니다. 이 잠재 고객의 ID는 ECID 및 이메일입니다.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
