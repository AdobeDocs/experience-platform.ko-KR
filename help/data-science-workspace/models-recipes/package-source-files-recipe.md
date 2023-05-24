---
keywords: Experience Platform;패키지 소스 파일;Data Science Workspace;인기 항목;Docker;Docker 이미지
solution: Experience Platform
title: 소스 파일을 레시피에 패키징
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 아카이브 파일로 패키징하는 방법에 대한 지침을 제공합니다. 이 파일은 UI에서 또는 API를 사용하여 레시피 가져오기 워크플로우를 따라 Adobe Experience Platform Data Science Workspace에서 레시피를 만드는 데 사용할 수 있습니다.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# 소스 파일을 레시피에 패키징

이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 Adobe Experience Platform에서 레시피를 만드는 데 사용할 수 있는 아카이브 파일로 패키징하는 방법에 대한 지침을 제공합니다 [!DNL Data Science Workspace] ui에서 또는 API를 사용하여 레시피 가져오기 워크플로우를 따릅니다.

이해할 개념:

- **레서피**: 레시피는 모델 사양에 대한 Adobe의 용어이며 훈련된 모델을 구축하고 실행하여 특정 비즈니스 문제를 해결하는 데 필요한 특정 머신 러닝, 인공 지능 알고리즘 또는 알고리즘, 처리 논리 및 구성의 앙상블을 나타내는 최상위 컨테이너입니다.
- **소스 파일**: 레시피의 논리가 포함된 프로젝트의 개별 파일입니다.

## 사전 요구 사항

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 레시피 만들기

레시피 만들기는 소스 파일을 패키징하여 아카이브 파일을 만드는 것으로 시작합니다. 소스 파일은 당면한 특정 문제를 해결하는 데 사용되는 머신 러닝 논리 및 알고리즘을 정의하며, 다음 중 하나로 작성됩니다 [!DNL Python], R, PySpark 또는 Scala. 빌드된 아카이브 파일은 도커 이미지 형식을 취합니다. 빌드되면 패키지된 아카이브 파일을으로 가져옵니다. [!DNL Data Science Workspace] 레시피를 만들려면 [UI에서](./import-packaged-recipe-ui.md) 또는 [api 사용](./import-packaged-recipe-api.md).

### 도커 기반 모델 작성 {#docker-based-model-authoring}

Docker 이미지를 사용하면 개발자가 라이브러리 및 기타 종속성과 같이 응용 프로그램에 필요한 모든 부분을 패키지화하여 하나의 패키지로 제공할 수 있습니다.

빌드된 도커 이미지는 레시피 만들기 워크플로 중에 제공된 자격 증명을 사용하여 Azure Container Registry에 푸시됩니다.

Azure Container Registry 자격 증명을 얻으려면 로그인하십시오. [Adobe Experience Platform](https://platform.adobe.com). 왼쪽 탐색 열에서 다음 위치로 이동합니다. **[!UICONTROL 워크플로]**. 선택 **[!UICONTROL 레시피 가져오기]** 뒤에 선택 **[!UICONTROL 시작]**. 참조하려면 아래 스크린샷을 참조하십시오.

![](../images/models-recipes/package-source-files/import.png)

다음 **[!UICONTROL 구성]** 페이지가 열립니다. 적절한 항목 제공 **[!UICONTROL 레시피 이름]**&#x200B;예를 들어 &quot;소매 판매 레시피&quot;와 같은 경우 원할 경우 설명 또는 설명서 URL을 제공하십시오. 완료되면 다음을 클릭합니다. **[!UICONTROL 다음]**.

![](../images/models-recipes/package-source-files/configure.png)

적절한 항목 선택 *런타임*&#x200B;을(를) 클릭한 다음 을(를) 선택합니다 **[!UICONTROL 분류]** 대상 *유형*. 완료되면 Azure 컨테이너 레지스트리 자격 증명이 생성됩니다.

>[!NOTE]
>
>*유형* 레시피가 설계된 머신 러닝 문제의 클래스이며, 교육 실행 평가를 맞춤화하기 위해 교육 후에 사용됩니다.

>[!TIP]
>
>- 대상 [!DNL Python] 레서피 선택 **[!UICONTROL Python]** 런타임.
>- R 레시피의 경우 **[!UICONTROL R]** 런타임.
>- PySpark 레시피의 경우 **[!UICONTROL PySparc]** 런타임. 아티팩트 유형이 자동으로 채워집니다.
>- Scala 레시피의 경우 **[!UICONTROL 스파크]** 런타임. 아티팩트 유형이 자동으로 채워집니다.


![](../images/models-recipes/package-source-files/docker-creds.png)

Docker 호스트, 사용자 이름 및 암호 값을 확인합니다. 빌드하고 푸시하는 데 사용됩니다. [!DNL Docker] 아래에 요약된 워크플로의 이미지입니다.

>[!NOTE]
>
>소스 URL은 아래에 설명된 단계를 완료한 후 제공됩니다. 구성 파일에 대해서는 다음에 나오는 자습서에 설명되어 있습니다. [다음 단계](#next-steps).

### 소스 파일 패키징

에 있는 샘플 코드베이스를 가져와 시작합니다. <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform 데이터 과학 작업 영역 참조</a> 리포지토리.

- [Python Docker 이미지 빌드](#python-docker)
- [R 도커 이미지 빌드](#r-docker)
- [PySpark Docker 이미지 작성](#pyspark-docker)
- [Scala (Spark) 도커 이미지 빌드](#scala-docker)

### 빌드 [!DNL Python] 도커 이미지 {#python-docker}

아직 복제하지 않았다면 [!DNL GitHub] 다음 명령을 사용하여 로컬 시스템에 리포지토리:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리로 이동합니다. `experience-platform-dsw-reference/recipes/python/retail`. 여기에서 스크립트를 찾을 수 있습니다. `login.sh` 및 `build.sh` Docker에 로그인하고 를 빌드하는 데 사용됩니다. [!DNL Python Docker] 이미지. 다음 항목이 있는 경우 [도커 자격 증명](#docker-based-model-authoring) 준비, 다음 명령을 순서대로 입력합니다.

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
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

이 URL을 복사하고 다음으로 이동 [다음 단계](#next-steps).

### 빌드 R [!DNL Docker] 이미지 {#r-docker}

아직 복제하지 않았다면 [!DNL GitHub] 다음 명령을 사용하여 로컬 시스템에 리포지토리:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리로 이동합니다. `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 복제된 저장소 내. 여기에서 파일을 찾을 수 있습니다. `login.sh` 및 `build.sh` Docker에 로그인하고 R Docker 이미지를 빌드하는 데 사용할 수 있습니다. 다음 항목이 있는 경우 [도커 자격 증명](#docker-based-model-authoring) 준비, 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 도커 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 도커 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같습니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

이 URL을 복사하고 다음으로 이동 [다음 단계](#next-steps).

### PySpark Docker 이미지 작성 {#pyspark-docker}

다음을 복제하여 시작 [!DNL GitHub] 다음 명령을 사용하여 로컬 시스템에 리포지토리:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

디렉토리로 이동합니다. `experience-platform-dsw-reference/recipes/pyspark/retail`. 스크립트 `login.sh` 및 `build.sh` 는 여기에 있으며 Docker에 로그인하고 Docker 이미지를 빌드하는 데 사용됩니다. 다음 항목이 있는 경우 [도커 자격 증명](#docker-based-model-authoring) 준비, 다음 명령을 순서대로 입력합니다.

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

이 URL을 복사하고 다음으로 이동 [다음 단계](#next-steps).

### Scala Docker 이미지 빌드 {#scala-docker}

다음을 복제하여 시작 [!DNL GitHub] 터미널에서 다음 명령을 사용하여 로컬 시스템에 리포지토리:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

그런 다음 디렉터리로 이동합니다 `experience-platform-dsw-reference/recipes/scala` 스크립트 찾기 위치 `login.sh` 및 `build.sh`. 이러한 스크립트는 Docker에 로그인하고 Docker 이미지를 빌드하는 데 사용됩니다. 다음 항목이 있는 경우 [도커 자격 증명](#docker-based-model-authoring) 준비, 다음 명령을 순서대로 터미널에 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>를 사용하여 Docker에 로그인하려고 할 때 권한 오류가 발생하는 경우 `login.sh` 스크립트, 명령을 사용해 보십시오. `bash login.sh`.

로그인 스크립트를 실행할 때 도커 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 도커 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 도커 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같습니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

이 URL을 복사하고 다음으로 이동 [다음 단계](#next-steps).

## 다음 단계 {#next-steps}

이 튜토리얼에서는 소스 파일을 레시피로 패키지하는 방법에 대해 알아보았습니다. 레시피를 가져오기 위한 사전 요구 사항 단계입니다. [!DNL Data Science Workspace]. 이제 Azure Container Registry에 해당 이미지 URL과 함께 도커 이미지가 있어야 합니다. 이제 패키지된 레시피를 로 가져오는 방법에 대한 자습서를 시작할 준비가 되었습니다. [!DNL Data Science Workspace]. 시작하려면 아래 튜토리얼 링크 중 하나를 선택하십시오.

- [UI에서 패키지된 레시피 가져오기](./import-packaged-recipe-ui.md)
- [API를 사용하여 패키지된 레시피 가져오기](./import-packaged-recipe-api.md)
