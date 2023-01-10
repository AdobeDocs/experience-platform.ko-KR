---
keywords: Experience Platform;홈;인기 항목;Oracle 개체 저장소;oracle 개체 저장소
solution: Experience Platform
title: UI에서 Oracle 개체 저장소 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Oracle 개체 저장소 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 만들기 [!DNL Oracle Object Storage] UI의 소스 연결

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Oracle Object Storage] Adobe Experience Platform UI를 사용한 소스 연결.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

에 연결하려면 [!DNL Oracle Object Storage]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUrl` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 끝점입니다. 끝점 형식은 다음과 같습니다. `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 액세스 키 ID입니다. |
| `secretKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 암호입니다. |
| `bucketName` | 사용자가 액세스를 제한한 경우 필요한 허용된 버킷 이름입니다. 버킷 이름은 3자에서 63자 사이여야 하며 문자 또는 숫자로 시작하고 끝나야 하며, 소문자, 숫자 또는 하이픈만 포함할 수 있습니다(`-`). 버킷 이름은 IP 주소처럼 지정할 수 없습니다. |
| `folderPath` | 사용자가 액세스를 제한한 경우 필요한 허용된 폴더 경로입니다. |

이러한 값을 가져오는 방법에 대한 자세한 내용은 [Oracle 개체 저장소 인증 안내서](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

필요한 자격 증명을 수집하면 아래 단계에 따라 Platform에 연결할 새 Oracle 개체 저장소 계정을 만들 수 있습니다.

## oracle 개체 저장소에 연결

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 클라우드 스토리지] 카테고리, 선택 **[!UICONTROL Oracle 개체 저장소]** 그런 다음 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 기존 계정

기존 계정을 사용하려면 [!DNL Oracle Object Storage] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름, 선택적 설명 및 을 입력합니다. [!DNL Oracle Object Storage] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![새](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 다음 단계

이 자습서에 따라 [!DNL Oracle Object Storage] 계정이 필요합니다. 이제 다음 자습서를 [클라우드 저장소에서 플랫폼으로 데이터를 가져오도록 데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).
