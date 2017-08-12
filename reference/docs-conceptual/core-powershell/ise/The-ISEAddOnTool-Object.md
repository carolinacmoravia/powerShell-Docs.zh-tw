---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "ISEAddOnTool 物件"
ms.assetid: ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
ms.openlocfilehash: 15f0cdd1425b9f87edeb0404fc385275e4a9d1d8
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2017
---
# <a name="the-iseaddontool-object"></a><span data-ttu-id="bda85-103">ISEAddOnTool 物件</span><span class="sxs-lookup"><span data-stu-id="bda85-103">The ISEAddOnTool Object</span></span>
  <span data-ttu-id="bda85-104">**ISEAddonTool** 物件代表一個已安裝的附加元件工具，可為 Windows PowerShell ISE 提供額外的功能。</span><span class="sxs-lookup"><span data-stu-id="bda85-104">An **ISEAddonTool** object represents an installed add-on tool that provides additional functionality toWindows PowerShell ISE.</span></span> <span data-ttu-id="bda85-105">**命令**工具即為一例，您可以依序按一下 [檢視] 和 [顯示命令附加元件] 來顯示此工具。</span><span class="sxs-lookup"><span data-stu-id="bda85-105">An example is the **Commands** tool that you can display by clicking **View**, then **Show Command Add-on**.</span></span> <span data-ttu-id="bda85-106">您接著可以藉由操作各種可用的 **ISEAddOnTool** 物件來存取此工具。</span><span class="sxs-lookup"><span data-stu-id="bda85-106">This tool is then accessible to you by manipulating the various available **ISEAddOnTool** objects.</span></span>

 <span data-ttu-id="bda85-107">每個附加元件工具都可以與垂直窗格或水平窗格產生關聯。</span><span class="sxs-lookup"><span data-stu-id="bda85-107">Each add-on tool can be associated with either the vertical pane or the horizontal pane.</span></span> <span data-ttu-id="bda85-108">垂直窗格會停駐於 Windows PowerShell ISE 的右邊。</span><span class="sxs-lookup"><span data-stu-id="bda85-108">The vertical pane is docked to the right edge of Windows PowerShell ISE.</span></span> <span data-ttu-id="bda85-109">水平窗格則會停駐於底部。</span><span class="sxs-lookup"><span data-stu-id="bda85-109">The horizontal pane is docked to the bottom edge.</span></span>

 <span data-ttu-id="bda85-110">Windows PowerShell ISE 中的每個 PowerShell 索引標籤都可以安裝一組自己的附加元件工具。</span><span class="sxs-lookup"><span data-stu-id="bda85-110">Each PowerShell tab in Windows PowerShell ISE can have its own set of add-on tools installed.</span></span> <span data-ttu-id="bda85-111">請參閱 [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md) 和 [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)，來存取可供目前所選取索引標籤使用的工具集合，或者 [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) 集合物件中任何 **PowerShellTab** 物件上的相同屬性。</span><span class="sxs-lookup"><span data-stu-id="bda85-111">See [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md) and [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md) to access the collection of tools available to the currently selected tab or the same properties on any of the **PowerShellTab** objects in the [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) collection object.</span></span>

## <a name="methods"></a><span data-ttu-id="bda85-112">方法</span><span class="sxs-lookup"><span data-stu-id="bda85-112">Methods</span></span>
 <span data-ttu-id="bda85-113">沒有任何 Windows PowerShell ISE 特定的方法適用於這個類別的物件。</span><span class="sxs-lookup"><span data-stu-id="bda85-113">There are no Windows PowerShell ISE-specific methods available for objects of this class.</span></span>

## <a name="properties"></a><span data-ttu-id="bda85-114">[內容]</span><span class="sxs-lookup"><span data-stu-id="bda85-114">Properties</span></span>

###  <span data-ttu-id="bda85-115"><a name="Control"></a> Control</span><span class="sxs-lookup"><span data-stu-id="bda85-115"><a name="Control"></a> Control</span></span>
  <span data-ttu-id="bda85-116">在 Windows PowerShell ISE 3.0 與更新的版本中支援，而且不存在於之前的版本。</span><span class="sxs-lookup"><span data-stu-id="bda85-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="bda85-117">**Control** 屬性可提供許多命令附加元件詳細資料的讀取權。</span><span class="sxs-lookup"><span data-stu-id="bda85-117">The **Control** property provides read access to many of the details of the Commands add-on tool.</span></span>

```
# View the properties of the Commands add-on tool.
# (assumes that it is visible in the vertical pane)
$psISE.CurrentVisibleVerticalTool.Control
HostObject                  : Microsoft.PowerShell.Host.ISE.ObjectModelRoot
Content                     :
HasContent                  :
ContentTemplate             :
ContentTemplateSelector     :
ContentStringFormat         :
BorderBrush                 :
BorderThickness             :
Background                  :
Foreground                  :
FontFamily                  :
FontSize                    :
FontStretch                 :
FontStyle                   :
FontWeight                  :
HorizontalContentAlignment  :
VerticalContentAlignment    :
TabIndex                    :
IsTabStop                   :
Padding                     :
Template                    : System.Windows.Controls.ControlTemplate
Style                       :
OverridesDefaultStyle       :
UseLayoutRounding           :
Triggers                    : {}
TemplatedParent             :
Resources                   : {System.Windows.Controls.TabItem}
DataContext                 :
BindingGroup                :
Language                    :
Name                        :
Tag                         :
InputScope                  :
ActualWidth                 : 370.75
ActualHeight                : 676.559097412109
LayoutTransform             :
Width                       :
MinWidth                    :
MaxWidth                    :
Height                      :
MinHeight                   :
MaxHeight                   :
FlowDirection               : LeftToRight
Margin                      :
HorizontalAlignment         :
VerticalAlignment           :
FocusVisualStyle            :
Cursor                      :
ForceCursor                 :
IsInitialized               : True
IsLoaded                    :
ToolTip                     :
ContextMenu                 :
Parent                      :
HasAnimatedProperties       :
InputBindings               :
CommandBindings             :
AllowDrop                   :
DesiredSize                 : 227.66,676.559097412109
IsMeasureValid              : True
IsArrangeValid              : True
RenderSize                  : 370.75,676.559097412109
RenderTransform             :
RenderTransformOrigin       :
IsMouseDirectlyOver         : False
IsMouseOver                 : False
IsStylusOver                : False
IsKeyboardFocusWithin       : False
IsMouseCaptured             :
IsMouseCaptureWithin        : False
IsStylusDirectlyOver        : False
IsStylusCaptured            :
IsStylusCaptureWithin       : False
IsKeyboardFocused           : False
IsInputMethodEnabled        :
Opacity                     :
OpacityMask                 :
BitmapEffect                :
Effect                      :
BitmapEffectInput           :
CacheMode                   :
Uid                         :
Visibility                  : Visible
ClipToBounds                : False
Clip                        :
SnapsToDevicePixels         : False
IsFocused                   :
IsEnabled                   :
IsHitTestVisible            :
IsVisible                   : True
Focusable                   :
PersistId                   : 1
IsManipulationEnabled       :
AreAnyTouchesOver           : False
AreAnyTouchesDirectlyOver   :
AreAnyTouchesCapturedWithin : False
AreAnyTouchesCaptured       :
TouchesCaptured             : {}
TouchesCapturedWithin       : {}
TouchesOver                 : {}
TouchesDirectlyOver         : {}
DependencyObjectType        : System.Windows.DependencyObjectType
IsSealed                    : False
Dispatcher                  : System.Windows.Threading.Dispatcher

```

###  <span data-ttu-id="bda85-118"><a name="IsVisible"></a> IsVisible</span><span class="sxs-lookup"><span data-stu-id="bda85-118"><a name="IsVisible"></a> IsVisible</span></span>
  <span data-ttu-id="bda85-119">在 Windows PowerShell ISE 3.0 與更新的版本中支援，而且不存在於之前的版本。</span><span class="sxs-lookup"><span data-stu-id="bda85-119">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="bda85-120">布林值屬性，指出附加元件工具目前是否會顯示於它的指派窗格中。</span><span class="sxs-lookup"><span data-stu-id="bda85-120">The Boolean property that indicates whether the add-on tool is currently visible in its assigned pane.</span></span> <span data-ttu-id="bda85-121">如果顯示，您可以將 **IsVisible** 屬性設定為 **$false** 來隱藏工具，或者將 **IsVisible** 屬性設定為 **$true**，讓附加元件工具可顯示於 PowerShell 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="bda85-121">If it is visible, you can set the **IsVisible** property to **$false** to hide the tool, or set the **IsVisible** property to **$true** to make an add-on tool visible on its PowerShell tab.</span></span> <span data-ttu-id="bda85-122">請注意，隱藏附加元件工具之後，就無法再透過 **CurrentVisibleHorizontalTool** 或 **CurrentVisibleVerticalTool** 物件來存取，因此無法透過在該物件上使用這個屬性來顯示。</span><span class="sxs-lookup"><span data-stu-id="bda85-122">Note that after an add-on tool is hidden, it is no longer accessible through the **CurrentVisibleHorizontalTool** or **CurrentVisibleVerticalTool** objects, and therefore cannot be made visible by using this property on that object.</span></span>

```
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible=$true

```

###  <span data-ttu-id="bda85-123"><a name="name"></a> Name</span><span class="sxs-lookup"><span data-stu-id="bda85-123"><a name="name"></a> Name</span></span>
  <span data-ttu-id="bda85-124">在 Windows PowerShell ISE 3.0 與更新的版本中支援，而且不存在於之前的版本。</span><span class="sxs-lookup"><span data-stu-id="bda85-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="bda85-125">可取得附加元件工具名稱的唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="bda85-125">The read-only property that gets the name of the add-on tool.</span></span>

```
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.name
Commands

```

## <a name="see-also"></a><span data-ttu-id="bda85-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bda85-126">See Also</span></span>
- [<span data-ttu-id="bda85-127">ISEAddOnToolCollection 物件</span><span class="sxs-lookup"><span data-stu-id="bda85-127">The ISEAddOnToolCollection Object</span></span>](The-ISEAddOnToolCollection-Object.md)
- [<span data-ttu-id="bda85-128">Windows PowerShell ISE 指令碼物件模型</span><span class="sxs-lookup"><span data-stu-id="bda85-128">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="bda85-129">Windows PowerShell ISE 物件模型參考</span><span class="sxs-lookup"><span data-stu-id="bda85-129">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [<span data-ttu-id="bda85-130">ISE 物件模型階層</span><span class="sxs-lookup"><span data-stu-id="bda85-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
