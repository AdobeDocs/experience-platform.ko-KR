---
description: 파일 기반 대상으로 데이터를 활성화할 때 파일 서식 옵션을 구성하는 방법에 대해 알아봅니다
title: 파일 기반 대상에 대한 파일 서식 옵션 구성
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 0eb17d4d7ad9db3737a14f383bdafe40d59eb12c
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 19%

---

# 파일 기반 대상에 대한 파일 서식 옵션 구성

>[!IMPORTANT]
> 
>이 문서에 설명된 파일 서식 옵션은 현재 CSV 파일에만 사용할 수 있습니다.

내보낸 파일에 대한 다양한 파일 서식 옵션을 구성하는 옵션은 [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect) 또는 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect)와 같은 파일 기반 대상에 연결](/help/destinations/ui/connect-destination.md)할 때 사용할 수 있습니다.[

Experience Platform UI를 사용하여 내보낸 파일에 대한 다양한 파일 서식 옵션을 구성할 수 있습니다. Experience Platform에서 받은 파일을 최적으로 읽고 해석하기 위해 내보낸 파일의 여러 속성을 사용자 측의 파일 수신 시스템의 요구 사항과 일치하도록 수정할 수 있습니다.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## CSV 파일에 대한 파일 형식 지정 구성 {#file-configuration}

파일 서식 옵션을 표시하려면 [대상에 연결](/help/destinations/ui/connect-destination.md) 워크플로우를 시작하십시오. 내보낸 `CSV`개 파일에 사용할 수 있는 파일 형식 설정을 표시하려면 **데이터 형식: 세그먼트** 및 **파일 형식: CSV**&#x200B;을 선택하십시오.

>[!IMPORTANT]
>
>연결 중인 대상에 이러한 모든 옵션을 사용할 수 없을 수도 있습니다. 대상에서 지원할 파일 서식 옵션을 결정하는 것은 대상 개발자의 책임입니다. 대상 개발자는 대상에 연결할 때 사용할 수 있는 옵션을 결정할 수 있습니다. Experience Platform UI에서 필수 옵션이 별표로 표시됩니다.
> 
>Adobe이 빌드한 클라우드 스토리지 대상 - [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [데이터 랜딩 영역](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - 현재 아래에 강조 표시된 6개의 CSV 옵션만 지원합니다.

![사용 가능한 파일 서식 옵션을 보여 주는 이미지입니다.](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 구분 기호 {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="구분 기호"
>abstract="이 컨트롤을 사용하여 각 필드 및 값에 대한 구분 기호를 설정합니다. 각 선택 항목에 대한 예제는 설명서를 참조하십시오."

이 컨트롤을 사용하여 내보낸 CSV 파일의 각 필드 및 값에 대한 구분 기호를 설정합니다. 사용 가능한 옵션은 다음과 같습니다.

* 콜론 `(:)`
* 쉼표 `(,)`
* 파이프 `(|)`
* 세미콜론 `(;)`
* 탭 `(\t)`

#### 예시

UI에서 선택한 각 내용과 함께 내보낸 CSV 파일의 아래 예를 봅니다.

* **[!UICONTROL 콜론`(:)`]**&#x200B;이(가) 선택된 출력 예: `male:John:Doe`
* **[!UICONTROL 쉼표`(,)`]**&#x200B;이(가) 선택된 출력 예: `male,John,Doe`
* **[!UICONTROL 파이프`(|)`]**&#x200B;이(가) 선택된 출력 예: `male|John|Doe`
* **[!UICONTROL 세미콜론`(;)`]**&#x200B;이(가) 선택된 출력 예: `male;John;Doe`
* **[!UICONTROL 탭`(\t)`]**&#x200B;이(가) 선택된 출력 예: `male \t John \t Doe`

### 인용 부호 {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="인용 부호"
>abstract="내보낸 문자열에서 큰따옴표를 제거하려면 이 옵션을 사용하십시오. 각 선택 항목에 대한 예제는 설명서를 참조하십시오."

내보낸 문자열에서 큰따옴표를 제거하려면 이 옵션을 사용하십시오. 사용 가능한 옵션은 다음과 같습니다.

* **[!UICONTROL Null 문자(\0000)]**. 내보낸 CSV 파일에서 큰따옴표를 제거하려면 이 옵션을 사용합니다.
* **[!UICONTROL 큰따옴표(&quot;)]**. 내보낸 CSV 파일에 큰 따옴표를 유지하려면 이 옵션을 사용합니다.

#### 예시

UI에서 선택한 각 내용이 포함된 내보낸 CSV 파일의 콘텐츠 아래 예를 봅니다.

* **[!UICONTROL Null 문자(\0000)]**&#x200B;이(가) 선택된 출력 예: `Test,John,LastName`
* **[!UICONTROL 큰따옴표(&quot;)]**&#x200B;이(가) 선택된 출력 예: `"Test","John","LastName"`

### 문자 이스케이프 {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="문자 이스케이프"
>abstract="이미 인용된 값 내에서 인용 부호를 이스케이프하는 데 사용되는 단일 문자를 설정합니다. 각 선택 항목에 대한 예제는 설명서를 참조하십시오."

이 옵션을 사용하여 이미 인용된 값 내에서 따옴표를 이스케이프 처리할 단일 문자를 설정합니다. 예를 들어, 이 옵션은 문자열의 일부가 이미 큰따옴표로 묶여 있는 큰 따옴표로 묶인 문자열이 있는 경우 유용합니다. 이 옵션은 내부 큰따옴표를 바꿀 문자를 결정합니다. 사용 가능한 옵션은 다음과 같습니다.

* 백슬래시 `(\)`
* 작은 따옴표 `(')`

#### 예시

UI에서 선택한 각 내용이 포함된 내보낸 CSV 파일의 콘텐츠 아래 예를 봅니다.

* **[!UICONTROL 백슬래시`(\)`]**&#x200B;이(가) 선택된 출력 예: `"Test,\"John\",LastName"`
* **[!UICONTROL 작은 따옴표`(')`]**&#x200B;이(가) 선택된 출력 예: `"Test,'"John'",LastName"`

### 빈 값 출력 {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="빈 값 출력"
>abstract="내보낸 CSV 파일에서 빈 값을 표시하는 방법을 설정하려면 이 옵션을 사용합니다. 각 선택 항목에 대한 예제는 설명서를 참조하십시오."

이 컨트롤을 사용하여 빈 값의 문자열 표현을 설정합니다. 이 옵션은 내보낸 CSV 파일에 빈 값이 표시되는 방식을 결정합니다. 사용 가능한 옵션은 다음과 같습니다.

* **[!UICONTROL Null(null)]**
* **큰따옴표(&quot;&quot;)의 빈 문자열**
* **[!UICONTROL 빈 문자열]**

#### 예시

UI에서 선택한 각 내용이 포함된 내보낸 CSV 파일의 콘텐츠 아래 예를 봅니다.

* **[!UICONTROL null]**&#x200B;이(가) 선택된 출력 예: `male,NULL,TestLastName`. 이 경우 Experience Platform은 빈 값을 null 값으로 변환합니다.
* **&quot;&quot;**&#x200B;이(가) 선택된 출력 예: `male,"",TestLastName`. 이 경우 Experience Platform은 빈 값을 큰따옴표 쌍으로 변환합니다.
* **[!UICONTROL 빈 문자열]**&#x200B;이 선택된 출력 예: `male,,TestLastName`. 이 경우 Experience Platform은 빈 값을 유지하고 큰 따옴표 없이 그대로 내보냅니다.

>[!TIP]
>
>아래 구간에서 empty value 출력과 null value 출력의 차이점은 empty value에는 empty value의 실제 값이 empty라는 점이다. NULL 값에는 값이 전혀 없습니다. 빈 값을 테이블에 빈 유리로, 널 값을 테이블에 전혀 유리가 없는 것으로 생각하자.

### Null 값 출력 {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Null 값 출력"
>abstract="내보낸 파일 내에서 null 값의 문자열 표현을 설정하려면 이 컨트롤을 사용합니다. 각 선택 항목에 대한 예제는 설명서를 참조하십시오."

내보낸 파일 내에서 null 값의 문자열 표현을 설정하려면 이 컨트롤을 사용합니다. 이 옵션은 내보낸 CSV 파일에 null 값이 표시되는 방식을 결정합니다. 사용 가능한 옵션은 다음과 같습니다.

* **[!UICONTROL Null(null)]**
* **큰따옴표(&quot;&quot;)의 빈 문자열**
* **[!UICONTROL 빈 문자열]**

#### 예시

UI에서 선택한 각 내용이 포함된 내보낸 CSV 파일의 콘텐츠 아래 예를 봅니다.

* **[!UICONTROL null]**&#x200B;이(가) 선택된 출력 예: `male,NULL,TestLastName`. 이 경우 변환은 발생하지 않으며 CSV 파일에 null 값이 포함됩니다.
* **&quot;&quot;**&#x200B;이(가) 선택된 출력 예: `male,"",TestLastName`. 이 경우 Experience Platform은 빈 문자열 주위에서 null 값을 큰따옴표로 바꿉니다.
* **[!UICONTROL 빈 문자열]**&#x200B;이 선택된 출력 예: `male,,TestLastName`. 이 경우 Experience Platform은 null 값을 큰따옴표 없이 빈 문자열로 바꿉니다.

### 압축 포맷 {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="압축 포맷"
>abstract="데이터를 파일에 저장할 때 사용할 압축 유형을 설정합니다. 지원되는 옵션은 GZIP 및 NONE입니다. 각 선택 항목에 대한 예제는 설명서를 참조하십시오."

데이터를 파일에 저장할 때 사용할 압축 유형을 설정합니다. 지원되는 옵션은 GZIP 및 NONE입니다. 이 옵션은 압축된 파일을 내보내는지 여부를 결정합니다.

### 인코딩

*UI 스크린샷에 표시되지 않음*. 저장된 CSV 파일의 인코딩(charset)을 지정합니다. 옵션은 UTF-8 또는 UTF-16입니다.

### 따옴표 이스케이프 처리를 위한 문자

*UI 스크린샷에 표시되지 않음*. 따옴표를 포함하는 값을 항상 따옴표로 묶어야 하는지 여부를 나타내는 플래그입니다.

기본적으로 따옴표 문자가 포함된 모든 값은 이스케이프 처리됩니다.

### 선 구분 기호

*UI 스크린샷에 표시되지 않음*. 쓰기에 사용해야 하는 선 구분 기호를 정의합니다. 최대 길이는 1자입니다.

### 선행 공백 무시

*UI 스크린샷에 표시되지 않음*. 내보내는 값에서 선행 공백을 건너뛰어야 하는지 여부를 나타내는 플래그입니다.

**[!UICONTROL True]**&#x200B;이(가) 선택된 출력 예: `"male","John","TestLastName"`
**[!UICONTROL False]**&#x200B;이(가) 선택된 출력 예: `" male","John","TestLastName"`

### 후행 공백 무시

UI 스크린샷에 표시되지 않습니다. 내보내는 값에서 후행 공백을 건너뜁니다.

**[!UICONTROL True]**&#x200B;이(가) 선택된 출력 예: `"male","John","TestLastName"`
**[!UICONTROL False]**&#x200B;이(가) 선택된 출력 예: `"male ","John","TestLastName"`

### 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제 파일 컨텐츠를 다운스트림 파일 수신 시스템의 요구 사항에 맞게 조정하도록 CSV 데이터 파일에 대한 파일 내보내기 옵션을 구성하는 방법을 이해할 수 있습니다. 그런 다음 [파일 기반 대상 활성화 자습서](/help/destinations/ui/activate-batch-profile-destinations.md)를 읽고 기본 클라우드 저장소 위치로 파일 내보내기를 시작할 수 있습니다.
