---
title: Bereitstellen von Windows Server Essentials Experience als gehosteten Server
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a455c6b4-b29f-4f76-8c6b-1578b6537717
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c299d2b5f3d6b48693c473754a5205a7d26b5d6a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Bereitstellen von Windows Server Essentials Experience als gehosteten Server

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Dokument enthält spezifische Informationen für Hostinganbieter, die Microsoft Windows Server-16 mit der Windows Server Essentials Experience-Rolle (bezeichnet als Windows Server Essentials im weiteren Verlauf des Dokuments) installiert in ihrer Testumgebung bereitstellen und Windows Server Essentials-Umgebung als Dienst an ihre Kunden anbieten möchten. Dieses Dokument enthält die folgenden Abschnitte:  
  

-   [Übersicht über die Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Vorteile des Hostens der Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [Unterstützte Bereitstellungsoptionen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [Unterstützte Netzwerktopologien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Anpassen des Images der Windows Server Essentials Experience-Rolle](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Automatisieren der Bereitstellung von Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Migrieren von Daten von Windows Small Business Server zu Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Führen Sie allgemeiner Aufgaben mithilfe von Windows PowerShell aus](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [E-Mail-Integration in Windows Server Essentials](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [Überwachen Sie und verwalten Sie, indem Sie mit systemeigenen Tools](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [Testen von Szenarien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [Informationen zum Support](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

-   [Übersicht über die Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Vorteile des Hostens der Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [Unterstützte Bereitstellungsoptionen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [Unterstützte Netzwerktopologien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Anpassen des Images der Windows Server Essentials Experience-Rolle](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Automatisieren der Bereitstellung von Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Migrieren von Daten von Windows Small Business Server zu Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Führen Sie allgemeiner Aufgaben mithilfe von Windows PowerShell aus](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [E-Mail-Integration in Windows Server Essentials](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [Überwachen Sie und verwalten Sie, indem Sie mit systemeigenen Tools](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [Testen von Szenarien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [Informationen zum Support](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

  
##  <a name="BKMK_WSEEOverview"></a>Übersicht über die Windows Server Essentials Experience  
 Die Windows Server Essentials Experience ist eine Serverrolle, die in der Windows Server2012 R2 Standard und Windows Server2012 R2 Datacenter verfügbar ist. Wenn Windows Server Essentials Experience-Rolle auf einem Server unter Windows Server2012 R2 installiert ist, kann der Kunde alle Features nutzen, die in Windows Server Essentials ohne die Sperren und Beschränkungen verfügbar sind. Die Windows Server Essentials-Umgebung ermöglicht die folgenden standortübergreifenden Lösungen für kleine und mittelständische Unternehmen:  
  
-   **Datenspeicherung und -Schutz** können Sie den Kunden speichern "¢ Daten an einem zentralen Ort und Server und Client Daten schützen, indem Sie die Server- und Clientcomputer (weniger als 75) im Netzwerk sichern.  
  
-   **Benutzerverwaltung** können Sie die Benutzer und Gruppen über das vereinfachte Server-Dashboard verwalten. Darüber hinaus ermöglicht die Integration mit Microsoft Azure Active Directory (Azure AD) einfachen Datenzugriff für Microsoft online Services (z.B. Office365, Exchange Online und SharePoint Online) für Benutzer, mithilfe der Anmeldeinformationen für die Domäne.  
  
-   **Dienstintegration** können Sie den Server mit Microsoft online Services (z.B. Office365 SharePoint Online und Microsoft Azure Backup) integrieren. Sie können auch die Server in Ihre Dienste oder Dienste von Drittanbietern integrieren.  
  
-   **Zugriff überall** der Kunde kann Zugriff auf den Server, Netzwerkcomputer und Daten von praktisch überall sie haben eine Internetverbindung und über fast alle Geräte. Remotewebzugriff können sie Anwendungen und Daten mit einem optimale, Fingereingabe geeignete Browserfunktionen zugreifen. My Server-App können sie Daten aus einer Windows Phone oder Microsoft Store-App zugreifen.  
  
-   **Medienstreaming** Wenn Sie das Medienpaket auf einem Server mit Windows Server Essentials-Umgebung aktiviert installieren, die Endkunden kann Musik, Videos und Fotos in freigegebenen Ordnern speichern, und klicken Sie dann über Computer im Netzwerk oder Remote Web Access auf diese Mediendateien zugreifen.  
  
-   **Überwachung der Integrität** können Sie die Integrität des Netzwerks überwachen und benutzerspezifische Statusberichte abrufen.  
  
##  <a name="BKMK_Benefits"></a>Vorteile des Hostens der Windows Server Essentials Experience  
  Windows Server Essentials Experience ist eine Rolle in Windows Server, daher können Sie das vorhandene bereitstellungs- und verwaltungsframework von Windows Server zum Bereitstellen und Konfigurieren von Windows Server Essentials Experience-Rolle. Windows Server Essentials Experience-Rolle hostet bietet die folgenden Vorteile:  
  
-   **optimierte Bereitstellung** durch Aktivieren der Windows Server Essentials Experience-Rolle, einige der am häufigsten verwendeten Rollen und Features eingeschaltet und mit bewährten Methoden für kleine und mittelständische Unternehmen konfiguriert sind. Sie können die Windows Server Essentials-Funktionen anpassen oder einige der lokalen Funktionen ausblenden. Wenn Sie Windows Azure Pack verwenden, können Sie die Katalogvorlage für Windows Server Essentials Experience auf Windows Server2012 R2 herunterladen.  
  
-   **Vereinfachtes Dashboard** das Windows Server Essentials-Dashboard vereinfacht allgemeine Aufgaben wie das Verwalten der Serverordner, Serverspeicher, Sicherung und Wiederherstellung, Benutzer oder Gruppenkonten, Geräten, Remotezugriff und E-Mail. Kleine und mittelständische Geschäftskunden können anstatt den Helpdesk um technischen Support täglichen Verwaltungsaufgaben ausführen.  
  
-   **Erweiterbarkeit** das Windows Server Essentials-Dashboard und Windows Server Essentials Connector-Software sind erweiterbar. Sie können Ihr eigenes Branding hinzufügen und Dienstintegration, damit Ihre Kunden einen Einstiegspunkt für alles über ihre Server und Dienste haben.  
  
-   **Monitor** eine neue Version von System Center Monitoring Pack zum Überwachen und verwalten mehrere Server mit Windows Server Essentials verfügbar ist. Informationen zum Herunterladen des Management Packs finden Sie unter [System Center Management Pack für Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).  
  
##  <a name="BKMK_SupportedDeployment"></a>Unterstützte Bereitstellungsoptionen  
  Windows Server Essentials Experience können als Domänencontroller in einer neuen Active Directory-Umgebung bereitgestellt werden. oder sie können in einer vorhandenen Active Directory-Umgebung als Mitglied einer Domäne bereitgestellt werden.  
  
 Es wird empfohlen, dass Sie zuerst Windows Server2012 R2 Standard oder Windows Server2012 R2 Datacenter bereitstellen und installieren Sie Windows Server Essentials Experience-Rolle. Mit dieser Bereitstellungsmethode erhalten Sie alle Funktionen der Windows Server Essentials-Edition, jedoch ohne die Sperren und Beschränkungen.  
  

 Weitere Informationen zum Installieren von Windows Server2012 R2 mit Windows Server Essentials Experience-Rolle finden Sie unter [installieren und Konfigurieren von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  


  
##  <a name="BKMK_SupportedToplogy"></a>Unterstützte Netzwerktopologien  
 Um Windows Server Essentials-Umgebung von einem Roamingclient aus zu verwenden, muss VPN aktiviert werden. Um den Remotezugriff auf den Server von einem Roamingclient zu aktivieren, müssen Sie zum Öffnen von Port 443 und Port 80 auf dem Server.  
  
 Nachfolgend sind zwei typischen serverseitige Netzwerktopologien und wie VPN und Remotewebzugriffs konfiguriert werden kann:  
  
-   **Topologie 1** (Dies ist die bevorzugte Topologie, und speichert alle Server und der VPN IP-Adressbereich im gleichen Subnetz.):  
  
    -   Richten Sie den Server in einem separaten virtuellen Netzwerk unter einem Gerät (Network Address Translation, NAT).  
  
    -   Aktivieren Sie den DHCP-Dienst im virtuellen Netzwerk, oder weisen Sie eine statische IP-Adresse für den Server.  
  
    -   Weiterleiten von öffentlichen IP-Port 443 auf dem Router für LAN-Adresse des Servers.  
  
    -   Zulassen von VPN-Passthrough für Port 443.  
  
    -   Legen Sie den VPN-IPv4-Adresspool in demselben Subnetzbereich befinden wie die Serveradresse ein.  
  
    -   Weisen Sie sekundären Servern eine statische IP-Adresse im gleichen Subnetz, aber außerhalb des VPN-Adresspools.  
  
-   **Topologie 2**:  
  
    -   Weisen Sie dem Server eine private IP-Adresse.  
  
    -   Ermöglichen Sie Port 443 auf dem Server um eine öffentliche Port 443-IP-Adresse zu erreichen.  
  
    -   Zulassen von VPN-Passthrough für Port 443.  
  
    -   Weisen Sie verschiedene Bereiche für die VPN-IPv4-Adresspool und Adresse des Servers.  
  
 Bei Topologie 2 werden Szenarien für sekundäre Server nicht unterstützt, da Sie einen anderen Server mit der gleichen Domäne hinzufügen können.  
  
 Sie können VPN während einer unbeaufsichtigten Bereitstellung mithilfe von unseren Windows PowerShell-Skript aktivieren oder mit dem Assistenten nach der Erstkonfiguration konfiguriert werden.  
  
 Aktivieren von VPN mithilfe von Windows PowerShell, führen den folgenden Befehl mit Administratorrechten auf dem Server mit Windows Server Essentials und alle erforderlichen Informationen bereitzustellen.  
  
```  
##  
## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
##  
  
$myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
$mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
$mySslCertificatePassword = ConvertTo-SecureString  œAsPlainText  œForce '******';   ## password for private key of the SSL certificate  
$skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
Set-WssDomainNameConfiguration  œDomainName $myExternalDomainName  œCertificatePath $mySslCertificateFile  œCertificateFilePassword $mySslCertificatePassword  œNoCertificateVerification  
##  
## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
##  
  
Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
  
```  
  
> [!NOTE]
>  Wenn Sie eine VPN-Verbindung bereitstellen können, bevor der Kunde den Server wird, stellen Sie sicher, dass Serverport 3389 über das Internet erreichbar ist, damit der Kunde kann Remote Desktop Protocol verwenden, um mit dem Server verbinden, und konfigurieren Sie ihn.  
  
##  <a name="BKMK_CustomizeImage"></a>Anpassen des Images der Windows Server Essentials Experience-Rolle  
 Sie können das Image anpassen, vor dem Konfigurieren der Windows Server Essentials Experience-Rolle. Weitere Informationen zu standardmäßigen Windows Server Sysprep-Prozess finden Sie unter [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx). Nachdem Sie das Image mithilfe von Sysprep vorbereitet haben, können Sie es verwenden oder erneut versiegeln in Install.wim für eine neue Bereitstellung.  
  
 Wenn Sie Virtual Machine Manager verwenden, können Sie eine Vorlage mithilfe der ausgeführten Instanz erstellen. Dieser Vorgang mithilfe von Sysprep zum Vorbereiten der Instanz ein, und fährt den Computer. Nachdem Sie die Vorlage in der Bibliothek speichern, können Sie es auf einem Fall.  
  
 Nach der Installation von Windows Server Essentials Experience-Rolle können Sie die Features in Windows Server Essentials anpassen. Eine der wichtigsten Anpassungen ist der **IsHosted** Registrierungsschlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\Deployment\IsHosted**.  
  
 Wenn dieser Schlüssel auf 0 x 1 festgelegt ist, werden einige der Features auf lokalen Verhalten geändert. Diese Funktion Änderungen:  
  
-   **Clientsicherung** Clientsicherung ist für neu verbundene Clientcomputer standardmäßig deaktiviert.  
  
-   **Clientwiederherstellungsdienst** Clientwiederherstellungsdienst wird deaktiviert, und die Benutzeroberfläche wird mehr über das Dashboard.  
  
-   **Dateiversionsverlauf** dateiversionsverlaufseinstellungen für neu erstellte Benutzerkonten werden vom Server nicht automatisch verwaltet.  
  
-   **Server-Sicherung** serversicherungsdienst wird deaktiviert, und die Benutzeroberfläche des Server-Sicherung über das Dashboard ausgeblendet.  
  
-   **Speicherplätze** über das Dashboard wird die Benutzeroberfläche für das Erstellen oder Verwalten von Speicherplätzen ausgeblendet werden.  
  
-   **Überall** Router- und VPN-Konfiguration wird standardmäßig übersprungen, wenn Sie den Anywhere Access-Assistenten ausführen.  
  
 Wenn Sie das Verhalten der einzelnen aufgeführten Funktionen steuern möchten, können Sie den entsprechenden Registrierungsschlüssel für jede festlegen. Informationen dazu, wie Sie den Registrierungsschlüssel festlegen, finden Sie unter der [anpassen und Bereitstellen von Windows Server Essentials in Windows Server2012 R2](https://technet.microsoft.com/library/dn293241.aspx)  
  
##  <a name="BKMK_AutomateDeployment"></a>Automatisieren der Bereitstellung von Windows Server Essentials Experience  
 Zum Automatisieren der Bereitstellung müssen Sie zunächst das Betriebssystem bereitstellen und installieren Sie Windows Server Essentials Experience-Rolle.  
  
-   Folgen Sie den Anweisungen, um automatisch Bereitstellen von Windows Server2012 R2 Standard oder Windows Server2012 R2 Datacenter [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx).  
  
-   Vorgehensweise beim Installieren der Windows Server Essentials Experience-Rolle mithilfe von Windows PowerShell finden Sie unter [installieren und Konfigurieren von Windows Server Essentials](https://technet.microsoft.com/library/dn281793.aspx).  
  
> [!NOTE]
>  Stellen Sie sicher, dass die Einstellungen für die virtuellen Hostcomputers und der Windows Server Essentials Experience Zeitzone entsprechen. Andernfalls können verschiedene Fehler auftreten. Dazu gehören: die Erstkonfiguration des Servers möglicherweise nicht erfolgreich in zertifikatsspezifischen Aufgaben, die das Zertifikat funktioniert ggf. erst einige Stunden nach Windows Server Essentials Experience-Rolle installiert ist, und Geräteinformationen werden nicht korrekt aktualisiert.  
  
 Verwenden Sie nach der Bereitstellung des Windows PowerShell-Cmdlets **Get-WssConfigurationStatus** überprüfen, ob die Erstkonfiguration erfolgreich war. Der zurückgegebene Status sollte einer der folgenden sein: **Notstarted**, **FinishedWithWarning**, **mit**, **fertig gestellt**, **fehlgeschlagen**, oder **PendingReboot**.  
  
 Der Server wird während der Erstkonfiguration neu gestartet werden. Wenn Sie diesen automatischen Neustart verhindern müssen, können Sie den folgenden Befehl, um einen Registrierungsschlüssel hinzufügen, bevor Sie mit der Erstkonfiguration beginnen:  
  
```  
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false  
  
```  
  
 Nach der Erstkonfiguration beginnen, können Sie **Get-WssConfigurationStatus** zum Status der Erstkonfiguration zu überprüfen und der Status **PendingReboot**, können Sie den Server neu starten.  
  
##  <a name="BKMK_Migrate"></a>Migrieren von Daten von Windows Small Business Server zu Windows Server Essentials Experience  
 Sie können Daten von Servern mit Windows Small Business Server2011, Windows Small Business Server2008, Windows Small Business Server2003 oder Windows Server Essentials mit dem Server mit Windows Server Essentials migrieren. Überprüfen der [Migrieren zu Windows Server Essentials](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md) Migration Handbuch für lokalen 2migrations und erforderlichen Anpassungen entsprechend Ihrer Hostingumgebung vorzunehmen.  
  
> [!NOTE]
>  Es wird empfohlen, dass Sie den Quellserver und dem Zielserver im gleichen Subnetz platzieren. Wenn dies nicht möglich ist, sollten Sie Folgendes sicherstellen:  
>   
>  -   Der Quellserver und Zielserver Zugriff gegenseitig auf "¢ s interne DNS-Namen.  
> -   Alle erforderlichen Ports sind geöffnet.  
  
 Nach der Migration können Sie Ihre Lizenzen zum Sperren und Beschränkungen entfernen aktualisieren. Weitere Informationen finden Sie unter [Übergang von Windows Server Essentials zu Windows Server2012 Standard](https://technet.microsoft.com/library/jj247582.aspx).  
  
##  <a name="BKMK_PowerShell"></a>Führen Sie allgemeiner Aufgaben mithilfe von Windows PowerShell aus  
 Dieser Abschnittenthält einige gängige Aufgaben, die Sie mithilfe von Windows PowerShell ausführen können.  
  
### <a name="enable-remote-web-access"></a>Aktivieren des Remotewebzugriffs  
 **Syntax**:  
  
 Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
  
 **Beispiel für**:  
  
 $Enable-WssRemoteWebAccess œDenyAccessByDefault œApplyToExistingUsers  
  
 Mit diesem Befehl wird Remotewebzugriff aktiviert, mit dem Router automatisch konfiguriert, und die Standardzugriffsberechtigungen für alle vorhandenen Benutzer ändern.  
  
### <a name="add-user"></a>Fügen Sie Benutzer hinzu  
 **Syntax**:  
  
 Add-WssUser [-Name] < String\ > [-Kennwort] < Securestring\ > [-AccessLevel < String\ > {Benutzer & 124; Administrator}] [-FirstName < String\ >] [-LastName < String\ >] [-AllowRemoteAccess] [-AllowVpnAccess] [< CommonParameters\ >]  
  
 **Beispiel für**:  
  
 $password = ConvertTo-SecureString "Passw0rd!" Asplaintext - œforce$ Add-WssUser-Namen User2Test-Kennwort $password - Accesslevel Administrator - FirstName "user2" - LastName testen  
  
 Mit diesem Befehl wird einen Administrator namens User2Test mit Kennwort Passw0rd hinzugefügt.  
  
### <a name="add-server-folder"></a>Serverordner hinzufügen  
 **Syntax**:  
  
 Add-WssFolder [-Name] < String\ > [-Path] < String\ > [[-Description] < String\ >] [-KeepPermissions] [< CommonParameters\ >]  
  
 **Beispiel für**:  
  
 Hinzufügen von $-WssFolder-namens "MyTestFolder"-Pfad "C:\ServerFolders\MyTestFolder"  
  
 Mit diesem Befehl wird der Serverordner namens MyTestFolder am angegebenen Speicherort hinzufügen.  
  
##  <a name="BKMK_EmailIntegration"></a>E-Mail-Integration in Windows Server Essentials  
 Sie können Windows Server Essentials Experience in Office365 integrieren oder gehosteten Exchange-Server. Wenn Sie Ihren Kunden Ihre gehostete E-Mail verwenden möchten, müssen Sie ein Add-In zur Integration von Windows Server Essentials Experience mit Ihrer gehosteten E-Mail-Lösung zu entwickeln. Weitere Informationen finden Sie unter [SDK für Windows Server Essentials](https://msdn.microsoft.com/library/gg513877.aspx).  
  
##  <a name="BKMK_Monitoring"></a>Überwachen Sie und verwalten Sie, indem Sie mit systemeigenen Tools  
 Dieser Abschnittbeschreibt die systemeigenen Tools, die in Windows Server2012 R2 zum Überwachen und Verwalten des Servers verfügbar sind.  
  
### <a name="group-policy"></a>Gruppenrichtlinie  
  Windows Server Essentials Experience nutzt die systemeigene gruppenrichtlinienunterstützung in Windows Server2012 R2 und stellt eine Benutzeroberfläche zum Konfigurieren der Ordnerumleitung und Sicherheit bereit.  
  
> [!NOTE]
>  In einer gehosteten Umgebung Wenn die Ordnerumleitung für ein Benutzerprofil aktiviert ist, kann länger dauern für Endbenutzer anmelden, wenn die Datengröße erheblich ist.  
  
### <a name="system-center-monitoring-pack"></a>System Center-Überwachungspaket  
 System Center Monitoring Pack für Windows Server Essentials Experience überwacht die Integrität der Warnung System helfen Ihnen beim Verwalten der großen Anzahl von Servern mit Windows Server Essentials, die kleinen Organisationen zugeordnet sind. Weitere Informationen finden Sie unter [System Center Management Pack für Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).  
  
### <a name="backup-and-restore"></a>Sicherung und Wiederherstellung  
  Windows Server2012 R2 mit Windows Server Essentials-Umgebung können Sie Server- und Clientcomputer im Netzwerk sichern.  
  
#### <a name="server-backup"></a>Server-Sicherung  
 Windows Server Essentials unterstützt zwei Methoden zum Sichern des Servers: lokale und externe Sicherung. Sie können diese Optionen anpassen, wenn Sie Ihre eigene Lösung zur serversicherung bereitstellen möchten.  
  
-   **Lokale Sicherung** können Sie inkrementelle Sicherungen auf Blockebene in regelmäßigen Abständen auf einem separaten Datenträger ausführen. Als Hostinganbieter könnten Sie anfügen eine virtuelle Festplatte mit dem virtuellen Computer mit Windows Server Essentials und konfigurieren Sie dann die serversicherung auf dieser virtuellen Festplatte. Die virtuelle Festplatte sollte auf einem anderen physischen Datenträger als der virtuelle Computer mit Windows Server Essentials befinden.  
  
    > [!NOTE]
    >  Wenn Sie andere sicherungslösungen für die virtuellen Computer und nicht, dass die Benutzer die Windows Server Essentials systemeigene serversicherungsfunktion angezeigt möchten, können Sie sie deaktivieren und die zugehörige Benutzeroberfläche im Dashboard entfernen. Weitere Informationen finden Sie in der [Anpassen der Serversicherung](https://technet.microsoft.com/library/dn293413.aspx) Abschnitt [anpassen und Bereitstellen von Windows Server Essentials in Windows Server2012 R2](https://technet.microsoft.com/library/dn293241.aspx).  
  
-   **Externe Sicherung** können Sie in regelmäßigen Abständen die Server-Daten in einem cloudbasierten Dienst sichern. Sie können herunterladen und installieren Microsoft Azure Backup-Integration-Modul für Windows Server Essentials um die Azure-Sicherung zu nutzen, die von Microsoft bereitgestellt wird.  
  
     Weitere Informationen finden Sie unter der Integration von Windows Azure Backup mit Windows Server Essentials-Abschnittim [Manage Server Backup](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md).  
  
     Wenn Sie oder Ihre Benutzer einen anderen Clouddienst bevorzugen, sollten Sie Folgendes beachten:  
  
    -   Aktualisieren Sie die Benutzeroberfläche des Dashboards, sodass Ihre bevorzugten Cloud-Dienst nicht auf den Standardwert Azure Backup verknüpft.  
  
    -   (Optional) Entwickeln Sie ein Add-In für das Dashboard konfigurieren und Verwalten der cloudbasierten Sicherungsdienst.  
  
#### <a name="client-computer-backup"></a>Client Computer Backup  
 Windows Server Essentials-Umgebung unterstützt zwei Arten von Daten Clientsicherung: vollständige Clientsicherung und Dateiversionsverlauf.  
  
> [!NOTE]
>  Sichern des Clients kann die Leistung beeinträchtigen, da die Daten über VPN vom Client an den Server übertragen werden müssen.  
  
##### <a name="full-client-backup"></a>Vollständige Clientsicherung  
 Vollständige Clientsicherung ist standardmäßig für die Client-Geräte, die mit dem Windows Server Essentials-Netzwerk verbunden sind. Vollständig der Systeminformationen und Daten für den Client gesichert, und die Datendeduplizierung unterstützt. Die Sicherungsdaten werden auf dem Server mit Windows Server Essentials gespeichert werden. Dies kann ein fehlerhafter Client Daten aus einem früheren Sicherungspunkt abrufen.  
  
 Beachten vollständigen clientcomputersicherung Folgendes:  
  
-   **Leistung** erste Clientsicherung kann aufgrund der Menge an hochzuladenden Daten zeitaufwändig sein.  
  
-   **Stabilität** manchmal ist die Internetverbindung nicht zuverlässig auf dem Client. Clientsicherung automatisch fortgesetzt werden soll und die clientsicherungsdatenbank erstellt einen Prüfpunkt, jedes Mal, wenn 40GB Daten gesichert werden. Sie können diesen Wert in einen kleineren Wert ändern, wenn Sie davon ausgehen, dass die Internetverbindung nicht zuverlässig ist.  
  
    -   So aktivieren Sie einen Prüfpunkt Auftrag: Legen Sie auf dem Server den Registrierungsschlüssel **HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs** auf 1 fest.  
  
    -   So ändern Sie den Prüfpunkt-Schwellenwert: Ändern Sie auf dem Client **HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold** vom Standardwert von 40GB.  
  
-   **Bare-Metal-Recovery des Clients**, da Windows Preinstall Environment eine VPN-Verbindung nicht unterstützt, bare-Metal-Recovery des Clients nicht unterstützt. Sie sollten die Aufgabe ausblenden, indem Sie die Schritteim [anpassen und Bereitstellen von Windows Server Essentials in Windows Server2012 R2](https://technet.microsoft.com/library/dn293241.aspx).  
  
##### <a name="file-history"></a>Dateiversionsverlauf  
 Dateiversionsverlauf ist ein Feature in Windows8.1 und Windows8 zum Sichern von Profildaten (Bibliotheken, Desktop, Kontakte, Favoriten) auf einer Netzwerkfreigabe. Sie können die Dateiversionsverlauf-Einstellung für alle Computer mit Windows8.1 oder Windows8, die mit Windows Server Essentials-Netzwerk verbunden sind, zentral verwalten. Die Sicherungsdaten werden auf dem Windows Server Essentials-Server gespeichert. Sie sollten die Aufgabe ausblenden, indem Sie die Schritteim [anpassen und Bereitstellen von Windows Server Essentials in Windows Server2012 R2](https://technet.microsoft.com/library/dn293241.aspx)  
  
### <a name="storage-management"></a>Speicherverwaltung  
 Mithilfe von Speicherplätzen können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren, Festplatten hinzufügen, dynamisch und Datenvolumes mit bestimmten ausfallsicherheitsstufen erstellen. Dies ist auf dem Host oder auf dem virtuellen Computer möglich. Wenn Sie diese Funktion auf einem virtuellen Computer mit Windows Server Essentials ausblenden möchten, befolgen Sie die Anweisungen in [anpassen und Bereitstellen von Windows Server Essentials in Windows Server2012 R2](https://technet.microsoft.com/library/dn293241.aspx).  
  
##  <a name="BKMK_Scenarios"></a>Testen von Szenarien  
 Aus Hostperspektive sollten Sie die folgenden Szenarien testen:  
  

-   [Server-Bereitstellung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)  
  
-   [Server-Konfiguration](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)  
  
-   [Servermanagement](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)  
  
-   [Client-Benutzeroberfläche](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)  

  
###  <a name="BKMK_ServerDeploy"></a>Server-Bereitstellung  
 Sie können die folgenden Bereitstellungsszenarien für den Server testen:  
  
-   Bereitstellen eines Servers mit Windows Server2012 R2 als Domänencontroller in Ihrer Testumgebung, und installieren Sie Windows Server Essentials Experience-Rolle.  
  
-   Bereitstellen eines Servers mit Windows Server2012 R2 in Ihrer Testumgebung, Verbinden des Servers zu einer vorhandenen Domäne und installieren Sie Windows Server Essentials Experience-Rolle.  
  
-   Passen Sie das Windows Server Essentials-Image nach Bedarf an.  
  
-   Automatisieren der Windows Server Essentials-Bereitstellung mit einer unbeaufsichtigten Datei und Windows PowerShell.  
  
-   Migrieren von Servern mit lokalem Windows Small Business Server auf gehostete Server mit Windows Server Essentials ausgeführt.  
  
###  <a name="BKMK_ServerConfig2"></a>Server-Konfiguration  
 Sie können die folgenden Server-Konfigurationsszenarien testen:  
  
-   Konfigurieren von Zugriff überall (VPN, Remotewebzugriff und DirectAccess).  
  
-   Konfigurieren von Speicher und Serverordnern.  
  
-   Aktivieren von BranchCache.  
  
-   (Falls zutreffend) Konfigurieren der Serversicherung, Onlinesicherung, Clientsicherung und Dateiversionsverlauf.  
  
-   (Falls zutreffend) Konfigurieren und Verwalten von Speicherplätzen.  
  
-   (Falls zutreffend) Konfigurieren Sie die Integration der E-Mail-Lösung (Office365 und gehosteter Exchange-Server).  
  
-   (Falls zutreffend) Konfigurieren Sie Integration mit anderen Microsoft online Services.  
  
-   (Falls zutreffend) Konfigurieren des Medienservers.  
  
###  <a name="BKMK_ServerManage"></a>Servermanagement  
 Sie können die folgenden Server-Management-Szenarien testen:  
  
-   Verwalten von Benutzern und Gruppen.  
  
-   Konfigurieren und Empfangen von e-Mail-Benachrichtigungen für Warnungen.  
  
-   Ausführen von Best Practices Analyzer, um festzustellen, ob ein Fehler oder eine Warnung angezeigt.  
  
-   Konfigurieren des System Center Operations Manager-Pakets.  
  
-   Konfigurieren der serverwiederherstellung im Falle einer Beschädigung des Betriebssystems.  
  
###  <a name="BKMK_ClientXP"></a>Client-Benutzeroberfläche  
 Sie können die folgenden Endbenutzerszenarien testen:  
  
-   Bereitstellen von Clients über das Internet (PC oder Mac-Betriebssysteme).  
  
-   Verwenden Sie Launchpad zum Zugriff auf freigegebene Ordner auf dem Client.  
  
-   Zugreifen auf des Serverressourcen über Remotewebzugriff von verschiedenen Geräten (PC, Smartphone und Tablet).  
  
-   Zugriff auf die My Server-App für Windows Phone.  
  
-   (Falls zutreffend) Zugreifen auf den Dateiversionsverlauf, Clientsicherung und Wiederherstellung und Ordnerumleitung.  
  
-   (Falls zutreffend) Überprüfen Sie die E-Mail-integrationsumgebung.  
  
##  <a name="BKMK_Support"></a>Informationen zum Support  
 Sie können die Windows Server Essentials-Software Development Kit (SDK) und die Windows Server Essentials Assessment und Deployment Kit (ADK) herunterladen:  
  
-   [Windows Server Essentials-Software Development Kit](https://msdn.microsoft.com/library/gg513877.aspx)SDK  
  
-   [Anpassen und Bereitstellen von Windows Server Essentials in Windows Server2012 R2](https://technet.microsoft.com/library/dn293241.aspx)  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Was ist neu in Windows Server Essentials](../get-started/what-s-new.md)  

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)  

-   [Erste Schrittemit Windows Server Essentials](../get-started/get-started.md)
