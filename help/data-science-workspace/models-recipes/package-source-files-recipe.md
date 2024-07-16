---
keywords: Experience Platform;패키지 소스 파일;Data Science Workspace;인기 주제;도커;도커 이미지
solution: Experience Platform
title: 레시피에 Source 파일 패키징
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 아카이브 파일로 패키징하는 방법에 대한 지침을 제공합니다. 이 파일은 UI에서 또는 API를 사용하여 레시피 가져오기 워크플로우를 따라 Adobe Experience Platform Data Science Workspace에서 레시피를 만드는 데 사용할 수 있습니다.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# 소스 파일을 레시피로 패키징

이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 보관 파일로 패키징하는 방법에 대한 지침을 제공합니다. 이 파일은 UI에서 또는 API를 사용하여 레시피 가져오기 워크플로우를 따라 Adobe Experience Platform [!DNL Data Science Workspace]에서 레시피를 만드는 데 사용할 수 있습니다.

이해할 개념:

- **레시피**: 레시피는 모델 사양에 대한 Adobe의 용어이며, 훈련된 모델을 만들고 실행하여 특정 비즈니스 문제를 해결하는 데 필요한 특정 기계 학습, 인공 지능 알고리즘 또는 알고리즘, 처리 논리 및 구성의 앙상블을 나타내는 최상위 컨테이너입니다.
- **Source 파일**: 레시피의 논리가 들어 있는 프로젝트의 개별 파일입니다.

## 전제 조건

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 레시피 만들기

레시피 만들기는 소스 파일을 패키징하여 아카이브 파일을 만드는 것으로 시작합니다. Source 파일은 특정 문제를 해결하는 데 사용되는 머신 러닝 논리 및 알고리즘을 정의하며 [!DNL Python], R, PySpark 또는 Scala로 작성됩니다. 빌드된 아카이브 파일은 도커 이미지 형식을 취합니다. 빌드되면 패키지된 보관 파일을 [!DNL Data Science Workspace](으)로 가져와서 UI에서 [레시피를 만들거나](./import-packaged-recipe-ui.md) 또는 [API를 사용](./import-packaged-recipe-api.md)합니다.

### 도커 기반 모델 작성 {#docker-based-model-authoring}

Docker 이미지를 사용하면 개발자가 라이브러리 및 기타 종속성과 같이 응용 프로그램에 필요한 모든 부분을 패키지화하여 하나의 패키지로 제공할 수 있습니다.

빌드된 도커 이미지는 레시피 만들기 워크플로 중에 제공된 자격 증명을 사용하여 Azure Container Registry에 푸시됩니다.

Azure Container Registry 자격 증명을 얻으려면 [Adobe Experience Platform](https://platform.adobe.com)에 로그인하십시오. 왼쪽 탐색 열에서 **[!UICONTROL 워크플로]**(으)로 이동합니다. **[!UICONTROL 레시피 가져오기]**&#x200B;를 선택한 후 **[!UICONTROL 시작]**&#x200B;을 선택하십시오. 참조하려면 아래 스크린샷을 참조하십시오.

![](../images/models-recipes/package-source-files/import.png)

**[!UICONTROL 구성]** 페이지가 열립니다. 적절한 **[!UICONTROL 레시피 이름]**(예: &quot;소매 판매 레시피&quot;를 입력하고 선택적으로 설명 또는 설명서 URL을 제공하십시오. 완료되면 **[!UICONTROL 다음]**&#x200B;을 클릭하세요.

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
>- Scala 레시피의 경우 **[!UICONTROL Spark]** 런타임을 선택하십시오. 아티팩트 유형이 자동으로 채워집니다.

![](../images/models-recipes/package-source-files/docker-creds.png)

Docker 호스트, 사용자 이름 및 암호 값을 확인합니다. 아래 요약된 워크플로에서 [!DNL Docker] 이미지를 빌드하고 푸시하는 데 사용됩니다.

>[!NOTE]
>
>Source URL은 아래에 설명된 단계를 완료한 후 제공됩니다. 구성 파일은 [다음 단계](#next-steps)에 있는 후속 튜토리얼에 설명되어 있습니다.

### 소스 파일 패키징

<a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform 데이터 과학 Workspace 참조</a> 리포지토리에 있는 샘플 코드베이스를 가져와 시작합니다.

- [Python Docker 이미지 빌드](#python-docker)
- [R 도커 이미지 빌드](#r-docker)
- [PySpark Docker 이미지 작성](#pyspark-docker)
- [Scala (Spark) 도커 이미지 빌드](#scala-docker)

### [!DNL Python] 도커 이미지 빌드 {#python-docker}

이 작업을 수행하지 않은 경우 다음 명령을 사용하여 [!DNL GitHub] 리포지토리를 로컬 시스템에 복제합니다.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

`experience-platform-dsw-reference/recipes/python/retail` 디렉터리로 이동합니다. 여기에는 Docker에 로그인하고 [!DNL Python Docker] 이미지를 빌드하는 데 사용되는 `login.sh` 및 `build.sh` 스크립트가 있습니다. [Docker 자격 증명](#docker-based-model-authoring)이 준비된 경우 다음 명령을 순서대로 입력하십시오.

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

이 URL을 복사하고 [다음 단계](#next-steps)(으)로 이동합니다.

### R [!DNL Docker] 이미지 작성 {#r-docker}

이 작업을 수행하지 않은 경우 다음 명령을 사용하여 [!DNL GitHub] 리포지토리를 로컬 시스템에 복제합니다.

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

복제된 리포지토리 내의 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 디렉터리로 이동합니다. 여기에는 Docker에 로그인하고 R Docker 이미지를 빌드하는 데 사용할 파일 `login.sh` 및 `build.sh`이(가) 있습니다. [Docker 자격 증명](#docker-based-model-authoring)이 준비된 경우 다음 명령을 순서대로 입력하십시오.

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

이 URL을 복사하고 [다음 단계](#next-steps)(으)로 이동합니다.

### PySpark Docker 이미지 작성 {#pyspark-docker}

다음 명령을 사용하여 [!DNL GitHub] 리포지토리를 로컬 시스템에 복제합니다.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

`experience-platform-dsw-reference/recipes/pyspark/retail` 디렉터리로 이동합니다. `login.sh` 및 `build.sh` 스크립트가 여기에 있으며 Docker에 로그인하고 Docker 이미지를 빌드하는 데 사용됩니다. [Docker 자격 증명](#docker-based-model-authoring)이 준비된 경우 다음 명령을 순서대로 입력하십시오.

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

그런 다음 스크립트 `login.sh` 및 `build.sh`을(를) 찾을 수 있는 `experience-platform-dsw-reference/recipes/scala` 디렉터리로 이동합니다. 이러한 스크립트는 Docker에 로그인하고 Docker 이미지를 빌드하는 데 사용됩니다. [Docker 자격 증명](#docker-based-model-authoring)이 준비된 경우 터미널에 다음 명령을 순서대로 입력하십시오.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>`login.sh` 스크립트를 사용하여 Docker에 로그인할 때 권한 오류가 발생하면 `bash login.sh` 명령을 사용해 보십시오.

로그인 스크립트를 실행할 때 도커 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드 시 빌드에 도커 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에 도커 소스 파일 URL이 제공됩니다. 이 특정 예제의 경우 다음과 같습니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

이 URL을 복사하고 [다음 단계](#next-steps)(으)로 이동합니다.

## 다음 단계 {#next-steps}

이 튜토리얼에서는 소스 파일을 레시피로 패키지하는 방법에 대해 살펴보았습니다. 레시피를 [!DNL Data Science Workspace](으)로 가져오기 위한 필수 조건 단계입니다. 이제 Azure Container Registry에 해당 이미지 URL과 함께 도커 이미지가 있어야 합니다. 이제 패키지된 레시피를 [!DNL Data Science Workspace](으)로 가져오는 방법에 대한 자습서를 시작할 준비가 되었습니다. 시작하려면 아래 튜토리얼 링크 중 하나를 선택하십시오.

- [UI에서 패키지된 레시피 가져오기](./import-packaged-recipe-ui.md)
- [API를 사용하여 패키지된 레시피 가져오기](./import-packaged-recipe-api.md)
