---
title: 대상에 프로필 및 세그먼트 활성화
seo-title: 대상에 프로필 및 세그먼트 활성화
description: 세그먼트를 대상에 매핑하여 Adobe 실시간 고객 데이터 플랫폼의 데이터를 활성화합니다. 이를 수행하려면 아래 단계를 따르십시오.
seo-description: 세그먼트를 대상에 매핑하여 Adobe 실시간 고객 데이터 플랫폼의 데이터를 활성화합니다. 이를 수행하려면 아래 단계를 따르십시오.
translation-type: tm+mt
source-git-commit: faaa4eda5174bb8d27a76d767891df15df69e30a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# 대상에 프로필 및 세그먼트 활성화

세그먼트를 대상에 매핑하여 Adobe 실시간 고객 데이터 플랫폼의 데이터를 활성화합니다. 이를 수행하려면 아래 단계를 따르십시오.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 대상을 [연결했어야 합니다](/help/rtcdp/destinations/assets/connect-destination.png). 아직 수행하지 않은 경우 [대상 카탈로그로](/help/rtcdp/destinations/destinations-catalog.md)이동하여 지원되는 대상을 탐색하고 하나 이상의 대상을 설정합니다.

## 데이터 활성화 {#activate-data}

1. 대상 **[!UICONTROL > 찾아보기에서]**&#x200B;세그먼트를 활성화할 대상을 선택합니다.
2. 대상의 이름을 클릭합니다. 활성화 흐름으로 이동합니다.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)대상에 대한 활성화 흐름이 이미 있는 경우 대상에 현재 전송되고 있는 세그먼트를 볼 수 있습니다. 오른쪽 레일에서 **[!UICONTROL 활성화]** 편집을 선택하고 아래 단계에 따라 정품 인증 세부 사항을 수정합니다.
3. 활성화 **[!UICONTROL 를]**&#x200B;선택합니다.
4. 대상 **[!UICONTROL 활성화]** 워크플로의 세그먼트 **[!UICONTROL 선택]** 페이지에서 대상에 전송할 세그먼트를 선택합니다.
   ![세그먼트-대상](/help/rtcdp/destinations/assets/select-segments.png)
5. *조건부*. 이 단계는 세그먼트를 활성화하려는 대상 유형에 따라 다릅니다. <br> *이메일 대상* 및 *클라우드 스토리지 대상*&#x200B;의 경우 [속성 **[!UICONTROL 선택]** ] 페이지에서 새 필드 **** 추가새 필드를 선택하고 대상에 보낼 속성을 선택합니다.
특성 중 하나를 조합 스키마에서 [고유한](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 식별자로 사용하는 것이 좋습니다. 필수 속성에 대한 자세한 내용은 [이메일 마케팅 대상](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 아티클의 ID를 참조하십시오.
   ![대상 속성](/help/rtcdp/destinations/assets/select-attributes-step.png)*소셜 네트워크 대상*&#x200B;의 경우 **[!UICONTROL ID 매핑]** 단계에서 대상 ID에 매핑할 소스 속성을 선택합니다.
   ![필드를 채우기 전 ID 매핑](/help/rtcdp/destinations/assets/facebook-identity-mapping-1.png)아래 예에서 ID 스키마의 개인 이메일 주소는 Facebook [이메일 해싱 요구 사항을 준수하기 위해 Experience Platform으로 수집되었습니다](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements). 매핑을 **[!UICONTROL 선택한]** 후 [다음]을 누릅니다.
   ![필드 채우기 후 ID 매핑](/help/rtcdp/destinations/assets/facebook-identity-mapping-2.png)

6. [ **[!UICONTROL 세그먼트 예약]** ] 페이지에서는 대상으로 데이터를 전송하는 시작 날짜와 대상으로 데이터를 보내는 빈도를 확인할 수 있습니다.

   >[!IMPORTANT]
   >
   >소셜 대상의 경우 이 단계에서 대상의 출처를 선택해야 합니다. 아래 이미지에서 옵션 중 하나를 선택한 후에만 다음 단계로 진행할 수 있습니다.

   ![데이터 원본 선택](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. [ **[!UICONTROL 검토]** ] 페이지에서 선택 사항의 요약을 볼 수 있습니다. 흐름을 구분하려면 **[!UICONTROL 취소]** 를, 설정을 **[!UICONTROL 수정하려면]** [뒤로]를, **[!UICONTROL 마침을]** 선택하여 선택을 확인하고 데이터를 대상에 보내기 시작합니다.

![선택 확인](/help/rtcdp/destinations/assets/confirm-selection.png)

## 활성화 편집 {#edit-activation}

아래 절차에 따라 실시간 CDP에서 기존 정품 인증 과정을 편집합니다.

1. 왼쪽 **[!UICONTROL 탐색 막대에서 대상을]** 선택한 다음 **[!UICONTROL 찾아보기]** 탭을 클릭하고 대상 이름을 클릭합니다.
2. 오른쪽 레일에서 **[!UICONTROL 활성화]** 편집을 선택하여 대상으로 전송할 세그먼트를 변경합니다.

## 세그먼트 활성화 성공 여부 확인 {#verify-activation}

### 이메일 마케팅 대상 및 클라우드 스토리지 대상

이메일 마케팅 대상 및 클라우드 스토리지 대상의 경우 Adobe Real-time CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 파일이나 `.csv` 파일을 생성합니다. 저장 위치에 매일 새 파일이 만들어집니다. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

3일 연속으로 받은 파일은 다음과 같습니다.

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

스토리지 위치에 이러한 파일이 있는지 확인한 후 정품 인증을 완료했습니다.

### 광고 대상

데이터를 활성화할 각 광고 대상을 확인합니다. 정품 인증이 성공적으로 완료되면 광고 플랫폼에 대상이 채워집니다.

### 소셜 네트워크 대상

Facebook의 경우 활성화는 Facebook 광고 관리자에서 프로그래밍 방식으로 Facebook 사용자 지정 대상을 [만들게 됩니다](https://www.facebook.com/adsmanager/manage/). 사용자가 활성화된 세그먼트에 대해 자격이 부여되거나 자격이 부여되면 대상의 세그먼트 멤버십이 추가되고 제거됩니다.

>[!TIP]
>
>Adobe Real-time CDP와 Facebook의 통합으로 이전 고객 채우기가 지원됩니다. 세그먼트를 대상으로 활성화하면 모든 내역 세그먼트 자격 조건은 Facebook으로 전송됩니다.

## 활성화 비활성화 {#disable-activation}

기존 활성화 흐름을 비활성화하려면 아래 단계를 수행하십시오.

1. 왼쪽 **[!UICONTROL 탐색 막대에서 대상을]** 선택한 다음 **[!UICONTROL 찾아보기]** 탭을 클릭하고 대상 이름을 클릭합니다.
2. 오른쪽 레일에 **[!UICONTROL 있는]** Enabled 컨트롤을 클릭하여 활성화 흐름 상태를 변경합니다.
3. 데이터 흐름 상태 **업데이트** 창에서 **확인** 을 선택하여 활성화 흐름을 비활성화합니다.

AWS Kinesis에서 액세스 키(비밀 액세스 키 쌍)를 생성하여 Adobe에서 AWS Kinesis 계정에 대한 실시간 CDP 액세스를 부여합니다. 자세한 내용은 [AWS Kinesis 설명서를 참조하십시오](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).