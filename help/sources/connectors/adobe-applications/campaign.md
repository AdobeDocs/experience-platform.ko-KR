---
keywords: Experience Platform;홈;인기 항목;Adobe Campaign Managed Cloud Services;campaign;캠페인 관리 서비스
title: Adobe Campaign Managed Cloud Services
description: 사용자 인터페이스를 사용하여 Campaign Managed Cloud Services를 Experience Platform에 연결하는 방법을 알아봅니다
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: 1d29cdd39075aad937d078aa116ec2f6e6ec6a56
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# Adobe Campaign Managed Cloud Services

Adobe Campaign Managed Cloud Services은 크로스채널 고객 경험을 디자인하고 시각적 캠페인 오케스트레이션, 실시간 상호 작용 관리 및 크로스채널 실행을 지원하는 관리 플랫폼을 제공합니다. 자세한 내용은 [Adobe Campaign v8 설명서](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=ko)를 참조하세요.

Adobe Campaign Managed Cloud Services 소스 커넥터를 사용하면 Adobe Campaign v8에서 Adobe Experience Platform으로 게재 및 추적 로그 데이터를 수집할 수 있습니다. 이 커넥터는 플랫폼 내에서 배치 소스로 작동합니다.

## 전제 조건

소스 연결을 만들어 Campaign v8을 Experience Platform으로 가져오려면 먼저 다음 사전 요구 사항을 완료해야 합니다.

* [Adobe Campaign 클라이언트 콘솔을 사용하여 이벤트 로그 가져오기 설정](#view-delivery-and-tracking-log-data)
* [XDM ExperienceEvent 스키마 만들기](#create-a-schema)
* [데이터 세트 만들기](#create-a-dataset)

### 게재 및 추적 로그 데이터 보기 {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Campaign에서 로그 데이터를 보려면 Adobe Campaign v8 클라이언트 콘솔에 대한 액세스 권한이 있어야 합니다. 클라이언트 콘솔을 다운로드하고 설치하는 방법에 대한 자세한 내용은 [Campaign v8 설명서](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html)를 참조하십시오.

클라이언트 콘솔을 통해 Campaign v8 인스턴스에 로그인합니다. [!DNL Explorer] 탭에서 [!DNL Administration]을(를) 선택한 다음 [!DNL Configuration]을(를) 선택합니다. [!DNL Data schemas]을(를) 선택한 다음 이름 또는 레이블에 대한 `broadLog` 필터를 적용합니다. 표시되는 목록에서 이름이 `broadLogRcp`인 수신자 게재 로그 원본 스키마를 선택합니다.

![탐색기 탭이 선택된 Adobe Campaign v8 클라이언트 콘솔, 관리, 구성 및 데이터 스키마 노드 확장 및 필터링 설정이 &quot;broad&quot;로 설정되어 있습니다.](./images/campaign/explorer.png)

그런 다음 **데이터** 탭을 선택합니다.

![데이터 탭이 선택된 Adobe Campaign v8 클라이언트 콘솔입니다.](./images/campaign/data.png)

데이터 패널에서 마우스 오른쪽 버튼을 클릭/클릭하여 상황별 메뉴를 엽니다. 여기에서 **목록 구성...**&#x200B;을(를) 선택하십시오.

![상황에 맞는 메뉴가 열려 있고 목록 구성 옵션이 선택된 Adobe Campaign v8 클라이언트 콘솔입니다.](./images/campaign/configure.png)

목록 구성 창이 나타나며, 원하는 필드를 기존 목록에 추가하여 데이터 패널에서 데이터를 볼 수 있는 인터페이스를 제공합니다.

![보기용으로 추가할 수 있는 수신자 게재 로그의 구성 목록입니다.](./images/campaign/list-configuration.png)

이제 이전 단계에서 추가된 구성 필드를 포함하여 수신자 게재 로그를 볼 수 있습니다.

>[!TIP]
>
>동일한 단계를 반복할 수 있지만 추적 로그 데이터를 보려면 `tracking`을(를) 필터링합니다.

![받는 사람 게재 로그가 마지막으로 수정한 이름, 게재 채널, 내부 게재 이름 및 레이블에 대한 정보와 함께 표시됩니다.](./images/campaign/recipient-delivery-logs.png)

### 스키마 만들기 {#create-a-schema}

그런 다음 게재 로그와 추적 로그 모두에 대한 XDM ExperienceEvent 스키마를 만듭니다. 게재 로그 스키마에 Campaign 게재 로그 필드 그룹을 적용하고 추적 로그 스키마에 Campaign 추적 로그 필드 그룹을 적용해야 합니다. `externalID` 필드도 스키마의 기본 ID로 정의해야 합니다.

>[!NOTE]
>
>Campaign 데이터를 [!DNL Real-Time Customer Profile]&#x200B;(으)로 수집하려면 XDM ExperienceEvent 스키마에 프로필이 활성화되어 있어야 합니다.

스키마를 만드는 방법에 대한 자세한 지침은 [UI에서 XDM 스키마 만들기](../../../xdm/tutorials/create-schema-ui.md)에 대한 안내서를 참조하십시오.

### 데이터 세트 만들기 {#create-a-dataset}

마지막으로 스키마에 대한 데이터 세트를 만들어야 합니다. 데이터 집합을 만드는 방법에 대한 자세한 지침은 [UI에서 데이터 집합 만들기](../../../catalog/datasets/user-guide.md)에 대한 안내서를 참조하세요.

## Adobe Campaign Managed Cloud Services 소스의 예상 대기 시간 {#latency}

일반적인 데이터 볼륨과 백로그가 없다고 가정할 때 Experience Platform에서 Campaign 이벤트에서 데이터 가용성까지 걸리는 시간은 일반적으로 표준 구성(15분 복제, 마이크로 배치 내보내기 및 예약된 Experience Platform 데이터 흐름 포함)에서 15~30분입니다. 이는 예정된 마이크로 배치 동기화(보통 수십 분 정도)를 통해 달성되는 거의 실시간 프로세스이지만 지속적인 스트리밍은 아닙니다.

| 시나리오 | 세부 사항 | 예상 지연 시간 |
| --- | --- | --- |
| 캠페인 이벤트는 중간 소싱/메시지 센터 인스턴스에서 생성됩니다 | 게재 또는 추적 이벤트(보내기, 열기, 클릭 등)는 Campaign v8 실행(중간/메시지 센터) 노드에서 발생합니다. | Campaign 런타임 내 실시간(현재 Experience Platform에 표시되지 않음). |
| 런타임에서 Campaign 마케팅 데이터베이스로 복제 | 이벤트 데이터가 중간/메시지 센터에서 Campaign 마케팅 데이터베이스([!DNL Snowflake] 또는 [!DNL Postgres], 고객 크기에 따라 다름)로 복제됩니다. 표준 통합 패턴은 일반 복제 작업을 가정합니다. | 표준 15분 복제 케이던스를 기준으로 ~15분. |
| Campaign 마케팅 데이터베이스에서 랜딩 영역(예: [!DNL Data Landing Zone], [!DNL Amazon S3] 또는 [!DNL Azure Blob])으로 내보내기 | Campaign의 내보내기 워크플로우(내보내기 서비스)는 일정에 따라 실행되어 신규/변경된 게재 및 추적 로그를 추출하고 파일 기반 랜딩 영역에 마이크로 배치로 기록합니다. | 분, 내보내기 일정 간격 |
| Experience Platform 소스 데이터 흐름이 내보낸 파일을 선택합니다. | Adobe Campaign Managed Cloud Services 소스가 Experience Platform [!DNL Flow Service]에서 일괄 데이터 흐름으로 구성되어 있습니다. 정기적으로 랜딩 영역을 검색하고 새 파일을 수집하여 구성된 ExperienceEvent 데이터 세트에 기록합니다. 모니터링은 &quot;성공한 배치&quot;와 &quot;실패한 배치&quot;를 노출합니다. | 분, 데이터 흐름 예약 간격 |
| 데이터 레이크 및 실시간 고객 프로필에서 사용할 수 있는 데이터 | 배치가 수집되면 레코드는 데이터 레이크에 랜딩되고 (데이터 세트에 프로필이 활성화된 경우) 실시간 고객 프로필로 업데이트됩니다. 일괄 처리 수집 및 프로필 수집을 위한 표준 Experience Platform SLA가 적용됩니다. | 데이터 흐름과 동일한 실행 창 내, 즉 배치 실행이 완료된 직후. 일반적으로 다운스트림 서비스에 몇 분 안에 레코드를 사용할 수 있습니다. |

{style="table-layout:auto"}

## Experience Platform UI를 사용하여 Adobe Campaign Managed Cloud Services 소스 연결 만들기

이제 Campaign 클라이언트 콘솔에서 데이터 로그에 액세스하고 스키마 및 데이터 세트를 만들었으므로 소스 연결을 만들어 Campaign Managed Services 데이터를 Experience Platform으로 가져올 수 있습니다.

Campaign v8 게재 로그 및 추적 로그 데이터를 Experience Platform으로 가져오는 방법에 대한 자세한 지침은 [UI에서 Campaign Managed Services 소스 연결 만들기](../../tutorials/ui/create/adobe-applications/campaign.md)에 대한 안내서를 참조하십시오.

>[!IMPORTANT]
>
>최근에 제거된 이메일 수신자와 이메일의 상호 작용이 개인 정보를 Experience Platform으로 다시 수집할 수 있는 경계 사례가 있습니다. 경우에 따라 해당 사용자에게 마케팅을 다시 활성화할 수 있습니다.
>
>* 이 시나리오는 개인 정보 보호 요청이 Experience Platform에서 실행된 시간과 Adobe Campaign Classic에서 실행된 시간 사이에만 활성화됩니다. 요청이 Campaign에서 실행된 후 레코드가 Campaign으로 내보내지지 않는지 확인합니다. 이 문제를 해결하려면 실행 72시간 후 GDPR 요청을 다시 발행하십시오.
