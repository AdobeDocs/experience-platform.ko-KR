---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 인바운드 소스 데이터를 활성화하여 고객 프로필 채우기
topic: overview
translation-type: tm+mt
source-git-commit: d6d2faf3d5eabcd8e948d3717fd8f8df4b9cb85a

---


# 인바운드 소스 데이터를 활성화하여 고객 프로필 채우기

소스 커넥터의 인바운드 데이터를 사용하여 실시간 고객 프로필 데이터를 향상시키고 채울 수 있습니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [XDM(Experience Data Model) 시스템](../../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의](../../../xdm/schema/composition.md)기본 사항:스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
- [실시간 고객 프로필](../../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.

또한 이 자습서에서는 소스 커넥터를 만들고 구성해야 합니다.  UI에서 다른 커넥터를 만들기 위한 자습서 목록은 [소스 커넥터 개요에서](../../home.md)찾을 수 있습니다.

## 실시간 고객 프로필 데이터 채우기

고객 프로파일을 강화하려면 대상 데이터 세트의 소스 스키마가 실시간 고객 프로파일에서 사용할 수 있도록 호환되어야 합니다. 호환 스키마는 다음 요구 사항을 충족합니다.

- 스키마에는 ID 속성으로 지정된 속성이 하나 이상 있습니다.
- 스키마에는 기본 ID로 정의된 ID 속성이 있습니다.
- 기본 ID가 대상 속성인 데이터 흐름 내의 매핑이 있습니다.

소스 작업 영역에서 찾아보기 **탭을 클릭하여** 기본 연결을 나열합니다. 표시된 목록에서 프로파일을 채울 데이터 흐름 연결이 포함된 연결을 찾습니다. 연결 이름을 클릭하여 세부 정보에 액세스합니다.

![](../../images/tutorials/dataflow/cloud-storage/browse.png)

연결의 소스 *활동* 화면이 나타나 연결이 소스 데이터를 인제스트하는 데이터 세트를 표시합니다. 프로필에 대해 활성화할 데이터 세트 이름을 클릭합니다.

![](../../images/tutorials/dataflow/cloud-storage/dataset-dataflow.png)

데이터 *집합 활동* 화면이 나타납니다. 화면 *오른쪽의* 속성 열에는 데이터 세트에 대한 세부 사항이 표시되며, 프로필 **스위치와 데이터** 세트가 준수하는 스키마에 대한 링크가 포함됩니다. 스키마 이름을 클릭하여 해당 컴포지션을 봅니다.

![](../../images/tutorials/dataflow/cloud-storage/select-dataset-schema.png)

스키마 *편집기가* 나타나고 중앙 캔버스에 스키마 구조를 표시합니다. 캔버스 내에서 기본 ID로 설정할 필드를 선택합니다. 표시되는 *필드 속성* 탭에서 ID **확인란을** 선택한 다음 기본 **ID를**&#x200B;선택합니다. 마지막으로 적절한 ID **네임스페이스를**&#x200B;선택한 다음 적용을 **클릭합니다**.

![](../../images/tutorials/dataflow/cloud-storage/set-schema-identity.png)

스키마 구조의 최상위 객체를 클릭하면 스키마 *속성* 열이 나타납니다. 프로필 스위치를 전환하여 프로필에 대한 스키마를 **활성화합니다** . 저장을 **클릭하여** 변경 내용을 완료합니다.

![](../../images/tutorials/dataflow/cloud-storage/enable-profile.png)

이제 프로필이 활성화되어 있으므로 데이터 집합 *활동* 화면으로 돌아가서 속성 **열 내에서 프로필** 토글을 클릭하여 *데이터* 집합을활성화합니다.

![](../../images/tutorials/dataflow/cloud-storage/enable-dataset-profile.png)

프로필의 스키마와 데이터 세트를 모두 활성화하면 해당 데이터 세트에 인제스트된 데이터도 고객 프로필을 채웁니다.

>[!NOTE] 최근에 활성화된 데이터 집합 내의 기존 데이터는 프로필에 사용되지 않습니다.

## 다음 단계

이 튜토리얼을 따라 프로필 모형에 대한 인바운드 데이터를 활성화했습니다. 자세한 내용은 실시간 [고객 프로필 개요를](../../../profile/home.md)참조하십시오.