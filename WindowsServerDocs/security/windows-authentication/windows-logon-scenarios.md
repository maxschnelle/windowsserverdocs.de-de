---
title: Windows-Anmeldeszenarios
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 66b7c568-67b7-4ac9-a479-a5a3b8a66142
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 3e3876680031cdb31f2fa3e6ce200efdf6fb5185
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936450"
---
# <a name="windows-logon-scenarios"></a>Windows-Anmeldeszenarios

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Referenz Thema für IT-Experten werden gängige Windows-Anmelde-und-Anmelde Szenarien zusammengefasst.

Die Windows-Betriebssysteme erfordern, dass sich alle Benutzer bei dem Computer mit einem gültigen Konto anmelden, um auf lokale und Netzwerkressourcen zuzugreifen. Auf Windows-basierten Computern werden Ressourcen durch Implementieren des Anmelde Prozesses, in dem die Benutzer authentifiziert werden, geschützt. Nachdem ein Benutzer authentifiziert wurde, implementieren Autorisierungs-und Zugriffs Steuerungstechnologien die zweite Phase des Schutzes von Ressourcen: ermitteln, ob der authentifizierte Benutzer für den Zugriff auf eine Ressource autorisiert ist.

Der Inhalt dieses Themas gilt für Windows-Versionen, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind.

Darüber hinaus können Anwendungen und Dienste erfordern, dass sich Benutzer anmelden, um auf die Ressourcen zuzugreifen, die von der Anwendung oder dem Dienst angeboten werden. Der Anmeldevorgang ähnelt dem Anmeldevorgang, da ein gültiges Konto und korrekte Anmelde Informationen erforderlich sind. Anmelde Informationen werden jedoch in der SAM-Datenbank (Security Account Manager) auf dem lokalen Computer und ggf. in Active Directory gespeichert. Anmelde Konto-und Anmelde Informationen werden von der Anwendung oder dem Dienst verwaltet und können optional lokal im Schließfach für Anmelde Informationen gespeichert werden.

Informationen zur Funktionsweise der Authentifizierung finden Sie unter [Konzepte der Windows-Authentifizierung](windows-authentication-concepts.md).

In diesem Thema werden folgende Szenarien beschrieben:

-   [Interaktive Anmeldung](#BKMK_InteractiveLogon)

-   [Netzwerk Anmeldung](#BKMK_NetworkLogon)

-   [Anmeldung mit Smartcards](#BKMK_SmartCardLogon)

-   [Biometrische Anmeldung](#BKMK_BioLogon)

## <a name="interactive-logon"></a><a name="BKMK_InteractiveLogon"></a>Interaktive Anmeldung
Der Anmeldevorgang beginnt entweder dann, wenn ein Benutzer Anmelde Informationen im Dialogfeld Anmelde Informationen eingibt, oder wenn der Benutzer eine Smartcard in den Smartcardleser einfügt oder wenn der Benutzer mit einem biometrischen Gerät interagiert. Benutzer können eine interaktive Anmeldung durchführen, indem Sie ein lokales Benutzerkonto oder ein Domänen Konto verwenden, um sich an einem Computer anzumelden.

Das folgende Diagramm zeigt die interaktiven Anmelde Elemente und den Anmeldevorgang.

![Diagramm mit den interaktiven Anmelde Elementen und dem Anmeldevorgang](../media/windows-logon-scenarios/AuthN_LSA_Architecture_Client.gif)

**Windows-Client – Authentifizierungsarchitektur**

### <a name="local-and-domain-logon"></a><a name="BKMK_LocaDomainLogon"></a>Lokale und Domänen Anmeldung
Die Anmelde Informationen, die der Benutzer für eine Domänen Anmeldung anzeigt, enthalten alle Elemente, die für eine lokale Anmeldung erforderlich sind, z. b. Konto Name, Kennwort oder Zertifikat und Active Directory Domänen Informationen. Der Prozess bestätigt die Identifizierung des Benutzers für die Sicherheitsdatenbank auf dem lokalen Computer des Benutzers oder einer Active Directory Domäne. Dieser obligatorische Anmeldevorgang kann nicht für Benutzer in einer Domäne ausgeschaltet werden.

Benutzer können auf zwei Arten eine interaktive Anmeldung an einem Computer ausführen:

-   Lokal, wenn der Benutzer direkten physischen Zugriff auf den Computer hat oder wenn der Computer zu einem Netzwerk von Computern gehört.

    Eine lokale Anmeldung gewährt einem Benutzer die Berechtigung für den Zugriff auf Windows-Ressourcen auf dem lokalen Computer. Eine lokale Anmeldung erfordert, dass der Benutzer über ein Benutzerkonto in der Sicherheits Konten Verwaltung (Security Accounts Manager, Sam) auf dem lokalen Computer verfügt. Sam schützt und verwaltet Benutzer-und Gruppeninformationen in Form von Sicherheits Konten, die in der lokalen Computer Registrierung gespeichert sind. Der Computer kann über Netzwerk Zugriff verfügen, ist jedoch nicht erforderlich. Informationen zu lokalen Benutzerkonten und Gruppenmitgliedschaften werden verwendet, um den Zugriff auf lokale Ressourcen zu verwalten.

    Bei einer Netzwerk Anmeldung wird dem Benutzer die Berechtigung zum Zugriff auf Windows-Ressourcen auf dem lokalen Computer zusätzlich zu allen Ressourcen auf vernetzten Computern erteilt, die durch das Zugriffs Token der Anmelde Informationen definiert werden. Sowohl bei einer lokalen Anmeldung als auch bei einer Netzwerk Anmeldung ist es erforderlich, dass der Benutzer über ein Benutzerkonto im Sicherheits Konten Manager (Security Accounts Manager, Sam) auf dem lokalen Computer verfügt. Informationen zu lokalen Benutzerkonten und Gruppenmitgliedschaften werden verwendet, um den Zugriff auf lokale Ressourcen zu verwalten, und das Zugriffs Token für den Benutzer definiert, auf welche Ressourcen auf vernetzten Computern zugegriffen werden kann.

    Eine lokale Anmeldung und eine Netzwerk Anmeldung sind nicht ausreichend, um dem Benutzer und dem Computer die Berechtigung zum Zugriff auf und zur Verwendung von Domänen Ressourcen zu erteilen.

-   Remote, über Terminal Dienste oder Remotedesktopdienste (RDS). in diesem Fall wird die Anmeldung als Remote interaktiv qualifiziert.

Nach einer interaktiven Anmeldung führt Windows Anwendungen im Namen des Benutzers aus, und der Benutzer kann mit diesen Anwendungen interagieren.

Eine lokale Anmeldung gewährt einem Benutzer die Berechtigung für den Zugriff auf Ressourcen auf dem lokalen Computer oder auf Ressourcen auf vernetzten Computern. Wenn der Computer einer Domäne hinzugefügt wird, versucht die Winlogon-Funktion, sich bei dieser Domäne anzumelden.

Eine Domänen Anmeldung gewährt einem Benutzer die Berechtigung, auf lokale und Domänen Ressourcen zuzugreifen. Eine Domänen Anmeldung erfordert, dass der Benutzer über ein Benutzerkonto in Active Directory verfügt. Der Computer muss über ein Konto in der Active Directory Domäne verfügen und physisch mit dem Netzwerk verbunden sein. Benutzer müssen auch über die Benutzerrechte verfügen, um sich an einem lokalen Computer oder einer Domäne anzumelden. Informationen zu Domänen Benutzerkonten und Gruppenmitgliedschaften werden verwendet, um den Zugriff auf Domänen-und lokale Ressourcen zu verwalten.

### <a name="remote-logon"></a><a name="BKMK_RemoteLogon"></a>Remote Anmeldung
In Windows basiert der Zugriff auf einen anderen Computer über die Remote Anmeldung auf der Remotedesktopprotokoll (RDP). Da sich der Benutzer vor dem Versuch, eine Remote Verbindung herzustellen, bereits erfolgreich am Client Computer angemeldet haben muss, wurden interaktive Anmeldevorgänge erfolgreich abgeschlossen.

RDP verwaltet die Anmelde Informationen, die der Benutzer mit dem Remotedesktop-Client eingibt. Diese Anmelde Informationen sind für den Zielcomputer gedacht, und der Benutzer muss über ein Konto auf diesem Bereitstellungs Zielcomputer verfügen. Außerdem muss der Bereitstellungs Zielcomputer so konfiguriert sein, dass eine Remote Verbindung akzeptiert wird. Zum Versuch, den Authentifizierungsprozess auszuführen, werden die Anmelde Informationen des Ziel Computers gesendet. Wenn die Authentifizierung erfolgreich ist, wird der Benutzer mit lokalen Ressourcen und Netzwerkressourcen verbunden, auf die über die angegebenen Anmelde Informationen zugegriffen werden kann.

## <a name="network-logon"></a><a name="BKMK_NetworkLogon"></a>Netzwerk Anmeldung
Eine Netzwerk Anmeldung kann nur verwendet werden, nachdem eine Benutzer-, Dienst-oder Computer Authentifizierung stattfindet. Während der Netzwerk Anmeldung verwendet der Prozess nicht die Anmelde Informationen für die Anmelde Informationen, um Daten zu sammeln. Stattdessen werden zuvor festgelegte Anmelde Informationen oder eine andere Methode zum Sammeln von Anmelde Informationen verwendet. Bei diesem Vorgang wird die Identität des Benutzers an jeden Netzwerkdienst bestätigt, auf den der Benutzer zugreifen möchte. Dieser Prozess ist in der Regel für den Benutzer unsichtbar, es sei denn, es müssen alternative Anmelde Informationen angegeben werden.

Um diese Art der Authentifizierung bereitzustellen, umfasst das Sicherheitssystem die folgenden Authentifizierungsmechanismen:

-   Kerberos 5-Protokoll

-   Zertifikate für öffentliche Schlüssel

-   Secure Sockets Layer/Transport Layer Security (SSL/TLS)

-   Digest

-   NTLM für Kompatibilität mit Microsoft Windows NT 4,0-basierten Systemen

Informationen zu den Elementen und Prozessen finden Sie im obigen interaktiven Anmelde Diagramm.

## <a name="smart-card-logon"></a><a name="BKMK_SmartCardLogon"></a>Anmeldung mit Smartcards
Smartcards können verwendet werden, um sich ausschließlich bei Domänen Konten anzumelden, nicht bei lokalen Konten. Die Smartcard-Authentifizierung erfordert die Verwendung des Kerberos-Authentifizierungs Protokolls. In Windows 2000 Server eingeführt wurde, wird in Windows-basierten Betriebssystemen eine Erweiterung des öffentlichen Schlüssels für die anfängliche Authentifizierungsanforderung des Kerberos-Protokolls implementiert. Im Gegensatz zur Kryptografie mit dem gemeinsamen geheimen Schlüssel ist die Kryptografie mit öffentlichem Schlüssel asymmetrisch, d. h., es sind zwei verschiedene Schlüssel erforderlich: eine zum Verschlüsseln, eine andere zum Entschlüsseln. Die Schlüssel, die zum Ausführen beider Vorgänge erforderlich sind, bilden gemeinsame private/öffentliche Schlüsselpaare.

Um eine typische Anmelde Sitzung zu initiieren, muss ein Benutzer seine Identität nachweisen, indem er Informationen bereitstellt, die nur dem Benutzer und der zugrunde liegenden Kerberos-Protokoll Infrastruktur bekannt sind. Die geheimen Informationen sind ein kryptografischer, gemeinsam verwendeter Schlüssel, der aus dem Kennwort des Benutzers abgeleitet wurde. Ein gemeinsamer geheimer Schlüssel ist symmetrisch. Dies bedeutet, dass derselbe Schlüssel sowohl für die Verschlüsselung als auch für die Entschlüsselung verwendet wird.

Das folgende Diagramm zeigt die für die Smartcardanmeldung erforderlichen Elemente und Prozesse.

![Diagramm mit den Elementen und Prozessen, die für die Smartcard-Anmeldung erforderlich sind](../media/windows-logon-scenarios/SmartCardCredArchitecture.gif)

**Smartcard-Anmeldeanbieterarchitektur**

Wenn eine Smartcard anstelle eines Kennworts verwendet wird, wird ein privates/öffentliches Schlüsselpaar, das auf der Smartcard des Benutzers gespeichert ist, durch den gemeinsamen geheimen Schlüssel ersetzt, der aus dem Kennwort des Benutzers abgeleitet ist. Der private Schlüssel wird nur auf der Smartcard gespeichert. Der öffentliche Schlüssel kann allen Benutzern zur Verfügung gestellt werden, für die der Besitzer vertrauliche Informationen austauschen möchte.

Weitere Informationen zum Anmeldevorgang für Smartcards in Windows finden Sie unter [Funktionsweise der Smartcard-Anmeldung in Windows](https://technet.microsoft.com/library/ff404285.aspx).

## <a name="biometric-logon"></a><a name="BKMK_BioLogon"></a>Biometrische Anmeldung
Ein Gerät wird zum Erfassen und Erstellen eines digitalen Merkmals eines Artefakts verwendet, z. b. eines Fingerabdrucks. Diese digitale Darstellung wird dann mit einem Beispiel desselben Artefakts verglichen, und wenn die beiden erfolgreich verglichen werden, kann die Authentifizierung erfolgen. Computer mit einem der in der Liste **gilt für** am Anfang dieses Themas angegebenen Betriebssysteme können so konfiguriert werden, dass Sie diese Art der Anmeldung akzeptieren. Wenn die biometrische Anmeldung jedoch nur für die lokale Anmeldung konfiguriert ist, muss der Benutzer beim Zugriff auf eine Active Directory Domäne Domänen Anmelde Informationen darstellen.

## <a name="additional-resources"></a>Weitere Ressourcen
Informationen zur Verwaltung von Anmelde Informationen, die während der Anmeldung übermittelt werden, finden Sie unter [Verwaltung von Anmelde Informationen in der Windows-Authentifizierung](https://technet.microsoft.com/library/dn169014.aspx).

[Technische Übersicht zur Windows-Anmeldung und -Authentifizierung.](https://technet.microsoft.com/library/dn169029.aspx)


