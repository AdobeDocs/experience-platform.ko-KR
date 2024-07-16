---
title: 고객 타임스탬프 순서 지정
description: 프로필 데이터의 일관성을 보장하기 위해 데이터 세트에 고객 타임스탬프 순서를 추가하는 방법을 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 고객 타임스탬프 순서 지정

Adobe Experience Platform에서는 프로필 스토어로 스트리밍을 통해 데이터를 수집할 때 기본적으로 데이터 순서가 보장되지 않습니다. 고객 타임스탬프 주문을 사용하면 제공된 고객 타임스탬프에 따라 최신 메시지가 프로필 스토어에 보존될 수 있습니다. 그러면 모든 오래된 메시지가 삭제되고 세분화 및 대상과 같은 프로필 데이터를 사용하는 다운스트림 서비스에서 **사용할 수 없음**&#x200B;이 됩니다. 따라서 프로필 데이터가 일관되고 소스 시스템과 동기화된 상태를 유지할 수 있습니다.

고객 타임스탬프 순서를 활성화하려면 [외부 Source 시스템 감사 특성 필드 그룹](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) 내의 `extSourceSystemAudit.lastUpdatedDate` 필드를 사용하고 Adobe 기술 계정 관리자에게 문의하거나 샌드박스 및 데이터 세트 정보를 고객 지원 Adobe에 문의하십시오.

## 제한

이 비공개 베타 기간 동안 고객 타임스탬프 순서를 사용할 때 다음 제한이 적용됩니다.

- 프로필 스토어에서 **스트리밍 수집**&#x200B;과(와) 함께 수집된 **프로필 특성**&#x200B;의 고객 타임스탬프 순서만 사용할 수 있습니다.
   - 데이터 레이크 또는 ID 서비스의 데이터에 대해 **no** 순서 보증이 제공됩니다.
- **비프로덕션** 샌드박스에서만 고객 타임스탬프 순서를 사용할 수 있습니다.
- 고객 타임스탬프 순서 지정을 샌드박스당 **5** 데이터 세트에만 적용할 수 있습니다.
- **스트리밍 업데이트를 사용하여 고객 타임스탬프 순서를 사용하도록 설정한 데이터 집합에서 부분 행 업데이트를 보낼 수 없습니다**.
- `extSourceSystemAudit.lastUpdatedDate` 필드 **은(는) [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 형식이어야 합니다**. ISO 8601 형식을 사용하는 경우 **은(는) `yyyy-MM-ddTHH:mm:ss.sssZ` 형식의 전체 날짜/시간으로**&#x200B;해야 합니다(예: `2028-11-13T15:06:49.001Z`).
- **must**&#x200B;에 수집된 모든 데이터 행에 `extSourceSystemAudit.lastUpdatedDate` 필드가 최상위 필드 그룹으로 포함되어 있습니다. 즉, 이 필드 **must**&#x200B;은(는) XDM 스키마 내에 중첩되지 않습니다. 이 필드가 없거나 잘못된 형식인 경우 잘못된 형식의 레코드가 **수집되지**&#x200B;되며 해당 오류 메시지가 전송됩니다.
- 고객 타임스탬프 순서 **에 대해 활성화된 모든 데이터 집합은 이전에 수집된 데이터가 없는 새 데이터 집합이어야 합니다**.
- 지정된 프로필 조각의 경우 최신 `extSourceSystemAudit.lastUpdatedDate`이(가) 포함된 행만 수집됩니다. `extSourceSystemAudit.lastUpdatedDate`이(가) 더 오래되었거나 같은 연령의 행이 포함된 행은 무시됩니다.

## 권장 사항

고객 타임스탬프 주문을 구현할 때는 다음 고려 사항을 염두에 두십시오.

- 프로필 스토어로 데이터를 보내는 모든 내부 시스템의 시계를 동기화해야 합니다.
- ISO 8061 형식 타임스탬프에는 밀리초 수준의 정밀도가 있어야 합니다.
