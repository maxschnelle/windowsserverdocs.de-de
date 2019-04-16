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
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="windows-authentication-architecture"></a>Architektur der Windows-Authentifizierung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Übersichtsthema für IT-Experten wird erläutert, die grundlegende Architektur-Schema für Windows-Authentifizierung.

Authentifizierung ist der Prozess, mit dem das System die Anmeldung oder die Anmeldeinformationen eines Benutzers überprüft. Benutzername und Kennwort eines Benutzers werden mit einer autorisierten Liste verglichen, und wenn das System eine Übereinstimmung findet, wird Zugriff gewährt, in dem Umfang, in der Liste der Berechtigungen für diesen Benutzer angegeben.

Im Rahmen einer erweiterbaren Architektur implementieren Sie die Betriebssysteme Windows Server einen Standardsatz von Authentifizierung Security Support Provider, darunter Negotiate, Kerberos-Protokoll, NTLM, Schannel (sicherer Kanal) und Digest. Die Protokolle, die von diesen Anbietern verwendet ermöglichen die Authentifizierung von Benutzern, Computern und Diensten und der Authentifizierungsprozess ermöglicht autorisierten Benutzern und Diensten, Zugriff auf Ressourcen auf sichere Weise.

In Windows Server authentifizieren Anwendungen von Benutzern mithilfe der SSPI, um Aufrufe für die Authentifizierung zu abstrahieren. Daher müssen Entwickler nicht verstehen die Komplexität von bestimmten Authentifizierungsprotokolle oder Authentifizierungsprotokolle in ihre Programme erstellen.

Windows Server-Betriebssysteme enthalten eine Reihe von Sicherheitskomponenten, aus denen das Windows-Sicherheitsmodell besteht. Diese Komponenten stellen Sie sicher, dass die Anwendung auf Ressourcen ohne Authentifizierung und Autorisierung zugreifen können. Den folgenden Abschnitten werden die Elemente der authentifizierungsarchitektur.

### <a name="local-security-authority"></a>Local Security Authority
Local Security Authority (LSA) ist ein geschütztes Subsystem, das authentifiziert und Benutzer auf dem lokalen Computer anmeldet. LSA verwaltet außerdem Informationen zu allen Aspekten der lokalen Sicherheit auf einem Computer (diese Aspekte werden zusammen als die lokale Sicherheitsrichtlinie bezeichnet). Darüber hinaus verschiedene Dienste für die Übersetzung zwischen Namen und Sicherheits-IDs (SIDs).

Das Sicherheitssubsystem hält den Überblick über die Sicherheitsrichtlinien und die Konten, die auf einem Computer sind. Im Falle einer Domäne sind Domänencontroller, diese Richtlinien und Konten, die für die Domäne in Kraft sind in denen sich der Domänencontroller befindet. Diese Richtlinien und Konten werden in Active Directory gespeichert. Der LSA-Subsystem stellt Dienste zum Überprüfen der Zugriff auf Objekte, die Benutzerrechte überprüfen und die Generierung von Nachrichten überwachen.

### <a name="security-support-provider-interface"></a>Security Support Provider Interface
Die Security Support Provider-Schnittstelle (SSPI) ist die API, die integrierte Sicherheitsdienste für Authentifizierung, Nachrichtenintegrität, Datenschutz und Sicherheit Quality-of-Service für alle Protokolle der verteilten Anwendung erhält.

Die SSPI ist die Implementierung der Generic Security Service API (GSSAPI). SSPI bietet einen Mechanismus, mit dem eine verteilte Anwendung eine von mehreren Sicherheitsfunktionen, um eine authentifizierte Verbindung ohne Wissen der Detail des Sicherheitsprotokolls erhalten aufrufen kann.

## <a name="see-also"></a>Siehe auch

-   [Security Support Provider-Schnittstellenarchitektur](security-support-provider-interface-architecture.md)

-   [Anmeldeinformationen-Prozesse in der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md)

-   [Technische Übersicht über Windows-Authentifizierung](https://technet.microsoft.com/library/dn169029.aspx)


