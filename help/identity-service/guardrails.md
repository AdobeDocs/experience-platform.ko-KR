---
keywords: Experience Platform;ID;ID 서비스;문제 해결;보호 기능;지침;제한;
title: ID 서비스에 대한 보호 기능
description: 이 문서에서는 ID 그래프 사용을 최적화하는 데 도움이 되는 ID 서비스 데이터의 사용 및 비율 제한에 대한 정보를 제공합니다.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 2%

---

# 보호 기능 [!DNL Identity Service] 데이터

이 문서에서는 [!DNL Identity Service] id 그래프의 사용을 최적화하는 데 도움이 되는 데이터. 다음 보호 기능을 검토할 때 데이터를 올바르게 모델링했다고 가정합니다. 데이터를 모델링하는 방법에 대한 질문이 있는 경우 고객 서비스 담당자에게 문의하십시오.

## 시작하기

다음 Experience Platform 서비스는 ID 데이터 모델링 작업에 관련되어 있습니다.

* [ID](home.md): 플랫폼에 수집하여 다양한 데이터 소스에서 ID를 전달합니다.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): 여러 소스의 데이터를 사용하여 통합 소비자 프로필을 만들 수 있습니다.

## 데이터 모델 제한

아래 표는 정적 제한에 대한 보호 지침과 ID 네임스페이스에 대해 고려해야 하는 유효성 검사 규칙에 대한 지침을 제공합니다.

### 정적 제한

다음 표에서는 ID 데이터에 적용된 정적 제한에 대해 설명합니다.

| 가드레일 | 제한 | 참고 |
| --- | --- | --- |
| 그래프의 ID 수 | 150 | 이 제한은 샌드박스 수준에서 적용됩니다. 제한에 도달하면 ID 그래프가 업데이트되지 않습니다. **참고**: ID 그래프의 최대 ID 수 **개별 병합된 프로필용** 은 50입니다. 50개 이상의 ID를 갖는 ID 그래프를 기반으로 병합된 프로필은 실시간 고객 프로필에서 제외됩니다. 자세한 내용은 다음 안내서를 참조하십시오. [프로필 데이터에 대한 보호 기능](../profile/guardrails.md). |
| XDM 레코드의 ID 수 | 20 | 필요한 최소 XDM 레코드 수는 2개입니다. |
| 사용자 지정 네임스페이스 수 | None | 만들 수 있는 사용자 지정 네임스페이스의 수에는 제한이 없습니다. |
| 그래프 수 | None | 만들 수 있는 ID 그래프 수에는 제한이 없습니다. |
| 네임스페이스 표시 이름 또는 ID 기호의 문자 수 | None | 네임스페이스 표시 이름 또는 ID 심볼의 문자 수에는 제한이 없습니다. |

### ID 값 유효성 검사

다음 표에서는 ID 값의 성공적인 유효성 검사를 위해 따라야 하는 기존 규칙에 대해 설명합니다.

| 네임스페이스 | 유효성 검사 규칙 | 규칙을 위반할 때 시스템 동작 |
| --- | --- | --- |
| ECID | <ul><li>ECID의 ID 값은 정확히 38자여야 합니다.</li><li>ECID의 ID 값은 숫자로만 구성되어야 합니다.</li></ul> | <ul><li>ECID의 ID 값이 정확히 38자가 아닌 경우 레코드를 건너뜁니다.</li><li>ECID의 ID 값에 숫자가 아닌 문자가 포함되어 있으면 레코드를 건너뜁니다.</li></ul> |
| 비ECID | ID 값은 1024자를 초과할 수 없습니다. | ID 값이 1024자를 초과하는 경우 레코드를 건너뜁니다. |

### ID 네임스페이스 수집

2023년 1월 31일부터 Identity 서비스는 신규 고객에 대한 Adobe Analytics ID(AAID) 수집을 차단합니다. 이 ID는 일반적으로 [Adobe Analytics 소스](../sources/connectors/adobe-applications/analytics.md) 그리고 [Adobe Audience Manager 소스](../sources//connectors/adobe-applications/audience-manager.md) 및 는 ECID가 동일한 웹 브라우저를 나타내므로 중복됩니다. 이 기본 구성을 변경하려면 계정 관리자에게 문의하십시오.

## 다음 단계

자세한 내용은 다음 설명서를 참조하십시오 [!DNL Identity Service]:

* [[!DNL Identity Service] 개요](home.md)
* [ID 그래프 뷰어](ui/identity-graph-viewer.md)
