---
title: bitsadmin
description: Windows-Befehls Thema für bitadmin, ein Befehlszeilen Tool, das zum Erstellen, herunterladen oder Hochladen von Aufträgen und zum Überwachen des Fortschritts verwendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4853036e-1df8-45ad-8be6-cfb097b8dd27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae6536b5c149f54bbfd37a5e0e814ffaa09a6bae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848743"
---
# <a name="bitsadmin"></a>bitsadmin

> **Gilt für**: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10

Bitadmin ist ein Befehlszeilen Tool, das Sie zum Erstellen von Aufträgen zum Herunterladen oder hochladen und zum Überwachen des Fortschritts verwenden können. Das bitadmin-Tool verwendet Schalter, um die auszuführende Arbeit zu identifizieren.  Sie können `bitsadmin /?` oder `bitsadmin /HELP` abrufen, um eine Liste der Switches abzurufen.

Die meisten Switches benötigen einen \<Job-\> Parameter, den Sie auf den anzeigen amen des Auftrags oder die GUID festlegen. Beachten Sie, dass der Anzeige Name eines Auftrags möglicherweise nicht eindeutig ist. Die Schalter **/Create** und **/List** geben die GUID eines Auftrags zurück.

Standardmäßig können Sie auf Informationen zu ihren eigenen Aufträgen zugreifen. Für den Zugriff auf Informationen für die Aufträge eines anderen Benutzers müssen Sie über Administratorrechte verfügen. Wenn der Auftrag mit erhöhten Rechten erstellt wurde, müssen Sie bizadmin über ein Fenster mit erhöhten Rechten ausführen. Andernfalls haben Sie schreibgeschützten Zugriff auf den Auftrag.

Viele der Schalter entsprechen den Methoden in den [Bits-Schnittstellen](/windows/desktop/bits/bits-interfaces). Weitere Informationen, die für die Verwendung eines Schalters relevant sein können, finden Sie in der entsprechenden-Methode.

Verwenden Sie die folgenden Schalter, um einen Auftrag zu erstellen, die Eigenschaften eines Auftrags festzulegen und abzurufen und den Status eines Auftrags zu überwachen. Beispiele, die zeigen, wie einige dieser Switches zum Ausführen von Aufgaben verwendet werden, finden Sie unter [bizadmin examples](bitsadmin-examples.md).

## <a name="switches"></a>Switches

[bitsadmin addfile](bitsadmin-addfile.md)  
[bitsadmin addfileset](bitsadmin-addfileset.md)  
[bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)  
[bitsadmin cache](bitsadmin-cache.md)  
[bitsadmin cancel](bitsadmin-cancel.md)  
[bitsadmin complete](bitsadmin-complete.md)  
[bitsadmin create](bitsadmin-create.md)  
[bitsadmin getaclflags](bitsadmin-getaclflags.md)  
[bitsadmin getbytestotal](bitsadmin-getbytestotal.md)  
[bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)  
[bitsadmin getclientcertificate](bitsadmin-getclientcertificate.md)  
[bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)  
[bitsadmin getcreationtime](bitsadmin-getcreationtime.md)  
[bitsadmin getcustomheaders](bitsadmin-getcustomheaders.md)  
[bitsadmin getdescription](bitsadmin-getdescription.md)  
[bitsadmin getdisplayname](bitsadmin-getdisplayname.md)  
[bitsadmin geterror](bitsadmin-geterror.md)  
[bitsadmin geterrorcount](bitsadmin-geterrorcount.md)  
[bitsadmin getfilestotal](bitsadmin-getfilestotal.md)  
[bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)  
[bitsadmin gethelpertokenflags](bitsadmin-gethelpertokenflags.md)  
[bitsadmin gethelpertokensid](bitsadmin-gethelpertokensid.md)  
[bizadmin gethttpmethod](bitsadmin-gethttpmethod.md)
[bizadmin getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)  
[bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)  
[bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)  
[bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)  
[bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)  
[bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)  
[bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)  
[bitsadmin getowner](bitsadmin-getowner.md)  
[bitsadmin getpeercachingflags](bitsadmin-getpeercachingflags.md)  
[bitsadmin getpriority](bitsadmin-getpriority.md)  
[bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)  
[bitsadmin getproxylist](bitsadmin-getproxylist.md)  
[bitsadmin getproxyusage](bitsadmin-getproxyusage.md)  
[bitsadmin getreplydata](bitsadmin-getreplydata.md)  
[bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)  
[bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)  
[bitsadmin getsecurityflags](bitsadmin-getsecurityflags.md)  
[bitsadmin getstate](bitsadmin-getstate.md)  
[bitsadmin gettemporaryname](bitsadmin-gettemporaryname.md)  
[bitsadmin gettype](bitsadmin-gettype.md)  
[bitsadmin getvalidationstate](bitsadmin-getvalidationstate.md)  
[bitsadmin help](bitsadmin-help.md)  
[bitsadmin info](bitsadmin-info.md)  
[bitsadmin list](bitsadmin-list.md)  
[bitsadmin listfiles](bitsadmin-listfiles.md)  
[bipadmin](bitsadmin-makecustomheaderswriteonly.md) -
[bipadmin-Monitor](bitsadmin-monitor.md)  
[bitsadmin nowrap](bitsadmin-nowrap.md)  
[bitsadmin peercaching](bitsadmin-peercaching.md)  
[bitsadmin peers](bitsadmin-peers.md)  
[bitsadmin rawreturn](bitsadmin-rawreturn.md)  
[bitsadmin removeclientcertificate](bitsadmin-removeclientcertificate.md)  
[bitsadmin removecredentials](bitsadmin-removecredentials.md)  
[bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)  
[bitsadmin reset](bitsadmin-reset.md)  
[bitsadmin resume](bitsadmin-resume.md)  
[bitsadmin setaclflag](bitsadmin-setaclflag.md)  
[bitsadmin setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)  
[bitsadmin setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)  
[bitsadmin setcredentials](bitsadmin-setcredentials.md)  
[bitsadmin setcustomheaders](bitsadmin-setcustomheaders.md)  
[bitsadmin setdescription](bitsadmin-setdescription.md)  
[bitsadmin setdisplayname](bitsadmin-setdisplayname.md)  
[bitsadmin sethelpertoken](bitsadmin-sethelpertoken.md)  
[bitsadmin sethelpertokenflags](bitsadmin-sethelpertokenflags.md)  
[bizadmin sethttpmethod](bitsadmin-sethttpmethod.md)
[bitadmin setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)  
[bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)  
[bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)  
[bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)  
[bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)  
[bitsadmin setpeercachingflags](bitsadmin-setpeercachingflags.md)  
[bitsadmin setpriority](bitsadmin-setpriority.md)  
[bitsadmin setproxysettings](bitsadmin-setproxysettings.md)  
[bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)  
[bitsadmin setsecurityflags](bitsadmin-setsecurityflags.md)  
[bitsadmin setvalidationstate](bitsadmin-setvalidationstate.md)  
[bitsadmin suspend](bitsadmin-suspend.md)  
[bitsadmin takeownership](bitsadmin-takeownership.md)  
[bitsadmin transfer](bitsadmin-transfer.md)  
[bitsadmin util](bitsadmin-util.md)  
[bitsadmin wrap](bitsadmin-wrap.md)  
