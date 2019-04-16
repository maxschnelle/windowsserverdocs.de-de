---
title: Häufig gestellte Fragen zu Windows Admin Center
description: Antworten zum Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 04/12/2019
ms.prod: windows-server-threshold
ms.openlocfilehash: 2f1591a32147e3c11ba635f1a11d36b7f38a3470
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296742"
---
# Häufig gestellte Fragen zu Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Hier erhalten Sie Antworten auf die am häufigsten gestellten Fragen zu Windows Admin Center.

## Was ist Windows Admin Center?

Windows Admin Center ist eine leichte browserbasierte GUI-Plattform und Toolset für IT-Administratoren zum Verwalten von Windows Server und Windows 10. Es ist die Weiterentwicklung von vertrauten Verwaltungstools wie Server-Manager und Microsoft Management Console (MMC) in einer modernisierten, vereinfachten, integrierten und sicheren Umgebung.

## Kann ich Windows Admin Center in Produktionsumgebungen verwenden?

Ja Windows Admin Center ist im Allgemeinen verfügbar und zur umfassenden Verwendung in Produktionsumgebungen geeignet. Die aktuelle Plattformfunktionen und die wichtigsten Tools erfüllen Microsoft Standardversion den Kriterien und unserer Qualität für Verwendbarkeit, Zuverlässigkeit, Leistung, Barrierefreiheit, Sicherheit und Übernahme.

[!INCLUDE [support-policy](../includes/support-policy.md)]

## Wie viel kostet Windows Admin Center?

Windows Admin Center ist ohne zusätzliche Kosten über Windows erhältlich. Sie können Windows Admin Center (als separater Download verfügbar) mit den gültigen Lizenzen für Windows Server oder Windows 10 ohne zusätzliche Kosten erhalten - es ist unter Windows als ergänzender EULA (ENDBENUTZER-LIZENZVERTRAG) lizenziert.

## Welche Versionen von Windows Server können mit Windows Admin Center verwaltet werden?

Windows Admin Center ist für Windows Server 2019 So aktivieren Sie wichtige Designs in der Version von Windows Server 2019 optimiert: hybride Cloudlösungen in bestimmten Szenarien und hyperkonvergente infrastrukturverwaltung. Zwar ist Windows Admin Center mit Windows Server 2019 am besten geeignet sind, es unterstützt eine Vielzahl von Versionen, die Kunden bereits verwalten: Windows Server 2012 und höher sind vollständig unterstützt. Es gibt auch eingeschränkte Funktion für die Verwaltung von Windows Server 2008 R2.

## Ist Windows Admin Center ein vollständiger Ersatz für alle integrierten und RSAT-Tools?

Nein. Obwohl viele Standardszenarien von Windows Admin Center verwaltet werden können, tauscht es nicht vollständig alle herkömmliche Tools von Microsoft Management Console (MMC) aus. Für eine detaillierte Aufstellung, welche Tools in Windows Admin Center enthalten sind weitere Informationen zum [Verwalten von Servern](..\use\manage-servers.md) , in unserer Dokumentation. Windows Admin Center hat die folgenden wichtigsten Funktionen in der Server-Manager-Lösung:

* Anzeigen von Ressourcen und Ressourcenverwendung
* Verwaltung von Zertifikaten
* Verwalten von Geräten
* Ereignisanzeige
* Datei-Explorer
* Firewall-Verwaltung
* Verwalten von installierte Apps
* Konfigurieren von lokalen Benutzern und Gruppen
* Netzwerkeinstellungen
* Anzeigen und Beenden von Prozessen und erstellen von Prozesssicherungen
* Bearbeiten der Registrierung
* Verwalten von geplante Aufgaben
* Verwalten von Windows-Diensten
* Aktivieren/Deaktivieren von Rollen und Features
* Verwalten von Hyper-V VMs und virtuelle Switches
* Verwalten von Speicher
* Verwalten von Speicherreplikat
* Verwalten von Windows Updates
* PowerShell-Konsole
* Remotedesktop-Verbindung

Windows Admin Center bietet auch diese Lösungen:

* Computermanagement – bietet eine Teilmenge der Server-Manager-Features zum Verwalten von Windows 10-Client-PCs
* Failovercluster-Manager – bietet Unterstützung für die laufende Verwaltung von Failovercluster und Cluster-Ressourcen
* Hyperkonvergente Cluster-Manager – bietet eine völlig neue Erfahrung, die speziell für Direkte Speicherplätze und Hyper-V gilt. Es bietet das Dashboard und betont Diagramme und Warnungen für die Überwachung.

Windows Admin Center ergänzt und ersetzt RSAT (Remote Server Administration Tools) nicht, da Rollen wie Active Directory, DNS, DHCP IIS noch nicht entsprechende Management-Funktionen im Windows Admin Center haben.

## Kann Windows Admin Center zur Verwaltung der kostenlosen Microsoft Hyper-V Server werden?

Ja Windows Admin Center kann zum Verwalten von Microsoft Hyper-V Server 2016 und Microsoft Hyper-V Server 2012 R2 verwendet werden.

## Kann ich Windows Admin Center auf einem Windows 10 Computer bereitstellen?

Ja, Windows Admin Center kann auf Windows 10 (Version 1709 oder höher) installiert und im Desktopmodus ausgeführt werden.  Windows Admin Center kann auch auf einem Server mit Windows Server 2016 installiert oder in gatewaymodus größer sein, und dann über einen Webbrowser auf einem Windows 10-Computer. [Erfahren Sie mehr über die Optionen für die Installation](..\plan\installation-options.md).

## Ich habe gehört, dass Windows Admin Center PowerShell hinter den Kulissen verwendet, können die tatsächlichen Skripts, die es verwendet angezeigt?

Ja! das [Showscript-Feature](..\use\get-started.md#view-powershell-scripts-used-in-windows-admin-center) in Windows Admin Center-Vorschau 1806 hinzugefügt wurde, und ist jetzt in der GA-Channel enthalten.

## Gibt es Pläne für Windows Admin Center zum Verwalten von Windows Server 2008 R2 oder einer früheren Version?

Windows Admin Center unterstützt **Eingeschränkte** Funktionen zum Verwalten von Windows Server 2008 R2. Windows Admin Center nutzt die Funktionen von PowerShell, und Plattform-Technologien, die in Windows Server 2008 R2 und früheren Versionen nicht vorhanden sind, und diese werden daher nicht voll unterstützt. Windows Server 2008/2008 R2 läuft im Januar 2020 Unterstützung daher empfiehlt Microsoft Kunden [auf Azure zu wechseln, oder aktualisieren Sie auf die neueste Version von Windows Server](https://www.microsoft.com/en-us/cloud-platform/windows-server-2008).

## Gibt es Pläne für Windows Admin Center zum Verwalten von Linux-Verbindungen?

Untersuchen wir aufgrund Kundennachfrage, aber es ist derzeit nicht geplant, bereitzustellen und Support besteht nur aus einer Konsolenverbindung über SSH.

## Welche Webbrowser können von Windows Admin Center unterstützt werden?

Die aktuellen Versionen von Microsoft Edge (Windows 10, Version 1709 oder höher) und Browsern von Google Chrome werden getestet und auf Windows 10 unterstützt. [Ansicht Browser bestimmte bekannte Probleme](..\support\known-issues.md#browser-specific-issues). Andere moderne Webbrowser oder andere Plattformen sind derzeit nicht Bestandteil unserer Testmatrix und werden daher nicht *offiziell* unterstützt.

## Wie behandelt Windows Admin Center Sicherheit?

Datenverkehr vom Browser an das Windows Admin Center-Gateway verwendet HTTPS. Datenverkehr vom Gateway auf verwaltete Server ist standardmäßig PowerShell und WMI über WinRM. Wir unterstützen LAPS (Local Administrator Password Solution), eingeschränkte ressourcenbasierte Delegierung, Gateway-Steuerung des Zugriffs über AD oder Azure AD und rollenbasierte Zugriffssteuerung für die Verwaltung von Zielservern.

## Werden Windows Admin Center wird CredSSP verwendet?

Ja, erfordert Windows Admin Center in einigen Fällen CredSSP. Dies ist erforderlich, um Ihre Anmeldeinformationen für die Authentifizierung auf Computern über die bestimmten Server, die, den Sie abzielen, für die Verwaltung übergeben. Beispielsweise, wenn Sie virtuelle Computer auf **Server B**verwalten, aber die Vhdx-Dateien für diese virtuellen Computer auf eine Dateifreigabe **Server C**gehostete speichern möchten, Windows Admin Center müssen verwenden CredSSP zur Authentifizierung mit **Server C** für den Zugriff auf die Dateifreigabe.

Windows Admin Center behandelt die Konfiguration von CredSSP automatisch nach der Aufforderung zur Zustimmung des von Ihnen. Vor dem Konfigurieren von CredSSP, wird Windows Admin Center überprüfen, um sicherzustellen, dass das System die aktuellen CredSSP [Updates](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)verfügt. Während CredSSP aktiviert ist, werden ein Signal für die Server-Übersicht und eine Option zum Deaktivieren-

![CredSSP auf Server (Übersicht)](../media/CredSSP-overview.png)

CredSSP ist derzeit in den folgenden Bereichen verwendet:

- Mit zerlegt SMB-Speicher im virtuellen Computer-Tool (im Beispiel oben.)
- Verwenden die Updates tool in der Failover oder zusammengeführte Cluster-Management-Lösungen, die führt [Clusterfähiges aktualisieren](https://docs.microsoft.com/windows-server/failover-clustering/cluster-aware-updating) 

## Gibt es Abhängigkeiten mit der Cloud?

Windows Admin Center erfordert keinen Zugriff auf das Internet oder Microsoft Azure. Windows Admin Center verwaltet Windows Server und Windows-Instanzen überall: auf physischen Systemen oder virtuellen Computern auf einem beliebigen Hypervisor, oder in einer beliebigen Cloud. Obwohl die Integration mit unterschiedlichen Azure-Diensten mit der Zeit hinzugefügt werden, werden optionale Zusatzfunktionen verwendet Windows Admin Center ist nicht notwendig.

## Gibt es andere Abhängigkeiten oder erforderliche Komponenten?

Windows Admin Center kann auf Windows 10 Fall Anniversary Update (1709) oder höher, oder Windows Server 2016 oder höher installiert werden. Zum Verwalten von Windows Server 2008 R2, 2012 oder 2012 R2, ist die Installation von Windows Management Framework 5.1 auf diesen Servern erforderlich. Es gibt keine andere Abhängigkeiten. IIS ist nicht erforderlich, Agents sind nicht erforderlich, SQL Server ist nicht erforderlich.

## Was geschieht mit Erweiterbarkeit und Drittanbieter-Unterstützung?

Windows Admin Center hat ein SDK verfügbar, sodass jeder Benutzer eine eigene Erweiterung schreiben kann. Als Plattform war unser Ökosystemwachstum und die Partner-Erweiterbarkeit eine der wichtigsten Prioritäten. [Weitere Informationen zum Windows Admin Center SDK](..\extend\extensibility-overview.md).

## Kann ich Hyperkonvergente Infrastruktur mit Windows Admin Center verwalten?

Ja Windows Admin Center unterstützt die Verwaltung von hyperkonvergenten Clustern unter Windows Server 2016 oder Windows Server 2019. Die zusammengeführte Cluster-Manager-Lösung im Windows Admin Center wurde zuvor in der Vorschau, aber es ist jetzt **in der Regel verfügbar**, die einige neue Funktionen in der Vorschau. Lesen Sie [Weitere Informationen zum Verwalten der Hyperkonvergenten Infrastruktur](..\use\manage-hyper-converged.md).

## Erfordert Windows Admin Center das System Center?

Nein. Windows Admin Center dient als Ergänzung zu System Center, System Center ist jedoch nicht erforderlich. [Weitere Informationen zu Windows Admin Center und System Center Lesen](related-management.md#system-center).

## Kann Windows Admin Center den System Center Virtual Machine Manager (SCVMM) ersetzen?

Windows Admin Center und SCVMM ergänzen sich. Windows Admin Center ersetzt die herkömmliche Microsoft Management Console (MMC) Snap-Ins und die Server-Administratorerfahrung.  Windows Admin Center kann nicht die Überwachungsaspekte von SCVMM ersetzen. [Weitere Informationen zu Windows Admin Center und System Center Lesen](related-management.md#system-center).

## Was ist Windows Admin Center - Vorschau, welche Version ist für mich geeignet?

Es stehen zwei Versionen von Windows Admin Center zum Download zur Verfügung:

### Windows Admin Center

* Für IT-Administratoren, die nicht häufig aktualisieren können oder die mehr Validierungszeit für die Versionen, die sie in der Produktion verwenden benötigen. Unsere aktuellen allgemein verfügbar (GA)-Version ist Windows Admin Center 1904.
* [!INCLUDE [support-policy](../includes/support-policy.md)]
* Um die neueste Version [hier herunterladen](https://aka.ms/WACDownload)zu erhalten.

### Windows Admin Center – Vorschau

>[!NOTE]
>Die aktuelle GA-Version (Windows Admin Center 1904) enthält alle vorherigen Preview-Funktionen.
>Der Insider Preview wird in den kommenden Monaten zurückgegeben.

* Für IT-Administratoren, die die neuesten und interessantesten Features auf einer regulären Trittfrequenz verwenden möchten. Unsere Absicht ist, nachfolgende Update Freigaben in jedem Monat herauszugeben. Die Kern-Plattform ist weiterhin einsatzbereit, und die Lizenz enthält Produktionsnutzungsrechte. Die Einführung der neuen Tools und Funktionen, die als Vorschau deutlich markiert sind, eignen sich für die Bewertung und zum Testen.
* Um die neuesten Insider Preview-Version zu erhalten, können registrierte Insider Windows Admin Center-Vorschau direkt aus der [Windows Server Insider Preview herunterladen Seite](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)unter der Dropdownliste zusätzliche Downloads herunterladen. Wenn Sie noch nicht als Insider registriert sind, lesen Sie [Erste Schritte mit Windows Server](https://insider.windows.com/en-us/for-business-getting-started-server/) auf dem Windows-Insider für Unternehmen-Portal.

## Warum wurde "Windows Admin Center" als der endgültige Name für "Projekt Honolulu" ausgewählt?

Windows Admin Center ist der offizielle Produktname für "Projekt Honolulu" und verstärkt unserer Vision für IT-Administratoren mit einer integrierten Lösung und einer Vielzahl administrativer Verwaltungskerne und -Szenarien. Es zeigt auch unseren zentralen Fokus für IT Admin Benutzer und bietet eine optimale Kundenorientierung.

## Wo erfahren Sie mehr über Windows Admin Center oder erhalten weitere Informationen zu den oben aufgeführten Themen?

Unsere [Startseite](https://aka.ms/WindowsAdminCenter) ist der beste Ausgangspunkt und verfügt über Links zu unserer Dokumentation und dem neu kategorisierten Inhalt, Downloadadressen, der Bereitstellung von Feedback, Referenzinformationen und andere Ressourcen.

## Was ist die Versionsgeschichte des Windows Admin Center?

[Die Version Versionsgeschichte hier angezeigt.](..\overview.md#release-history)

## Ich habe ein Problem mit Windows Admin Center, wo erhalte ich Hilfe?

Lesen Sie unser [Handbuch zur Problembehandlung](..\use\troubleshooting.md) und unsere Liste der [bekannten Probleme](..\use\known-issues.md).
