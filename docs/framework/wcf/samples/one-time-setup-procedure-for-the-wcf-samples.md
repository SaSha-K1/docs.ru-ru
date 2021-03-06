---
title: Процедура однократной настройки образцов Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: a5848ffd-3eb5-432d-812e-bd948ccb6bca
ms.openlocfilehash: bf25ea4734bad007fa3ac19df0664932d981519c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "90548121"
---
# <a name="one-time-setup-procedure-for-the-windows-communication-foundation-samples"></a>Процедура однократной настройки образцов Windows Communication Foundation

Большинство примеров Windows Communication Foundation (WCF) размещаются в службы IIS (IIS) и запускаются из общего виртуального каталога. Эта одноразовая процедура установки создает папку на диске; Он также добавляет виртуальный каталог в IIS с именем **servicemodelsamples**.

Виртуальный каталог **servicemodelsamples** используется для создания и запуска всех примеров, использующих размещенную в IIS службу. Это единственный виртуальный каталог, необходимый для выполнения примеров. При построении образца будет заменена любая служба, развернутая ранее в этом виртуальном каталоге. Развернут и доступен в данном виртуальном каталоге будет только последний построенный образец.

> [!NOTE]
> Необходимо выполнить все команды от имени учетной записи локального администратора. Если вы используете Windows 7, Windows Vista или Windows Server 2008 R2, необходимо также запустить командную строку с повышенными привилегиями. Для этого щелкните правой кнопкой мыши значок командной строки и выберите команду **Запуск от имени администратора**. Все команды в данном разделе должны выполняться в командной строке с соответствующим образом заданными параметрами пути.  Проще всего добиться этого, используя командную строку Visual Studio. Чтобы открыть этот запрос, нажмите **кнопку Пуск**, **выберите все программы**, прокрутите вниз до пункта **Visual Studio 2010**, выберите **инструменты Visual Studio**, щелкните правой кнопкой мыши **командную строку Visual Studio (2010)** и выберите команду **Запуск от имени администратора**. Если установлен один из выпусков Visual Studio Express, эта командная строка недоступна. В этом случае добавьте в системный путь строку «C:\Windows\Microsoft.Net\Framework\v4.0».

### <a name="one-time-setup-procedure-for-wcf-samples"></a>Однократно настраиваемая процедура для образцов WCF

1. Убедитесь, что ASP.NET настроен. Дополнительные сведения о настройке ASP.NET см. в разделе [инструкции по размещению службы](internet-information-service-hosting-instructions.md)IIS.

2. Убедитесь, что установлен .NET Framework 4. Выполните поиск в следующем каталоге версии 4.0 (или более поздней): **\виндовс\микрософт.нет\фрамеворк**

3. Убедитесь, что установлен Visual Studio 2012 или более поздней версии, либо установлена операционная система Windows Server 2008 SP2 или более поздней версии.

4. Выполните указанные ниже команды. Дополнительные сведения о том, почему должны выполняться эти команды, см. в разделе [сбой размещенной службы IIS](/previous-versions/dotnet/netframework-3.5/ms752252(v=vs.90)).

    > [!WARNING]
    > Если IIS был переустановлен, необходимо вновь выполнить следующие команды.

    ```console
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\aspnet_regiis" –i –enable
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\ServiceModelReg.exe" -r
    ```

    > [!WARNING]
    > При выполнении команды `aspnet_regiis –i –enable` пул приложений по умолчанию будет выполняться с помощью .NET Framework 4, что может привести к проблемам несовместимости других приложений на том же компьютере.

5. Следуйте [инструкциям брандмауэра](firewall-instructions.md) , чтобы включить порты, используемые образцами.

6. Проверьте наличие следующего каталога по умолчанию: \<InstallDrive> :**\ WF_WCF_Samples**. Если образцы были предварительно установлены, этот каталог будет выбран по умолчанию.

7. Если образцы не установлены, установите их из [примеров Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459).

8. После установки образцов перейдите на страницу: \<InstallDrive> :**\ WF_WCF_Samples \вкф\сетуп \\ **

9. Запустите пакетный файл **Setupvroot.bat** . Выполняются следующие шаги.

    - В службах IIS создается виртуальный каталог с именем ServiceModelSamples.

    - Создаются новые каталоги диска с именами «%SystemDrive%\Inetpub\wwwroot\ServiceModelSamples» и «%SystemDrive%\Inetpub\wwwroot\ServiceModelSamples\bin».

    Если вы предпочитаете настроить эти каталоги вручную, см. [инструкции по настройке виртуального каталога](virtual-directory-setup-instructions.md). Чтобы отменить все изменения, произведенные на данном шаге, запустите файл cleanupvroot.bat по окончании использования образцов.

    > [!NOTE]
    > Если только не запущен файл cleanupvroot.bat, эта процедура выполняется только один раз для каждого компьютера.

10. Предоставьте разрешение на изменение папки «%SystemDrive%\inetpub\wwwroot» для учетной записи, от имени которой выполняется построение образцов, и для пользователя сетевой службы. При построении некоторых образцов, размещенных на веб-сервере, может быть выполнена попытка копирования компилированных двоичных файлов в указанное ранее расположение, и если соответствующие разрешения не заданы, построение прервется. Кроме того, можно оставить разрешения по мере их возникновения и запустить командную строку SDK или командную строку Visual Studio (2012) в качестве администратора или построить образцы в Visual Studio 2012, а также запустить от имени администратора.

    > [!NOTE]
    > Если этот шаг не выполнен, построение всех образцов, размещенных в службах IIS, завершится с ошибкой. Убедитесь, что разрешения заданы правильно, или запустите и командную строку пакета SDK, и командную строку Visual Studio (2012) от имени администратора.

11. Создайте на компьютере каталог C:\logs. Некоторые образцы могут ожидать его наличия. Убедитесь, что соответствующая учетная запись имеет разрешение на запись в этот каталог. Для Windows 7, Windows Vista и Windows Server 2008 R2 эта учетная запись является **сетевой службой**. Для Windows Server 2008 учетная запись — NT Authority\Network Service. Для Windows XP и Windows Server 2003 учетная запись — ASPNET.

12. Запустите файл Setupcerttool.bat. Этот файл находится в  \<InstallPath> папке \ WF_WCF_Samples \вкф\сетуп\.  Этот скрипт выполнит следующие задачи.

    - Построит средство FindPrivateKey.

    - Создаст каталог с именем %ProgramFiles%\ServiceModelSampleTools.

    - Скопирует в этот каталог новое средство FindPrivateKey.

    Данное средство необходимо для образцов, в которых используются сертификаты и которые размещены в службах IIS.

    > [!NOTE]
    > В целях безопасности по завершении работы с образцами не забудьте удалить определение виртуального каталога и разрешения, предоставленные на шагах установки, запустив пакетный файл Cleanupvroot.bat.

13. Резидентным образцам (не размещенным в службах IIS) требуется разрешение на регистрацию HTTP-адресов на компьютере для прослушивания. Разрешение на резервирование пространства имен HTTP поступает от учетной записи пользователя, используемой для выполнения образца. По умолчанию учетные записи администратора имеют разрешение на регистрацию любых HTTP-адресов. Неадминистративным учетным записям должно быть предоставлено разрешение на использование пространства имен HTTP, применяемых в образцах кода. Дополнительные сведения о настройке резервирования пространств имен см. в разделе [Настройка протоколов HTTP и HTTPS](../feature-details/configuring-http-and-https.md).

14. Для некоторых примеров требуется очередь сообщений. Инструкции по установке см. в разделе [Установка очереди сообщений (MSMQ)](installing-message-queuing-msmq.md) .

    > [!NOTE]
    > Перед запуском всех образцов, использующих очереди сообщений, необходимо убедиться, что запущена служба очередей сообщений.

15. Для некоторых образцов требуются сертификаты. См. [инструкции по установке сертификата сервера службы IIS (IIS)](iis-server-certificate-installation-instructions.md).
