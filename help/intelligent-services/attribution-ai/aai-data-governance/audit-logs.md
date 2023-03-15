---
keywords: 통찰력;기여도 ai;기여도 ai 통찰력;AAI 쿼리 서비스;기여도 쿼리;기여도 점수
title: Attribution AI 개요의 감사 로그
description: Attribution AI에서 감사 로그를 보고 관리하는 방법을 알아봅니다.
source-git-commit: a68d4634c6341f27673fdd70d96f7e214032b5a9
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 38%

---

# 감사 로그

시스템에서 수행되는 활동의 투명성과 가시성을 높이기 위해 이제 Attribution AI 워크플로 내의 사용자 활동이 감사 로그에 캡처되어 Attribution AI 모델에 대한 사용자 중심의 변경 사항을 이해합니다. 이러한 로그는 문제 해결에 도움이 될 수 있는 감사 추적을 형성하며, 기업이 기업 데이터 관리 정책 및 규정 요구 사항을 효과적으로 준수하는 데 도움이 됩니다.  HIPAA(Health Insurance Portability and Accountability Act)를 준수하고 Attribution AI 또는 Customer AI를 통해 허용된 중요한 개인 데이터를 생성, 수신, 유지 관리 또는 전송하는 경우, Adobe 및 Healthcare Shield 라이선스가 포함된 BAA를 실행할 책임이 있습니다.

기본적으로 감사 로그는 어떤 사람이 어떤 작업을 언제 수행했는지 알려 줍니다. 로그에 기록된 각 작업에는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 작업 유형과 관련된 추가 속성을 나타내는 메타데이터가 포함됩니다. Attribution AI에서 사용자가 수행한 만들기, 업데이트 및 삭제 작업을 추적합니다.

<!-- [The audit logs selected in the Attribution AI workspace](../../../attribution-ai/aai-data-governance/images/data-governance/audit-logs-cai.png) -->

## 감사 로그 액세스

조직에서 이 기능을 활성화하면 활동이 발생할 때 감사 로그가 자동으로 수집됩니다. 로그 수집을 수동으로 활성화할 필요가 없습니다.

감사 로그를 보고 내보내려면 Adobe Console의 감사 로그 액세스 액세스 제어 권한이 필요합니다. Attribution AI 기능에 대한 개별 권한을 관리하는 방법을 알아보려면 [액세스 제어 설명서](../aai-data-governance/access-controls.md).

