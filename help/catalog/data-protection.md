---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform의 데이터 보호
topic: data protection
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Adobe Experience Platform의 데이터 보호

Adobe Experience Platform에서 수집하여 사용하는 모든 데이터는 원본 또는 파일 형식에 상관없이 [!DNL Data Lake]모든 데이터를 포함하는 매우 세부적인 데이터 저장소 [!DNL Platform]에 저장됩니다. 조직 [!DNL Data Lake] 에 존재하는 모든 데이터는 암호화되어 저장되고 관리되며, 별도의 [!DNL Microsoft Azure Data Lake] 스토리지 계정으로 관리됩니다.

다음 프로세스 흐름 다이어그램에서는 데이터를 수집, 처리, 암호화 및 유지하는 방법을 보여 줍니다. [!DNL Experience Platform]

![](images/data-protection/flow.png)

사용 중인 데이터가 암호화되 [!DNL Data Lake Storage]는 방법에 대한 자세한 내용은 Azure Data Lake 저장소의 [데이터 암호화 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). 사용 중인 데이터가 암호화되 [!DNL Cosmos DB]는 방법에 대한 자세한 내용은 Azure Cosmos DB의 [데이터 암호화 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).