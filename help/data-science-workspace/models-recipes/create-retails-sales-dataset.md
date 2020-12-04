---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics;recipes
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 만들기
topic: tutorial
type: Tutorial
description: 이 자습서에서는 다른 모든 Adobe Experience Platform 데이터 과학 작업 공간 자습서에 필요한 사전 요구 사항 및 자산을 제공합니다. 완료되면 소매 영업 스키마 및 데이터 세트를 Experience Platform에 있는 사용자 및 IMS 조직의 구성원에게 사용할 수 있습니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 소매 판매 스키마 및 데이터 세트 만들기

이 자습서에서는 다른 모든 튜토리얼에 필요한 사전 요구 사항과 에셋을 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 제공합니다. 완료되면 사용자와 IMS 조직의 구성원이 소매 판매 스키마 및 데이터 세트를 사용할 수 있습니다 [!DNL Experience Platform].

## 시작하기

이 튜토리얼을 시작하기 전에 다음 전제 조건이 필요합니다.
- 액세스 권한 [!DNL Adobe Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자 [!DNL Experience Platform]에게 연락하여 진행하십시오.
- API [!DNL Experience Platform] 호출 인증 이 자습서를 [성공적으로 완료하려면 Adobe Experience Platform API](../../tutorials/authentication.md) 인증 및 액세스 튜토리얼을 완료하십시오.
   - 인증: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - 클라이언트 암호: `{CLIENT_SECRET}`
   - 클라이언트 인증서: `{PRIVATE_KEY}`
- 소매 영업 [레서피에 대한 샘플 데이터 및 소스 파일](../pre-built-recipes/retail-sales.md). Adobe 공개 Git 리포지토리에서 이 및 기타 [!DNL Data Science Workspace] 튜토리얼에 필요한 에셋을 [다운로드합니다](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) 및 다음 [!DNL Python] 패키지:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [딕터](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 이 튜토리얼에서 사용되는 다음 개념에 대한 작업 이해:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [스키마 컴포지션의 기본 사항](../../xdm/schema/field-dictionary.md)

## 소매 판매 스키마 및 데이터 세트 만들기

제공된 부트스트랩 스크립트를 사용하여 소매 판매 스키마 및 데이터 세트가 자동으로 생성됩니다. 아래 단계를 순서대로 수행합니다.

### 파일 구성

1. 자습서 리소스 [!DNL Experience Platform] 패키지 내에서 디렉토리로 이동한 `bootstrap`후 적절한 텍스트 편집기를 사용하여 엽니다 `config.yaml` .
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
   - `ims_token` :여기 `{ACCESS_TOKEN}` 가세요
   - `ingest_data` :이 자습서의 목적을 위해 소매 판매 스키마 및 데이터 세트를 만들려면 이 값 `"True"` 을 로 설정합니다. 의 값은 스키마만 `"False"` 생성합니다.
   - `build_recipe_artifacts` :이 자습서의 목적을 위해 스크립트에서 레서피 결함을 생성하지 못하도록 이 값 `"False"` 을 설정합니다.
   - `kernel_type` :레서피 객체의 실행 유형입니다. 이 값을 설정된 `Python` 대로 `build_recipe_artifacts` 두거나 `"False"`올바른 실행 유형을 지정합니다.

4. 섹션에서 소매 판매 샘플 데이터에 대해 다음 정보를 적절히 입력하고 편집한 후 파일을 저장하고 닫습니다. `Titles` 아래에 표시된 예:

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

1. 터미널 애플리케이션을 열고 자습서 리소스 [!DNL Experience Platform] 디렉토리로 이동합니다.
2. 디렉토리를 `bootstrap` 현재 작업 경로로 설정하고 다음 명령을 입력하여 스크립트를 `bootstrap.py` [!DNL Python] 실행합니다.

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >스크립트 작성은 몇 분 정도 걸릴 수 있습니다.

## 다음 단계

부트스트랩 스크립트가 성공적으로 완료되면 소매 판매 입력 및 출력 스키마 및 데이터 세트를 볼 수 있습니다 [!DNL Experience Platform]. 자세한 내용은 [스키마 데이터 미리 보기 자습서](./preview-schema-data.md)를 참조하십시오.

또한 제공된 부트스트랩 스크립트를 사용하여 소매 세일즈 샘플 데이터 [!DNL Experience Platform] 를 인제스트했습니다.

인제스트된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - 데이터 과학 작업 공간의 Jupiter 노트북을 사용하여 데이터를 액세스, 탐색, 시각화 및 이해할 수 있습니다.
- [소스 파일을 레서피로 패키지](./package-source-files-recipe.md)
   - 이 자습서에 따라 소스 파일을 가져올 수 있는 레시피 파일 [!DNL Data Science Workspace] 에 패키징하여 자신만의 모델을 가져오는 방법을 살펴볼 수 있습니다.