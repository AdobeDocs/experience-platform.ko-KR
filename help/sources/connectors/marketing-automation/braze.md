---
title: Braze Currents 소스 개요
description: 브레이즈 커런트에서 Experience Platform으로 데이터를 스트리밍하는 방법에 대해 알아봅니다.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 2%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>다음 [!DNL Braze Currents] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 스트리밍 애플리케이션에서 데이터를 수집할 수 있도록 지원합니다. 스트리밍 공급자에 대한 지원은 다음을 포함합니다. [!DNL Braze Currents].

[!DNL Braze] 는 실시간으로 소비자와 브랜드 간의 고객 중심 상호 작용을 강화합니다. [!DNL Braze Currents] 는 Braze 플랫폼의 참여 이벤트에 대한 실시간 데이터 스트림으로, 에서 가장 강력하면서도 세부적인 내보내기입니다. [!DNL Braze] 플랫폼.

## 전제 조건

이 안내서의 단계를 완료하려면 다음이 필요합니다.

* 에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 새 스트리밍 소스 연결을 만들 수 있는 권한입니다.
* 에 대한 로그인 [[!DNL Braze] 대시보드](https://dashboard.braze.com/sign_in), 사용되지 않음 [Current Connector 라이선스](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)및 커넥터를 만들 수 있는 권한. 자세한 내용은 [설정 요구 사항 [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### 필요한 자격 증명 수집

제출 방법 [!DNL Braze Currents] 데이터를 Experience Platform 하려면 다음에 Experience Platform 자격 증명을 입력해야 합니다. [!DNL Braze] UI 대시보드.

| 필드 | 설명 |
| --- | --- |
| 클라이언트 ID | Experience Platform 소스와 연결된 클라이언트 ID. |
| 클라이언트 암호 | Experience Platform 소스와 연결된 클라이언트 암호입니다. |
| 임차인 ID | Experience Platform 소스와 연결된 테넌트 ID입니다. |
| 샌드박스 이름 | Experience Platform 소스와 연결된 샌드박스 입니다. |
| 데이터 흐름 ID | Experience Platform 소스와 연결된 데이터 흐름 ID. |
| 스트리밍 엔드포인트 | Experience Platform 소스와 연결된 스트리밍 엔드포인트. **참고**: [!DNL Braze] 는 이 항목을 일괄 처리 스트리밍 끝점으로 자동 변환합니다. |

이러한 값을 검색하는 방법에 대한 자세한 내용은 [platform API 시작하기](../../../landing/api-authentication.md). 사용에 대한 자세한 내용 [!DNL Braze] 대시보드, 다음 읽기 [!DNL Braze] 방법 안내서 [전류 탐색](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## 다음 단계

이 문서를 읽으면 의 데이터를 스트리밍하는 데 필요한 사전 요구 사항 설정을 완료한 것입니다. [!DNL Braze Currents] Experience Platform 계정. 이제 의 안내서로 진행할 수 있습니다. [연결 중 [!DNL Braze Currents] 사용자 인터페이스를 사용하여 Experience Platform](../../tutorials/ui/create/marketing-automation/braze.md).