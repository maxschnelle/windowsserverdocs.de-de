---
title: bitsadmin
description: Referenz Thema für den bizadmin-Befehl, bei dem es sich um ein Befehlszeilenprogramm handelt, das zum Erstellen, herunterladen oder Hochladen von Aufträgen und zum Überwachen des Status verwendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4853036e-1df8-45ad-8be6-cfb097b8dd27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94a829ce21c4571188fb5ffeb9a0a1d991637d07
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82710048"
---
# <a name="bitsadmin"></a>bitsadmin

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10

Bitadmin ist ein Befehlszeilen Tool, mit dem Aufträge erstellt, heruntergeladen oder hochgeladen und der Fortschritt überwacht werden kann. Das bitadmin-Tool verwendet Schalter, um die auszuführende Arbeit zu identifizieren. Sie können oder `bitsadmin /?` `bitsadmin /help` abrufen, um eine Liste von Switches abzurufen.

Die meisten Schalter benötigen `<job>` einen Parameter, den Sie auf den anzeigen amen des Auftrags oder die GUID festlegen. Der Anzeige Name eines Auftrags muss nicht eindeutig sein. Die Schalter **/Create** und **/List** geben die GUID eines Auftrags zurück.

Standardmäßig können Sie auf Informationen zu ihren eigenen Aufträgen zugreifen. Für den Zugriff auf Informationen für die Aufträge eines anderen Benutzers müssen Sie über Administratorrechte verfügen. Wenn der Auftrag mit erhöhten Rechten erstellt wurde, müssen Sie **bizadmin** über ein Fenster mit erhöhten Rechten ausführen. Andernfalls haben Sie schreibgeschützten Zugriff auf den Auftrag.

Viele der Schalter entsprechen den Methoden in den [Bits-Schnittstellen](https://docs.microsoft.com/windows/win32/bits/bits-interfaces). Weitere Informationen, die für die Verwendung eines Schalters relevant sein können, finden Sie in der entsprechenden-Methode.

Verwenden Sie die folgenden Schalter, um einen Auftrag zu erstellen, die Eigenschaften eines Auftrags festzulegen und abzurufen und den Status eines Auftrags zu überwachen. Beispiele, die zeigen, wie einige dieser Switches zum Ausführen von Aufgaben verwendet werden, finden Sie unter [bizadmin examples](bitsadmin-examples.md).

## <a name="available-switches"></a>Verfügbare Switches

- [biout admin/AddFile](bitsadmin-addfile.md)
- [biout admin/ADDFILESET](bitsadmin-addfileset.md)
- [biout admin/ADDFILEWITHRANGES](bitsadmin-addfilewithranges.md)
- [biout admin/Cache](bitsadmin-cache.md)
- [biout admin/Cache/DELETE](bitsadmin-cache-and-delete.md)
- [biout admin/Cache/DeleteUrl](bitsadmin-cache-and-deleteurl.md)
- [biout admin/Cache/getexpirationtime](bitsadmin-cache-and-getexpirationtime.md)
- [biout admin/Cache/getlimit](bitsadmin-cache-and-getlimit.md)
- [biout admin/Cache/Help](bitsadmin-cache-and-help.md)
- [biout admin/Cache/Info](bitsadmin-cache-and-info.md)
- [biout admin/Cache/List](bitsadmin-cache-and-list.md)
- [biout admin/Cache/setexpirationtime](bitsadmin-cache-and-setexpirationtime.md)
- [biout admin/Cache/setLimit](bitsadmin-cache-and-setlimit.md)
- [biout admin/Cache/Clear](bitsadmin-cache-clear.md)
- [biout admin/Cancel](bitsadmin-cancel.md)
- [biout admin/Complete](bitsadmin-complete.md)
- [biout admin/Create](bitsadmin-create.md)
- [biout admin/examples](bitsadmin-examples.md)
- [biout admin/getaclflags](bitsadmin-getaclflags.md)
- [biout admin/GetBytesTotal](bitsadmin-getbytestotal.md)
- [biout admin/getbytestransferred](bitsadmin-getbytestransferred.md)
- [biout admin/getclientcertificate](bitsadmin-getclientcertificate.md)
- [biout admin/getcompletiontime](bitsadmin-getcompletiontime.md)
- [biout admin/GetCreationTime](bitsadmin-getcreationtime.md)
- [biout admin/getcustomheaders](bitsadmin-getcustomheaders.md)
- [biout admin/GetDescription](bitsadmin-getdescription.md)
- [biout admin/GetDisplayName](bitsadmin-getdisplayname.md)
- [biout admin/getError](bitsadmin-geterror.md)
- [biout admin/GetErrorCount](bitsadmin-geterrorcount.md)
- [biout admin/getfilestotal](bitsadmin-getfilestotal.md)
- [biout admin/getfilestransferred](bitsadmin-getfilestransferred.md)
- [biout admin/gethelpertokenflags](bitsadmin-gethelpertokenflags.md)
- [biout admin/gethelpertokensid](bitsadmin-gethelpertokensid.md)
- [biout admin/gethttpmethod](bitsadmin-gethttpmethod.md)
- [biout admin/getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)
- [biout admin/getminretrydelay](bitsadmin-getminretrydelay.md)
- [biout admin/getmodificationtime](bitsadmin-getmodificationtime.md)
- [biout admin/getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
- [biout admin/getnotifycmdline](bitsadmin-getnotifycmdline.md)
- [biout admin/getnotifyflags](bitsadmin-getnotifyflags.md)
- [biout admin/getnotifyinterface](bitsadmin-getnotifyinterface.md)
- [biout admin/GetOwner](bitsadmin-getowner.md)
- [biout admin/getpeercachingflags](bitsadmin-getpeercachingflags.md)
- [biout admin/GetPriority](bitsadmin-getpriority.md)
- [biout admin/getproxybypasslist](bitsadmin-getproxybypasslist.md)
- [biout admin/getproxylist](bitsadmin-getproxylist.md)
- [biout admin/getproxyusage](bitsadmin-getproxyusage.md)
- [biout admin/getreplydata](bitsadmin-getreplydata.md)
- [biout admin/getreplyfilename](bitsadmin-getreplyfilename.md)
- [biout admin/getreplyprogress](bitsadmin-getreplyprogress.md)
- [biout admin/getsecurityflags](bitsadmin-getsecurityflags.md)
- [biout admin/GetState](bitsadmin-getstate.md)
- [biout admin/gettemporaryname](bitsadmin-gettemporaryname.md)
- [biout admin/GetType](bitsadmin-gettype.md)
- [biout admin/getvalidationstate](bitsadmin-getvalidationstate.md)
- [biout admin/Help](bitsadmin-help.md)
- [biout admin/Info](bitsadmin-info.md)
- [biout admin/List](bitsadmin-list.md)
- [biout admin/listFiles](bitsadmin-listfiles.md)
- [biout admin/makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
- [biout admin/Monitor](bitsadmin-monitor.md)
- [biout admin/NoWrap](bitsadmin-nowrap.md)
- [biout admin/Peercaching](bitsadmin-peercaching.md)
- [biout admin/Peercaching/getconfigurationflags](bitsadmin-peercaching-and-getconfigurationflags.md)
- [biout admin/Peercaching/Help](bitsadmin-peercaching-and-help.md)
- [biout admin/Peercaching/setconfigurationflags](bitsadmin-peercaching-and-setconfigurationflags.md)
- [biout admin/Peers](bitsadmin-peers.md)
- [biout admin/Peers/Clear](bitsadmin-peers-and-clear.md)
- [biout admin/Peers/Discover](bitsadmin-peers-and-discover.md)
- [biout admin/Peers/Help](bitsadmin-peers-and-help.md)
- [biout admin/Peers/List](bitsadmin-peers-and-list.md)
- [biout admin/rawreturn](bitsadmin-rawreturn.md)
- [biout admin/removeclientcertificate](bitsadmin-removeclientcertificate.md)
- [biout admin/removecredentials](bitsadmin-removecredentials.md)
- [biout admin/REPLACEREMOTEPREFIX](bitsadmin-replaceremoteprefix.md)
- [biout Admin/Reset](bitsadmin-reset.md)
- [biout admin/Resume](bitsadmin-resume.md)
- [biout admin/setaclflag](bitsadmin-setaclflag.md)
- [biout admin/setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)
- [biout admin/setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)
- [biout admin/SetCredentials](bitsadmin-setcredentials.md)
- [biout admin/setcustomheaders](bitsadmin-setcustomheaders.md)
- [biout admin/setDescription](bitsadmin-setdescription.md)
- [biout admin/setdisplayname](bitsadmin-setdisplayname.md)
- [biout admin/sethelpertoken](bitsadmin-sethelpertoken.md)
- [biout admin/sethelpertokenflags](bitsadmin-sethelpertokenflags.md)
- [biout admin/sethttpmethod](bitsadmin-sethttpmethod.md)
- [biout admin/setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)
- [biout admin/setminretrydelay](bitsadmin-setminretrydelay.md)
- [biout admin/setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
- [biout admin/setnotifycmdline](bitsadmin-setnotifycmdline.md)
- [biout admin/setnotifyflags](bitsadmin-setnotifyflags.md)
- [biout admin/setpeercachingflags](bitsadmin-setpeercachingflags.md)
- [biout admin/SetPriority](bitsadmin-setpriority.md)
- [biout admin/setproxysettings](bitsadmin-setproxysettings.md)
- [biout admin/setreplyfilename](bitsadmin-setreplyfilename.md)
- [biout admin/setsecurityflags](bitsadmin-setsecurityflags.md)
- [biout admin/setvalidationstate](bitsadmin-setvalidationstate.md)
- [biout admin/Suspend](bitsadmin-suspend.md)
- [biout admin/TakeOwnership](bitsadmin-takeownership.md)
- [biout admin/Transfer](bitsadmin-transfer.md)
- [biout admin/util](bitsadmin-util.md)
- [biout admin/util/enableanalyticchannel](bitsadmin-util-and-enableanalyticchannel.md)
- [biout admin/util/GETIEPROXY](bitsadmin-util-and-getieproxy.md)
- [biout admin/util/Help](bitsadmin-util-and-help.md)
- [biout admin/util/RepairService](bitsadmin-util-and-repairservice.md)
- [biout admin/util/SETIEPROXY](bitsadmin-util-and-setieproxy.md)
- [biout admin/util/Version](bitsadmin-util-and-version.md)
- [biout admin/Wrap](bitsadmin-wrap.md)
