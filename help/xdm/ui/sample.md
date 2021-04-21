---
solution: Experience Platform
title: UI에서 XDM 스키마에 대한 샘플 데이터 생성
description: Adobe Experience Platform 사용자 인터페이스에서 기존 스키마를 기반으로 샘플 JSON 데이터를 생성하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# UI에서 XDM 스키마에 대한 샘플 데이터 생성

데이터를 Adobe Experience Platform으로 인제스트하려면 데이터의 형식 및 구조가 기존 XDM(Experience Data Model) 스키마를 준수해야 합니다. 특정 데이터 세트에 대한 스키마의 복잡성에 따라 데이터 세트에 수집이 예상하는 데이터의 정확한 모양을 결정하기가 어려울 수 있습니다.

Experience Platform UI에서 정의하는 모든 스키마의 경우 스키마 구조를 준수하는 샘플 JSON 개체를 생성할 수 있습니다. 이 객체는 해당 스키마를 사용하는 데이터 세트에 인제스트된 모든 데이터에 대한 템플릿 역할을 할 수 있습니다.

플랫폼 UI의 왼쪽 탐색 영역에서 **[!UICONTROL Schemas]**&#x200B;을 선택합니다. **[!UICONTROL Browse]** 탭에서 샘플 데이터를 생성할 스키마를 찾습니다. 목록에서 해당 스키마를 선택하고 오른쪽 레일 업데이트를 통해 스키마에 대한 세부 정보를 표시합니다. 여기서 **[!UICONTROL Download sample file]**&#x200B;을 선택합니다.

![](../images/ui/sample/sample-data.png)

샘플 JSON 파일은 브라우저에서 다운로드됩니다. 이제 이 스키마를 사용하는 데이터 세트로 인제스트할 때 데이터를 구조화하는 방법에 대한 참조로 이 파일을 사용할 수 있습니다.

## 다음 단계

이 안내서에서는 플랫폼 UI의 XDM 스키마에서 샘플 JSON 파일을 생성하는 방법을 다룹니다. 스키마 레지스트리 API를 사용하여 샘플 데이터를 생성하는 방법에 대한 자세한 내용은 [샘플 데이터 끝점 안내서](../api/sample-data.md)를 참조하십시오.

데이터 인제스트 작업을 시작할 준비가 되면, CSV 파일을 XDM](../../ingestion/tutorials/map-a-csv-file.md)에 매핑하는 방법에 대한 자습서를 참조하여 플랫 데이터 파일(예: CSV)을 XDM 스키마에 매핑하고 이를 플랫폼에 인제스트하는 방법을 알아보십시오. [ 또는 [소스 연결](../../sources/home.md)을 설정하여 외부 소스에서 데이터를 가져와서 XDM에 매핑할 수 있습니다.

UI에서 [!UICONTROL Schemas] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL Schemas] 작업 영역 개요](./overview.md)를 참조하십시오.
