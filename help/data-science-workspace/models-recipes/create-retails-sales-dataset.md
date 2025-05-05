---
keywords: Experience Platform; 소매 판매 레서피; 데이터 과학 작업 영역; 인기 있는 주제; 조리법
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 만들기
type: Tutorial
description: 이 튜토리얼 다른 모든 Adobe Experience Platform 데이터 과학 작업 영역 자습서에 필요한 사전 요구 사항 및 자산을 제공합니다. 완료되면 소매 판매 스키마 및 데이터 세트를 Experience Platform에서 사용자 및 조직의 구성원이 사용할 수 있습니다.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---


# 소매 판매 스키마 및 데이터 세트 만들기

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

이 자습서에서는 다른 모든 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 자습서에 필요한 사전 요구 사항 및 자산을 제공합니다. 완료되면 [!DNL Experience Platform]에서 사용자 및 조직의 멤버가 소매 판매 스키마 및 데이터 세트를 사용할 수 있습니다.

## 시작하기

이 튜토리얼 시작 전 다음과 같은 전제 조건이 있어야 합니다.
- [!DNL Adobe Experience Platform]에 액세스. [!DNL Experience Platform]의 조직에 대한 액세스 권한이 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.
- [!DNL Experience Platform] API 호출 권한 부여. 이 자습서를 성공적으로 완료하려면 [Adobe Experience Platform API 인증 및 액세스](https://www.adobe.com/go/platform-api-authentication-en) 자습서를 완료하여 다음 값을 얻으십시오.
   - 인증: `{ACCESS_TOKEN}`
   - x-api-키: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - 클라이언트 암호: `{CLIENT_SECRET}`
   - 클라이언트 인증서: `{PRIVATE_KEY}`
- Retail Sales Recipe[&#128279;](../pre-built-recipes/retail-sales.md)에 대한 샘플 데이터 및 소스 파일.[ 이 자습서 및 기타 [!DNL Data Science Workspace] 자습서에 필요한 자산을 Adobe Systems 공용 Git 저장소](https://github.com/adobe/experience-platform-dsw-reference/)에서 다운로드하십시오.
- [Python >= 2.7](https://www.python.org/downloads/) 및 다음 [!DNL Python] 패키지:
   - [핍](https://pypi.org/project/pip/)
   - [파이YAML](https://pyyaml.org/)
   - [딕터(dictor)](https://pypi.org/project/dictor/)
   - [증권 시세 표시기](https://pypi.org/project/jwt/)
- 이 튜토리얼에 사용된 다음 개념에 대한 작업 이해:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [스키마 컴포지션 기본 사항](../../xdm/schema/field-dictionary.md)

## 소매 판매 스키마 및 데이터 세트 만들기

소매 판매 스키마 및 데이터 세트는 제공된 부트스트랩 스크립트를 사용하여 자동으로 생성됩니다. 다음 단계를 순서대로 수행합니다.

### 파일 구성

1. [!DNL Experience Platform] 자습서 리소스 패키지 내에서 `bootstrap` 디렉터리로 이동한 다음 적절한 텍스트 편집기를 사용하여 `config.yaml`을(를) 엽니다.
2. `Enterprise` 섹션에서 다음 값을 입력합니다.

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. `Platform` 섹션에 있는 값을 편집합니다. 아래 예제를 참조하십시오.

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: API 호출의 기본 경로입니다. 이 값은 수정하지 마십시오.
   - `ims_token`: `{ACCESS_TOKEN}`이(가) 여기에 있습니다.
   - `ingest_data`: 이 자습서에서는 소매 판매 스키마 및 데이터 세트를 만들려면 이 값을 `"True"`(으)로 설정하십시오. 값은 `"False"` 스키마만 만듭니다.
   - `build_recipe_artifacts`: 이 튜토리얼 목적에 따라 스크립트가 Recipe 아티팩트를 생성하지 않도록 하려면 이 값을 로 `"False"` 설정합니다.
   - `kernel_type`: Recipe 아티팩트의 실행 유형입니다. 이 값을 로 설정된 `"False"`것처럼 `build_recipe_artifacts` `Python` 둡니다. 그렇지 않으면 올바른 실행 유형을 지정합니다.

4. `Titles` 섹션에서 소매 판매 샘플 데이터에 대해 다음 정보를 적절하게 제공하고, 편집이 완료되면 파일을 저장하고 닫습니다. 아래 예:

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

1. 터미널 응용 프로그램을 열고 [!DNL Experience Platform] 자습서 리소스 디렉터리로 이동합니다.
2. `bootstrap` 디렉터리를 현재 작업 경로로 설정하고 다음 명령을 입력하여 `bootstrap.py` [!DNL Python] 스크립트를 실행합니다.

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >스크립트를 완료하는 데 몇 분 정도 걸릴 수 있습니다.

## 다음 단계

부트스트랩 스크립트가 완료되면 [!DNL Experience Platform]에서 소매 판매 입력 및 출력 스키마와 데이터 세트를 볼 수 있습니다. [미리 보기 스키마 데이터 튜토리얼](./preview-schema-data.md)을(를) 참조하십시오.
추가 정보.

제공된 부트스트랩 스크립트를 사용하여 소매 판매 샘플 데이터를 [!DNL Experience Platform]에 수집했습니다.

수집된 데이터로 작업을 계속하려면 다음을 수행합니다.
- [Jupyter Notebooks를 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - 데이터 과학 Workspace의 Jupyter Notebooks를 사용하여 데이터에 액세스하고, 탐색하고, 시각화하고, 이해할 수 있습니다.
- [소스 파일을 레시피에 패키징](./package-source-files-recipe.md)
   - 이 튜토리얼 따라 소스 파일을 가져올 수 있는 레시피 파일로 패키징하여 자체 모델을 가져오는 [!DNL Data Science Workspace] 방법을 알아보세요.
