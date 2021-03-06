---
title: Размещение веб-узлов в приложении, использующем очереди
ms.date: 03/30/2017
ms.assetid: c7a539fa-e442-4c08-a7f1-17b7f5a03e88
ms.openlocfilehash: c2b41ee1d0a82693760bc3e1b6144d2190153f24
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249778"
---
# <a name="web-hosting-a-queued-application"></a>Размещение веб-узлов в приложении, использующем очереди

Служба активации Windows (WAS) управляет активацией и временем жизни рабочих процессов, которые содержат приложения, размещенные в службах Windows Communication Foundation (WCF). Модель процесса WAS обобщает модель процесса IIS 6.0 для HTTP-сервера, удаляя зависимость от HTTP. Это позволяет службам WCF использовать протоколы HTTP и отличные от HTTP, такие как net. MSMQ и MSMQ. formatname, в среде размещения, которая поддерживает активацию на основе сообщений и предлагает возможность размещения большого количества приложений на определенном компьютере.  
  
 WAS содержит службу активации очереди сообщений (MSMQ), которая активирует приложение с использованием очередей, где одно или более сообщений ставятся в очередь сообщений MSMQ, одну из очередей, используемых приложением. Служба активации MSMQ является службой NT, запускающейся по умолчанию автоматически.  
  
 Дополнительные сведения о WAS и его преимуществах см. [в разделе Размещение в службе активации Windows](hosting-in-windows-process-activation-service.md). Дополнительные сведения об MSMQ см. в статье [Общие сведения о очередях](queues-overview.md).
  
## <a name="queue-addressing-in-was"></a>Адресация очереди в WAS  

 Приложения WAS имеют адреса в виде универсальных кодов ресурсов (URI). Адреса приложений состоят из двух частей: основной префикс URI и относительный адрес, специальный для каждого приложения (путь). Вместе эти две части показывают внешний адрес приложения. Базовый префикс URI создается на основе привязки сайта и используется для всех приложений сайта, например "net. msmq://localhost", "MSMQ. formatname://localhost" или "net. TCP://localhost". После этого адреса приложений создаются путем создания фрагментов пути для конкретного приложения (например, "/Аппликатиононе") и добавления их к базовому префиксу URI для получения полного URI приложения, например "net. msmq://ЛОКАЛХОСТ/аппликатиононе".  
  
 Служба активации MSMQ использует URI приложения для проверки соответствия с очередью, сообщения которой служба активации MSMQ должна контролировать. При запуске служба активации MSMQ перечисляет все общие и частные очереди на компьютере, с которого она их получает согласно настройкам конфигурации, и отслеживает наличие в них сообщений. Служба активации MSMQ обновляет список очередей для проверки каждые 10 минут. Если в очереди найдено сообщение, служба активации проверяет соответствие имени очереди и самого длинного согласующегося URI для привязки net.msmq и активирует приложение.  
  
> [!NOTE]
> Активируемое приложение должно соответствовать (иметь самый длинный согласующийся код) префиксу имени очереди.  
  
 Например, имя очереди: msmqWebHost/orderProcessing/service.svc. Если приложение 1 имеет виртуальный каталог /msmqWebHost/orderProcessing с файлом service.svc в нем, а приложение 2 имеет виртуальный каталог /msmqWebHost с orderProcessing.svc в нем, активируется приложение 1. Если приложение 1 удалено, активируется приложение 2.  
  
> [!NOTE]
> При создании очереди ни одно сообщение из всех отправленных в очередь не активирует приложение до тех пор, пока служба активации MSMQ не обновит список очередей, что произойдет максимум через 10 минут после создания очереди. При повторном запуске службы активации список очередей также обновляется.  
  
### <a name="the-effect-of-private-and-public-queues-on-addressing"></a>Влияние общих и частных очередей на адресацию  

 Служба активизации MSMQ не делает различий между мониторингом частных и общих очередей. В принципе, общая и частная очереди не могут иметь одинаковых имен. Но, если это так, приложение, размещенное на веб-сервере, может быть активировано чтением сообщения из любой из очередей.  
  
### <a name="queue-configuration-for-activation"></a>Конфигурация очереди для активации  

 Служба активации MSMQ работает как NETWORK SERVICE. Это служба, осуществляющая мониторинг очередей для активации приложений. Для того, чтобы служба активировала приложения из очереди, очередь должна быть доступна NETWORK SERVICE для просмотра сообщений в списке управления доступом (ACL).  
  
### <a name="poison-messaging"></a>Подозрительные сообщения  

 Обработка подозрительных сообщений в WCF обрабатывается каналом, который не только обнаруживает, что сообщение является подозрительным, но и выбирает расстановку на основе пользовательской конфигурации. В результате, в очереди находится одно сообщение. Приложение, размещающееся на веб-сервере, прерывает последующие попытки, и сообщение перемещается в очередь повторного выполнения. В момент истечения времени цикла повторного выполнения сообщение перемещается из очереди повторного выполнения в главную очередь для повторной попытки. Однако, чтобы это произошло, канал в очереди должен быть активным. Если цикл в приложении задает WAS, сообщение остается в очереди повторного выполнения до тех пор, пока в основную очередь не поступит другое сообщение, активирующее приложение в очереди. Обходным путем в этом случае является перемещение сообщения вручную из очереди повторного выполнения обратно в основную очередь для повторной активации приложения.  
  
### <a name="subqueue-and-system-queue-caveat"></a>Вложенная очередь и недостаток системных очередей  

 Приложение, размещенное WAS не может быть активировано посредством сообщений из системных очередей, таких как общесистемная очередь недоставленных сообщений или вложенных очередей, таких как вложенные очереди подозрительных сообщений. Это ограничение для данной версии продукта.  
  
## <a name="see-also"></a>См. также

- [Обработка подозрительных сообщений](poison-message-handling.md)
- [Конечные точки служб и адресация очереди](service-endpoints-and-queue-addressing.md)
