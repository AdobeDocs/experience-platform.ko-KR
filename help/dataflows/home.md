---
keywords: Experience Platform;홈;자주 찾는 항목;데이터 흐름;데이터 흐름;데이터;모니터링;데이터 흐름 모니터링;데이터 흐름 모니터링;모니터링;데이터 흐름 모니터링;데이터 흐름 모니터링;흐름;흐름 서비스;
solution: Experience Platform
title: 데이터 흐름 개요
description: 이 문서에서는 Adobe Experience Platform에서 데이터 흐름이 사용되는 방식을 보여 주는 데이터 흐름을 소개합니다.
exl-id: 8fe08ffa-f095-4e9f-8bab-d060985f0236
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 7%

---

# 데이터 흐름 개요

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되고, Experience Platform 내에서 분석되며, 다양한 대상으로 활성화됩니다. Experience Platform은 데이터 흐름을 투명하게 제공하여 이 잠재적으로 비선형적인 데이터 흐름을 추적하는 프로세스를 보다 쉽게 만듭니다.

## 데이터 흐름 사용

데이터 흐름은 Experience Platform 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되어 데이터를 소스 커넥터에서 대상 데이터 세트로 이동하는 데 도움이 되며, 이 데이터 흐름은 최종적으로 대상에 활성화되기 전에 ID 서비스 및 실시간 고객 프로필에 의해 사용됩니다.

소스 커넥터에서 데이터 흐름을 사용하는 방법에 대한 자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.

## 데이터 준비 중

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

수집된 후 데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../data-prep/home.md)를 참조하십시오.

## 데이터 흐름 모니터링

Experience Platform API 또는 Experience Platform UI를 사용하여 데이터 흐름을 모니터링할 수 있습니다. API를 사용하여 데이터 흐름을 모니터링하는 방법은 [데이터 흐름 모니터링 API 자습서](./api/monitor.md)를 참조하십시오. Experience Platform UI에서 데이터 흐름을 모니터링하는 방법을 알아보려면 [소스에 대한 데이터 흐름 모니터링](./ui/monitor-sources.md) 및 [대상에 대한 데이터 흐름 모니터링](./ui/monitor-destinations.md)에 대한 튜토리얼을 참조하십시오.
