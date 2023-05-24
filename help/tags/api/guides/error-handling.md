---
title: 오류 처리
description: Reactor API에서 오류를 처리하는 방법에 대해 알아봅니다.
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# 오류 처리

Reactor API를 호출하는 동안 문제가 발생하면 다음 방법 중 하나로 오류가 반환될 수 있습니다.

* **즉각적인 오류**: 즉각적인 오류가 발생하는 요청을 수행할 때 API에 의해 오류 응답이 반환되고, HTTP 상태는 발생한 일반 오류 유형을 반영합니다.
* **지연된 오류**: 지연된 오류(예: 비동기 활동)를 초래하는 API 요청을 수행할 때에서 API에 의해 오류가 반환될 수 있습니다. `meta.status_details` 관련 리소스.

## 오류 형식

오류 응답은 다음을 준수하는 것을 목표로 합니다. [JSON:API 오류 사양](http://jsonapi.org/format/#errors)및 는 일반적으로 다음 구조를 준수합니다.

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 문제가 발생하는 특정 항목에 대한 고유 식별자입니다. |
| `status` | 이 문제에 적용할 수 있는 HTTP 상태 코드이며, 문자열 값으로 표현됩니다. |
| `code` | 문자열 값으로 표현되는 애플리케이션별 오류 코드. |
| `title` | 사람이 인식할 수 있는 짧은 문제 요약 **변경하지 말아야 함** 현지화 목적을 제외하고 발생 시 ~ 발생 시. |
| `detail` | 사람이 인식할 수 있는 이 문제 발생 관련 설명. 좋아요 `title`, 이 필드의 값은 현지화될 수 있습니다. |
| `source` | 다음 멤버를 선택적으로 포함하여 오류 소스에 대한 참조를 포함하는 객체입니다.<ul><li>`pointer`: a [JSON 포인터(RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) 요청 문서에서 연결된 엔티티를 참조하는 문자열(예: `/data` 기본 데이터 객체의 경우 또는 `/data/attributes/title` (특정 속성의 경우).</li></ul> |
| `meta` | 오류에 대한 비표준 메타데이터를 포함하는 객체입니다. |

{style="table-layout:auto"}

## 오류 참조

다음 표에는 API가 반환할 수 있는 다양한 오류가 나와 있습니다.

| 오류 제목 | 설명 |
| --- | --- |
| `authentication-failure` | IMS 액세스 토큰이 잘못되었습니다. 다시 로그인하여 새 액세스 토큰을 받을 수 있습니다. 또는 기술 계정의 경우 새 JWT를 생성하고 IMS 액세스 토큰으로 바꿉니다. |
| `connection-refused` | 서버에 연결할 수 없습니다. |
| `decrypt-bad-passphrase` | 제공된 암호로 데이터의 암호를 해독할 수 없습니다. |
| `decrypt-failed` | 제공된 개인 키로 데이터의 암호를 해독할 수 없습니다. 키가 로컬에서 작동하고 공백이 잘렸는지 확인합니다. |
| `decrypt-no-data` | 개인 키가 없으면 데이터의 암호를 해독할 수 없습니다. 암호화된 개인 키를 제공하십시오. |
| `delegate-descriptor-unresolved` | 확장에서 이 위임 설명자에 대한 예상 정의를 제공하지 않았습니다. 확장을 업데이트해야 할 수 있습니다. |
| `deleted-resources` | 라이브러리에 추가하려는 리소스가 삭제되었습니다. |
| `environment-in-use` | 환경은 한 번에 하나의 라이브러리에만 할당할 수 있습니다. 옵션 1은 다른 환경을 선택하는 것입니다. 옵션 2는 라이브러리를 다른 환경으로 이동하거나 라이브러리를 삭제하여 이 환경을 해제하는 것입니다. |
| `environment-required` | 빌드를 만들려면 먼저 라이브러리에 환경이 할당되어 있어야 합니다. |
| `extension-not-found` | 데이터 요소 또는 규칙 구성 요소를 정의하는 확장은 라이브러리에 포함되지 않습니다. 필요한 모든 확장이 라이브러리에 추가되었는지 확인합니다. |
| `extension-package-path-error` | extension.json에 정의된 경로가 잘못 생성되었습니다. |
| `extension-package-transform-definition-error` | 개체 속성에 대해 잘못된 변형을 정의했습니다. 각 개체 속성에는 하나의 변환이 정의되어 있을 수 있으며 파일 변환이거나 함수 변환이어야 합니다. |
| `extension-package-zip-error` | ExtensionPackage의 압축을 풀거나 배포할 파일의 압축을 푸는 동안 오류가 발생했습니다. |
| `host-in-use` | 하나 이상의 환경에서 호스트를 사용하는 경우 호스트를 삭제할 수 없습니다. |
| `host-required` | 이 라이브러리에 할당된 환경에 올바른 호스트가 없습니다. 라이브러리에 할당된 환경을 확인합니다. 그런 다음 해당 환경에 유효한 호스트를 할당합니다. |
| `host-type-error` | SFTP 호스트만 사용하기 전에 자격 증명을 확인해야 하므로 해당 호스트 유형에 대해서만 사전 테스트를 사용할 수 있습니다. |
| `illegal-custom-code-transform` | customCode 변환은 사용할 수 없습니다. 함수 또는 파일 변형을 지정하십시오. |
| `ims-not-authorized` | 계정을 인증하는 도중 알 수 없는 오류가 발생했습니다. 나중에 다시 시도하십시오. |
| `ims-session-error` | 로그인 세션에 문제가 있습니다. 로그아웃했다가 다시 로그인하십시오. |
| `internal-error` | 내부 오류가 발생했습니다. 잠시 기다린 후 다시 시도해 주십시오. 문제가 지속되면 클라이언트 지원 센터에 문의하십시오. |
| `invalid-data_element` | 잘못된 데이터 요소를 라이브러리에 추가할 수 없습니다. |
| `invalid-embed_code` | 올바른 포함 코드가 아니거나 개발 또는 스테이징 환경에 연결하려고 합니다. Dynamic DTM(Tag Management) 포함 코드는 프로덕션 환경에만 연결할 수 있습니다. |
| `invalid-extension` | 잘못된 확장을 라이브러리에 추가할 수 없습니다. |
| `invalid-extension_package_id` | 확장 패키지의 일부 개체 속성만 수정할 수 있습니다. 허용되지 않는 항목 중 하나를 수정하려고 했습니다. |
| `invalid-new-owner-org-id` | 할당하려는 조직 ID가 올바른 조직 ID가 아닙니다. |
| `invalid-org` | 활성 조직이 API에 액세스할 수 없습니다. 올바른 조직을 사용하고 있는지 확인하십시오. |
| `invalid-rule` | 잘못된 규칙을 라이브러리에 추가할 수 없습니다. |
| `invalid-settings-syntax` | 설정 JSON을 구문 분석하는 동안 구문 오류가 발생했습니다. |
| `library-file-not-found` | zip 패키지 내에서 extension.json에 정의된 필수 파일을 찾을 수 없습니다. |
| `minification-error` | 잘못된 코드로 인해 코드를 컴파일할 수 없습니다. |
| `multiple-revisions` | 각 리소스의 버전은 하나만 라이브러리에 포함할 수 있습니다. |
| `no-available-orgs` | 이 사용자 계정은 태그에 대한 액세스 권한이 있는 제품 프로필에 속하지 않습니다. Admin Console을 사용하여 태그 권한이 있는 제품 프로필에 이 사용자를 추가하십시오. |
| `not-authorized` | 이 사용자 계정에는 이 작업을 수행하는 데 필요한 권한이 없습니다. |
| `not-found` | 기록을 찾을 수 없습니다. 검색하려는 개체의 ID를 확인합니다. |
| `not-unique` | 사용하려는 이름이 이미 사용 중입니다. 이 리소스의 경우 &#39;name&#39; 속성은 고유해야 합니다. |
| `public-release-not-authorized` | 확장의 공개 릴리스는 다음을 통해 조정됩니다. `launch-ext-dev@adobe.com`. 다음에 대한 문서 보기: [확장 해제](../../extension-dev/submit/release.md) 추가 정보. |
| `read-only` | 이 리소스는 읽기 전용이므로 수정할 수 없습니다. |
| `session-timeout` | 사용자 세션이 만료되었습니다. 로그아웃했다가 다시 로그인하십시오. |
| `sftp-authentication-failed` | SFTP 연결에 대한 인증에 실패했습니다. |
| `sftp-connection-timeout` | SFTP 연결 시간이 초과되었습니다. |
| `sftp-exception` | SFTP를 사용하여 서버에 연결할 때 예외가 발생했습니다. |
| `sftp-status-exception` | 서버와 통신하려는 도중 SFTP 예외가 발생했습니다. |
| `socket-error` | 서버와 통신하는 동안 소켓 오류가 발생했습니다. |
| `ssh-disconnect` | SSH 세션의 연결이 끊어졌습니다. |
| `timeout-error` | 서버와의 연결 시간이 초과되었습니다. |
| `unknown-error` | 예기치 않은 오류가 발생했습니다. 나중에 다시 시도하거나 고객 지원 센터에 문의하여 진행 상황을 설명할 수 있습니다. |
| `unsupported-custom-code-language` | 지원되지 않는 사용자 지정 코드 언어가 제공되었습니다. |
| `upgraded-extension-required` | 확장 업그레이드를 설치한 후에는 업그레이드가 프로덕션에 도달할 때까지 모든 라이브러리에 확장 업그레이드를 포함해야 합니다. 유일한 예외는 확장이 아직 게시되지 않은 경우입니다. |
| `upstream-build-required` | 이 라이브러리를 빌드하려면 먼저 업스트림 라이브러리에 대해 성공적으로 빌드해야 합니다. |

{style="table-layout:auto"}
