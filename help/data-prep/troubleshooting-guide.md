---
keywords: Experience Platform;홈;인기 있는 주제
title: 데이터 준비 문제 해결 안내서
topic-legacy: troubleshooting
description: 이 문서에서는 Adobe Experience Platform 데이터 준비에 대해 자주 묻는 질문과 답변을 제공합니다.
source-git-commit: e96263847f53ea2c884c273fd7986855d4c478c1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# [!DNL Data Prep] 문제 해결 안내서

이 문서에서는 Adobe Experience Platform에 대해 자주 묻는 질문에 대한 답변을 제공합니다 [!DNL Data Prep]뿐만 아니라 일반적인 오류에 대한 문제 해결 안내서도 제공됩니다. 일반적으로 플랫폼 API에 대한 질문 및 문제 해결 정보는 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md).

## FAQ

다음은 FAQ 목록입니다 [!DNL Data Prep] 그리고 그들의 대답들.

### 변환 오류는 어떻게 해결됩니까?

[!DNL Data Prep] 모든 변환 오류를 발생한 열에 현지화합니다. 결과적으로 해당 열이 무효화되고 나머지 행은 계속 처리됩니다. 이러한 변환 문제는 **경고**. 정기적으로 경고를 검토하고 변환 문제를 고려하여 변환 논리를 조정하는 것이 좋습니다. 이렇게 하면 Experience Platform에 수집된 데이터의 품질이 증가합니다.

열을 **필수 여부** 변환 문제로 인해 무효화된 경우 행이 수집되지 않습니다. 부분 데이터 처리가 활성화되면 전체 흐름이 실패하기 전에 이러한 거부의 임계값을 설정할 수 있습니다. 무효화 속성이 스키마 수준 유효성 검사에 영향을 주지 않으면 행이 계속 수집됩니다.

변환 오류 없이 유효하지 않은 행도 거부됩니다. 예를 들어, 데이터 수집 플로우에는 필수 필드에 대한 통과 매핑(변환 논리 없음)이 있으며, 해당 속성에 대해 들어오는 값이 없을 수 있습니다. 이 행은 거부됩니다.