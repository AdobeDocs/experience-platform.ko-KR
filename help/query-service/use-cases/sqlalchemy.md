---
title: Python 및 SQLAlchemy를 사용하여 플랫폼 데이터 관리
description: SQL 대신 Python을 사용하여 Platform 데이터를 관리하는 데 SQLAlchemy를 사용하는 방법을 알아봅니다.
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 을 사용하여 플랫폼 데이터 관리 [!DNL Python] 및 [!DNL SQLAlchemy]

Adobe Experience Platform 데이터 관리를 보다 유연하게 하기 위해 SQLAlchemy를 사용하는 방법을 알아봅니다. SQL에 익숙하지 않은 사용자의 경우 SQLAlchemy가 관계형 데이터베이스를 사용할 때 개발 시간을 크게 향상시킬 수 있습니다. 이 문서에서는 연결할 지침 및 예를 제공합니다 [!DNL SQLAlchemy] 서비스를 쿼리하고 Python을 사용하여 데이터베이스와 상호 작용하기 시작합니다.

[!DNL SQLAlchemy] 는 ORM(Object Relational Mapper) 및 [!DNL Python] SQL 데이터베이스에 저장된 데이터를 로 전송할 수 있는 코드 라이브러리 [!DNL Python] 개체. 그런 다음 다음을 사용하여 플랫폼 데이터 레이크 내에 있는 데이터에 대해 CRUD 작업을 수행할 수 있습니다 [!DNL Python] 코드가 있어야 합니다. 따라서 PSQL만 사용하여 데이터를 관리할 필요가 없습니다.

## 시작하기

연결에 필요한 자격 증명을 획득하려면 [!DNL SQLAlchemy] Experience Platform을 수행하려면 플랫폼 UI의 쿼리 작업 영역에 액세스할 수 있어야 합니다. 현재 쿼리 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

## [!DNL Query Service] 자격 증명 {#credentials}

자격 증명을 찾으려면 Platform UI에 로그인하고 를 선택합니다 **[!UICONTROL 쿼리]** 왼쪽 탐색에서 다음을 차례로 수행합니다 **[!UICONTROL 자격 증명]**. 로그인 자격 증명을 찾는 방법에 대한 전체 지침은 [자격 증명 안내서](../ui/credentials.md).

![쿼리 서비스에 대한 만료 자격 증명이 강조 표시된 자격 증명 탭](../images/use-cases/credentials.png)

포트 80이 Query Service에 연결하는 데 권장되는 포트이지만 포트 5432를 사용할 수도 있습니다.

>[!IMPORTANT]
>
>만료 자격 증명(위 이미지에 표시됨)을 사용하여 쿼리 서비스에 연결하는 경우, 연결의 세션 기간은 조직 설정에 정의된 일정 시간 후에 만료됩니다. 기본적으로 이 기간은 24시간입니다. 방법을 알아보려면 설명서 를 참조하십시오. [만료되지 않은 자격 증명을 사용하여 클라이언트 연결](../ui/credentials.md#non-expiring-credentials), 또는 방법 [만료 자격 증명을 위한 세션 기간 변경](../ui/credentials.md#expiring-credentials).

QS 자격 증명에 액세스할 수 있으면 [!DNL Python] 편집자 선택.

### 자격 증명 저장 위치 [!DNL Python] {#store-credentials}

사용자 [!DNL Python] 편집기, 가져오기 `urllib.parse.quote` 라이브러리 및 각 자격 증명 변수를 매개 변수로 저장합니다. 다음 `urllib.parse` 모듈은 URL 문자열을 구성 요소로 구분하는 표준 인터페이스를 제공합니다. 견적 함수는 URL 문자열의 특수 문자를 대체하여 데이터를 URL 구성 요소로 사용할 수 있도록 합니다. 필요한 코드의 예는 아래에 나와 있습니다.

>[!TIP]
>
>사용 [!DNL Python]여러 줄 암호 문자열을 입력하려면 세 개의 따옴표를 사용하십시오.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>연결할 암호를 입력합니다 [!DNL SQLAlchemy] 만료 자격 증명을 사용하는 경우 Experience Platform이 만료됩니다. 자세한 내용은 [자격 증명 섹션](#credentials) 추가 정보.

### 엔진 인스턴스 만들기 [#create-engine]

변수가 만들어지면 를 가져옵니다 `create_engine` SQLAlchemy에서 쿼리 서비스 자격 증명을 컴파일하고 형식을 지정할 문자열을 만들고 함수를 만듭니다. 다음 `create_engine` 그런 다음 함수를 사용하여 엔진 인스턴스를 구성합니다.

>[!NOTE]
>
>`create_engine`엔진의 인스턴스를 반환합니다. 그러나 연결을 필요로 하는 쿼리가 호출될 때까지 쿼리 서비스에 대한 연결이 열리지 않습니다.

타사 클라이언트를 사용하여 플랫폼에 액세스할 때는 SSL을 활성화해야 합니다. 엔진의 일부로, `connect_args` 추가 키워드 인수를 입력하려면 SSL 모드를 로 설정하는 것이 좋습니다 `require`. 자세한 내용은 [SSL 모드 설명서](../clients/ssl-modes.md) 를 참조하십시오.

아래 예는 다음과 같습니다 [!DNL Python] 엔진 및 연결 문자열을 초기화하는 데 필요한 코드입니다.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>연결할 암호를 입력합니다 [!DNL SQLAlchemy] 만료 자격 증명을 사용하는 경우 Experience Platform이 만료됩니다. 자세한 내용은 [자격 증명 섹션](#credentials) 추가 정보.

이제 다음을 사용하여 Platform 데이터를 쿼리할 준비가 되었습니다. [!DNL Python]. 아래 표시된 예제는 쿼리 서비스 테이블 이름의 배열을 반환합니다.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
