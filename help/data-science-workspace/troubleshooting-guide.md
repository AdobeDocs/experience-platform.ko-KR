---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: 데이터 과학 작업 공간 문제 해결 가이드
topic: Troubleshooting
description: 이 문서에서는 Adobe Experience Platform 데이터 과학 작업 공간에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
translation-type: tm+mt
source-git-commit: 76e598c743df320e4b3cb821e118749fe7304d9c
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 문제 해결 안내서

이 문서는 Adobe Experience Platform에 대한 FAQ에 대한 답변을 제공합니다 [!DNL Data Science Workspace]. 일반적으로 API에 대한 질문 및 문제 해결 [!DNL Platform] 은 [Adobe Experience Platform API 문제 해결 가이드를 참조하십시오](../landing/troubleshooting.md).

## [!DNL JupyterLab] 환경이 [!DNL Google Chrome]

>[!IMPORTANT]
>
>이 문제는 해결되었지만 Google Chrome 80.x 브라우저에 여전히 존재할 수 있습니다. 크롬 브라우저가 최신 버전인지 확인하십시오.

브라우저 [!DNL Google Chrome] 버전 80.x에서는 기본적으로 모든 타사 쿠키가 차단됩니다. 이 정책은 Adobe Experience Platform 내 [!DNL JupyterLab] 에서 로드되지 않을 수 있다.

이 문제를 해결하려면 다음 단계를 수행하십시오.

브라우저에서 오른쪽 [!DNL Chrome] 상단으로 이동하고 설정 **을 선택합니다** . 또는 주소 표시줄에 &quot;chrome://settings/&quot;을 복사하여 붙여넣을 수 있습니다. 그런 다음 페이지 아래쪽으로 스크롤하고 **고급** 드롭다운을 클릭합니다.

![chrome](./images/faq/chrome-advanced.png)

개인 *정보 및 보안* 섹션이 나타납니다. 그런 다음 **사이트 설정을** 클릭한 다음 **쿠키 및 사이트 데이터를 클릭합니다**.

![chrome](./images/faq/privacy-security.png)

![chrome](./images/faq/cookies.png)

마지막으로 &quot;타사 쿠키 차단&quot;을 &quot;해제&quot;로 전환합니다.

![chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>또는 타사 쿠키를 비활성화하고 [* 추가할 수도 있습니다.]ds.adobe.net을 허용 목록에 연결합니다.

주소 표시줄의 &quot;chrome://flags/&quot;으로 이동합니다. 오른쪽의 드롭다운 메뉴를 사용하여 *&quot;기본 쿠키로* SameSite&quot;라는 플래그를 검색하고 비활성화합니다.

![샘플 플래그 사용 안 함](./images/faq/samesite-flag.png)

2단계 후 브라우저를 다시 실행하라는 메시지가 표시됩니다. 다시 실행한 후 액세스할 수 [!DNL Jupyterlab] 있어야 합니다.

## Safari [!DNL JupyterLab] 에서 액세스할 수 없는 이유는 무엇입니까?

Safari는 Safari &lt; 12에서 기본적으로 타사 쿠키를 비활성화합니다. 가상 컴퓨터 인스턴스가 부모 프레임과 다른 도메인에 있으므로 현재 Adobe Experience Platform에서는 타사 쿠키를 활성화해야 합니다. [!DNL Jupyter] 타사 쿠키를 활성화하거나 같은 다른 브라우저로 전환하십시오 [!DNL Google Chrome].

Safari 12의 경우 사용자 에이전트를 &#39;[!DNL Chrome]&#39; 또는 &#39;[!DNL Firefox]&#39;로 전환해야 합니다. 사용자 에이전트를 전환하려면 먼저 *Safari* 메뉴를 열고 기본 설정을 **선택합니다**. 기본 설정 창이 나타납니다.

![Safari 환경 설정](./images/faq/preferences.png)

Safari 환경 설정 창에서 **고급을 선택합니다**. 그런 다음 메뉴 모음 *에 현상 표시 메뉴를* 선택합니다. 이 단계가 완료된 후 기본 설정 창을 닫을 수 있습니다.

![Safari 고급](./images/faq/advanced.png)

그런 다음 위쪽 탐색 모음에서 현상 **메뉴를** 선택합니다. 현상 드롭다운 *에서* 사용자 에이전트 *위로*&#x200B;마우스를 가져갑니다. 사용할 사용자 에이전트 **[!DNL Chrome]** 또는 **[!DNL Firefox]** 사용자 에이전트 문자열을 선택할 수 있습니다.

![현상 메뉴](./images/faq/user-agent.png)

## 파일을 업로드하거나 삭제할 때 &#39;403 금지&#39; 메시지가 표시되는 이유는 무엇입니까 [!DNL JupyterLab]?

브라우저가 [!DNL Ghostery] 또는 [!DNL AdBlock] Plus와 같은 광고 차단 소프트웨어로 활성화되면 각 광고 차단 소프트웨어에서 &quot;\*.adobe.net&quot; 도메인이 정상적으로 작동되도록 허용되어야 [!DNL JupyterLab] 합니다. 이것은 [!DNL JupyterLab] 가상 컴퓨터가 도메인과 다른 도메인에서 실행되기 [!DNL Experience Platform] 때문입니다.

## 내 [!DNL Jupyter Notebook] 모습 중 일부가 스크램블되거나 코드로 렌더링되지 않는 이유는 무엇입니까?

문제가 있는 셀이 실수로 &quot;코드&quot;에서 &quot;표시&quot;로 변경된 경우 이 문제가 발생할 수 있습니다. 코드 셀에 초점을 맞추는 동안 키 조합을 **ESC+M** 누르면 셀 유형이 마크다운으로 변경됩니다. 선택한 셀의 노트북 맨 위에 있는 드롭다운 표시기로 셀 유형을 변경할 수 있습니다. 셀 유형을 코드로 변경하려면 변경할 지정된 셀을 선택하여 시작합니다. 그런 다음 셀의 현재 유형을 나타내는 드롭다운을 클릭하고 &quot;코드&quot;를 선택합니다.

![](./images/faq/code_type.png)

## 사용자 정의 라이브러리를 어떻게 [!DNL Python] 설치합니까?

커널은 [!DNL Python] 널리 사용되는 많은 기계 학습 라이브러리와 함께 미리 설치됩니다. 그러나 코드 셀 내에서 다음 명령을 실행하여 추가 사용자 정의 라이브러리를 설치할 수 있습니다.

```shell
!pip install {LIBRARY_NAME}
```

사전 설치된 [!DNL Python] 라이브러리의 전체 목록은 JupiterLab 사용 안내서의 [부록 섹션을 참조하십시오](./jupyterlab/overview.md#supported-libraries).

## 사용자 정의 PySpark 라이브러리를 설치할 수 있습니까?

PySpark 커널용 라이브러리를 추가로 설치할 수는 없습니다. 그러나 사용자 정의 PySpark 라이브러리를 설치하려면 Adobe 고객 서비스 담당자에게 문의하십시오.

사전 설치된 PySpark 라이브러리 목록은 JupiterLab 사용 안내서의 [부록 섹션을 참조하십시오](./jupyterlab/overview.md#supported-libraries).

## PySpark 커널용 [!DNL Spark] 클러스터 리소스 [!DNL JupyterLab] 를 구성할 [!DNL Spark] 수 있습니까?

전자 필기장의 첫 번째 셀에 다음 블록을 추가하여 리소스를 구성할 수 있습니다.

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

구성 가능한 속성의 전체 목록을 포함하여 클러스터 리소스 구성에 대한 자세한 내용은 JupiterLab [!DNL Spark] 사용 안내서를 참조하십시오 [](./jupyterlab/overview.md#kernels).

## 대용량의 데이터 세트에 대해 특정 작업을 실행하려 할 때 오류가 발생하는 이유는 무엇입니까?

일반적으로 드라이버나 실행자의 메모리가 부족함을 `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 의미합니다. 데이터 제한 및 대규모 데이터 세트에서 작업을 실행하는 방법에 대한 자세한 내용은 JupiterLab [데이터 액세스](./jupyterlab/access-notebook-data.md) 설명서를 참조하십시오. 일반적으로 이 오류는 을(를) 에서 `mode` (으)로 변경하여 해결할 수 `interactive` 있습니다 `batch`.