---
title: 'Windows Admin Center-SDK-Fallstudie: reine Speicher'
description: 'Windows Admin Center-SDK-Fallstudie: reine Speicher'
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 25018474fd22d05804ecc7faafbd633fbb4db269
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849921"
---
# <a name="pure-storage-extension"></a>Reine Speichererweiterung.

## <a name="providing-end-to-end-array-management-for-windows-admin-center"></a>Bereitstellung von End-to-End-Array-Verwaltung für Windows Admin Center 

[Reine Storage](https://www.purestorage.com/) bietet Unternehmen, die All-Flash-Daten-Storage-Lösungen, die datenorientierte Architektur beschleunigen Sie Ihr Unternehmen einen Wettbewerbsvorteil zu übermitteln.  Reiner Microsoft Gold-Partner für Microsoft Windows Server zertifiziert ist und entwickelt technische Integrationen für wichtige Microsoft-Lösungen wie Azure, Hyper-V, SQL Server, System Center, Windows PowerShell und Windows-SMB. Reiner kündigte vor kurzem eine technische Vorschau einer Erweiterung, die Unterstützung der neuesten Version von Windows Admin Center, das eine Einzelansicht in reinen FlashArray Produkte bereitstellt.  Von dieser Erweiterung sind Benutzer befugt ist, über ein Tool zur führen Sie Überwachungsaufgaben, in Echtzeit Leistungsmetriken anzeigen und Verwalten von Speichervolumes und Initiatoren.

Wenn Windows Admin Center als "Project Honolulu" bekannt war, reiner gesehen haben den Wert der Kunden zu bieten und Partnern die Möglichkeit, mehrere reine Storage FlashArrays über die zentrale Konsole zu verwalten, die Windows Admin Center bietet.

Wenn reiner informierte den Anwendungsfall mit "Projekt Honolulu" fanden sie sofort das Potenzial für die Bereitstellung einer einheitliche Verwaltungsoberfläche zwischen Windows Admin Center und FlashArray. Reiner zusammengearbeitet eng mit dem Windows Admin Center-Entwicklungsteam, das bei der die Implementierungsdetails für die Funktionen zu definieren. Reiner konnte auch Feedback in den frühen Phasen des Windows Admin Center, und Beiträge an den Microsoft-Team. 

![Reine Speichererweiterung.](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Wir haben einen Satz, der unsere FlashArray Weboberfläche zum Aktivieren der direktverwaltung von Windows Admin Center imitiert integriert. Unsere Kunden und Partner profitieren von einem einzelnen Bereich zusammengefasst und zusammen mit zwei andere Verwaltungstools verwenden müssen. Zusätzlich zu den einzelnen Verwaltungspunkt werden Vorteile für den Kunden je nach Kontext Windows-Server zu verwalten, die mit der FlashArray verbunden sind."</cite>
>
> --Barkz, Technical Director, Microsoft-Lösungen und -Integration, reine Speicher

Die Funktionen, die in der reinen Speichererweiterung Lösung enthalten sind enthalten:
- Die Verbindung mit mehreren FlashArrays.
- Anzeigen von FlashArray Details, darunter IOPs, Bandbreite, Latenz, eine Reduzierung der Datenmenge und Verwaltung des Adressraums ein. Hierbei handelt es sich um den gleichen Details, die Sie über die grafische Benutzeroberfläche FlashArray-Management zu erhalten.
- Zeigen Sie die konfigurierten Hostgruppen, die verwendet werden, um Zugriff auf freigegebenen Volumes für Windows Server-Hosts und freigegebene Clustervolumes (CSVs) zu aktivieren.
- Ansicht Hosts – Alle Informationen, die Konnektivität ist verfügbar, einschließlich Hostnamen-iSCSI-qualifizierten Namen (IQN) "und" World Wide Names (WWNs).
- Verwalten von Volumes – Dies schließt die Möglichkeit zum Erstellen und Zerstören von Volumes. Sobald ein Volume zerstört wird wird im Bucket Destroyed Elemente dieser und müssen Sie Eradicate über die wichtigsten FlashArray Management GUI.
- Verwalten von Initiatoren – Dies ist eines der interessantesten Features, die Bereitstellung von Kontext, der den einzelnen Servern, die von der Bereitstellung von Windows Admin Center verwaltet. Sie können für einzelne Windows-Server, überprüfen Sie die verbundenen Datenträgern (Volumes) anzeigen, Multipfad-e/a (MPIO) ist installiert/konfiguriert, und erstellen und einbinden neue Volumes.

Ein [Demovideo](https://youtu.be/IFAeCAd6V2g) erstellt wurde, die zeigt, alle Features, die der reinen Speichererweiterung Lösung bereitstellt. 

Der nachfolgende Screenshot zeigt anzeigen, welche Datenträger (Volumes) mit einem bestimmten Windows Server-Host verbunden sind. Zusätzlich zum Anzeigen von Details Konnektivität, überprüfen wir, ob es sich bei Multipfad-e/a konfiguriert ist.

![Reine Speichererweiterung.](../../media/extend-case-study-purestorage/purestorage-2.png)

Zusätzlich zum Anzeigen der Datenträger können können sofort auf den Host ohne Windows-datenträgerverwaltung verwenden neue Volumes erstellt und eingebunden werden.

![Reine Speichererweiterung.](../../media/extend-case-study-purestorage/purestorage-3.png)

Da unsere Technical Preview, die bisher erfasst Feedback von Kunden freigegeben sehr positiv wurde und hat auch bietet uns einen Einblick in die verschiedenen Funktionen in zukünftigen Versionen hinzufügen. 

Weitere Ressourcen:
- [Reine Blogbeitrag von Storage-Erweiterung Ankündigung](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/us/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2) Podcast
