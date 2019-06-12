---
title: Bereitstellen von Windows Server Essentials Experience als einen gehosteten Server
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: 94d4040b65a63fe64e5d49d55f82c4deead5a121
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433584"
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Bereitstellen von Windows Server Essentials Experience als einen gehosteten Server

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Dokument enthält spezifische Informationen für Hostinganbieter, die Microsoft Windows Server-16 mit Windows Server Essentials Experience-Rolle (bezeichnet als Windows Server Essentials im weiteren Verlauf des Dokuments) installiert in ihrer testumgebung bereitstellen möchten, und Windows Server Essentials Experience als Dienst für ihre Kunden anbieten möchten. Dieses Dokument enthält die folgenden Abschnitte:  
  

-   [Übersicht über die Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Vorteile des Hostings von Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [Unterstützte Bereitstellungsoptionen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [Unterstützte Netzwerktopologien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Anpassen des Images der Windows Server Essentials Experience-Rolle](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Automatisieren der Bereitstellung von Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Migrieren von Daten von Windows Small Business Server zu Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Führen Sie allgemeiner Aufgaben mithilfe von Windows PowerShell aus](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [E-Mail-Integration in Windows Server Essentials](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [Überwachen Sie und verwalten Sie, indem Sie mit systemeigenen tools](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [Testszenarien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [Supportinformationen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

-   [Übersicht über die Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Vorteile des Hostings von Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [Unterstützte Bereitstellungsoptionen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [Unterstützte Netzwerktopologien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Anpassen des Images der Windows Server Essentials Experience-Rolle](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Automatisieren der Bereitstellung von Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Migrieren von Daten von Windows Small Business Server zu Windows Server Essentials Experience](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Führen Sie allgemeiner Aufgaben mithilfe von Windows PowerShell aus](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [E-Mail-Integration in Windows Server Essentials](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [Überwachen Sie und verwalten Sie, indem Sie mit systemeigenen tools](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [Testszenarien](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [Supportinformationen](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

  
##  <a name="BKMK_WSEEOverview"></a> Übersicht über die Windows Server Essentials Experience  
 Die Windows Server Essentials Experience ist eine Serverrolle, die in der Windows Server 2012 R2 Standard und Windows Server 2012 R2 Datacenter verfügbar ist. Wenn Windows Server Essentials Experience-Rolle auf einem Server mit Windows Server 2012 R2 installiert ist, kann Kunden alle Funktionen nutzen, die in Windows Server Essentials ohne Sperren und Beschränkungen verfügbar sind. Die Windows Server Essentials-Umgebung können die folgenden standortübergreifenden Lösungen für kleine und mittelständische Unternehmen:  
  
-   **Datenspeicherung und-Schutz** können Sie den Kunden speichern "des s Daten an einem zentralen Ort und Server-und Clientdaten schützen, indem Sie die Server- und Clientcomputer (weniger als 75) im Netzwerk sichern.  
  
-   **Benutzerverwaltung** Sie können die Benutzer und Gruppen über das vereinfachte Server-Dashboard verwalten. Darüber hinaus ermöglicht die Integration in Microsoft Azure Active Directory (Azure AD) einfachen Datenzugriff für Microsoft online Services (z. B. Office 365, Exchange Online und SharePoint Online) für Benutzer, mit ihren Domänenanmeldeinformationen an.  
  
-   **Integration von Service** können Sie den Server mit Microsoft online Services (z. B. Office 365, SharePoint Online und Microsoft Azure Backup) integrieren. Sie können den Server auch in Ihre Dienste oder in Dienste von Drittanbietern integrieren.  
  
-   **Zugriff überall** Kunden können von nahezu überall aus und mit fast jedem Gerät auf Server, Netzwerkcomputer und Daten zugreifen, sofern sie eine Internetverbindung haben. Mit dem Remotewebzugriff können sie über eine optimierte Browserumgebung, die die Fingereingabe unterstützt, auf Anwendungen und Daten zugreifen. My Server-app können sie Daten aus einer Windows Phone oder eine Microsoft Store-app zugreifen.  
  
-   **Medienstreaming** Wenn Sie das Medienpaket auf einem Server mit Windows Server Essentials Experience aktiviert installieren, die Kunden kann Musik, Videos und Fotos in freigegebenen Ordnern speichern und dann auf diese Mediendateien zugreifen, aus der Netzwerkcomputer oder Der Remotewebzugriff.  
  
-   **Statusüberwachung** Sie können die Integrität des Netzwerks überwachen und benutzerspezifische Statusberichte abrufen.  
  
##  <a name="BKMK_Benefits"></a> Vorteile des Hostings von Windows Server Essentials Experience  
  Windows Server Essentials Experience ist eine Rolle in Windows Server, daher können Sie das vorhandene bereitstellungs- und verwaltungsframework von Windows Server bereitstellen und konfigurieren Sie die Windows Server Essentials Experience-Rolle. Die Windows Server Essentials Experience-Rolle hostet, bietet die folgenden Vorteile:  
  
-   **Optimierte Bereitstellung** durch die Windows Server Essentials Experience-Rolle aktivieren, einige der am häufigsten häufigsten verwendeten Rollen und Funktionen aktiviert und mit bewährten Methoden für kleine und mittelständische Unternehmen konfiguriert. Sie können die Windows Server Essentials-Funktionen anpassen oder einige der lokalen Funktionen ausblenden. Wenn Sie die Windows Azure Pack verwenden, können Sie die Katalogvorlage für Windows Server Essentials Experience unter Windows Server 2012 R2 herunterladen.  
  
-   **Vereinfachtes Dashboard** Das Windows Server Essentials-Dashboard vereinfacht allgemeine Aufgaben wie das Verwalten von Serverordnern, Serverspeichern, Sicherung und Wiederherstellung, Benutzer- oder Gruppenkonten, Geräten, Remotezugriff und E-Mail. Kleine und mittelständische Unternehmen können täglich wiederkehrende Verwaltungsaufgaben ausführen, anstatt den Helpdesk um technischen Support bitten zu müssen.  
  
-   **Erweiterbarkeit** Das Windows Server Essentials-Dashboard und Windows Server Essentials Connector-Software sind erweiterbar. Sie können ihr eigenes Branding und eine Dienstintegration hinzufügen, damit Ihre Kunden einen zentralen Einstiegspunkt für alle Belange in Bezug auf ihre Server und Dienste haben.  
  
-   **Monitor** Es steht eine neue Version des System Center-Überwachungspakets zur Verfügung, um mehrere Server mit Windows Server Essentials zu überwachen und zu verwalten. Informationen zum Herunterladen des Management Packs finden Sie unter [System Center Management Pack für Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).  
  
##  <a name="BKMK_SupportedDeployment"></a> Unterstützte Bereitstellungsoptionen  
  Windows Server Essentials Experience kann als Domänencontroller in einer neuen Active Directory-Umgebung bereitgestellt werden. oder sie können in einer vorhandenen Active Directory-Umgebung als Mitglied einer Domäne bereitgestellt werden.  
  
 Es wird empfohlen, zuerst Bereitstellen von Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter, und klicken Sie dann die Windows Server Essentials Experience-Rolle zu installieren. Mit dieser Bereitstellungsmethode erhalten Sie alle Funktionen der Windows Server Essentials-Edition, jedoch ohne die Sperren und Beschränkungen.  
  

 Weitere Informationen zum Installieren von Windows Server 2012 R2 mit Windows Server Essentials Experience-Rolle finden Sie unter [installieren und Konfigurieren von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  


  
##  <a name="BKMK_SupportedToplogy"></a> Unterstützte Netzwerktopologien  
 Um Windows Server Essentials-Umgebung von einem roamingclient aus zu verwenden, muss VPN aktiviert werden. Um den Remotezugriff auf den Server von einem Roamingclient aus zu aktivieren, müssen Sie auf dem Server Port 443 und Port 80 öffnen.  
  
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
  
  -   Ermöglichen Sie es dem Port 443 auf dem Server, eine öffentliche Port-443-IP-Adresse zu erreichen.  
  
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
  
##  <a name="BKMK_CustomizeImage"></a> Anpassen des Images der Windows Server Essentials Experience-Rolle  
 Sie können das Image vor dem Konfigurieren der Rolle "Windows Server Essentials-Umgebung" anpassen. Weitere Informationen zum standardmäßigen Windows Server Sysprep-Prozess finden Sie im [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx). Nachdem Sie das Image mithilfe von Sysprep vorbereitet haben, können Sie es verwenden oder es für eine neue Bereitstellung erneut in "Install.wim" versiegeln.  
  
 Wenn Sie Virtual Machine Manager verwenden, können Sie eine Vorlage mithilfe der ausgeführten Instanz erstellen. Bei diesem Vorgang wird die Instanz mithilfe von Sysprep vorbereitet und der Computer heruntergefahren. Nachdem Sie die Vorlage in Ihrer Bibliothek gespeichert haben, können Sie sie je nach spezifischen Anforderungen verwenden.  
  
 Nachdem Sie Windows Server Essentials Experience-Rolle installiert haben, können Sie die Features in Windows Server Essentials anpassen. Eine der wichtigsten Anpassungen ist der Registrierungsschlüssel **IsHosted**: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\Deployment\IsHosted**.  
  
 Wenn dieser Schlüssel auf 0x1 festgelegt ist, ändern einige der lokalen Funktionen ihr Verhalten. Unter anderem ändern sich die folgenden Funktionen:  
  
- **Clientsicherung** Die Clientsicherung ist jetzt für neu verbundene Clientcomputer standardmäßig deaktiviert.  
  
- **Clientwiederherstellungsdienst** Clientwiederherstellungsdienst will be disabled, and the UI will be hidden from the Dashboard.  
  
- **Dateiversionsverlauf** Die Dateiversionsverlaufseinstellungen für neu erstellte Benutzerkonten werden nicht automatisch vom Server verwaltet.  
  
- **Serversicherung** Der Serversicherungsdienst wird deaktiviert, und die Serversicherungsbenutzeroberfläche wird nicht mehr im Dashboard angezeigt.  
  
- **Speicherplätze** Die Benutzeroberfläche für das Erstellen oder Verwalten von Speicherplätzen wird nicht mehr im Dashboard angezeigt.  
  
- **Zugriff überall** Die Router- und VPN-Konfiguration wird standardmäßig übersprungen, wenn Sie den Assistenten zum Einrichten von "Zugriff überall" ausführen.  
  
  Wenn Sie das Verhalten der einzelnen aufgeführten Funktionen steuern möchten, können Sie den entsprechenden Registrierungsschlüssel für jede festlegen. Informationen dazu, wie Sie den Registrierungsschlüssel festlegen, finden Sie unter [Anpassen und Bereitstellen von Windows Server Essentials unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx).  
  
##  <a name="BKMK_AutomateDeployment"></a> Automatisieren der Bereitstellung von Windows Server Essentials Experience  
 Zum Automatisieren der Bereitstellung müssen Sie zunächst das Betriebssystem bereitstellen und installieren Sie dann auf die Windows Server Essentials Experience-Rolle.  
  
-   Folgen Sie den Anweisungen, zur automatischen Bereitstellung von Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx).  
  
-   Vorgehensweise: Installieren Sie Windows Server Essentials Experience-Rolle mithilfe von Windows PowerShell finden Sie unter [installieren und Konfigurieren von Windows Server Essentials](https://technet.microsoft.com/library/dn281793.aspx).  
  
> [!NOTE]
>  Stellen Sie sicher, dass die zeitzoneneinstellungen des virtuellen Hostcomputers und der Windows Server Essentials Experience identisch sind. Andernfalls können verschiedene Fehler auftreten. Dazu gehören: die Erstkonfiguration des Servers möglicherweise nicht erfolgreich zertifikatsspezifischen Aufgaben, die das Zertifikat funktioniert ggf. erst einige Stunden nach die Windows Server Essentials Experience-Rolle installiert ist, und die Geräteinformationen nicht aktualisiert werden werden. richtig.  
  
 Nach der Bereitstellung verwenden Sie das Windows PowerShell-Cmdlet **Get-WssConfigurationStatus**, um zu überprüfen, ob die Erstkonfiguration erfolgreich war. Der zurückgegebene Status sollte einer der folgenden sein: **Notstarted**, **FinishedWithWarning**, **Running**, **Finished**, **Failed** oder **PendingReboot**.  
  
 Der Server wird während der Erstkonfiguration neu gestartet. Wenn Sie diesen automatischen Neustart verhindern müssen, können Sie den folgenden Befehl verwenden, um einen Registrierungsschlüssel hinzuzufügen, bevor Sie mit der Erstkonfiguration beginnen:  
  
```  
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false  
  
```  
  
 Sobald Sie mit der Erstkonfiguration beginnen, können Sie **Get-WssConfigurationStatus** verwenden, um den Status der Erstkonfiguration zu überprüfen. Wenn der Status **PendingReboot** ist, können Sie den Server neu starten.  
  
##  <a name="BKMK_Migrate"></a> Migrieren von Daten von Windows Small Business Server zu Windows Server Essentials Experience  
 Sie können Daten von Servern mit Windows Small Business Server 2011, Windows Small Business Server 2008, Windows Small Business Server 2003 oder Windows Server Essentials mit dem Server mit Windows Server Essentials migrieren. Überprüfen Sie die [Migrieren zu Windows Server Essentials](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md) Migration Leitfaden zu von einem lokalen 2migrations und erforderlichen Anpassungen entsprechend Ihrer Hostingumgebung vorzunehmen.  
  
> [!NOTE]
>  Platzieren Sie den Quellserver und den Zielserver am besten im gleichen Subnetz. Falls dies nicht möglich ist, stellen Sie Folgendes sicher:  
> 
> - Der Quellserver und Zielserver können aufeinander zugreifen "des s interne DNS-Namen.  
>   -   Alle erforderlichen Ports sind geöffnet.  
  
 Nach der Migration können Sie Ihre Lizenzen aktualisieren, um die Sperren und Beschränkungen zu entfernen. Weitere Informationen finden Sie unter [Übergang von Windows Server Essentials in Windows Server 2012 Standard](https://technet.microsoft.com/library/jj247582.aspx).  
  
##  <a name="BKMK_PowerShell"></a> Führen Sie allgemeiner Aufgaben mithilfe von Windows PowerShell aus  
 In diesem Abschnitt werden einige allgemeinen Aufgaben erläutert, die Sie mithilfe von Windows PowerShell ausführen können.  
  
### <a name="enable-remote-web-access"></a>Aktivieren von Remotewebzugriff  
 **Syntax**:  
  
 Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
  
 **Beispiel**:  
  
 $Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
  
 Mit diesem Befehl wird Remotewebzugriff aktiviert, wobei der Router automatisch konfiguriert wird. Zudem werden die Standardzugriffsberechtigungen für alle vorhandenen Benutzer geändert.  
  
### <a name="add-user"></a>Benutzer hinzufügen  
 **Syntax**:  
  
 Hinzufügen-WssUser [-Name] < Zeichenfolge\> [-Kennwort] < Securestring\> [-AccessLevel < Zeichenfolge\> {Benutzer &#124; Administrator}] [-FirstName < Zeichenfolge\>] [-LastName < Zeichenfolge\>] [- AllowRemoteAccess] [-AllowVpnAccess] [< Allgemeineparameter\>]  
  
 **Beispiel**:  
  
 $password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test  
  
 Dieser Befehl fügt einen Administrator mit dem Namen "User2Test", und das Kennwort Passw0rd!.  
  
### <a name="add-server-folder"></a>Hinzufügen eines Serverordners  
 **Syntax**:  
  
 Hinzufügen-WssFolder [-Name] < Zeichenfolge\> [-Path] < Zeichenfolge\> [[-Beschreibung] < Zeichenfolge\>] [-KeepPermissions] [< Allgemeineparameter\>]  
  
 **Beispiel**:  
  
 $Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
  
 Dieser Befehl fügt einen Serverordner namens MyTestFolder an der angegebenen Position.  
  
##  <a name="BKMK_EmailIntegration"></a> E-Mail-Integration in Windows Server Essentials  
 Sie können Windows Server Essentials Experience mit Office 365 integrieren oder gehosteten Exchange-Server. Damit Ihre Kunden auch Ihren gehosteten E-Mail-Dienst verwenden können, müssen Sie ein Add-In entwickeln, um die Windows Server Essentials-Umgebung in Ihre gehostete E-Mail-Lösung zu integrieren. Weitere Informationen finden Sie im [Windows Server Essentials SDK](https://msdn.microsoft.com/library/gg513877.aspx).  
  
##  <a name="BKMK_Monitoring"></a> Überwachen Sie und verwalten Sie, indem Sie mit systemeigenen tools  
 Dieser Abschnitt beschreibt die systemeigenen Tools, die in Windows Server 2012 R2 zum Überwachen und Verwalten des Servers verfügbar sind.  
  
### <a name="group-policy"></a>Gruppenrichtlinie  
  Windows Server Essentials Experience nutzt die systemeigene gruppenrichtlinienunterstützung in Windows Server 2012 R2 und stellt eine Benutzeroberfläche zum Konfigurieren der Ordnerumleitung und Sicherheitseinstellungen bereit.  
  
> [!NOTE]
>  In einer gehosteten Umgebung kann bei aktivierter Ordnerumleitung für ein Benutzerprofil das Anmelden von Endbenutzern länger dauern, wenn die Datengröße erheblich ist.  
  
### <a name="system-center-monitoring-pack"></a>System Center-Überwachungspaket  
 System Center Monitoring Pack für Windows Server Essentials Experience-überwacht die Integrität Warnungssystem helfen Ihnen beim Verwalten der großen Anzahl von Servern mit Windows Server Essentials, die kleinen Organisationen zugeordnet sind. Weitere Informationen finden Sie unter [System Center Management Pack für Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809).  
  
### <a name="backup-and-restore"></a>Sicherung und Wiederherstellung  
  Windows Server 2012 R2 mit Windows Server Essentials-Umgebung können Sie Server- und Clientcomputer im Netzwerk sichern.  
  
#### <a name="server-backup"></a>Serversicherung  
 Windows Server Essentials unterstützt zwei Formen der Serversicherung: die lokale Sicherung und die externe Sicherung. Sie können diese Optionen anpassen, wenn Sie Ihre eigene Lösung zur Serversicherung bereitstellen möchten.  
  
-   **Lokale Sicherung** Mithilfe der lokalen Sicherung können Sie regelmäßig eine inkrementelle Sicherung auf Blockebene auf einem separaten Datenträger ausführen. Als Hostinganbieter könnten Sie eine virtuelle Festplatte mit dem virtuellen Computer mit Windows Server Essentials verbinden und dann die Serversicherung auf dieser virtuellen Festplatte konfigurieren. Die virtuelle Festplatte sollte sich auf einem anderen physischen Datenträger als der virtuelle Computer mit Windows Server Essentials befinden.  
  
    > [!NOTE]
    >  Wenn Sie andere Sicherungslösungen für die virtuellen Computer verwenden und Sie verhindern möchten, dass die Benutzer die systemeigene Serversicherungsfunktion von Windows Server Essentials sehen, können Sie sie deaktivieren und die zugehörige Benutzeroberfläche im Dashboard entfernen. Weitere Informationen finden Sie im Abschnitt [Anpassen der Serversicherung](https://technet.microsoft.com/library/dn293413.aspx) unter [Anpassen und Bereitstellen von Windows Server Essentials unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx).  
  
-   **Externe Sicherung** Mithilfe dieser Sicherung können Sie die Serverdaten in regelmäßigen Abständen in einem Cloud-basierten Dienst sichern. Sie können die herunterladen und installieren Microsoft Azure Backup-Integration-Modul für Windows Server Essentials um die Azure-Sicherung nutzen zu können, die von Microsoft bereitgestellt wird.  
  
     Weitere Informationen finden Sie unter integrieren Windows Azure Backup mit Windows Server Essentials-Abschnitt im [Manage Server Backup](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md).  
  
     Beachten Sie Folgendes, wenn Sie oder Ihre Benutzer einen anderen Cloud-Dienst bevorzugen:  
  
    -   Aktualisieren Sie die Benutzeroberfläche des Dashboards, damit es auf den bevorzugten Cloud-Dienst anstelle von die standardmäßige Azure-Sicherung.  
  
    -   (Optional) Entwickeln Sie ein Add-In für das Dashboard, um den Cloud-basierten Sicherungsdienst zu konfigurieren und zu verwalten.  
  
#### <a name="client-computer-backup"></a>Clientcomputersicherung  
 Die Windows Server Essentials-Umgebung unterstützt zwei Formen der Clientdatensicherung: die vollständige Clientsicherung und den Dateiversionsverlauf.  
  
> [!NOTE]
>  Die Clientsicherung kann sich auf die Leistung auswirken, da die Daten über VPN vom Client an den Server übertragen werden müssen.  
  
##### <a name="full-client-backup"></a>Vollständige Clientsicherung  
 Die vollständige Clientsicherung ist standardmäßig für alle Clientgeräte aktiviert, die mit dem Windows Server Essentials-Netzwerk verbunden sind. Dabei werden alle Systeminformationen und Daten für den Client gesichert. Sie unterstützt zudem die Datendeduplizierung. Die Sicherungsdaten werden auf dem Server mit Windows Server Essentials gespeichert werden. Dadurch kann ein fehlerhafter Client Daten von einem früheren Sicherungspunkt abrufen.  
  
 Beachten Sie vor einer vollständigen Clientcomputersicherung Folgendes:  
  
-   **Leistung** Die erste Clientsicherung kann aufgrund der Menge an hochzuladenden Daten zeitaufwendig sein.  
  
-   **Stabilität** Es kann vorkommen, dass die Internetverbindung auf Clientseite nicht stabil ist. Clientsicherung soll automatisch fortgesetzt, und die clientsicherungsdatenbank erstellt einen Prüfpunkt, jedes Mal, wenn 40 GB Daten gesichert werden. Sie können diesen Wert in einen kleineren Wert ändern, wenn die Internetverbindung nicht zuverlässig ist.  
  
    -   So aktivieren Sie einen Prüfpunkt Auftrag Setzen Sie auf dem Server den Registrierungsschlüssel **HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs** auf 1.  
  
    -   So ändern Sie den Prüfpunkt-Schwellenwert Ändern Sie auf dem Client **HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold** von seinem Standardwert von 40 GB.  
  
-   **Bare-Metal-Recovery des Clients** Da die Windows-Vorinstallationsumgebung keine VPN-Verbindungen unterstützt, wird die Bare-Metal-Recovery des Clients nicht unterstützt. Sie sollten die Aufgabe des Clientwiederherstellungsdiensts ausblenden, indem Sie die Schritte unter [Anpassen und Bereitstellen von Windows Server Essentials in Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx)ausführen.  
  
##### <a name="file-history"></a>Dateiversionsverlauf  
 Der Dateiversionsverlauf ist eine Windows 8.1- und Windows 8-Funktion zum Sichern von Profildaten (Bibliotheken, Desktop, Kontakte, Favoriten) auf einer Netzwerkfreigabe. Sie können die Dateiversionsverlauf-Einstellung für alle Computer mit Windows 8.1 oder Windows 8 zentral verwalten, die mit einem Windows Server Essentials-Netzwerk verbunden sind. Die Sicherungsdaten werden auf dem Server gespeichert, auf dem Windows Server Essentials ausgeführt wird. Sie sollten die Aufgabe des Clientwiederherstellungsdiensts ausblenden, indem Sie die Schritte unter [Anpassen und Bereitstellen von Windows Server Essentials in Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx)ausführen.  
  
### <a name="storage-management"></a>Speicherverwaltung  
 Mithilfe von Speicherplätzen können Sie die physische Speicherkapazität verschiedenartiger Festplatten aggregieren, Festplatten dynamisch hinzufügen und Datenvolumes mit bestimmten Ausfallsicherheitsstufen erstellen. Dies ist auf dem Host oder auf dem virtuellen Computer möglich. Wenn Sie diese Funktion auf einem virtuellen Computer mit Windows Server Essentials ausblenden möchten, folgen Sie den Anweisungen unter [Anpassen und Bereitstellen von Windows Server Essentials in Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx).  
  
##  <a name="BKMK_Scenarios"></a> Testszenarien  
 Aus Hostperspektive sollten Sie am besten folgende Szenarien testen:  
  

-   [Server-Bereitstellung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)  
  
-   [Server-Konfiguration](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)  
  
-   [Serververwaltung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)  
  
-   [Clientumgebung](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)  

  
###  <a name="BKMK_ServerDeploy"></a> Server-Bereitstellung  
 Sie können die folgenden Bereitstellungsszenarien für den Server testen:  
  
-   Bereitstellen eines Servers mit Windows Server 2012 R2 als Domänencontroller in der Lab-Umgebung, und installieren Sie Windows Server Essentials Experience-Rolle.  
  
-   Bereitstellen eines Servers mit Windows Server 2012 R2 in Ihrer testumgebung, Verbinden des Servers zu einer vorhandenen Domäne und installieren Sie dann auf die Windows Server Essentials Experience-Rolle.  
  
-   Anpassen des Windows Server Essentials-Images nach Bedarf.  
  
-   Automatisieren der Windows Server Essentials-Bereitstellung mit einer unbeaufsichtigten Datei und Windows PowerShell.  
  
-   Migrieren von lokalen Servern mit Windows Small Business Server auf gehostete Server mit Windows Server Essentials.  
  
###  <a name="BKMK_ServerConfig2"></a> Server-Konfiguration  
 Sie können die folgenden Konfigurationsszenarien für den Server testen:  
  
-   Konfigurieren von "Zugriff überall" (VPN, Remotewebzugriff und DirectAccess).  
  
-   Konfigurieren von Speicher und Serverordnern.  
  
-   Aktivieren von BranchCache.  
  
-   (Falls zutreffend) Konfigurieren der Serversicherung, Onlinesicherung, Clientsicherung und des Dateiversionsverlaufs.  
  
-   (Falls zutreffend) Konfigurieren und Verwalten von Speicherplätzen  
  
-   (Falls zutreffend) Konfigurieren der Integration der E-Mail-Lösung (Office 365 und gehosteter Exchange-Server).  
  
-   (Falls zutreffend) Konfigurieren der Integration in andere Microsoft Online Services.  
  
-   (Falls zutreffend) Konfigurieren des Medienservers  
  
###  <a name="BKMK_ServerManage"></a> Serververwaltung  
 Sie können die folgenden Verwaltungsszenarien für den Server testen:  
  
-   Verwalten von Benutzern und Gruppen.  
  
-   Konfigurieren und Empfangen von E-Mail-Benachrichtigungen für Warnungen  
  
-   Ausführen von Best Practices Analyzer, um festzustellen, ob ein Fehler oder eine Warnmeldung vorliegt.  
  
-   Konfigurieren des System Center Operations Manager Packs.  
  
-   Konfigurieren der Serverwiederherstellung im Falle einer Beschädigung des Betriebssystems.  
  
###  <a name="BKMK_ClientXP"></a> Clientumgebung  
 Sie können die folgenden Endbenutzerszenarien testen:  
  
-   Bereitstellen von Clients über das Internet (PC oder Mac).  
  
-   Zugreifen auf freigegebene Ordner über das Launchpad auf dem Client  
  
-   Zugreifen auf Serverressourcen mithilfe von Remotewebzugriff von verschiedenen Geräten (PC, Telefon, Tablet) aus.  
  
-   Zugreifen auf die App "Eigener Server" für Windows Phone.  
  
-   (Falls zutreffend) Zugreifen auf den Dateiversionsverlauf, die Clientsicherung und -wiederherstellung und Ordnerumleitung.  
  
-   (Falls zutreffend) Überprüfen der E-Mail-Integrationsumgebung.  
  
##  <a name="BKMK_Support"></a> Supportinformationen  
 Sie können die Windows Server Essentials-Software Development Kit (SDK) und die Windows Server Essentials Assessment und Deployment Kit (ADK) herunterladen:  
  
-   [Windows Server Essentials-Software Development Kit](https://msdn.microsoft.com/library/gg513877.aspx)SDK  
  
-   [Anpassen und Bereitstellen von Windows Server Essentials unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn293241.aspx)  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Neuerungen in Windows Server Essentials](../get-started/what-s-new.md)  

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)  

-   [Erste Schritte in Windows Server Essentials](../get-started/get-started.md)
