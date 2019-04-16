---
ms.assetid: b146f47e-3081-4c8e-bf68-d0f993564db2
title: "Bereitstellung virtualisierter Domänencontroller und Konfiguration"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dcb377cef003458bcdf2e4b3564167cee4310020
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-deployment-and-configuration"></a>Bereitstellung virtualisierter Domänencontroller und Konfiguration

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema behandelt:  
  
-   [Überlegungen zur Installation](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_InstallConsiderations)  
  
    Dazu zählen plattformanforderungen und andere wichtigen Einschränkungen.  
  
-   [Virtualisierte beim Klonen des Domänencontrollers](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCCloning)  
  
    Dies wird ausführlich erläutert, die gesamte das Klonen virtualisierter Domänencontroller Prozess.  
  
-   [Sichere Wiederherstellung des virtualisierten Domänencontrollers](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCSafeRestore)  
  
    Dies wird ausführlich erläutert, die Überprüfungen, die während der sichere Wiederherstellung des virtualisierten Domänencontrollers vorgenommen werden.  
  
## <a name="BKMK_InstallConsiderations"></a>Überlegungen zur Installation  
Es ist keine spezielle Rollen- oder Featureinstallation für virtualisierte Domänencontroller. alle Domänencontroller enthalten automatisch Wiederherstellungsfunktionen für das Klonen und die sichere. Sie können nicht entfernen oder deaktivieren diese Funktionen.  
  
Verwendung von Windows Server 2012-Domänencontroller erfordert einen Windows Server 2012 AD DS-Schemaversion 56 oder höher und die Gesamtstrukturfunktionsebene Windows Server 2003 im einheitlichen Modus entspricht oder höher.  
  
Beide schreibbar und schreibgeschützte Domänencontroller unterstützen alle Aspekte von virtualisierten Domänencontrollern, ebenso wie globale Kataloge und FSMO-Rollen.  
  
> [!IMPORTANT]  
> Der PDC-Emulator-FSMO-Rolleninhaber muss online sein, wenn das Klonen beginnt.  
  
### <a name="BKMK_PlatformReqs"></a>Plattform-Anforderungen  
Klonen von virtualisierten Domänencontroller sind erforderlich:  
  
-   PDC-Emulator-FSMO-Rolle auf einem Windows Server 2012-Domänencontroller gehostet  
  
-   PDC-Emulator während des Klonens verfügbar  
  
Das Klonen und die sichere Wiederherstellung erforderlich ist:  
  
-   Virtualisierte Windows Server 2012-Gäste  
  
-   Virtualisierunghostplattform unterstützt die VM-Generations-ID (VMGID)  
  
Überprüfen der nachfolgenden Tabelle Virtualisierungsprodukte und gibt an, ob diese virtualisierte Domänencontroller und VM-Generations-ID unterstützen  
  
|||  
|-|-|  
|**Virtualisierungsprodukt**|**Unterstützung für virtualisierte Domänencontroller und VMGID**|  
|**Microsoft Windows Server 2012-Server mit Hyper-V-Feature**|Ja|  
|**Microsoft Windows Server 2012 Hyper-V-Server**|Ja|  
|**Features von Microsoft Windows 8 mit Hyper-V-Client**|Ja|  
|**Windows Server 2008 R2 und WindowsServer 2008**|Nein|  
|**Nicht von Microsoft stammende Virtualisierungslösungen**|Hersteller|  
  
Obwohl Microsoft Windows 7 Virtual PC, Virtual PC 2007, Virtual PC 2004 und Virtual Server 2005 unterstützt, sie 64-Bit-Gästen können nicht ausgeführt werden, noch VM-Generations-ID unterstützen.  
  
Hilfe mit Virtualisierungsprodukten von Drittanbietern und deren Unterstützung Virtualisierungsprodukten virtualisierte Domänencontroller Hersteller, direkt.  
  
Weitere Informationen finden Sie Richtlinien für die Unterstützung [Microsoft-Software, die in nicht-Microsoft-Hardwarevirtualisierungssoftware ausgeführt](https://support.microsoft.com/kb/897615).  
  
### <a name="critical-caveats"></a>Wichtige Einschränkungen  
Virtualisierte Domänencontroller bieten *nicht* sichere Wiederherstellung Folgendes unterstützen:  
  
-   VHD- und VHDX-Dateien manuell über vorhandene VHD-Dateien kopiert haben.  
  
-   VHD- und VHDX-Dateien, die mit der Datei dateisicherungen oder vollständige Sicherungssoftware wiederhergestellt  
  
> [!NOTE]  
> VHDX-Dateien sind auf Windows Server 2012 Hyper-V neu.  
  
Keiner dieser Vorgänge Semantik der VM-Generations-ID abgedeckt ist und daher nicht ändern sich die VM-Generations-ID. Wiederherstellung von Domänencontrollern über die Methoden kann entweder zu einem USN-Rollback und entweder Isolieren des Domänencontrollers oder veralteten Objekten und der Anforderung für gesamtstrukturweite Bereinigungsvorgänge führen.  
  
> [!WARNING]  
> Sichere Wiederherstellung des virtualisierten Domänencontrollers ist kein Ersatz für systemstatussicherungen und den AD DS-Papierkorb.  
>   
> Nach der Wiederherstellung einer Momentaufnahme sind die Deltas von zuvor nicht replizierten Änderungen, die von diesem Domänencontroller stammen, nach der Momentaufnahme verloren. Sichere Wiederherstellung implementiert eine automatisierte nicht autoritative Wiederherstellung um eine versehentliche domänencontrollerquarantäne zu verhindern, dass *nur*.  
  
Weitere Informationen zu USN-Blasen und veralteten Objekten finden Sie unter [Problembehandlung für Active Directory-Vorgänge, die mit Fehler 8606: "zum Erstellen eines Objekts wurden nicht genügend Attribute übergeben"](https://support.microsoft.com/kb/2028495).  
  
## <a name="BKMK_VDCCloning"></a>Virtualisierte beim Klonen des Domänencontrollers  
Es gibt eine Reihe von Phasen und Schritten für das Klonen eines virtualisierten Domänencontrollers, unabhängig von der Verwendung grafischer Tools oder Windows PowerShell. Sind auf hoher Ebene die drei Phasen:  
  
**Vorbereiten der Umgebung**  
  
-   Schritt 1: Überprüfen Sie, dass der Hypervisor die VM-Generations-ID unterstützt und damit das Klonen  
  
-   Schritt 2: Stellen Sie sicher, dass die PDC-Emulatorrolle von einem Domänencontroller, der Windows Server 2012 ausgeführt wird und ob er online und erreichbar, vom geklonten Domänencontroller gehostet wird, während des Klonens.  
  
**Den Quelldomänencontroller vorbereiten**  
  
-   Schritt 3: Autorisieren der Quelldomänencontroller für das Klonen.  
  
-   Schritt 4: Entfernen Sie inkompatible Dienste oder Programme oder zur Datei CustomDCCloneAllowList.xml hinzufügen.  
  
-   Schritt 5: Erstellen der Datei DCCloneConfig.xml  
  
-   Schritt 6: Nehmen Sie Quelldomänencontroller offline  
  
**Den geklonte Domänencontroller erstellen**  
  
-   Schritt 7: Kopieren Sie oder exportieren Sie den virtuellen Quellcomputer, und fügen Sie den XML-Code hinzu, wenn nicht bereits kopiert wurde.  
  
-   Schritt 8: Erstellen einer neuen virtuellen Maschine aus der Kopie.  
  
-   Schritt 9: Starten Sie den neuen virtuellen Computer, um das Klonen zu beginnen.  
  
Es gibt keine Unterschiede bei der Vorgang beim grafische Tools wie der Hyper-V-Verwaltungskonsole oder Befehlszeilentools wie Windows PowerShell verwenden, damit die Schritte nur einmal mit beiden Oberflächen dargestellt werden. Dieses Thema enthält Beispiele für Windows PowerShell Sie End-to-End-Automatisierung des klonprozesses erkunden können; Sie sind nicht für die einzelnen Schritte erforderlich. Es ist kein grafisches Verwaltungstool für virtualisierte Domänencontroller, die in Windows Server 2012 enthalten.  
  
Es gibt verschiedene Punkte im Verfahren, in denen Sie haben, Optionen für den geklonten Computer erstellen und wie Sie die XML-Dateien hinzufügen. Diese Schritte sind in den Details unten aufgeführt. Ansonsten ist der Prozess unveränderbar.  
  
Das folgende Diagramm zeigt die virtualisierten Domänencontroller Klonens, in denen die Domäne bereits vorhanden ist.  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_CloningProcessFlow.png)  
  
### <a name="step-1---validate-the-hypervisor"></a>Schritt 1: Überprüfen des Hypervisors  
Stellen Sie sicher, dass der Quelldomänencontroller auf einem unterstützten Hypervisor ausgeführt wird, indem Sie die Dokumentation des Anbieters durchsehen. Virtualisierte Domänencontroller sind hypervisorunabhängig und erfordern keine Hyper-V.  
  
Wenn der Hypervisor Microsoft Hyper-V ist, stellen Sie sicher, dass sie auf Windows Server 2012 ausgeführt wird. Sie können dies überprüfen, über die Geräteverwaltung  
  
Öffnen **Devmgmt.msc** und überprüfen Sie die **Systemgeräte** für installierte Microsoft Hyper-V-Geräten und Treibern. Das bestimmte Systemgerät erforderlich für virtualisierte Domänencontroller ist der **Microsoft Hyper-V Generation Counter** (Treiber: vmgencounter.sys).  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVVMGenIDCounter.png)  
  
### <a name="step-2---verify-the-pdce-fsmo-role"></a>Schritt 2: Überprüfen der PDCE FSMO-Rolle  
Bevor Sie versuchen, einen Domänencontroller zu klonen, müssen Sie überprüfen, dass der Domänencontroller, der primären Domänencontroller-Emulator-FSMO Windows Server 2012 ausgeführt wird. Der PDC-Emulator (PDCE) ist aus mehreren Gründen erforderlich:  
  
1.  Der PDCE erstellt die spezielle **Klonbare Domänencontroller** gruppieren und legt die Berechtigungen dafür auf den Stamm der Domäne zu einem Domänencontroller zu klonen.  
  
2.  Der klonende Domänencontroller kontaktiert den PDCE direkt über das DRSUAPI RPC-Protokoll, um Computerobjekte für den geklonten Domänencontroller erstellen.  
  
    > [!NOTE]  
    > Windows Server 2012 erweitert das vorhandene Remoteprotokoll (Directory Replication Service, DRS) (UUID **E3514235-4B06-11D1-AB04-00C04FC2DCD2**) eine neue RPC-Methode enthalten **IDL_DRSAddCloneDC** (Opnum **28**). Die **IDL_DRSAddCloneDC** -Methode erstellt ein neues Domänencontrollerobjekt durch Kopieren von Attributen aus einem vorhandenen Domänencontrollerobjekt.  
    >   
    > Der Status eines Domänencontrollers bestehen aus Computer, Server, NTDS-Einstellungen, FRS, DFSR und Verbindung Objekte, die für jeden Domänencontroller beibehalten werden. Wenn ein Objekt zu duplizieren, ersetzt diese RPC-Methode alle Referenzen zum ursprünglichen Domänencontroller durch entsprechende Objekte des neuen Domänencontrollers. Der Aufrufer muss die Kontrolle über Zugriff auf rechten DS-Clone-Domänencontroller auf den Domänennamenskontext verfügen.  
    >   
    > Verwendung dieser neuen Methode ist immer direkten Zugriff an die PDC-Emulator vom Aufrufer erforderlich.  
    >   
    > Da diese RPC-Methode neu ist, benötigt Ihre Netzwerkanalysesoftware aktualisierte Parser, um die Felder für das neue Opnum 28 in die vorhandene UUID E3514235-4B06 - 11 D 1-AB04-00C04FC2DCD2 enthalten. Andernfalls können Sie diesen Datenverkehr nicht analysieren.  
    >   
    > Weitere Informationen finden Sie unter [4.1.29 IDL_DRSAddCloneDC (Opnum 28)](https://msdn.microsoft.com/en-us/library/hh554213(v=prot.13).aspx).  
  
***Dies bedeutet auch, dass bei Verwendung nicht vollständig gerouteter Netzwerke Netzwerksegmente mit Zugriff auf den PDCE Klonen virtualisierter Domänencontroller benötigt***. Es ist akzeptabel, verschieben einen geklonten Domänencontroller mit einem anderen Netzwerk nach dem Klonen – wie einen physischen Domänencontroller –, solange Sie darauf achten, dass die logischen AD DS-Standortinformationen zu aktualisieren.  
  
> [!IMPORTANT]  
> Beim Klonen einer Domäne, die nur einen einzigen Domänencontroller enthält, müssen Sie sicherstellen, dass der Quelldomänencontroller wieder online ist, bevor Sie die klonkopien starten. Eine Produktionsdomäne sollte immer mindestens zwei Domänencontroller enthalten.  
  
#### <a name="active-directory-users-and-computers-method"></a>Active Directory-Benutzer und Computer-Methode  
  
1.  Klicken Sie mit der rechten Maustaste auf die Domäne mit dem MMC-Snap-in "dsa.msc" ein, und klicken Sie auf **Betriebsmaster**. Beachten Sie den Domänencontroller mit dem Namen auf der Registerkarte PDC und schließen Sie das Dialogfeld zu.  
  
2.  Mit der rechten Maustaste Computerobjekt dieses Domänencontrollers, und klicken Sie auf **Eigenschaften**, überprüfen Sie dann die Betriebssysteminformationen.  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Sie können die folgenden Active Directory Windows PowerShell-Modul-Cmdlets, um die Version des PDC-Emulators zurückzugeben kombinieren:  
  
```  
Get-adddomaincontroller  
Get-adcomputer  
```  
  
Wenn nicht die Domäne bereitgestellt wird, wird diese Cmdlets die Domäne des Computers, auf dem ausgeführt davon.  
  
Der folgende Befehl gibt PDCE- und Betriebssysteminformationen Informationen:  
  
```  
get-adcomputer(Get-ADDomainController -Discover -Service "PrimaryDC").name -property * | format-list dnshostname,operatingsystem,operatingsystemversion  
```  
  
In diesem Beispiel unten zeigt angeben des Domänennamens und Filtern der zurückgegebenen Eigenschaften vor der Windows PowerShell-Pipeline:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PDCOSInfo.png)  
  
### <a name="step-3---authorize-a-source-dc"></a>Schritt 3: Autorisieren eines Quelldomänencontrollers  
Der Quelldomänencontroller muss das Zugriffsrecht (Auto) haben **Domänencontroller die Erstellung eines Klons von sich selbst erlauben** auf dem Namenskontextkopf der Domäne. Standardmäßig verfügt die bekannte Gruppe **Klonbare Domänencontroller** über diese Berechtigung und enthält keine Mitglieder. Der PDCE erstellt diese Gruppe, wenn diese FSMO-Rolle auf einem Windows Server 2012-Domänencontroller übertragen.  
  
#### <a name="active-directory-administrative-center-method"></a>Active Directory-Verwaltungscenter-Methode  
  
1.  Starten Sie Dsac.exe, navigieren Sie zu dem Quelldomänencontroller, und öffnen Sie die Detailseite.  
  
2.  In der **Mitglied von** Abschnitt, fügen Sie der **Klonbare Domänencontroller** Gruppe für diese Domäne.  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Sie können die folgenden Active Directory Windows PowerShell-Modul-Cmdlets kombinieren **Get-Adcomputer** und **hinzufügen Adgroupmember** einen Domänencontroller hinzufügen der **Klonbare Domänencontroller** Gruppe:  
  
```  
Get-adcomputer <dc name> | %{add-adgroupmember "cloneable domain controllers" $_.samaccountname}  
```  
  
Addiert, z. B. Server DC1 zur Gruppe, ohne dass Sie den distinguished Name des Gruppenmitglieds angeben müssen:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_AddDcToGroup.png)  
  
#### <a name="rebuilding-default-permissions"></a>Neuerstellung der Standardberechtigungen  
Wenn Sie diese Berechtigung vom domänenkopf entfernen, schlägt das Klonen fehl. Sie können die Berechtigung mithilfe der Active Directory-Verwaltungscenter oder Windows PowerShell neu erstellen.  
  
##### <a name="active-directory-administrative-center-method"></a>Active Directory-Verwaltungscenter-Methode  
  
1.  Öffnen **Active Directory-Verwaltungscenter**mit der rechten Maustaste auf den domänenkopf, klicken Sie auf **Eigenschaften**, klicken Sie auf die **Erweiterungen** auf **Security**, und klicken Sie dann auf **erweitert**. Klicken Sie auf **nur dieses Objekt**.  
  
2.  Klicken Sie auf **hinzufügen**unter **Geben Sie die zu verwendenden Objektnamen ein**, geben Sie den Gruppennamen **Klonbare Domänencontroller.**  
  
3.  Klicken Sie unter Berechtigungen auf **Domänencontroller die Erstellung eines Klons von sich selbst erlauben**, und klicken Sie dann auf **OK**.  
  
> [!NOTE]  
> Sie können auch die Standardberechtigung entfernen und individuelle Domänencontroller hinzufügen. Dies ist wahrscheinlich jedoch fortlaufende Wartungsprobleme verursachen, in denen neue Administratoren diese Anpassung nicht bewusst sind. Das Ändern der Standardeinstellung Sicherheit nicht erhöht und es wird davon abgeraten.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Verwenden Sie die folgenden Befehle in einer mit Administratorrechten Windows PowerShell-Konsole ein. Diese Befehle erkennen den Domänennamen und fügen ihn zurück die Standardberechtigungen:  
  
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
  
Alternativ führen Sie das Beispiel [fixvdcpermissions. ps1](../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms) in einer Windows PowerShell-Konsole, woraufhin die Konsole als Administrator mit erhöhten Rechten auf einem Domänencontroller in der betroffenen Domäne startet. Die Berechtigungen werden automatisch festgelegt. Das Beispiel befindet sich im Anhang dieses Moduls.  
  
### <a name="step-4---remove-incompatible-applications-or-services-if-not-using-customdccloneallowlistxml"></a>Schritt 4: Entfernen inkompatibler Anwendungen oder Dienste (wenn CustomDCCloneAllowList.xml nicht verwendet)  
Programme oder Dienste, die zuvor von Get-ADDCCloningExcludedApplicationList zurückgegeben *und nicht zu CustomDCCloneAllowList.xml hinzugefügt* -muss vor dem Klonen entfernt werden. Deinstallieren der Anwendung oder ein Dienst ist die empfohlene Methode.  
  
> [!WARNING]  
> Alle inkompatiblen Programme oder Dienste nicht deinstalliert oder zu CustomDCCloneAllowList.xml hinzugefügt wird verhindert, dass das Klonen.  
  
Verwenden Sie das Cmdlet Get-AdComputerServiceAccount, um eigenständige verwaltete Dienstkonten (MSAs) in der Domäne zu suchen und, wenn dieser Computer diese verwendet wird. Wenn verwaltete Dienstkonten installiert ist, verwenden Sie das Cmdlet "Uninstall-ADServiceAccount", um das lokal installierte Dienstkonto zu entfernen. Sobald Sie fertig sind, mit den Quelldomänencontroller offline in Schritt 6 aufnehmen, können Sie wieder hinzufügen den MSA über Install-ADServiceAccount, wenn der Server wieder online ist. Weitere Informationen finden Sie unter [Uninstall-ADServiceAccount](https://technet.microsoft.com/en-us/library/hh852310).  
  
> [!IMPORTANT]  
> Eigenständige MSAs zuerst in Windows Server 2008 R2 - wurden in Windows Server 2012 durch Gruppen-MSAs ersetzt. Gruppen-MSAs unterstützen das Klonen.  
  
### <a name="step-5---create-dccloneconfigxml"></a>Schritt 5: Erstellen der Datei DCCloneConfig.xml  
Die Datei DcCloneConfig.xml ist für das Klonen von Domänencontrollern erforderlich. Die Inhalte ermöglichen Ihnen, eindeutige Details wie den neuen Computernamen und IP-Adresse angeben.  
  
Die Datei CustomDCCloneAllowList.xml ist optional, es sei denn, Sie Anwendungen oder potenziell inkompatiblen Windows-Dienste auf dem Quelldomänencontroller installieren. Die Dateien erfordern präzise Benennung, Formatierung und Platzierung. andernfalls das Klonen fehlschlägt.  
  
Aus diesem Grund sollten Sie immer die Windows PowerShell-Cmdlets verwenden, um die XML-Dateien erstellen und speichern Sie sie an der richtigen Stelle.  
  
#### <a name="generating-with-new-addccloneconfigfile"></a>Generieren mit New-ADDCCloneConfigFile  
Das Active Directory Windows PowerShell-Modul enthält ein neues Cmdlet in Windows Server 2012:  
  
```  
New-ADDCCloneConfigFile  
```  
  
Führen Sie das Cmdlet auf dem vorgeschlagenen Quelldomänencontroller, den Sie klonen möchten. Das Cmdlet unterstützt mehrere Argumente und bei der Verwendung immer testet den Computer und die Umgebung, in dem er ausgeführt wird, es sei denn, Sie geben, das offline-Argument.  
  
||||  
|-|-|-|  
|**Active Directory**<br /><br />**Cmdlet**|**Argumente**|**Erläuterung**|  
|**New-ADDCCloneConfigFile**|*<no argument specified>*|Erstellt eine leere DcCloneConfig.xml-Datei im DSA-Arbeitsverzeichnis (Standard: % systemroot%\ntds)|  
||-CloneComputerName|Gibt den Computernamen des geklonten Domänencontroller. String-Datentyp.|  
||-Pfad|Gibt den Ordner aus, um die Datei DcCloneConfig.xml zu erstellen. Wenn nicht angegeben, schreibt in das DSA-Arbeitsverzeichnis (Standard: % systemroot%\ntds). String-Datentyp.|  
||-SiteName|Gibt den Namen des AD-logischen Standort während der Erstellung des geklonten Computers hinzufügen. String-Datentyp.|  
||-IPv4Address|Gibt die statische IPv4-Adresse des geklonten Computers an. String-Datentyp.|  
||-IPv4SubnetMask|Gibt die statische IPv4-Subnetzmaske des geklonten Computers an. String-Datentyp.|  
||-IPv4DefaultGateway|Gibt die statische IPv4-Standardgatewayadresse des geklonten Computers an. String-Datentyp.|  
||-IPv4DNSResolver|Gibt die statischen IPv4-DNS-Einträge des geklonten Computers in eine durch Trennzeichen getrennte Liste an. Arraydatentyp. Bis zu vier Einträge können bereitgestellt werden.|  
||– PreferredWINSServer|Gibt die statische IPv4-Adresse des primären WINS-Servers an. String-Datentyp.|  
||– AlternateWINSServer|Gibt die statische IPv4-Adresse des sekundären WINS-Servers an. String-Datentyp.|  
||-IPv6DNSResolver|Gibt die statischen IPv6-DNS-Einträge des geklonten Computers in eine durch Trennzeichen getrennte Liste an. Es gibt keine Möglichkeit, um statische Ipv6-Informationen in das Klonen virtualisierter Domänencontroller festzulegen. Arraydatentyp.|  
||-Offline|Führt die Validierungstests besteht und überschreibt jede vorhandene dccloneconfig.XML-Datei. Hat keine Parameter. Weitere Informationen finden Sie unter [Running New-ADDCCloneConfigFile im Offlinemodus](../../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode).|  
||*-Statisch*|Erforderlich, wenn die statischen IP-Argumente IPv4SubnetMask, IPv4SubnetMask oder IPv4DefaultGateway angegeben. Hat keine Parameter.|  
  
Tests wie bei der Ausführung im Onlinemodus:  
  
-   PDC-Emulator ist WindowsServer 2012 oder höher  
  
-   Quelldomänencontroller ist Mitglied der Gruppe "Klonbare Domänencontroller"  
  
-   Quelldomänencontroller enthält ausgeschlossenen Anwendungen oder Dienste nicht  
  
-   Quelldomänencontroller enthält keine bereits eine dccloneconfig.XML-Datei im angegebenen Pfad  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewDCCloneConfig.png)  
  
### <a name="step-6---take-the-source-domain-controller-offline"></a>Schritt 6: Quelldomänencontroller offline schalten  
Sie können keine keinen laufenden Quelldomänencontroller kopieren. Es muss ordnungsgemäß heruntergefahren werden. Klonen eines Domänencontrollers durch Stromverlust angehalten.  
  
#### <a name="graphical-method"></a>Grafische Methode  
Verwenden Sie die Schaltfläche zum Herunterfahren im ausgeführten Domänencontroller oder Hyper-V-Manager "Herunterfahren".  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_Shutdown.png)  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVShutdown.png)  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Sie können eine virtuelle Maschine mit einer der folgenden Cmdlets Herunterfahren:  
  
```  
Stop-computer  
Stop-vm  
```  
  
Stop-Computer ist ein Cmdlet, das Herunterfahren von Computern unabhängig von der Virtualisierung unterstützt, und das ältere Shutdown.exe-Dienstprogramm entspricht. Stop-Vm ist ein neues Cmdlet in der Windows Server 2012 Hyper-V Windows PowerShell-Modul, und entspricht den Energieoptionen im Hyper-V-Manager. Die zweite Option ist nützlich in laborumgebungen, in dem der Domänencontroller oft in einem privaten virtualisierten Netzwerk funktioniert.  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopComputer2.png)  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopVM.png)  
  
### <a name="step-7---copy-disks"></a>Schritt 7: Kopieren von Datenträgern  
In der Kopierphase ist eine administrative Entscheidung erforderlich:  
  
-   Kopieren Sie die Datenträger manuell ohne Hyper-V  
  
-   Exportieren des virtuellen Computers mit Hyper-V  
  
-   Exportieren der zusammengeführten Datenträger mithilfe von Hyper-V  
  
Alle Datenträger eines virtuellen Computers kopiert werden müssen, nicht nur das Systemlaufwerk. Wenn der Quelldomänencontroller verschiedene Datenträger verwendet, und Sie planen, Ihren geklonten Domänencontroller an einen anderen Hyper-V-Host zu verschieben, müssen Sie exportieren.  
  
Manuelle Kopieren von Datenträgern wird empfohlen, wenn der Quelldomänencontroller verfügt nur über *eine* Laufwerk. Importieren/Exportieren von wird empfohlen, für virtuelle Computer mit *mehrere* Laufwerk oder anderen komplexen virtuellen hardwareanpassungen wie mehreren NICs.  
  
Wenn Sie Dateien manuell kopieren, löschen Sie alle Momentaufnahmen vor dem Kopieren. Wenn Sie den virtuellen Computer exportieren, löschen Sie Momentaufnahmen vor dem Exportieren oder löschen Sie sie aus dem neuen virtuellen Computer nach dem Importieren.  
  
> [!WARNING]  
> Momentaufnahmen sind unterschiedliche Datenträger, die einen Domänencontroller in vorherigen Zustand wiederhergestellt werden können. Wenn Sie einen Domänencontroller klonen und dann seine Momentaufnahme vor dem Klonen wiederherstellen würden, würde Sie duplizierte Domänencontroller in der Gesamtstruktur am Ende. Frühere Momentaufnahmen ist auf einem neu geklonten Domänencontroller kein Wert vorhanden.  
  
#### <a name="manually-copying-disks"></a>Manuelles Kopieren von Datenträgern  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V-Manager-Methode  
Verwenden Sie das Hyper-V-Manager-Snap-in, um zu bestimmen, welche Datenträger mit dem Quelldomänencontroller verbunden sind. Verwenden Sie Überprüfungsoption überprüfen, ob der Domänencontroller unterschiedliche Datenträger verwendet (Dies erfordert, dass Sie auch den übergeordneten Datenträger kopieren)  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVInspect.png)  
  
Zum Löschen von Momentaufnahmen, wählen Sie eine virtuelle Maschine, und löschen Sie die momentaufnahmeunterstruktur.  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDeleteSnapshot.gif)  
  
Sie können dann die VHD- oder VHDX-Dateien, die mit Windows-Explorer, Xcopy.exe oder Robocopy.exe manuell kopieren. Es sind keine speziellen Schritte erforderlich. Es wird empfohlen, die Dateinamen ändern, auch wenn auf einen anderen Ordner verschieben.  
  
> [!NOTE]  
> Kopieren Sie zwischen Hostcomputern in einem LAN (1-Gbit oder größer), die **Xcopy.exe/j** Option VHD/VHDX-Dateien deutlich schneller als jedes andere Tool, aber wesentlich höheren bandbreitennutzung kopiert.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Um die Datenträger mithilfe von Windows PowerShell zu ermitteln, verwenden Sie die Hyper-V-Module:  
  
```  
Get-vmidecontroller  
Get-vmscsicontroller  
Get-vmfibrechannelhba  
Get-vmharddiskdrive  
```  
  
Sie können z. B. alle IDE-Festplatten zurückkehren, von einem virtuellen Computer mit dem Namen **DC2** mit dem folgenden Beispiel:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_ReturnIDE.png)  
  
Wenn der Datenträgerpfad auf eine AVHD- oder AVHDX-Datei verweist, handelt es sich um eine Momentaufnahme. Verwenden Sie zum Löschen der Momentaufnahmen im Zusammenhang mit einer Festplatte und Zusammenführen der realen VHD- oder VHDX-Cmdlets:  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
Zum Beispiel So löschen Sie alle Momentaufnahmen von einem virtuellen Computer namens DC2-SOURCECLONE:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_DelSnapshots.png)  
  
Verwenden Sie zum Kopieren von Dateien mithilfe von Windows PowerShell das folgende Cmdlet aus:  
  
```  
Copy-Item  
```  
  
Kombinieren Sie mit Cmdlets des virtuellen Computers in Pipelines, um die Automatisierung zu unterstützen. Pipelines sind Kanäle zur Datenübergabe zwischen mehreren Cmdlets zum Übergeben von Daten. Kopieren Sie das Laufwerk von einem offline-Quelldomänencontroller namens DC2-SOURCECLONE auf einen neuen Datenträger namens c:\temp\copy.vhd ohne des exakten Pfad zu seinem Systemlaufwerk kennen:  
  
```  
Get-VMIdeController dc2-sourceclone | Get-VMHardDiskDrive | select-Object {copy-item -path $_.path -destination c:\temp\copy.vhd}  
```  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSCopyDrive.png)  
  
> [!IMPORTANT]  
> Sie können nicht beim Klonen Passthru-Datenträger verwenden, wie diese keine virtuelle Datenträgerdatei sondern eine tatsächliche Festplatte verwenden.  
  
> [!NOTE]  
> Weitere Informationen zu Windows PowerShell-Operationen mit Pipelines finden Sie unter [Piping und die Pipeline in Windows PowerShell](https://technet.microsoft.com/en-us/library/ee176927.aspx).  
  
#### <a name="exporting-the-vm"></a>Exportieren des virtuellen Computers  
Als Alternative zum Kopieren der Datenträger können Sie die gesamte Hyper-V-VM als Kopie exportieren. Beim Exportieren wird automatisch erstellt einen Ordner mit dem Namen für den virtuellen Computer und alle Datenträger und Konfigurationsinformationen enthält.  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVExport.png)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V-Manager-Methode  
So exportieren Sie einen virtuellen Computer mit Hyper-V-Manager:  
  
1.  Mit der rechten Maustaste die Quell-Domänencontroller, und klicken Sie auf **exportieren**.  
  
2.  Wählen Sie einen vorhandenen Ordner als Exportcontainer aus.  
  
3.  Warten Sie, bis der Statusspalte nicht mehr **exportieren**.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Verwenden Sie zum Exportieren eines virtuellen Computers mit dem Hyper-V Windows PowerShell-Modul-Cmdlet aus:  
  
```  
Export-vm  
```  
  
So exportieren Sie einen virtuellen Computer namens DC2-SOURCECLONE auf einen Ordner namens C:\VM:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSExport.png)  
  
> [!NOTE]  
> Windows Server 2012 Hyper-V unterstützt neue Export- und Importfunktionen, die außerhalb des Bereichs dieser Schulung sind. Überprüfen Sie TechNet auf Weitere Informationen.  
  
#### <a name="exporting-merged-disks-using-hyper-v"></a>Exportieren der zusammengeführten Datenträger mithilfe von Hyper-V  
Die letzte Option besteht, die datenträgerzusammenführungs- und Konvertierungsoptionen in Hyper-V zu verwenden. Damit können Sie eine Kopie einer vorhanden Datenträgerstruktur - machen, auch wenn Sie eine Momentaufnahme AVHD-/avhdx - in einem einzigen neue Datenträger bereitstellen. Wie in dem manuellen Kopieren-Szenario ist dies in erster Linie für einfachere virtuelle Computer vorgesehen, die nur ein einziges Laufwerk verwenden, z. B. C:\\. Der einzige Vorteil ist, dass im Gegensatz zum manuellen Kopieren sie nicht erst Momentaufnahmen löschen erforderlich ist. Dieser Vorgang ist natürlich langsamer als einfach löschen der Momentaufnahmen und Kopieren von Datenträgern.  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V-Manager-Methode  
So erstellen Sie einen zusammengeführten Datenträger mit Hyper-V-Manager:  
  
1.  Klicken Sie auf **Datenträger bearbeiten**.  
  
2.  Suchen Sie nach der niedrigste untergeordnete Datenträger. Z. B. Wenn Sie einen differenzierenden Datenträger verwenden, wird der untergeordneten Datenträger der niedrigste untergeordnete. Wenn der virtuelle Computer eine Momentaufnahme (oder mehrere) verfügt, wird die aktuell ausgewählte Momentaufnahme der niedrigste untergeordnete Datenträger.  
  
3.  Wählen Sie die **zusammenführen** Option zum Erstellen von eines einzigen Datenträgers die gesamte übergeordnete und untergeordnete Struktur.  
  
4.  Wählen Sie eine neue virtuelle Festplatte, und geben Sie einen Pfad. Dies gleicht die vorhandenen VHD-/VHDX-Dateien in eine einzige neue portable Einheit, die nicht gefährdet frühere Momentaufnahmen wiederhergestellt ist.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Verwenden Sie zum Erstellen eines zusammengeführten Datenträgers aus einer komplexen Sammlung von übergeordneten Datenträgern mithilfe der Hyper-V Windows PowerShell-Modul-Cmdlet aus:  
  
```  
Convert-vm  
```  
  
Z. B. mit dem Namen so exportieren die gesamte Kette der Datenträger-Momentaufnahmen eines virtuellen Computers (dieses Mal ohne differenzierende Datenträger) und übergeordnete Datenträger auf einem einzigen neue Datenträger DC4 GEKLONT. VHDX:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSConvertVhd.png)  
  
#### <a name="BKMK_Offline"></a>Hinzufügen der XML zum Offlinesystemdatenträger  
Wenn Sie die Datei Dccloneconfig.xml auf den ausgeführten Quelldomänencontroller kopiert haben, müssen Sie jetzt die aktualisierte dccloneconfig.xml-Datei auf den kopierten/exportierten offlinesystemdatenträger kopieren. Je nach installierter Programme, die zuvor mit Get-ADDCCloningExcludedApplicationList erkannt werden müssen Sie auch die Datei CustomDCCloneAllowList.xml auf den Datenträger kopieren.  
  
Die folgenden Speicherorte können die Datei DcCloneConfig.xml enthalten:  
  
1.  DSA-Arbeitsverzeichnis  
  
2.  %windir%\ntds  
  
3.  Lese-/Schreib-Wechselmedien Wechselmedien in der Reihenfolge des Laufwerkbuchstabens, im Stammverzeichnis des Laufwerks  
  
Diese Pfade sind nicht konfigurierbar. Nach dem Klonen begonnen hat, Datei den überprüft diese Speicherorte in dieser Reihenfolge und verwendet die erste Datei DcCloneConfig.xml gefunden, unabhängig von den anderen Inhalt des Ordners.  
  
Die folgenden Speicherorte können die Datei CustomDCCloneAllowList.xml enthalten:  
  
1.  HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters  
  
    AllowListFolder (*REG_SZ*)  
  
2.  DSA-Arbeitsverzeichnis  
  
3.  %windir%\ntds  
  
4.  Lese-/Schreib-Wechselmedien Wechselmedien in der Reihenfolge des Laufwerkbuchstabens, im Stammverzeichnis des Laufwerks  
  
Sie können New-ADDCCloneConfigFile ausführen mit der **-offline** Argument (auch als Offlinemodus bezeichnet) für die Datei DcCloneConfig.xml zu erstellen und in einem korrekten Speicherort. Die folgenden Beispiele zeigen, wie Sie New-ADDCCloneConfigFile im Offlinemodus ausführen.  
  
Zum Erstellen eines geklonten Domänencontrollers mit dem Namen CloneDC1 im Offlinemodus am Standort "REDMOND" mit statischen IPv4-Adresse, geben Sie Folgendes ein:  
  
```  
New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS  
```  
  
Zum Erstellen eines geklonten Domänencontrollers mit dem Namen Clone2 im Offlinemodus mit statischen IPv4- und IPv6-Einstellungen geben:  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS  
```  
  
Zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit statischen IPv4 und IPv6-Einstellungen, und geben Sie mehrere DNS-Server für die DNS-auflösungseinstellungen, geben Sie Folgendes ein:  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS   
```  
  
Zum Erstellen eines geklonten Domänencontrollers mit dem Namen Clone1 im Offlinemodus mit dynamischen IPv4- und IPv6-Einstellungen geben:  
  
```  
New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS  
```  
  
Geben Sie zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit dynamischen IPv4 und IPv6-Einstellungen:  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS  
  
```  
  
##### <a name="windows-explorer-method"></a>Windows Explorer-Methode  
Windows Server 2012 bietet jetzt eine grafische Option für das Bereitstellen von VHD- und VHDX-Dateien. Dies erfordert die Installation der Funktion "Desktopdarstellung" unter Windows Server 2012.  
  
1.  Klicken Sie auf die neu kopierte VHD/VHDX-Datei, die der Quelldomänencontroller Systemlaufwerk oder DSA-Arbeitsverzeichnis Ordner enthält, und klicken Sie dann auf **bereitstellen** aus der **Speicherortordner** Menü.  
  
2.  Kopieren Sie in den jetzt bereitgestellten Laufwerk die XML-Dateien auf einen gültigen Speicherort. Sie möglicherweise aufgefordert, Berechtigungen für den Ordner.  
  
3.  Klicken Sie auf das bereitgestellte Laufwerk, und klicken Sie auf **Auswerfen** aus der **Disk-Tools** Menü.  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVClickMountedDrive.png)  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDetailsMountedDrive.gif)  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVEjectMountedDrive.gif)  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Alternativ können Sie den Offlinedatenträger bereitstellen und kopieren Sie die XML-Datei mit den Windows PowerShell-Cmdlets:  
  
```  
mount-vhd  
get-disk  
get-partition  
get-volume  
Add-PartitionAccessPath  
Copy-Item  
```  
  
Dadurch können Sie die vollständige Kontrolle über den Prozess. Beispielsweise kann das Laufwerk mit einem bestimmten Laufwerkbuchstaben bereitgestellt, die Datei kopiert und Bereitstellung des Laufwerks aufheben.  
  
```  
mount-vhd <disk path> -passthru -nodriveletter | get-disk | get -partition | get-volume | get-partition | where {$_.partition number -eq 2} | Add-PartitionAccessPath -accesspath <drive letter>  
  
copy-item <xml file path><destination path>\dccloneconfig.xml  
  
dismount-vhd <disk path>  
```  
  
Zum Beispiel:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSMountVHD.png)  
  
Sie können auch die neue **Mount-DiskImage** Cmdlet, um eine virtuelle Festplatte (oder ISO)-Datei bereitstellen.  
  
### <a name="step-8---create-the-new-virtual-machine"></a>Schritt 8: Erstellen der neuen virtuellen Maschine  
Der letzte Konfigurationsschritt vor Beginn des klonprozesses ist das Erstellen eines neuen virtuellen Computers, der die Datenträger aus dem kopierten Quelldomänencontroller verwendet. Je nach Auswahl in der Kopierphase Datenträger haben Sie zwei Optionen:  
  
1.  Ordnen Sie eine neue virtuelle Maschine zum kopierten Datenträger  
  
2.  Importieren des virtuellen Computers  
  
#### <a name="associating-a-new-vm-with-copied-disks"></a>Zuordnen eines neuen virtuellen Computers zu kopierten Datenträgern  
Wenn Sie den Systemdatenträger manuell kopiert haben, müssen Sie eine neue virtuelle Maschine, die Verwendung des kopierten Datenträgers erstellen. Der Hypervisor legt automatisch die VM-Generations-ID beim Erstellen eine neue virtuellen Maschine; in der virtuellen Maschine oder in Hyper-V-Host sind keine Änderungen an der Konfiguration erforderlich.  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVConnectVHD.gif)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V-Manager-Methode  
  
1.  Erstellen Sie eine neue virtuelle Maschine.  
  
2.  Geben Sie die VM-Name, Speicher und Netzwerk.  
  
3.  Geben Sie den kopierten Systemdatenträger, auf der Seite virtuelle Festplatte verbinden.  
  
4.  Führen Sie den Assistenten zum Erstellen des virtuellen Computers.  
  
Wenn mehrere Datenträger, Netzwerkadapter oder andere Anpassungen wurden, konfigurieren Sie sie vor dem Starten des Domänencontrollers. Für komplexe virtuelle Computer wird die "Export-Import-Methode zum Kopieren von Datenträgern empfohlen.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Sie können das Hyper-V Windows PowerShell-Modul verwenden, zum Automatisieren der Erstellung eines virtuellen Computers in Windows Server 2012, mit dem folgenden Cmdlet:  
  
```  
New-VM  
```  
  
Zum Beispiel hier die DC4-CLONEDFROMDC2 VM wird erstellt, mit 1GB RAM, aus der Datei c:\vm\dc4-systemdrive-clonedfromdc2.vhd gestartet, und verwenden das virtuelle Netzwerk 10.0 verwendet:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewVM.png)  
  
#### <a name="import-vm"></a>Import-VM  
Wenn Sie Ihren virtuellen Computer zuvor exportiert haben, jetzt müssen Sie es importieren als Kopie zurück. Hierbei werden die exportierte XML-Datei verwendet, um den Computer mit der alle vorherigen Einstellungen, Laufwerken, Netzwerken und arbeitsspeichereinstellungen erneut zu erstellen.  
  
Wenn Sie beabsichtigen, zusätzliche Kopien von demselben exportierten virtuellen Computer zu erstellen, stellen Sie nach Bedarf beliebig viele Kopien des virtuellen Computers. Verwenden Sie für jede Kopie importieren.  
  
> [!IMPORTANT]  
> Es ist wichtig, verwenden Sie die **Kopie** -Option wie Export alle Informationen aus der Quelle beibehalten Importieren den Server mit **verschieben** oder **In Place** kommt verursacht, wenn auf dem gleichen Hyper-V-Hostserver durchgeführt.  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V-Manager-Methode  
So importieren Sie mit dem Hyper-V-Manager-Snap-in:  
  
1.  Klicken Sie auf **virtuellen Computer importieren**  
  
2.  Auf der **Ordner suchen** Seite, wählen Sie die exportierte VM-Definitionsdatei mithilfe der Schaltfläche "Durchsuchen"  
  
3.  Auf der **virtuellen Computer auswählen** auf dem Quell-PC.  
  
4.  Auf der **Importtyp** auf **virtuellen Computer kopieren (eine neue eindeutige ID erstellen)**, klicken Sie dann auf **Fertig stellen**.  
  
5.  Benennen Sie den importierten virtuellen Computer auf demselben Hyper-V-Host zu importieren. Er muss den gleichen Namen wie der exportierte Quelldomänencontroller.  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportLocateFolder.png)  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportSelectVM.png)  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportChooseType.gif)  
  
Denken Sie daran, alle importierten Momentaufnahme über die Hyper-V-Verwaltungs-Snap-in zu entfernen:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportDelSnap.gif)  
  
> [!WARNING]  
> Löschen alle importierten Momentaufnahme ist extrem wichtig. Wenn angewendet, würden sie führt zu Replikationsfehlern, doppelten IP-Informationen und anderen Unterbrechungen den geklonte Domänencontroller den Status eines Domänencontrollers vorherigen- und möglicherweise live - zurück.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  
Sie können das Hyper-V Windows PowerShell-Modul verwenden, zum Importieren eines virtuellen Computers in Windows Server 2012, verwenden die folgenden Cmdlets zu automatisieren:  
  
```  
Import-VM  
Rename-VM  
```  
  
Beispiel: Hier die exportierte virtuelle Computer VM DC2-CLONED mit seiner automatisch ermittelten XML-Datei, und klicken Sie dann unmittelbar in seinen neuen virtuellen Computernamen DC5-CLONEDFROMDC2 umbenannt importiert:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSImportVM.png)  
  
Denken Sie daran, alle importierten Momentaufnahme über die folgenden Cmdlets zu entfernen:  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
Zum Beispiel:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSGetVMSnap.png)  
  
> [!WARNING]  
> Stellen Sie sicher, dass beim Importieren des Computers statische MAC-Adressen nicht auf dem Quelldomänencontroller zugewiesen wurden. Wenn ein Quellcomputer mit einer statischen MAC geklont wird, diese kopierten Computer nicht ordnungsgemäß senden oder Empfangen von Netzwerkdatenverkehr. Legen Sie eine neue eindeutige statische oder dynamische MAC-Adresse, wenn dies der Fall ist. Sie können sehen, wenn ein virtueller Computer statische MAC-Adressen mit dem Befehl verwendet:  
>   
> **Get-VM - Name des virtuellen Computers**   
>  ***Test-Vm* | Get-VMNetworkAdapter | fl \ ***  
  
### <a name="step-9---clone-the-new-virtual-machine"></a>Schritt 9: Klonen der neuen virtuellen Maschine  
Optional vor Beginn des klonprozesses starten Sie den geklonten offline-Quelldomänencontroller neu. Stellen Sie sicher, dass der PDC-Emulator unabhängig davon online ist.  
  
Um das Klonen zu beginnen, müssen Sie einfach starten Sie den neuen virtuellen Computer. Der Prozess wird automatisch initiiert, und der Domänencontroller wird automatisch neu gestartet, nachdem das Klonen abgeschlossen ist.  
  
> [!IMPORTANT]  
> Halten die Domänencontroller für einen längeren Zeitraum ausgeschaltet wird nicht empfohlen, und wenn der Klon demselben Standort wie der Quelldomänencontroller hinzugefügt wird, können der anfänglichen internen und standortübergreifenden Replikationstopologie zu erstellen, wenn der Quelldomänencontroller offline ist länger dauern.  
  
Wenn Windows PowerShell verwenden, um einen virtuellen Computer zu starten, wird das neue Hyper-V-Module-Cmdlet:  
  
```  
Start-VM  
```  
  
Zum Beispiel:  
  
![Bereitstellung für virtualisierte Domänencontroller](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSStartVM.png)  
  
Nach dem Neustart des Computers nach Abschluss des Klonvorgangs ist ein Domänencontroller, und Sie können sich normal anmelden, um normalen Vorgang zu bestätigen. Wenn Fehler vorhanden sind, wird der Server festgelegt, für die Problembehandlung im Verzeichnisdienst-Wiederherstellungsmodus gestartet.  
  
## <a name="BKMK_VDCSafeRestore"></a>Virtualisierungs-Sicherheitsmaßnahmen  
Im Gegensatz zum Klonen virtualisierter Domänencontroller, haben die Windows Server 2012-virtualisierungssicherheitsmaßnahmen keine Konfigurationsschritte. Das Feature funktioniert ohne Eingriffe, solange Sie einige einfache Bedingungen einhalten:  
  
-   Der Hypervisor unterstützt die VM-Generations-ID  
  
-   Es ist ein gültiger Partner-Domänencontroller, der ein wiederhergestellter Domänencontroller nicht autoritativ Änderungen replizieren kann.  
  
### <a name="validate-the-hypervisor"></a>Überprüfen des Hypervisors  
Stellen Sie sicher, dass der Quelldomänencontroller auf einem unterstützten Hypervisor ausgeführt wird, indem Sie die Dokumentation des Anbieters durchsehen. Virtualisierte Domänencontroller sind hypervisorunabhängig und erfordern keine Hyper-V.  
  
Überprüfen Sie die vorherigen [Plattformanforderungen](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_PlatformReqs) Abschnitt für bekannte VM-Generations-ID-Unterstützung.  
  
Wenn Sie virtuelle Computer von einem quellhypervisor zu einem anderen zielhypervisor migrieren, können Virtualisierungs-Sicherheitsmaßnahmen werden oder können je nach, ob die Hypervisors die VM-Generations-ID unterstützen nicht ausgelöst werden, wie in der folgenden Tabelle beschrieben.  
  
|Quellhypervisor|Zielhypervisor|Ergebnis|  
|---------------------|---------------------|----------|  
|Unterstützt die VM-Generations-ID|VM-Generations-ID wird nicht unterstützt werden.|Keine Auslösung von Sicherheitsmaßnahmen (Wenn eine dccloneconfigfile.XML-Datei vorhanden ist, DC, startet im DSRM gestartet)|  
|VM-Generations-ID wird nicht unterstützt werden.|Unterstützt die VM-Generations-ID|Auslösung von Sicherheitsmaßnahmen|  
|Unterstützt die VM-Generations-ID|Unterstützt die VM-Generations-ID|Sicherheitsmaßnahmen nicht ausgelöst, da die Definition des virtuellen Computer nicht geändert hat, was bedeutet, dass die VM-Generations-ID dieselbe bleibt,|  
  
### <a name="validate-the-replication-topology"></a>Überprüfen der Replikationstopologie  
Virtualisierungssicherheitsmaßnahmen initiieren eine nicht autoritative eingehende Replikation für das Delta der Active Directory-Replikation sowie nicht autoritative erneute Synchronisierung aller SYSVOL-Inhalte. Dadurch wird der Domänencontroller mit voller Funktionalität aus einer Momentaufnahme zurückkehrt und letztendlich konsistent mit dem Rest der Umgebung.  
  
Mit dieser neuen Funktion sind einige Anforderungen und Einschränkungen:  
  
-   Ein wiederhergestellter Domänencontroller muss einen beschreibbaren Domänencontroller kontaktieren können.  
  
-   Alle Domänencontroller in einer Domäne müssen nicht gleichzeitig wiederhergestellt werden  
  
-   Alle Änderungen von einem wiederhergestellten Domänencontroller stammen, die noch nicht ausgehend repliziert wurden seit Erstellung der Momentaufnahme sind unwiderruflich verloren  
  
Während der Abschnitt zur Problembehandlung werden diese Szenarien behandelt, Details unten stellen jedoch sicher, dass Sie keine Topologie erstellen, die Probleme verursachen können.  
  
#### <a name="writable-domain-controller-availability"></a>Verfügbarkeit eines beschreibbaren Domänencontrollers  
Wenn wiederhergestellt haben, muss ein Domänencontroller Konnektivität mit einem beschreibbaren Domänencontroller haben. Das Delta der Aktualisierungen nicht von ein schreibgeschützten Domänencontroller gesendet werden. Die Topologie ist wahrscheinlich bereits korrekt dafür, wie einem beschreibbaren Domänencontroller immer einen beschreibbaren Partner benötigt. Wenn alle beschreibbaren Domänencontroller gleichzeitig wiederhergestellt werden, können Sie eine gültige Quelle finden. Gleiches gilt, wenn die beschreibbaren Domänencontroller für Wartungszwecke offline oder andernfalls über das Netzwerk nicht erreichbar sind.  
  
#### <a name="simultaneous-restore"></a>Gleichzeitige wiederherstellen  
Alle Domänencontroller in einer einzelnen Domäne nicht gleichzeitig wiederhergestellt werden. Wenn alle Momentaufnahmen gleichzeitig wiederhergestellt werden, Active Directory-Replikation funktioniert normal, aber die SYSVOL-Replikation hält. Die wiederherstellungsarchitektur von FRS und DFSR erfordern die Replikatinstanz in nicht autoritative Synchronisierungsmodus festlegen. Wenn alle Domänencontroller gleichzeitig wiederhergestellt werden, und jeder Domänencontroller markiert werden selbst nicht autorisierend für SYSVOL, versucht alle, Gruppenrichtlinien und Skripts von einem autoritativen Partner zu synchronisieren; an diesem Punkt sind jedoch alle Partner auch nicht autorisierend.  
  
> [!IMPORTANT]  
> Wenn alle Domänencontroller auf einmal wiederhergestellt werden, verwenden Sie die folgenden Artikeln einen Domänencontroller - normalerweise den PDC-Emulator - als autorisierend, so einrichten, dass die anderen Domänencontroller den normalen Betrieb zurückkehren können:  
>   
> [Mithilfe des BurFlags-Registrierungsschlüssels zum erneuten Initialisieren der Dateireplikationsdienst-Replikatsätze](https://support.microsoft.com/kb/290762)  
>   
> [Vorgehensweise beim Erzwingen einer autorativen und nicht autoritative Synchronisierungs für DFSR-repliziertes SYSVOL (wie "D4/D2" für FRS)](https://support.microsoft.com/kb/2218556)  
  
> [!WARNING]  
> Führen Sie nicht alle Domänencontroller in einer Gesamtstruktur oder Domäne an, auf dem gleichen hypervisorhost. Das führt einen einzelnen Fehlerpunkt, die AD DS, Exchange, SQL und andere Unternehmensvorgänge jedes Mal Unternehmensvorgänge, die der Hypervisor offline geschaltet wird. Dies unterscheidet sich von der Verwendung von nur einem Domänencontroller für eine gesamte Domäne oder Gesamtstruktur. Mehrere Domänencontroller auf mehreren Plattformen unterstützen Redundanz und Fehlertoleranz zu bieten.  
  
#### <a name="post-snapshot-replication"></a>Nach der Snapshot-Replikation  
Wiederherstellen Sie Snapshots bis alle Änderungen lokalen Ursprungs, die seit der Erstellung der Momentaufnahme repliziert wurden ausgehende nicht. Alle ursprünglichen Änderungen sind unwiderruflich verloren, wenn andere Domänencontroller nicht bereits über eine Replikation erhalten.  
  
Verwenden Sie Repadmin.exe, um alle nicht replizierten ausgehenden Änderungen zwischen einem Domänencontroller und seinen Partnern anzuzeigen:  
  
1.  Geben Sie Namen und die DSA-Objekt-GUIDs mit der domänencontrollerpartner zurück:  
  
    ```  
    Repadmin.exe /showrepl <DC Name of the partner> /repsto  
    ```  
  
2.  Geben Sie die ausstehende eingehende Replikation des Partnerdomänencontrollers an den Domänencontroller wiederhergestellt werden zurück:  
  
    ```  
    Repadmin.exe /showchanges < Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare>  
    ```  
  
Alternativ können Sie nur die Anzahl der nicht replizierten Änderungen finden Sie unter:  
  
```  
Repadmin.exe /showchanges <Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare> /statistics  
```  
  
Zum Beispiel (mit der Ausgabe, die für die Lesbarkeit und wichtige Einträge geändert ***kursiven***), sehen Sie die Replikationspartnerschaften von DC4:  
  
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
  
Jetzt wissen Sie, dass er mit DC2 und DC3 repliziert. Sie zeigen dann der Liste der Änderungen, DC2 gibt es immer noch nicht von DC4 erhalten hat, und sehen, dass eine neue Gruppe:  
  
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
  
Sie würden auch den anderen Partner, um sicherzustellen, dass es nicht bereits repliziert hat testen.  
  
Wenn Sie keine Rolle spielt, die Objekte nicht repliziert und nur wissen, dass alle Objekte ausstehenden wurden, können Sie die **Migrationskriterien** Option:  
  
```  
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com /statistics  
  
***********************************************  
********* Grand total *************************  
Packets:              1  
Objects:              1Object Additions:     1Object Modifications: 0Object Deletions:     0Object Moves:         0Attributes:           12Values:               13  
```  
  
> [!IMPORTANT]  
> Testen Sie alle beschreibbaren Partner, falls Sie Fehler oder eine ausstehende Replikation sehen. Solange mindestens einer konvergiert ist, ist es im Allgemeinen sicher, die Wiederherstellung der Momentaufnahme als transitive Replikation die anderen Server letztendlich abstimmt.  
>   
> Achten Sie darauf, beachten Sie alle Fehler bei der Replikation von ShowChanges angezeigt wird und nicht fortgesetzt, bis diese behoben sind.  
  
### <a name="windows-powershell-snapshot-cmdlets"></a>Windows PowerShell-Momentaufnahmen-Cmdlets  
Die folgenden Windows PowerShell-Hyper-V-Modul-Cmdlets bieten Snapshot-Funktionen in Windows Server 2012:  
  
```  
Checkpoint-VM  
Export-VMSnapshot  
Get-VMSnapshot  
Remove-VMSnapshot  
Rename-VMSnapshot  
Restore-VMSnapshot  
```  
  


