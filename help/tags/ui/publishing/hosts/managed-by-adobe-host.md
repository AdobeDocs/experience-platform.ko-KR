---
title: Adobe 관리 호스트 개요
description: Adobe Experience Platform에서 태그 라이브러리 빌드를 배포하기 위한 기본 호스팅 옵션에 대해 알아봅니다.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 55%

---

# Adobe 관리 호스트 개요

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Adobe 관리 호스트는 Adobe Experience Platform에서 태그 라이브러리 빌드를 배포하기 위한 기본 호스트 설정입니다. 데이터 수집 사용자 인터페이스를 통해 새 속성을 만들면 기본 Adobe 관리 호스트가 만들어집니다.

Adobe 관리 호스트를 사용하는 라이브러리 빌드는 Adobe와 계약한 타사 컨텐츠 전달 네트워크(CDN)로 전달됩니다. 이러한 CDN은 Adobe과 독립적으로 작동하므로 Experience Platform이 유지 보수를 받고 있거나 다운되었을 경우 배포된 코드가 사이트 및 애플리케이션에서 정상적으로 계속 작동합니다. Adobe 관리 호스트의 포함 코드는 CDN의 기본 라이브러리 파일을 참조하므로 클라이언트 장치가 런타임 시 이 파일을 검색할 수 있습니다.

이 문서에서는 Experience Platform의 Adobe 관리 호스트에 대한 개요를 제공하며 UI에서 새 Adobe 관리 호스트를 생성하는 방법에 대한 단계를 제공합니다.

## Akamai

현재 Adobe의 기본 CDN 공급자는 [Akamai](https://www.akamai.com/kr/ko/)입니다. Akamai의 강력한 CDN은 전 세계 대량 웹 방문자의 사용자에게 컨텐츠를 제공하도록 빌드되었습니다. CDN은 전 세계 방문자에게 가능한 한 빨리 컨텐츠를 제공하기 위해 로드 밸런싱되고 지리적 최적화 노드로 구성된 중복 네트워크를 실행합니다.

특히 Akamai는 87개국에서 1,150개 이상의 네트워크에 137,000개 이상의 서버를 운영하고 있습니다. 중복성 측면에서 CDN은 한 서버에서 다른 서버로 라우팅될 뿐만 아니라 필요에 따라 서버의 한 노드에서 다른 서버로 라우팅할 수도 있습니다. 즉, 각 노드는 여러 서버로 구성되므로 한 서버가 다운될 때마다 동일한 노드의 다른 서버가 인수할 수 있는 문제가 되지 않습니다.

전체 노드가 작동 중단되면 Akamai는 캐싱된 동일한 콘텐츠가 있는 다음으로 가장 가까운 노드에서 제공됩니다. 노드는 방문자 위치, 트래픽 로드 및 기타 요소에 따라 동적으로 선택되므로 각 방문자에 대해 최선의 로컬 노드에서 일관되게 컨텐츠가 제공됩니다.

Akamai에 호스팅된 파일의 도메인은 `assets.adobedtm.com`입니다. 이는 포함된 `<script>` 코드 내에서 호출되는 방법에 따라 안전하게 참조되거나 그렇지 않을 수 있습니다(`http://` 또는 `https://`).

>[!WARNING]
>
>Akamai 네트워크에서 라이브러리를 사용할 수 없는 경우 Experience Platform에서 이로 인해 발생할 수 있는 오류를 방지할 수 없습니다.

## 라이브러리 빌드 캐싱

Adobe 관리 호스트를 사용하는 경우 라이브러리 빌드가 두 위치에 캐시됩니다.

* [Edge 캐싱](#edge)
* [브라우저 캐싱](#browser)

### Edge 캐싱 {#edge}

CDN의 기본 목적은 컨텐츠를 클라이언트 장치에 의해 보다 빠르게 검색할 수 있도록 지리적으로 최종 사용자에게 더 가까운 서버에 컨텐츠를 지능적으로 배포하는 것입니다. CDN은 전 세계에서 지리적으로 분산된 서버에 사용할 수 있는 컨텐츠(&quot;에지 노드&quot;)의 사본을 만들어 이를 달성합니다.

빌드가 Adobe 관리 호스트에 배포되면 CDN은 여러 중앙 서버(&quot;원본&quot;)에 빌드를 배포한 다음 빌드의 사본을 캐싱하기 위해 전 세계에 있는 여러 다양한 에지 노드로 보냅니다. 이러한 에지 노드에 저장된 빌드의 캐싱된 버전은 최종적으로 클라이언트 장치에 제공됩니다.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Adobe 관리 호스트의 경우 새로운 환경에 처음 게시된 라이브러리가 글로벌 CDN에 전파하는 데 최대 5분이 걸릴 수 있습니다.

에지 노드가 특정 파일(예: 라이브러리 빌드)에 대한 요청을 받으면 노드가 먼저 파일의 만료 시간을 확인합니다. 시간이 만료되지 않은 경우 에지 노드에서 캐싱된 버전을 제공합니다. 시간이 만료된 경우 에지 노드는 가장 가까운 원본에서 새 복사본을 요청하며 새로 고침된 복사본을 제공하고 새 만료 시간으로 새로 고침된 복사본을 캐싱합니다.

>[!NOTE]
>
>에지 노드 캐싱 외에도 자체 캐싱을 수행하는 중간 네트워크(예: 회사 또는 모바일 네트워크)도 있을 수 있습니다. 빌드가 예상대로 캐싱되지 않으면 이러한 네트워크가 기본 원인일 수 있습니다.

#### Edge 캐시 무효화 {#invalidation}

새 라이브러리 빌드를 업로드할 때 적용 가능한 모든 에지 노드의 캐시가 무효화됩니다. 즉, 최근 새 복사본을 검색한 방법과 관계없이 각 노드는 캐시된 버전을 유효하지 않은 것으로 간주합니다. 다음에 에지 노드가 해당 파일에 대한 요청을 받으면 노드가 원본에서 새 사본을 검색합니다.

Akamai에는 여러 원본 서버가 있어 서로 간에 파일을 복제하고, 파일을 먼저 받은 원본을 알 수 없기 때문에 이러한 노드 요청이 최신 버전이 없는 원본을 히트할 수 있습니다. 그런 다음 이전 버전을 다시 캐시합니다. 이러한 문제가 발생하지 않도록 하기 위해 다음 간격으로 새 빌드에 대해 여러 개의 캐시 무효화가 수행됩니다.

* 업로드 후 즉시
* 업로드 후 5분
* 업로드 후 60분

이러한 시차를 둔 캐시 무효화 기능을 통해 원본 서버 그룹이 최신 버전의 파일을 자체 간에 복제할 수 있으므로 파일을 검색할 때 모두 최신 버전을 보유하게 됩니다.

### 브라우저 캐싱 {#browser}

또한 라이브러리 빌드는 `cache-control` HTTP 헤더를 사용하여 브라우저에 캐싱됩니다. Adobe 관리 호스트를 사용하는 경우 API 응답으로 반환되는 헤더를 제어할 수 없으므로 캐싱에 대한 Adobe 기본값이 사용됩니다. 즉, Adobe 관리 호스트에 사용자 지정 헤더를 활용할 수 없습니다. 사용자 지정 `cache-control` 헤더가 필요한 경우 [자체 호스팅](self-hosting-libraries.md)을 대신 고려할 수 있습니다.

브라우저에 캐싱되는 라이브러리 빌드(`cache-control` 헤더에서 결정됨)의 만료 시간은 사용 중인 태그 환경에 따라 달라집니다.

| 환경 | `cache-control` 값 |
| --- | --- |
| 개발 | `max-age=0, no-cache, no-store` |
| 스테이징 | `max-age=0, no-cache, no-store` |
| 프로덕션 | `max-age=3600` |

위의 테이블에서 알 수 있듯이 개발 및 스테이징 환경에서 브라우저 캐싱은 지원되지 않습니다. 따라서 높은 트래픽 또는 프로덕션 컨텍스트에서는 개발 또는 스테이징 포함 코드를 사용할 수 없습니다.

Cache-control 헤더는 기본 라이브러리 빌드에만 적용됩니다. 기본 라이브러리 아래에 있는 모든 하위 리소스는 항상 순-신규로 간주되므로 브라우저에서 캐싱할 필요가 없습니다.

## UI에서 Adobe 관리 호스팅 사용

Experience Platform UI 또는 데이터 수집 UI에서 속성을 처음 만들면 Adobe 관리 호스트가 자동으로 생성됩니다. 즉시 사용 가능한 속성이 있는 사용 가능한 모든 환경도 기본적으로 Adobe 관리 호스트에 할당됩니다.

>[!NOTE]
>
>모든 환경에서 기본 Adobe 관리 호스트가 할당되지 않은 경우 호스트를 삭제할 수 있습니다. 이 작업을 수행한 후 Adobe 관리 호스트로 다시 전환하려면 다음 단계를 통해 새 호스트를 생성할 수 있습니다.
>
>1. 속성에서 **[!UICONTROL 호스트]** 탭을 선택한 다음 **[!UICONTROL 호스트 추가]**&#x200B;를 선택합니다.
>1. 호스트 이름을 입력하고 호스트 유형으로 **[!UICONTROL Adobe에서 관리]**&#x200B;를 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.
>
>그런 다음 Adobe 관리 호스트에 환경을 원하는 대로 다시 할당할 수 있습니다.

## 다음 단계

이 문서에서는 Adobe Experience Platform의 태그 라이브러리에 대한 Adobe 관리 호스팅에 대한 개요를 제공합니다. 기타 호스팅 옵션에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [SFTP 호스팅](./sftp-host.md)
* [자체 호스팅 라이브러리](./self-hosting-libraries.md)

환경을 위한 호스트를 관리하는 방법에 대한 자세한 내용은 [환경 안내서](../environments.md)를 참조하십시오.
