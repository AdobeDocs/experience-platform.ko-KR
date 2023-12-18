---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;애플리케이션;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 애플리케이션 데이터 유형
description: XDM(애플리케이션 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# [!UICONTROL 애플리케이션] 데이터 유형

[!UICONTROL 애플리케이션] 는 애플리케이션에서 생성된 상호 작용과 관련된 세부 사항을 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 애플리케이션은 최종 사용자가 설치, 실행, 종료 또는 제거할 수 있는 모바일 또는 데스크탑 애플리케이션과 같은 소프트웨어 경험을 의미합니다. 이 데이터 유형의 속성은 챗봇, 브라우저 기반 플러그인 또는 애플리케이션에 적용되지 않는 기타 경험과 같은 에이전트를 설명하기 위한 것이 아닙니다.

<img src="../images/data-types/application.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 측정]](./measure.md) | 응용 프로그램 종료에 대한 세부 정보를 설명합니다. |
| `crashes` | [[!UICONTROL 측정]](./measure.md) | 이 속성은 응용 프로그램이 의도한 대로 종료되지 않을 때 트리거됩니다. |
| `featureUsages` | [[!UICONTROL 측정]](./measure.md) | 측정 중인 응용 프로그램 기능 활성화의 모든 데이터를 설명합니다. |
| `firstLaunches` | [[!UICONTROL 측정]](./measure.md) | 첫 번째 론치에 대한 데이터를 포함합니다. 이 속성은 설치 후 첫 번째 실행 시 트리거됩니다. |
| `installs` | [[!UICONTROL 측정]](./measure.md) | 특정 설치 이벤트를 사용할 수 있을 때 장치에서 응용 프로그램 설치를 기록합니다. |
| `launches` | [[!UICONTROL 측정]](./measure.md) | 응용 프로그램 시작과 관련된 값을 설명합니다. 이 작업은 세션 시간 제한이 초과된 경우 충돌, 설치 및 백그라운드에서 다시 시작하는 작업을 포함하여 실행할 때마다 트리거됩니다. |
| `upgrades` | [[!UICONTROL 측정]](./measure.md) | 이전에 설치된 응용 프로그램의 업그레이드에 대한 데이터를 포함합니다. 이 이벤트는 업그레이드 후 첫 번째 실행에서 트리거됩니다. |
| `id` | 문자열 | 애플리케이션에 대한 고유 식별자. |
| `name` | 문자열 | 애플리케이션 이름. |
| `userPerspective` | 문자열 | 이벤트 발생 시 사용자와 앱 또는 브랜드 간의 관점 또는 물리적 관계. 앱과 관련하여 사용자의 관점을 이해하면 포함하지 않으려는 대부분의 시간에 세션을 정확하게 생성하는 데 도움이 됩니다 `background` 및 `detached` &quot;활성&quot; 세션의 일부인 이벤트입니다. 이 속성의 값은 아래 나열된 열거형 값 중 하나와 같아야 합니다. <li> `foreground`: 사용자 및 앱이 서로 직접 상호 작용하고 있습니다. </li> <li> `background`: 앱과 사용자가 서로 간접적으로 상호 작용하고 있습니다. 예를 들어, 화면이 잠겨 있거나 다른 앱이 전경에서 사용되는 동안 앱에서 값을 측정하고 새로 고칠 수 있습니다.  </li> <li> `detached`: 분리는 이벤트가 앱과 관련되었지만 외부 시스템에서 이메일 또는 푸시 알림 전송과 같이 앱에서 직접 제공되지 않았음을 의미합니다. |
| `version` | 문자열 | 애플리케이션의 버전입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
