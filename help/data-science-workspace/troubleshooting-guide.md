---
keywords: Experience Platform;문제 해결;Data Science Workspace;인기 있는 주제
solution: Experience Platform
title: 데이터 과학 작업 공간 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform 데이터 과학 작업 영역에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 문제 해결 안내서

이 문서에서는 Adobe Experience Platform에 대해 자주 묻는 질문에 대한 답변을 제공합니다 [!DNL Data Science Workspace]. 관련 질문 및 문제 해결 [!DNL Platform] 일반적으로 API는 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md).

## JupyterLab Notebook 쿼리 상태가 실행 상태에서 중단됨

JupyterLab Notebook은 일부 메모리 부족 상태에서 셀이 무기한으로 실행 중임을 나타낼 수 있습니다. 예를 들어 큰 데이터 세트를 쿼리하거나 여러 후속 쿼리를 수행할 때 JupyterLab Notebook에 사용 가능한 메모리가 부족하여 결과 데이터 프레임 개체를 저장할 수 있습니다. 이런 상황에서 볼 수 있는 몇 가지 지표가 있다. 먼저, 셀은 다음에 의해 표시된 실행으로 보여지더라도 커널은 유휴 상태로 진입한다. [`*`] 셀 옆에 있는 아이콘. 또한 맨 아래 막대는 사용/사용 가능한 RAM의 양을 나타냅니다.

![사용 가능한 RAM](./images/jupyterlab/user-guide/allocate-ram.png)

데이터를 읽는 동안 할당된 최대 메모리 양에 도달할 때까지 메모리가 증가할 수 있습니다. 최대 메모리에 도달하면 메모리가 해제되고 커널이 다시 시작됩니다. 즉, 이 시나리오에서 사용된 메모리는 커널 재시작으로 인해 매우 낮은 것으로 표시될 수 있지만, 재시작 직전에 메모리가 할당된 최대 RAM에 매우 근접했을 수 있습니다.

이 문제를 해결하려면 JupyterLab의 오른쪽 상단에 있는 톱니바퀴 아이콘을 선택하고 슬라이더를 오른쪽으로 이동한 다음 을 선택합니다. **[!UICONTROL 구성 업데이트]** 추가 RAM을 할당합니다. 또한 여러 쿼리를 실행하고 있고 RAM 값이 최대 할당 양에 가까워지면 이전 쿼리의 결과가 필요하지 않는 한 커널을 다시 시작하여 사용 가능한 RAM을 재설정합니다. 이렇게 하면 현재 쿼리에 사용할 수 있는 최대 RAM 용량을 확보하게 됩니다.

![추가 ram 할당](./images/jupyterlab/user-guide/notebook-gpu-config.png)

최대 메모리(RAM)를 할당하고서도 이 문제가 발생하는 경우, 데이터 열이나 범위를 줄여 더 작은 데이터 세트 크기에서 작동하도록 쿼리를 수정할 수 있습니다. 전체 데이터를 사용하려면 Spark 노트북을 활용하는 것이 좋습니다.

## [!DNL JupyterLab] 환경이 로드되지 않음 [!DNL Google Chrome]

>[!IMPORTANT]
>
>이 문제는 해결되었지만 Google Chrome 80.x 브라우저에는 여전히 존재할 수 있습니다. Chrome 브라우저가 최신 상태인지 확인하십시오.

포함 [!DNL Google Chrome] 브라우저 버전 80.x에서는 모든 타사 쿠키가 기본적으로 차단됩니다. 이 정책을 사용하면 다음을 방지할 수 있습니다. [!DNL JupyterLab] Adobe Experience Platform 내에서 로드할 수 있습니다.

이 문제를 해결하려면 다음 단계를 사용하십시오.

내 [!DNL Chrome] 브라우저에서 오른쪽 상단으로 이동하여 을 선택합니다. **설정** (또는 주소 표시줄에 &quot;chrome://settings/&quot;을 복사하여 붙여 넣을 수 있습니다.) 그런 다음 페이지 아래쪽으로 스크롤하여 **고급** 드롭다운입니다.

![chrome advanced](./images/faq/chrome-advanced.png)

다음 **개인 정보 보호 및 보안** 섹션이 나타납니다. 그런 다음 을 클릭합니다. **사이트 설정** 뒤에 오는 **쿠키 및 사이트 데이터**.

![chrome advanced](./images/faq/privacy-security.png)

![chrome advanced](./images/faq/cookies.png)

마지막으로 &quot;서드파티 쿠키 차단&quot;을 &quot;끄기&quot;로 전환합니다.

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>또는 서드파티 쿠키를 비활성화하고 를 추가할 수 있습니다 [*.]허용 목록 ds.adobe.net으로 이동합니다.

주소 표시줄에서 &quot;chrome://flags/&quot;으로 이동합니다. 제목이 있는 플래그 검색 및 비활성화 *&quot;SameSite를 기본 쿠키로 지정&quot;* 오른쪽 드롭다운 메뉴를 사용하여

![samesite 플래그 비활성화](./images/faq/samesite-flag.png)

2단계 후에는 브라우저를 다시 시작하라는 메시지가 표시됩니다. 재실행 후, [!DNL Jupyterlab] 에 액세스할 수 있어야 합니다.

## 액세스할 수 없는 이유 [!DNL JupyterLab] Safari에서?

Safari는 Safari &lt; 12에서 기본적으로 서드파티 쿠키를 비활성화합니다. 이유: [!DNL Jupyter] 가상 컴퓨터 인스턴스가 상위 프레임과 다른 도메인에 있습니다. Adobe Experience Platform에서는 현재 서드파티 쿠키를 활성화해야 합니다. 다음과 같은 타사 쿠키를 활성화하거나 다른 브라우저로 전환하십시오. [!DNL Google Chrome].

Safari 12의 경우 사용자 에이전트를 &#39;(으)로 전환해야 합니다.[!DNL Chrome]&#39; 또는 &#39;[!DNL Firefox]&#39;. 사용자 에이전트를 전환하려면 먼저 *Safari* 메뉴 및 선택 **환경 설정**. 기본 설정 창이 나타납니다.

![Safari 환경 설정](./images/faq/preferences.png)

Safari 환경 설정 창에서 다음을 선택합니다. **고급**. 그런 다음 *메뉴 모음에 Develop 메뉴 표시* 상자. 이 단계를 완료한 후 기본 설정 창을 닫을 수 있습니다.

![Safari 고급](./images/faq/advanced.png)

그런 다음 맨 위 탐색 막대에서 **개발** 메뉴 아래의 제품에서 사용할 수 있습니다. 다음 범위 내에서 **개발** 드롭다운, 마우스로 가리키기 **사용자 에이전트**. 다음을 선택할 수 있습니다. **[!DNL Chrome]** 또는 **[!DNL Firefox]** 사용하려는 사용자 에이전트 문자열입니다.

![개발 메뉴](./images/faq/user-agent.png)

## 에서 파일을 업로드하거나 삭제할 때 &#39;403 금지됨&#39; 메시지가 표시되는 이유는 무엇입니까? [!DNL JupyterLab]?

브라우저가 과 같은 광고 차단 소프트웨어로 활성화된 경우 [!DNL Ghostery] 또는 [!DNL AdBlock] 또한 각 광고 차단 소프트웨어에서 &quot;\*.adobe.net&quot; 도메인을 허용해야 합니다. [!DNL JupyterLab] 정상적으로 작동합니다. 이유는 다음과 같습니다. [!DNL JupyterLab] 가상 컴퓨터는 다음과 다른 도메인에서 실행됩니다. [!DNL Experience Platform] 도메인.

## 왜 내 일부만 [!DNL Jupyter Notebook] 스크램블 된 것처럼 보이거나 코드로 렌더링하지 않습니까?

해당 셀이 실수로 &quot;Code&quot;에서 &quot;Markdown&quot;으로 변경된 경우 이러한 문제가 발생할 수 있습니다. 코드 셀이 포커스가 있는 동안 키 조합을 누릅니다. **ESC+M** 셀 유형을 Markdown으로 변경합니다. 선택한 셀에 대해 노트북 위쪽에 있는 드롭다운 표시기에 의해 셀 유형을 변경할 수 있습니다. 셀 유형을 코드로 변경하려면 먼저 변경할 특정 셀을 선택합니다. 그런 다음 셀의 현재 유형을 나타내는 드롭다운을 클릭한 다음 &quot;코드&quot;를 선택합니다.

![](./images/faq/code_type.png)

## 사용자 지정 설치 방법 [!DNL Python] 라이브러리?

다음 [!DNL Python] 커널은 많은 인기 있는 머신 러닝 라이브러리와 함께 사전 설치됩니다. 그러나 코드 셀 내에서 다음 명령을 실행하여 추가 사용자 지정 라이브러리를 설치할 수 있습니다.

```shell
!pip install {LIBRARY_NAME}
```

사전 설치된 전체 목록의 경우 [!DNL Python] 라이브러리, 다음을 참조하십시오. [jupyterLab 사용 안내서의 부록 섹션](./jupyterlab/overview.md#supported-libraries).

## 사용자 지정 PySpark 라이브러리를 설치할 수 있습니까?

죄송합니다. PySpark 커널에 대한 추가 라이브러리를 설치할 수 없습니다. 그러나 Adobe 고객 서비스 담당자에게 문의하여 사용자 정의 PySpark 라이브러리를 설치할 수 있습니다.

사전 설치된 PySpark 라이브러리 목록은 [jupyterLab 사용 안내서의 부록 섹션](./jupyterlab/overview.md#supported-libraries).

## 다음을 구성할 수 있습니까 [!DNL Spark] 클러스터 리소스 [!DNL JupyterLab] [!DNL Spark] 아니면 PySpark 커널이요?

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

에 대한 자세한 내용 [!DNL Spark] 구성 가능한 속성의 전체 목록을 포함한 클러스터 리소스 구성은 [JupyterLab 사용 안내서](./jupyterlab/overview.md#kernels).

## 대규모 데이터 세트에 대한 특정 작업을 실행하려고 할 때 오류가 발생하는 이유는 무엇입니까?

다음과 같은 이유로 오류가 발생하는 경우 `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 이는 일반적으로 운전자나 실행자의 메모리가 부족함을 의미합니다. JupyterLab Notebooks 참조 [데이터 액세스](./jupyterlab/access-notebook-data.md) 데이터 제한 및 대규모 데이터 세트에서 작업을 실행하는 방법에 대한 자세한 내용은 설명서에서 확인할 수 있습니다. 일반적으로 이 오류는 를 변경하여 해결할 수 있습니다 `mode` 출처: `interactive` 끝 `batch`.

또한 대규모 Spark/PySpark 데이터 세트를 작성하는 동안 데이터를 캐시합니다(`df.cache()`) 쓰기 코드를 실행하기 전에 성능을 크게 향상시킬 수 있습니다.

<!-- remove this paragraph at a later date once the sdk is updated -->

데이터를 읽는 동안 문제가 발생하고 데이터에 변형을 적용하는 경우 변형 전에 데이터를 캐시해 보십시오. 데이터를 캐시하면 네트워크를 통한 다중 읽기가 방지됩니다. 데이터를 읽는 것부터 시작하십시오. 다음, 캐시(`df.cache()`) 데이터를 복제합니다. 마지막으로 변형을 수행합니다.

## Spark/PySpark 노트북이 데이터를 읽고 쓰는 데 왜 이렇게 오래 걸립니까?

데이터를 다음과 같이 변환하는 경우 `fit()`로 변환은 여러 번 실행될 수 있습니다. 성능을 향상시키려면 다음을 사용하여 데이터를 캐시합니다. `df.cache()` 을 수행하기 전에 `fit()`. 이렇게 하면 변환은 한 번만 실행되며 네트워크를 통해 여러 번 읽기를 방지할 수 있습니다.

**권장 순서:** 데이터를 읽는 것부터 시작하십시오. 그런 다음 캐싱에 따라 변환을 수행합니다(`df.cache()`) 데이터를 복제합니다. 마지막으로 다음을 수행합니다. `fit()`.

## Spark/PySpark 노트북이 실행되지 않는 이유는 무엇입니까?

다음 오류가 발생하는 경우:

- 단계 오류로 인해 작업이 중단되었습니다. 각 파티션에 동일한 수의 요소가 있는 RDD만 압축할 수 있습니다.
- 원격 RPC 클라이언트 연결이 끊어지고 다른 메모리 오류가 발생했습니다.
- 데이터 세트를 읽고 쓸 때 성능이 저하됩니다.

데이터를 캐시하고 있는지 확인합니다(`df.cache()`)를 클릭하여 데이터를 작성합니다. Notebooks에서 코드를 실행할 때 `df.cache()` 다음 작업 전 `fit()` 은 노트북 성능을 크게 향상시킬 수 있습니다. 사용 `df.cache()` 데이터 세트를 쓰기 전에 변형을 여러 번 실행하지 않고 한 번만 실행합니다.

## [!DNL Docker Hub] 데이터 과학 작업 영역의 제한 사항

2020년 11월 20일부터 도커 허브의 익명 및 무료 인증 사용에 대한 요금 제한이 적용됩니다. 익명 및 무료 [!DNL Docker Hub] 사용자는 6시간마다 100개의 컨테이너 이미지 가져오기 요청으로 제한됩니다. 이러한 변경 사항의 영향을 받는 경우 다음 오류 메시지가 표시됩니다. `ERROR: toomanyrequests: Too Many Requests.` 또는 `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

현재, 이 제한은 6시간 이내에 100개의 Notebook to Recipes를 작성하려고 하거나 Data Science Workspace 내에서 자주 확대 및 축소되는 Spark 기반 Notebooks를 사용하는 경우에만 조직에 영향을 줍니다. 그러나 이러한 클러스터가 유휴 상태로 유지되기 전에 2시간 동안 활성 상태를 유지하므로 그렇게 할 가능성은 낮습니다. 이렇게 하면 클러스터가 활성 상태일 때 필요한 가져오기 수가 줄어듭니다. 위의 오류 중 하나라도 발생하면 다음 시간까지 기다려야 합니다. [!DNL Docker] 제한이 재설정됩니다.

에 대한 자세한 내용 [!DNL Docker Hub] 비율 제한, 다음을 방문하십시오. [DockerHub 설명서](https://www.docker.com/increase-rate-limits). 이에 대한 해결 방법은 후속 릴리스에서 진행 중이며 향후 제공될 예정입니다.
