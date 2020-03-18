---
title: Übersicht zu Windows Admin Center
description: Informationen zum Verwalten von Windows Server mithilfe von Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 01/07/2020
ms.localizationpriority: high
ms.prod: windows-server
ms.openlocfilehash: bb2f6d7fcbf18ef9bc67534982d1a98fdc5172a1
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79320034"
---
# <a name="windows-admin-center"></a>Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Windows Admin Center ist eine lokal bereitgestellte, browserbasierte App zum Verwalten von Windows-Servern, Clustern, hyperkonvergenter Infrastruktur und Windows 10-PCs. Sie ist ohne über Windows hinausgehende Kosten erhältlich und für den Einsatz in Produktionsumgebungen bereit.

Weitere Informationen zu den Neuerungen finden Sie unter [Versionsverlauf](support/release-history.md).

## <a name="download-now"></a>Jetzt herunterladen

**Laden Sie [Windows Admin Center](https://www.microsoft.com/evalcenter/evaluate-windows-admin-center) aus dem Microsoft Evaluation Center herunter**. Obwohl dort steht „Bewertung beginnen“, handelt es sich um die allgemein verfügbare Version für den Einsatz in der Produktion, die als Teil Ihrer Windows- oder Windows Server-Lizenz enthalten ist.

Hilfe zur Installation finden Sie unter [Installieren](deploy/install.md). Tipps zu den ersten Schritten mit dem Windows Admin Center finden Sie unter [Erste Schritte](use/get-started.md).

Nicht als Vorschau bereitgestellte Versionen von Windows Admin Center können mithilfe von Microsoft Update oder durch manuelles Herunterladen und Installieren von Windows Admin Center aktualisiert werden. Für jede nicht als Vorschauversion bereitgestellte Version von Windows Admin Center wird nach der Veröffentlichung der nächsten nicht als Vorschau bereitgestellten Version 30 Tage lang Support geleistet. Weitere Informationen finden Sie in unserer [Supportrichtlinie](support/index.md).

## <a name="windows-admin-center-scenarios"></a>Windows Admin Center-Szenarien

Für die folgenden Aufgaben können Sie das Windows Admin Center verwenden:

|     |     |
| --- | --- |
| ![](media/simple-icon.png)| **Vereinfachen der Serververwaltung** <br/> Verwalten Sie Ihre Server und Cluster mit modernisierten Versionen vertrauter Tools wie Server-Manager. Sie können die Installation in weniger als 5 Minuten ausführen und sofort mit der Verwaltung beginnen, es ist keine zusätzliche Konfiguration erforderlich. Weitere Informationen finden Sie unter [Was ist Windows Admin Center?](understand/what-is.md) |
| ![](media/future-icon.png)| **Arbeiten mit Hybridlösungen** <br/> Die Integration in Azure unterstützt Sie beim optionalen Verbinden ihrer lokalen Server mit relevanten Clouddiensten. Weitere Informationen finden Sie unter [Azure-Hybriddienste](azure/index.md). |
| ![](media/secure-icon.png)| **Optimieren der hyperkonvergenten Verwaltung** <br/> Optimieren Sie die Verwaltung von Azure Stack HCI oder hyperkonvergenten Windows Server-Clustern. Verwenden Sie vereinfachte Workloads, um virtuelle Computer, Volumes mit „Direkte Speicherplätze“, Software-Defined Networking und mehr zu erstellen und zu verwalten. Weitere Informationen finden Sie unter [Verwalten hyperkonvergenter Infrastruktur mit Windows Admin Center](use/manage-hyper-converged.md).|

Hier finden Sie ein Video, das Ihnen eine Übersicht bietet, gefolgt von einem Poster, das weitere Informationen enthält:
>[!VIDEO https://www.youtube.com/embed/WCWxAp27ERk]

[![Windows Admin Center – Poster](media/WAC1910Poster_thumb_small.PNG)](media/WAC1910Poster_thumb.png)

[PDF herunterladen](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1910Poster.pdf)


## <a name="contents-at-a-glance"></a>Inhalt auf einen Blick

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Grundlegende Informationen</h3>
            <ul>
            <li><a href="understand/what-is.md">Was ist Windows Admin Center?</a>
            <li><a href="understand/faq.md">Häufig gestellte Fragen</a>
            <li><a href="understand/case-studies.md">Fallstudien</a>
            <li><a href="understand/related-management.md">Verwandte Verwaltungsprodukte</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Planen</h3>
            <ul>
            <li><a href="plan/installation-options.md">Welche Art von Installation ist für Sie geeignet?</a>
            <li><a href="plan/user-access-options.md">Zugriffsoptionen für Benutzer</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Bereitstellen</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">Vorbereiten der Umgebung</a>
            <li><a href="deploy/install.md">Installieren von Windows Admin Center</a>
            <li><a href="deploy/high-availability.md">Hohe Verfügbarkeit aktivieren</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Konfigurieren</h3>
            <ul>
            <li><a href="configure/settings.md">Windows Admin Center – Einstellungen</a>
            <li><a href="configure/user-access-control.md">Steuerung des Benutzerzugriffs und der Berechtigungen</a>
            <li><a href="configure/shared-connections.md">Gemeinsam genutzte Verbindungen</a>
            <li><a href="configure/using-extensions.md">Erweiterungen</a>
            <li><a href="configure/use-powershell.md">Automatisieren mit PowerShell</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Verwendung</h3>
            <ul>
            <li><a href="use/get-started.md">Starten und Hinzufügen von Verbindungen</a>
            <li><a href="use/manage-servers.md">Verwalten von Servern</a>
            <li><a href="use/deploy-hyperconverged-infrastructure.md">Bereitstellen einer hyperkonvergenten Infrastruktur</a>
            <li><a href="use/manage-hyper-converged.md">Verwalten der hyperkonvergenten Infrastruktur</a>
            <li><a href="use/manage-failover-clusters.md">Verwalten von Failoverclustern</a>
            <li><a href="use/manage-virtual-machines.md">Verwalten von virtuellen Computern</a>
            <li><a href="use/logging.md">Protokollierung</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Herstellen einer Verbindung mit Azure</h3>
            <ul>
            <li><a href="azure/index.md">Azure-Hybriddienste</a></li>
            <li><a href="azure/azure-integration.md">Verbinden von Windows Admin Center mit Azure</a></li>
            <li><a href="azure/deploy-wac-in-azure.md">Bereitstellen von Windows Admin Center in Azure</a></li>
            <li><a href="azure/manage-azure-vms.md">Verwalten von Azure-VMs mit Windows Admin Center</a></li>
            </ul>
        </td>
    </tr>
    <tr>
            <td style="vertical-align: top;">
            <h3>Support</h3>
            <ul>
            <li><a href="support/release-history.md">Releaseverlauf</a>
            <li><a href="support/index.md">Supportrichtlinie</a>
            <li><a href="support/troubleshooting.md">Allgemeine Schritte zur Problembehandlung</a>
            <li><a href="support/known-issues.md">Bekannte Probleme</a>
            </ul>
        </td>
            <td style="vertical-align: top;">
            <h3>Erweitern</h3>
            <ul>
            <li><a href="extend/extensibility-overview.md">Übersicht der Erweiterungen</a>
            <li><a href="extend/understand-extensions.md">Grundlegendes zu Erweiterungen</a>
            <li><a href="extend/developing-extensions.md">Entwickeln einer Erweiterung</a>
            <li><a href="extend/publish-extensions.md">Handbücher</a>
            <li><a href="extend/publish-extensions.md">Veröffentlichen von Erweiterungen</a>
            </ul>
        </td>
    </tr>

</table>

## <a name="video-based-learning"></a>Videobasiertes Lernen

Hier finden Sie einige Videos von Microsoft Ignite 2019-Sitzungen:

- [Windows Admin Center: Unlock Azure Hybrid value](https://aka.ms/WAC-BRK3165) (Windows Admin Center: Nutzen des Azure Hybrid-Mehrwerts)
- [Windows Admin Center: What’s new and what’s next](https://aka.ms/WAC-BRK2048) (Windows Admin Center: Was ist neu und wie geht's weiter?)
- [Automatically monitor, secure and update your on-premises servers from Azure with Windows Admin Center](https://aka.ms/WAC-THR2146)(Automatisches Überwachen, Sichern und Aktualisieren Ihrer lokalen Server von Azure über Windows Admin Center)
- [Get more done with Windows Admin Center third-party extensions](https://aka.ms/WAC-THR2140) (Mehr Erledigen mit Windows Admin Center-Erweiterungen von Drittanbietern)
- [Be a Windows Admin Center expert: Best practices for deployment, configuration, and security](https://aka.ms/WAC-THR2135) (Werden Sie ein Windows Admin Center-Experte: Bewährte Methoden für Bereitstellung, Konfiguration und Sicherheit)
- [Windows Admin Center: Better together with System Center and Microsoft Azure](https://aka.ms/WAC-THR2176) (Windows Admin Center: Bessere Zusammenarbeit mit System Center und Microsoft Azure)
- [How to use Microsoft Azure hybrid services together with Windows Admin Center and Windows Server](https://aka.ms/WAC-THR2073) (Verwenden von Microsoft Azure-Hybriddiensten zusammen mit Windows Admin Center und Windows Server)
- [Live Q&A: Manage your hybrid server environment with Windows Admin Center](https://aka.ms/WAC-MLS1055) (Live-F&A: Verwalten Ihrer hybriden Serverumgebung mit Windows Admin Center)
- [Learning Path: Hybrid management technologies](https://aka.ms/WAC-HybridMgmtTech) (Lernpfad: Hybridverwaltungstechnologien)
- [Hands on Lab: Windows Admin Center and Hybrid](https://aka.ms/WAC-HOL2019) (Praktische Übungseinheit: Windows Admin Center und Hybridlösungen)

Im folgenden finden Sie einige Videos von Windows Server Summit 2019-Sitzungen:

- [Go hybrid with Windows Admin Center](https://aka.ms/WAC-WSS2019-GoHybridWAC) (Umstellen auf eine hybride Umgebung mit Windows Admin Center)
- [What's new with Windows Admin Center v1904](https://aka.ms/WAC-WSS2019-WhatsNewv1904) (Neuerungen in Windows Admin Center v1904)

Und hier finden Sie einige zusätzliche Ressourcen:

- [Windows Admin Center server management reimagined](https://aka.ms/WAC-ServerMgmtReimagined) (Die Serververwaltung von Windows Admin Center wurde neu gestaltet)
- [Manage Servers and Virtual Machines Anywhere with Windows Admin Center](https://aka.ms/WAC-Webinar2019) (Verwalten von Servern und virtuellen Computern an jedem Ort mit Windows Admin Center)
- [How to get started with Windows Admin Center](https://www.youtube.com/embed/PcQj6ZklmK0) (Erste Schritte mit Windows Admin Center)

## <a name="see-how-customers-are-benefitting-from-windows-admin-center"></a>Erfahren Sie, wie Kunden von Windows Admin Center profitieren

|     |
| --- |
| „[Windows Admin Center] hat unseren Aufwand bei der Verwaltung des Management Systems um mehr als 75 % verringert.“<br> *Rand Morimoto, President, Convergent Computing* |
| „Dank [Windows Admin Center] können wir unsere Kunden problemlos remote über das HTML5-Portal verwalten, und aufgrund der vollständigen Integration von Azure Active Directory sind wir in der Lage, die Sicherheit mit mehrstufiger Authentifizierung zu erhöhen.“<br/> *Silvio Di Benedetto, Gründer und Chefberater, Inside Technologies* |
| „Wir konnten [Server Core] SKUs auf effektivere Weise bereitstellen, die Ressourceneffizienz, Sicherheit und Automatisierung verbessern, trotzdem ein hohes Maß an Produktivität erzielen und Fehler reduzieren, die auftreten können, wenn ausschließlich Skripts eingesetzt werden.“ <br/> *Guglielmo Mengora, Gründer und CEO, VaiSulWeb* |
| „Mit [Windows Admin Center] steht vor allem im SMB-Markt Kunden jetzt ein einfach zu verwendendes Tool zum Verwalten ihrer internen Infrastruktur zur Verfügung. Dadurch wird der Verwaltungsaufwand minimiert und viel Zeit gespart. Und das Beste: Es fallen keine zusätzlichen Lizenzgebühren für [Windows Admin Center] an!“ <br/> *Helmut Otto, Hauptgeschäftsführer, SecureGUARD* |

[Erfahren Sie mehr über Unternehmen, die Windows Admin Center in ihrer Produktionsumgebung verwenden.](understand/case-studies.md)

## <a name="related-products"></a>Verwandte Produkte

Windows Admin Center dient zum Verwalten von einzelnen Servern oder Clustern. Es ergänzt vorhandene Überwachungs- und Verwaltungslösungen von Microsoft, wie z.B. Remoteserver-Verwaltungstools (RSAT), System Center, Intune oder Azure Stack, ersetzt diese jedoch nicht.

[Hier erfahren Sie, wie Windows Admin Center andere Microsoft-Management-Lösungen ergänzt.](understand/related-management.md)

## <a name="stay-updated"></a>Bleiben Sie auf dem Laufenden

![](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR)[Folgen Sie uns auf Twitter](https://twitter.com/servermgmt)

![](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw)[Lesen Sie unsere Blogs](https://blogs.technet.microsoft.com/servermanagement/)
