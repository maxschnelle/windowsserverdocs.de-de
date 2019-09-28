---
title: Aktivieren des Modus "immer offline" für schnelleren Zugriff auf Dateien
description: Verwenden des Always Offline-Modus von Offlinedateien, um schnelleren Zugriff auf zwischengespeicherte Dateien und umgeleitete Ordner bereitzustellen.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 389fdd26a7e1d9824f1eaf0136a544547f08eb05
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401958"
---
# <a name="enable-always-offline-mode-for-faster-access-to-files"></a>Aktivieren des Modus "immer offline" für schnelleren Zugriff auf Dateien

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2 und Windows (halbjährlicher Kanal)

In diesem Dokument wird beschrieben, wie der Modus "immer offline" Offlinedateien verwendet wird, um einen schnelleren Zugriff auf zwischengespeicherte Dateien und umgeleitete Ordner bereitzustellen. "Immer offline" bietet auch eine geringere Bandbreitenauslastung, da Benutzer immer offline arbeiten, auch wenn Sie über eine Hochgeschwindigkeitsnetzwerk Verbindung verbunden sind.

## <a name="prerequisites"></a>Erforderliche Komponenten

Um den Modus "immer offline" zu aktivieren, muss Ihre Umgebung die folgenden Voraussetzungen erfüllen.

- Eine Active Directory Domain Services Domäne (AD DS) mit Client Computern, die der Domäne beigetreten sind. Es gibt keine Anforderungen an die Gesamtstruktur-oder Domänen Funktionsebene oder Schema Anforderungen.
- Client Computer unter Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012. (Client Computer, auf denen frühere Versionen von Windows ausgeführt werden, können bei sehr schnellen Netzwerkverbindungen möglicherweise weiterhin in den Online Modus übergehen.)
- Ein Computer, auf dem Gruppenrichtlinie-Verwaltung installiert ist.

## <a name="enable-always-offline-mode"></a>Aktivieren des Modus "immer offline"

Wenn Sie den Modus "immer offline" aktivieren möchten, verwenden Sie Gruppenrichtlinie, um die Richtlinien Einstellung **langsamen Verbindungs Modus konfigurieren** zu aktivieren und die Wartezeit auf **1** (Millisekunde) festzulegen. Dies bewirkt, dass Client Computer, auf denen Windows 8 oder Windows Server 2012 ausgeführt wird, automatisch den Modus "immer offline" verwenden.

>[!NOTE]
>Computer mit Windows 7, Windows Vista, Windows Server 2008 R2 oder Windows Server 2008 können weiterhin in den Online Modus wechseln, wenn die Latenz der Netzwerkverbindung unter eine Millisekunde sinkt.

1. Öffnen Sie **Gruppenrichtlinie-Verwaltung**.
2. Klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit, und klicken Sie dann auf Gruppenrichtlinien Objekt **in dieser Domäne erstellen,** um optional ein neues Gruppenrichtlinie Objekt (GPO) für Offlinedateien Einstellungen zu erstellen.
3. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf das GPO, für das Sie die Offlinedateien Einstellungen konfigurieren möchten, und wählen Sie dann **Bearbeiten**aus. Der **Gruppenrichtlinienverwaltungs-Editor** wird angezeigt.
4. Erweitern Sie in der Konsolen **Struktur unter Computer Konfiguration**den Knoten **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **Netzwerk**, und erweitern Sie **Offlinedateien**.
5. Klicken Sie mit der rechten Maustaste auf **Modus für langsame Verbindungen konfigurieren**, und wählen Sie dann **Bearbeiten**aus. Das Fenster Fenster für **langsamen Verbindungs Modus konfigurieren** wird angezeigt.
6. Wählen Sie **Aktiviert** aus.
7. Wählen Sie im Feld **Optionen die Option** **anzeigen**aus. Das **Fensterinhalt anzeigen** wird angezeigt.
8. Geben Sie im Feld **Wertname** die Dateifreigabe an, für die Sie den Modus "immer offline" aktivieren möchten.
9. Um den Modus "immer offline" für alle Dateifreigaben zu aktivieren, geben Sie **\* ein**.
10. Geben Sie im Feld **Wert den Wert** **Latenz = 1** ein, um den Latenz Schwellenwert auf eine Millisekunde festzulegen, und klicken Sie dann auf **OK**.

>[!NOTE]
>Standardmäßig synchronisiert Windows im Modus "immer offline" alle zwei Stunden Dateien im Offlinedateien Cache im Hintergrund. Um diesen Wert zu ändern, verwenden Sie die Richtlinien Einstellung **Synchronisierung im Hintergrund konfigurieren** .

## <a name="more-information"></a>Weitere Informationen

* [Übersicht über Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
* [Bereitstellen der Ordner Umleitung mit Offlinedateien](deploy-folder-redirection.md)