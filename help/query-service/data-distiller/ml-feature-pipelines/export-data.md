---
title: 외부 ML 환경으로 데이터 내보내기
description: Data Distiller으로 만든 준비된 교육 데이터 세트를 ML 환경에서 읽어 모델을 교육하고 점수를 매길 수 있는 클라우드 스토리지 위치에 공유하는 방법에 대해 알아봅니다.
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 3%

---

# 외부 ML 환경으로 데이터 내보내기

이 문서에서는 Data Distiller으로 만든 준비된 교육 데이터 세트를 ML 환경에서 읽어 모델을 교육하고 점수를 매길 수 있는 클라우드 스토리지 위치에 공유하는 방법을 보여 줍니다. 이 예제에서는 교육 데이터 세트를 [데이터 랜딩 영역(DLZ)](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html). 기계 학습 환경에서 작업하는 데 필요한 경우 저장소 대상을 변경할 수 있습니다.

다음 [대상에 대한 흐름 서비스](https://developer.adobe.com/experience-platform-apis/references/destinations/) 계산된 기능 데이터 세트를 적절한 클라우드 스토리지 위치에 랜딩하여 기능 파이프라인을 완료하는 데 사용됩니다.

## 소스 연결 만들기 {#create-source-connection}

소스 연결은 Adobe Experience Platform 데이터 세트에 대한 연결을 구성할 책임이 있으므로 결과 흐름은 데이터를 찾을 위치와 형식을 정확하게 알 수 있습니다.

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## 대상 연결 만들기 {#create-target-connection}

대상 연결은 대상 파일 시스템에 대한 연결을 담당합니다. 이를 위해서는 먼저 클라우드 스토리지 계정(이 예제의 데이터 랜딩 영역)에 대한 기본 연결을 만든 다음 지정된 압축 및 형식 옵션을 사용하여 특정 파일 경로에 대한 타겟 연결을 만들어야 합니다.

사용 가능한 클라우드 스토리지 대상은 연결 사양 ID로 각각 식별됩니다.

| 클라우드 스토리지 유형 | 연결 사양 ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Azure Blob 저장소 | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure 데이터 레이크 | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| 데이터 랜딩 영역 | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Google 클라우드 스토리지 | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## 데이터 흐름 만들기 {#create-data-flow}

마지막 단계는 소스 연결에 지정된 데이터 세트와 대상 연결에 지정된 대상 파일 경로 사이에 데이터 흐름을 만드는 것입니다.

사용 가능한 각 클라우드 스토리지 유형은 흐름 사양 ID로 식별됩니다.

| 클라우드 스토리지 유형 | 흐름 사양 ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Azure Blob 저장소 | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure 데이터 레이크 | 17be2013-2549-41ce-96e7-a70363bec293 |
| 데이터 랜딩 영역 | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Google 클라우드 스토리지 | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

다음 코드는 일정이 먼 미래로 시작되도록 설정된 데이터 흐름을 만듭니다. 이렇게 하면 모델 개발 중에 Ad Hoc Flow를 트리거할 수 있습니다. 교육된 모델이 있으면 데이터 흐름의 일정을 업데이트하여 원하는 일정에 따라 기능 데이터 세트를 공유할 수 있습니다.

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

데이터 흐름이 만들어지면 이제 임시 흐름 실행을 트리거하여 필요에 따라 기능 데이터 세트를 공유할 수 있습니다.

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## 데이터 랜딩 영역에 대한 공유 간소화

데이터 세트를 데이터 랜딩 영역에 보다 쉽게 공유하려면 `aepp` 라이브러리가 다음을 제공합니다. `exportDatasetToDataLandingZone` 단일 함수 호출에서 위의 단계를 실행하는 함수:

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

이 코드는 제공된 매개 변수를 기반으로 소스 연결, 타겟 연결 및 데이터 흐름을 만들고 데이터 흐름의 임시 실행을 한 단계로 실행합니다.
