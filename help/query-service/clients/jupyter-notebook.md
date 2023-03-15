---
title: Jupyter Notebook을 쿼리 서비스에 연결
description: Jupyter Notebook을 Adobe Experience Platform 쿼리 서비스와 연결하는 방법에 대해 알아봅니다.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# 연결 [!DNL Jupyter Notebook] 쿼리 서비스

이 문서에서는 연결에 필요한 단계를 다룹니다 [!DNL Jupyter Notebook] Adobe Experience Platform 쿼리 서비스 사용

## 시작하기

이 안내서에서는 이미 다음에 대한 액세스 권한이 있어야 합니다. [!DNL Jupyter Notebook] 인터페이스에 익숙합니다. 다운로드하려면 [!DNL Jupyter Notebook] 또는 자세한 내용은 [공식 [!DNL Jupyter Notebook] 설명서](https://jupyter.org/).

연결에 필요한 자격 증명을 획득하려면 [!DNL Jupyter Notebook] 을(를) Experience Platform 하려면 다음에 대한 액세스 권한이 있어야 합니다. [!UICONTROL 쿼리] Platform UI의 작업 공간 현재 다음에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오. [!UICONTROL 쿼리] 작업 영역.

>[!TIP]
>
>[!DNL Anaconda Navigator] 는 일반적인 설치 및 실행을 보다 쉽게 할 수 있도록 해 주는 데스크톱 GUI(그래픽 사용자 인터페이스)입니다 [!DNL Python] 프로그램: [!DNL Jupyter Notebook]. 또한 명령줄 명령을 사용하지 않고도 패키지, 환경 및 채널을 관리할 수 있습니다.
>웹 사이트의 안내가 있는 설치 프로세스를 따라 [선호하는 버전의 응용 프로그램 설치](https://docs.anaconda.com/anaconda/install/).
>Anaconda Navigator 홈 화면에서 다음을 선택합니다. **[!DNL Jupyter Notebook]** 지원되는 응용 프로그램 목록에서 프로그램을 시작합니다.
>자세한 내용은 [공식 Anaconda 설명서](https://docs.anaconda.com/anaconda/navigator/).

공식 Jupyter 설명서에 다음 지침을 제공합니다. [명령줄 인터페이스에서 notebook 실행](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

새 을(를) 연 후 [!DNL Jupyter Notebook] 웹 응용 프로그램에서 **[!DNL New]** UI의 드롭다운, **[!DNL Python 3]** 새 Notebook을 만들려면 다음 [!DNL Notebook] 편집기가 나타납니다.

의 첫 번째 줄에서 [!DNL Notebook] 편집기에서 다음 값을 입력합니다. `pip install psycopg2-binary` 및 선택 **[!DNL Run]** 을 클릭합니다. 입력 줄 아래에 성공 메시지가 나타납니다.

>[!IMPORTANT]
>
>이 프로세스의 일부로 연결을 만들려면 다음을 선택해야 합니다. **[!DNL Run]** 를 입력하여 각 코드 행을 실행합니다.

다음으로, 가져오기 [!DNL PostgreSQL] 데이터베이스 어댑터 [!DNL Python]. 값 입력: `import psycopg2`및 선택 **[!DNL Run]**. 이 프로세스에 대한 성공 메시지가 없습니다. 오류 메시지가 없으면 다음 단계를 계속합니다.

이제 값을 입력하여 Adobe Experience Platform 자격 증명을 제공해야 합니다. `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. 연결 자격 증명은 [!UICONTROL 쿼리] 섹션, [!UICONTROL 자격 증명] Platform UI의 탭 방법 설명서 참조 [조직 자격 증명 찾기](../ui/credentials.md) 자세한 지침은 을 참조하십시오.

타사 클라이언트를 사용하여 세부 정보를 반복적으로 입력하는 작업을 줄일 때 만료되지 않는 자격 증명을 사용하는 것이 좋습니다. 에 대한 지침은 설명서 를 참조하십시오. [만료되지 않는 자격 증명을 생성하고 사용하는 방법](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Platform UI에서 자격 증명을 복사할 때에는 자격 증명의 추가적인 형식이 필요하지 않습니다. 속성과 값 사이에 하나의 공백이 있는 한 줄로 지정할 수 있습니다. 자격 증명은 따옴표로 묶여 있으며 **아님** 쉼표로 구분됩니다.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

사용자 [!DNL Jupyter Notebook] 이제 인스턴스가 쿼리 서비스에 연결되어 있습니다.

## 쿼리 실행 예

연결했으므로 [!DNL Jupyter Notebook] 쿼리 서비스를 사용하려면 다음을 사용하여 데이터 세트에 대한 쿼리를 수행할 수 있습니다. [!DNL Notebook] 입력. 다음 예제에서는 간단한 쿼리를 사용하여 프로세스를 보여 줍니다.

다음 값을 입력합니다.

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

그런 다음 매개 변수(`data` 위의 예에서) 을 눌러 쿼리 결과를 포맷되지 않은 응답으로 표시합니다.

보다 사람이 읽을 수 있는 방식으로 결과의 서식을 지정하려면 다음 명령을 사용하십시오.

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

이러한 명령은 성공 메시지를 생성하지 않습니다. 오류 메시지가 없는 경우 함수를 사용하여 SQL 쿼리 결과를 테이블 형식으로 출력할 수 있습니다.

다음을 입력하고 실행합니다. `df.head()` 테이블화된 쿼리 결과를 표시하는 함수입니다.

## 다음 단계

쿼리 서비스와 연결했으므로 [!DNL Jupyter Notebook] 쿼리를 작성합니다. 쿼리 작성 및 실행 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
