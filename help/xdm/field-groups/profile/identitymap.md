---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;identityMap;ID 맵;ID 맵;스키마 디자인;맵;맵;유니온 스키마;유니온
title: IdentityMap 스키마 필드 그룹
description: XDM 개별 프로필 클래스에 대해 알아봅니다.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 대한 문서를 참조하십시오.

[!UICONTROL IdentityMap]은(는) [[!UICONTROL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md)의 표준 스키마 필드 그룹이며 [[!UICONTROL XDM 개별 프로필] 클래스](../../classes/individual-profile.md)의 호환 필드 그룹입니다. 필드 그룹은 네임스페이스로 입력된 사용자 ID 세트가 포함된 단일 맵 필드를 제공합니다.

![[!UICONTROL IdentityMap] 스키마 필드 그룹의 다이어그램](../../images/field-groups/identitymap.png)

사용 사례의 이점 및 단점 등 자세한 내용은 [스키마 컴포지션 기본 사항](../../schema/composition.md#identityMap)의 ID 맵 섹션을 참조하십시오.

**예**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소의 [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json)을(를) 참조하십시오.
