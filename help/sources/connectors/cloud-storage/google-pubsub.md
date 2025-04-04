---
title: Google PubSub Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Google PubSub를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# [!DNL Google PubSub] 원본

>[!IMPORTANT]
>
>[!DNL Google PubSub] 소스는 Real-Time CDP Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

Adobe Experience Platform은 [!DNL AWS], [!DNL Google Cloud Platform] 및 [!DNL Azure]과(와) 같은 클라우드 공급자에 대한 기본 연결을 제공하므로 이러한 시스템에서 다운스트림 서비스 및 대상에서 사용할 데이터를 Experience Platform으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 포맷 또는 업로드 없이도 데이터를 Experience Platform으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. Experience Platform을 사용하면 [!DNL Google PubSub]에서 실시간으로 데이터를 가져올 수 있습니다.

## 전제 조건 {#prerequisites}

이 섹션에서는 [!DNL Google PubSub] 계정을 Experience Platform에 연결하기 전에 완료해야 하는 필수 구성 요소 설정에 대해 설명합니다.

### 서비스 계정 만들기 {#create-service-account}

**서비스 계정**&#x200B;은(는) 사용자가 아닌 응용 프로그램에서 자주 사용하는 계정 유형입니다. 서비스 계정은 계정에 고유한 이메일 주소로 식별됩니다.

* 서비스 계정은 **보안 주체**&#x200B;이며 [!DNL Google Cloud] 리소스에 대한 액세스 권한을 서비스 계정에 부여할 수 있습니다. 예를 들어 지정된 프로젝트에 대한 연산 관리자 역할 `(roles/compute.admin)`을(를) 서비스 계정에 부여할 수 있습니다. 이렇게 하면 서비스 계정이 해당 특정 프로젝트의 Compute Engine 리소스를 관리할 수 있습니다.
* 다른 한편으로 서비스 계정은 리소스이기도 합니다. 다른 주도자에게 서비스 계정에 액세스할 수 있는 권한을 부여할 수 있습니다. 예를 들어 사용자에게 서비스 계정의 서비스 계정 사용자 역할 `(roles/iam.serviceAccountUser)`을(를) 부여하여 사용자가 해당 서비스 계정을 리소스에 첨부하도록 할 수 있습니다. 또는 사용자에게 서비스 계정 관리자 역할 `(roles/iam.serviceAccountAdmin)`을(를) 부여하여 사용자가 서비스 계정 보기, 편집, 사용 안 함 및 삭제와 같은 작업을 완료할 수 있도록 할 수 있습니다.

사용 사례에 적합한 인증 유형을 결정하는 방법에 대한 자세한 내용은 [[!DNL Google] 인증 방법에 대한 안내서](https://cloud.google.com/docs/authentication)를 참조하십시오.

아래 설명된 단계에 따라 서비스 계정을 만드십시오.

먼저 [!DNL Google Developer Console]의 [!DNL IAM] 페이지로 이동한 다음 **[!DNL Create Service Account]**&#x200B;을(를) 선택합니다.

![Google Developer Console의 서비스 계정 만들기 창](../../images/tutorials/create/google-pubsub/create-service-account.png)

다음으로 서비스 계정의 표시 이름과 ID를 입력한 다음 **[!DNL Create and Continue]**&#x200B;을(를) 선택합니다.

![Google Developer Console의 서비스 계정 세부 정보](../../images/tutorials/create/google-pubsub/service-account-details.png)

### 서비스 계정 키 생성 {#generate-service-account-keys}

서비스 계정에 대한 키를 생성하려면 서비스 계정 페이지에서 키 헤더를 선택합니다. 여기에서 **[!DNL Add key]**&#x200B;을(를) 선택한 다음 드롭다운 메뉴에서 **[!DNL Create new key]**&#x200B;을(를) 선택합니다. 이 패널을 사용하여 기존 키를 업로드할 수도 있습니다.

![Google Developer Console의 키 추가 창](../../images/tutorials/create/google-pubsub/add-key.png)

성공하면 컴퓨터에 개인 키가 저장되었으며 파일이 다운로드된다는 메시지가 표시됩니다. 그런 다음 Experience Platform에서 [!DNL Google PubSub] 계정을 만들 때 이 파일의 콘텐츠를 자격 증명으로 사용할 수 있습니다.

### 주제 및 구독 수준에서 권한 부여 {#grant-permissions}

주제 및 구독 수준에서 권한을 부여하려면 주제 콘솔 페이지로 이동한 다음 **[!DNL Show info panel]**&#x200B;을(를) 선택합니다. 그런 다음 [!DNL Permissions] 탭에서 [!DNL Add Principal]을(를) 선택한 다음 사용 권한과 함께 서비스 계정 사용자를 추가합니다.

![주제 및 구독 수준에서 권한을 부여할 수 있는 Google Developer Console의 팝업 창](../../images/tutorials/create/google-pubsub/add-principal.png)

## 최적의 [!DNL Google PubSub usage]을(를) 위한 구성 {#optimal-configurations}

이 섹션에서는 Experience Platform에서 [!DNL Google PubSub] 소스의 사용을 최적화하기 위해 권장되는 구성에 대해 간략히 설명합니다.

### 구독 속성 {#subscription-properties}

[!DNL Google Developer Console]을(를) 사용하여 **승인 기한을 늘립니다**. 이렇게 하면 메시지를 다시 보내기 전에 사용자가 구성한 시간에따라 [!DNL Google Publisher]이(가) 대기할 수 있습니다. 이러한 지연은 가입자 수준에서 불필요한 부하를 줄이는 데 도움이 된다.

![Google Developer Console의 승인 기한 인터페이스입니다.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

**[!DNL exactly one delivery]** 사용 이 구성은 [!DNL Google Publisher]에게 확인 기한이 만료되기 전에 구독으로 보낸 메시지가 다시 전송되지 않도록 합니다. 이 설정을 사용하여 승인 메시지가 구독으로 다시 전송되지 않도록 할 수 있습니다.

![Google Developer Console에 있는 정확히 하나의 게재 구성 페이지입니다.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

**[!DNL Retry after exponential backoff delay]**&#x200B;을(를) 사용하면 서버를 추가로 압도할 위험을 줄일 수 있습니다. [!DNL Google Developer Console]에서 이 구성을 사용하면 다른 연결을 시도하기 전에 시스템에 복구 시간을 더 많이 제공하여 일시적인 오류(일반적으로 자체적으로 해결되는 임시 오류)를 보다 잘 완화할 수 있습니다.

![Google Developer Console의 다시 시도 정책 창](../../images/tutorials/create/google-pubsub/retry-policy.png)

최대 로드 중에 승인되지 않은 데이터가 손실되지 않도록 하려면 **구독 메시지 보존 기간을 24시간 이상으로 설정해야 합니다**. 또한 **배달 못한 편지 항목을 사용**&#x200B;하여 드물게 발생하는 경계 사례에서도 데이터 손실이 발생하지 않도록 합니다.

>[!IMPORTANT]
>
>[!DNL Google PubSub] 구독당 하나의 원본 데이터 흐름만 만들 수 있습니다. 샌드박스에서 구독을 재사용하면 데이터가 손실됩니다.

## Experience Platform에 [!DNL Google PubSub] 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Google PubSub]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

* [흐름 서비스 API를 사용하여 Google PubSub 소스 연결 만들기](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [흐름 서비스 API를 사용하여 스트리밍 데이터 수집](../../tutorials/api/collect/streaming.md)

### UI 사용

* [UI에서 Google PubSub 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
