---
keywords: Experience Platform;소스 파일 패키지;Data Science Workspace;인기 항목;Docker;docker 이미지
solution: Experience Platform
title: 배합식에 소스 파일 패키지
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 아카이브 파일로 패키지하는 방법에 대한 지침을 제공합니다. 이 파일은 UI의 레서피 가져오기 워크플로우에 따라 또는 API를 사용하여 Adobe Experience Platform Data Science Workspace에서 레서피를 만드는 데 사용할 수 있습니다.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# 배합식에 소스 파일 패키지

이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 아카이브 파일로 패키지하는 방법에 대한 지침을 제공하며 이 파일을 Adobe Experience Platform에서 레서피를 만드는 데 사용할 수 있습니다 [!DNL Data Science Workspace] 레서피 가져오기 워크플로우에 따라 UI나 API를 사용합니다.

이해할 개념:

- **레서피**: 레서피는 Adobe의 모델 사양 용어이며, 특정 기계 학습, 인공 지능 알고리즘 또는 알고리즘 앙상블, 처리 논리 및 구성 등을 나타내어, 숙련된 모델을 구축하고 실행하는 데 필요한 구성을 나타내어 특정 비즈니스 문제를 해결하는 데 도움이 되는 최상위 컨테이너입니다.
- **소스 파일**: 레서피에 대한 논리를 포함하는 프로젝트의 개별 파일입니다.

## 전제 조건

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 레서피 만들기

레서피 생성은 아카이브 파일을 만들기 위해 소스 파일을 패키징하는 것으로 시작합니다. 소스 파일은 특정 문제를 해결하는 데 사용되는 기계 학습 논리와 알고리즘을 정의하고 다음 중 하나로 작성됩니다 [!DNL Python], R, PySpark 또는 Scala. 작성된 아카이브 파일은 Docker 이미지를 사용합니다. 빌드되면 패키지화된 아카이브 파일을 [!DNL Data Science Workspace] 조리법을 만들다 [UI에서](./import-packaged-recipe-ui.md) 또는 [api 사용](./import-packaged-recipe-api.md).

### Docker 기반 모델 작성 {#docker-based-model-authoring}

Docker 이미지를 사용하면 개발자가 라이브러리 및 기타 종속성 등 필요한 모든 부분으로 애플리케이션을 패키징하여 하나의 패키지로 배포할 수 있습니다.

작성된 Docker 이미지가 레서피 만들기 워크플로우 중에 제공한 자격 증명을 사용하여 Azure 컨테이너 레지스트리에 푸시됩니다.

Azure 컨테이너 레지스트리 자격 증명을 가져오려면 로그인하십시오 [Adobe Experience Platform](https://platform.adobe.com). 왼쪽 탐색 열에서 **[!UICONTROL 워크플로우]**. 선택 **[!UICONTROL 레서피 가져오기]** 선택한 후 **[!UICONTROL Launch]**. 참조하려면 아래 스크린샷을 참조하십시오.

![](../images/models-recipes/package-source-files/import.png)

다음 **[!UICONTROL 구성]** 페이지가 열립니다. 적절한 **[!UICONTROL 레서피 이름]**&#x200B;예를 들어, &quot;소매 영업 레서피&quot;와 선택적으로 설명 또는 설명서 URL을 제공합니다. 완료되면 를 클릭합니다. **[!UICONTROL 다음]**.

![](../images/models-recipes/package-source-files/configure.png)

적절한 *런타임*&#x200B;를 선택한 다음 **[!UICONTROL 분류]** 대상 *유형*. 완료되면 Azure 컨테이너 레지스트리 자격 증명이 생성됩니다.

>[!NOTE]
>
>*유형* 은 배합식이 설계되고 교육 후에 사용되는 기계 학습 문제의 클래스입니다. 이 경우 교육 실행 평가를 위한 것입니다.

>[!TIP]
>
>- 대상 [!DNL Python] 레서피 선택 **[!UICONTROL 파이톤]** 런타임.
>- R 레서피 의 경우 **[!UICONTROL R]** 런타임.
>- PySpark 레서피의 경우 **[!UICONTROL PySpark]** 런타임. 객체 유형이 자동으로 채워집니다.
>- Scala 레서피의 경우 **[!UICONTROL 스파크]** 런타임. 객체 유형이 자동으로 채워집니다.


![](../images/models-recipes/package-source-files/docker-creds.png)

Docker 호스트, 사용자 이름 및 암호 값을 확인합니다. 이러한 항목은 를 빌드하고 푸시하는 데 사용됩니다 [!DNL Docker] 아래에 요약된 워크플로우에 있는 이미지입니다.

>[!NOTE]
>
>소스 URL은 아래 설명된 단계를 완료한 후 제공됩니다. 구성 파일은 다음에 있는 자습서에서 설명합니다. [다음 단계](#next-steps).

### 소스 파일 패키지

다음에서 찾은 샘플 코드 베이스를 가져와서 시작합니다 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform 데이터 과학 작업 공간 참조</a> 저장소.

- [Python Docker 이미지 작성](#python-docker)
- [R Docker 이미지 작성](#r-docker)
- [PySpark Docker 이미지 작성](#pyspark-docker)
- [Scala(Spark) Docker 이미지 작성](#scala-docker)

### 빌드 [!DNL Python] Docker 이미지 {#python-docker}

아직 복제하지 않았다면 [!DNL GitHub] 다음 명령을 사용하여 로컬 시스템에 저장소 추가:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리로 이동합니다 `experience-platform-dsw-reference/recipes/python/retail`. 여기에서 스크립트를 찾을 수 있습니다 `login.sh` 및 `build.sh` Docker에 로그인하고 [!DNL Python Docker] 이미지. 만약 [Docker 자격 증명](#docker-based-model-authoring) 준비, 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 Docker 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

이 URL을 복사하여 [다음 단계](#next-steps).

### 빌드 R [!DNL Docker] 이미지 {#r-docker}

아직 복제하지 않았다면 [!DNL GitHub] 다음 명령을 사용하여 로컬 시스템에 저장소 추가:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리로 이동합니다 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 복제된 저장소 내에 있어야 합니다. 여기서 파일을 찾을 수 있습니다 `login.sh` 및 `build.sh` Docker에 로그인하고 R Docker 이미지를 작성하는 데 사용할 수 있는 페이지입니다. 만약 [Docker 자격 증명](#docker-based-model-authoring) 준비, 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 Docker 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

이 URL을 복사하여 [다음 단계](#next-steps).

### PySpark Docker 이미지 작성 {#pyspark-docker}

먼저 을 복제하십시오 [!DNL GitHub] 다음 명령을 사용하여 로컬 시스템에 저장소 추가:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리로 이동합니다 `experience-platform-dsw-reference/recipes/pyspark/retail`. 스크립트 `login.sh` 및 `build.sh` 은 여기에서 Docker에 로그인하고 Docker 이미지를 만드는 데 사용됩니다. 만약 [Docker 자격 증명](#docker-based-model-authoring) 준비, 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 Docker 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

이 URL을 복사하여 [다음 단계](#next-steps).

### Scala Docker 이미지 작성 {#scala-docker}

먼저 을 복제하십시오 [!DNL GitHub] 터미널의 다음 명령을 사용하여 로컬 시스템에 저장소

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

다음으로 디렉토리로 이동합니다 `experience-platform-dsw-reference/recipes/scala` 스크립트를 찾을 수 있는 위치 `login.sh` 및 `build.sh`. 이러한 스크립트는 Docker에 로그인하고 Docker 이미지를 작성하는 데 사용됩니다. 만약 [Docker 자격 증명](#docker-based-model-authoring) 준비 완료, 터미널에 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>을 사용하여 Docker에 로그인하려고 할 때 권한 오류가 발생하는 경우 `login.sh` 스크립트, 명령을 사용해 보십시오. `bash login.sh`.

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 Docker 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

이 URL을 복사하여 [다음 단계](#next-steps).

## 다음 단계 {#next-steps}

이 자습서에서는 소스 파일을 레서피로 패키지하는 작업을 수행했으며, 레서피를 로 가져오는 사전 요구 단계입니다. [!DNL Data Science Workspace]. 이제 Azure 컨테이너 레지스트리에 해당 이미지 URL과 함께 Docker 이미지가 있어야 합니다. 이제 패키지된 레시피를 로 가져오는 방법에 대한 자습서를 시작할 준비가 되었습니다. [!DNL Data Science Workspace]. 시작하려면 아래 자습서 링크 중 하나를 선택하십시오.

- [UI에서 패키지된 레서피 가져오기](./import-packaged-recipe-ui.md)
- [API를 사용하여 패키지된 레서피 가져오기](./import-packaged-recipe-api.md)
