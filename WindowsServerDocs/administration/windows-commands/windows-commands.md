---
title: Windows-Befehle
description: Verweis
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: jasongerend
ms.author: jgerend
manager: dongill
ms.date: 06/09/2020
ms.prod: windows-server
ms.openlocfilehash: 66de80652f764840af70e88dfd39df2398ae495c
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721114"
---
# <a name="windows-commands"></a>Windows-Befehle

Für alle unterstützten Versionen von Windows (Server und Client) ist eine Reihe von Win32-Konsolen Befehlen integriert.

In diesem Dokumentations Satz werden die Windows-Befehle beschrieben, die Sie zum Automatisieren von Aufgaben mithilfe von Skripts oder Skript Erstellungs Tools verwenden können.

Wenn Sie Informationen zu einem bestimmten Befehl suchen möchten, klicken Sie im folgenden a-Z-Menü auf den Buchstaben, mit dem der Befehl beginnt, und klicken Sie dann auf den Befehlsnamen.

[A](#a)  |
 [B](#b)  |
 [C](#c)  |
 [D](#d)  |
 [E](#e)  |
 [F](#f)  |
 [G](#g)  |
 [H](#h)  |
 [I](#i)  |
 [J](#j)  |
 [K](#k)  |
 [L](#l)  |
 [M](#m)  |
 [N](#n)  |
 [O](#o)  |
 [P](#p)  |
 [F](#q)  |
 [R](#r)  |
 [S](#s)  |
 [T](#t)  |
 [U](#u)  |
 [V](#v)  |
 [W](#w)  |
 [X](#x) | J | Z

## <a name="prerequisites"></a>Voraussetzungen

Die in diesem Thema enthaltenen Informationen gelten für:

- Windows Server 2019
- Windows Server (Halbjährlicher Kanal)
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- WindowsServer 2008
- Windows 10
- Windows 8.1

### <a name="command-shell-overview"></a>Übersicht über Befehlsshell

Die Befehlsshell war die erste Shell, die in Windows integriert wurde, um Routineaufgaben wie die Verwaltung von Benutzerkonten oder nächtliche Sicherungen mit Batch Dateien (BAT-Dateien) zu automatisieren. Mit Windows Script Host können Sie komplexere Skripts in der Befehlsshell ausführen. Weitere Informationen finden Sie unter [cscript](cscript.md) oder [WScript](wscript.md). Sie können Vorgänge effizienter mithilfe von Skripts ausführen, als dies mithilfe der Benutzeroberfläche möglich ist. Skripts akzeptieren alle Befehle, die in der Befehlszeile verfügbar sind.

Windows verfügt über zwei Befehls Shells: die Befehlsshell und [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6). Bei jeder Shell handelt es sich um ein Softwareprogramm, das eine direkte Kommunikation zwischen Ihnen und dem Betriebssystem oder der Anwendung ermöglicht und eine Umgebung zum Automatisieren des IT-betriebsbereit stellt

PowerShell wurde entwickelt, um die Funktionen der Befehlsshell zum Ausführen von PowerShell-Befehlen zu erweitern, die als Cmdlets bezeichnet werden. Cmdlets ähneln Windows-Befehlen, bieten jedoch eine erweiterbare Skriptsprache. Sie können Windows-Befehle und PowerShell-Cmdlets in PowerShell ausführen, aber in der Befehlsshell können nur Windows-Befehle und keine PowerShell-Cmdlets ausgeführt werden.

Bei der stabilsten aktuellen Windows-Automatisierung empfiehlt es sich, PowerShell anstelle von Windows-Befehlen oder Windows Script Host für Windows Automation zu verwenden.

> [!NOTE]
>Sie können auch [PowerShell Core](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6)herunterladen und installieren, die Open Source-Version von PowerShell.

> [!CAUTION]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie die folgenden Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Daten auf dem Computer sichern.

> [!NOTE]
> Führen Sie **regedit.exe** aus, und legen Sie den folgenden **reg_DWOrd Wert**fest, um die Vervollständigung von Datei-und Verzeichnisnamen in der Befehlsshell für eine Computer-oder Benutzer Anmelde Sitzung zu aktivieren bzw
>
> HKEY_LOCAL_MACHINE \software\microsoft\command processor\completionchar\ reg_DWOrd
>
> Um den **reg_DWOrd** Wert festzulegen, verwenden Sie den Hexadezimalwert eines Steuer Zeichens für eine bestimmte Funktion (z. b. **0 9** ist Tab und **0 08** ist RÜCKTASTE). Benutzerdefinierte Einstellungen haben Vorrang vor Computereinstellungen, und Befehlszeilenoptionen haben Vorrang vor den Registrierungs Einstellungen.

## <a name="command-line-reference-a-z"></a>Befehlszeilen Referenz A-Z

Wenn Sie Informationen zu einem bestimmten Windows-Befehl suchen möchten, klicken Sie im folgenden a-Z-Menü auf den Buchstaben, mit dem der Befehl beginnt, und klicken Sie dann auf den Befehlsnamen.

[A](#a)  |
 [B](#b)  |
 [C](#c)  |
 [D](#d)  |
 [E](#e)  |
 [F](#f)  |
 [G](#g)  |
 [H](#h)  |
 [I](#i)  |
 [J](#j)  |
 [K](#k)  |
 [L](#l)  |
 [M](#m)  |
 [N](#n)  |
 [O](#o)  |
 [P](#p)  |
 [F](#q)  |
 [R](#r)  |
 [S](#s)  |
 [T](#t)  |
 [U](#u)  |
 [V](#v)  |
 [W](#w)  |
 [X](#x) | J | Z

### <a name="a"></a>Ein

- [active](active.md)
- [add](add.md)
- [add alias](add-alias.md)
- [add volume](add-volume.md)
- [append](append.md)
- [arp](arp.md)
- [assign](assign.md)
- [assoc](assoc.md)
- [at](at.md)
- [atmadm](atmadm.md)
- [attach-vdisk](attach-vdisk.md)
- [attrib](attrib.md)
- [attributes](attributes.md)
  - [attributes disk](attributes-disk.md)
  - [attributes volume](attributes-volume.md)
- [auditpol](auditpol.md)
  - [auditpol backup](auditpol-backup.md)
  - [auditpol clear](auditpol-clear.md)
  - [auditpol get](auditpol-get.md)
  - [auditpol list](auditpol-list.md)
  - [auditpol remove](auditpol-remove.md)
  - [auditpol resourcesacl](auditpol-resourcesacl.md)
  - [auditpol restore](auditpol-restore.md)
  - [auditpol set](auditpol-set.md)
- [autochk](autochk.md)
- [autoconv](autoconv.md)
- [autofmt](autofmt.md)
- [automount](automount.md)

### <a name="b"></a>B

- [bcdboot](bcdboot.md)
- [bcdedit](bcdedit.md)
- [bdehdcfg](bdehdcfg.md)
  - [bdehdcfg driveinfo](bdehdcfg-driveinfo.md)
  - [bdehdcfg newdriveletter](bdehdcfg-newdriveletter.md)
  - [bdehdcfg quiet](bdehdcfg-quiet.md)
  - [bdehdcfg restart](bdehdcfg-restart.md)
  - [bdehdcfg size](bdehdcfg-size.md)
  - [bdehdcfg target](bdehdcfg-target.md)
- [begin backup](begin-backup.md)
- [begin restore](begin-restore.md)
- [bitsadmin](bitsadmin.md)
  - [bitsadmin addfile](bitsadmin-addfile.md)
  - [bitsadmin addfileset](bitsadmin-addfileset.md)
  - [bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)
  - [bitsadmin cache](bitsadmin-cache.md)
    - [bitsadmin cache and delete](bitsadmin-cache-and-delete.md)
    - [bitsadmin cache and deleteurl](bitsadmin-cache-and-deleteurl.md)
    - [bitsadmin cache and getexpirationtime](bitsadmin-cache-and-getexpirationtime.md)
    - [bitsadmin cache and getlimit](bitsadmin-cache-and-getlimit.md)
    - [bitsadmin cache and help](bitsadmin-cache-and-help.md)
    - [bitsadmin cache and info](bitsadmin-cache-and-info.md)
    - [bitsadmin cache and list](bitsadmin-cache-and-list.md)
    - [bitsadmin cache and setexpirationtime](bitsadmin-cache-and-setexpirationtime.md)
    - [bitsadmin cache and setlimit](bitsadmin-cache-and-setlimit.md)
    - [bitsadmin cache and clear](bitsadmin-cache-clear.md)
  - [bitsadmin cancel](bitsadmin-cancel.md)
  - [bitsadmin complete](bitsadmin-complete.md)
  - [bitsadmin create](bitsadmin-create.md)
  - [bitsadmin examples](bitsadmin-examples.md)
  - [bitsadmin getaclflags](bitsadmin-getaclflags.md)
  - [bitsadmin getbytestotal](bitsadmin-getbytestotal.md)
  - [bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)
  - [bitsadmin getclientcertificate](bitsadmin-getclientcertificate.md)
  - [bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)
  - [bitsadmin getcreationtime](bitsadmin-getcreationtime.md)
  - [bitsadmin getcustomheaders](bitsadmin-getcustomheaders.md)
  - [bitsadmin getdescription](bitsadmin-getdescription.md)
  - [bitsadmin getdisplayname](bitsadmin-getdisplayname.md)
  - [bitsadmin geterror](bitsadmin-geterror.md)
  - [bitsadmin geterrorcount](bitsadmin-geterrorcount.md)
  - [bitsadmin getfilestotal](bitsadmin-getfilestotal.md)
  - [bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)
  - [bitsadmin gethelpertokenflags](bitsadmin-gethelpertokenflags.md)
  - [bitsadmin gethelpertokensid](bitsadmin-gethelpertokensid.md)
  - [bitsadmin gethttpmethod](bitsadmin-gethttpmethod.md)
  - [bitsadmin getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)
  - [bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)
  - [bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)
  - [bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
  - [bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)
  - [bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)
  - [bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)
  - [bitsadmin getowner](bitsadmin-getowner.md)
  - [bitsadmin getpeercachingflags](bitsadmin-getpeercachingflags.md)
  - [bitsadmin getpriority](bitsadmin-getpriority.md)
  - [bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)
  - [bitsadmin getproxylist](bitsadmin-getproxylist.md)
  - [bitsadmin getproxyusage](bitsadmin-getproxyusage.md)
  - [bitsadmin getreplydata](bitsadmin-getreplydata.md)
  - [bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)
  - [bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)
  - [bitsadmin getsecurityflags](bitsadmin-getsecurityflags.md)
  - [bitsadmin getstate](bitsadmin-getstate.md)
  - [bitsadmin gettemporaryname](bitsadmin-gettemporaryname.md)
  - [bitsadmin gettype](bitsadmin-gettype.md)
  - [bitsadmin getvalidationstate](bitsadmin-getvalidationstate.md)
  - [bitsadmin help](bitsadmin-help.md)
  - [bitsadmin info](bitsadmin-info.md)
  - [bitsadmin list](bitsadmin-list.md)
  - [bitsadmin listfiles](bitsadmin-listfiles.md)
  - [bitsadmin makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
  - [bitsadmin monitor](bitsadmin-monitor.md)
  - [bitsadmin nowrap](bitsadmin-nowrap.md)
  - [bitsadmin peercaching](bitsadmin-peercaching.md)
    - [bitsadmin peercaching and getconfigurationflags](bitsadmin-peercaching-and-getconfigurationflags.md)
    - [bitsadmin peercaching and help](bitsadmin-peercaching-and-help.md)
    - [bitsadmin peercaching and setconfigurationflags](bitsadmin-peercaching-and-setconfigurationflags.md)
  - [bitsadmin peers](bitsadmin-peers.md)
    - [bitsadmin peers and clear](bitsadmin-peers-and-clear.md)
    - [bitsadmin peers and discover](bitsadmin-peers-and-discover.md)
    - [bitsadmin peers and help](bitsadmin-peers-and-help.md)
    - [bitsadmin peers and list](bitsadmin-peers-and-list.md)
  - [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  - [bitsadmin removeclientcertificate](bitsadmin-removeclientcertificate.md)
  - [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  - [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  - [bitsadmin reset](bitsadmin-reset.md)
  - [bitsadmin resume](bitsadmin-resume.md)
  - [bitsadmin setaclflag](bitsadmin-setaclflag.md)
  - [bitsadmin setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)
  - [bitsadmin setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)
  - [bitsadmin setcredentials](bitsadmin-setcredentials.md)
  - [bitsadmin setcustomheaders](bitsadmin-setcustomheaders.md)
  - [bitsadmin setdescription](bitsadmin-setdescription.md)
  - [bitsadmin setdisplayname](bitsadmin-setdisplayname.md)
  - [bitsadmin sethelpertoken](bitsadmin-sethelpertoken.md)
  - [bitsadmin sethelpertokenflags](bitsadmin-sethelpertokenflags.md)
  - [bitsadmin sethttpmethod](bitsadmin-sethttpmethod.md)
  - [bitsadmin setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)
  - [bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)
  - [bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
  - [bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)
  - [bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)
  - [bitsadmin setpeercachingflags](bitsadmin-setpeercachingflags.md)
  - [bitsadmin setpriority](bitsadmin-setpriority.md)
  - [bitsadmin setproxysettings](bitsadmin-setproxysettings.md)
  - [bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)
  - [bitsadmin setsecurityflags](bitsadmin-setsecurityflags.md)
  - [bitsadmin setvalidationstate](bitsadmin-setvalidationstate.md)
  - [bitsadmin suspend](bitsadmin-suspend.md)
  - [bitsadmin takeownership](bitsadmin-takeownership.md)
  - [bitsadmin transfer](bitsadmin-transfer.md)
  - [bitsadmin util](bitsadmin-util.md)
    - [bitsadmin util and enableanalyticchannel](bitsadmin-util-and-enableanalyticchannel.md)
    - [bitsadmin util and getieproxy](bitsadmin-util-and-getieproxy.md)
    - [bitsadmin util and help](bitsadmin-util-and-help.md)
    - [bitsadmin util and repairservice](bitsadmin-util-and-repairservice.md)
    - [bitsadmin util and setieproxy](bitsadmin-util-and-setieproxy.md)
    - [bitsadmin util and version](bitsadmin-util-and-version.md)
  - [bitsadmin wrap](bitsadmin-wrap.md)
- [bootcfg](bootcfg.md)
  - [bootcfg addsw](bootcfg-addsw.md)
  - [bootcfg copy](bootcfg-copy.md)
  - [bootcfg dbg1394](bootcfg-dbg1394.md)
  - [bootcfg debug](bootcfg-debug.md)
  - [bootcfg default](bootcfg-default.md)
  - [bootcfg delete](bootcfg-delete.md)
  - [bootcfg ems](bootcfg-ems.md)
  - [bootcfg query](bootcfg-query.md)
  - [bootcfg raw](bootcfg-raw.md)
  - [bootcfg rmsw](bootcfg-rmsw.md)
  - [bootcfg timeout](bootcfg-timeout.md)
- [break](break_1.md)

### <a name="c"></a>C

- [cacls](cacls.md)
- [call](call.md)
- [cd](cd.md)
- [certreq](certreq_1.md)
- [certutil](certutil.md)
- [change](change.md)
  - [change logon](change-logon.md)
  - [change port](change-port.md)
  - [change user](change-user.md)
- [chcp](chcp.md)
- [chdir](chdir.md)
- [chglogon](chglogon.md)
- [chgport](chgport.md)
- [chgusr](chgusr.md)
- [chkdsk](chkdsk.md)
- [chkntfs](chkntfs.md)
- [choice](choice.md)
- [cipher](cipher.md)
- [clean](clean.md)
- [cleanmgr](cleanmgr.md)
- [clip](clip.md)
- [cls](cls.md)
- [cmd](Cmd.md)
- [cmdkey](cmdkey.md)
- [cmstp](cmstp.md)
- [color](color.md)
- [comp](comp.md)
- [compact](compact.md)
- [Compact Vdisk](compact-vdisk.md)
- [convert](convert.md)
  - [convert basic](convert-basic.md)
  - [dynamisch konvertieren](convert-dynamic.md)
  - [convert gpt](convert-gpt.md)
  - [convert mbr](convert-mbr.md)
- [copy](copy.md)
- [cprofile](cprofile.md)
- [erstellen](create.md)
  - [Erstellen von EFI-Partitionen](create-partition-efi.md)
  - [ [erweiterte Partition](create-partition-extended.md) erstellen
  - [logische Partition erstellen](create-partition-logical.md)
  - [Erstellen einer Partition MSR](create-partition-msr.md)
  - [create partition primary](create-partition-primary.md)
  - [volumespiegelung erstellen](create-volume-mirror.md)
  - [Erstellen eines Volume-RAID](create-volume-raid.md)
  - [einfaches Volume erstellen](create-volume-simple.md)
  - [volumestripe erstellen](create-volume-stripe.md)
- [cscript](cscript.md)

### <a name="d"></a>D

- [date](date.md)
- [dcgpofix](dcgpofix.md)
- [defrag](defrag.md)
- [del](del.md)
- [delete](delete.md)
  - [Datenträger löschen](delete-disk.md)
  - [Partition löschen](delete-partition.md)
  - [Schatten löschen](delete-shadows.md)
  - [delete volume](delete-volume.md)
- [detach vdisk](detach-vdisk.md)
- [einzelnen](detail.md)
  - [Detail Festplatte](detail-disk.md)
  - [Detail Partition](detail-partition.md)
  - [Detail-Vdisk](detail-vdisk.md)
  - [Detail Volume](detail-volume.md)
- [Dfsdiag](dfsdiag.md)
  - [Dfsdiag-testdcs](dfsdiag-testdcs.md)
  - [Dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md)
  - [Dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md)
  - [Dfsdiag testreferral](dfsdiag-testreferral.md)
  - [Dfsdiag Testsites](dfsdiag-testsites.md)
- [dfsrmig](dfsrmig.md)
- [diantz](diantz.md)
- [dir](dir.md)
- [diskcomp](diskcomp.md)
- [diskcopy](diskcopy.md)
- [diskpart](diskpart.md)
- [diskperf](diskperf.md)
- [diskraid](diskraid.md)
- [diskshadow](diskshadow.md)
- [dispdiag](dispdiag.md)
- [dnscmd](dnscmd.md)
- [doskey](doskey.md)
- [driverquery](driverquery.md)

### <a name="e"></a>E

- [echo](echo.md)
- [edit](edit.md)
- [endlocal](endlocal.md)
- [Wiederherstellung beenden](end-restore.md)
- [erase](erase.md)
- [eventcreate](eventcreate.md)
- [eventquery](eventquery.md)
- [eventtriggers](eventtriggers.md)
- [Evntcmd](evntcmd.md)
- [exec](exec.md)
- [exit](exit_2.md)
- [expand](expand.md)
- [Erweitern von Vdisk](expand-vdisk.md)
- [sichtbar](expose.md)
- [extend](extend.md)
- [extract](extract.md)

### <a name="f"></a>F

- [fc](fc.md)
- [filesystems](filesystems.md)
- [find](find.md)
- [findstr](findstr.md)
- [finger](finger.md)
- [flattemp](flattemp.md)
- [fondue](fondue.md)
- [for](for.md)
- [forfiles](forfiles.md)
- [format](format.md)
- [freedisk](freedisk.md)
- [fsutil](fsutil.md)
  - [fsutil 8dot3name](fsutil-8dot3name.md)
  - [fsutil behavior](fsutil-behavior.md)
  - [fsutil dirty](fsutil-dirty.md)
  - [fsutil file](fsutil-file.md)
  - [fsutil fsinfo](fsutil-fsinfo.md)
  - [fsutil hardlink](fsutil-hardlink.md)
  - [fsutil objectid](fsutil-objectid.md)
  - [fsutil quota](fsutil-quota.md)
  - [fsutil repair](fsutil-repair.md)
  - [fsutil reparsepoint](fsutil-reparsepoint.md)
  - [fsutil resource](fsutil-resource.md)
  - [fsutil sparse](fsutil-sparse.md)
  - [fsutil tiering](fsutil-tiering.md)
  - [fsutil transaction](fsutil-transaction.md)
  - [fsutil usn](fsutil-usn.md)
  - [fsutil volume](fsutil-volume.md)
  - [fsutil wim](fsutil-wim.md)
- [ftp](ftp.md)
  - [ftp append](ftp-append.md)
  - [ftp ascii](ftp-ascii.md)
  - [ftp bell](ftp-bell_1.md)
  - [ftp binary](ftp-binary.md)
  - [ftp bye](ftp-bye.md)
  - [ftp cd](ftp-cd.md)
  - [ftp close](ftp-close_1.md)
  - [ftp debug](ftp-debug.md)
  - [ftp delete](ftp-delete.md)
  - [ftp dir](ftp-dir.md)
  - [ftp disconnect](ftp-disconnect_1.md)
  - [ftp get](ftp-get.md)
  - [ftp glob](ftp-glob_1.md)
  - [ftp hash](ftp-hash_1.md)
  - [ftp lcd](ftp-lcd.md)
  - [ftp literal](ftp-literal_1.md)
  - [ftp ls](ftp-ls_1.md)
  - [ftp mget](ftp-mget.md)
  - [ftp mkdir](ftp-mkdir.md)
  - [ftp mls](ftp-mls_1.md)
  - [ftp mput](ftp-mput_1.md)
  - [ftp open](ftp-open_1.md)
  - [ftp prompt](ftp-prompt_1.md)
  - [ftp put](ftp-put.md)
  - [ftp pwd](ftp-pwd_1.md)
  - [ftp quit](ftp-quit.md)
  - [ftp quote](ftp-quote.md)
  - [ftp recv](ftp-recv.md)
  - [ftp remotehelp](ftp-remotehelp_1.md)
  - [ftp rename](ftp-rename.md)
  - [ftp rmdir](ftp-rmdir.md)
  - [ftp send](ftp-send_1.md)
  - [ftp status](ftp-status.md)
  - [ftp trace](ftp-trace_1.md)
  - [ftp type](ftp-type.md)
  - [ftp user](ftp-user.md)
  - [ftp verbose](ftp-verbose_1.md)
  - [ftp mdelete](ftp-.mdelete_1.md)
  - [ftp mdir](ftp.mdir.md)
- [ftype](ftype.md)
- [fveupdate](fveupdate.md)

### <a name="g"></a>G

- [getmac](getmac.md)
- [gettype](gettype.md)
- [goto](goto.md)
- [gpfixup](gpfixup.md)
- [gpresult](gpresult.md)
- [gpt](gpt.md)
- [gpupdate](gpupdate.md)
- [graftabl](graftabl.md)

### <a name="h"></a>H

- [help](help.md)
- [helpctr](helpctr.md)
- [hostname](hostname.md)

### <a name="i"></a>I

- [icacls](icacls.md)
- [if](if.md)
- [Importieren (shadowdisk)](import.md)
- [Importieren (DiskPart)](import_1.md)
- [inactive](inactive.md)
- [inuse](inuse.md)
- [ipconfig](ipconfig.md)
- [ipxroute](ipxroute.md)
- [irftp](irftp.md)

### <a name="j"></a>J

- [jetpack](jetpack.md)

### <a name="k"></a>K

- [klist](klist.md)
- [ksetup](ksetup.md)
  - [ksetup addenctypeattr](ksetup-addenctypeattr.md)
  - [ksetup addhosttorealmmap](ksetup-addhosttorealmmap.md)
  - [ksetup addkdc](ksetup-addkdc.md)
  - [ksetup addkpasswd](ksetup-addkpasswd.md)
  - [ksetup addrealmflags](ksetup-addrealmflags.md)
  - [ksetup changepassword](ksetup-changepassword.md)
  - [ksetup delenctypeattr](ksetup-delenctypeattr.md)
  - [ksetup delhosttorealmmap](ksetup-delhosttorealmmap.md)
  - [ksetup delkdc](ksetup-delkdc.md)
  - [ksetup delkpasswd](ksetup-delkpasswd.md)
  - [ksetup delrealmflags](ksetup-delrealmflags.md)
  - [ksetup domain](ksetup-domain.md)
  - [ksetup dumpstate](ksetup-dumpstate.md)
  - [ksetup getenctypeattr](ksetup-getenctypeattr.md)
  - [ksetup listrealmflags](ksetup-listrealmflags.md)
  - [ksetup mapuser](ksetup-mapuser.md)
  - [ksetup removerealm](ksetup-removerealm.md)
  - [ksetup server](ksetup-server.md)
  - [ksetup setcomputerpassword](ksetup-setcomputerpassword.md)
  - [ksetup setenctypeattr](ksetup-setenctypeattr.md)
  - [ksetup setrealm](ksetup-setrealm.md)
  - [ksetup setrealmflags](ksetup-setrealmflags.md)
- [ktmutil](ktmutil.md)
- [ktpass](ktpass.md)

### <a name="l"></a>L

- [label](label.md)
- [list](list.md)
  - [Anbieter auflisten](list-providers.md)
  - [Schatten auflisten](list-shadows.md)
  - [Writer auflisten](list-writers.md)
- [Metadaten laden](load-metadata.md)
- [lodctr](lodctr.md)
- [logman](logman.md)
  - [logman create](logman-create.md)
  - [Warnung zu logman Create](logman-create-alert.md)
  - [logman Create-API](logman-create-api.md)
  - [logman Create cfg](logman-create-cfg.md)
  - [logman Create Counter](logman-create-counter.md)
  - [logman Create Trace](logman-create-trace.md)
  - [logman delete](logman-delete.md)
  - [Importieren und logman-Export von logman](logman-import-export.md)
  - [logman query](logman-query.md)
  - [logman Start und logman beendet](logman-start-stop.md)
  - [logman update](logman-update.md)
  - [logman Update-Warnung](logman-update-alert.md)
  - [logman Update-API](logman-update-api.md)
  - [logman update cfg](logman-update-cfg.md)
  - [logman update Counter](logman-update-counter.md)
  - [logman update Trace](logman-update-trace.md)
- [logoff](logoff.md)
- [lpq](lpq.md)
- [lpr](lpr.md)

### <a name="m"></a>M

- [macfile](macfile.md)
- [makecab](makecab.md)
- [Verwalten von BDE](manage-bde.md)
  - [Verwalten des BDE-Status](manage-bde-status.md)
  - [Verwalten von BDE](manage-bde-on.md)
  - [Verwalten von BDE](manage-bde-off.md)
  - [Verwalten von BDE Pause](manage-bde-pause.md)
  - [Verwalten von BDE Resume](manage-bde-resume.md)
  - [BDE-Sperre verwalten](manage-bde-lock.md)
  - [Verwalten von BDE Unlock](manage-bde-unlock.md)
  - [Verwalten von BDE Entsperrens](manage-bde-autounlock.md)
  - [BDE-Schutzvorrichtungen verwalten](manage-bde-protectors.md)
  - [Verwalten von BDE TPM](manage-bde-tpm.md)
  - [Verwalten von BDE-tidentifier](manage-bde-setidentifier.md)
  - [Verwalten von BDE forcerecovery](manage-bde-forcerecovery.md)
  - [Verwalten von BDE ChangePassword](manage-bde-changepassword.md)
  - [Verwalten von BDE changepin](manage-bde-changepin.md)
  - [Verwalten von BDE ChangeKey](manage-bde-changekey.md)
  - [Verwalten von BDE KeyPackage](manage-bde-keypackage.md)
  - [Verwalten des BDE-Upgrades](manage-bde-upgrade.md)
  - [Verwalten von BDE wipeer FreeSpace](manage-bde-wipefreespace.md)
- [mapadmin](mapadmin.md)
- [md](md.md)
- [Vdisk zusammenführen](merge-vdisk.md)
- [mkdir](mkdir.md)
- [mklink](mklink.md)
- [mmc](mmc.md)
- [mode](mode.md)
- [more](more.md)
- [mount](mount.md)
- [mountvol](mountvol.md)
- [move](move.md)
- [mqbkup](mqbkup.md)
- [mqsvc](mqsvc.md)
- [mqtgsvc](mqtgsvc.md)
- [msdt](msdt.md)
- [msg](msg.md)
- [msiexec](msiexec.md)
- [msinfo32](msinfo32.md)
- [mstsc](mstsc.md)

### <a name="n"></a>N

- [nbtstat](nbtstat.md)
- [netcfg](netcfg.md)
- [NET Print](net-print.md)
- [netsh](netsh.md)
- [netstat](netstat.md)
- [nfsadmin](nfsadmin.md)
- [nfsshare](nfsshare.md)
- [nfsstat](nfsstat.md)
- [nlbmgr](nlbmgr.md)
- [nslookup](nslookup.md)
  - [Befehl „nslookup exit“](nslookup-exit-command.md)
  - [Befehl „nslookup finger“](nslookup-finger-command.md)
  - [nslookup help](nslookup-help.md)
  - [nslookup ls](nslookup-ls.md)
  - [nslookup lserver](nslookup-lserver.md)
  - [nslookup root](nslookup-root.md)
  - [nslookup server](nslookup-server.md)
  - [nslookup set](nslookup-set.md)
  - [nslookup set all](nslookup-set-all.md)
  - [nslookup set class](nslookup-set-class.md)
  - [nslookup set d2](nslookup-set-d2.md)
  - [nslookup set debug](nslookup-set-debug.md)
  - [nslookup set domain](nslookup-set-domain.md)
  - [nslookup set port](nslookup-set-port.md)
  - [nslookup set querytype](nslookup-set-querytype.md)
  - [nslookup set recurse](nslookup-set-recurse.md)
  - [nslookup set retry](nslookup-set-retry.md)
  - [nslookup set root](nslookup-set-root.md)
  - [nslookup set search](nslookup-set-search.md)
  - [nslookup set srchlist](nslookup-set-srchlist.md)
  - [nslookup set timeout](nslookup-set-timeout.md)
  - [nslookup set type](nslookup-set-type.md)
  - [nslookup set vc](nslookup-set-vc.md)
  - [nslookup view](nslookup-view.md)
- [ntbackup](ntbackup.md)
- [ntcmdprompt](ntcmdprompt.md)
- [ntfrsutl](ntfrsutl.md)

### <a name="o"></a>O

- [aufzu](offline.md)
  - [Offline-Datenträger](offline-disk.md)
  - [Offline-Volume](offline-volume.md)
- [Internet](online.md)
  - [Online-Datenträger](online-disk.md)
  - [Online Volume](online-volume.md)
- [openfiles](openfiles.md)

### <a name="p"></a>P

- [pagefileconfig](pagefileconfig.md)
- [path](path.md)
- [pathping](pathping.md)
- [pause](pause.md)
- [pbadmin](pbadmin.md)
- [pentnt](pentnt.md)
- [perfmon](perfmon.md)
- [ping](ping.md)
- [pnpunattend](pnpunattend.md)
- [pnputil](pnputil.md)
- [popd](popd.md)
- [PowerShell](powershell.md)
- [PowerShell ISE](powershell_ise.md)
- [print](print.md)
- [prncnfg](prncnfg.md)
- [prndrvr](prndrvr.md)
- [prnjobs](prnjobs.md)
- [prnmngr](prnmngr.md)
- [prnport](prnport.md)
- [prnqctl](prnqctl.md)
- [prompt](prompt.md)
- [pubprn](pubprn.md)
- [pushd](pushd.md)
- [pushprinterconnections](pushprinterconnections.md)
- [pwlauncher](pwlauncher.md)

### <a name="q"></a>Q

- [qappsrv](qappsrv.md)
- [qprocess](qprocess.md)
- [Frage](query.md)
  - [query process](query-process.md)
  - [Abfrage Sitzung](query-session.md)
  - [termserver Abfragen](query-termserver.md)
  - [Benutzer Abfragen](query-user.md)
- [quser](quser.md)
- [qwinsta](qwinsta.md)

### <a name="r"></a>R

- [rcp](rcp.md)
- [rd](rd.md)
- [rdpsign](rdpsign.md)
- [recover](recover.md)
- [Datenträger Gruppe wiederherstellen](recover_1.md)
- [reg](reg.md)
  - [reg hinzufügen](reg-add.md)
  - [reg-Vergleich](reg-compare.md)
  - [reg-Kopie](reg-copy.md)
  - [reg löschen](reg-delete.md)
  - [reg-Export](reg-export.md)
  - [reg-Import](reg-import.md)
  - [reg laden](reg-load.md)
  - [reg-Abfrage](reg-query.md)
  - [reg-Wiederherstellung](reg-restore.md)
  - [REG speichern](reg-save.md)
  - [reg entladen](reg-unload.md)
- [regini](regini.md)
- [regsvr32](regsvr32.md)
- [relog](relog.md)
- [REM-Batchdatei](rem.md)
- [REM-Skript](rem_1.md)
- [remove](remove.md)
- [ren](ren.md)
- [rename](rename.md)
- [Reparieren](repair.md)
  - [Reparieren von BDE](repair-bde.md)
- [replace](replace.md)
- [neu einlesen](rescan.md)
- [reset](reset.md)
  - [reset session](reset-session.md)
- [erhalten](retain.md)
- [umzukehren](revert.md)
- [rexec](rexec.md)
- [risetup](risetup.md)
- [rmdir](rmdir.md)
- [robocopy](robocopy.md)
- [Route WS2008](route_ws2008.md)
- [rpcinfo](rpcinfo.md)
- [rpcping](rpcping.md)
- [rsh](rsh.md)
- [rundll32](rundll32.md)
- [rundll32 Datei printui](rundll32-printui.md)
- [rwinsta](rwinsta.md)

### <a name="s"></a>E

- [chen](san.md)
- [SC-Konfiguration](sc-config.md)
- [SC erstellen](sc-create.md)
- [SC löschen](sc-delete.md)
- [SC-Abfrage](sc-query.md)
- [schtasks](schtasks.md)
- [scwcmd](scwcmd.md)
  - [scwcmd-Analyse](scwcmd-analyze.md)
  - [scwcmd konfigurieren](scwcmd-configure.md)
  - [scwcmd-Register](scwcmd-register.md)
  - [scwcmd-Rollback](scwcmd-rollback.md)
  - [scwcmd-Transformation](scwcmd-transform.md)
  - [scwcmd-Ansicht](scwcmd-view.md)
- [secedit](secedit.md)
  - ["Secedit" analysieren](secedit-analyze.md)
  - [secedit konfigurieren](secedit-configure.md)
  - [secedit-Export](secedit-export.md)
  - [generaterollback für secedit](secedit-generaterollback.md)
  - [secedit-Import](secedit-import.md)
  - [secedit-Überprüfung](secedit-validate.md)
- [select](select.md)
  - [select disk](select-disk.md)
  - [Partition auswählen](select-partition.md)
  - [Vdisk auswählen](select-vdisk.md)
  - [select volume](select-volume.md)
- [serverceipoptin](serverceipoptin.md)
- [ServerManagerCmd](servermanagercmd.md)
- [serverweroptin](serverweroptin.md)
- [Festlegen von Umgebungsvariablen](set_1.md)
- [Schatten Kopie festlegen](set_2.md)
  - [Kontext festlegen](set-context.md)
  - [ID festlegen](set-id.md)
  - [setlocal](setlocal.md)
  - [Metadaten festlegen](set-metadata.md)
  - [Set-Option](set-option.md)
  - [ausführlich festlegen](set-verbose.md)
- [setx](setx.md)
- [sfc](sfc.md)
- [shadow](shadow.md)
- [shift](shift.md)
- [showmount](showmount.md)
- [shrink](shrink.md)
- [shutdown](shutdown.md)
- [Wiederherstellung simulieren](simulate-restore.md)
- [sort](sort.md)
- [start](start.md)
- [Unterbefehls Satz Gerät](subcommand-set-device.md)
- [Unterbefehls Satz "drivergroup"](subcommand-set-drivergroup.md)
- [Unterbefehls Satz "drivergroupfilter"](subcommand-set-drivergroupfilter.md)
- [Unterbefehls Satz "DriverPackage"](subcommand-set-driverpackage.md)
- [Bild des untergeordneten Befehlssatzes](subcommand-set-image.md)
- [Unterbefehls Satz-ImageGroup](subcommand-set-imagegroup.md)
- [Unterbefehls Satz Server](subcommand-set-server.md)
- [Unterbefehls Satz Transportserver](subcommand-set-transportserver.md)
- [Unterbefehls Satz MulticastTransmission](subcommand-start-multicasttransmission.md)
- [Namespace des Unterbefehls starten](subcommand-start-namespace.md)
- [Unterbefehl zum Start Server](subcommand-start-server.md)
- [Unterbefehl starten von Transportserver](subcommand-start-transportserver.md)
- [Unterbefehl zum Abbrechen des Servers](subcommand-stop-server.md)
- [Unterbefehl zum Abbrechen von Transportserver](subcommand-stop-transportserver.md)
- [subst](subst.md)
- [sxstrace](sxstrace.md)
- [sysocmgr](sysocmgr.md)
- [systeminfo](systeminfo.md)


### <a name="t"></a>T

- [takeown](takeown.md)
- [tapicfg](tapicfg.md)
- [taskkill](taskkill.md)
- [tasklist](tasklist.md)
- [tcmsetup](tcmsetup.md)
- [telnet](telnet.md)
  - [Telnet schließen](telnet-close.md)
  - [Telnet-Anzeige](telnet-display.md)
  - [Telnet geöffnet](telnet-open.md)
  - [Telnet-Quit](telnet-quit.md)
  - [Telnet-Sendevorgang](telnet-send.md)
  - [Telnet-Satz](telnet-set.md)
  - [Telnet-Status](telnet-status.md)
  - [Telnet nicht festgelegt](telnet-unset.md)
- [tftp](tftp.md)
- [time](time.md)
- [timeout](timeout_1.md)
- [title](title_1.md)
- [tlntadmn](tlntadmn.md)
- [tpmtool](tpmtool.md)
- [tpmvscmgr](tpmvscmgr.md)
- [tracerpt](tracerpt_1.md)
- [tracert](tracert.md)
- [tree](tree.md)
- [tscon](tscon.md)
- [tsdiscon](tsdiscon.md)
- [tsecimp](tsecimp_1.md)
- [tskill](tskill.md)
- [tsprof](tsprof.md)
- [type](type.md)
- [typeperf](typeperf.md)
- [tzutil](tzutil.md)

### <a name="u"></a>U

- [Heben des](unexpose.md)
- [UniqueId](uniqueid.md)
- [unlodctr](unlodctr_1.md)

### <a name="v"></a>V

- [ver](ver.md)
- [verifier](verifier.md)
- [verify](verify_1.md)
- [vol](vol.md)
- [vssadmin](vssadmin.md)
  - [vssadmin delete shadows](vssadmin-delete-shadows.md)
  - [vssadmin list shadows](vssadmin-list-shadows.md)
  - [vssadmin list writers](vssadmin-list-writers.md)
  - [vssadmin resize shadowstorage](vssadmin-resize-shadowstorage.md)

### <a name="w"></a>W

- [waitfor](waitfor.md)
- [wbadmin](wbadmin.md)
  - [Wbadmin delete-Katalog](wbadmin-delete-catalog.md)
  - [Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  - [Wbadmin-Sicherung deaktivieren](wbadmin-disable-backup.md)
  - [Wbadmin-Sicherung aktivieren](wbadmin-enable-backup.md)
  - [Wbadmin Get Disks](wbadmin-get-disks.md)
  - [Wbadmin-Get-Elemente](wbadmin-get-items.md)
  - [Wbadmin-Status "Get"](wbadmin-get-status.md)
  - [Wbadmin-Get-Versionen](wbadmin-get-versions.md)
  - [Wbadmin-Wiederherstellungs Katalog](wbadmin-restore-catalog.md)
  - [Wbadmin-Sicherung starten](wbadmin-start-backup.md)
  - [Wbadmin-Wiederherstellung starten](wbadmin-start-recovery.md)
  - [WBADMIN-START SYSRECOVERY](wbadmin-start-sysrecovery.md)
  - [Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)
  - [Wbadmin start Systemstatus](wbadmin-start-systemstaterecovery.md)
  - [Auftrag zum Abbrechen von Wbadmin](wbadmin-stop-job.md)
- [wdsutil](wdsutil.md)
- [wecutil](wecutil.md)
- [wevtutil](wevtutil.md)
- [where](where_1.md)
- [whoami](whoami.md)
- [winnt](winnt.md)
- [winnt32](winnt32.md)
- [winpop](winpop.md)
- [winrs](winrs.md)
- [WinSAT-Arbeitsspeicher](winsat-mem.md)
- [WinSAT-MF-Medien](winsat-mfmedia.md)
- [wmic](wmic.md)
- [Maschine](writer.md)
- [wscript](wscript.md)

### <a name="x"></a>X

- [xcopy](xcopy.md)
