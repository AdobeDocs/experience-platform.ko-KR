---
keywords: Experience Platform;소매 영업 레서피;데이터 과학 작업 공간;인기 항목;레서피
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 다른 모든 Adobe Experience Platform Data Science Workspace 튜토리얼에 필요한 사전 요구 사항과 에셋을 제공합니다. 완료되면 소매 판매 스키마 및 데이터 세트를 Experience Platform에 있는 사용자 및 IMS 조직 구성원이 사용할 수 있습니다.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 소매 판매 스키마 및 데이터 세트 만들기

이 자습서에서는 다른 모든 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 튜토리얼에 필요한 사전 요구 사항과 에셋을 제공합니다. 완료되면 [!DNL Experience Platform]에 귀하 및 귀사의 IMS 조직 구성원이 소매 판매 스키마 및 데이터 세트를 사용할 수 있습니다.

## 시작하기

이 자습서를 시작하기 전에 다음 사전 요구 사항을 충족해야 합니다.
- [!DNL Adobe Experience Platform]에 액세스합니다. [!DNL Experience Platform]에서 IMS 조직에 액세스할 수 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.
- [!DNL Experience Platform] API 호출을 수행하는 인증. 이 자습서를 성공적으로 완료하려면 [Adobe Experience Platform API 인증 및 액세스](https://www.adobe.com/go/platform-api-authentication-en) 튜토리얼을 완료하십시오.
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key:`{API_KEY}`
   - x-gw-ims-org-id:`{IMS_ORG}`
   - 클라이언트 암호:`{CLIENT_SECRET}`
   - 클라이언트 인증서:`{PRIVATE_KEY}`
- [소매 영업 레서피](../pre-built-recipes/retail-sales.md)에 대한 샘플 데이터 및 소스 파일. [Adobe 공개 Git 리포지토리](https://github.com/adobe/experience-platform-dsw-reference/)에서 이 및 기타 [!DNL Data Science Workspace] 튜토리얼에 필요한 에셋을 다운로드합니다.
- [Python >= 2.7](https://www.python.org/downloads/) 과 다음  [!DNL Python] 패키지:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [사전](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 이 튜토리얼에서 사용되는 다음 개념에 대한 작업 이해입니다.
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [스키마 컴포지션의 기본 사항](../../xdm/schema/field-dictionary.md)

## 소매 판매 스키마 및 데이터 세트 만들기

제공된 부트스트랩 스크립트를 사용하여 소매 판매 스키마 및 데이터 세트가 자동으로 생성됩니다. 아래 단계를 순서대로 수행합니다.

### 파일 구성

1. [!DNL Experience Platform] 자습서 리소스 패키지 내에서 `bootstrap` 디렉토리로 이동한 다음 적절한 텍스트 편집기를 사용하여 `config.yaml`를 엽니다.
2. `Enterprise` 섹션에서 다음 값을 입력합니다.

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. `Platform` 섹션 아래에 있는 값을 편집합니다(아래 예).

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` :API 호출에 대한 기본 경로입니다. 이 값을 수정하지 마십시오.
   - `ims_token` :당신 `{ACCESS_TOKEN}` 은 여기 있어요
   - `ingest_data` :이 자습서의 목적을 위해 소매 판매 스키마 및 데이터 세트 `"True"` 를 만들려면 이 값을 로 설정합니다. `"False"` 값은 스키마만 생성합니다.
   - `build_recipe_artifacts` :이 자습서를 위해 스크립트에서 레서피 가공물 `"False"` 을 생성하지 않도록 하려면 이 값을 로 설정합니다.
   - `kernel_type` :Recipe 객체의 실행 유형입니다. `build_recipe_artifacts`이(가) `"False"`(으)로 설정된 경우 이 값을 `Python`(으)로 유지하고, 그렇지 않은 경우 올바른 실행 유형을 지정합니다.

4. `Titles` 섹션에서 소매 판매 샘플 데이터에 대해 다음 정보를 적절히 입력하고 편집 후 파일을 저장하고 닫습니다. 아래에 표시된 예:

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

1. 터미널 응용 프로그램을 열고 [!DNL Experience Platform] 자습서 리소스 디렉토리로 이동합니다.
2. `bootstrap` 디렉토리를 현재 작업 경로로 설정하고 다음 명령을 입력하여 `bootstrap.py` [!DNL Python] 스크립트를 실행합니다.

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >스크립트를 완료하는 데 몇 분이 걸릴 수 있습니다.

## 다음 단계

부트스트랩 스크립트가 성공적으로 완료되면 소매 판매 입력 및 출력 스키마 및 데이터 세트를 [!DNL Experience Platform]에서 볼 수 있습니다. [스키마 데이터 미리 보기 자습서](./preview-schema-data.md)를 참조하십시오.
를 참조하십시오.

제공된 부트스트랩 스크립트를 사용하여 소매 판매 샘플 데이터를 [!DNL Experience Platform]에 인제스트했습니다.

인제스트된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - 데이터 과학 작업 영역의 Jupiter 노트북을 사용하여 데이터를 액세스, 탐색, 시각화 및 이해할 수 있습니다.
- [소스 파일을 레서피에 패키지화](./package-source-files-recipe.md)
   - 이 자습서에 따라 소스 파일을 가져올 수 있는 레서피 파일에 패키징하여 자신의 모델을 [!DNL Data Science Workspace]으로 가져오는 방법을 알아보십시오.
