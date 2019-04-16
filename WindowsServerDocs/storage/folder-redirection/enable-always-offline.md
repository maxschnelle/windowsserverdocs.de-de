---
title: Aktivieren Sie immer Offline-Modus für den schnelleren Zugriff auf Dateien
description: Informationen zur Verwendung den Modus immer Offline von Offlinedateien schnelleren Zugriff auf zwischengespeicherte Dateien und umgeleitete Ordner bereitstellen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: bc54b1e33d09e7f2b9eea01e4f09fb83f13dc1af
ms.sourcegitcommit: 505505b7ec99506e7ff50eddbdd6aa94a602abe6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/11/2018
ms.locfileid: "3831390"
---
# Aktivieren Sie immer Offline-Modus für den schnelleren Zugriff auf Dateien

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016

Dieses Dokument beschreibt, wie Sie den Modus immer Offline, der Offline-Dateien verwenden, um schneller Zugriff auf zwischengespeicherte Dateien und umgeleitete Ordner bereitzustellen. Immer Offline bietet außerdem niedriger Bandbreite aus, da Benutzer immer offline arbeiten, auch wenn sie über eine schnelle Netzwerkverbindung verbunden sind.

## Voraussetzungen

Um immer Offline-Modus zu aktivieren, muss Ihre Umgebung folgende Voraussetzungen erfüllen.

- Eine Active Directory Domain Services (AD DS)-Domäne mit Clientcomputern mit der Domäne verbunden. Es gibt keine Gesamtstruktur oder Domäne Funktionsebene Anforderungen oder Schema-Anforderungen.
- Clientcomputer, die unter Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012. (Clientcomputer, auf denen frühere Versionen von Windows möglicherweise für den Wechsel in den Onlinemodus auf sehr schnelle Netzwerkverbindungen fortgesetzt.)
- Ein Computer mit Gruppenrichtlinien-Verwaltungskonsole installiert.

## Immer Offline-Modus aktivieren

Verwenden von Gruppenrichtlinien zum Aktivieren des immer Offline-Modus aktivieren die Einstellung **Konfigurieren langsame Modus** und Festlegen der Wartezeit auf **1** (Millisekunde). Dadurch werden Clientcomputer unter Windows 8 oder Windows Server 2012 immer Offlinemodus automatisch zu verwenden.

>[!NOTE]
>Computern unter Windows 7, möglicherweise Windows Vista, Windows Server 2008 R2 oder Windows Server 2008 Übergang zu den Online-Modus fortgesetzt, wenn die Wartezeit der Verbindung eine Millisekunde unterschreitet.

1. Öffnen Sie **die Gruppenrichtlinien-Verwaltungskonsole**.
2. Um ein neues Gruppenrichtlinienobjekt (GPO) für Offlinedateien Einstellungen optional zu erstellen, mit der rechten Maustaste der entsprechenden Domäne oder Organisationseinheit (OE), und wählen Sie dann **Erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne und hier verknüpfen**.
3. In der Konsolenstruktur mit der rechten Maustaste im GPOs, für die Sie konfigurieren Sie die Offlinedateien-Einstellungen, und wählen Sie dann **Bearbeiten**möchten. Den **Gruppenrichtlinienverwaltungs-Editor** angezeigt wird.
4. In der Konsolenstruktur unter **Computerkonfiguration**erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **Netzwerk**und **Offlinedateien**.
5. Mit der rechten Maustaste **Konfigurieren langsame Modus**, und wählen Sie dann **Bearbeiten**. Das Fenster **Konfigurieren langsame Modus** wird angezeigt.
6. Wählen Sie **Aktiviert** aus.
7. Wählen Sie im Feld **Optionen** **Anzeigen**. Der **Inhalt anzeigen-Fenster** wird angezeigt.
8. Geben Sie im Feld **Wertname** der Dateifreigabe für die Sie immer Offline-Modus aktivieren möchten.
9. Geben Sie zum Aktivieren des Modus immer Offline auf alle Dateifreigaben **\***.
10. Geben Sie im Feld **Wert** **Latenz = 1** den Schwellenwert Latenz auf eine Millisekunde, und wählen Sie dann auf **OK**.

>[!NOTE]
>Standardmäßig synchronisiert im immer Offline-Modus Windows Dateien im Cache für die Offline-Dateien im Hintergrund alle zwei Stunden. Um diesen Wert ändern, verwenden Sie die Einstellung **Hintergrund-Synchronisierung konfigurieren** .

## Weitere Informationen

* [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
* [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)