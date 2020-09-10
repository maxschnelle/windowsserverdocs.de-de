---
title: Aktivieren der Ordnerumleitung auf dem Windows Server Essentials-Zielserver1
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
H1: Aktivieren der Ordner Umleitung auf dem Windows Server Essentials-Ziel Server
ms.assetid: f67d195e-36f6-495a-8361-6d5faa889441
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 9ea3b7b6c42c85ef553e56f017d068fabea42eee
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622871"
---
# <a name="enable-folder-redirection-on-the-windows-server-essentials-destination-server1"></a>Aktivieren der Ordnerumleitung auf dem Windows Server Essentials-Zielserver1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können diese Aufgabe ausführen, wenn die Ordnerumleitung auf dem Quellserver aktiviert ist.

 Verwenden Sie zunächst das Windows Server Essentials-Dashboard, um die Ordner Umleitung auf dem Ziel Server zu aktivieren. Löschen Sie daraufhint die alte Gruppenrichtlinieneinstellung zur Ordnerumleitung.

### <a name="to-enable-folder-redirection-on-the-destination-server"></a>So aktivieren Sie die Ordnerumleitung auf dem Zielserver

1.  Öffnen Sie auf dem Ziel Server das Windows Server Essentials-Dashboard.

2.  Klicken Sie in der Navigationsleiste **Geräte**.

3.  Klicken Sie im Bereich**Geräteaufgaben** auf **Implementieren von Gruppenrichtlinien**.

4.  Wählen Sie auf der Seite **Aktivieren der Richtlinie für die Ordnerumleitung** die Ordner aus, die umgeleitet werden sollen, und klicken Sie dann auf **Weiter**.

5.  Klicken Sie auf der Seite **Sicherheitsrichtlinieneinstellungen aktivieren** auf **Fertig stellen**.

### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>Löschen der alten Gruppenrichtlinieneinstellung zur Ordnerumleitung.

1. Öffnen Sie auf dem Zielserver das Verwaltungstool **Gruppenrichtlinienverwaltung**.

2. Erweitern Sie in **Gruppenrichtlinienverwaltung**den Eintrag **Gesamtstruktur:**<em>IhrNetzwerkDomänenname</em>den Eintrag **Domänen**den Eintrag *IhrNetzwerkDomänenname*und erweitern Sie dann **Gruppenrichtlinienobjekte**.

3. Klicken Sie mit der rechten Maustaste auf **W7PVP Ordnerumleitung** und klicken Sie dann auf **Löschen**.

4. Lesen Sie die Warnung und klicken Sie dann auf **Ja**.

5. Schließen Sie die **Gruppenrichtlinienverwaltung**.

   Um die Änderung an der Ordnerumleitung zu übernehmen, müssen Netzwerkbenutzer zuerst ihren Computer abmelden und dann wieder anmelden. Dadurch wird die Übertragung von allen umgeleiteten Ordnern auf den Zielserver sichergestellt .
