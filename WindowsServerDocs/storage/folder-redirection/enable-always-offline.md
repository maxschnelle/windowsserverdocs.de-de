---
title: Aktivieren Sie für einen schnelleren Zugriff auf Dateien immer Offline-Modus
description: So verwenden Sie den Modus "immer Offline" von Offlinedateien, schnelleren Zugriff auf zwischengespeicherte Dateien und umgeleiteten Ordner gewähren.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8684926beb0f0c911ac384970d15ba7d25f84079
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475936"
---
# <a name="enable-always-offline-mode-for-faster-access-to-files"></a>Aktivieren Sie für einen schnelleren Zugriff auf Dateien immer Offline-Modus

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2019, WindowsServer 2016, WindowsServer 2012, Windows Server 2012 R2 und Windows (halbjährlicher Kanal)

Dieses Dokument beschreibt, wie Sie mit, dass der Modus "immer Offline" von Offlinedateien schnelleren Zugriff auf zwischengespeicherte Dateien und umgeleiteten Ordner gewähren. Immer Offline auch bietet geringere bandbreitenverwendung, da der Benutzer immer offline arbeiten, selbst wenn sie über eine schnelle Netzwerkverbindung besteht.

## <a name="prerequisites"></a>Vorraussetzungen

Um immer Offline-Modus zu aktivieren, muss Ihre Umgebung die folgenden Voraussetzungen erfüllen.

- Eine Active Directory Domain Services (AD DS)-Domäne mit Clientcomputern, die in die Domäne eingebunden werden soll. Es gibt keine Anforderungen von Gesamtstruktur oder Domäne auf Funktionsebene oder schemaanforderungen.
- Client-Computer unter Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012. (Client-Computern, die mit früheren Versionen von Windows können für den Übergang in den Onlinemodus Hochgeschwindigkeitsnetzwerk Verbindungen weiterhin.)
- Ein Computer mit die Gruppenrichtlinien-Verwaltungskonsole installiert.

## <a name="enable-always-offline-mode"></a>Immer Offline-Modus aktivieren

Um immer Offline-Modus zu aktivieren, mithilfe von Gruppenrichtlinien zum Aktivieren der **Modus für langsame Verbindungen konfigurieren** Richtlinie festlegen, und legen die Latenz auf **1** (in Millisekunden). Dadurch wird die Client-Computern mit Windows 8 oder Windows Server 2012 automatisch immer Offline-Modus verwenden.

>[!NOTE]
>Computer, die mit Windows 7, möglicherweise Windows Vista, Windows Server 2008 R2 oder Windows Server 2008 für den Übergang zum Online-Modus fortgesetzt, wenn die Latenz der Netzwerkverbindung unter einer Millisekunde sinkt.

1. Open **Gruppenrichtlinienverwaltung**.
2. Um eine neue Gruppe Gruppenrichtlinienobjekt (GPO) für die Einstellungen für Offlinedateien optional zu erstellen, mit der rechten Maustaste der entsprechenden Domäne oder Organisationseinheit (OU), und wählen Sie dann **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**.
3. In der Konsolenstruktur mit der Maustaste des GPOs für die Sie zum Konfigurieren von Einstellungen für Offlinedateien, und wählen Sie dann **bearbeiten**. Die **Gruppenrichtlinienverwaltungs-Editor** angezeigt wird.
4. In der Konsolenstruktur unter **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **Netzwerk**, und erweitern Sie **Offlinedateien**.
5. Mit der rechten Maustaste **Modus für langsame Verbindungen konfigurieren**, und wählen Sie dann **bearbeiten**. Die **Modus für langsame Verbindungen konfigurieren** Fenster wird angezeigt.
6. Wählen Sie **Aktiviert** aus.
7. In der **Optionen** Kontrollkästchen **anzeigen**. Die **Inhalt anzeigen Fenster** wird angezeigt.
8. In der **Wertnamen** geben die Dateifreigabe, die für die Sie aktivieren, immer Offline-Modus möchten.
9. Um auf alle freigegebenen Ordner immer Offline-Modus zu aktivieren, geben Sie **\***.
10. In der **Wert** geben **Latenz = 1** Schwellenwert für die Latenzzeit auf 1 Millisekunde festgelegt, und wählen Sie dann **OK**.

>[!NOTE]
>Standardmäßig synchronisiert immer Offline-Modus in Windows-Dateien im Zwischenspeicher für Offlinedateien im Hintergrund alle zwei Stunden. Um diesen Wert zu ändern, verwenden die **Configure Background Sync** richtlinieneinstellung.

## <a name="more-information"></a>Weitere Informationen

* [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
* [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)