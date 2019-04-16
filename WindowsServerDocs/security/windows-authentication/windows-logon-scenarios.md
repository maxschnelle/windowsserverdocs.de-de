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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="windows-logon-scenarios"></a>Windows-Anmeldeszenarios

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Referenzthema für IT-Experten werden allgemeine Windows-Anmeldung und anmeldeszenarien zusammengefasst.

Windows-Betriebssysteme müssen alle Benutzer melden Sie sich bei dem Computer mit einem gültigen Konto für den Zugriff auf lokale und Netzwerkressourcen. Windows-basierte Computer Sichern von Ressourcen durch die Implementierung des Anmeldevorgangs, in dem Benutzer authentifiziert werden. Nachdem ein Benutzer authentifiziert wurde, implementieren Autorisierung und Technologien zum kontrollieren die zweite Phase des Ressourcenschutzes: bestimmen, ob der authentifizierte Benutzer berechtigt ist, auf eine Ressource zuzugreifen.

Der Inhalt dieses Themas gilt für Versionen von Windows in der **gilt für** -Liste am Anfang dieses Themas.

Darüber hinaus können Anwendungen und Dienste müssen Benutzer anmelden, um die Ressourcen zugreifen, die von der Anwendung oder ein Dienst angeboten werden. Der Anmeldevorgang ähnelt den Anmeldevorgang, ein gültiges Konto und die richtigen Anmeldeinformationen erforderlich sind, aber Anmeldeinformationen werden in der Datenbank (Security Account Manager, SAM) auf dem lokalen Computer und in Active Directory gespeichert, sofern zutreffend. Anmeldung Konto- und Anmeldeinformationen erfolgt durch die Anwendung oder den Dienst, und optional kann lokal gespeichert werden im Schließfach für Anmeldeinformationen.

Zum Verständnis der Funktionsweise der Authentifizierung finden Sie unter [Windows-Authentifizierungskonzepte](windows-authentication-concepts.md).

In diesem Thema werden die folgenden Szenarien beschrieben:

-   [Interaktive Anmeldung](#BKMK_InteractiveLogon)

-   [Netzwerkanmeldung](#BKMK_NetworkLogon)

-   [Smartcard-Anmeldung](#BKMK_SmartCardLogon)

-   [Biometrische Anmeldung](#BKMK_BioLogon)

## <a name="BKMK_InteractiveLogon"></a>Interaktive Anmeldung
Die Anmeldung beginnt, wenn ein Benutzer im Dialogfeld Anmeldeinformationen Eintrag Anmeldeinformationen eingibt oder wenn der Benutzer eine Smartcard in den Smartcardleser oder wenn der Benutzer, eine biometrische Geräte interagiert. Benutzer können eine interaktive Anmeldung mithilfe eines lokalen Benutzerkontos oder ein Domänenkonto anmelden an einem Computer ausführen.

Das folgende Diagramm zeigt die interaktive Anmeldung Elemente und die Anmeldung.

![Das Diagramm zeigt die interaktive Anmeldung Elemente und die Anmeldung](../media/windows-logon-scenarios/AuthN_LSA_Architecture_Client.gif)

**Windows Client – Authentifizierungsarchitektur**

### <a name="BKMK_LocaDomainLogon"></a>Lokale Benutzerkonten und Anmeldung
Anmeldeinformationen, die der Benutzer für eine domänenanmeldung zeigt enthalten alle Elemente, die für eine lokale Anmeldung, z.B. von Kontonamen und das Kennwort oder Zertifikat sowie Informationen zur Active Directory-Domäne erforderlich. Der Prozess bestätigt die Identifizierung des Benutzers auf die Sicherheitsdatenbank auf dem Computer des Benutzers lokale oder Active Directory-Domäne. Diese obligatorische Anmeldevorgang kann für Benutzer in einer Domäne deaktiviert werden.

Benutzer können eine interaktive Anmeldung an einem Computer auf zwei verschiedene Arten ausführen:

-   Lokal, hat der Benutzer beim direkten physischen Zugriff auf den Computer, oder wenn der Computer in einem Netzwerk von Computern ist.

    Eine lokale Anmeldung gewährt eine Benutzer die Berechtigung zum Zugriff auf Windows-Ressourcen auf dem lokalen Computer. Eine lokale Anmeldung erfordert, dass der Benutzer ein Benutzerkonto in der Sicherheitskontenverwaltung (SAM) auf dem lokalen Computer. Die Sicherheitskontenverwaltung schützt und verwaltet, Benutzer- und Gruppeninformationen in Form von Sicherheitskonten, die in der Registrierung des lokalen Computers gespeichert. Der Computer kann Zugriff auf das Netzwerk haben, aber es ist nicht erforderlich. Lokale Benutzerkonten und Gruppen Mitgliedschaft Benutzerinformationen wird verwendet, um den Zugriff auf lokale Ressourcen verwalten.

    Zur Anmeldung am Netzwerk gewährt eine Benutzer die Berechtigung Windows auf dem lokalen Computer sowie alle Ressourcen auf Computern im Netzwerk den Zugriff auf Ressourcen gemäß der Anmeldeinformation Zugriffstoken. Eine lokale Anmeldung und zur Anmeldung am Netzwerk erforderlich, dass der Benutzer ein Benutzerkonto in der Sicherheitskontenverwaltung (SAM) auf dem lokalen Computer. Lokale Benutzerkonten und Gruppen Mitgliedschaft Benutzerinformationen wird verwendet, um den Zugriff auf lokale Ressourcen zu verwalten, und das Zugriffstoken des Benutzers definiert, welche Ressourcen auf Computern im Netzwerk zugegriffen werden können.

    Eine lokale Anmeldung und zur Anmeldung am Netzwerk sind nicht ausreichend, um die Benutzer und Computer verwenden, um Zugriff auf und Domänenressourcen Berechtigung.

-   Remote qualifiziert über Terminaldienste oder Remotedesktopdienste (RDS), in dem Fall die Anmeldung Weitere ist als remote interaktive.

Nach einer interaktiven Anmeldung Windows Anwendungen im Auftrag des Benutzers ausgeführt, und dem Benutzer die Interaktion mit den betreffenden Anwendungen.

Eine lokale Anmeldung gewährt eine Benutzer die Berechtigung zum Zugriff auf Ressourcen auf dem lokalen Computer oder Ressourcen auf Computern im Netzwerk. Wenn der Computer einer Domäne angehört, versucht die Winlogon-Funktionalität für diese Domäne anmelden.

Eine domänenanmeldung gewährt einem Benutzer die Berechtigung für den lokalen Zugriff auf und Domänenressourcen. Eine domänenanmeldung erfordert, dass der Benutzer ein Benutzerkonto in Active Directory verfügt. Der Computer muss über ein Konto verfügen, in der Active Directory-Domäne und physisch mit dem Netzwerk verbunden sein. Benutzer benötigen auch die Benutzerrechte auf einem lokalen Computer oder einer Domäne anmelden. Domäne Benutzerkontoinformationen und Informationen zur Gruppenmitgliedschaft werden verwendet, um den Zugriff auf die Domäne und den lokalen Ressourcen verwalten.

### <a name="BKMK_RemoteLogon"></a>Remote-Anmeldung
In Windows stützt sich auf über Remote-Anmeldung auf einem anderen Computer zugreifen auf die RDP (Remotedesktopprotokoll). Da der Benutzer bereits erfolgreich an den Clientcomputer angemeldet haben muss, bevor Sie versuchen, eine Remoteverbindung, haben die interaktive Anmeldung Prozesse erfolgreich abgeschlossen.

RDP verwaltet die Anmeldeinformationen, die der Benutzer eingibt, mit dem Remotedesktopclient an. Diese Anmeldeinformationen für den Zielcomputer vorgesehen sind, und der Benutzer muss ein Konto auf dem Zielcomputer verfügen. Darüber hinaus muss der Zielcomputer konfiguriert werden, um eine Remoteverbindung zu übernehmen. Die Ziel-Computer-Anmeldeinformationen werden gesendet, um zu versuchen, den Authentifizierungsvorgang ausführen. Wenn die Authentifizierung erfolgreich ist, wird der Benutzer an lokale verbunden ist, und Netzwerkressourcen verfügbar sind mit den angegebenen Anmeldeinformationen.

## <a name="BKMK_NetworkLogon"></a>Netzwerkanmeldung
Zur Anmeldung am Netzwerk kann nur verwendet werden, nachdem die Benutzer, Dienst oder Computerauthentifizierung ausgeführt wurde. Bei der Anmeldung am Netzwerk wird der Prozess nicht die Anmeldeinformationen Eintrag Dialogfelder verwenden, zum Sammeln von Daten. In diesem Fall Anmeldeinformationen zuvor eingerichtet oder ein anderes Verfahren zum Sammeln von Anmeldeinformationen verwendet wird. Dieser Vorgang bestätigt die Identität des Benutzers einem Netzwerkdienst, die der Benutzer zugreifen möchte. Dieser Prozess wird in der Regel für den Benutzer nicht sichtbar, es sei denn, alternative Anmeldeinformationen bereitgestellt werden.

Um diese Art der Authentifizierung bereitzustellen, enthält das Sicherheitssystem Authentifizierungsmechanismen:

-   Kerberos V5-Protokoll

-   Zertifikate mit öffentlichem Schlüssel

-   Secure Sockets Layer/Transport Layer Security (SSL/TLS)

-   Digestauthentifizierung

-   NTLM für die Kompatibilität mit Microsoft Windows NT 4.0-basierte Systeme

Informationen zu den Elementen und Prozesse finden Sie im obigen Diagramm interaktive Anmeldung.

## <a name="BKMK_SmartCardLogon"></a>Smartcard-Anmeldung
Smartcards können verwendet werden, nur für Domänenkonten, keine lokalen Konten anmelden. Smartcard-Authentifizierung erfordert die Verwendung des Kerberos-Authentifizierungsprotokolls. Eingeführt in Windows2000 Server in Windows-Betriebssystemen eine public Key-Erweiterung der Kerberos-Protokolls anfängliche Authentifizierungsanforderung implementiert wird. Im Gegensatz zur freigegebenen Kryptografie mit geheimem Schlüssel Kryptografie mit öffentlichem Schlüssel asymmetrischen ist, zwei verschiedene Schlüssel werden benötigt, d.h.: eine zum Verschlüsseln, einen anderen entschlüsseln. Zusammen bilden die Schlüssel, die für beide Vorgänge erforderlich sind ein Paar aus privatem und öffentlichem Schlüssel.

Um eine normale Sitzung zu initiieren, muss ein Benutzer seine Identität nachweisen, durch Bereitstellen von Informationen, die nur für den Benutzer und die zugrunde liegende Infrastruktur des Kerberos-Protokoll bezeichnet. Die geheime Informationen ist ein freigegebener Kryptografieschlüssel das Kennwort des Benutzers abgeleitet. Ein gemeinsamen geheimer Schlüssel ist symmetrischen, was bedeutet, dass für die Ver- und Entschlüsselung derselbe Schlüssel verwendet wird.

Das folgende Diagramm zeigt die Elemente und Prozesse für die Smartcard-Anmeldung erforderlich.

![Das Diagramm zeigt die Elemente und Prozesse für die Smartcard-Anmeldung erforderlich](../media/windows-logon-scenarios/SmartCardCredArchitecture.gif)

**Smartcard-Anmeldeinformationsanbieter-Architektur**

Wenn eine Smartcard anstelle eines Kennworts verwendet wird, wird ein privates/öffentliches Schlüsselpaar auf Smartcard des Benutzers gespeichert für den gemeinsamen geheimen Schlüssel ersetzt, die von das Kennwort des Benutzers abgeleitet wird. Der private Schlüssel ist nur auf der Smartcard gespeichert. Der öffentliche Schlüssel kann für alle Personen zur Verfügung werden mit dem Besitzer vertrauliche Informationen austauschen möchte.

Weitere Informationen über die Smartcard-Anmeldung in Windows finden Sie unter [Funktionsweise Smartcard-Anmeldung in Windows](https://technet.microsoft.com/library/ff404285.aspx).

## <a name="BKMK_BioLogon"></a>Biometrische Anmeldung
Ein Gerät wird zum Erfassen und erstellen eine digitale Eigenschaft ein Artefakt bereit, z.B. ein Fingerabdruck verwendet. Diese digitalen Darstellung wird dann zum Beispiel für das gleiche Artefakt verglichen und Authentifizierung kann auftreten, wenn die beiden erfolgreich verglichen werden. Computer unter einem der Betriebssysteme in der **gilt für** Liste am Anfang dieses Themas kann konfiguriert werden, um diese Form der Anmeldung zu akzeptieren. Wenn biometrische Anmeldeinformationen nur für die lokale Anmeldung konfiguriert ist, muss der Benutzer jedoch Domänenanmeldeinformationen zu präsentieren, beim Zugriff auf Active Directory-Domäne.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
Informationen zur Verwaltung von Anmeldeinformationen, die während des Anmeldevorgangs in Windows finden Sie unter [Verwaltung von Anmeldeinformationen in Windows-Authentifizierung](https://technet.microsoft.com/library/dn169014.aspx).

[Windows-Anmeldung und Authentifizierung (technische Übersicht)](https://technet.microsoft.com/library/dn169029.aspx)


