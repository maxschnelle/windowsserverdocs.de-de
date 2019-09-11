---
title: Die wichtigsten Supportlösungen für Windows Server
description: Links zu Lösungen für Probleme mit Windows Server
ms.prod: windows-server-threshold
ms.service: na
manager: alant
ms.technology: server-general
ms.date: 03/16/2018
ms.topic: article
author: kaushika-msft
ms.author: elizapo
ms.openlocfilehash: 29dd518ce7634a1cf8b3b7a84d8c7a4388d6027f
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866983"
---
# <a name="top-support-solutions-for-windows-server-2016"></a>Die wichtigsten Supportlösungen für Windows Server 2016

Microsoft veröffentlicht regelmäßig Updates und Lösungen für Windows Server. Um sicherzustellen, dass Ihre Server zukünftige Updates einschließlich der Sicherheitsupdates erhalten können, ist es wichtig, sie auf dem neuesten Stand zu halten. Eine komplette Liste der veröffentlichten Updates finden Sie unter [Updateverlauf für Windows 10 und Windows Server 2016](https://support.microsoft.com/en-us/help/4000825/windows-10-windows-server-2016-update-history).

Hierbei handelt es sich um die wichtigsten Microsoft-Support-Lösungen für häufige Probleme mit Windows Server 2016. Die unten angegebenen Links enthalten Links zu KB-Artikel, Updates und Bibliotheksartikeln.

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

## <a name="solutions-for-installing-or-upgrading-windows-server"></a>Lösungen für die Installation oder das Upgrade von Windows Server

- [Auflösen von Windows 10-upgradefehlern: Technische Informationen für IT-Experten](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)
- [Wartungs Stapel Update für Windows 10, Version 1607 und Windows Server 2016: 8. August 2017](https://support.microsoft.com/en-US/help/4035631)
- [Kompatibilitäts Update für das Upgrade auf Windows 10, Version 1607 und Windows Server 2016: 3. August 2017](https://support.microsoft.com/en-US/help/4033524)
- [Ein direktes System Upgrade wird auf Windows-basierten Azure-VMS nicht unterstützt.](https://support.microsoft.com/en-US/help/4014997)
- [Upgrade-und Konvertierungsoptionen für Windows Server 2016](../get-started/supported-upgrade-paths.md)
- [Server Rollen Upgrade und Migrations Matrix für Windows Server 2016](../get-started/server-role-upgradeability-table.md)
- [Windows Server-Installation und-Upgrade](../get-started/installation-and-upgrade.md)
- [Versionshinweise: Wichtige Probleme in Windows Server 2016](../get-started/windows-server-2016-ga-release-notes.md)
- [Empfehlungen für die Umstellung auf Windows Server 2016](../get-started/recommendations-moving-to-server2016.md)

## <a name="solutions-for-volume-activation"></a>Lösungen zur Volumenaktivierung
- [Windows Server 2016-Aktivierung](../get-started/server-2016-activation.md)
- [Aktivierungsmethoden überprüfen und auswählen](https://technet.microsoft.com/library/jj134256(ws.11).aspx)
- [Aktivierungs Fehler Codes für die Volumen Aktivierung](https://technet.microsoft.com/library/dn502528.aspx)
- [Behandeln von Problemen mit dem Schlüssel Verwaltungsdienst (Key Management Service, KMS)](https://technet.microsoft.com/library/ee939272.aspx)
- [Problembehandlung bei Volumen Aktivierung](https://technet.microsoft.com/library/ff793439.aspx)
- [Aktivierungs Fehler Codes](https://technet.microsoft.com/library/ff793399.aspx)
- [Bei der Windows-Installation tritt möglicherweise ein Fehler auf: "der eingegebene Product Key entspricht keinem der für die Installation verfügbaren Windows-Images. Geben Sie eine andere Product Key "](https://support.microsoft.com/help/2796988/windows-8-or-windows-server-2012-installation-may-fail-with-error-mess)

## <a name="solutions-related-to-dcpromo-and-installing-domain-controllers"></a>Lösungen im Zusammenhang mit DCPromo und Installieren von Domänencontrollern
- [Active Directory-und Active Directory Domain Services Port Anforderungen](https://technet.microsoft.com/library/dd772723(v=ws.10).aspx)
- [Active Directory Firewallports – wir versuchen, dies einfach zu machen](http://blogs.msmvps.com/acefekay/2011/11/01/active-directory-firewall-ports-let-s-try-to-make-this-simple/)
- [Exchange Server-Unterstützung für Windows Server 2016](https://technet.microsoft.com/library/ff728623(v=exchg.150).aspx)
- [Verwenden von "Ntdsutil. exe" zum übertragen und übernehmen von FSMO-Rollen an einen Domänen](https://support.microsoft.com/kb/255504)
- [Behandeln von Problemen bei der Domänencontrollerbereitstellung](../identity/ad-ds/deploy/troubleshooting-domain-controller-deployment.md)
- [Problembehandlung bei Active Directory-Installations-Assistenten](https://msdn.microsoft.com/library/bb727058.aspx)
- [Bekannte Probleme beim Installieren und Entfernen von AD DS](https://technet.microsoft.com/library/cc754463(v=ws.10).aspx)

## <a name="solutions-for-active-directory-federation-services-ad-fs"></a>Lösungen für Active Directory-Verbunddienste (AD FS)
- [Konfigurieren der automatischen Registrierung von in die Domäne eingebundenen Windows-Geräten mit Azure Active Directory](/azure/active-directory/active-directory-conditional-access-automatic-device-registration-setup)
- [Einrichten der Ausstellung von Ansprüchen](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup#step-2-setup-issuance-of-claims)
- [Konfigurieren von AD FS zum Authentifizieren von Benutzern, die in LDAP-Verzeichnissen gespeichert sind](../identity/ad-fs/operations/configure-ad-fs-to-authenticate-users-stored-in-ldap-directories.md)
- [AD FS: Unterstützung der alternativen Hostnamenbindung für die Zertifikatauthentifizierung](../identity/ad-fs/operations/ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)
- [Schutz vor Kenn Wort Angriffen](https://blogs.technet.microsoft.com/tspring/2017/01/20/federated-to-microsoft-cloud-and-account-lockouts/)
- [Aktualisieren auf AD FS unter Windows Server 2016 unter Verwendung einer WID-Datenbank](../identity/ad-fs/deployment/upgrading-to-ad-fs-in-windows-server-2016.md)
- [Windows 10-Anmeldung – aktivieren der Geräte Authentifizierung mit AD FS](../identity/ad-fs/operations/configure-device-based-conditional-access-on-premises.md)
- [Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016](../identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap-2016.md)
- [Access Control Richtlinien in Windows Server 2016 AD FS](../identity/ad-fs/operations/access-control-policies-in-ad-fs.md)

## <a name="solutions-related-to-active-directory-replication"></a>Lösungen für die Active Directory-Replikation

- [Behandeln von Active Directory-Replikationsproblemen](../identity/ad-ds/manage/troubleshoot/troubleshooting-active-directory-replication-problems.md)
- [Active Directory-Replikationsstatusmonitor Tool aus dem Microsoft Download Center herunterladen](https://www.microsoft.com/en-in/download/details.aspx?id=30005)
- [E2E Beheben allgemeiner Active Directory Replikations Fehler](https://support.microsoft.com/kb/3108513)
- [Problembehandlung bei AD Replication Error 8606: Zum Erstellen eines Objekts wurden unzureichende Attribute angegeben.](https://support.microsoft.com/kb/2028495)
- [Ereignis-ID 2108 und Ereignis-ID 1084 treten während der eingehenden Replikation von Active Directory in Windows 2000 Server und Windows Server 2003 auf](https://support.microsoft.com/kb/837932)
- [Problembehandlung bei AD Replication Error 8451: Beim Replikations Vorgang ist ein Datenbankfehler aufgetreten.](https://support.microsoft.com/kb/2645996)
- [Problembehandlung bei AD Replication Error 1127: Beim Zugriff auf die Festplatte ist ein Datenträger Vorgang auch nach Wiederholungs versuchen fehlgeschlagen.](https://support.microsoft.com/kb/2025726)
- [Bereinigen von Server Metadaten](https://technet.microsoft.com/library/cc816907.aspx)