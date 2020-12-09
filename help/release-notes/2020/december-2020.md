---
title: Adobe Experience Platform 릴리스 노트
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: December 9, 2020
author: ens60013
translation-type: tm+mt
source-git-commit: 25c162f50f0a66d77eb638dbf87893af3c543ddc
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 10%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜:2020년 12월 9일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 소스에 대한 계정 및 연결 세부 정보 업데이트 | 이제 API와 UI를 사용하여 기존 스트리밍 연결의 이름, 설명 및 자격 증명을 업데이트할 수 [!DNL Flow Service] 있습니다. 자세한 내용은 API를 사용하여 연결 [업데이트 및 UI를 사용하여 계정 세부 사항](../../sources/tutorials/api/update.md) [편집 관련 자습서를 참조하십시오](../../sources/tutorials/ui/monitor.md). |
| 데이터 흐름 삭제 | 이제 API 및 UI를 사용하여 오류가 있거나 불필요한 데이터 흐름을 [!DNL Flow Service] 삭제할 수 있습니다. 자세한 내용은 API를 사용하여 데이터 흐름 [삭제](../../sources/tutorials/api/delete-dataflows.md) 및 UI를 사용하여 데이터 흐름 [삭제에 대한 자습서를 참조하십시오](../../sources/tutorials/ui/delete.md). |

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).