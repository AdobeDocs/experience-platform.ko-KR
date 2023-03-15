---
keywords: Experience Platform;홈;자주 찾는 항목;Oracle 개체 저장소;oracle 개체 저장소
solution: Experience Platform
title: UI에서 Oracle 개체 스토리지 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Oracle 개체 스토리지 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 만들기 [!DNL Oracle Object Storage] UI의 소스 연결

이 튜토리얼에서는 [!DNL Oracle Object Storage] Adobe Experience Platform UI를 사용한 소스 연결.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

에 연결하려면 [!DNL Oracle Object Storage], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUrl` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 끝점입니다. 끝점 형식은 다음과 같습니다. `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 액세스 키 ID. |
| `secretKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 암호입니다. |
| `bucketName` | 사용자의 액세스가 제한된 경우 허용된 버킷 이름이 필요합니다. 버킷 이름은 3자에서 63자 사이여야 하며 문자 또는 숫자로 시작하고 끝나야 하며 소문자, 숫자 또는 하이픈(`-`). 버킷 이름의 형식은 IP 주소처럼 지정할 수 없습니다. |
| `folderPath` | 사용자의 액세스가 제한된 경우 허용되는 폴더 경로가 필요합니다. |

이러한 값을 얻는 방법에 대한 자세한 내용은 [Oracle 개체 스토리지 인증 안내서](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

필요한 자격 증명을 수집했으면 아래 단계에 따라 플랫폼에 연결할 새 Oracle 개체 스토리지 계정을 생성할 수 있습니다.

## oracle 개체 저장소에 연결

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 클라우드 스토리지] 범주, 선택 **[!UICONTROL Oracle 개체 스토리지]** 다음을 선택합니다. **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 기존 계정

기존 계정을 사용하려면 [!DNL Oracle Object Storage] 새 데이터 흐름을 만들 계정 을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![기존](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 새 계정

새 계정을 만드는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**&#x200B;을 누르고 이름, 설명(선택 사항) 및 [!DNL Oracle Object Storage] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![신규](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 다음 단계

이 자습서를 따라 [!DNL Oracle Object Storage] 계정입니다. 이제 의 다음 자습서로 진행할 수 있습니다. [클라우드 스토리지에서 플랫폼으로 데이터를 가져오기 위한 데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).
