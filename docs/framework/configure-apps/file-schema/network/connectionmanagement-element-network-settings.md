---
title: Элемент <connectionManagement> (параметры сети)
description: <connectionManagement>Элемент "Параметры сети" указывает максимальное число подключений к сетевому узлу в .NET Framework.
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement
- http://schemas.microsoft.com/.NetConfiguration/v2.0#connectionManagement
helpviewer_keywords:
- <connectionManagement> element
- connectionManagement element
ms.assetid: bedccaab-12a2-4511-8f67-e961f249aec6
ms.openlocfilehash: 52b780c739a00cb53694b547ee1a33c1b5d98c86
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91167318"
---
# <a name="connectionmanagement-element-network-settings"></a>Элемент \<connectionManagement> (параметры сети)

Задает максимальное число подключений к сетевому узлу.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<connectionManagement>**

## <a name="syntax"></a>Синтаксис  
  
```xml  
<connectionManagement>
</connectionManagement>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  

 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  

 Отсутствует.  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|**Элемент**|**Описание**|  
|-----------------|---------------------|  
|[add](add-element-for-connectionmanagement-network-settings.md)|Добавляет IP-адрес или DNS-имя в список управления подключениями.|  
|[пусто](clear-element-for-connectionmanagement-network-settings.md)|Очищает список управления подключениями.|  
|[remove](remove-element-for-connectionmanagement-network-settings.md)|Удаляет IP-адрес или DNS-имя из списка управления подключениями.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|**Элемент**|**Описание**|  
|-----------------|---------------------|  
|[system.net](system-net-element-network-settings.md)|Содержит параметры сети, определяющие способ подключения .NET Framework к Интернету.|  
  
## <a name="remarks"></a>Remarks  

 `connectionManagement`Элемент определяет максимальное число подключений к серверу или группе серверов.  
  
## <a name="configuration-files"></a>Файлы конфигурации  

 Этот элемент может использоваться в файле конфигурации приложения или в файле конфигурации компьютера (Machine.config).  
  
## <a name="example"></a>Пример  

 В следующем примере приложение настраивается для использования четырех подключений к серверу `www.contoso.com` и двух подключений ко всем остальным серверам.  
  
```xml  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <add address = "http://www.contoso.com" maxconnection = "4" />  
      <add address = "*" maxconnection = "2" />  
    </connectionManagement>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также раздел

- <xref:System.Net.ServicePoint>
- <xref:System.Net.ServicePointManager>
- [Схема параметров сети](index.md)
