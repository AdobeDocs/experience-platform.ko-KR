---
keywords: Experience Platform;소매 영업 레서피;데이터 과학 작업 공간;인기 있는 주제;레서피
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 다른 모든 Adobe Experience Platform Data Science Workspace 자습서에 필요한 사전 요구 사항과 자산을 제공합니다. 완료되면 Experience Platform 시 사용자와 IMS 조직의 구성원이 소매 판매 스키마 및 데이터 세트를 사용할 수 있습니다.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---


# 소매 판매 스키마 및 데이터 세트 만들기

이 자습서에서는 다른 모든 항목에 필요한 사전 요구 사항과 자산을 제공합니다 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 튜토리얼. 완료되면 사용자와 IMS 조직의 구성원이 소매 판매 스키마 및 데이터 세트를 사용할 수 있습니다. [!DNL Experience Platform].

## 시작하기

이 자습서를 시작하기 전에 다음 전제 조건이 있어야 합니다.
- 액세스 권한 [!DNL Adobe Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 [!DNL Experience Platform]을(를) 계속하기 전에 시스템 관리자에게 문의하십시오.
- 인증 [!DNL Experience Platform] API 호출. 을(를) 완료합니다 [Adobe Experience Platform API 인증 및 액세스](https://www.adobe.com/go/platform-api-authentication-en) 이 자습서를 완료하기 위해 다음 값을 가져오는 자습서:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - 클라이언트 암호: `{CLIENT_SECRET}`
   - 클라이언트 인증서: `{PRIVATE_KEY}`
- 에 대한 샘플 데이터 및 소스 파일 [소매 판매 레서피](../pre-built-recipes/retail-sales.md). 이 자산 및 기타 요소에 필요한 자산 다운로드 [!DNL Data Science Workspace] 의 자습서 [공개 Git 리포지토리 Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) 및 [!DNL Python] 패키지:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [다이토어](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 이 자습서에서 사용되는 다음 개념에 대한 작업 이해:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [스키마 작성 기본 사항](../../xdm/schema/field-dictionary.md)

## 소매 판매 스키마 및 데이터 세트 만들기

제공된 부트스트랩 스크립트를 사용하여 소매 판매 스키마 및 데이터 세트가 자동으로 생성됩니다. 다음 순서로 아래 절차를 따르십시오.

### 파일 구성

1. 내부 [!DNL Experience Platform] 자습서 리소스 패키지, 디렉토리로 이동합니다. `bootstrap`, 및 열기 `config.yaml` 적절한 텍스트 편집기 사용.
2. 아래에 `Enterprise` 섹션에서 다음 값을 입력합니다.

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 아래의 값을 편집합니다. `Platform` 섹션을 참조하십시오.

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: API 호출에 대한 기본 경로입니다. 이 값은 수정하지 마십시오.
   - `ims_token`: 사용자 `{ACCESS_TOKEN}` 여기 와
   - `ingest_data`: 이 자습서를 사용하려면 이 값을 로 설정하십시오. `"True"` 를 사용하여 소매 판매 스키마 및 데이터 세트를 만듭니다. 값 `"False"` 스키마만 만듭니다.
   - `build_recipe_artifacts`: 이 자습서를 사용하려면 이 값을 로 설정하십시오. `"False"` 스크립트가 배합식 객체를 생성하지 않도록 합니다.
   - `kernel_type`: 레서피 아티팩트의 실행 유형입니다. 이 값을 로 둡니다. `Python` if `build_recipe_artifacts` 는 로 설정되어 있습니다. `"False"`그렇지 않으면 올바른 실행 유형을 지정합니다.

4. 아래에 `Titles` 섹션에서 소매 판매 샘플 데이터에 대해 다음 정보를 적절히 제공하고 편집 후 파일을 저장하고 닫습니다. 아래 표시된 예:

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

1. 터미널 애플리케이션을 열고 [!DNL Experience Platform] 자습서 리소스 디렉토리.
2. 설정 `bootstrap` 디렉토리를 현재 작업 경로로 사용하고 `bootstrap.py` [!DNL Python] 다음 명령을 입력하여 스크립트를 작성합니다.

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >스크립트를 완료하는 데 몇 분이 걸릴 수 있습니다.

## 다음 단계

부트스트랩 스크립트가 성공적으로 완료되면 Retail Sales 입출력 스키마와 데이터 세트를 볼 수 있습니다 [!DNL Experience Platform]. 자세한 내용은 [스키마 데이터 튜토리얼 미리 보기](./preview-schema-data.md)
추가 정보.

또한 소매 판매 샘플 데이터를에 성공적으로 수집했습니다. [!DNL Experience Platform] 제공된 부트스트랩 스크립트 사용.

수집된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - Data Science Workspace에서 Jupiter Notebook을 사용하여 데이터에 액세스하고, 탐색하고, 시각화하고, 이해할 수 있습니다.
- [배합식에 소스 파일 패키지](./package-source-files-recipe.md)
   - 이 자습서에 따라 고유한 모델을 [!DNL Data Science Workspace] 가져오기 가능한 레서피 파일에 소스 파일을 패키징하여
