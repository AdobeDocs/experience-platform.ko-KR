---
title: 2024년 11월 이전에 생성된 데이터 흐름에 대한 데이터 세트 내보내기 일정 확장
description: 2025년 9월 1일에 중지되는 2024년 11월 이전에 생성된 데이터 세트 내보내기 데이터 흐름에 대한 내보내기 일정을 확장하는 방법을 알아봅니다.
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 08a1c6a1830ace4661ab6aa5b547c4473301ce84
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---


# 2024년 11월 이전에 생성된 데이터 흐름에 대한 데이터 세트 내보내기 일정 확장

>[!IMPORTANT]
>
>**필요한 작업**: 조직에 2024년 11월 이전에 만든 [데이터 세트 내보내기 데이터 흐름](export-datasets.md)이 있는 경우 이러한 데이터 흐름은 2025년 9월 1일에 작동을 중지합니다. 이 안내서에서는 유지할 데이터 흐름에 대해 내보내기 일정을 이 날짜 이후로 확장하는 방법을 설명합니다.

## 개요 {#overview}

Experience Platform의 [2024년 9월 릴리스](/help/release-notes/2024/september-2024.md#destinations)에서 Adobe은 2024년 9월 릴리스 전에 생성된 모든 데이터 세트 내보내기 데이터 흐름에 대해 기본 종료 날짜인 **2025년 5월 1일**&#x200B;을(를) 도입했습니다.

**이 날짜는 이후** 2024년 11월 이전&#x200B;**에 만들어진 모든 데이터 집합 내보내기 데이터 흐름에 대해 2025년 9월 1일**&#x200B;로 업데이트되었습니다.

2024년 11월 이전에 만든 데이터 집합 내보내기 데이터 흐름은 만료 날짜를 수동으로 연장하지 않는 한 **2025년 9월 1일**&#x200B;에 데이터 내보내기를 중지합니다.

**2025년 9월 1일** 이후에도 데이터 흐름을 계속 내보내려면 이 안내서의 단계에 따라 데이터 집합을 내보내는 각 대상에 대한 일정을 확장해야 합니다.

## 영향을 받는 대상 {#affected-destinations}

조직에는 아래 나열된 대상으로 데이터를 전송하는 활성 데이터 세트 내보내기 데이터 흐름이 있을 수 있습니다. 다음 섹션의 단계에 따라 연습 비디오를 시청하여 만료되도록 설정된 데이터 세트를 식별하는 방법을 알아보십시오.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## 비디오 튜토리얼 {#video}

예정된 종료 날짜가 포함된 데이터 세트 내보내기를 식별하고 유지할 데이터 흐름에 대한 내보내기 일정을 확장하는 방법에 대한 단계별 데모는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## 1단계: 영향을 받는 데이터 흐름 식별 {#identify-dataflows}

데이터 세트 내보내기 데이터 흐름에 대한 내보내기 일정을 연장하기 전에 먼저 다가오는 만료 날짜의 영향을 받는 데이터 흐름을 식별해야 합니다. 작업이 필요한 데이터 흐름을 찾으려면 아래 단계를 따르십시오.

1. Experience Platform UI에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**(으)로 이동합니다.
2. 활성 데이터 집합 내보내기 데이터 흐름이 있는 대상에서 **[!UICONTROL 활성화]**&#x200B;를 선택하십시오.

   >[!TIP]
   >
   >카탈로그의 왼쪽에 있는 **[!UICONTROL 데이터 형식]** 필터를 사용하여 **[!UICONTROL 데이터 세트]**&#x200B;별로 사용 가능한 대상을 필터링합니다.

3. 데이터 세트 내보내기가 있는 데이터 흐름만 표시하려면 **[!UICONTROL 데이터 세트]** 데이터 형식을 선택하십시오.
   데이터 유형별로 데이터 흐름을 필터링하는 방법을 보여 주는 ![스크린샷입니다.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. **[!UICONTROL 생성됨]** 열 헤더를 선택하고 **[!UICONTROL 오름차순 정렬]**&#x200B;을 선택하여 이전 데이터 흐름을 확인하십시오.
   ![데이터 흐름을 오름차순으로 정렬하는 방법을 보여 주는 스크린샷입니다.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. 2024년 11월 이전에 생성된 데이터 흐름 중 유지할 데이터 흐름을 식별합니다.

## 2단계: 데이터 세트 내보내기 워크플로우에 액세스 {#access-workflow}

유지할 각 데이터 흐름에 대해 데이터 세트 내보내기 워크플로우에 액세스하여 일정을 수정해야 합니다.

1. **[!UICONTROL 이름]** 열에서 데이터 흐름 이름을 선택하십시오. **[!UICONTROL 데이터 흐름 실행]** 페이지로 이동합니다.
2. 이 페이지에서 **[!UICONTROL 데이터 세트 내보내기]** 옵션을 선택하십시오.
   ![데이터 흐름 실행 페이지에서 데이터 세트 내보내기 옵션을 보여 주는 스크린샷입니다.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. **[!UICONTROL 데이터 세트 선택]** 페이지에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다. 데이터 흐름에 새 데이터 세트를 추가할 필요가 없습니다.
4. 이렇게 하면 데이터 집합 내보내기 만료 날짜를 알리는 알림을 볼 수 있는 **[!UICONTROL 예약]** 페이지로 이동합니다.
   ![만료 알림이 있는 데이터 집합 내보내기 데이터 흐름](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## 3단계: 내보내기 일정 확장 {#extend-export-schedule}

이제 2025년 9월 1일 이후로 내보내기 일정을 수정할 수 있습니다.

1. **[!UICONTROL 일정 편집]**&#x200B;을 선택하세요.
   ![일정 편집 단추를 표시하는 예약 단계의 스크린샷입니다.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. 새 내보내기 일정을 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.
   예약 옵션을 표시하는 예약 단계의 ![스크린샷입니다.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >데이터 세트 내보내기 일정을 구성하는 방법에 대한 자세한 지침은 [데이터 세트 내보내기 설명서](export-datasets.md#scheduling)를 참조하세요.

## 2025년 9월 1일 마감일을 놓치면 어떻게 됩니까? {#missed-deadline}

데이터 세트 내보내기 데이터 흐름이 2025년 9월 1일에 만료되고 일정을 연장하지 않은 경우 Adobe에 연락하여 데이터 손실 없이 데이터 흐름을 다시 활성화할 수 있는 **30일 유예 기간**&#x200B;이 있습니다. 여기에는 9월 1일부터 Adobe에 연락한 날짜 사이에 내보내지 않은 데이터가 포함됩니다.

>[!IMPORTANT]
>
>Adobe에서는 이 유예 기간을 제공하지만 중단 없는 데이터 내보내기를 보장하고 잠재적인 서비스 중단을 방지하기 위해 2025년 9월 1일 마감 전까지 일정을 연장하는 것이 좋습니다.
