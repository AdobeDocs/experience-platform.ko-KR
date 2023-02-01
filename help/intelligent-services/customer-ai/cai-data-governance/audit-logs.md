---
keywords: 인사이트;고객 ai;고객 ai 인사이트;CAI 쿼리 서비스;고객 ai 쿼리;고객 ai 점수
title: 고객 AI의 감사 로그 개요
description: Customer AI에서 감사 로그를 보고 관리하는 방법을 알아봅니다.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 36%

---

# 감사 로그

시스템에서 수행되는 활동의 투명성과 가시성을 높이기 위해 이제 고객 AI 워크플로우 내의 사용자 활동을 감사 로그에 캡처하여 고객 AI 모델에 대한 사용자 기반 변경 사항을 이해합니다. 이러한 로그는 문제 해결에 도움이 될 수 있는 감사 추적을 형성하며 기업의 데이터 관리 정책 및 규정 요구 사항을 효과적으로 준수할 수 있도록 도와줍니다.  HIPAA(Health Insurance Portability and Accountability Act)를 적용받고 Attribution AI 또는 Customer AI를 통해 허용 가능한 중요한 개인 데이터를 생성, 수신, 유지 관리 또는 전송하는 경우 Adobe 및 라이센스 관리 쉴드를 통해 BAA를 실행해야 합니다.

기본적으로 감사 로그는 어떤 사람이 어떤 작업을 언제 수행했는지 알려 줍니다. 로그에 기록된 각 작업에는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 작업 유형과 관련된 추가 속성을 나타내는 메타데이터가 포함됩니다. Customer AI 사용자가 수행한 만들기, 업데이트 및 삭제 작업을 추적합니다.

[Customer AI 작업 공간에서 선택한 감사 로그](../../customer-ai/images/data-governance/audit-logs-cai.png)

## 감사 로그 액세스

조직에서 이 기능을 활성화하면 활동이 발생할 때 감사 로그가 자동으로 수집됩니다. 로그 수집을 수동으로 활성화할 필요가 없습니다.

감사 로그를 보고 내보내려면 Adobe Console의 감사 로그 액세스 액세스 제어 권한이 필요합니다. 고객 AI 기능에 대한 개별 권한을 관리하는 방법에 대한 자세한 내용은 [액세스 제어 설명서](../cai-data-governance/access-controls.md).