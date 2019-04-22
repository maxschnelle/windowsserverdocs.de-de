---
title: bitsadmin
description: Windows-Befehle Thema **Bitsadmin** -Bitsadmin ist ein Befehlszeilentool, das Sie verwenden können, erstellen, herunterladen oder Hochladen Aufträge und ihren Fortschritt überwachen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4853036e-1df8-45ad-8be6-cfb097b8dd27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da0f05ec716cffb7d7532ebac50a091729a6bb18
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821071"
---
# <a name="bitsadmin"></a>bitsadmin

> **Gilt für**: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows 10

Bitsadmin ist ein Befehlszeilentool, mit denen Sie Download erstellen oder Uploadaufträge und ihren Status überwachen. Das Tool Bitsadmin verwendet Switches zum Identifizieren der auszuführenden Vorgänge an.  Rufen Sie `bitsadmin /?` oder `bitsadmin /HELP` um eine Liste der Befehlszeilenoptionen zu erhalten.

Die meisten Switches erfordern eine \<Auftrag\> Parameter, der Sie der Auftrags Display-Name oder GUID festgelegt. Beachten Sie, dass Anzeigename des Auftrags möglicherweise nicht eindeutig ist. Die **/ create** und **/list** Switches Zurückgeben eines Auftrags-GUID.

Standardmäßig können Sie Informationen zu Ihrer eigenen Aufträge zugreifen. Um Informationen für Aufträge des Benutzers zuzugreifen, müssen Sie über Administratorrechte verfügen. Wenn der Auftrag in einem Zustand mit erhöhten Rechten erstellt wurde, müssen Sie über ein Fenster mit erhöhten Rechten Bitsadmin ausführen; Andernfalls müssen Sie nur-Lese Zugriff auf den Auftrag.

Viele der Switches entsprechen den Methoden in der [BITS Schnittstellen](/windows/desktop/bits/bits-interfaces). Weitere Informationen, die einen Switch relevant sein könnten, finden Sie die entsprechende Methode.

Verwenden Sie die folgenden Schalter zum Erstellen eines Auftrags, festgelegt und die Eigenschaften eines Auftrags abrufen, und Überwachen des Status eines Auftrags. Beispiele, die zeigen, wie Sie einige dieser Optionen verwenden, um Aufgaben auszuführen, finden Sie unter [Bitsadmin Beispiele](bitsadmin-examples.md).

## <a name="switches"></a>Switches

[Bitsadmin addfile](bitsadmin-addfile.md)  
[Bitsadmin addfileset](bitsadmin-addfileset.md)  
[Bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)  
[bitsadmin cache](bitsadmin-cache.md)  
[Bitsadmin "Abbrechen"](bitsadmin-cancel.md)  
[Bitsadmin abgeschlossen](bitsadmin-complete.md)  
[Bitsadmin erstellen](bitsadmin-create.md)  
[Bitsadmin getaclflags](bitsadmin-getaclflags.md)  
[Bitsadmin getbytestotal](bitsadmin-getbytestotal.md)  
[Bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)  
[Bitsadmin getclientcertificate](bitsadmin-getclientcertificate.md)  
[Bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)  
[Bitsadmin getcreationtime](bitsadmin-getcreationtime.md)  
[bitsadmin getcustomheaders](bitsadmin-getcustomheaders.md)  
[bitsadmin getdescription](bitsadmin-getdescription.md)  
[bitsadmin getdisplayname](bitsadmin-getdisplayname.md)  
[bitsadmin geterror](bitsadmin-geterror.md)  
[Bitsadmin geterrorcount](bitsadmin-geterrorcount.md)  
[bitsadmin getfilestotal](bitsadmin-getfilestotal.md)  
[Bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)  
[Bitsadmin gethelpertokenflags](bitsadmin-gethelpertokenflags.md)  
[Bitsadmin gethelpertokensid](bitsadmin-gethelpertokensid.md)  
[Bitsadmin Gethttpmethod](bitsadmin-gethttpmethod.md)
[Bitsadmin Getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)  
[Bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)  
[Bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)  
[bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)  
[bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)  
[Bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)  
[Bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)  
[Bitsadmin "GetOwner"](bitsadmin-getowner.md)  
[bitsadmin getpeercachingflags](bitsadmin-getpeercachingflags.md)  
[bitsadmin getpriority](bitsadmin-getpriority.md)  
[bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)  
[bitsadmin getproxylist](bitsadmin-getproxylist.md)  
[Bitsadmin getproxyusage](bitsadmin-getproxyusage.md)  
[bitsadmin getreplydata](bitsadmin-getreplydata.md)  
[bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)  
[bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)  
[Bitsadmin getsecurityflags](bitsadmin-getsecurityflags.md)  
[Bitsadmin getstate](bitsadmin-getstate.md)  
[bitsadmin gettemporaryname](bitsadmin-gettemporaryname.md)  
[bitsadmin gettype](bitsadmin-gettype.md)  
[bitsadmin getvalidationstate](bitsadmin-getvalidationstate.md)  
[bitsadmin help](bitsadmin-help.md)  
[bitsadmin info](bitsadmin-info.md)  
[bitsadmin list](bitsadmin-list.md)  
[bitsadmin listfiles](bitsadmin-listfiles.md)  
[Bitsadmin Makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
[Bitsadmin überwachen](bitsadmin-monitor.md)  
[bitsadmin nowrap](bitsadmin-nowrap.md)  
[Bitsadmin-peercaching](bitsadmin-peercaching.md)  
[Bitsadmin peers](bitsadmin-peers.md)  
[bitsadmin rawreturn](bitsadmin-rawreturn.md)  
[Bitsadmin removeclientcertificate](bitsadmin-removeclientcertificate.md)  
[Bitsadmin removecredentials](bitsadmin-removecredentials.md)  
[Bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)  
[bitsadmin reset](bitsadmin-reset.md)  
[Bitsadmin fortsetzen](bitsadmin-resume.md)  
[Bitsadmin setaclflag](bitsadmin-setaclflag.md)  
[Bitsadmin setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)  
[Bitsadmin setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)  
[Bitsadmin setcredentials](bitsadmin-setcredentials.md)  
[Bitsadmin setcustomheaders](bitsadmin-setcustomheaders.md)  
[bitsadmin setdescription](bitsadmin-setdescription.md)  
[bitsadmin setdisplayname](bitsadmin-setdisplayname.md)  
[Bitsadmin sethelpertoken](bitsadmin-sethelpertoken.md)  
[Bitsadmin sethelpertokenflags](bitsadmin-sethelpertokenflags.md)  
[Bitsadmin Sethttpmethod](bitsadmin-sethttpmethod.md)
[Bitsadmin Setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)  
[Bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)  
[bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)  
[bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)  
[Bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)  
[bitsadmin setpeercachingflags](bitsadmin-setpeercachingflags.md)  
[Bitsadmin setpriority](bitsadmin-setpriority.md)  
[bitsadmin setproxysettings](bitsadmin-setproxysettings.md)  
[bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)  
[Bitsadmin setsecurityflags](bitsadmin-setsecurityflags.md)  
[bitsadmin setvalidationstate](bitsadmin-setvalidationstate.md)  
[Bitsadmin anhalten](bitsadmin-suspend.md)  
[Bitsadmin takeownership](bitsadmin-takeownership.md)  
[Bitsadmin Übertragung](bitsadmin-transfer.md)  
[bitsadmin util](bitsadmin-util.md)  
[bitsadmin wrap](bitsadmin-wrap.md)  
