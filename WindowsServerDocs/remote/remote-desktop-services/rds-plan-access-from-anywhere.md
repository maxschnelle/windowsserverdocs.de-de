---
title: Remote Desktop Services - Zugriff von überall aus
description: Informationen zur Planung für eine RD-Gateway
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c38fab1-3586-4b7a-8bf0-7d85a8d5361d
author: lizap
ms.author: elizapo
ms.date: 11/03/2016
manager: dongill
ms.openlocfilehash: 2b10428ff90c50c4d7e113552ddda3cca5447b06
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845831"
---
# <a name="remote-desktop-services---access-from-anywhere"></a>Remote Desktop Services - Zugriff von überall aus

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Endbenutzer können auf interne Netzwerkressourcen sicher von außerhalb der Unternehmensfirewall über RD-Gateway verbinden.

Unabhängig davon, wie Sie die Desktops für Ihre Endbenutzer konfigurieren können Sie einfach das RD-Gateway in der Verbindung erforderlichen für eine schnelle, sichere Verbindung anschließen. Für Endbenutzer, die eine Verbindung über veröffentlichte Feeds können Sie die RD-Gateway-Eigenschaft konfigurieren, wie Sie die allgemeine Bereitstellungseigenschaften konfigurieren. Für Endbenutzer das Herstellen einer Verbindung über auf ihre Desktops geladen, ohne einen Feed können sie einfach den Namen des Hinweises mit den RD-Gateways als eine Verbindungseigenschaft hinzufügen, unabhängig davon, welche Remote Desktop-Client-Anwendung, die sie verwenden.

Die drei primären Aufgaben des RD-Gateways, in der Reihenfolge der Verbindungssequenz sind:
1. **Einrichten einen verschlüsselten SSL-Tunnel zwischen dem End-Gerät des Benutzers und dem RD-Gatewayserver**: Verbindungsherstellung über alle Remotedesktop-Gatewayserver, der RD-Gateway-Server muss ein Zertifikat installiert, die dem End-Gerät des Benutzers erkennt verfügen. In den Tests und Machbarkeitsstudien selbstsignierte Zertifikate können verwendet werden, aber nur öffentlich vertrauenswürdige Zertifikate von einer Zertifizierungsstelle in einer produktionsumgebung verwendet werden soll.
2. **Authentifizieren des Benutzers in der Umgebung**: Das RD-Gateway verwendet den Posteingang IIS-Dienst-Authentifizierung durchzuführen und können auch das RADIUS-Protokoll nutzen nutzen [Multi-Factor Authentication](rds-plan-mfa.md) Lösungen wie Azure MFA. Abgesehen von der Standard-Richtlinien erstellt haben können Sie erstellen zusätzliche Remotedesktop-Ressourcenautorisierungsrichtlinien (RD-RAPs) und RD-Verbindungsautorisierungsrichtlinien (RD-CAPs) um genauer zu definieren, welche Benutzer Zugriff haben sollen auf welche Ressourcen in die sichere Umgebung.
3. **Hin und her übertragen von Datenverkehr zwischen dem End-Gerät des Benutzers und die angegebene Ressource**: Das RD-Gateway wird für diese Aufgabe ausgeführt, solange die Verbindung hergestellt wurde fortgesetzt. Sie können verschiedene Timeouteigenschaften angeben, auf den RD-Gateway-Servern, um die Sicherheit der Umgebung zu verwalten, für den Fall, dass der Benutzer außerhalb des Geräts führt.

Sie finden weitere Informationen zu der Gesamtarchitektur einer Remote Desktop Services-Bereitstellung [in das desktophosting-Referenzarchitektur](desktop-hosting-reference-architecture.md).