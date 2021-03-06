---
ms.openlocfilehash: e9f769af6d85403c2a6f085cbc3462cf549adae9
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497332"
---
### <a name="wpf-treeviewitem-must-be-used-within-a-treeview"></a>В TreeView необходимо использовать TreeViewItem WPF

#### <a name="details"></a>Подробнее

В версии 4.5 было представлено изменение, которое ограничивает использование элементов <xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName> за пределами <xref:System.Windows.Controls.TreeView?displayProperty=fullName>. Это происходит в следующих случаях.<ul><li>Визуальный родительский элемент <xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName> не является панелью. (<xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName>, созданный для <xref:System.Windows.Controls.TreeView?displayProperty=fullName>, будет иметь панель в качестве родительского элемента.)</li><li><xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName> является потомком <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=fullName>, выступающего в виде &quot;узла элементов&quot; для элемента управления "Список" (ListBox, DataGrid, ListView и т. д.). Виртуализацию включать необязательно.</li><li><xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=fullName> — это прокрутка элемента (<code>ScrollUnit=&quot;Item&quot;</code>).</li><li>Кто-то вызывает <code>VirtualizingStackPanel.MakeVisible(v)</code> для прокрутки элемента <code>v</code> в представлении. Это можно сделать явно или неявно несколькими способами. Возможно, самым распространенным способом является простой щелчок <code>v</code> для перевода в его фокуса.</li><li>Цепочка визуальных родительских элементов от <code>v</code> до <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=fullName> проходит через <xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName>.</li></ul>Другими словами, это происходит в том случае, когда <xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName> используется вне <xref:System.Windows.Controls.TreeView?displayProperty=fullName> и пользователь щелкает потомка <xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName>, чтобы сделать его видимым. Проблема никогда не возникнет, если у <xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName> отсутствуют имеющие фокус потомки. Пример такой ситуации — <xref:System.Windows.Controls.TreeViewItem?displayProperty=fullName> является корнем DataTemplate. При возникновении этой проблемы создается исключение InvalidCastException в рамках платформы WPF.

#### <a name="suggestion"></a>Предложение

Будет создано исправление для этой ошибки.

| name    | Значение       |
|:--------|:------------|
| Область   |Дополнительный номер|
|Version|4.5|
|Type|Среда выполнения|

#### <a name="affected-apis"></a>Затронутые API

Невозможно обнаружить с помощью анализа API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
