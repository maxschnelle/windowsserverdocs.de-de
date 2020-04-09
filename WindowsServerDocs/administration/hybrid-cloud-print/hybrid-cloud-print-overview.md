---
title: Übersicht über Windows Server Hybrid Cloud Print
description: Hybrid Cloud Print ermöglicht IT-Experten die Unterstützung von Druckanforderungen für BYOD-oder in die Domäne eingebundener Geräte
ms.prod: windows-server
ms.technology: server-general
author: trudyha
ms.author: trudyha
ms.date: 10/16/2017
ms.openlocfilehash: f448e8709f9e73165ba1a477c59567fcff4a2008
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852003"
---
# <a name="windows-server-hybrid-cloud-print-overview"></a>Übersicht über Windows Server Hybrid Cloud Print

**Gilt für:**
-   Windows Server 2016

## <a name="what-is-hybrid-cloud-print"></a>Was ist Hybrid Cloud Print?
**Hybrid Cloud Print** ist ein neues Feature für Windows Server 2016, das über **Features bei Bedarf**verfügbar ist. Dadurch können IT-Experten Druckanforderungen für Personen unterstützen, die ihre eigenen Geräte verwenden, oder Geräte verwenden, die mit Ihrem Azure Active Directory verknüpft sind. Dies umfasst auch mobile Geräte wie Windows Phone, Laptops oder Tablets, auf denen Windows 10 oder Windows Mobile ausgeführt wird. Es bietet Druckunterstützung von allen Personen, die Zugriff auf das Internet haben.

Für IT-Administratoren bietet **Hybrid Cloud Print** sicheren Benutzer Zugriff auf lokale Drucker mithilfe der Multi-Factor Authentication von Azure, um den Benutzer Zugriff zu überprüfen. Die Funktion für einmaliges Anmelden (Single Sign-on, SSO) vereinfacht die Benutzer Funktionalität. **Hybrid Cloud Print** basiert auf der Windows- **Druck Server** Rolle und bietet IT-Experten eine ähnliche Darstellung wie die Verwaltung von Druckern und Benutzer Zugriffssicherheit.

**Hybrid Cloud Print** ermöglicht es Personen in Ihrer Organisation, von den Geräten, die Sie zum Abschluss ihrer Arbeit verwenden, zu drucken, auch wenn Sie nicht von Ihrem Desk oder Workplace entfernt sind.

**Hybrid Cloud Print** wird in Windows 10 Creators Update und Windows 10 S unterstützt.
 
## <a name="feature-summary"></a>Funktions Zusammenfassung
**Hybrid Cloud Print** besteht aus zwei Hauptserver seitigen **Komponenten: Ermittlungs** Dienst und Windows- **Druck** Dienst.
- Ermittlungsdienst-Endpunkt, der unter einem IIS **-Dienst ausgeführt** wird, der einen mopria Alliance-Industriestandard für die Drucker Ermittlung in der Cloud
- Der **Windows-Druck** Dienst Endpunkt, der auf einem IIS-Dienst ausgeführt wird, der das branchenübliche Internet Druck Protokoll (IPP) unterstützt.

## <a name="deployment"></a>Bereitstellung
**Hybrid Cloud Print** unterstützt verschiedene Bereitstellungs Optionen, je nachdem, wo Ihre Organisation eine Benutzerauthentifizierung erfordert. Eine Bereitstellung könnte wie folgt aussehen:

![Ein Diagramm, das eine grafische Darstellung der Hybrid Cloud-Drucklösung anzeigt](../media/hybrid-cloud-print/wshcp-deployment-options.png)

*Hybrid Cloud Print-Lösungs Diagramm*

Das Diagramm zeigt Folgendes:
- **Hybrid Cloud Print** using Azure Active Directory als Benutzer Identitäts Anbieter. 
- **Windows-Druck** Dienst **-** und Ermittlungsdienst Endpunkte werden bei Azure Active Directory registriert, damit das Client Gerät das für diese Dienste zu verwendende erforderliche Benutzer Authentifizierungs Token abrufen kann. 
- Ein MDM-Dienst, wie z. b. **Microsoft InTune**, stellt dem Client Gerät Richtlinien bereit, die für die Verbindung Azure Active Directory mit dem **Windows-Druck** **Dienst und** -Ermittlungsdienst

Diese Tabelle enthält weitere Informationen zu den Elementen im Diagramm.  

| Element | Beschreibung |
| ------- | ----------- |
| Azure Active Directory  | Bietet und steuert die Benutzeridentität und Autorisierungs Funktionalität |
| Active Directory        | Bietet und steuert die Benutzeridentität und Autorisierungs Funktionalität |
| Azure AD Connect  | Synchronisiert Benutzer Anmelde Informationen zwischen Azure AD und lokalem AD. |
| MDM-Dienst (InTune) | Bietet Funktionen zur Bereitstellung von Geräte Richtlinien, um sicherzustellen, dass das Client Gerät (BYOD-Gerät) den Unternehmensrichtlinien entspricht. |
| Azure AD Proxy | Bietet eine langlebige Verbindung, die von hinter Ihrer Firewall zu Azure hergestellt wird, damit bestimmter konfigurierter Anwendungs Datenverkehr aus dem Internet in das Unternehmensnetzwerk übertragen werden kann. |
| Azure-Web-App | Der Kern der Hybrid Cloud-Drucklösung. Stellt die erforderlichen Webendpunkte zum Ermitteln von Druckern und zum Senden von Druck Inhalten für Geräte bereit, die nicht der Domäne beigetreten sind. |
| BYOD-Gerät/Windows-Druck Server Spooler/Drucker | Diese sind unverändert. Keine Änderung der Funktionalität in der Bereitstellung. |

Es gibt zwei Möglichkeiten zum Installieren von **Hybrid Cloud Print**:
- \* * Features bei Bedarf. Weitere Informationen zum Hinzufügen und Entfernen von Rollen-und Featuredateien finden Sie unter [Konfigurieren von Features bei Bedarf in Windows Server](https://docs.microsoft.com/windows-server/administration/server-manager/configure-features-on-demand-in-windows-server) . 
- \* * Einstellungen für Windows Server 2016, die Administratoren zu **Einstellungen** -> **apps** -> **Verwalten optionaler Features** -> **Hinzufügen eines** Features und suchen nach dem Paket "Features bei Bedarf" 
- PowerShell-Befehle: führen Sie in einem PowerShell-Administrator Fenster die folgenden Befehle aus:

```PowerShell
    Install-Module -Name PublishCloudPrinter
    Import-Module PublishCloudPrinter
    ```
