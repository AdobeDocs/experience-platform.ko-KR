---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: 지능형 서비스에서 사용할 데이터 준비
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 03135f564bd72fb60e41b02557cb9ca9ec11e6e8

---


# 지능형 서비스에서 사용할 데이터 준비

Intelligent Services가 마케팅 이벤트 데이터로부터 통찰력을 얻으려면, 데이터는 세밀하게 풍부해지고 표준 구조로 유지되어야 합니다. 지능형 서비스는 XDM(Experience Data Model) 스키마를 활용하여 이를 실현합니다. 특히, Intelligent Services에서 사용되는 모든 데이터 집합은 CEE( **Consumer ExperienceEvent)** XDM 스키마를 따라야 합니다.

이 문서에서는 여러 채널의 마케팅 이벤트 데이터를 이 스키마로 매핑하는 방법에 대한 일반적인 지침을 제공하며 스키마 내의 중요한 필드에 대한 정보를 요약하여 데이터를 해당 구조에 효과적으로 매핑하는 방법을 결정합니다.

## CEE 스키마 이해

Consumer ExperienceEvent 스키마는 디지털 마케팅 이벤트(웹 또는 모바일)뿐만 아니라 온라인 또는 오프라인 상거래 활동과 관련된 개인의 행동에 대해 설명합니다. 이 스키마는 의미적으로 잘 정의된 필드(열) 때문에 데이터를 덜 명확하게 하는 알 수 없는 이름을 피하여 Intelligent Services에 사용해야 합니다.

모든 XDM 스키마와 마찬가지로 CEE 믹스도 확장할 수 있습니다. 즉, CEE 믹스에 추가 필드를 추가할 수 있으며 필요한 경우 여러 스키마에 다른 변형을 포함할 수 있습니다.

믹싱의 전체 예는 [공용 XDM 저장소에서](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)찾을 수 있으며 아래 섹션에 설명된 키 필드에 대한 참조로 사용해야 합니다.

### 키 필드

아래 표는 CEE 믹스에서 활용해야 하는 주요 필드를 중점적으로 다루며, 지능형 서비스가 유용한 통찰력을 도출해내기 위해 설명 및 참조 설명서에 대한 링크 등을 제공합니다.

| XDM 필드 | 설명 | 참조 |
| --- | --- | --- |
| `xdm:channel` | ExperienceEvent와 관련된 마케팅 채널입니다. 이 필드에는 채널 유형, 미디어 유형 및 위치 유형에 대한 정보가 포함되어 있습니다. **속성 AI가 데이터와&#x200B;_연동되도록 하려면 이 필드를 제공해야_**&#x200B;합니다. 일부 예제 매핑은 아래 [](#example-channels) 표를 참조하십시오. | [경험 채널 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | 제품 SKU, 이름, 가격 및 수량을 포함하여 고객이 선택한 제품을 나타내는 항목 배열입니다. | [상거래 세부 정보 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | 구매 발주 번호 및 지불 정보를 포함하여 ExperienceEvent에 대한 상거래 관련 정보를 포함합니다. | [상거래 세부 정보 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | 상호 작용, 페이지 세부 사항 및 레퍼러 등 ExperienceEvent와 관련된 웹 세부 사항을 나타냅니다. | [ExperienceEvent 웹 세부 사항 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### 채널 예 {#example-channels}

이 `xdm:channel` 필드는 ExperienceEvent와 관련된 마케팅 채널을 나타냅니다. 다음 표에서는 XDM에 매핑되는 마케팅 채널의 몇 가지 예를 제공합니다.

| Channel | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| 유료 검색 | 유료 | 검색 | 클릭 |
| 소셜 - 마케팅 | 획득 | SOCIAL | 클릭 |
| 표시 | 유료 | 표시 | 클릭 |
| 이메일 | 유료 | 이메일 | 클릭 |
| 내부 레퍼러 | 소유 | DIRECT | 클릭 |
| ViewThrough 표시 | 유료 | 표시 | 노출 횟수 |
| QR 코드 리디렉션 | 소유 | DIRECT | 클릭 |
| SMS 문자 메시지 | 소유 | SMS | 클릭 |
| 모바일 | 소유 | 모바일 | 클릭 |

## 데이터 매핑 및 인제스트

마케팅 이벤트 데이터를 CEE 스키마에 매핑할 수 있는지 확인한 후 데이터를 Intelligent Services로 가져오는 프로세스를 시작할 수 있습니다. 데이터를 스키마에 매핑하고 서비스에 인제스트하는 데 도움이 필요하면 Adobe 컨설팅 서비스에 문의하십시오.

Adobe Experience Platform 구독을 보유하고 있고 직접 데이터를 매핑하고 인제스트하려면 아래 섹션에 설명된 단계를 따르십시오.

### Adobe Experience Platform 사용

>[!NOTE] 아래 단계에서는 Experience Platform을 구독해야 합니다. 플랫폼에 대한 액세스 권한이 없는 경우 [다음 단계](#next-steps) 섹션으로 건너뛸 수 있습니다.

이 섹션에서는 자세한 단계를 위한 자습서에 대한 링크를 포함하여 Intelligent Services에서 사용하기 위해 Experience Platform에 데이터를 매핑하고 인제스트하는 워크플로우에 대해 간략하게 설명합니다.

#### CEE 스키마 및 데이터 집합 만들기

데이터 통합 준비를 시작할 준비가 되면 첫 번째 단계는 CEE 믹싱을 사용하는 새 XDM 스키마를 만드는 것입니다. 다음 자습서에서는 UI 또는 API에서 새 스키마를 만드는 프로세스를 안내합니다.

* [UI에서 스키마 만들기](../xdm/tutorials/create-schema-ui.md)
* [API에서 스키마 만들기](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] 위의 자습서는 스키마를 만들기 위한 일반 작업 과정을 따릅니다. 스키마에 대한 클래스를 선택할 때는 XDM ExperienceEvent **클래스를**&#x200B;사용해야 합니다. 이 클래스가 선택되면 CEE 믹싱을 스키마에 추가할 수 있습니다.

CEE 믹스를 스키마에 추가한 후 데이터 내의 추가 필드에 대해 필요에 따라 다른 믹스를 추가할 수 있습니다.

스키마를 만들고 저장하면 해당 스키마를 기반으로 새 데이터 세트를 만들 수 있습니다. 다음 자습서에서는 UI 또는 API 파섹

* [UI에서 데이터 집합](../catalog/datasets/user-guide.md#create) 만들기(기존 스키마 사용 워크플로우에 따라)
* [API에서 데이터 세트 만들기](../catalog/datasets/create.md)

#### 데이터 매핑 및 인제스트

CEE 스키마 및 데이터 세트를 만든 후 데이터 테이블을 스키마로 매핑하고 해당 데이터를 플랫폼에 인제스트할 수 있습니다. UI에서 CSV 파일을 XDM 스키마에 [](../ingestion/tutorials/map-a-csv-file.md) 매핑하는 방법에 대한 자세한 내용은 자습서를 참조하십시오. 데이터 세트를 채운 후에는 동일한 데이터 세트를 사용하여 추가 데이터 파일을 인제스트할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서에서는 Intelligent Services에서 사용할 데이터를 준비하는 방법에 대한 일반적인 지침을 제공합니다. 사용 사례에 따라 추가 컨설팅을 필요로 하는 경우 Adobe 컨설팅 지원에 문의하십시오.

데이터 세트에 고객 경험 데이터를 성공적으로 채우면 지능형 서비스를 사용하여 인사이트를 생성할 수 있습니다. 시작하려면 다음 문서를 참조하십시오.

* [기여도 AI 개요](./attribution-ai/overview.md)
* [고객 AI 개요](./customer-ai/overview.md)
