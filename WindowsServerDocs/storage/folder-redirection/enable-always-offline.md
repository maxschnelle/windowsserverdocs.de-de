---
title: Aktivieren des Modus „Immer offline“ für schnelleren Zugriff auf Dateien
description: Verwenden des Modus „Immer offline“ von Offlinedateien, um schnelleren Zugriff auf zwischengespeicherte Dateien und umgeleitete Ordner bereitzustellen.
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2a4526a70379ad414cdf866419a3b893e42256d5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942221"
---
# <a name="enable-always-offline-mode-for-faster-access-to-files"></a>Aktivieren des Modus „Immer offline“ für schnelleren Zugriff auf Dateien

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2 und Windows (halbjährlicher Kanal)

Dieses Dokument beschreibt, wie der Modus „Immer offline“ von Offlinedateien verwendet wird, um schnelleren Zugriff auf zwischengespeicherte Dateien und umgeleitete Ordner bereitzustellen. „Immer offline“ bietet auch schnelleren Zugriff auf Dateien und geringere Bandbreitenverwendung, weil Benutzer selbst dann immer offline arbeiten, wenn sie über eine Hochgeschwindigkeits-Netzwerkverbindung verbunden sind.

## <a name="prerequisites"></a>Voraussetzungen

Um den Modus „Immer offline“ zu aktivieren, muss Ihre Umgebung die folgenden Voraussetzungen erfüllen.

- Eine Active Directory Domain Services-Domäne (AD DS) mit Clientcomputern, die der Domäne beigetreten sind. Es gibt keine Anforderungen an die Gesamtstruktur- oder Domänenfunktionsebene oder Schemaanforderungen.
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausführen. (Clientcomputer, auf denen frühere Versionen von Windows ausgeführt werden, können bei sehr schnellen Netzwerkverbindungen möglicherweise weiterhin in den Onlinemodus übergehen.)
- Ein Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.

## <a name="enable-always-offline-mode"></a>Aktivieren des Modus „Immer offline“

Um den Modus „Immer offline“ zu aktivieren, verwenden Sie die Gruppenrichtlinie, um die Richtlinieneinstellung **Modus für langsame Verbindungen konfigurieren** zu aktivieren, und legen Sie die Latenz auf **1** (Millisekunde) fest. Dies bewirkt, dass Clientcomputer, auf denen Windows 8 oder Windows Server 2012 ausgeführt wird, automatisch den Modus „Immer offline“ verwenden.

>[!NOTE]
>Computer mit Windows 7, Windows Vista, Windows Server 2008 R2 oder Windows Server 2008 können weiterhin in den Onlinemodus wechseln, wenn die Latenz der Netzwerkverbindung unter eine Millisekunde sinkt.

1. Öffnen Sie **Gruppenrichtlinienverwaltung**.
2. Um optional ein neues Gruppenrichtlinienobjekt (GPO) für die Einstellungen von Offlinedateien zu erstellen, klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit (OU), und wählen Sie dann **Gruppenrichtlinienobjekt hier erstellen und verknüpfen** aus.
3. Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, für das Sie die Einstellungen für Offlinedateien konfigurieren möchten, und wählen Sie dann **Bearbeiten** aus. Der **Gruppenrichtlinienverwaltungs-Editor** wird geöffnet.
4. Erweitern Sie in der Konsolenstruktur unter **Computerkonfiguration** die Optionen **Richtlinien**, **Verwaltungsvorlagen**, **Netzwerk** und **Offlinedateien**.
5. Klicken Sie mit der rechten Maustaste auf **Modus für langsame Verbindungen konfigurieren**, und wählen Sie dann **Bearbeiten** aus. Das Fenster **Modus für langsame Verbindungen konfigurieren** wird angezeigt.
6. Wählen Sie **Aktiviert**aus.
7. Wählen Sie im Feld **Optionen** die Option **Anzeigen** aus. Das Fenster **Inhalt anzeigen** wird angezeigt.
8. Geben Sie im Feld **Wertname** die Dateifreigabe an, für die Sie den Modus „Immer offline“ aktivieren möchten.
9. Um den Modus „Immer offline“ für alle Dateifreigaben zu aktivieren, geben Sie **\*** ein.
10. Geben Sie im Feld **Wert** die Angabe **Latenz=1** ein, um den Latenzschwellenwert auf eine Millisekunde festzulegen, und wählen Sie dann **OK** aus.

>[!NOTE]
>Standardmäßig synchronisiert Windows im Modus „Immer offline“ alle zwei Stunden Dateien im Offlinedateiencache im Hintergrund. Um diesen Wert zu ändern, verwenden Sie die Richtlinieneinstellung **Hintergrundsynchronisierung konfigurieren**.

## <a name="more-information"></a>Weitere Informationen

* [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht](folder-redirection-rup-overview.md)
* [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md)