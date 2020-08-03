---
title: Migration von DirectAccess zu Always on-VPN
description: Für die Migration von DirectAccess zu Always on VPN ist ein bestimmter Prozess zum Migrieren von Clients erforderlich. Dadurch können Racebedingungen minimiert werden, die durch das Ausführen von Migrations Schritten entstehen.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 06/07/2018
ms.openlocfilehash: 68184fe43fd027ea24bd0e77623002ec88368e86
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517695"
---
# <a name="migrate-to-always-on-vpn-and-decommission-directaccess"></a>Migrieren zu Always on VPN und Außerbetriebnahme von DirectAccess

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

[ **Vorherige &#171;:** Planen der DirectAccess-Always on VPN-Migration](da-always-on-migration-planning.md)<br>

Für die Migration von DirectAccess zu Always on VPN ist ein bestimmter Prozess zum Migrieren von Clients erforderlich. Dadurch können Racebedingungen minimiert werden, die durch das Ausführen von Migrations Schritten entstehen. Der Migrationsprozess umfasst auf hoher Ebene die folgenden vier Hauptschritte:

1.  **Stellen Sie eine Seite-an-Seite-VPN-Infrastruktur bereit.** Nachdem Sie die Migrations Phasen und die Features festgelegt haben, die Sie in die Bereitstellung einbeziehen möchten, stellen Sie die VPN-Infrastruktur nebeneinander mit der vorhandenen DirectAccess-Infrastruktur bereit.

2.  **Stellen Sie die Zertifikate und die Konfiguration für die Clients bereit.**  Sobald die VPN-Infrastruktur bereit ist, erstellen Sie die erforderlichen Zertifikate und veröffentlichen Sie auf dem Client. Wenn die Clients die Zertifikate erhalten haben, stellen Sie das Skript für die VPN_Profile.ps1 Konfiguration bereit. Alternativ können Sie InTune verwenden, um den VPN-Client zu konfigurieren. Verwenden Sie Microsoft Endpoint Configuration Manager oder Microsoft InTune, um erfolgreiche VPN-Konfigurations Bereitstellungen zu überwachen.

3.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

Stellen Sie vor dem Starten des Migrations Vorgangs von DirectAccess zum Always on-VPN sicher, dass Sie die Migration geplant haben.  Wenn Sie die Migration nicht geplant haben, finden Sie weitere Informationen unter [Planen der DirectAccess-Always on für die VPN-Migration](da-always-on-migration-planning.md).

>[!TIP]
>Bei diesem Abschnitt handelt es sich nicht um eine schrittweise Bereitstellungs Anleitung für Always on-VPN, sondern um die Ergänzung [Always on VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) und zur Bereitstellung einer Migrations spezifischen Bereitstellungs Anleitung.

## <a name="deploy-a-side-by-side-vpn-infrastructure"></a>Bereitstellen einer Seite-an-Seite-VPN-Infrastruktur

Sie stellen die VPN-Infrastruktur nebeneinander mit der vorhandenen DirectAccess-Infrastruktur bereit.  Ausführliche Informationen finden Sie unter [Always on VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) , um die Always on VPN-Infrastruktur zu installieren und zu konfigurieren.

Die parallele Bereitstellung besteht aus den folgenden Hauptaufgaben:

1.  Erstellen Sie die Gruppen VPN-Benutzer, VPN-Server und NPS-Server.

2.  Erstellen und veröffentlichen Sie die erforderlichen Zertifikat Vorlagen.

3.  Registrieren Sie die Server Zertifikate.

4.  Installieren und Konfigurieren des Remote Zugriffs Dienstanbieter für Always on-VPN.

5.  Installieren und Konfigurieren von NPS.

6.  Konfigurieren Sie DNS-und Firewallregeln für Always on-VPN.

Die folgende Abbildung bietet eine visuelle Referenz für die Infrastrukturänderungen in der gesamten DirectAccess-to –-always on-VPN-Migration.

![Diagramm der Änderungen an der Infrastruktur in DirectAccess-to – always on VPN Migration](../../media/DA-to-AlwaysOnVPN/6b64f322f945f837f22a32bf87a228f8.png)

## <a name="deploy-certificates-and-vpn-configuration-script-to-the-clients"></a>Bereitstellen von Zertifikaten und VPN-Konfigurations Skripts für Clients

Obwohl der Großteil der VPN-Client Konfiguration im Abschnitt bereitstellen [Always on VPN](../vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment.md) erforderlich ist, sind zwei zusätzliche Schritte erforderlich, um die Migration von DirectAccess zu Always on VPN erfolgreich abzuschließen.

Sie müssen sicherstellen, dass das **VPN_Profile.ps1** erfolgt, _nachdem_ das Zertifikat ausgestellt wurde, sodass der VPN-Client nicht versucht, eine Verbindung ohne diesen herzustellen. Hierzu führen Sie ein Skript aus, mit dem nur die Benutzer hinzugefügt werden, die sich im Zertifikat für Ihre Bereitstellung für die VPN-Bereitstellung registriert haben, die Sie zum Bereitstellen der Always on-VPN-Konfiguration verwenden.

>[!NOTE]
>Microsoft empfiehlt, dass Sie diesen Prozess testen, bevor Sie ihn für einen Ihrer Benutzer Migrations Ringe ausführen.

1.  **Erstellen und veröffentlichen Sie das VPN-Zertifikat, und aktivieren Sie die automatische Registrierung Gruppenrichtlinie Objekt (GPO).** Bei herkömmlichen, Zertifikat basierten Windows 10-VPN-bereit Stellungen wird ein Zertifikat für das Gerät oder den Benutzer ausgestellt, damit es die Verbindung authentifizieren kann. Wenn das neue Authentifizierungszertifikat erstellt und für die automatische Registrierung veröffentlicht wird, müssen Sie ein Gruppenrichtlinien Objekt mit der Einstellung für die automatische Registrierung erstellen und bereitstellen, die für die Gruppe "VPN-Benutzer" konfiguriert ist. Die Schritte zum Konfigurieren von Zertifikaten und zur automatischen Registrierung finden Sie unter [Konfigurieren der Serverinfrastruktur](../vpn/always-on-vpn/deploy/vpn-deploy-server-infrastructure.md).

2.  **Fügen Sie der Gruppe "VPN-Benutzer" Benutzer hinzu.** Fügen Sie Benutzer hinzu, die Sie zur Gruppe der VPN-Benutzer migrieren. Diese Benutzer bleiben in dieser Sicherheitsgruppe, nachdem Sie Sie migriert haben, damit Sie in Zukunft beliebige Zertifikat Updates empfangen können. Fügen Sie dieser Gruppe weiterhin Benutzer hinzu, bis Sie alle Benutzer aus DirectAccess in Always on VPN verschoben haben.

3.  **Identifizieren Sie Benutzer, die ein VPN-Authentifizierungszertifikat erhalten haben.** Wenn Sie von DirectAccess migrieren, müssen Sie eine Methode hinzufügen, um zu identifizieren, wann ein Client das erforderliche Zertifikat erhalten hat und bereit ist, die VPN-Konfigurationsinformationen zu empfangen. Führen Sie das **GetUsersWithCert.ps1** Skript aus, um Benutzer hinzuzufügen, die derzeit nicht wider sperrte Zertifikate aus dem angegebenen Vorlagen Namen in eine angegebene AD DS Sicherheitsgruppe ausgestellt haben. Nachdem Sie z. b. das **GetUsersWithCert.ps1** Skript ausgeführt haben, wird jeder Benutzer, der ein gültiges Zertifikat aus der VPN-Authentifizierungszertifikat Vorlage ausgestellt hat, der Bereitstellungs Gruppe für die VPN-Bereitstellung

    >[!NOTE]
    >Wenn Sie nicht über eine Methode verfügen, um zu ermitteln, wann ein Client das erforderliche Zertifikat erhalten hat, können Sie die VPN-Konfiguration bereitstellen, bevor das Zertifikat für den Benutzer ausgestellt wurde, wodurch die VPN-Verbindung fehlschlägt. Um diese Situation zu vermeiden, führen Sie das **GetUsersWithCert.ps1** Skript für die Zertifizierungsstelle oder einen Zeitplan aus, um die Benutzer zu synchronisieren, die das Zertifikat für die Bereitstellung der VPN-Bereitstellung erhalten haben. Anschließend verwenden Sie diese Sicherheitsgruppe, um Ihre VPN-Konfigurations Bereitstellung in Microsoft Endpoint Configuration Manager oder InTune als Ziel festzustellen. Dadurch wird sichergestellt, dass der verwaltete Client die VPN-Konfiguration nicht empfängt, bevor er das Zertifikat erhalten hat.

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

4. Stellen Sie die Always on-VPN-Konfiguration bereit. Wenn die VPN-Authentifizierungs Zertifikate ausgestellt werden und Sie das **GetUsersWithCert.ps1** Skript ausführen, werden die Benutzer der Sicherheitsgruppe für die Bereitstellung von VPN-bereit Stellungen hinzugefügt.


| Wenn Sie...  | Folge |
| ---- | ---- |
| Configuration Manager | Erstellen Sie eine Benutzer Sammlung, die auf der Mitgliedschaft dieser Sicherheitsgruppe basiert.<br><br>![Dialogfeld "Kriterieneigenschaften"](../../media/DA-to-AlwaysOnVPN/b38723b3ffcfacd697b83dd41a177f66.png)|
| Intune | Richten Sie die Sicherheitsgruppe einfach direkt nach der Synchronisierung ein. |

Jedes Mal, wenn Sie das Skript für die **GetUsersWithCert.ps1** Konfiguration ausführen, müssen Sie auch eine AD DS Ermittlungs Regel ausführen, um die Sicherheitsgruppen Mitgliedschaft in Configuration Manager zu aktualisieren. Stellen Sie außerdem sicher, dass das Mitgliedschafts Update für die Bereitstellungs Sammlung häufig genug ist (mit dem Skript und der Ermittlungs Regel abgestimmt).

Weitere Informationen zur Verwendung von Configuration Manager oder InTune zum Bereitstellen von Always on-VPN für Windows-Clients finden Sie unter [Always on die VPN-Bereitstellung für Windows Server und Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md). Stellen Sie jedoch sicher, dass Sie diese Migrations spezifischen Aufgaben integrieren.

>[!NOTE]
>Die Einbindung dieser Migrations spezifischen Aufgaben ist ein entscheidender Unterschied zwischen einer einfachen Always on-VPN-Bereitstellung und der Migration von DirectAccess zu Always on VPN. Stellen Sie sicher, dass Sie die Sammlung ordnungsgemäß als Ziel für die Sicherheitsgruppe definieren, anstatt die-Methode im Bereitstellungs Handbuch zu verwenden.


## <a name="remove-devices-from-the-directaccess-security-group"></a>Entfernen von Geräten aus der DirectAccess-Sicherheitsgruppe

Wenn Benutzer das Authentifizierungszertifikat und das **VPN_Profile.ps1** Konfigurationsskript erhalten, werden die entsprechenden erfolgreichen VPN-Konfigurationsskript Bereitstellungen in Configuration Manager oder InTune angezeigt. Entfernen Sie das Gerät des Benutzers nach jeder Bereitstellung aus der DirectAccess-Sicherheitsgruppe, damit Sie später DirectAccess entfernen können. Sowohl InTune als auch Configuration Manager enthalten Informationen zu Benutzer Geräte Zuweisungen, die Ihnen bei der Ermittlung der Geräte des Benutzers helfen.

>[!NOTE]
>Wenn Sie DirectAccess-GPOs über Organisationseinheiten (OUs) anstelle von Computer Gruppen anwenden, verschieben Sie das Computer Objekt des Benutzers aus der Organisationseinheit.

## <a name="decommission-the-directaccess-infrastructure"></a>Außerbetriebnahme der DirectAccess-Infrastruktur

Wenn Sie alle DirectAccess-Clients zu Always on VPN migriert haben, können Sie die DirectAccess-Infrastruktur außer Betrieb nehmen und die DirectAccess-Einstellungen aus Gruppenrichtlinie entfernen. Microsoft empfiehlt, die folgenden Schritte auszuführen, um DirectAccess ordnungsgemäß aus Ihrer Umgebung zu entfernen:

1. **Entfernen Sie die Konfigurationseinstellungen.** Entfernen Sie die Gruppenrichtlinien Objekte und die Remote Zugriffs-Gruppenrichtlinien Einstellungen Remote Zugriff, die durch Öffnen der Remote Zugriffs-Verwaltungskonsole erstellt wurden, und wählen Sie Konfigurationseinstellungen entfernen aus, wie in der folgenden Abbildung dargestellt. Wenn Sie die Gruppe entfernen, bevor Sie die Konfiguration entfernen, treten wahrscheinlich Fehler auf.

    ![Prozess zum Entfernen von DirectAccess aus Ihrer Umgebung](../../media/DA-to-AlwaysOnVPN/dbdc3d80e8dc1b8665f7b15d7d2ee1f6.png)

2. **Entfernen Sie Geräte aus der DirectAccess-Sicherheitsgruppe.** Wenn die Benutzer erfolgreich migriert werden, entfernen Sie Ihre Geräte aus der DirectAccess-Sicherheitsgruppe. Überprüfen Sie vor dem Entfernen von DirectAccess aus Ihrer Umgebung, ob die DirectAccess-Sicherheitsgruppe leer ist. Entfernen Sie die Sicherheitsgruppe nicht, wenn Sie noch Mitglieder enthält. Wenn Sie die Sicherheitsgruppe mit Mitgliedern entfernen, riskieren Sie, dass Mitarbeiter keinen Remote Zugriff von ihren Geräten aus haben. Verwenden Sie Microsoft Endpoint Configuration Manager oder Microsoft InTune, um Geräte Zuweisungs Informationen zu bestimmen und herauszufinden, welches Gerät zu den einzelnen Benutzern gehört.

3. **Bereinigen Sie DNS.** Stellen Sie sicher, dass Sie alle Datensätze von Ihrem internen DNS-Server und dem öffentlichen DNS-Server im Zusammenhang mit DirectAccess entfernen, z. b. da.contoso.com, DAGateway.contoso.com.

4. **Außerbetriebnahme des DirectAccess-Servers.** Wenn Sie die Konfigurationseinstellungen und DNS-Einträge erfolgreich entfernt haben, können Sie den DirectAccess-Server beenden. Entfernen Sie hierzu entweder die Rolle in Server-Manager, oder entfernen Sie den Server, und entfernen Sie ihn aus AD DS.

5. **Entfernen Sie alle DirectAccess-Zertifikate aus Active Directory Zertifikat Diensten.** Wenn Sie Computer Zertifikate für die DirectAccess-Implementierung verwendet haben, entfernen Sie die veröffentlichten Vorlagen aus dem Ordner Zertifikat Vorlagen in der Zertifizierungsstellen Konsole.

## <a name="next-step"></a>Nächster Schritt

Die Migration von DirectAccess zu Always on VPN ist abgeschlossen.
