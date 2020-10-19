---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data type;
solution: Experience Platform
title: 사람 이름 데이터 유형
topic: overview
description: 이 문서에서는 사람 이름 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# [!UICONTROL 사람 이름] 데이터 유형

[!UICONTROL 사람 이름은] 사람의 전체 이름을 설명하는 표준 XDM 데이터 유형입니다. 이름 구조에 대한 규칙이 언어와 문화에서 크게 다르므로 항상 이 데이터 형식을 사용하여 이름을 모델링해야 합니다.

또한 데이터 유형에는 형식이나 비정규 인사말 만들기와 같이 전체 이름의 일부만 사용해야 하는 경우에 사용할 수 있는 여러 가지 선택 속성이 제공됩니다.

<img src="../images/data-types/person-name.png" width="500" /><br />

| 속성 | 설명 |
| --- | --- |
| `courtesyTitle` | 개인의 제목, 높임말 또는 인사말(예: `Mr.`, `Miss.`또는 `Dr.`)의 약어입니다. |
| `firstName` | 작성 순서에서 이름의 첫 번째 세그먼트는 이름 언어로 가장 일반적으로 수락됩니다. |
| `fullName` | 문자 순서로 가장 일반적으로 이름 언어로 허용되는 사람의 전체 이름입니다. |
| `lastName` | 작성 순서에서 이름의 마지막 세그먼트는 이름 언어로 가장 일반적으로 수락됩니다. |
| `middleName` | 이름과 성 사이에 제공되는 중간, 대체 또는 추가 이름 |
| `suffix` | 개인 이름 뒤에 추가 정보(예: `Jr.`, `Sr.`, `M.D.`, `PhD``I`, `II``III`,,등)를 제공하기 위해 제공되는 문자그룹입니다. |

개인 이름 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)