---
title: Bereitstellen von Windows Server Essentials Experience als einen gehosteten Server
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: a455c6b4-b29f-4f76-8c6b-1578b6537717
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5222298c4b8a3fd98c40474233fc7208607a3df7
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470995"
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Bereitstellen von Windows Server Essentials Experience als einen gehosteten Server

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Dokument enthält spezifische Informationen für Hostinganbieter, die Microsoft Windows Server 16 mit der Rolle "Windows Server Essentials-Umgebung" (im weiteren Verlauf des Dokuments als Windows Server Essentials bezeichnet) bereitstellen möchten, und beabsichtigen, ihren Kunden Windows Server Essentials-Umgebung als Dienst anzubieten. Dieses Dokument enthält die folgenden Abschnitte:


-   [Übersicht über die Windows Server Essentials-Umgebung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)

-   [Vorteile des Hostens der Windows Server Essentials-Umgebung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)

-   [Unterstützte Bereitstellungsoptionen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)

-   [Unterstützte Netzwerktopologien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)

-   [Anpassen des Images der Windows Server Essentials-Umgebung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)

-   [Automatisieren der Bereitstellung der Windows Server Essentials-Umgebung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)

-   [Migrieren von Daten vom lokalen Windows Small Business Server (SBS) zur gehosteten Windows Server Essentials-Umgebung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)

-   [Durchführen allgemeiner Aufgaben mithilfe von Windows PowerShell](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)

-   [E-Mail-Integration in Windows Server Essentials](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)

-   [Überwachen und Verwalten mithilfe von systemeigenen Tools](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)

-   [Testszenarios](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)

-   [Supportinformationen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)


##  <a name="windows-server-essentials-experience-overview"></a><a name="BKMK_WSEEOverview"></a>Übersicht über die Windows Server Essentials-Funktionen
 Bei Windows Server Essentials handelt es sich um eine Server Rolle, die in Windows Server 2012 R2 Standard und Windows Server 2012 R2 Datacenter verfügbar ist. Wenn die Rolle "Windows Server Essentials-Benutzer" auf einem Server mit Windows Server 2012 R2 installiert ist, kann der Kunde alle Features, die in Windows Server Essentials verfügbar sind, ohne Sperren und Beschränkungen nutzen. Die Windows Server Essentials-Umgebung ermöglicht die folgenden standortübergreifenden Lösungen für kleine und mittelständische Unternehmen:

-   **Datenspeicherung und-Schutz** Sie können die Daten des Kunden an einem zentralen Ort speichern und Server-und Client Daten schützen, indem Sie die Server-und Client Computer (weniger als 75) im Netzwerk sichern.

-   **Benutzerverwaltung** Sie können die Benutzer und Gruppen über das vereinfachte Server-Dashboard verwalten. Darüber hinaus ermöglicht die Integration mit Microsoft Azure Active Directory (Azure AD) den einfachen Datenzugriff für Microsoft Onlinedienste (z. b. Office 365, Exchange Online und SharePoint Online) für Benutzer mithilfe Ihrer Anmelde Informationen für die Domäne.

-   **Dienst Integration** Sie können den Server in Microsoft Onlinedienste (z. b. Office 365, SharePoint Online und Microsoft Azure Backup) integrieren. Sie können den Server auch in Ihre Dienste oder in Dienste von Drittanbietern integrieren.

-   **Zugriff überall** Kunden können von nahezu überall aus und mit fast jedem Gerät auf Server, Netzwerkcomputer und Daten zugreifen, sofern sie eine Internetverbindung haben. Mit dem Remotewebzugriff können sie über eine optimierte Browserumgebung, die die Fingereingabe unterstützt, auf Anwendungen und Daten zugreifen. Die My Server-App ermöglicht Ihnen den Zugriff auf Daten aus einem Windows Phone oder einer Microsoft Store-App.

-   **Medien Streaming** Wenn Sie das Medienpaket auf einem Server installieren, auf dem Windows Server Essentials-Benutzerfreundlichkeit aktiviert ist, können Kunden Musik, Videos und Fotos in freigegebenen Ordnern speichern und dann von Netzwerkcomputern oder Remote Webzugriff aus auf diese Mediendateien zugreifen.

-   **Statusüberwachung** Sie können die Integrität des Netzwerks überwachen und benutzerspezifische Statusberichte abrufen.

##  <a name="benefits-of-hosting-windows-server-essentials-experience"></a><a name="BKMK_Benefits"></a>Vorteile des Hostens der Windows Server Essentials-Umgebung
  Windows Server Essentials ist eine Rolle in Windows Server, sodass Sie das vorhandene Bereitstellungs-und Verwaltungs Framework in Windows Server zum Bereitstellen und Konfigurieren der Rolle "Windows Server Essentials-Funktionen" wieder verwenden können. Das Hosting der Rolle "Windows Server Essentials-Umgebung" bietet die folgenden Vorteile:

-   **Optimierte Bereitstellung** Durch einfaches Aktivieren der Rolle "Windows Server Essentials-Benutzer" sind einige der am häufigsten verwendeten Rollen und Features aktiviert und mit bewährten Methoden für kleine und mittelständische Unternehmen konfiguriert. Sie können die Windows Server Essentials-Funktionen anpassen oder einige der lokalen Funktionen ausblenden. Wenn Sie die Windows Azure Pack verwenden, können Sie die Katalog Vorlage für Windows Server Essentials-Funktionen unter Windows Server 2012 R2 herunterladen.

-   **Vereinfachtes Dashboard** Das Windows Server Essentials-Dashboard vereinfacht allgemeine Aufgaben wie das Verwalten von Serverordnern, Serverspeichern, Sicherung und Wiederherstellung, Benutzer- oder Gruppenkonten, Geräten, Remotezugriff und E-Mail. Kleine und mittelständische Unternehmen können täglich wiederkehrende Verwaltungsaufgaben ausführen, anstatt den Helpdesk um technischen Support bitten zu müssen.

-   **Erweiterbarkeit** Das Windows Server Essentials-Dashboard und Windows Server Essentials Connector-Software sind erweiterbar. Sie können ihr eigenes Branding und eine Dienstintegration hinzufügen, damit Ihre Kunden einen zentralen Einstiegspunkt für alle Belange in Bezug auf ihre Server und Dienste haben.

-   **Monitor** Es steht eine neue Version des System Center-Überwachungspakets zur Verfügung, um mehrere Server mit Windows Server Essentials zu überwachen und zu verwalten. Informationen zum Herunterladen der Management Pack finden Sie unter [System Center Management Pack für Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).

##  <a name="supported-deployment-options"></a><a name="BKMK_SupportedDeployment"></a>Unterstützte Bereitstellungs Optionen
  Windows Server Essentials kann in einer neuen Active Directory Umgebung als Domänen Controller bereitgestellt werden. oder kann in einer vorhandenen Active Directory Umgebung als Domänen Mitglied bereitgestellt werden.

 Es wird empfohlen, zuerst Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter bereitzustellen und dann die Rolle "Windows Server Essentials-Rolle" zu installieren. Mit dieser Bereitstellungs Methode erhalten Sie alle Funktionen der Windows Server Essentials-Edition ohne die Sperren und Beschränkungen.


 Weitere Informationen zum Installieren von Windows Server 2012 R2 mit der Rolle "Windows Server Essentials-Rolle" finden Sie unter [Installieren und Konfigurieren von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).



##  <a name="supported-network-topologies"></a><a name="BKMK_SupportedToplogy"></a>Unterstützte Netzwerktopologien
 Um Windows Server Essentials-Funktionen von einem Roamingclient aus verwenden zu können, muss VPN aktiviert werden. Um den Remotezugriff auf den Server von einem Roamingclient aus zu aktivieren, müssen Sie auf dem Server Port 443 und Port 80 öffnen.

 Nachfolgend sind zwei typische serverseitige Netzwerktopologien und die Konfiguration des VPN und Remotewebzugriffs beschrieben:

- **Topologie 1** (Dies ist die bevorzugte Topologie, bei der sich alle Server und der VPN IP-Adressbereich im gleichen Subnetz befinden.):

  -   Richten Sie den Server in einem separaten virtuellen Netzwerk unter einem NAT-Gerät (Network Address Translation) ein.

  -   Aktivieren Sie den DHCP-Dienst im virtuellen Netzwerk, oder weisen Sie eine statische IP-Adresse für den Server zu.

  -   Leiten Sie den öffentlichen IP-Port 443 auf dem Router an die LAN-Adresse des Servers weiter.

  -   Lassen Sie das VPN-Passthrough für Port 443 zu.

  -   Legen Sie den VPN-IPv4-Adresspool in demselben Subnetzbereich wie die Serveradresse fest.

  -   Weisen Sie sekundären Servern eine statische IP-Adresse in demselben Subnetz zu, aber außerhalb des VPN-Adresspools.

- **Topologie 2**:

  -   Weisen Sie dem Server eine private IP-Adresse zu.

  -   Ermöglichen Sie es dem Port 443 auf dem Server, eine öffentliche Port-443-IP-Adresse zu erreichen.

  -   Lassen Sie das VPN-Passthrough für Port 443 zu.

  -   Weisen Sie dem VPN-IPv4-Adresspool und der Serveradresse verschiedene Bereiche zu.

  Bei Topologie 2 werden Szenarien für sekundäre Server nicht unterstützt, da Sie der gleichen Domäne keinen weiteren Server hinzufügen können.

  Sie können das VPN während einer unbeaufsichtigten Bereitstellung mit dem Windows PowerShell-Skript aktivieren oder mit dem Assistenten nach der Erstkonfiguration konfigurieren.

  Wenn Sie das VPN mithilfe von Windows PowerShell aktivieren, führen Sie den folgenden Befehl mit Administratorberechtigungen auf dem Server mit Windows Server Essentials aus und geben Sie alle erforderlichen Informationen an.

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
>  Wenn Sie keine VPN-Verbindung bereitstellen können, bevor der Kunde den Server übernimmt, stellen Sie sicher, dass der Serverport 3389 über das Internet erreichbar ist, sodass der Kunde das Remotedesktopprotokoll verwenden kann, um eine Verbindung mit dem Server herzustellen und um es zu konfigurieren.

##  <a name="customize-the-image-of-windows-server-essentials-experience-role"></a><a name="BKMK_CustomizeImage"></a>Anpassen des Images der Rolle "Windows Server Essentials-Rolle"
 Sie können das Image vor dem Konfigurieren der Rolle "Windows Server Essentials-Umgebung" anpassen. Weitere Informationen zum standardmäßigen Windows Server Sysprep-Prozess finden Sie im [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx). Nachdem Sie das Image mithilfe von Sysprep vorbereitet haben, können Sie es verwenden oder es für eine neue Bereitstellung erneut in "Install.wim" versiegeln.

 Wenn Sie Virtual Machine Manager verwenden, können Sie eine Vorlage mithilfe der ausgeführten Instanz erstellen. Bei diesem Vorgang wird die Instanz mithilfe von Sysprep vorbereitet und der Computer heruntergefahren. Nachdem Sie die Vorlage in Ihrer Bibliothek gespeichert haben, können Sie sie je nach spezifischen Anforderungen verwenden.

 Nachdem Sie die Rolle "Windows Server Essentials-Benutzer" installiert haben, können Sie die Features in Windows Server Essentials anpassen. Eine der wichtigsten Anpassungen ist der Registrierungsschlüssel **IsHosted** : **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\Deployment\IsHosted**.

 Wenn dieser Schlüssel auf 0x1 festgelegt ist, ändern einige der lokalen Funktionen ihr Verhalten. Unter anderem ändern sich die folgenden Funktionen:

- **Clientsicherung** Die Clientsicherung ist jetzt für neu verbundene Clientcomputer standardmäßig deaktiviert.

- **Clientwiederherstellungsdienst** Der Clientwiederherstellungsdienst wird deaktiviert, und die Benutzeroberfläche wird nicht mehr im Dashboard angezeigt.

- **Dateiversionsverlauf** Die Dateiversionsverlaufseinstellungen für neu erstellte Benutzerkonten werden nicht automatisch vom Server verwaltet.

- **Serversicherung** Der Serversicherungsdienst wird deaktiviert, und die Serversicherungsbenutzeroberfläche wird nicht mehr im Dashboard angezeigt.

- **Speicherplätze** Die Benutzeroberfläche für das Erstellen oder Verwalten von Speicherplätzen wird nicht mehr im Dashboard angezeigt.

- **Zugriff überall** Die Router- und VPN-Konfiguration wird standardmäßig übersprungen, wenn Sie den Assistenten zum Einrichten von "Zugriff überall" ausführen.

  Wenn Sie das Verhalten der einzelnen aufgeführten Funktionen steuern möchten, können Sie den entsprechenden Registrierungsschlüssel für jede festlegen. Informationen dazu, wie Sie den Registrierungsschlüssel festlegen, finden Sie unter [Anpassen und Bereitstellen von Windows Server Essentials unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx).

##  <a name="automate-the-deployment-of-windows-server-essentials-experience"></a><a name="BKMK_AutomateDeployment"></a>Automatisieren der Bereitstellung von Windows Server Essentials
 Zum Automatisieren der Bereitstellung müssen Sie zuerst das Betriebssystem bereitstellen und dann die Rolle "Windows Server Essentials-Benutzer" installieren.

-   Befolgen Sie die Anweisungen im [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx), um Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter automatisch bereitzustellen.

-   Informationen zum Installieren der Rolle "Windows Server Essentials-Benutzer" mithilfe von Windows PowerShell finden Sie unter [Installieren und Konfigurieren von Windows Server Essentials](https://technet.microsoft.com/library/dn281793.aspx).

> [!NOTE]
>  Stellen Sie sicher, dass die Zeitzoneneinstellungen des virtuellen Host Computers und der Windows Server Essentials-Umgebung identisch sind. Andernfalls können verschiedene Fehler auftreten. Hierzu gehören: die Erstkonfiguration des Servers ist möglicherweise bei Zertifikat bezogenen Tasks nicht erfolgreich, das Zertifikat funktioniert möglicherweise einige Stunden nach der Installation der Windows Server Essentials-Rolle, und die Geräteinformationen werden nicht ordnungsgemäß aktualisiert.

 Nach der Bereitstellung verwenden Sie das Windows PowerShell-Cmdlet **Get-WssConfigurationStatus**, um zu überprüfen, ob die Erstkonfiguration erfolgreich war. Der zurückgegebene Status sollte einer der folgenden sein: **Notstarted**, **FinishedWithWarning**, **Running**, **Finished**, **Failed**oder **PendingReboot**.

 Der Server wird während der Erstkonfiguration neu gestartet. Wenn Sie diesen automatischen Neustart verhindern müssen, können Sie den folgenden Befehl verwenden, um einen Registrierungsschlüssel hinzuzufügen, bevor Sie mit der Erstkonfiguration beginnen:

```
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false

```

 Sobald Sie mit der Erstkonfiguration beginnen, können Sie **Get-WssConfigurationStatus** verwenden, um den Status der Erstkonfiguration zu überprüfen. Wenn der Status **PendingReboot** ist, können Sie den Server neu starten.

##  <a name="migrate-data-from-windows-small-business-server-to-windows-server-essentials-experience"></a><a name="BKMK_Migrate"></a>Migrieren von Daten von Windows Small Business Server zu Windows Server Essentials
 Sie können Daten von Servern mit Windows Small Business Server 2011, Windows Small Business Server 2008, Windows Small Business Server 2003 oder Windows Server Essentials zu dem Server migrieren, auf dem Windows Server Essentials ausgeführt wird. Lesen Sie das Migrations Handbuch [Migrieren zu Windows Server Essentials](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md) für lokale 2migrationen, und nehmen Sie erforderliche Anpassungen basierend auf Ihrer Hostingumgebung vor.

> [!NOTE]
>  Platzieren Sie den Quellserver und den Zielserver am besten im gleichen Subnetz. Falls dies nicht möglich ist, stellen Sie Folgendes sicher:
>
> - Der Quell Server und der Zielserver können auf die internen DNS-Namen des internen Servers zugreifen.
>   -   Alle erforderlichen Ports sind geöffnet.

 Nach der Migration können Sie Ihre Lizenzen aktualisieren, um die Sperren und Beschränkungen zu entfernen. Weitere Informationen finden Sie unter [Umstellung von Windows Server Essentials auf Windows Server 2012 Standard](https://technet.microsoft.com/library/jj247582.aspx).

##  <a name="perform-common-tasks-by-using-windows-powershell"></a><a name="BKMK_PowerShell"></a>Ausführen allgemeiner Aufgaben mithilfe von Windows PowerShell
 In diesem Abschnitt werden einige allgemeinen Aufgaben erläutert, die Sie mithilfe von Windows PowerShell ausführen können.

### <a name="enable-remote-web-access"></a>Aktivieren von Remotewebzugriff
 **Syntax**:

 Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]

 **Beispiel:**

 $Enable-wssremotewebaccess "œdenyaccessbydefault" "œapplytexistingusers"

 Mit diesem Befehl wird Remotewebzugriff aktiviert, wobei der Router automatisch konfiguriert wird. Zudem werden die Standardzugriffsberechtigungen für alle vorhandenen Benutzer geändert.

### <a name="add-user"></a>Benutzer hinzufügen
 **Syntax**:

 Add-wssuser [-Name] <String \> [-password] <SecureString \> [-AccessLevel <String \> {User &#124; Administrator}] [-FirstName <String \> ] [-LastName <String \> ] [-allowremoteaccess] [-allowvpnaccess] [<CommonParameters \> ]

 **Beispiel:**

 $Password = ConvertTo-SecureString "Passw0rd!" -asplaintext œforce $ Add-wssuser-Name User2Test-Password $Password-Access Level Administrator-FirstName User2-LastName Test

 Mit diesem Befehl wird ein Administrator namens User2Test with Password Passw0rd! hinzugefügt.

### <a name="add-server-folder"></a>Hinzufügen eines Serverordners
 **Syntax**:

 Add-wssfolder [-Name] <Zeichenfolge \> [-path] <Zeichenfolge \> [[-Description] <String \> ] [-keepberechtigungen] [<CommonParameters \> ]

 **Beispiel:**

 $Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"

 Mit diesem Befehl wird ein Server Ordner mit dem Namen "mytestfolder" am angegebenen Speicherort hinzugefügt.

##  <a name="email-integration-with-windows-server-essentials"></a><a name="BKMK_EmailIntegration"></a>E-Mail-Integration in Windows Server Essentials
 Sie können Windows Server Essentials-Funktionen mit Office 365 oder gehostetem Exchange Server integrieren. Damit Ihre Kunden auch Ihren gehosteten E-Mail-Dienst verwenden können, müssen Sie ein Add-In entwickeln, um die Windows Server Essentials-Umgebung in Ihre gehostete E-Mail-Lösung zu integrieren. Weitere Informationen finden Sie im [Windows Server Essentials SDK](https://msdn.microsoft.com/library/gg513877.aspx).

##  <a name="monitor-and-manage-by-using-native-tools"></a><a name="BKMK_Monitoring"></a>Überwachen und verwalten mithilfe von systemeigenen Tools
 In diesem Abschnitt werden die systemeigenen Tools erläutert, die in Windows Server 2012 R2 zum Überwachen und Verwalten des-Servers zur Verfügung stehen.

### <a name="group-policy"></a>Gruppenrichtlinie
  Windows Server Essentials-Umgebung nutzt die systemeigene Gruppenrichtlinie-Unterstützung in Windows Server 2012 R2 und bietet eine Benutzeroberfläche zum Konfigurieren der Ordner Umleitung und der Sicherheitseinstellungen.

> [!NOTE]
>  In einer gehosteten Umgebung kann bei aktivierter Ordnerumleitung für ein Benutzerprofil das Anmelden von Endbenutzern länger dauern, wenn die Datengröße erheblich ist.

### <a name="system-center-monitoring-pack"></a>System Center-Überwachungspaket
 Das System Center-Überwachungspaket für Windows Server Essentials verfügt über das Integritäts Warnungs System, das Sie bei der Verwaltung einer großen Anzahl von Servern unter Windows Server Essentials unterstützt, die für kleine Unternehmen vorgesehen sind. Weitere Informationen finden Sie unter [System Center Management Pack für Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).

### <a name="backup-and-restore"></a>Sichern und Wiederherstellen
  Windows Server 2012 R2 mit Windows Server Essentials bietet Ihnen die Möglichkeit, Server-und Client Computer im Netzwerk zu sichern.

#### <a name="server-backup"></a>Serversicherung
 Windows Server Essentials unterstützt zwei Formen der Serversicherung: die lokale Sicherung und die externe Sicherung. Sie können diese Optionen anpassen, wenn Sie Ihre eigene Lösung zur Serversicherung bereitstellen möchten.

-   **Lokale Sicherung** Mithilfe der lokalen Sicherung können Sie regelmäßig eine inkrementelle Sicherung auf Blockebene auf einem separaten Datenträger ausführen. Als Hostinganbieter könnten Sie eine virtuelle Festplatte mit dem virtuellen Computer mit Windows Server Essentials verbinden und dann die Serversicherung auf dieser virtuellen Festplatte konfigurieren. Die virtuelle Festplatte sollte sich auf einem anderen physischen Datenträger als der virtuelle Computer mit Windows Server Essentials befinden.

    > [!NOTE]
    >  Wenn Sie andere Sicherungslösungen für die virtuellen Computer verwenden und Sie verhindern möchten, dass die Benutzer die systemeigene Serversicherungsfunktion von Windows Server Essentials sehen, können Sie sie deaktivieren und die zugehörige Benutzeroberfläche im Dashboard entfernen. Weitere Informationen finden Sie im Abschnitt [Anpassen der Serversicherung](https://technet.microsoft.com/library/dn293413.aspx) unter [Anpassen und Bereitstellen von Windows Server Essentials unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx).

-   **Externe Sicherung** Mithilfe dieser Sicherung können Sie die Serverdaten in regelmäßigen Abständen in einem Cloud-basierten Dienst sichern. Sie können das Microsoft Azure Backup-Integrationsmodul für Windows Server Essentials herunterladen und installieren, um den von Microsoft bereitgestellten Azure Backup zu nutzen.

     Weitere Informationen finden Sie im Abschnitt Integrieren von Windows Azure Backup in Windows Server Essentials in [Verwalten der Server Sicherung](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md).

     Beachten Sie Folgendes, wenn Sie oder Ihre Benutzer einen anderen Cloud-Dienst bevorzugen:

    -   Aktualisieren Sie die Benutzeroberfläche des Dashboards, sodass Sie mit Ihrem bevorzugten clouddienst und nicht mit dem Standard Azure Backup verknüpft ist.

    -   (Optional) Entwickeln Sie ein Add-In für das Dashboard, um den Cloud-basierten Sicherungsdienst zu konfigurieren und zu verwalten.

#### <a name="client-computer-backup"></a>Clientcomputersicherung
 Die Windows Server Essentials-Umgebung unterstützt zwei Formen der Clientdatensicherung: die vollständige Clientsicherung und den Dateiversionsverlauf.

> [!NOTE]
>  Die Clientsicherung kann sich auf die Leistung auswirken, da die Daten über VPN vom Client an den Server übertragen werden müssen.

##### <a name="full-client-backup"></a>Vollständige Clientsicherung
 Die vollständige Clientsicherung ist standardmäßig für alle Clientgeräte aktiviert, die mit dem Windows Server Essentials-Netzwerk verbunden sind. Dabei werden alle Systeminformationen und Daten für den Client gesichert. Sie unterstützt zudem die Datendeduplizierung. Die Sicherungsdaten werden auf dem Server gespeichert, auf dem Windows Server Essentials ausgeführt wird. Dadurch kann ein fehlerhafter Client Daten von einem früheren Sicherungspunkt abrufen.

 Beachten Sie vor einer vollständigen Clientcomputersicherung Folgendes:

-   **Leistung** Die erste Clientsicherung kann aufgrund der Menge an hochzuladenden Daten zeitaufwendig sein.

-   **Stabilität** Es kann vorkommen, dass die Internetverbindung auf Clientseite nicht stabil ist. Die Client Sicherung ist so konzipiert, dass Sie automatisch fortgesetzt wird, und die Client Sicherungs Datenbank erstellt immer dann einen Prüfpunkt, wenn 40 GB Daten gesichert werden. Sie können diesen Wert in einen kleineren Wert ändern, wenn die Internetverbindung nicht zuverlässig ist.

    -   So aktivieren Sie einen Prüfpunkt Auftrag Setzen Sie auf dem Server den Registrierungsschlüssel **HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs** auf 1.

    -   So ändern Sie den Prüfpunkt-Schwellenwert Ändern Sie auf dem Client **HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold** vom Standardwert in 40 GB.

-   **Bare-Metal-Recovery des Clients** Da die Windows-Vorinstallationsumgebung keine VPN-Verbindungen unterstützt, wird die Bare-Metal-Recovery des Clients nicht unterstützt. Sie sollten die Aufgabe des Clientwiederherstellungsdiensts ausblenden, indem Sie die Schritte unter [Anpassen und Bereitstellen von Windows Server Essentials in Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx)ausführen.

##### <a name="file-history"></a>Dateiversionsverlauf
 Der Dateiversionsverlauf ist eine Windows 8.1- und Windows 8-Funktion zum Sichern von Profildaten (Bibliotheken, Desktop, Kontakte, Favoriten) auf einer Netzwerkfreigabe. Sie können die Dateiversionsverlauf-Einstellung für alle Computer mit Windows 8.1 oder Windows 8 zentral verwalten, die mit einem Windows Server Essentials-Netzwerk verbunden sind. Die Sicherungsdaten werden auf dem Server gespeichert, auf dem Windows Server Essentials ausgeführt wird. Sie sollten den Task "Client Wiederherstellungs Dienst" ausblenden, indem Sie die Schritte unter Anpassen und Bereitstellen von [Windows Server Essentials in Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx) ausführen.

### <a name="storage-management"></a>Speicherverwaltung
 Mithilfe von Speicherplätzen können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren, Festplatten dynamisch hinzufügen und Datenvolumes mit bestimmten Ausfallsicherheitsstufen erstellen. Dies ist auf dem Host oder auf dem virtuellen Computer möglich. Wenn Sie diese Funktion auf einem virtuellen Computer mit Windows Server Essentials ausblenden möchten, folgen Sie den Anweisungen unter [Anpassen und Bereitstellen von Windows Server Essentials in Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx).

##  <a name="test-scenarios"></a><a name="BKMK_Scenarios"></a>Test Szenarien
 Aus Hostperspektive sollten Sie am besten folgende Szenarien testen:


-   [Serverbereitstellung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)

-   [Server Konfiguration](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)

-   [Server Verwaltung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)

-   [Clienterfahrung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)


###  <a name="server-deployment"></a><a name="BKMK_ServerDeploy"></a>Server Bereitstellung
 Sie können die folgenden Bereitstellungsszenarien für den Server testen:

-   Stellen Sie einen Server unter Windows Server 2012 R2 als Domänen Controller in der Lab-Umgebung bereit, und installieren Sie dann die Rolle "Windows Server Essentials-Umgebung".

-   Stellen Sie einen Server unter Windows Server 2012 R2 in der Lab-Umgebung bereit, verknüpfen Sie diesen Server mit einer vorhandenen Domäne, und installieren Sie dann die Rolle "Windows Server Essentials-Umgebung".

-   Anpassen des Windows Server Essentials-Images nach Bedarf.

-   Automatisieren der Windows Server Essentials-Bereitstellung mit einer unbeaufsichtigten Datei und Windows PowerShell.

-   Migrieren von lokalen Servern mit Windows Small Business Server auf gehostete Server mit Windows Server Essentials.

###  <a name="server-configuration"></a><a name="BKMK_ServerConfig2"></a>Server Konfiguration
 Sie können die folgenden Konfigurationsszenarien für den Server testen:

-   Konfigurieren von "Zugriff überall" (VPN, Remotewebzugriff und DirectAccess).

-   Konfigurieren von Speicher und Serverordnern.

-   Aktivieren von BranchCache.

-   (Falls zutreffend) Konfigurieren der Serversicherung, Onlinesicherung, Clientsicherung und des Dateiversionsverlaufs.

-   (Falls zutreffend) Konfigurieren und Verwalten von Speicherplätzen

-   (Falls zutreffend) Konfigurieren der Integration der E-Mail-Lösung (Office 365 und gehosteter Exchange-Server).

-   (Falls zutreffend) Konfigurieren der Integration in andere Microsoft Online Services.

-   (Falls zutreffend) Konfigurieren des Medienservers

###  <a name="server-management"></a><a name="BKMK_ServerManage"></a>Server Verwaltung
 Sie können die folgenden Verwaltungsszenarien für den Server testen:

-   Verwalten von Benutzern und Gruppen.

-   Konfigurieren und Empfangen von E-Mail-Benachrichtigungen für Warnungen

-   Ausführen von Best Practices Analyzer, um festzustellen, ob ein Fehler oder eine Warnmeldung vorliegt.

-   Konfigurieren des System Center Operations Manager Packs.

-   Konfigurieren der Serverwiederherstellung im Falle einer Beschädigung des Betriebssystems.

###  <a name="client-experience"></a><a name="BKMK_ClientXP"></a>Client Darstellung
 Sie können die folgenden Endbenutzerszenarien testen:

-   Bereitstellen von Clients über das Internet (PC oder Mac).

-   Zugreifen auf freigegebene Ordner über das Launchpad auf dem Client

-   Zugreifen auf Serverressourcen mithilfe von Remotewebzugriff von verschiedenen Geräten (PC, Telefon, Tablet) aus.

-   Zugreifen auf die App "Eigener Server" für Windows Phone.

-   (Falls zutreffend) Zugreifen auf den Dateiversionsverlauf, die Clientsicherung und -wiederherstellung und Ordnerumleitung.

-   (Falls zutreffend) Überprüfen der E-Mail-Integrationsumgebung.

##  <a name="support-information"></a><a name="BKMK_Support"></a>Support Informationen
 Sie können das Windows Server Essentials Software Development Kit (SDK) und das Windows Server Essentials Assessment and Deployment Kit (ADK) herunterladen:

-   [Windows Server Essentials Software Development Kit](https://msdn.microsoft.com/library/gg513877.aspx) SDK

-   [Anpassen und Bereitstellen von Windows Server Essentials in Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx)

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Neues in Windows Server Essentials](../get-started/what-s-new.md)

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

-   [Erste Schritte in Windows Server Essentials](../get-started/get-started.md)
