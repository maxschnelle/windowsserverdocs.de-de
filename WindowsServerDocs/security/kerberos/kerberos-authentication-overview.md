---
title: Kerberos Authentication Overview
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9f8878fb959c34663b1e1f3858fa7e0b6e7b6105
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824111"
---
# <a name="kerberos-authentication-overview"></a>Kerberos Authentication Overview

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Kerberos ist ein Authentifizierungsprotokoll zur Überprüfung der Identität eines Benutzers oder Hosts. Dieses Thema enthält Informationen zur Kerberos-Authentifizierung in Windows Server 2012 und Windows 8.

## <a name="BKMK_OVER"></a>Featurebeschreibung
Mit dem Betriebssystem Windows Server werden das Authentifizierungsprotokoll Kerberos, Version 5, sowie Erweiterungen für die Authentifizierung mit öffentlichen Schlüsseln, den Transport von Autorisierungsdaten und die Delegierung implementiert. Die Kerberos-Authentifizierungsclient wird als Security Support Provider implementiert \(SSP\), und darauf über die Security Support Provider Interface \(SSPI\). Die Erstauthentifizierung von Benutzern ist das einmaligen Anmelden von Windows-Anmeldung integriert\-Architektur.

Das Kerberos-Schlüsselverteilungscenter \(KDC\) integriert ist, in andere Sicherheitsdienste für Windows Server, die auf dem Domänencontroller ausgeführt werden. Das KDC verwendet die Active Directory Domain Services-Datenbank der Domäne als Sicherheitskontendatenbank. AD DS ist für Kerberos-Standardimplementierungen innerhalb der Domäne oder Gesamtstruktur erforderlich.

## <a name="kerb_tr_Kerb_Benefits"></a>Praktische Anwendungen
Die Vorteile erzielt werden, mithilfe von Kerberos für Domäne\-Authentifizierung sind:

-   **Delegierte Authentifizierung.**

    Dienste, die auf Windows-Betriebssystemen ausgeführt können auf einen Clientcomputer imitieren, beim Zugriff auf Ressourcen im Auftrag des Clients. In vielen Fällen kann ein Dienst die Arbeit für den Client abschließen, indem er auf Ressourcen auf dem lokalen Computer zugreift. Wenn ein Clientcomputer sich beim Dienst authentifiziert, bieten das NTLM- und Kerberos-Protokoll die Autorisierungsinformationen, die ein Dienst benötigt, um lokal die Identität des Clientcomputers anzunehmen. Allerdings sind einige verteilten Anwendungen ausgelegt, damit ein-Front-\-End-Dienst muss der Clientcomputer die Identität verwenden beim Herstellen einer zum Sichern Verbindung\-end-Diensten auf anderen Computern. Die Kerberos-Authentifizierung unterstützt einen Delegierungsmechanismus, der es einem Dienst ermöglicht, im Auftrag seines Clients zu fungieren, wenn eine Verbindung mit anderen Diensten hergestellt wird.

-   **Einmaliges Anmelden.**

    Mithilfe der Kerberos-Authentifizierung innerhalb einer Domäne oder Gesamtstruktur kann ein Benutzer oder Dienst auf Ressourcen mit der Erlaubnis von Administratoren auf Ressourcen zugreifen, ohne dass mehrere Anforderungen von Anmeldeinformationen erfolgen. Nach der ersten Anmeldung bei der Domäne über die Windows-Anmeldung verwaltet Kerberos die Anmeldeinformationen in der gesamten Gesamtstruktur, wenn ein Zugriff auf Ressourcen versucht wird.

-   **Die Interoperabilität.**

    Die Implementierung des Kerberos V5-Protokolls von Microsoft basiert auf Standards\-Nachverfolgen von Spezifikationen, die auf der Internet Engineering Task Force empfohlen werden \(IETF\). Bei Windows-Betriebssystemen schafft das Kerberos-Protokoll daher die Grundlage für die Interoperabilität mit anderen Netzwerken, in denen das Kerberos-Protokoll für die Authentifizierung verwendet wird. Darüber hinaus veröffentlicht Microsoft eine Windows-Protokolldokumentation zur Implementierung des Kerberos-Protokolls. Die Dokumentation enthält, die technischen Anforderungen, Einschränkungen, Abhängigkeiten und Windows\-spezifischen Protokollverhalten für die Microsoft Implementierung des Kerberos-Protokolls.

-   **Effizientere Authentifizierung bei Servern.**

    Vor Kerberos konnte die NTLM-Authentifizierung verwendet werden, bei der ein Anwendungsserver eine Verbindung mit einem Domänencontroller herstellen muss, um jeden einzelnen Clientcomputer oder Dienst zu authentifizieren. Ersetzen Sie durch das Kerberos-Protokoll treten erneuerbare Sitzungstickets Pass\-über die Authentifizierung. Der Server ist nicht erforderlich, wechseln Sie zu einem Domänencontroller \(es sei denn, es ein Privileg Attribut Zertifikat überprüfen muss \(PAC\)\). Stattdessen kann der Server den Clientcomputer authentifizieren, indem er vom Client vorgelegte Anmeldeinformationen untersucht. Clientcomputer können Anmeldeinformationen für einen bestimmten Server einmal erhalten und diese Anmeldeinformationen dann während einer Netzwerkanmeldesitzung wiederverwenden.

-   **Gegenseitige Authentifizierung.**

    Mithilfe des Kerberos-Protokolls kann ein Teilnehmer an einem der beiden Enden einer Netzwerkverbindung überprüfen, ob der Teilnehmer am anderen Ende die Entität ist, die er zu sein vorgibt. NTLM ist Clients die Identität eines Servers zu überprüfen, oder aktivieren einen Server zum Überprüfen der Identität eines anderen nicht möglich. Die NTLM-Authentifizierung wurde für eine Netzwerkumgebung konzipiert, in die Echtheit der Server unterstellt wird. Das Kerberos-Protokoll geht nicht von derartigen Annahmen aus.

## <a name="see-also"></a>Siehe auch
[Übersicht über die Windows-Authentifizierung](../windows-authentication/windows-authentication-overview.md)


