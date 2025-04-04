---
title: Python 및 SQLAlchemy를 사용하여 Experience Platform 데이터 관리
description: SQL 대신 Python을 사용하여 SQLAlchemy를 사용하여 Experience Platform 데이터를 관리하는 방법에 대해 알아봅니다.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# [!DNL Python] 및 [!DNL SQLAlchemy]을(를) 사용하여 Experience Platform 데이터 관리

Adobe Experience Platform 데이터 관리의 유연성을 높이기 위해 SQLAlchemy를 사용하는 방법에 대해 알아봅니다. SQL에 익숙하지 않은 사용자의 경우 SQLAlchemy를 사용하면 관계형 데이터베이스를 사용할 때 개발 시간을 크게 향상시킬 수 있습니다. 이 문서에서는 [!DNL SQLAlchemy]을(를) 쿼리 서비스에 연결하고 Python을 사용하여 데이터베이스와 상호 작용하는 지침 및 예제를 제공합니다.

[!DNL SQLAlchemy]은(는) SQL 데이터베이스에 저장된 데이터를 [!DNL Python] 개체로 전송할 수 있는 ORM(Object Relational Mapper) 및 [!DNL Python] 코드 라이브러리입니다. 그런 다음 [!DNL Python] 코드를 사용하여 Experience Platform 데이터 레이크 내에 보관된 데이터에 대해 CRUD 작업을 수행할 수 있습니다. 따라서 PSQL만 사용하여 데이터를 관리할 필요가 없습니다.

## 시작하기

[!DNL SQLAlchemy]을(를) Experience Platform에 연결하는 데 필요한 자격 증명을 획득하려면 Experience Platform UI에서 쿼리 작업 영역에 액세스할 수 있어야 합니다. 현재 쿼리 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

## [!DNL Query Service] 자격 증명 {#credentials}

자격 증명을 찾으려면 Experience Platform UI에 로그인하고 왼쪽 탐색에서 **[!UICONTROL 쿼리]**&#x200B;를 선택한 다음 **[!UICONTROL 자격 증명]**&#x200B;을 선택하십시오. 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오.

![쿼리 서비스에 대한 만료 자격 증명이 있는 자격 증명 탭이 강조 표시되었습니다.](../images/use-cases/credentials.png)

포트 80이 쿼리 서비스 연결에 권장되는 포트이지만 포트 5432를 사용할 수도 있습니다.

>[!IMPORTANT]
>
>만료되는 자격 증명(위 이미지에 표시됨)을 사용하여 쿼리 서비스에 연결하는 경우 조직의 설정에 정의된 기간 후에 연결의 세션 수명이 만료됩니다. 기본적으로 이 기간은 24시간입니다. [만료되지 않는 자격 증명으로 클라이언트를 연결](../ui/credentials.md#non-expiring-credentials)하는 방법 또는 [만료되는 자격 증명에 대한 세션 수명을 변경](../ui/credentials.md#expiring-credentials)하는 방법에 대해 알아보려면 설명서를 참조하세요.

QS 자격 증명에 대한 액세스 권한이 있으면 선택한 [!DNL Python] 편집기를 엽니다.

### [!DNL Python]에 자격 증명 저장 {#store-credentials}

[!DNL Python] 편집기에서 `urllib.parse.quote` 라이브러리를 가져오고 각 자격 증명 변수를 매개 변수로 저장합니다. `urllib.parse` 모듈은 URL 문자열을 구성 요소로 나눌 수 있는 표준 인터페이스를 제공합니다. quote 함수는 URL 문자열의 특수 문자를 대체하여 데이터를 URL 구성 요소로 안전하게 사용합니다. 필수 코드의 예는 아래에 나와 있습니다.

>[!TIP]
>
>[!DNL Python]의 삼중 따옴표를 사용하여 여러 줄 암호 문자열을 입력하십시오.

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
>만료되는 자격 증명을 사용하는 경우 [!DNL SQLAlchemy]을(를) Experience Platform에 연결하기 위해 제공한 암호가 만료됩니다. 자세한 내용은 [자격 증명 섹션](#credentials)을 참조하세요.

### 엔진 인스턴스 [#create-engine] 만들기

변수가 만들어지면 `create_engine` 함수를 가져오고 문자열을 만들어 SQLAlchemy로 쿼리 서비스 자격 증명을 컴파일하고 형식을 지정하십시오. 그런 다음 `create_engine` 함수를 사용하여 엔진 인스턴스를 만듭니다.

>[!NOTE]
>
>`create_engine`엔진 인스턴스를 반환합니다. 그러나 연결이 필요한 쿼리가 호출될 때까지 쿼리 서비스에 대한 연결을 열지 않습니다.

타사 클라이언트를 사용하여 Experience Platform에 액세스할 때 SSL을 활성화해야 합니다. 엔진의 일부로 `connect_args`을(를) 사용하여 추가 키워드 인수를 입력하십시오. SSL 모드를 `require`(으)로 설정하는 것이 좋습니다. 허용되는 값에 대한 자세한 내용은 [SSL 모드 설명서](../clients/ssl-modes.md)를 참조하십시오.

아래 예제에서는 엔진 및 연결 문자열을 초기화하는 데 필요한 [!DNL Python] 코드를 표시합니다.

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
>만료되는 자격 증명을 사용하는 경우 [!DNL SQLAlchemy]을(를) Experience Platform에 연결하기 위해 제공한 암호가 만료됩니다. 자세한 내용은 [자격 증명 섹션](#credentials)을 참조하세요.

이제 [!DNL Python]을(를) 사용하여 Experience Platform 데이터를 쿼리할 준비가 되었습니다. 아래 예는 쿼리 서비스 테이블 이름의 배열을 반환합니다.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
