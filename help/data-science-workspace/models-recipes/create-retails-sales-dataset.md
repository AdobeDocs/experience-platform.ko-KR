---
keywords: Experience Platform;소매 판매 레시피;Data Science Workspace;인기 주제;레시피
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 만들기
type: Tutorial
description: 이 자습서에서는 다른 모든 Adobe Experience Platform 데이터 과학 작업 영역 자습서에 필요한 사전 요구 사항 및 에셋을 제공합니다. 완료되면 Experience Platform 시 사용자와 조직의 멤버가 소매 판매 스키마 및 데이터 세트를 사용할 수 있습니다.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---


# 소매 판매 스키마 및 데이터 세트 만들기

이 자습서에서는 다른 모든 작업에 필요한 사전 요구 사항과 에셋을 제공합니다 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 튜토리얼. 완료되면에 사용자와 조직 구성원이 소매 판매 스키마 및 데이터 세트를 사용할 수 있습니다. [!DNL Experience Platform].

## 시작하기

이 자습서를 시작하기 전에 다음 사전 요구 사항이 있어야 합니다.
- 액세스 대상: [!DNL Adobe Experience Platform]. 에서 조직에 대한 액세스 권한이 없는 경우 [!DNL Experience Platform]을(를) 계속하려면 시스템 관리자에게 문의하십시오.
- 수행할 인증 [!DNL Experience Platform] API 호출. 다음을 완료합니다. [Adobe Experience Platform API 인증 및 액세스](https://www.adobe.com/go/platform-api-authentication-en) 자습서 : 이 자습서를 성공적으로 완료하기 위해 다음 값을 가져옵니다.
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - 클라이언트 암호: `{CLIENT_SECRET}`
   - 클라이언트 인증서: `{PRIVATE_KEY}`
- 샘플 데이터 및 소스 파일 [소매 판매 레시피](../pre-built-recipes/retail-sales.md). 이 작업 및 기타 작업에 필요한 에셋 다운로드 [!DNL Data Science Workspace] 의 튜토리얼 [공개 Git 저장소 Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) 및 다음 [!DNL Python] 패키지:
   - [핍](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [독재자](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 이 자습서에서 사용되는 다음 개념에 대한 작업 이해:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [스키마 컴포지션 기본 사항](../../xdm/schema/field-dictionary.md)

## 소매 판매 스키마 및 데이터 세트 만들기

소매 판매 스키마 및 데이터 세트는 제공된 부트스트랩 스크립트를 사용하여 자동으로 생성됩니다. 다음 단계를 순서대로 수행합니다.

### 파일 구성

1. 내부 [!DNL Experience Platform] 튜토리얼 리소스 패키지에서 디렉토리로 이동합니다. `bootstrap`, 및 열기 `config.yaml` 적절한 텍스트 편집기 사용.
2. 아래 `Enterprise` 섹션에 다음 값을 입력합니다.

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 아래에 있는 값을 편집합니다. `Platform` 섹션의 예는 다음과 같습니다.

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: API 호출의 기본 경로. 이 값은 수정하지 마십시오.
   - `ims_token`: 사용자 `{ACCESS_TOKEN}` 여기 로 이동합니다.
   - `ingest_data`: 이 자습서의 목적을 위해 이 값을 로 설정합니다. `"True"` 소매 판매 스키마 및 데이터 세트를 만들기 위해 값 `"False"` 은 스키마만 생성합니다.
   - `build_recipe_artifacts`: 이 자습서의 목적을 위해 이 값을 로 설정합니다. `"False"` 스크립트가 레서피 아티팩트를 생성하지 않도록 합니다.
   - `kernel_type`: 레시피 아티팩트의 실행 유형입니다. 이 값을 다음으로 남기기 `Python` if `build_recipe_artifacts` 다음으로 설정됨 `"False"`, 그렇지 않으면 올바른 실행 유형을 지정합니다.

4. 아래 `Titles` 섹션에서 소매 판매 샘플 데이터에 맞게 다음 정보를 제공하고, 편집한 후 파일을 저장하고 닫습니다. 아래 예제:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### 부트스트랩 스크립트 실행

1. 터미널 애플리케이션을 열고 다음 위치로 이동합니다. [!DNL Experience Platform] 튜토리얼 리소스 디렉터리입니다.
2. 설정 `bootstrap` 디렉터리를 현재 작업 경로로 사용하고 `bootstrap.py` [!DNL Python] 다음 명령을 입력하여 스크립트를 작성합니다.

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >스크립트를 완료하는 데 몇 분 정도 걸릴 수 있습니다.

## 다음 단계

부트스트랩 스크립트가 성공적으로 완료되면에서 소매 판매 입력 및 출력 스키마와 데이터 세트를 볼 수 있습니다. [!DNL Experience Platform]. 다음을 참조하십시오. [스키마 데이터 미리 보기 자습서](./preview-schema-data.md)
추가 정보.

또한 소매 판매 샘플 데이터를에 정상적으로 수집했습니다. [!DNL Experience Platform] 제공된 부트스트랩 스크립트 사용.

수집된 데이터로 작업을 계속하려면 다음을 수행합니다.
- [Jupyter Notebooks를 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - 데이터 과학 작업 영역에서 Jupyter Notebooks를 사용하여 데이터에 액세스하고, 탐색하고, 시각화하고, 이해할 수 있습니다.
- [소스 파일을 레시피에 패키징](./package-source-files-recipe.md)
   - 이 튜토리얼을 따라 나만의 모델을 로 가져오는 방법을 알아봅니다. [!DNL Data Science Workspace] 가져온 레시피 파일에 소스 파일을 패키지하여.
