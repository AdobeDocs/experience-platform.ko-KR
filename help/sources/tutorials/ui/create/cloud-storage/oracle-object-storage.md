---
keywords: Experience Platform;홈;자주 찾는 항목;Oracle 개체 저장소;oracle 개체 저장소
solution: Experience Platform
title: UI에서 Oracle 개체 스토리지 Source 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Oracle 개체 스토리지 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# UI에서 [!DNL Oracle Object Storage] Source 연결 만들기

이 자습서에서는 Adobe Experience Platform UI를 사용하여 [!DNL Oracle Object Storage] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Oracle Object Storage]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUrl` | 인증에 필요한 [!DNL Oracle Object Storage] 끝점입니다. 끝점 형식은 `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com`입니다. |
| `accessKey` | 인증에 필요한 [!DNL Oracle Object Storage] 액세스 키 ID. |
| `secretKey` | 인증에 필요한 [!DNL Oracle Object Storage] 암호입니다. |
| `bucketName` | 사용자의 액세스가 제한된 경우 허용된 버킷 이름이 필요합니다. 버킷 이름은 3자에서 63자 사이여야 하며 문자 또는 숫자로 시작하고 끝나야 하며 소문자, 숫자 또는 하이픈(`-`)만 포함할 수 있습니다. 버킷 이름의 형식은 IP 주소처럼 지정할 수 없습니다. |
| `folderPath` | 사용자의 액세스가 제한된 경우 허용되는 폴더 경로가 필요합니다. |

이러한 값을 가져오는 방법에 대한 자세한 내용은 [Oracle 개체 저장소 인증 안내서](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)를 참조하세요.

필요한 자격 증명을 수집했으면 아래 단계에 따라 플랫폼에 연결할 새 Oracle 개체 스토리지 계정을 생성할 수 있습니다.

## oracle 개체 저장소에 연결

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 저장소] 범주에서 **[!UICONTROL Oracle 개체 저장소]**&#x200B;를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL Oracle Object Storage] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![기존](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 이름, 선택적 설명 및 [!DNL Oracle Object Storage] 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![새로 만들기](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 다음 단계

이 자습서에 따라 [!DNL Oracle Object Storage] 계정에 대한 연결을 설정했습니다. 이제 [클라우드 저장소에서 플랫폼으로 데이터를 가져오기 위한 데이터 흐름 구성](../../dataflow/batch/cloud-storage.md)에 대한 다음 자습서로 진행할 수 있습니다.
