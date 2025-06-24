---
title: Demandbase 의도
description: Experience Platform의 Demandbase Intent 소스에 대해 알아봅니다.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko#rtcdp-editions newtab=true"
badgeB2P: label="B2P 버전" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko#rtcdp-editions newtab=true"
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: 5757bc84a9aeec18eb5fe21d6f02160b2ba55166
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 1%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase]은(는) B2B 판매 및 마케팅 성공에 사용할 수 있는 계정 기반 마케팅 플랫폼입니다. [!DNL Demandbase Intent]은(는) [!DNL Demandbase] 계정을 Experience Platform에 연결하고 계정 의도 데이터를 통합하는 데 사용할 수 있는 Adobe Experience Platform 소스입니다.

[!DNL Demandbase] 원본을 사용하면 실시간 참여를 기반으로 관심 높은 계정을 식별할 수 있습니다. 가장 강력한 의도 신호의 우선 순위를 지정하여 정확한 세그먼트를 만들고 과대 타겟팅 캠페인을 제공할 수 있으므로 마케팅 노력이 전환 가능성이 가장 높은 계정에 집중할 수 있습니다. 인텐트 기반 전략을 활성화하면 광고 지출의 최적화, 참여 증가 및 ROI 향상을 실현할 수 있습니다.

[!DNL Demandbase] 원본에 대한 필수 구성 요소 정보는 이 문서를 참조하십시오.

## 전제 조건 {#prerequisites}

[!DNL Demandbase]을(를) Experience Platform에 연결하기 전에 필수 구성 요소 단계에 대해 다음 섹션을 읽어 보십시오.

### 허용 목록에 추가하다 IP 주소

소스 커넥터를 사용하기 전에 IP 주소 목록을 허용 목록에 추가하다에 추가해야 합니다. 영역별 IP 주소를 허용 목록에 추가하다에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 허용 목록에 추가하다 자세한 내용은 [IP 주소](../../ip-address-allow-list.md) 페이지를 참조하십시오.

### Experience Platform에 대한 권한 구성

[!DNL Demandbase] 계정을 Experience Platform에 연결하려면 계정에 대해 **[!UICONTROL 소스 보기]** 및 **[!UICONTROL 소스 관리]** 권한이 모두 활성화되어야 합니다. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/abac/ui/permissions.md)를 참조하십시오.

### 파일 및 디렉터리에 대한 이름 지정 제약 조건

아래 나열된 제한 사항은 클라우드 스토리지 파일 또는 디렉토리의 이름을 지정할 때 고려해야 합니다.

* 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
* 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공되면 자동으로 제거됩니다.
* 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
* `" \ / : | < > * ?` 문자는 사용할 수 없습니다.
* 잘못된 URL 경로 문자는 허용되지 않습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)을 참조하십시오.
* LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

### 필요한 자격 증명 수집

Experience Platform의 [!DNL Demandbase]은(는) [!DNL Google Cloud Storage]에 의해 호스팅됩니다. [!DNL Demandbase] 계정을 인증하려면 다음 자격 증명에 적절한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 액세스 키 ID | [!DNL Demandbase] 액세스 키 ID. Experience Platform 계정을 인증하는 데 필요한 61자의 영숫자 문자열입니다. |
| 비밀 액세스 키 | [!DNL Demandbase] 비밀 액세스 키입니다. Experience Platform 계정을 인증하는 데 필요한 40자의 Base64로 인코딩된 문자열입니다. |
| 버킷 이름 | 데이터를 가져올 [!DNL Demandbase] 버킷. |
| 폴더 경로 | 액세스 권한을 제공할 폴더의 경로입니다. |

이러한 자격 증명에 대한 자세한 내용은 [[!DNL Google Cloud Storage] HMAC 키 안내서](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)를 참조하십시오. 액세스 키를 생성하는 방법에 대한 단계는  [!DNL Google Cloud Storage] 소스 개요[&#128279;](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account)의 사전 요구 사항 안내서를 참조하십시오.

## [!DNL Demandbase] 스키마

[!DNL Demandbase] 스키마 및 데이터 구조에 대한 자세한 내용은 이 섹션을 참조하십시오.

[!DNL Demandbase] 스키마를 **Company Intent Weekly**&#x200B;라고 합니다. 지정된 계정 및 키워드에 대한 주간 의도 정보 (익명 B2B 구매자 연구 및 콘텐츠 소비)입니다. 데이터는 Parquet 형식입니다.

| 필드 이름 | 데이터 유형 | 필수 여부 | 비즈니스 키 | 참고 |
| --- | --- | --- | --- | --- |
| `company_id` | 문자열 | 참 | 예 | 정식 회사 ID입니다. |
| `domain` | 문자열 | 참 | 예 | 의도를 표시하는 계정의 식별된 도메인입니다. |
| `start_date` | 날짜 | 참 | 예 | 기간 중 의도 활동이 발생한 시작 날짜입니다. |
| `end_date` | 날짜 | 참 | 예 | 기간 중 의도 활동이 발생한 종료 날짜입니다. |
| `duration_type` | 문자열 | 참 | 예 | 기간 유형. 일반적으로 이 값은 선택한 롤업 기간에 따라 일별, 주별 또는 월별일 수 있습니다. 이 데이터 샘플의 경우 이 값은 `week`입니다. |
| `keyword_set_id` | 문자열 | 참 | 예 | 키워드 집합 ID입니다. 지정된 고객마다 고유합니다. |
| `keyword_set` | 문자열 | 참 | 예 | 키워드 집합 이름입니다. |
| `keyword` | 문자열 | 참 | | 의도 키워드. |
| `is_trending` | 문자열 | 참 | | 지정된 트렌드의 현재 상태입니다. 트렌드 상태는 이전 7주 동안의 평균과 비교하여 지난 주에 의도 활동의 버스트로 측정됩니다. |
| `intent_strength` | ENUM[STRING] | 참 | | 의도 강도에 대한 정량화된 측정입니다. 허용되는 값은 `HIGH`, `MED` 및 `LOW`입니다. |
| `num_people_researching` | 정수 | 참 | | 지난 7일 동안 키워드를 조사하는 `company_id`에 속한 사람의 수입니다. |
| `num_trending_days` | 정수 | 참 | | 지정된 기간 동안 키워드가 트렌드한 일 수입니다. |
| `trending_score` | 정수 | 참 | | 트렌드 점수. |
| `record_id` | 문자열 | 참 | | 고유한 기본 레코드 ID입니다. |
| `partition_date` | 날짜 | 참 | | 스냅샷의 캘린더 날짜입니다. 이 작업은 매주, 주말이 끝날 때 수행됩니다. |

{style="table-layout:auto"}

>[!TIP]
>
>스키마에 대한 모든 변경 사항은 사전에 Adobe에 전달됩니다. 원활한 스키마 개발을 지원하기 위해서는 이전 버전과의 호환성 유지가 필수적입니다. Experience Platform에서는 추가 전용 버전 관리 접근 방식을 적용하여 스키마에 대한 모든 업데이트가 비파괴되도록 합니다. 즉, 변경 사항을 엄격히 금지하고 기존 스키마를 강화하거나 확장하는 변경만 허용합니다.

## UI에서 [!DNL Demandbase] 계정을 Experience Platform에 연결

필수 구성 요소 설정을 완료했으면 [Experience Platform에  [!DNL Demandbase] 계정 연결](../../tutorials/ui/create/data-partners/demandbase.md)에 대한 자습서를 읽고 통합을 시작하십시오.

## 자주 묻는 질문 {#faq}

[!DNL Demandbase] 원본과 관련된 FAQ에 대한 답변을 보려면 이 섹션을 참조하십시오.

### Real-Time CDP B2B edition에서 해당 계정 의도 데이터를 사용하려면 [!DNL Demandbase]과(와) 기존 계약이 있어야 합니까?

+++답변

예. Experience Platform 및 Real-Time CDP B2B edition 내에서 의도 데이터에 액세스하고 활용하려면 [!DNL Demandbase]과(와) 활성 계약이 있어야 합니다. 통합은 [!DNL Demandbase]과의 기존 계약을 활용하여 Experience Platform 및 Real-Time CDP에서 계정 의도 신호를 수집하고 활성화합니다.

+++

### 이 통합에서 [!DNL Demandbase]의 사용자 지정 필드가 지원됩니까?

+++답변

현재 수집 및 활성화를 위해 표준 [!DNL Demandbase] 필드만 사용할 수 있습니다. 지원되는 필드 목록을 보려면 필드 가용성에 대한 자세한 내용은 [[!DNL Demandbase] 스키마 가이드](#schema)를 참조하십시오.

+++

### 임시로 [!DNL Demandbase]에서 Experience Platform으로 데이터를 수집할 수 있습니까?

+++답변

예, 임시로 [!DNL Demandbase]의 데이터를 수집할 수 있습니다. [!DNL Demandbase]의 새 데이터가 있는 한 새로운 데이터 흐름을 만들어 최신 의도 데이터를 수집할 수 있습니다. 그러나 활성 데이터 흐름은 한 번에 하나만 가질 수 있습니다. 따라서 새 데이터 흐름을 만들기 전에 기존 데이터 흐름을 삭제해야 합니다.

+++

### 의도 데이터에 대한 유효성 검사 프로세스는 무엇이며 특정 계정에 연결된 의도 데이터를 어떻게 확인할 수 있습니까?

+++답변

의도 데이터의 유효성을 검사하고 특정 계정에 연결된 의도 신호를 확인하려면 AccountID별로 [Adobe Experience Platform 쿼리 서비스](../../../query-service/home.md)를 사용하십시오.

+++

### 특정 회사에 대한 의도를 어떻게 찾을 수 있습니까?

+++답변

회사 이름 또는 AccountID를 사용하여 의도 데이터를 검색하려면 [Query Service](../../../query-service/home.md)에서 SQL 쿼리를 실행하십시오. 특정 회사에 대한 모든 의도 데이터를 보려면 회사 이름이나 AccountID를 사용하여 쿼리 서비스에서 SQL 쿼리를 실행하여 연관된 모든 의도 신호를 가져올 수 있습니다.

+++


### Experience Platform에서 계정 일치 프로세스에 문제가 있습니다. 어떻게 해야 합니까?

+++답변

해결 방법은 특정 문제에 따라 다릅니다.

* **Experience Platform에서 회사 도메인이 잘못되거나 누락되었습니다**: 계정 데이터의 회사 도메인 값이 잘못되어 문제가 발생한 경우 정확한 일치를 위해 Experience Platform에서 회사 도메인 필드를 업데이트하십시오.
* **데이터 흐름의 잘못된 필드 매핑**: 데이터 흐름의 잘못된 회사 도메인 필드 경로로 인해 문제가 발생한 경우, 올바른 필드 경로를 참조하도록 데이터 흐름 구성을 업데이트하십시오.

+++

### Experience Platform에서 의도 데이터를 삭제하려면 어떻게 해야 합니까?

+++답변

Experience Platform에서 의도 데이터를 삭제하려면 [데이터 세트를 삭제](../../../catalog/datasets/user-guide.md#delete-a-dataset)해야 합니다.

+++

### [!DNL Demandbase]에서 Experience Platform으로 계정을 일치시키는 데 사용되는 필드는 무엇입니까?

+++답변

`accountOrganization.domain` 필드는 일치하는 계정에 사용됩니다. 조직에서 다른 사용자 정의 필드를 사용하여 웹 사이트 이름을 저장하는 경우 정확한 매핑을 위해 올바른 필드 경로를 제공해야 합니다.

+++

### Experience Platform에서 회사 도메인을 업데이트하면 어떻게 됩니까?

+++답변

회사 도메인이 업데이트되면 다음 데이터 흐름 실행에 새 도메인 값이 적용됩니다. 이렇게 하면 다음과 같은 이점이 있습니다.

* 향후 의도 데이터 수집에서는 계정 일치를 위해 업데이트된 도메인을 사용합니다.
* 이전에 일치하지 않는 의도 신호는 이제 의도한 계정과 올바르게 정렬될 수 있습니다.
* 이전에 수집된 데이터 전용 새 데이터에 대해 소급 변경 작업을 수행하지 않으며 들어오는 데이터가 업데이트를 반영합니다.

+++

### 도메인 일치 프로세스란 무엇입니까?

+++답변

Experience Platform의 도메인 일치는 스크러빙된 도메인 필드 값의 정확한 일치를 기반으로 합니다. Experience Platform은 접두사(예: https:/<span>/www.)를 자동으로 제거하고 최상위 도메인(예: adobe.com)을 유지합니다. 일치에는 정확한 도메인 값이 필요하며 퍼지 일치 또는 하위 도메인은 지원되지 않습니다.

+++

### 의도 데이터는 어디에서 사용할 수 있습니까?

+++답변

의도 데이터는 [계정 대상](../../../segmentation/types/account-audiences.md)에서 사용하여 타깃팅, 세분화 및 개인화를 향상시킬 수 있습니다. 의도한 신호를 활용함으로써 기업은 특정 주제에 높은 관심을 보이는 계정을 식별하고 참여하여 마케팅 및 판매 활동을 최적화할 수 있습니다

+++
