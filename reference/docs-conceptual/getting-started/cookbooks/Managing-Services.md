---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "管理服務"
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: 9fd6c8bcfecc99756188409629ddf94b880aab91
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2017
---
# <a name="managing-services"></a><span data-ttu-id="351e7-103">管理服務</span><span class="sxs-lookup"><span data-stu-id="351e7-103">Managing Services</span></span>
<span data-ttu-id="351e7-104">有八個針對各種服務工作設計的核心服務 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="351e7-104">There are eight core Service cmdlets, designed for a wide range of service tasks .</span></span> <span data-ttu-id="351e7-105">我們將只探討列出及變更服務執行中狀態的 Cmdlet，但您可以使用 **Get-Help \&#42;-Service** 取得服務 Cmdlet 清單，並使用 **Get-Help<Cmdlet-Name>** (例如 **Get-Help New-Service**) 尋找每個服務 Cmdlet 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="351e7-105">We will look only at listing and changing running state for services, but you can get a list Service cmdlets by using **Get-Help \&#42;-Service**, and you can find information about each Service cmdlet by using **Get-Help<Cmdlet-Name>**, such as **Get-Help New-Service**.</span></span>

## <a name="getting-services"></a><span data-ttu-id="351e7-106">取得服務</span><span class="sxs-lookup"><span data-stu-id="351e7-106">Getting Services</span></span>
<span data-ttu-id="351e7-107">您可以使用 **Get-Service** Cmdlet 取得本機或遠端電腦上的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-107">You can get the services on a local or remote computer by using the **Get-Service** cmdlet.</span></span> <span data-ttu-id="351e7-108">如同 **Get-Process**，在不使用參數的情況下使用 **Get-Service** 命令會傳回所有服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-108">As with **Get-Process**, using the **Get-Service** command without parameters returns all services.</span></span> <span data-ttu-id="351e7-109">您可以依名稱篩選，甚至可以使用星號作為萬用字元︰</span><span class="sxs-lookup"><span data-stu-id="351e7-109">You can filter by name, even using an asterisk as a wildcard:</span></span>

```
PS> Get-Service -Name se*
Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="351e7-110">因為服務的實際名稱不一定很明顯，所以您有時可能需要依顯示名稱尋找服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-110">Because it is not always obvious what the real name for the service is, you may find you need to find services by display name.</span></span> <span data-ttu-id="351e7-111">您可以依特定名稱、使用萬用字元或使用顯示名稱清單來執行這項操作︰</span><span class="sxs-lookup"><span data-stu-id="351e7-111">You can do this by specific name, using wildcards, or using a list of display names:</span></span>

```
PS> Get-Service -DisplayName se*
Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center
PS> Get-Service -DisplayName ServiceLayer,Server
Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="351e7-112">您可以使用 Get-Service Cmdlet 的 ComputerName 參數取得遠端電腦上的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-112">You can use the ComputerName parameter of the Get-Service cmdlet to get the services on remote computers.</span></span> <span data-ttu-id="351e7-113">ComputerName 參數接受多個值和萬用字元，因此您可以使用單一命令取得多部電腦上的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-113">The ComputerName parameter accepts multiple values and wildcard characters, so you can get the services on multiple computers with a single command.</span></span> <span data-ttu-id="351e7-114">例如，下列命令會取得 Server01 遠端電腦上的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-114">For example, the following command gets the services on the Server01 remote computer.</span></span>

```
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a><span data-ttu-id="351e7-115">取得必要和相依的服務</span><span class="sxs-lookup"><span data-stu-id="351e7-115">Getting Required and Dependent Services</span></span>
<span data-ttu-id="351e7-116">Get-Service Cmdlet 有兩個對服務管理很有用的參數。</span><span class="sxs-lookup"><span data-stu-id="351e7-116">The Get-Service cmdlet has two parameters that are very useful in service administration.</span></span> <span data-ttu-id="351e7-117">DependentServices 參數可取得依存於此服務的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-117">The DependentServices parameter gets services that depend on the service.</span></span> <span data-ttu-id="351e7-118">RequiredServices 參數可取得此服務依存的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-118">The RequiredServices parameter gets services upon which this service depends.</span></span>

<span data-ttu-id="351e7-119">這些參數只會顯示 Get-Service 所傳回之 System.ServiceProcess.ServiceController 物件的 DependentServices 和 ServicesDependedOn (別名=RequiredServices) 屬性值，但它們簡化了命令，讓您更容易取得這項資訊。</span><span class="sxs-lookup"><span data-stu-id="351e7-119">These parameters just display the values of the DependentServices and ServicesDependedOn (alias=RequiredServices) properties of the System.ServiceProcess.ServiceController object that Get-Service returns, but they simplify commands and make getting this information much simpler.</span></span>

<span data-ttu-id="351e7-120">下列命令會取得 LanmanWorkstation 服務所需的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-120">The following command gets the services that the LanmanWorkstation service requires.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices
Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

<span data-ttu-id="351e7-121">下列命令會取得需要 LanmanWorkstation 服務的服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-121">The following command gets the services that require the LanmanWorkstation service.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -DependentServices
Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

<span data-ttu-id="351e7-122">您甚至可以取得具有相依性的所有服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-122">You can even get all services that have dependencies.</span></span> <span data-ttu-id="351e7-123">下列命令會執行這項操作，然後使用 Format-Table Cmdlet 顯示電腦上服務的 Status、Name、RequiredServices 和 DependentServices 屬性。</span><span class="sxs-lookup"><span data-stu-id="351e7-123">The following command does just that, and then it uses the Format-Table cmdlet to display the Status, Name, RequiredServices and DependentServices properties of the services on the computer.</span></span>

```
Get-Service -Name * | where {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a><span data-ttu-id="351e7-124">停止、啟動、暫停及重新啟動服務</span><span class="sxs-lookup"><span data-stu-id="351e7-124">Stopping, Starting, Suspending, and Restarting Services</span></span>
<span data-ttu-id="351e7-125">所有服務 Cmdlet 都有相同的一般形式。</span><span class="sxs-lookup"><span data-stu-id="351e7-125">The Service cmdlets all have the same general form.</span></span> <span data-ttu-id="351e7-126">服務可以使用一般名稱或顯示名稱來指定，並接受清單和萬用字元作為值。</span><span class="sxs-lookup"><span data-stu-id="351e7-126">Services can be specified by common name or display name, and take lists and wildcards as values.</span></span> <span data-ttu-id="351e7-127">若要停止列印多工緩衝處理器，請使用：</span><span class="sxs-lookup"><span data-stu-id="351e7-127">To stop the print spooler, use:</span></span>

```
Stop-Service -Name spooler
```

<span data-ttu-id="351e7-128">若要啟動已停止的列印多工緩衝處理器，請使用：</span><span class="sxs-lookup"><span data-stu-id="351e7-128">To start the print spooler after it is stopped, use:</span></span>

```
Start-Service -Name spooler
```

<span data-ttu-id="351e7-129">若要暫停列印多工緩衝處理器，請使用：</span><span class="sxs-lookup"><span data-stu-id="351e7-129">To suspend the print spooler, use:</span></span>

```
Suspend-Service -Name spooler
```

<span data-ttu-id="351e7-130">**Restart-Service** Cmdlet 與其他服務 Cmdlet 的運作方式相同，不過我們將示範一些更複雜的範例。</span><span class="sxs-lookup"><span data-stu-id="351e7-130">The **Restart-Service** cmdlet works in the same manner as the other Service cmdlets, but we will show some more complex examples for it.</span></span> <span data-ttu-id="351e7-131">最簡單的使用方式是指定服務的名稱︰</span><span class="sxs-lookup"><span data-stu-id="351e7-131">In the simplest use, you specify the name of the service:</span></span>

```
PS> Restart-Service -Name spooler
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

<span data-ttu-id="351e7-132">您會發現自己一再重複收到有關列印多工緩衝處理器正在啟動的警告訊息。</span><span class="sxs-lookup"><span data-stu-id="351e7-132">You will notice that you get a repeated warning message about the Print Spooler starting up.</span></span> <span data-ttu-id="351e7-133">當您執行需要一些時間的服務操作時，Windows PowerShell 會通知您，它仍在嘗試執行工作。</span><span class="sxs-lookup"><span data-stu-id="351e7-133">When you perform a service operation that takes some time, Windows PowerShell will notify you that it is still attempting to perform the task.</span></span>

<span data-ttu-id="351e7-134">如果您想要重新啟動多項服務，您可以取得服務清單、加以篩選，然後執行重新啟動︰</span><span class="sxs-lookup"><span data-stu-id="351e7-134">If you want to restart multiple services, you can get a list of services, filter them, and then perform the restart:</span></span>

```
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

<span data-ttu-id="351e7-135">這些服務 Cmdlet 沒有 ComputerName 參數，但您可以使用 Invoke-Command Cmdlet 在遠端電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="351e7-135">These Service cmdlets do not have a ComputerName parameter, but you can run them on a remote computer by using the Invoke-Command cmdlet.</span></span> <span data-ttu-id="351e7-136">例如，下列命令會重新啟動 Server01 遠端電腦上的多工緩衝處理器服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-136">For example, the following command restarts the Spooler service on the Server01 remote computer.</span></span>

```
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a><span data-ttu-id="351e7-137">設定服務屬性</span><span class="sxs-lookup"><span data-stu-id="351e7-137">Setting Service Properties</span></span>
<span data-ttu-id="351e7-138">Set-Service Cmdlet 會變更本機或遠端電腦上的服務屬性。</span><span class="sxs-lookup"><span data-stu-id="351e7-138">The Set-Service cmdlet changes the properties of a service on a local or remote computer.</span></span> <span data-ttu-id="351e7-139">因為服務狀態是屬性，所以您可以使用這個 Cmdlet 來啟動、停止及暫停服務。</span><span class="sxs-lookup"><span data-stu-id="351e7-139">Because the service status is a property, you can use this cmdlet to start, stop, and suspend a service.</span></span> <span data-ttu-id="351e7-140">Set-Service Cmdlet 也有 StartupType 參數，可讓您變更服務啟動類型。</span><span class="sxs-lookup"><span data-stu-id="351e7-140">The Set-Service cmdlet also has a StartupType parameter that lets you change the service startup type.</span></span>

<span data-ttu-id="351e7-141">若要在 Windows Vista 和更新的 Windows 版本上使用 Set-Service，請使用 [以系統管理員身分執行] 選項開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="351e7-141">To use Set-Service on Windows Vista and later versions of Windows, open Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="351e7-142">如需詳細資訊，請參閱 [Set-Service [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)。</span><span class="sxs-lookup"><span data-stu-id="351e7-142">For more information, see [Set-Service [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>

## <a name="see-also"></a><span data-ttu-id="351e7-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="351e7-143">See Also</span></span>
- [<span data-ttu-id="351e7-144">Get-Service [m2]</span><span class="sxs-lookup"><span data-stu-id="351e7-144">Get-Service [m2]</span></span>](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)
- [<span data-ttu-id="351e7-145">Set-Service [m2]</span><span class="sxs-lookup"><span data-stu-id="351e7-145">Set-Service [m2]</span></span>](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)
- [<span data-ttu-id="351e7-146">Restart-Service [m2]</span><span class="sxs-lookup"><span data-stu-id="351e7-146">Restart-Service [m2]</span></span>](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)
- [<span data-ttu-id="351e7-147">Suspend-Service [m2]</span><span class="sxs-lookup"><span data-stu-id="351e7-147">Suspend-Service [m2]</span></span>](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)
