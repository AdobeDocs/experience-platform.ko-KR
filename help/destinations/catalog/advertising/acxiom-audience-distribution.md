---
title: Acxiom 대상 배포
description: ' [!DNL Acxiom Audience Distribution] 대상을 사용하여 [!DNL Acxiom''s Real ID] 기술로 대상을 향상하고  [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] 등의 여러 플랫폼에 대상을 활성화합니다.'
badge: Beta
source-git-commit: 7db60161b638cce1845c430f6086441599a0bc61
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 6%

---


# [!DNL Acxiom Audience Distribution] 대상

>[!NOTE]
>
>[!DNL Acxiom Audience Distribution] 대상이 Beta 상태입니다. 이 대상 커넥터 및 설명서 페이지는 [!DNL Acxiom] 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 Acxiom에 직접 [여기](mailto:acxiom-adobe-help@acxiom.com)로 문의하십시오.

[!DNL Acxiom Audience Distribution] 대상을 사용하여 [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) 기술로 대상을 향상하고 [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] 등과 같은 여러 플랫폼으로 대상을 활성화하십시오.

이 자습서에서는 [!DNL Adobe Experience Platform] 사용자 인터페이스를 사용하여 [!DNL Acxiom Audience Distribution] 대상 커넥터를 만드는 지침을 제공합니다. 이 커넥터를 사용하여 대상자를 빌드하고 선택한 대상에 배포합니다.

## 사용 사례 {#use-cases}

[!DNL Acxiom Audience Distribution] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Adobe Experience Platform] 고객이 이 커넥터를 사용하여 해결할 수 있는 사용 사례 예제를 소개합니다.

### Experience Platform에서 Acxiom 계정으로 대상자 보내기 {#send-audiences}

채널 간 획득을 위해 대상을 [!DNL Experience Platform]에서 [!DNL Acxiom] 계정으로 보내려는 마케팅 전문가인 경우 이 대상 커넥터를 사용하십시오.

예를 들어 글로벌 금융 서비스 브랜드의 마케팅 운영 부서에서는 여러 광고 플랫폼을 통한 크로스 채널 고객 확보에 관심이 있습니다. [!DNL Acxiom Audience Distribution] 대상 커넥터를 사용하여 대상을 [!DNL Experience Platform]에서 [!DNL Acxiom](으)로 보내고, [!DNL Acxiom's Real ID] 기술로 대상을 향상시키며, [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] 등과 같은 여러 플랫폼에 대상을 활성화할 수 있습니다.

## 전제 조건 {#prerequisites}

* **사용 약관 확인:** 새 [!DNL Acxiom Audience Distribution] 대상을 구성하려면 [!DNL Acxiom's] 사용 약관 계약을 읽고 서명해야 합니다. 실행된 판매 주문이 완료되면 계약 링크를 받게 됩니다. 계약에 서명할 때까지 Experience Platform 대상 카탈로그에 [!DNL Acxiom Audience Distribution] 대상 카드가 표시되지 않습니다. 계약에 동의하고 서명하면 [!DNL Adobe]이(가) 온보딩 프로세스를 완료하고 [!DNL Acxiom Audience Distribution] 대상 카드가 표시됩니다.
* **Adobe 조직 ID를 알고 있습니다.** 사용 약관 계약을 완료하려면 [!DNL Adobe] 조직 ID가 필요합니다. [조직 ID를 보는 방법](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)에 대한 자세한 내용은 [!DNL Adobe's] *Experience Cloud의 조직* 항목을 참조하십시오.

## 지원되는 대상 {#supported-destinations}

[!DNL Acxiom Audience Distribution] 대상은 현재 다음 플랫폼에 대한 대상 활성화를 지원합니다.<br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## 대상에 연결 {#connect}

[!DNL Acxiom's Audience Distribution] 대상에 대한 인증은 사용자 편의를 위해 백그라운드에서 자동으로 처리됩니다.

## 대상별 설정 {#destination-settings}

일부 [!DNL Acxiom Audience Distribution] 대상에 추가 정보가 필요합니다. 아래 섹션에서는 이러한 옵션을 구성하는 방법에 대한 자세한 지침을 제공합니다.

### [!DNL LG Ads] {#lg-ads}

대상에 대한 세부 정보를 구성하려면 아래 필드를 채우십시오.

* **세그먼트 범주**: 세그먼트가 속하는 대상 범주 또는 세로 범주. 예: 금융 서비스, 자동차, 건강 등

![LG 광고 대상 세부 정보](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 참조하십시오.

>[!NOTE]
>
>[!DNL Acxiom Audience Distribution] 대상은 전체 파일 내보내기만 지원합니다.

### 속성 및 ID 매핑 {#map}

[!DNL Acxiom Audience Distribution] 대상이 대상 데이터를 올바르게 수신하려면 Experience Platform의 원본 필드를 올바른 [!DNL Acxiom Audience Distribution] 대상 필드에 매핑해야 합니다.

[!DNL Acxiom Audience Distribution]에서는 다음 대상 필드에 대한 매핑만 허용합니다. 아래 표에 설명된 대상 필드는 아래 표시된 순서대로 매핑해야 합니다.

| 필드 이름 | 설명 | 필수 여부 | 필드 순서 | 최대 길이 |
|---|---|---|---|---|          
| 이름 | 개인의 이름 | 아니요 | 1 | 255 |
| 가운데 | 개인의 중간 이름 또는 이니셜 | 아니요 | 2 | 50 |
| 성 | 개인의 성 | 예 | 3 | 255 |
| 세대 접미사 | 개인의 접미사 | 아니요 | 4 | 10 |
| 주소란 1 | 기본 거주지의 주소 1 필드 | 예 | 5 | 255 |
| 주소란 2 | 기본 거주지의 주소 2 필드 | 아니요 | 6 | 255 |
| 구/군/시 | 시티 오브 프라이머리 레지던스 | 예 | 7 | 255 |
| 주/도 | 주 거주지의 약어 | 예 | 8 | 2 |
| 우편번호 | 기본 거주지의 전체 우편 번호 | 예 | 9 | 10 |
| 이메일 | 기본 이메일 기본적으로 이 필드는 중복 제거 키로 사용되어 레코드를 고유하게 만듭니다. | 아니요 | 10 | 255 |
| 휴대폰 | 개인 전화 번호(지역 코드 + 번호)<br> 기본적으로 이 필드는 중복 제거 키로 사용되어 레코드를 고유하게 만듭니다. | 아니요 | 11 | 10 |

**[!UICONTROL Source 필드]** 열에서 해당 대상 필드에 매핑할 각 원본 특성의 이름을 입력하거나 화살표 아이콘을 선택하여 **[!UICONTROL 원본 필드 선택]** 화면을 엽니다.<br>
![매핑 화면](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

모든 필드를 매핑한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택합니다.

[!DNL Adobe's] 표준 스키마를 사용하지 않는 경우 쿼리 서비스를 사용하여 [!DNL Adobe] 표준 스키마를 필드 이름으로 채우는 방법에 대한 자세한 내용은 [쿼리 서비스 UI 안내서](../../../query-service/ui/overview.md) 설명서를 참조하십시오.

### 검토 {#review}

위의 모든 단계를 완료하면 대상 연결 상태 및 대상 세부 사항을 검토한 후 활성화(배포)할 수 있습니다. 선택한 대상이 목록의 맨 아래에 표시됩니다. 각 대상자는 [!DNL Acxiom Audience Distribution] API에 대한 별도의 호출이 됩니다.

결과에 만족하면 **[!UICONTROL 완료]**&#x200B;를 선택하여 대상을 활성화하세요.

![대상자 검토](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png)

## 문제 해결 {#troubleshooting}

대상 담당자가 대상자를 찾을 수 없는 경우 [!DNL Adobe] 담당자에게 지원을 요청하십시오.

[!DNL Adobe] 담당자에게 다음 정보를 제공해야 합니다.
* 대상자 이름
* 대상 이름
* 대상자 활성화 날짜
* 내보낸 파일 이름

## 다음 단계 {#next-steps}

이 자습서에 따라 선택한 대상 플랫폼에 대한 대상을 성공적으로 활성화했습니다. 그런 다음 대상 플랫폼 담당자에게 문의하여 캠페인 설정을 시작합니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)를 참조하십시오.


