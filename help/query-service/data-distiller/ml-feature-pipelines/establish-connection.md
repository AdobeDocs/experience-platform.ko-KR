---
title: Jupyter Notebook에서 Data Distiller에 연결
description: Jupyter Notebook에서 Data Distiller에 연결하는 방법을 알아봅니다.
source-git-commit: 60c5a624bfbe88329ab3e12962f129f03966ce77
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Jupyter Notebook에서 Data Distiller에 연결

고가치 고객 경험 데이터를 사용하여 머신 러닝 파이프라인을 보강하려면 먼저 다음에서 데이터 Distiller에 연결해야 합니다. [!DNL Jupyter Notebooks]. 이 문서에서는에서 Data Distiller에 연결하는 단계를 다룹니다. [!DNL Python] 기계 학습 환경의 전자 필기장입니다.

## 시작하기

이 안내서에서는 사용자가 대화형에 익숙하다고 가정합니다 [!DNL Python] notebooks 및 notebook 환경에 대한 액세스 권한이 있습니다. 노트북은 클라우드 기반 머신 러닝 환경 내에서 호스팅되거나 [[!DNL Jupyter Notebook]](https://jupyter.org/).

### 연결 자격 증명 가져오기 {#obtain-credentials}

Data Distiller 및 기타 Adobe Experience Platform 서비스에 연결하려면 Experience Platform API 자격 증명이 필요합니다. API 자격 증명은에서 만들 수 있습니다.  [Adobe Developer 콘솔](https://developer.adobe.com/console/home) 개발자가 Experience Platform에 액세스할 수 있는 사람. 특히 데이터 과학 워크플로에 대한 Oauth2 API 자격 증명을 만들고 조직의 Adobe 시스템 관리자가 적절한 권한이 있는 역할에 자격 증명을 할당하도록 하는 것이 좋습니다.

다음을 참조하십시오 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) api 자격 증명을 만들고 필요한 권한을 얻는 방법에 대한 자세한 지침은 를 참조하십시오.

데이터 과학에 권장되는 권한은 다음과 같습니다.

- 데이터 과학에 사용될 샌드박스(일반적으로 `prod`)
- 데이터 모델링: [!UICONTROL 스키마 관리]
- 데이터 관리: [!UICONTROL 데이터 세트 관리]
- 데이터 수집: [!UICONTROL 소스 보기]
- 대상: [!UICONTROL 데이터 세트 대상 관리 및 활성화]
- 쿼리 서비스: [!UICONTROL 쿼리 관리]

기본적으로 역할(및 해당 역할에 할당된 API 자격 증명)은 레이블이 지정된 데이터에 액세스하지 못하도록 차단됩니다. 조직의 데이터 거버넌스 정책에 따라 시스템 관리자는 데이터 과학 사용에 적절하다고 판단되는 레이블이 지정된 특정 데이터에 대한 액세스 권한을 역할에 부여할 수 있습니다. 플랫폼 고객은 관련 규정 및 조직 정책을 준수하기 위해 레이블 액세스 및 정책을 적절하게 관리할 책임이 있습니다.

### 자격 증명을 별도의 구성 파일에 저장 {#store-credentials}

자격 증명을 안전하게 유지하려면 코드에 직접 자격 증명 정보를 쓰지 않는 것이 좋습니다. 대신 자격 증명 정보를 별도의 구성 파일에 보관하고 Experience Platform 및 Data Distiller에 연결하는 데 필요한 값을 읽습니다.

예를 들어 다음 파일을 만들 수 있습니다. `config.ini` 및 에는 다음 정보(세션 간에 저장하는 데 유용한 데이터 세트 ID와 같은 다른 정보와 함께)가 포함되어 있습니다.

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

그런 다음 노트북에서 다음을 사용하여 자격 증명 정보를 메모리로 읽을 수 있습니다. `configParser` 표준 패키지 [!DNL Python] 라이브러리:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

그런 다음 다음과 같이 코드 내에서 자격 증명 값을 참조할 수 있습니다.

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Aepp Python 라이브러리 설치 {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) 는 Adobe에서 관리하는 오픈 소스입니다. [!DNL Python] 다른 Experience Platform 서비스에 요청할 때 Data Distiller에 연결하고 쿼리를 제출하는 함수를 제공하는 라이브러리입니다. 다음 `aepp` 라이브러리는 PostgreSQL 데이터베이스 어댑터 패키지에 종속됩니다.  `psycopg2` 대화형 데이터 Distiller 쿼리 을 사용하여 데이터 Distiller에 연결하고 Experience Platform 데이터 세트를 쿼리할 수 있습니다. `psycopg2` 단독으로, `aepp` 는 모든 Experience Platform API 서비스에 대한 요청을 수행하는 데 더 많은 편리함과 추가 기능을 제공합니다.

설치 또는 업그레이드 `aepp` 및 `psycopg2` 사용자 환경에서 다음을 사용할 수 있습니다 `%pip` 노트북의 매직 명령:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

그런 다음 를 구성할 수 있습니다. `aepp` 다음 코드를 사용하여 자격 증명이 포함된 라이브러리:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Data Distiller에 대한 연결 만들기 {#create-connection}

한 번 `aepp` 은 자격 증명으로 구성됩니다. 다음 코드를 사용하여 Data Distiller에 대한 연결을 만들고 다음과 같이 대화형 세션을 시작할 수 있습니다.

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

그런 다음 Experience Platform 샌드박스에서 데이터 세트를 쿼리할 수 있습니다. 쿼리할 데이터 세트의 ID가 주어지면 카탈로그 서비스에서 해당 테이블 이름을 검색하고 테이블에서 쿼리를 실행할 수 있습니다.

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### 빠른 쿼리 성능을 위해 단일 데이터 세트에 연결 {#connect-to-single-dataset}

기본적으로 Data Distiller 연결은 샌드박스의 모든 데이터 세트에 연결됩니다. 보다 빠른 쿼리와 줄어든 리소스 사용량을 위해 대신 특정 관심 데이터 세트에 연결할 수 있습니다. 다음을 변경하여 이 작업을 수행할 수 있습니다. `dbname` Data Distiller 연결 개체에서 `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## 다음 단계

이 문서를 읽고 다음에서 Data Distiller에 연결하는 방법을 배웠습니다. [!DNL Python] 기계 학습 환경의 전자 필기장입니다. 머신 러닝 환경에서 Experience Platform에서 피드 사용자 지정 모델로의 기능 파이프라인을 만드는 다음 단계는 다음과 같습니다 [데이터 세트 탐색 및 분석](./exploratory-analysis.md).
