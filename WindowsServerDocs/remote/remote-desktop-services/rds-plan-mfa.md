---
title: Remotedesktopdienste – Mehrstufige Authentifizierung
description: Informationen zur Planung für die Verwendung von MFA mit RDS.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 09ea784e-5644-417a-a3d9-bdbcebc313f9
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: c46ad24c62510b4a100a89b5c10a8f52c1a66151
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857353"
---
# <a name="remote-desktop-services---multi-factor-authentication"></a>Remotedesktopdienste – Mehrstufige Authentifizierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Nutzen Sie die Leistungsfähigkeit von Active Directory mit mehrstufiger Authentifizierung, um den Schutz Ihrer Unternehmensressourcen mit hoher Sicherheit durchzusetzen.

Für Ihre Endbenutzer, die eine Verbindung mit ihren Desktops und Anwendungen herstellen, ähnelt die Erfahrung der bisherigen Situation, wenn sie eine zweite Authentifizierungsmaßnahme ergreifen, um sich mit der gewünschten Ressource zu verbinden:
- Starten einer Desktop- oder Remoteanwendung über eine RDP-Datei oder Remotedesktop-Clientanwendung
- Beim Herstellen einer Verbindung mit dem RD-Gateway für den sicheren Remotezugriff wird eine SMS oder eine MFA-Abfrage für eine mobile App empfangen
- Ordnungsgemäße Authentifizierung und Verbindung mit der erforderlichen Ressource

Weitere Informationen zum Konfigurationsprozess finden Sie unter [Integrieren Sie Ihre Remotedesktopgateway-Infrastruktur mit der Netzwerkrichtlinienserver-Erweiterung (Network Policy Server, NPS) und Azure AD](https://docs.microsoft.com/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway).
