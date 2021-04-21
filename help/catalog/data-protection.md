---
keywords: Experience Platform;홈;인기 항목;카탈로그;데이터 보호;암호화 데이터 레이크
solution: Experience Platform
title: Adobe Experience Platform의 데이터 보호
topic-legacy: data protection
description: Data Lake에 지속되는 모든 데이터는 조직의 고유한 격리된 Microsoft Azure Data Lake 저장소 계정에서 암호화, 저장 및 관리됩니다. 다음 프로세스 흐름 다이어그램은 데이터를 Experience Platform에 의해 수집, 처리, 암호화 및 지속되는 방법을 보여줍니다.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Adobe Experience Platform의 데이터 보호

Adobe Experience Platform에서 인제스트하고 사용하는 모든 데이터는 원본 또는 파일 형식에 상관없이 [!DNL Platform]에서 관리하는 모든 데이터를 포함하는 매우 세분화된 데이터 저장소인 [!DNL Data Lake]에 저장됩니다. [!DNL Data Lake]에 남아 있는 모든 데이터는 조직의 고유한 분리된 [!DNL Microsoft Azure Data Lake] 저장소 계정에서 암호화, 저장 및 관리됩니다.

다음 프로세스 흐름 다이어그램은 데이터를 인제스트, 처리, 암호화 및 [!DNL Experience Platform]에 의해 지속되는 방법을 보여줍니다.

![](images/data-protection/flow.png)

나머지 데이터가 [!DNL Data Lake Storage]에서 암호화되는 방법에 대한 자세한 내용은 Azure Data Lake 저장소](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)의 [데이터 암호화에 있는 문서를 참조하십시오. 나머지 데이터가 [!DNL Cosmos DB]에서 암호화되는 방법에 대한 자세한 내용은 Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)의 [데이터 암호화에 있는 문서를 참조하십시오.
