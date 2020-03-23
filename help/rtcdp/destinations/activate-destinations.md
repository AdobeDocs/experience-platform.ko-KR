---
title: 대상에 프로필 및 세그먼트 활성화
seo-title: 대상에 프로필 및 세그먼트 활성화
description: 세그먼트를 대상에 매핑하여 Adobe 실시간 고객 데이터 플랫폼의 데이터를 활성화합니다. 이를 수행하려면 아래 단계를 따르십시오.
seo-description: 세그먼트를 대상에 매핑하여 Adobe 실시간 고객 데이터 플랫폼의 데이터를 활성화합니다. 이를 수행하려면 아래 단계를 따르십시오.
translation-type: tm+mt
source-git-commit: 73925aa59f9981d8945fb0be6c4924e1831cf902

---


# 대상에 프로필 및 세그먼트 활성화

세그먼트를 대상에 매핑하여 Adobe 실시간 고객 데이터 플랫폼의 데이터를 활성화합니다. 이를 수행하려면 아래 단계를 따르십시오.

## 전제 조건 {#prerequisites}

대상에 데이터를 활성화하려면 대상을 [연결했어야](/help/rtcdp/destinations/assets/connect-destination.png)합니다. 아직 설정하지 않은 경우 [대상 카탈로그로](/help/rtcdp/destinations/destinations-catalog.md)이동하여 지원되는 대상을 찾아 하나 이상의 대상을 설정합니다.

## 데이터 활성화 {#activate-data}

1. 대상 **>찾아보기에서**&#x200B;세그먼트를 활성화할 대상을 선택합니다.
2. 대상의 이름을 클릭합니다. 그러면 활성화 흐름이 표시됩니다.
   ![활성화](/help/rtcdp/destinations/assets/activate-flow.png)-흐름 대상에 대한 활성화 흐름이 이미 있는 경우 대상으로 현재 전송되는 세그먼트를 볼 수 있습니다. 오른쪽 **레일에서 [활성화** 편집]을 선택하고 아래 단계에 따라 활성화 세부 사항을 수정합니다.
3. 활성화를 **선택합니다**.
4. 대상 **활성화** 마법사의 세그먼트 **선택** 페이지에서 대상으로 전송할 세그먼트를 선택합니다.
   ![세그먼트 대 대상](/help/rtcdp/destinations/assets/select-segments.png)
5. *조건부*. 이 단계는 이메일 마케팅 대상에 매핑된 세그먼트에만 적용됩니다. <br> [ **대상 속성** ] 페이지에서 **[새 필드** 추가]를 선택하고 대상으로 전송할 속성을 선택합니다.
특성 중 하나를 조합 스키마에서 [고유 식별자로](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 지정하는 것이 좋습니다. 필수 속성에 대한 자세한 내용은 이메일 마케팅 [대상](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 아티클의 ID를 참조하십시오.
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. 예약 **페이지에서** 대상으로 데이터를 전송하는 시작 날짜와 대상으로 데이터를 보내는 빈도를 볼 수 있습니다.
7. 검토 **페이지에서** 선택 사항의 요약을 볼 수 있습니다. 취소를 **선택하여** 흐름을 **분류하고,** 뒤로를 선택하여 **설정을 수정하거나, 마침을** 선택하여선택을 확인하고 데이터를 대상으로 전송을 시작합니다.

![확인 선택](/help/rtcdp/destinations/assets/confirm-selection.png)

## 활성화 편집 {#edit-activation}

아래 절차에 따라 실시간 CDP에서 기존 활성화 흐름을 편집합니다.

1. 왼쪽 **탐색** 막대에서 대상을 선택한 다음 [찾아보기] **탭을 클릭하고** 대상 이름을 클릭합니다.
2. 오른쪽 레일에서 **[!UICONTROL Edit activation]** 선택하여 대상에 전송할 세그먼트를 변경합니다.

## 세그먼트 활성화 성공 여부 확인 {#verify-activation}

### 이메일 마케팅 대상 및 클라우드 스토리지 대상

이메일 마케팅 대상 및 클라우드 스토리지 대상의 경우 Adobe Real-time CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 파일이나 `.csv` 파일을 생성합니다. 매일 저장 위치에 새 파일이 만들어집니다. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

3일 연속으로 받은 파일은 다음과 같습니다.

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

스토리지 위치에 이러한 파일이 있는지 확인한 후 정품 인증을 완료했습니다.

### 광고 대상

데이터를 활성화할 각 광고 대상을 확인합니다. 정품 인증이 완료되면 광고 플랫폼에 대상이 채워집니다.

## 활성화 비활성화 {#disable-activation}

기존 활성화 흐름을 비활성화하려면 아래 단계를 따르십시오.

1. 왼쪽 **탐색** 막대에서 대상을 선택한 다음 [찾아보기] **탭을 클릭하고** 대상 이름을 클릭합니다.
2. 오른쪽 레일의 **[!UICONTROL Enabled]** 컨트롤을 클릭하여 활성화 흐름 상태를 변경합니다.
3. 데이터 **흐름 상태** 업데이트 창에서 확인을 선택하여 **활성화 흐름을** 비활성화합니다.

