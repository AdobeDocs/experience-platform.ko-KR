---
title: 설명서 셀프 서비스 템플릿 // 대상 이름으로 바꾸기
description: 이 템플릿을 사용하여 Adobe Experience Platform 카탈로그에서 대상에 대한 공개 설명서를 만듭니다. // 개요 섹션의 단락으로 대체합니다
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 396b9a9ec1509abedba96797f68ad3e5aa2e5988
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# 대상 {#your-destination}

*이 템플릿을 진행하면 모든 단락을 기울임꼴로 바꾸거나 삭제합니다(이 단락은 시작).*

*먼저 페이지 상단에서 메타데이터(제목 및 설명)를 업데이트합니다. 이 페이지에서 UICONTROL의 모든 인스턴스를 무시하십시오. 기계 번역 프로세스를 통해 페이지를 지원하는 여러 언어로 올바르게 변환하는 태그입니다. 문서를 제출한 후 문서에 태그를 추가합니다.*

## 개요 {#overview}

*고객에게 제공하는 가치를 비롯하여 귀사에 대한 간단한 개요를 제공합니다. 자세한 내용을 보려면 제품 설명서 홈 페이지에 대한 링크를 포함하십시오.*

>[!IMPORTANT]
>
>이 설명서 페이지는 *YOURDESTINATION* 팀이 만들었습니다. 문의 사항이나 업데이트 요청에 대해서는 *링크 또는 이메일 주소 삽입에서 직접 연락하여 업데이트*&#x200B;에 연결할 수 있습니다

## 전제 조건 {#prerequisites}

*Adobe Experience Platform 사용자 인터페이스에서 대상을 설정하기 전에 고객이 알아야 하는 모든 사항에 대한 정보를 이 섹션에 추가합니다. 다음 항목에 해당될 수 있습니다.*

* *허용 목록에 추가되어야 함*
* *이메일 해싱 요구 사항*
* *고객 측의 모든 계정 세부 사항*
* *플랫폼에 연결하기 위해 API 키를 가져오는 방법*

*고객에게 유용한 경우 관련 설명서에 연결할 수 있습니다.*

## 지원되는 ID {#supported-identities}

*대상이 지원하는 ID에 대한 정보를 이 섹션에 추가합니다. 몇 가지 표준 값으로 테이블을 미리 입력했습니다. 대상에 적용되지 않는 값과 미리 채워지지 않은 값을 삭제합니다.*

** 대상은 아래 표에 설명된 ID의 활성화를 지원합니다. [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스를 다음 별칭으로 참조할 수도 있습니다. &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 자세한 내용은 [ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html)에서 다음 문서를 참조하십시오. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스이면 이 타겟 ID를 선택합니다. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - YOURDESTINATIONdestination에 사용되는 식별자(이름, 전화번호 또는 기타)로 세그먼트(대상)의 모든 멤버를  ** 내보냅니다.

## 사용 사례

*YOURDESTINATION* 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례가 여기에 있습니다.

### 사용 사례 #1

*모바일 메시징 플랫폼의 경우:*

*주택 임대 및 판매 플랫폼에서는 고객의 Android 및 iOS 장치에 모바일 알림을 푸시하여 이전에 렌터링을 검색한 영역에 100개의 업데이트된 목록이 있음을 알려 줍니다.*

### 사용 사례 #2

*소셜 네트워크 플랫폼의 경우:*

*스포츠 의류 브랜드는 기존 고객에게 소셜 미디어 계정을 통해 연결되기를 원한다. 의류 브랜드는 자신의 CRM에서 Adobe Experience Platform으로 이메일 주소를 수집하고, 자체 오프라인 데이터에서 세그먼트를 작성하고, 이러한 세그먼트를 YOURDESTINATION로 보내 고객의 소셜 미디어 피드에 광고를 표시할 수 있습니다.*

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)

*새 대상을 구성할 때 고객이 입력해야 하는 필드를 추가합니다. 이러한 필드는 대상별로 다르며 대상 SDK의 구성에 따라 다릅니다. 대상 필드가 아래 나열된 필드와 같을 수 없습니다.*

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 대상  ** 계정 ID입니다.


<!--

*Replace YOURDESTINATION with your destination name and TOBEFILLEDIN with the category that your destination belongs to.*

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the ***TOBEFILLEDIN*** category. Select ***YOURDESTINATION***, then select **[!UICONTROL Configure]**.


    >[!NOTE]
    >
    >If a connection with this destination already exists, you can see an **[!UICONTROL Activate]** button on the destination card. For more information about the difference between **[!UICONTROL Activate]** and **[!UICONTROL Configure]**, refer to the [Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destinations-workspace.html#catalog) section of the destination workspace documentation.  

    ![Connect to YOURDESTINATION](./assets/yourdestination1.png)

2. In the **Account** step, if you had previously set up a connection to your *YOURDESTINATION* destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to *YOURDESTINATION*. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your *YOURDESTINATION* account.

    >[!NOTE]
    >
    >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your ***YOURDESTINATION*** account. This ensures that you don't complete the workflow with incorrect credentials.

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your ***YOURDESTINATION*** account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow and fill your account ID. <br> Also in this step, you can select any marketing action that should apply to this destination. Marketing actions indicate the intent for which data will be exported to the destination. You can select from Adobe-defined marketing actions or you can create your own marketing action. For more information about marketing actions, see the [Data usage policies overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html).

    ![Connect to YOURDESTINATION](./assets/yourdestination2.png)

5. Your destination is now created. You can select **[!UICONTROL Save & Exit]** if you want to activate segments later on or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

-->

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en)를 참조하십시오.

<!--

To activate segments to *YOURDESTINATION*, follow the steps below: 

1. In **[!UICONTROL Destinations > Browse]**, select the *YOURDESTINATION* destination where you want to activate your segments.

2. Click the name of the destination. This takes you to the Activate flow.
    ![activate-flow](./assets/yourdestination3.png)
    Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to *YOURDESTINATION*.
    ![segments-to-destination](./assets/activate-segments-google-customer-match.png)
5.  In the **[!UICONTROL Mapping]** step, select which attributes and identities from the source XDM schema to map to the target schema. Select **[!UICONTROL Add new mapping]** and browse your schema, select identity namespaces and map them to the corresponding target identity.  
![identity mapping initial screen](./assets/gcm-identity-mapping.png) <br>&nbsp;
   *Plain text email address as primary identity*: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below. Set up a mapping between any other attributes you plan to use.
   ![identity mapping step](./assets/ssd-template-identity.png) <br>&nbsp;
6. On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.
7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Adobe Experience Platform checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html#enforcement) in the data governance documentation section.
 
![confirm-selection](./assets/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](./assets/gcm-review.png)

-->

## 내보낸 데이터 {#exported-data}

*데이터를 대상에 내보내는 방법에 대한 메모를 추가합니다. 이렇게 하면 고객이 대상에 올바르게 통합되었는지 확인하는 데 도움이 됩니다. 예를 들어 아래 JSON과 같은 샘플 JSON을 제공할 수 있습니다.*

```
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)를 참조하십시오.

## 추가 리소스 {#additional-resources}

*제품 설명서 또는 고객이 성공하기 위해 중요하다고 생각하는 기타 리소스에 대한 추가 링크를 제공할 수 있습니다.*
