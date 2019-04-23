---
title: Bereichsnamen
description: Dieses Thema enthält eine Übersicht über die Verwendung von Bereichsnamen im Netzwerkrichtlinienserver-verbindungsanforderung, die Verarbeitung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d011eaad-f72a-4a83-8099-8589c4ee8994
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0257c4d15db4fc54e55ef430f6f2eea9cea2ec4d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882821"
---
# <a name="realm-names"></a>Bereichsnamen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


In diesem Thema können einen Überblick über die Verwendung von Bereichsnamen im Netzwerkrichtlinienserver verbindungsanforderungsverarbeitung.

Das Benutzernamen RADIUS-Attribut ist eine Zeichenfolge, die in der Regel einen Benutzerstandort für das Konto und einen Benutzernamen für das Konto enthält. Standort des Benutzers wird auch der Bereich oder einen Bereichsnamen genannt, und ist ein Synonym für das Konzept der Domäne sind, einschließlich DNS-Domänen, Active-Domänen und Windows NT 4.0-Domänen. Z. B. wenn ein Benutzerkonto in der Benutzerdatenbank für die Konten für eine Domäne mit dem Namen "Beispiel.com" befindet, ist "Beispiel.com" der Bereichsname.

Ein weiteres Beispiel, wenn das Benutzernamen RADIUS-Attribut den Benutzernamen enthält user1@example.com"user1" ist der Name des Benutzerkontos, und "Beispiel.com" besitzt den Bereichsnamen. Bereichsnamen können als ein Präfix oder Suffix im Benutzernamen angezeigt:

- **Example\user1**. In diesem Beispiel den Bereichsnamen **Beispiel** ist ein Präfix und kann auch den Namen des Active Directory&reg; Domänendienste \(AD DS\) Domäne.

- **user1@example.com**. In diesem Beispiel den Bereichsnamen **"example.com"** ist ein Suffix ein, und es ist entweder einen DNS-Domänennamen oder den Namen der AD DS-Domäne.

Können Sie sicherstellen, dass die verbindungsanforderungen von RADIUS-Clients, die so genannte Netzwerkzugriffsserver, an, die RADIUS-Server weitergeleitet werden Bereichsnamen in Verbindungsanforderungsrichtlinien beim Entwerfen und Bereitstellen von Ihrem RADIUS-Infrastruktur konfiguriert authentifizieren Sie und autorisieren Sie die verbindungsanforderung.

Wenn NPS als RADIUS-Server mit der Standard-Verbindungsanforderungsrichtlinie konfiguriert ist, verarbeitet der NPS verbindungsanforderungen für die Domäne, in dem die NPS-Mitglied ist, und bei vertrauenswürdigen Domänen.

Zum Konfigurieren von NPS als RADIUS-Proxy und Weiterleiten von verbindungsanforderungen an nicht vertrauenswürdigen Domänen fungieren, müssen Sie eine neue Verbindungsanforderungsrichtlinie erstellen. In der neue Verbindungsanforderungsrichtlinie müssen Sie das Benutzernamen-Attribut mit den Bereichsnamen konfigurieren, die im Benutzernamen Attribut der verbindungsanforderungen enthalten sein wird, die Sie weiterleiten möchten. Sie müssen auch die Verbindungsanforderungsrichtlinie mit einem remote-RADIUS-Servergruppe konfigurieren. Die Verbindungsanforderungsrichtlinie kann NPS zu berechnen, welche verbindungsanforderungen zum Weiterleiten an den RADIUS-Remoteservergruppe basierend auf der Realm-Abschnitt des User-Name-Attributs.

## <a name="acquiring-the-realm-name"></a>Erwerben den Bereichsnamen

Der Bereichsteil Name der Benutzername wird bereitgestellt, wenn Typen Kennwort-basierte die Anmeldeinformationen des Benutzers während einer Verbindung versuchen oder ein Verbindungs-Manager-CM-Profil auf dem Computer des Benutzers konfiguriert ist, um den Bereichsnamen automatisch bereitzustellen.

Sie können festlegen, dass Benutzer des Netzwerks die Bereichsnamen eingeben, bei der Eingabe ihrer Anmeldeinformationen während der Netzwerk-Verbindungsversuche.

Beispielsweise können Benutzer aufgefordert werden, geben Sie ihren Benutzernamen, einschließlich der Name des Benutzerkontos und der Bereichsname in **Benutzernamen** in die **Connect** Dialogfeld beim Herstellen eines DFÜ-Verbindung oder virtuelle private Netzwerks (VPN) die Verbindung.

Darüber hinaus, wenn Sie ein benutzerdefiniertes Dialing-Paket mit den Connection Manager-Verwaltungskit (CMAK) erstellen, unterstützen Sie Benutzer durch den Bereichsnamen automatisch hinzufügen, um den Benutzerkontonamen in den CM-Profilen, die auf Benutzercomputern installiert sind. Beispielsweise können Sie einen Bereich und der Benutzer die Namenssyntax, damit der Benutzer hat nur der Name des Benutzerkontos an, bei der Eingabe von Anmeldeinformationen in der CM-Profil angeben. In diesem Fall muss der Benutzer nicht kennen, oder speichern die Domäne, wo sich ihr Konto befindet.

Nachdem der Benutzer die Kennwort-basierte Anmeldeinformationen eingeben, wird der Benutzername während des Authentifizierungsprozesses aus dem Zugriffsclient an Network Access Server übergeben. Network Access Server konstruiert eine verbindungsanforderung und den Bereichsnamen im Benutzernamen ein RADIUS-Attribut enthält, in der Access-Request-Nachricht, die mit dem RADIUS-Proxy oder den Server gesendet wird.

Wenn der RADIUS-Server ein NPS ist, wird die Access-Request-Nachricht anhand des Satzes von konfigurierten Verbindungsanforderungsrichtlinien ausgewertet. Bedingungen für die Verbindungsanforderungsrichtlinie können es sich um die Spezifikation des Inhalts der User-Name-Attribut enthalten.

Sie können einen Satz von Verbindungsanforderungsrichtlinien konfigurieren, die für den Bereichsnamen im Benutzernamen Attribut der eingehenden Nachrichten gelten. Dadurch können Sie Routingregeln erstellen, die RADIUS-Nachrichten mit einem bestimmten Bereichsnamen auf einen bestimmten Satz von RADIUS-Server weiterleiten, wenn NPS als RADIUS-Proxy verwendet wird.

## <a name="attribute-manipulation-rules"></a>Attribut bearbeiten Regeln

Bevor die RADIUS-Nachricht wird entweder lokal verarbeitet (wenn NPS als RADIUS-Server verwendet wird) oder auf einen anderen RADIUS-Server (wenn NPS als RADIUS-Proxy verwendet wird) weitergeleitet, kann das Benutzernamen Attribut in der Nachricht durch Attribut Manipulation Regeln geändert werden. Sie können Attribut Manipulation-Regeln für das User-Name-Attribut konfigurieren, durch auswählen **Benutzernamen** auf die **Bedingungen** Registerkarte in den Eigenschaften einer Verbindungsanforderungsrichtlinie. NPS-Attribut bearbeiten Regeln verwenden die Syntax für reguläre Ausdrücke.

Sie können die Attribut-Manipulation-Regeln für das Attribut "Benutzername" So ändern Sie die folgenden konfigurieren:

- Entfernen Sie den Bereichsnamen aus dem Benutzernamen \(auch bekannt als Bereich entfernen\). Z. B. den Benutzernamen user1@example.com in "user1" geändert wird.

- Ändern Sie den Bereichsnamen, aber nicht die Syntax. Z. B. den Benutzernamen user1@example.com geändert wird, um user1@wcoast.example.com.

- Ändern Sie die Syntax des Bereichsnamens. Z. B. den Benutzer Name example\user1 geändert wird, um user1@example.com.

Nachdem der Benutzer-Name-Attribut gemäß den Regeln der Attribut-Bearbeitung, die Sie konfigurieren geändert wird, werden zusätzliche Einstellungen, der das erste übereinstimmende Verbindungsanforderungsrichtlinie verwendet, um zu bestimmen, ob:

- Der NPS verarbeitet die Access-Request-Nachricht, lokal (wenn NPS als RADIUS-Server verwendet wird).

- Der NPS leitet die Nachricht an einen anderen RADIUS-Server (wenn NPS als RADIUS-Proxy verwendet wird).

## <a name="configuring-the-nps-supplied-domain-name"></a>Konfigurieren der NPS-angegeben Domänennamens

Wenn der Benutzername nicht über einen Domänennamen enthält, stellt einen NPS bereit. Standardmäßig ist der NPS bereitgestellte Domänenname der Domäne, von der NPS Mitglied ist. Sie können die NPS-angegeben Domänennamens über die folgende registrierungseinstellung angeben:

    
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\RasMan\PPP\ControlProtocols\BuiltIn\DefaultDomain
    

>[!CAUTION]
>Durch eine fehlerhafte Bearbeitung der Registrierung können schwere Systemschäden verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

Einige nicht-Microsoft-Netzwerkzugriffsserver löschen oder ändern den Domänennamen, wie vom Benutzer angegeben. Infolgedessen wird die netzwerkanforderung für den Zugriff für die Standarddomäne authentifiziert, die möglicherweise nicht die Domäne für das Konto des Benutzers. Um dieses Problem zu beheben, konfigurieren Sie RADIUS-Server um den Benutzernamen in das richtige Format mit dem genauen Domänennamen zu ändern.
