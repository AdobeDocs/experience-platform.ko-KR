---
title: 세션 세부 정보 보고 데이터 유형
description: 세션 세부 정보 보고 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 8bcaa0d8-2f85-4189-b0b5-8c72ecbb0660
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 13%

---

# [!UICONTROL 세션 세부 정보] 보고 데이터 형식

[!UICONTROL 세션 세부 정보] 보고는 미디어 재생 세션과 관련된 데이터를 추적하는 표준 XDM(Experience Data Model) 데이터 형식입니다.
미디어 보고 필드는 Adobe 서비스에서 사용자가 보낸 미디어 컬렉션 필드를 분석하는 데 사용됩니다. 이 데이터는 다른 특정 사용자 지표와 함께 계산되고 보고됩니다. 스키마는 사용자 비헤이비어 및 콘텐츠 소비 패턴에 대한 통찰력을 제공하는 광범위한 속성을 포함합니다. [!UICONTROL 세션 세부 정보] 보고 데이터 형식을 사용하여 재생 이벤트, 광고 상호 작용, 진행률 마커, 일시 중지 및 기타 지표를 로깅하여 사용자 참여를 캡처합니다.

+++세션 세부 정보 보고 데이터 유형의 다이어그램을 표시하려면 선택합니다.
![세션 세부 정보 보고 데이터 형식의 다이어그램입니다.](../images/data-types/session-details-reporting.png)
+++

>[!NOTE]
>
>각 디스플레이 이름에는 해당 오디오 및 비디오 매개 변수에 대한 추가 정보를 볼 수 있는 링크가 포함되어 있습니다. 연결된 페이지에는 Adobe, 구현 값, 네트워크 매개 변수, 보고 및 중요 고려 사항으로 수집된 비디오 및 데이터에 대한 세부 사항이 포함되어 있습니다.

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|--------------------------------------------------------------------------------------------------|
| [[!UICONTROL 10% 진행률 마커]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#ten-%25-progress-marker) | `hasProgress10` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 10%를 통과했음을 나타냅니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [[!UICONTROL 25% 진행률 마커]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#twenty-five-%25-progress-marker) | `hasProgress25` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 25%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [[!UICONTROL 50% 진행률 마커]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#50%25-progress-marker) | `hasProgress50` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 50%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [[!UICONTROL 75% 진행률 마커]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#seventy-five-%25-progress-marker) | `hasProgress75` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 75%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [[!UICONTROL 95% 진행률 마커]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#ninety-five-%25-progress-marker) | `hasProgress95` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 95%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [[!UICONTROL 광고 수]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#ad-count) | `adCount` | 정수 | 재생 도중 시작된 광고 횟수. |
| [!UICONTROL 광고 로드 유형] | `adLoad` | 문자열 | 고객별 내부 표현으로 정의되는 로드된 광고 유형. |
| [[!UICONTROL 앨범]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#album) | `album` | 문자열 | 뮤직 레코딩 또는 비디오가 포함된 앨범 이름. |
| [[!UICONTROL 아티스트]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#artist) | `artist` | 문자열 | 뮤직 레코딩 또는 비디오의 앨범 아티스트나 단체의 이름. |
| [[!UICONTROL 자산 ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#asset-id) | `assetID` | 문자열 | [!UICONTROL 자산 ID]은(는) TV 시리즈 에피소드 식별자, 동영상 자산 식별자 또는 라이브 이벤트 식별자와 같은 미디어 자산 콘텐츠에 대한 고유 식별자입니다. 일반적으로 이러한 ID는 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 권한에서 파생됩니다. 이러한 식별자는 다른 소유권 또는 사내 시스템에서도 사용할 수 있습니다. |
| [[!UICONTROL 작성자]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#author) | `author` | 문자열 | 미디어 작성자의 이름입니다. |
| [[!UICONTROL 대상 평균 시간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#average-minute-audience) | `averageMinuteAudience` | 숫자 특정 미디어 항목에 사용된 평균 콘텐츠 시간(즉, 총 콘텐츠 시간을 모든 재생 세션의 길이로 나눈 시간)을 설명합니다. |
| [[!UICONTROL 브로드캐스트 콘텐츠 형식]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-type) | `contentType` | 문자열 | 스트림 배달의 [!UICONTROL 브로드캐스트 콘텐츠 형식]. [!UICONTROL 스트림 유형]당 사용 가능한 값은 다음과 같습니다.<br>오디오: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; 및 &quot;radio&quot;;<br>비디오: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; 및 &quot;DVoD&quot;.<br>고객은 이 매개 변수에 대한 사용자 지정 값을 제공할 수 있습니다. |
| [[!UICONTROL 브로드캐스트 네트워크]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#network) | `network` | 문자열 | 네트워크/채널 이름. |
| [[!UICONTROL 챕터 수]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#chapter-count) | `chapterCount` | 정수 | 재생 도중 시작된 챕터 횟수. |
| [[!UICONTROL 콘텐츠 채널]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-channel) | `channel` | 문자열 | [!UICONTROL 콘텐츠 채널]은(는) 콘텐츠가 재생된 배포 채널입니다. |
| [[!UICONTROL 컨텐츠 완료]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-complete) | `isCompleted` | 부울 | [!UICONTROL 콘텐츠 완료]은(는) 시간 미디어 에셋이 완료될 때까지 관찰되었는지 여부를 나타냅니다. 이 이벤트가 뷰어가 전체 비디오를 시청했음을 의미하지는 않습니다. 뷰어는 앞으로 건너뛸 수도 있습니다. |
| [!UICONTROL 콘텐츠 배달 네트워크] | `cdn` | 문자열 | 재생된 콘텐츠의 [!UICONTROL 콘텐츠 배달 네트워크]. |
| [[!UICONTROL 콘텐츠 ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-id) | `name` | 문자열 | [!UICONTROL 콘텐츠 ID]은(는) 콘텐츠의 고유 식별자입니다. 다른 업계 또는 CMS ID에 다시 연결하는 데 사용할 수 있습니다. |
| [[!UICONTROL 콘텐츠 이름]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-name-(variable)) | `friendlyName` | 문자열 | [!UICONTROL 콘텐츠 이름]은(는) 콘텐츠의 &quot;친숙한&quot;(사람이 읽을 수 있음) 이름입니다. |
| [[!UICONTROL 콘텐츠 플레이어 이름]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-player-name) | `playerName` | 문자열 | 콘텐츠 플레이어의 이름입니다. |
| [[!UICONTROL 콘텐츠 시작]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-starts) | `isPlayed` | 부울 | 미디어의 첫 번째 프레임이 사용되면 [!UICONTROL 콘텐츠 시작]이(가) true가 됩니다. 광고, 버퍼링 중에 사용자가 그만두면 [!UICONTROL 콘텐츠 시작] 이벤트가 일어나지 않습니다. |
| [[!UICONTROL 콘텐츠 체류 시간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-time-spent) | `timePlayed` | 정수 | [!UICONTROL 콘텐츠 체류 시간]은(는) 기본 콘텐츠에서 재생 유형의 모든 이벤트에 대한 이벤트 기간(초)을 합합니다. |
| [[!UICONTROL 작성자 이름]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#originator) | `originator` | 문자열 | 콘텐츠 작성자의 이름입니다. |
| [[!UICONTROL 일 파트]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#day-part) | `dayPart` | 문자열 | 콘텐츠가 브로드캐스트 또는 재생되는 시간을 정의하는 속성입니다. 이는 고객이 필요에 따라 값을 설정할 수 있습니다 |
| [[!UICONTROL 에피소드 번호]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#episode) | `episode` | 문자열 | 에피소드의 번호입니다. |
| [[!UICONTROL 예상 스트림]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#estimated-streams) | `estimatedStreams` | 숫자 | 각 개별 콘텐츠에 대한 예상 비디오 또는 오디오 스트림 수입니다. |
| [[!UICONTROL 페더레이션 데이터]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#federated-data) | `isFederated` | 부울 | 히트가 페더레이션되면( 고객이 자체 구현이 아니라 페더레이션된 데이터 공유의 일부로 수신함) [!UICONTROL 페더레이션 데이터]가 true로 설정됩니다. |
| [[!UICONTROL 피드 유형]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#media-feed-type) | `feed` | 문자열 | EAST HD 또는 SD와 같은 실제 피드 관련 데이터나 URL과 같은 피드 소스를 나타낼 수 있는 피드 유형입니다. |
| [[!UICONTROL 첫 방송 날짜]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#first-air-date) | `firstAirDate` | 문자열 | 컨텐츠가 TV에 처음 방송된 날짜. 모든 날짜 형식이 허용되지만, Adobe은 YYYY-MM-DD 형식을 권장합니다. |
| [[!UICONTROL 첫 번째 디지털 날짜]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#first-digital-date) | `firstDigitalDate` | 문자열 | 콘텐츠가 디지털 채널 또는 플랫폼에서 처음으로 방송된 날짜. 모든 날짜 형식이 허용되지만, Adobe은 YYYY-MM-DD 형식을 권장합니다. |
| [[!UICONTROL 장르]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#genre) | `genre` | 문자열 | 콘텐츠 생성자가 정의한 콘텐츠 유형 또는 그룹입니다. 값은 변수 구현에서 쉼표로 구분해야 합니다. |
| [[!UICONTROL 승인된 미디어]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#authorized) | `authorized` | 문자열 | Adobe 인증을 통해 사용자에게 권한이 부여되었는지 확인합니다. |
| [[!UICONTROL 미디어 콘텐츠 길이]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-length-(variable)) | `length` | 정수 | 예 | [!UICONTROL 미디어 콘텐츠 길이]에 클립 길이/런타임이 포함되어 있습니다. 이는 사용되는 콘텐츠의 최대 길이(또는 기간)입니다(초). |
| [[!UICONTROL 미디어 다운로드 플래그]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#media-downloaded-flag) | `isDownloaded` | 부울 | 다운로드되면 스트림은 디바이스에서 로컬로 재생됩니다. |
| [[!UICONTROL 미디어 세그먼트 보기 수]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-segment-views) | `hasSegmentView` | 부울 | [!UICONTROL 미디어 세그먼트 보기 수]는 첫 번째 프레임이 아니라 최소 하나 이상 본 시기를 나타냅니다. |
| [[!UICONTROL 미디어 세션 ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#media-session-id) | `ID` | 문자열 | [!UICONTROL 미디어 세션 ID]은(는) 개별 재생에 고유한 콘텐츠 스트림의 인스턴스를 식별합니다.<br><em>참고:<em>`sessionId`은(는) `sessionStart`과(와) 다운로드한 모든 이벤트를 제외한 모든 이벤트에 전송됩니다. |
| [[!UICONTROL 미디어 세션 서버 시간 초과]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#seconds-since-last-call) | `secondsSinceLastCall` | 숫자 [!UICONTROL 미디어 세션 서버 시간 제한]은(는) 마지막으로 알려진 사용자의 상호 작용과 세션이 닫힌 시간 사이에 경과된 시간(초)을 나타냅니다. |
| [[!UICONTROL 미디어 시작]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#media-starts) | `isViewed` | 부울 | 미디어에 대한 로드 이벤트입니다. 이는 뷰어가 재생 버튼을 선택할 때 발생합니다. 이 이벤트는 프리롤 광고, 버퍼링, 오류 등이 있는 경우에도 계산됩니다. |
| [[!UICONTROL 미디어 체류 시간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#media-time-spent) | `totalTimePlayed` | 정수 | 광고 시청 시간을 포함해 특정 시간 미디어 에셋에서 사용자가 사용한 총 시간을 설명합니다. |
| [[!UICONTROL MVPD 식별자]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#mvpd) | `mvpd` | 문자열 | Adobe 인증을 통해 제공된 [!UICONTROL MVPD 식별자]. |
| [[!UICONTROL 이벤트 일시 중지]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#pause-events) | `pauseCount` | 정수 | [!UICONTROL 일시 중지 이벤트]는 재생 중에 발생한 일시 중지 기간 수를 계산합니다. |
| [[!UICONTROL 영향을 받는 스트림 일시 중지]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#paused-impacted-streams) | `hasPauseImpactedStreams` | 부울 단일 미디어 항목 재생 중에 한 번 이상의 일시 정지가 발생했는지 여부를 나타냅니다. |
| [!UICONTROL Pcccr] | `pccr` | 부울 | [!UICONTROL Pcccr]은(는) 리디렉션이 발생했음을 나타냅니다. |
| [!UICONTROL Pev3] | `pev3` | 문자열 | [!UICONTROL Pev3]은(는) 보고에 사용되는 미디어 스트림 유형입니다. |
| [[!UICONTROL 게시자]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#publisher) | `publisher` | 문자열 | 오디오 콘텐츠 게시자의 이름입니다. |
| [[!UICONTROL 라디오 방송국]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#station) | `station` | 문자열 | 오디오가 재생되는 라디오 방송국 이름. |
| [[!UICONTROL 등급 값]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-rating) | `rating` | 문자열 | TV 유해 콘텐츠 가이드라인으로 정의된 등급. |
| [[!UICONTROL 레코드 레이블]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#label) | `label` | 문자열 | 레코드 레이블의 이름입니다. |
| [[!UICONTROL 다시 시작]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-resumes) | `hasResume` | 부울 | 버퍼, 일시 중단 또는 중단이 30분 이상 경과하고 다시 시작된 각 재생을 표시합니다. |
| [[!UICONTROL 시즌 번호]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#season) | `season` | 문자열 | 표시가 속한 [!UICONTROL 시즌 번호]입니다. 시즌 시리즈는 표시가 시리즈의 일부인 경우에만 필요합니다. |
| [[!UICONTROL 시리즈 이름]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#show) | `show` | 문자열 | 프로그램/시리즈 이름. 프로그램 이름은 표시가 시리즈의 일부인 경우에만 필요합니다. |
| [[!UICONTROL 유형 표시]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#show-type) | `showType` | 문자열 | 컨텐츠 유형(예: 트레일러 또는 전체 에피소드). |
| [[!UICONTROL 스트림 형식]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#stream-format) | `streamFormat` | 문자열 | 스트림 형식(HD, SD)입니다. |
| [[!UICONTROL 스트림 형식]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#stream-type) | `streamType` | 문자열 | 미디어 스트림의 유형입니다. |
| [[!UICONTROL 총 일시 중단 기간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#total-pause-duration) | `pauseTime` | 정수 | [!UICONTROL 총 일시 중지 기간]은(는) 사용자가 재생을 일시 중지한 기간(초)을 설명합니다. |
| [[!UICONTROL 고유 재생 시간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#unique-time-played) | `uniqueTimePlayed` | 정수 | 시간 미디어 에셋에서 사용자가 본 고유 간격의 합을 설명합니다(즉, 여러 번 본 재생 간격 길이는 오직 한 번만 카운트됨). |
| [[!UICONTROL 버전]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#sdk-version) | `appVersion` | 문자열 | 플레이어에서 사용하는 SDK 버전입니다. 플레이어에 적합한 사용자 정의 값을 가질 수 있습니다. |
| [[!UICONTROL 비디오 세그먼트]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=ko#content-segment) | `segment` | 문자열 | 조회한 콘텐츠 중 일부를 설명하는 간격(단위: 분). |

{style="table-layout:auto"}

<!-- Could not find details for :
Ad Load Type
Content Delivery Network
Pccr
Pev3
-->
