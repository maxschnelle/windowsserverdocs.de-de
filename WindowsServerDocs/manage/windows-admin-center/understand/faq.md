---
title: Häufig gestellte Fragen zu Windows Admin Center
description: Antworten zum Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.openlocfilehash: 53f34992b875730be80ba479f387095aebbc8132
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469561"
---
# <a name="windows-admin-center-frequently-asked-questions"></a>Häufig gestellte Fragen zu Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Hier erhalten Sie Antworten auf die am häufigsten gestellten Fragen zu Windows Admin Center.

## <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center?

Windows Admin Center ist eine schlanke, browserbasierte GUI-Plattform und ein Toolset für IT-Administratoren zum Verwalten von Windows Server und Windows 10. Es ist die Weiterentwicklung von vertrauten integrierten Verwaltungstools, wie Server-Manager und Microsoft Management Console (MMC), mit einer modernisierten, vereinfachten, integrierten und sicheren Benutzeroberfläche.

## <a name="can-i-use-windows-admin-center-in-production-environments"></a>Kann ich Windows Admin Center in Produktionsumgebungen verwenden?

Ja. Windows Admin Center ist allgemein verfügbar und zur umfassenden Verwendung in Produktionsumgebungen geeignet. Die aktuellen Plattformfunktionen und die Kerntools entsprechen den Standardkriterien von Microsoft für die Veröffentlichung und unserer Messlatte für Verwendbarkeit, Zuverlässigkeit, Leistung, Verfügbarkeit, Sicherheit und Akzeptanz.

[!INCLUDE [support-policy](../includes/support-policy.md)]

## <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Wie viel kostet die Verwendung von Windows Admin Center?

Für Windows Admin Center fallen jenseits der Kosten für Windows keine zusätzlichen Kosten an. Sie können Windows Admin Center (als separater Download verfügbar) mit den gültigen Lizenzen für Windows Server oder Windows 10 ohne zusätzliche Kosten verwenden – es ist unter einer ergänzenden Windows-EULA (ENDBENUTZER-LIZENZVERTRAG) lizenziert.

## <a name="what-versions-of-windows-server-can-i-manage-with-windows-admin-center"></a>Welche Versionen von Windows Server können mit Windows Admin Center verwaltet werden?

Windows Admin Center ist für Windows Server 2019 optimiert, um wichtige-Themen im Windows Server 2019-Release zu fördern: insbesondere hybride Cloudlösungen und die Verwaltung von hyperkonvergenter Infrastruktur. Zwar funktioniert Windows Admin Center optimal mit Windows Server 2019, es unterstützt jedoch auch eine Vielzahl von Versionen, die von Kunden bereits verwendet werden: Windows Server 2012 und höher werden vollständig unterstützt. Es besteht außerdem eingeschränkte Funktionalität für die Verwaltung von Windows Server 2008 R2.

## <a name="is-windows-admin-center-a-complete-replacement-for-all-traditional-in-box-and-rsat-tools"></a>Ist Windows Admin Center ein vollständiger Ersatz für alle herkömmlichen integrierten und RSAT-Tools?

Nein. Zwar kann Windows Admin Center viele gängige Szenarien verwalten, es ersetzt aber nicht alle herkömmlichen MMC-Tools (Microsoft Management Console) vollständig. Eine detaillierte Aufstellung der in Windows Admin Center enthaltenen Tools finden Sie unter [Serververwaltung](../use/manage-servers.md) in unserer Dokumentation. Windows Admin Center hat die folgenden wichtigsten Funktionen in der Server-Manager-Lösung:

* Anzeigen von Ressourcen und Ressourcenverwendung
* Zertifikatverwaltung
* Verwalten von Geräten
* Ereignisanzeige
* Datei-Explorer
* Verwalten der Firewall
* Verwalten installierter Apps
* Konfigurieren von lokalen Benutzern und Gruppen
* Netzwerkeinstellungen
* Anzeigen und Beenden von Prozessen und Erstellen von Prozesssicherungen
* Bearbeiten der Registrierung
* Verwalten von geplanten Aufgaben
* Verwalten von Windows-Diensten
* Aktivieren/Deaktivieren von Rollen und Features
* Verwalten von Hyper-V-VMs und virtuellen Switches
* Verwalten von Speicher
* Verwalten von Speicherreplikaten
* Verwalten von Windows Updates
* PowerShell-Konsole
* Remotedesktopverbindung

Windows Admin Center bietet außerdem diese Lösungen:

* Computerverwaltung: eine Teilmenge der Server-Manager-Features zum Verwalten von Windows 10-Client-PCs
* Failovercluster-Manager: Unterstützung für die laufende Verwaltung von Failoverclustern und Clusterressourcen
* Manager für hyperkonvergente Cluster: eine völlig neue Benutzeroberfläche, die für direkte Speicherplätze und Hyper-V maßgeschneidert ist. Sie konzentriert sich auf das Dashboard und legt den Schwerpunkt auf Diagramme und Benachrichtigungen zur Überwachung.

Windows Admin Center ergänzt RSAT (Remote Server Administration Tools), ersetzt sie aber nicht, da Rollen wie Active Directory, DHCP, DNS oder IIS noch nicht über gleichwertige Verwaltungsfunktionen im Windows Admin Center verfügen.

## <a name="can-windows-admin-center-be-used-to-manage-the-free-microsoft-hyper-v-server"></a>Kann Windows Admin Center zur Verwaltung des kostenlosen Microsoft Hyper-V Servers verwendet werden?

Ja. Windows Admin Center kann zum Verwalten von Microsoft Hyper-V Server 2016 und Microsoft Hyper-V Server 2012 R2 verwendet werden.

## <a name="can-i-deploy-windows-admin-center-on-a-windows-10-computer"></a>Kann ich Windows Admin Center auf einem Windows 10-Computer bereitstellen?

Ja, Windows Admin Center kann unter Windows 10 (Version 1709 oder höher) installiert und im Desktopmodus ausgeführt werden.  Windows Admin Center kann auch auf einem Server mit Windows Server 2016 oder höher im Gatewaymodus installiert werden, der Zugriff erfolgt dann über einen Webbrowser von einem Windows 10-Computer aus. [Weitere Informationen über Installationsoptionen](../plan/installation-options.md).

## <a name="ive-heard-that-windows-admin-center-uses-powershell-under-the-hood-can-i-see-the-actual-scripts-that-it-uses"></a>Ich habe gehört, dass Windows Admin Center hinter den Kulissen PowerShell verwendet – kann ich die eigentlichen Skripts sehen, die es verwendet?

Ja! Das [Showscript-Feature](../use/get-started.md#view-powershell-scripts-used-in-windows-admin-center) wurde in der Windows Admin Center-Vorschau 1806 hinzugefügt und ist nun im GA-Kanal enthalten.

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-windows-server-2008-r2-or-earlier"></a>Gibt es Pläne, Windows Admin Center zum Verwalten von Windows Server 2008 R2 oder früherer Versionen nutzbar zu machen?

Windows Admin Center unterstützt jetzt die Verwaltung von Windows Server 2008 R2 mit **eingeschränkter** Funktionalität. Windows Admin Center nutzt die Funktionen von PowerShell und Plattformtechnologien, die in Windows Server 2008 R2 und früheren Versionen nicht vorhanden sind, daher ist eine vollständige Unterstützung nicht realisierbar. Windows Server 2008/2008 R2 erreichen das Supportende im Januar 2020, daher empfiehlt Microsoft Kunden, [auf Azure umzusteigen oder ein Upgrade auf die aktuellste Version von Windows Server vorzunehmen](https://www.microsoft.com/en-us/cloud-platform/windows-server-2008).

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-linux-connections"></a>Bestehen Pläne, Windows Admin Center für die Verwaltung von Linux-Verbindungen einzusetzen?

Aufgrund der Nachfrage von Kundenseite untersuchen wir das, es gibt aber zurzeit keinen festen Zeitplan, und möglicherweise wird sich die Unterstützung auf eine Konsolenverbindung über SSH beschränken.

## <a name="which-web-browsers-are-supported-by-windows-admin-center"></a>Welche Webbrowser werden von Windows Admin Center unterstützt?

Die aktuellen Versionen der Browser Microsoft Edge (Windows 10, Version 1709 oder höher) und Google Chrome wurden unter Windows 10 getestet und werden unterstützt. [Browserspezifische bekannte Probleme anzeigen](../support/known-issues.md#browser-specific-issues). Andere moderne Webbrowser oder andere Plattformen sind derzeit nicht Bestandteil unserer Testmatrix und werden daher nicht *offiziell* unterstützt.

## <a name="how-does-windows-admin-center-handle-security"></a>Wie behandelt Windows Admin Center Sicherheit?

Der Datenverkehr vom Browser zum Windows Admin Center-Gateway verwendet HTTPS. Der Datenverkehr vom Gateway zu verwalteten Servern ist standardmäßig PowerShell und WMI über WinRM. Wir unterstützen LAPS (Local Administrator Password Solution), ressourcenbasierte eingeschränkte Stellvertretung, Gateway-Zugriffssteuerung mithilfe von AD oder Azure AD und rollenbasierte Kontrolle für die Verwaltung von Zielservern.

## <a name="does-windows-admin-center-use-credssp"></a>Verwendet Windows Admin Center CredSSP?

Ja, in einigen Fällen erfordert Windows Admin Center CredSSP. Dies ist erforderlich, um Ihre Anmeldeinformationen an Computer jenseits des spezifischen Servers zu übergeben, der Ihr Verwaltungsziel darstellt. Angenommen, Sie verwalten virtuelle Computer auf **server B**, möchten aber die VHDX-Dateien für diese virtuellen Computer auf einer Dateifreigabe speichern, die von **server C** gehostet wird, dann muss Windows Admin Center CredSSP für die Authentifizierung bei **server C** verwenden, um auf die Dateifreigabe zuzugreifen.

Windows Admin Center übernimmt die Konfiguration von CredSSP automatisch, nachdem es Ihre Zustimmung eingeholt hat. Bevor es CredSSP konfiguriert, überprüft Windows Admin Center, ob das System über die aktuellen CredSSP-[Updates](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018) verfügt. Während CredSSP aktiviert ist, werden ein Badge in der Serverübersicht und eine Option zur Deaktivierung angezeigt.

![CredSSP auf dem Server (Übersicht)](../media/CredSSP-overview.png)

CredSSP wird zurzeit in den folgenden Bereichen verwendet:

- Beim Einsatz von verstreutem SMB-Speicher im VM-Tool (das Beispiel oben.)
- Bei Verwendung des Updates-Tools in der Clusterverwaltungslösung für Failover oder für hyperkonvertente Cluster, das eine [clusterfähige Aktualisierung](https://docs.microsoft.com/windows-server/failover-clustering/cluster-aware-updating) ausführt. 

## <a name="are-there-any-cloud-dependencies"></a>Gibt es Abhängigkeiten mit der Cloud?

Windows Admin Center erfordert weder Internetzugang noch Microsoft Azure. Windows Admin Center kann Instanzen von Windows Server und Windows überall verwalten: auf physischen Systemen, auf virtuellen Computern oder beliebigen Hypervisorn oder bei Ausführung in beliebigen Clouds. Zwar wird im Lauf der Zeit Integration mit verschiedenen Azure-Diensten hinzugefügt, dabei handelt es sich aber um optionale Mehrwertfunktionen, die keine Voraussetzung für die Verwendung von Windows Admin Center darstellen.

## <a name="are-there-any-other-dependencies-or-prerequisites"></a>Gibt es andere Abhängigkeiten oder erforderliche Komponenten?

Windows Admin Center kann unter Windows 10 Fall Anniversary Update (1709) oder höher oder unter Windows Server 2016 oder höher installiert werden. Zum Verwalten von Windows Server 2008 R2, 2012 oder 2012 R2 ist die Installation von Windows Management Framework 5.1 auf diesen Servern erforderlich. Es gibt keine weiteren Abhängigkeiten. IIS ist nicht erforderlich, Agents sind nicht erforderlich, SQL Server ist nicht erforderlich.

## <a name="what-about-extensibility-and-3rd-party-support"></a>Wie sieht es mit Erweiterbarkeit und Drittanbieter-Unterstützung aus?

Für Windows Admin Center ist ein SDK verfügbar, sodass jeder seine eigene Erweiterung erstellen kann. Als Plattform hatten für uns der Ausbau unseres Ökosystems und das Ermöglichen von Erweiterbarkeit durch Partner von Anfang an eine Kernpriorität. [Weitere Informationen zum Windows Admin Center SDK](../extend/extensibility-overview.md).

## <a name="can-i-manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Lässt sich hyperkonvergente Infrastruktur mit Windows Admin Center verwalten?

Ja. Windows Admin Center unterstützt die Verwaltung von hyperkonvergenten Clustern unter Windows Server 2016 oder Windows Server 2019. Die Lösung zur Verwaltung hyperkonvergenter Cluster in Windows Admin Center wurde bisher als Vorschau bereitgestellt, ist jetzt aber **allgemein verfügbar**, mit einigen neuen Funktionen im Vorschaustadium. Zu weiteren Informationen [lesen Sie mehr über das Verwalten von hyperkonvergenter Infrastruktur](../use/manage-hyper-converged.md).

## <a name="does-windows-admin-center-require-system-center"></a>Ist System Center für Windows Admin Center erforderlich?

Nein. Windows Admin Center dient als Ergänzung zu System Center, System Center ist aber nicht erforderlich. [Weitere Informationen zu Windows Admin Center und System Center](related-management.md#system-center).

## <a name="can-windows-admin-center-replace-system-center-virtual-machine-manager-scvmm"></a>Kann der System Center Virtual Machine Manager (SCVMM) durch Windows Admin Center ersetzt werden?

Windows Admin Center und SCVMM ergänzen sich. Windows Admin Center soll die herkömmlichen MMC-Snap-Ins (Microsoft Management Console) und die Benutzeroberfläche zur Serververwaltung ersetzen.  Windows Admin Center ist nicht dazu bestimmt, die Überwachungsaspekte von SCVMM zu ersetzen. [Weitere Informationen zu Windows Admin Center und System Center](related-management.md#system-center).

## <a name="what-is-windows-admin-center-preview-which-version-is-right-for-me"></a>Was ist die Windows Admin Center-Vorschauversion, welche Version ist für mich geeignet?

Es stehen zwei Versionen von Windows Admin Center zum Download zur Verfügung:

### <a name="windows-admin-center"></a>Windows Admin Center

* Dies ist die richtige Version für IT-Administratoren, die keine häufigen Updates ausführen können oder mehr Validierungszeit für die Versionen wünschen, die sie in der Produktion verwenden. Unsere aktuelle allgemein verfügbare (generally available, GA) Version ist Windows Admin Center 1904.
* [!INCLUDE [support-policy](../includes/support-policy.md)]
* Das neueste Release können Sie [hier herunterladen](https://aka.ms/WACDownload).

### <a name="windows-admin-center-preview"></a>Windows Admin Center – Vorschau

* Dies ist die richtige Version für IT-Administratoren, die die neuesten und tollsten Features in regelmäßiger Folge erhalten möchten. Es ist unser Ziel, etwa monatlich Updatereleases zur Verfügung zu stellen. Die Kernplattform ist weiterhin produktionsgeeignet, und die Lizenz erteilt Nutzungsrechte für die Produktion. Beachten Sie jedoch, dass Sie mit der Einführung neuer Tools und Funktionen rechnen müssen, die eindeutig als VORSCHAU gekennzeichnet sind und zur Bewertung und für Tests geeignet sind.
* Um die neueste Insider Preview-Version zu erhalten, können registrierte Insider die Windows Admin Center-Vorschauversion direkt von der [Downloadseite für Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver) über die Dropdownliste „Weitere Downloads“ herunterladen. Wenn Sie noch nicht als Insider registriert sind, lesen Sie [Erste Schritte mit Windows Server](https://insider.windows.com/en-us/for-business-getting-started-server/) auf dem Windows Insiders for Business-Portal.

## <a name="why-was-windows-admin-center-chosen-as-the-final-name-for-project-honolulu"></a>Warum wurde „Windows Admin Center“ als endgültiger Name für „Projekt Honolulu“ gewählt?

Windows Admin Center ist der offizielle Produktname für „Projekt Honolulu“ und bestärkt unsere Vision einer integrierten Lösung für IT-Administratoren, die eine große Bandbreite von Kernaufgaben und Szenarien bei der Verwaltung abdeckt. Er hebt auch unsere Kundenorientierung auf die Benutzerbedürfnisse von IT-Administratoren als zentralen Aspekt unserer Investitions- und Produktplanung hervor.

## <a name="where-can-i-learn-more-about-windows-admin-center-or-get-more-details-on-the-topics-above"></a>Wo kann ich mehr über Windows Admin Center erfahren oder mehr Details zu den oben angesprochenen Themen erhalten?

Unsere [Startseite](https://aka.ms/WindowsAdminCenter) ist der beste Ausgangspunkt und weist Links zu unserem neu kategorisierten Dokumentationsinhalt zusammen mit Informationen über Feedback, Referenzinformationen und weiteren Quellen auf.

## <a name="what-is-the-version-history-of-windows-admin-center"></a>Wie ist der Versionsverlauf von Windows Admin Center?

[Versionsverlauf hier ansehen.](../overview.md#release-history)

## <a name="im-having-an-issue-with-windows-admin-center-where-can-i-get-help"></a>Ich habe ein Problem mit Windows Admin Center, wo erhalte ich Hilfe?

Lesen Sie unseren [Leitfaden zur Problembehandlung](../use/troubleshooting.md) und unsere Liste der [bekannten Probleme](../use/known-issues.md).
