---
title: "Kerberos-Authentifizierung: Übersicht"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="kerberos-authentication-overview"></a>Kerberos-Authentifizierung: Übersicht

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Kerberos ist ein Authentifizierungsprotokoll, das zur Überprüfung der Identität eines Benutzers oder Hosts verwendet wird. Dieses Thema enthält Informationen zur Kerberos-Authentifizierung in Windows Server 2012 und Windows 8.

## <a name="BKMK_OVER"></a>Featurebeschreibung
Die Windows Server-Betriebssysteme implementieren das Kerberos V5-Authentifizierungsprotokoll und Erweiterungen für die Authentifizierung des öffentlichen Schlüssels, Transport von Autorisierungsdaten und die Delegierung. Implementiert die Kerberos-Authentifizierungsclient wird als Security Support Provider \(SSP\) und über die Security Support Provider Interface \(SSPI\) zugegriffen werden kann. Die Erstauthentifizierung von Benutzern ist in den Winlogon einzelne Standardparameter-Architektur integriert.

Die \(KDC\) Kerberos Key Distribution Center ist in andere Windows Server-Sicherheitsdienste integriert, die auf dem Domänencontroller ausgeführt werden. Das KDC verwendet die Active Directory-Domänendienste-Datenbank der Domäne als Sicherheitskontendatenbank. Active Directory-Domänendiensten ist für Kerberos-standardimplementierungen innerhalb der Domäne oder Gesamtstruktur erforderlich.

## <a name="kerb_tr_Kerb_Benefits"></a>In der Praxis
Bietet die folgenden mithilfe von Kerberos für Domäne\-basierte Authentifizierung Vorteile sind:

-   **Delegierte Authentifizierung.**

    Dienste, die auf Windows-Betriebssystemen ausgeführt werden können Identität eines Clientcomputers annehmen, beim Zugriff auf Ressourcen im Auftrag des Clients. In vielen Fällen kann ein Dienst seine Arbeit für den Client durch den Zugriff auf Ressourcen auf dem lokalen Computer abschließen. Wenn ein Clientcomputer mit dem Dienst authentifiziert, bieten NTLM- und Kerberos-Protokoll die Autorisierungsinformationen, die Dienst benötigt, um die Client-Computer lokal zu imitieren. Einige verteilten Anwendungen sehen jedoch so, dass ein Front\-End-Dienst des Clientcomputers Identität, beim Verbinden mit Back\-End-Diensten auf anderen Computern verwenden muss. Kerberos-Authentifizierung unterstützt einen delegierungsmechanismus, der einen Dienst, im Auftrag seines Clients zu fungieren, beim Verbinden mit anderen Diensten ermöglicht.

-   **Einmaliges Anmelden.**

    Mithilfe von Kerberos kann-Authentifizierung innerhalb einer Domäne oder in einer Gesamtstruktur ein Benutzer oder den Dienstleistungszugriff auf Ressourcen, die von Administratoren, ohne dass mehrere Anforderungen für Anmeldeinformationen zugelassen werden. Nach der ersten Anmeldung bei der Domäne über die Windows-Anmeldung verwaltet Kerberos die Anmeldeinformationen in der Gesamtstruktur, wenn, den Zugriff auf Ressourcen versucht wird.

-   **Interoperabilität.**

    Die Implementierung des Kerberos V5-Protokolls von Microsoft basiert auf Standards\-Track-Spezifikationen, die auf der Internet Engineering Task Force \(IETF\) empfohlen werden. In Windows-Betriebssystemen schafft das Kerberos-Protokoll daher eine Grundlage für die Interoperabilität mit anderen Netzwerken, in denen das Kerberos-Protokoll für die Authentifizierung verwendet wird. Darüber hinaus veröffentlicht Microsoft Windows-protokolldokumentation zur Implementierung des Kerberos-Protokolls. Die Dokumentation enthält die technischen Anforderungen, Einschränkungen, Abhängigkeiten und Windows-spezifischen Protokollverhalten für Microsoft Implementierung des Kerberos-Protokolls.

-   **Effizientere Authentifizierung bei Servern.**

    Vor Kerberos konnte die NTLM-Authentifizierung verwendet werden der erfordert, dass eines Anwendungsservers eine Verbindung mit einem Domänencontroller herstellen auf um jedem Clientcomputer oder Dienst zu authentifizieren. Ersetzen Sie mit dem Kerberos-Protokoll treten erneuerbare Sitzungstickets Pass\-through-Authentifizierung. Der Server ist nicht erforderlich, fahren Sie mit einem Domänencontroller \ (es sei denn, es muss ein \(PAC\)\) Recht Attribut Zertifikat zu überprüfen. Stattdessen kann der Server den Clientcomputer anhand der Anmeldeinformationen, die vom Client authentifizieren. Clientcomputer können Anmeldeinformationen für einen bestimmten Server einmal erhalten, und klicken Sie dann diese Anmeldeinformationen während einer netzwerkanmeldesitzung wiederverwenden.

-   **Gegenseitige Authentifizierung.**

    Mithilfe des Kerberos-Protokolls überprüfen ein Teilnehmer an beiden Enden einer Netzwerkverbindung, ob der Teilnehmer am anderen Ende die Entität, die er ist zu sein vorgibt. NTLM ist Clients zum Überprüfen der Identität eines Servers oder eines Servers zum Überprüfen der Identität eines anderen nicht möglich. NTLM-Authentifizierung wurde für eine Umgebung entwickelt, in der Server unterstellt wird. Das Kerberos-Protokoll geht nicht solche.

## <a name="see-also"></a>Siehe auch
[Windows-Authentifizierung: Übersicht](../windows-authentication/windows-authentication-overview.md)


