---
title: Experience Platform UI를 사용하여 AWS으로 고객 관리 키 설정 및 구성
description: Amazon 리소스 이름(ARN)으로 CMK 앱을 설정하고 암호화 키 ID를 Adobe Experience Platform으로 전송하는 방법에 대해 알아봅니다.
exl-id: f0e38a60-d448-4975-977e-1367fca10515
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# Experience Platform UI를 사용하여 AWS으로 고객 관리 키 설정 및 구성

이 안내서를 사용하여 Experience Platform UI를 통해 AWS에서 호스팅되는 Experience Platform 인스턴스용 CMK(Customer Managed Keys)를 활성화할 수 있습니다.

>[!IMPORTANT]
>
>이 안내서를 계속하기 전에 [의 CMK용 AWS KMS 구성](./configure-kms.md) 문서에 자세히 설명된 설정을 완료했는지 확인하십시오.

## AWS 키 정책을 업데이트하여 Experience Platform과 키 통합

AWS 키를 Experience Platform과 통합하려면 KMS 작업 영역의 **[!DNL Key Policy]** 섹션에서 JSON을 편집해야 합니다. 기본 키 정책은 아래 JSON과 유사합니다.

<!-- The AWS ID below is fake. Q) Can I refer to it simply as AWS_ACCOUNT_ID ? Is that suitable? -->

```JSON
{
  "Id": "key-consolepolicy-3",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Enable IAM User Permissions",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123464903283:root" // this is a mock AWS Principal ID, your ID will differ
      },
      "Action": "kms:*",
      "Resource": "*"
    }
  ]
}
```

위의 예에서 동일한 계정(`Principal.AWS`) 내의 모든 리소스(`"Resource": "*"`)가 키에 액세스할 수 있습니다. 이 정책을 사용하면 지정된 계정으로 제한된 암호화 및 암호 해독 작업을 계정의 서비스에서 수행할 수 있습니다. 이 키에 대한 액세스 권한을 Experience Platform 단일 테넌트 계정에 부여하려면 기본 AWS 정책에 새 문을 추가하십시오. Experience Platform UI에서 필요한 JSON 정책을 가져와 AWS KMS 키에 적용하여 Adobe Experience Platform과의 보안 연결을 설정할 수 있습니다.

Experience Platform UI에서 왼쪽 탐색 레일의 **[!UICONTROL 관리]** 섹션으로 이동한 다음 **[!UICONTROL 암호화]**&#x200B;를 선택합니다. [!UICONTROL 암호화 구성] 작업 영역의 [!UICONTROL 고객 관리 키] 카드에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![고객 관리 키 카드에 강조 표시된 [구성]이 있는 Experience Platform 암호화 구성 작업 영역입니다.](../../../images/governance-privacy-security/key-management-service/encryption-configuration.png)

[!UICONTROL 고객 관리 키 구성]이 나타납니다. [!UICONTROL 고객 관리 키] [!UICONTROL 암호화 구성]에 표시된 CMK KMS 정책에서 `statement` 개체를 복사합니다.

<!-- Select the copy icon (![A copy icon.](../../../../images/icons/copy.png)) to copy the CMK KMS policy to your clipboard. A green pop-up notification confirms that the policy was copied.  -->

<!-- I cannot add the 'and the copy icon highlighted.' to the alt text below as i do not have access to this UI. -->

![CMK KMS 정책이 표시된 고객 관리 키 구성입니다.](../../../images/governance-privacy-security/key-management-service/copy-cmk-policy.png)

<!-- This part of the workflow was in contention at the time of the demo.  -->

그런 다음 AWS KMS 작업 영역으로 돌아가 아래에 표시된 키 정책을 업데이트합니다.

![업데이트된 정책과 [마침]이 강조 표시된 워크플로의 검토 단계입니다.](../../../images/governance-privacy-security/key-management-service/updated-cmk-policy.png)

아래 표시된 대로 [!UICONTROL 플랫폼 암호화 구성] 작업 영역에서 다음 네 개의 문을 기본 정책에 추가합니다. `Enable IAM User Permissions`, `CJA Flow IAM User Permissions`, `CJA Integrity IAM User Permissions`, `CJA Oberon IAM User Permissions`.

```json
{
    "Version": "2012-10-17",
    "Id": "key-consolepolicy",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::975049898882:root" // this is a mock AWS Principal ID, your ID will differ
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "975049898882" // this is a mock AWS Principal ID, your ID will differ
                }
            }
        },
        {
            "Sid": "CJA Flow IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::767397686373:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "767397686373"
                }
            }
        },
        {
            "Sid": "CJA Integrity IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::730335345392:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "730335345392"
                }
            }
        },
        {
            "Sid": "CJA Oberon IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::891377157113:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "891377157113"
                }
            }
        }
    ]
}
```

업데이트된 정책을 확인하고 키를 만들려면 **[!DNL Finish]**&#x200B;을(를) 선택하십시오. 이제 구성에는 5개의 명령문이 포함되어 있으므로 AWS 계정이 Adobe Experience Platform과 통신할 수 있습니다. 변경 사항이 즉시 적용됩니다.

AWS [!DNL Key Management Service]의 업데이트된 [!DNL Customer Managed Keys] 작업 영역이 나타납니다.

### Experience Platform에 AWS 암호화 키 세부 정보 추가

그런 다음 암호화를 사용하려면 키의 Amazon 리소스 이름(ARN)을 Experience Platform [!UICONTROL 고객 관리 키 구성]에 추가하십시오. AWS의 [!DNL Customer Managed Keys] 섹션에서 [!DNL Key Management Service]의 목록에서 새 키의 별칭을 선택합니다.

![새 키 별칭이 강조 표시된 AWS KMS 고객 관리 키 작업 영역입니다.](../../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

키의 세부 정보가 표시됩니다. AWS의 모든 항목에는 Amazon 리소스 이름(ARN)이 있으며,
는 AWS 서비스 전반에 걸쳐 리소스를 지정하는 데 사용되는 고유 식별자입니다. 표준화된 형식 `arn:partition:service:region:account-id:resource`을(를) 따릅니다.

복사 아이콘을 선택하여 ARN을 복사합니다. 확인 대화 상자가 나타납니다.

![ARN이 강조 표시된 AWS KMS 고객 관리 키의 키 세부 정보입니다.](../../../images/governance-privacy-security/key-management-service/keys-details-arn.png)

이제 Experience Platform [!UICONTROL 고객 관리 키 구성] UI로 다시 이동합니다. **[!UICONTROL AWS 암호화 키 세부 정보 추가]** 섹션에서 AWS UI에서 복사한 **[!UICONTROL 구성 이름]** 및 **[!UICONTROL KMS 키 ARN]**&#x200B;을(를) 추가합니다.

![구성 이름과 KMS 키 ARN이 있는 Experience Platform 암호화 구성 작업 영역은 AWS 암호화 키 세부 정보 추가 섹션에서 강조 표시되어 있습니다.](../../../images/governance-privacy-security/key-management-service/add-encryption-key-details.png)

그런 다음 **[!UICONTROL 저장]**&#x200B;을 선택하여 구성 이름, KMS 키 ARN을 제출하고 키 유효성 검사를 시작합니다.

![저장 이 강조 표시된 Experience Platform 암호화 구성 작업 영역입니다.](../../../images/governance-privacy-security/key-management-service/save.png)

[!UICONTROL 암호화 구성] 작업 영역으로 돌아갑니다. 암호화 구성의 상태가 **[!UICONTROL 고객 관리 키]** 카드 하단에 표시됩니다.

![Experience Platform UI의 암호화 구성 작업 공간(고객 관리 키 카드에서 처리 중 강조 표시됨)](../../../images/governance-privacy-security/key-management-service/configuration-status.png)

키를 확인하면 모든 샌드박스에 대한 Data Lake 및 프로필 데이터 저장소에 Key Vault 식별자가 추가됩니다.

>[!NOTE]
>
>프로세스 기간은 데이터 크기에 따라 다릅니다. 일반적으로 프로세스는 24시간 이내에 완료됩니다. 각 샌드박스는 일반적으로 2~3분 후에 업데이트됩니다.

## 키 해지 {#key-revocation}

>[!IMPORTANT]
>
>액세스를 취소하기 전에 다운스트림 애플리케이션에 미치는 키 취소의 영향을 이해합니다.

다음은 키 취소에 대한 주요 고려 사항입니다.

- 키를 취소하거나 비활성화하면 Experience Platform 데이터에 액세스할 수 없게 됩니다. 이 작업은 취소할 수 없으며 주의하여 수행해야 합니다.
- 암호화 키에 대한 액세스가 해지된 경우 전파 타임라인을 고려하십시오. 몇 분에서 24시간 내에 운영 데이터 저장소에 액세스할 수 없게 됩니다. 캐시되거나 일시적인 데이터 저장소는 7일 이내에 액세스할 수 없게 됩니다.

키를 취소하려면 AWS KMS 작업 영역으로 이동합니다. **[!DNL Customer managed keys]** 섹션에는 AWS 계정에 사용할 수 있는 모든 키가 표시됩니다. 목록에서 키의 별칭을 선택합니다.

![새 키 별칭이 강조 표시된 AWS KMS 고객 관리 키 작업 영역입니다.](../../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

키의 세부 정보가 표시됩니다. 키를 비활성화하려면 **[!DNL Key actions]**&#x200B;을(를) 선택한 다음 드롭다운 메뉴에서 **[!DNL Disable]**&#x200B;을(를) 선택합니다.

![키 동작 및 사용 안 함 설정이 강조 표시된 AWS KMS UI의 AWS 키에 대한 세부 정보.](../../../images/governance-privacy-security/key-management-service/disable-key.png)

확인 대화 상자가 나타납니다. **[!DNL Disable key]**&#x200B;을(를) 선택하여 선택을 확인합니다. 키 비활성화의 영향은 약 5분 내에 Experience Platform 애플리케이션 및 UI에 반영되어야 합니다.

>[!NOTE]
>
>키를 비활성화한 후에는 필요에 따라 위에서 설명한 것과 동일한 방법을 사용하여 키를 다시 활성화할 수 있습니다. 이 옵션은 **[!DNL Key actions]** 드롭다운에서 사용할 수 있습니다.

![비활성화 키가 강조 표시된 키 비활성화 대화 상자.](../../../images/governance-privacy-security/key-management-service/disable-key-dialog.png)

또는 키가 다른 서비스에서 사용되는 경우 키 정책에서 직접 Experience Platform에 대한 액세스를 제거할 수 있습니다. **[!DNL Key Policy]** 섹션에서 **[!UICONTROL 편집]**&#x200B;을(를) 선택합니다.

![편집 기능이 있는 AWS 키의 세부 정보 섹션이 키 정책 섹션에 강조 표시되어 있습니다.](../../../images/governance-privacy-security/key-management-service/edit-key-policy.png)

**[!DNL Edit key policy]** 페이지가 나타납니다. Experience Platform UI에서 복사된 정책 문을 강조 표시하고 삭제하여 고객 관리 키 앱에 대한 권한을 제거합니다. 그런 다음 **[!DNL Save changes]**&#x200B;을(를) 선택하여 프로세스를 완료합니다.

![JSON 개체 문 및 변경 내용 저장이 강조 표시된 AWS의 키 정책 작업 영역 편집](../../../images/governance-privacy-security/key-management-service/delete-statement-and-save-changes.png)

## 키 회전 {#key-rotation}

AWS은 자동 및 온디맨드 키 순환을 제공합니다. 키 손상 위험을 줄이거나 보안 규정 준수 요구 사항을 충족하기 위해 필요에 따라 또는 정기적으로 새 암호화 키를 자동으로 생성할 수 있습니다. 자동 키 회전을 예약하여 키의 수명을 제한하고, 키가 손상된 경우 회전 후 사용할 수 없게 됩니다. 최신 암호화 알고리즘의 보안성은 매우 높지만, 키 회전은 중요한 보안 규정 준수 조치이며 보안 모범 사례를 준수하는 것을 보여 줍니다.

### 자동 키 회전 {#automatic-key-rotation}

자동 키 회전은 기본적으로 비활성화되어 있습니다. KMS 작업 영역에서 자동 키 순환을 예약하려면 **[!DNL Key rotation]** 탭을 선택한 다음 **[!DNL Automatic key rotation section]**&#x200B;에서 **[!DNL Edit]**&#x200B;을(를) 선택합니다.

![키 순환 및 편집이 강조 표시된 AWS 키의 세부 정보 섹션입니다.](../../../images/governance-privacy-security/key-management-service/key-rotation.png)

**[!DNL Edit automatic key rotation]** 작업 영역이 나타납니다. 여기에서 라디오 단추를 선택하여 자동 키 회전을 활성화하거나 비활성화합니다. 그런 다음 텍스트 입력 필드 또는 드롭다운 메뉴를 사용하여 키 순환의 기간을 선택합니다. **[!DNL Save]**&#x200B;을(를) 선택하여 설정을 확인하고 주요 세부 정보 작업 영역으로 돌아갑니다.

>[!NOTE]
>
>최소 키 회전 기간은 90일이며, 최대는 2560일입니다.

![순환 기간과 [저장]이 강조 표시된 자동 키 순환 작업 영역 편집](../../../images/governance-privacy-security/key-management-service/automatic-key-rotation.png)

### 온디맨드 키 회전 {#on-demand-key-rotation}

현재 키가 손상된 경우 즉시 키 순환을 수행하려면 **[!DNL Rotate Now]**&#x200B;을(를) 선택하십시오. AWS에서는 이 기능을 10회전으로 제한합니다. 정기 유지 보수의 경우 대신 자동 키 순환을 예약하십시오.

![지금 회전이 강조 표시된 AWS 키의 세부 정보 섹션입니다.](../../../images/governance-privacy-security/key-management-service/on-demand-key-rotation.png)

## 다음 단계

이 문서를 읽고 나면 Adobe Experience Platform용 AWS KMS에서 암호화 키를 만들고, 구성하고, 관리하는 방법에 대해 알아보았습니다. 그런 다음, 조직의 보안 및 규정 준수 정책을 검토하여 키 순환 일정 조정 및 안전한 키 저장 보장 등 Best Practice를 구현합니다.
