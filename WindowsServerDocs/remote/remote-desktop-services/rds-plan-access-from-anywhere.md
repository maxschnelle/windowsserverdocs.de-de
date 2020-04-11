---
title: Remotedesktopdienste – ortsunabhängiger Zugriff
description: Informationen zur Planung für ein RD-Gateway
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 5c38fab1-3586-4b7a-8bf0-7d85a8d5361d
author: lizap
ms.author: elizapo
ms.date: 11/03/2016
manager: dongill
ms.openlocfilehash: fb0fddbe86c4c06280fdbe55f2f6a7f490a1340b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857393"
---
# <a name="remote-desktop-services---access-from-anywhere"></a>Remotedesktopdienste – ortsunabhängiger Zugriff

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Endbenutzer können über RD-Gateway sicher von außerhalb der Unternehmensfirewall eine Verbindung mit internen Netzwerkressourcen herstellen.

Unabhängig von der Konfiguration der Desktops für deine Endbenutzer kannst du einfach das RD-Gateway in den Verbindungsflow aufnehmen, um eine schnelle, sichere Verbindung zu ermöglichen. Für Endbenutzer, die eine Verbindung über veröffentlichte Feeds herstellen, kannst du die RD-Gatewayeigenschaft genauso konfigurieren wie die allgemeinen Bereitstellungseigenschaften. Endbenutzer, die ohne Feed eine Verbindung mit ihren Desktops herstellen, können einfach den Namen des RD-Gateways des Unternehmens als Verbindungseigenschaft hinzufügen. Dabei spielt es keine Rolle, welche Remotedesktop-Clientanwendung sie nutzen.

Die drei Hauptaufgaben des RD-Gateways (in der Reihenfolge der Verbindungssequenz) lauten wie folgt:
1. **Einrichten eines verschlüsselten SSL-Tunnels zwischen dem Gerät des Endbenutzers und dem RD-Gatewayserver:** Damit eine Verbindung über einen RD-Gatewayserver hergestellt werden kann, muss auf dem RD-Gatewayserver ein Zertifikat installiert sein, das vom Gerät des Endbenutzers erkannt wird. In Tests und Machbarkeitsstudien können selbstsignierte Zertifikate verwendet werden. In Produktionsumgebungen sollten jedoch nur öffentlich vertrauenswürdige Zertifikate von einer Zertifizierungsstelle zum Einsatz kommen.
2. **Authentifizieren des Benutzers in der Umgebung:** Das RD-Gateway verwendet den IIS-Posteingangsdienst für die Authentifizierung und kann sogar das RADIUS-Protokoll nutzen, um von Lösungen für die [mehrstufige Authentifizierung](rds-plan-mfa.md) (etwa Azure MFA) zu profitieren. Zusätzlich zu den erstellten Standardrichtlinien kannst du RD-Ressourcenautorisierungsrichtlinien (RD Resource Authorization Policies, RD RAPs) sowie RD-Verbindungsautorisierungsrichtlinien (RD Connection Authorization Policies, RD CAPs) erstellen, um genauer zu definieren, auf welche Ressourcen bestimmte Benutzer in der sicheren Umgebung zugreifen können.
3. **Hin- und Herübertragen von Datenverkehr zwischen dem Endbenutzergerät und der angegebenen Ressource:** Das RD-Gateway führt diese Aufgabe so lange aus, wie die Verbindung besteht. Du kannst verschiedene Timeouteigenschaften für die RD-Gatewayserver festlegen, um die Sicherheit der Umgebung zu gewährleisten, sollte sich der Benutzer vom Gerät entfernen.

Weitere Einzelheiten zur gesamten Architektur einer Remotedesktopdienste-Bereitstellung findest du unter [Referenzarchitektur für das Desktophosting](desktop-hosting-reference-architecture.md).