---
title: Gehosteten Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: 23e586c22ca14af7b02550e2fa1c9522e379170c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="hosted-windows-server-essentials"></a>Gehosteten Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Dokument enthält spezifische Informationen für Hostinganbieter, die Windows Server Essentials in ihrer testumgebung bereitstellen und Windows Server Essentials als Dienst ihren Kunden anbieten möchten.  
  
## <a name="what-is-windows-server-essentials"></a>Was ist Windows Server Essentials?  
 Windows Server Essentials ist eine standortübergreifenden Lösung für kleine Unternehmen, worin der erstklassigen, 64-Bit-produkttechnologien zum Übermitteln von einer Server-Umgebung für die meisten kleinen Unternehmen geeignet. Die folgenden Technologien sind in Windows Server Essentials enthalten.  
  
 **Server-Betriebssystem:** Windows Server 2012-produkttechnologien bilden das Kernstück von Windows Server Essentials. Weitere Informationen finden Sie auf der [Windows Server 2012-Website](https://www.microsoft.com/en-us/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh).  
  
 **Schutz von Daten:** Windows Server Essentials nutzt mehrere neue Funktionen in Windows Server 2012, um einen stark verbesserten Datenschutz bereitzustellen. Die [neue Feature "Speicherplätze"](https://technet.microsoft.com/library/hh831739.aspx) können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren dynamisch Festplatten hinzufügen und Datenvolumes mit bestimmten ausfallsicherheitsstufen erstellen. Führen Sie Windows Server Essentials kann vollständige systemsicherungen und bare-Metal-Recoverys des Servers selbst als auch für die Clientcomputer mit dem Netzwerk verbunden? nun mit Unterstützung für Volumes, die größer als 2 TB. Neues in Windows Server 2012, der [Windows Azure Online Backup](https://technet.microsoft.com/library/hh831419.aspx) kann zum Schützen von Dateien und Ordner in einem cloudbasierten Speicherdienst, die von Microsoft verwaltet wird. Windows Server Essentials auch zentral verwaltet und konfiguriert die Dateiversionsverlauf-Funktion von Windows 8.1-Clients, die Unterstützung der Benutzer beim Wiederherstellen von versehentlich gelöschte oder überschriebene Dateien ohne Unterstützung durch den Administrator.  
  
 **Überall Zugriff:** Remotewebzugriff bietet eine optimierte, Fingereingabe geeignete Browserfunktionen, für den Zugriff auf Anwendungen und Daten von praktisch überall aus, den Sie eine Internetverbindung und über fast alle Geräte verfügen. Windows Server Essentials enthält zudem eine aktualisierte Windows Phone-app und eine neue app für Windows 8.1-Client Computern, zulassen, dass Benutzer intuitiv eine Verbindung herstellen möchten, um zu durchsuchen und Zugriff auf Dateien und Ordner auf dem Server. Dateien werden auch automatisch für den Offlinezugriff zwischengespeichert und synchronisiert, sobald eine Verbindung mit dem Server verfügbar ist. Windows Server Essentials wird die Einrichtung virtuellen privaten Netzwerk (VPN) in ein Kinderspiel Assistenten-gesteuerte-Prozess von nur wenigen Klicks und vereinfacht die Verwaltung von VPN-Zugriff für Benutzer. Clientcomputer können eine VPN-Verbindung Windows SBS-Umgebung, ohne dass Amt auch Remote Beitritt zu nutzen.  
  
 **Flexibilität bei der arbeitsauslastung:** arbeitet Windows Server Essentials können Kunden auswählen, welche Anwendungen und Dienste lokal und welche in der Cloud ausgeführt. In früheren Versionen enthalten Windows Small Business Server Standard Exchange-Server als Komponente, die Kosten und Komplexität für Kunden hinzugefügt, die cloudbasierte Dienste für messaging und Zusammenarbeit nutzen wollten. Mit Windows Server Essentials können Kunden die gleiche Art von integrierten Verwaltungsfunktionen nutzen, ob sie eine lokale Kopie von Exchange Server ausführen, einen gehosteten Exchange-Dienst abonnieren oder Microsoft Office 365 abonnieren möchten.  
  
 **Systemüberwachung:** Windows Server Essentials überwacht den eigenen Integritätsstatus und den Status von Clientcomputern unter Windows 8.1, Windows 7 und Mac OS X, Version 10.5 und höher. Integritätsstatus benachrichtigt Sie bei Problemen im Zusammenhang mit computersicherungen, Serverspeicher, wenig Speicherplatz und vieles mehr.  
  
 **Erweiterbarkeit:** Windows Server Essentials baut auf dem Erweiterungsmodell von Windows SBS 2011 Essentials, die anderen Softwareherstellern, dem Kernprodukt Funktionen und Features hinzufügen können, und fügt ein neuer Satz von Web-services-APIs. Sichert auch Kompatibilität mit den vorhandenen [Software Development Kit](https://msdn.microsoft.com/library/gg513958.aspx) (SDK) und [-add-ins](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials) für Windows SBS 2011 Essentials erstellt wurden.  
  
## <a name="how-can-i-customize-an-image"></a>Wie kann ich ein Abbild angepasst?  
 Finden Sie in der [Windows Server Essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124), die einen standardmäßigen Windows Server Sysprep-Vorgang mit zusätzlichen anpassungsschritten für Windows Server Essentials ist. Führen Sie zum Beenden der Anpassung die Anweisungen im [Erstellen eines einfachen angepassten Abbilds](https://technet.microsoft.com/en-us/library/jj200117) und [Anpassen des Abbilds](https://technet.microsoft.com/en-us/library/jj200161), und folgen Sie dann die Anweisungen im [Vorbereiten des Abbilds für die Bereitstellung](https://technet.microsoft.com/en-us/library/jj200142) um das endgültige Abbild aufzuzeichnen.  
  
 Achten Sie besonders auf die folgenden Punkte:  
  
1.  Sie sollten die anfängliche Konfiguration (IC) durch Hinzufügen einer Datei "skipic.txt" in das Stammverzeichnis eines beliebigen Laufwerks überspringen. Drücken Sie nach dem Installieren des Servers vor der Erstkonfiguration UMSCHALT + F10, um das Befehlsfenster zu starten, und erstellen Sie eine Datei "skipic.txt" unter C: / befindet. Nach dem anpassen müssen Sie bedenken, um die Datei "skipic.txt" zu löschen.  
  
2.  Wenn Sie Windows Server Essentials auf einem Datenträger, die kleiner als 90 GB bereitstellen müssen, sollten Sie einen Registrierungsschlüssel, bevor Sie Sysprep hinzufügen:  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
 Nachdem Sysprep können Sie das Datenträgerabbild oder Reseal wieder in "Install.wim" für die neue Bereitstellung.  
  
 Wenn Sie Virtual Machine Manager verwenden, können Sie eine Vorlage mithilfe der ausgeführten Instanz erstellen. Erstellen einer Vorlage wird Sysprep für die Instanz und den Server Herunterfahren. Nachdem Sie es in der Bibliothek speichern, können Sie die Instanz auf einem Fall aufrufen.  
  
##  <a name="BKMK_automatedeployment"></a>Wie automatisieren kann ich die Bereitstellung?  
 Nachdem Sie das angepasste Image erhalten haben, können Sie die Bereitstellung mit dem eigenen Abbild tun. Um eine teilweise unbeaufsichtigte Installation ausführen können, müssen Sie angeben/Bereitstellen der Datei "Unattend.xml" für WinPE-Setup. Um eine vollständig unbeaufsichtigte Installation ausführen können, müssen Sie auch die Datei "cfg.ini" für Windows Server Essentials-Erstkonfiguration angeben.  
  
1.  Führen Sie nur für die unbeaufsichtigte Installation WinPE-Setup. Dies wird nur das WinPE-Setup automatisieren und die Installation wird vor der Erstkonfiguration angehalten werden soll, sodass die Endbenutzer Corp-Domäne und Administrator Informationen selbst nach RDP in Server-Sitzung verfügbar sind. Dazu:  
  
    1.  Geben Sie die Windows-Datei "Unattend.xml"-Datei. Führen Sie die [Windows 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) zum Generieren der das, und geben alle erforderlichen Informationen, einschließlich Servernamen, Product Keys und das Administratorkennwort. Geben Sie in der Microsoft-Windows-Setup-Abschnitt der Datei "Unattend.xml" die Informationen wie folgt.  
  
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
  
    2.  RDP-Port 3389 muss eine öffentliche IP-geöffnet werden, sodass der Kunde Administrator und das Kennwort in der Datei "Unattend.xml" RDP in den Server angegebene verwenden kann, um die Erstkonfiguration abzuschließen.  
  
    > [!NOTE]
    >  Wenn Sie das Standardkennwort nicht ändern, beendet die Server-Installation auf dem Bildschirm die Frage ein Kennwort eingegeben werden. **Hinweis** Endbenutzer müssen das Standardadministratorkonto verwenden, melden Sie sich an den Server und die Erstkonfiguration auszuführen.  
  
 Wenn Sie Virtual Machine Manager verwenden, können Sie das Administratorkennwort in der Konsole angeben, wenn Sie eine neue Instanz aus der Vorlage erstellen.  
  
1.  Führen Sie vollständig unbeaufsichtigtes Setup einschließlich einer unbeaufsichtigten Erstkonfiguration. Dazu:  
  
    1.  Geben Sie die Datei "Unattend.xml" wie oben, wenn die Bereitstellung von WinPE-Setup wird gestartet.  
  
    2.  Finden Sie in der Windows Server Essentials ADK im Abschnitt [Erstellen der Datei "cfg.ini"](https://technet.microsoft.com/en-us/library/jj200150), um die Datei "cfg.ini" zu generieren.  
  
    3.  Finden Sie Informationen in [InitialConfiguration].  
  
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
  
    4.  Finden Sie Informationen in [PostOSInstall].  
  
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
  
    5.  Wenn Sie den Parameter WebDomainName bereitstellen, stellen Sie sicher, dass der DNS-Eintrag auch aktualisiert wird, auf dem Server s öffentliche IP-Adresse verweisen.  
  
    6.  Wenn Sie die oben aufgeführten Angaben WebDomainName nicht erhalten haben, stellen Sie sicher, dass Port 3389 zu öffnen, damit Kunden RDP verwenden können, um eine Verbindung mit dem Server herstellen und VPN-Konfigurationen abschließen.  
  
> [!NOTE]
>  Stellen Sie sicher, dass die Zeitzoneneinstellung von VM-Hostservern und der VM mit Windows Server Essentials übereinstimmen. Andernfalls können verschiedene Fehler auftreten (Erstkonfiguration fehlschlagen, da auf Zertifikat Aufgaben im Zusammenhang mit Zertifikat funktioniert ggf. erst einige Stunden nach der Installation; Geräteinformationen werden nicht korrekt aktualisiert und so weiter).  
  
 Überprüfen Sie nach der Bereitstellung die folgenden Registrierungsschlüssel unter HKLM\software\microsoft\windows Server\setup überprüfen, ob die Erstkonfiguration erfolgreich war. Wenn SetupStage == ICDone & & ICStatus == 1, bedeutet dies die Erstkonfiguration erfolgreich abgeschlossen.  
  
## <a name="what-is-the-supported-network-topology"></a>Was ist die unterstützte Netzwerktopologie aus?  
 Um Windows Server Essentials von einem roamingclient aus zu verwenden, muss VPN aktiviert werden. Es wird empfohlen, Port 443 für VPN-SSTP-Verbindungen zu aktivieren. Wenn die Funktion "Medienserver" für Remotewebzugriff oder Webdienst-apps erforderlich ist, sollte auch Port 80 aktiviert werden.  
  
 Die VPN-Aktivierung kann während der unbeaufsichtigten Bereitstellung über das Windows PowerShell-Skript erfolgen, oder mithilfe des Assistenten nach der Erstkonfiguration konfiguriert werden.  
  

-   Zum Aktivieren von VPN während der unbeaufsichtigten Bereitstellung finden Sie unter [wie kann ich die Bereitstellung automatisieren? ](Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) in diesem Dokument.  

-   Zum Aktivieren von VPN während der unbeaufsichtigten Bereitstellung finden Sie unter [wie kann ich die Bereitstellung automatisieren? ](../install/Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) in diesem Dokument.  

  
-   VPN über Windows PowerShell aktivieren, führen Sie Folgendes Cmdlet mit Administratorrechten, und geben Sie alle erforderlichen Informationen.  
  
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
  
 Wenn Sie eine VPN-Verbindung vor der Übergabe des Servers an Kunden bereitstellen können, stellen Sie sicher, dass Serverport 3389 über das Internet erreichbar ist, sodass Endbenutzer RDP verwenden können, um eine Verbindung mit dem Server herstellen und die Konfiguration selbst durchführen.  
  
 Hier sind zwei typischen serverseitige Netzwerktopologien und die Konfiguration der VPN/Remotewebzugriff Web Access (Konfiguration) konnte:  
  
-   Topologie 1 (bevorzugt)  
  
    -   Server in einem separaten virtuellen Netzwerk unter einem NAT-Gerät.  
  
    -   DHCP-Dienst im virtuellen Netzwerk aktiviert ist oder der Server mit einer statischen IP-Adresse zugewiesen ist.  
  
    -   Server-Port 443 ist über öffentliche IP-Port 443 erreichbar.  
  
    -   VPN-Passthrough ist für Port 443 zulässig.  
  
    -   VPN-IPv4-Adresspool muss im gleichen Subnetz der Serveradresse handelte.  
  
    -   Einem zweiten Server sollte eine statische IP-Adresse im gleichen Subnetz, aber außerhalb des VPN-Adresspools zugewiesen werden.  
  
-   Topologie 2:  
  
    -   Der Server hat eine private IP-Adresse.  
  
    -   Port 443 auf dem Server ist über eine öffentliche IP-Adresse s-Port 443 erreichbar.  
  
    -   VPN-Passthrough ist für Port 443 zulässig.  
  
    -   VPN-IPv4-Adresspool ist in einem anderen Bereich der Serveradresse.  
  
 Bei Topologie 2 werden Szenarien für sekundäre Server nicht unterstützt.  
  
## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Wie werden allgemeine Aufgaben über Windows PowerShell ausgeführt?  
 **Aktivieren des Remotewebzugriffs**  
  
```  
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
```  
  
 Beispiel:  
  
```  
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
```  
  
 Mit diesem Befehl wird Remotewebzugriff aktiviert, mit dem Router automatisch konfiguriert, und die Standardzugriffsberechtigungen für alle vorhandenen Benutzer ändern.  
  
 **Fügen Sie Benutzer hinzu**  
  
```  
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]  
```  
  
 Beispiel:  
  
```  
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce  
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test  
```  
  
 Mit diesem Befehl wird einen Administrator namens User2Test mit Kennwort Passw0rd hinzugefügt.  
  
 **Benutzer aktivieren/deaktivieren**  
  
 Beispiel:  
  
```  
$CurrentUser = get-wssuser  œname user2test  
$CurrentUser.UserStatus = 0  
$CurrentUser.Commit()  
```  
  
 Mit diesem Befehl wird den Benutzer mit dem Namen user2test deaktiviert. "UserStatus" auf 1 festlegen, wird der Benutzer aktiviert werden.  
  
 **Serverordner hinzufügen**  
  
```  
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]  
```  
  
 Beispiel:  
  
```  
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
```  
  
 Mit diesem Befehl wird der Serverordner namens MyTestFolder am angegebenen Speicherort hinzufügen.  
  
## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>Wie füge ich einen zweiten Server mit der Windows Server Essentials-Domäne?  
 Da Windows Server Essentials ein Domänencontroller ist, können Sie einen zweiten Server mit der Domäne in die üblich Art und Weise beitreten.  
  
## <a name="which-email-solutions-can-be-integrated"></a>Welche e-Mail-Lösungen können integriert werden?  
 Windows Server Essentials unterstützt die Integration mit zwei gebrauchsfertigen e-Mail-Lösungen: Office 365 und lokale Exchange. Wenn Sie Ihre eigene gehostete e-Mail-Lösung ausführen, müssen Sie ein Add-in zur Integration von Windows Server Essentials mit dieser e-Mail-Lösung zu entwickeln.  
  
## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>Wie migriere ich lokalen Windows SBS (2011/2008/2003) auf dem gehosteten Windows Server Essentials?  
 Migrationshandbücher sind für lokalen Windows Small Business Server (Windows SBS) für Windows Server Essentials-Migrationen verfügbar. Einige der Schritte gelten möglicherweise nicht genau Ihrer gehosteten Umgebung. Allerdings müssen die allgemeinen Aufgaben und der Arbeitslasten zu migrierende übereinstimmen. Es wird empfohlen, Sie in finden der [Migrationshandbücher](https://go.microsoft.com/fwlink/p/?LinkID=254292) und die erforderlichen Anpassungen entsprechend Ihrer Hostingumgebung vorzunehmen.  
  
 Es wird empfohlen, dass Sie den Quellserver und dem Zielserver im gleichen Subnetz platzieren. Wenn dies nicht möglich ist, sollten Sie Folgendes sicherstellen:  
  
-   Der interne DNS-Name der Quellserver und Zielserver sind jeweils anderen erreichbar.  
  
-   Alle erforderlichen Ports sind geöffnet.  
  
## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Wie kann ich Windows Server Essentials auf Windows Server Standard aktualisieren?  
 Sie können Windows Server Essentials auf Windows Server Standard aktualisieren. Entfernen Sie sperren und Beschränkungen zu, und fügen Sie die Pakete, die in Windows Server Standard fehlen. Weitere Informationen [Herunterladen des Dokuments](https://go.microsoft.com/fwlink/p/?LinkID=253181).  
  
## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>Was sind die systemeigenen Tools zur Überwachung und Verwaltung?  
  
### <a name="group-policy-management"></a>Die Gruppenrichtlinien-Verwaltungskonsole  
 Windows Server Essentials nutzt die systemeigene gruppenrichtlinienunterstützung in Windows Server 2012 und stellt die Benutzeroberfläche zum Konfigurieren der Ordner ordnerumleitung und Sicherheitseinstellungen bereit.  
  
> [!NOTE]
>  In einer gehosteten Umgebung Wenn die ordnerumleitung für ein Benutzerprofil aktiviert ist, kann länger dauern für Endbenutzer anmelden, wenn die Datengröße erheblich ist.  
  
### <a name="management-pack"></a>Management pack  
 Windows Server Essentials Management Pack enthält Überwachungsfunktion über das System der Integrität Warnungen in Windows Server Essentials Hoster große Anzahl von Windows Server Essentials-Servern für verschiedene kleine Unternehmen Unternehmen verwalten können. Die Überwachung in dieser Version umfasst nur kritische Warnungen im System.  
  
#### <a name="management-pack-scope"></a>Umfang des Management Packs  
 Dieses Management Pack können Sie Funktionen von Windows Server Essentials zu überwachen. Features sind nicht überwacht, die im Betriebssystem Windows Server 2012 Standard generisch sind. Um Windows Server Essentials zu überwachen, sollten Sie das Windows Server Essentials-Management Pack und das Management Pack für Windows Server 2012 Standard verwenden.  
  
#### <a name="mandatory-configuration"></a>Obligatorische Konfiguration  
 Die folgenden Schritte müssen ausgeführt werden, bevor Sie das Management Pack verwenden können:  
  
1.  Installieren Sie den Agent, und konfigurieren Sie die Vertrauensstellung mithilfe der zertifikatvertrauensstellung. Da Windows Server Essentials als Domänencontroller vorkonfiguriert ist und Vertrauensstellungen mit anderen Domänen oder Gesamtstrukturen nicht möglich, wird der System Center Operations Manager-Agent auf Windows Server Essentials installiert werden soll und Vertrauensstellung mit der Verwaltungsserver mit Zertifikaten konfiguriert.  
  
2.  Laden Sie das Management Pack herunter. Zum Überwachen von Windows Server Essentials mithilfe von Operations Manager 2007 müssen Sie zunächst Herunterladen der [Windows Server Operating System Management Pack](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010) aus dem Management Pack-Katalog.  
  
3.  Importieren Sie Management Pack-Datei. Wenn Sie eine lokalisierte Version des Management Packs verwenden, müssen Sie sowohl die Hauptdatei des Management Pack-Datei und das Sprachpaket importieren.  
  
#### <a name="files-in-this-monitoring-pack"></a>Dateien in diesem Überwachungspaket  
 Der Monitoring Pack für Windows Server Essentials umfasst die folgenden Dateien:  
  
-   Microsoft.Windows.Server.2012.Essentials.mp  
  
-   MP Microsoft.Windows.Server.2012.Essentials. < Locale\ >  
  
### <a name="back-up-and-restore"></a>Sichern und Wiederherstellen  
 Windows Server Essentials können Sie den Server und den Client sichern.  
  
#### <a name="back-up-the-server"></a>Sichern des Servers  
 Windows Server Essentials unterstützt zwei Methoden zum Sichern des Servers: lokale und externe Sicherung.  
  
 **Lokale Sicherung** können Sie inkrementellen Sicherung auf Blockebene in regelmäßigen Abständen auf einem separaten Datenträger ausführen. Als Hostinganbieter könnten Sie verbinden ein virtuelles Datenträgers mit der VM mit Windows Server Essentials und konfigurieren Server-Sicherung auf diesem virtuellen Datenträger. Der virtuelle Datenträger sollte auf einem anderen physischen Datenträger als die VM mit Windows Server Essentials befinden.  
  
-   Wenn Sie einen anderen Mechanismus, um die VM mit Windows Server Essentials zu sichern, und nicht, dass des Benutzers das systemeigene Windows Server Essentials-Server-Sicherung-Feature finden Sie unter möchten, konnte Sie sie deaktivieren und gesamte zugehörige Benutzeroberfläche aus Windows Server Essentials-Dashboard entfernen. Weitere Informationen finden Sie im Abschnitt Anpassen der Serversicherung der [ADK-Dokument](https://go.microsoft.com/fwlink/p/?LinkID=249124).  
  
 **Externe Sicherung** können Sie in regelmäßigen Abständen Server-Daten in einem Cloud-Dienst sichern. Sie können herunterladen und Installieren der Microsoft Azure Backup-Integration-Modul für Windows Server Essentials zur Nutzung der Azure-Sicherung, die von Microsoft bereitgestellten.  
  
 Wenn Sie oder Ihre Benutzer einen anderen Clouddienst bevorzugen, sollten Sie folgende Schritte ausführen:  
  
1.  Aktualisieren Sie die Benutzeroberfläche des Windows Server Essentials-Dashboard, sodass er einen Link zu dem bevorzugten Cloud-Dienst anstelle des standardmäßigen Azure Backup enthält. Weitere Informationen finden Sie unter Anpassen der Abschnitt "Image" von der [ADK-Dokument](https://go.microsoft.com/fwlink/p/?LinkID=249124).  
  
2.  (Optional) Entwickeln Sie ein Add-In für Windows Server Essentials-Dashboard zum Konfigurieren und Verwalten des Cloud-sicherungsdiensts.  
  
#### <a name="back-up-the-client"></a>Sichern des Clients  
 Windows Server Essentials unterstützt zwei Arten von Daten Clientsicherung: vollständige Clientsicherung und Dateiversionsverlauf.  
  
> [!NOTE]
>  Sichern des Clients kann die Leistung beeinträchtigen, da die Daten über VPN vom Client an den Server übertragen werden müssen.  
  
 **Vollständige Clientsicherung** ist standardmäßig für alle Clientgeräte, die mit dem Windows Server Essentials-Netzwerk verbunden. Der komplette Client (System und Daten) inkrementell gesichert, und die Datendeduplizierung unterstützt. Die Sicherungsdaten werden auf dem Server mit Windows Server Essentials. Ein fehlerhafter Client können Sie seine Daten auf einen früheren Sicherungspunkt abrufen. Sie können diese Funktion deaktivieren anhand der Schritte in den erstellen Abschnitt der Datei "cfg.ini" die [ADK-Dokument](https://technet.microsoft.com/en-us/library/jj200150).  
  
 Beachten vollständigen Clientsicherung Folgendes:  
  
-   Leistung: erste Clientsicherung kann aufgrund der Menge an hochzuladenden Daten zeitaufwändig.  
  
-   Stabilität: in einigen Fällen ist die Internetverbindung nicht zuverlässig auf dem Client. Clientsicherung ist fortsetzbar entwickelt und der standardprüfpunkt liegt bei 40 GB (die clientsicherungsdatenbank wird einen Prüfpunkt erstellt jedes Mal, wenn 40 GB Daten gesichert wurden). Sie können diesen Wert in einen kleineren Wert ändern, wenn Sie davon ausgehen, dass die Internetverbindung nicht zuverlässig ist.  
  
    -   Legen zum Aktivieren eines Auftrags auf dem Server, Registrierungsschlüssel HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs auf 1 fest.  
  
    -   Ändern Sie HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold vom Standardwert (40 GB), um den Prüfpunkt-Schwellenwert, auf dem Client zu ändern.  
  
-   Bare-Metal-Recovery des Clients: Da Windows Preinstall Environment keine VPN-Verbindung nicht unterstützt, wird Clients Bare-Metal-Recovery nicht unterstützt.  
  
 **Dateiversionsverlauf** ist eine Windows 8.1-Funktion zum Sichern von Profildaten (Bibliotheken, Desktop, Kontakte, Favoriten) auf einer Netzwerkfreigabe. In Windows Server Essentials ermöglichen wir die zentrale Verwaltung der Einstellungen für alle Windows 8.1-Clients, die Windows Server Essentials hinzugefügt. Die Sicherungsdaten werden auf dem Windows Server Essentials-Server gespeichert. Sie können diese Funktion deaktivieren anhand der Schritte in das Erstellen der Datei "cfg.ini" Abschnitt der [ADK-Dokument](https://technet.microsoft.com/en-us/library/jj200150).  
  
### <a name="storage-management"></a>Speicherverwaltung  
 Die [neue Feature "Speicherplätze"](https://technet.microsoft.com/library/hh831739.aspx) können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren dynamisch Festplatten hinzufügen und Datenvolumes mit bestimmten ausfallsicherheitsstufen erstellen. Sie können auch einen iSCSI-Datenträger auf Windows Server Essentials auf den Speicher zu erweitern anfügen.  
  
## <a name="what-are-the-main-scenarios-i-should-test"></a>Was sind die wichtigsten Szenarien, die getestet werden soll?  
 Aus Hostperspektive empfiehlt es sich, dass Sie die folgenden Szenarien testen:  
  
 **Server-Bereitstellung**  
  
-   Bereitstellen von Windows Server Essentials-Server in Ihrer testumgebung.  
  
-   Passen Sie das Windows Server Essentials-Image nach Bedarf an.  
  
-   Automatisieren der Windows Server Essentials-Bereitstellung mit einer unbeaufsichtigten Datei und die Datei "cfg.ini".  
  
-   Migrieren Sie lokale Windows SBS zu gehosteten Windows Server Essentials.  
  
-   Ein Upgrade von Windows Server Essentials zu WindowsServer 2012.  
  
 **Server-Konfiguration**  
  
-   Konfigurieren Sie überall Zugriff (VPN, Remotewebzugriff, DirectAccess).  
  
-   Konfigurieren von Speicher und Server-Ordner.  
  
-   (Falls zutreffend) Konfigurieren von Serversicherung, Onlinesicherung, Clientsicherung, den Dateiversionsverlauf.  
  
-   (Falls zutreffend) Konfigurieren und Verwalten von Speicherplätzen.  
  
-   (Falls zutreffend) Konfigurieren Sie die Integration der e-Mail-Lösung (Office 365 gehosteten Exchange und So weiter).  
  
-   (Falls zutreffend) Konfigurieren des Medienservers.  
  
 **Servermanagement**  
  
-   Verwalten von Benutzern.  
  
-   Konfigurieren und Empfangen von e-Mail-Benachrichtigungen für Warnungen.  
  
-   BPA bei einem Fehler/Warnung ausführen.  
  
-   Konfigurieren Sie System Center Monitoring Pack.  
  
-   Konfigurieren der serverwiederherstellung im Falle einer Beschädigung.  
  
 **Client-Benutzeroberfläche**  
  
-   Clientbereitstellung über das Internet (PC oder Mac OS).  
  
-   Verwenden Sie Launchpad auf dem Client, um den Zugriff auf freigegebene Ordner.  
  
-   Zugreifen auf des Serverressourcen über Remotewebzugriff von verschiedenen Geräten (PC, Telefon, Tablet).  
  
-   My Server-app für Windows Phone.  
  
-   (Falls zutreffend) Dateiversionsverlauf, Clientsicherung und-Wiederherstellung (keine BMR), Ordnerumleitung.  
  
-   (Falls zutreffend) E-Mail-integrationsumgebung.  
  
## <a name="where-can-i-get-more-support"></a>Wo erhalte ich weitere Unterstützung?  
 Sie können die SDK- und ADK-Dokumente unter folgenden Links abrufen:  
  
-   [SDK](https://go.microsoft.com/fwlink/p/?LinkID=248648)  
  
-   [ADK](https://go.microsoft.com/fwlink/p/?LinkID=249124)  
  
 Sie können das Feature-Team über Connect einen Fehler melden. Zum Generieren der Logs zippen Sie den Ordner auf dem Server und den Clients, auf dem Server beitreten: C:\ProgramData\Microsoft\Windows Server\Logs.
