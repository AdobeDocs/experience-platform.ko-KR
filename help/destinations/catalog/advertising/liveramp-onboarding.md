---
title: LiveRamp - 온보드 연결
description: LiveRamp 커넥터를 사용하여 Adobe Real-Time Customer Data Platform에서 LiveRamp Connect로 대상을 온보딩하는 방법을 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 3%

---

# [!DNL LiveRamp - Onboarding] 연결 {#liveramp-onboarding}

[!DNL LiveRamp - Onboarding] 연결을 사용하여 Adobe Real-Time Customer Data Platform에서 [!DNL LiveRamp Connect]&#x200B;(으)로 대상자를 온보딩합니다.

## 사용 사례 {#use-cases}

[!DNL LiveRamp - Onboarding] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

마케터로서 [!DNL Ramp ID] 식별자를 사용하여 모바일, 오픈 웹, 소셜 및 [!DNL CTV] 플랫폼에서 사용자를 타깃팅할 수 있도록 Adobe Experience Platform에서 온보드 ID로 대상을 보내려고 합니다.[!DNL LiveRamp Connect]

## 전제 조건 {#prerequisites}

[!DNL LiveRamp - Onboarding] 연결에서 [LiveRamp의 SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) 저장소를 사용하여 파일을 내보냅니다.

Experience Platform에서 [!DNL LiveRamp - Onboarding]&#x200B;(으)로 데이터를 보내려면 먼저 [!DNL LiveRamp] 자격 증명이 필요합니다. 자격 증명이 없는 경우 [!DNL LiveRamp] 담당자에게 연락하여 자격 증명을 받으십시오.

## 지원되는 ID {#supported-identities}

[!DNL LiveRamp - Onboarding]은(는) 공식 [LiveRamp 설명서](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers)에 설명된 PII 기반 식별자, 알려진 식별자 및 사용자 지정 ID와 같은 ID의 활성화를 지원합니다.

활성화 워크플로의 [매핑 단계](#map)에서 대상 매핑을 사용자 지정 특성으로 정의해야 합니다.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | [!DNL LiveRamp - Onboarding] 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 일별 일괄 처리]** | 프로필은 대상 평가를 기반으로 Experience Platform에서 업데이트되므로 프로필(ID)은 대상 플랫폼으로 다운스트림으로 하루에 한 번 업데이트됩니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

**암호가 포함된 SFTP 인증** {#sftp-password}

![암호가 있는 SFTP를 사용하여 대상에 인증하는 방법을 보여 주는 샘플 스크린샷](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL 포트]**: [!DNL LiveRamp - Onboarding] 저장소 위치에 사용되는 포트입니다.  아래 설명된 대로 지리적 위치에 해당하는 포트를 사용하십시오.
   * **[!UICONTROL NA]**: 포트 `22` 사용
   * **[!UICONTROL AU]**: 포트 `2222` 사용
* **[!UICONTROL 사용자 이름]**: [!DNL LiveRamp - Onboarding] 저장소 위치의 사용자 이름입니다.
* **[!UICONTROL 암호]**: [!DNL LiveRamp - Onboarding] 저장소 위치의 암호입니다.
* **[!UICONTROL PGP/GPG 암호화 키]**: 선택적으로 RSA 형식의 공개 키를 연결하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.
  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL 하위 키 ID]**:암호화 키를 제공하는 경우 암호화 **[!UICONTROL 하위 키 ID]**&#x200B;도 제공해야 합니다. 하위 키 ID를 얻는 방법에 대해 알아보려면 [!DNL LiveRamp] [암호화 설명서](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key)를 참조하세요.

**SSH 키 인증이 있는 SFTP** {#sftp-ssh}

![SSH 키를 사용하여 대상에 인증하는 방법을 보여 주는 샘플 스크린샷](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL 포트]**: [!DNL LiveRamp - Onboarding] 저장소 위치에 사용되는 포트입니다.  아래 설명된 대로 지리적 위치에 해당하는 포트를 사용하십시오.
   * **[!UICONTROL EU]**: 포트 `4222` 사용
* **[!UICONTROL 사용자 이름]**: [!DNL LiveRamp - Onboarding] 저장소 위치의 사용자 이름입니다.
* **[!UICONTROL SSH 키]**: [!DNL LiveRamp - Onboarding] 저장소 위치에 로그인하는 데 사용되는 개인 [!DNL SSH] 키입니다. 개인 키의 형식은 [!DNL Base64] 인코딩 문자열로 지정해야 하며 암호로 보호되지 않아야 합니다.

   * [!DNL SSH] 키를 [!DNL LiveRamp - Onboarding] 서버에 연결하려면 [!DNL LiveRamp]의 기술 지원 포털을 통해 티켓을 제출하고 공개 키를 제공해야 합니다. 자세한 내용은 [LiveRamp 설명서](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client)를 참조하세요.

* **[!UICONTROL PGP/GPG 암호화 키]**: 선택적으로 RSA 형식의 공개 키를 연결하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.
  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL 하위 키 ID]**:암호화 키를 제공하는 경우 암호화 **[!UICONTROL 하위 키 ID]**&#x200B;도 제공해야 합니다. 하위 키 ID를 얻는 방법에 대해 알아보려면 [!DNL LiveRamp] [암호화 설명서](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key)를 참조하세요.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="암호화 하위 키 ID"
>abstract="LiveRamp 공개 암호화 키를 기반으로 암호화에 사용되는 하위 키 ID입니다. 인증 단계에서 암호화 키를 제공한 경우 이 필드는 필수 항목입니다."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="하위 키 ID를 얻는 방법을 알아봅니다"

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

대상에 대한 세부 정보를 채우는 방법을 보여 주는 ![Experience Platform UI 스크린샷](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 지역]**: LiveRamp SFTP 저장소 인스턴스의 지리적 지역입니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 [!DNL LiveRamp] `uploads` 하위 폴더의 경로입니다. `uploads` 접두사가 폴더 경로에 자동으로 추가됩니다. [!DNL LiveRamp]에서는 파일을 다른 기존 피드와 구분하고 모든 자동화가 원활하게 실행되도록 Adobe Real-Time CDP에서 게재할 전용 하위 폴더를 만들 것을 권장합니다.
   * 예를 들어 파일을 `uploads/my_export_folder`(으)로 내보내려면 **[!UICONTROL 폴더 경로]** 필드에 `my_export_folder`을(를) 입력합니다.
* **[!UICONTROL 압축 형식]**: Experience Platform에서 내보낸 파일에 사용할 압축 형식을 선택합니다. 사용 가능한 옵션은 **[!UICONTROL GZIP]** 또는 **[!UICONTROL 없음]**&#x200B;입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 일정 조정 {#scheduling}

[!UICONTROL 예약] 단계에서 아래 표시된 설정으로 각 대상에 대한 내보내기 일정을 만듭니다.

* **[!UICONTROL 파일 내보내기 옵션]**: [!UICONTROL 전체 파일 내보내기]. [증분 파일 내보내기](../../ui/activate-batch-profile-destinations.md#export-incremental-files)는 현재 [!DNL LiveRamp] 대상에 대해 지원되지 않습니다.
* **[!UICONTROL 빈도]**: [!UICONTROL 일별]
* **[!UICONTROL 날짜]**: 원하는 대로 내보내기 시작 및 종료 시간을 선택하십시오.

대상 예약 단계를 보여 주는 ![Experience Platform UI 스크린샷입니다.](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

내보낸 파일 이름은 현재 사용자가 구성할 수 없습니다. [!DNL LiveRamp - Onboarding] 대상으로 내보낸 모든 파일의 이름은 다음 템플릿을 기준으로 자동 지정됩니다.

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![내보낸 파일 이름 템플릿을 표시하는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

예를 들어, [!DNL Luma] 조직의 내보낸 파일 이름은 다음과 비슷할 수 있습니다.

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### 속성 및 ID 매핑 {#map}

**[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 특성 및 ID를 선택할 수 있습니다.

>[!IMPORTANT]
>
>이 대상은 활성화 흐름당 하나의 소스 ID 네임스페이스 활성화를 지원합니다. `Email` 및 `Phone`과(와) 같이 여러 ID 네임스페이스를 내보내야 하는 경우 각 ID에 대해 [별도의 활성화 흐름을 만들어야](../../ui/activate-batch-profile-destinations.md) 합니다.

**[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 대상 필드]** 매핑은 내보낸 CSV 파일의 열 머리글 이름을 정의합니다. **[!UICONTROL Target 필드]**&#x200B;에 사용자 지정 이름을 제공하여 내보낸 파일의 CSV 열 헤더를 원하는 이름으로 변경할 수 있습니다.

>[!IMPORTANT]
>
>[!DNL LiveRamp]&#x200B;(으)로 초기 파일을 배달한 후 대상 필드에 대한 변경 내용은 [!DNL LiveRamp] 계정 팀에 알리거나 [LiveRamp 지원에 티켓을 제출](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case)하여 변경 내용이 자동화 프로세스에 반영되도록 하십시오.

1. **[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택합니다. 화면에 새 매핑 행이 표시됩니다.

   ![매핑 화면을 표시하는 Experience Platform UI 화면입니다.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 특성 선택]** 범주를 선택하고 매핑할 XDM 특성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]** 범주를 선택하고 대상에 매핑할 ID를 선택합니다.

   ![소스 매핑 화면을 표시하는 Experience Platform UI 화면입니다.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. **[!UICONTROL 대상 필드 선택]** 창에서 선택한 원본 필드를 매핑할 특성 이름을 입력하십시오. 여기에 정의된 속성 이름은 내보낸 CSV 파일에 열 헤더로 반영됩니다.

   ![대상 매핑 화면을 표시하는 Experience Platform UI 화면입니다.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   특성 이름을 **[!UICONTROL Target 필드]**&#x200B;에 직접 입력하여 입력할 수도 있습니다.

   ![대상 매핑 화면을 표시하는 Experience Platform UI 화면입니다.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

원하는 매핑을 모두 추가했으면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하고 활성화 워크플로를 완료합니다.

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

데이터를 CSV 파일로 구성한 [!DNL LiveRamp - Onboarding] 저장소 위치로 내보냅니다.

내보낸 파일의 최대 크기는 1,000만 행입니다. Experience Platform은 선택한 대상이 1천만 행을 초과하는 경우 게재당 여러 파일을 생성합니다. 단일 파일 한도를 초과하려는 경우 [!DNL LiveRamp] 담당자에게 문의하여 일괄 처리 수집을 구성하도록 요청하십시오.

[!DNL LiveRamp - Onboarding] 대상으로 파일을 내보낼 때 Experience Platform은 각 [병합 정책 ID](../../../profile/merge-policies/overview.md)에 대해 하나의 CSV 파일을 생성합니다.

예를 들어 다음 대상을 고려해 보겠습니다.

* 대상자 A (병합 정책 1)
* 대상 B(병합 정책 2)
* 대상자 C (병합 정책 1)
* 대상자 D (병합 정책 1)

Experience Platform에서 두 개의 CSV 파일을 [!DNL LiveRamp - Onboarding]&#x200B;(으)로 내보냅니다.

* 대상 A, C 및 D가 포함된 하나의 CSV 파일
* 대상자 B가 포함된 CSV 파일 1개.

내보낸 CSV 파일에는 아래 예와 같이 속성 이름과 `audience_namespace:audience_ID` 쌍을 열 헤더로 사용하여 별도의 열에 선택한 속성과 해당 대상 상태의 프로필이 포함되어 있습니다.

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1_AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2_AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X_AUDIENCE_ID_X`

내보낸 파일에 포함된 프로필은 다음 대상 자격 상태 중 하나와 일치할 수 있습니다.

* `Active`: 프로필이 현재 대상자에 대해 자격이 있습니다.
* `Expired`: 프로필이 더 이상 대상자에 적합하지 않지만 과거에 자격이 있습니다.
* `""`(빈 문자열): 대상에 대해 프로필이 정격되지 않았습니다.

예를 들어, 하나의 `email` 특성, Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)에서 시작된 두 대상 및 하나의 [가져온](../../../segmentation/ui/audience-portal.md#import-audience) 외부 대상으로 내보낸 CSV 파일은 다음과 같이 표시될 수 있습니다.

```csv
email,ups_aa2e3d98-974b-4f8b-9507-59f65b6442df,ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

위의 예에서 `ups_aa2e3d98-974b-4f8b-9507-59f65b6442df` 및 `ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` 섹션은 세분화 서비스에서 시작된 대상을 설명하고, `CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e`은(는) [사용자 지정 업로드](../../../segmentation/ui/audience-portal.md#import-audience)(으)로 Experience Platform으로 가져온 대상을 설명합니다.

Experience Platform은 각 [병합 정책 ID](../../../profile/merge-policies/overview.md)에 대해 하나의 CSV 파일을 생성하므로 각 병합 정책 ID에 대해 별도의 데이터 흐름 실행도 생성합니다.

즉, [데이터 흐름 실행](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 페이지에서 **[!UICONTROL ID가 활성화됨]** 및 **[!UICONTROL 프로필이 수신됨]** 지표가 각 대상에 대해 표시되지 않고 동일한 병합 정책을 사용하는 각 대상 그룹에 대해 집계됩니다.

동일한 병합 정책을 사용하는 대상자 그룹에 대해 데이터 흐름이 생성되면 대상자 이름이 [모니터링 대시보드](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)에 표시되지 않습니다.

![ID가 활성화된 지표를 표시하는 Experience Platform UI 화면 표시입니다.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## 내보낸 데이터를 LiveRamp에 업로드 {#upload-to-liveramp}

데이터를 [!DNL LiveRamp - Onboarding] 저장소로 내보내면 데이터를 [!DNL LiveRamp] 플랫폼으로 업로드해야 합니다.

[!DNL LiveRamp - Onboarding] 저장소에서 [!DNL LiveRamp] 대상자로 파일을 업로드하는 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오. [대상자에게 첫 번째 파일을 업로드할 때의 고려 사항](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

[!DNL LiveRamp - Onboarding] 저장소를 구성하는 방법에 대한 자세한 내용은 [공식 설명서](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html)를 참조하세요.

## 변경 로그 {#changelog}

이 섹션에서는 이 대상 커넥터에 대한 기능 및 중요 설명서 업데이트를 캡처합니다.

+++ 변경 로그 보기

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2024년 3월 | 기능 및 설명서 업데이트 | <ul><li>유럽 및 오스트레일리아 [!DNL LiveRamp] [!DNL SFTP] 인스턴스에 대한 게재 지원이 추가되었습니다.</li><li>새로 지원되는 영역의 특정 구성을 설명하는 설명서가 업데이트되었습니다.</li><li>최대 파일 크기가 1,000만 행으로 증가했습니다(이전에는 500만 개에서).</li><li>파일 크기 증가를 반영하도록 설명서가 업데이트되었습니다.</li></ul> |
| 2023년 7월 | 초기 릴리스 | 초기 대상 릴리스 및 설명서가 게시되었습니다. |

{style="table-layout:auto"}

+++
