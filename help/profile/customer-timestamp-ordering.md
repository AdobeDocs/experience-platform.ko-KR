---
title: 고객 타임스탬프 순서 지정
description: 프로필 데이터의 일관성을 보장하기 위해 데이터 세트에 고객 타임스탬프 순서를 추가하는 방법을 알아봅니다.
badgePrivateBeta: label="비공개 베타" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: dffbdafc3f063906c8c8fb648ace59b2f1aedab8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# 고객 타임스탬프 순서 지정

Adobe Experience Platform에서는 프로필 스토어로 스트리밍을 통해 데이터를 수집할 때 기본적으로 데이터 순서가 보장되지 않습니다. 고객 타임스탬프 주문을 사용하면 제공된 고객 타임스탬프에 따라 최신 메시지가 프로필 스토어에 보존될 수 있습니다. 그러면 모든 오래된 메시지가 삭제되고 **아님** 세분화 및 대상과 같은 프로필 데이터를 사용하는 다운스트림 서비스에서 사용할 수 있습니다. 따라서 프로필 데이터가 일관되고 소스 시스템과 동기화된 상태를 유지할 수 있습니다.

고객 타임스탬프 순서를 활성화하려면 다음을 사용하십시오. `extSourceSystemAudit.lastUpdatedDate` 필드 내 [외부 소스 시스템 감사 속성 필드 그룹](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) 샌드박스 및 데이터 세트 정보를 참조하여 Adobe 기술 계정 관리자 또는 Adobe 고객 지원 센터에 문의하십시오.

## 제한

이 비공개 베타 기간 동안 고객 타임스탬프 순서를 사용할 때 다음 제한이 적용됩니다.

- 다음에서 고객 타임스탬프 정렬 기능만 사용할 수 있습니다. **프로필 속성** 수집 대상 **스트리밍 수집** 프로필 스토어에서.
   - 다음 항목이 있습니다. **아니요** 데이터 레이크 또는 ID 서비스의 데이터에 대해 제공되는 순서 지정 보증입니다.
- 다음에서 고객 타임스탬프 정렬 기능만 사용할 수 있습니다. **비프로덕션** 샌드박스.
- 고객 타임스탬프 순서 지정을 다음에 적용할 수만 있습니다. **5** 샌드박스당 데이터 세트.
- 본인 **할 수 없음** 스트리밍 업데이트를 사용하여 고객 타임스탬프 순서 지정이 활성화된 데이터 세트에서 부분 행 업데이트를 보냅니다.
- 다음 `extSourceSystemAudit.lastUpdatedDate` 필드 **필수** 다음에 있음 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 포맷. ISO 8601 형식을 사용하는 경우 **필수** 형식에서 전체 날짜/시간으로 사용 `yyyy-MM-ddTHH:mm:ss.sssZ` (예: `2028-11-13T15:06:49.001Z`).
- 수집된 데이터의 모든 행 **필수** 다음을 포함: `extSourceSystemAudit.lastUpdatedDate` 필드를 최상위 수준의 필드 그룹으로 지정합니다. 즉, 이 필드는 **필수** xdm 스키마 내에서 중첩될 수 없습니다. 이 필드가 누락되거나 형식이 잘못된 경우, 잘못된 형식의 레코드는 **아님** 수집되면 해당 오류 메시지가 전송됩니다.
- 고객 타임스탬프 주문에 대해 활성화된 모든 데이터 세트 **필수** 이전에 수집된 데이터가 없는 새 데이터 세트여야 합니다.
- 주어진 프로필 조각의 경우 최신 항목이 포함된 행만 `extSourceSystemAudit.lastUpdatedDate` 수집됩니다. 다음을 포함하는 행 `extSourceSystemAudit.lastUpdatedDate` 나이가 많거나 같은 연령은 무시됩니다.

## 추천 항목

고객 타임스탬프 주문을 구현할 때는 다음 고려 사항을 염두에 두십시오.

- 프로필 스토어로 데이터를 보내는 모든 내부 시스템의 시계를 동기화해야 합니다.
- ISO 8061 형식 타임스탬프에는 밀리초 수준의 정밀도가 있어야 합니다.
