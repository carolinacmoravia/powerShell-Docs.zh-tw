---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "PowerShell 指令碼"
ms.openlocfilehash: 9214b9e40ff6c181f921f89ef78406af20c30e5f
ms.sourcegitcommit: 755d7bc0740573d73613cedcf79981ca3dc81c5e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="powershell"></a>PowerShell

PowerShell 建基於 .NET Framework，是以工作為基礎的命令列殼層與指令碼語言；專為系統管理員和進階使用者而設計，可快速將多個作業系統 (Linux、macOS、Unix 及 Windows) 的管理，以及這些作業系統上執行的應用程式相關處理序自動化。

## <a name="powershell-is-open-source"></a>PowerShell 是開放原始碼

PowerShell 基本原始程式碼現在可在 GitHub 中取得並開放進行社群參與。 請參閱 [GitHub 上的 PowerShell 原始碼](https://github.com/powershell/powershell)。

您可以從 [get PowerShell](https://github.com/PowerShell/PowerShell#get-powershell) 所需的位元開始。
或者，可能是從[開始使用](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)的快速入門開始

## <a name="powershell-design-goals"></a>PowerShell 設計目標
Windows PowerShell 的設計目的是消除長久以來的問題並加入新功能，以改善命令列和指令碼環境。

### <a name="discoverability"></a>可搜尋性
Windows PowerShell 可讓您輕鬆搜尋它的功能。 例如，若要尋找可檢視和變更 Windows 服務的 Cmdlet 清單，請輸入：

```
Get-Command *-Service
```

搜尋到可完成工作的 Cmdlet 之後，即可使用 Get-Help Cmdlet 進一步了解此 Cmdlet。 例如，若要顯示 Get-Service Cmdlet 的說明，請輸入：

```
Get-Help Get-Service
```
多數 Cmdlet 皆會發出物件，此類物件可操作並轉譯成供顯示用的文字。 若要完全了解該 Cmdlet 的輸出，可將其輸出輸送至 Get-Member Cmdlet。 例如，下列命令會顯示 Get-Service Cmdlet 之物件輸出成員的相關資訊。

```
Get-Service | Get-Member
```

### <a name="consistency"></a>一致性
管理系統是一項複雜的工作，因此擁有一致介面的工具有助控制其中的複雜性。 可惜的是，不論命令列工具或可編寫指令碼的 COM 物件都不具有一致性。

因此，Windows PowerShell 的一致性是非常寶貴的資產。 例如，如果您知道如何使用 Sort-Object Cmdlet，即可利用該知識來排序任何 Cmdlet 的輸出。 而不必去了解每個 Cmdlet 的不同排序常式。

此外，Cmdlet 開發人員也不需要設計其 Cmdlet 的排序功能。 Windows PowerShell 提供具有基本功能的架構，可強制讓介面的許多方面保持一致。 雖然開發人員針對此架構少了一些選擇權，但是這個架構可讓他們更輕鬆開發出強固和易於使用的 Cmdlet。

### <a name="interactive-and-scripting-environments"></a>互動式和指令碼環境
Windows PowerShell 是一種結合的互動式和指令碼環境，可讓您存取命令列工具和 COM 物件，並讓您使用 .NET Framework Class Library (FCL) 的功能。

Windows 命令提示字元提供互動式環境及多種命令列工具，而這個環境則更加強化。 Windows Script Host (WSH) 指令碼可讓您使用多種命令列工具和 COM Automation 物件，但不提供互動式環境；基於此，這個環境也做了改善。

Windows PowerShell 將上述所有功能的存取結合，擴充互動式使用者和指令碼寫入器的功能，並使系統管理更容易進行。

### <a name="object-orientation"></a>物件導向
雖然您可以輸入文字命令來與 Windows PowerShell 互動，但 Windows PowerShell 是以物件為基礎，而非文字。 命令的輸出即為物件。 您可以將輸出物件傳送到另一個命令以作為輸入。 因此，Windows PowerShell 提供熟悉的介面給慣用其他介面的使用者，同時還引入功能強大的全新命令列範例。 它可讓您傳送物件，而不是文字，藉此延伸在命令之間傳送資料的概念。

### <a name="easy-transition-to-scripting"></a>輕鬆轉換指令碼
Windows PowerShell 可將以互動方式輸入命令的作業，輕鬆轉換為建立和執行指令碼。 您可以在 Windows PowerShell 命令提示字元中輸入命令，以探索執行工作的命令。 然後，您可以將這些命令儲存在文字記錄或歷程記錄中，再複製到檔案，以作為指令碼使用。
