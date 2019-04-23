---
title: Migration von DirectAccess zu Always On-VPN
description: Migration von DirectAccess zu Always On-VPN-erfordert einen bestimmten Prozess muss nach dem Migrieren von Clients, wodurch Racebedingungen zu, die Minimieren von der Durchführung der Schritte bei der Migration außerhalb der Reihenfolge auftreten.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 06/07/2018
ms.openlocfilehash: 94852b33936ece0b329614f428e845f2c7a2ac6a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854581"
---
# <a name="migrate-to-always-on-vpn-and-decommission-directaccess"></a>Migrieren zu Always On VPN und DirectAccess Außerbetriebnahme

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

&#171;[ **Vorherigen:** Planen von DirectAccess auf Always On-VPN-migration](da-always-on-migration-planning.md)<br>

Migration von DirectAccess zu Always On-VPN-erfordert einen bestimmten Prozess muss nach dem Migrieren von Clients, wodurch Racebedingungen zu, die Minimieren von der Durchführung der Schritte bei der Migration außerhalb der Reihenfolge auftreten. Auf einer hohen Ebene besteht aus diesen vier primäre Schritte während der Migration:

1.  **Stellen Sie eine Seite-an-Seite-VPN-Infrastruktur bereit.** Nachdem Sie ermittelt haben, Ihre Migrationsphasen und die Features, die in Ihrer Bereitstellung enthalten sein sollen, können Sie die VPN-Infrastruktur parallel mit der vorhandenen DirectAccess-Infrastruktur bereitstellen.  

2.  **Bereitstellen Sie Zertifikate und die Konfiguration für die Clients.**  Nachdem die VPN-Infrastruktur fertig ist, erstellen und veröffentlichen die erforderlichen Zertifikate an den Client. Wenn die Clients die Zertifikate erhalten haben, stellen Sie das Konfigurationsskript VPN_Profile.ps1 bereit. Alternativ können Sie Intune zum Konfigurieren des VPN-Clients verwenden. Verwenden Sie Microsoft System Center Configuration Manager oder Microsoft Intune, um die erfolgreiche VPN-Konfiguration-Bereitstellungen zu überwachen.

3.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

Achten Sie bevor Sie während der Migration wird von DirectAccess mit Always On-VPN-beginnen darauf, dass Sie für die Migration geplant haben.  Wenn Sie nicht die Migration geplant haben, finden Sie unter [Planen von DirectAccess auf die Migration zu Always On-VPN-](da-always-on-migration-planning.md).

>[!TIP] 
>In diesem Abschnitt ist es sich nicht um eine schrittweise bereitstellungsanleitung für Always On-VPN- sondern dient eher als Ergänzung zu [Always On-VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) und Anleitungen zur Migration-spezifische Bereitstellung bereitstellen.

## <a name="deploy-a-side-by-side-vpn-infrastructure"></a>Bereitstellen einer Seite-an-Seite-VPN-Infrastruktur

Sie stellen die VPN-Infrastruktur parallel mit der vorhandenen DirectAccess-Infrastruktur bereit.  Detaillierte Informationen finden Sie unter [Always On-VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) installieren und Konfigurieren der Always On-VPN-Infrastruktur. 

Seite-an-Seite-Deployment umfasst die folgenden grundlegenden Tasks:

1.  Erstellen Sie die VPN-Benutzer, VPN-Server und NPS-Server-Gruppen.

2.  Erstellen Sie und veröffentlichen Sie die erforderlichen Zertifikatvorlagen.

3.  Registrieren Sie die Serverzertifikate.

4.  Installieren Sie und konfigurieren Sie für die Always On-VPN-RAS-Dienst.

5.  Installieren und Konfigurieren von NPS.

6.  Konfigurieren von DNS und die Firewallregeln für Always On-VPN.

Die folgende Grafik zeigt eine visuelle Referenz für die infrastrukturänderungen für das DirectAccess-zu-Always On-VPN-Migration.

![](../../media/DA-to-AlwaysOnVPN/6b64f322f945f837f22a32bf87a228f8.png)

## <a name="deploy-certificates-and-vpn-configuration-script-to-the-clients"></a>Bereitstellen Sie Zertifikate und VPN-Konfigurationsskript für die Clients.

Obwohl der Großteil der VPN-Clientkonfiguration in der [Bereitstellen von Always On-VPN-](../vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment.md) Abschnitt zwei zusätzliche Schritte sind erforderlich, um die Migration von DirectAccess zu Always On-VPN-erfolgreich abgeschlossen. 

Sie müssen sicherstellen, dass die **VPN_Profile.ps1** stammt _nach_ das Zertifikat wurde ausgestellt, damit der VPN-Client nicht versucht, ohne eine Verbindung herstellen. Zu diesem Zweck führen Sie ein Skript, das nur die Benutzer an, die registriert wurden im Zertifikat in Ihre VPN-Bereitstellung bereit-Gruppe fügt hinzu, die Sie zum Bereitstellen der Always On-VPN-Konfiguration verwenden.

>[!NOTE] 
>Microsoft empfiehlt, dass Sie diesen Prozess testen, bevor Sie es auf Ihre Benutzer Migration Ringe ausführen.

1.  **Erstellen Sie und veröffentlichen Sie das VPN-Zertifikat, und aktivieren Sie die automatische Registrierung-Gruppenrichtlinienobjekt (GPO).** Für herkömmliche, auf Zertifikaten basierende Windows 10-VPN-Bereitstellungen wird ein Zertifikat, das Gerät oder der Benutzer ausgestellt, damit sie die Verbindung authentifizieren kann. Wenn das neue Authentifizierungszertifikat erstellt und für die automatische Registrierung veröffentlicht wird, muss erstellen und Bereitstellen von ein Gruppenrichtlinienobjekt mit der automatischen Registrierung-Einstellung so konfiguriert, dass der VPN-Benutzergruppe. Die Schritte zum Konfigurieren von Zertifikaten und die automatische Registrierung finden Sie unter [konfigurieren die Serverinfrastruktur](../vpn/always-on-vpn/deploy/vpn-deploy-server-infrastructure.md).

2.  **Hinzufügen von Benutzern der Gruppe der VPN-Benutzer.** Fügen Sie beliebige Benutzer, die Sie der Gruppe der VPN-Benutzer zu migrieren. Diese Benutzer bleiben in dieser Sicherheitsgruppe, nachdem Sie sie migriert haben, sodass sie alle zertifikatupdates in der Zukunft empfangen zu können. Weiterhin Benutzer dieser Gruppe hinzufügen, bis Sie alle Benutzer von DirectAccess in Always On-VPN-verschoben haben. 

3.  **Identifizieren Sie Benutzer, die eine VPN-Authentifizierungszertifikat erhalten haben.** Migrieren Sie von DirectAccess, daher müssen Sie zum Hinzufügen einer Methode zum Identifizieren, wenn ein Client das erforderliche Zertifikat erhalten hat und bereit ist, die VPN-Konfigurationsinformationen zu empfangen. Führen Sie die **GetUsersWithCert.ps1** Skript, um Benutzer hinzuzufügen, die derzeit nonrevoked Zertifikate, die nicht mit dem Namen der angegebenen Vorlage stammen, zu einer angegebenen AD DS-Sicherheitsgruppe, ausgestellt werden. Z. B. nach dem Ausführen der **GetUsersWithCert.ps1** -Skript ausgegeben jeder Benutzer ein gültiges Zertifikat aus der Vorlage, der Gruppe "VPN-Bereitstellung bereit hinzugefügt wird" VPN-Authentifizierungszertifikat.

    >[!NOTE] 
    >Wenn Sie eine Methode, um zu ermitteln, wann ein Client das erforderliche Zertifikat erhalten hat, nicht verfügen, können Sie die VPN-Konfiguration bereitstellen, bevor der Benutzer, verursacht die VPN-Verbindung nicht das Zertifikat ausgestellt wurde. Um dies zu vermeiden, führen Sie die **GetUsersWithCert.ps1** Skript bei der Zertifizierungsstelle oder nach einem Zeitplan zum Synchronisieren von Benutzern, die das Zertifikat in der Gruppe "VPN-Bereitstellung bereit" erhalten haben. Dann werden dieser Sicherheitsgruppe können Sie Ihre VPN-Bereitstellung in System Center Configuration Manager oder Intune, der sicherstellt, dass der verwaltete Client die VPN-Konfiguration nicht erhält, bevor sie das Zertifikat empfangen hat als Ziel.
    
    ### <a name="getuserswithcertps1"></a>GetUsersWithCert.ps1
    
    ```powershell
    Import-module ActiveDirectory
    Import-Module AdcsAdministration
    
    $TemplateName = 'VPNUserAuthentication'##Certificate Template Name (not the friendly name)
    $GroupName = 'VPN Deployment Ready' ##Group you will add the users to
    $CSServerName = 'localhost\corp-dc-ca' ##CA Server Information
    
    $users= @()
    $TemplateID = (get-CATemplate | Where-Object {$_.Name -like $TemplateName} | Select-Object oid).oid
    $View = New-Object -ComObject CertificateAuthority.View
    $NULL = $View.OpenConnection($CSServerName)
    $View.SetResultColumnCount(3)
    $i1 = $View.GetColumnIndex($false, "User Principal Name")
    $i2 = $View.GetColumnIndex($false, "Certificate Template")
    $i3 = $View.GetColumnIndex($false, "Revocation Date")
    $i1, $i2, $i3 | %{$View.SetResultColumn($_) }
    $Row= $View.OpenView()
    
    while ($Row.Next() -ne -1){
    $Cert = New-Object PsObject
    $Col = $Row.EnumCertViewColumn()
    [void]$Col.Next()
    do {
    $Cert | Add-Member -MemberType NoteProperty $($Col.GetDisplayName()) -Value $($Col.GetValue(1)) -Force
          }
    until ($Col.Next() -eq -1)
    $col = ''
    
    if($cert."Certificate Template" -eq $TemplateID -and $cert."Revocation Date" -eq $NULL){
       $users= $users+= $cert."User Principal Name"
    $temp = $cert."User Principal Name"
    $user = get-aduser -Filter {UserPrincipalName -eq $temp} –Property UserPrincipalName
    Add-ADGroupMember $GroupName $user
       }
      }
    ```

4. Stellen Sie die Always On-VPN-Konfiguration bereit. Als das VPN Clientauthentifizierungszertifikate ausgestellt werden, und Sie führen die **GetUsersWithCert.ps1** Skripts, die Benutzer werden hinzugefügt, der Sicherheitsgruppe der VPN-Bereitstellung bereit.


| Bei Verwendung von...  | Folge |
| ---- | ---- |
| System Center Configuration Manager | Erstellen Sie eine benutzersammlung, die basierend auf Mitgliedschaft in dieser Sicherheitsgruppe.<br><br>![](../../media/DA-to-AlwaysOnVPN/b38723b3ffcfacd697b83dd41a177f66.png)!|
| Intune | Zielen Sie die Sicherheitsgruppe einfach direkt auf, nachdem er synchronisiert wird. |
|
    
Bei jeder Ausführung der **GetUsersWithCert.ps1** Konfigurationsskript, müssen Sie auch eine AD DS-Regel für die Ermittlung die Mitgliedschaft in Sicherheitsgruppen in System Center Configuration Manager aktualisieren ausführen. Stellen Sie außerdem sicher, dass die Aktualisierung der Gruppenmitgliedschaft für die bereitstellungssammlung häufig genug auftritt (mit der Regel Skript und Ermittlung ausgerichtet).

Weitere Informationen zur Verwendung von System Center Configuration Manager oder Intune zum Bereitstellen von Always On-VPN-Clients für Windows finden Sie unter [Always On-VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md). Achten Sie darauf, aber diese Migration-spezifische Aufgaben integrieren.

>[!NOTE] 
>Integrieren diese Migration-spezifische Aufgaben ist eine wichtige Unterschied zwischen einem einfachen Always On-VPN-Bereitstellung und Migration von DirectAccess zu Always On-VPN. Achten Sie darauf, dass die Sicherheitsgruppe, statt die Methode im Bereitstellungshandbuch als Ziel die Sammlung definieren.


## <a name="remove-devices-from-the-directaccess-security-group"></a>Entfernen Sie Geräte aus der Sicherheitsgruppe für DirectAccess

Als Benutzer des Zertifikats erhalten und die **VPN_Profile.ps1** Konfigurationsskript, daraufhin erfolgreiche VPN-Konfiguration Skripterstellung für die Bereitstellung in System Center Configuration Manager oder Intune entsprechen. Entfernen Sie nach jeder Bereitstellung Gerät des Benutzers aus der Sicherheitsgruppe für DirectAccess, damit Sie später DirectAccess entfernen können. Sowohl Intune als auch System Center Configuration Manager enthält Benutzerzuweisungsinformationen und Gerät Zuweisung können Sie die von den Geräten jedes Benutzers zu bestimmen.

>[!NOTE] 
>Wenn Sie DirectAccess-Gruppenrichtlinienobjekte über Organisationseinheiten (Organizational Unit) anstatt Computergruppen anwenden, verschieben Sie die Computer-Objekt aus der Organisationseinheit des Benutzers.

## <a name="decommission-the-directaccess-infrastructure"></a>Außerbetriebnahme der DirectAccess-Infrastruktur

Wenn Sie die Migration von den DirectAccess-Clients zu Always On-VPN-abgeschlossen haben, können Sie außer Betrieb setzen die DirectAccess-Infrastruktur und entfernen Sie die DirectAccess-Einstellungen von der Gruppenrichtlinie. Microsoft empfiehlt, die folgenden Schritte aus, um ordnungsgemäß zu DirectAccess in Ihrer Umgebung entfernen:

1.  [!INCLUDE [remove-config-settings-shortdesc-include](../includes/remove-config-settings-shortdesc-include.md)]

    ![](../../media/DA-to-AlwaysOnVPN/dbdc3d80e8dc1b8665f7b15d7d2ee1f6.png)

2.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

3.  **Bereinigen Sie DNS.** Achten Sie darauf, dass Sie alle Datensätze aus Ihrem internen DNS-Server zu entfernen und öffentlicher DNS-Server im Zusammenhang mit DirectAccess können z. B. DA.contoso.com, DAGateway.contoso.com.

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

5.  **Entfernen Sie alle DirectAccess-Zertifikate von Active Directory Certificate Services.** Wenn Sie für die Implementierung des DirectAccess-Computerzertifikate verwendet, entfernen Sie veröffentlichten Vorlagen aus dem Ordner "Zertifikatvorlagen" in der Zertifizierungsstellenkonsole.

## <a name="next-step"></a>Nächster Schritt
Sie sind fertig Migration von DirectAccess zu Always On-VPN. 

---