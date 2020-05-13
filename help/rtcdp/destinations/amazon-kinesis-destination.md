---
title: Amazon Kinesis 대상
seo-title: Amazon Kinesis 대상
description: Amazon Kinesis 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform에서 데이터를 스트리밍합니다.
seo-description: Amazon Kinesis 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform에서 데이터를 스트리밍합니다.
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# (베타) Amazon Kinesis 대상


>[!IMPORTANT]
>
>Adobe Real-time CDP의 [!DNL Amazon Kinesis] 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

Amazon Web Services의 [!DNL Kinesis Data Streams] 서비스를 사용하면 대용량 데이터 레코드를 실시간으로 수집 및 처리할 수 있습니다.

Adobe Experience Platform에서 데이터를 스트리밍하기 위해 스토리지에 대한 실시간 아웃바운드 연결을 생성할 수 있습니다. [!DNL Amazon Kinesis]

* 자세한 내용 [!DNL Amazon Kinesis]은 [Amazon 설명서를 참조하십시오](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* API 호출 [!DNL Amazon Kinesis] 을 사용하여 연결하려면 [스트리밍 대상 API 자습서를 참조하십시오](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md).
* Adobe 실시간 CDP 사용자 인터페이스를 [!DNL Amazon Kinesis] 사용하여 연결하려면 아래 섹션을 참조하십시오.

![UI의 Amazon Kinesis](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## 사용 사례 {#use-cases}

Amazon Kinesis와 같은 스트리밍 대상을 사용하면 고부가가치 세그멘테이션 이벤트 및 관련 프로필 속성을 원하는 시스템에 손쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 &quot;전환율이 높은&quot; 세그먼트에 자격을 주는 백서를 다운로드했습니다. 잠재 고객이 Amazon Kinesis 대상에 속하는 세그먼트를 매핑하면 Amazon Kinesis에서 이 이벤트를 받게 됩니다. 기업 IT 시스템에서 가장 잘 작동하는 것처럼 현장 중심의 비즈니스 로직을 도입하여 설명할 수 있습니다.

## 연결 대상 {#connect-destination}

클라우드 [스토리지 대상 워크플로우 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)에서 지원하는 클라우드 스토리지 대상을 비롯하여 클라우드 스토리지 대상에 연결하는 방법에 대한 지침을 참조하십시오 [!DNL Amazon].

대상에 대해 [!DNL Amazon Kinesis] 대상 만들기 워크플로우에서 다음 정보를 입력합니다.

### 계정 단계에서 {#account-step}

* **Amazon Web Services 액세스 키 및 비밀 키**: 액세스 키 [!DNL Amazon Web Services]를 생성하여 Adobe에서 실시간 CDP에 계정에 대한 액세스 권한을 [!DNL Amazon Kinesis] 부여합니다. 자세한 내용은 [Amazon 웹 서비스 설명서를 참조하십시오](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **지역**: 데이터를 스트리밍할 [!DNL Amazon Web Services] 지역을 지정합니다.

![계정 단계의 입력 필드](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### 인증 단계에서 {#authentication-step}

* **이름**: 연결 대상 이름 입력 [!DNL Amazon Kinesis]
* **설명**: 연결에 대한 설명을 제공합니다 [!DNL Amazon Kinesis].
* **스트림**: 계정에 있는 기존 데이터 스트림의 이름을 [!DNL Amazon Kinesis] 입력합니다. Adobe 실시간 CDP는 데이터를 이 스트림으로 내보냅니다.

![인증 단계의 입력 필드](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](/help/rtcdp/destinations/activate-destinations.md) 프로필 및 세그먼트 활성화를 참조하십시오.

## 내보낸 데이터 {#exported-data}

내보낸 경험 플랫폼 데이터는 JSON 형식 [!DNL Amazon Kinesis] 으로 배치됩니다. 예를 들어 특정 세그먼트를 종료한 대상의 해시된 이메일 ID가 포함된 이벤트는 다음과 같을 수 있습니다.

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* [Amazon Kinesis에 연결하고 API 호출을 사용하여 데이터 활성화](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Azure 이벤트 허브 대상](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [대상 유형 및 카테고리](/help/rtcdp/destinations/destination-types.md)

