---
title: Adobe Experience Platform 릴리스 노트 - 2023년 1월
description: Adobe Experience Platform에 대한 2023년 1월 릴리스 노트입니다.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 9%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2023년 1월 25일**

Adobe Experience Platform의 기존 기능 업데이트:

- [소스](#sources)

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 클라우드 스토리지 소스의 하위 폴더에 대한 사용자 액세스 허용 | 이제 새 계정을 만들 때 클라우드 저장소 소스의 특정 하위 폴더에 대한 액세스를 정의할 수 있습니다. 만든 후에는 허용되는 하위 폴더의 데이터만 액세스할 수 있습니다. 이 기능은 다음 클라우드 스토리지 소스에서 사용할 수 있습니다. [Azure Blob 저장소](../../sources/connectors/cloud-storage/blob.md), [Google 클라우드 스토리지](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), 및 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 베타 가용성 [!DNL SugarCRM] | [!DNL SugarCRM] 이제 소스는 베타로 제공됩니다. 를 사용하십시오 [!DNL SugarCRM Accounts & Contacts] 그리고 [!DNL SugarCRM Events] 소스에서 데이터를 가져옵니다. [!DNL SugarCRM] Experience Platform 계정. 자세한 내용은 [[!DNL SugarCRM] 개요](../../sources/connectors/crm/sugarcrm.md). |