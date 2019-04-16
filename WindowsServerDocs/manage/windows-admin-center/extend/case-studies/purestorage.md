---
title: Windows Admin Center SDK-Fallstudie - reinen Speicher
description: Windows Admin Center SDK-Fallstudie - reinen Speicher
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 25018474fd22d05804ecc7faafbd633fbb4db269
ms.sourcegitcommit: ebeec824f802f020d0ece17524ba43b1baeba893
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2019
ms.locfileid: "8995322"
---
# Reine Speicher-Erweiterung

## Bietet End-to-End-Array-Verwaltung für Windows Admin Center 

[Reine Speicher](https://www.purestorage.com/) bietet Unternehmen, Daten für reine Flash-Speicher-Lösungen, die auf Daten ausgerichtete Architektur Ihres Unternehmens für einen Wettbewerbsvorteil verschaffen und beschleunigen damit bereitstellen.  Pure ist ein Microsoft Gold Partner für Microsoft Windows Server, zertifiziert und entwickelt technische Integration für die wichtigsten Microsoft-Lösungen wie Azure, Hyper-V, SQL Server, System Center, Windows PowerShell und Windows-SMB. Pure angekündigt eine Tech Preview einer Erweiterung unterstützen die neueste Version von Windows Admin Center, die eine Einzelansicht in reinen FlashArray Produkte bereitstellt.  Dieser Erweiterung sind Benutzer über ein Tool zur Überwachung Aufgaben durchführen, Leistungsmetriken in Echtzeit anzeigen und Verwalten von Speicher-Volumes und Initiatoren befugt.

Früh zu Windows Admin Center als "Projekt Honolulu" bezeichnet wurde, Pure gesehen hat den Wert auf Kunden und Partner die Möglichkeit, mehrere reinen Speicher FlashArrays von der zentralen Konsole zu verwalten, die Windows Admin Center bietet.

Zu Beginn Pure Untersuchung des Anwendungsfalls mit "Projekt Honolulu" realisiert sie sofort das Risiko, dass eine einheitliche Verwaltung benutzererfahrung zwischen Windows Admin Center und FlashArray. Pure Virtualisierungssoftware eng mit dem Windows Admin Center-Entwicklungsteam, was die Implementierungsdetails für die Features zu definieren. Pure konnte auch Feedback in den frühen Phasen von Windows Admin Center und Beiträge für das Microsoft-Team. 

![Reine Speicher-Erweiterung](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Wir haben eine Featuregruppe, die unsere FlashArray-Web-Benutzeroberfläche, um die direkte Verwaltung von Windows Admin Center ermöglichen imitiert integriert. Unsere Kunden und Partner profitieren von einer zentralen Konsole im Vergleich mit zwei unterschiedliche Management-Tools arbeiten müssen. Neben der zentrale Verwaltung kann Vorteile für den Kunden je nach Kontext auf Windows-Servern verwalten, die mit der FlashArray verbunden sind."</cite>
>
> – Barkz, Director technische Microsoft-Lösungen und Integration von reinen Speicher

Die Funktionen, die in die Erweiterung der reinen Speicher-Lösung enthalten sind enthalten:
- Herstellen einer Verbindung, um mehrere FlashArrays.
- Anzeigen von FlashArray Details, einschließlich IOPs, Bandbreite, Latenz, Reduzierung der Daten und Platz-Verwaltung. Hierbei handelt es sich um die gleichen Details, die Sie von der FlashArray Management-Benutzeroberfläche zu erhalten.
- Anzeigen von konfigurierten Host-Gruppen, die verwendet werden, um die freigegebenen Volume Zugriff für Windows Server-Hosts und freigegebenen Clustervolumes (CSVs) zu aktivieren.
- Ansicht Hosts – Alle Konnektivitätsinformationen, ist verfügbar, einschließlich Hostnamen, iSCSI qualifizierten Namen (IQNs) und World Wide Names (WWNs).
- Verwalten von Datenträgern – Dazu gehören die Fähigkeit zum Erstellen und Löschen von Volumes. Nachdem Sie ein Volume gelöscht wird in der zerstören Elemente Zelle platziert und müssen Sie Eradicate von der wichtigsten FlashArray Management-Benutzeroberfläche.
- Verwalten von Initiatoren – Dies ist ein von der interessantesten Features, die mit der Kontext, um den einzelnen Servern, die durch die Bereitstellung von Windows Admin Center verwaltet. Multipfad-e/a (MPIO) installiert/konfiguriert und erstellen/Montage neue Volumes ist, können Sie die verbundenen Datenträger (Volumes) für einzelne Windows Server, aktivieren Sie das Kontrollkästchen anzeigen.

Eine [Demo-video](https://youtu.be/IFAeCAd6V2g) wurde erstellt, der alle Features, die die Erweiterung der reinen Speicher-Lösung enthält. 

Der folgende Screenshot veranschaulicht die anzeigen, welche Datenträger (Volumes) mit einem bestimmten Windows Server-Host verbunden sind. Zusätzlich zur Anzeige der Konnektivität Detail, überprüfen wir, ob Multipfad-e/a konfiguriert ist.

![Reine Speicher-Erweiterung](../../media/extend-case-study-purestorage/purestorage-2.png)

Zusätzlich zur Anzeige der Datenträger, können neue Volumes erstellt und sofort auf den Host bereitgestellt, ohne Windows Datenträger Management-Tool verwenden zu müssen.

![Reine Speicher-Erweiterung](../../media/extend-case-study-purestorage/purestorage-3.png)

Da unsere Technical Preview, die bisher gesammelten Kundenfeedback Freigabe wurde und einen Einblick in verschiedene Features in zukünftigen Versionen hinzufügen auch uns erhalten haben. 

Weitere Ressourcen:
- [Reine Speicher Erweiterung Ankündigung Blogbeitrag](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/us/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2) podcast
