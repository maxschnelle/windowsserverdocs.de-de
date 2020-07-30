---
title: Gehostete Windows Server Essentials-Lösung
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: fda5628c-ad23-49de-8d94-430a4f253802
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 55d4059361189a0117bfd197c030fb860a1b10bd
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181226"
---
# <a name="hosted-windows-server-essentials"></a>Gehostete Windows Server Essentials-Lösung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Dokument enthält spezifische Informationen für Hoster, die Windows Server Essentials in Ihrem Lab bereitstellen und Windows Server Essentials als Dienst für Ihre Kunden bereitstellen möchten.

## <a name="what-is-windows-server-essentials"></a>Was ist Windows Server Essentials?
 Windows Server Essentials ist eine standortübergreifende Lösung für kleine Unternehmen, die eine Vielzahl von 64-Bit-Produkttechnologien umfasst, um eine Server Umgebung bereitzustellen, die für die meisten kleinen Unternehmen geeignet ist. Die folgenden Technologien sind in Windows Server Essentials enthalten.

 **Server Betriebssystem:** Windows Server 2012-Produkttechnologien sind der Kern von Windows Server Essentials. Weitere Informationen finden Sie auf der Website zu [Windows Server 2012](https://www.microsoft.com/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh).

 **Datenschutz:** Windows Server Essentials nutzt mehrere neue Features, die in Windows Server 2012 verfügbar sind, um erheblich verbesserte Funktionen zum Schutz von Daten bereitzustellen. Mithilfe des [neuen Features "Speicherplätze"](https://technet.microsoft.com/library/hh831739.aspx) können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren, Festplatten dynamisch hinzufügen und Datenvolumes mit bestimmten Ausfallsicherheitsstufen erstellen. Windows Server Essentials kann vollständige System Sicherungen und Bare-Metal-Wiederherstellungen des Servers selbst sowie der mit dem Netzwerk verbundenen Client Computer durchführen? mit Unterstützung für Volumes, die größer als 2 TB sind. Eine neue Funktion in Windows Server 2012, nämlich [Microsoft Azure Online Backup](https://technet.microsoft.com/library/hh831419.aspx) , kann verwendet werden, um Dateien und Ordner in einem cloudbasierten Speicherdienst zu schützen, der von Microsoft verwaltet wird. Windows Server Essentials verwaltet und konfiguriert außerdem das Feature "Datei Versionsverlauf" von Windows 8.1 Clients zentral, sodass Benutzer versehentlich gelöschte oder überschrieben Dateien ohne Unterstützung durch den Administrator wiederherstellen können.

 **Zugriff überall:** Remotewebzugriff bietet optimale, für die Toucheingabe geeignete Browserfunktionen, um von nahezu allen Orten mit Internetverbindung und über fast alle Geräte auf Anwendungen und Daten zuzugreifen. Windows Server Essentials bietet außerdem eine aktualisierte Windows Phone-APP und eine neue APP für Windows 8.1 Client Computer, sodass Benutzer intuitiv eine Verbindung mit Dateien und Ordnern auf dem Server herstellen, diese durchsuchen und auf diese zugreifen können. Dateien werden automatisch für den Offlinezugriff zwischengespeichert und synchronisiert, sobald eine Verbindung mit dem Server verfügbar wird. Windows Server Essentials schaltet die Einrichtung von virtuellen privaten Netzwerken (VPN) in einen einfach zu einem Assistenten gesteuerten Prozess mit wenigen Klicks um und vereinfacht die Verwaltung von VPN-Zugriff für Benutzer. Clientcomputer können eine VPN-Verbindung nutzen, um remote auf die Windows SBS-Umgebung zuzugreifen, sodass der Weg ins Büro nicht mehr erforderlich ist.

 **Flexibilität der Arbeitsauslastung:** Windows Server Essentials wurde entwickelt, damit Kunden flexibel auswählen können, welche Anwendungen und Dienste lokal und welche in der Cloud ausgeführt werden. In früheren Versionen enthielt Windows Small Business Server Standard als Komponentenprodukt Exchange Server, wodurch Kunden, die cloudbasierte Dienste für Messaging und Zusammenarbeit nutzen wollten, nicht nur mehr Kosten entstanden, sondern auch eine größere Komplexität zu bewältigen hatten. Mit Windows Server Essentials können Kunden die gleiche Art integrierter Verwaltungsfunktionen nutzen, unabhängig davon, ob Sie eine lokale Kopie von Exchange Server ausführen, einen gehosteten Exchange-Dienst abonnieren oder Microsoft Office 365 abonnieren.

 System **Überwachung:** Windows Server Essentials überwacht seinen eigenen Integritäts Status und den Status von Client Computern, auf denen Windows 8.1, Windows 7 und Mac OS X Version 10,5 und höher ausgeführt wird. Der Integritätsstatus benachrichtigt Sie u. a. bei Problemen im Zusammenhang mit Computersicherungen, dem Serverspeicher und wenig Speicherplatz.

 **Erweiterbarkeit:** Windows Server Essentials baut auf dem Erweiterbarkeits Modell von Windows SSB 2011 Essentials auf, das es anderen Softwareanbietern ermöglicht, dem Kernprodukt Funktionen und Features hinzuzufügen und einen neuen Satz von Webdienst-APIs hinzuzufügen. Das Feature sichert auch Kompatibilität mit dem vorhandenen [Software Development Kit](https://msdn.microsoft.com/library/gg513958.aspx) (SDK) und [Add-Ins](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials) , die für Windows SBS 2011 Essentials erstellt wurden.

## <a name="how-can-i-customize-an-image"></a>Wie wird ein Abbild angepasst?
 Weitere Informationen finden Sie unter [Windows Server Essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124), einem standardmäßigen Windows Server-System Vorbereitungsprozess mit zusätzlichen Windows Server Essentials-Anpassungs Schritten. Befolgen Sie zum Beenden der Anpassung die Anweisungen unter [Erstellen eines einfachen angepassten Abbilds](https://technet.microsoft.com/library/jj200117) und [Anpassen des Abbilds](https://technet.microsoft.com/library/jj200161). Befolgen Sie dann die Anweisungen unter [Vorbereiten des Abbilds für die Bereitstellung](https://technet.microsoft.com/library/jj200142) , um das endgültige Abbild aufzuzeichnen.

 Beachten Sie folgende Punkte:

1. Überspringen Sie die Erstkonfiguration durch Hinzufügen einer Datei "SkipIC.txt" im Stammverzeichnis eines beliebigen Laufwerks. Drücken Sie nach dem Installieren des Servers vor der Erstkonfiguration UMSCHALT+F10, um das Befehlsfenster zu öffnen und eine Datei "SkipIC.txt" unter "C:/" zu erstellen. Denken Sie nach dem Anpassen daran, die Datei "SkipIC.txt" zu löschen.

2. Wenn Sie Windows Server Essentials auf einem Datenträger bereitstellen müssen, der kleiner als 90 GB ist, sollten Sie vor der System Vorbereitung einen Registrierungsschlüssel hinzufügen:

   ```
   %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f
   ```

   Nach der Durchführung der Systemvorbereitung können Sie das Datenträgerabbild, für das die Systemvorbereitung durchgeführt wurde, verwenden oder für eine neue Bereitstellung erneut in "Install.wim" versiegeln.

   Wenn Sie Virtual Machine Manager verwenden, können Sie eine Vorlage mithilfe der ausgeführten Instanz erstellen. Durch das Erstellen einer Vorlage wird für die Instanz eine Systemvorbereitung durchgeführt und der Server heruntergefahren. Nachdem Sie die Instanz in Ihrer Bibliothek gespeichert haben, können Sie sie bei Bedarf jederzeit aufrufen.

##  <a name="how-do-i-automate-the-deployment"></a><a name="BKMK_automatedeployment"></a>Gewusst wie die Bereitstellung automatisieren?
 Nachdem Sie das angepasste Abbild aufgezeichnet haben, können Sie die Bereitstellung mit dem eigenen Abbild ausführen. Damit Sie eine teilweise unbeaufsichtigte Installation ausführen können, müssen Sie die Datei "unattend.xml" für WinPE-Setup angeben/bereitstellen. Um eine vollständig unbeaufsichtigte Installation durchzuführen, müssen Sie auch die cfg.ini Datei für die Erstkonfiguration von Windows Server Essentials bereitstellen.

1. Führen Sie nur ein unbeaufsichtigtes WinPE-Setup aus. Dadurch wird nur das WinPE-Setup automatisiert, und die Installation wird vor der Erstkonfiguration angehalten, sodass die Endbenutzer nach dem Herstellen einer RDP-Verbindung mit der Serversitzung Informationen zum Unternehmen, zur Domäne und zum Administrator selbst angeben können. Gehen Sie dazu folgendermaßen vor:

   1.  Geben Sie die Windows-Datei "unattend.xml" an. Führen Sie die [Windows 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) aus, um die Datei zu generieren, und geben Sie alle erforderlichen Informationen einschließlich Servername, Product Keys und Administrator Kennwort an. Geben Sie im Abschnitt Microsoft-Windows-Setup der Datei unattend.xml die folgenden Informationen an.

       ```
       <InstallFrom>
                <MetaData>
                    <Key>IMAGE/WINDOWS/EDITIONID</Key>
                    <Value>ServerSolution</Value>
                </MetaData>
                <MetaData>
                    <Key>IMAGE/WINDOWS/INSTALLATIONTYPE</Key>
                    <Value>Server</Value>
                </MetaData>
          </InstallFrom>
       ```

   2.  RDP-Port 3389 muss für eine öffentliche IP-Adresse geöffnet sein, damit der Kunde den Administrator und das in der unattend.xml-Datei angegebene Kennwort verwenden kann, um die Erstkonfiguration abzuschließen.

   > [!NOTE]
   >  Wenn Sie das Standardkennwort nicht ändern, hält die Serverinstallation mit einem Bildschirm an, in dem der Benutzer zur Eingabe eines Kennworts aufgefordert wird.**Hinweis** Endbenutzer müssen das Standardadministratorkonto verwenden, um sich beim Server anzumelden und die Erstkonfiguration auszuführen.

   Wenn Sie Virtual Machine Manager verwenden, können Sie das Administratorkennwort in der Konsole angeben, wenn Sie aus der Vorlage eine neue Instanz erstellen.

2. Führen Sie ein vollständig unbeaufsichtigtes Setup einschließlich einer unbeaufsichtigten Erstkonfiguration aus. Gehen Sie dazu folgendermaßen vor:

   1.  Geben Sie die Datei "unattend.xml" wie zuvor an, wenn die Bereitstellung von WinPE-Setup aus startet.

   2.  Informationen zum Generieren des cfg.ini finden Sie im Abschnitt Windows Server Essentials ADK mit dem Titel [Erstellen der Cfg.ini Datei](https://technet.microsoft.com/library/jj200150).

   3.  Geben Sie diese Informationen in [InitialConfiguration] an.

       ```
       WebDomainName=yourdomainname
       TrustedCertFileName=c:\cert\a.pfx
       TrustedCertPassword=Enteryourpassword
       EnableVPN=true
       EnableRWA=true
       ; Provide all information so that after setup is complete, your customer can use your domain name to visit the server directly with the admin/user information you provide in the [InitialConfiguration] section.

       VpnIPv4StartAddress=<IPV4Address>
       VpnIPv4EndAddress=<IPV4Address>
       VpnBaseIPv6Address=<IPV6Address>
       VpnIPv6PrefixLength=<number>
       ; Provide this information. IPv4StartAddress and IPv4Endaddress are required so that your VPN client can acquire valid IP through this range.

       IPv4DNSForwarder=<IPV4Address,IPV4Address,Â¦>
       IPv6DNSForwarder=<IPV6Address,IPV6Address,Â¦>
       ; Provide this information as needed according to your network environment settings.
       ```

   4.  Geben Sie diese Informationen in [PostOSInstall] an.

       ```
       IsHosted=true
       ; Must have, this will prevent Initial Configure webpage available for other computers under same subnet.

       StaticIPv4Address=<IPV4Address>
       StaticIPv4Gateway=<IPV4Address>
       StaticIPv6Address=<IPV6Address>
       StaticIPv6SubnetPrefixLength=<number>
       StaticIPv6Gateway=<IPV6Address>
       ; All these are optional if you have DHCP Server Service on the subnet, otherwise provide static IP here.
       ```

   5.  Wenn Sie den Parameter "Webdomain Name" angeben, stellen Sie sicher, dass auch der DNS-Eintrag aktualisiert wird, sodass er auf die öffentliche IP-Adresse des Servers verweist.

   6.  Wenn Sie die oben stehenden Informationen zum Parameter "WebDomainName" nicht angegeben haben, stellen Sie sicher, Port 3389 zu öffnen, damit Kunden über RDP eine Verbindung mit dem Server herstellen und die VPN-Konfigurationen abschließen können.

> [!NOTE]
>  Stellen Sie sicher, dass die Zeitzoneneinstellung des VM-Host Servers und der Windows Server Essentials-VM identisch sind. Wenn dies nicht der Fall ist, können verschiedene Fehler auftreten, z. B. kann bei der Erstkonfiguration bei Aufgaben im Zusammenhang mit Zertifikaten ein Fehler auftreten, ein Zertifikat funktioniert ggf. erst einige Stunden nach der Installation, oder die Geräteinformationen werden nicht korrekt aktualisiert.

 Überprüfen Sie nach der Bereitstellung den folgenden Registrierungsschlüssel unter "HKLM\software\microsoft\windows server\setup", um festzustellen, ob die Erstkonfiguration erfolgreich war. Wenn "SetupStage == ICDone && ICStatus == 1", wurde die Erstkonfiguration erfolgreich abgeschlossen.

## <a name="what-is-the-supported-network-topology"></a>Wie sieht die unterstützte Netzwerktopologie aus?
 Um Windows Server Essentials von einem Roamingclient aus verwenden zu können, muss VPN aktiviert werden. Es wird empfohlen, Port 443 für VPN-SSTP-Verbindungen zu aktivieren. Wenn die Funktion "Medienserver" für Remotewebzugriff oder Webdienst-Apps erforderlich ist, muss auch Port 80 aktiviert werden.

 Die VPN-Aktivierung kann während der unbeaufsichtigten Bereitstellung über das Windows PowerShell-Skript erfolgen oder nach der Erstkonfiguration mithilfe des Assistenten konfiguriert werden.


- Informationen zum Aktivieren von VPN während der unbeaufsichtigten Bereitstellung finden Sie unter [How do I automate the deployment?](Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) in diesem Dokument.

- Informationen zum Aktivieren von VPN während der unbeaufsichtigten Bereitstellung finden Sie unter [How do I automate the deployment?](../install/Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) in diesem Dokument.


- Wenn Sie VPN über Windows PowerShell aktivieren möchten, führen Sie das folgende Cmdlet mit Administratorrechten aus, und machen Sie alle erforderlichen Angaben.

  ```
  ##
  ## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).
  ##

  $myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server
  $mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file
  $mySslCertificatePassword = ConvertTo-SecureString '******';   ## password for private key of the SSL certificate
  $skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate

  Add-Type -AssemblyName 'Wssg.Web.DomainManagerObjectModel';
  [Microsoft.WindowsServerSolutions.RemoteAccess.Domains.DomainConfigurationHelper]::SetDomainNameAndCertificate($myExternalDomainName,$mySslCertificateFile,$mySslCertificatePassword,$skipCertificateVerification);
  ##
  ## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).
  ##

  Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;
  ```

  Wenn Sie vor der Übergabe des Servers an Kunden keine VPN-Verbindung bereitstellen können, stellen Sie sicher, dass Serverport 3389 im Internet erreichbar ist, sodass Kunden über RDP eine Verbindung mit dem Server herstellen und die Konfiguration selbst ausführen können.

  Nachfolgend sind zwei typische serverseitige Netzwerktopologien und die Konfiguration von VPN/Remotewebzugriff beschrieben:

- Topologie 1 (bevorzugt)

  -   Der Server befindet sich in einem separaten virtuellen Netzwerk unter einem NAT-Gerät.

  -   Der DHCP-Dienst ist im virtuellen Netzwerk aktiviert, oder dem Server wird eine statische IP-Adresse zugewiesen.

  -   Serverport 443 ist über den öffentlichen IP-Port 443 erreichbar.

  -   VPN-Passthrough ist für Port 443 zulässig.

  -   Der VPN-IPv4-Adresspool muss sich im gleichen Subnetz wie die Serveradresse befinden.

  -   Einem zweiten Server muss eine statische IP-Adresse im gleichen Subnetz, aber außerhalb des VPN-Adresspools zugewiesen werden.

- Topologie 2:

  -   Der Server verfügt über eine private IP-Adresse.

  -   Port 443 auf dem Server ist über den Port 443 der öffentlichen IP-Adresse erreichbar.

  -   VPN-Passthrough ist für Port 443 zulässig.

  -   Der VPN-IPv4-Adresspool befindet sich in einem anderen Bereich der Serveradresse.

  Bei Topologie 2 werden Szenarien mit einem zweiten Server nicht unterstützt.

## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Wie werden allgemeine Aufgaben über Windows PowerShell ausgeführt?
 **Aktivieren von Remotewebzugriff**

```
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]
```

 Beispiel:

```
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers
```

 Mit diesem Befehl wird Remotewebzugriff aktiviert, wobei der Router automatisch konfiguriert wird. Zudem werden die Standardzugriffsberechtigungen für alle vorhandenen Benutzer geändert.

 **Benutzer hinzufügen**

```
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]
```

 Beispiel:

```
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test
```

 Mit diesem Befehl wird ein Administrator namens User2Test with Password Passw0rd! hinzugefügt.

 **Aktivieren/Deaktivieren eines Benutzers**

 Beispiel:

```
$CurrentUser = get-wssuser  œname user2test
$CurrentUser.UserStatus = 0
$CurrentUser.Commit()
```

 Mit diesem Befehl wird der Benutzer mit dem Namen user2test deaktiviert. Durch Festlegen von "UserStatus" auf "1" wird der Benutzer aktiviert.

 **Hinzufügen eines Serverordners**

```
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]
```

 Beispiel:

```
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"
```

 Mit diesem Befehl wird ein Server Ordner mit dem Namen "mytestfolder" am angegebenen Speicherort hinzugefügt.

## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>Gewusst wie der Windows Server Essentials-Domäne einen zweiten Server hinzufügen?
 Da Windows Server Essentials ein Domänen Controller ist, können Sie einen zweiten Server standardmäßig der Domäne hinzufügen.

## <a name="which-email-solutions-can-be-integrated"></a>Welche E-Mail-Lösungen können integriert werden?
 Windows Server Essentials unterstützt die Integration mit zwei Standard-e-Mail-Lösungen: Office 365 und lokales Exchange. Wenn Sie Ihre eigene gehostete e-Mail-Lösung ausführen, müssen Sie ein Add-in entwickeln, um Windows Server Essentials in Ihre gehostete e-Mail-Lösung zu integrieren.

## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>Gewusst wie Migrieren von lokalen Windows SSB (2011/2008/2003) zu der gehosteten Windows Server Essentials-Instanz
 Migrations Handbücher sind für die Migration von lokalen Windows Small Business Server (Windows SSB) zu Windows Server Essentials verfügbar. Manche der darin beschriebenen Schritte entsprechen ggf. nicht genau Ihrer gehosteten Umgebung. Die allgemeinen Aufgaben und die Arbeitsauslastungen, die zu migrieren sind, sollten jedoch die gleichen sein. Es wird empfohlen, auf die [Migrationshandbücher](https://go.microsoft.com/fwlink/p/?LinkID=254292) zurückzugreifen und die erforderlichen Anpassungen entsprechend Ihrer Hostingumgebung vorzunehmen.

 Platzieren Sie den Quellserver und den Zielserver am besten im gleichen Subnetz. Falls dies nicht möglich ist, stellen Sie Folgendes sicher:

-   Der interne DNS-Name des Quellservers und des Zielservers können sich gegenseitig erreichen.

-   Alle erforderlichen Ports sind geöffnet.

## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Wie kann ich ein Upgrade von Windows Server Essentials auf Windows Server Standard ausführen?
 Sie können ein Upgrade von Windows Server Essentials auf Windows Server Standard durchführen. Entfernen Sie Sperren und Beschränkungen, und fügen Sie die für Windows Server Standard fehlenden Pakete hinzu. Um weitere Informationen zu erhalten, [laden Sie das Dokument herunter](https://go.microsoft.com/fwlink/p/?LinkID=253181).

## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>Welche systemeigenen Tools sind für Überwachung und Verwaltung verfügbar?

### <a name="group-policy-management"></a>Gruppenrichtlinienverwaltung
 Windows Server Essentials nutzt systemeigene Gruppenrichtlinie Unterstützung in Windows Server 2012 und stellt die Benutzeroberfläche zum Konfigurieren der Ordner Umleitung und Sicherheitseinstellungen bereit.

> [!NOTE]
>  In einer gehosteten Umgebung kann bei aktivierter Ordnerumleitung für ein Benutzerprofil das Anmelden von Endbenutzern länger dauern, wenn die Datengröße erheblich ist.

### <a name="management-pack"></a>Management Pack
 Das Windows Server Essentials-Management Pack bietet Überwachungsfunktionen über das Integritäts Warnungs System in Windows Server Essentials, damit Hoster eine große Anzahl von Windows Server Essentials-Servern verwalten können, die für verschiedene kleine Unternehmen vorgesehen sind. Die Überwachung in dieser Version umfasst nur kritische Warnungen im System.

#### <a name="management-pack-scope"></a>Umfang des Management Packs
 Diese Management Pack unterstützt Sie bei der Überwachung von Features, die für Windows Server Essentials spezifisch sind. Sie können damit keine Funktionen des Windows Server 2012 Standard-Betriebssystems überwachen. Um Windows Server Essentials zu überwachen, sollten Sie sowohl das Windows Server Essentials-Management Pack als auch das Management Pack für Windows Server 2012 Standard verwenden.

#### <a name="mandatory-configuration"></a>Erforderliche Konfiguration
 Bevor Sie das Management Pack verwenden können, müssen Sie folgende Schritte ausführen:

1.  Installieren Sie den Agent, und konfigurieren Sie die Vertrauensstellung mithilfe der Zertifikatvertrauensstellung. Da Windows Server Essentials als Domänen Controller vorkonfiguriert ist und keine Vertrauensstellung mit anderen Domänen oder Gesamtstrukturen aufweisen kann, sollte der System Center Operations Manager-Agent unter Windows Server Essentials installiert und die Vertrauensstellung mit den Management Server mithilfe von Zertifikaten konfiguriert werden.

2.  Laden Sie das Management Pack herunter. Zum Überwachen von Windows Server Essentials mithilfe von Operations Manager 2007 müssen Sie zunächst das [Windows Server-Betriebs System-Management Pack](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010) aus dem Management Pack-Katalog herunterladen.

3.  Importieren Sie die Management Pack-Datei. Wenn Sie eine lokalisierte Version des Management Packs verwenden, müssen Sie sowohl die Hauptdatei des Management Packs als auch das Sprachpaket importieren.

#### <a name="files-in-this-monitoring-pack"></a>Dateien in diesem Überwachungspaket
 Das Überwachungspaket für Windows Server Essentials umfasst die folgenden Dateien:

-   Microsoft.Windows.Server.2012.Essentials.mp

-   Microsoft. Windows. Server. 2012. Essentials. <locale \> . MP

### <a name="back-up-and-restore"></a>Sichern und Wiederherstellen
 Mit Windows Server Essentials können Sie sowohl den Server als auch den Client sichern.

#### <a name="back-up-the-server"></a>Sichern des Servers
 Windows Server Essentials unterstützt zwei Methoden zum Sichern des Servers: lokale Sicherungen und externe Sicherungen.

 Mithilfe der **lokalen Sicherung** können Sie regelmäßig eine inkrementelle Sicherung auf Blockebene auf einem separaten Datenträger ausführen. Als Host können Sie einen virtuellen Datenträger an die Windows Server Essentials-VM anfügen und die Server Sicherung auf diesem virtuellen Datenträger konfigurieren. Die virtuelle Festplatte sollte sich auf einem anderen physischen Datenträger als der Windows Server Essentials-VM befinden.

- Wenn Sie über einen anderen Mechanismus zum Sichern der Windows Server Essentials-VM verfügen, und Sie nicht möchten, dass der Benutzer die native Server Backup-Funktion von Windows Server Essentials anzeigen kann, können Sie Sie deaktivieren und die gesamte zugehörige Benutzeroberfläche aus dem Windows Server Essentials-Dashboard entfernen. Weitere Informationen finden Sie im Abschnitt "Anpassen der Server Sicherung" im [ADK-Dokument](https://go.microsoft.com/fwlink/p/?LinkID=249124).

  Mithilfe der **externen Sicherung** können Sie die Serverdaten regelmäßig in einem Cloud-Dienst sichern. Sie können das Microsoft Azure Backup-Integrationsmodul für Windows Server Essentials herunterladen und installieren, um die von Microsoft bereitgestellten Azure Backup zu nutzen.

  Führen Sie folgende Aktionen aus, wenn Sie oder Ihre Benutzer einen anderen Cloud-Dienst bevorzugen:

1.  Aktualisieren Sie die Benutzeroberfläche des Windows Server Essentials-Dashboards, sodass es einen Link zu Ihrem bevorzugten clouddienst anstelle der Standard Azure Backup enthält. Weitere Informationen finden Sie im Abschnitt "Anpassen des Abbilds" im [ADK-Dokument](https://go.microsoft.com/fwlink/p/?LinkID=249124).

2.  Optionale Entwickeln Sie ein Add-in für das Windows Server Essentials-Dashboard, um den cloudsicherungsdienst zu konfigurieren und zu verwalten.

#### <a name="back-up-the-client"></a>Sichern des Clients
 Windows Server Essentials unterstützt zwei Arten der Client Datensicherung: vollständige Client Sicherung und Datei Versionsgeschichte.

> [!NOTE]
>  Die Clientsicherung kann sich auf die Leistung auswirken, da die Daten über VPN vom Client an den Server übertragen werden müssen.

 Die **vollständige Client Sicherung** ist standardmäßig für alle Client Geräte aktiviert, die mit dem Windows Server Essentials-Netzwerk verbunden sind. Bei der vollständigen Clientsicherung wird der komplette Client (System und Daten) inkrementell gesichert und die Datendeduplizierung unterstützt. Die Sicherungsdaten befinden sich auf dem Server, auf dem Windows Server Essentials ausgeführt wird. Ein Client, auf dem ein Fehler aufgetreten ist, kann seine Daten auf einen früheren Sicherungspunkt wiederherstellen. Sie können diese Funktion deaktivieren, indem Sie die Schritte im Abschnitt Erstellen der Cfg.ini Datei im [ADK-Dokument](https://technet.microsoft.com/library/jj200150)ausführen.

 Beachten Sie vor einer vollständigen Clientsicherung Folgendes:

- Leistung: Die erste Clientsicherung kann aufgrund der Menge an hochzuladenden Daten zeitaufwändig sein.

- Stabilität: Es kann vorkommen, dass die Internetverbindung auf Clientseite nicht stabil ist. Die Clientsicherung ist fortsetzbar, und der Standardprüfpunkt liegt bei 40 GB (die Clientsicherungsdatenbank erstellt immer dann einen Prüfpunkt, wenn 40 GB Daten gesichert wurden). Sie können diesen Wert in einen kleineren Wert ändern, wenn die Internetverbindung nicht zuverlässig ist.

  -   Zum Aktivieren eines Prüfpunktauftrags legen Sie auf dem Server den Registrierungsschlüssel "HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs" auf "1" fest.

  -   Zum Ändern des Schwellenwerts für den Prüfpunkt ändern Sie auf dem Client den Standardwert (40 GB) von "HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold".

- Bare-Metal-Recovery des Clients: Da Windows Preinstall Environment keine VPN-Verbindungen unterstützt, wird die Bare-Metal-Recovery des Clients nicht unterstützt.

  Der **Datei Versionsverlauf** ist eine Windows 8.1 Funktion zum Sichern von Profildaten (Bibliotheken, Desktop, Kontakte, Favoriten) auf einer Netzwerkfreigabe. In Windows Server Essentials wird die zentrale Verwaltung der Datei Versions Verlaufs Einstellung für alle Windows 8.1 Clients ermöglicht, die mit Windows Server Essentials verknüpft sind. Die Sicherungsdaten werden auf dem Server gespeichert, auf dem Windows Server Essentials ausgeführt wird. Sie können diese Funktion deaktivieren, indem Sie die Schritte im Abschnitt Erstellen der Cfg.ini Datei im [ADK-Dokument](https://technet.microsoft.com/library/jj200150)ausführen.

### <a name="storage-management"></a>Speicherverwaltung
 Mithilfe des [neuen Features "Speicherplätze"](https://technet.microsoft.com/library/hh831739.aspx) können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren, Festplatten dynamisch hinzufügen und Datenvolumes mit bestimmten Ausfallsicherheitsstufen erstellen. Sie können auch einen iSCSI-Datenträger an Windows Server Essentials anfügen, um den Speicher zu erweitern.

## <a name="what-are-the-main-scenarios-i-should-test"></a>Welche Szenarien sollten hauptsächlich getestet werden?
 Aus der Perspektive des Hostens sollten Sie am besten folgende Szenarien testen:

 **Server Bereitstellung**

- Stellen Sie den Windows Server Essentials-Server in der Lab-Umgebung bereit.

- Anpassen des Windows Server Essentials-Images nach Bedarf.

- Automatisieren der Windows Server Essentials-Bereitstellung mit unbeaufsichtigten Dateien und cfg.ini.

- Migrieren Sie lokale Windows SSB zu gehosteten Windows Server Essentials.

- Führen Sie ein Upgrade von Windows Server Essentials auf Windows Server 2012 aus.

  **Server Konfiguration**

- Konfigurieren von Zugriff überall (VPN, Remotewebzugriff, Direktzugriff)

- Konfigurieren des Speicher- und des Serverordners

- (Falls zutreffend) Konfigurieren von Serversicherung, Onlinesicherung, Clientsicherung, File History

- (Falls zutreffend) Konfigurieren und Verwalten von Speicherplätzen

- (Falls zutreffend) Konfigurieren der Integration der E-Mail-Lösung (Office 365, gehosteter Exchange-Dienst usw.)

- (Falls zutreffend) Konfigurieren des Medienservers

  **Server Management**

- Verwalten von Benutzern

- Konfigurieren und Empfangen von E-Mail-Benachrichtigungen für Warnungen

- Ausführen von BPA bei einem Fehler/einer Warnung

- Konfigurieren Sie System Center Monitoring Pack.

- Konfigurieren der Serverwiederherstellung im Falle einer Beschädigung

  **Client Darstellung**

- Clientbereitstellung über das Internet (PC oder Mac OS).

- Zugreifen auf den freigegebenen Ordner über das Launchpad auf dem Client

- Zugreifen auf Serverressourcen über Remotewebzugriff von verschiedenen Geräten (PC, Telefon, Tablet) aus

- Eigener Server-App für Windows Phone

- (Falls zutreffend) Dateiversionsverlauf, Clientsicherung und -wiederherstellung (keine BMR), Ordnerumleitung

- (Falls zutreffend) Integration der E-Mail-Lösung in die Umgebung

## <a name="where-can-i-get-more-support"></a>Wo ist weiterer Support zu finden?
 Sie können die SDK- und ADK-Dokumente unter folgenden Links abrufen:

- [SDK](https://go.microsoft.com/fwlink/p/?LinkID=248648)

- [ADK](https://go.microsoft.com/fwlink/p/?LinkID=249124)

  Fehler können Sie über Connect dem für Funktionen zuständigen Team melden. Zum Generieren der Logs zippen Sie den Ordner und den Server und die Clients, die dem Server beitreten: C:\ProgramData\Microsoft\Windows Server\Logs.
