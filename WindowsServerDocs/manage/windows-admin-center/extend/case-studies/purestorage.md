---
title: Windows Admin Center SDK-Fallstudie-reiner Speicher
description: Windows Admin Center SDK-Fallstudie-reiner Speicher
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.openlocfilehash: a79b575397c5dc139200f69a0110ab3c909d5fd5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942702"
---
# <a name="pure-storage-extension"></a>Reine Speichererweiterung

## <a name="providing-end-to-end-array-management-for-windows-admin-center"></a>Bereitstellen einer End-to-End-Array Verwaltung für Windows Admin Center

[Reiner Speicher](https://www.purestorage.com/) bietet Enterprise-, all-Flash-Datenspeicherlösungen, die datenzentrierte Architekturen bereitstellen, um Ihr Unternehmen auf einen Wettbewerbsvorteil zu beschleunigen.  Pure ist ein Microsoft Gold-Partner, der für Microsoft Windows Server zertifiziert ist und technische Integrationen für wichtige Microsoft-Lösungen wie Azure, Hyper-V, SQL Server, System Center, Windows PowerShell und Windows SMB entwickelt. "Pure" hat vor kurzem eine technische Vorschau einer Erweiterung angekündigt, die die neueste Version von Windows Admin Center unterstützt, die eine Ansicht mit einem einzelnen Bereich für reine flasharray-Produkte bietet.  Aus dieser Erweiterung werden Benutzer von einem Tool zur Durchführung von Überwachungsaufgaben, Anzeigen von Echt Zeit Leistungsmetriken und Verwalten von Speichervolumes und Initiatoren ermächtigt.

Wenn das Windows Admin Center früher als "Project Honolulu" bezeichnet wurde, war es in der Lage, Kunden und Partnern die Möglichkeit zu geben, mehrere reine Speicher-Flash-Blitze aus dem einzelnen Glasbereich zu verwalten, den das Windows Admin Center bereitstellt.

Als pure begann, den Anwendungsfall mit "Project Honolulu" zu untersuchen, erkannten sie sofort das Potenzial, eine einheitliche Verwaltungsfunktion zwischen Windows Admin Center und flasharray bereitzustellen. Mit dem Entwicklungsteam von Windows Admin Center haben Sie eng zusammengearbeitet, um die Implementierungsdetails für die Features zu definieren. Pure konnte in den frühen Phasen des Windows Admin Centers auch Feedback geben und Beiträge an das Microsoft-Team senden.

![Reine Speichererweiterung](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Wir haben einen Featuresatz integriert, der unsere flasharray-Weboberfläche imitiert, um die direkt Verwaltung im Windows Admin Center zu ermöglichen. Unsere Kunden und Partner profitieren von einem einzelnen Glasbereich und müssen mit zwei verschiedenen Verwaltungs Tools arbeiten. Zusätzlich zu den einzelnen Verwaltungs Vorteilen können Kunden Windows-Server, die mit dem flasharray verbunden sind, auf die gleiche Weise verwalten. "</cite>
>
> --Barkz, Technical Director Microsoft Solutions & Integration, reiner Speicher

Zu den Features, die in der Erweiterung für reine Speicherlösungen enthalten sind, gehören:
- Herstellen einer Verbindung mit mehreren-blinharrays.
- Anzeigen der Details zum flasharray, einschließlich IOPS, Bandbreite, Latenz, Daten Reduzierung und Speicherplatz Verwaltung. Dabei handelt es sich um dieselben Details, die Sie von der Benutzeroberfläche für die clouddatenverwaltung erhalten.
- Anzeigen konfigurierter Host Gruppen, die verwendet werden, um den Zugriff auf freigegebenen Volumes für Windows Server-Hosts und freigegebene Clustervolumes (csvs) zu aktivieren.
- Hosts anzeigen – alle Konnektivitätsinformationen sind verfügbar, einschließlich Hostnamen, von iSCSI qualifizierter Namen (IQNs) und World Wide Names (WWNs).
- Verwalten von Volumes – Dies schließt die Möglichkeit ein, Volumes zu erstellen und zu zerstören. Sobald ein Volume zerstört wurde, wird es in den Bucket "zerstört Items" eingefügt, und Sie müssen von der Haupt-GUI der cloudverwaltung entfernt werden.
- Verwalten von Initiatoren – Dies ist eines der interessantesten Features, die den Kontext für die einzelnen Server bereitstellen, die von der Windows Admin Center-Bereitstellung verwaltet werden. Sie können die verbundenen Datenträger (Volumes) auf einzelnen Windows-Servern anzeigen und überprüfen, ob Multipfad-IO (MPIO) installiert/konfiguriert ist und neue Volumes erstellt bzw. bereitstellen.

Es wurde ein [Demonstrationsvideo](https://youtu.be/IFAeCAd6V2g) erstellt, in dem alle Features angezeigt werden, die von der Erweiterung für reine Speicherlösungen bereitstellt werden.

Der folgende Screenshot veranschaulicht, wie Sie anzeigen, welche Datenträger (Volumes) mit einem bestimmten Windows Server-Host verbunden sind. Zusätzlich zum Anzeigen der konnektivitätsdetails prüfen wir, ob Multipfad-e/a konfiguriert ist.

![Reine Speichererweiterung](../../media/extend-case-study-purestorage/purestorage-2.png)

Zusätzlich zum Anzeigen der Datenträger können neue Volumes erstellt und sofort auf dem Host bereitgestellt werden, ohne dass das Windows-Datenträger Verwaltungs Tool verwendet werden muss.

![Reine Speichererweiterung](../../media/extend-case-study-purestorage/purestorage-3.png)

Seit der Veröffentlichung unserer Technical Preview war das bisher gesammelte Kundenfeedback sehr positiv und hat uns auch Einblicke in verschiedene Features gegeben, die in zukünftigen Versionen hinzugefügt werden können.

Zusätzliche Ressourcen:
- [Blogbeitrag zur Ankündigung der reinen Speichererweiterung](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- " [Purereport](https://itunes.apple.com/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2) "-Podcast
