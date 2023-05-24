---
keywords: Amazon Kinesis;kinesis 대상;kinesis
title: Amazon Kinesis 연결
description: Amazon Kinesis 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform에서 데이터를 스트리밍합니다.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 4%

---

# [!DNL Amazon Kinesis] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
> 이 대상은 다음에만 사용할 수 있습니다. [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객.

다음 [!DNL Kinesis Data Streams] 서비스 기준 [!DNL Amazon Web Services] 에서는 실시간으로 큰 데이터 레코드 스트림을 수집하고 처리할 수 있습니다.

에 대한 실시간 아웃바운드 연결을 만들 수 있습니다. [!DNL Amazon Kinesis] Adobe Experience Platform에서 데이터를 스트리밍할 저장소입니다.

* 에 대한 자세한 내용 [!DNL Amazon Kinesis], 다음을 참조하십시오. [Amazon 설명서](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* 에 연결하려면 [!DNL Amazon Kinesis] 프로그래밍 방식으로 다음을 참조하십시오 [스트리밍 대상 API 튜토리얼](../../api/streaming-destinations.md).
* 에 연결하려면 [!DNL Amazon Kinesis] platform 사용자 인터페이스를 사용하는 방법은 아래 섹션을 참조하십시오.

![UI의 Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 사용 사례 {#use-cases}

다음과 같은 스트리밍 대상을 사용하여 [!DNL Amazon Kinesis]를 사용하면 고부가가치 세분화 이벤트 및 관련 프로필 속성을 선택한 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 백서를 다운로드하여 &quot;높은 전환 성향&quot; 세그먼트로 분류했습니다. 잠재 고객이 속한 세그먼트를 [!DNL Amazon Kinesis] 대상, 다음 위치에서 이 이벤트를 수신하게 됨: [!DNL Amazon Kinesis]. 여기서는 엔터프라이즈 IT 시스템과 가장 잘 작동할 것으로 생각되므로 DIY(Do-It-Yourself) 방식을 채택하고 이벤트 상단에 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 허용 목록에 추가하다 IP 주소 {#ip-address-allowlist}

Experience Platform은 고객의 보안 및 규정 준수 요구 사항을 충족하기 위해 허용 목록에 추가하다가 제공할 수 있는 정적 IP 목록을 제공합니다. [!DNL Amazon Kinesis] 대상. 을(를) 참조하십시오 [스트리밍 대상의 IP 주소 허용 목록](/help/destinations/catalog/streaming/ip-address-allow-list.md) 전체 IP 목록을 보려면 허용 목록에 추가하다를 선택합니다.

## 필수 [!DNL Amazon Kinesis] 권한 {#required-kinesis-permission}

에 데이터를 성공적으로 연결하고 내보내려면 [!DNL Amazon Kinesis] 스트림, Experience Platform은 다음 작업에 대한 권한이 필요합니다.

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

이러한 권한은 [!DNL Kinesis] Platform 사용자 인터페이스에서 Kinesis 대상을 구성하면 콘솔이 제공되고 Platform에서 확인합니다.

아래 예제는 데이터를 로 내보내는 데 필요한 최소 액세스 권한을 표시합니다. [!DNL Kinesis] 대상.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `kinesis:ListStreams` | Amazon Kinesis 데이터 스트림을 나열하는 작업입니다. |
| `kinesis:PutRecord` | 단일 데이터 레코드를 Kinesis 데이터 스트림에 쓰는 작업입니다. |
| `kinesis:PutRecords` | 한 번의 호출로 여러 데이터 레코드를 Kinesis 데이터 스트림에 쓰는 작업입니다. |

{style="table-layout:auto"}

에 대한 액세스 제어에 대한 자세한 내용 [!DNL Kinesis] 데이터 스트림, 다음 내용 읽기 [[!DNL Kinesis] 문서](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 이 대상에 연결할 때 다음 정보를 제공해야 합니다.

### 인증 정보 {#authentication-information}

아래 필드를 입력하고 선택 **[!UICONTROL 대상에 연결]**:

![Amazon Kinesis 인증 세부 정보에 대한 완료된 필드를 보여주는 UI 화면의 이미지](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]액세스 키 및 비밀 키**: 위치 [!DNL Amazon Web Services], 생성 `access key - secret access key` 쌍으로 플랫폼에 액세스 권한 부여 [!DNL Amazon Kinesis] 계정입니다. 다음에서 자세히 알아보기 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 지역]**: 다음 항목을 나타냄 [!DNL Amazon Web Services] 데이터를 스트리밍할 지역입니다.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="세그먼트 이름 포함"
>abstract="데이터 내보내기에 내보내는 세그먼트 이름이 포함되도록 하려면 전환하십시오. 이 옵션을 선택한 경우 데이터 내보내기 예는 설명서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="세그먼트 타임스탬프 포함"
>abstract="세그먼트를 생성 및 업데이트하거나 세그먼트를 대상에 매핑하여 활성화하는 경우 데이터 내보내기에 Unix 타임스탬프가 포함되도록 하려면 전환하십시오. 이 옵션을 선택한 경우 데이터 내보내기 예는 설명서를 참조하십시오."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![Amazon Kinesis 대상 세부 사항에 대한 완료된 필드를 보여주는 UI 화면의 이미지](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL 이름]**: 연결 이름을 입력합니다. [!DNL Amazon Kinesis]
* **[!UICONTROL 설명]**: 연결에 대한 설명을 입력합니다. [!DNL Amazon Kinesis].
* **[!UICONTROL 스트림]**: 의 기존 데이터 스트림 이름을 제공합니다. [!DNL Amazon Kinesis] 계정입니다. 플랫폼에서 데이터를 이 스트림으로 내보냅니다.
* **[!UICONTROL 세그먼트 이름 포함]**: 내보내는 세그먼트의 이름을 데이터 내보내기에 포함시키려면 전환합니다. 이 옵션을 선택한 데이터 내보내기의 예는 다음을 참조하십시오. [내보낸 데이터](#exported-data) 추가 아래에 섹션을 추가했습니다.
* **[!UICONTROL 세그먼트 타임스탬프 포함]**: 세그먼트를 만들고 업데이트할 때 UNIX 타임스탬프와, 세그먼트가 활성화 대상에 매핑될 때 UNIX 타임스탬프를 데이터 내보내기에 포함하도록 하려면 전환합니다. 이 옵션을 선택한 데이터 내보내기의 예는 다음을 참조하십시오. [내보낸 데이터](#exported-data) 추가 아래에 섹션을 추가했습니다.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

## 프로필 내보내기 동작 {#profile-export-behavior}

Experience Platform은 프로필의 내보내기 동작을 [!DNL Amazon Kinesis] 대상 : 세그먼트 자격 또는 기타 중요한 이벤트 후에 프로필에 대한 관련 업데이트가 발생한 경우에만 데이터를 대상으로 내보냅니다. 프로필은 다음과 같은 경우 대상으로 내보내집니다.

* 프로필 업데이트는 대상에 매핑된 세그먼트 중 하나 이상에 대한 세그먼트 멤버십 변경에 따라 결정되었습니다. 예를 들어 프로필이 대상에 매핑된 세그먼트 중 하나에 대해 자격이 있거나 대상에 매핑된 세그먼트 중 하나를 종료했습니다.
* 프로필 업데이트는 의 변경 사항으로 결정됩니다. [id 맵](/help/xdm/field-groups/profile/identitymap.md). 예를 들어 대상에 매핑된 세그먼트 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 속성에 새 ID를 추가했습니다.
* 프로필 업데이트는 대상에 매핑된 속성 중 하나 이상에 대한 속성 변경에 의해 결정되었습니다. 예를 들어 매핑 단계에서 대상에 매핑된 속성 중 하나가 프로필에 추가됩니다.

위에서 설명한 모든 경우에 관련 업데이트가 발생한 프로필만 대상으로 내보냅니다. 예를 들어 대상 흐름에 매핑된 세그먼트에 100명의 멤버가 있고 5개의 새 프로필이 세그먼트에 적합한 경우 대상으로 내보내기는 증분 방식으로 5개의 새 프로필만 포함합니다.

변경 내용이 있는 위치에 관계없이 매핑된 모든 속성을 프로파일에 대해 내보냅니다. 따라서 위의 예에서는 속성 자체가 변경되지 않았더라도 이러한 5개의 새 프로필에 대해 매핑된 모든 속성을 내보냅니다.

### 데이터 내보내기를 결정하는 사항 및 내보내기에 포함되는 사항 {#what-determines-export-what-is-included}

주어진 프로필에 대해 내보내는 데이터와 관련하여 의 두 가지 다른 개념을 이해하는 것이 중요합니다 *로 데이터 내보내기를 결정하는 것은 무엇입니까? [!DNL Amazon Kinesis] 대상* 및 *내보내기에 포함되는 데이터*.

| 대상 내보내기를 결정하는 사항 | 대상 내보내기에 포함된 사항 |
|---------|----------|
| <ul><li>매핑된 속성 및 세그먼트는 대상 내보내기에 대한 큐 역할을 합니다. 즉, 매핑된 세그먼트의 상태가 다음의 상태로 변경됩니다. `null` 끝 `realized` 또는 부터 `realized` 끝 `exiting`) 매핑된 속성이 업데이트되면 대상 내보내기가 시작됩니다.</li><li>ID를 현재 (으)로 매핑할 수 없으므로 [!DNL Amazon Kinesis] 대상, 특정 프로필의 id 변경 사항에 따라 대상 내보내기도 결정됩니다.</li><li>속성에 대한 변경 사항은 동일한 값인지 여부에 관계없이 속성에 대한 모든 업데이트로 정의됩니다. 즉, 값 자체가 변경되지 않았더라도 속성에 대한 덮어쓰기를 변경 사항으로 간주합니다.</li></ul> | <ul><li>다음 `segmentMembership` 객체에는 활성화 데이터 흐름에서 매핑된 세그먼트가 포함됩니다. 이 세그먼트의 자격 또는 세그먼트 종료 이벤트 후 프로필 상태가 변경되었습니다. 프로필의 자격이 되는 매핑되지 않은 다른 세그먼트는 대상 내보내기의 일부가 될 수 있습니다(이러한 세그먼트가 동일한 세그먼트에 속하는 경우) [병합 정책](/help/profile/merge-policies/overview.md) 활성화 데이터 흐름에서 매핑된 세그먼트로 사용됩니다. </li><li>의 모든 ID `identityMap` 개체도 포함됩니다(Experience Platform은 현재 [!DNL Amazon Kinesis] destination).</li><li>매핑된 속성만 대상 내보내기에 포함됩니다.</li></ul> |

{style="table-layout:fixed"}

예를 들어 다음과 같은 데이터 흐름을 고려해 보십시오. [!DNL Amazon Kinesis] 대상: 데이터 흐름에서 3개의 세그먼트가 선택되고 4개의 속성이 대상에 매핑되는 대상.

![Amazon Kinesis 대상 데이터 흐름](../../assets/catalog/http/profile-export-example-dataflow.png)

대상으로 프로필을 내보내는 방법은 대상 중 하나를 선택하거나 종료하는 프로필에 의해 결정됩니다. *세 개의 매핑된 세그먼트*. 그러나 데이터 내보내기에서 `segmentMembership` 오브젝트(참조) [내보낸 데이터](#exported-data) 아래 섹션) 특정 프로필이 멤버이고 내보내기를 트리거한 세그먼트와 동일한 병합 정책을 공유하는 경우 매핑되지 않은 다른 세그먼트가 나타날 수 있습니다. 프로필이 다음에 대한 자격이 있는 경우: **DeLorean 자동차를 사용하는 고객** 세그먼트이지만 의 구성원이기도 합니다. **Back to the Future 시청** 동영상 및 **의 팬** 세그먼트를 가리키면 이 다른 두 세그먼트도 `segmentMembership` 데이터 흐름에서 매핑되지 않은 데이터 내보내기의 객체입니다. 이러한 객체가 과 동일한 병합 정책을 공유하는 경우 **DeLorean 자동차를 사용하는 고객** 세그먼트.

프로필 속성 관점에서 위에 매핑된 네 개의 속성에 대한 변경 사항은 대상 내보내기를 결정하고 프로필에 있는 네 개의 매핑된 속성 중 하나는 데이터 내보내기에 표시됩니다.

## 내역 데이터 채우기 {#historical-data-backfill}

기존 대상에 새 세그먼트를 추가하거나 새 대상을 만들고 세그먼트를 대상에 매핑하면 Experience Platform은 이전 세그먼트 자격 데이터를 대상에 내보냅니다. 세그먼트에 적합한 프로필 *다음 이전* 대상에 추가된 세그먼트는 약 1시간 이내에 대상으로 내보내집니다.

## 내보낸 데이터 {#exported-data}

내보냄 [!DNL Experience Platform] 에 있는 데이터 영역 [!DNL Amazon Kinesis] JSON 형식의 대상. 예를 들어, 아래 내보내기에는 특정 세그먼트에 대해 자격이 있고 다른 두 세그먼트의 구성원이며 다른 세그먼트를 종료한 프로필이 포함됩니다. 내보내기에는 프로필 속성 이름, 성, 생년월일 및 개인 이메일 주소도 포함됩니다. 이 프로필의 ID는 ECID와 이메일입니다.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
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

아래는 다음에 대한 연결 대상 흐름에서 선택한 UI 설정에 따라 내보낸 데이터의 추가 예입니다. **[!UICONTROL 세그먼트 이름 포함]** 및 **[!UICONTROL 세그먼트 타임스탬프 포함]** 옵션:

+++ 아래의 데이터 내보내기 샘플에는 `segmentMembership` 섹션

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ 아래의 데이터 내보내기 샘플에는 의 세그먼트 타임스탬프가 포함됩니다. `segmentMembership` 섹션

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## 제한 및 재시도 정책 {#limits-retry-policy}

시간의 95%에서 Experience Platform은 HTTP 대상에 대한 각 데이터 흐름의 초당 요청 수가 10,000개 미만인 상태로 성공적으로 전송된 메시지에 대해 10분 미만의 처리량 지연 시간을 제공하려고 합니다.

HTTP API 대상에 대한 요청이 실패한 경우 Experience Platform은 실패한 요청을 저장하고 두 번 다시 시도하여 요청을 엔드포인트에 보냅니다.

>[!MORELIKETHIS]
>
>* [Amazon Kinesis에 연결하고 플로우 서비스 API를 사용하여 데이터를 활성화합니다](../../api/streaming-destinations.md)
>* [Azure 이벤트 허브 대상](./azure-event-hubs.md)
>* [대상 유형 및 범주](../../destination-types.md)

