---
title: Übersicht über die Windows Server Hybrid Cloud drucken
description: Drucken Sie Hybrid Cloud ermöglicht IT-Experten zur Unterstützung von print-Anforderungen für BYOD oder eine Domäne eingebundenen Geräten.
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: store
ms.technology: server-general
author: TrudyHa
ms.author: TrudyHa
ms.date: 10/16/2017
ms.openlocfilehash: faa9fde857a9a4ee3f7c03f682b3dbced0340417
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878831"
---
# <a name="windows-server-hybrid-cloud-print-overview"></a>Übersicht über die Windows Server Hybrid Cloud drucken

**Gilt für**
-   Windows Server 2016

## <a name="what-is-hybrid-cloud-print"></a>Was ist Hybrid Cloud drucken?
**Hybrid Cloud Drucken** steht ein neues Feature für Windows Server 2016 über **Features bei Bedarf**. Es ermöglicht IT-Experten zur Unterstützung von print-Anforderungen für Personen, die ihre eigenen Geräte mitbringen, oder verwenden Sie die Geräte, die mit Ihrem Azure Active Directory verknüpft. Dies schließt mobiler Geräte wie Windows Phone, Laptops oder Tablets unter Windows 10 oder Windows Mobile. Es bietet Unterstützung für den Druck von überall aus Personen, die Zugriff auf das Internet haben.

Für IT-Administratoren **Hybrid Cloud Drucken** bietet sicheren Benutzerzugriffs auf einem lokalen Drucker mithilfe des Azure Multi-Factor Authentication auf die um Benutzerzugriff zu überprüfen. Einmaliges Anmelden (SSO) Funktionalität vereinfacht die benutzerfreundlichkeit. **Hybrid Cloud Drucken** basiert auf Windows **Druckserver** Rolle, sodass IT-Experten eine Erfahrung, die zum Verwalten von Druckern und Sicherheit für den Benutzerzugriff ähnlich ist.

**Hybrid Cloud Drucken** können von Personen in Ihrer Organisation so drucken Sie sie verwenden, um ihre Arbeit - abgeschlossen wird, selbst wenn sie von ihren Helpdesk oder den Arbeitsplatz sind von den Geräten.

**Hybrid Cloud Drucken** in Windows 10 Creators Update und Windows 10 s unterstützt
 
## <a name="feature-summary"></a>Zusammenfassung der Funktionen
**Hybrid Cloud Drucken** besteht aus zwei Hauptkomponenten: serverseitige: **Ermittlung** -Dienst und **Windows Print** Service.
- **Ermittlung** Dienstendpunkt auf eine IIS-Dienst unterstützen Mopria-Alliance-Branchenstandard für die Ermittlung der Drucker in der Cloud ausgeführt wird.
- **Windows-Druckserver** Dienstendpunkt einen IIS-Dienst, der Unterstützung der Branche unter standard Internet Printing Protokoll (IPP) um sicherzustellen, dass das breiteste Clientbetriebssystem unterstützt.

## <a name="deployment"></a>Bereitstellung
**Hybrid Cloud Drucken** unterstützt eine Reihe von verschiedenen Bereitstellungsoptionen, je nachdem, in denen Benutzerauthentifizierung in der Organisation erforderlich ist. Hier ist eine Bereitstellung könnte folgendermaßen aussehen:

![Das Diagramm zeigt eine grafische Darstellung der Hybrid Cloud-Print-Lösung](../media/hybrid-cloud-print/wshcp-deployment-options.png)

*Diagramm der Hybrid Cloud-Print-Lösung*

Das Diagramm zeigt:
- **Hybrid Cloud Drucken** mit Azure Active Directory als benutzeridentitätsanbieter. 
- **Windows-Druckserver** Service und **Ermittlung** Dienstendpunkte mit Azure Active Directory zur Aktivierung des Client-Geräts, zum Abrufen der erforderlichen Authentifizierung Benutzertoken für diese Dienste verwenden registriert sind. 
- Eine MDM-Dienst, z. B. **Microsoft Intune**, stellt der Client-Gerät mit den Richtlinien, die Azure Active Directory zum Herstellen einer Verbindung erforderlich **Windows Print** Service und **Ermittlung**Service.

Diese Tabelle enthält weitere Informationen für die Elemente im Diagramm.  

| Element | Beschreibung |
| ------- | ----------- |
| Azure Active Directory  | Bietet und steuert die Benutzerfunktionalität für Identität und Autorisierung |
| Active Directory        | Bietet und steuert die Benutzerfunktionalität für Identität und Autorisierung |
| Azure AD Connect  | Benutzeranmeldeinformationen zwischen Azure AD synchronisiert, und klicken Sie mit der lokalen AD. |
| MDM-Dienst (Intune) | Bietet, dass die Richtlinie Bereitstellung Gerätefunktionen um sicherzustellen, dass Client-Gerät (BYOD-Gerät) mit den Unternehmensrichtlinien entspricht. |
| Azure AD Proxy | Stellt eine langlebige Verbindung, die hinter der Firewall in Azure zu bestimmten konfigurierte Anwendung-Datenverkehr über das Internet mit dem Unternehmensnetzwerk verbunden hergestellt wird. |
| Azure-Web-App | Der Kern der Hybrid Cloud-Print-Lösung. Enthält die erforderlichen Endpunkte zum Ermitteln von Druckern und Druckinhalte für nicht in die Domäne eingebundene Geräte zu senden. |
| BYOD-Gerät / Windows Server-Druckspooler / Drucker | Hierbei handelt es sich als-ist. Keine Änderung an der Funktionalität in der Bereitstellung. |

Es gibt zwei Möglichkeiten zum Installieren von **Hybrid Cloud Drucken**:
- **Features bei Bedarf** -finden Sie unter [Configure Features on Demand in Windows Server](https://docs.microsoft.com/windows-server/administration/server-manager/configure-features-on-demand-in-windows-server) Weitere Informationen zum Hinzufügen und Entfernen von Rollen und featuredateien. 
- **Einstellungen für Windows Server 2016** -Administratoren können, wechseln Sie zu **Einstellungen** -> **Apps** -> **optionale Features verwalten**  ->  **Hinzufügen einer Funktion** und suchen Sie nach der Features bei Bedarf Paket 
- PowerShell-Befehle – In einer PowerShell-Administratorfenster, führen Sie folgende Befehle:

```PowerShell
    Install-Module -Name PublishCloudPrinter
    Import-Module PublishCloudPrinter
    ```
