---
title: Jupyter Notebook을 쿼리 서비스에 연결
description: Jupyter Notebook을 Adobe Experience Platform 쿼리 서비스와 연결하는 방법에 대해 알아봅니다.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Jupyter Notebook] 연결

이 문서에서는 [!DNL Jupyter Notebook]을(를) Adobe Experience Platform 쿼리 서비스와 연결하는 데 필요한 단계를 설명합니다.

## 시작하기

이 안내서를 사용하려면 [!DNL Jupyter Notebook]에 대한 액세스 권한이 있고 해당 인터페이스에 익숙해야 합니다. [!DNL Jupyter Notebook] 이상을 다운로드하려면 [공식 [!DNL Jupyter Notebook] 설명서](https://jupyter.org/)를 참조하세요.

[!DNL Jupyter Notebook]을(를) Experience Platform에 연결하는 데 필요한 자격 증명을 획득하려면 Experience Platform UI에서 [!UICONTROL 쿼리] 작업 영역에 액세스할 수 있어야 합니다. 현재 [!UICONTROL 쿼리] 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

>[!TIP]
>
>[!DNL Anaconda Navigator]은(는) 데스크톱 GUI(그래픽 사용자 인터페이스)로, [!DNL Jupyter Notebook]과(와) 같은 일반적인 [!DNL Python] 프로그램을 쉽게 설치하고 시작할 수 있습니다. 또한 명령줄 명령을 사용하지 않고도 패키지, 환경 및 채널을 관리할 수 있습니다.
>웹 사이트에서 안내식 설치 프로세스를 따라 [선호하는 응용 프로그램 버전을 설치](https://docs.anaconda.com/anaconda/install/)하십시오.
>Anaconda Navigator 홈 화면의 지원되는 응용 프로그램 목록에서 **[!DNL Jupyter Notebook]**&#x200B;을(를) 선택하여 프로그램을 시작합니다.
>자세한 내용은 [공식 Anaconda 설명서](https://docs.anaconda.com/anaconda/navigator/)에서 확인할 수 있습니다.

공식 Jupyter 설명서는 [명령줄 인터페이스에서 전자 필기장을 실행](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook)&#x200B;(CLI)하는 방법에 대한 지침을 제공합니다.

## Launch [!DNL Jupyter Notebook]

새 [!DNL Jupyter Notebook] 웹 응용 프로그램을 연 후 UI에서 **[!DNL New]** 드롭다운을 선택한 다음 **[!DNL Python 3]**&#x200B;을(를) 선택하여 새 전자 필기장을 만듭니다. [!DNL Notebook] 편집기가 나타납니다.

[!DNL Notebook] 편집기의 첫 번째 줄에 다음 값을 입력하고 명령 모음에서 **[!DNL Run]**&#x200B;을(를) 선택합니다. `pip install psycopg2-binary`. 입력 줄 아래에 성공 메시지가 나타납니다.

>[!IMPORTANT]
>
>이 프로세스의 일부로 연결을 만들려면 **[!DNL Run]**&#x200B;을(를) 선택하여 각 코드 행을 실행해야 합니다.

그런 다음 [!DNL Python]에 대한 [!DNL PostgreSQL] 데이터베이스 어댑터를 가져옵니다. 값 `import psycopg2`을(를) 입력하고 **[!DNL Run]**&#x200B;을(를) 선택합니다. 이 프로세스에 대한 성공 메시지가 없습니다. 오류 메시지가 없으면 다음 단계를 계속합니다.

이제 값을 입력하여 Adobe Experience Platform 자격 증명을 제공해야 합니다. `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. 연결 자격 증명은 Experience Platform UI의 [!UICONTROL 자격 증명] 탭에 있는 [!UICONTROL 쿼리] 섹션에서 찾을 수 있습니다. 자세한 지침은 [조직 자격 증명을 찾는 방법](../ui/credentials.md)에 대한 설명서를 참조하십시오.

타사 클라이언트를 사용하여 세부 정보를 반복적으로 입력하는 작업을 줄일 때 만료되지 않는 자격 증명을 사용하는 것이 좋습니다. [만료되지 않는 자격 증명을 생성하고 사용하는 방법](../ui/credentials.md#non-expiring-credentials)에 대한 지침은 설명서를 참조하세요.

>[!IMPORTANT]
>
>Experience Platform UI에서 자격 증명을 복사할 때에는 자격 증명의 추가적인 형식이 필요하지 않습니다. 속성과 값 사이에 하나의 공백이 있는 한 줄로 지정할 수 있습니다. 자격 증명은 따옴표로 묶여 있으며 **not**&#x200B;은(는) 쉼표로 구분됩니다.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

[!DNL Jupyter Notebook] 인스턴스가 이제 쿼리 서비스에 연결되어 있습니다.

## 쿼리 실행 예

[!DNL Jupyter Notebook]을(를) 쿼리 서비스에 연결했으므로 [!DNL Notebook] 입력을 사용하여 데이터 세트에 대한 쿼리를 수행할 수 있습니다. 다음 예제에서는 간단한 쿼리를 사용하여 프로세스를 보여 줍니다.

다음 값을 입력합니다.

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

그런 다음 매개 변수(`data`)를 호출하여 쿼리 결과를 서식이 지정되지 않은 응답으로 표시합니다.

보다 사람이 읽을 수 있는 방식으로 결과의 서식을 지정하려면 다음 명령을 사용하십시오.

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

이러한 명령은 성공 메시지를 생성하지 않습니다. 오류 메시지가 없는 경우 함수를 사용하여 SQL 쿼리 결과를 테이블 형식으로 출력할 수 있습니다.

테이블화된 쿼리 결과를 보려면 `df.head()` 함수를 입력하고 실행하십시오.

## 다음 단계

쿼리 서비스에 연결되었으므로 [!DNL Jupyter Notebook]을(를) 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 가이드](../best-practices/writing-queries.md)를 참조하십시오.
