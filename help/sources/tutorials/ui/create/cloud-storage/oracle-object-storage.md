---
keywords: Experience Platform;홈;인기 항목;Oracle 개체 저장소;oracle 개체 저장소
solution: Experience Platform
title: UI에서 Oracle 개체 저장소 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Oracle 개체 저장소 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# UI에 [!DNL Oracle Object Storage] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform UI를 사용하여 [!DNL Oracle Object Storage] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Oracle Object Storage]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUrl` | 인증에 필요한 [!DNL Oracle Object Storage] 끝점입니다. 끝점 형식은 다음과 같습니다.`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 인증에 필요한 [!DNL Oracle Object Storage] 액세스 키 ID입니다. |
| `secretKey` | 인증에 필요한 [!DNL Oracle Object Storage] 암호입니다. |
| `bucketName` | 사용자가 액세스를 제한한 경우 허용되는 버킷 이름이 필요합니다. 버킷 이름은 3자에서 63자 사이여야 하며 문자 또는 숫자로 시작하고 끝나야 하며 소문자, 숫자 또는 하이픈(`-`)만 포함할 수 있습니다. 버킷 이름은 IP 주소처럼 형식을 지정할 수 없습니다. |
| `folderPath` | 사용자가 제한된 액세스 권한을 가진 경우 허용되는 폴더 경로입니다. |

이러한 값을 얻는 방법에 대한 자세한 내용은 [Oracle 개체 저장소 인증 안내서](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)를 참조하십시오.

필요한 자격 증명을 수집했으면 아래 단계에 따라 플랫폼에 연결할 새 Oracle 개체 저장소 계정을 만들 수 있습니다.

## oracle 개체 저장소에 연결

플랫폼 UI의 왼쪽 탐색 메뉴에서 **[!UICONTROL Sources]**&#x200B;을 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. [!UICONTROL Catalog] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL Cloud storage] 범주에서 **[!UICONTROL Oracle Object Storage]**&#x200B;을 선택한 다음 **[!UICONTROL Add data]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL Oracle Object Storage] 계정을 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택하여 계속 진행합니다.

![기존](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL New account]**&#x200B;을 선택한 다음 이름, 선택적 설명 및 [!DNL Oracle Object Storage] 자격 증명을 입력합니다. 완료되면 **[!UICONTROL Connect to source]**&#x200B;을 선택한 다음 새 연결이 설정될 때까지 잠시 기다려 주십시오.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 다음 단계

이 자습서를 따라 [!DNL Oracle Object Storage] 계정에 대한 연결을 설정했습니다. 이제 데이터 흐름 구성의 다음 자습서로 이동하여 클라우드 저장소에서 Platform](../../dataflow/batch/cloud-storage.md)으로 데이터를 가져올 수 있습니다.[
