---
keywords: Experience Platform;패키지 소스 파일;데이터 과학 작업 공간;인기 항목;문서;문서 이미지
solution: Experience Platform
title: 소스 파일을 레서피로 패키지화
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 보관 파일로 패키지하는 방법에 대한 지침을 제공합니다. 이 파일은 UI에서 또는 API를 사용하여 레서피 가져오기 워크플로우에 따라 Adobe Experience Platform Data Science Workspace에서 레서피를 만드는 데 사용할 수 있습니다.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# 소스 파일을 레서피에 패키지화

이 자습서에서는 제공된 소매 판매 샘플 소스 파일을 보관 파일로 패키지하는 방법에 대한 지침을 제공합니다. 이 지침은 UI의 레서피 가져오기 작업 과정에 따라 또는 API를 사용하여 Adobe Experience Platform [!DNL Data Science Workspace]에서 레서피를 만드는 데 사용할 수 있습니다.

이해할 개념:

- **레서피**:레서피는 Adobe(Model) 사양에서 사용되는 용어로, 특정 기계 학습, 인공 지능(AI) 알고리즘 또는 알고리즘의 조합, 처리 논리 및 구성을 나타내는 최상위 컨테이너로, 훈련된 모델을 구축 및 실행하여 특정 비즈니스 문제를 해결하는 데 필요합니다.
- **소스 파일**:레서피에 대한 논리가 포함된 프로젝트의 개별 파일입니다.

## 전제 조건

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 레서피 제작

레서피 생성은 소스 파일을 패키징하여 아카이브 파일을 작성하는 것부터 시작합니다. 소스 파일은 특정 문제를 해결하는 데 사용되는 기계 학습 로직과 알고리즘을 정의하며 [!DNL Python], R, PySpark 또는 Scala로 작성됩니다. 작성된 아카이브 파일은 Docker 이미지 형식을 취합니다. 일단 빌드되면 패키지된 아카이브 파일을 [!DNL Data Science Workspace]으로 가져와 API](./import-packaged-recipe-api.md)를 사용하여 UI](./import-packaged-recipe-ui.md) 또는 [에서 레서피 [를 만듭니다.

### 문서 기반 모델 작성 {#docker-based-model-authoring}

개발자는 Docker 이미지를 사용하여 라이브러리 및 기타 종속성 등 필요한 모든 부분으로 애플리케이션을 패키지하여 하나의 패키지로 내보낼 수 있습니다.

레서피 만들기 작업 과정 중에 제공된 자격 증명을 사용하여 빌드된 Docker 이미지가 Azure 컨테이너 레지스트리에 푸시됩니다.

Azure 컨테이너 레지스트리 자격 증명을 얻으려면 [Adobe Experience Platform](https://platform.adobe.com)에 로그인하십시오. 왼쪽 탐색 열에서 **[!UICONTROL Workflows]**&#x200B;으로 이동합니다. **[!UICONTROL Import Recipe]**&#x200B;을 선택하고 **[!UICONTROL Launch]**&#x200B;을 선택합니다. 자세한 내용은 아래 스크린샷을 참조하십시오.

![](../images/models-recipes/package-source-files/import.png)

**[!UICONTROL Configure]** 페이지가 열립니다. 적절한 **[!UICONTROL Recipe Name]**(예: &quot;소매 판매 레서피&quot;)을 제공하고 선택적으로 설명 또는 문서 URL을 제공합니다. 완료되면 **[!UICONTROL Next]**&#x200B;을 클릭합니다.

![](../images/models-recipes/package-source-files/configure.png)

적절한 *Runtime*&#x200B;을 선택한 다음 *유형*&#x200B;에 대해 **[!UICONTROL Classification]**&#x200B;를 선택합니다. Azure 컨테이너 레지스트리 자격 증명이 완료되면 생성됩니다.

>[!NOTE]
>
>*Typein* 은 레서피가 디자인되고 교육 실행 평가를 위한 교육 후에 사용되는 기계 학습 문제 클래스입니다.

>[!TIP]
>
>- [!DNL Python] 레서피의 경우 **[!UICONTROL Python]** 런타임을 선택합니다.
>- R 레서피의 경우 **[!UICONTROL R]** 런타임을 선택합니다.
>- PySpark 레서피의 경우 **[!UICONTROL PySpark]** 런타임을 선택합니다. 가공물 유형이 자동으로 채워집니다.
>- Scala 레서피의 경우 **[!UICONTROL Spark]** 런타임을 선택합니다. 가공물 유형이 자동으로 채워집니다.


![](../images/models-recipes/package-source-files/docker-creds.png)

Docker 호스트, 사용자 이름 및 암호 값을 확인합니다. 이러한 이미지는 아래 나와 있는 워크플로우에서 [!DNL Docker] 이미지를 빌드하고 푸시하는 데 사용됩니다.

>[!NOTE]
>
>소스 URL은 아래 설명된 단계를 완료한 후 제공됩니다. 구성 파일은 [다음 단계](#next-steps)에 있는 후속 자습서에서 설명합니다.

### 소스 파일 패키지

먼저 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform 데이터 과학 작업 공간 참조</a> 저장소에 있는 샘플 코드베이스를 입수합니다.

- [Python Docker 이미지 만들기](#python-docker)
- [R Docker 이미지 만들기](#r-docker)
- [PySpark Docker 이미지 제작](#pyspark-docker)
- [Build Scala (Spark) Docker 이미지](#scala-docker)

### [!DNL Python] Docker 이미지 {#python-docker} 만들기

이렇게 하지 않은 경우 다음 명령을 사용하여 [!DNL GitHub] 저장소를 로컬 시스템에 복제합니다.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

`experience-platform-dsw-reference/recipes/python/retail` 디렉토리로 이동합니다. 여기에서 Docker에 로그인하고 [!DNL Python Docker] 이미지를 만드는 데 사용되는 스크립트 `login.sh` 및 `build.sh`을(를) 찾을 수 있습니다. [Docker 자격 증명](#docker-based-model-authoring) 준비가 되었으면 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드할 때 빌드에 대한 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에서 Docker 소스 파일 URL이 제공됩니다. 이 특정 예에서는 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

이 URL을 복사하고 [다음 단계](#next-steps)로 이동합니다.

### 빌드 R [!DNL Docker] 이미지 {#r-docker}

이렇게 하지 않은 경우 다음 명령을 사용하여 [!DNL GitHub] 저장소를 로컬 시스템에 복제합니다.

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

복제된 저장소 내의 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 디렉토리로 이동합니다. 여기에서 Docker에 로그인하고 R Docker 이미지를 만드는 데 사용할 `login.sh` 및 `build.sh` 파일을 찾을 수 있습니다. [Docker 자격 증명](#docker-based-model-authoring) 준비가 되었으면 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드할 때 빌드에 대한 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에서 Docker 소스 파일 URL이 제공됩니다. 이 특정 예에서는 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

이 URL을 복사하고 [다음 단계](#next-steps)로 이동합니다.

### PySpark Docker 이미지 만들기 {#pyspark-docker}

다음 명령을 사용하여 [!DNL GitHub] 저장소를 로컬 시스템에 복제하여 시작합니다.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

`experience-platform-dsw-reference/recipes/pyspark/retail` 디렉토리로 이동합니다. `login.sh` 및 `build.sh` 스크립트는 여기에 있으며 Docker에 로그인하고 Docker 이미지를 만드는 데 사용됩니다. [Docker 자격 증명](#docker-based-model-authoring) 준비가 되었으면 다음 명령을 순서대로 입력합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드할 때 빌드에 대한 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에서 Docker 소스 파일 URL이 제공됩니다. 이 특정 예에서는 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

이 URL을 복사하고 [다음 단계](#next-steps)로 이동합니다.

### Scala Docker 이미지 {#scala-docker} 만들기

터미널에서 다음 명령을 사용하여 [!DNL GitHub] 저장소를 로컬 시스템에 복제하여 시작합니다.

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

그런 다음 `experience-platform-dsw-reference/recipes/scala` 디렉토리로 이동하여 `login.sh` 및 `build.sh` 스크립트를 찾을 수 있습니다. 이러한 스크립트는 Docker에 로그인하고 Docker 이미지를 작성하는 데 사용됩니다. [Docker 자격 증명](#docker-based-model-authoring)이(가) 준비되었으면 다음 명령을 입력하여 터미널을 시작합니다.

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>`login.sh` 스크립트를 사용하여 Docker에 로그인하려고 할 때 권한 오류가 발생하는 경우 `bash login.sh` 명령을 사용해 보십시오.

로그인 스크립트를 실행할 때 Docker 호스트, 사용자 이름 및 암호를 제공해야 합니다. 빌드할 때 빌드에 대한 Docker 호스트 및 버전 태그를 제공해야 합니다.

빌드 스크립트가 완료되면 콘솔 출력에서 Docker 소스 파일 URL이 제공됩니다. 이 특정 예에서는 다음과 같이 표시됩니다.

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

이 URL을 복사하고 [다음 단계](#next-steps)로 이동합니다.

## 다음 단계 {#next-steps}

이 자습서에서는 소스 파일을 레서피로 패키징했습니다. 레서피를 [!DNL Data Science Workspace]으로 가져오기 위한 전제 조건 단계입니다. 이제 해당 이미지 URL과 함께 Azure 컨테이너 레지스트리에 Docker 이미지가 있어야 합니다. 이제 패키지화된 레서피를 [!DNL Data Science Workspace]으로 가져오는 방법에 대한 자습서를 시작할 준비가 되었습니다. 시작하려면 아래 자습서 링크 중 하나를 선택하십시오.

- [UI에서 패키지된 레서피 가져오기](./import-packaged-recipe-ui.md)
- [API를 사용하여 패키지된 레서피 가져오기](./import-packaged-recipe-api.md)
