---
title: Erweiterungen für Windows Admin Center
description: Erweiterungen für das Windows Admin Center SDK (Projekt Honolulu)
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9dd372b765df3dce719c44ce99ed6e4ab6d156fc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956117"
---
# <a name="extensions-for-windows-admin-center"></a>Erweiterungen für Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Windows Admin Center ist als erweiterbare Plattform konzipiert, damit Partner und Entwickler vorhandene Funktionen innerhalb des Windows Admin Centers nutzen, nahtlos in andere IT-Verwaltungs Produkte und-Lösungen integrieren und für Kunden zusätzlichen Wert bereitstellen können. Jede Projekt Mappe und jedes Tool im Windows Admin Center ist als Erweiterung mit denselben Erweiterbarkeits Features erstellt, die für Partner und Entwickler zur Verfügung stehen, sodass Sie leistungsstarke Tools erstellen können, wie Sie noch heute im Windows Admin Center verfügbar sind.

Windows Admin Center-Erweiterungen werden mit modernen Webtechnologien wie HTML5, CSS, Angular, typescript und jQuery erstellt und können Zielserver über PowerShell oder WMI verwalten. Sie können Zielserver, Dienste oder Geräte auch über verschiedene Protokolle (z. b. Rest) verwalten, indem Sie ein Windows Admin Center Gateway-Plug-in aufbauen.

## <a name="why-you-should-consider-developing-an-extension-for-windows-admin-center"></a>Warum Sie eine Erweiterung für Windows Admin Center entwickeln sollten

Hier ist der Wert, den Sie für Ihr Produkt und ihre Kunden nutzen können, indem Sie Erweiterungen für Windows Admin Center entwickeln:

- **Integration in Windows Admin Center-Tools:** Integrieren Sie Ihre Produkte und Dienste in die Server-und Cluster Verwaltungs Tools in Windows Admin Center, und stellen Sie Ihren Kunden eine einheitliche, nahtlose End-to-End-Überwachung, Verwaltung und Problembehandlung bereit.
- **Nutzen Sie Plattformsicherheit, Identitäts-und Verwaltungsfunktionen:** Aktivieren Sie die Unterstützung von Azure Active Directory (AAD), Multi-Factor Authentication, rollenbasierten Access Control (Role-Based, RBAC), Protokollierung, Überwachung für Ihr Produkt und ihre Dienste, indem Sie die Funktionen der Windows Admin Center-Plattform nutzen, um die komplexen Anforderungen der heutigen IT-
- **Entwickeln Sie mit den neuesten Webtechnologien:** Erstellen Sie mit modernen Webtechnologien, wie z.b. HTML5, CSS, Angular, typescript und jQuery, und umfangreiche, leistungsstarke UI-Steuerelemente, die im Windows Admin Center SDK enthalten sind, schnell beeindruckende Benutzererfahrung.
- **Erweitern der Produktbetreuung:** Werden Sie Teil des Windows Admin Center-Ökosystems, das sich auf unsere erweiternde Kundenbasis erweitert.

## <a name="start-developing-with-the-windows-admin-center-sdk"></a>Beginnen Sie mit der Entwicklung mit dem Windows Admin Center SDK

Der Einstieg in die Entwicklung des Windows Admin Centers ist einfach!  Den Beispielcode finden Sie in unserer SDK-Dokumentation für [Tool](develop-tool.md) [-, Projektmappen-und](develop-solution.md)Gateway- [Plug](develop-gateway-plugin.md) -in-Erweiterungs Typen. Dort verwenden Sie die Windows Admin Center-CLI, um ein neues Erweiterungsprojekt zu erstellen, und befolgen dann die einzelnen Leitfäden, um Ihr Projekt an Ihre Anforderungen anzupassen.

Wir haben ein Windows Admin Center [SDK-Entwurfs-Toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip) zur Verfügung gestellt, mit dem Sie Erweiterungen in PowerPoint mithilfe von Windows Admin Center-Stilen,-Steuerelementen und-Seitenvorlagen schnell bereinigen können. Sehen Sie sich an, wie Ihre Erweiterung im Windows Admin Center aussehen kann, bevor Sie mit dem Programmieren beginnen!

Außerdem haben wir Beispielcode auf GitHub gehostet: [Entwicklertools](https://aka.ms/wacsdk) ist eine Beispiel-projektmappenerweiterung, die eine umfangreiche Sammlung von Steuerelementen enthält, die Sie durchsuchen und in ihrer eigenen Erweiterung verwenden können. Entwicklertools ist eine voll funktionsfähige Erweiterung, die im Entwicklermodus in das Windows Admin Center quer geladen werden kann.

Weitere Informationen zum SDK und zu den ersten Schritten finden Sie in den folgenden Themen:

- [Verstehen der Funktionsweise von Erweiterungen](understand-extensions.md)
- [Entwickeln einer Erweiterung](developing-extensions.md)
- [Handbücher](guides.md)
- [Veröffentlichen der Erweiterung](publish-extensions.md)

## <a name="partner-spotlight"></a>Partner Spotlight

Sehen Sie sich den erstaunlichen Wert an, den unsere Partner mit der Einführung in das Windows Admin Center-Ökosystem begonnen haben, und testen Sie diese Erweiterungen noch heute. Erfahren Sie mehr über das [Installieren von Erweiterungen aus dem](../configure/using-extensions.md) Windows Admin Center.

### <a name="biitops"></a>BiitOps
Die Erweiterung für biitops-Änderungen bietet Änderungs Nachverfolgung für Hardware-, Software-und Konfigurationseinstellungen auf ihren physischen/virtuellen Windows Server-Computern. Die Erweiterung für biitops-Änderungen zeigt genau, was neu ist, was sich geändert hat und was in einem einzelnen Bereich gelöscht wurde, um Probleme im Zusammenhang mit Compliance, Zuverlässigkeit und Sicherheit zu verfolgen. [Erfahren Sie mehr über die Erweiterung für biitops-Änderungen](case-studies/biitops.md).

![Biitops-Erweiterung](../media/extensibility-overview/biitops-1.png)

### <a name="dataon"></a>DataON

Die Erweiterung "DataOn" muss über die Erweiterung "Überwachung", "Verwaltung" und "End-to-End" in der hyperkonvergierten Infrastruktur und in den Speichersystemen von Daten auf Basis von Windows Server. Die Erweiterung muss einen eindeutigen Wert hinzufügen, wie z. b. Verlaufs Daten Berichte, Datenträger Zuordnung, Systemwarnungen und San-ähnlichen CallHome Service, und ergänzt den Windows Admin Center-Server und die hyperkonvergenten Infrastruktur Verwaltungsfunktionen durch eine nahtlose, einheitliche Funktionalität. [Erfahren Sie mehr über die Erweiterung "DataOn" und deren Entwicklungs](case-studies/dataon.md)Möglichkeiten.

![DataOn muss Erweiterung](../media/extensibility-overview/dataon-must-extension.png)

### <a name="fujitsu"></a>Fujitsu

Die ServerView Health-und RAID-Integritäts Erweiterungen von Fujitsu für Windows Admin Center bieten eine ausführliche Überwachung und Verwaltung kritischer Hardwarekomponenten wie z. b. Prozessoren, Arbeitsspeicher, Energie-und Speicher Subsysteme für Fujitsu PRIMERGY-Server. Durch die Verwendung der UX-Entwurfsmuster und UI-Steuerelemente von Windows Admin Center hat Fujitsu einen großen Schritt für unsere Vision von End-to-End-Einblicken in Server Rollen und-Dienste, das Betriebssystem und die Hardware Verwaltung über die Windows Admin Center-Plattform eingeführt. [Erfahren Sie mehr über die Erweiterungen von Fujitsu und deren Entwicklungs](case-studies/fujitsu.md)Möglichkeiten.

![Fujitsu Server View-Erweiterung](../media/extensibility-overview/fujitsu-serverview-extension.png)

### <a name="lenovo"></a>Lenovo

Die Lenovo xclarity Integrator-Erweiterung übernimmt die Hardware Verwaltung auf der nächsten Ebene, indem Sie nahtlos in verschiedene Umgebungen in Windows Admin Center integriert wird. Die xclarity Integrator-Lösung bietet eine allgemeine Übersicht über alle Lenovo-Server, und verschiedene Tool Erweiterungen stellen Hardware Details bereit, unabhängig davon, ob Sie mit einem einzelnen Server, einem Failovercluster oder einem hyperkonvergenten Cluster verbunden sind. [Erfahren Sie mehr über die Lenovo xclarity Integrator-Erweiterung](case-studies/lenovo.md).

![Lenovo-Erweiterung](../media/extensibility-overview/lenovo-extension.png)

### <a name="pure-storage"></a>Pure Storage

Reiner Speicher bietet Enterprise-, all-Flash-Datenspeicherlösungen, die datenzentrierte Architekturen bereitstellen, um Ihr Unternehmen auf einen Wettbewerbsvorteil zu beschleunigen. Die reine Speichererweiterung für das Windows Admin Center bietet eine Ansicht mit einem einzelnen Bereich für reine flasharray-Produkte und ermöglicht Benutzern das Durchführen von Überwachungsaufgaben, das Anzeigen von Echt Zeit Leistungsmetriken und das Verwalten von Speichervolumes und Initiatoren über eine einzige Benutzeroberfläche. [Erfahren Sie mehr über die reinen Erweiterungen und deren Entwicklungs](case-studies/purestorage.md)Möglichkeiten.

![Reine Speichererweiterung](../media/extensibility-overview/purestorage-extension.png)

### <a name="qct"></a>QCT

Die qct Management Suite-Erweiterung ergänzt Windows Admin Center durch die Bereitstellung physischer Serverüberwachung und-Verwaltung für qct-Azure Stack HCI-zertifizierte Systeme. Die qct Management Suite-Erweiterung zeigt Server Hardwareinformationen an und bietet eine intuitive Assistent-Benutzeroberfläche, die Ihnen hilft, physische Datenträger effizient zu ersetzen, Hardware-Ereignisprotokoll Tools und S.M.A.R.T. basierte Verwaltung vorhersag barer Datenträger. [Erfahren Sie mehr über die qct Management Suite-Erweiterung](case-studies/qct.md).

![Qct-Erweiterung](../media/extensibility-overview/qct-extension.png)