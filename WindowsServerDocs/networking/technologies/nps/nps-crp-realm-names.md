---
title: Bereichsnamen
description: Dieses Thema enthält eine Übersicht über die Verwendung von Bereichsnamen in der Netzwerkrichtlinienserver-verbindungsanforderung Verarbeitung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d011eaad-f72a-4a83-8099-8589c4ee8994
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 29a835c9965c2115d0aac1ef9b704e05f430db8b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="realm-names"></a>Bereichsnamen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016


In diesem Thema können eine Übersicht über die Verwendung von Bereichsnamen im Netzwerkrichtlinienserver-verbindungsverarbeitung.

Den Benutzernamen ein RADIUS-Attribut ist eine Zeichenfolge, die in der Regel einem Benutzer Konto Speicherort und Namen eines Benutzerkontos enthält. Die Position des Benutzers Konto steht für den Bereich oder Bereichsnamen und ist gleichbedeutend mit dem Konzept der Domäne, einschließlich der DNS-Domänen, Active Directory® Domänen und Windows NT 4.0-Domänen. Z. B. wenn ein Benutzerkonto in der Benutzerkonten-Datenbank für eine Domäne mit dem Namen "Beispiel.com" befindet, ist "Beispiel.com" den Bereichsnamen ein.

Beispielsweise enthält das Benutzernamen ein RADIUS-Attribut der Benutzername user1@example.com, "user1" ist der Name des Benutzerkontos und "Beispiel.com" besitzt den Bereichsnamen ein. Bereichsnamen können in der Benutzername als Präfix oder als Suffix dargestellt werden:

- **Example\user1**. In diesem Beispiel den Bereichsnamen **Beispiel** ist ein Präfix; Sie ist auch der Name des Active Directory&reg; \(AD DS\)-Domänendiensten.

- **user1@example.com**. In diesem Beispiel den Bereichsnamen **example.com** ist ein Suffix; und entweder einen DNS-Domänennamen oder den Namen des AD DS-Domäne ist.

Sie können Bereichsnamen in Verbindungsanforderungsrichtlinien beim Entwerfen und Bereitstellen von RADIUS-Infrastruktur konfiguriert verwenden, um sicherzustellen, dass verbindungsanforderungen von RADIUS-Clients, die Abkürzung Netzwerkzugriffsserver für RADIUS-Server, die authentifizieren und autorisieren die verbindungsanforderung können weitergeleitet werden.

Wenn Sie NPS als RADIUS-Server mit der Standard-Verbindungsanforderungsrichtlinie konfiguriert ist, verarbeitet NPS verbindungsanforderungen für die Domäne, in dem der NPS-Server ein Mitglied und vertrauenswürdigen Domänen.

Zum Konfigurieren von NPS als RADIUS-Proxy und Weiterleitung von Verbindungsanfragen auf nicht vertrauenswürdigen Domänen fungieren, müssen Sie eine neue Verbindungsanforderungsrichtlinie erstellen. In die neue Verbindungsanforderungsrichtlinie müssen Sie den Benutzernamen ein Attribut mit den Bereichsnamen konfigurieren, die die Benutzer-Name-Attribut von verbindungsanforderungen enthalten sind, die Sie weiterleiten möchten. Sie müssen auch die Verbindungsanforderungsrichtlinie mit einem RADIUS-Remoteservergruppe konfigurieren. Die Verbindungsanforderungsrichtlinie kann NPS zu berechnen, welche verbindungsanforderungen an den RADIUS-Remoteservergruppe basierend auf den Bereich Teil der Benutzer-Name-Attribut weiterzuleiten.

## <a name="acquiring-the-realm-name"></a>Erfassen den Bereichsnamen

Der Bereich Teil des Benutzernamens wird bereitgestellt, wenn Typen Kennwort-basierte die Anmeldeinformationen des Benutzers während einer Verbindung versucht oder ein Manager Verbindungs-Profil auf dem Computer des Benutzers konfiguriert ist, um den Bereichsnamen automatisch bereitzustellen.

Sie können festlegen, dass Benutzer Ihres Netzwerks ihre Bereichsnamen angeben, bei der Eingabe ihrer Anmeldeinformationen bei Verbindungsversuchen Netzwerk.

Beispielsweise können Sie Benutzern, geben Sie ihren Benutzernamen ein, z. B. den Namen des Benutzerkontos und den Bereichsnamen benötigen **Benutzernamen** in der **verbinden** Dialogfeld beim Herstellen einer Verbindung DFÜ-Verbindung oder virtuelle private Netzwerk (VPN).

Darüber hinaus, wenn Sie benutzerdefinierte Wählen eines Pakets mit der Verbindung Manager-Verwaltungskit (CMAK erstellen) unterstützen Sie Benutzer durch den Bereichsnamen automatisch hinzufügen, um den Namen des Benutzerkontos in CM-Profile, die auf den Computern der Benutzer installiert werden. Beispielsweise können Sie eine Syntax Bereich und der Benutzer Namen, damit der Benutzer hat nur den Namen des Benutzerkontos an, bei der Eingabe von Anmeldeinformationen im Profil CM angeben. In diesem Fall muss der Benutzer nicht kennen oder die Domäne, in denen ihr Benutzerkonto ist, zu beachten.

Nach dem Benutzer ihre Anmeldeinformationen Kennwort-basierte eingeben, wird der Benutzername während des Authentifizierungsprozesses aus dem Zugriffsclient an Network Access Server übergeben. Network Access Server eine Anforderung der Verbindung erstellt und enthält den Bereichsnamen innerhalb der Benutzernamen ein RADIUS-Attribut in der Zugriffsanforderung Nachricht, die mit dem RADIUS-Proxy oder Server gesendet wird.

Wenn der RADIUS-Server einen NPS-Server ist, wird die Access-Anforderungsnachricht anhand der konfigurierten Verbindungsanforderungsrichtlinien ausgewertet. Bedingungen für die Verbindungsanforderungsrichtlinie können die Spezifikation des Inhalts der Benutzer-Name-Attribut enthalten.

Sie können eine Reihe von Verbindungsanforderungsrichtlinien konfigurieren, die für den Bereichsnamen innerhalb der Benutzer-Name-Attribut der eingehenden Nachrichten sind. Dadurch können Sie Routingregeln zu erstellen, die RADIUS-Nachrichten mit einem bestimmten Bereichsnamen auf eine bestimmte Gruppe von RADIUS-Server weiterleiten, wenn Sie NPS als RADIUS-Proxy verwendet wird.

## <a name="attribute-manipulation-rules"></a>Attribut Manipulation Regeln

Bevor die RADIUS-Meldung ist entweder lokal verarbeitet (wenn NPS als RADIUS-Server verwendet wird) oder an einen anderen RADIUS-Server (Wenn Sie NPS als RADIUS-Proxy verwendet wird) weitergeleitet, kann die Benutzer-Name-Attribut in der Meldung von Attribut Manipulation Regeln geändert werden. Sie können Attribut Manipulation Regeln für die Benutzer-Name-Attribut konfigurieren, durch die Auswahl **Benutzernamen** auf die **Bedingungen** Registerkarte in den Eigenschaften einer Verbindungsanforderungsrichtlinie. NPS-Attribut Manipulation Regeln verwenden Syntax regulärer Ausdrücke.

Sie können Attribut Manipulation Regeln für die Benutzer-Name-Attribut so ändern Sie die folgenden konfigurieren:

- Entfernen Sie den Bereichsnamen aus den Benutzernamen \ (auch bekannt als Bereich Stripping\). Z. B. den Benutzernamen user1@example.com auf "user1" geändert wird.

- Ändern Sie den Bereichsnamen jedoch nicht die Syntax. Z. B. den Benutzernamen user1@example.com geändert wurde user1@wcoast.example.com.

- Ändern Sie die Syntax für den Bereichsnamen ein. Z. B. die Benutzer Namen example\user1 geändert wurde user1@example.com.

Nachdem der Benutzer-Name-Attribut gemäß den Regeln des Attributs Manipulation, die Sie konfigurieren geändert wird, zusätzliche Einstellungen der ersten übereinstimmenden Verbindungsanforderungsrichtlinie wird bestimmt, ob:

- Der NPS-Server verarbeitet die Access-Anforderungsnachricht lokal (wenn NPS als RADIUS-Server verwendet wird).

- Der NPS-Server leitet die Nachricht an einen anderen RADIUS-Server (Wenn Sie NPS als RADIUS-Proxy verwendet wird).

## <a name="configuring-the-the-nps-supplied-domain-name"></a>Konfigurieren von dem der NPS-bereitgestellte Domänenname

Wenn der Benutzername keinen Domänennamen enthalten ist, stellt einen von NPS bereit. Standardmäßig ist der NPS-bereitgestellte Domänenname der Domäne, der der NPS-Server angehört. Sie können den NPS bereitgestellten Domänennamen über die folgende registrierungseinstellung angeben:

    
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\RasMan\PPP\ControlProtocols\BuiltIn\DefaultDomain
    

>[!CAUTION]
>Durch eine fehlerhafte Bearbeitung der Registrierungs kann schwere Systemschäden verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Daten auf dem Computer sichern.

Einige nicht-Microsoft-Netzwerkzugriffsserver löschen oder ändern den Domänennamen wie vom Benutzer angegeben. Folglich wird die Netzwerk-zugriffsanforderung für die Standarddomäne authentifiziert möglicherweise nicht der Domäne für das Konto des Benutzers. Um dieses Problem zu beheben, konfigurieren Sie Ihre RADIUS-Server, um den Benutzernamen in das richtige Format mit dem entsprechenden Domänennamen ändern.
