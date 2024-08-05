---
keywords: Experience Platform;문제 해결;Data Science Workspace;인기 있는 주제
solution: Experience Platform
title: 데이터 과학 Workspace 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform Data Science Workspace에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 문제 해결 안내서

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

이 문서에서는 Adobe Experience Platform [!DNL Data Science Workspace]에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 일반적으로 [!DNL Platform] API에 대한 질문과 문제 해결은 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## JupyterLab Notebook 쿼리 상태가 실행 상태에서 중단됨

JupyterLab Notebook은 일부 메모리 부족 상태에서 셀이 무기한으로 실행 중임을 나타낼 수 있습니다. 예를 들어, 큰 데이터 세트 쿼리하거나 여러 후속 쿼리를 수행할 때 JupiterLab Notebook은 결과 데이터 프레임 개체를 스토어 데 사용 가능한 메모리가 부족할 수 있습니다. 이 상황에서 볼 수 있는 몇 가지 지표가 있습니다. 첫째, 커널은 유휴 상태로 균일 전환되지만 셀은 셀 옆에 아이콘으로 [`*`] 표시된 실행 중으로 표시됩니다. 또한 아래쪽 막대는 사용/사용 가능한 RAM의 양을 나타냅니다.

![사용 가능한 램](./images/jupyterlab/user-guide/allocate-ram.png)

데이터를 읽는 동안 메모리는 할당된 메모리의 최대 양에 도달할 때까지 증가할 수 있습니다. 메모리는 최대 메모리에 도달하고 커널이 다시 시작되는 즉시 해제됩니다. 즉, 이 시나리오에서 사용된 메모리는 커널 다시 시작으로 인해 매우 낮은 것으로 표시될 수 있지만 다시 시작하기 직전에는 메모리가 할당된 최대 RAM에 매우 가까웠을 것입니다.

이 문제를 해결하려면 JupyterLab의 오른쪽 상단에 있는 톱니바퀴 아이콘을 선택하고 슬라이더를 오른쪽으로 밀고 **[!UICONTROL 구성 업데이트]**&#x200B;를 선택하여 추가 RAM을 할당합니다. 또한 여러 쿼리를 실행하고 있고 RAM 값이 최대 할당 양에 가까워지면 이전 쿼리의 결과가 필요하지 않는 한 커널을 다시 시작하여 사용 가능한 RAM을 재설정합니다. 이렇게 하면 현재 쿼리에 사용할 수 있는 최대 RAM 용량을 확보하게 됩니다.

![더 많은 ram 할당](./images/jupyterlab/user-guide/notebook-gpu-config.png)

최대 메모리(RAM)를 할당하고서도 이 문제가 발생하는 경우, 데이터 열이나 범위를 줄여 더 작은 데이터 세트 크기에서 작동하도록 쿼리를 수정할 수 있습니다. 전체 데이터를 사용하려면 Spark 노트북을 활용하는 것이 좋습니다.

## [!DNL JupyterLab] 환경이 로드되지 않습니다. [!DNL Google Chrome]

>[!IMPORTANT]
>
>이 문제는 해결되었지만 Google 크롬 80.x 브라우저 브라우저에는 여전히 존재할 수 있습니다. 크롬 브라우저 최신 버전인지 확인하십시오.

브라우저 버전 80.x에서는 [!DNL Google Chrome] 모든 서드파티 쿠키가 기본적으로 차단됩니다. 이 정책 Adobe Experience Platform 내에 로드되지 않을 수 있습니다 [!DNL JupyterLab] .

이 문제를 해결하려면 다음 단계를 사용합니다.

[!DNL Chrome] 브라우저에서 오른쪽 상단으로 이동하여 설정&#x200B;**선택합니다**(또는 주소 표시줄에 &quot;chrome://settings/&quot;를 복사하여 붙여넣을 수 있음). 그런 다음 페이지 맨 아래로 스크롤하여 **고급** 드롭다운을 클릭합니다.

![Chrome 고급](./images/faq/chrome-advanced.png)

개인 정보 및 보안&#x200B;**섹션이**&#x200B;나타납니다. 다음, 사이트 설정&#x200B;**다음에**&#x200B;쿠키 및 사이트 데이터를&#x200B;**클릭합니다**.

![Chrome 고급](./images/faq/privacy-security.png)

![Chrome 고급](./images/faq/cookies.png)

마지막으로 &quot;서드파티 쿠키 차단&quot;을 &quot;OFF&quot;로 전환합니다.

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>또는 서드파티 쿠키를 비활성화하고 [*을(를) 추가할 수 있습니다.허용 목록에 ]ds.adobe.net

주소 표시줄에서 &quot;chrome://flags/&quot;으로 이동합니다. 오른쪽의 드롭다운 메뉴를 사용하여 *&quot;SameSite를 기본 쿠키로 지정&quot;* 플래그를 검색하고 비활성화합니다.

![samesite 플래그 비활성화](./images/faq/samesite-flag.png)

2단계 후에는 브라우저를 다시 시작하라는 메시지가 표시됩니다. 다시 실행한 후에는 [!DNL Jupyterlab]에 액세스할 수 있습니다.

## Safari에서 [!DNL JupyterLab]에 액세스할 수 없는 이유는 무엇입니까?

Safari는 Safari &lt; 12에서 기본적으로 서드파티 쿠키를 비활성화합니다. [!DNL Jupyter] 가상 컴퓨터 인스턴스가 상위 프레임과 다른 도메인에 있으므로 Adobe Experience Platform에서는 현재 서드파티 쿠키를 사용하도록 설정해야 합니다. 타사 쿠키를 활성화하거나 [!DNL Google Chrome]과(와) 같은 다른 브라우저로 전환하십시오.

Safari 12의 경우 사용자 에이전트를 &#39;[!DNL Chrome]&#39; 또는 &#39;[!DNL Firefox]&#39;(으)로 전환해야 합니다. 사용자 에이전트를 전환하려면 *Safari* 메뉴를 열고 **기본 설정**&#x200B;을 선택하세요. 기본 설정 창이 나타납니다.

![Safari 환경 설정](./images/faq/preferences.png)

Safari 환경 설정 창에서 **고급**&#x200B;을 선택합니다. 그런 다음 *메뉴 표시줄의* 상자를 선택합니다. 이 단계를 완료한 후 기본 설정 창을 닫을 수 있습니다.

![Safari 고급](./images/faq/advanced.png)

그런 다음 맨 위 탐색 모음에서 **개발** 메뉴를 선택합니다. **개발** 드롭다운에서 **사용자 에이전트** 위로 마우스를 가져갑니다. 사용할 **[!DNL Chrome]** 또는 **[!DNL Firefox]** 사용자 에이전트 문자열을 선택할 수 있습니다.

![메뉴 개발](./images/faq/user-agent.png)

## [!DNL JupyterLab]에서 파일을 업로드하거나 삭제하려고 할 때 &#39;403 사용할 수 없음&#39; 메시지가 표시되는 이유는 무엇입니까?

[!DNL Ghostery] 또는 [!DNL AdBlock] Plus와 같은 광고 차단 소프트웨어로 브라우저를 사용하는 경우 [!DNL JupyterLab]이(가) 정상적으로 작동하도록 하려면 각 광고 차단 소프트웨어에서 &quot;\*.adobe.net&quot; 도메인을 허용해야 합니다. [!DNL JupyterLab] 가상 컴퓨터가 [!DNL Experience Platform] 도메인과 다른 도메인에서 실행되기 때문입니다.

## [!DNL Jupyter Notebook]의 일부 부분이 스크램블 상태로 보이거나 코드로 렌더링되지 않는 이유는 무엇입니까?

해당 셀이 실수로 &quot;Code&quot;에서 &quot;Markdown&quot;으로 변경된 경우 이러한 문제가 발생할 수 있습니다. 코드 셀이 포커스를 갖는 동안 키 조합 **ESC+M**&#x200B;을 누르면 셀의 형식이 Markdown으로 변경됩니다. 선택한 셀에 대해 노트북 위쪽에 있는 드롭다운 표시기에 의해 셀 유형을 변경할 수 있습니다. 셀 유형을 코드로 변경하려면 먼저 변경할 특정 셀을 선택합니다. 그런 다음 셀의 현재 유형을 나타내는 드롭다운을 클릭한 다음 &quot;코드&quot;를 선택합니다.

![](./images/faq/code_type.png)

## 사용자 지정 [!DNL Python] 라이브러리를 설치하려면 어떻게 해야 합니까?

[!DNL Python] 커널은 많이 사용되는 기계 학습 라이브러리와 함께 미리 설치됩니다. 그러나 코드 셀 내에서 다음 명령을 실행하여 추가 사용자 지정 라이브러리를 설치할 수 있습니다.

```shell
!pip install {LIBRARY_NAME}
```

사전 설치된 [!DNL Python] 라이브러리의 전체 목록은 JupyterLab 사용 설명서의 [부록 섹션](./jupyterlab/overview.md#supported-libraries)을 참조하십시오.

## 사용자 지정 PySpark 라이브러리를 설치할 수 있습니까?

죄송합니다. PySpark 커널에 대한 추가 라이브러리를 설치할 수 없습니다. 그러나 Adobe 고객 서비스 담당자에게 문의하여 사용자 정의 PySpark 라이브러리를 설치할 수 있습니다.

사전 설치된 PySpark 라이브러리 목록은 JupyterLab 사용 안내서의 [부록 섹션](./jupyterlab/overview.md#supported-libraries)을 참조하십시오.

## [!DNL JupyterLab] [!DNL Spark] 또는 PySpark 커널에 대한 [!DNL Spark] 클러스터 리소스를 구성할 수 있습니까?

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

구성 가능한 속성의 전체 목록을 포함하여 [!DNL Spark] 클러스터 리소스 구성에 대한 자세한 내용은 [JupyterLab 사용 안내서](./jupyterlab/overview.md#kernels)를 참조하십시오.

## 대규모 데이터 세트에 대한 특정 작업을 실행하려고 할 때 오류가 발생하는 이유는 무엇입니까?

`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`과(와) 같은 이유로 오류가 발생하는 경우 일반적으로 드라이버나 Executor의 메모리가 부족함을 의미합니다. 데이터 제한 및 대규모 데이터 세트에서 작업을 실행하는 방법에 대한 자세한 내용은 JupyterLab Notebooks [데이터 액세스](./jupyterlab/access-notebook-data.md) 설명서를 참조하십시오. 일반적으로 이 오류는 `mode`을(를) `interactive`에서 `batch`(으)로 변경하여 해결할 수 있습니다.

또한 대규모 Spark/PySpark 데이터 세트를 작성하는 동안 쓰기 코드를 실행하기 전에 데이터(`df.cache()`)를 캐시하면 성능이 크게 향상될 수 있습니다.

<!-- remove this paragraph at a later date once the sdk is updated -->

데이터를 읽는 동안 문제 가 발생하고 데이터에 변환을 적용하는 경우 변환 전에 데이터를 캐싱 해 보십시오. 데이터를 캐싱하면 네트워크를 통한 다중 읽기가 방지됩니다. 데이터를 읽어 시작. 다음, 데이터를 캐시(`df.cache()`)합니다. 마지막으로 변환을 수행합니다.

## Spark/PySpark 노트북이 데이터를 읽고 쓰는 데 시간이 오래 걸리는 이유는 무엇인가요?

를 사용하는 `fit()`경우와 같이 데이터에 대한 변환을 수행하는 경우 변환이 여러 번 실행될 수 있습니다. 성능을 향상시키려면 를 수행하기 `fit()`전에 을 사용하여 `df.cache()` 데이터를 캐시하십시오. 이렇게 하면 변환은 한 번만 실행되며 네트워크를 통해 여러 번 읽기를 방지할 수 있습니다.

**권장 순서:** 데이터를 읽는 것부터 시작합니다. 그런 다음 변환을 수행한 다음 데이터를 캐싱(`df.cache()`)합니다. 마지막으로 `fit()`을(를) 수행합니다.

## Spark/PySpark 노트북이 실행되지 않는 이유는 무엇입니까?

다음 오류가 발생하는 경우:

- 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
- 원격 RPC 클라이언트 연결 해제 및 기타 메모리 오류입니다.
- 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.

데이터를 쓰기 전에 데이터 (`df.cache()`)를 캐싱 중인지 확인하십시오. Notebook에서 코드를 실행할 때 다음과 `fit()` 같은 작업을 앞에 사용하면 `df.cache()` Notebook 성능을 크게 향상시킬 수 있습니다. 데이터 집합을 쓰기 전에 `df.cache()`을(를) 사용하면 변형이 여러 번 실행되지 않고 한 번만 실행됩니다.

## 데이터 과학 Workspace의 [!DNL Docker Hub] 제한

2020년 11월 20일부터 Docker Hub의 익명 및 무료 인증 사용에 대한 속도 제한이 적용되었습니다. 익명 및 무료 [!DNL Docker Hub] 사용자는 6시간마다 100개의 컨테이너 이미지 가져오기 요청으로 제한됩니다. 이러한 변경 사항의 영향을 받는 경우 다음 오류 메시지가 `ERROR: toomanyrequests: Too Many Requests.` `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`표시됩니다.

현재 이 제한은 6시간 일정 내에 100개의 Notebook to Recipes를 빌드하려고 하거나 자주 확장 및 축소되는 Data Science 작업 영역 내에서 Spark 기반 Notebook을 사용하는 경우에만 조직에 영향을 줍니다. 그러나 이러한 클러스터가 유휴 상태가 되기 전에 2시간 동안 활성 상태로 유지되기 때문에 그럴 가능성은 거의 없습니다. 이렇게 하면 클러스터가 활성 상태일 때 필요한 끌어오기 수가 줄어듭니다. 위의 오류 중 하나라도 발생하면 한도가 재설정될 때까지 기다려야 합니다 [!DNL Docker] .

속도 제한에 대한 [!DNL Docker Hub] 자세한 내용은 DockerHub 설명서를](https://www.docker.com/increase-rate-limits) 방문 하세요[. 이에 대한 해결책은 현재 작업 중이며 후속 릴리스에서 나올 것으로 예상됩니다.
