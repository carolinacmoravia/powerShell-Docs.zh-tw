---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "其他有用的指令碼物件"
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 8334d0b346e59dea3643a93bf52b780b361d1945
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2017
---
# <a name="other-useful-scripting-objects"></a><span data-ttu-id="ff9ea-103">其他有用的指令碼物件</span><span class="sxs-lookup"><span data-stu-id="ff9ea-103">Other Useful Scripting Objects</span></span>
  <span data-ttu-id="ff9ea-104">下列物件會提供 Windows PowerShell ISE 中額外的指令碼功能。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-104">The following objects provide additional scripting functionality in Windows PowerShell ISE.</span></span> <span data-ttu-id="ff9ea-105">它們不屬於 **$psISE** 階層。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-105">They are not part of the **$psISE** hierarchy.</span></span>

## <a name="useful-scripting-objects"></a><span data-ttu-id="ff9ea-106">有用的指令碼物件</span><span class="sxs-lookup"><span data-stu-id="ff9ea-106">Useful Scripting objects</span></span>

### <a name="psunsupportedconsoleapplications"></a><span data-ttu-id="ff9ea-107">$psUnsupportedConsoleApplications</span><span class="sxs-lookup"><span data-stu-id="ff9ea-107">$psUnsupportedConsoleApplications</span></span>
 <span data-ttu-id="ff9ea-108">有一些關於 Windows PowerShell ISE 與主控台應用程式互動方式的限制。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-108">There are some limitations on how Windows PowerShell ISE interacts with console applications.</span></span> <span data-ttu-id="ff9ea-109">需要使用者介入的命令或自動化指令碼，可能無法依照它從 Windows PowerShell 主控台運作的方式來運作。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-109">A command or an automation script that requires user intervention might not work the way it works from the Windows PowerShell console.</span></span> <span data-ttu-id="ff9ea-110">您可能想要封鎖這些命令或指令碼在 [Windows PowerShell ISE 命令] 窗格中執行。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-110">You might want to block these commands or scripts from running in the Windows PowerShell ISE Command pane.</span></span> <span data-ttu-id="ff9ea-111">**$psUnsupportedConsoleApplications** 物件會保留這類命令的清單。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-111">The **$psUnsupportedConsoleApplications** object keeps a list of such commands.</span></span> <span data-ttu-id="ff9ea-112">如果您嘗試執行此清單中的命令，您會收到不支援這類命令的訊息。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-112">If you try to run the commands in this list, you get a message that they are not supported.</span></span> <span data-ttu-id="ff9ea-113">下列指令碼會在清單中新增項目。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-113">The following script adds an entry to the list.</span></span>

```
# List the unsupported commands
psUnsupportedConsoleApplications
# Add a command to this list
psUnsupportedConsoleApplications.Add(“Mycommand”)
#Show the augmented list of commands
psUnsupportedConsoleApplications

```

### <a name="pslocalhelp"></a><span data-ttu-id="ff9ea-114">$psLocalHelp</span><span class="sxs-lookup"><span data-stu-id="ff9ea-114">$psLocalHelp</span></span>
 <span data-ttu-id="ff9ea-115">這個字典物件會在本機編譯的 HTML 說明檔中，維護說明主題及其相關聯連結之間內容相關性的對應。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-115">This is a dictionary object that maintains a context-sensitive mapping between Help topics and their associated links in the local compiled HTML Help file.</span></span> <span data-ttu-id="ff9ea-116">您可以使用它來尋找特定主題的本機說明。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-116">It is used to locate the local Help for a particular topic.</span></span> <span data-ttu-id="ff9ea-117">您可以新增或刪除此清單中的主題。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-117">You can add or delete topics from this list.</span></span> <span data-ttu-id="ff9ea-118">下列程式碼範例示範一些 **$psLocalHelp** 中所含的索引鍵值組範例。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-118">The following code example shows some example key-value pairs that are contained in **$psLocalHelp**.</span></span>

```
# See the local help map
$psLocalHelp | Format-List

```

### <a name="sample-output"></a><span data-ttu-id="ff9ea-119">取樣輸出</span><span class="sxs-lookup"><span data-stu-id="ff9ea-119">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="ff9ea-120">索引鍵：Add-Computer</span><span class="sxs-lookup"><span data-stu-id="ff9ea-120">Key : Add-Computer</span></span>|<span data-ttu-id="ff9ea-121">值： WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span><span class="sxs-lookup"><span data-stu-id="ff9ea-121">Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span></span>|
|<span data-ttu-id="ff9ea-122">索引鍵：Add-Content</span><span class="sxs-lookup"><span data-stu-id="ff9ea-122">Key : Add-Content</span></span>|<span data-ttu-id="ff9ea-123">值︰WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span><span class="sxs-lookup"><span data-stu-id="ff9ea-123">Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span></span>|

 <span data-ttu-id="ff9ea-124">下列指令碼會在清單中新增項目。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-124">The following script adds an entry to the list.</span></span>

```
$psLocalHelp.Add("get-myNoun","c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a><span data-ttu-id="ff9ea-125">$psOnlineHelp</span><span class="sxs-lookup"><span data-stu-id="ff9ea-125">$psOnlineHelp</span></span>
 <span data-ttu-id="ff9ea-126">這個字典物件會維護說明主題的主題標題及其相關聯外部 URL 之間內容相關性的對應。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-126">This is a dictionary object that maintains a context-sensitive mapping between topic titles of Help topics and their associated external URLs.</span></span> <span data-ttu-id="ff9ea-127">您可以使用它，在 Web 上尋找特定主題的說明。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-127">It is used to locate the Help for a particular topic on the web.</span></span> <span data-ttu-id="ff9ea-128">您可以新增或刪除此清單中的主題。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-128">You can add or delete topics from this list.</span></span>

```
$psOnlineHelp | Format-List

```

### <a name="sample-output"></a><span data-ttu-id="ff9ea-129">取樣輸出</span><span class="sxs-lookup"><span data-stu-id="ff9ea-129">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="ff9ea-130">索引鍵：Add-Computer</span><span class="sxs-lookup"><span data-stu-id="ff9ea-130">Key : Add-Computer</span></span>|<span data-ttu-id="ff9ea-131">值︰http://go.microsoft.com/fwlink/p/?LinkID=135194</span><span class="sxs-lookup"><span data-stu-id="ff9ea-131">Value : http://go.microsoft.com/fwlink/p/?LinkID=135194</span></span>|
|<span data-ttu-id="ff9ea-132">索引鍵：Add-Content</span><span class="sxs-lookup"><span data-stu-id="ff9ea-132">Key : Add-Content</span></span>|<span data-ttu-id="ff9ea-133">值︰http://go.microsoft.com/fwlink/p/?LinkID=113278</span><span class="sxs-lookup"><span data-stu-id="ff9ea-133">Value : http://go.microsoft.com/fwlink/p/?LinkID=113278</span></span>|

 <span data-ttu-id="ff9ea-134">下列指令碼會在清單中新增項目。</span><span class="sxs-lookup"><span data-stu-id="ff9ea-134">The following script adds an entry to the list.</span></span>

```
$psOnlineHelp.Add("get-myNoun","http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a><span data-ttu-id="ff9ea-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ff9ea-135">See Also</span></span>
- [<span data-ttu-id="ff9ea-136">Windows PowerShell ISE 指令碼物件模型</span><span class="sxs-lookup"><span data-stu-id="ff9ea-136">The Windows PowerShell ISE Scripting Object Model</span></span>](../../core-powershell/ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  