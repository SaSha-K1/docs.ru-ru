---
ms.openlocfilehash: 25ce391f917bd270d4d9a75f608e4a8ec763d15c
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497691"
---
### <a name="itemsclear-does-not-remove-duplicates-from-selecteditems"></a>Items.Clear не удаляет дубликаты из SelectedItems

#### <a name="details"></a>Подробнее

Если в элементе Selector, поддерживающем выбор нескольких элементов, в коллекции <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> присутствуют дубликаты, один и тот же элемент присутствует несколько раз.  Удаление этих элементов из источника данных (например, путем вызова Items.Clear) не приведет к их удалению из коллекции <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName>. Будет удален только первый экземпляр. Более того, последующее использование коллекции <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName>, например вызов SelectedItems.Clear(), может вызвать проблемы, например исключение <xref:System.ArgumentException?displayProperty=fullName>, так как коллекция <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> содержит элементы, которые отсутствуют в источнике данных.

#### <a name="suggestion"></a>Предложение

По возможности выполните обновление до .NET 4.6.2.

| name    | Значение       |
|:--------|:------------|
| Область   |Дополнительный номер|
|Version|4.5|
|Type|Среда выполнения|

#### <a name="affected-apis"></a>Затронутые API

- <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.Windows.Controls.Primitives.MultiSelector.SelectedItems`

-->
