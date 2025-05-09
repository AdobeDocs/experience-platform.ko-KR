---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;
title: 속성 기반 액세스 제어 개요
description: 이 문서에서는 Adobe Experience Platform의 속성 기반 액세스 제어에 대한 정보를 제공합니다
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 13%

---

# 속성 기반 액세스 제어 개요 {#attribute-based-access-control-overview}

속성 기반 액세스 제어는 관리자가 속성에 따라 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있도록 해 주는 Adobe Experience Platform의 기능입니다. 속성은 스키마 필드 또는 세그먼트에 추가된 레이블과 같이 객체에 추가된 메타데이터일 수 있습니다. 관리자는 사용자 액세스 권한을 관리하기 위해 속성이 포함된 액세스 정책을 정의합니다.

이 기능을 사용하여 XDM(경험 데이터 모델) 스키마 필드에 조직 또는 데이터 사용 범위를 정의하는 레이블로 레이블을 지정합니다. 이와 동시에 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드를 둘러싼 액세스 정책을 정의하고 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 또한 속성 기반 액세스 제어를 통해 관리자는 특정 세그먼트에 대한 액세스를 관리할 수 있습니다.

>[!IMPORTANT]
>
>속성 기반 액세스 제어를 Experience Platform의 데이터 거버넌스 기능과 혼동하지 마십시오. 데이터 거버넌스 기능을 사용하면 조직의 사용자가 데이터에 액세스할 수 있는 방식이 아니라 레이블과 정책을 사용하여 Experience Platform에서 데이터가 사용되는 방식을 제어할 수 있습니다. 자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 참조하십시오.

속성 기반 액세스 제어를 통해 조직 관리자는 모든 Experience Platform 워크플로 및 리소스에 걸쳐 중요한 개인 데이터(SPD), 개인 식별 정보(PII) 및 사용자 지정된 유형의 데이터에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 특정 필드에만 액세스할 수 있는 사용자 역할과 필드에 해당하는 데이터를 정의할 수 있습니다.

다음 비디오에서는 속성 기반 액세스 제어에 대한 이해를 돕기 위해 역할, 리소스 및 정책을 구성하는 방법에 대해 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3451845?learn=on&captions=kor)

## 속성 기반 액세스 제어 용어

속성 기반 액세스 제어에는 다음 구성 요소가 포함됩니다.

| 용어 | 정의 |
| --- | --- |
| 속성 | 속성은 사용자와 사용자가 액세스할 수 있는 Experience Platform 리소스 간의 상관 관계를 나타내는 식별자입니다. 속성은 스키마 필드 또는 세그먼트에 추가된 레이블과 같이 객체에 추가된 메타데이터일 수 있습니다. 관리자는 사용자 액세스 권한을 관리하기 위해 속성이 포함된 액세스 정책을 정의합니다. |
| 레이블 | 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트 및 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터를 제어하는 방법을 유연하게 선택할 수 있습니다. 우수 사례는 데이터가 Experience Platform에 수집되는 즉시 또는 데이터가 Experience Platform에서 사용할 수 있게 되는 즉시 데이터에 레이블을 지정하는 것을 권장합니다. |
| 권한 | 권한에는 샌드박스 생성, 스키마 정의 및 데이터 세트 관리와 같은 Experience Platform 기능을 보거나 사용할 수 있는 기능이 포함됩니다. |
| 사용 권한 집합 | 권한 집합은 관리자가 역할에 적용할 수 있는 권한 그룹을 나타냅니다. 관리자는 개별 권한을 할당하는 대신 역할에 권한 집합을 할당할 수 있습니다. 이를 통해 권한 그룹을 포함하는 사전 정의된 역할에서 사용자 정의 역할을 만들 수 있습니다. |
| 정책 | 정책은 속성을 함께 가져와서 허용되는 작업과 허용되지 않는 작업을 설정하는 문입니다. 정책은 로컬 또는 전역일 수 있으며 다른 정책을 무시할 수 있습니다. |
| 리소스 | 리소스는 주체가 액세스할 수 있거나 액세스할 수 없는 에셋 또는 개체입니다. 리소스는 세그먼트 또는 스키마 필드일 수 있습니다. |
| 역할 | 역할은 Experience Platform 인스턴스와 상호 작용하고 액세스 제어 정책을 구성하는 사용자 유형을 분류하는 방법입니다. 역할 기반 액세스 제어 환경에서 사용자 액세스 프로비저닝은 일반적인 책임과 요구 사항을 통해 그룹화됩니다. 역할에는 주어진 권한 집합이 있으며 조직의 멤버들은 필요한 보기 또는 쓰기 액세스 범위에 따라 하나 이상의 역할에 할당될 수 있습니다. |
| 주제 | 제목은 작업을 수행하기 위해 리소스에 대한 액세스를 요청하는 사용자입니다. |
| 사용자 그룹 | 사용자 그룹은 함께 그룹화된 여러 사용자이며 동일한 기능을 실행할 수 있는 액세스 권한을 갖습니다. |

## 권한

>[!IMPORTANT]
>
>조직이 속성 기반 액세스 제어에 대해 활성화되면 Adobe Experience Cloud의 역할 대신 Adobe Admin Console에 대한 권한을 사용하여 조직의 사용자, 기능, 레이블 및 기타 리소스에 대한 권한을 관리할 수 있습니다.

권한은 관리자가 사용자 역할 및 액세스 정책을 정의하여 제품 애플리케이션 내의 기능 및 개체에 대한 액세스 권한을 관리할 수 있는 Experience Cloud 영역입니다.

권한을 통해 역할을 만들고 관리하며, 이러한 역할에 대해 원하는 리소스 권한을 할당할 수 있습니다. 또한 권한을 사용하여 레이블, 샌드박스 및 특정 역할과 연관된 사용자를 관리할 수 있습니다. 자세한 내용은 [사용 권한 안내서](ui/browse.md)를 참조하세요.

## 속성 기반 액세스 제어 API

속성 기반 액세스 제어 API를 사용하면 API를 사용하여 Experience Platform 내에서 역할, 정책 및 제품을 프로그래밍 방식으로 관리할 수 있습니다. 자세한 내용은 [API를 사용하여 특성 기반 액세스 제어 구성 관리](api/overview.md)에 대한 안내서를 참조하십시오.

## Adobe Experience Platform의 속성 기반 액세스 제어

다음 섹션에서는 속성 기반 액세스 제어를 Experience Platform의 다른 구성 요소에 통합하는 방법에 대해 설명합니다.

### 액세스 제어

Experience Platform은 [Adobe Admin Console](https://adminconsole.adobe.com) 역할을 활용하여 사용 권한 및 샌드박스를 사용자와 연결합니다. 권한은 데이터 모델링, 프로필 관리 및 샌드박스 관리를 포함하여 다양한 Experience Platform 기능에 대한 액세스를 제어합니다. 조직이 속성 기반 액세스 제어에 대해 활성화되면 Adobe Experience Cloud의 역할 대신 Adobe Admin Console에 대한 권한을 사용하여 조직의 사용자, 기능, 레이블 및 기타 리소스에 대한 권한을 관리할 수 있습니다.

의료 및/또는 Privacy Shields를 구입하는 고객의 속성 기반 액세스 제어 기능은 제한적입니다. 이 기능의 특징은 다음과 같습니다.

* 권한 인터페이스: 속성 기반 액세스 제어에 대한 사용자 역할, 권한 및 정책을 정의할 수 있는 인터페이스를 제공합니다.

* 레이블 지정: 액세스 제어 정책을 활용하기 위해 사용자 역할, 스키마 필드, 세그먼트 및 기타 지원되는 객체에 레이블을 추가, 편집 및 제거합니다. **참고:** 동일한 액세스 제한을 적용하려면 레이블이 지정된 특성을 사용하는 세그먼트에도 마찬가지로 레이블이 지정되어야 합니다.

Admin Console에서 새 권한 인터페이스로 모든 Experience Platform 기반 응용 프로그램에 대한 관리 워크플로가 전환됩니다.

>[!IMPORTANT]
>
>조직이 활성화되면 역할이 자동으로 권한 인터페이스로 마이그레이션됩니다. Admin Console의 역할은 당분간 그대로 유지됩니다. 조직이 활성화된 후에는 **역할을 수정하지 마십시오**.

액세스 제어에 대한 자세한 내용은 [액세스 제어 개요](../home.md)를 참조하십시오.

### 대상 {#destinations}

[!DNL Destinations]은(는) Experience Platform의 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

관리자는 속성 기반 액세스 제어 기능을 사용하여 다음을 수행할 수 있습니다.

* 역할, 권한 및 레이블을 기반으로 활성화 프로세스의 특정 세그먼트를 보기 위한 사용자 액세스를 구성합니다.
   * 활성화 프로세스에서, 사용자는 대상에 대해 활성화하고자 하는 세그먼트를 선택해야 할 수 있습니다. 관리자는 사용자가 액세스할 수 있는 레이블로 레이블이 지정된 세그먼트와 레이블이 포함되지 않은 세그먼트만 표시하도록 조직의 사용자를 규정할 수 있습니다.
* 역할, 권한 및 레이블을 기반으로 활성화 프로세스의 특정 필드를 보기 위한 사용자 액세스를 구성합니다.
   * 활성화 프로세스에서, 사용자는 대상에 대해 활성화하고자 하는 필드를 선택해야 할 수 있습니다. 관리자는 사용자가 액세스할 수 있는 레이블로 레이블이 지정된 필드와 레이블이 포함되지 않은 필드만 표시하도록 조직의 사용자를 규정할 수 있습니다.

>[!IMPORTANT]
>
>요약하면 대상 및 속성 기반 액세스 제어 작업 시 다음과 같은 의미에 유의하십시오.
>
>* 활성화 워크플로의 [대상 포털](/help/segmentation/ui/audience-portal.md#browse) 및 [세그먼트 단계 선택](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments)에서 액세스 및 볼 수 있는 권한이 있는 대상만 활성화할 수 있습니다.
>* 활성화 워크플로의 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)에서는 액세스 권한이 있는 활성화 필드만 보고 선택할 수 있습니다.
>* 내보내기 위해 매핑된 모든 필드에 대한 액세스 권한이 없는 기존 대상에 대해 추가 세그먼트를 활성화하려고 하면 활성화 워크플로가 차단됩니다.

[!DNL Destinations]에 대한 자세한 내용은 [[!DNL Destinations] 개요](../../destinations/home.md)를 참조하세요.

### ID 서비스

Adobe Experience Platform [!DNL Identity Service]을(를) 사용하면 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 더 나은 보기를 얻을 수 있으므로 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

특성 기반 액세스 제어의 일부로 `view-identity-graph` 권한을 사용하면 사용자 인터페이스 또는 API를 통해 ID 그래프에 액세스할 수 있는 조직의 사용자를 결정할 수 있습니다. 자세한 내용은 [ID 그래프 뷰어 사용](../../identity-service/features/identity-graph-viewer.md)에 대한 안내서를 참조하십시오.

[!DNL Identity Service]에 대한 자세한 내용은 [[!DNL Identity Service] 개요](../../identity-service/home.md)를 참조하세요.

### 실시간 고객 프로필

Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소나 시기에 상관없이 고객이 통합적이고 일관적이며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 서로 다른 고객 데이터를 하나의 통합 보기로 통합하여 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공할 수 있습니다.

관리자는 속성 기반 액세스 제어 기능을 사용하여 다음을 수행할 수 있습니다.

* 역할, 권한 및 레이블을 기반으로 특정 프로필 속성에 대한 사용자 액세스를 구성합니다.
   * 관리자는 사용자가 액세스할 수 있는 레이블로 레이블 지정된 프로필 속성과 레이블을 포함하지 않는 프로필 속성만 표시하도록 조직의 사용자를 규정할 수 있습니다.
   * 관리자는 세그먼트를 만들 때 사용자가 액세스할 수 있는 레이블로 레이블이 지정된 프로필 속성만 표시하도록 조직의 사용자를 규정할 수 있습니다.
* 데이터 모델의 XDM 스키마에 사용되는 특정 데이터 필드에 레이블을 지정하여 데이터 미리보기에 대한 사용자 액세스를 구성합니다.

프로필에 대한 자세한 내용은 [프로필 개요](../../profile/home.md)를 참조하세요.

### Segmentation Service

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

관리자는 속성 기반 액세스 제어 기능을 사용하여 다음을 수행할 수 있습니다.

* 역할, 권한 및 레이블을 기반으로 특정 세그먼트를 보고 관리할 수 있도록 사용자 액세스를 구성합니다.
   * 관리자는 세그먼테이션 UI를 사용할 때 조직의 사용자에게 사용자가 액세스할 수 있는 레이블로 레이블 지정된 세그먼트와 레이블을 포함하지 않는 세그먼트만 표시하도록 프로비저닝할 수 있습니다.

[!DNL Segmentation Service]에 대한 자세한 내용은 [[!DNL Segmentation Service] 개요](../../segmentation/home.md)를 참조하세요.

### XDM

XDM(경험 데이터 모델)은 디지털 경험의 성능을 개선하기 위해 설계된 오픈 소스 사양입니다. Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

속성 기반 액세스 제어를 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* [필드 그룹 및 클래스에 데이터 사용 레이블 적용](../../xdm/tutorials/labels.md). 이렇게 하면 필드 그룹 또는 클래스 수준의 구성에 따라 필드 그룹 또는 클래스가 동일한 여러 스키마에 동일한 속성으로 태그가 지정된 필드가 있습니다.
* 사용자에게 할당된 역할에 적용되는 권한 집합에 따라 특정 XDM 스키마 필드에 대한 사용자 액세스를 구성합니다.

XDM에 대한 자세한 내용은 [XDM 개요](../../xdm/home.md)를 참조하세요.