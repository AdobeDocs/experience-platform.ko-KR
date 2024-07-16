---
keywords: Experience Platform;홈;인기 있는 주제;
title: 데이터 준비 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform 데이터 준비에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# [!DNL Data Prep] 문제 해결 안내서

이 문서에서는 Adobe Experience Platform [!DNL Data Prep]에 대해 자주 묻는 질문에 대한 답변과 일반적인 오류에 대한 문제 해결 안내서를 제공합니다. 일반적으로 Platform API에 대한 질문 및 문제 해결 정보는 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## FAQ

다음은 [!DNL Data Prep]과(와) 답변에 대한 FAQ 목록입니다.

### 변환 오류는 어떻게 해결됩니까?

[!DNL Data Prep]은(는) 모든 변환 오류를 발생한 열로 지역화합니다. 그 결과 해당 열이 무효화되고 나머지 행은 계속 처리됩니다. 이러한 변환 문제는 **경고**(으)로 기록됩니다. 정기적으로 경고를 검토하고 변형 문제를 고려하여 변형 논리를 조정하는 것이 좋습니다. 이렇게 하면 Experience Platform에 수집된 데이터의 품질이 향상됩니다.

변환 문제로 인해 **Required**(으)로 표시된 열이 무효화된 경우 행이 수집되지 않습니다. 부분 데이터 수집이 활성화되면 전체 흐름이 실패하기 전에 이러한 거부의 임계값을 설정할 수 있습니다. 무효화된 속성이 스키마 수준 유효성 검사에 영향을 주지 않았다면 행은 계속 수집됩니다.

변환 오류가 없더라도 유효하지 않은 모든 행도 거부됩니다. 예를 들어 데이터 수집 흐름에는 필수 필드에 대한 통과 매핑(변환 논리 없음)이 있을 수 있으며 해당 속성에 대한 들어오는 값이 없습니다. 이 행은 거부됩니다.

### 필드에 있는 특수 문자를 어떻게 이스케이프 처리할 수 있습니까?

`${...}`을(를) 사용하여 필드의 특수 문자를 이스케이프 처리할 수 있습니다. 그러나 마침표(`.`)가 있는 필드가 포함된 JSON 파일은 이 메커니즘에서 지원되지 않습니다. 계층과 상호 작용할 때 자식 특성에 마침표(`.`)가 있으면 백슬래시(`\`)를 사용하여 특수 문자를 이스케이프 처리해야 합니다. 예를 들어 `address`은(는) 특성 `street.name`을(를) 포함하는 개체로, `address.street.name` 대신 `address.street\.name`로 참조할 수 있습니다.

### 계산된 필드의 최대 길이는 얼마입니까?

계산된 필드의 최대 길이는 4096자입니다.