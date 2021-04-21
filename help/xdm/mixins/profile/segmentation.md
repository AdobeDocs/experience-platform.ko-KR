---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;세그먼트;세그먼트;세그먼트 구성원 자격;스키마 디자인;맵;맵;
solution: Experience Platform
title: 세그먼트 멤버십 세부 정보 혼합
topic-legacy: overview
description: 이 문서에서는 세그먼트 멤버십 세부 사항 믹싱에 대한 개요를 제공합니다.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# [!UICONTROL Segment Membership Details] 믹싱

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL Segment Membership Details] 는 클래스의 표준  [[!DNL XDM Individual Profile] 혼합입니다](../../classes/individual-profile.md). 이 혼합은 개인이 속한 세그먼트, 마지막 자격 시간, 멤버십이 유효한 시점 등 세그먼트 멤버십과 관련된 정보를 캡처하는 단일 맵 필드를 제공합니다.

>[!WARNING]
>
>`segmentMembership` 필드는 이 믹싱을 사용하여 프로필 스키마에 수동으로 추가해야 하지만 이 필드를 수동으로 채우거나 업데이트해서는 안 됩니다. 세그멘테이션 작업이 수행됨에 따라 시스템은 각 프로파일에 대한 `segmentMembership` 맵을 자동으로 업데이트합니다.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `segmentMembership` | 맵 | 개인의 세그먼트 멤버쉽을 설명하는 지도 객체입니다. 이 개체의 구조는 아래에 자세히 설명되어 있습니다. |

다음은 시스템이 특정 프로필에 대해 채운 예제 `segmentMembership` 맵입니다. 세그먼트 멤버십은 개체의 루트 수준 키로 표시된 대로 네임스페이스별로 정렬됩니다. 따라서 각 네임스페이스 아래의 개별 키는 프로필이 속하는 세그먼트의 ID를 나타냅니다. 각 세그먼트 객체에는 멤버십에 대한 세부 정보를 제공하는 여러 개의 하위 필드가 포함되어 있습니다.

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `xdm:version` | 이 프로필에서 자격이 부여된 세그먼트의 버전. |
| `xdm:lastQualificationTime` | 이 프로필이 세그먼트에 자격을 준 마지막 시간의 타임스탬프. |
| `xdm:validUntil` | 세그먼트 멤버십이 더 이상 유효한 것으로 간주되지 않는 시점의 타임스탬프 |
| `xdm:status` | 세그먼트 멤버십이 현재 요청의 일부로 실현되었는지 여부를 나타냅니다. 다음 값이 허용됩니다. <ul><li>`existing`:프로필이 요청 전에 이미 세그먼트의 일부이며 멤버십을 계속 유지합니다.</li><li>`realized`:프로파일이 현재 요청의 일부로 세그먼트를 입력하고 있습니다.</li><li>`exited`:프로파일이 현재 요청의 일부로 세그먼트를 종료합니다.</li></ul> |
| `xdm:payload` | 일부 세그먼트 멤버십에는 멤버십과 직접 관련된 추가 값을 설명하는 페이로드가 포함됩니다. 각 멤버십에 대해 주어진 유형의 페이로드를 하나만 제공할 수 있습니다. `xdm:payloadType` 페이로드 유형(`boolean`,  `number` `propensity`, 또는  `string`)을 나타내며, 페이로드 유형에 대한 값을 동기 속성에 제공합니다. |

혼합에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
