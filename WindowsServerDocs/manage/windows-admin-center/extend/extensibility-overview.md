---
title: Erweiterungen für Windows Admin Center
description: Erweiterungen für Windows Admin Center SDK (Projekt Honolulu)
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fa3d7e75b32f0195346e58db54b7932c8d2fd3b9
ms.sourcegitcommit: 659544db1e19d6eecc52c7de07116ae735280544
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/11/2019
ms.locfileid: "9001842"
---
# Erweiterungen für Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Windows Admin Center wird als eine erweiterbare Plattform zum Aktivieren von Partnern und Entwicklern und Funktionen in Windows Admin Center genutzt, integriert sich nahtlos in andere Produkte für IT-Administrationsprodukte und -Lösungen und mehr. Jede Lösung und jedes Tool im Windows Admin Center ist eine Erweiterung mit denselben Erweiterungsfeatures für Partner und Entwickler, damit Sie die in Windows Admin Center verfügbaren leistungsstarken Tools nutzen können.

Windows Admin Center-Erweiterungen basieren auf modernen Webtechnologien einschließlich HTML5, CSS, Angular, TypeScript and jQuery und verwalten Zielserver über PowerShell oder WMI. Sie können auch Zielserver, Dienste oder Geräte über unterschiedliche Protokolle wie REST verwalten, durch die Erstellung eines Windows Admin Center Gateway-Plug-In.

## Warum Sie die Entwicklung einer Erweiterung für das Windows Admin Center in Betracht ziehen sollten

Hier ist der Wert für Ihr Produkt und Ihre Kunden durch die Entwicklung von Erweiterungen für Windows Admin Center:

- **Integrieren mit Windows Admin Center Tools:** Integrieren Sie Ihre Produkte und Dienstleistungen mit Server- und Cluster-Verwaltungstools in Windows Admin Center, und übermitteln Sie nahtlos, End-to-End-Management-Überwachung, Problembehandlung für Ihre Kunden.
- **Plattformsicherheit, Identitäts- und Management-Funktionen nutzen:** Aktivieren Sie Azure Active Directory (AAD) Support, Multi-Factor Authentication, Role-Based Access Control (RBAC), Protokollierung, Überwachung für Ihre Produkte und Dienste mithilfe von Windows Admin Center-Funktionen, um die komplexen Plattform-Anforderungen in heutigen IT-Organisationen zu erfüllen.
- **Entwickeln mit den neuesten Webtechnologien:** Erstellen Sie schnell beeindruckende Benutzererlebnisse mit modernen Webtechnologien einschließlich HTML5, CSS, Angular, TypeScript and jQuery und umfangreichen und leistungsstarken UI-Steuerelementen, die im Windows Admin Center SDK enthalten sind.
- **Produktreichweite vergrößern:** Werden Sie Teil des neuen Windows Admin Center-Ökosystems, erweitern Sie die schnell wachsende Kundenbasis und nutzen Sie das Windows Server 2019 Einführungsmomentum in diesem Jahr.

## Entwickeln Sie mit dem Windows Admin Center SDK

Erste Schritte bei der Entwicklung von Windows Admin Center ist einfach!  Beispielcode finden Sie für die [, die [Lösung](develop-solution.md)und [Gateway-Plug-in](develop-gateway-plugin.md) ](develop-tool.md)-Erweiterung-Typen in der SDK-Dokumentation. Es werden Sie nutzen, die Windows Admin Center-CLI zum Erstellen eines neuen Erweiterungsprojekts, und führen die Handbüchern aus, um das Projekt, um Ihren Bedürfnissen anzupassen.

Wir haben versucht ein Windows Admin Center [SDK-Design-Toolkits](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip) können Sie schnell Modell Erweiterungen in PowerPoint mit Windows Admin Center Stile, Steuerelemente und Vorlagen. Finden Sie unter die Erweiterung in Windows Admin Center sehen kann, bevor Sie mit der Codierung beginnen!

Wir haben auch auf GitHub gehosteten Beispielcode: [Entwicklertools](https://aka.ms/wacsdk) ist eine Beispiel-Lösung-Erweiterung enthält eine umfassende Sammlung von Steuerelementen, die Sie durchsuchen und in Ihre eigene Erweiterung verwenden können. Entwicklertools ist eine voll funktionsfähige Erweiterung, die in Windows Admin Center im Entwicklermodus Seite geladen werden können.

Lesen Sie die Themen unten, um mehr über das SDK und die ersten Schritte zu erfahren:

- [Verstehen der Funktionsweise von Erweiterungen](understand-extensions.md)
- [Entwickeln Sie eine Erweiterung](developing-extensions.md)
- [Handbücher](guides.md)
- [Veröffentlichen Sie die Erweiterung](publish-extensions.md)

## Partner Spotlight

Sehen Sie den Wert, den unsere Partner mit dem Windows Admin Center-Ökosystem haben und probieren Sie die Erweiterungen heute aus. Auf [Erweiterungen installieren](../configure/using-extensions.md) im Windows Admin Center erfahren Sie mehr.

### DataON

DataON's MUST-Erweiterungen sorgt dafür, dass die Überwachung, Verwaltung und End-to-End-Einblick in DataONs hyperkonvergenten Infrastruktur und Systemen basierend auf Windows Server. Die MUST-Erweiterung fügt eindeutigen Wert wie verlaufsdatenberichterstellung, Datenträger Zuordnung, System SAN-ähnlichen Aufruf home systemwarnungen und -Dienste, die Windows Admin Center und Management-Funktionen von hyperkonvergenten Infrastrukturen durch eine nahtlose, einheitliche Erfahrung. [Erfahren Sie mehr über DataON's MUST-Erweiterungen und die Erfahrung der Entwicklung](case-studies/dataon.md).

![DataON MUST-Erweiterung](../media/extensibility-overview/dataon-must-extension.png)

### Fujitsu

Fujitsu ServerView Integritäts- und RAID-Integritätserweiterung für Windows Admin Center bietet ausführliche Überwachung und Verwaltung von wichtigen Hardwarekomponenten wie Prozessoren, Arbeitsspeicher, Strom- und Speicher-Subsystemen für Fujitsu PRIMERGY-Server. Durch das Windows Admin Center UX Entwurfsmuster und UI-Steuerelemente, hat Fujitsu einen großen Schritt zur unsere Vision der End-to-End-Einblick in die Serverrollen und Dienste, Betriebssysteme sowie die Verwaltung von Hardware über die Windows Admin Center Geschäftswelt Plattform gemacht. [Erfahren Sie mehr über Fujitsu-Erweiterungen und die Erfahrung in der Entwicklung](case-studies/fujitsu.md).

![Fujitsu ServerView-Erweiterung](../media/extensibility-overview/fujitsu-serverview-extension.png)

### Lenovo

Die Lenovo XClarity Integrator-Erweiterung dauert Hardware-Verwaltung des nächsten Levels durch die nahtlose Integration in verschiedenen Funktionen in Windows Admin Center. Die XClarity Integrator-Lösung bietet einen allgemeinen Überblick über alle Lenovo-Server und anderen Tool-Erweiterungen bieten Hardwaredetails, ob Sie mit einem einzelnen Server, Failovercluster oder einem hyperkonvergenten Cluster verbunden sind. [Erfahren Sie mehr über die Lenovo XClarity Integrator-Erweiterung](case-studies/lenovo.md).

![Lenovo-Erweiterung](../media/extensibility-overview/lenovo-extension.png)

### Reine Speicher

Reine Speicher bietet Unternehmen, Daten für reine Flash-Speicher-Lösungen, die auf Daten ausgerichtete Architektur Ihres Unternehmens für einen Wettbewerbsvorteil verschaffen und beschleunigen damit bereitstellen. Die reine Speicher-Erweiterung für Windows Admin Center bietet eine Einzelansicht in reinen FlashArray Produkte und kann Benutzer monitoring Aufgaben durchführen, Leistungsmetriken in Echtzeit anzeigen und Verwalten von Speicher-Volumes und Initiatoren über eine einzelne Benutzeroberfläche auftreten. [Erfahren Sie mehr über die Pure Erweiterungen und die Erfahrung der Entwicklung](case-studies/purestorage.md).

![Reine Speicher-Erweiterung](../media/extensibility-overview/purestorage-extension.png)

### Squared Up

Squared Up bietet eine optimale Erfahrung basierend auf System Center Operations Manager und integriert Azure Log Analytics, Application Insights und anderen Monitoring-Lösungen. Die [Erweiterung Squared Up](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-docs&utm_medium=public-relations&utm_campaign=honolulu) ermöglicht optimale Leistungsdaten und Live-Anwendungstopologien und Abhängigkeiten im Kontext von Server- und Clusterverwaltung des Windows Admin Centers. Vorherige Kunden sehen den Wert der immensen Datenzufuhr aus vielen unterschiedlichen Quellen in eine einzelne Quelle. [Erfahren Sie mehr über Squared Up und die Erfahrung in der Entwicklung](case-studies/squared-up.md).

![Squared Up-Erweiterung](../media/extensibility-overview/squaredup-extension.png)