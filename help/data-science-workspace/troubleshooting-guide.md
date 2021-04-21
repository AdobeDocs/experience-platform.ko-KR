---
keywords: Experience Platform;문제 해결;데이터 과학 작업 공간;인기 있는 주제
solution: Experience Platform
title: 데이터 과학 작업 공간 문제 해결 안내서
topic-legacy: Troubleshooting
description: 이 문서에서는 Adobe Experience Platform Data Science Workspace에 대한 질문과 답변을 제공합니다.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 문제 해결 안내서

이 문서에서는 Adobe Experience Platform [!DNL Data Science Workspace]에 대한 FAQ에 대한 답변을 제공합니다. 일반적으로 [!DNL Platform] API에 대한 질문 및 문제 해결에 대해서는 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## [!DNL JupyterLab] 환경이  [!DNL Google Chrome]

>[!IMPORTANT]
>
>이 문제는 해결되었지만 Google Chrome 80.x 브라우저에 여전히 존재할 수 있습니다. 크롬 브라우저가 최신 버전인지 확인하십시오.

[!DNL Google Chrome] 브라우저 버전 80.x에서는 기본적으로 모든 타사 쿠키가 차단됩니다. 이 정책으로 인해 [!DNL JupyterLab]이(가) Adobe Experience Platform 내에서 로드되지 않을 수 있습니다.

이 문제를 해결하려면 다음 단계를 수행하십시오.

[!DNL Chrome] 브라우저에서 오른쪽 상단으로 이동하고 **설정**&#x200B;을 선택합니다(또는 주소 표시줄에 &quot;chrome://settings/&quot;을 복사하여 붙여 넣을 수 있습니다). 그런 다음 페이지 아래쪽으로 스크롤하고 **고급** 드롭다운을 클릭합니다.

![chrome](./images/faq/chrome-advanced.png)

**개인 정보 및 보안** 섹션이 나타납니다. 다음으로 **사이트 설정**&#x200B;을 클릭한 다음 **쿠키 및 사이트 데이터**&#x200B;를 클릭합니다.

![chrome](./images/faq/privacy-security.png)

![chrome](./images/faq/cookies.png)

마지막으로 &quot;타사 쿠키 차단&quot;을 &quot;해제&quot;로 전환합니다.

![chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>또는 타사 쿠키를 비활성화하고 [*을 추가할 수도 있습니다.]ds.adobe.net을 허용 목록에 연결합니다.

주소 표시줄에 있는 &quot;chrome://flags/&quot;으로 이동합니다. 오른쪽의 드롭다운 메뉴를 사용하여 *&quot;기본 쿠키로 SameSite&quot;*&#x200B;라는 플래그를 검색하고 비활성화합니다.

![samesite 플래그 사용 안 함](./images/faq/samesite-flag.png)

2단계 후 브라우저를 다시 실행하라는 메시지가 표시됩니다. 다시 시작한 후에는 [!DNL Jupyterlab]에 액세스할 수 있어야 합니다.

## Safari에서 [!DNL JupyterLab]에 액세스할 수 없는 이유는 무엇입니까?

Safari는 Safari &lt; 12에서 기본적으로 타사 쿠키를 비활성화합니다. [!DNL Jupyter] 가상 컴퓨터 인스턴스가 부모 프레임과 다른 도메인에 있으므로 Adobe Experience Platform은 현재 타사 쿠키를 활성화해야 합니다. 타사 쿠키를 활성화하거나 [!DNL Google Chrome] 같은 다른 브라우저로 전환하십시오.

Safari 12의 경우 사용자 에이전트를 &#39;[!DNL Chrome]&#39; 또는 &#39;[!DNL Firefox]&#39;(으)로 전환해야 합니다. 사용자 에이전트를 전환하려면 *Safari* 메뉴를 열고 **환경 설정**&#x200B;을 선택합니다. 환경 설정 창이 나타납니다.

![Safari 환경 설정](./images/faq/preferences.png)

Safari 환경 설정 창에서 **고급**&#x200B;을 선택합니다. 그런 다음 메뉴 모음&#x200B;*상자에*&#x200B;현상 표시 메뉴를 선택합니다. 이 단계가 완료된 후 기본 설정 창을 닫을 수 있습니다.

![Safari 고급](./images/faq/advanced.png)

그런 다음 위쪽 탐색 모음에서 **현상** 메뉴를 선택합니다. **현상** 드롭다운 내에서 **사용자 에이전트** 위로 마우스를 가져갑니다. 사용할 **[!DNL Chrome]** 또는 **[!DNL Firefox]** 사용자 에이전트 문자열을 선택할 수 있습니다.

![현상 메뉴](./images/faq/user-agent.png)

## [!DNL JupyterLab]에서 파일을 업로드하거나 삭제하려고 할 때 &#39;403 금지&#39; 메시지가 표시되는 이유는 무엇입니까?

[!DNL Ghostery] 또는 [!DNL AdBlock] Plus와 같은 광고 차단 소프트웨어에서 사용 중인 브라우저에서 [!DNL JupyterLab]이(가) 정상적으로 작동하도록 각 광고 차단 소프트웨어에서 &quot;\*.adobe.net&quot; 도메인을 허용해야 합니다. 이것은 [!DNL JupyterLab] 가상 컴퓨터가 [!DNL Experience Platform] 도메인과 다른 도메인에서 실행되기 때문입니다.

## 내 [!DNL Jupyter Notebook]의 일부 부분은 스크램블되거나 코드로 렌더링되지 않는 이유는 무엇입니까?

이 문제는 해당 셀이 실수로 &quot;코드&quot;에서 &quot;표시&quot;로 변경된 경우에 발생할 수 있습니다. 코드 셀에 초점을 맞추는 동안 키 조합 **ESC+M**&#x200B;을 누르면 셀의 유형이 마크다운으로 변경됩니다. 셀의 유형은 선택한 셀의 노트북 맨 위에 있는 드롭다운 표시기로 변경할 수 있습니다. 셀 유형을 코드로 변경하려면 변경할 지정된 셀을 선택하여 시작합니다. 그런 다음 셀의 현재 유형을 나타내는 드롭다운을 클릭하고 &quot;코드&quot;를 선택합니다.

![](./images/faq/code_type.png)

## 사용자 정의 [!DNL Python] 라이브러리를 어떻게 설치합니까?

[!DNL Python] 커널은 자주 사용되는 많은 컴퓨터 학습 라이브러리와 함께 미리 설치됩니다. 그러나 코드 셀 내에서 다음 명령을 실행하여 추가 사용자 정의 라이브러리를 설치할 수 있습니다.

```shell
!pip install {LIBRARY_NAME}
```

사전 설치된 [!DNL Python] 라이브러리의 전체 목록은 JupiterLab 사용 안내서](./jupyterlab/overview.md#supported-libraries)의 [부록 섹션을 참조하십시오.

## 사용자 정의 PySpark 라이브러리를 설치할 수 있습니까?

PySpark 커널에 대한 라이브러리를 추가로 설치할 수는 없습니다. 그러나 사용자 정의 PySpark 라이브러리를 설치하려면 Adobe 고객 서비스 담당자에게 문의하십시오.

사전 설치된 PySpark 라이브러리 목록은 JupiterLab 사용 안내서](./jupyterlab/overview.md#supported-libraries)의 [부록 섹션을 참조하십시오.

## [!DNL JupyterLab] [!DNL Spark] 또는 PySpark 커널에 대해 [!DNL Spark] 클러스터 리소스를 구성할 수 있습니까?

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

구성 가능한 속성의 전체 목록을 포함하여 [!DNL Spark] 클러스터 리소스 구성에 대한 자세한 내용은 [JupiterLab 사용자 안내서](./jupyterlab/overview.md#kernels)를 참조하십시오.

## 큰 데이터 세트에 대해 특정 작업을 실행하려고 할 때 오류가 발생하는 이유는 무엇입니까?

`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 등의 이유로 오류가 발생하는 경우 일반적으로 드라이버나 실행자의 메모리가 부족함을 의미합니다. 데이터 제한 및 대용량 데이터 세트에서 작업을 실행하는 방법에 대한 자세한 내용은 JupiterLab 노트북 [데이터 액세스](./jupyterlab/access-notebook-data.md) 설명서를 참조하십시오. 일반적으로 이 오류는 `mode`을 `interactive`에서 `batch`로 변경하여 해결할 수 있습니다.

## [!DNL Docker Hub] 데이터 과학 작업 공간의 제한 사항

2020년 11월 20일 현재 Docker Hub의 익명 및 무료 인증 사용에 대한 요율 제한이 시행되었습니다. 익명 사용자와 무료 [!DNL Docker Hub] 사용자는 6시간마다 100개의 컨테이너 이미지 가져오기 요청으로 제한됩니다. 이러한 변경 사항에 영향을 받는 경우 다음 오류 메시지를 받게 됩니다.`ERROR: toomanyrequests: Too Many Requests.` 또는 `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

현재 이 제한은 6시간 이내에 레서피에 100개의 노트북을 만들려고 하거나 빈번하게 비율을 높이거나 낮추고 있는 데이터 과학 작업 공간 내의 Spark 기반 노트북을 사용하는 경우에만 조직에 영향을 줍니다. 그러나 이 클러스터는 유휴 상태를 유지하기 전에 2시간 동안 활성 상태를 유지하므로 이러한 상태를 유지할 수 없습니다. 이렇게 하면 클러스터가 활성 상태일 때 필요한 가져오기 수가 줄어듭니다. 위의 오류가 발생하면 [!DNL Docker] 제한이 재설정될 때까지 기다려야 합니다.

[!DNL Docker Hub] 속도 제한에 대한 자세한 내용은 [DockerHub 설명서](https://www.docker.com/increase-rate-limits)를 참조하십시오. 이에 대한 해결 방법은 후속 릴리스에서 작동하고 있어야 합니다.
