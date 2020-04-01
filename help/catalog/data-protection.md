---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform의 데이터 보호
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Adobe Experience Platform의 데이터 보호

Adobe Experience Platform에서 인제스트하고 사용하는 모든 데이터는 원본 데이터 또는 파일 형식에 상관없이 플랫폼이 관리하는 모든 데이터를 포함하는 매우 세분화된 데이터 저장소인 Data Lake에 저장됩니다. Data Lake에 지속되는 모든 데이터는 조직의 고유한 Microsoft Azure Data Lake 저장소 계정에서 암호화, 저장 및 관리됩니다.

다음 프로세스 흐름 다이어그램은 경험 플랫폼에서 데이터를 수집, 처리, 암호화 및 유지하는 방법을 보여줍니다.

![](images/data-protection/flow.png)

Data Lake Storage에서 데이터가 암호화되는 방법에 대한 자세한 내용은 Azure Data Lake 저장소의 [데이터 암호화에 대한 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Cosmos DB에서 데이터를 암호화하는 방법에 대한 자세한 내용은 Azure Cosmos DB의 [데이터 암호화에 대한 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).