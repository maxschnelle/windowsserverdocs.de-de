---
title: Architektur der Windows-Authentifizierung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4a9deef6481c1f7dacb56e8166584de1c59d613c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403274"
---
# <a name="windows-authentication-architecture"></a>Architektur der Windows-Authentifizierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Übersichts Thema für IT-Experten erläutert das grundlegende architektonische Schema für die Windows-Authentifizierung.

Die Authentifizierung ist der Prozess, bei dem das System die Anmelde-oder Anmelde Informationen eines Benutzers überprüft. Der Name und das Kennwort eines Benutzers werden mit einer autorisierten Liste verglichen, und wenn das System eine Entsprechung erkennt, wird der Zugriff auf den in der Berechtigungs Liste für diesen Benutzer angegebenen Wert gewährt.

Im Rahmen einer erweiterbaren Architektur implementieren die Windows Server-Betriebssysteme einen Standardsatz von Authentifizierungs-Sicherheits Support Anbietern, darunter aushandeln, Kerberos-Protokoll, NTLM, Schannel (sicherer Kanal) und Digest. Die Protokolle, die von diesen Anbietern verwendet werden, ermöglichen die Authentifizierung von Benutzern, Computern und Diensten, und der Authentifizierungsprozess ermöglicht autorisierten Benutzern und Diensten, auf sichere Weise auf Ressourcen zuzugreifen.

In Windows Server authentifizieren Anwendungen Benutzer mithilfe der SSPI, um Aufrufe für die Authentifizierung zu abstrahieren. Daher müssen Entwickler die Komplexität spezifischer Authentifizierungsprotokolle nicht verstehen oder Authentifizierungsprotokolle in Ihren Anwendungen erstellen.

Windows Server-Betriebssysteme beinhalten eine Reihe von Sicherheitskomponenten, die das Windows-Sicherheitsmodell bilden. Diese Komponenten stellen sicher, dass Anwendungen keinen Zugriff auf Ressourcen ohne Authentifizierung und Autorisierung erhalten. In den folgenden Abschnitten werden die Elemente der Authentifizierungs Architektur beschrieben.

### <a name="local-security-authority"></a>Lokale Sicherheitsautorität
Bei der lokalen Sicherheits Autorität (Local Security Authority, LSA) handelt es sich um ein geschütztes Subsystem, das Benutzer authentifiziert und auf dem lokalen Computer anmeldet. Außerdem verwaltet LSA Informationen über alle Aspekte der lokalen Sicherheit auf einem Computer (diese Aspekte werden zusammen als lokale Sicherheitsrichtlinie bezeichnet). Außerdem werden verschiedene Dienste für die Übersetzung zwischen Namen und Sicherheits-IDs (SIDs) bereitstellt.

Das Sicherheits Subsystem verfolgt die Sicherheitsrichtlinien und die Konten, die sich auf einem Computersystem befinden, nach. Bei einem Domänen Controller sind diese Richtlinien und Konten diejenigen, die für die Domäne, in der sich der Domänen Controller befindet, wirksam sind. Diese Richtlinien und Konten werden in Active Directory gespeichert. Das LSA-Subsystem bietet Dienste zum Validieren des Zugriffs auf Objekte, zum Überprüfen von Benutzerrechten und zum Erstellen von Überwachungs Meldungen.

### <a name="security-support-provider-interface"></a>Security Support Provider-Schnittstelle
Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist die API, die integrierte Sicherheitsdienste für Authentifizierung, Nachrichten Integrität, Datenschutz von Nachrichten und Sicherheits Qualität für ein beliebiges verteiltes Anwendungsprotokoll erhält.

SSPI ist die Implementierung der Generic Security Service API (GSSAPI). SSPI bietet einen Mechanismus, mit dem eine verteilte Anwendung einen von mehreren Sicherheitsanbietern zum Abrufen einer authentifizierten Verbindung abrufen kann, ohne die Details des Sicherheitsprotokolls kennen zu müssen.

## <a name="see-also"></a>Siehe auch

-   [Architektur der Security Support Provider-Schnittstelle](security-support-provider-interface-architecture.md)

-   [Anmeldeinformationen-Prozesse in der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md)

-   [Windows-Authentifizierung: Technische Übersicht](https://technet.microsoft.com/library/dn169029.aspx)


