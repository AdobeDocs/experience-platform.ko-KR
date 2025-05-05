---
keywords: Experience Platform;패키지 소스 파일;Data Science Workspace;인기 주제;도커;도커 이미지
solution: Experience Platform
title: 레시피에 Source 파일 패키징
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 아카이브 파일로 패키징하는 방법에 대한 지침을 제공합니다. 이 파일은 UI에서 또는 API를 사용하여 레시피 가져오기 워크플로우를 따라 Adobe Experience Platform Data Science Workspace에서 레시피를 만드는 데 사용할 수 있습니다.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# 소스 파일을 레시피로 패키징

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 데이터 과학 작업 영역 이전에 사용 권한이 있는 기존 고객을 대상으로 합니다.

이 튜토리얼에서는 제공된 소매 판매 샘플 원본 파일을 보관 파일로 패키지하는 방법에 대한 지침을 제공하며, 이 파일은 UI 또는 API를 사용하여 레서피 가져오기 작업 과정 따라 Adobe Experience Platform [!DNL Data Science Workspace] 에서 레서피 만드는 데 사용할 수 있습니다.

이해해야 할 개념:

- **레시피**: 레서피는 모델 사양에 대한 Adobe Systems 용어로, 특정 기계 학습, 인공 인텔리전스 알고리즘 또는 알고리즘 앙상블, 처리 논리 및 학습된 모델을 빌드 및 실행하여 특정 비즈니스 문제를 해결하는 데 필요한 구성을 나타내는 최상위 컨테이너입니다.
- **소스 파일**: 레서피 로직을 포함하는 프로젝트의 개별 파일입니다.

## 전제 조건

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 레시피 만들기

레시피 생성은 아카이브 파일을 빌드 소스 파일을 패키징하는 것으로 시작됩니다. 소스 파일은 당면한 특정 문제 문제를 해결하는 데 사용되는 기계 학습 논리 및 알고리즘을 정의하며 , R, PySpark 또는 Scala로 [!DNL Python]작성됩니다. 빌드된 아카이브 파일은 Docker 이미지 형식을 취합니다. 빌드가 완료되면 패키지된 아카이브 파일을 UI[&#128279;](./import-packaged-recipe-ui.md) [또는 API](./import-packaged-recipe-api.md)를 사용하여 레서피 생성하기 위해 가져옵니다[!DNL Data Science Workspace].

### Docker 기반 모델 작성 {#docker-based-model-authoring}

Docker 이미지를 사용하면 개발자가 필요한 모든 부분(예: 라이브러리 및 기타 종속성)으로 애플리케이션 패키지를 패키지화하여 하나의 패키지로 제공할 수 있습니다.

빌드된 도커 이미지는 레시피 만들기 워크플로 중에 제공된 자격 증명을 사용하여 Azure Container Registry에 푸시됩니다.

Azure Container Registry 자격 증명을 얻으려면 [Adobe Experience Platform](https://platform.adobe.com)에 로그인하십시오. 왼쪽 탐색 열에서 **[!UICONTROL 워크플로]**(으)로 이동합니다. **[!UICONTROL 레시피 가져오기]**&#x200B;를 선택한 후 **[!UICONTROL 시작]**&#x200B;을 선택하십시오. 참조를 위해 아래 스크린 샷을 참조하십시오.

![](../images/models-recipes/package-source-files/import.png)

**[!UICONTROL 구성]** 페이지 가 열립니다. 적절한 **[!UICONTROL 레서피 이름]**(예: &quot;소매 판매 레서피&quot;)을 제공하고 선택적으로 설명 또는 설명서 URL을 제공합니다. 완료되면 다음(Next)**을 클릭합니다**.

![](../images/models-recipes/package-source-files/configure.png)

적절한 *런타임*&#x200B;을 선택한 다음 *유형*&#x200B;에 대한 **[!UICONTROL 분류]**&#x200B;을(를) 선택하십시오. 완료되면 Azure 컨테이너 레지스트리 자격 증명이 생성됩니다.

>[!NOTE]
>
>*유형*&#x200B;은(는) 레시피가 설계된 머신 러닝 문제의 클래스이며, 교육 실행 평가를 맞춤화하기 위해 교육 후에 사용됩니다.

>[!TIP]
>
>- [!DNL Python] 레시피의 경우 **[!UICONTROL Python]** 런타임을 선택하십시오.
>- R 레시피의 경우 **[!UICONTROL R]** 런타임을 선택하십시오.
>- PySpark 레시피의 경우 **[!UICONTROL PySpark]** 런타임을 선택하십시오. 아티팩트 유형이 자동으로 채워집니다.
>- Scala 레시피의 경우 Spark **런타임을**&#x200B;선택합니다. 아티팩트 유형이 자동으로 채워집니다.

![](../images/models-recipes/package-source-files/docker-creds.png)

Docker 호스트, username 및 암호에 대한 값을 기록해 둡니다. 이러한 워크플로우는 아래 설명된 워크플로우에서 이미지를 빌드하고 푸시 [!DNL Docker] 하는 데 사용됩니다.

>[!NOTE]
>
>소스 URL은 아래 설명된 단계를 완료한 후에 제공됩니다. 구성 파일은 다음 단계에 있는 후속 자습서에 [설명되어 있습니다](#next-steps).

### 소스 파일 패키징

시작 Experience Platform Data Science 작업 영역 Reference</a> 저장소에 있는 샘플 코드베이스를 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">가져옵니다.

- [Python Docker 이미지 빌드](#python-docker)
- [R Docker 이미지 빌드](#r-docker)
- [PySpark Docker 이미지 빌드](#pyspark-docker)
- [Scala (Spark) 도커 이미지 빌드](#scala-docker)

### Docker 이미지 빌드 [!DNL Python] {#python-docker}

아직 복제하지 않은 경우 다음 명령을 사용하여 로컬 시스템에 저장소 복제 [!DNL GitHub] 를 수행합니다.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리 `experience-platform-dsw-reference/recipes/python/retail`로 이동합니다. 여기에서 스크립트를 `login.sh` 찾을 수 있으며 `build.sh` Docker에 로그인하고 이미지를 빌드 [!DNL Python Docker] 하는 데 사용됩니다. Docker 자격 증명[&#128279;](#docker-based-model-authoring)이 준비되었으면 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드할 때 빌드에 대한 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 Docker 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같이 표시됩니다좋아요.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

이 URL을 복사하고 다음 단계로[&#128279;](#next-steps) 이동합니다.

### R [!DNL Docker] 이미지 빌드 {#r-docker}

아직 복제하지 않은 경우 다음 명령을 사용하여 로컬 시스템에 저장소 복제 [!DNL GitHub] 를 수행합니다.

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

복제된 저장소 내의 디렉토리 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 로 이동합니다. 여기에서 Docker에 로그인 하고 R Docker 이미지를 빌드 하는 데 사용할 파일과 `login.sh` `build.sh` 파일을 찾을 수 있습니다. Docker 자격 증명[&#128279;](#docker-based-model-authoring)이 준비되었으면 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드할 때 빌드에 대한 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 Docker 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같이 표시됩니다좋아요.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

이 URL을 복사하고 [다음 단계](#next-steps)(으)로 이동합니다.

### PySpark Docker 이미지 작성 {#pyspark-docker}

다음 명령을 사용하여 로컬 시스템에 저장소를 [!DNL GitHub] 복제하여 시작 하십시오.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리 `experience-platform-dsw-reference/recipes/pyspark/retail`로 이동합니다. 스크립트 `login.sh` `build.sh` 는 여기에 있으며 Docker에 로그인 하고 Docker 이미지를 빌드 하는 데 사용됩니다. Docker 자격 증명[&#128279;](#docker-based-model-authoring)이 준비되었으면 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 도커 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 도커 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같습니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

이 URL을 복사하고 [다음 단계](#next-steps)(으)로 이동합니다.

### Scala Docker 이미지 빌드 {#scala-docker}

터미널에서 다음 명령을 사용하여 [!DNL GitHub] 리포지토리를 로컬 시스템에 복제합니다.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

다음, 스크립트를 `login.sh` 찾을 수 있는 디렉토리 `experience-platform-dsw-reference/recipes/scala` 로 이동하고 `build.sh`. 이러한 스크립트는 Docker에 로그인 하고 Docker 이미지를 빌드 하는 데 사용됩니다. Docker 자격 증명[&#128279;](#docker-based-model-authoring)이 준비되었으면 터미널에 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>스크립트를 사용하여 `login.sh` Docker에 로그인하려고 할 때 권한 오류가 발생하면 명령을 `bash login.sh`사용해 보십시오.

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드할 때 빌드에 대한 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 Docker 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같이 표시됩니다좋아요.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

이 URL을 복사하고 다음 단계로[&#128279;](#next-steps) 이동합니다.

## 다음 단계 {#next-steps}

이 튜토리얼에서는 Recipe [!DNL Data Science Workspace]를 로 가져오기 위한 전제 조건 단계인 Recipe로 소스 파일을 패키징하는 방법에 대해 설명했습니다. 이제 해당 이미지 URL와 함께 Azure Container Registry에 Docker 이미지가 있어야 합니다. 이제 패키지된 레서피 [!DNL Data Science Workspace]가져오기에 대한 튜토리얼을 시작할 준비가 되었습니다. 시작하려면 아래 튜토리얼 링크 중 하나를 선택하십시오.

- [UI에서 패키지된 레서피 가져오기](./import-packaged-recipe-ui.md)
- [API를 사용하여 패키지된 레시피 가져오기](./import-packaged-recipe-api.md)
