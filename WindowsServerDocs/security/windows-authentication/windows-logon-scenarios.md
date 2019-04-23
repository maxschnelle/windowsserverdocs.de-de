---
title: Windows-Anmeldeszenarios
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66b7c568-67b7-4ac9-a479-a5a3b8a66142
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: d6a1d52bee3c2d14ea83ccb794ecea1872868df5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828181"
---
# <a name="windows-logon-scenarios"></a>Windows-Anmeldeszenarios

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Referenzthema für IT-Experten werden die allgemeinen Windows-Anmeldung und anmeldeszenarien zusammengefasst.

Die Windows-Betriebssysteme müssen alle Benutzer melden Sie sich bei dem Computer mit einem gültigen Konto für den Zugriff auf lokale Ressourcen und Netzwerkressourcen. Windows-Computern Sichern von Ressourcen durch die Implementierung des Anmeldevorgangs, in dem Benutzer authentifiziert werden. Nachdem ein Benutzer authentifiziert wurde, Autorisierung und Techniken zur Versionskontrolle implementieren Sie die zweite Phase des Ressourcenschutzes: bestimmen, ob der authentifizierte Benutzer autorisiert ist, auf eine Ressource zuzugreifen.

Den Inhalt der in diesem Thema gelten für Versionen von Windows in festgelegt die **gilt für** Liste am Anfang dieses Themas.

Darüber hinaus können Anwendungen und Dienste müssen Benutzer melden Sie sich auf diese Ressourcen zugreifen, die von der Anwendung oder Dienst angeboten werden. Der Anmeldeprozess ähnelt der Anmeldeprozess ein gültiges Konto und die richtigen Anmeldeinformationen erforderlich sind, jedoch die Anmeldeinformationen werden in der Datenbank (Security Account Manager, SAM) auf dem lokalen Computer und in Active Directory gespeichert, sofern zutreffend. Anmeldung Konto- und Anmeldeinformationen, die von der Anwendung oder Dienst verwaltet wird, und optional können lokal gespeichert werden im Schließfach für Anmeldeinformationen.

Funktionsweise der Authentifizierung finden Sie unter [Windows-Authentifizierungskonzepte](windows-authentication-concepts.md).

In diesem Thema wird beschrieben, die folgenden Szenarien:

-   [Interaktive Anmeldung](#BKMK_InteractiveLogon)

-   [Netzwerkanmeldung](#BKMK_NetworkLogon)

-   [Smartcard-Anmeldung](#BKMK_SmartCardLogon)

-   [Biometrische Anmeldung](#BKMK_BioLogon)

## <a name="BKMK_InteractiveLogon"></a>Interaktive Anmeldung
Der Anmeldeprozess beginnt, wenn ein Benutzer Anmeldeinformationen im Dialogfeld Anmeldeinformationen Eintrag eingibt oder, wenn der Benutzer eine Smartcard in den Smartcardleser einfügt oder wenn der Benutzer mit einem biometrischen Gerät interagiert. Benutzer können eine interaktive Anmeldung mit, dass ein lokales Benutzerkonto oder ein Domänenkonto auf einem Computer Anmelden ausführen.

Das folgende Diagramm zeigt die interaktive Anmeldung-Elemente und der Anmeldevorgang.

![Das Diagramm zeigt die interaktive Anmeldung-Elemente und der Anmeldevorgang](../media/windows-logon-scenarios/AuthN_LSA_Architecture_Client.gif)

**Windows Client – Authentifizierungsarchitektur**

### <a name="BKMK_LocaDomainLogon"></a>Lokale und Domänenprinzipale-Anmeldung
Anmeldeinformationen, die der Benutzer für eine domänenanmeldung vorweisen enthalten alle Elemente, die für eine lokale Anmeldung, z. B. Kontoname und das Kennwort oder Zertifikat sowie Informationen in Active Directory-Domäne erforderlich sind. Der Vorgang bestätigt die Identifizierung des Benutzers die Sicherheitsdatenbank auf dem lokalen Computer des Benutzers oder einer Active Directory-Domäne. Dieser erforderliche Anmeldevorgang kann nicht für Benutzer in einer Domäne deaktiviert werden.

Benutzer können eine interaktive Anmeldung an einem Computer auf zwei Arten ausführen:

-   Lokal, hat der Benutzer beim direkten physischen Zugriff auf dem Computer, oder wenn der Computer Teil eines Netzwerks der Computer ist.

    Eine lokale Anmeldung gewährt eine Benutzer die Berechtigung den Zugriff auf Windows-Ressourcen auf dem lokalen Computer. Eine lokale Anmeldung ist erforderlich, dass der Benutzer ein Benutzerkonto in den Security Accounts Manager (SAM) auf dem lokalen Computer verfügt. Das SAM schützt und verwaltet, Benutzer- und Gruppeninformationen in Form von Sicherheitskonten, die in der Registrierung des lokalen Computers gespeichert. Der Computer über das Netzwerk zugreifen kann, aber es ist nicht erforderlich. Lokale Benutzerkonten und-Gruppen Benutzermitgliedschaftsinformationen dient zum Verwalten des Zugriffs auf lokale Ressourcen.

    Zur Anmeldung am Netzwerk gewährt eine Benutzer die Berechtigung Windows auf dem lokalen Computer zusätzlich zu den Ressourcen auf vernetzten Computern den Zugriff auf Ressourcen gemäß der Anmeldeinformationen des Zugangs-Token. Sowohl eine lokale Anmeldung und zur Anmeldung am Netzwerk erfordern, dass der Benutzer ein Benutzerkonto in den Security Accounts Manager (SAM) auf dem lokalen Computer verfügt. Lokale Benutzerkonten und-Gruppen Benutzermitgliedschaftsinformationen dient zum Verwalten des Zugriffs auf lokale Ressourcen und das Zugriffstoken für den Benutzer definiert, welche Ressourcen auf vernetzten Computern zugegriffen werden können.

    Eine lokale Anmeldung und zur Anmeldung am Netzwerk sind nicht ausreichend zum Erteilen der Benutzer- und Computerobjekte Berechtigung den Zugriff auf und auf Domänenressourcen verwenden.

-   Remote vollqualifizierten über "Terminal Services" oder Remote Desktop Services (RDS), in dem Fall der Anmeldung weiter ist als remote interactive.

Nach einer interaktiven Anmeldung Windows Anwendungen im Auftrag des Benutzers ausgeführt, und der Benutzer mit den Anwendungen interagieren kann.

Eine lokale Anmeldung gewährt eine Benutzer die Berechtigung für den Zugriff auf Ressourcen auf dem lokalen Computer oder Ressourcen auf vernetzten Computern. Wenn der Computer einer Domäne angehört, versucht die Winlogon-Funktionalität für diese Domäne anmelden.

Eine domänenanmeldung gewährt einem Benutzer die Berechtigung auf lokalen und Domänenressourcen. Eine domänenanmeldung ist erforderlich, dass der Benutzer ein Benutzerkonto in Active Directory verfügt. Der Computer muss über ein Konto in Active Directory-Domäne verfügen und mit dem Netzwerk physisch verbunden sein. Benutzer müssen auch die Benutzerrechte zum Anmelden bei einem lokalen Computer oder eine Domäne verfügen. Informationen zum Domänenbenutzerkonto und Informationen zu Gruppenmitgliedschaften werden zum Verwalten des Zugriffs auf Domänen- und lokalen Ressourcen.

### <a name="BKMK_RemoteLogon"></a>Remoteanmeldung
In Windows stützt sich auf den Zugriff auf einen anderen Computer über remote-Anmeldung für das Remote Desktop Protocol (RDP). Da der Benutzer bereits erfolgreich auf dem Clientcomputer angemeldet haben muss, bevor Sie versuchen, eine Remoteverbindung, interaktive Anmeldung Prozesse erfolgreich abgeschlossen.

RDP werden die Anmeldeinformationen, die der Benutzer eingibt, mithilfe von Remote Desktop-Client verwaltet. Diese Anmeldeinformationen für den Zielcomputer vorgesehen sind, und der Benutzer muss ein Konto auf diesem Zielcomputer verfügen. Darüber hinaus muss der Zielcomputer konfiguriert werden, um eine Remoteverbindung zu akzeptieren. Die Ziel-Computer-Anmeldeinformationen werden gesendet, um zu versuchen, Sie führen den Authentifizierungsprozess. Wenn die Authentifizierung erfolgreich ist, wird der Benutzer auf den lokalen verbunden ist, und Netzwerkressourcen, die verfügbar sind, indem mithilfe der angegebenen Anmeldeinformationen.

## <a name="BKMK_NetworkLogon"></a>Netzwerkanmeldung
Zur Anmeldung am Netzwerk kann nur verwendet werden, nachdem der Benutzer, Computer oder Dienst-Authentifizierung stattgefunden hat. Während der Anmeldung am Netzwerk wird der Prozess nicht die Dialogfelder der Anmeldeinformationen-Eintrag verwendet, zum Sammeln von Daten. Stattdessen Anmeldeinformationen zuvor eingerichtet oder eine andere Methode zum Sammeln von Anmeldeinformationen verwendet wird. Dieser Prozess wird die Identität des Benutzers, dem Netzwerkdienst, der der Benutzer versucht, den Zugriff auf bestätigt. Dieser Prozess ist in der Regel für den Benutzer unsichtbar, es sei denn, Sie müssen alternative Anmeldeinformationen angegeben werden.

Um diese Art der Authentifizierung zu ermöglichen, enthält das Sicherheitssystem Authentifizierungsmechanismen:

-   Kerberos V5-Protokoll

-   Zertifikate mit öffentlichen Schlüsseln

-   Secure Sockets Layer/Transport Layer Security (SSL/TLS)

-   Digest

-   NTLM, für die Kompatibilität mit Microsoft Windows NT 4.0-basierte Systeme

Informationen zu den Elementen und -Prozesse finden Sie unter dem oben stehenden Diagramm für interaktive Anmeldung.

## <a name="BKMK_SmartCardLogon"></a>Smartcard-Anmeldung
Smartcards können nur für Domänenkonten, die nicht für lokale Konten anmelden verwendet werden. Smartcard-Authentifizierung erfordert die Verwendung des Kerberos-Authentifizierungsprotokolls. Eingeführt in Windows 2000 Server in Windows-basierten Betriebssystemen eine public Key-Erweiterung auf die ursprüngliche Authentifizierungsanforderung des Protokolls implementiert ist Kerberos. Im Gegensatz zu gemeinsamen geheimen Schlüsseln, Kryptografie mit öffentlichem Schlüssel asymmetrischen ist, also zwei verschiedene Schlüssel sind erforderlich: eine zum Verschlüsseln, ein weiteres zum Entschlüsseln. Zusammen bilden die Schlüssel, die beide Vorgänge durchführen müssen eine Private/öffentliche Schlüsselpaar.

Um einer typischen Sitzung zu initiieren, muss ein Benutzer seine Identität nachweisen, durch die Bereitstellung von Informationen, die nur für den Benutzer und die zugrunde liegende Infrastruktur von Kerberos-Protokoll bekannt. Die geheime Informationen ist eine kryptografische gemeinsam verwendeten Schlüssel, der das Kennwort des Benutzers abgeleitet. Ein gemeinsamen geheimer Schlüssel ist symmetrisch, was bedeutet, dass der gleiche Schlüssel für die Verschlüsselung und Entschlüsselung verwendet wird.

Das folgende Diagramm zeigt die Elemente und Prozesse, die für die Smartcard-Anmeldung.

![Das Diagramm zeigt die Elemente und Prozesse, die für die Smartcard-Anmeldung](../media/windows-logon-scenarios/SmartCardCredArchitecture.gif)

**Smartcard-anmeldeanbieterarchitektur**

Wenn eine Smartcard anstelle eines Kennworts verwendet wird, wird eine Private/öffentliche Schlüsselpaar auf Smartcard des Benutzers gespeichert für den gemeinsamen geheimen Schlüssel ersetzt, die von das Kennwort des Benutzers abgeleitet ist. Der private Schlüssel wird nur auf der Smartcard gespeichert. Der öffentliche Schlüssel kann verfügbar für jeden gemacht werden für die der Besitzer möchte vertrauliche Informationen austauschen.

Weitere Informationen über den Prozess des Smartcard-Anmeldung in Windows finden Sie unter [Funktionsweise Smartcard-Anmeldung in Windows](https://technet.microsoft.com/library/ff404285.aspx).

## <a name="BKMK_BioLogon"></a>Biometrische Anmeldung
Ein Gerät wird verwendet, um zu erfassen und erstellen ein digitales Merkmal eines Artefakts, z. B. ein Fingerabdruck. Diese digitalen Darstellung wird dann mit der ein Beispiel für dasselbe Element verglichen, und die Authentifizierung kann auftreten, wenn die beiden erfolgreich verglichen werden. Computer mit einem Betriebssystem, der festgelegt wird, der **gilt für** Liste am Anfang dieses Themas kann konfiguriert werden, um diese Form der Anmeldung zu akzeptieren. Wenn biometrische Anmeldung nur für die lokale Anmeldung konfiguriert ist, muss der Benutzer jedoch Anmeldeinformationen für die Domäne vorhanden, wenn Active Directory-Domäne den Zugriff auf.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
Informationen dazu, wie Windows beim Anmeldevorgang übermittelte Anmeldeinformationen verwaltet, finden Sie unter [Verwaltung von Anmeldeinformationen bei der Windows-Authentifizierung](https://technet.microsoft.com/library/dn169014.aspx).

[Windows-Anmeldung und Authentifizierung – technische Übersicht](https://technet.microsoft.com/library/dn169029.aspx)


