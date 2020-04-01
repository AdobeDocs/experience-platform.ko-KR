---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 대상 세그먼트 내보내기를 위한 데이터 세트 만들기
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# 대상 세그먼트 내보내기를 위한 데이터 세트 만들기

Adobe Experience Platform을 사용하면 고객 프로파일을 특정 속성에 따라 손쉽게 고객으로 세분화할 수 있습니다. 세그먼트가 만들어지면 해당 대상을 액세스 및 작동 가능한 데이터 세트로 내보낼 수 있습니다. 내보내기가 성공하려면 데이터 세트를 제대로 구성해야 합니다.

이 자습서에서는 경험 플랫폼 UI를 사용하여 대상 세그먼트를 내보내는 데 사용할 수 있는 데이터 세트를 만드는 데 필요한 단계를 안내합니다.

이 자습서는 세그먼트 결과를 [평가하고](./evaluate-a-segment.md)액세스하기 위해 튜토리얼에 설명된 단계와 직접 관련이 있습니다. 세그먼트 평가 자습서에서는 Catalog API를 사용하여 데이터 세트를 만드는 단계를 제공하는 반면 이 자습서에서는 Experience Platform UI를 사용하여 데이터 세트를 만드는 단계를 간략하게 설명합니다.

## 시작하기

세그먼트를 내보내려면 데이터 집합이 XDM 개별 프로필 조합 스키마를 기반으로 해야 합니다. 공용 스키마는 XDM 개별 프로필 클래스인 동일한 클래스를 공유하는 모든 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 결합 보기 스키마에 대한 자세한 내용은 스키마 레지스트리 [개발자 안내서의](../../xdm/schema/composition.md#union)실시간 고객 프로필 섹션을 참조하십시오.

UI에서 결합 스키마를 보려면 왼쪽 **탐색에서** 프로필을 클릭한 다음 *아래 표시된 조합 스키마* 탭을 클릭합니다.

![Experience Platform UI 파섹](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## 데이터 집합 작업 영역

Experience Platform UI의 데이터 집합 작업 영역을 사용하면 IMS 조직이 만든 모든 데이터 집합을 보고 관리하고 새 데이터 집합을 만들 수 있습니다.

데이터 집합 작업 영역을 보려면 왼쪽 **탐색에서 데이터** 집합을 클릭한 다음 검색 *탭을 클릭합니다* . 데이터 집합에는 *이름*, 만들어진 *날짜 및* 시간, 생성된 *열,*&#x200B;소스 *열,*****&#x200B;스키마, 배치 작업 영역, 마지막 배치 상태 등을 표시하는 데이터 집합 목록이 포함되어 있습니다. 또한 데이터 집합은 마지막 업데이트일 날짜 및 시간이 마지막 업데이트일 날짜 및 시간만큼 표시됩니다. 각 열의 너비에 따라 왼쪽이나 오른쪽으로 스크롤하여 모든 열을 볼 수 있습니다.

>[!NOTE] 검색 막대 옆에 있는 필터 아이콘을 클릭하여 필터링 기능을 사용하여 실시간 고객 프로파일에 대해 활성화된 데이터 세트만 표시합니다.

![모든 데이터 집합 보기](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## 데이터 세트 만들기

데이터 세트를 만들려면 데이터 집합 **작업 영역의 오른쪽** 맨 위에 있는 데이터 집합 만들기를 클릭합니다.

![데이터 세트 만들기를 클릭합니다.](../images/tutorials/segment-export-dataset/dataset-click-create.png)

데이터 집합 *만들기* 화면에서 스키마에서 **데이터 집합 만들기를** 클릭하여 계속합니다.

![데이터 소스 선택](../images/tutorials/segment-export-dataset/create-dataset.png)

## XDM 개별 프로필 결합 스키마 선택

데이터 세트에 사용할 XDM 개별 프로필 조합 스키마를 선택하려면 [스키마 선택] 화면에서 &quot;Union&quot; 유형의 &quot;XDM 개별 프로필&quot; 스키마를 *찾습니다* .

XDM 개별 프로필 옆에 **있는 라디오**&#x200B;단추를 선택한 다음 **오른쪽** 위 모서리에서 다음을클릭합니다.

![스키마 선택](../images/tutorials/segment-export-dataset/select-schema.png)

## 데이터 세트 구성

데이터 **세트 구성** 화면에서 데이터 세트에 이름을 지정해야 *하며* 데이터 세트에 대한 *설명도* 제공할 수 있습니다.

**데이터 집합 이름에 대한 참고 사항:**
- 데이터 세트 이름은 짧고 설명적이어야 나중에 라이브러리에서 데이터 세트를 쉽게 찾을 수 있습니다.
- 데이터 집합 이름은 고유해야 합니다. 즉, 나중에 다시 사용할 수 없도록 지정해야 합니다.
- 설명 필드를 사용하여 데이터 세트에 대한 추가 정보를 제공하는 것이 좋습니다. 다른 사용자가 차후에 데이터 세트를 구별할 수 있도록 도울 수 있습니다.

데이터 세트에 이름과 설명이 있으면 마침을 **클릭합니다**.

![데이터 세트 구성](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 데이터 집합 활동

이제 빈 데이터 집합이 생성되었으며 데이터 집합 작업 *영역의 데이터* 집합 활동 탭으로 돌아갑니다. 작업 영역의 왼쪽 위 모서리에 &quot;추가된 배치가 없습니다.&quot;라는 알림과 함께 데이터 세트 이름이 표시됩니다. 이 데이터 세트에 아직 배치를 추가하지 않았으므로 이 작업이 필요합니다.

데이터 세트의 오른쪽에는 **데이터 세트 ID와 같은** 새 데이터 세트 ID *와*&#x200B;관련된 정보 *탭 정보가*&#x200B;표시됩니다. *데이터 세트 ID, 데이터 세트 이름*, 설명 *CNAME*, CNAME, CNAME, CNAME ******, Schema Streaming Streaming SourceHandSource가 들어 있습니다. 또한 정보 탭에는 데이터 세트를 만든 시기 *및* 마지막 수정 *날짜에 대한 정보도 포함되어* 있습니다.

대상 세그먼트 내보내기 **작업 과정을**&#x200B;완료하려면 이 값이 필요하므로 데이터 집합 ID를 참고하십시오.

![데이터 집합 활동](../images/tutorials/segment-export-dataset/dataset-activity.png)

## 다음 단계

이제 XDM 개별 프로필 조합 스키마를 기반으로 데이터 세트를 만들었으므로 데이터 집합 ID를 **사용하여** 세그먼트 결과 [](./evaluate-a-segment.md) 평가 및 액세스 자습서를 계속할 수 있습니다.

현재 세그먼트 결과 평가 자습서로 돌아가서 세그먼트 [내보내기 워크플로우의 대상](./evaluate-a-segment.md#generate-profiles-for-audience-members) 구성원을 [](./evaluate-a-segment.md#export-a-segment) 위해 XDM 개별 프로필 생성 단계를 선택하십시오.
