---
title: Adobe Analytics Source 커넥터에 대한 매핑 필드
description: Analytics Source Connector를 사용하여 Adobe Analytics 필드를 XDM 필드에 매핑합니다.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 316879afe8c94657156c768cdc14d4710da9fd35
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 6%

---

# Analytics 필드 매핑

Adobe Experience Platform을 사용하면 Analytics 소스를 통해 Adobe Analytics 데이터를 수집할 수 있습니다. ADC를 통해 수집된 데이터 중 일부는 Analytics 필드에서 직접 XDM(Experience Data Model) 필드로 매핑될 수 있지만 다른 데이터에는 성공적으로 매핑될 변환 및 특정 함수가 필요합니다.

![Analytics에서 Experience Platform으로의 Adobe Analytics 데이터 여정에 대한 그림입니다.](../images/analytics-data-experience-platform.png)

## 스트리밍 미디어 매개 변수

스트리밍 미디어 매개 변수에 대한 자세한 내용은 다음 표를 참조하십시오.

| 데이터 피드 | XDM 필드 패스 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | 문자열 | 사람이 인식할 수 있는 알기 쉬운 비디오 이름. |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | 문자열 | 미디어 작성자의 이름입니다. |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | 문자열 | 뮤직 레코딩 또는 비디오의 앨범 아티스트나 단체의 이름. |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | 문자열 | 뮤직 레코딩 또는 비디오가 포함된 앨범 이름. |
| `videolength` | `mediaReporting.sessionDetails.length ` | 정수 | 비디오의 길이 또는 런타임입니다. |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | 문자열 |
| `video` | `mediaReporting.sessionDetails.name` | 문자열 | 비디오의 ID입니다. |
| `videoshow` | `mediaReporting.sessionDetails.show` | 문자열 | 프로그램 또는 시리즈 이름. 프로그램/시리즈 이름은 표시가 시리즈의 일부인 경우에만 필요합니다. |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | 문자열 | &quot;비디오&quot; 또는 &quot;오디오&quot; 등 스트리밍 미디어 유형. |
| `videoseason` | `mediaReporting.sessionDetails.season` | 문자열 | 시연이 포함된 시즌 번호입니다. 이 값은 표시가 시리즈의 일부인 경우에만 필요합니다. |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | 문자열 | 에피소드의 번호입니다. |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | 문자열[] | 비디오의 장르입니다. |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | 문자열 | 개별 재생에 고유한 컨텐츠 스트림의 인스턴스에 대한 식별자입니다. |
| `videoplayername` | `mediaReporting.sessionDetails.playerName ` | 문자열 | 비디오 플레이어의 이름입니다. |
| `videochannel` | `mediaReporting.sessionDetails.channel` | 문자열 | 콘텐츠가 재생된 위치의 배포 채널입니다. |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | 문자열 | 콘텐츠에 사용되는 스트림 전달 유형입니다. 모든 비디오 보기에 대해 자동으로 &quot;비디오&quot;로 설정됩니다. 권장 값에는 VOD, Live, Linear, UGC, DVOD, Radio, Podcast, Audiobook 및 Song이 포함됩니다. |
| `videonetwork` | `mediaReporting.sessionDetails.network` | 문자열 | 네트워크 또는 채널 이름입니다. |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | 문자열 | 피드 유형. 실제 피드 관련 데이터(예: &quot;East HD&quot; 또는 &quot;SD&quot;)나 피드 소스(예: URL)를 나타낼 수 있습니다. |
| `videosegment` | `mediaReporting.sessionDetails.segment` | 문자열 |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | 부울 | 비디오가 시작되었는지 여부를 나타내는 부울 값입니다. 이 문제는 사용자가 재생 버튼을 선택하면 발생하며 프리롤 광고, 버퍼링, 오류 등이 있는 경우에도 계산됩니다. |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | 부울 | 미디어의 첫 번째 프레임이 시작되었는지 여부를 나타내는 부울 값입니다. 광고 또는 버퍼링 시간 중에 사용자가 그만두면 &quot;콘텐츠 시작&quot;이 적용되지 않습니다. |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | 정수 | 기본 콘텐츠에서 `type=PLAY`의 모든 이벤트에 대한 기간(초)입니다. |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | 부울 | 시간 미디어 에셋이 완료될 때까지 관찰했는지 보여 주는 부울 값입니다. 이 값은 앞으로 잠재적으로 건너뛸 뷰어를 설명하지 않으므로 이 값은 뷰어가 전체 비디오를 시청했음을 의미하지는 않습니다. |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | 정수 | 광고 시청 시간을 포함하여 특정 시간 미디어 에셋에서 사용자가 사용한 총 시간입니다. |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | 정수 | 시간 미디어 에셋에서 사용자가 본 고유 간격의 합계입니다. 즉, 여러 번 본 재생 구간의 길이는 한 번만 카운트됩니다. |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | 번호 | 특정 미디어 항목에 소요된 평균 콘텐츠 시간입니다. 즉, 전체 콘텐츠 체류 시간을 모든 재생 세션의 길이로 나눈 값입니다. |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | 부울 | 주어진 비디오의 플레이헤드가 총 비디오 길이의 10% 마커를 통과했는지 여부를 나타내는 부울 값입니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | 부울 | 주어진 비디오의 플레이헤드가 총 비디오 길이의 25% 마커를 통과했는지 여부를 나타내는 부울 값입니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | 부울 | 주어진 비디오의 플레이헤드가 총 비디오 길이의 50% 마커를 통과했는지 여부를 나타내는 부울 값입니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | 부울 | 주어진 비디오의 플레이헤드가 총 비디오 길이의 75% 마커를 통과했는지 여부를 나타내는 부울 값입니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | 부울 | 주어진 비디오의 플레이헤드가 총 비디오 길이의 95% 마커를 통과했는지 여부를 나타내는 부울 값입니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | 부울 | 단일 미디어 항목 재생 중에 한 번 이상의 일시 중지가 발생했는지 여부를 나타내는 부울 값입니다. |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | 정수 | 재생 도중 발생한 일시 중단 횟수. |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | 정수 | 사용자가 재생을 일시 중단한 총 기간(초)입니다. |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | 문자열 | Adobe 인증을 통해 제공되는 MVPD 식별자. |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | 문자열 | 사용자가 Adobe 인증을 통해 인증되었음을 정의합니다. |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | 콘텐츠가 브로드캐스트되거나 재생되는 시간을 정의합니다. |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | 부울 | 버퍼, 일시 중지 또는 지연 기간이 30분 이상 지난 후 다시 시작된 각 재생을 표시하는 부울 값. |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | 부울 | 적어도 한 개의 프레임이 조회되었음을 나타내는 부울 값. 이 프레임은 첫 번째 프레임일 필요가 없습니다. |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | 문자열 | 레코드 레이블의 이름입니다. |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | 문자열 | 오디오가 재생되는 라디오 방송국 또는 이름입니다. |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | 문자열 | 오디오 콘텐츠 게시자의 이름입니다. |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | 번호 | 마지막으로 알려진 사용자 상호 작용과 세션 종료 시점 사이에 경과된 시간(초)을 나타냅니다. |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | 문자열 | 자체 내부 표현으로 정의된 로드된 광고 유형. |

{style="table-layout:auto"}

## Advertising 매개 변수

광고 매개 변수에 대한 자세한 내용은 다음 표를 참조하십시오.

| 데이터 피드 | XDM 필드 패스 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | 문자열 | 광고의 이름입니다. 보고에서 &quot;광고 이름&quot;은 분류이고 &quot;광고 이름(변수)&quot;은 eVar입니다. |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | 정수 | 상위 광고 시작 내에 있는 광고의 색인입니다. 예를 들어 첫 번째 광고는 색인 0을 가지고 두 번째 광고는 색인 1을 가집니다. |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | 정수 | 비디오 광고의 길이(초 단위)입니다. |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | 문자열 | 광고를 렌더링하는 데 사용되는 플레이어의 이름입니다. |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | 문자열 | 광고 브레이크 ID입니다. |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | 문자열 | 사람이 인식할 수 있는 친숙한 광고 브레이크 이름입니다. |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | 문자열 | 광고에서 다루고 있는 제품의 회사 또는 브랜드입니다. |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | 문자열 | 광고 캠페인의 ID입니다. |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | 부울 | 광고가 시작되었는지 여부를 나타내는 부울 값. |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | 부울 | 가 완료되었는지 여부를 나타내는 부울 값입니다. |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | 정수 | 광고를 시청하는 데 걸린 총 시간(초)입니다. |

{style="table-layout:auto"}

## 챕터 매개 변수

챕터 매개 변수에 대한 자세한 내용은 다음 표를 참조하십시오.

| 데이터 피드 | XDM 필드 패스 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | 문자열 | 자동으로 생성된 챕터의 ID입니다. |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | 부울 | 챕터가 시작되었는지 여부를 나타내는 부울 값입니다. |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | 부울 | 챕터가 완료되었는지 여부를 나타내는 부울 값입니다. |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | 정수 | 챕터에서 보낸 시간(초 단위)입니다. |

{style="table-layout:auto"}

## 플레이어 상태 매개 변수

플레이어 상태 매개 변수에 대한 자세한 내용은 다음 표를 참조하십시오.

| 데이터 피드 | XDM 필드 패스 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | 부울 | 비디오 상태가 전체 화면으로 설정되었는지 여부를 나타내는 부울 값입니다. |
| `videostatefullscreencount` | `mediaReporting.states[].count` | 정수 | 비디오 상태가 전체 화면으로 설정된 횟수입니다. |
| `videostatefullscreentime` | `mediaReporting.states[].time` | 정수 | 비디오 상태가 전체 화면으로 설정된 총 기간입니다. |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | 부울 | 자막을 사용할지 여부를 나타내는 부울 값입니다. |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | 정수 | 자막이 활성화된 횟수입니다. |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | 정수 | 자막을 활성화한 총 시간. |
| `videostatemute` | `mediaReporting.states[].isSet` | 부울 | 비디오 상태가 음소거로 설정되었는지 여부를 나타내는 부울 값입니다. |
| `videostatemutecount` | `mediaReporting.states[].count` | 정수 | 비디오가 음소거된 횟수입니다. |
| `videostatemutetime` | `mediaReporting.states[].time` | 정수 | 뮤트된 비디오의 총 기간입니다. |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | 부울 | PIP(Picture-in-Picture) 모드의 활성화 여부를 나타내는 부울 값입니다. |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | 정수 | PIP(Picture-in-Picture) 모드가 활성화된 횟수. |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | 정수 | PIP(Picture-in-Picture) 모드가 활성화된 총 기간 |
| `videostateinfocus` | `mediaReporting.states[].isSet` | 부울 | 인포커스 모드가 활성화되었는지 여부를 나타내는 부울 값 |
| `videostateinfocuscount` | `mediaReporting.states[].count` | 정수 | 화면 내 모드가 활성화된 횟수입니다. |
| `videostateinfocustime` | `mediaReporting.states[].time` | 정수 | 인포커스 모드가 활성화된 시간의 총 기간입니다. |

{style="table-layout:auto"}

## 품질 매개 변수

품질 매개변수에 대한 정보는 다음 표를 참조하십시오.

| 데이터 피드 | XDM 필드 패스 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | 번호 | 평균 비트율(kbps, 정수)입니다. 이 지표는 재생 기간과 관련하여 재생 세션 중에 발생한 모든 비트율 값의 가중 평균으로 계산됩니다. |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | 부울 | 비트율 변경이 발생한 스트림 수를 나타내는 부울 값. 이 지표는 재생 세션 중에 하나 이상의 비트율 변경 이벤트가 발생한 경우에만 true로 설정됩니다. |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | 정수 |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | 문자열 | 비트율 변경 횟수입니다. 이 값은 재생 세션 중에 발생한 모든 비트율 변경 이벤트의 합계로 계산됩니다. |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | 정수 | 비디오 로드와 비디오 시작 사이에 경과된 기간(초 단위)입니다. |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | 부울 | 프레임이 드롭된 스트림 수를 나타내는 부울 값입니다. 이 지표는 재생 세션 중에 하나 이상의 프레임이 드롭된 경우에만 true로 설정됩니다. |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | 정수 | 메인 콘텐츠 재생 도중 드롭된 프레임 횟수. |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | 정수 | 버퍼 이벤트 수입니다. 이 지표는 재생 세션 중에 발생한 다른 버퍼 상태의 수로 계산됩니다. 플레이어가 재생 또는 일시 중지와 같은 다른 상태에서 버퍼 상태에 들어가는 횟수입니다. |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | 정수 | 버퍼링에 걸린 총 시간(초)입니다. 이 값은 재생 세션 중에 발생한 모든 버퍼 이벤트 기간의 합계로 계산됩니다. |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | 부울 | 버퍼링의 영향을 받은 스트림 수를 나타내는 부울 값. 이 지표는 재생 세션 중에 하나 이상의 버퍼 이벤트가 발생한 경우에만 true로 설정됩니다. |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | 부울 | 오류 이벤트가 발생한 스트림 수를 나타내는 부울 값입니다. 예를 들어 재생 세션 중에 trackError 가 호출되고 type=error 하트비트 호출이 생성된 경우, 이 지표는 재생 중에 하나 이상의 오류가 발생한 경우에만 true로 설정됩니다. |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | 정수 | 발생한 오류 횟수입니다. 이 값은 재생 세션 중에 발생한 모든 오류 이벤트의 합계로 계산됩니다. |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | 문자열 배열 | 플레이어 SDK에서 생성한 고유 오류 ID입니다. 제공된 오류 API를 통해 구현 시 오류 코드 또는 ID를 제공해야 합니다. |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | 문자열 배열 | CDN 오류와 같은 외부 소스의 고유 오류 ID. 제공된 오류 API를 통해 구현 시 오류 코드 또는 ID를 제공해야 합니다. |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | 부울 | 재생 중에 Media SDK에서 생성한 고유 오류 ID. |

{style="table-layout:auto"}

## 사용되지 않는 필드

더 이상 사용되지 않는 Analytics 매핑 필드에 대한 정보는 이 섹션을 참조하십시오.

### 직접 매핑 필드

+++사용되지 않는 직접 매핑 필드의 테이블을 보려면 선택

| 데이터 피드 | XDM 필드 | XDM 유형 | 설명 |
| --- | --- | --- | --- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 문자열 | 사용자 지정 Analytics eVar. 각 조직은 eVar를 다르게 사용할 수 있습니다. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 문자열 | 사용자 지정 Analytics prop. 각 조직은 prop을 다르게 사용할 수 있습니다. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | 정수 | 브라우저의 번호 ID입니다. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | 정수 | 브라우저의 픽셀 단위 높이입니다. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | 정수 | 브라우저의 픽셀 단위 폭입니다. |
| `m_campaign` | `marketing.trackingCode` | 문자열 | 추적 코드 차원에 사용되는 변수입니다. |
| `m_channel` | `web.webPageDetails.siteSection` | 문자열 | 사이트 섹션 차원에 사용되는 변수입니다. |
| `m_domain` | `environment.domain` | 문자열 | 도메인 차원에 사용되는 변수입니다. 사용자의 인터넷 서비스 공급자(ISP)를 기반으로 합니다. |
| `m_geo_city` | `placeContext.geo.city` | 문자열 | 히트의 도시 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_geo_dma` | `placeContext.geo.dmaID` | 정수 | 히트에 대한 인구 통계학적 영역의 숫자 ID입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_geo_region` | `placeContext.geo.stateProvince` | 문자열 | 히트의 주 또는 지역 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_geo_zip` | `placeContext.geo.postalCode` | 문자열 | 히트의 우편 번호입니다. 히트의 IP 주소를 기반으로 합니다. |
| `m_keywords` | `search.keywords` | 문자열 | 키워드 차원에 사용되는 변수입니다. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 정수 | 방문자의 운영 체제를 나타내는 숫자 ID입니다. 이는 user_agent 열을 기반으로 합니다. |
| `m_page_url` | `web.webPageDetails.URL` | 문자열 | 페이지 조회수의 URL입니다. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | 문자열 | 페이지 이름이 있는 히트에서 1과 같습니다. 이 기능은 Adobe Analytics 페이지 보기 수 지표와 유사합니다. |
| `m_referrer` | `web.webReferrer.URL` | 문자열 | 이전 페이지의 페이지 URL. |
| `m_search_page_num` | `search.pageDepth` | 정수 | 모든 검색 페이지 등급 차원에 사용됩니다. 사용자가 사이트를 클릭스루하기 전에 사이트가 표시된 검색 결과 페이지를 나타냅니다. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 문자열 | 상태 변수입니다. |
| `m_user_server` | `web.webPageDetails.server` | 문자열 | 서버 차원에 사용되는 변수입니다. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 문자열 | 우편번호 차원을 채우는 데 사용되는 변수입니다. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | 문자열 | Accept-Language HTTP 헤더에 표시된 대로 모든 수락된 언어를 나열합니다. |
| `homepage` | `web.webPageDetails.isHomePage` | 부울 | 더 이상 사용되지 않습니다. 현재 URL이 브라우저의 홈 페이지인 경우 표시됩니다. |
| `ipv6` | `environment.ipV6` | 문자열 |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | 문자열 | 브라우저가 지원하는 JavaScript 버전. |
| `user_agent` | `environment.browserDetails.userAgent` | 문자열 | HTTP 헤더에서 전송된 사용자 에이전트 문자열입니다. |
| `mobileappid` | `application.name` | 문자열 | `[AppName][BundleVersion]` 형식으로 저장된 모바일 앱 ID입니다. |
| `mobiledevice` | `device.model` | 문자열 | 모바일 장치의 이름입니다. iOS에서는 쉼표로 구분된 2자리 문자열로 저장됩니다. 첫 번째 숫자는 디바이스 생성을 나타내고 두 번째 숫자는 디바이스 제품군을 나타냅니다. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | 문자열 | 모바일 서비스에서 사용됩니다. 관심 영역을 나타냅니다. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | 번호 | 모바일 서비스에서 사용됩니다. 관심 영역 거리를 나타냅니다. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | 번호 | 컨텍스트 데이터 변수 a.loc.acc에서 수집됩니다. 수집 시 GPS의 정확도를 미터 단위로 나타냅니다. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | 문자열 | 컨텍스트 데이터 변수 a.loc.category에서 수집됩니다. 특정 위치의 범주를 설명합니다. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | 문자열 | 컨텍스트 데이터 변수 a.loc.id에서 수집됩니다. 특정 관심 영역에 대한 식별자. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | 문자열 | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | 번호 | Mobile Services 비콘 Major. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | 번호 | Mobile Services 비콘 Minor. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | 문자열 | Mobile Services 비콘 UUID |
| `mobileinstalls` | `application.firstLaunches` | 오브젝트 | 설치 또는 재설치 후 처음 실행할 때 트리거됩니다. | {id (문자열), 값 (숫자)} |
| `mobileupgrades` | `application.upgrades` | 오브젝트 | 앱 업그레이드 수를 보고합니다. 업그레이드 후 또는 버전 번호가 변경될 때 처음 실행할 때 트리거됩니다. | {id (문자열), 값 (숫자)} |
| `mobilelaunches` | `application.launches` | 오브젝트 | 앱을 시작한 횟수입니다. | {id (문자열), 값 (숫자)} |
| `mobilecrashes` | `application.crashes` | 오브젝트 |  | {id (문자열), 값 (숫자)} |
| `mobilemessageclicks` | `directMarketing.clicks` | 오브젝트 |  | {id (문자열), 값 (숫자)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | 오브젝트 | | {id (문자열), 값 (숫자)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | 오브젝트 | | {id (문자열), 값 (숫자)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | 오브젝트 | 비디오 품질 시작 시간입니다. | {id (문자열), 값 (숫자)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | 오브젝트 | | {id (문자열), 값 (숫자)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | 오브젝트 | 비디오 품질 버퍼 카운트 | {id (문자열), 값 (숫자)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | 오브젝트 | 비디오 품질 버퍼 시간 | {id (문자열), 값 (숫자)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | 오브젝트 | 비디오 품질 변경 카운트 | {id (문자열), 값 (숫자)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | 오브젝트 | 비디오 품질 평균 비트 전송률 | {id (문자열), 값 (숫자)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | 오브젝트 | 비디오 품질 오류 카운트 | {id (문자열), 값 (숫자)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | 오브젝트 | | {id (문자열), 값 (숫자)} |

{style="table-layout:auto"}

+++

## 생성된 매핑 필드

ADC에서 제공되는 선택 필드는 변환해야 하며 XDM에서 Adobe Analytics의 직접 복사본 이상의 로직이 생성되어야 합니다.

+++더 이상 사용되지 않는 생성된 매핑 필드의 테이블을 보려면 선택

| 데이터 피드 | XDM 필드 | XDM 유형 | 설명 |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 오브젝트 | 목록 prop으로 구성된 사용자 지정 Analytics prop. 여기에는 구분된 값 목록이 포함되어 있습니다. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 오브젝트 | 계층 변수에서 사용됩니다. 여기에는 구분된 값 목록이 포함되어 있습니다. | {values (배열), 구분 기호 (문자열)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 배열 | 사용자 지정 분석 목록 변수입니다. 구분된 값 목록을 포함합니다. | {value (문자열), key (문자열)} |
| `m_color` | `device.colorDepth` | 정수 | c_color 열의 값을 기반으로 하는 색상 심도 ID입니다. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | 부울 | 쿠키 지원 차원에 사용되는 변수입니다. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | 오브젝트 | 히트에서 트리거된 표준 상거래 이벤트. | {id (문자열), 값 (숫자)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 오브젝트 | 히트에서 트리거된 사용자 지정 이벤트입니다. | {id (오브젝트), value (오브젝트)} |
| `m_geo_country` | `placeContext.geo.countryCode` | 문자열 | IP를 기반으로 하는, 히트가 발생한 국가의 약어입니다. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | 번호 | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | 번호 | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | 부울 | Java™이 활성화되어 있는지 여부를 나타내는 플래그입니다. |
| `m_latitude` | `placeContext.geo._schema.latitude` | 번호 | |
| `m_longitude` | `placeContext.geo._schema.longitude` | 번호 | |
| `m_page_event_var1` | `web.webInteraction.URL` | 문자열 | 링크 추적 이미지 요청에만 사용되는 변수입니다. 이 변수에는 클릭한 다운로드 링크, 종료 링크 또는 사용자 지정 링크의 URL이 포함됩니다. |
| `m_page_event_var2` | `web.webInteraction.name` | 문자열 | 링크 추적 이미지 요청에만 사용되는 변수입니다. 지정된 경우 링크의 사용자 지정 이름이 나열됩니다. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | 부울 | 페이지를 찾을 수 없음 차원을 채우는 데 사용되는 변수입니다. 이 변수는 비어 있거나 &quot;ErrorPage&quot;를 포함해야 합니다. |
| `m_pagename_no_url` | `web.webPageDetails.name` | 번호 | 페이지 이름(설정된 경우)입니다. 지정된 페이지가 없으면 이 값은 비워 둡니다. |
| `m_paid_search` | `search.isPaid` | 부울 | 히트가 유료 검색 감지와 일치하는 경우 설정되는 플래그입니다. |
| `m_product_list` | `productListItems[].items` | 배열 | products 변수를 통해 전달되는 제품 목록입니다. | {SKU(문자열), 수량(정수), priceTotal(숫자)} |
| `m_ref_type` | `web.webReferrer.type` | 문자열 | 히트에 대한 참조 유형을 나타내는 숫자 ID입니다.<br/>`1`: 사이트 내부<br/>`2`: 기타 웹 사이트<br/>`3`: 검색 엔진<br/>`4`: 하드 드라이브<br/>`5`: USENET<br/>`6`: 입력/책갈피 표시(레퍼러 없음)<br/>`7`: 전자 메일<br/>`8`: JavaScript 없음<br/>`9`: 소셜 네트워크 |
| `m_search_engine` | `search.searchEngine` | 문자열 | 방문자를 사이트로 유도한 검색 엔진을 나타내는 숫자 ID입니다. |
| `post_currency` | `commerce.order.currencyCode` | 문자열 | 거래 중에 사용된 통화 코드. |
| `post_cust_hit_time_gmt` | `timestamp` | 문자열 | 타임스탬프가 활성화된 데이터 세트에서만 사용됩니다. UNIX® 시간을 기준으로 히트와 함께 전송된 타임스탬프입니다. |
| `post_cust_visid` | `identityMap` | 오브젝트 | 고객 방문자 ID입니다. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | 부울 | 고객 방문자 ID입니다. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | 문자열 | 고객 방문자 ID입니다. |
| `post_visid_high` + `visid_low` | `identityMap` | 오브젝트 | 방문에 대한 고유 식별자. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | 문자열 | 방문에 대한 고유 식별자. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | 부울 | 방문을 고유하게 식별하기 위해 `visid_low`과(와) 함께 사용됩니다. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | 문자열 | 방문을 고유하게 식별하기 위해 `visid_low`과(와) 함께 사용됩니다. |
| `post_visid_low` | `identityMap` | 오브젝트 | 방문을 고유하게 식별하기 위해 visid_high와 함께 사용됩니다. |
| `hit_time_gmt` | `receivedTimestamp` | 문자열 | UNIX® 시간을 기반으로 한 히트의 타임스탬프입니다. |
| `hitid_high` + `hitid_low` | `_id` | 문자열 | 히트를 식별하는 고유 식별자입니다. |
| `hitid_low` | `_id` | 문자열 | 히트를 고유하게 식별하기 위해 hitid_high와 함께 사용됩니다. |
| `ip` | `environment.ipV4` | 문자열 | 이미지 요청의 HTTP 헤더를 기반으로 한 IP 주소입니다. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | 부울 | 사용된 JavaScript 버전. |
| `mcvisid_high` + `mcvisid_low` | identityMap | 오브젝트 | Experience Cloud 방문자 ID입니다. |
| `mcvisid_high` + `mcvisid_low` | endUserID_experience.mcid.id | 문자열 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | 부울 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | 문자열 | ECID(Experience Cloud ID)는 MCID라고도 하며 경우에 따라 네임스페이스에서 사용됩니다. |
| `mcvisid_low` | `identityMap` | 오브젝트 | Experience Cloud 방문자 ID입니다. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | 문자열 | 히트 결합 ID. Analytics 필드 sdid_high 및 sdid_low 는 두 개(또는 그 이상) 수신 히트를 함께 연결하는 데 사용되는 보조 데이터 ID입니다. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | 문자열 | Mobile Services 비콘 Proximity. |

{style="table-layout:auto"}

+++

## 필드 분할 매핑

이러한 필드에는 단일 소스가 있지만 **다중** XDM 위치에 매핑됩니다.

+++사용되지 않는 분할 매핑 필드의 테이블을 보려면 선택

| 데이터 피드 | XDM 필드 | XDM 유형 | 설명 |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | 정수 | 모니터의 해상도를 나타내는 숫자 ID입니다. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | 문자열 | 모바일 운영 체제 버전. |

{style="table-layout:auto"}

+++

## 고급 매핑 필드

선택 필드(&quot;게시물 값&quot;이라고 함)에는 Adobe이 처리 규칙, VISTA 규칙 및 조회 테이블을 사용하여 값을 조정한 후의 데이터가 포함됩니다. 대부분의 게시물 값에는 사전 처리된 대응 항목이 있습니다.

Analytics 소스 커넥터는 사전 처리된 데이터를 Experience Platform의 데이터 세트로 전송합니다. 변환을 사용하여 이 데이터를 후처리된 해당 데이터로 변환할 수 있습니다. 쿼리 서비스를 사용하여 이러한 변환을 수행하는 방법에 대한 자세한 내용은 쿼리 서비스 사용 안내서의 [Adobe 정의 함수](/help/query-service/sql/adobe-defined-functions.md)를 참조하십시오.

쿼리 서비스를 사용하여 이러한 변환을 수행하는 방법에 대한 자세한 내용은 쿼리 서비스 사용 안내서의 [Adobe 정의 함수](/help/query-service/sql/adobe-defined-functions.md)를 참조하십시오.

+++사용되지 않는 고급 매핑 필드의 테이블을 보려면 선택

| 데이터 피드 | XDM 필드 | XDM 유형 | 설명 |
| — | — | — | — ||
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 문자열 | 사용자 지정 Analytics eVar. 각 조직은 eVar를 다르게 사용할 수 있습니다. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 문자열 | 사용자 지정 Analytics prop. 각 조직은 prop을 다르게 사용할 수 있습니다. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | 정수 | 브라우저의 픽셀 단위 높이입니다. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | 정수 | 브라우저의 픽셀 단위 폭입니다. |
| `post_campaign` | `marketing.trackingCode` | 문자열 | 추적 코드 차원에 사용되는 변수입니다. |
| `post_channel` | `web.webPageDetails.siteSection` | 문자열 | 사이트 섹션 차원에 사용되는 변수입니다. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | 문자열 | 설정된 경우 사용자 지정 방문자 ID입니다. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | 문자열 | 방문자가 도달하는 첫 번째 페이지의 URL입니다. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | 문자열 | 원래 시작 페이지 차원에 사용되는 변수입니다. 방문자의 시작 페이지에 대한 페이지 이름입니다. |
| `post_keywords` | `search.keywords` | 문자열 | 히트에 대해 수집된 키워드입니다. |
| `post_page_url` | `web.webPageDetails.URL` | 문자열 | 페이지 조회수의 URL입니다. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | 문자열 | 페이지 이름이 있는 히트에서 1과 같습니다. 이 기능은 Adobe Analytics 페이지 보기 수 지표와 유사합니다. |
| `post_purchaseid` | `commerce.order.purchaseID` | 문자열 | 구매를 고유하게 식별하는 데 사용되는 변수입니다. |
| `post_referrer` | `web.webReferrer.URL` | 문자열 | 이전 페이지의 URL. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 문자열 |  상태 변수입니다. |
| `post_user_server` | `web.webPageDetails.server` | 문자열 | 서버 차원에 사용되는 변수입니다. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 문자열 | 우편번호 차원을 채우는 데 사용되는 변수입니다. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | 정수 | 브라우저의 숫자 ID입니다. |
| `domain` | `environment.domain` | 문자열 | 도메인 차원에 사용되는 변수입니다. 사용자의 인터넷 서비스 공급자(ISP)를 기반으로 합니다. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | 문자열 | 방문자에 대한 첫 번째 참조 URL입니다. |
| `geo_city` | `placeContext.geo.city` | 문자열 | 히트의 도시 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `geo_dma` | `placeContext.geo.dmaID` | 정수 | 히트에 대한 인구 통계학적 영역의 숫자 ID입니다. 히트의 IP 주소를 기반으로 합니다. |
| `geo_region` | `placeContext.geo.stateProvince` | 문자열 | 히트의 주 또는 지역 이름입니다. 히트의 IP 주소를 기반으로 합니다. |
| `geo_zip` | `placeContext.geo.postalCode` | 문자열 | 히트의 우편 번호입니다. 히트의 IP 주소를 기반으로 합니다. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 정수 | 방문자의 운영 체제를 나타내는 숫자 ID입니다. 이는 user_agent 열을 기반으로 합니다. |
| `search_page_num` | `search.pageDepth` | 정수 | 이 변수는 모든 검색 페이지 등급 차원에 사용되며 사이트의 검색 결과 중 어느 페이지가 검색되는지 나타냅니다 | 사용자가 사이트를 클릭스루하기 전에 표시되었습니다. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | 문자열 | 검색 키워드 차원에 사용되는 변수입니다. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | 정수 | 방문 횟수 차원에 사용되는 변수입니다. 1에서 시작하며 새 방문이 시작될 때마다 (사용자당) 증가합니다. |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | 정수 | 히트 깊이 차원에 사용되는 변수입니다. 이 값은 사용자가 생성할 각 히트에 대해 1씩 증가하며 각 방문 후에 재설정됩니다. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | 문자열 | 방문의 첫 번째 레퍼러입니다. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | 정수 | 방문의 첫 번째 페이지 이름입니다. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 오브젝트 | 목록 prop으로 구성된 사용자 지정 Analytics prop. 여기에는 구분된 값 목록이 포함되어 있습니다. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 오브젝트 | 계층 변수에서 사용되며 구분된 값 목록을 포함합니다. | {values (배열), 구분 기호 (문자열)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 배열 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. | {value (문자열), key (문자열)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | 부울 | 쿠키 지원 차원에 사용되는 변수입니다. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | 오브젝트 | 히트에서 트리거된 표준 상거래 이벤트. | {id (문자열), 값 (숫자)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 오브젝트 | 히트에서 트리거된 사용자 지정 이벤트입니다.| {id (오브젝트), value (오브젝트)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | 부울 | Java™이 활성화되어 있는지 여부를 나타내는 플래그입니다. |
| `post_latitude` | `placeContext.geo._schema.latitude` | 숫자 |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | 숫자 |   |
| `post_page_event` | `web.webInteraction.type` | 문자열 | 이미지 요청(표준 히트, 다운로드 링크, 종료 링크 또는 클릭한 사용자 지정 링크)에서 전송된 히트 유형입니다. |
| `post_page_event` | `web.webInteraction.linkClicks.value` | 숫자 | 히트가 링크 클릭인 경우 1입니다. 이는 Adobe Analytics의 페이지 이벤트 지표와 유사합니다. |
| `post_page_event_var1` | `web.webInteraction.URL` | 문자열 | 이 변수는 링크 추적 이미지 요청에만 사용됩니다. 클릭한 다운로드 링크, 종료 링크 또는 사용자 지정 링크의 URL입니다. |
| `post_page_event_var2` | `web.webInteraction.name` | 문자열 | 이 변수는 링크 추적 이미지 요청에만 사용됩니다. 링크의 사용자 지정 이름입니다. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | 부울 | 페이지를 찾을 수 없음 차원을 채우는 데 사용됩니다. 이 변수는 비어 있거나 &quot;ErrorPage&quot;를 포함해야 합니다. |
| `post_pagename_no_url` | `web.webPageDetails.name` | 숫자 | 페이지 이름(설정된 경우)입니다. 지정된 페이지가 없으면 이 값은 비워 둡니다. |
| `post_product_list` | `productListItems[].items` | 배열 | products 변수를 통해 전달되는 제품 목록입니다. | {SKU(문자열), 수량(정수), priceTotal(숫자)} |
| `post_search_engine` | `search.searchEngine` | 문자열 | 방문자를 사이트로 유도한 검색 엔진을 나타내는 숫자 ID입니다. |
| `mvvar1_instances` | `.list.items[]` | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| `mvvar2_instances` | `.list.items[]` | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| `mvvar3_instances` | `.list.items[]` | 오브젝트 | 변수 값 목록입니다. 구현에 따라 구분된 사용자 지정 값 목록을 포함합니다. |
| `color` | `device.colorDepth` | 정수 | c_color 열의 값을 기반으로 하는 색상 심도 ID입니다. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | 문자열 | 방문자의 첫 번째 레퍼러 유형을 나타내는 숫자 ID입니다. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | 정수 | UNIX® 시간에서 방문자의 첫 번째 히트 타임스탬프입니다. |
| `geo_country` | `placeContext.geo.countryCode` | 문자열 | IP를 기반으로 한, 히트가 발생한 국가의 약어입니다. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | 숫자 |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | 숫자 |  |
| `paid_search` | `search.isPaid` | 부울 | 히트가 유료 검색 감지와 일치하는 경우 설정되는 플래그입니다. |
| `ref_type` | `web.webReferrer.type` | 문자열 | 히트에 대한 참조 유형을 나타내는 숫자 ID입니다. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | 부울 | 방문의 첫 번째 히트가 유료 검색 히트에서 왔는지를 나타내는 플래그(1=유료, 0=유료 아님)입니다. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | 문자열 | 방문의 첫 번째 레퍼러 유형을 나타내는 숫자 ID. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | 문자열 | 방문의 첫 번째 검색 엔진에 대한 숫자 ID입니다. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | 정수 | UNIX® 시간 내 방문의 첫 번째 히트 타임스탬프. |

+++