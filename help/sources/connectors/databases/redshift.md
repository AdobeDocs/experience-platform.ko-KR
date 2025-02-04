---
title: Amazon Redshift Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Amazon Redshift를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: 77941e08df893fab6dfdaf987c56c4d5a3fd4757
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# [!DNL Amazon Redshift] 원본

>[!IMPORTANT]
>
>- [!DNL Amazon Redshift] 소스는 Real-Time CDP Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.
>
>- 이제 Amazon Web Services(AWS)에서 Adobe Experience Platform을 실행할 때 [!DNL Amazon Redshift] 소스를 사용할 수 있습니다. 현재 AWS에서 실행 중인 Experience Platform은 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.


Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 데이터베이스에서 데이터를 수집하는 기능을 지원합니다. 플랫폼은 관계형, NoSQL 또는 데이터 웨어하우스와 같은 다양한 유형의 데이터베이스에 연결할 수 있습니다. 데이터베이스 공급자에 대한 지원에는 [!DNL Amazon Redshift]이(가) 포함됩니다.

## Azure에서 Experience Platform을 위해 [!DNL Amazon Redshift] 소스 설정 {#azure}

Azure에서 Experience Platform을 위해 [!DNL Amazon Redshift] 계정을 설정하는 방법을 알아보려면 아래 단계를 참조하세요.

### IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## Amazon Web Services에서 Experience Platform을 위한 [!DNL Amazon Redshift] 소스 설정 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. 현재 AWS에서 실행 중인 Experience Platform은 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.

[!DNL Amazon Redshift] 계정을 Amazon Web Services(AWS)의 Experience Platform에 연결하기 위해 다음 IP 주소를 허용 목록에 추가하다에 추가합니다.

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

## API를 사용하여 [!DNL Amazon Redshift]을(를) 플랫폼에 연결

- [흐름 서비스 API를 사용하여 Amazon Redshift를 Experience Platform에 연결](../../tutorials/api/create/databases/redshift.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL Amazon Redshift]을(를) 플랫폼에 연결

- [UI에서 Amazon Redshift 소스 연결 만들기](../../tutorials/ui/create/databases/redshift.md)
- [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
