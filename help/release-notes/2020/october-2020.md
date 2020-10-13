---
title: Adobe Experience Platform 릴리스 정보
description: 2020년 10월 Experience Platform 릴리스 노트
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: ab87cac94ae69acde3be75ae95b11cf003a274e9
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 7%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜:2020년 10월**

- [데이터 준비](#data-prep)
- [소스](#sources)

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| `is_set` 함수 위에 있어야 합니다 | 이 `is_set` 함수를 사용하면 소스 데이터 내에 속성이 있는지 확인할 수 있습니다. `is_set` 과 함께 사용하여 속성 `is_empty` 의 존재와 속성 내의 값 존재를 모두 확인할 수 있습니다. |
| `get_values` 함수 위에 있어야 합니다 | 이 `get_values` 함수를 사용하면 주어진 키에 대한 입력 맵에서 값을 가져올 수 있습니다. |

자세한 내용은 [데이터 준비 개요를 참조하십시오](../../data-prep/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계층 매핑 | 데이터 수집 프로세스 중에 JSON 또는 Partiented와 같은 계층적 소스 파일을 미리 볼 수 있습니다. |
| SFTP에 대한 SSH 인증 지원 | SFTP 계정을 RSA/DSA Open SSH 키 [!DNL Platform] 를 사용하여 연결할 수 있습니다. 자세한 내용은 [SFTP 개요를](../../sources/connectors/cloud-storage/ftp-sftp.md) 참조하십시오. |
| 향상된 UX | 데이터 수집 프로세스 [!DNL Profile] 중에 데이터 세트를 활성화할 수 있습니다. 자세한 내용은 [클라우드 스토리지 데이터 흐름](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 자습서를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).