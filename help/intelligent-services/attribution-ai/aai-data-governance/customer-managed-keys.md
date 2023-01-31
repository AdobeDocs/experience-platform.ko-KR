---
keywords: 통찰력;기여도 분석 ai;기여도 AI 통찰력;AAI 쿼리 서비스;기여도 분석 쿼리;기여도 분석 점수; AAI의 고객 관리 키
feature: Customer-Managed Keys in Attribution AI
title: 고객 관리 키
description: Attribution AI용 고객 관리 키를 설정하는 방법을 알아봅니다.
source-git-commit: 3b1cc7ca710071df9de06428f7eed2993219ae1a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 24%

---

# 고객 관리 키

Attribution AI은 [의료 보호](https://www.adobe.com/kr/trust/compliance/hipaa-ready.html) 및 Privacy &amp; Security Shield 고객이 Attribution AI 데이터에 적용할 CMK(Azure Customer Managed Keys)를 활용할 수 있습니다. 설정 프로세스는 다음과 같습니다 [Adobe Experience Platform CMK 설정](../../../landing/governance-privacy-security/customer-managed-keys.md) 그리고 거기에 설명된 단계를 따를 수 있습니다.

설명서는에서 읽을 수 있습니다. [Adobe Experience Platform의 고객 관리 키](../../../landing/governance-privacy-security/encryption.md) 및 설정 프로세스를 진행하도록 요약된 단계를 따릅니다.

>[!NOTE]
>
>[!DNL Customer Managed Keys] 현재 는 구입한 조직에만 사용할 수 있습니다 [[!DNL Healthcare Shield or Privacy & Security Shield]](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/vertical-blueprints/healthcare-vertical.html%3Flang%3Den) 추가 기능 제공.

Platform에서 사용하는 모든 데이터는 CMK의 유무에 관계없이 데이터를 안전하게 유지하기 위해 전송 중이거나 사용하지 않을 때 암호화됩니다. Adobe Experience Platform 암호화에 대한 자세한 내용은 [데이터 암호화](../../../landing/governance-privacy-security/encryption.md).