---
keywords: Experience Platform;문제 해결;데이터 과학 작업 공간;인기 있는 주제
solution: Experience Platform
title: Data Science Workspace 문제 해결 안내서
topic-legacy: Troubleshooting
description: 이 문서에서는 Adobe Experience Platform Data Science Workspace에 대해 자주 묻는 질문과 답변을 제공합니다.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: c2c2b1684e2c2c3c76dc23ad1df720abd6c4356c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 문제 해결 안내서

이 문서에서는 Adobe Experience Platform [!DNL Data Science Workspace]에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 일반적으로 [!DNL Platform] API에 대한 질문 및 문제 해결에 대해서는 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## [!DNL JupyterLab] 환경이 로드되지 않습니다.  [!DNL Google Chrome]

>[!IMPORTANT]
>
>이 문제는 해결되었지만 Google Chrome 80.x 브라우저에 계속 있을 수 있습니다. Chrome 브라우저가 최신 상태인지 확인하십시오.

[!DNL Google Chrome] 브라우저 버전 80.x를 사용하면 기본적으로 모든 타사 쿠키가 차단됩니다. 이 정책으로 인해 [!DNL JupyterLab] 이 Adobe Experience Platform 내에서 로드되지 않을 수 있습니다.

이 문제를 해결하려면 다음 단계를 수행하십시오.

[!DNL Chrome] 브라우저에서 오른쪽 상단으로 이동하고 **설정**&#x200B;을 선택합니다(또는 주소 표시줄에 &quot;chrome://settings/&quot;을 복사하여 붙여 넣을 수 있음). 그런 다음 페이지 하단으로 스크롤하여 **고급** 드롭다운을 클릭합니다.

![chrome advanced](./images/faq/chrome-advanced.png)

**개인 정보 및 보안** 섹션이 나타납니다. 그런 다음 **사이트 설정**&#x200B;을 클릭한 후 **쿠키 및 사이트 데이터**&#x200B;를 클릭합니다.

![chrome advanced](./images/faq/privacy-security.png)

![chrome advanced](./images/faq/cookies.png)

마지막으로 &quot;타사 쿠키 차단&quot;을 &quot;해제&quot;로 전환합니다.

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>또는 타사 쿠키를 비활성화하고 [*를 추가할 수 있습니다.]ds.adobe.net 을 허용 목록에 추가합니다.

주소 표시줄에서 &quot;chrome://flags/&quot;으로 이동합니다. 오른쪽의 드롭다운 메뉴를 사용하여 *&quot;SameSite를 기본 쿠키로 지정&quot;* 플래그를 검색하고 비활성화합니다.

![samesite 플래그 비활성화](./images/faq/samesite-flag.png)

2단계 후 브라우저를 다시 시작하라는 메시지가 표시됩니다. 다시 실행한 후에는 [!DNL Jupyterlab]에 액세스할 수 있어야 합니다.

## Safari에서 [!DNL JupyterLab]에 액세스할 수 없는 이유는 무엇입니까?

Safari는 12 이하 Safari에서 기본적으로 타사 쿠키를 비활성화합니다. [!DNL Jupyter] 가상 컴퓨터 인스턴스가 상위 프레임이 아닌 다른 도메인에 있으므로 Adobe Experience Platform에서는 현재 타사 쿠키를 활성화해야 합니다. 타사 쿠키를 활성화하거나 [!DNL Google Chrome] 등의 다른 브라우저로 전환하십시오.

Safari 12의 경우 사용자 에이전트를 &#39;[!DNL Chrome]&#39; 또는 &#39;[!DNL Firefox]&#39;(으)로 전환해야 합니다. 사용자 에이전트를 전환하려면 *Safari* 메뉴를 열고 **환경 설정**&#x200B;을 선택합니다. 환경설정 창이 나타납니다.

![Safari 환경 설정](./images/faq/preferences.png)

Safari 환경 설정 창에서 **고급**&#x200B;을 선택합니다. 그런 다음 메뉴 막대에 *개발 메뉴 표시* 상자를 선택합니다. 이 단계가 완료되면 기본 설정 창을 닫을 수 있습니다.

![Safari 고급](./images/faq/advanced.png)

그런 다음 맨 위 탐색 막대에서 **개발** 메뉴를 선택합니다. **개발** 드롭다운 내에서 **사용자 에이전트** 위로 마우스를 가져갑니다. 사용하려는 **[!DNL Chrome]** 또는 **[!DNL Firefox]** 사용자 에이전트 문자열을 선택할 수 있습니다.

![개발 메뉴](./images/faq/user-agent.png)

## [!DNL JupyterLab]에서 파일을 업로드하거나 삭제하려고 할 때 &#39;403 금지됨&#39; 메시지가 표시되는 이유는 무엇입니까?

브라우저가 [!DNL Ghostery] 또는 [!DNL AdBlock] Plus와 같은 광고 차단 소프트웨어를 사용하여 활성화되어 있으면 [!DNL JupyterLab]이(가) 정상적으로 작동하도록 각 광고 차단 소프트웨어에서 &quot;\*.adobe.net&quot; 도메인을 허용해야 합니다. [!DNL JupyterLab] 가상 컴퓨터가 [!DNL Experience Platform] 도메인과 다른 도메인에서 실행되기 때문입니다.

## [!DNL Jupyter Notebook] 의 일부 부분은 스크램블된 것처럼 보이거나 코드로 렌더링되지 않는 이유는 무엇입니까?

이 문제는 해당 셀이 실수로 &quot;코드&quot;에서 &quot;Markdown&quot;으로 변경되면 발생할 수 있습니다. 코드 셀에 초점을 맞추고 있는 동안 키 조합 **ESC+M**&#x200B;을 누르면 셀의 유형이 Markdown으로 변경됩니다. 선택한 셀에 대한 전자 필기장 맨 위에 있는 드롭다운 표시기로 셀의 유형을 변경할 수 있습니다. 셀 유형을 코드로 변경하려면 먼저 변경할 셀을 선택합니다. 그런 다음 셀의 현재 유형을 나타내는 드롭다운을 클릭하고 &quot;코드&quot;를 선택합니다.

![](./images/faq/code_type.png)

## 사용자 지정 [!DNL Python] 라이브러리를 설치하려면 어떻게 합니까?

[!DNL Python] 커널에는 많이 사용되는 기계 학습 라이브러리가 미리 설치됩니다. 그러나 코드 셀 내에서 다음 명령을 실행하여 추가 사용자 지정 라이브러리를 설치할 수 있습니다.

```shell
!pip install {LIBRARY_NAME}
```

사전 설치된 [!DNL Python] 라이브러리의 전체 목록은 JupiterLab 사용 안내서](./jupyterlab/overview.md#supported-libraries)의 [부록 섹션을 참조하십시오.

## 사용자 지정 PySpark 라이브러리를 설치할 수 있습니까?

안타깝게도 PySpark 커널용 추가 라이브러리는 설치할 수 없습니다. 그러나 Adobe 고객 서비스 담당자에게 연락하여 사용자 정의 PySpark 라이브러리를 설치할 수 있습니다.

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

구성 가능한 속성의 전체 목록을 포함하여 [!DNL Spark] 클러스터 리소스 구성에 대한 자세한 내용은 [JupiterLab 사용 안내서](./jupyterlab/overview.md#kernels)를 참조하십시오.

## 더 큰 데이터 세트에 대해 특정 작업을 실행하려고 할 때 오류가 표시되는 이유는 무엇입니까?

`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 등의 이유로 오류가 발생하는 경우 일반적으로 드라이버나 실행자의 메모리가 부족함을 의미합니다. 데이터 제한 및 대규모 데이터 세트에서 작업을 실행하는 방법에 대한 자세한 내용은 JupiterLab Notebook [데이터 액세스](./jupyterlab/access-notebook-data.md) 설명서를 참조하십시오. 일반적으로 이 오류는 `interactive`에서 `batch`로 `mode`을 변경하여 해결할 수 있습니다.

또한 큰 Spark/PySpark 데이터 세트를 작성하는 동안 쓰기 코드를 실행하기 전에 데이터(`df.cache()`)를 캐시하면 성능이 크게 향상됩니다.

<!-- remove this paragraph at a later date once the sdk is updated -->

데이터를 읽는 동안 문제가 발생하여 데이터에 변형을 적용하는 경우 변환 전에 데이터를 캐싱해 보십시오. 데이터를 캐싱하면 네트워크에서 여러 읽기가 방지됩니다. 먼저 데이터를 읽습니다. 그런 다음 데이터를 캐시합니다(`df.cache()`). 마지막으로 변형을 수행합니다.

## Spark/PySpark 노트북에서 데이터를 읽고 쓰는 데 시간이 오래 걸리는 이유는 무엇입니까?

`fit()` 사용과 같이 데이터에 대한 변환을 수행하는 경우 변형이 여러 번 실행될 수 있습니다. 성능을 높이려면 `fit()`을 수행하기 전에 `df.cache()`을 사용하여 데이터를 캐시합니다. 이렇게 하면 변환이 한 번만 실행되며 네트워크에서 여러 읽기를 방지할 수 있습니다.

**권장 순서:** 데이터를 읽어서 시작합니다. 그런 다음 데이터를 캐싱(`df.cache()`)하여 변환을 수행합니다. 마지막으로 `fit()`을 수행합니다.

## Spark/PySpark 노트북을 실행하지 못하는 이유는 무엇입니까?

다음 오류를 수신하는 경우:

- 스테이지 오류로 인해 작업이 중단되었습니다..각 파티션에서 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
- 원격 RPC 클라이언트가 연결이 끊기고 다른 메모리 오류가 발생했습니다.
- 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.

데이터를 쓰기 전에 데이터(`df.cache()`)를 캐시하는지 확인합니다. 전자 필기장에서 코드를 실행할 때 `fit()` 등과 같은 작업 전에 `df.cache()`을 사용하면 전자 필기장 성능을 크게 향상시킬 수 있습니다. 데이터 집합을 쓰기 전에 `df.cache()`을 사용하면 변형이 여러 번 실행되는 대신 한 번만 실행됩니다.

## [!DNL Docker Hub] 데이터 과학 작업 공간의 제한

2020년 11월 20일 현재 Docker Hub의 익명 및 무료 인증 사용에 대한 비율 제한이 적용되었습니다. 익명 및 무료 [!DNL Docker Hub] 사용자는 6시간마다 100개의 컨테이너 이미지 가져오기 요청으로 제한됩니다. 이러한 변경 사항의 영향을 받는 경우에는 다음 오류 메시지가 표시됩니다.`ERROR: toomanyrequests: Too Many Requests.` 또는 `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`

현재, 6시간 이내에 레서피에 100개의 노트북을 작성하려고 하거나, 확장 및 다운이 빈번한 데이터 과학 작업 공간 내에서 Spark 기반 노트북을 사용하는 경우에만 조직에 이 제한이 적용됩니다. 그러나 이러한 클러스터는 유휴 상태가 되기 전에 2시간 동안 활성 상태로 유지되므로 이러한 작업은 거의 발생하지 않습니다. 이렇게 하면 클러스터가 활성 상태일 때 필요한 가져오기 수가 줄어듭니다. 위의 오류가 발생하면 [!DNL Docker] 제한이 재설정될 때까지 기다려야 합니다.

[!DNL Docker Hub] 비율 제한에 대한 자세한 내용은 [DockerHub 설명서](https://www.docker.com/increase-rate-limits)를 참조하십시오. 이에 대한 해결 방법은 후속 릴리스에서 계속 작동되고 예상됩니다.
