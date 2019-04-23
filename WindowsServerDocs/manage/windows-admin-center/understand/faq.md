---
title: Häufig gestellte Fragen zu Windows Admin Center
description: Antworten zum Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 39f862485cf938981aae37e352f3448998b7c9c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829571"
---
# <a name="windows-admin-center-frequently-asked-questions"></a>Häufig gestellte Fragen zu Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Hier erhalten Sie Antworten auf die am häufigsten gestellten Fragen zu Windows Admin Center.

## <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center?

Windows Admin Center ist eine leichte browserbasierte GUI-Plattform und Toolset für IT-Administratoren zum Verwalten von Windows Server und Windows 10. Es ist die Weiterentwicklung von vertrauten Verwaltungstools wie Server-Manager und Microsoft Management Console (MMC) in einer modernisierten, vereinfachten, integrierten und sicheren Umgebung.

## <a name="can-i-use-windows-admin-center-in-production-environments"></a>Kann ich Windows Admin Center in Produktionsumgebungen verwenden?

Ja. Windows Admin Center ist im Allgemeinen verfügbar und zur umfassenden Verwendung in Produktionsumgebungen geeignet. Als Plattform, die immer stärker und breiter wird, bedeutet das Verlassen der Vorschau, dass die Funktionen der aktuellen Plattform und die wichtigsten Tools der Microsoft Standardversion den Kriterien und unserer Qualität für Verwendbarkeit, Zuverlässigkeit, Leistung, Verfügbarkeit und Sicherheit entsprechen.

## <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Wie viel kostet Windows Admin Center?

Windows Admin Center ist ohne zusätzliche Kosten über Windows erhältlich. Sie können Windows Admin Center (als separater Download verfügbar) mit den gültigen Lizenzen für Windows Server oder Windows 10 ohne zusätzliche Kosten erhalten - es ist unter Windows als ergänzender EULA (ENDBENUTZER-LIZENZVERTRAG) lizenziert.

## <a name="what-versions-of-windows-server-can-i-manage-with-windows-admin-center"></a>Welche Versionen von Windows Server können mit Windows Admin Center verwaltet werden?

Windows Admin Center ist optimiert für Windows Server-2019 zu wichtigen Themen, in der Version von Windows Server-2019: Hybrid cloud-Szenarien und hyper-konvergiert infrastrukturverwaltung insbesondere. Obwohl Windows Admin Center am besten mit Windows Server-2019 funktionieren, unterstützt es das Verwalten einer Vielzahl von Versionen, die Kunden bereits verwenden: WindowsServer 2012 und höher werden vollständig unterstützt. Es gibt auch eingeschränkter Funktionalität für die Verwaltung von Windows Server 2008 R2.

## <a name="is-windows-admin-center-a-complete-replacement-for-all-traditional-in-box-and-rsat-tools"></a>Ist Windows Admin Center ein vollständiger Ersatz für alle integrierten und RSAT-Tools?

Nein. Obwohl viele Standardszenarien von Windows Admin Center verwaltet werden können, tauscht es nicht vollständig alle herkömmliche Tools von Microsoft Management Console (MMC) aus. Für eine ausführliche Betrachtung darüber, welche Tools in Windows Admin Center, enthalten sind, erfahren Sie mehr über [serververwaltung](..\use\manage-servers.md) in unserer Dokumentation. Windows Admin Center hat die folgenden wichtigsten Funktionen in der Server-Manager-Lösung:

* Anzeigen von Ressourcen und Ressourcenverwendung
* Zertifikatverwaltung
* Verwalten von Geräten
* Ereignisanzeige
* Datei-Explorer
* Verwalten der Firewall
* Verwalten installierter Apps
* Konfigurieren von lokalen Benutzern und Gruppen
* Netzwerkeinstellungen
* Anzeigen und Beenden von Prozessen und erstellen von Prozesssicherungen
* Bearbeiten der Registrierung
* Verwaltung geplanter Aufgaben
* Verwalten von Windows-Diensten
* Aktivieren/Deaktivieren von Rollen und Features
* Verwalten von Hyper-V VMs und virtuelle Switches
* Verwalten von Speicher
* Verwalten von Funktion "Speicherreplikat"
* Verwalten von Windows Updates
* PowerShell-Konsole
* Remotedesktopverbindung

Windows Admin Center bietet auch diese Lösungen:

* Computermanagement – bietet eine Teilmenge der Server-Manager-Features zum Verwalten von Windows 10-Client-PCs
* Failovercluster-Manager – bietet Unterstützung für die laufende Verwaltung von Failovercluster und Cluster-Ressourcen
* Hyperkonvergente Cluster-Manager – bietet eine völlig neue Erfahrung, die speziell für Direkte Speicherplätze und Hyper-V gilt. Es bietet das Dashboard und betont Diagramme und Warnungen für die Überwachung.

Windows Admin Center ergänzt und ersetzt RSAT (Remote Server Administration Tools) nicht, da Rollen wie Active Directory, DNS, DHCP IIS noch nicht entsprechende Management-Funktionen im Windows Admin Center haben.

## <a name="can-windows-admin-center-be-used-to-manage-the-free-microsoft-hyper-v-server"></a>Kann Windows Admin Center zur Verwaltung der kostenlosen Microsoft Hyper-V Server werden?

Ja. Windows Admin Center kann zum Verwalten von Microsoft Hyper-V Server 2016 und Microsoft Hyper-V Server 2012 R2 verwendet werden.

## <a name="can-i-deploy-windows-admin-center-on-a-windows-10-computer"></a>Kann ich Windows Admin Center auf einem Windows 10 Computer bereitstellen?

Ja, Windows Admin Center kann auf Windows 10 (Version 1709 oder höher) installiert und im Desktopmodus ausgeführt werden.  Windows Admin Center kann auch sein, auf einem Server mit Windows Server 2016 oder höher im Gateway-Modus, und klicken Sie dann über einen Webbrowser auf einem Windows 10-Computer zugegriffen. [Erfahren Sie mehr über die Optionen für die Installation](..\plan\installation-options.md).

## <a name="ive-heard-that-windows-admin-center-uses-powershell-under-the-hood-can-i-see-the-actual-scripts-that-it-uses"></a>Ich habe gehört, dass Windows Admin Center mithilfe von PowerShell im Hintergrund, sehe ich, dass die tatsächliche Skripts, die sie verwendet?

Ja! die [Showscript Feature](..\use\get-started.md#view-powershell-scripts-used-in-windows-admin-center) wurde in Windows Admin Center Preview 1806 hinzugefügt und ist nun in der GA-Kanal enthalten.

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-windows-server-2008-r2-or-earlier"></a>Gibt es Pläne für Windows Admin Center zum Verwalten von Windows Server 2008 R2 oder einer früheren Version?

Unterstützt ab sofort Windows Admin Center **beschränkt** Funktionen zum Verwalten von Windows Server 2008 R2. Windows Admin Center nutzt die Funktionen von PowerShell, und Plattform-Technologien, die in Windows Server 2008 R2 und früheren Versionen nicht vorhanden sind, und diese werden daher nicht voll unterstützt. Windows Server 2008/2008 R2 nähern Ende des Supports Januar 2020, deshalb empfiehlt Microsoft Kunden [Umstieg auf Azure oder ein Upgrade auf die neueste Version von Windows Server](https://www.microsoft.com/en-us/cloud-platform/windows-server-2008).

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-linux-connections"></a>Gibt es Pläne für Windows Admin Center zum Verwalten von Linux-Verbindungen?

Wir werden untersuchen das Problem aufgrund der Kundennachfrage, jedoch ist derzeit nicht gesperrten geplant übermitteln, und Unterstützung bestehen nur eine Konsolenverbindung über SSH.

## <a name="which-web-browsers-are-supported-by-windows-admin-center"></a>Welche Webbrowser können von Windows Admin Center unterstützt werden?

Die aktuellen Versionen von Microsoft Edge (Windows 10, Version 1709 oder höher) und Browsern von Google Chrome werden getestet und auf Windows 10 unterstützt. [Browser anzeigen bestimmte bekannte Probleme](..\use\known-issues.md#browser-specific-issues). Andere moderne Browser oder anderen Plattformen werden derzeit nicht Teil unserer Testmatrix und sind daher nicht *offiziell* unterstützt.

## <a name="how-does-windows-admin-center-handle-security"></a>Wie behandelt Windows Admin Center Sicherheit?

Datenverkehr vom Browser an das Windows Admin Center-Gateway verwendet HTTPS. Datenverkehr vom Gateway auf verwaltete Server ist standardmäßig PowerShell und WMI über WinRM. Wir unterstützen LAPS (Local Administrator Password Solution), eingeschränkte ressourcenbasierte Delegierung, Gateway-Steuerung des Zugriffs über AD oder Azure AD und rollenbasierte Zugriffssteuerung für die Verwaltung von Zielservern.

## <a name="are-there-any-cloud-dependencies"></a>Gibt es Abhängigkeiten mit der Cloud?

Windows Admin Center erfordert keinen Zugriff auf das Internet oder Microsoft Azure. Windows Admin Center verwaltet Windows Server und Windows-Instanzen überall: auf physischen Systemen oder virtuellen Computern auf einem beliebigen Hypervisor, oder in einer beliebigen Cloud. Obwohl die Integration mit unterschiedlichen Azure-Diensten mit der Zeit hinzugefügt werden, werden optionale Zusatzfunktionen verwendet Windows Admin Center ist nicht notwendig.

## <a name="are-there-any-other-dependencies-or-prerequisites"></a>Gibt es andere Abhängigkeiten oder erforderliche Komponenten?

Windows Admin Center kann auf Windows 10 Fall Anniversary Update (1709) oder höher, oder Windows Server 2016 oder höher installiert werden. Zum Verwalten von Windows Server 2008 R2, 2012 oder 2012 R2, ist die Installation von Windows Management Framework 5.1 auf diesen Servern erforderlich. Es gibt keine andere Abhängigkeiten. IIS ist nicht erforderlich, Agents sind nicht erforderlich, SQL Server ist nicht erforderlich.

## <a name="what-about-extensibility-and-3rd-party-support"></a>Was geschieht mit Erweiterbarkeit und Drittanbieter-Unterstützung?

Windows Admin Center ist eine SDK zur Verfügung, damit alle Benutzer ihre eigenen Erweiterung schreiben kann. Als Plattform war unser Ökosystemwachstum und die Partner-Erweiterbarkeit eine der wichtigsten Prioritäten. [Weitere Informationen zum Windows Admin Center SDK](..\extend\extensibility-overview.md).

## <a name="can-i-manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Kann ich Hyperkonvergente Infrastruktur mit Windows Admin Center verwalten?

Ja. Windows Admin Center unterstützt die Verwaltung der hyperkonvergenten Cluster unter Windows Server 2016 oder Windows Server-2019. Die hyperkonvergenten Cluster-Manager-Lösung in Windows Admin Center zuvor in der Vorschau war, ist nun jedoch **Allgemein verfügbaren**, einige neue Funktionen in der Vorschau. Lesen Sie [Weitere Informationen zum Verwalten der Hyperkonvergenten Infrastruktur](..\use\manage-hyper-converged.md).

## <a name="does-windows-admin-center-require-system-center"></a>Erfordert Windows Admin Center das System Center?

Nein. Windows Admin Center dient als Ergänzung zu System Center, System Center ist jedoch nicht erforderlich. [Weitere Informationen zu Windows Admin Center und System Center](related-management.md#system-center).

## <a name="can-windows-admin-center-replace-system-center-virtual-machine-manager-scvmm"></a>Kann Windows Admin Center den System Center Virtual Machine Manager (SCVMM) ersetzen?

Windows Admin Center und SCVMM ergänzen sich. Windows Admin Center ersetzt die herkömmliche Microsoft Management Console (MMC) Snap-Ins und die Server-Administratorerfahrung.  Windows Admin Center kann nicht die Überwachungsaspekte von SCVMM ersetzen. [Weitere Informationen zu Windows Admin Center und System Center](related-management.md#system-center).

## <a name="what-is-windows-admin-center-preview-which-version-is-right-for-me"></a>Was ist Windows Admin Center - Vorschau, welche Version ist für mich geeignet?

Es stehen zwei Versionen von Windows Admin Center zum Download zur Verfügung:

### <a name="windows-admin-center"></a>Windows Admin Center

* Für IT-Administratoren, die nicht häufig aktualisieren können oder die mehr Validierungszeit für die Versionen, die sie in der Produktion verwenden benötigen. Unsere aktuelle Version der allgemein verfügbar (GA) ist Windows Admin Center 1809.5.
* Laden Sie die neueste GA-Version [hier herunter](https://aka.ms/WACDownload).

* Windows Admin Center GA-Versionen werden unterstützt kontinuierlich basierend auf von Microsoft [Modern Lifecycle-Richtlinie](https://support.microsoft.com/help/30881/modern-lifecycle-policy). Dies bedeutet, dass nur die neueste veröffentlichte Version von Windows Admin Center bei allgemeiner Verfügbarkeit unterstützt, verarbeitet und müssen der Benutzer "auf dem Laufenden bleiben" durch ein Upgrade auf die neueste Version von Windows Admin Center bei allgemeiner Verfügbarkeit innerhalb von 30 Tagen der Verfügbarkeit bleibt unterstützt. Diese Richtlinie gilt für sowohl die Windows Admin Center-Plattform selbst sowie alle Microsoft-Erweiterungen sind allgemein verfügbar und in der Windows Admin Center-Erweiterung feed veröffentlicht. Beachten Sie, dass einige Erweiterungen häufiger als andere, zwischen Windows Admin Center GA-Versionen aktualisiert werden können.

### <a name="windows-admin-center-preview"></a>Windows Admin Center – Vorschau

* Für IT-Administratoren, die die neuesten und interessantesten Features auf einer regulären Trittfrequenz verwenden möchten. Unser Ziel ist es, geben nachfolgende Aktualisierung Versionen jeden Monat oder so. Die Kern-Plattform ist weiterhin einsatzbereit, und die Lizenz enthält Produktionsnutzungsrechte. Die Einführung der neuen Tools und Funktionen, die als Vorschau deutlich markiert sind, eignen sich für die Bewertung und zum Testen.
* Wenn Sie die neueste Vorabversion erhalten möchten, können registrierte Insider Windows Admin Center - Vorschau direkt aus der [Windows Server Insider Preview herunterladen Seite](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)unter der Dropdownliste zusätzliche Downloads herunterladen. Wenn Sie noch nicht als Insider registriert sind, lesen Sie [Erste Schritte mit Windows Server](https://insider.windows.com/en-us/for-business-getting-started-server/) auf dem Windows-Insider für Unternehmen-Portal.

## <a name="why-was-windows-admin-center-chosen-as-the-final-name-for-project-honolulu"></a>Warum wurde "Windows Admin Center" als der endgültige Name für "Projekt Honolulu" ausgewählt?

Windows Admin Center ist der offizielle Produktname für "Projekt Honolulu" und verstärkt unserer Vision für IT-Administratoren mit einer integrierten Lösung und einer Vielzahl administrativer Verwaltungskerne und -Szenarien. Es zeigt auch unseren zentralen Fokus für IT Admin Benutzer und bietet eine optimale Kundenorientierung.

## <a name="where-can-i-learn-more-about-windows-admin-center-or-get-more-details-on-the-topics-above"></a>Wo erfahren Sie mehr über Windows Admin Center oder erhalten weitere Informationen zu den oben aufgeführten Themen?

Unsere [Startseite](https://aka.ms/WindowsAdminCenter) ist der beste Ausgangspunkt und verfügt über Links zu unserer Dokumentation und dem neu kategorisierten Inhalt, Downloadadressen, der Bereitstellung von Feedback, Referenzinformationen und andere Ressourcen.

## <a name="what-is-the-version-history-of-windows-admin-center"></a>Was ist die Versionsgeschichte des Windows Admin Center?

[Zeigen Sie hier den Versionsverlauf.](..\overview.md#release-history)

## <a name="im-having-an-issue-with-windows-admin-center-where-can-i-get-help"></a>Ich habe ein Problem mit Windows Admin Center, wo erhalte ich Hilfe?

Lesen Sie unser [Handbuch zur Problembehandlung](..\use\troubleshooting.md) und unsere Liste der [bekannten Probleme](..\use\known-issues.md).
