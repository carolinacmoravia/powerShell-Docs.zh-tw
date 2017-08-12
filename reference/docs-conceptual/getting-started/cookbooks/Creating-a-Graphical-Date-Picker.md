---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "建立圖形化日期選擇器"
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 5cb952264092d345945318968cf0b3028b11f3e9
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2017
---
# <a name="creating-a-graphical-date-picker"></a><span data-ttu-id="8b073-103">建立圖形化日期選擇器</span><span class="sxs-lookup"><span data-stu-id="8b073-103">Creating a Graphical Date Picker</span></span>
<span data-ttu-id="8b073-104">使用 Windows PowerShell 3.0 與更新的版本建立表單，表單上具有圖形化日曆樣式控制項，可讓使用者選取月份中的某個日期。</span><span class="sxs-lookup"><span data-stu-id="8b073-104">Use Windows PowerShell 3.0 and later releases to create a form with a graphical, calendar-style control that lets users select a day of the month.</span></span>

## <a name="create-a-graphical-date-picker-control"></a><span data-ttu-id="8b073-105">建立圖形化的日期選擇器控制項</span><span class="sxs-lookup"><span data-stu-id="8b073-105">Create a graphical date-picker control</span></span>
<span data-ttu-id="8b073-106">將下列程式碼複製並貼上到 Windows PowerShell ISE，然後將它儲存為 Windows PowerShell 指令碼 (.ps1)。</span><span class="sxs-lookup"><span data-stu-id="8b073-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form 

$form.Text = "Select a Date" 
$form.Size = New-Object Drawing.Size @(243,230) 
$form.StartPosition = "CenterScreen"

$calendar = New-Object System.Windows.Forms.MonthCalendar 
$calendar.ShowTodayCircle = $False
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar) 

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$form.Topmost = $True

$result = $form.ShowDialog() 

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

<span data-ttu-id="8b073-107">指令碼一開始會載入兩個 .NET Framework 類別：**System.Drawing** 和 **System.Windows.Forms**。</span><span class="sxs-lookup"><span data-stu-id="8b073-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="8b073-108">接著，您會啟動新的 .NET Framework 類別 **Windows.Forms.Form** 的執行個體，這樣可以提供空白表單或視窗讓您可以開始新增控制項。</span><span class="sxs-lookup"><span data-stu-id="8b073-108">You then start a new instance of the .NET Framework class **Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```
$form = New-Object Windows.Forms.Form
```

<span data-ttu-id="8b073-109">建立 Form 類別的執行個體之後，指派值給此類別的三個屬性。</span><span class="sxs-lookup"><span data-stu-id="8b073-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

-   <span data-ttu-id="8b073-110">**Text**。</span><span class="sxs-lookup"><span data-stu-id="8b073-110">**Text.**</span></span> <span data-ttu-id="8b073-111">這會成為視窗的標題。</span><span class="sxs-lookup"><span data-stu-id="8b073-111">This becomes the title of the window.</span></span>

-   <span data-ttu-id="8b073-112">**Size**。</span><span class="sxs-lookup"><span data-stu-id="8b073-112">**Size.**</span></span> <span data-ttu-id="8b073-113">這是表單的大小，單位為像素。</span><span class="sxs-lookup"><span data-stu-id="8b073-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="8b073-114">上述指令碼會建立 243 像素寬、230 像素高的表單。</span><span class="sxs-lookup"><span data-stu-id="8b073-114">The preceding script creates a form that’s 243 pixels wide by 230 pixels tall.</span></span>

-   <span data-ttu-id="8b073-115">**StartingPosition**。</span><span class="sxs-lookup"><span data-stu-id="8b073-115">**StartingPosition.**</span></span> <span data-ttu-id="8b073-116">此選擇性屬性在上述指令碼中是設定為 **CenterScreen**。</span><span class="sxs-lookup"><span data-stu-id="8b073-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="8b073-117">若未新增此屬性，Windows 會在表單開啟時選取一個位置。</span><span class="sxs-lookup"><span data-stu-id="8b073-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="8b073-118">透過將 **StartingPosition** 設定為 **CenterScreen**，您可以在每次載入表單時，將表單自動顯示在畫面中間。</span><span class="sxs-lookup"><span data-stu-id="8b073-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```
$form.Text = "Select a Date" 
$form.Size = New-Object Drawing.Size @(243,230) 
$form.StartPosition = "CenterScreen"
```

<span data-ttu-id="8b073-119">接著，在您的表單中建立並新增日曆控制項。</span><span class="sxs-lookup"><span data-stu-id="8b073-119">Next, create and then add a calendar control in your form.</span></span> <span data-ttu-id="8b073-120">在此範例中，目前的日期並未反白顯示或圈起來。</span><span class="sxs-lookup"><span data-stu-id="8b073-120">In this example, the current day is not highlighted or circled.</span></span> <span data-ttu-id="8b073-121">使用者一次只能在日曆上選取一個日期。</span><span class="sxs-lookup"><span data-stu-id="8b073-121">Users can select only one day on the calendar at one time.</span></span>

```
$calendar = New-Object System.Windows.Forms.MonthCalendar 
$calendar.ShowTodayCircle = $False
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

<span data-ttu-id="8b073-122">接著，為您的表單建立 **[確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b073-122">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="8b073-123">指定 **[確定]** 按鈕的大小與行為。</span><span class="sxs-lookup"><span data-stu-id="8b073-123">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="8b073-124">在此範例中，按鈕位置是距離表單上邊緣 165 像素，並距離左邊緣 38 像素。</span><span class="sxs-lookup"><span data-stu-id="8b073-124">In this example, the button position is 165 pixels from the form’s top edge, and 38 pixels from the left edge.</span></span> <span data-ttu-id="8b073-125">按鈕高度是 23 像素，而按鈕寬度是 75 像素。</span><span class="sxs-lookup"><span data-stu-id="8b073-125">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="8b073-126">指令碼會使用預先定義的 Windows Forms 類型來決定按鈕行為。</span><span class="sxs-lookup"><span data-stu-id="8b073-126">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="8b073-127">同樣地，您也會建立 **[取消]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b073-127">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="8b073-128">**[取消]** 按鈕距離上邊緣 165 像素，但距離視窗左邊緣 113 像素。</span><span class="sxs-lookup"><span data-stu-id="8b073-128">The **Cancel** button is 165 pixels from the top, but 113 pixels from the left edge of the window.</span></span>

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="8b073-129">將 **Topmost** 屬性設定為 **$True**，以強制視窗開啟在其他已開啟視窗與對話方塊的上方。</span><span class="sxs-lookup"><span data-stu-id="8b073-129">Set the **Topmost** property to **$True** to force the window to open atop other open windows and dialog boxes.</span></span>

```
$form.Topmost = $True
```

<span data-ttu-id="8b073-130">新增下面這行程式碼，以在 Windows 中顯示該表單。</span><span class="sxs-lookup"><span data-stu-id="8b073-130">Add the following line of code to display the form in Windows.</span></span>

```
$result = $form.ShowDialog()
```

<span data-ttu-id="8b073-131">最後， **If** 區塊內的程式碼會指示 Windows 當使用者選取日曆上的日期並按一下 **[確定]** 按鈕或按下 **Enter** 鍵時要執行的表單動作。</span><span class="sxs-lookup"><span data-stu-id="8b073-131">Finally, the code inside the **If** block instructs Windows what to do with the form after users select a day on the calendar, and then click the **OK** button or press the **Enter** key.</span></span> <span data-ttu-id="8b073-132">Windows PowerShell 會將選取的日期顯示給使用者。</span><span class="sxs-lookup"><span data-stu-id="8b073-132">Windows PowerShell displays the selected date to users.</span></span>

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a><span data-ttu-id="8b073-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8b073-133">See Also</span></span>
- [<span data-ttu-id="8b073-134">Hey Scripting Guy：Why don’t these PowerShell GUI examples work?</span><span class="sxs-lookup"><span data-stu-id="8b073-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644) (Hey Scripting Guy：PowerShell GUI 範例為什麼動不起來？)
- [<span data-ttu-id="8b073-135">GitHub：Dave Wyatt's WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="8b073-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates) (GitHub：Dave Wyatt 的 WinFormsExampleUpdates)
- [<span data-ttu-id="8b073-136">本週 Windows PowerShell 秘訣︰建立圖形化日期選擇器</span><span class="sxs-lookup"><span data-stu-id="8b073-136">Windows PowerShell Tip of the Week:  Creating a Graphical Date Picker</span></span>](http://technet.microsoft.com/library/ff730942.aspx)
