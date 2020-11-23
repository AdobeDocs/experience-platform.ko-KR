---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: 스키마 레지스트리 API 개발자 가이드
description: '스키마 레지스트리 API를 사용하면 Experience Platform 내에서 사용 가능한 모든 스키마 및 관련 XDM 리소스를 프로그래밍 방식으로 관리할 수 있습니다. '
topic: developer guide
translation-type: tm+mt
source-git-commit: d0e5865fddcf2592e9b6d8d4b2747bdceee6bda7
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# [!DNL Schema Registry] API 개발자 가이드

이 [!DNL Schema Registry] 는 사용 가능한 모든 라이브러리 리소스에 액세스할 수 있는 사용자 인터페이스와 RESTful API를 제공하여 Adobe Experience Platform 내의 스키마 라이브러리에 액세스하는 데 사용됩니다.

스키마 레지스트리 API는 플랫폼 내에서 사용 가능한 모든 스키마 및 관련 XDM(Experience Data Model) 리소스를 프로그래밍 방식으로 관리할 수 있도록 해주는 여러 끝점을 제공합니다. 여기에는 애플리케이션을 사용하는 Adobe, 파트너 및 공급업체에서 정의한 애플리케이션이 포함됩니다. [!DNL Experience Platform]

이러한 끝점은 아래에 요약되어 있습니다. 자세한 내용은 개별 종단점 안내서를 참조하고 필요한 헤더, 샘플 API 호출 읽기 등에 대한 [자세한 내용은 시작 안내서](./getting-started.md) 를 참조하십시오.

>[!IMPORTANT]
>
>XDM은 JSON 스키마 포맷을 사용하여 인제스트된 고객 경험 데이터의 구조를 설명하고 검증합니다. 스키마 레지스트리 API를 사용하기 전에 이 기본 기술에 대한 더 나은 이해를 위해 [공식 JSON 스키마 설명서를](https://json-schema.org/) 검토하는 것이 좋습니다.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [스키마 레지스트리 API 참조를 방문하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## 스키마

XDM 스키마는 Platform으로 인제스트된 데이터의 구조와 형식을 나타내고 유효성을 확인합니다. 스키마는 클래스와 0개 이상의 혼합으로 구성됩니다. 끝점을 사용하여 스키마를 생성, 보기, 편집 및 삭제할 수 `/schemas` 있습니다. 이 끝점을 사용하는 방법에 대해 알아보려면 [스키마 끝점 안내서를 참조하십시오](./schemas.md).

스키마 레지스트리 API에서 믹싱 및 데이터 유형 추가 등 전체 스키마를 만드는 방법에 대한 단계별 지침은 [API 스키마 만들기 자습서를 참조하십시오](../tutorials/create-schema-api.md).

## 클래스

클래스는 스키마에 포함할 데이터의 동작 측면(레코드 또는 시간 시리즈)을 정의합니다. 또한 클래스는 해당 클래스를 기반으로 하는 모든 스키마가 포함해야 하는 공통 속성의 기본 구조를 결정합니다. 스키마의 클래스는 해당 스키마에 사용할 수 있는 믹스를 결정합니다. API에서 클래스 [작업에 대한 자세한 내용은 클래스 끝점 안내서](./classes.md) 를 참조하십시오.

## 믹신

믹서는 개인, 우편 주소 또는 웹 브라우저 환경과 같은 특정 개념을 나타내는 하나 이상의 필드를 정의하는 구성 요소를 재사용할 수 있습니다. 믹스인은 호환 클래스를 구현하는 스키마의 일부로 포함되도록 합니다. 이 스키마의 데이터 비헤이비어(레코드 또는 시간 시리즈)에 따라 달라집니다. API에서 [혼합으로 작업하는 방법을 알아보려면 믹싱 종단점 안내서를](./mixins.md) 참조하십시오.

## 데이터 유형

데이터 유형은 기본 리터럴 필드와 같은 방식으로 클래스 또는 믹싱에서 참조 유형 필드로 사용되며, 데이터 유형이 여러 하위 필드를 정의할 수 있다는 점에서 중요한 차이가 있습니다. 다중 필드 구조를 일관되게 사용할 수 있다는 점에서 혼합과 유사하지만, 데이터 유형은 스키마 구조의 어느 위치에나 포함될 수 있는 반면 혼합은 루트 수준에서만 추가할 수 있으므로 보다 유연합니다. API의 데이터 유형 작업에 대한 자세한 내용은 [데이터 유형 끝점 안내서](./data-types.md) 를 참조하십시오.

## 설명자

설명자는 스키마 내의 특정 필드에 지정된 메타데이터 집합으로, 해당 필드(및 스키마 자체)가 다른 스키마와 관련된 방식을 비롯하여 다양한 컨텍스트 세부 정보를 제공합니다. 각 스키마에는 하나 이상의 설명자 개체가 적용될 수 있으며 서로 다른 용도를 제공하는 여러 가지 설명자 유형이 있습니다. API의 설명자 [작업에 대한 자세한 내용, 다양한 설명자 유형 및 사용 사례에 대한 개요는 설명자 끝점 안내서](./descriptors.md) 를 참조하십시오.

## 노조

Platform을 사용하면 특정 사용 사례에 대해 스키마를 구성할 수 있지만, 특정 클래스에 속하는 스키마의 &quot;union&quot;을 작성할 수도 있습니다. 결합 스키마는 동일한 클래스를 공유하는 모든 스키마의 필드를 단일 표현으로 취합합니다. 실시간 고객 프로필과 함께 사용할 수 있도록 스키마를 활성화하면 [해당](../../profile/home.md)스키마는 특정 클래스에 대한 유니폼에 포함됩니다. 따라서 결합 스키마는 직접 편집할 수 없으며 프로필에서 사용할 스키마를 포함하거나 제외해야만 영향을 받을 수 있습니다.

스키마 레지스트리 API에서 조합을 보는 방법에 대한 자세한 내용은 [조합 끝점 안내서를 참조하십시오](./unions.md).

## 내보내기/가져오기

스키마 레지스트리 API를 사용하면 샌드박스와 IMS 조직 간에 XDM 리소스를 전송하고 공유할 수 있습니다. 스키마, 혼합 또는 데이터 유형의 경우 리소스 구조와 종속 리소스가 포함된 내보내기 페이로드를 생성할 수 있습니다. 그런 다음 이 페이로드를 사용하여 리소스를 대상 샌드박스 및 IMS Org로 가져올 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [스키마 레지스트리 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) 를 참조하십시오.

## 샘플 데이터

스키마 라이브러리 내에서 지정된 스키마에 대한 샘플 데이터를 생성할 수 있습니다. 그런 다음 반환된 응답 개체를 데이터 수집의 소스로 사용할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [스키마 레지스트리 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) 를 참조하십시오.

## 감사 로그

스키마 레지스트리는 다른 업데이트 간에 리소스(클래스, 혼합, 데이터 유형 또는 스키마)에 발생한 모든 변경 사항의 로그를 유지 관리합니다. 특정 리소스에 대한 로그를 검색할 수 있습니다. 이 종단점에 대한 GET 요청 경로 `$id` 또는 `meta:altId` 를 제공하여 로그를 검색할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [스키마 레지스트리 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) 를 참조하십시오.

## 다음 단계

스키마 레지스트리 API를 사용하여 호출을 시작하려면 [시작 안내서](./getting-started.md) 를 읽은 다음 끝점 가이드 중 하나를 선택하여 특정 끝점을 사용하는 방법을 학습합니다.