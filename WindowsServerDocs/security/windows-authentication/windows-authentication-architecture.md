---
title: Architektur der Windows-Authentifizierung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c9d6bb-9b03-407d-89b6-97c7551b256b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: fd6e2cbc233a91b62e3c8c9caf1154f91c3863ac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855861"
---
# <a name="windows-authentication-architecture"></a>Architektur der Windows-Authentifizierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Übersichtsthema für IT-Experten erläutert das grundlegende architektonische-Schema für die Windows-Authentifizierung.

Authentifizierung ist der Prozess, mit dem das System die Anmelde- oder die Anmeldeinformationen des Benutzers überprüft. Namen und das Kennwort eines Benutzers mit einer autorisierten Liste verglichen werden, und wenn das System eine Übereinstimmung erkannt wird, erhält Zugriff auf die in der Berechtigungsliste für diesen Benutzer angegeben.

Im Rahmen einer erweiterbaren Architektur implementieren die Windows-Betriebssysteme einen Standardsatz von Authentifizierung Security Support Provider, darunter Negotiate, Kerberos-Protokoll, NTLM, Schannel (sicherer Kanal) und Digest. Die von diesen Anbietern verwendeten Protokolle aktivieren der Authentifizierung von Benutzern, Computern und Diensten, und der Authentifizierungsprozess ermöglicht autorisierten Benutzern und Diensten auf sichere Weise den Zugriff auf Ressourcen.

In Windows Server authentifizieren Anwendungen von Benutzern mit, dass die SSPI um Aufrufe für die Authentifizierung zu abstrahieren. Daher müssen Entwickler nicht verstehen, die Komplexität der bestimmte Authentifizierungsprotokolle oder Authentifizierungsprotokolle in ihre Anwendungen zu erstellen.

Windows Server-Betriebssysteme enthalten eine Reihe von Sicherheitskomponenten, aus denen das Windows-Sicherheitsmodell. Diese Komponenten stellen Sie sicher, dass Anwendungen Zugriff auf Ressourcen ohne Authentifizierung und Autorisierung nicht möglich. Den folgenden Abschnitten werden die Elemente der authentifizierungsarchitektur.

### <a name="local-security-authority"></a>Lokale Sicherheitsautorität
Der Local Security Authority (LSA) ist ein geschütztes Subsystem, das authentifiziert und meldet sich der Benutzer auf dem lokalen Computer. Darüber hinaus behält LSA Informationen zu allen Aspekten der lokalen Sicherheitsgruppe auf einem Computer (diese Aspekte werden zusammenfassend als die lokale Sicherheitsrichtlinie bezeichnet). Darüber hinaus verschiedene Dienste für die Übersetzung zwischen den Namen und die Sicherheits-IDs (SIDs).

Das Subsystem für nachverfolgung von Sicherheitsrichtlinien und die Konten, die auf einem Computersystem sind. Im Fall einer Domäne sind die Controller, diese Richtlinien und die Konten, die für die Domäne in Kraft sind in denen sich der Domänencontroller befindet. Diese Richtlinien und die Konten werden in Active Directory gespeichert. Der LSA-Subsystem bietet Dienste für den Zugriff auf Objekte zu überprüfen, überwachungsmeldungen, die Benutzerrechte überprüfen und generieren.

### <a name="security-support-provider-interface"></a>Security Support Provider Interface
Die Security Support Provider Interface (SSPI) ist die API, die integrierte Sicherheitsdienste für Authentifizierung, Nachrichtenintegrität, Nachrichtendatenschutz und Sicherheit Quality-of-Service für jedes beliebige verteilte Anwendungsprotokoll erhält.

SSPI ist die Implementierung der Generic Security Service API (GSSAPI). SSPI bietet einen Mechanismus, mit dem eine verteilte Anwendung einen Sicherheitsanbieter zum Herstellen einer authentifizierten Verbindung ohne Kenntnisse der Details des Sicherheitsprotokoll für das aufrufen kann.

## <a name="see-also"></a>Siehe auch

-   [Sicherheitsarchitektur für die Schnittstelle von Support-Anbieter](security-support-provider-interface-architecture.md)

-   [Anmeldeinformationen-Prozesse bei der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md)

-   [Technische Übersicht über Windows-Authentifizierung](https://technet.microsoft.com/library/dn169029.aspx)


