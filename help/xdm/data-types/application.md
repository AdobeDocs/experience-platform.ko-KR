---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;응용 프로그램;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 응용 프로그램 데이터 유형
description: 이 문서에서는 XDM(애플리케이션 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# [!UICONTROL 애플리케이션] 데이터 유형

[!UICONTROL 애플리케이션] 는 애플리케이션에서 생성된 상호 작용과 관련된 세부 사항을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다. 응용 프로그램은 최종 사용자가 설치, 실행, 닫기 또는 제거할 수 있는 모바일 또는 데스크톱 응용 프로그램과 같은 소프트웨어 환경을 나타냅니다. 이 데이터 유형에 대한 속성은 차트보트, 브라우저 기반 플러그인 또는 애플리케이션에 적용되지 않는 기타 경험과 같은 에이전트를 설명하는 것이 아닙니다.

<img src="../images/data-types/application.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 측정]](./measure.md) | 응용 프로그램 종료에 대한 세부 정보를 설명합니다. |
| `crashes` | [[!UICONTROL 측정]](./measure.md) | 이 속성은 애플리케이션이 의도한 대로 종료되지 않을 때 트리거됩니다. |
| `featureUsages` | [[!UICONTROL 측정]](./measure.md) | 측정되는 응용 프로그램 기능의 활성화로부터 얻은 모든 데이터를 설명합니다. |
| `firstLaunches` | [[!UICONTROL 측정]](./measure.md) | 첫 번째 실행 시 데이터를 포함합니다. 이 속성은 설치 후 처음 시작할 때 트리거됩니다. |
| `installs` | [[!UICONTROL 측정]](./measure.md) | 특정 설치 이벤트를 사용할 수 있는 경우 장치에 응용 프로그램 설치를 기록합니다. |
| `launches` | [[!UICONTROL 측정]](./measure.md) | 응용 프로그램 실행과 관련된 값을 설명합니다. 세션 시간이 초과되면 충돌, 설치 및 백그라운드 시작을 포함하여 실행 시마다 트리거됩니다. |
| `upgrades` | [[!UICONTROL 측정]](./measure.md) | 이전에 설치된 애플리케이션 업그레이드에 대한 데이터를 포함합니다. 업그레이드 후 첫 번째 실행 시 트리거됩니다. |
| `id` | 문자열 | 응용 프로그램의 고유 식별자입니다. |
| `name` | 문자열 | 응용 프로그램의 이름입니다. |
| `userPerspective` | 문자열 | 이벤트가 발생한 시점에 사용자와 앱 또는 브랜드 간의 관점 또는 물리적 관계. 앱과 관련하여 사용자의 관점을 이해하면 포함하지 않으려는 대부분의 시간에 따라 세션을 정확하게 생성할 수 있습니다 `background` 및 `detached` 이벤트를 &quot;활성&quot; 세션의 일부로 표시합니다. 이 속성의 값은 아래 나열된 열거형 값 중 하나와 같아야 합니다. <li> `foreground`: 사용자 및 앱이 서로 직접 상호 작용합니다. </li> <li> `background`: 앱과 사용자가 간접적으로 상호 작용합니다. 예를 들어, 화면이 잠겨 있거나 포그라운드에서 다른 앱이 사용되는 동안 앱에서 값을 측정하고 새로 고칠 수 있습니다.  </li> <li> `detached`: 분리된 것은 이벤트가 앱과 관련되어 있지만 외부 시스템에서 이메일 보내기 또는 푸시 알림 등과 같이 앱에서 직접 오지 않았음을 의미합니다. |
| `version` | 문자열 | 애플리케이션 버전입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
