---
title: mTLS(상호 전송 계층 보안) 개요
description: mTLS를 사용하여 이벤트 전달을 위해 Adobe에서 발급한 공개 인증서를 안전하게 검색하는 방법에 대해 알아봅니다.
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: ab16cc3f70ec54460c7c4834e665c828d75d4d9e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# 상호 전송 계층 보안([!DNL mTLS]) 개요

[!UICONTROL 환경 UI]에서 상호 전송 계층 보안([!DNL mTLS]) 인증서를 바인딩하여 확장의 보안을 제어하십시오. [!DNL mTLS] 인증서는 보안 통신에서 서버 또는 클라이언트의 ID를 증명하는 디지털 자격 증명입니다. [!DNL mTLS] 서비스 API를 사용하는 경우 이러한 인증서를 통해 Adobe Experience Platform 이벤트 전달과의 상호 작용을 확인하고 암호화할 수 있습니다. 이 프로세스는 데이터를 보호할 뿐만 아니라 모든 연결이 신뢰할 수 있는 파트너로부터 연결되는지 확인합니다.

## 새 환경에서 [!DNL mTLS] 구현 {#implement-mtls}

라이브러리 빌드가 에지 네트워크에 올바르게 배포되도록 이벤트 전달 환경을 설정합니다. 설치하는 동안 배포 요구 사항에 가장 적합한 호스팅 옵션을 선택할 수 있습니다. 보안 통신을 위해 [!DNL mTLS] 인증서도 새 환경에 자동으로 추가됩니다.

새 환경을 만들려면 이벤트 전달 속성의 왼쪽 패널에서 **[!UICONTROL 환경]** 탭을 선택한 다음 **[!UICONTROL 환경 추가]**&#x200B;를 선택합니다.

![기존 환경을 표시하는 이벤트 전달 속성으로, [!UICONTROL 환경 추가]를 강조 표시합니다.](../../../images/extensions/server/cloud-connector/add-environment.png)

다음 페이지에서 이 설정에 사용할 환경을 선택합니다. 세 가지 환경을 사용할 수 있습니다.

>[!NOTE]
>
>속성은 하나의 개발, 하나의 스테이징 및 하나의 프로덕션 환경으로 제한됩니다.

| 환경 | 설명 |
| --- | --- |
| 개발 | 개발 환경은 팀 구성원이 이벤트 전달의 라이브러리 또는 변경 사항을 테스트하기 위한 것입니다. |
| 스테이징 | 스테이징 환경은 선택 사항이며 승인된 팀 구성원이 라이브러리를 게시하기 전에 테스트하고 승인할 수 있습니다. |
| 프로덕션 | 프로덕션 환경은 라이브 프로덕션 데이터에 사용됩니다. |

![환경 선택 화면에서 [!UICONTROL 개발을 위해 ]을(를) 강조 표시합니다.](../../../images/extensions/server/cloud-connector/select-environment.png)

**[!UICONTROL 환경 만들기]** 페이지에서 **[!UICONTROL 이름]**&#x200B;을 입력하고 **[!UICONTROL 호스트 선택]** 드롭다운 메뉴에서 ***Adobe 관리***&#x200B;를 선택합니다. **[!UICONTROL 인증서]**&#x200B;이(가) ***자동으로 추가됨***&#x200B;입니다. 마지막으로 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![개발 환경 만들기 페이지에서 [!UICONTROL 이름], [!UICONTROL 호스트 선택] 및 [!UICONTROL 저장]을 강조 표시합니다.](../../../images/extensions/server/cloud-connector/create-environment.png)

환경이 만들어지고 새 환경을 표시하는 **[!UICONTROL 환경]** 탭으로 돌아갑니다.

![개발 환경을 강조 표시하는 [!UICONTROL 환경] 탭](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## 환경 인증서 세부 정보 보기 {#view-certificate}

환경에 대한 인증서 세부 정보를 보려면 이벤트 전달 속성의 왼쪽 패널에서 **[!UICONTROL 환경]** 탭을 선택한 다음 세부 정보를 볼 환경을 선택합니다.

다음 인증서 세부 정보가 표시됩니다.

| 필드 이름 | 설명 |
| --- | --- |
| 인증서 | 다음을 포함한 인증서 세부 정보:<ul><li>**이름**: 인증서의 이름입니다.</li><li>**만든 날짜**: 인증서가 만들어진 날짜입니다.</li><li>**상태**: 인증서의 현재 상태:<ul><li>**현재**: 인증서가 현재 사용 중입니다.</li><li>**사용되지 않음**: 인증서가 사용 중이지 아직 만료되지 않았습니다. 계속 사용하도록 선택할 수 있습니다.</li><li>**만료됨**: 인증서가 만료되었으며 회색으로 표시되어 더 이상 사용할 수 없습니다.</li></ul></ul> |
| 만료 | 인증서 만료 날짜. |
| Variable Name | 인증서의 변수 이름입니다. |
| 상태 | 인증서의 현재 상태:<ul><li>**배포됨**: 인증서가 배포되었으며 활성 상태입니다.</li><li>**배포**: 인증서를 배포하는 중입니다.</li><li>**배포가 필요합니다**: 이 상태는 사용되지 않는 인증서를 선택할 때 나타납니다.</li></ul> |

![개발 환경 편집 페이지에서 [!UICONTROL 인증서] 세부 정보를 강조 표시합니다.](../../../images/extensions/server/cloud-connector/certificate-details.png)

### 오래된 인증서 선택 및 배포 {#deploy-obsolete-certificate}

오래된 인증서를 사용하려면 이벤트 전달 속성의 왼쪽 패널에서 **[!UICONTROL 환경]** 탭으로 이동한 다음 환경을 선택하여 세부 정보를 확인합니다.

![개발 환경을 강조 표시하는 [!UICONTROL 환경] 탭](../../../images/extensions/server/cloud-connector/new-environment-created.png)

**[!UICONTROL 인증서]** 드롭다운에서 오래된 인증서를 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![오래된 인증서와 저장 이 강조 표시된 [!UICONTROL 인증서] 드롭다운을 강조 표시하는 개발 환경 편집 페이지입니다.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

인증서를 배포하려면 **[!UICONTROL 인증서 배포]** 대화 상자에서 **[!UICONTROL 저장 및 배포]**&#x200B;를 선택하십시오.

![저장 및 배포가 강조 표시된 인증서 배포 대화 상자.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## 다음 단계 {#next-steps}

이 문서에서는 이벤트 전달 속성에 대한 환경을 만들고, 인증서를 추가하고, 오래된 인증서를 사용하는 방법을 보여 줍니다. [!DNL mTLS] 인증서에 대한 자세한 내용은 [[!DNL mTLS] 서비스 API 개요](../../../../data-governance/mtls-api/overview.md)를 참조하십시오.

이벤트 전달 규칙에서 [!DNL mTLS] 인증서를 사용하는 방법에 대해 알아보려면 [Cloud Connector 확장 개요](../cloud-connector/overview.md/#mtls-rules)를 참조하세요.
