---
title: Windows-Befehle
description: Windows-Befehle
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: jasongerend
ms.author: jgerend
manager: dongill
ms.date: 06/26/2019
ms.prod: windows-server
ms.openlocfilehash: 9d68e2becbf9c6522be7e1ff6e6742d44f3a8247
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829233"
---
# <a name="windows-commands"></a>Windows-Befehle

Für alle unterstützten Versionen von Windows (Server und Client) ist eine Reihe von Win32-Konsolen Befehlen integriert.

In diesem Dokumentations Satz werden die Windows-Befehle beschrieben, die Sie zum Automatisieren von Aufgaben mithilfe von Skripts oder Skript Erstellungs Tools verwenden können.

Wenn Sie Informationen zu einem bestimmten Befehl suchen möchten, klicken Sie im folgenden a-Z-Menü auf den Buchstaben, mit dem der Befehl beginnt, und klicken Sie dann auf den Befehlsnamen.

[A](#a) |
[B](#b) | 
[C](#c) | 
[D](#d) | 
[E](#e) | 
[F](#f) | 
[G](#g) | 
[H](#h) | 
[I](#i) |
[J](#j) | 
[K](#k) | 
[L](#l) | 
[M](#m) | 
[N](#n) | 
[O](#o) | 
[P](#p) | 
[Q](#q) | 
[R](#r) | 
[S](#s) | 
[t](#t) | 
[U](#u) | 
[V](#v) | 
[W](#w) | 
[X](#x) | J | Z

## <a name="prerequisites"></a>Erforderliche Komponenten

Die in diesem Thema enthaltenen Informationen gelten für:

-   Windows Server 2019
-   Windows Server (Halbjährlicher Kanal)
-   Windows Server 2016
-   Windows Server 2012 R2
-   Windows Server 2012 
-   Windows Server 2008 R2
-   WindowsServer 2008
-   Windows 10
-   Windows 8.1

### <a name="command-shell-overview"></a>Übersicht über Befehlsshell

Die Befehlsshell war die erste Shell, die in Windows integriert wurde, um Routineaufgaben wie die Verwaltung von Benutzerkonten oder nächtliche Sicherungen mit Batch Dateien (BAT-Dateien) zu automatisieren. Mit Windows Script Host können Sie komplexere Skripts in der Befehlsshell ausführen. Weitere Informationen finden Sie unter [cscript](cscript.md) oder [WScript](wscript.md). Sie können Vorgänge effizienter mithilfe von Skripts ausführen, als dies mithilfe der Benutzeroberfläche möglich ist. Skripts akzeptieren alle Befehle, die in der Befehlszeile verfügbar sind.

Windows verfügt über zwei Befehls Shells: die Befehlsshell und [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6). Bei jeder Shell handelt es sich um ein Softwareprogramm, das eine direkte Kommunikation zwischen Ihnen und dem Betriebssystem oder der Anwendung ermöglicht und eine Umgebung zum Automatisieren des IT-betriebsbereit stellt

PowerShell wurde entwickelt, um die Funktionen der Befehlsshell zum Ausführen von PowerShell-Befehlen zu erweitern, die als Cmdlets bezeichnet werden. Cmdlets ähneln Windows-Befehlen, bieten jedoch eine erweiterbare Skriptsprache. Sie können Windows-Befehle und PowerShell-Cmdlets in PowerShell ausführen, aber in der Befehlsshell können nur Windows-Befehle und keine PowerShell-Cmdlets ausgeführt werden.

Bei der stabilsten aktuellen Windows-Automatisierung empfiehlt es sich, PowerShell anstelle von Windows-Befehlen oder Windows Script Host für Windows Automation zu verwenden. 
> [!NOTE]
>Sie können auch [PowerShell Core](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6)herunterladen und installieren, die Open Source-Version von PowerShell. 

> [!CAUTION]
> Eine fehlerhafte Bearbeitung der Registrierung kann Ihr System schwer beschädigen. Bevor Sie die folgenden Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Daten auf dem Computer sichern.

> [!NOTE]
> Führen Sie **Regedit. exe** aus, und legen Sie den folgenden **reg_DWOrd Wert**fest, um die Vervollständigung von Datei-und Verzeichnisnamen in der Befehlsshell für eine Computer-oder Benutzer Anmelde Sitzung zu aktivieren oder deaktivieren
> 
> HKEY_LOCAL_MACHINE \software\microsoft\command processor\completionchar\ reg_DWOrd
> 
> Um den **reg_DWOrd** Wert festzulegen, verwenden Sie den Hexadezimalwert eines Steuer Zeichens für eine bestimmte Funktion (z. b. **0 9** ist Tab und **0 08** ist RÜCKTASTE). Benutzerdefinierte Einstellungen haben Vorrang vor Computereinstellungen, und Befehlszeilenoptionen haben Vorrang vor den Registrierungs Einstellungen.

## <a name="command-line-reference-a-z"></a>Befehlszeilen Referenz A-Z

Wenn Sie Informationen zu einem bestimmten Windows-Befehl suchen möchten, klicken Sie im folgenden a-Z-Menü auf den Buchstaben, mit dem der Befehl beginnt, und klicken Sie dann auf den Befehlsnamen.

[A](#a) |
[B](#b) | 
[C](#c) | 
[D](#d) | 
[E](#e) | 
[F](#f) | 
[G](#g) | 
[H](#h) | 
[I](#i) |
[J](#j) | 
[K](#k) | 
[L](#l) | 
[M](#m) | 
[N](#n) | 
[O](#o) | 
[P](#p) | 
[Q](#q) | 
[R](#r) | 
[S](#s) | 
[t](#t) | 
[U](#u) | 
[V](#v) | 
[W](#w) | 
[X](#x) | J | Z

### <a name="a"></a>A
-   [append](append.md)
-   [arp](arp.md)
-   [assoc](assoc.md)
-   [at](at.md)
-   [atmadm](atmadm.md)
-   [attrib](attrib.md)
-   [auditpol](auditpol.md)
-   [autochk](autochk.md)
-   [autoconv](autoconv.md)
-   [autofmt](autofmt.md)

### <a name="b"></a>B
- [bcdboot](bcdboot.md)
- [bcdedit](bcdedit.md)
- [bdehdcfg](bdehdcfg.md)
- [bitsadmin](bitsadmin.md)
  -   [bitsadmin addfile](bitsadmin-addfile.md)
  -   [bitsadmin addfileset](bitsadmin-addfileset.md)
  -   [bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)
  -   [bitsadmin cancel](bitsadmin-cancel.md)
  -   [bitsadmin complete](bitsadmin-complete.md)
  -   [bitsadmin create](bitsadmin-create.md)
  -   [bitsadmin getaclflags](bitsadmin-getaclflags.md)
  -   [bitsadmin getbytestotal](bitsadmin-getbytestotal.md)
  -   [bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)
  -   [bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)
  -   [bitsadmin getcreationtime](bitsadmin-getcreationtime.md)
  -   [bitsadmin getdescription](bitsadmin-getdescription.md)
  -   [bitsadmin getdisplayname](bitsadmin-getdisplayname.md)
  -   [bitsadmin geterror](bitsadmin-geterror.md)
  -   [bitsadmin geterrorcount](bitsadmin-geterrorcount.md)
  -   [bitsadmin getfilestotal](bitsadmin-getfilestotal.md)
  -   [bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)
  -   [bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)
  -   [bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)
  -   [bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
  -   [bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)
  -   [bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)
  -   [bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)
  -   [bitsadmin getowner](bitsadmin-getowner.md)
  -   [biout admin-Priorität erhalten](bitsadmin-getpriority.md)
  -   [bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)
  -   [bitsadmin getproxylist](bitsadmin-getproxylist.md)
  -   [bitsadmin getproxyusage](bitsadmin-getproxyusage.md)
  -   [bitsadmin getreplydata](bitsadmin-getreplydata.md)
  -   [bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)
  -   [bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)
  -   [bitsadmin getstate](bitsadmin-getstate.md)
  -   [bitsadmin gettype](bitsadmin-gettype.md)
  -   [bitsadmin help](bitsadmin-help.md)
  -   [bitsadmin info](bitsadmin-info.md)
  -   [bitsadmin list](bitsadmin-list.md)
  -   [bitsadmin listfiles](bitsadmin-listfiles.md)
  -   [bitsadmin monitor](bitsadmin-monitor.md)
  -   [bitsadmin nowrap](bitsadmin-nowrap.md)
  -   [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  -   [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  -   [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  -   [bitsadmin reset](bitsadmin-reset.md)
  -   [bitsadmin resume](bitsadmin-resume.md)
  -   [bitsadmin setaclflag](bitsadmin-setaclflag.md)
  -   [bitsadmin setcredentials](bitsadmin-setcredentials.md)
  -   [bitsadmin setdescription](bitsadmin-setdescription.md)
  -   [bitsadmin setdisplayname](bitsadmin-setdisplayname.md)
  -   [bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)
  -   [bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
  -   [bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)
  -   [bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)
  -   [bitsadmin setpriority](bitsadmin-setpriority.md)
  -   [bitsadmin setproxysettings](bitsadmin-setproxysettings.md)
  -   [bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)
  -   [bitsadmin suspend](bitsadmin-suspend.md)
  -   [bitsadmin takeownership](bitsadmin-takeownership.md)
  -   [bitadmin-Übertragung](bitsadmin-transfer.md)
  -   [bitsadmin util](bitsadmin-util.md)
  -   [bitsadmin wrap](bitsadmin-wrap.md)
- [bootcfg](bootcfg.md)
  -   [bootcfg addsw](bootcfg-addsw.md)
  -   [bootcfg copy](bootcfg-copy.md)
  -   [bootcfg dbg1394](bootcfg-dbg1394.md)
  -   [bootcfg debug](bootcfg-debug.md)  
  -   [bootcfg default](bootcfg-default.md)
  -   [bootcfg delete](bootcfg-delete.md)
  -   [bootcfg ems](bootcfg-ems.md)
  -   [bootcfg query](bootcfg-query.md)
  -   [bootcfg raw](bootcfg-raw.md)
  -   [bootcfg rmsw](bootcfg-rmsw.md)
  -   [bootcfg timeout](bootcfg-timeout.md)
- [break](break_1.md)

### <a name="c"></a>A
- [cacls](cacls_1.md)
- [call](call.md)
- [cd](cd.md)
- [certreq](certreq_1.md)
- [certutil](certutil.md)
- [change](change.md)
  -   [change logon](change-logon.md)
  -   [change port](change-port.md)
  -   [change user](change-user.md)
- [chcp](chcp.md)
- [chdir](chdir_1.md)
- [chglogon](chglogon.md)
- [chgport](chgport.md)
- [chgusr](chgusr.md)
- [chkdsk](chkdsk.md)
- [chkntfs](chkntfs.md)
- [choice](choice.md)
- [cipher](cipher.md)
- [cleanmgr](cleanmgr.md)
- [clip](clip.md)
- [cls](cls.md)
- [Cmd](Cmd.md)
- [cmdkey](cmdkey.md)
- [cmstp](cmstp.md)
- [color](color.md)
- [comp](comp.md)
- [compact](compact.md)
- [convert](convert.md)
- [copy](copy.md)
- [cprofile](cprofile.md)
- [cscript](cscript.md)

### <a name="d"></a>D
-   [date](date.md)
-   [dcgpofix](dcgpofix.md)
-   [defrag](defrag.md)
-   [del](del.md)
-   [dfsrmig](dfsrmig.md)
-   [diantz](diantz.md)
-   [dir](dir.md)
-   [diskcomp](diskcomp.md)
-   [diskcopy](diskcopy.md)
-   [diskpart](diskpart.md)
-   [diskperf](diskperf.md)
-   [diskraid](diskraid.md)
-   [diskshadow](diskshadow.md)
-   [dispdiag](dispdiag.md)
-   [dnscmd](Dnscmd.md)
-   [doskey](doskey.md)
-   [driverquery](driverquery.md)

### <a name="e"></a>E
-   [echo](echo.md)
-   [edit](edit.md)
-   [endlocal](endlocal.md)
-   [erase](erase.md)
-   [eventcreate](eventcreate.md)
-   [eventquery](eventquery.md)
-   [eventtriggers](eventtriggers.md)
-   [evntcmd](Evntcmd.md)
-   [exit](exit_2.md)
-   [expand](expand.md)
-   [extract](extract.md)

### <a name="f"></a>C
- [fc](fc.md)
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
  -   [fsutil 8dot3name](fsutil-8dot3name.md) 
  -   [fsutil behavior](fsutil-behavior.md) 
  -   [fsutil file](fsutil-file.md)
  -   [fsutil fsinfo](fsutil-fsinfo.md)
  -   [fsutil hardlink](fsutil-hardlink.md)
  -   [fsutil objectid](fsutil-objectid.md)
  -   [fsutil quota](fsutil-quota.md)
  -   [fsutil repair](fsutil-repair.md)
  -   [fsutil reparsepoint](fsutil-reparsepoint.md)
  -   [fsutil resource](fsutil-resource.md)
  -   [fsutil sparse](fsutil-sparse.md)
  -   [fsutil tiering](fsutil-tiering.md)
  -   [fsutil transaction](fsutil-transaction.md)
  -   [fsutil usn](fsutil-usn.md)
  -   [fsutil volume](fsutil-volume.md)
  -   [fsutil wim](fsutil-wim.md)
- [FTP](ftp.md)
- [ftype](ftype.md)
- [fveupdate](fveupdate.md)

### <a name="g"></a>G
-   [getmac](getmac.md)
-   [gettype](gettype.md)
-   [goto](goto.md)
-   [gpfixup](gpfixup.md)
-   [gpresult](gpresult.md)
-   [gpupdate](gpupdate.md)
-   [graftabl](graftabl.md)

### <a name="h"></a>H
-   [help](help.md)
-   [helpctr](helpctr.md)
-   [hostname](hostname.md)

### <a name="i"></a>I
-   [icacls](icacls.md)
-   [if](if.md)
-   [inuse](inuse.md)
-   [ipconfig](ipconfig.md)
-   [ipxroute](ipxroute.md)
-   [irftp](irftp.md)

### <a name="j"></a>J
-   [jetpack](jetpack.md)

### <a name="k"></a>K
- [klist](klist.md)
- [ksetup](ksetup.md)
  -   [Ksetup: setrealm](ksetup-setrealm.md)
  -   [Ksetup: mapuser](ksetup-mapuser.md)
  -   [Ksetup: addkdc](ksetup-addkdc.md)
  -   [Ksetup: Delta Controller](ksetup-delkdc.md)
  -   [Ksetup: addkpasswd](ksetup-addkpasswd.md)
  -   [Ksetup: Delta Pass WD](ksetup-delkpasswd.md)
  -   [Ksetup: Server](ksetup-server.md)
  -   [Ksetup: setcomputerpassword](ksetup-setcomputerpassword.md)
  -   [Ksetup: removerealm](ksetup-removerealm.md)
  -   [Ksetup: Domäne](ksetup-domain.md)
  -   [Ksetup: ChangePassword](ksetup-changepassword.md)
  -   [Ksetup: listrealmflags](ksetup-listrealmflags.md)
  -   [Ksetup: setrealmflags](ksetup-setrealmflags.md)
  -   [Ksetup: adressalm Flags](ksetup-addrealmflags.md)
  -   [Ksetup: Delta Flags](ksetup-delrealmflags.md)
  -   [Ksetup: dumpstate](ksetup-dumpstate.md)
  -   [Ksetup: addhosttorealmmap](ksetup-addhosttorealmmap.md)
  -   [Ksetup: Delta Host Report Map](ksetup-delhosttorealmmap.md)
  -   [Ksetup: setenctypeattr](ksetup-setenctypeattr.md)
  -   [Ksetup: getenctypeattr](ksetup-getenctypeattr.md)
  -   [Ksetup: addenctypeattr](ksetup-addenctypeattr.md)
  -   [Ksetup: Delta Type](ksetup-delenctypeattr.md) 
- [ktmutil](ktmutil.md)
- [ktpass](ktpass.md)

### <a name="l"></a>L
- [label](label.md)
- [lodctr](lodctr.md)
- [logman](logman.md)
  -   [logman create](logman-create.md)
  -   [logman query](logman-query.md)
  -   [logman Start & 124; anzuhalten](logman-start-stop.md)
  -   [logman delete](logman-delete.md)
  -   [logman update](logman-update.md)
  -   [logman Import & 124; Exports](logman-import-export.md)
- [logoff](logoff.md)
- [lpq](lpq.md)
- [lpr](lpr.md)

### <a name="m"></a>M
- [macfile](macfile.md)
- [makecab](makecab.md)
- [manage-bde](manage-bde.md)
  -   [manage-bde: Status](manage-bde-status.md)
  -   [manage-bde: on](manage-bde-on.md)
  -   [manage-bde: Off](manage-bde-off.md)
  -   [manage-bde: Anhalten](manage-bde-pause.md)
  -   [manage-bde: Resume](manage-bde-resume.md)
  -   [manage-bde: Lock](manage-bde-lock.md)
  -   [manage-bde: entsperren](manage-bde-unlock.md)
  -   [manage-bde: automatische Entsperrung](manage-bde-autounlock.md)
  -   [manage-bde: Schutzvorrichtungen](manage-bde-protectors.md)
  -   [manage-bde: TPM](manage-bde-tpm.md)
  -   [manage-bde:-Objekt-tifier](manage-bde-setidentifier.md)
  -   [manage-bde: forcerecovery](manage-bde-forcerecovery.md)
  -   [manage-bde: ChangePassword](manage-bde-changepassword.md)
  -   [manage-bde: changepin](manage-bde-changepin.md)
  -   [manage-bde: ChangeKey](manage-bde-changekey.md)
  -   [manage-bde: KeyPackage](manage-bde-keypackage.md)
  -   [manage-bde: Upgrade](manage-bde-upgrade.md)
  -   [manage-bde: wipeer FreeSpace](manage-bde-wipefreespace.md)
- [mapadmin](mapadmin.md)
- [Md](Md.md)
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
- [netsh](netsh.md)
- [netstat](netstat.md)
- [Net print](net-print.md)
- [nfsadmin](nfsadmin.md)
- [nfsshare](nfsshare.md)
- [nfsstat](nfsstat.md)
- [nlbmgr](nlbmgr.md)
- [nslookup](nslookup.md)
  -   [Nslookup-Exit-Befehl](nslookup-exit-command.md)
  -   [Nslookup-fingerbefehl](nslookup-finger-command.md)
  -   [nslookup help](nslookup-help.md)
  -   [nslookup ls](nslookup-ls.md)
  -   [nslookup lserver](nslookup-lserver.md)
  -   [nslookup root](nslookup-root.md)
  -   [nslookup server](nslookup-server.md)
  -   [nslookup set](nslookup-set.md)
  -   [nslookup set all](nslookup-set-all.md)
  -   [nslookup set class](nslookup-set-class.md)
  -   [nslookup set d2](nslookup-set-d2.md)
  -   [nslookup set debug](nslookup-set-debug.md)
  -   [nslookup set domain](nslookup-set-domain.md)
  -   [nslookup set port](nslookup-set-port.md)
  -   [nslookup set querytype](nslookup-set-querytype.md)
  -   [nslookup set recurse](nslookup-set-recurse.md)
  -   [nslookup set retry](nslookup-set-retry.md)
  -   [nslookup set root](nslookup-set-root.md)
  -   [nslookup set search](nslookup-set-search.md)
  -   [nslookup set srchlist](nslookup-set-srchlist.md)
  -   [nslookup set timeout](nslookup-set-timeout.md)
  -   [nslookup set type](nslookup-set-type.md)
  -   [nslookup set vc](nslookup-set-vc.md)
  -   [nslookup view](nslookup-view.md)
- [ntbackup](ntbackup.md)
- [ntcmdprompt](ntcmdprompt.md)
- [ntfrsutl](ntfrsutl.md)

### <a name="o"></a>O
-   [openfiles](openfiles.md)

### <a name="p"></a>P
-   [pagefileconfig](pagefileconfig.md)
-   [path](path.md)
-   [pathping](pathping.md)
-   [pause](pause.md)
-   [pbadmin](pbadmin.md)
-   [pentnt](pentnt.md)
-   [perfmon](perfmon.md)
-   [ping](ping.md)
-   [pnpunattend](pnpunattend.md)
-   [pnputil](pnputil.md)
-   [popd](popd.md)
-   [PowerShell](PowerShell.md)
-   [PowerShell_ise](PowerShell_ise.md)
-   [print](print.md)
-   [prncnfg](prncnfg.md)
-   [prndrvr](prndrvr.md)
-   [prnjobs](prnjobs.md)
-   [prnmngr](prnmngr.md)
-   [prnport](prnport.md)
-   [prnqctl](prnqctl.md)
-   [prompt](prompt.md)
-   [pubprn](pubprn.md)
-   [pushd](pushd.md)
-   [pushprinterconnections](pushprinterconnections.md)

### <a name="q"></a>Q
-   [qappsrv](qappsrv.md)
-   [qprocess](qprocess.md)
-   [Frage](query.md)
-   [quser](quser.md)
-   [qwinsta](qwinsta.md)

### <a name="r"></a>R
- [rcp](rcp.md)
- [rd](rd.md)
- [rdpsign](rdpsign.md)
- [recover](recover.md)
- [reg](reg.md)
  -   [reg hinzufügen](reg-add.md)
  -   [reg-Vergleich](reg-compare.md)
  -   [reg-Kopie](reg-copy.md)
  -   [reg löschen](reg-delete.md)
  -   [reg-Export](reg-export.md)
  -   [reg-Import](reg-import.md)
  -   [reg laden](reg-load.md)
  -   [reg-Abfrage](reg-query.md)
  -   [reg-Wiederherstellung](reg-restore.md)
  -   [REG speichern](reg-save.md)
  -   [reg entladen](reg-unload.md)
- [regini](regini.md)
- [regsvr32](regsvr32.md)
- [relog](relog.md)
- [rem](rem.md)
- [ren](ren.md)
- [rename](rename.md)
- [repair-bde](repair-bde.md)
- [replace](replace.md)
- [reset session](reset-session.md)
- [rexec](rexec.md)
- [risetup](risetup.md)
- [rmdir](rmdir.md)
- [robocopy](robocopy.md)
- [route_ws2008](route_ws2008.md)
- [rpcinfo](rpcinfo.md)
- [rpcping](rpcping.md)
- [rsh](rsh.md)
- [rundll32](rundll32.md)
- [rwinsta](rwinsta.md)

### <a name="s"></a>S
- [schtasks](schtasks.md)
- [scwcmd](Scwcmd.md)
  -   [scwcmd: analysieren](scwcmd-analyze.md)
  -   [scwcmd: Konfigurieren](scwcmd-configure.md)
  -   [scwcmd: registrieren](scwcmd-register.md) 
  -   [scwcmd: Rollback](scwcmd-rollback.md) 
  -   [scwcmd: Transformation](scwcmd-transform.md) 
  -   [scwcmd: Ansicht](scwcmd-view.md) 
- [secedit](secedit.md)
  -   [secedit: analysieren](secedit-analyze.md)
  -   [secedit: Konfigurieren](secedit-configure.md)
  -   [secedit: Export](secedit-export.md)
  -   [secedit: generaterollback](secedit-generaterollback.md)
  -   [secedit: Importieren](secedit-import.md)
  -   [secedit: Validate](secedit-validate.md)
- [serverceipoptin](serverceipoptin.md)
- [Servermanagercmd](Servermanagercmd.md)
- [serverweroptin](serverweroptin.md)
- [set](set_1.md)
- [setlocal](setlocal.md)
- [setx](setx.md)
- [sfc](sfc.md)
- [shadow](shadow.md)
- [shift](shift.md)
- [showmount](showmount.md)
- [shutdown](shutdown.md)
- [sort](sort.md)
- [start](start.md)
- [subst](subst.md)
- [sxstrace](sxstrace.md)
- [sysocmgr](sysocmgr.md)
- [systeminfo](systeminfo.md)

### <a name="t"></a>T
-   [takeown](takeown.md)
-   [tapicfg](tapicfg.md)
-   [taskkill](taskkill.md)
-   [tasklist](tasklist.md)
-   [tcmsetup](tcmsetup.md)
-   [telnet](telnet.md)
-   [tftp](tftp.md)
-   [time](time.md)
-   [timeout](timeout_1.md)
-   [title](title_1.md)
-   [tlntadmn](tlntadmn.md)
-   [tpmvscmgr](tpmvscmgr.md)
-   [tracerpt](tracerpt_1.md)
-   [tracert](tracert.md)
-   [tree](tree.md)
-   [tscon](tscon.md)
-   [tsdiscon](tsdiscon.md)
-   [tsecimp](tsecimp_1.md)
-   [tskill](tskill.md)
-   [tsprof](tsprof.md)
-   [type](type.md)
-   [typeperf](typeperf.md)
-   [tzutil](tzutil.md)

### <a name="u"></a>U
-   [unlodctr](unlodctr_1.md)

### <a name="v"></a>V
-   [ver](ver.md)
-   [verifier](verifier.md)
-   [verify](verify_1.md)
-   [vol](vol.md)
-   [vssadmin](vssadmin.md) -- 

### <a name="w"></a>W
- [waitfor](waitfor.md)
- [wbadmin](wbadmin.md)
  -   [Wbadmin-Sicherung aktivieren](wbadmin-enable-backup.md)
  -   [Wbadmin-Sicherung deaktivieren](wbadmin-disable-backup.md)
  -   [Wbadmin-Sicherung starten](wbadmin-start-backup.md)
  -   [Auftrag zum Abbrechen von Wbadmin](wbadmin-stop-job.md)
  -   [Wbadmin-Get-Versionen](wbadmin-get-versions.md)
  -   [Wbadmin-Get-Elemente](wbadmin-get-items.md)
  -   [Wbadmin-Wiederherstellung starten](wbadmin-start-recovery.md)
  -   [Wbadmin-Status "Get"](wbadmin-get-status.md)
  -   [Wbadmin Get Disks](wbadmin-get-disks.md)
  -   [Wbadmin start Systemstatus](wbadmin-start-systemstaterecovery.md)
  -   [Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)
  -   [Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  -   [WBADMIN-START SYSRECOVERY](wbadmin-start-sysrecovery.md)
  -   [Wbadmin-Wiederherstellungs Katalog](wbadmin-restore-catalog.md)
  -   [Wbadmin delete-Katalog](wbadmin-delete-catalog.md)
- [wdsutil](wdsutil.md)
- [wecutil](wecutil.md)
- [wevtutil](wevtutil.md)
- [where](where_1.md)
- [whoami](whoami.md)
- [winnt](winnt.md)
- [winnt32](winnt32.md)
- [winpop](winpop.md)
- [winrs](winrs.md)
- [wmic](wmic.md)
- [wscript](wscript.md)

### <a name="x"></a>X
-   [xcopy](xcopy.md)
