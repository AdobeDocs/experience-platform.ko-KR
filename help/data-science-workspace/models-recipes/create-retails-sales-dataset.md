---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 만들기
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# 소매 판매 스키마 및 데이터 세트 만들기

이 자습서에서는 다른 모든 Adobe Experience Platform 데이터 과학 작업 영역 자습서에 필요한 사전 요구 사항 및 자산을 제공합니다. 완료되면 Retail Sales 스키마와 데이터 세트를 사용자 및 IMS Organization on Experience Platform에서 사용할 수 있습니다.

## 시작하기

이 튜토리얼을 시작하기 전에 다음 사전 요구 사항을 충족해야 합니다.
- Adobe Experience Platform 이용 Experience Platform에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자에게 문의하십시오.
- Experience Platform API 호출 인증. 이 자습서를 [성공적으로 완료하려면 Adobe Experience Platform API](../../tutorials/authentication.md) 인증 및 액세스 튜토리얼을 완료하십시오.
   - 인증: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - 클라이언트 암호: `{CLIENT_SECRET}`
   - 클라이언트 인증서: `{PRIVATE_KEY}`
- 소매 영업 레서피에 대한 샘플 데이터 및 소스 [파일입니다](../pre-built-recipes/retail-sales.md). Adobe 공개 Git 리포지토리에서 이 및 기타 데이터 과학 작업 영역 자습서에 필요한 [에셋을 다운로드할 수 있습니다](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) 및 다음 Python 패키지:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [딕터](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 이 튜토리얼에서 사용되는 다음 개념에 대한 작업 이해:
   - [XDM(Experience Data Model)](../../xdm/home.md)
   - [스키마 구성 기초](../../xdm/schema/field-dictionary.md)

## 소매 영업 스키마 및 데이터 세트 만들기

소매 판매 스키마 및 데이터 세트는 제공된 부트스트랩 스크립트를 사용하여 자동으로 생성됩니다. 아래 단계를 순서대로 수행합니다.

### 파일 구성

1. Experience Platform 자습서 리소스 패키지 내에서 디렉토리로 이동한 `bootstrap`다음 적절한 텍스트 편집기를 사용하여 `config.yaml` 엽니다.
2. 섹션에서 `Enterprise` 다음 값을 입력합니다.

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 아래 예와 같이 `Platform` 섹션 아래에 있는 값을 편집합니다.

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` :API 호출에 대한 기본 경로입니다. 이 값을 수정하지 마십시오.
   - `ims_token` :여기 `{ACCESS_TOKEN}` 가시면 됩니다
   - `ingest_data` :이 자습서의 목적을 위해 이 값을 로 설정하여 소매 판매 스키마 및 데이터 세트를 만듭니다 `"True"` . 의 값은 스키마만 `"False"` 만듭니다.
   - `build_recipe_artifacts` :이 자습서의 목적을 위해 스크립트에서 레서피 결함을 생성하지 못하도록 이 값을 `"False"` 설정합니다.
   - `kernel_type` :레서피 객체의 실행 유형입니다. 이 값을 로 `Python` 설정한 `build_recipe_artifacts` 것처럼 `"False"`두거나 올바른 실행 유형을 지정합니다.

4. 이 `Titles` 섹션에서 소매 판매 샘플 데이터에 대해 다음 정보를 적절히 입력하고 편집한 후 파일을 저장하고 닫습니다. 아래 표시된 예:

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

1. 터미널 애플리케이션을 열고 Experience Platform 자습서 리소스 디렉토리로 이동합니다.
2. 다음 명령을 입력하여 `bootstrap` 디렉토리를 현재 작업 경로로 설정하고 Python `bootstrap.py` 스크립트를 실행합니다.

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] 스크립트를 완료하는 데 몇 분이 걸릴 수 있습니다.

## 다음 단계

부트스트랩 스크립트가 성공적으로 완료되면 Adobe Experience Platform에서 소매 판매 입력 및 출력 스키마 및 데이터 세트를 볼 수 있습니다. 자세한 내용은 [스키마 데이터 미리 보기 자습서를](./preview-schema-data.md)참조하십시오.

또한 제공된 부트스트랩 스크립트를 사용하여 Adobe Experience Platform에 소매 세일즈 샘플 데이터를 성공적으로 인제스트했습니다.

인제스트된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - 데이터 과학 작업 공간에서 Jupiter 노트북을 사용하여 데이터에 액세스하고 데이터를 탐색, 시각화 및 이해할 수 있습니다.
- [소스 파일을 레서피로 패키지화](./package-source-files-recipe.md)
   - 이 튜토리얼에서는 소스 파일을 가져올 수 있는 Recipe 파일로 패키징하여 자신만의 모델을 데이터 과학 작업 영역으로 가져오는 방법을 살펴봅니다.