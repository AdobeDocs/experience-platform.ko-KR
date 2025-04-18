---
solution: Experience Platform
title: PDF에 Experience Platform 대시보드 다운로드
type: Documentation
description: Experience Platform UI 내에서 사용할 수 있는 PDF으로 다운로드 기능을 사용하여 대시보드 시각화의 사본을 저장합니다.
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# PDF에 대시보드 다운로드

Adobe Experience Platform 내의 대시보드는 Experience Platform 사용자 인터페이스 내에서 PDF으로 다운로드하여 조직 구성원과 정보를 공유할 수 있습니다.

이 문서에서는 Experience Platform UI를 사용하여 대시보드를 다운로드하고 기본 브라우저 인쇄 메뉴를 사용하여 PDF에 대시보드를 저장하는 방법에 대한 요약을 제공합니다.

>[!WARNING]
>
>대시보드에 포함된 데이터에는 고객에 대한 PII(개인 식별 정보) 또는 조직과 관련된 중요한 데이터가 포함될 수 있습니다. PDF에 저장된 모든 대시보드 데이터는 조직의 데이터 개인 정보 보호 지침에 따라 적절하게 처리해야 합니다.

## 대시보드 다운로드

대시보드 다운로드를 시작하려면 다운로드할 대시보드(예: [!UICONTROL 프로필] 대시보드)로 이동한 다음 대시보드의 오른쪽 상단 모서리에서 추가 옵션 메뉴(**`...`**)를 선택합니다. 그런 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.

![줄임표 및 다운로드 드롭다운이 강조 표시된 Experience Platform 프로필 대시보드입니다.](images/download/download-button.png)

## PDF 미리 보기

**[!UICONTROL 다운로드]**&#x200B;를 선택하면 브라우저의 기본 인쇄 메뉴가 열립니다. 이 예에서는 Google Chrome 인쇄 메뉴가 표시됩니다.

인쇄 메뉴를 사용하면 저장할 PDF을 미리 볼 수 있습니다. PDF은 Experience Platform UI에 표시되므로 대시보드 위젯을 실제로 표현한 것이며 PDF의 크기는 현재 표시되는 모든 대시보드 위젯을 단일 페이지에 표시하도록 자동으로 조정됩니다.

![오른쪽에 인쇄 옵션 패널이 있는 단일 페이지 형식으로 표시되는 프로필 개요입니다.](images/download/download-chrome-print.png)

PDF에는 Experience Platform 로고, 대시보드 이름, 사용자 이름 및 대시보드를 다운로드한 날짜 및 시간이 포함된 자동으로 생성된 헤더가 포함됩니다. 이 정보는 읽기 전용이므로 PDF에서 편집할 수 없습니다.

![자동으로 생성된 헤더가 강조 표시된 인쇄 미리 보기를 닫습니다.](images/download/download-pdf.png)

## PDF으로 저장

PDF을 미리 본 후 **저장**&#x200B;을 선택하여 PDF을 저장할 위치를 선택합니다.

>[!NOTE]
>
>필요한 경우 해당 옵션이 자동으로 선택되지 않은 경우 **대상** 드롭다운을 사용하여 **PDF으로 저장**&#x200B;을 선택할 수 있습니다.

![프로필 개요가 [대상] 드롭다운인 [PDF으로 저장] 인쇄 옵션이 강조 표시된 단일 페이지 형식으로 표시됩니다.](images/download/download-chrome-print-destination.png)

## 대시보드 PDF 사용자 지정

생성된 PDF은 UI에서 볼 수 있는 대시보드와 일치하며 현재 대시보드에 표시된 위젯만 포함합니다. 특정 대시보드를 사용자 정의하여 위젯의 크기와 위치를 변경하거나 보기에서 위젯을 추가 및 제거할 수 있습니다. Experience Platform UI에서 대시보드 모양을 사용자 지정하면 생성되는 PDF 모양도 변경됩니다.

예를 들어 세 개의 표준 위젯 위에 스택된 여러 전체 너비 위젯을 포함하도록 프로필 대시보드의 모양을 수정할 수 있습니다.

![길쭉한 위젯을 표시하는 프로필 대시보드입니다.](images/download/download-modify.png)

업데이트된 대시보드를 다운로드하도록 선택하면 맞춤화된 프로필 대시보드의 모양과 일치하는 새로운 PDF 미리보기가 생성됩니다. 또한 PDF의 크기를 자동으로 조정하여 표시되는 모든 위젯이 한 페이지 PDF에 포함되도록 합니다.

![오른쪽에 인쇄 옵션 패널이 있는 단일 페이지 형식으로 표시되는 프로필 개요입니다.](images/download/download-chrome-print-modified.png)

대시보드 사용자 지정에 대한 자세한 내용은 [대시보드 사용자 지정 개요](customize/overview.md)를 참조하세요.

## 다음 단계

이제 대시보드를 다운로드하여 PDF으로 저장했으므로 다음 단계를 반복하여 추가 대시보드를 다운로드하거나 조직의 구성원과 PDF을 공유할 수 있습니다.
