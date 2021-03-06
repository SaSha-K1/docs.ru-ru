---
title: Сопоставление JSON и XML.
ms.date: 03/30/2017
ms.assetid: 22ee1f52-c708-4024-bbf0-572e0dae64af
ms.openlocfilehash: 649d0f50aae806394587c7b79a7970c2de03e087
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/26/2020
ms.locfileid: "96234652"
---
# <a name="mapping-between-json-and-xml"></a>Сопоставление JSON и XML.

Модули чтения и записи, создаваемые фабрикой <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory>, обеспечивают интерфейс API XML к содержимому в формате JavaScript Object Notation (JSON, объектной нотации JavaScript). Формат JSON предусматривает кодирование данных с использованием подмножества объектных литералов JavaScript. Читатели и модули записи, созданные этой фабрикой, также используются при отправке или получении содержимого JSON приложениями Windows Communication Foundation (WCF) с помощью <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement> или <xref:System.ServiceModel.WebHttpBinding> .

Модуль чтения JSON при инициализации JSON-содержимым ведет себя так же, как модуль чтения текстовых XML-данных при инициализации экземпляром XML. Модуль записи JSON при получении последовательности вызовов, в результате которой модуль чтения текстовых XML-данных создает определенный экземпляр XML, записывает JSON-содержимое. В этом разделе описано сопоставление между этим экземпляром XML-данных и JSON-содержимым для использования в сложных сценариях.

Внутренне JSON представляется в виде информационного набора XML при обработке WCF. Обычно внутреннее представление не должно заботить разработчика, поскольку сопоставление является исключительно логическим: JSON обычно не преобразуется физически в XML в памяти, равно как и XML не преобразуется в JSON. Сопоставление означает, что для обращения к JSON-содержимому используются интерфейсы API XML.

Когда WCF использует JSON, обычный сценарий заключается в том, что <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> автоматически подключается к <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> поведению или по <xref:System.ServiceModel.Description.WebHttpBehavior> поведению при необходимости. Сериализатор <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> понимает сопоставление между JSON и набором сведений XML и действует так, как будто работает непосредственно с JSON. (Можно использовать сериализатор <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> без какого-либо модуля чтения или записи XML, зная, что XML соответствует приведенному ниже сопоставлению).

В сложных сценариях может понадобиться непосредственно обратиться к приведенному ниже сопоставлению. Такие сценарии имеют место, когда требуется сериализовать десериализовать JSON особыми способами, не полагаясь на <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>, или при использовании типа <xref:System.ServiceModel.Channels.Message> непосредственно для сообщений, содержащих JSON. Сопоставление JSON-XML также используется для ведения журнала сообщений. При использовании функции ведения журнала сообщений в WCF сообщения JSON регистрируются в виде XML-кода в соответствии с сопоставлением, описанным в следующем разделе.

Для пояснения принципов сопоставления ниже приведен пример JSON-документа.

```json
{"product":"pencil","price":12}
```

Для чтения этого JSON-документа с помощью одного из упомянутых выше модулей чтения используется та же последовательность вызовов класса <xref:System.Xml.XmlDictionaryReader>, что и для чтения следующего XML-документа.

```xml
<root type="object">
    <product type="string">pencil</product>
    <price type="number">12</price>
</root>
```

Кроме того, если сообщение JSON в примере получено WCF и зарегистрировано, то в предыдущем журнале будет отображен фрагмент XML.

## <a name="mapping-between-json-and-the-xml-infoset"></a>Сопоставление между JSON и набором сведений XML

Формально сопоставление происходит между JSON, как описано в [документе RFC 4627](https://www.ietf.org/rfc/rfc4627.txt) (за исключением определенных ограничений, ослабленных и других добавленных ограничений) и информационного набора XML (а не текстового XML), как описано в [наборе данных XML](https://www.w3.org/TR/2004/REC-xml-infoset-20040204/). Определения *элементов информации* и полей в [квадратных скобках] см. в этом разделе.

Пустой документ JSON сопоставляется с пустым XML-документом, а пустой XML-документ сопоставляется с пустым документом JSON. В сопоставлении XML с JSON, предшествующие пробелы и конечные пробелы после документа не допускаются.

Сопоставление определяется между информационной единицей документа (Document Information Item, DII) и информационной единицей элемента (Element Information Item, EII) и JSON. Информационная единица элемента (или свойство [document element] информационной единицы документа) называется корневым элементом JSON. Обратите внимание, что фрагменты документов (XML-данные с несколькими корневыми элементами) в этом сопоставлении не поддерживаются.

Пример. Следующий документ

```xml
<?xml version="1.0"?>
<root type="number">42</root>
```

и следующий элемент

```xml
<root type="number">42</root>
```

оба могут быть сопоставлены JSON. `root`Элемент> <является корневым ЭЛЕМЕНТОМ JSON в обоих случаях.

Кроме того, в случае DII необходимо иметь в виду следующее.

- Некоторые элементы в списке [children] присутствовать не должны. Не следует полагаться на это при чтении XML-данных, полученных из JSON.

- Список [children] не содержит информационных единиц комментариев.

- Список [children] не содержит информационных единиц DTD.

- Список [children] не содержит информационных единиц персональных данных (объявление `<?xml…>` не считается информационной единицей персональных данных).

- Набор [notations] пуст.

- Набор [unparsed entities] пуст.

Пример. Следующий документ не может быть сопоставлен JSON, поскольку список [children] содержит персональные данные и комментарий.

```xml
<?xml version="1.0"?>
<!--comment--><?pi?>
<root type="number">42</root>
```

EII для корневого элемента JSON имеет следующие характеристики.

- Свойство [local name] имеет значение "root".

- Свойство [namespace name] не имеет значения.

- Свойство [prefix] не имеет значения.

- Список [children] может содержать информационные единицы элементов (которые представляют внутренние элементы; см. описание ниже) или информационные единицы символов (Character Information Item, CII; см. описание ниже) либо ни то, ни другое, но не то и другое одновременно.

- Набор [attributes] может содержать приведенные ниже необязательные информационные единицы атрибутов (Attribute Information Item, AII).

- Атрибут типа JSON ("type") (см. описание ниже). Этот атрибут используется для сохранения типа JSON (string, number, boolean, object, array или null) в полученных в результате сопоставления XML-данных.

- Атрибут имени контракта данных (" \_ \_ тип"), как описано далее. Этот атрибут может присутствовать только при условии, что присутствует также атрибут типа JSON и его свойство [normalized value] имеет значение "object". Этот атрибут используется сериализатором `DataContractJsonSerializer` для сохранения сведений о типе контракта данных - например, в случаях полиморфизма, где сериализуется производный тип и где ожидается базовый тип. Если используется не `DataContractJsonSerializer`, в большинстве случаев этот атрибут игнорируется.

- [в пространствах имен в области] содержит привязку "XML" в `http://www.w3.org/XML/1998/namespace` соответствии со спецификацией информационного набора.

- Свойства [children], [attributes] и [in-scope namespaces] не должны содержать никаких единиц, кроме указанных выше, а свойство [namespace attributes] не должно иметь никаких членов; тем не менее, при чтении XML-данных, полученных из JSON, на это полагаться нельзя.

Пример. Следующий документ не может быть сопоставлен JSON, поскольку набор [namespace attributes] не пуст.

```xml
<?xml version="1.0"?>
<root xmlns:a="myattributevalue">42</root>
```

AII для атрибута типа JSON имеет следующие характеристики.

- Свойство [namespace name] не имеет значения.
- Свойство [prefix] не имеет значения.
- Свойство [local name] имеет значение «type».
- Свойство [normalized value] имеет одно из возможных значений-типов, описанных в следующем разделе.
- Флаг [specified] имеет значение `true`.
- Свойство [attribute type] не имеет значения.
- Свойство [references] не имеет значения.

AII для атрибута имени контракта данных JSON имеет следующие характеристики.

- Свойство [namespace name] не имеет значения.
- Свойство [prefix] не имеет значения.
- [local name] — " \_ \_ Type" (два символа подчеркивания и затем "тип").
- Свойство [normalized value] равно любой строке Юникод - сопоставление этой строки с JSON описывается в следующем разделе.
- Флаг [specified] имеет значение `true`.
- Свойство [attribute type] не имеет значения.
- Свойство [references] не имеет значения.

Внутренние элементы, содержащиеся в корневом элементе JSON или других внутренних элементах, имеют следующие характеристики.

- [локальное имя] может иметь любое значение, как описано далее.
- Свойства [namespace name], [prefix], [children], [attributes], [namespace attributes] и [in-scope namespaces] подчиняются тем же правилам, что и корневой элемент JSON.

И в корневом элементе JSON, и во внутренних элементах атрибут типа JSON определяет сопоставление с JSON, возможные дочерние информационные единицы ([children]) и их интерпретацию. Атрибут [нормализованное значение] учитывает регистр, должен быть строчным и не может содержать пробелы.

|[нормализованное значение] все атрибута типа JSON|Допустимые дочерние информационные единицы соответствующей EII|Соответствие в JSON|
|---------------------------------------------------------|---------------------------------------------------|---------------------|
|`string` (или отсутствие AII типа JSON)<br /><br /> `string` и отсутствие AII типа JSON - одно и то же, поэтому `string` используется по умолчанию.<br /><br /> Следовательно, `<root> string1</root>` соответствует `string` "string1" в JSON.|0 или более CII|Фрагмент JSON типа `string` (RFC по JSON, раздел 2.5). Каждый фрагмент типа `char` - это символ, соответствующий свойству [character code] из CII. Если CII нет, он сопоставляется пустому фрагменту JSON типа `string`.<br /><br /> Пример. Следующий элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="string">42</root>`<br /><br /> Фрагмент JSON: "42".<br /><br /> При сопоставлении XML-JSON символы, которые должны быть снабжены escape-символом, сопоставляются символам с escape-символом, все остальные символы сопоставляются символам без escape-символа. Символ "/" является специальным — он экранирован, даже если он не должен быть (записан как " \\ /").<br /><br /> Пример. Следующий элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="string">the "da/ta"</root>`<br /><br /> Фрагмент JSON — это " \\ /та Da" \\ \\ .<br /><br /> При сопоставлении JSON-XML символы с escape-знаком и символы без escape-знака корректно сопоставляются соответствующему свойству [character code].<br /><br /> Пример. Фрагмент JSON "\u0041BC" сопоставляется следующему XML-элементу:<br /><br /> `<root type="string">ABC</root>`<br /><br /> Строка может быть заключена в пробелы ("ws" в разделе 2 JSON RFC), которая не сопоставлена с XML.<br /><br /> Пример. Фрагмент JSON           "ABC" (с пробелами перед первой двойной кавычкой) сопоставляется следующему XML-элементу:<br /><br /> `<root type="string">ABC</root>`<br /><br /> Все пробелы в XML сопоставлены с пробелами в JSON.<br /><br /> Пример. Следующий XML-элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="string">  A BC      </root>`<br /><br /> Фрагмент JSON: " A BC ".|
|`number`|1 или более CII|JSON `number` (JSON RFC, раздел 2,4), возможно, окружен пробелами. Каждый символ в сочетании чисел и пробелов является символом, который соответствует [коду символа] из ции.<br /><br /> Пример. Следующий элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="number">    42</root>`<br /><br /> Фрагмент JSON:    42<br /><br /> (Пробел сохраняется).|
|`boolean`|4 или 5 CII (что соответствует `true` или `false` ), возможно, окружены дополнительными пробелами CII.|Последовательность CII, соответствующая строке "true", сопоставляется литералу `true`, а последовательность CII, соответствующая строке "false", сопоставляется литералу `false`. Окружающие пробелы сохраняются.<br /><br /> Пример. Следующий элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="boolean"> false</root>`<br /><br /> Фрагмент JSON: `false`.|
|`null`|Не допускается ни одного.|Литерал `null`. Для сопоставления JSON с XML `null` может быть окружено пробелом ("ws" в разделе 2), который не сопоставлен с XML.<br /><br /> Пример. Следующий элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="null"/>`<br /><br /> или<br /><br /> `<root type="null"></root>`<br /><br /> :<br /><br /> Фрагмент JSON в обоих случаях - `Null`.|
|`object`|0 или более EII.|Фрагмент `begin-object` (левая фигурная скобка), согласно разделу 2.2 RFC по JSON, после которой идет запись-член для каждой EII, как описано ниже. Если EII больше одной, между записями-членами ставятся разделители значений (запятые). После этого идет фрагмент end-object (правая фигурная скобка).<br /><br /> Пример. Следующий элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="object">`<br /><br /> `<type1 type="string">aaa\</type1>`<br /><br /> `<type2 type="string">bbb\</type2>`<br /><br /> `</root >`<br /><br /> Фрагмент JSON: `{"type1":"aaa","type2":"bbb"}`.<br /><br /> Если в сопоставлении XML-JSON присутствует атрибут типа контракта данных, в начале вставляется дополнительная запись-член. Его имя является [локальным именем] атрибута типа контракта данных (" \_ \_ тип"), а его значением является [нормализованное значение] атрибута. И наоборот, при сопоставлении JSON с XML, если имя первой записи члена является [локальным именем] атрибута типа контракта данных (то есть " \_ \_ тип"), соответствующий атрибут типа контракта данных содержится в сопоставленном XML, но соответствующий EII отсутствует. Обратите внимание, что для применения этого особого сопоставления эта запись-член должна идти первой в объекте JSON. Это отход от обычной обработки JSON, где порядок записей-членов не имеет значения.<br /><br /> Пример:<br /><br /> Следующий фрагмент JSON сопоставляется XML.<br /><br /> `{"__type":"Person","name":"John"}`<br /><br /> XML представляет собой следующий код.<br /><br /> `<root type="object" __type="Person">   <name type="string">John</name> </root>`<br /><br /> Обратите внимание, что \_ \_ ПРИСУТСТВУЕТ тип все, но отсутствует \_ \_ тип EII.<br /><br /> Однако если порядок в JSON будет обратным, как показано в следующем примере:<br /><br /> `{"name":"John","\_\_type":"Person"}`<br /><br /> соответствующий XML-код будет выглядеть так:<br /><br /> `<root type="object">   <name type="string">John</name>   <__type type="string">Person</__type> </root>`<br /><br /> То есть \_ _Type прекращает иметь особое значение и сопоставляется с EII, как обычно, а не все.<br /><br /> Правила добавления/удаления escape-знаков для свойства [normalized value] AII при сопоставлении значению JSON такие же, как и для строк JSON (см. строку "string" выше в таблице).<br /><br /> Пример:<br /><br /> `<root type="object" __type="\abc" />`<br /><br /> Предыдущий пример может быть сопоставлен следующему фрагменту JSON.<br /><br /> `{"__type":"\\abc"}`<br /><br /> При сопоставлении XML с JSON первый EII [локальное имя] не должен быть " \_ \_ Type".<br /><br /> Пробел ( `ws` ) никогда не создается при сопоставлении XML с JSON для объектов и игнорируется при сопоставлении JSON с XML.<br /><br /> Пример. Следующий фрагмент JSON сопоставляется XML-элементу:<br /><br /> `{ "ccc" : "aaa", "ddd" :"bbb"}`<br /><br /> XML-элемент показан в следующем коде.<br /><br /> `<root type="object">    <ccc type="string">aaa</ccc>    <ddd type="string">bbb</bar> </root >`|
|массиве|0 или более EII|Фрагмент begin-array (левая квадратная скобка), согласно разделу 2.3 RFC по JSON, после которой идет запись-массив для каждой EII, как описано ниже. Если EII больше одной, между записями-массивами ставятся разделители значений (запятые). После этого идет фрагмент end-array.<br /><br /> Пример. Следующий XML-элемент сопоставляется фрагменту JSON:<br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`<br /><br /> Фрагмент JSON `["aaa","bbb"]`<br /><br /> Пробел ( `ws` ) никогда не создается в сопоставлении XML с JSON для массивов и игнорируется в сопоставлении JSON с XML.<br /><br /> Пример. фрагмент JSON.<br /><br />`["aaa", "bbb"]`<br /><br /> XML-элемент, которому он сопоставляется:<br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`|

Записи-члены работают следующим образом.

- Свойство [local name] внутреннего элемента сопоставляется `string`-части фрагмента `member`, согласно 2.2 RFC по JSON.

Пример. Следующий элемент сопоставляется фрагменту JSON:

```xml
<root type="object">
    <myLocalName type="string">aaa</myLocalName>
</root>
```

Получается следующий фрагмент JSON:

```json
{"myLocalName":"aaa"}
```

- При сопоставлении XML-JSON символы, которые в JSON должны быть снабжены escape-знаком, предваряются escape-знаком, остальные символы - нет. Символ "/", хотя и не является требующим escape-знака символом, тем не менее предваряется escape-знаком (при сопоставлении JSON-XML предварять escape-знаком его не нужно). Это необходимо для поддержки формата AJAX ASP.NET для данных типа `DateTime` в JSON.

- При сопоставлении JSON-XML все символы (включая символы без escape-знака, если необходимо) используются для формирования фрагмента типа `string`, который представляет собой значение свойства [local name].

- Внутренние элементы (список [children]) сопоставляются значению в разделе 2.2, в соответствии с атрибутом типа JSON (`JSON Type Attribute`), аналогично корневому элементу JSON (`Root JSON Element`). Несколько уровней вложения EII (включая вложения в массивах) допустимы.

Пример. Следующий элемент сопоставляется фрагменту JSON:

```xml
<root type="object">
    <myLocalName1 type="string">myValue1</myLocalName1>
    <myLocalName2 type="number">2</myLocalName2>
    <myLocalName3 type="object">
        <myNestedName1 type="boolean">true</myNestedName1>
        <myNestedName2 type="null"/>
    </myLocalName3>
</root >
```

В результате получается следующий фрагмент JSON:

```json
{"myLocalName1":"myValue1","myLocalName2":2,"myLocalName3":{"myNestedName1":true,"myNestedName2":null}}
```

> [!NOTE]
> В показанном выше сопоставлении отсутствует этап XML-кодирования. Поэтому WCF поддерживает только документы JSON, в которых все символы в именах ключей являются допустимыми символами в именах XML-элементов. Например, документ JSON {"<": "a"} не поддерживается, так как < не является допустимым именем для XML-элемента.

Обратная ситуация (символы, допустимые в XML, но недопустимые в JSON) никаких проблем не вызывает, поскольку описанное выше сопоставление предусматривает добавление или удаление escape-символов JSON.

Записи-массивы работают следующим образом.

- Свойство [local name] внутреннего элемента имеет значение "item".

- Список [children] внутреннего элемента сопоставляется значению в разделе 2.3, в соответствии с атрибутом типа JSON, как и для корневого элемента JSON. Несколько уровней вложения EII (включая вложения в объектах) допустимы.

Пример. Следующий элемент сопоставляется фрагменту JSON:

```xml
<root type="array">
    <item type="string">myValue1</item>
    <item type="number">2</item>
    <item type="array">
    <item type="boolean">true</item>
    <item type="null"/></item>
</root>
```

Фрагмент JSON выглядит следующим образом:

```json
["myValue1",2,[true,null]]
```

## <a name="see-also"></a>См. также

- <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>
- [Автономная сериализация JSON](stand-alone-json-serialization.md)
