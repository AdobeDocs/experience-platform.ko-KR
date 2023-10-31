---
description: 지원되는 ID 및 속성 매핑 구성에 대한 대상을 구성하는 방법에 대해 알아봅니다.
title: 지원되는 매핑 구성
exl-id: a477a3f2-a229-4b22-8588-ee58bd5436c6
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---

# 지원되는 매핑 구성

Destination SDK으로 빌드된 대상은 대상 유형을 기반으로 특정 ID 네임스페이스 및 속성 매핑 구성을 지원합니다.

이 문서에서는 대상을 구성할 때 사용할 수 있는 지원되는 모든 매핑 구성에 대해 설명합니다.

>[!WARNING]
>
>이 문서에 설명되지 않은 모든 매핑 구성은 Destination SDK에서 지원되지 않습니다.

대상을 작성할 때 이 페이지에 설명된 매핑 구성 중 하나에 따라 스키마 및 ID 네임스페이스를 구성합니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 스트리밍 대상에 대해 지원되는 매핑 {#streaming-mappings}

Destination SDK으로 구축된 실시간(스트리밍) 대상은 아래 표에 설명된 매핑 구성을 지원합니다.

| 소스 필드 | 대상 필드 |
| --- | --- |
| XDM 속성 | 사용자 지정 속성 |
| ID 네임스페이스 | ID 네임스페이스 |

아래 구성 예제를 통해 위의 표에서 두 매핑을 모두 사용할 수 있습니다.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### XDM 속성을 사용자 지정 속성에 매핑 {#streaming-xdm-to-custom}

사용자는 소스 XDM 프로필의 속성을 대상 측의 사용자 지정 속성에 매핑할 수 있습니다.

대상 필드 매핑을 선택할 때는 대상 사용자 지정 속성의 이름을 수동으로 입력해야 합니다.

![사용자 지정 속성 선택을 보여 주는 플랫폼 UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

결과 UI 경험이 아래 이미지에 표시됩니다.

![스트리밍 대상의 사용자 지정 속성에 대한 XDM 속성 매핑을 보여 주는 플랫폼 UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### ID 네임스페이스를 파트너 ID 네임스페이스에 매핑 {#streaming-identity-to-identity}

사용자는 Platform에서 정의한 ID 네임스페이스에 사용자 정의 또는 전역 ID 네임스페이스를 매핑할 수 있습니다.

결과 UI 경험이 아래 이미지에 표시됩니다.

![스트리밍 대상의 ID에 대한 ID 매핑을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## 파일 기반 대상에 대해 지원되는 매핑 {#batch-mappings}

Destination SDK으로 빌드된 파일 기반 대상은 아래 표에 설명된 매핑 구성을 지원합니다. 자세한 매핑 예는 다음 섹션을 참조하십시오.

| 소스 필드 | 대상 필드 |
| --- | --- |
| XDM 속성 | 속성 / 사용자 지정 속성 |
| ID 네임스페이스 | 속성 / 사용자 지정 속성 |
| ID 네임스페이스 | ID 네임스페이스 |

아래 구성 예제를 통해 고객은 위 표의 모든 매핑을 사용할 수 있습니다.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### XDM 속성을 사용자 지정 속성에 매핑 {#batch-xdm-to-custom}

사용자는 소스 XDM 프로필의 속성을 대상 측의 사용자 지정 속성에 매핑할 수 있습니다.

파일 기반 대상의 경우 대상 필드는 소스 필드와 이름이 같은 기본 속성으로 자동 채워집니다.

결과 UI 경험이 아래 이미지에 표시됩니다.

![파일 기반 대상의 사용자 지정 속성에 대한 XDM 매핑을 보여 주는 Platform UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

사용자는 기본 이름을 그대로 두거나 대상 필드 선택 화면에 사용자 지정 속성 이름을 입력할 수 있습니다.

![파일 기반 대상에 대한 사용자 지정 타겟 속성 선택을 보여 주는 Platform UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### ID 네임스페이스를 사용자 지정 속성에 매핑 {#batch-identity-to-custom}

사용자는 Platform에서 사용자 정의 또는 전역 ID 네임스페이스를 대상 측의 사용자 정의 속성에 매핑할 수 있습니다.

ID 네임스페이스를 소스 필드로 선택하면 대상 필드에 동등한 ID 네임스페이스가 자동으로 채워집니다. 대상 필드를 사용자 지정 속성으로 바꾸려면 사용자가 대상 필드 선택 화면에 사용자 지정 속성 이름을 입력해야 합니다.

![파일 기반 대상에 대한 사용자 지정 타겟 속성 선택을 보여 주는 Platform UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

결과 UI 경험이 아래 이미지에 표시됩니다.

![파일 기반 대상의 사용자 지정 속성에 대한 ID 매핑을 보여 주는 Platform UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### ID 네임스페이스를 파트너 ID 네임스페이스에 매핑 {#batch-identity-to-identity}

사용자는 Platform에서 사용자 정의 또는 글로벌 ID 네임스페이스를 동일한 ID 네임스페이스에 매핑할 수 있습니다.

ID 네임스페이스를 소스 필드로 선택하면 대상 필드에 동등한 ID 네임스페이스가 자동으로 채워집니다.

결과 UI 경험이 아래 이미지에 표시됩니다.

![파일 기반 대상의 ID에 대한 ID 매핑을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## 다음 단계 {#next-steps}

이 문서를 읽고 나면 Destination SDK으로 빌드된 대상에서 지원하는 매핑에 대해 보다 잘 이해할 수 있습니다.

다른 대상 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [일괄 처리 구성](batch-configuration.md)
* [과거 프로필 자격 요건](historical-profile-qualifications.md)
