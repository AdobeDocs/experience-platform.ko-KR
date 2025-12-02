---
title: 미디어 이벤트 보내기
description: Adobe Experience Platform Edge Network으로 미디어 데이터를 전송합니다.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# 미디어 이벤트 보내기

**[!UICONTROL Send media event]** 작업은 미디어 이벤트를 데이터스트림으로 보내며, 이 데이터스트림은 Adobe Experience Platform 또는 Adobe Analytics과 같은 앱 및 서비스에서 사용할 수 있습니다. 이 작업은 속성에서 스트리밍 미디어 콘텐츠를 추적할 때 유용합니다.

![미디어 이벤트 보내기 화면을 표시하는 Experience Platform UI 이미지입니다.](../assets/send-media-event.png)

사용 가능한 옵션은 선택한 **[!UICONTROL Media event type]**&#x200B;에 따라 다릅니다. 모든 미디어 이벤트 유형에는 콘텐츠 플레이어 이름인 **[!UICONTROL Player ID]**&#x200B;이(가) 필요합니다.

일부 이벤트 유형은 다른 필드를 구성하는 기능을 제공합니다. 미디어 이벤트 유형이 여기에 나열되지 않으면 [!UICONTROL Player ID] 필드만 사용할 수 있습니다. 다음 미디어 이벤트 유형에는 다른 필드가 포함됩니다.

## [!UICONTROL Ad break start]

광고 Pod 세부 사항을 구성할 수 있습니다.

* **[!UICONTROL Ad break name]**: 친숙한 광고 브레이크 이름입니다.
* **[!UICONTROL Ad break offset (seconds)]**: 콘텐츠 내부의 광고 브레이크 오프셋(초)입니다.
* **[!UICONTROL Ad break index]**: 콘텐츠 내부의 광고 브레이크 색인(1부터 시작).

## [!UICONTROL Ad start]

광고 세부 정보를 구성할 수 있습니다.

* **[!UICONTROL Ad name]**: 친숙한 광고 이름입니다.
* **[!UICONTROL Ad ID]**: 광고 ID입니다. 모든 영숫자 값이 지원됩니다.
* **[!UICONTROL Ad length (seconds)]**: 비디오 광고의 길이(초)입니다.
* **[!UICONTROL Advertiser]**: 광고에서 다루고 있는 제품의 회사 또는 브랜드입니다.
* **[!UICONTROL Campaign ID]**: 광고 캠페인의 ID입니다.
* **[!UICONTROL Creative ID]**: 광고 문안의 ID입니다.
* **[!UICONTROL Creative URL]**: 광고 문안의 URL.
* **[!UICONTROL Placement ID]**: 광고 배치 ID입니다.
* **[!UICONTROL Site ID]**: 광고 사이트의 ID입니다.
* **[!UICONTROL Pod position]**: 부모 광고 브레이크 내에 있는 광고 인덱스(0부터 시작).

이 이벤트 유형은 사용자 지정 메타데이터를 미디어 이벤트 페이로드의 일부로 제공하는 기능도 지원합니다.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**: 비트율, 드롭된 프레임, 초당 프레임 및 시작 시간을 지정하는 [체감 품질](/help/xdm/data-types/qoe-data-details-collection.md) 개체입니다.

## [!UICONTROL Chapter start]

챕터 세부 사항을 구성할 수 있습니다.

* **[!UICONTROL Chapter name]**: 챕터 또는 세그먼트의 이름입니다.
* **[!UICONTROL Chapter length]**: 챕터의 길이(초)입니다.
* **[!UICONTROL Chapter index]**: 콘텐츠 내부의 챕터 위치입니다.
* **[!UICONTROL Chapter offset]**: 콘텐츠 시작부터 챕터의 오프셋(초)입니다.

이 이벤트 유형은 사용자 지정 메타데이터를 미디어 이벤트 페이로드의 일부로 제공하는 기능도 지원합니다.

## [!UICONTROL Error]

오류 세부 정보를 구성할 수 있습니다.

* **[!UICONTROL Error name]**: 오류 이름입니다.
* **[!UICONTROL Source]**: 오류의 원인입니다.

## [!UICONTROL Session start]

미디어 세션 세부 사항을 구성할 수 있습니다.

* **[!UICONTROL Handle media session automatically]**: 웹 SDK에서 필요한 ping을 자동으로 보낼 수 있는 확인란입니다. 수동으로 Ping을 전송하려면 이 확인란의 선택을 취소할 수 있습니다.
* **[!UICONTROL Playhead]**: 재생 플레이헤드(초)입니다.
* **[!UICONTROL Content type]**: 콘텐츠 형식입니다. 모든 문자열 값이 지원됩니다. Adobe은 다음 사전 설정도 제공합니다.
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**: 사용되는 콘텐츠의 최대 기간(초)입니다. 알 수 없는 기간이 있는 Live Media의 경우 `86400` 값이 기본값입니다.
* **[!UICONTROL Content ID]**: 콘텐츠의 콘텐츠 ID입니다.
* **[!UICONTROL Ad load type]**: 로드된 광고 유형입니다. 다음 두 가지 값이 지원됩니다.
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**: 노래가 속한 앨범입니다.
* **[!UICONTROL Artist]**: 이 곡의 아티스트입니다.
* **[!UICONTROL Asset ID]**: 미디어 에셋의 콘텐츠에 대한 고유 식별자입니다. 이러한 ID는 일반적으로 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 권한에서 파생됩니다. 이러한 식별자는 다른 소유권 또는 사내 시스템에서도 사용할 수 있습니다.
* **[!UICONTROL Author]**: 오디오북 작성자의 이름입니다.
* **[!UICONTROL Authorized]**: 사용자가 Adobe 인증을 통해 로그인했는지 여부를 결정하는 플래그입니다.
* **[!UICONTROL Day part]**: 콘텐츠가 브로드캐스트 또는 재생되는 시간입니다. 모든 문자열 값이 지원됩니다.
* **[!UICONTROL Episode]**: 에피소드 번호입니다.
* **[!UICONTROL Feed type]**: 피드 유형입니다.
* **[!UICONTROL First air date]**: 콘텐츠가 TV에 처음 방송된 날짜입니다. Adobe 모든 문자열 값이 지원됩니다. 하지만 `YYYY-MM-DD` 형식을 사용하는 것이 좋습니다.
* **[!UICONTROL First digital date]**: 디지털 채널 또는 플랫폼에서 콘텐츠가 처음으로 방송된 날짜입니다. Adobe 모든 문자열 값이 지원됩니다. 하지만 `YYYY-MM-DD` 형식을 사용하는 것이 좋습니다.
* **[!UICONTROL Content name]**: 콘텐츠의 알기 쉬운 이름.
* **[!UICONTROL Genre]**: 콘텐츠 생성자가 정의한 콘텐츠의 유형 또는 그룹입니다. 이 필드는 쉼표로 구분된 여러 값을 지원합니다.
* **[!UICONTROL Label]**: 레코드 레이블의 이름입니다.
* **[!UICONTROL Rating]**: TV 유해 콘텐츠 가이드라인으로 정의된 등급입니다.
* **[!UICONTROL MVPD]**: Adobe 인증에서 제공한 MVPD.
* **[!UICONTROL Network]**: 네트워크 또는 채널 이름입니다.
* **[!UICONTROL Originator]**: 콘텐츠 작성자입니다.
* **[!UICONTROL Publisher]**: 오디오 콘텐츠 게시자입니다.
* **[!UICONTROL Season]**: 쇼가 시리즈의 일부인 경우 쇼의 시즌 번호입니다.
* **[!UICONTROL Show]**: 표시가 시리즈의 일부인 경우 시리즈 이름입니다.
* **[!UICONTROL Show type]**: 표시 유형입니다. 모든 문자열 값이 지원됩니다. Adobe은 다음 사전 설정도 제공합니다.
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**: 스트림 유형입니다.
* **[!UICONTROL Stream format]**: HD 또는 SD와 같은 스트림의 형식입니다.
* **[!UICONTROL Station]**: 라디오 방송국의 이름 또는 ID.

이 이벤트 유형은 사용자 지정 메타데이터를 미디어 이벤트 페이로드의 일부로 제공하는 기능도 지원합니다. 또한 데이터 스트림 구성 재정의를 허용하므로 이 데이터를 수신하는 앱 및 서비스를 제어할 수 있습니다. 개별 명령과 태그 확장 구성 설정 모두에서 데이터스트림 구성 재정의를 설정하면 개별 명령이 우선합니다. 자세한 내용은 [데이터 스트림 구성 재정의](../configure/configuration-overrides.md)를 참조하십시오.

## [!UICONTROL States update]

상태 업데이트 세부 사항을 구성할 수 있습니다. 다음 상태를 시작하거나 종료할 수 있습니다.

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

다음 필드를 사용할 수 있습니다.

* **[!UICONTROL States started]**: 상태가 시작되었음을 나타내는 드롭다운 메뉴입니다. **[!UICONTROL Add another state that started]** 단추를 선택하면 동일한 작업에서 여러 상태를 시작할 수 있습니다.
* **[!UICONTROL States ended]**: 상태가 종료되었음을 나타내는 드롭다운 메뉴입니다. **[!UICONTROL Add another state that ended]** 단추를 선택하면 동일한 작업에서 여러 상태를 종료할 수 있습니다.
