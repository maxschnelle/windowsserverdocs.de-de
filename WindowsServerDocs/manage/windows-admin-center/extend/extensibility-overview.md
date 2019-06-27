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
ms.openlocfilehash: beb2b3d1eefc5d70e39baa461708938ac9c17be5
ms.sourcegitcommit: 3be280c8638214857dc355b201eb56a04499a5e5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2019
ms.locfileid: "67396684"
---
# <a name="extensions-for-windows-admin-center"></a>Erweiterungen für Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Windows Admin Center wird als eine erweiterbare Plattform zum Aktivieren von Partnern und Entwicklern und Funktionen in Windows Admin Center genutzt, integriert sich nahtlos in andere Produkte für IT-Administrationsprodukte und -Lösungen und mehr. Jede Lösung und jedes Tool im Windows Admin Center ist eine Erweiterung mit denselben Erweiterungsfeatures für Partner und Entwickler, damit Sie die in Windows Admin Center verfügbaren leistungsstarken Tools nutzen können.

Windows Admin Center-Erweiterungen basieren auf modernen Webtechnologien einschließlich HTML5, CSS, Angular, TypeScript and jQuery und verwalten Zielserver über PowerShell oder WMI. Sie können auch Zielserver, Dienste oder Geräte über unterschiedliche Protokolle wie REST verwalten, durch die Erstellung eines Windows Admin Center Gateway-Plug-In.

## <a name="why-you-should-consider-developing-an-extension-for-windows-admin-center"></a>Warum Sie die Entwicklung einer Erweiterung für das Windows Admin Center in Betracht ziehen sollten

Hier ist der Wert für Ihr Produkt und Ihre Kunden durch die Entwicklung von Erweiterungen für Windows Admin Center:

- **Mit Windows Admin Center-Tools integriert werden:** Server und Cluster Verwaltungstools in Windows Admin Center Ihre Produkte und Dienste integriert werden und einheitlichen und nahtlosen, End-to-End Überwachung, Verwaltung, Problembehandlung, um Ihre Kunden zu übermitteln.
- **Nutzen Sie Plattform-Sicherheit, Identität und Management-Funktionen:** Aktivieren der Unterstützung von Azure Active Directory (AAD), Multi-Factor Authentication, Role-Based Access Control (RBAC), Protokollierung, Überwachung, die für Ihre Produkte und Dienste durch die Nutzung von Windows Admin Center-Plattformfunktionen, die heutigen komplexen Anforderungen IT-Organisationen.
- **Verwenden die neuesten webtechnologien zu entwickeln:** Erstellen Sie schnell ansprechende Benutzeroberflächen mit modernen webtechnologien wie HTML5, CSS, Angular, TypeScript und jQuery und umfangreiche und leistungsstarke UI-Steuerelemente, die im Windows Admin Center SDK enthalten.
- **Erweitern Sie die Produkt-Outreach:** Werden Sie Teil des neuen Windows Admin Center-Ökosystems mit Outreach zu unseren schnell wachsenden Kundenstamm und nutzen die Windows Server-2019 starten Momentum später in diesem Jahr.

## <a name="start-developing-with-the-windows-admin-center-sdk"></a>Entwickeln Sie mit dem Windows Admin Center-SDK

Einstieg mit der Entwicklung von Windows Admin Center ist ganz einfach!  Beispielcode finden Sie für [Tool](develop-tool.md), [Lösung](develop-solution.md), und [Gateway-Plug-Ins](develop-gateway-plugin.md) Erweiterungstypen in der SDK-Dokumentation. Es nutzt die Windows Admin Center-CLI zum Erstellen eines neuen Projekts der Erweiterung, und befolgen dann die einzelnen Handbücher, um das Projekt, um Ihre Anforderungen anzupassen.

Haben Sie eine Windows Admin Center [SDK Entwurf Toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip) verfügbar, mit denen Sie die Erweiterungen in PowerPoint – Dank Windows Admin Center Stile, Steuerelemente und Seitenvorlagen schnell zu modellieren. Erfahren Sie, wie die Erweiterung in Windows Admin Center aussehen kann vor dem Programmieren!

Wir haben außerdem Beispielcode auf GitHub gehostet: [Entwicklertools](https://aka.ms/wacsdk) ist eine Beispiel-Lösung-Erweiterung, die eine umfangreiche Sammlung von Steuerelementen, die Sie durchsuchen und verwenden Sie in Ihrer eigenen Extension enthält. Entwicklertools ist eine voll funktionsfähige Erweiterung, die in Windows Admin Center im Entwicklermodus Seite geladen werden können.

Lesen Sie die Themen unten, um mehr über das SDK und die ersten Schritte zu erfahren:

- [Funktionsweise von Erweiterungen](understand-extensions.md)
- [Entwickeln einer Erweiterung](developing-extensions.md)
- [Handbücher](guides.md)
- [Veröffentlichen Sie Ihrer extension](publish-extensions.md)

## <a name="partner-spotlight"></a>Partner Spotlight

Sehen Sie den Wert, den unsere Partner mit dem Windows Admin Center-Ökosystem haben und probieren Sie die Erweiterungen heute aus. Auf [Erweiterungen installieren](../configure/using-extensions.md) im Windows Admin Center erfahren Sie mehr.

### <a name="biitops"></a>BiitOps
Die BiitOps Änderungen-Erweiterung bietet änderungsnachverfolgung, die für die Hardware, Software und Konfiguration von Einstellungen für Ihre physische/virtuelle Windows Server-Computer. Die BiitOps Änderungen, die Erweiterung anzeigen, wird genau Neuigkeiten, was sich geändert hat und was in einem einzelnen Bereich-transparente verfolgen, Probleme gelöscht wurde im Zusammenhang mit Kompatibilität, Zuverlässigkeit und Sicherheit. [Erfahren Sie mehr über die Erweiterung BiitOps Änderungen](case-studies/biitops.md).

![BiitOps-Erweiterung](../media/extensibility-overview/biitops-1.png)

### <a name="dataon"></a>DataON

Die Erweiterung muss Spitzengruppe bietet Überwachung, Verwaltung und End-to-End-Einblick in Spitzengruppes hyperkonvergenten Infrastruktur und Speichersysteme, die basierend auf Windows Server. Die Erweiterung muss hinzufügt, eindeutigen Wert z. B. Vergangenheitsdaten reporting, datenträgerzuordnung, systemwarnungen und SAN-ähnlichen Aufruf home-Dienst, ergänzen die Windows Admin Center-Server und einer hyperkonvergenten Infrastruktur-Management-Funktionen über eine nahtlose, einheitliche Erfahrung. [Erfahren Sie mehr über DataON's MUST-Erweiterungen und die Erfahrung der Entwicklung](case-studies/dataon.md).

![DataON MUST-Erweiterung](../media/extensibility-overview/dataon-must-extension.png)

### <a name="fujitsu"></a>Fujitsu

Fujitsu ServerView-Integrität und RAID-Health-Erweiterungen für Windows Admin Center werden ausführliche Überwachung und Verwaltung von kritischen Hardwarekomponenten wie Prozessoren, Arbeitsspeicher und Speicherkapazität Subsysteme für Fujitsu PRIMERGY-Server bereitstellen. Durch das Windows Admin Center UX Entwurfsmuster und UI-Steuerelemente, hat Fujitsu einen großen Schritt zur unsere Vision der End-to-End-Einblick in die Serverrollen und Dienste, Betriebssysteme sowie die Verwaltung von Hardware über die Windows Admin Center Geschäftswelt Plattform gemacht. [Erfahren Sie mehr über Fujitsu-Erweiterungen und die Erfahrung in der Entwicklung](case-studies/fujitsu.md).

![Fujitsu ServerView-Erweiterung](../media/extensibility-overview/fujitsu-serverview-extension.png)

### <a name="lenovo"></a>Lenovo

Die Lenovo XClarity Integrator-Erweiterung nimmt die hardwareverwaltung auf die nächste Stufe durch die nahtlose Integration in verschiedene Umgebungen innerhalb Windows Admin Center. Die XClarity Integrator-Lösung bietet einen allgemeinen Überblick über alle Lenovo-Server, und verschiedene Tools-Erweiterungen bieten Hardwaredetails, ob Sie mit einem einzelnen Server, Failovercluster oder eines hyperkonvergenten Clusters verbunden sind. [Erfahren Sie mehr über die Erweiterung Lenovo XClarity Integrator](case-studies/lenovo.md).

![Lenovo-Erweiterung](../media/extensibility-overview/lenovo-extension.png)

### <a name="pure-storage"></a>Pure Storage

Pure-Speicher bietet Unternehmen, die All-Flash-Daten-Storage-Lösungen, die datenorientierte Architektur beschleunigen Sie Ihr Unternehmen einen Wettbewerbsvorteil zu übermitteln. Die reine Storage-Erweiterung für Windows Admin Center bietet einen zentralen Überblick in reinen FlashArray-Produkte und ermöglicht Benutzern, führen Sie Überwachungsaufgaben, in Echtzeit Leistungsmetriken anzeigen und Verwalten von Speichervolumes und Initiatoren, die über eine einzige Benutzeroberfläche auftreten. [Erfahren Sie mehr über die Pure-Erweiterungen und ihre Entwicklungsumgebung](case-studies/purestorage.md).

![Reine speichererweiterung](../media/extensibility-overview/purestorage-extension.png)

### <a name="qct"></a>QCT

Die Erweiterung QCT Management Suite ergänzt Windows Admin Center, durch die Bereitstellung von physischen Servern zu Überwachung und Verwaltung von QCT Azure Stack HCI zertifizierten Systeme. Die QCT Management Suite-Erweiterung zeigt Serverhardwareinformationen und bietet ein intuitiver Assistent UI können Sie die physischen ersetzen, Hardware-Ereignisprotokoll-Tools und s.m.a.r.t. Datenträger basieren predictive datenträgerverwaltung. [Erfahren Sie mehr über die QCT Management Suite-Erweiterung](case-studies/qct.md).

![QCT-Erweiterung](../media/extensibility-overview/qct-extension.png)

### <a name="squared-up"></a>Squared Up

Squared Up bietet eine optimale Erfahrung basierend auf System Center Operations Manager und integriert Azure Log Analytics, Application Insights und anderen Monitoring-Lösungen. Die [Erweiterung Squared Up](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-docs&utm_medium=public-relations&utm_campaign=honolulu) ermöglicht optimale Leistungsdaten und Live-Anwendungstopologien und Abhängigkeiten im Kontext von Server- und Clusterverwaltung des Windows Admin Centers. Vorherige Kunden sehen den Wert der immensen Datenzufuhr aus vielen unterschiedlichen Quellen in eine einzelne Quelle. [Erfahren Sie mehr über Squared Up und die Erfahrung in der Entwicklung](case-studies/squared-up.md).

![Squared Up-Erweiterung](../media/extensibility-overview/squaredup-extension.png)