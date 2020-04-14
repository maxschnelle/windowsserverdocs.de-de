---
title: Bereitstellen von Nano Server
description: Erläuterungen zum Erstellen und Bereitstellen benutzerdefinierter Images, Pakete, Treiber, Domänen, Rollen und Features
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.topic: get-started-article
ms.assetid: 9f109c91-7c2e-4065-856c-ce9e2e9ce558
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 9eceb92c239ce222f9f1498dfdeb8a21220af86f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827113"
---
# <a name="deploy-nano-server"></a>Bereitstellen von Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Ab Windows Server, Version 1709, steht Nano Server nur als [Basis-Betriebssystemimage für Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sieh dir [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahre, was dies bedeutet. 

Dieses Thema enthält Informationen, die Sie benötigen, um Nano Server-Images bereitzustellen, die stärker an Ihre Bedürfnisse angepasst sind als die einfachen Beispiele im Thema „Nano Server Quick Start“ (Schnellstart von Nano Server). Sie finden hier Informationen, wie Sie ein benutzerdefiniertes Nano Server-Image mit genau den von Ihnen gewünschten Features erstellen, Nano Server-Images aus VHD oder WIM installieren, Dateien bearbeiten, mit Domänen arbeiten, Pakete mithilfe verschiedener Methoden handhaben und mit Serverrollen arbeiten.

## <a name="nano-server-image-builder"></a>Nano Server Image Builder

Nano Server Image Builder ist ein Tool, das Sie mit einer grafischen Oberfläche bei der Erstellung eines benutzerdefinierten Nano Server-Images und startbarer USB-Medien unterstützt. Basierend auf Ihren Eingaben generiert es wiederverwendbare PowerShell-Skripts, mit denen Sie problemlos konsistente Nano Server-Installationen unter Windows Server 2016 Datacenter- oder Standard-Editionen automatisieren können.

Laden Sie das Tool aus dem [Download Center](https://www.microsoft.com/download/details.aspx?id=54065) herunter. 

Das Tool benötigt außerdem das [Windows Assessment and Deployment Kit (ADK)](https://developer.microsoft.comwindows/hardware/windows-assessment-deployment-kit).


Nano Server Image Builder erstellt angepasste Nano Server-Images im VHD-, VHDX- oder ISO-Format und kann startbare USB-Medien zum Bereitstellen von Nano Server oder zum Ermitteln der Hardwarekonfiguration eines Servers erstellen. Ferner stehen Ihnen mit dem Tool folgende Möglichkeiten zur Verfügung:

- Akzeptieren der Lizenzbedingungen 
- Erstellen von VHD-, VHDX- oder ISO-Formaten
- Hinzufügen von Serverrollen
- Hinzufügen von Gerätetreibern
- Festlegen des Computernamens, des Administratorkennworts, des Protokolldateipfads und der Zeitzone
- Beitreten zu einer Domäne mithilfe eines vorhandenen Active Directory-Kontos oder eines genutzten Domänenbeitritts-Blobs
- Aktivieren von WinRM für die Kommunikation außerhalb des lokalen Subnetzes
- Aktivieren von virtuellen LAN-IDs und Konfigurieren statischer IP-Adressen
- Spontanes Hinzufügen neuer Wartungspakete
- Hinzufügen eines Befehls „setupcomplete.cmd“ oder anderer benutzerdefinierter Skripts, die nach dem Verarbeiten der Datei „unattend.xml“ ausgeführt werden
- Aktivieren von Notverwaltungsdiensten (EMS) für den Zugriff auf die Konsole des seriellen Anschlusses
- Aktivieren von Entwicklungsdiensten, um zu Testzwecken signierte Treiber und unsignierte Anwendungen sowie die PowerShell-Standardshell zu aktivieren
- Aktivieren des Debuggings über serielle, USB-, TCP/IP- oder IEEE 1394-Protokolle
- Erstellen von USB-Medien mithilfe von WinPE, das den Server partitioniert und das Nano-Image installiert
- Erstellen von USB-Medien mithilfe von WinPE, das Ihre vorhandene Nano Server-Hardwarekonfiguration erkennt und alle Details als Protokoll sowie auf dem Bildschirm ausgibt. Hierzu gehören Netzwerkkarten, MAC-Adressen und der Firmware-Typ (BIOS oder UEFI). Beim Erkennungsprozess werden neben allen Volumes auf dem System auch die Geräte aufgelistet, die nicht über einen Treiber im Server Core-Treiberpaket verfügen.

Wenn Sie mit einigen dieser Prozesse nicht vertraut sind, finden Sie weiter unten in diesem Thema weiterführende Informationen. Ferner finden Sie dort weitere Nano Server betreffende Themen, sodass Sie die für das Tool benötigten Informationen bereitstellen können.

## <a name="creating-a-custom-nano-server-image"></a><a name=BKMK_CreateImage></a>Erstellen eines benutzerdefinierten Nano Server-Images  
Für Windows Server 2016 wird Nano Server auf den physischen Medien verteilt. Dort Sie finden einen Ordner namens **NanoServer** mit einem .wim-Image und einem Unterordner namens **Packages**. Die dort enthaltenen Paketdateien verwenden Sie zum Hinzufügen von Serverrollen und Features zum VHD-Image und zum anschließenden Starten.  

Du kannst diese Pakete auch mit dem NanoServerPackage-Anbieter des PowerShell-Moduls „PackageManagement“ (OneGet) suchen und installieren. Beachten Sie hierzu den Abschnitt „Online-Installieren von Rollen und Features“ in diesem Thema.  

Die nachstehende Tabelle zeigt die Rollen und Features, die in dieser Version von Nano Server verfügbar sind, einschließlich der Windows PowerShell-Optionen, mit denen die zugehörigen Pakete installiert werden. Einige Pakete werden direkt mit eigenen Windows PowerShell-Switches installiert (beispielsweise -Compute). Andere werden installiert, indem Sie Paketnamen an den Parameter „-Package“ übergeben. Diese Paketnamen können Sie in einer durch Trennzeichen getrennten Liste zusammenfassen. Sie können die verfügbaren Pakete mit dem Cmdlet „Get-NanoServerPackage“ dynamisch auflisten.  


|                                                                             Rolle oder Feature                                                                             |                                                                                                                                                                                                          Option                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                     Hyper-V-Rolle (einschließlich NetQoS)                                                                     |                                                                                                                                                                                                         -Compute                                                                                                                                                                                                          |
|                                                   Failovercluster und andere Komponenten, wie im Anschluss an diese Tabelle beschrieben                                                   |                                                                                                                                                                                                        -Clustering                                                                                                                                                                                                        |
| Grundlegende Treiber für eine Vielzahl von Netzwerkadaptern und Speichercontrollern. Hierbei handelt es sich um denselben Treibersatz, der in einer Server Core-Installation von Windows Server 2016 enthalten ist. |                                                                                                                                                                                                        -OEMDrivers                                                                                                                                                                                                        |
|                                                Dateiserverrolle und andere Speicherkomponenten, wie im Anschluss an diese Tabelle beschrieben                                                 |                                                                                                                                                                                                         -Storage                                                                                                                                                                                                          |
|                                                          Windows Defender, einschließlich einer Standardsignaturdatei                                                           |                                                                                                                                                                                                         -Defender                                                                                                                                                                                                         |
|                         Reverse-Weiterleitungen für die Anwendungskompatibilität, z.B. allgemeine Anwendungsframeworks wie Ruby, Node.js usw.                         |                                                                                                                                                                                                  Jetzt standardmäßig enthalten                                                                                                                                                                                                  |
|                                                                             DNS-Serverrolle                                                                             |                                                                                                                                                                                         -Package Microsoft-NanoServer-DNS-Package                                                                                                                                                                                         |
|                                                              PowerShell Desired State Configuration (DSC)                                                               |                                                                                                                               -Package Microsoft-NanoServer-DSC-Package<br />**Hinweis:** Ausführliche Informationen finden Sie unter [Using DSC on Nano Server (Verwenden von DSC unter Nano Server)](https://msdn.microsoft.com/powershell/dsc/nanoDsc).                                                                                                                               |
|                                                                    Internetinformationsdienste (IIS).                                                                    |                                                                                                                                       -Package Microsoft-NanoServer-IIS-Package<br />**Hinweis:** Weitere Informationen zum Arbeiten mit IIS findest du unter [IIS auf Nano Server](IIS-on-Nano-Server.md).                                                                                                                                        |
|                                                                   Hostunterstützung für Windows-Container                                                                   |                                                                                                                                                                                                        -Containers                                                                                                                                                                                                        |
|                                                               System Center Virtual Machine Manager-Agent                                                               | -Package Microsoft-NanoServer-SCVMM-Package<br />-Package Microsoft-NanoServer-SCVMM-Compute-Package<br />**Hinweis:** Verwende das SCVMM Compute-Paket nur, wenn du Hyper-V überwachst. Für zusammengeführte Bereitstellungen in VMM solltest du auch den Speicherparameter angeben. Weitere Informationen findest du in der [VMM-Dokumentation](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-compute-add-nano-hyper-v). |
|                                                                 System Center Operations Manager-Agent                                                                  |                                                                                                                 Wird separat installiert. Weitere Informationen findest du in der System Center Operations Manager-Dokumentation unter https://technet.microsoft.com/system-center-docs/om/manage/install-agent-on-nano-server.                                                                                                                 |
|                                                                 Data Center Bridging (einschließlich DCBQoS)                                                                 |                                                                                                                                                                                         -Package Microsoft-NanoServer-DCB-Package                                                                                                                                                                                         |
|                                                                     Bereitstellen auf einem virtuellen Computer                                                                      |                                                                                                                                                                                        -Package Microsoft-NanoServer-Guest-Package                                                                                                                                                                                        |
|                                                                     Bereitstellen auf einem physischen Computer                                                                     |                                                                                                                                                                                        -Package Microsoft-NanoServer-Host-Package                                                                                                                                                                                        |
|     BitLocker, Trusted Platform Module (TPM), Volumeverschlüsselung, Plattform-ID, Kryptografieanbieter und andere Funktionen, die mit einem sicheren Start verbunden sind     |                                                                                                                                                                                    -Package Microsoft-NanoServer-SecureStartup-Package                                                                                                                                                                                    |
|                                                                    Unterstützung von Hyper-V für abgeschirmte VMs                                                                     |                                                                                                                                         -Package Microsoft-NanoServer-ShieldedVM-Package<br />**Hinweis:** Dieses Paket ist nur für die Datacenter-Edition von Nano Server verfügbar.                                                                                                                                         |
|                                                             SNMP-Agent (Simple Network Management-Protokoll)                                                             |                                   -Package Microsoft-NanoServer-SNMP-Agent-Package.cab<br />**Hinweis:** Nicht auf Windows Server 2016-Installationsmedien enthalten. Nur online verfügbar. Details findest du unter [Online-Installieren von Rollen und Features](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server#a-namebkmkonlineainstalling-roles-and-features-online).                                    |
|               IPHelper-Dienst, der mithilfe von IPv6-Übertragungstechnologien (6to4, ISATAP, Port Proxy und Teredo) und IP-HTTPS Tunnelkonnektivität bereitstellt.               |                                -Package Microsoft-NanoServer-IPHelper-Service-Package.cab<br />**Hinweis:** Nicht auf Windows Server 2016-Installationsmedien enthalten. Nur online verfügbar. Details findest du unter [Online-Installieren von Rollen und Features](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server#a-namebkmkonlineainstalling-roles-and-features-online).                                 |

> [!NOTE]  
> Wenn Sie Pakete mit diesen Optionen installieren, wird auch ein zugehöriges Language Pack installiert, das auf dem ausgewählten Gebietsschema des Servermediums basiert. Sie finden die verfügbaren Language Packs und deren Gebietsschemakürzel auf den Installationsmedien in Unterordnern, die nach dem Gebietsschema des Images benannt sind.  

> [!NOTE]  
> Bei Verwendung des Parameters „-Storage“ zum Installieren von Dateidiensten werden diese Dienste nicht aktiviert. Aktivieren Sie dieses Feature von einem Remotecomputer mit Server Manager. 

### <a name="failover-clustering-items-installed-by-the--clustering-parameter"></a>Vom Parameter „-Clustering“ installierte Failoverclusteringelemente

- Failoverclusteringrolle
- VM-Failoverclustering
- Direkte Speicherplätze (S2D)
- Quality of Service für Speicher
- Volumereplikationsclustering
- SMB-Zeugendienst


### <a name="file-and-storage-items-installed-by-the--storage-parameter"></a>Vom Parameter „-Storage“ installierte Datei- und Speicherelemente

- Dateiserverrolle
- Datendeduplizierung
- Multipfad-E/A, einschließlich eines Laufwerks für das gerätespezifische Modul von Microsoft (MSDSM)
- ReFS (Version 1 und 2)
- iSCSI-Initiator (aber nicht iSCSI-Ziel)
- Speicherreplikat
- Speicherverwaltungsdienst mit SMI-S-Unterstützung
- SMB-Zeugendienst
- Dynamische Volumes
- Grundlegende Windows-Speicheranbieter (für Windows-Speicherverwaltung)




### <a name="installing-a-nano-server-vhd"></a>Installieren einer Nano Server-VHD  
In diesem Beispiel wird ein GPT-basiertes VHDX-Image mit einem vorhandenen Computernamen einschließlich Hyper-V-Gasttreibern mit Nano Server-Installationsmedien auf einer Netzwerkfreigabe erstellt. Beginnen Sie in einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten mit dem folgenden Cmdlet:  

`Import-Module <Server media location>\NanoServer\NanoServerImageGenerator; New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\server_en-us -BasePath .\Base -TargetPath .\FirstStepsNano.vhdx -ComputerName FirstStepsNano`  

Das Cmdlet führt alle nachstehenden Aufgaben aus:  

1.  Wählen Sie „Standard“ als Basisedition.  

2.  Sie werden zur Eingabe des Administratorkennworts aufgefordert.  

3.  Kopieren Sie die Installationsmedien von \\\Path\To\Media\server_en-us nach .\Base.  

4.  Konvertieren Sie das WIM-Image in ein VHD-Image. (Durch die Dateierweiterung des Zielpfadarguments wird bestimmt, ob eine MBR-basierte VHD für virtuelle Computer der Generation 1 oder eine GPT-basierte VHDX für virtuelle Computer der Generation 2 erstellt wird.)  

5.  Kopieren Sie die resultierende VHD-Datei nach „.\FirstStepsNano.vhdx“.  

6.  Legen Sie das Administratorkennwort für das Image wie angegeben fest.  

7.  Legen Sie als Computernamen des Images „FirstStepsNano“ fest.  

8.  Installieren Sie die Hyper-V-Gasttreiber.  

Hierdurch wird das Image „.\FirstStepsNano.vhdx“ erstellt.  

Das Cmdlet generiert während seiner Ausführung ein Protokoll und informiert Sie nach Fertigstellung darüber, wo dieses Protokoll gespeichert ist. Die vom Begleiterskript durchgeführte WIM-VHD-Konvertierung generiert unter %TEMP%\Convert-WindowsImage\\\<GUID> ein eigenes Protokoll (wobei \<GUID> ein eindeutiger Bezeichner der Konvertierungssitzung ist).  

Solange Sie denselben Basispfad verwenden, können Sie den Medienpfadparameter stets auslassen, wenn Sie dieses Cmdlet ausführen, da es zwischengespeicherte Dateien des Basispfads verwendet. Wenn Sie keinen Basispfad angeben, generiert das Cmdlet einen Standardpfad im TEMP-Ordner. Wenn Sie andere Quellmedien, aber denselben Basispfad verwenden möchten, sollten Sie jedoch den Medienpfadparameter angeben.  

>[!NOTE]  
>Sie können nun angeben, ob als Nano Server-Edition die Standard- oder die Datacenter-Edition erstellt werden soll. Verwenden Sie den Parameter „-Edition“, um *Standard* oder *Datacenter* anzugeben.  

Sobald ein Image vorhanden ist, können Sie es nach Bedarf mit dem Cmdlet *Edit-NanoServerImage* ändern.  

Wenn Sie keinen Computernamen angeben, wird ein zufälliger Name generiert.  

### <a name="installing-a-nano-server-wim"></a>Installieren eines Nano Server-WIM  

1. Kopieren Sie den Ordner *NanoServerImageGenerator* aus dem Ordner „\NanoServer“ unter Windows Server 2016 ISO in einen lokalen Ordner auf Ihrem Computer.  
2. Starten Sie Windows PowerShell als Administrator, ändern Sie das Verzeichnis in den Ordner, in dem Sie den Ordner „NanoServerImageGenerator“ gespeichert haben, und importieren Sie anschließend das Modul mit `Import-Module .\NanoServerImageGenerator -Verbose`.  

   >[!NOTE]  
   >Möglicherweise müssen Sie die Windows PowerShell-Ausführungsrichtlinie anpassen. `Set-ExecutionPolicy RemoteSigned` sollte gut funktionieren.  

Um ein Nano Server-Image zu erstellen, das als Hyper-V-Host fungiert, führen Sie Folgendes aus:  

`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerPhysical\NanoServer.wim -ComputerName <computer name> -OEMDrivers -Compute -Clustering`  

Wobei  
-   „-MediaPath“ der Stamm des DVD-Mediums bzw. ISO-Images ist, das Windows Server 2016 enthält.  
-   „-BasePath“ eine Kopie der Nano Server-Binärdateien enthält, sodass Sie „New-NanoServerImage -BasePath“ verwenden können, ohne bei künftigen Ausführungen „-MediaPath“ angeben zu müssen.  
-   „-TargetPath“ die resultierende WIM-Datei mit den von Ihnen ausgewählten Rollen und Features enthält. Stellen Sie sicher, dass Sie die WIM-Erweiterung angeben.  
-   „-Compute“ die Hyper-V-Rolle hinzufügt.  
-   „-OemDrivers“ eine Reihe allgemeiner Treiber hinzufügt.  

Sie werden zur Eingabe eines Administratorkennworts aufgefordert.  

Wenn Sie hierzu weitere Informationen benötigen, führen Sie `Get-Help New-NanoServerImage -Full` aus.  

Starten Sie Windows PE (WinPE), und stellen Sie sicher, dass von WinPE auf die gerade erstellte WIM-Datei zugegriffen werden kann. (Sie könnten beispielsweise die WIM-Datei in ein startbares WinPE-Image auf einem USB-Speicherstick kopieren.)  

Nach dem Start von WinPE verwenden Sie „Diskpart.exe“, um die Festplatte des Zielcomputers vorzubereiten. Führen Sie die folgenden Diskpart-Befehle aus (passen Sie die Befehle entsprechend an, wenn Sie nicht UEFI und GPT verwenden):  

> [!WARNING]  
> Mit diesen Befehlen werden alle Daten auf der Festplatte gelöscht.  

**Diskpart.exe Select disk 0 Clean Convert GPT Create partition efi size=100 Format quick FS=FAT32 label=System Assign letter=s Create partition msr size=128 Create partition primary Format quick FS=NTFS label=NanoServer Assign letter=n List volume Exit**  

Wenden Sie das Nano Server-Image an (passen Sie den Pfad der WIM-Datei an):  

**Dism.exe /apply-image /imagefile:.\NanoServer.wim /index:1 /applydir:n:\ Bcdboot.exe n:\Windows /s s:**  

Entferne das DVD-Medium bzw. den USB-Speicherstick, und starte das System mit **Wpeutil.exe reboot** neu.  


### <a name="editing-files-on-nano-server-locally-and-remotely"></a>Lokales und remotes Bearbeiten von Dateien auf Nano Server  
 Stellen Sie in beiden Fällen eine Verbindung zu Nano Server her, beispielsweise mit Windows PowerShell-Remoting.  

 Nachdem Sie eine Verbindung zu Nano Server hergestellt haben, können Sie eine auf Ihrem lokalen Computer gespeicherte Datei bearbeiten, indem Sie den relativen oder absoluten Pfad der Datei an den Befehl „psEdit“ übergeben. Beispiel:   
`psEdit C:\Windows\Logs\DISM\dism.log` oder `psEdit .\myScript.ps1`  

Bearbeiten Sie eine Datei auf dem remoten Nano Server, indem Sie eine Remotesitzung mit `Enter-PSSession -ComputerName 192.168.0.100 -Credential ~\Administrator` starten und anschließend den relativen oder absoluten Pfad der Datei wie folgt an den Befehl „psEdit“ übergeben:   
`psEdit C:\Windows\Logs\DISM\dism.log`  

## <a name="installing-roles-and-features-online"></a><a name=BKMK_online></a>Online-Installieren von Rollen und Features  
> [!NOTE]
> Wenn Sie ein optionales Nano Server-Paket von Medien oder aus dem Onlinerepository installieren, sind keine aktuellen Sicherheitsfixes enthalten. Um einen Versionskonflikt zwischen den optionalen Paketen und dem Basisbetriebssystem zu vermeiden, solltest du nach dem Installieren optionaler Pakete und **vor** dem erneuten Starten des Servers das [aktuellste kumulative Update](https://technet.microsoft.com/windows-server-docs/get-started/update-nano-server) installieren.

### <a name="installing-roles-and-features-from-a-package-repository"></a>Installieren von Rollen und Features aus einem Paketrepository  
Sie können Nano Server-Pakete im Onlinepaketrepository suchen und daraus installieren, indem Sie den NanoServerPackage-Anbieter des PowerShell-Moduls „PackageManagement“ PowerShell verwenden. Um diesen Anbieter zu installieren, verwenden Sie die folgenden Cmdlets:

```powershell
Install-PackageProvider NanoServerPackage
Import-PackageProvider NanoServerPackage
```

>[!NOTE]
>Wenn bei der Ausführung von Install-PackageProvider Fehler auftreten, überprüfe, ob du das [neueste kumulative Update](https://technet.microsoft.com/windows-server-docs/get-started/update-nano-server) ([KB3206632](https://support.microsoft.com/kb/3206632) oder höher) installiert hast, oder verwende Save-Module wie folgt: 

```powershell
Save-Module -Path $Env:ProgramFiles\WindowsPowerShell\Modules\ -Name NanoServerPackage -MinimumVersion 1.0.1.0
Import-PackageProvider NanoServerPackage
```

Nachdem dieser Anbieter installiert und importiert wurde, können Sie Nano Server-Pakete mithilfe von Cmdlets suchen, herunterladen und installieren, die speziell für das Arbeiten mit Nano Server-Pakete konzipiert sind:

```powershell
Find-NanoServerPackage  
Save-NanoServerPackage  
Install-NanoServerPackage
```  

Sie können ebenfalls generische PackageManagement-Cmdlets verwenden und den NanoServerPackage-Anbieter angeben:

```powershell
Find-Package -ProviderName NanoServerPackage
Save-Package -ProviderName NanoServerPackage
Install-Package -ProviderName NanoServerPackage
Get-Package -ProviderName NanoServerPackage
```

Fügen Sie `-ProviderName NanoServerPackage` hinzu, um eines dieser Cmdlets mit Nano Server-Paketen auf Nano Server zu verwenden. Wenn Sie den Parameter „-ProviderName“ nicht hinzufügen, durchläuft PackageManagement alle Anbieter. Führen Sie für weitere Informationen zu diesen Cmdlets `Get-Help <cmdlet>` aus. Hier sind einige allgemeine Verwendungsbeispiele:

### <a name="searching-for-nano-server-packages"></a>Suchen nach Nano Server-Paketen  
Verwenden Sie `Find-NanoServerPackage` oder `Find-Package -ProviderName NanoServerPackage`, um nach Nano Server-Paketen zu suchen, die im Onlinerepository verfügbar sind, und eine Liste dieser Pakete auszugeben. Sie können beispielsweise mit dem folgenden Cmdlet eine Liste der aktuellen Pakete abrufen:

```powershell
Find-NanoServerPackage
```

Durch Ausführen von `Find-Package -ProviderName NanoServerPackage -DisplayCulture` werden alle verfügbaren Kulturen angezeigt.

Sollten Sie eine bestimmte Gebietsschemaversion wie z.B. Englisch (USA) benötigen, können Sie `Find-NanoServerPackage -Culture en-us` oder  
`Find-Package -ProviderName NanoServerPackage -Culture en-us` oder `Find-Package -Culture en-us -DisplayCulture`.

Um ein bestimmtes Paket anhand seines Namens zu finden, verwenden Sie den Parameter „-Name“, bei dem auch Platzhalter zulässig sind. Dieser Parameter akzeptiert auch Platzhalter. Um beispielsweise nach allen Paketen mit VMM im Namen zu suchen, verwende `Find-NanoServerPackage -Name *VMM*` oder `Find-Package -ProviderName NanoServerPackage -Name *VMM*`.

Mit den Parametern „-RequiredVersion“, „-MinimumVersion“ oder „-MaximumVersion“ können Sie nach einer bestimmten Version suchen. Um alle verfügbaren Versionen zu suchen, verwenden Sie „-AllVersions“. Andernfalls wird nur die aktuelle Version zurückgegeben. Beispiel: `Find-NanoServerPackage -Name *VMM* -RequiredVersion 10.0.14393.0`. Oder für alle Versionen: `Find-Package -ProviderName NanoServerPackage -Name *VMM* -AllVersions`

### <a name="installing-nano-server-packages"></a>Installieren von Nano Server-Paketen  
Sie können ein Nano Server-Paket (einschließlich seiner Abhängigkeitspakete, sofern vorhanden) mit `Install-NanoServerPackage` oder `Install-Package -ProviderName NanoServerPackage` lokal oder als Offline-Image auf Nano Server installieren. Beide nehmen Eingaben von der Pipeline an.

Um die aktuelle Version eines Nano Server-Pakets auf einem Online-Nano Server zu installieren, verwenden Sie `Install-NanoServerPackage -Name Microsoft-NanoServer-Containers-Package` oder `Install-Package -Name Microsoft-NanoServer-Containers-Package`. PackageManagement verwendet die Kultur des Nano Servers.

Sie können ein Nano Server-Paket in einem Offline-Image installieren und dabei wie folgt eine bestimmte Version und Kultur angeben:

`Install-NanoServerPackage -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

oder:

`Install-Package -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

Hier sind einige Beispiele für das Verknüpfen von Paketsuchergebnissen mit dem Installations-Cmdlet:  

`Find-NanoServerPackage *dcb* | Install-NanoServerPackage` sucht alle Pakete mit „dcb“ im Namen und installiert sie anschließend.

`Find-Package *nanoserver-compute-* | Install-Package` sucht Pakete mit „nanoserver-compute-“ im Namen und installiert sie.

`Find-NanoServerPackage -Name *nanoserver-compute* | Install-NanoServerPackage -ToVhd C:\MyNanoVhd.vhd` sucht Pakete mit „compute“ im Namen und installiert sie in einem Offline-Image.

`Find-Package -ProviderName NanoserverPackage *nanoserver-compute-* | Install-Package -ToVhd C:\MyNanoVhd.vhd` hat dieselbe Funktion wie ein Paket, das „nanoserver-compute-“ im Namen hat.

### <a name="downloading-nano-server-packages"></a>Herunterladen von Nano Server-Paketen  

`Save-NanoServerPackage` bzw. `Save-Package` ermöglicht dir, Pakete herunterzuladen und zu speichern, ohne sie zu installieren. Beide Cmdlets nehmen Eingaben aus der Pipeline an.

Um beispielsweise ein Nano Server-Paket herunterzuladen und in einem Verzeichnis zu speichern, das dem Platzhalterpfad entspricht, verwenden Sie `Save-NanoServerPackage -Name Microsoft-NanoServer-DNS-Package -Path C:\` In diesem Beispiel wurde „‑Culture” nicht angegeben, sodass die Kultur des lokalen Computers verwendet wird. Es wurde keine Version angegeben, sodass die aktuelle Version gespeichert wird.

`Save-Package -ProviderName NanoServerPackage -Name Microsoft-NanoServer-IIS-Package -Path C:\ -Culture it-IT -MinimumVersion 10.0.14393.0` speichert eine bestimmte Version, und zwar für die italienische Sprache und das italienische Gebietsschema.

Du kannst Suchergebnisse wie in den folgenden Beispielen über die Pipeline senden:

`Find-NanoServerPackage -Name *containers* -MaximumVersion 10.2 -MinimumVersion 1.0 -Culture es-ES | Save-NanoServerPackage -Path C:\`

oder

`Find-Package -ProviderName NanoServerPackage -Name *shield* -Culture es-ES | Save-Package -Path`

### <a name="inventory-installed-packages"></a>Inventarisieren installierter Pakete
Mit `Get-Package` können Sie ermitteln, welche Nano Server-Pakete installiert sind. Mit `Get-Package -ProviderName NanoserverPackage` sehen Sie beispielsweise, welche Pakete auf Nano Server installiert sind.

Um die Nano Server-Pakete zu suchen, die in einem Offline-Image installiert sind, führen Sie `Get-Package -ProviderName NanoserverPackage -FromVhd C:\MyNanoVhd.vhd` aus.


### <a name="installing-roles-and-features-from-local-source"></a>Installieren von Rollen und Features von einer lokalen Quelle  
Zwar wird empfohlen, Serverrollen und andere Pakete offline zu installieren, möglicherweise müssen Sie diese aber online (bei ausgeführtem Nano Server) in Container-Szenarios installieren. Gehen Sie hierzu folgendermaßen vor:  

1.  Kopieren Sie den Ordner „Packages“ vom Installationsmedium lokal auf den Server, auf dem Nano Server ausgeführt wird (z.B. nach „C:\packages“).  

2.  Erstellen Sie eine neue Datei „Unattend.xml“ auf einem anderen Computer, und kopieren Sie diese nach Nano Server. Sie können diesen XML-Inhalt kopieren und in die von Ihnen erstellte XML-Datei einfügen (das Beispiel zeigt das Installieren des IIS-Pakets):  



```  
<?xml version=1.0 encoding=utf-8?>
    <unattend xmlns=urn:schemas-microsoft-com:unattend>  
    <servicing>  
        <package action=install>  
            <assemblyIdentity name=Microsoft-NanoServer-IIS-Feature-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral />  
            <source location=c:\packages\Microsoft-NanoServer-IIS-Package.cab />  
        </package>  
        <package action=install>  
            <assemblyIdentity name=Microsoft-NanoServer-IIS-Feature-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=en-US />  
            <source location=c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab />  
        </package>  
    </servicing>  
    <cpi:offlineImage cpi:source= xmlns:cpi=urn:schemas-microsoft-com:cpi />  
</unattend>  
```  




3. Ändern Sie in der neuen, von Ihnen erstellten (bzw. kopierten) XML-Datei den Eintrag „C:\packages“ in das Verzeichnis, in das Sie den Inhalt des Ordners „Packages“ kopiert haben.  

4. Wechseln Sie zu dem Verzeichnis mit der neu erstellten XML-Datei, und führen Sie Folgendes aus:  

   **dism /online /apply-unattend:.\unattend.xml**  



5. Vergewissern Sie sich, dass das Paket und das zugehörige Language Pack ordnungsgemäß installiert wurde, indem Sie Folgendes ausführen:  

   **dism /online /get-packages**  

   Du solltest den Text „Package Identity: Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~en-US~10.0.10586.0“ zweimal sehen, einmal für den Versionstyp (Release Type) „Language Pack“ und einmal für den Versionstyp „Feature Pack“.  

## <a name="customizing-an-existing-nano-server-vhd"></a>Anpassen einer vorhandenen Nano Server-VHD  
Sie können die Details einer vorhandenen VHD ändern, indem Sie – wie im folgenden Beispiel – das Cmdlet „Edit-NanoServerImage“ verwenden:  

`Edit-NanoServerImage   -BasePath .\Base   -TargetPath .\BYOVHD.vhd`  

Dieses Cmdlet hat dieselbe Funktion wie „New-NanoServerImage“, allerdings wird kein WIM-Image in ein VHD-Image konvertiert, sondern das vorhandene Image wird geändert. Das Cmdlet unterstützt dieselben Parameter wie „New-NanoServerImage“, mit Ausnahme von „-MediaPath“ und „-MaxSize“, sodass die ursprüngliche VHD mit diesen Parametern erstellt worden sein muss, bevor Sie Änderungen mit „Edit-NanoServerImage“ vornehmen können.  

## <a name="additional-tasks-you-can-accomplish-with-new-nanoserverimage-and-edit-nanoserverimage"></a>Weitere mit „New-NanoServerImage“ und „Edit-NanoServerImage“ ausführbare Aufgaben  

### <a name="joining-domains"></a>Beitreten zu Domänen  
„New-NanoServerImage“ bietet zwei Methoden, um einer Domäne beizutreten. Beide beruhen auf der Offline-Domänenbereitstellung, bei einer dieser Methoden wird für den Beitritt jedoch ein Blob genutzt. In diesem Beispiel nutzt das Cmdlet ein Domänen-Blob für die Contoso-Domäne vom lokalen Computer (der natürlich Teil der Contoso-Domäne sein muss). Anschließend stellt es das Image unter Verwendung des Blobs offline bereit:  

`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomHarvest.vhdx -ComputerName JoinDomHarvest -DomainName Contoso`  

Nach Beendigung dieses Cmdlets sollte die Active Directory-Computerliste einen Computer namens „JoinDomHarvest“ enthalten.  

Sie können dieses Cmdlet auch auf einem Computer verwenden, der nicht zu einer Domäne gehört. Hierzu nutzen Sie ein Blob eines beliebigen Computers, der zu der Domäne gehört, und anschließend stellen Sie das Blob für das Cmdlet bereit. Beachten Sie Folgendes: Wenn Sie ein solches Blob eines anderen Computers nutzen, enthält das Blob bereits den Namen dieses Computers. Wenn Sie also versuchen, den Parameter *-ComputerName* hinzuzufügen, wird ein Fehler ausgegeben.  

Sie können das Blob mit dem folgenden Befehl nutzen:  

**djoin**  
 **/Provision**  
 **/Domain Contoso**  
 **/Machine JoiningDomainsNoHarvest**  
 **/SaveFile JoiningDomainsNoHarvest.djoin**  

Führen Sie „New-NanoServerImage“ mit dem genutzten Blob aus:  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomNoHrvest.vhd -DomainBlobPath .\Path\To\Domain\Blob\JoinDomNoHrvestContoso.djoin`  

Wenn Sie bereits über einen Knoten in der Domäne verfügen, der denselben Computernamen aufweist wie Ihr künftiger Nano Server, könnten Sie den Computernamen wiederverwenden, indem Sie den Parameter `-ReuseDomainNode` hinzufügen.  

### <a name="adding-additional-drivers"></a>Hinzufügen zusätzlicher Treiber
Nano Server stellt ein Paket bereit, das eine Reihe von allgemeinen Treibern für eine Vielzahl von Netzwerkadaptern und Speichercontrollern enthält. Möglicherweise sind jedoch keine Treiber für Ihre Netzwerkadapter enthalten. Mithilfe der folgenden Schritte können Sie Treiber in einem funktionierenden System suchen, extrahieren und zum Nano Server-Image hinzufügen.

1. Installieren Sie Windows Server 2016 auf dem physischen Computer, auf dem Nano Server ausgeführt werden soll.
2. Öffnen Sie den Geräte-Manager, und identifizieren Sie Geräte in den folgenden Kategorien:
3. Netzwerkadapter
4. Speichercontroller
5. Laufwerke
6. Klicken Sie für jedes Gerät in diesen Kategorien mit der rechten Maustaste auf den Gerätenamen, und klicken Sie anschließend auf **Eigenschaften**. Klicken Sie im nun geöffneten Dialogfeld auf die Registerkarte **Treiber**, und klicken Sie anschließend auf **Treiberdetails**.
7. Merken Sie sich den angezeigten Dateinamen und den angezeigten Pfad der Treiberdatei. Ein Beispiel: Der Name der Treiberdatei lautet „e1i63x64.sys“, und sie befindet sich unter „C:\Windows\System32\Drivers“.
8. Suchen Sie in einer Befehlszeile nach der Treiberdatei, und suchen Sie nach allen Instanzen mit „dir e1i*.sys /s /b“. In diesem Beispiel ist die Treiberdatei auch in folgendem Pfad vorhanden: C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd\e1i63x64.sys.
9. Wechsele in einem Eingabeaufforderungsfenster mit erhöhten Rechten zu dem Verzeichnis, in dem sich die Nano Server-VHD befindet, und führe anschließend die folgenden Befehle aus: **md mountdir**

    **dism\dism /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir**

    **dism\dism /Add-Driver /image:.\mountdir /driver: C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd**

    **dism\dism /Unmount-Image /MountDir:.\MountDir /Commit**
10. Wiederholen Sie diese Schritte für alle benötigten Treiberdateien.

> [!NOTE]  
> In dem Ordner, in dem Ihre Treiber gespeichert sind, müssen sowohl die SYS-Dateien als auch die zugehörigen INF-Dateien vorhanden sein. Ferner unterstützt Nano Server nur signierte 64\-Bit-Treiber. 

### <a name="injecting-drivers"></a>Hinzufügen von Treibern  
Nano Server stellt ein Paket bereit, das eine Reihe von allgemeinen Treibern für eine Vielzahl von Netzwerkadaptern und Speichercontrollern enthält. Möglicherweise sind jedoch keine Treiber für Ihre Netzwerkadapter enthalten. Sie können die folgende Syntax verwenden, um mit „New-NanoServerImage“ das Verzeichnis nach verfügbaren Treibern zu durchsuchen und diese zum Nano Server-Image hinzuzufügen:  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers`  

> [!NOTE]
> In dem Ordner, in dem Ihre Treiber gespeichert sind, müssen sowohl die SYS-Dateien als auch die zugehörigen INF-Dateien vorhanden sein. Ferner unterstützt Nano Server nur signierte 64-Bit-Treiber.

Mit dem Parameter „-DriverPath” können Sie auch ein Array von Pfaden zu den INF-Treiberdateien erstellen:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers\netcard64.inf`

### <a name="connecting-with-winrm"></a>Herstellen einer Verbindung mit WinRM  
Um mithilfe der Windows-Remoteverwaltung (WinRM) (von einem anderen Computer, der sich nicht im gleichen Subnetz befindet) eine Verbindung zu einem Nano Server-Computer herstellen zu können, öffnen Sie Port 5985 für eingehenden TCP-Datenverkehr auf dem Nano Server-Image. Verwenden Sie das folgende Cmdlet:  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\ConnectingOverWinRM.vhd -EnableRemoteManagementPort`  

### <a name="setting-static-ip-addresses"></a>Festlegen statischer IP-Adressen  
Um ein Nano Server-Image so zu konfigurieren, dass es statische IP-Adressen verwendet, müssen Sie zunächst nach dem Namen oder Index der Schnittstelle suchen, die Sie ändern möchten, indem Sie „Get-NetAdapter“, Netsh oder die Nano Server-Wiederherstellungskonsole verwenden. Verwenden Sie zum Angeben der Konfiguration die Parameter „-Ipv6Address“, „-Ipv6Dns“, „-Ipv4Address“, „-Ipv4SubnetMask“, „-Ipv4Gateway“ und „-Ipv4Dns“. Beispiel:  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\StaticIpv4.vhd -InterfaceNameOrIndex Ethernet -Ipv4Address 192.168.1.2 -Ipv4SubnetMask 255.255.255.0 -Ipv4Gateway 192.168.1.1 -Ipv4Dns 192.168.1.1`  

### <a name="custom-image-size"></a>Benutzerdefinierte Imagegröße  
Sie können das Nano Server-Image mit dem Parameter „-MaxSize“ wie in diesem Beispiel so konfigurieren, dass es sich um dynamisch erweiterbares VHD oder VHDX handelt:  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -MaxSize 100GB`  

### <a name="embedding-custom-data"></a>Einbetten von benutzerdefinierten Daten  
Verwenden Sie den Parameter „-CopyPath“, um Ihre eigenen Skripts oder Binärdateien in das Nano Server-Image einzubetten und ein Array von zu kopierenden Dateien und Verzeichnissen zu übergeben. Der Parameter „-CopyPath” akzeptiert auch eine Hashtabelle zum Festlegen des Zielpfads für Dateien und Verzeichnisse.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -CopyPath .\tools`

### <a name="running-custom-commands-after-the-first-boot"></a>Ausführen von benutzerdefinierten Befehlen nach dem ersten Start
Verwenden Sie den Parameter „-SetupCompleteCommand”, um als Teil von „setupcomplete.cmd“ benutzerdefinierte Befehle auszuführen und ein Array von Befehlen zu übergeben:

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -SetupCompleteCommand @(echo foo, echo bar)`


### <a name="running-custom-powershell-scripts-as-part-of-image-creation"></a>Benutzerdefinierte PowerShell-Skripts als Teil der Erstellung von Images ausführen
Verwenden Sie zum Ausführen von benutzerdefinierten PowerShell-Skripts als Teil des Image-Erstellungsprozesses „-OfflineScriptPath”-Parameter, um „.ps1-Skripts” ein Array von Pfaden zu übergeben. Wenn diese Skripts Argumente annehmen, verwenden Sie „-OfflineScriptArgument”, um eine Hashtabelle mit zusätzlichen Argumente an die Skripts zu übergeben.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -OfflineScriptPath C:\MyScripts\custom.ps1 -OfflineScriptArgument @{Param1=Value1; Param2=Value2}`


### <a name="support-for-development-scenarios"></a>Unterstützung für Entwicklungsszenarios
Wenn Sie auf Nano Server entwickeln und testen möchten, können Sie den Parameter „-Development“ verwenden. Dadurch wird es möglich, PowerShell als die lokale Standardshell einzusetzen, unsignierte Treiber zu installieren, Debuggerbinärdateien zu kopieren, einen Port für das Debuggen zu öffnen, die Testsignierung zu aktivieren und die Installation von AppX-Paketen ohne Entwicklerlizenz zu aktivieren:

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`


### <a name="custom-unattend-file"></a>Benutzerdefinierte Datei für die unbeaufsichtigte Installation  
Wenn Sie eine eigene Datei für die unbeaufsichtigte Installation verwenden möchten, verwenden Sie den Parameter „-UnattendPath“:  

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -UnattendPath \\path\to\unattend.xml`  

Durch das Angeben eines Administratorkennworts oder Computernamens in dieser Datei für die unbeaufsichtigte Installation werden die durch „-AdministratorPassword“ und „-ComputerName“ festgelegten Werte überschrieben. 

> [!NOTE]
> Nano Server unterstützt kein Festlegen von TCP/IP-Einstellungen über Dateien für die unbeaufsichtigte Installation. Du kannst „Setupcomplete.cmd“ zum Konfigurieren von TCP/IP-Einstellungen verwenden.

### <a name="collecting-log-files"></a>Sammeln von Protokolldateien
Wenn Sie während der Imageerstellung die Protokolldateien erfassen möchten, verwenden Sie den Parameter „-LogPath”, um ein Verzeichnis anzugeben, in das die Protokolldateien kopiert werden.

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -LogPath C:\Logs`


> [!NOTE]
> Einige Parameter auf New-NanoServerImage und Edit-NanoServerImage sind nur zur internen Verwendung und können problemlos ignoriert werden. Dazu gehören die Parameter „-SetupUI” und „-Internal”.


## <a name="installing-apps-and-drivers"></a>Installieren von Apps und Treibern
[comment]: # (Von Xumin Sun, Fehler #68620.)  

### <a name="windows-server-app-installer"></a>Windows Server App-Installer
Der WSA-Installer (Windows Server App) stellt eine zuverlässige Installationsoption für Nano Server dar. Da Windows Installer (MSI) nicht auf Nano Server unterstützt wird, ist WSA auch die einzige verfügbare Installationstechnologie für nicht von Microsoft stammende Produkte. WSA nutzt die Windows-App-Pakettechnologie, die konzipiert wurde, um Anwendungen mithilfe eines deklarativen Manifests sicher und zuverlässig zu installieren und zu warten. Es erweitert das Windows-App-Paketinstallationsprogramm, sodass es Windows Server-spezifische Erweiterungen unterstützt. Allerdings unterstützt WSA nicht das Installieren von Treibern.

Das Erstellen und Installieren eines WSA-Pakets auf Nano Server umfasst Schritte für den Herausgeber und den Consumer des Pakets.

Der Herausgeber des Pakets sollte wie folgt vorgehen:

1. Installiere [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) einschließlich der erforderlichen Tools zum Erstellen eines WSA-Pakets: MakeAppx, MakeCert, Pvk2Pfx, SignTool.
2. Deklariere ein Manifest: Beachte das [WSA-Manifesterweiterungsschema](https://msdn.microsoft.com/library/windows/apps/mt670653.aspx), um die Manifestdatei „AppxManifest.xml“ zu erstellen.
3. Verwenden Sie das Tool **MakeAppx**, um ein WSA-Paket zu erstellen.
4. Verwenden Sie die Tools **MakeCert** und **Pvk2Pfx** zum Erstellen des Zertifikats, und verwenden Sie dann **Signtool** zum Signieren des Pakets.

Anschließend sollte der Paket-Consumer die folgenden Schritte durchführen:

1. Führen Sie das PowerShell-Cmdlet [*Import-Certificate*](https://technet.microsoft.com/library/hh848630) aus, um das Zertifikat des Herausgebers aus Schritt 4 oben in Nano Server zu importieren. Verwenden Sie dabei für certStoreLocation den Wert „Cert:\LocalMachine\TrustedPeople“. Beispiel: `Import-Certificate -FilePath .\xyz.cer -CertStoreLocation Cert:\LocalMachine\TrustedPeople`
2. Installieren Sie die App auf Nano Server, indem Sie das PowerShell-Cmdlet [**Add-AppxPackage**](https://technet.microsoft.com/library/mt575516(v=wps.620).aspx) ausführen, um ein WSA-Paket auf Nano Server zu installieren. Beispiel: `Add-AppxPackage wsaSample.appx`

#### <a name="additional-resources-for-creating-apps"></a>Weitere Ressourcen für das Erstellen von Apps
WSA ist die Servererweiterung der Windows-App-Pakettechnologie (wenngleich sie nicht im Microsoft Store gehostet wird). Wenn Sie Apps mit WSA veröffentlichen möchten, werden die folgenden Themen Ihnen helfen, um sich mit der App-Paketpipeline vertraut zu machen:

- [Vorgehensweise: Erstellen eines allgemeinen Paketmanifests](https://msdn.microsoft.com/library/windows/desktop/br211475.aspx)
- [App-Objekt-Manager (MakeAppx.exe)](https://msdn.microsoft.com/library/windows/desktop/hh446767(v=vs.85).aspx)
- [So erstellst du ein App-Paketsignaturzertifikat](https://msdn.microsoft.com/library/windows/desktop/jj835832(v=vs.85).aspx)
- [SignTool](https://msdn.microsoft.com/library/windows/desktop/aa387764(v=vs.85).aspx)

### <a name="installing-drivers-on-nano-server"></a>Installieren von Treibern auf Nano Server
Sie können mithilfe von INF-Treiberpaketen nicht von Microsoft stammende Treiber auf Nano Server installieren. Hierzu gehören PnP-Treiberpakete (Plug & Play) und Dateisystemfilter-Treiberpakete. Netzwerkfiltertreiber werden derzeit nicht auf Nano Server unterstützt.

Sowohl PnP- als auch Dateisystemfilter-Treiberpakete müssen die Anforderungen für universelle Gerätetreiber erfüllen und den Installationsprozess sowie allgemeine Treiberpaketrichtlinien wie beispielsweise das Signieren einhalten. Hier finden Sie zugehörige Dokumente:

- [Signieren von Treibern](https://msdn.microsoft.com/windows/hardware/drivers/install/driver-signing)
- [Verwenden einer universellen INF-Datei](https://msdn.microsoft.com/windows/hardware/drivers/install/using-a-configurable-inf-file)

#### <a name="installing-driver-packages-offline"></a>Offline-Installieren von Treiberpaketen

Unterstützte Treiberpakete können offline mithilfe der Cmdlets [DISM.exe](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/dism-driver-servicing-command-line-options-s14) bzw. [DISM PowerShell](https://technet.microsoft.com/library/dn376497.aspx) auf Nano Server installiert werden.

#### <a name="installing-driver-packages-online"></a>Online-Installieren von Treiberpaketen
PnP-Treiberpakete können mithilfe von [PnpUtil](https://msdn.microsoft.com/library/windows/hardware/ff550419(v=vs.85).aspx) online auf Nano Server installiert werden. Die Online-Treiberinstallation für Nicht-PnP-Treiberpakete wird derzeit nicht auf Nano Server unterstützt.






--------------------------------------------------  


## <a name="joining-nano-server-to-a-domain"></a><a name=BKMK_JoinDomain></a>Hinzufügen von Nano Server zu einer Domäne  

### <a name="to-add-nano-server-to-a-domain-online"></a>So fügen Sie Nano Server online zu einer Domäne hinzu  

1.  Nutzen Sie mit dem folgenden Befehl ein Daten-Blob eines Computers in der Domäne, auf dem bereits Windows Threshold Server ausgeführt wird:  

    `djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`  

    Das Datenblob wird nun in einer Datei namens „odjblob“ gespeichert.  

2.  Kopieren Sie die Datei „odjblob“ mit den folgenden Befehlen auf den Nano Server-Computer:  

    **net use z: \\\\\<IP-Adresse des Nano-Servers>\c$**  

    > [!NOTE]  
    > Wenn der Befehl „net use“ fehlschlägt, müssen Sie wahrscheinlich die Regeln der Windows-Firewall anpassen. Öffnen Sie hierzu zunächst ein Eingabeaufforderungsfenster mit erhöhten Rechten, starten Sie Windows PowerShell, und stellen Sie anschließend mit den folgenden Befehlen eine Verbindung zum Nano Server-Computer mit Windows PowerShell-Remoting her:  
    >   
    > `Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`  
    >   
    > `$ip = <ip address of Nano Server>`  
    >   
    > `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`  
    >   
    > Geben Sie das Administratorkennwort ein, wenn Sie dazu aufgefordert werden, und führen Sie dann diesen Befehl aus, um die Firewallregel festzulegen:  
    >   
    > **netsh advfirewall firewall set rule group=File and Printer Sharing new enable=yes**  
    >   
    > Beenden Sie Windows PowerShell mit `Exit-PSSession`, und wiederholen Sie den Befehl „net use“. Setzen Sie im Erfolgsfall das Kopieren des Inhalts der Datei „odjblob“ auf Nano Server fort.  

    **md z:\Temp**  

    **copy odjblob z:\Temp**  

3.  Prüfen Sie die Domäne, mit der Nano Server verknüpft werden soll, und stellen Sie sicher, dass DNS konfiguriert ist. Überprüfen Sie auch, dass die Namensauflösung der Domäne bzw. ein Domänencontroller wie erwartet funktioniert. Öffnen Sie hierzu ein Eingabeaufforderungsfenster mit erhöhten Rechten, starten Sie Windows PowerShell, und stellen Sie anschließend mit den folgenden Befehlen eine Verbindung zum Nano Server-Computer mit Windows PowerShell-Remoting her:  

    `Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`  

    `$ip = <ip address of Nano Server>`  

    `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`  

    Geben Sie das Administratorkennwort ein, wenn Sie dazu aufgefordert werden. Nslookup ist auf Nano Server nicht verfügbar, Sie können deshalb die Namensauflösung mit „Resolve-DNSName“ überprüfen.

4. Ist die Namensauflösung erfolgreich, führen Sie in derselben Windows PowerShell-Sitzung den folgenden Befehl für den Beitritt zur Domäne aus:  

    `djoin /requestodj /loadfile c:\Temp\odjblob /windowspath c:\windows /localos`  

5.  Starten Sie den Nano Server-Computer neu, und beenden Sie anschließend die Windows PowerShell-Sitzung:  

    `shutdown /r /t 5`  

    `Exit-PSSession`  

6.  Nachdem Sie Nano Server zu einer Domäne hinzugefügt haben, fügen Sie das Domänenbenutzerkonto zur Administratorengruppe auf dem Nano Server hinzu.

7. Entferne aus Sicherheitsgründen den Nano Server mit dem folgenden Befehl aus der Liste der vertrauenswürdigen Hosts: `Set-Item WSMan:\localhost\client\TrustedHosts ` 

**Alternative Vorgehensweise für das Beitreten zu einer Domäne in nur einem Schritt**  

Nutzen Sie zunächst mit dem folgenden Befehl das Daten-Blob eines anderen Computers in der Domäne, auf dem bereits Windows Threshold Server ausgeführt wird:  

`djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`  

Öffnen Sie (z. B. im Editor) die Datei „odjblob“, kopieren Sie ihren Inhalt, und fügen Sie den Inhalt anschließend in den Abschnitt \<AccountData> der untenstehenden Datei „Unattend.xml“ ein.  

Speichern Sie diese Datei „Unattend.xml“ im Ordner „C:\NanoServer“, und verwenden Sie anschließend die folgenden Befehle, um die VHD einzubinden und die Einstellungen im Abschnitt `offlineServicing` anzuwenden:  

**dism\dism /Mount-ImagemediaFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir**  

**dism\dismmedia:.\mountdir /Apply-Unattend:.\unattend.xml**  

Erstellen Sie einen Ordner „Panther“ (von Windows-Systemen für die Speicherung von Dateien während des Setups verwendet; bei Interesse siehe [Speicherort der Setup-Protokolldateien unter Windows 7, Windows Server 2008 R2 und Windows Vista](https://support.microsoft.com/kb/927521)), kopieren Sie die Datei „Unattend.xml“ in diesen Ordner, und heben Sie anschließend die Einbindung der VHD mit den folgenden Befehlen auf:  

**md .\mountdir\windows\panther**  

**copy .\unattend.xml .\mountdir\windows\panther**  

**dism\dism /Unmount-Image /MountDir:.\mountdir /Commit**  

Beim ersten Starten von Nano Server von dieser VHD werden die übrigen Einstellungen angewendet.  

Nachdem Sie Nano Server zu einer Domäne hinzugefügt haben, fügen Sie das Domänenbenutzerkonto zur Administratorengruppe auf dem Nano Server hinzu.  

## <a name="working-with-server-roles-on-nano-server"></a>Arbeiten mit Serverrollen auf Nano Server

### <a name="using-hyper-v-on-nano-server"></a>Verwenden von Hyper-V auf Nano Server  
Hyper-V funktioniert auf Nano Server in derselben Weise wie unter Windows Server im Server Core-Modus, jedoch mit zwei Ausnahmen:  

-   Sie müssen die gesamte Verwaltung remote ausführen, und auf dem Verwaltungscomputer muss derselbe Build von Windows Server ausgeführt werden wie auf dem Nano Server. Ältere Versionen von Hyper-V-Manager- oder Hyper-V Windows PowerShell-Cmdlets funktionieren nicht.  

-   RemoteFX ist nicht verfügbar.  

In dieser Version wurden die folgenden Features von Hyper-V überprüft:  

-   Aktivieren von Hyper-V  

-   Erstellen von virtuellen Computern der Generation 1 und 2  

-   Erstellen virtueller Switches  

-   Starten virtueller Computer und Ausführen von Windows-Gastbetriebssystemen  
- Hyper-V-Replikat  



Wenn Sie eine Livemigration virtueller Computer durchführen möchten, erstellen Sie einen virtuellen Computer auf einer SMB-Freigabe oder verbinden Ressourcen auf einer vorhandenen SMB-Freigabe mit einem vorhandenen virtuellen Computer. Dabei ist es wichtig, dass Sie die Authentifizierung ordnungsgemäß konfigurieren. Sie können hierbei aus zwei Möglichkeiten wählen:  

**Eingeschränkte Delegierung**  

Die eingeschränkte Delegierung funktioniert wie in früheren Versionen. Weitere Informationen finden Sie in den folgenden Artikeln:  

-   [Enabling Hyper-V Remote Management - Configuring Constrained Delegation For SMB and Highly Available SMB (Aktivieren der Remoteverwaltung von Hyper-V – Konfigurieren der eingeschränkten Delegierung für SMB und hoch verfügbaren SMB)](https://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-smb-and-highly-available-smb.aspx)  

-   [Enabling Hyper-V Remote Management - Configuring Constrained Delegation For Non-Clustered Live Migration (Aktivieren der Remoteverwaltung von Hyper-V – Konfigurieren der eingeschränkten Delegierung für nicht gruppierte Livemigration)](https://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-non-clustered-live-migration.aspx)  

**CredSSP**  

Beachten Sie zunächst den Abschnitt „Verwenden von Windows PowerShell“ in diesem Thema, um CredSSP zu aktivieren und zu testen. Anschließend können Sie auf dem Verwaltungscomputer Hyper-V-Manager verwenden und die Option „Als anderer Benutzer verbinden“ auswählen. Hyper-V-Manager wird CredSSP verwenden. Sie sollten dies auch dann tun, wenn Sie Ihr aktuelles Konto verwenden.  

Windows PowerShell-Cmdlets für Hyper-V können CimSession- oder Anmeldeinformationsparameter verwenden, die beide mit CredSSP funktionieren.  

### <a name="using-failover-clustering-on-nano-server"></a><a name=BKMK_Failover></a>Verwenden des Failoverclustering auf Nano Server  
Das Failoverclustering funktioniert auf Nano Server in derselben Weise wie unter Windows Server im Server Core-Modus. Beachten Sie jedoch die folgenden Warnhinweise:  

-   Cluster müssen mit dem Failovercluster-Manager oder mit Windows PowerShell remote verwaltet werden.  

-   Alle Nano Server-Clusterknoten müssen derselben Domäne angehören, ähnlich wie Clusterknoten unter Windows Server.  

-   Das Domänenkonto muss auf allen Nano Server-Knoten über Administratorrechte verfügen, ähnlich wie Clusterknoten unter Windows Server.  

-   Alle Befehle müssen in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden.  

> [!NOTE]  
> Darüber hinaus werden in dieser Version bestimmte Features nicht unterstützt:  
>   
> -   Sie können keine Failoverclustering-Cmdlets auf einem lokalen Nano Server über Windows PowerShell ausführen.  
> -   Gruppierung von Rollen, ausgenommen Hyper-V und Dateiserver.  

Die folgenden Windows PowerShell-Cmdlets sind nützlich beim Verwalten von Failoverclustern:  

Du kannst mit `New-Cluster -Name <clustername> -Node <comma-separated cluster node list>` einen neuen Cluster erstellen.  

Nachdem Sie einen neuen Cluster eingerichtet haben, sollten Sie auf allen Knoten `Set-StorageSetting -NewDiskPolicy OfflineShared` ausführen.  

Um dem Cluster einen weiteren Knoten hinzuzufügen, verwende `Add-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>`.  

Du entfernst mit `Remove-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>` einen Knoten aus dem Cluster.  

Du erstellst einen horizontal skalierbaren Dateiserver mit `Add-ClusterScaleoutFileServerRole -name <sofsname> -cluster <clustername>`.  

Weitere Cmdlets für das Failoverclustering finden Sie unter [Microsoft.FailoverClusters.PowerShell](https://technet.microsoft.com/library/ee461009.aspx).  

### <a name="using-dns-server-on-nano-server"></a><a name=BKMK_DNS></a>Verwenden des DNS-Servers auf Nano Server  
Um die DNS-Serverrolle auf Nano Server bereitzustellen, fügen Sie das Microsoft-NanoServer-DNS-Package zum Image hinzu. (Beachten Sie hierzu den Abschnitt „Erstellen eines benutzerdefinierten Nano Server-Images“ in diesem Thema.) Sobald der Nano Server ausgeführt wird, stellen Sie eine Verbindung zum Server her. Führen Sie den folgenden Befehl von einer Windows PowerShell-Konsole mit erhöhten Rechten aus, um das Feature zu aktivieren:  

`Enable-WindowsOptionalFeature -Online -FeatureName DNS-Server-Full-Role`  

### <a name="using-iis-on-nano-server"></a><a name=BKMK_IIS></a>Verwenden von IIS auf Nano Server  
Unter [IIS on Nano Server (IIS auf Nano Server)](IIS-on-Nano-Server.md) werden die Schritte für die Verwendung der IIS-Rolle (Internetinformationsdienste) beschrieben. 

### <a name="using-mpio-on-nano-server"></a>Verwenden von MPIO auf Nano Server
Unter [MPIO on Nano Server (MPIO auf Nano Server)](MPIO-on-Nano-Server.md) werden die Schritte für die Verwendung von MPIO beschrieben. 

### <a name="using-ssh-on-nano-server"></a><a name=BKMK_SSH></a>Verwenden von SSH auf Nano Server
Eine Anleitung zum Installieren und Verwenden von SSH auf Nano Server mit dem OpenSSH-Projekt finden Sie unter der [Win32-OpenSSH-Wiki](https://github.com/PowerShell/Win32-OpenSSH/wiki).

## <a name="appendix-sample-unattendxml-file-that-joins-nano-server-to-a-domain"></a>Anhang 2: Beispieldatei „Unattend.xml“, mit der Nano Server zu einer Domäne hinzugefügt wird  

> [!NOTE]  
> Achten Sie darauf, nach dem Einfügen in die „Unattend“-Datei das nachfolgende Leerzeichen im Inhalt von „odjblob“ zu löschen.  

```  
<?xml version='1.0' encoding='utf-8'?>  
<unattend xmlns=urn:schemas-microsoft-com:unattend xmlns:wcm=https://schemas.microsoft.com/WMIConfig/2002/State xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance>  

  <settings pass=offlineServicing>  
    <component name=Microsoft-Windows-UnattendedJoin processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>  
        <OfflineIdentification>                
           <Provisioning>    
             <AccountData> AAAAAAARUABLEABLEABAoAAAAAAAMABSUABLEABLEABAwAAAAAAAAABbMAAdYABc8ABYkABLAABbMAAEAAAAMAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABAsAAAAAAAQAAZoABNUABOYABZYAANQABMoAAOEAAMIAAOkAANoAAMAAAXwAAJAAAAYAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABLEAALMABLQABU0AATMABXAAAAAAAKdf/mhfXoAAUAAAQAAAAb8ABLQABbMABcMABb4ABc8ABAIAAAAAAb8ABLQABbMABcMABb4ABc8ABLQABb0ABZIAAGAAAAsAAR4ABTQABUAAAAAAACAAAQwABZMAAZcAAUgABVcAAegAARcABKkABVIAASwAAY4ABbcABW8ABQoAAT0ABN8AAO8ABekAAJMAAVkAAZUABckABXEABJUAAQ8AAJ4AAIsABZMABdoAAOsABIsABKkABQEABUEABIwABKoAAaAABXgABNwAAegAAAkAAAAABAMABLIABdIABc8ABY4AADAAAA4AAZ4ABbQABcAAAAAAACAAkKBW0ID8nJDWYAHnBAXE77j7BAEWEkl+lKB98XC2G0/9+Wd1DJQW4IYAkKBAADhAnKBWEwhiDAAAM2zzDCEAM6IAAAgAAAAAAAQAAAAAAAAAAAABwzzAAA  
</AccountData>  
           </Provisioning>    
         </OfflineIdentification>    
    </component>  
  </settings>  

  <settings pass=oobeSystem>  
    <component name=Microsoft-Windows-Shell-Setup processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>  
      <UserAccounts>  
        <AdministratorPassword>  
           <Value>Tuva</Value>  
           <PlainText>true</PlainText>  
        </AdministratorPassword>  
      </UserAccounts>  
      <TimeZone>Pacific Standard Time</TimeZone>  
    </component>  
  </settings>  

  <settings pass=specialize>  
    <component name=Microsoft-Windows-Shell-Setup processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>  
      <RegisteredOwner>My Team</RegisteredOwner>  
      <RegisteredOrganization>My Corporation</RegisteredOrganization>  
    </component>  
  </settings>  
</unattend>  
```  

