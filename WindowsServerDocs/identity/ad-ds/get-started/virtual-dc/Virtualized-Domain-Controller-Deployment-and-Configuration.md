---
ms.assetid: b146f47e-3081-4c8e-bf68-d0f993564db2
title: Bereitstellung und Konfiguration virtualisierter Domänencontroller
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 7c2ae279a39566a30670111198d0e4840f57f6fc
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939070"
---
# <a name="virtualized-domain-controller-deployment-and-configuration"></a>Bereitstellung und Konfiguration virtualisierter Domänencontroller

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema behandelt Folgendes:

- [Überlegungen zur Installation](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_InstallConsiderations)

    Dazu zählen Plattformanforderungen und andere wichtige Einschränkungen.

- [Klonen von virtualisierten Domänencontrollern](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCCloning)

    Hier wird der gesamte Prozess für das Klonen von virtualisierten Domänencontrollern ausführlich erläutert.

- [Sichere Wiederherstellung des virtualisierten Domänencontrollers](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCSafeRestore)

    Hier werden die Überprüfungen bei der sicheren Wiederherstellung des virtualisierten Domänencontrollers ausführlich erläutert.

## <a name="installation-considerations"></a><a name="BKMK_InstallConsiderations"></a>Überlegungen zur Installation
Es gibt keine spezielle Rollen- oder Featureinstallation für virtualisierte Domänencontroller, sondern alle Domänencontroller enthalten automatisch Funktionen für das Klonen und die sichere Wiederherstellung. Sie können diese Funktionen nicht entfernen oder deaktivieren.

Für die Verwendung von Windows Server 2012-Domänencontrollern sind die Windows Server 2012 AD DS-Schemaversion 56 oder höher und eine Windows Server 2003 Native oder höher entsprechende Gesamtstrukturfunktionsebene erforderlich.

Sowohl beschreibbare als auch schreibgeschützte Domänencontroller unterstützen alle Aspekte von virtualisierten Domänencontrollern, so wie globale Kataloge und FSMO-Rollen.

> [!IMPORTANT]
> Der Halter der FSMO-Rolle für den Emulator des primären Domänencontrollers (PDC) muss online sein, wenn das Klonen beginnt.

### <a name="platform-requirements"></a><a name="BKMK_PlatformReqs"></a>Platt Form Anforderungen
Für das Klonen von virtualisierten Domänencontrollern ist Folgendes erforderlich:

- FSMO-Rolle für den PDC-Emulator, gehostet auf einem Windows Server 2012-Domänencontroller

- Verfügbarkeit des PDC-Emulators während des Klonens

Für das Klonen und die sichere Wiederherstellung ist Folgendes erforderlich:

- Virtualisierte Windows Server 2012-Gäste

- Virtualisierunghostplattform mit Unterstützung für VM-Generations-ID (VMGID)

Sehen Sie sich die Tabelle unten an, in der Sie Virtualisierungsprodukte finden und erfahren, ob diese virtualisierte Domänencontroller und die VM-Generations-ID unterstützen.

|**Virtualisierungsprodukt**|**Unterstützung für virtualisierte Domänencontroller und VMGID**|
|--|--|
|**Microsoft Windows Server 2012-Server mit Hyper-V-Feature**|Ja|
|**Microsoft Windows Server 2012 Hyper-V-Server**|Ja|
|**Microsoft Windows 8 mit Hyper-V-Clientfeature**|Ja|
|**Windows Server 2008 R2 und Windows Server 2008**|Nein|
|**Nicht von Microsoft stammende Virtualisierungslösungen**|Hersteller kontaktieren|

Zwar unterstützt Microsoft Windows 7 Virtual PC, Virtual PC 2007, Virtual PC 2004 und Virtual Server 2005, aber diese bieten keine Unterstützung für die Ausführung von 64-Bit-Gästen und die VM-Generations-ID.

Für Hilfe mit Virtualisierungsprodukten von Drittanbietern und deren Unterstützung für virtualisierte Domänencontroller wenden Sie sich direkt an den Anbieter.

Weitere Informationen finden Sie in der Supportrichtlinie für [Microsoft-Software, die in Hardwarevirtualisierungssoftware ausgeführt wird, die nicht von Microsoft stammt](https://support.microsoft.com/kb/897615).

### <a name="critical-caveats"></a>Wichtige Einschränkungen
Virtualisierte Domänencontroller bieten *keine* Unterstützung für die sichere Wiederherstellung von folgenden Elementen:

- VHD- und VHDX-Dateien, die manuell über vorhandene VHD-Dateien kopiert werden

- VHD- und VHDX-Dateien, die mit Software für Dateisicherungen oder vollständige Festplattensicherungen wiederhergestellt wurden

> [!NOTE]
> VHDX-Dateien, die neu für Windows Server 2012 Hyper-V sind

Keiner dieser Vorgänge ist unter der Semantik der VM-Generations-ID abgedeckt, deshalb wird die VM-Generations-ID nicht geändert. Die Wiederherstellung von Domänencontrollern über die Methoden kann entweder zu einem USN-Rollback oder einer Quarantäne für den Domänencontroller führen oder zu veralteten Objekten und der Anforderung für gesamtstrukturweite Bereinigungsvorgänge führen.

> [!WARNING]
> Die sichere Wiederherstellung des virtualisierten Domänencontrollers ist kein Ersatz für Systemstatussicherungen und den AD DS-Papierkorb.
>
> Nach der Wiederherstellung einer Momentaufnahme gehen die Deltas von zuvor nicht replizierten Änderungen, die nach der Momentaufnahme von diesem Domänencontroller stammen, gehen dauerhaft verloren. Die sichere Wiederherstellung implementiert eine automatisierte nicht autoritative Wiederherstellung, *nur* um eine versehentliche Domänencontrollerquarantäne zu vermeiden.

Weitere Informationen zu USN-Blasen und veralteten Objekten finden Sie unter [Problembehandlung für Active Directory-Vorgänge, bei denen der Fehler 8606 „Es wurden nicht genügend Attribute übergeben, um ein Objekt zu erstellen“ auftritt](https://support.microsoft.com/kb/2028495).

## <a name="virtualized-domain-controller-cloning"></a><a name="BKMK_VDCCloning"></a>Klonen von virtualisierten Domänencontrollern
Es gibt eine Reihe von Phasen und Schritten für das Klonen eines virtualisierten Domänencontrollers, unabhängig von der Verwendung grafischer Tools oder der Windows PowerShell. Allgemein gesagt, gibt es die drei folgenden Phasen:

**Vorbereiten der Umgebung**

- Schritt 1: Vergewissern Sie sich, dass der Hypervisor die VM-Generations-ID und damit das Klonen unterstützt.

- Schritt 2: Überprüfen Sie, ob die PDC-Emulatorrolle von einem Domänen Controller gehostet wird, auf dem Windows Server 2012 ausgeführt wird und der während des Klonens Online und erreichbar ist.

**Vorbereiten des Quelldomänencontrollers**

- Schritt 3: Autorisieren Sie den Quelldomänencontroller für das Klonen.

- Schritt 4: Entfernen Sie inkompatible Dienste oder Programme, oder fügen Sie diese zur Datei CustomDCCloneAllowList.xml hinzu.

- Schritt 5: Erstellen Sie die Datei „DCCloneConfig.xml“

- Schritt 6: Nehmen Sie den Quelldomänencontroller offline.

**Erstellen des geklonten Domänencontrollers**

- Schritt 7: Kopieren oder exportieren Sie den virtuellen Quellcomputer, und fügen Sie die XML hinzu, wenn sie nicht bereits kopiert wurde.

- Schritt 8: Erstellen Sie einen neuen virtuellen Computer aus der Kopie.

- Schritt 9: Starten Sie den neuen virtuellen Computer, um das Klonen zu beginnen.

Da es keine Unterschiede bei der Vorgehensweise gibt, wenn Sie grafische Tools wie die Hyper-V-Verwaltungskonsole oder Befehlszeilentools wie Windows PowerShell verwenden, werden die Schritte nur einmal mit beiden Oberflächen dargestellt. In diesem Thema werden Windows PowerShell-Beispiele bereitgestellt, mit denen Sie die End-to-End-Automatisierung des Klonprozesses erkunden können. Für die einzelnen Schritte sind die Beispiele nicht erforderlich. In Windows Server 2012 ist kein grafisches Verwaltungstool für virtualisierte Domänencontroller enthalten.

Es gibt verschiedene Punkte im Verfahren, an denen Sie Optionen haben, wie Sie den geklonten Computer erstellen und die XML-Dateien hinzufügen. Diese Schritte sind in den Details unten erwähnt. Ansonsten ist der Prozess unveränderbar.

Im folgenden Diagramm ist der Prozess für das Klonen des virtualisierten Domänencontrollers dargestellt, bei dem die Domäne bereits vorhanden ist.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_CloningProcessFlow.png)

### <a name="step-1---validate-the-hypervisor"></a>Schritt 1: Überprüfen des Hypervisors
Stellen Sie sicher, dass der Quelldomänencontroller auf einem unterstützten Hypervisor ausgeführt wird, indem Sie die Dokumentation des Anbieters durchsehen. Virtualisierte Domänencontroller sind hypervisorunabhängig, was bedeutet, dass Hyper-V nicht erforderlich ist.

Wenn der Hypervisor Microsoft Hyper-V ist, stellen Sie sicher, dass er unter Windows Server 2012 ausgeführt wird. Sie können dies über die Geräteverwaltung überprüfen.

Öffnen Sie **Devmgmt.msc**, und sehen Sie sich die **Systemgeräte** für installierte Microsoft Hyper-V-Geräte und -Treiber. Für einen virtualisierten Domänencontroller ist spezifisch der **Microsoft Hyper-V Generation Counter** (Treiber: vmgencounter.sys) erforderlich.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVVMGenIDCounter.png)

### <a name="step-2---verify-the-pdce-fsmo-role"></a>Schritt 2: Überprüfen der PDCE FSMO-Rolle
Bevor Sie versuchen, einen Domänencontroller zu klonen, müssen Sie überprüfen, ob auf dem Domänencontroller, der die FSMO-Rolle für den Emulator des primären Domänencontrollers hostet, Windows Server 2012 ausgeführt wird. Der PDC-Emulator (PDCE) ist aus verschiedenen Gründen erforderlich:

1. Der PDCE erstellt die spezielle Gruppe **Klonbare Domänencontroller** und legt die Berechtigungen dafür auf den Stamm der Domäne fest, damit ein Domänencontroller sich selbst klonen kann.

2. Der klonende Domänencontroller kontaktiert den PDCE direkt über das DRSUAPI RPC-Protokoll, um Computerobjekte für den geklonten Domänencontroller zu erstellen.

    > [!NOTE]
    > Windows Server 2012 erweitert das vorhandene Remoteprotokoll für den Verzeichnisreplikationsdienst (Directory Replication Service, DRS) (UUID **E3514235-4B06-11D1-AB04-00C04FC2DCD2**), um die neue RPC-Methode **IDL_DRSAddCloneDC** (Opnum **28**) einzuschließen. Die **IDL_DRSAddCloneDC**-Methode erstellt ein neues Domänencontrollerobjekt durch das Kopieren von Attributen von einem vorhandenen Domänencontrollerobjekt.
    >
    > Die Status eines Domänencontrollers setzen sich aus Computer, Server, NTDS-Einstellungen, FRS, DFSR und Verbindungsobjekten zusammen, die für jeden Domänencontroller beibehalten werden. Bei der Duplizierung eines Objekts ersetzt diese RPC-Methode alle Referenzen zum ursprünglichen Domänencontroller durch entsprechende Objekte des neuen Domänencontrollers. Der Anrufer muss über das Zugriffsrecht „DS-Clone-Domain-Controller“ im Domänennamenskontext verfügen.
    >
    > Für die Verwendung dieser neuen Methode ist immer ein direkter Zugriff auf den PDC-Emulatordomänencontroller vom Anrufer erforderlich.
    >
    > Da diese RPC-Methode neu ist, benötigt Ihre Netzwerkanalysesoftware aktualisierte Parser, um Felder für das neue Opnum 28 in die vorhandene UUID E3514235-4B06-11D1-AB04-00C04FC2DCD2 einzuschließen. Andernfalls können Sie diesen Datenverkehr nicht analysieren.
    >
    > Weitere Informationen finden Sie unter [4.1.29 IDL_DRSAddCloneDC (Opnum 28)](/openspecs/windows_protocols/ms-drsr/ef0bfb1d-037b-4626-a6d9-cc7589bc5786).

***Das bedeutet auch, dass für das Klonen eines virtualisierten Domänencontrollers bei Verwendung nicht vollständig gerouteter Netzwerke Netzwerksegmente mit Zugriff auf den PDCE erforderlich sind***. Es ist akzeptabel, einen geklonten Domänencontroller nach dem Klonen – wie einen physischen Domänencontroller – in ein anderes Netzwerk zu verschieben, solange Sie darauf achten, die Informationen zum logischen AD DS-Standort zu aktualisieren.

> [!IMPORTANT]
> Beim Klonen einer Domäne, die nur einen einzigen Domänencontroller enthält, müssen Sie sicherstellen, dass der Quelldomänencontroller wieder online ist, bevor Sie die Klonkopien starten. Eine Produktionsdomäne sollte immer mindestens zwei Domänencontroller enthalten.

#### <a name="active-directory-users-and-computers-method"></a>Methode mit Active Directory-Benutzern und -Computern

1. Klicken Sie im Dsa.msc-Snap-In mit der rechten Maustaste auf die Domäne, und klicken Sie auf **Betriebsmaster**. Notieren Sie den auf der Registerkarte PDC benannten Domänencontroller, und schließen Sie das Dialogfeld.

2. Klicken Sie mit der rechten Maustaste auf das Computerobjekt dieses Domänencontrollers, und klicken auf **Eigenschaften**. Überprüfen Sie dann die Betriebssysteminformationen.

#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Sie können die folgenden Cmdlets des Active Directory Windows PowerShell-Moduls verwenden, um die Version des PDC-Emulators zurückzugeben:

```
Get-adddomaincontroller
Get-adcomputer
```

Wenn diesen Cmdlets die Domain nicht bereitgestellt wird, gehen sie von der Domäne des Computers aus, auf denen sie ausgeführt werden.

Der folgende Befehl gibt PDCE- und Betriebssysteminformationen zurück:

```
get-adcomputer(Get-ADDomainController -Discover -Service "PrimaryDC").name -property * | format-list dnshostname,operatingsystem,operatingsystemversion
```

Im unten stehenden Beispiel wird das Angeben des Domänennamens und Filtern der zurückgegebenen Eigenschaften vor der Windows PowerShell-Pipeline dargestellt:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PDCOSInfo.png)

### <a name="step-3---authorize-a-source-dc"></a>Schritt 3: Autorisieren eines Quelldomänencontrollers
Der Quelldomänencontroller muss über das Zugriffsrecht **Domänencontroller die Erstellung eines Klons von sich selbst erlauben** auf dem Namenskontextkopf der Domäne verfügen. Standardmäßig verfügt die bekannte Gruppe **Klonbare Domänencontroller** über diese Berechtigung und enthält keine Mitglieder. Der PDCE erstellt diese Gruppe, wenn diese FSMO-Rolle an einen Windows Server 2012-Domänencontroller übertragen wird.

#### <a name="active-directory-administrative-center-method"></a>Methode mit dem Active Directory-Verwaltungscenter

1. Starten Sie Dsac.exe, und navigieren Sie zum Quelldomänencontroller. Öffnen Sie dann die Detailseite.

2. Fügen Sie im Abschnitt **Mitglied von** die Gruppe **Klonbare Domänencontroller** für die Domäne hinzu.

#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Sie können die Cmdlets **get-adcomputer** und **add-adgroupmember** des Active Directory Windows PowerShell-Moduls kombinieren, um einen Domänencontroller zur Gruppe **Klonbare Domänencontroller** hinzuzufügen:

```
Get-adcomputer <dc name> | %{add-adgroupmember "cloneable domain controllers" $_.samaccountname}
```

Damit wird beispielsweise der Server DC1 zur Gruppe hinzugefügt, ohne dass Sie den Distinguished Name des Gruppenmitglieds angeben müssen:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_AddDcToGroup.png)

#### <a name="rebuilding-default-permissions"></a>Neuerstellung der Standardberechtigungen
Wenn Sie diese Berechtigung vom Domänenkopf entfernen, schlägt das Klonen fehl. Sie die Berechtigung über das Active Directory-Verwaltungscenter oder Windows PowerShell erneut erstellen.

##### <a name="active-directory-administrative-center-method"></a>Methode mit dem Active Directory-Verwaltungscenter

1. Öffnen Sie das **Active Directory-Verwaltungscenter**, klicken Sie mit der rechten Maustaste auf den Domänenkopf, klicken Sie auf **Eigenschaften**, klicken Sie auf die Registerkarte **Erweiterungen**, klicken Sie auf **Sicherheit**, und klicken Sie dann auf **Erweitert**. Klicken Sie auf **Nur dieses Objekt**.

2. Klicken Sie auf **Hinzufügen**, und geben Sie unter **Geben Sie die zu verwendenden Objektnamen ein** den Gruppennamen **Klonbare Domänencontrollers** ein.

3. Klicken Sie unter Berechtigungen auf **Domänencontroller die Erstellung eines Klons von sich selbst erlauben**, und klicken Sie dann auf **OK**.

> [!NOTE]
> Sie können auch die Standardberechtigung entfernen und individuelle Domänencontroller hinzufügen. Da wird wahrscheinlich jedoch fortlaufende Wartungsprobleme nach sich ziehen, bei denen neuen Administratoren diese Anpassung nicht bewusst ist. Das Ändern der Standardeinstellung sorgt nicht für mehr Sicherheit und wird nicht empfohlen.

##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Verwenden Sie die folgenden Befehle an einer Eingabeaufforderung mit Administratorrechten der Windows PowerShell-Konsole. Diese Befehle erkennen den Domänennamen und fügen ihn zurück die Standardberechtigungen ein:

```
import-module activedirectory
cd ad:
$domainNC = get-addomain
$dcgroup = get-adgroup "Cloneable Domain Controllers"
$sid1 = (get-adgroup $dcgroup).sid
$acl = get-acl $domainNC
$objectguid = new-object Guid 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e
$ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid1,"ExtendedRight","Allow",$objectguid
$acl.AddAccessRule($ace1)
set-acl -aclobject $acl $domainNC
cd c:
```

Alternativ können Sie das Beispiel [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms) in einer Windows PowerShell-Konsole, woraufhin die Konsole einen erweiterten Administrator auf einem Domänencontroller in der betroffenen Domäne startet. Die Berechtigungen werden automatisch festgelegt. Das Beispiel befindet sich im Anhang dieses Moduls.

### <a name="step-4---remove-incompatible-applications-or-services-if-not-using-customdccloneallowlistxml"></a>Schritt 4: Entfernen inkompatibler Anwendungen oder Dienste (wenn CustomDCCloneAllowList.xml nicht verwendet wird)
Alle Programme oder Dienste, die zuvor von Get-ADDCCloningExcludedApplicationList zurückgegeben und *nicht zu CustomDCCloneAllowList.xml hinzugefügt wurden*, müssen vor dem Klonen entfernt werden. Die empfohlene Methode ist das Deinstallieren der Anwendung oder des Diensts.

> [!WARNING]
> Alle inkompatiblen Programme oder Dienste, die nicht deinstalliert oder zu CustomDCCloneAllowList.xml hinzugefügt werden, verhindern das Klonen.

Verwenden Sie das Cmdlet Get-AdComputerServiceAccount, um nach eigenständigen verwalteten Dienstkonten in der Domäne zu suchen und festzustellen, ob dieser Computer diese verwendet. Wenn verwaltete Dienstkonten installiert sind, verwenden Sie das Cmdlet Uninstall-ADServiceAccount, um das lokal installierte Dienstkonto zu entfernen. Wenn Sie Schritt 6 abgeschlossen und den Quelldomänencontroller offline gestellt haben, können Sie den MSA über Install-ADServiceAccount erneut hinzufügen, wenn der Server wieder online ist. Weitere Informationen finden Sie unter [Uninstall-ADServiceAccount](/openspecs/windows_protocols/ms-drsr/ef0bfb1d-037b-4626-a6d9-cc7589bc5786).

> [!IMPORTANT]
> Eigenständige MSAs, die zuerst in Windows Server 2008 R2 eingeführt wurden, wurden in Windows Server 2012 durch Gruppen-MSAs ersetzt. Gruppen-MSAs unterstützen das Klonen.

### <a name="step-5---create-dccloneconfigxml"></a>Schritt 5: Erstellen der Datei DCCloneConfig.xml
Die Datei DcCloneConfig.xml ist für das Klonen von Domänencontrollern erforderlich. Ihre Inhalte ermöglichen Ihnen, eindeutige Details wie den Namen und die IP-Adresse des neuen Computers anzugeben.

Die Datei CustomDCCloneAllowList.xml ist optional, solange Sie keine Anwendungen oder potenziell inkompatiblen Windows-Dienste auf dem Quelldomänencontroller installieren. Für die Dateien ist eine präzise Benennung, Formatierung und Platzierung erforderlich, da andernfalls das Klonen fehlschlägt.

Aus diesem Grund sollten Sie immer die Windows PowerShell-Cmdlets verwenden, um die XML-Dateien zu erstellen und am korrekten Standort zu platzieren.

#### <a name="generating-with-new-addccloneconfigfile"></a>Generieren mit New-ADDCCloneConfigFile
Das Active Directory Windows PowerShell-Modul enthält ein neues Cmdlet in Windows Server 2012:

```
New-ADDCCloneConfigFile
```

Sie führen das Cmdlet auf dem vorgeschlagenen Quelldomänencontroller aus, den Sie klonen möchten. Das Cmdlet unterstützt mehrere Argumente und testet bei Verwendung immer den Computer und die Umgebung, auf dem bzw. in der es ausgeführt wurde, es sei denn, Sie geben das -offline-Argument an.

|**ActiveDirectory**<p>**Cmdlet**|**Argumente**|**Erklärung**|
|--|--|--|
|**New-ADDCCloneConfigFile**|*<no argument specified>*|Erstellt eine leere „DcCloneConfig.xml“-Datei im DSA-Arbeitsverzeichnis (Standard: %systemroot%\ntds)|
||-CloneComputerName|Gibt den Computernamen des geklonten Domänencontrollers an. String-Datentyp|
||-Path|Gibt den Ordner für die Erstellung der DcCloneConfig.xml-Datei an. Falls nicht angegeben, wird die Datei in das DSA-Arbeitsverzeichnis (Standard: %systemroot%\ntds) geschrieben. String-Datentyp|
||-SiteName|Gibt den logischen AD-Standortnamen an, dem während der Erstellung des geklonten Computerkontos beigetreten wird. String-Datentyp|
||-IPv4Address|Gibt die statische IPv4-Adresse des geklonten Computers an. String-Datentyp|
||-IPv4SubnetMask|Gibt die statische IPv4-Subnetzmaske des geklonten Computers an. String-Datentyp|
||-IPv4DefaultGateway|Gibt die statische IPv4-Standardgatewayadresse des geklonten Computers an. String-Datentyp|
||-IPv4DNSResolver|Gibt die statischen IPv4-DNS-Einträge des geklonten Computers in einer durch Trennzeichen getrennten Liste an. Arraydatentyp. Bis zu vier Einträge können bereitgestellt werden.|
||-PreferredWINSServer|Gibt die statische IPv4-Adresse des primären WINS-Computers an. String-Datentyp|
||-AlternateWINSServer|Gibt die statische IPv4-Adresse des sekundären WINS-Computers an. String-Datentyp|
||-IPv6DNSResolver|Gibt die statischen IPv6-DNS-Einträge des geklonten Computers in einer durch Trennzeichen getrennten Liste an. Es gibt keine Möglichkeit, um statische IPv6-Informationen beim Klonen von virtualisierten Domänencontrollern festzulegen. Arraydatentyp.|
||-Offline|Führt keine Validierungstests durch und überschreibt jede vorhandene dccloneconfig.xml-Datei. Hat keine Parameter.|
||*-Statisch*|Erforderlich, wenn die statischen IP-Argumente IPv4SubnetMask, IPv4SubnetMask oder IPv4DefaultGateway angegeben werden. Hat keine Parameter.|

Bei Ausführung im Onlinemodus durchgeführte Tests:

- PDC-Emulator ist Windows Server 2012 oder höher

- Quelldomänencontroller ist Mitglied der Gruppe „Klonbare Domänencontroller“

- Quelldomänencontroller enthält keine ausgeschlossenen Anwendungen oder Dienste

- Quelldomänencontroller enthält noch keine DcCloneConfig.xml-Datei am angegebenen Pfad

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewDCCloneConfig.png)

### <a name="step-6---take-the-source-domain-controller-offline"></a>Schritt 6: Quelldomänencontroller offline nehmen
Sie können keinen laufenden Quelldomänencontroller kopieren, sondern er muss ordnungsgemäß heruntergefahren werden. Sie sollten niemals einen Domänencontroller klonen, der durch einen nicht ordnungsgemäßen Stromverlust angehalten wurde.

#### <a name="graphical-method"></a>Grafische Methode
Verwenden Sie die Schaltfläche zum Herunterfahren im ausgeführten Domänencontroller oder die Schaltfläche zum Herunterfahren im Hyper-V-Manager.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_Shutdown.png)

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVShutdown.png)

#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Sie können einen virtuellen Computer über eins der folgenden Cmdlets herunterfahren:

```
Stop-computer
Stop-vm
```

Stop-computer ist ein Cmdlet, das das Herunterfahren von Computern unabhängig von der Virtualisierung unterstützt, und entspricht dem Vorversionsdienstprogramm Shutdown.exe. Stop-vm ist ein neues Cmdlet im Windows Server 2012 Hyper-V Windows PowerShell-Modul, das den Energieoptionen im Hyper-V-Manager entspricht. Letztere Option ist nützlich in Laborumgebungen, in denen Domänencontroller oft in einem privaten virtualisierten Netzwerk betrieben werden.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopComputer2.png)

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopVM.png)

### <a name="step-7---copy-disks"></a>Schritt 7: Kopieren von Datenträgern
In der Kopierphase ist eine administrative Entscheidung erforderlich:

- Manuelles Kopieren der Datenträger ohne Hyper-V

- Exportieren des virtuellen Computers mithilfe von Hyper-V

- Exportieren der zusammengeführten Datenträger mithilfe von Hyper-V

Alle Datenträger eines virtuellen Computers müssen kopiert werden, nicht nur das Systemlaufwerk. Wenn der Quelldomänencontroller verschiedene Datenträger verwendet und Sie planen, Ihren geklonten Domänencontroller auf einen anderen Hyper-V-Host zu verschieben, müssen Sie exportieren.

Das manuelle Kopieren von Datenträgern wird empfohlen, wenn der Domänencontroller nur über *ein* Laufwerk verfügt. Das Exportieren/Importieren wird für virtuelle Computer mit *mehreren* Laufwerken oder anderen komplexen virtuellen Hardwareanpassungen wie mehreren NICs empfohlen.

Wenn Sie Dateien manuell kopieren, löschen Sie vor dem Kopieren alle Momentaufnahmen. Wenn Sie den virtuellen Computer exportieren, löschen Sie Momentaufnahmen vor dem Exportieren oder nach dem Importieren von dem neuen virtuellen Computer.

> [!WARNING]
> Momentaufnahmen sind unterschiedliche Datenträger, die einen Domänencontroller in einen früheren Status zurücksetzen können. Wenn Sie einen Domänencontroller klonen und dann seine Momentaufnahme vor dem Klonen wiederherstellen würden, hätten Sie duplizierte Domänencontroller in der Gesamtstruktur. Frühere Momentaufnahmen auf einem neu geklonten Domänencontroller haben keinen Nutzen.

#### <a name="manually-copying-disks"></a>Manuelles Kopieren von Datenträgern

##### <a name="hyper-v-manager-method"></a>Methode mit dem Hyper-V-Manager
Verwenden Sie das Hyper-V-Manager-Snap-In, um zu ermitteln, welche Datenträger mit dem Quelldomänencontroller verbunden sind. Verwenden Sie Überprüfungsoption, um zu prüfen, ob der Domänencontroller unterschiedliche Datenträger verwendet (dann müssten Sie auch den übergeordneten Datenträger kopieren).

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVInspect.png)

Zum Lösungen von Momentaufnahmen wählen Sie einen virtuellen Computer aus und löschen die Momentaufnahmeunterstruktur.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDeleteSnapshot.gif)

Sie können dann die VHD- oder VHDX-Dateien über Windows Explorer, Xcopy.exe oder Robocopy.exe manuell kopieren. Es sind keine speziellen Schritte erforderlich. Als bewährte Methode sollten Sie die Dateinamen ändern, selbst wenn Sie die Dateien in einen anderen Ordner verschieben.

> [!NOTE]
> Wenn Sie zwischen Hostcomputern in einem LAN (1-GBit oder größer) kopieren, kopiert die Option **Xcopy.exe /J** VHD-/VHDX-Dateien deutlich schneller als jedes andere Tool, allerdings zum Preis einer wesentlich höheren Bandbreitennutzung.

##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Zum Ermitteln der Datenträger, die Windows PowerShell verwenden, benutzen Sie die Hyper-V-Module:

```
Get-vmidecontroller
Get-vmscsicontroller
Get-vmfibrechannelhba
Get-vmharddiskdrive
```

Sie können beispielsweise mit dem folgenden Beispiel alle IDE-Festplattenlaufwerke von einem virtuellen Computer mit dem Namen **DC2** zurückgeben:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_ReturnIDE.png)

Wenn der Datenträgerpfad auf eine AVHD- oder AVHDX-Datei verweist, handelt es sich um eine Momentaufnahme. Zum Löschen der mit einem Datenträger verbundenen Momentaufnahmen und Zusammenführen der realen VHD- oder VHDX-Dateien verwenden Sie die Cmdlets:

```
Get-VMSnapshot
Remove-VMSnapshot
```

So löschen Sie beispielsweise alle Momentaufnahmen von einem virtuellen Computer namens DC2-SOURCECLONE:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_DelSnapshots.png)

Verwenden Sie zum Kopieren der Dateien mithilfe von Windows PowerShell das folgende Cmdlet:

```
Copy-Item
```

Kombinieren Sie dies mit Cmdlets des virtuellen Computers in Pipelines, um die Automatisierung zu unterstützen. Pipelines sind Kanäle zur Datenübergabe zwischen mehreren Cmdlets. So können Sie beispielsweise das Laufwerk eines Offline-Quelldomänencontrollers namens DC2-SOURCECLONE auf einen neuen Datenträger namens c:\temp\copy.vhd kopieren, ohne des exakten Pfad zu seinem Systemlaufwerk kennen zu müssen:

```
Get-VMIdeController dc2-sourceclone | Get-VMHardDiskDrive | select-Object {copy-item -path $_.path -destination c:\temp\copy.vhd}
```

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSCopyDrive.png)

> [!IMPORTANT]
> Sie können beim Klonen Passthru-Datenträger verwenden, da diese keine virtuelle Datenträgerdatei, sondern eine tatsächliche Festplatte benutzen.

> [!NOTE]
> Weitere Informationen zu Windows PowerShell-Vorgängen mit Pipelines finden Sie unter [Piping und die Pipeline in Windows PowerShell](/previous-versions/windows/it-pro/windows-powershell-1.0/ee176927(v=technet.10)).

#### <a name="exporting-the-vm"></a>Exportieren des virtuellen Computers
Alternativ zum Kopieren der Datenträger können Sie den gesamten virtuellen Hyper-V-Computer als Kopie exportieren. Beim Exportieren wird automatisch ein für den virtuellen Computer benannter Ordner erstellt, der alle Datenträger und Konfigurationsinformationen enthält.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVExport.png)

##### <a name="hyper-v-manager-method"></a>Methode mit dem Hyper-V-Manager
So exportieren Sie einen virtuellen Computer mit Hyper-V-Manager:

1. Klicken Sie mit der rechten Maustaste auf den Domänencontroller, und klicken Sie auf **Exportieren**.

2. Wählen Sie einen vorhandenen Ordner als Exportcontainer aus.

3. Warten Sie, bis in der Statusspalte nicht mehr **Wird exportiert** angezeigt wird.

##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Verwenden Sie zum Exportieren eines virtuellen Computers mit dem Hyper-V Windows PowerShell-Modul das Cmdlet:

```
Export-vm
```

So exportieren Sie beispielsweise einen virtuellen Computer namens DC2-SOURCECLONE an einen Ordner namens C:\VM:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSExport.png)

> [!NOTE]
> Windows Server 2012 Hyper-V unterstützt neue Export- und Importfunktionen, die über den Rahmen dieses Trainings hinausgehen. Weitere Informationen finden Sie auf der TechNet-Website.

#### <a name="exporting-merged-disks-using-hyper-v"></a>Exportieren der zusammengeführten Datenträger mithilfe von Hyper-V
Die letzte Option besteht darin, die Datenträgerzusammenführungs- und Konvertierungsoptionen in Hyper-V zu verwenden. Damit können Sie eine Kopie einer vorhanden Datenträgerstruktur auf einem einzigen neue Datenträger erstellen, selbst wenn AVHD-/AVHDX-Momentaufnahmendateien enthalten sind. Wie beim manuellen Datenträger Kopier Szenario ist dies hauptsächlich für einfachere virtuelle Computer vorgesehen, die nur ein einziges Laufwerk verwenden, z. b. "C:" \\ . Der einzige Vorteil ist, dass Sie hier im Gegensatz zum manuellen Kopieren nicht erst Momentaufnahmen löschen müssen. Dieser Vorgang ist natürlich langsamer als das einfache Löschen der Momentaufnahmen und das Kopieren von Datenträgern.

##### <a name="hyper-v-manager-method"></a>Methode mit dem Hyper-V-Manager
So erstellen Sie einen zusammengeführten Datenträger mit Hyper-V-Manager:

1. Klicken Sie auf Datenträger **Bearbeiten**.

2. Suchen Sie nach dem niedrigsten untergeordneten Datenträger. Wenn Sie beispielsweise einen differenzierenden Datenträger verwenden, die der untergeordnete Datenträger der niedrigste untergeordnete Datenträger. Wenn der virtuelle Computer über eine Momentaufnahme (oder mehrere) verfügt, ist die aktuell ausgewählte Momentaufnahme der niedrigste untergeordnete Datenträger.

3. Wählen Sie die Option **Zusammenführen** aus, um aus der gesamten Struktur aus übergeordneten und untergeordneten Datenträgern einen einzigen Datenträger zu erstellen.

4. Wählen Sie eine neue virtuelle Festplatte aus, und geben Sie einen Pfad an. Damit werden die vorhandenen VHD-/VHDX-Dateien ein eine einzige neue portable Einheit aufgelöst, bei der kein Risiko besteht, dass frühere Momentaufnahmen wiederhergestellt werden.

##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Verwenden Sie zum Erstellen eines zusammengeführten Datenträgers aus einer komplexen Sammlung von übergeordneten Datenträgern mithilfe des Hyper-V Windows PowerShell-Moduls das Cmdlet:

```
Convert-vm
```

So exportieren Sie beispielsweise die gesamte Kette der Festplattenmomentaufnahmen eines virtuellen Computers (dieses Mal ohne differenzierende Datenträger) und den übergeordneten Datenträger an einen neuen einzelnen Datenträger namens DC4-CLONED.VHDX:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSConvertVhd.png)

#### <a name="adding-xml-to-the-offline-system-disk"></a><a name="BKMK_Offline"></a>Hinzufügen der XML zum Offlinesystemdatenträger
Wenn Sie die Datei Dccloneconfig.xml auf den ausgeführten Quelldomänencontroller kopiert haben, müssen Sie jetzt die aktualisierte dccloneconfig.xml-Datei an den kopierten/exportierten Offlinesystemdatenträger kopieren. Je nachdem, welche installierten Anwendungen zuvor mit Get-ADDCCloningExcludedApplicationList erkannt wurden, müssen Sie möglicherweise auch die Datei CustomDCCloneAllowList.xml auf den Datenträger kopieren.

Die Datei DcCloneConfig.xml kann sich an den folgenden Speicherorten befinden:

1. DSA-Arbeitsverzeichnis

2. %windir%\NTDS

3. Lese-/Schreib-Wechselmedien in der Reihenfolge des Laufwerkbuchstabens, im Stamm des Laufwerks

Diese Pfade sind nicht konfigurierbar. Wenn das Klonen begonnen hat, werden diese Speicherorte in dieser spezifischen Reihenfolge überprüft und die zuerst gefundene DcCloneConfig.xml-Datei wird verwendet, unabhängig von Inhalten der anderen Ordner.

Die Datei CustomDCCloneAllowList.xml kann sich an den folgenden Speicherorten befinden:

1. HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters

    AllowListFolder (*REG_SZ*)

2. DSA-Arbeitsverzeichnis

3. %windir%\NTDS

4. Lese-/Schreib-Wechselmedien in der Reihenfolge des Laufwerkbuchstabens, im Stamm des Laufwerks

Sie können New-ADDCCloneConfigFile mit dem Argument **-offline** ausführen (das auch als Offlinemodus bezeichnet wird), um die Datei DcCloneConfig.xml zu erstellen und an einem korrekten Speicherort zu platzieren. Im folgenden Beispiel ist gezeigt, wie Sie New-ADDCCloneConfigFile im Offlinemodus ausführen.

Um einen geklonten Domänen Controller mit dem Namen CloneDC1 im Offline Modus zu erstellen, geben Sie an einer Website mit dem Namen "Redmond" mit statischer IPv4-Adresse

```
New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS
```

Zum Erstellen eines geklonten Domänencontrollers mit dem Namen %%amp;quot;Clone2%%amp;quot; im Offlinemodus mit statischen IPv4- und IPv6-Einstellungen geben Sie Folgendes ein:

```
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS
```

Zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit statischen IPv4- und dynamischen IPv6-Einstellungen und zum Angeben mehrerer DNS-Server für die DNS-Auflösungseinstellungen geben Sie Folgendes ein:

```
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS
```

Zum Erstellen eines geklonten Domänencontrollers mit dem Namen %%amp;quot;Clone1%%amp;quot; im Offlinemodus mit statischen IPv4- und IPv6-Einstellungen geben Sie Folgendes ein:

```
New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS
```

Zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit dynamischen IPv4- und IPv6-Einstellungen geben Sie Folgendes ein:

```
New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS

```

##### <a name="windows-explorer-method"></a>Windows Explorer-Methode
Windows Server 2012 bietet jetzt eine grafische Option für das Bereitstellen von VHD- und VHDX-Dateien. Dafür ist die Installation des Desktopdarstellungsfeatures in Windows Server 2012 erforderlich.

1. Klicken Sie auf die neu kopierte VHD-/VHDX-Datei, die das Systemlaufwerk des Quelldomänencontrollers oder den Speicherortordner des DSA-Arbeitsverzeichnisses enthält, und klicken Sie dann im Menü **Datenträgerimagetools** auf**Bereitstellen**.

2. Kopieren Sie im jetzt bereitgestellten Laufwerk die XML-Dateien an einen gültigen Speicherort. Möglicherweise werden Sie aufgefordert, Berechtigungen für den Ordner zu bestätigen.

3. Klicken Sie auf das bereitgestellte Laufwerk, und klicken Sie im Menü **Datenträgertools** auf **Auswerfen**.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVClickMountedDrive.png)

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDetailsMountedDrive.gif)

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVEjectMountedDrive.gif)

##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Alternativ können Sie das Offlinelaufwerk bereitstellen und die XML-Datei über die folgenden Windows PowerShell-Cmdlets kopieren:

```
mount-vhd
get-disk
get-partition
get-volume
Add-PartitionAccessPath
Copy-Item
```

Damit erhalten Sie die vollständige Kontrolle über den Prozess. Sie können beispielsweise das Laufwerk mit einem bestimmten Laufwerksbuchstaben bereitstellen, die Datei kopieren und die Bereitstellung des Laufwerks aufheben.

```
mount-vhd <disk path> -passthru -nodriveletter | get-disk | get -partition | get-volume | get-partition | where {$_.partition number -eq 2} | Add-PartitionAccessPath -accesspath <drive letter>

copy-item <xml file path><destination path>\dccloneconfig.xml

dismount-vhd <disk path>
```

Beispiel:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSMountVHD.png)

Alternativ können Sie mit dem neuen Cmdlet **Mount-DiskImage** eine VHD-Datei (oder ISO-Datei) bereitstellen.

### <a name="step-8---create-the-new-virtual-machine"></a>Schritt 8: Erstellen des neuen virtuellen Computers
Der letzte Konfigurationsschritt vor Beginn des Klonprozesses ist das Erstellen eines neuen virtuellen Computers, der die Datenträger aus dem kopierten Quelldomänencontroller verwendet. Je nach Ihrer Auswahl beim Kopieren der Datenträger haben Sie zwei Optionen:

1. Zuordnen eines neuen virtuellen Computers zum kopierten Datenträger

2. Importieren des exportierten virtuellen Computers

#### <a name="associating-a-new-vm-with-copied-disks"></a>Zuordnen eines neuen virtuellen Computers zu kopierten Datenträgern
Wenn Sie die Systemdatenträger manuell kopiert haben, müssen Sie einen neuen virtuellen Computer unter Verwendung des kopierten Datenträgers erstellen. Der Hypervisor legt die VM-Generations-ID bei der Erstellung eines neuen virtuellen Computers automatisch fest, sodass keine Konfigurationsänderungen im virtuellen Computer oder dem Hyper-V-Host erforderlich sind.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVConnectVHD.gif)

##### <a name="hyper-v-manager-method"></a>Methode mit dem Hyper-V-Manager

1. Erstellen Sie einen neuen virtuellen Computer.

2. Geben Sie den Namen, den Arbeitsspeicher und das Netzwerk für den virtuellen Computer an.

3. Geben Sie auf der Seite zum Verbinden der virtuellen Festplatte den kopierten Systemdatenträger an.

4. Schließen Sie den Assistenten ab, um den virtuellen Computer zu erstellen.

Wenn mehrere Datenträger, Netzwerkadapter oder andere Anpassungen vorhanden waren, konfigurieren Sie diese, bevor Sie den Domänencontroller starten. Für komplexe virtuelle Computer wird die Export-Import-Methode für das Kopieren von Datenträgern empfohlen.

##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Sie können das Hyper-V Windows PowerShell-Modul verwenden, um die Erstellung eines virtuellen Computers in Windows Server 2012 mit dem folgenden Cmdlet zu automatisieren:

```
New-VM
```

Hier wird beispielsweise der virtuelle Computer DC4-CLONEDFROMDC2 VM mit 1 GB RAM erstellt, der von der Datei c:\vm\dc4-systemdrive-clonedfromdc2.vhd gestartet wird und das virtuelle Netzwerk 10.0 verwendet:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewVM.png)

#### <a name="import-vm"></a>VM importieren
Wenn Sie Ihren virtuellen Computer zuvor exportiert haben, müssen Sie ihn jetzt als Kopie zurück importieren. Dabei wird die exportierte XML-Datei verwendet, um den Computer mit allen vorherigen Einstellungen, Laufwerken, Netzwerken und Arbeitsspeichereinstellungen erneut zu erstellen.

Wenn Sie beabsichtigen, zusätzliche Kopien von demselben exportierten virtuellen Computer zu erstellen, erstellen Sie so viele Kopien des virtuellen Computers wie erforderlich. Verwenden Sie dann den Importvorgang für jede Kopie.

> [!IMPORTANT]
> Es ist wichtig, die Option **Kopieren** zu verwenden, da beim Exportieren all Informationen von der Quelle beibehalten werden. Wenn Sie den Server mit **Verschieben** oder **Überschreiben** importieren, kommt es bei Ausführung auf dem Hyper-V-Hostserver zu einer Informationskollision.

##### <a name="hyper-v-manager-method"></a>Methode mit dem Hyper-V-Manager
So importieren Sie mit dem Hyper-V-Manager-Snap-In:

1. Klicken Sie auf **Virtuellen Computer importieren**.

2. Wählen Sie auf der Seite **Ordner suchen** die Definitionsdatei des exportierten virtuellen Computers über die Schaltfläche zum Durchsuchen aus.

3. Klicken Sie auf der Seite **Virtuellen Computer auswählen** auf den Quellcomputer.

4. Klicken Sie auf der Seite **Importtyp auswählen** auf **Virtuellen Computer kopieren (neue eindeutige ID erstellen)**, und klicken Sie dann auf **Fertig stellen**.

5. Benennen Sie den importierten virtuellen Computer um, wenn Sie auf demselben Hyper-V-Host importieren, da er denselben Namen hat wie der exportierte Quelldomänencontroller.

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportLocateFolder.png)

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportSelectVM.png)

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportChooseType.gif)

Denken Sie daran, alle importierten Momentaufnahme über das Hyper-V-Verwaltungs-Snap-In zu entfernen:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportDelSnap.gif)

> [!WARNING]
> Das Löschen aller importierten Momentaufnahmen ist äußerst wichtig, da sie bei Anwendung den geklonten Domänencontroller in den Status eines früheren, möglicherweise Livedomänencontrollers zurücksetzen würden, was zu Replikationsfehlern, doppelten IP-Informationen und anderen Unterbrechungen führen würde.

##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode
Sie können das Hyper-V Windows PowerShell-Modul verwenden, um das Importieren eines virtuellen Computers in Windows Server 2012 mit den folgenden Cmdlets zu automatisieren:

```
Import-VM
Rename-VM
```

Hier wird beispielsweise der exportierte virtuelle Computer VM DC2-CLONED mit seiner automatisch ermittelten XML-Datei importiert und dann unmittelbar in seinen neuen virtuellen Computernamen DC5-CLONEDFROMDC2 umbenannt:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSImportVM.png)

Denken Sie daran, alle importierten Momentaufnahme über die folgenden Cmdlets zu entfernen:

```
Get-VMSnapshot
Remove-VMSnapshot
```

Beispiel:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSGetVMSnap.png)

> [!WARNING]
> Stellen Sie sicher, dass dem Quelldomänencontroller beim Importieren des Computers keine statischen MAC-Adressen zugewiesen wurden. Wenn ein Quellcomputer mit einer statischen MAC-Adresse geklont wird, können diese kopierten Computer Netzwerkdatenverkehr nicht ordnungsgemäß senden oder empfangen. Legen Sie in diesem Fall eine neue eindeutige statische oder dynamische MAC-Adresse fest. Sie können mit dem folgenden Befehl anzeigen, ob ein virtueller Computer eine statische MAC-Adresse verwendet:
>
> **Get-VM-VMName** ** *Test-VM* | Get-vmnetworkadapter | ktion\\***

### <a name="step-9---clone-the-new-virtual-machine"></a>Schritt 9: Klonen des neuen virtuellen Computers
Starten Sie optional vor Beginn des Klonprozesses den geklonten Offline-Quelldomänencontroller neu. Stellen Sie sicher, dass der PDC-Emulator unabhängig davon online ist.

Zum Beginnen des Klonprozess starten Sie einfach den neuen virtuellen Computer. Der Prozess wird automatisch initiiert, und der Domänencontroller wird nach Abschluss des Klonens automatisch neu gestartet.

> [!IMPORTANT]
> Sie sollten Domänencontroller nicht für einen längeren Zeitraum ausgeschaltet lassen, und wenn der Klon demselben Standort hinzugefügt wird wie der Quelldomänencontroller, dauert der Aufbau der anfänglichen internen und standortübergreifenden Replikationstopologie möglicherweise länger, wenn der Quelldomänencontroller offline ist.

Wenn Sie Windows PowerShell zum Starten eines virtuellen Computers verwenden, wird das folgende Cmdlet verwendet:

```
Start-VM
```

Beispiel:

![Virtualisierte DC-Bereitstellung](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSStartVM.png)

Wenn der Computer nach dem Klonen neu gestartet wird, ist er ein Domänencontroller, und Sie können sich normal anmelden, um den ordnungsgemäßen Betrieb zu bestätigen. Falls Fehler auftreten, ist der Server dafür eingerichtet, im Verzeichnisdienst-Wiederherstellungsmodus zu starten, um die Fehler zu untersuchen.

## <a name="virtualization-safeguards"></a><a name="BKMK_VDCSafeRestore"></a>Virtualisierungssicherheitsmaßnahmen
Im Gegensatz zum Klonen virtualisierter Domänencontroller haben die Windows Server 2012-Virtualisierungssicherheitsmaßnahmen keine Konfigurationsschritte. Das Feature funktioniert ohne Eingriffe, solange Sie einige einfache Bedingungen einhalten:

- Der Hypervisor unterstützt die VM-Generations-ID.

- Es gibt einen gültigen Partnerdomänencontroller, von dem ein wiederhergestellter Domänencontroller nicht autoritativ Änderungen replizieren kann.

### <a name="validate-the-hypervisor"></a>Überprüfen des Hypervisors
Stellen Sie sicher, dass der Quelldomänencontroller auf einem unterstützten Hypervisor ausgeführt wird, indem Sie die Dokumentation des Anbieters durchsehen. Virtualisierte Domänencontroller sind hypervisorunabhängig, was bedeutet, dass Hyper-V nicht erforderlich ist.

Sehen Sie sich den vorherigen Abschnitt [Plattformanforderungen](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_PlatformReqs) für bekannte VM-Generations-ID-Unterstützung noch einmal an.

Wenn Sie virtuelle Computer von einem Quellhypervisor zu einem anderen Zielhypervisor migrieren, werden möglicherweise Virtualisierungssicherheitsmaßnahmen ausgelöst oder nicht, je nachdem, ob die Hypervisors die VM-Generations-ID unterstützt, wie in der folgenden Tabelle erklärt.

|Quellhypervisor|Zielhypervisor|Ergebnis|
|---------------------|---------------------|----------|
|Unterstützung für VM-Generations-ID|Keine Unterstützung für VM-Generations-ID|Keine Auslösung von Sicherheitsmaßnahmen (wenn eine DCCloneConfigFile.xml-Datei vorhanden ist, wird der Domänencontroller im DSRM gestartet)|
|Keine Unterstützung für VM-Generations-ID|Unterstützung für VM-Generations-ID|Auslösung von Sicherheitsmaßnahmen|
|Unterstützung für VM-Generations-ID|Unterstützung für VM-Generations-ID|Keine Auslösung von Sicherheitsmaßnahmen, da sich die Definition des virtuellen Computer nicht geändert hat, was bedeutet, dass die VM-Generations-ID dieselbe bleibt|

### <a name="validate-the-replication-topology"></a>Überprüfen der Replikationstopologie
Virtualisierungssicherheitsmaßnahmen initiieren eine nicht autoritative eingehende Replikation für das Delta der Active Directory-Replikation sowie eine nicht autoritative erneute Synchronisierung aller SYSVOL-Inhalte. Damit wird sichergestellt, dass der Domänencontroller mit voller Funktionalität aus einer Momentaufnahme zurückkehrt und letztendlich konsistent mit der restlichen Umgebung ist.

Diese neue Funktion zieht einige Anforderungen und Einschränkungen nach sich:

- Ein wiederhergestellter Domänencontroller muss einen beschreibbaren Domänencontroller kontaktieren können.

- Es dürfen nicht alle Domänencontroller in einer Domäne wiederhergestellt werden.

- Alle Änderungen, die von einem wiederhergestellten Domänencontroller stammen und seit Erstellung der Momentaufnahme noch nicht ausgehend repliziert wurden, sind für immer verloren.

Zwar werden diese Szenarien auch im Abschnitt zur Fehlerbehandlung dargestellt, aber die Details unten stellen sicher, dass Sie keine Topologie erstellen, die Probleme verursachen kann.

#### <a name="writable-domain-controller-availability"></a>Verfügbarkeit eines beschreibbaren Domänencontrollers
Bei einer Wiederherstellung muss ein Domänencontroller eine Verbindung zu einem beschreibbaren Domänencontroller haben, da ein schreibgeschützter Domänencontroller das Delta der Aktualisierungen nicht senden kann. Die Topologie ist wahrscheinlich bereits korrekt dafür eingerichtet, da ein beschreibbaren Domänencontroller immer einen beschreibbaren Partner benötigt. Wenn jedoch alle beschreibbaren Domänencontroller gleichzeitig wiederhergestellt werden, findet keiner eine gültige Quelle. Gleiches gilt, wenn die beschreibbaren Domänencontroller für Wartungszwecke offline oder aus anderen Gründen nicht über das Netzwerk erreichbar sind.

#### <a name="simultaneous-restore"></a>Gleichzeitige Wiederherstellung
Stellen Sie niemals alle Domänencontroller in einer einzigen Domäne gleichzeitig wieder her. Wenn alle Momentaufnahmen gleichzeitig wiederhergestellt werden, funktioniert zwar die Active Directory-Replikation normal, aber die SYSVOL-Replikation hält an. Die Wiederherstellungsarchitektur von FRS und DFSR verlangt, dass die Replikatinstanz in einen nicht autoritativen Synchronisierungsmodus gesetzt wird. Wenn alle Domänencontroller auf einmal wiederhergestellt werden, und sich jeder Domänencontroller für SYSVOL als nicht autoritativ kennzeichnet, versuchen alle, Gruppenrichtlinien und Skripts von einem autoritativen Partner zu synchronisieren, aber an diesem Punkt sind auch alle Partner nicht autoritativ.

> [!IMPORTANT]
> Wenn alle Domänencontroller auf einmal wiederhergestellt werden, verwenden Sie die Informationen in den folgenden Artikeln, um einen Domänencontroller, normalerweise den PDC-Emulator als autoritativ festzulegen, damit die anderen Domänencontroller zu einem normalen Betrieb zurückkehren können:
>
> [Verwenden des BurFlags-Registrierungsschlüssels zum erneuten Initialisieren des Replikatsatzes des Dateireplikationsdienstes](https://support.microsoft.com/kb/290762)
>
> [Erzwingen einer autoritativen und nicht autoritativen Synchronisierung für DFSR-repliziertes SYSVOL (wie „D4/D2“ für FRS)](https://support.microsoft.com/kb/2218556)

> [!WARNING]
> Führen Sie nicht alle Domänencontroller in einer Gesamtstruktur oder einer Domäne auf demselben Hypervisorhost aus. Damit wird eine einzelne Fehlerquelle eingeführt, die jedes mal, wenn der Hypervisor offline genommen wird, AD DS-, Exchange-, SQL- und andere Unternehmensvorgänge lahmlegt. Das ist nicht anders als die Verwendung von nur einem Domänencontroller für eine gesamte Domäne oder Gesamtstruktur. Mehrere Domänencontroller auf mehreren Plattformen tragen zu Redundanz und Fehlertoleranz bei.

#### <a name="post-snapshot-replication"></a>Replikation nach der Momentaufnahme
Stellen Sie keine Momentaufnahmen wieder her, bis alle Änderungen lokalen Ursprungs, die seit der Erstellung der Momentaufnahme vorgenommen wurden, ausgehend repliziert wurden. Alle ursprünglichen Änderungen sind unwiderruflich verloren, wenn andere Domänencontroller sie noch nicht über eine Replikation erhalten haben.

Verwenden Sie Repadmin.exe, um alle nicht replizierten ausgehenden Änderungen zwischen einem Domänencontroller und seinen Partnern anzuzeigen:

1. Geben Sie mit dem folgenden Befehl die Namen der Domänencontrollerpartner und die DSA-Objekt-GUIDs zurück:

    ```
    Repadmin.exe /showrepl <DC Name of the partner> /repsto
    ```

2. Geben Sie die ausstehende eingehende Replikation des Partnerdomänencontrollers an den wiederherzustellenden Domänencontroller zurück:

    ```
    Repadmin.exe /showchanges < Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare>
    ```

Alternativ können Sie nur die Anzahl der nicht replizierten Änderungen anzeigen:

```
Repadmin.exe /showchanges <Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare> /statistics
```

Im folgenden Beispiel (mit einer aus Gründen der Lesbarkeit vereinfachten Ausgabe, in der wichtige Einträge ***kursiv***dargestellt sind) sehen Sie die Replikationspartnerschaften von DC4:

```
C:\>repadmin.exe /showrepl dc4.corp.contoso.com /repsto

Default-First-Site-Name\DC4
DSA Options: IS_GC
Site Options: (none)
DSA object GUID: 5d083398-4bd3-48a4-a80d-fb2ebafb984f
DSA invocationID: 730fafec-b6d4-4911-88f2-5b64e48fc2f1

==== OUTBOUND NEIGHBORS FOR CHANGE NOTIFICATIONS ============

DC=corp,DC=contoso,DC=com
    Default-First-Site-Name\DC3 via RPC
        DSA object GUID: f62978a8-fcf7-40b5-ac00-40aa9c4f5ad3
        Last attempt @ 2011-11-11 15:04:12 was successful.
    Default-First-Site-Name\DC2 via RPC
        DSA object GUID: 3019137e-d223-4b62-baaa-e241a0c46a11
        Last attempt @ 2011-11-11 15:04:15 was successful.
```

Sie wissen jetzt, dass dieser mit DC2 und DC3 repliziert. Sie zeigen dann die Liste der Änderungen an, für die DC2 angibt, dass er sie immer noch nicht von DC4 erhalten hat, und sehen, dass eine neue Gruppe vorhanden ist:

```
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com

==== SOURCE DSA: (null) ====
Objects returned: 1
(0) add CN=newgroup4,CN=Users,DC=corp,DC=contoso,DC=com
    1> parentGUID: 55fc995a-04f4-4774-b076-d6a48ac1af99
    1> objectGUID: 96b848a2-df1d-433c-a645-956cfbf44086
    2> objectClass: top; group
    1> instanceType: 0x4 = ( WRITE )
    1> whenCreated: 11/11/2011 3:03:57 PM Eastern Standard Time
```

Sie würden auch den anderen Partner testen, um sicherzustellen, dass dieser noch nicht bereits repliziert hat.

Falls Sie nicht wissen möchten, welche Objekte nicht repliziert wurden, und nur wissen wollen, ob Objekte ausstehen, können Sie alternativ die Option **/statistics** verwenden:

```
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com /statistics

***********************************************
********* Grand total *************************
Packets:              1
Objects:              1Object Additions:     1Object Modifications: 0Object Deletions:     0Object Moves:         0Attributes:           12Values:               13
```

> [!IMPORTANT]
> Testen Sie alle beschreibbaren Partner, falls Sie Fehler oder eine ausstehende Replikation sehen. Solange mindestens einer konvergiert ist, ist eine Wiederherstellung der Momentaufnahme im Allgemeinen sicher, da eine transitive Replikation die anderen Server letztendlich abstimmt.
>
> Achten Sie darauf, von /showchanges angezeigte Fehler in der Replikation zu notieren, und fahren Sie nicht fort, bis diese behoben sind.

### <a name="windows-powershell-snapshot-cmdlets"></a>Windows PowerShell-Momentaufnahmen-Cmdlets
Die folgenden Cmdlets des Windows PowerShell Hyper-V-Moduls stellen Momentaufnahmefunktionen in Windows Server 2012 bereit:

```
Checkpoint-VM
Export-VMSnapshot
Get-VMSnapshot
Remove-VMSnapshot
Rename-VMSnapshot
Restore-VMSnapshot
```

