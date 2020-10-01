---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data prep;data preparation;preparing data;
solution: Experience Platform
title: 매핑 함수
topic: overview
description: 이 문서에서는 Adobe Experience Platform 내의 데이터 준비를 소개합니다.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 데이터 준비

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다. 데이터 준비는 CSV 통합 작업 과정을 포함하여 데이터 통합 프로세스에서 &quot;맵&quot; 단계로 표시됩니다. 데이터 엔지니어는 데이터 준비를 사용하여 통합 중에 다음 데이터 조작을 수행할 수 있습니다.

- XDM 속성에 입력 속성을 할당하는 간단한 통과 매핑 정의
- XDM 속성에 할당할 수 있는 행 내 계산을 수행할 계산된 필드를 만듭니다.
- 문자열, 숫자 또는 날짜 조작 함수를 적용하여 데이터를 변환합니다.
- 계층적 함수를 사용하여 XDM 계층 구성
- 데이터 준비 내에서 수정되는 대로 데이터 미리 보기

또한 데이터 준비는 데이터 무결성을 인제스트할 때 유지할 수 있도록 여러 가지 내부 데이터 유효성 검사를 적용합니다. 가능한 경우 데이터 준비(Data Prep)는 들어오는 데이터 스키마를 XDM에 자동으로 매핑합니다. 데이터 엔지니어는 제안된 매핑을 변경, 수정 및 삭제하고 적절한 매핑으로 대체할 수 있습니다.

## 매핑

매핑은 입력 특성 또는 계산된 필드의 연결로서, 하나의 XDM 특성에 해당합니다. 개별 매핑을 만들어 단일 속성을 여러 XDM 특성에 매핑할 수 있습니다.

다른 매핑 기능에 대한 자세한 내용은 [매핑 기능 안내서를 참조하십시오](./functions.md).

## 매핑 집합

한 스키마를 다른 스키마로 변환하는 매핑 집합을 통칭하여 매핑 집합이라고 합니다. 단일 매핑 세트가 각 데이터 흐름의 일부로 생성됩니다. 매핑 세트는 데이터 플로우의 필수 부분이며 데이터 흐름의 일부로 생성, 편집 및 모니터링됩니다.

## 다음 단계

이 문서에서는 Adobe Experience Platform의 데이터 준비에 대한 기본 사항을 다룹니다. 서로 다른 매핑 기능에 대한 자세한 내용은 [매핑 기능 안내서를 참조하십시오](./functions.md). 서로 다른 날짜/시간 문자열에 대한 자세한 내용은 [날짜 문자열 안내서를 참조하십시오](./dates.md).