---
title: Übersicht über Windows Admin Center
description: Informationen zum Verwalten von Windows Server mithilfe von Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 04/12/2019
ms.localizationpriority: high
ms.prod: windows-server-threshold
ms.openlocfilehash: 3208c20e8bf9f4cfab4340aa33b24175bbc72dda
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188331"
---
# <a name="windows-admin-center"></a>Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

**Windows Admin Center** (mit dem Codenamen **Projekt Honolulu**) wird eine Weiterentwicklung der Windows Server integrierte Verwaltungstools; es ist eine zentrale Konsole, die alle Aspekte der Verwaltung von lokalen Servern und Remoteservern konsolidiert. Als eine lokal bereitgestellte, Browser-basierte Management wünschen sind keine Verbindung mit dem Internet und Azure erforderlich. Windows Admin Center ermöglicht die vollständige Kontrolle über alle Aspekte der Bereitstellung, einschließlich privater Netzwerke, die nicht mit dem Internet verbunden sind.

## <a name="introduction"></a>Einführung

>[!VIDEO https://www.youtube.com/embed/PcQj6ZklmK0]

![Infografik zu Windows Admin Center](media/WAC1809Poster_thumb.PNG)

[PDF herunterladen](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1809Poster.pdf)

## <a name="quick-start"></a>Schnellstart

Sie können Windows Admin Center einrichten und von in Ihrer Umgebung in Minuten ausführen:

1. [Download](https://aka.ms/windowsadmincenter)
2. [Installieren](deploy/install.md)
3. [Erste Schritte](use/get-started.md)

## <a name="contents-at-a-glance"></a>Inhalt auf einen Blick

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Grundlegende Informationen</h3>
            <ul>
            <li><a href="understand/what-is.md">Was ist Windows Admin Center?</a>
            <li><a href="understand/faq.md">FAQ</a>
            <li><a href="understand/case-studies.md">Fallstudien</a>
            <li><a href="understand/related-management.md">Verwandte Produkte</a>
            <li><a href="understand/videos.md">Videos</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Planen</h3>
            <ul>
            <li><a href="plan/installation-options.md">Welche Art von Installation für Sie geeignet ist?</a>
            <li><a href="plan/user-access-options.md">User Access-Optionen</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Bereitstellen</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">Vorbereiten der Umgebung</a>
            <li><a href="deploy/install.md">Installieren Sie Windows Admin Center</a>
            <li><a href="deploy/high-availability.md">Hochverfügbarkeit aktivieren</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Konfigurieren</h3>
            <ul>
            <li><a href="configure/settings.md">Windows Admin Center-Einstellungen</a>
            <li><a href="configure/user-access-control.md">User Access Control und Berechtigungen</a>
            <li><a href="configure/using-extensions.md">Erweiterungen</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Verwendung</h3>
            <ul>
            <li><a href="use/get-started.md">Starten & Verbindungen hinzufügen</a>
            <li><a href="use/manage-servers.md">Verwalten von Servern</a>
            <li><a href="use/manage-hyper-converged.md">Verwalten von hyper-konvergiert-Infrastruktur</a>
            <li><a href="use/manage-failover-clusters.md">Verwalten von Failoverclustern</a>
            <li><a href="use/manage-virtual-machines.md">Verwalten von virtuellen Computern</a>
            <li><a href="use/logging.md">Protokollierung</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Verbinden mit Azure</h3>
            <ul>
            <li><a href="azure/index.md">Azure hybriddienste</a></li>
            <li><a href="azure/azure-integration.md">Verbinden von Windows Admin Center in Azure</a></li>
            <li><a href="azure/deploy-wac-in-azure.md">Bereitstellen von Windows Admin Center in Azure</a></li>
            <li><a href="azure/manage-azure-vms.md">Verwalten von Azure-VMs mit Windows Admin Center</a></li>
            </ul>
        </td>
    </tr>
    <tr>
            <td style="vertical-align: top;">
            <h3>Support</h3>
            <ul>
            <li><a href="support/index.md">Support-Richtlinie</a>
            <li><a href="support/troubleshooting.md">Allgemeine Schritte zur Problembehandlung</a>
            <li><a href="support/known-issues.md">Bekannte Probleme</a>
            </ul>
        </td>
            <td style="vertical-align: top;">
            <h3>Erweitern</h3>
            <ul>
            <li><a href="extend/extensibility-overview.md">Übersicht der Erweiterungen</a>
            <li><a href="extend/understand-extensions.md">Grundlegendes zu Erweiterungen</a>
            <li><a href="extend/developing-extensions.md">Entwickeln Sie eine Erweiterung</a>
            <li><a href="extend/publish-extensions.md">Anleitungen</a>
            <li><a href="extend/publish-extensions.md">Veröffentlichen von Erweiterungen</a>
            </ul>
        </td>
    </tr>

</table>

## <a name="release-history"></a>Revisionsverlauf

Lernen Sie unsere neuesten Funktionen kennen:

- Version [1904](https://aka.ms/wac1904) wird von die neueste GA-Version, die das Tool Azure Hybrid Services führt, und bietet Features, die zuvor in der Vorschau an den Kanal allgemein verfügbar waren.
- Version [1903](https://aka.ms/wac1903) bringt Sie e-Mail-Benachrichtigungen über Azure Monitor die Möglichkeit, Server oder PC-Verbindungen von Active Directory und neue Tools zum Verwalten von Active Directory, DHCP und DNS hinzuzufügen.
- Version [1902](https://aka.ms/wac1902) softwaredefinierten Netzwerk (SDN) Verwaltung, einschließlich neuer SDN-Tools zum Verwalten von ACLs, Gateway-Verbindungen und logische Netzwerke eine Liste der gemeinsam genutzte Verbindungen und Verbesserungen hinzugefügt.
- Version [1812](https://aka.ms/wac1812) enthält nun ein dunkles Design (in der Vorschau), Einstellungen zur Energiekonfiguration, BMC-Informationen und PowerShell-Unterstützung zum Verwalten von [Erweiterungen](./configure/using-extensions.md#manage-extensions-with-powershell) und [Verbindungen](./use/get-started.md#use-powershell-to-import-or-export-your-connections-with-tags).
- Version [1809.5](https://aka.ms/wac1809.5) ist ein kumulatives GA-Update, das verschiedene Qualitäts- und funktionale Verbesserungen sowie Fehlerkorrekturen in der gesamten Plattform und einige neue Features in der Verwaltungslösung für hyperkonvergente Infrastrukturen enthält.
- Version [1809](https://cloudblogs.microsoft.com/windowsserver/2018/09/20/windows-admin-center-1809-and-sdk-now-generally-available/) war eine GA-Version, die Features umfasst, die zuvor dem GA-Channel als Preview zur Verfügung standen.
- Version [1808](https://aka.ms/WACPreview1808-InsiderBlog) enthält nun das Tool Installierte Apps sowie viele „verdeckte“ Verbesserungen und wichtige Updates zum Preview-SDK.
- Version [1807](https://aka.ms/WACPreview1807-InsiderBlog) enthält nun eine optimierte Azure-Verbindung, Verbesserungen an der VM-Bestandsseite, Funktionen für die Dateifreigabe, eine Integration der Azure-Updateverwaltung und vieles mehr. 
- Version [1806](https://aka.ms/WACPreview1806-InsiderBlog) umfasst nun das Show PowerShell-Skript sowie SDN-Verwaltung, 2008 R2-Verbindungen, SDN, geplante Aufgaben und viele weitere Verbesserungen.
- Version 1804.25 - Wartungsupdate für Benutzer, die Windows Admin Center in vollständig offline installieren.
- Version [1804](https://cloudblogs.microsoft.com/windowsserver/2018/04/12/announcing-windows-admin-center-our-reimagined-management-experience/) - Projekt Honolulu wird Windows Admin Center und fügt Sicherheitsfeatures und rollenbasierte Zugriffssteuerung hinzu. Unsere erste GA-Version.
- Version [1803](https://blogs.windows.com/windowsexperience/2018/03/13/announcing-project-honolulu-technical-preview-1803-and-rsat-insider-preview-for-windows-10) Bietet zusätzliche Unterstützung für die Azure AD-Zugriffssteuerung, die ausführliche Protokollierung, verschiedene Inhalte und eine Reihe von Verbesserungs-Tools.
- Version [1802](https://blogs.windows.com/windowsexperience/2018/02/13/announcing-windows-server-insider-preview-build-17093-project-honolulu-technical-preview-1802) Bietet zusätzliche Unterstützung für Eingabehilfen, Lokalisierung, Bereitstellungen mit hoher Verfügbarkeit, Kategorien, Hyper-V-Host-Einstellungsdatei und Gateway-Authentifizierung.
- Version [1712](https://blogs.windows.com/windowsexperience/2017/12/19/announcing-project-honolulu-technical-preview-1712-build-05002) hat weitere Features für virtuelle Computer und Leistungsverbesserungen in allen Tools.
- Version [1711](https://cloudblogs.microsoft.com/windowsserver/2017/12/01/1711-update-to-project-honolulu-technical-preview-is-now-available/) hat stark erwartete Tools (Remotedesktop und PowerShell) zusammen mit weiteren Verbesserungen.
- Version [1709](https://cloudblogs.microsoft.com/windowsserver/2017/09/22/project-honolulu-technical-preview-is-now-available-for-download/) ist unsere erste öffentliche Preview-Version.

## <a name="stay-updated"></a>Dem neusten Stand

![ ](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR)[Folgen Sie uns auf Twitter](https://twitter.com/servermgmt)

![ ](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw)[Lesen Sie unsere Blogs](https://blogs.technet.microsoft.com/servermanagement/)
