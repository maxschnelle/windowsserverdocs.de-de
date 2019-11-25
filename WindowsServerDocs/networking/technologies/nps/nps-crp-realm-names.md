---
title: Bereichsnamen
description: Dieses Thema bietet einen Überblick über die Verwendung von Bereichs Namen in der Netzwerk Richtlinien Server-Verbindungs Anforderungs Verarbeitung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d011eaad-f72a-4a83-8099-8589c4ee8994
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7f9c611b793df36c2e588b2fa099df4e5382194c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405471"
---
# <a name="realm-names"></a>Bereichsnamen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016


In diesem Thema finden Sie eine Übersicht über die Verwendung von Bereichs Namen in der Verbindungs Anforderungs Verarbeitung für Netzwerk Richtlinien Server.

Das RADIUS-Attribut für den Benutzernamen ist eine Zeichenfolge, die in der Regel einen Benutzerkonto Speicherort und einen Benutzerkonto Namen enthält. Der Speicherort des Benutzerkontos wird auch als Bereichs-oder Bereichs Name bezeichnet und ist mit dem Konzept der Domäne, einschließlich DNS-Domänen, Active Directory® Domänen und Windows NT 4,0-Domänen, gleichbedeutend. Wenn sich beispielsweise ein Benutzerkonto in der Benutzerkonten Datenbank für eine Domäne mit dem Namen example.com befindet, ist example.com der Bereichs Name.

Wenn das RADIUS-Attribut für den Benutzernamen beispielsweise den Benutzernamen user1@example.comenthält, ist user1 der Name des Benutzerkontos, und example.com ist der Bereichs Name. Bereichs Namen können als Präfix oder als Suffix im Benutzernamen angezeigt werden:

- " **Example\user1**". In diesem Beispiel ist das **Beispiel** für den Bereichs Namen ein Präfix. Außerdem handelt es sich um den Namen einer Active Directory&reg; Domänen Diensten \(AD DS\) Domäne.

- <strong>user1@example.com</strong>. In diesem Beispiel ist der Bereichs Name **example.com** ein Suffix. Dabei handelt es sich entweder um einen DNS-Domänen Namen oder den Namen einer AD DS Domäne.

Sie können in Verbindungs Anforderungs Richtlinien konfigurierte Bereichs Namen beim Entwerfen und Bereitstellen der RADIUS-Infrastruktur verwenden, um sicherzustellen, dass Verbindungsanforderungen von RADIUS-Clients, auch Netzwerk Zugriffs Server genannt, an RADIUS-Server weitergeleitet werden, die authentifizieren und autorisieren Sie die Verbindungsanforderung.

Wenn NPS als RADIUS-Server mit der standardmäßigen Verbindungs Anforderungs Richtlinie konfiguriert ist, verarbeitet NPS Verbindungsanforderungen für die Domäne, in der das NPS Mitglied ist, sowie für vertrauenswürdige Domänen.

Wenn Sie NPS als RADIUS-Proxy konfigurieren und Verbindungsanforderungen an nicht vertrauenswürdige Domänen weiterleiten möchten, müssen Sie eine neue Verbindungs Anforderungs Richtlinie erstellen. In der neuen Verbindungs Anforderungs Richtlinie müssen Sie das User Name-Attribut mit dem Bereichs Namen konfigurieren, der im Benutzernamen Attribut der Verbindungsanforderungen enthalten ist, die Sie weiterleiten möchten. Außerdem müssen Sie die Verbindungs Anforderungs Richtlinie mit einer RADIUS-Remote Server Gruppe konfigurieren. Die Verbindungs Anforderungs Richtlinie ermöglicht NPS die Berechnung der Verbindungsanforderungen, die auf Grundlage des Bereichs Teils des Benutzernamen Attributs an die Remote-RADIUS-Server Gruppe weiterzuleiten sind.

## <a name="acquiring-the-realm-name"></a>Abrufen des Bereichs namens

Der Bereichs Namensteil des Benutzernamens wird bereitgestellt, wenn der Benutzer während eines Verbindungsversuchs Kenn Wort basierte Anmelde Informationen eingibt oder wenn ein Verbindungs-Manager-Profil auf dem Computer des Benutzers so konfiguriert ist, dass der Bereichs Name automatisch bereitgestellt wird.

Sie können festlegen, dass Benutzer Ihres Netzwerks ihren Bereichs Namen angeben, wenn Sie Ihre Anmelde Informationen während der Netzwerk Verbindungsversuche eingeben.

Beispielsweise können Sie festlegen, dass Benutzer ihren **Benutzernamen eingeben** müssen, einschließlich des Benutzerkonto namens und des Bereichs namens, wenn Sie eine DFÜ-oder VPN-Verbindung (virtuelles privates Netzwerk **) herstellen.**

Wenn Sie ein benutzerdefiniertes Einwählpaket mit dem Verbindungs-Manager-Verwaltungskit (CMAK) erstellen, können Sie Benutzer unterstützen, indem Sie dem Benutzerkonto Namen in cm-Profilen, die auf den Computern der Benutzer installiert sind, den Bereichs Namen automatisch hinzufügen. Beispielsweise können Sie einen Bereichs Namen und eine Benutzernamen Syntax im cm-Profil angeben, sodass der Benutzer nur den Benutzerkonto Namen angeben muss, wenn Anmelde Informationen eingegeben werden. In diesem Fall muss der Benutzer die Domäne, in der sich das Benutzerkonto befindet, nicht kennen oder merken.

Während des Authentifizierungs Vorgangs wird der Benutzername vom Zugriffs Client an den Netzwerk Zugriffs Server übermittelt, nachdem Benutzer ihre Kenn Wort basierten Anmelde Informationen eingeben. Der Netzwerk Zugriffs Server erstellt eine Verbindungsanforderung und schließt den Bereichs Namen innerhalb des RADIUS-Attributs für den Benutzernamen in die Access-Request-Nachricht ein, die an den RADIUS-Proxy oder-Server gesendet wird.

Wenn der RADIUS-Server ein NPS ist, wird die Access-Request-Nachricht anhand des Satzes konfigurierter Verbindungs Anforderungs Richtlinien ausgewertet. Bedingungen für die Verbindungs Anforderungs Richtlinie können die Spezifikation des Inhalts des Attributs "Benutzer Name" einschließen.

Sie können einen Satz von Verbindungs Anforderungs Richtlinien konfigurieren, die für den Bereichs Namen innerhalb des Benutzernamen Attributs eingehender Nachrichten spezifisch sind. Dadurch können Sie Routing Regeln erstellen, die RADIUS-Nachrichten mit einem bestimmten Bereichs Namen an einen bestimmten Satz von RADIUS-Servern weiterleiten, wenn NPS als RADIUS-Proxy verwendet wird.

## <a name="attribute-manipulation-rules"></a>Regeln für die Attribut Bearbeitung

Bevor die RADIUS-Nachricht entweder lokal verarbeitet wird (wenn NPS als RADIUS-Server verwendet wird) oder an einen anderen RADIUS-Server weitergeleitet wird (wenn NPS als RADIUS-Proxy verwendet wird), kann das Benutzernamens Attribut in der Nachricht mithilfe von Attribut Bearbeitungs Regeln geändert werden. Sie können Regeln für die Attribut Bearbeitung für das Attribut Benutzername konfigurieren, indem Sie in den Eigenschaften einer Verbindungs Anforderungs Richtlinie auf der Registerkarte **Bedingungen** den **Benutzernamen** auswählen. Regeln für die NPS-Attribut Bearbeitung verwenden Syntax für reguläre Ausdrücke.

Sie können Regeln für die Attribut Bearbeitung für das User-Name-Attribut konfigurieren, um Folgendes zu ändern:

- Entfernen Sie den Bereichs Namen aus dem Benutzernamen \(auch als Bereichs Entfernungs\)bezeichnet. Beispielsweise wird der Benutzername user1@example.com in user1 geändert.

- Ändern Sie den Bereichs Namen, aber nicht die Syntax. Beispielsweise wird der Benutzername user1@example.com in user1@wcoast.example.comgeändert.

- Ändern Sie die Syntax des Bereichs namens. Beispielsweise wird der Benutzername "example\user1" in "user1@example.com" geändert.

Nachdem das Attribut "Benutzer Name" gemäß den von Ihnen konfigurierten Attribut Bearbeitungs Regeln geändert wurde, werden zusätzliche Einstellungen der ersten übereinstimmenden Verbindungs Anforderungs Richtlinie verwendet, um zu bestimmen, ob:

- Der NPS verarbeitet die Access-Request-Nachricht lokal (wenn NPS als RADIUS-Server verwendet wird).

- Der NPS leitet die Nachricht an einen anderen RADIUS-Server weiter (wenn NPS als RADIUS-Proxy verwendet wird).

## <a name="configuring-the-nps-supplied-domain-name"></a>Konfigurieren des von NPS bereitgestellten Domänen Namens

Wenn der Benutzername keinen Domänen Namen enthält, stellt NPS einen bereit. Standardmäßig ist der von NPS bereitgestellte Domänen Name die Domäne, deren Mitglied der NPS ist. Sie können den NPS-bereitgestellten Domänen Namen mithilfe der folgenden Registrierungs Einstellung angeben:

    
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\RasMan\PPP\ControlProtocols\BuiltIn\DefaultDomain
    

>[!CAUTION]
>Durch eine fehlerhafte Bearbeitung der Registrierung können schwere Systemschäden verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

Einige Netzwerk Zugriffs Server, die nicht von Microsoft unterliegen, löschen oder ändern den Domänen Namen, wie er vom Benutzer angegeben wurde. Das Ergebnis ist, dass die Netzwerk Zugriffs Anforderung für die Standard Domäne authentifiziert wird, die möglicherweise nicht die Domäne für das Benutzerkonto ist. Um dieses Problem zu beheben, konfigurieren Sie die RADIUS-Server so, dass der Benutzername in das richtige Format mit dem genauen Domänen Namen geändert wird.
