---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,設定,安裝"
description: "提供在目標節點管理本機群組的機制。"
title: "DSC GroupSet 資源"
ms.openlocfilehash: 158cb28747c5fe1987eb62b2cc0f6d6f6fb14332
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-groupset-resource"></a>DSC GroupSet 資源

> 適用於：Windows PowerShell Windows 5.0

Windows PowerShell 預期狀態設定 (DSC) 的 **GroupSet** 資源會提供一個機制，在目標節點管理本機群組。 此資源是為 `GroupName` 參數中指定的每個群組呼叫 [Group 資源](groupResource.md)的[複合資源](authoringResourceComposite.md)。

當您想要新增及 (或) 移除多個群組的相同成員清單、移除多個群組，或新增具有相同成員清單的多個群組時，請使用此資源。

##<a name="syntax"></a>語法##
```
Group [string] #ResourceName
{
    GroupName = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ MembersToInclude = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Properties

|  屬性  |  描述   | 
|---|---| 
| GroupName| 您要確保其特定狀態的群組名稱。| 
| MembersToExclude| 使用這個屬性從現有的群組成員資格移除成員。 這個屬性值為字串陣列，格式為 *Domain*\\*UserName*。 如果您在設定中設定這個屬性，請勿使用 **Members** 屬性。 這樣會產生錯誤。| 
| 認證| 存取遠端資源時所需的認證。 **注意**：此帳戶必須具有適當的 Active Directory 權限，藉此將所有非本機帳戶加入群組；否則會發生錯誤。
| Ensure| 表示群組是否存在。 請將此屬性設為 "Absent" 以確保群組不存在。 屬性設定為 "Present" (預設值)，可確保群組存在。| 
| 成員| 您可以使用這個屬性，以指定的成員來取代目前的群組成員資格。 這個屬性值為字串陣列，格式為 *Domain*\\*UserName*。 如果您在設定中設定這個屬性，請勿使用 **MembersToExclude** 或 **MembersToInclude** 屬性。 這樣會產生錯誤。| 
| MembersToInclude| 使用這個屬性將成員新增至群組的現有成員資格。 這個屬性值為字串陣列，格式為 *Domain*\\*UserName*。 如果您在設定中設定這個屬性，請勿使用 **Members** 屬性。 這樣會產生錯誤。| 
| DependsOn | 表示必須先執行另一個資源的設定，再設定這個資源。 例如，如果第一個想要執行的資源設定指令碼區塊的識別碼是 __ResourceName__，而它的類型是 __ResourceType__，則使用這個屬性的語法就是 `DependsOn = "[ResourceType]ResourceName"`。| 

## <a name="example-1"></a>範例 1

下例示範如何確保 "myGroup" 和 "myOtherGroup" 兩個群組會出現。 

```powershell
configuration GroupSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        GroupSet GroupSetTest
        {
            GroupName        = @("myGroup", "myOtherGroup")
            Ensure           = "Present"
            MembersToInclude = @("contoso\alice", "contoso\bob")
            MembersToExclude = $("contoso\john")
            Credential       = Get-Credential
        }
    }
}
$cd = @{
    AllNodes = @(
        @{
            NodeName                    = 'localhost'
            PSDscAllowPlainTextPassword = $true
            PSDscAllowDomainUser        = $true
        }
    )
}


GroupSetTest -ConfigurationData $cd
```

>**注意︰**為求簡潔，本例使用純文字認證。 如需如何在設定 MOF 檔案中加密認證的相關資訊，請參閱[保護 MOF 檔案](secureMOF.md)。


