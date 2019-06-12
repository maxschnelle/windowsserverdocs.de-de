---
title: Gehostete Windows Server Essentials-Lösung
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fda5628c-ad23-49de-8d94-430a4f253802
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: dded002df4ed0bbd70c549a8841b769a77f2fd6a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433544"
---
# <a name="hosted-windows-server-essentials"></a>Gehostete Windows Server Essentials-Lösung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Dokument enthält spezifische Informationen für Hostinganbieter, die Windows Server Essentials in ihrer testumgebung bereitstellen und ihren Kunden Windows Server Essentials als einen Dienst anbieten möchten.  
  
## <a name="what-is-windows-server-essentials"></a>Was ist Windows Server Essentials?  
 Windows Server Essentials ist eine standortübergreifende Lösung für kleine Unternehmen, die auch Best-of-Breed-, 64-Bit-Produkt-Technologien, um eine serverumgebung eignet sich gut für den Großteil der kleine Unternehmen bereitzustellen. Die folgenden Technologien sind in Windows Server Essentials enthalten.  
  
 **Server-Betriebssystem:** Windows Server 2012-produkttechnologien bilden, das Kernstück von Windows Server Essentials wird. Weitere Informationen finden Sie auf der Website zu [Windows Server 2012](https://www.microsoft.com/en-us/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh).  
  
 **Datenschutz:** Windows Server Essentials nutzt mehrere neue Funktionen in Windows Server 2012, um stark verbesserten Datenschutz bereitzustellen. Mithilfe des [neuen Features "Speicherplätze"](https://technet.microsoft.com/library/hh831739.aspx) können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren, Festplatten dynamisch hinzufügen und Datenvolumes mit bestimmten Ausfallsicherheitsstufen erstellen. Führen Sie Windows Server Essentials kann vollständige systemsicherungen und bare-Metal-Recoverys des Servers selbst als auch für die Clientcomputer, die mit dem Netzwerk verbunden? jetzt mit Unterstützung für Volumes, die größer als 2 TB. Eine neue Funktion in Windows Server 2012, nämlich [Microsoft Azure Online Backup](https://technet.microsoft.com/library/hh831419.aspx) , kann verwendet werden, um Dateien und Ordner in einem cloudbasierten Speicherdienst zu schützen, der von Microsoft verwaltet wird. Windows Server Essentials auch zentral verwaltet und konfiguriert die Dateiversionsverlauf-Funktion von Windows 8.1-Clients, die Unterstützung von Benutzern beim Wiederherstellen von versehentlich gelöschte oder überschriebene Dateien ohne Unterstützung durch den Administrator.  
  
 **Zugriff überall:** Remotewebzugriff bietet optimale, für die Fingereingabe geeignete Browserfunktionen, um von nahezu allen Orten mit Internetverbindung und über fast alle Geräte auf Anwendungen und Daten zuzugreifen. Windows Server Essentials enthält zudem eine aktualisierte Windows Phone-app und eine neue app für Windows 8.1-Client Computern, sodass Benutzer intuitiv eine Verbindung herstellen, durchsuchen und Zugriff auf Dateien und Ordner auf dem Server. Dateien werden automatisch für den Offlinezugriff zwischengespeichert und synchronisiert, sobald eine Verbindung mit dem Server verfügbar wird. Windows Server Essentials wird die Einrichtung von virtuelle private Netzwerke (VPN) in einen problemlos, assistentengesteuerter Prozess von nur wenigen Klicks, und vereinfacht die Verwaltung von VPN-Zugriff für Benutzer. Clientcomputer können eine VPN-Verbindung nutzen, um remote auf die Windows SBS-Umgebung zuzugreifen, sodass der Weg ins Büro nicht mehr erforderlich ist.  
  
 **Flexibilität bei der Arbeitsauslastung:** Windows Server Essentials wurde entwickelt, können Kunden flexibel wählen, welche Anwendungen und Dienste lokal und welche in der Cloud ausgeführt. In früheren Versionen enthielt Windows Small Business Server Standard als Komponentenprodukt Exchange Server, wodurch Kunden, die cloudbasierte Dienste für Messaging und Zusammenarbeit nutzen wollten, nicht nur mehr Kosten entstanden, sondern auch eine größere Komplexität zu bewältigen hatten. Mit Windows Server Essentials können Kunden die gleiche Art von integrierte Verwaltung nutzen, ob sie eine lokale Kopie von Exchange Server ausführen, einen gehosteten Exchange-Dienst abonnieren oder Microsoft Office 365 abonnieren möchten.  
  
 **Systemüberwachung:** Windows Server Essentials überwacht den eigenen Integritätsstatus und den Status von Clientcomputern mit, Windows 8.1, Windows 7 und Mac OS X, Version 10.5 und höher. Der Integritätsstatus benachrichtigt Sie u. a. bei Problemen im Zusammenhang mit Computersicherungen, dem Serverspeicher und wenig Speicherplatz.  
  
 **Erweiterbarkeit:** Windows Server Essentials baut auf dem Erweiterungsmodell von Windows SBS 2011 Essentials, das ermöglicht es anderen Softwareanbietern, dem Kernprodukt Funktionen und Features hinzuzufügen, und fügt einen neuen Satz von Webdienst-APIs. Das Feature sichert auch Kompatibilität mit dem vorhandenen [Software Development Kit](https://msdn.microsoft.com/library/gg513958.aspx) (SDK) und [Add-Ins](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials) , die für Windows SBS 2011 Essentials erstellt wurden.  
  
## <a name="how-can-i-customize-an-image"></a>Wie wird ein Abbild angepasst?  
 Finden Sie in der [Windows Server Essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124), d.h. einen standardmäßigen Vorgang zur Windows Server Sysprep mit zusätzlichen Windows Server Essentials. Befolgen Sie zum Beenden der Anpassung die Anweisungen unter [Erstellen eines einfachen angepassten Abbilds](https://technet.microsoft.com/library/jj200117) und [Anpassen des Abbilds](https://technet.microsoft.com/library/jj200161). Befolgen Sie dann die Anweisungen unter [Vorbereiten des Abbilds für die Bereitstellung](https://technet.microsoft.com/library/jj200142) , um das endgültige Abbild aufzuzeichnen.  
  
 Beachten Sie folgende Punkte:  
  
1. Überspringen Sie die Erstkonfiguration durch Hinzufügen einer Datei "SkipIC.txt" im Stammverzeichnis eines beliebigen Laufwerks. Drücken Sie nach dem Installieren des Servers vor der Erstkonfiguration UMSCHALT+F10, um das Befehlsfenster zu öffnen und eine Datei "SkipIC.txt" unter "C:/" zu erstellen. Denken Sie nach dem Anpassen daran, die Datei "SkipIC.txt" zu löschen.  
  
2. Wenn Sie Windows Server Essentials auf einem Datenträger, die kleiner als 90 GB bereitstellen möchten, sollten Sie einen Registrierungsschlüssel, bevor Sie Sysprep hinzufügen:  
  
   ```  
   %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
   ```  
  
   Nach der Durchführung der Systemvorbereitung können Sie das Datenträgerabbild, für das die Systemvorbereitung durchgeführt wurde, verwenden oder für eine neue Bereitstellung erneut in "Install.wim" versiegeln.  
  
   Wenn Sie Virtual Machine Manager verwenden, können Sie eine Vorlage mithilfe der ausgeführten Instanz erstellen. Durch das Erstellen einer Vorlage wird für die Instanz eine Systemvorbereitung durchgeführt und der Server heruntergefahren. Nachdem Sie die Instanz in Ihrer Bibliothek gespeichert haben, können Sie sie bei Bedarf jederzeit aufrufen.  
  
##  <a name="BKMK_automatedeployment"></a> Wie wird automatisiert die Bereitstellung?  
 Nachdem Sie das angepasste Abbild aufgezeichnet haben, können Sie die Bereitstellung mit dem eigenen Abbild ausführen. Damit Sie eine teilweise unbeaufsichtigte Installation ausführen können, müssen Sie die Datei "unattend.xml" für WinPE-Setup angeben/bereitstellen. Um eine vollständig unbeaufsichtigte Installation ausführen können, müssen Sie auch die Datei "cfg.ini" für Windows Server Essentials-Erstkonfiguration angeben.  
  
1. Führen Sie nur ein unbeaufsichtigtes WinPE-Setup aus. Dadurch wird nur das WinPE-Setup automatisiert, und die Installation wird vor der Erstkonfiguration angehalten, sodass die Endbenutzer nach dem Herstellen einer RDP-Verbindung mit der Serversitzung Informationen zum Unternehmen, zur Domäne und zum Administrator selbst angeben können. Gehen Sie dazu wie folgt vor:  
  
   1.  Geben Sie die Windows-Datei "unattend.xml" an. Führen Sie die [Windows 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) , generieren die Datei, und geben alle erforderlichen Informationen, einschließlich Servernamen, Product Keys und das Administratorkennwort. Geben Sie in der Microsoft-Windows-Setup-Abschnitt der Datei "Unattend.xml" die Informationen wie unten gezeigt ein.  
  
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
  
   2.  RDP-Port 3389 muss auf eine öffentliche IP-Adresse geöffnet werden, damit der Kunde Administrator und das Kennwort in der Datei "Unattend.xml" für RDP-Verbindungen auf dem Server angegebene verwenden kann, um die Erstkonfiguration abzuschließen.  
  
   > [!NOTE]
   >  Wenn Sie das Standardkennwort nicht ändern, hält die Serverinstallation mit einem Bildschirm an, in dem der Benutzer zur Eingabe eines Kennworts aufgefordert wird.**Hinweis** Endbenutzer müssen das Standardadministratorkonto verwenden, um sich beim Server anzumelden und die Erstkonfiguration auszuführen.  
  
   Wenn Sie Virtual Machine Manager verwenden, können Sie das Administratorkennwort in der Konsole angeben, wenn Sie aus der Vorlage eine neue Instanz erstellen.  
  
2. Führen Sie ein vollständig unbeaufsichtigtes Setup einschließlich einer unbeaufsichtigten Erstkonfiguration aus. Gehen Sie dazu wie folgt vor:  
  
   1.  Geben Sie die Datei "unattend.xml" wie zuvor an, wenn die Bereitstellung von WinPE-Setup aus startet.  
  
   2.  Finden Sie in der Windows Server Essentials ADK im Abschnitt [erstellen Sie die Datei "cfg.ini"](https://technet.microsoft.com/library/jj200150), um die Datei "cfg.ini" zu generieren.  
  
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
  
   5.  Wenn Sie den Parameter "WebDomainName" angeben, stellen Sie sicher, dass der DNS-Eintrag auch aktualisiert wird, sodass Sie um auf dem Server s öffentliche IP-Adresse zu verweisen.  
  
   6.  Wenn Sie die oben stehenden Informationen zum Parameter "WebDomainName" nicht angegeben haben, stellen Sie sicher, Port 3389 zu öffnen, damit Kunden über RDP eine Verbindung mit dem Server herstellen und die VPN-Konfigurationen abschließen können.  
  
> [!NOTE]
>  Stellen Sie sicher, dass die Zeitzone-Einstellung von der VM-Host-Server und die VM mit Windows Server Essentials identisch ist. Wenn dies nicht der Fall ist, können verschiedene Fehler auftreten, z. B. kann bei der Erstkonfiguration bei Aufgaben im Zusammenhang mit Zertifikaten ein Fehler auftreten, ein Zertifikat funktioniert ggf. erst einige Stunden nach der Installation, oder die Geräteinformationen werden nicht korrekt aktualisiert.  
  
 Überprüfen Sie nach der Bereitstellung den folgenden Registrierungsschlüssel unter "HKLM\software\microsoft\windows server\setup", um festzustellen, ob die Erstkonfiguration erfolgreich war. Wenn "SetupStage == ICDone && ICStatus == 1", wurde die Erstkonfiguration erfolgreich abgeschlossen.  
  
## <a name="what-is-the-supported-network-topology"></a>Wie sieht die unterstützte Netzwerktopologie aus?  
 Um Windows Server Essentials von einem roamingclient aus zu verwenden, muss VPN aktiviert werden. Es wird empfohlen, Port 443 für VPN-SSTP-Verbindungen zu aktivieren. Wenn die Funktion "Medienserver" für Remotewebzugriff oder Webdienst-Apps erforderlich ist, muss auch Port 80 aktiviert werden.  
  
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
  
  -   Port 443 auf dem Server ist über eine öffentliche IP-Adresse s Port 443 erreichbar.  
  
  -   VPN-Passthrough ist für Port 443 zulässig.  
  
  -   Der VPN-IPv4-Adresspool befindet sich in einem anderen Bereich der Serveradresse.  
  
  Bei Topologie 2 werden Szenarien mit einem zweiten Server nicht unterstützt.  
  
## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Wie werden allgemeine Aufgaben über Windows PowerShell ausgeführt?  
 **Aktivieren des Remotewebzugriffs**  
  
```  
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
```  
  
 Beispiel:  
  
```  
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
```  
  
 Mit diesem Befehl wird Remotewebzugriff aktiviert, wobei der Router automatisch konfiguriert wird. Zudem werden die Standardzugriffsberechtigungen für alle vorhandenen Benutzer geändert.  
  
 **Fügen Sie Benutzer hinzu**  
  
```  
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]  
```  
  
 Beispiel:  
  
```  
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce  
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test  
```  
  
 Dieser Befehl fügt einen Administrator mit dem Namen "User2Test", und das Kennwort Passw0rd!.  
  
 **Aktivieren/Deaktivieren eines Benutzers**  
  
 Beispiel:  
  
```  
$CurrentUser = get-wssuser  œname user2test  
$CurrentUser.UserStatus = 0  
$CurrentUser.Commit()  
```  
  
 Mit diesem Befehl wird den Benutzer, die mit dem Namen user2test deaktiviert. Durch Festlegen von "UserStatus" auf "1" wird der Benutzer aktiviert.  
  
 **Serverordner hinzufügen**  
  
```  
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]  
```  
  
 Beispiel:  
  
```  
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
```  
  
 Dieser Befehl fügt einen Serverordner namens MyTestFolder an der angegebenen Position.  
  
## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>Wie füge ich einen zweiten Server mit der Windows Server Essentials-Domäne?  
 Da Windows Server Essentials ein Domänencontroller ist, können Sie einen zweiten Server in die Domäne in der standardmäßige Art und Weise verknüpfen.  
  
## <a name="which-email-solutions-can-be-integrated"></a>Welche E-Mail-Lösungen können integriert werden?  
 Windows Server Essentials unterstützt die Integration mit zwei gebrauchsfertigen e-Mail-Lösungen: Office 365 und lokale Exchange-Lösung. Wenn Sie Ihre eigene gehostete e-Mail-Lösung ausführen, müssen Sie ein Add-in zum Integrieren von Windows Server Essentials in Ihre gehostete e-Mail-Lösung entwickeln.  
  
## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>Wie migriere ich die lokale Windows SBS (2011/2008/2003) mit dem gehosteten Windows Server Essentials?  
 Migrationshandbücher sind für die lokalen Windows Small Business Server (Windows SBS) zu Windows Server Essentials-Migrationen verfügbar. Manche der darin beschriebenen Schritte entsprechen ggf. nicht genau Ihrer gehosteten Umgebung. Die allgemeinen Aufgaben und die Arbeitsauslastungen, die zu migrieren sind, sollten jedoch die gleichen sein. Es wird empfohlen, auf die [Migrationshandbücher](https://go.microsoft.com/fwlink/p/?LinkID=254292) zurückzugreifen und die erforderlichen Anpassungen entsprechend Ihrer Hostingumgebung vorzunehmen.  
  
 Platzieren Sie den Quellserver und den Zielserver am besten im gleichen Subnetz. Falls dies nicht möglich ist, stellen Sie Folgendes sicher:  
  
-   Der interne DNS-Name des Quellservers und des Zielservers können sich gegenseitig erreichen.  
  
-   Alle erforderlichen Ports sind geöffnet.  
  
## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Wie kann ich Windows Server Essentials auf Windows Server Standard aktualisieren?  
 Sie können Windows Server Essentials auf Windows Server Standard aktualisieren. Entfernen Sie Sperren und Beschränkungen, und fügen Sie die für Windows Server Standard fehlenden Pakete hinzu. Um weitere Informationen zu erhalten, [laden Sie das Dokument herunter](https://go.microsoft.com/fwlink/p/?LinkID=253181).  
  
## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>Welche systemeigenen Tools sind für Überwachung und Verwaltung verfügbar?  
  
### <a name="group-policy-management"></a>Gruppenrichtlinienverwaltung  
 Windows Server Essentials nutzt die systemeigene gruppenrichtlinienunterstützung in Windows Server 2012 und die Benutzeroberfläche zum Konfigurieren von ordnereinstellungen für ordnerumleitung und Sicherheitseinstellungen bereit.  
  
> [!NOTE]
>  In einer gehosteten Umgebung kann bei aktivierter Ordnerumleitung für ein Benutzerprofil das Anmelden von Endbenutzern länger dauern, wenn die Datengröße erheblich ist.  
  
### <a name="management-pack"></a>Management Pack  
 Management Pack für Windows Server Essentials bietet Überwachungsfunktion erfüllen, über die Integrität Warnungssystem in Windows Server Essentials Hoster, die eine große Anzahl von Windows Server Essentials-Servern für verschiedene kleine Unternehmen verwalten können. Die Überwachung in dieser Version umfasst nur kritische Warnungen im System.  
  
#### <a name="management-pack-scope"></a>Umfang des Management Packs  
 Dieses Management Pack können Sie Funktionen, die speziell für Windows Server Essentials zu überwachen. Sie können damit keine Funktionen des Windows Server 2012 Standard-Betriebssystems überwachen. Um Windows Server Essentials zu überwachen, sollten Sie das Windows Server Essentials-Management Pack und das Management Pack für Windows Server 2012 Standard verwenden.  
  
#### <a name="mandatory-configuration"></a>Erforderliche Konfiguration  
 Bevor Sie das Management Pack verwenden können, müssen Sie folgende Schritte ausführen:  
  
1.  Installieren Sie den Agent, und konfigurieren Sie die Vertrauensstellung mithilfe der Zertifikatvertrauensstellung. Da Windows Server Essentials als Domänencontroller vorkonfiguriert ist und keine Vertrauensstellung mit anderen Domänen oder Gesamtstrukturen, die System Center Operations Manager-Agent auf Windows Server Essentials installiert werden sollte und Vertrauensstellung mit der Verwaltung konfiguriert Server, die mithilfe von Zertifikaten.  
  
2.  Laden Sie das Management Pack herunter. Um Windows Server Essentials mithilfe von Operations Manager 2007 zu überwachen, müssen Sie zunächst Herunterladen der [Windows Server Operating System Management Pack](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010) aus dem Management Pack-Katalog.  
  
3.  Importieren Sie die Management Pack-Datei. Wenn Sie eine lokalisierte Version des Management Packs verwenden, müssen Sie sowohl die Hauptdatei des Management Packs als auch das Sprachpaket importieren.  
  
#### <a name="files-in-this-monitoring-pack"></a>Dateien in diesem Überwachungspaket  
 Monitoring Pack für Windows Server Essentials enthält die folgenden Dateien:  
  
-   Microsoft.Windows.Server.2012.Essentials.mp  
  
-   Microsoft.Windows.Server.2012.Essentials.<locale\>.mp  
  
### <a name="back-up-and-restore"></a>Sichern und Wiederherstellen  
 Windows Server Essentials können Sie sowohl die Server-als auch das Sichern.  
  
#### <a name="back-up-the-server"></a>Sichern des Servers  
 Windows Server Essentials unterstützt zwei Methoden zum Sichern des Servers: lokale und externe Sicherung.  
  
 Mithilfe der**lokalen Sicherung** können Sie regelmäßig eine inkrementelle Sicherung auf Blockebene auf einem separaten Datenträger ausführen. Als Hostinganbieter könnten Sie einen virtuellen Datenträger an die VM mit Windows Server Essentials Anfügen und konfigurieren Sie die serversicherung auf diesem virtuellen Datenträger. Der virtuelle Datenträger sollte auf einem anderen physischen Datenträger als die VM mit Windows Server Essentials befinden.  
  
- Wenn Sie einen anderen Mechanismus zum Sichern der VM mit Windows Server Essentials verfügen und nicht, dass Ihre Benutzer, der systemeigenen Windows Server Essentials-Server-Sicherung-Funktion finden Sie unter möchten, konnte Sie deaktivieren und entfernen Sie die gesamte zugehörige Benutzeroberfläche aus Windows Server Essentials Instrumententafel. Weitere Informationen finden Sie im Abschnitt "Anpassen der Serversicherung" von der [ADK-Dokument](https://go.microsoft.com/fwlink/p/?LinkID=249124).  
  
  Mithilfe der **externen Sicherung** können Sie die Serverdaten regelmäßig in einem Cloud-Dienst sichern. Sie können die herunterladen und installieren Microsoft Azure Backup-Integration-Modul für Windows Server Essentials zum Nutzen der Azure-Sicherung, die von Microsoft bereitgestellt werden.  
  
  Führen Sie folgende Aktionen aus, wenn Sie oder Ihre Benutzer einen anderen Cloud-Dienst bevorzugen:  
  
1.  Aktualisieren Sie die Benutzeroberfläche des Windows Server Essentials-Dashboard, damit, dass es sich um einen Link zu Ihrer bevorzugten Cloud-Dienst anstelle des standardmäßigen Azure Backup bietet. Weitere Informationen finden Sie im Abschnitt "Anpassen des Abbilds" im [ADK-Dokument](https://go.microsoft.com/fwlink/p/?LinkID=249124).  
  
2.  (Optional) Entwickeln Sie ein Add-in für Windows Server Essentials-Dashboard zum Konfigurieren und Verwalten von Cloud-sicherungsdiensts.  
  
#### <a name="back-up-the-client"></a>Sichern des Clients  
 Windows Server Essentials unterstützt zwei Arten von clientdatensicherung: vollständige Clientsicherung und Dateiversionsverlauf.  
  
> [!NOTE]
>  Die Clientsicherung kann sich auf die Leistung auswirken, da die Daten über VPN vom Client an den Server übertragen werden müssen.  
  
 **Vollständige Clientsicherung** ist standardmäßig für alle Client-Geräte, die mit dem Windows Server Essentials-Netzwerk verbunden. Bei der vollständigen Clientsicherung wird der komplette Client (System und Daten) inkrementell gesichert und die Datendeduplizierung unterstützt. Die Sicherungsdaten werden auf dem Server, Windows Server Essentials ausgeführt wird. Ein Client, auf dem ein Fehler aufgetreten ist, kann seine Daten auf einen früheren Sicherungspunkt wiederherstellen. Sie können diese Funktion deaktivieren anhand der Schritte im Erstellen den Datei "cfg.ini" Teil der [ADK-Dokument](https://technet.microsoft.com/library/jj200150).  
  
 Beachten Sie vor einer vollständigen Clientsicherung Folgendes:  
  
- Leistung: Die erste Clientsicherung kann aufgrund der Menge an hochzuladenden Daten zeitaufwändig sein.  
  
- Stabilität: Es kann vorkommen, dass die Internetverbindung auf Clientseite nicht stabil ist. Die Clientsicherung ist fortsetzbar, und der Standardprüfpunkt liegt bei 40 GB (die Clientsicherungsdatenbank erstellt immer dann einen Prüfpunkt, wenn 40 GB Daten gesichert wurden). Sie können diesen Wert in einen kleineren Wert ändern, wenn die Internetverbindung nicht zuverlässig ist.  
  
  -   Zum Aktivieren eines Prüfpunktauftrags legen Sie auf dem Server den Registrierungsschlüssel "HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs" auf "1" fest.  
  
  -   Zum Ändern des Schwellenwerts für den Prüfpunkt ändern Sie auf dem Client den Standardwert (40 GB) von "HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold".  
  
- Bare-Metal-Recovery des Clients: Da Windows Preinstall Environment keine VPN-Verbindungen unterstützt, wird die Bare-Metal-Recovery des Clients nicht unterstützt.  
  
  **Dateiversionsverlauf** ist eine Windows 8.1-Funktion zum Sichern von Profildaten (Bibliotheken, Desktop, Kontakte, Favoriten) auf einer Netzwerkfreigabe. In Windows Server Essentials können zentrale Verwaltung der Dateiversionsverlauf-Einstellung für alle Windows 8.1-Clients, die mit Windows Server Essentials verknüpft. Die Sicherungsdaten werden auf dem Server gespeichert, auf dem Windows Server Essentials ausgeführt wird. Sie können diese Funktion deaktivieren anhand der Schritte im Erstellen den Datei "cfg.ini" Teil der [ADK-Dokument](https://technet.microsoft.com/library/jj200150).  
  
### <a name="storage-management"></a>Speicherverwaltung  
 Mithilfe des [neuen Features "Speicherplätze"](https://technet.microsoft.com/library/hh831739.aspx) können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren, Festplatten dynamisch hinzufügen und Datenvolumes mit bestimmten Ausfallsicherheitsstufen erstellen. Sie können auch einen iSCSI-Datenträger auf Windows Server Essentials auf den Speicher zu erweitern anfügen.  
  
## <a name="what-are-the-main-scenarios-i-should-test"></a>Welche Szenarien sollten hauptsächlich getestet werden?  
 Aus der Perspektive des Hostens sollten Sie am besten folgende Szenarien testen:  
  
 **Server-Bereitstellung**  
  
- Bereitstellen von Windows Server Essentials-Server in Ihrer laborumgebung.  
  
- Anpassen des Windows Server Essentials-Images nach Bedarf.  
  
- Automatisieren der Windows Server Essentials-Bereitstellung mit unbeaufsichtigten Datei und die Datei "cfg.ini".  
  
- Migrieren von lokalen Windows SBS zu gehosteten Windows Server Essentials.  
  
- Upgrade von Windows Server Essentials zu WindowsServer 2012.  
  
  **Server-Konfiguration**  
  
- Konfigurieren von Zugriff überall (VPN, Remotewebzugriff, Direktzugriff)  
  
- Konfigurieren des Speicher- und des Serverordners  
  
- (Falls zutreffend) Konfigurieren von Serversicherung, Onlinesicherung, Clientsicherung, File History  
  
- (Falls zutreffend) Konfigurieren und Verwalten von Speicherplätzen  
  
- (Falls zutreffend) Konfigurieren der Integration der E-Mail-Lösung (Office 365, gehosteter Exchange-Dienst usw.)  
  
- (Falls zutreffend) Konfigurieren des Medienservers  
  
  **Serververwaltung**  
  
- Verwalten der Benutzer  
  
- Konfigurieren und Empfangen von E-Mail-Benachrichtigungen für Warnungen  
  
- Ausführen von BPA bei einem Fehler/einer Warnung  
  
- Konfigurieren Sie System Center Monitoring Pack.  
  
- Konfigurieren der Serverwiederherstellung im Falle einer Beschädigung  
  
  **Clientumgebung**  
  
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
