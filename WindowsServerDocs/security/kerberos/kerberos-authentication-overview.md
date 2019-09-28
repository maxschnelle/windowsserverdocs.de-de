---
title: Kerberos Authentication Overview
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 646c6309-e865-4be2-b415-44dd125af5c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 33712dc8502035bd9e47e1d2bdd4583eb8347dec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386308"
---
# <a name="kerberos-authentication-overview"></a>Kerberos Authentication Overview

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Kerberos ist ein Authentifizierungsprotokoll zur Überprüfung der Identität eines Benutzers oder Hosts. Dieses Thema enthält Informationen zur Kerberos-Authentifizierung in Windows Server 2012 und Windows 8.

## <a name="BKMK_OVER"></a>Funktionsbeschreibung
Mit dem Betriebssystem Windows Server werden das Authentifizierungsprotokoll Kerberos, Version 5, sowie Erweiterungen für die Authentifizierung mit öffentlichen Schlüsseln, den Transport von Autorisierungsdaten und die Delegierung implementiert. Der Kerberos-Authentifizierungs Client wird als Security Support Provider \(ssp @ no__t-1 implementiert, und er kann über die Security Support Provider-Schnittstelle \(sspi @ no__t-3 aufgerufen werden. Die anfängliche Benutzerauthentifizierung ist in die Winlogon-Architektur mit einmaligem Anmelden @ no__t-0on integriert.

Der Kerberos-Schlüsselverteilungscenter \(kdc @ no__t-1 ist in andere Windows Server-Sicherheitsdienste integriert, die auf dem Domänen Controller ausgeführt werden. Der KDC verwendet die Active Directory Domain Services Datenbank der Domäne als Sicherheits Konten Datenbank. AD DS ist für Kerberos-Standardimplementierungen innerhalb der Domäne oder Gesamtstruktur erforderlich.

## <a name="kerb_tr_Kerb_Benefits"></a>Praktische Anwendungen
Die Vorteile der Verwendung von Kerberos für die Domäne @ no__t-0basierte Authentifizierung sind folgende:

-   **Delegierte Authentifizierung.**

    Dienste, die unter Windows-Betriebssystemen ausgeführt werden, können die Identität eines Client Computers annehmen, wenn Sie im Auftrag des Clients auf Ressourcen zugreifen. In vielen Fällen kann ein Dienst die Arbeit für den Client abschließen, indem er auf Ressourcen auf dem lokalen Computer zugreift. Wenn ein Clientcomputer sich beim Dienst authentifiziert, bieten das NTLM- und Kerberos-Protokoll die Autorisierungsinformationen, die ein Dienst benötigt, um lokal die Identität des Clientcomputers anzunehmen. Einige verteilte Anwendungen sind jedoch so konzipiert, dass ein Front @ no__t-0end-Dienst die Identität des Client Computers verwenden muss, wenn er eine Verbindung mit den Diensten von Back @ no__t-1End auf anderen Computern herstellt. Die Kerberos-Authentifizierung unterstützt einen Delegierungsmechanismus, der es einem Dienst ermöglicht, im Auftrag seines Clients zu fungieren, wenn eine Verbindung mit anderen Diensten hergestellt wird.

-   **Einmaliges Anmelden.**

    Mithilfe der Kerberos-Authentifizierung innerhalb einer Domäne oder Gesamtstruktur kann ein Benutzer oder Dienst auf Ressourcen mit der Erlaubnis von Administratoren auf Ressourcen zugreifen, ohne dass mehrere Anforderungen von Anmeldeinformationen erfolgen. Nach der ersten Anmeldung bei der Domäne über die Windows-Anmeldung verwaltet Kerberos die Anmeldeinformationen in der gesamten Gesamtstruktur, wenn ein Zugriff auf Ressourcen versucht wird.

-   **Interoper.**

    Die Implementierung des Kerberos V5-Protokolls von Microsoft basiert auf den Standards @ no__t-0track-Spezifikationen, die für die Internet Engineering Task Force \(ietf @ no__t-2 empfohlen werden. Bei Windows-Betriebssystemen schafft das Kerberos-Protokoll daher die Grundlage für die Interoperabilität mit anderen Netzwerken, in denen das Kerberos-Protokoll für die Authentifizierung verwendet wird. Darüber hinaus veröffentlicht Microsoft eine Windows-Protokolldokumentation zur Implementierung des Kerberos-Protokolls. In der Dokumentation sind die technischen Anforderungen, Einschränkungen, Abhängigkeiten und das Windows @ no__t-0specific-Protokoll Verhalten für die Microsoft-Implementierung des Kerberos-Protokolls enthalten.

-   **Effizientere Authentifizierung bei Servern.**

    Vor Kerberos konnte die NTLM-Authentifizierung verwendet werden, bei der ein Anwendungsserver eine Verbindung mit einem Domänencontroller herstellen muss, um jeden einzelnen Clientcomputer oder Dienst zu authentifizieren. Mit dem Kerberos-Protokoll ersetzen die Protokolle für die neuere Sitzung Pass @ no__t-0 durch Authentifizierung. Der Server muss nicht zu einem Domänen Controller \(wechseln, es sei denn, er muss ein Berechtigungs Attribut Zertifikat \(pac @ no__t-2 @ no__t-3 überprüfen. Stattdessen kann der Server den Clientcomputer authentifizieren, indem er vom Client vorgelegte Anmeldeinformationen untersucht. Clientcomputer können Anmeldeinformationen für einen bestimmten Server einmal erhalten und diese Anmeldeinformationen dann während einer Netzwerkanmeldesitzung wiederverwenden.

-   **Gegenseitige Authentifizierung.**

    Mithilfe des Kerberos-Protokolls kann ein Teilnehmer an einem der beiden Enden einer Netzwerkverbindung überprüfen, ob der Teilnehmer am anderen Ende die Entität ist, die er zu sein vorgibt. NTLM ermöglicht Clients nicht, die Identität eines Servers zu überprüfen oder einem Server zu ermöglichen, die Identität eines anderen Servers zu überprüfen. Die NTLM-Authentifizierung wurde für eine Netzwerkumgebung konzipiert, in die Echtheit der Server unterstellt wird. Das Kerberos-Protokoll geht nicht von derartigen Annahmen aus.

## <a name="see-also"></a>Siehe auch
[Windows-Authentifizierung: Übersicht](../windows-authentication/windows-authentication-overview.md)


