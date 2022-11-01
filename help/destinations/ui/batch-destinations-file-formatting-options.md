---
description: 파일 기반 대상으로 데이터를 활성화할 때 파일 형식 옵션을 구성하는 방법을 알아봅니다
title: (베타) 파일 기반 대상에 대한 파일 형식 옵션을 구성합니다
source-git-commit: 23a7a1997e05d2bde26de5b73a23ea051bf2b3bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# (베타) 파일 기반 대상에 대한 파일 형식 옵션을 구성합니다

>[!IMPORTANT]
>
>다음 **[!UICONTROL 파일 서식 옵션]** Adobe Experience Platform의 기능은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.
>이 기능에 액세스하려면 Adobe 담당자에게 문의하십시오.
> 
>이 문서에 설명된 파일 형식 옵션은 현재 CSV 파일에만 사용할 수 있습니다.

내보낸 파일에 대한 다양한 파일 형식 옵션을 구성하는 옵션은 [connect](/help/destinations/ui/connect-destination.md) 파일 기반 대상(예: ) [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect), 또는 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Experience Platform UI를 사용하여 내보낸 파일에 대한 다양한 파일 형식 옵션을 구성할 수 있습니다. Experience Platform에서 받은 파일을 최적의 방식으로 읽고 해석할 수 있도록 내보낸 파일의 여러 속성을 사용자 측에서 파일 수신 시스템의 요구 사항에 맞게 수정할 수 있습니다.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## 파일 형식 구성 {#file-configuration}

>[!IMPORTANT]
>
>연결하려는 대상에 이러한 옵션을 사용할 수 없습니다. 대상에서 지원할 파일 형식 옵션을 결정하는 것은 대상 개발자의 책임입니다. 대상 개발자는 대상에 연결할 때 사용할 수 있는 옵션을 결정할 수 있습니다. 필수 옵션은 Experience Platform UI에서 별표로 표시됩니다.

파일 서식 옵션을 표시하려면 [대상에 연결](/help/destinations/ui/connect-destination.md) 워크플로우를 시작하고 세그먼트를 **파일 유형**. 이 섹션에서는 내보낸 파일에 사용할 수 있는 파일 형식 설정에 대해 설명합니다 `CSV` 파일.

![사용 가능한 파일 형식 옵션 중 일부를 보여주는 이미지입니다.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 구분 기호

각 필드 및 값에 대해 구분자를 설정합니다. 예, `,` 쉼표로 구분된 값 또는 `/t` 탭으로 구분된 값에 사용할 수 있습니다.

### 따옴표 문자

구분 기호가 값의 일부가 될 수 있는 따옴표 붙은 값을 이스케이프하는 데 사용되는 단일 문자를 설정합니다.

### 이스케이프 문자

이미 따옴표로 묶인 값 내에 따옴표를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다.

### 빈 값 출력

빈 값의 문자열 표현을 설정합니다.

### Null 값 출력

내보낸 파일 내에서 null 값의 문자열 표현을 설정합니다.

출력 예 **[!UICONTROL null]** 선택: `male,NULL,TestLastName`
출력 예 **&quot;&quot;** 선택: `male,"",TestLastName`
출력 예 **[!UICONTROL 빈 문자열]** 선택: `male,,TestLastName`

### 압축 포맷

데이터를 파일에 저장할 때 사용할 압축 코덱을 설정합니다. 지원되는 옵션은 GZIP 및 NONE입니다.

### 인코딩

*UI 스크린샷에 표시되지 않음*. 저장된 CSV 파일의 인코딩(charset)을 지정합니다. 옵션은 UTF-8 또는 UTF-16입니다.

### 따옴표를 이스케이프 처리할 Char

*UI 스크린샷에 표시되지 않음*. 따옴표를 포함하는 값을 항상 따옴표로 묶어야 하는지 여부를 나타내는 플래그입니다.

기본값은 따옴표 문자가 포함된 모든 값을 이스케이프 처리하는 것입니다.

### 라인 구분 기호

*UI 스크린샷에 표시되지 않음*. 작성에 사용해야 하는 라인 구분자를 정의합니다. 최대 길이는 1자입니다.

### 선행 공백 무시

*UI 스크린샷에 표시되지 않음*. 내보낼 값에서 공백 선행 여부를 나타내는 플래그입니다.

출력 예 **[!UICONTROL True]** 선택: `"male","John","TestLastName"`
출력 예 **[!UICONTROL False]** 선택: `" male","John","TestLastName"`

### 후행 공백 무시

UI 스크린샷에 표시되지 않습니다. 내보낼 값에서 후행 공백을 건너뛸 것인지 여부를 나타내는 플래그입니다.

출력 예 **[!UICONTROL True]** 선택: `"male","John","TestLastName"`
출력 예 **[!UICONTROL False]** 선택: `"male ","John","TestLastName"`

### 다음 단계 {#next-steps}

이 문서를 읽은 후에는 CSV 데이터 파일에 대한 파일 내보내기 옵션을 구성하여 다운스트림 파일 수신 시스템의 요구 사항에 맞게 파일 내용을 조정하는 방법을 알 수 있습니다. 다음으로, [파일 기반 대상 활성화 자습서](/help/destinations/ui/activate-batch-profile-destinations.md) 파일을 선호하는 클라우드 저장소 위치로 내보내기를 시작합니다.
