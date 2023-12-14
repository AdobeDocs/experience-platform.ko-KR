---
title: 세션 세부 정보 데이터 유형
description: 세션 세부 정보 XDM(Experience Data Model) 데이터 유형에 대해 알아봅니다.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 8%

---

# [!UICONTROL 세션 세부 정보] 데이터 유형

[!UICONTROL 세션 세부 정보] 는 미디어 재생 세션과 관련된 데이터를 추적하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 스키마는 미디어 콘텐츠가 소비되는 방식에 대한 통찰력을 제공하는 광범위한 속성을 포함합니다. 사용 [!UICONTROL 세션 세부 정보] 재생 이벤트, 광고 상호 작용, 진행률 마커, 일시 중지 및 기타 지표를 로깅하여 사용자 참여를 캡처하는 데이터 유형입니다. 이를 통해 사용자 행동 및 콘텐츠 소비 패턴에 대한 중요한 통찰력을 얻을 수 있습니다.

+++세션 세부 정보 데이터 유형의 다이어그램을 표시하려면 선택합니다.
![세션 세부 정보 데이터 유형의 다이어그램입니다.](../images/data-types/session-details-information.png)
+++

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 미디어 세션 ID] | `ID` | 문자열 | 다음 [!UICONTROL 미디어 세션 ID] 는 개별 재생에 고유한 콘텐츠 스트림의 인스턴스를 식별합니다. |
| [!UICONTROL 컨텐츠 ID] | `name` | 문자열 | **필수** 다음 [!UICONTROL 컨텐츠 ID] 는 콘텐츠에 대한 고유 식별자입니다. 다른 업계 또는 CMS ID에 다시 연결하는 데 사용할 수 있습니다. |
| [!UICONTROL 컨텐츠 이름] | `friendlyName` | 문자열 | 다음 [!UICONTROL 컨텐츠 이름] 는 콘텐츠의 &quot;친숙한&quot;(사람이 읽을 수 있음) 이름입니다. |
| [!UICONTROL 미디어 콘텐츠 길이] | `length` | 정수 | **필수** 다음 [!UICONTROL 미디어 콘텐츠 길이] 클립 길이/런타임 포함 - 사용되는 컨텐츠의 최대 길이(또는 기간)입니다(초). |
| [!UICONTROL 브로드캐스트 콘텐츠 유형] | `contentType` | 문자열 | **필수** 다음 [!UICONTROL 브로드캐스트 콘텐츠 유형] 스트림 전달 중. 사용 가능한 값 [!UICONTROL 스트림 유형] 포함:<br>오디오: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; 및 &quot;radio&quot;;<br>비디오: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; 및 &quot;DVoD&quot;.<br>고객은 이 매개변수에 대한 사용자 정의 값을 제공할 수 있습니다. |
| [!UICONTROL 컨텐츠 플레이어 이름] | `playerName` | 문자열 | **필수** 콘텐츠 플레이어의 이름입니다. |
| [!UICONTROL 콘텐츠 채널] | `channel` | 문자열 | **필수** 다음 [!UICONTROL 콘텐츠 채널] 는 콘텐츠가 재생된 위치의 배포 채널입니다. |
| [!UICONTROL 버전] | `appVersion` | 문자열 | 플레이어에서 사용하는 SDK 버전입니다. 플레이어에 적합한 사용자 정의 값을 가질 수 있습니다. |
| [!UICONTROL 시리즈 이름] | `show` | 문자열 | 프로그램/시리즈 이름. 프로그램 이름은 표시가 시리즈의 일부인 경우에만 필요합니다. |
| [!UICONTROL 시즌 번호] | `season` | 문자열 | 다음 [!UICONTROL 시즌 번호] 시연이 포함된 시연입니다. 시즌 시리즈는 표시가 시리즈의 일부인 경우에만 필요합니다. |
| [!UICONTROL 에피소드 번호] | `episode` | 문자열 | 에피소드의 번호입니다. |
| [!UICONTROL 자산 ID] | `assetID` | 문자열 | 다음 [!UICONTROL 자산 ID] 는 TV 시리즈 에피소드 식별자, 동영상 자산 식별자 또는 라이브 이벤트 식별자와 같은 미디어 자산 컨텐츠에 대한 고유 식별자입니다. 일반적으로 이러한 ID는 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 권한에서 파생됩니다. 이러한 식별자는 다른 소유권 또는 사내 시스템에서도 사용할 수 있습니다. |
| [!UICONTROL 장르] | `genre` | 문자열 | 콘텐츠 생성자가 정의한 콘텐츠 유형 또는 그룹입니다. 값은 변수 구현에서 쉼표로 구분해야 합니다. |
| [!UICONTROL 최초 방송 날짜] | `firstAirDate` | 문자열 | 컨텐츠가 TV에 처음 방송된 날짜. 모든 날짜 형식이 허용되지만, Adobe은 YYYY-MM-DD 형식을 권장합니다. |
| [!UICONTROL 최초 디지털 날짜] | `firstDigitalDate` | 문자열 | 콘텐츠가 디지털 채널 또는 플랫폼에서 처음으로 방송된 날짜. 모든 날짜 형식이 허용되지만, Adobe은 YYYY-MM-DD 형식을 권장합니다. |
| [!UICONTROL 등급 값] | `rating` | 문자열 | TV 유해 콘텐츠 가이드라인으로 정의된 등급. |
| [!UICONTROL  작성자 이름] | `originator` | 문자열 | 콘텐츠 작성자의 이름입니다. |
| [!UICONTROL 브로드캐스트 네트워크] | `network` | 문자열 | 네트워크/채널 이름. |
| [!UICONTROL 유형 표시] | `showType` | 문자열 | 컨텐츠 유형(예: 트레일러 또는 전체 에피소드). |
| [!UICONTROL 광고 로드 유형] | `adLoad` | 문자열 | 각 고객의 내부 표현으로 정의되는 로드된 광고 유형. |
| [!UICONTROL MVPD 식별자] | `mvpd` | 문자열 | 다음 [!UICONTROL MVPD 식별자] Adobe 인증을 통해 제공되었습니다. |
| [!UICONTROL 승인된 미디어] | `authorized` | 문자열 | Adobe 인증을 통해 사용자에게 권한이 부여되었는지 확인합니다. |
| [!UICONTROL 방송 시간대] | `dayPart` | 문자열 | 콘텐츠가 브로드캐스트 또는 재생되는 시간을 정의하는 속성입니다. 이는 고객이 필요에 따라 값을 설정할 수 있습니다 |
| [!UICONTROL 피드 유형] | `feed` | 문자열 | EAST HD 또는 SD와 같은 실제 피드 관련 데이터나 URL과 같은 피드 소스를 나타낼 수 있는 피드 유형입니다. |
| [!UICONTROL 스트림 형식] | `streamFormat` | 문자열 | 스트림 형식(HD, SD)입니다. |
| [!UICONTROL 다시 시작] | `hasResume` | 부울 | 버퍼, 일시 중지 또는 지연 기간이 30분 이상 지난 후 다시 시작된 각 재생을 표시합니다. |
| [!UICONTROL 스트림 유형] | `streamType` | 문자열 | 미디어 스트림의 유형입니다. |
| [!UICONTROL 아티스트] | `artist` | 문자열 | 뮤직 레코딩 또는 비디오를 수행하는 앨범 아티스트나 그룹의 이름. |
| [!UICONTROL 앨범] | `album` | 문자열 | 뮤직 레코딩 또는 비디오가 속한 앨범의 이름. |
| [!UICONTROL 레코드 레이블] | `label` | 문자열 | 레코드 레이블의 이름입니다. |
| [!UICONTROL 작성자] | `author` | 문자열 | 미디어 작성자의 이름입니다. |
| [!UICONTROL 라디오 방송국] | `station` | 문자열 | 오디오가 재생되는 라디오 방송국 이름. |
| [!UICONTROL 게시자] | `publisher` | 문자열 | 오디오 콘텐츠 게시자의 이름입니다. |
| [!UICONTROL 비디오 세그먼트] | `segment` | 문자열 | 조회한 콘텐츠 부분을 설명하는 간격(분). |
| [!UICONTROL 미디어 다운로드 플래그] | `isDownloaded` | 부울 | 다운로드한 후 스트림은 디바이스에서 로컬로 재생됩니다. |
| [!UICONTROL 페더레이션 데이터] | `isFederated` | 부울 | [!UICONTROL 페더레이션 데이터] 히트가 페더레이션되면(즉, 고객이 자체 구현이 아니라 페더레이션된 데이터 공유의 일부로 수신함) true로 설정됩니다. |
| [!UICONTROL 미디어 시작] | `isViewed` | 부울 | 미디어에 대한 로드 이벤트입니다. 이는 뷰어가 재생 버튼을 선택할 때 발생합니다. 이 이벤트는 프리롤 광고, 버퍼링, 오류 등이 있는 경우에도 계산됩니다. |
| [!UICONTROL 콘텐츠 시작] | `isPlayed` | 부울 | [!UICONTROL 컨텐츠 시작] 미디어의 첫 번째 프레임이 사용되면 true가 됩니다. 광고, 버퍼링 중에 사용자가 그만두면 가 없습니다 [!UICONTROL 컨텐츠 시작] 이벤트. |
| [!UICONTROL 컨텐츠 완료] | `isCompleted` | 부울 | [!UICONTROL 컨텐츠 완료] 시간 미디어 에셋이 완료될 때까지 관찰했는지 보여 줍니다. 이 이벤트가 뷰어가 전체 비디오를 시청했음을 의미하지는 않습니다. 뷰어는 앞으로 건너뛸 수도 있습니다. |
| [!UICONTROL 콘텐츠 체류 시간] | `timePlayed` | 정수 | [!UICONTROL 콘텐츠 체류 시간] 기본 컨텐츠에서 재생 유형의 모든 이벤트에 대한 이벤트 기간(초)을 합합니다. |
| [!UICONTROL 미디어 체류 시간] | `totalTimePlayed` | 정수 | 광고 시청 시간을 포함하여 특정 시간 미디어 에셋에서 사용자가 사용한 총 시간을 설명합니다. |
| [!UICONTROL 고유 재생 시간] | `uniqueTimePlayed` | 정수 | 시간 미디어 에셋에서 사용자가 본 고유 간격의 합을 설명합니다(즉, 여러 번 본 재생 간격 길이는 오직 한 번만 카운트됨). |
| [!UICONTROL 분당 평균 시청 시간] | `averageMinuteAudience` | 숫자 | 특정 미디어 항목에 사용된 평균 콘텐츠 시간(즉, 총 콘텐츠 시간을 모든 재생 세션의 길이로 나눈 시간)을 설명합니다. |
| [!UICONTROL 광고 수] | `adCount` | 정수 | 재생 도중 시작된 광고 횟수. |
| [!UICONTROL 챕터 수] | `chapterCount` | 정수 | 재생 도중 시작된 챕터의 수입니다. |
| [!UICONTROL 10% 진행률 마커] | `hasProgress10` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 10%를 통과했음을 나타냅니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [!UICONTROL 25% 진행률 마커] | `hasProgress25` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 25%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [!UICONTROL 50% 진행률 마커] | `hasProgress50` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 50%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [!UICONTROL 75% 진행률 마커] | `hasProgress75` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 75%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [!UICONTROL 95% 진행률 마커] | `hasProgress95` | 부울 | 스트림 길이에 따라 플레이헤드가 미디어 마커의 95%를 통과했음을 보여 줍니다. 마커는 뒤로 검색하는 경우에도 한 번만 카운트됩니다. 앞으로 검색하는 경우 건너뛴 마커는 카운트되지 않습니다. |
| [!UICONTROL 예상 스트림] | `estimatedStreams` | 숫자 | 각 개별 콘텐츠에 대한 예상 비디오 또는 오디오 스트림 수입니다. |
| [!UICONTROL 일시 중단의 영향을 받는 스트림] | `hasPauseImpactedStreams` | 부울 | 단일 미디어 항목 재생 중에 한 번 이상의 일시 정지가 발생했는지 여부를 나타냅니다. |
| [!UICONTROL 이벤트 일시 중지] | `pauseCount` | 정수 | [!UICONTROL 이벤트 일시 중지] 재생 도중 발생한 일시 중지 기간 수를 계산합니다. |
| [!UICONTROL 총 일시 중단 기간] | `pauseTime` | 정수 | [!UICONTROL 총 일시 중단 기간] 사용자가 재생을 일시 중단한 기간(초)을 설명합니다. |
| [!UICONTROL 미디어 세그먼트 보기 수] | `hasSegmentView` | 부울 | [!UICONTROL 미디어 세그먼트 보기 수] 첫 번째 프레임이 아니라 최소 한 개 이상의 프레임이 본 시점을 나타냅니다. |
| [!UICONTROL 미디어 세션 서버 시간 초과] | `secondsSinceLastCall` | 숫자 | 다음 [!UICONTROL 미디어 세션 서버 시간 초과] 마지막으로 알려진 사용자 인터랙션과 세션 종료 시점 사이에 경과한 시간(초)을 나타냅니다. |
| [!UICONTROL 컨텐츠 전달 네트워크] | `cdn` | 문자열 | 다음 [!UICONTROL 컨텐츠 전달 네트워크] 재생된 콘텐츠 |
| [!UICONTROL Pev3] | `pev3` | 문자열 | [!UICONTROL Pev3] 는 보고에 사용되는 미디어 스트림 유형입니다. |
| [!UICONTROL Pccr] | `pccr` | 부울 | [!UICONTROL Pccr] 리디렉션이 발생했음을 나타냅니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
