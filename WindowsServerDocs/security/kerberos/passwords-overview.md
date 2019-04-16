---
title: "Übersicht über Kennwörter"
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6c1b8d56b5c0da738e7dae5c0072be81040f90d8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="passwords-overview"></a>Übersicht über Kennwörter

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten beschreibt die Kennwörter in der Windows-Betriebssysteme und Links zu Dokumentationen und Diskussionen über die Verwendung von Kennwörtern in eine Strategie für die Anmeldeinformationen verwendet.

## <a name="BKMK_OVER"></a>Featurebeschreibung
Betriebssysteme und Anwendungen noch heute sind so konzipiert, um Kennwörter und auch bei Verwendung von Smartcards oder biometrische Systeme alle Konten weiterhin Kennwörter und sie können dennoch in einigen Fällen verwendet werden. Einige Konten, insbesondere für Konten verwendet, um die Dienste ausgeführt werden müssen können auch keine Smartcards und biometrische Token und daher ein Kennwort zur Authentifizierung. Windows schützt Kennwörter mit kryptografische Hashes.

Weitere Informationen zu Windows-Kennwörtern finden Sie unter [technische Übersicht über Kennwörter](https://technet.microsoft.com/library/hh994558(WS.10).aspx).

## <a name="BKMK_APP"></a>In der Praxis
Die häufigste Methode zum Authentifizieren der Identität eines Benutzers werden in Windows und viele andere Betriebssysteme eine geheime Passphrase oder ein Kennwort verwendet. Sichern Ihrer Netzwerkumgebung erfordert, dass alle Benutzer sichere Kennwörter verwendet werden. Dadurch vermeiden Sie die Bedrohung ein böswilliger Benutzer ein unsicheres Kennwort zu erraten, über manuelle Methoden oder mithilfe von Tools, um die Anmeldeinformationen eines gefährdeten Benutzerkontos zu erhalten. Dies gilt insbesondere für Administratorkonten. Wenn Sie ein komplexes Kennwort regelmäßig ändern, reduziert sich die Wahrscheinlichkeit einer Gefährdung dieses Konto Kennwortangriffs.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
In Windows Server2012 und Windows8 sind Bildcodes neu. Eine Kombination aus Benutzer ausgewähltes Bild mit einer Reihe von Gesten gekoppelt sind. Bild von Kennwörtern ist auf Domäne\ eingebundene Computer deaktiviert. Links zu weiteren Informationen zu Bildcodes in aufgelisteten [Siehe auch](#BKMK_LINKS) unten.

Es wurde keine Änderung der Kennwort-Funktionen in Windows Server2012 und Windows8. Keine neuen Gruppenrichtlinieneinstellungen es wurden hinzugefügt. Allerdings wurden Verbesserungen und Erweiterungen in der Verwaltung von Anmeldeinformationen \(and password\), vorgenommen, z.B. mit Bildcodes, das Schließfach für Anmeldeinformationen und Windows8 mit einem Microsoft-Konto anmelden, früher als eine Windows Live ID bezeichnet

## <a name="BKMK_DEP"></a>Veraltete Funktionen
Kein Kennwortfunktionalität ist in Windows Server2012 und Windows8 veraltet.

## <a name="BKMK_SOFT"></a>Anforderungen der Clientsoftware
In Unternehmen werden Kennwörter in der Regel in Active Directory-Domänendienste verwaltet. Kennwörter können auch auf dem lokalen Computer mit den Einstellungen in der lokalen Sicherheitsrichtlinie, Kontorichtlinien, Password Policy verwaltet werden.

## <a name="BKMK_LINKS"></a>Siehe auch
Diese Tabelle enthält zusätzliche Ressourcen für die Kennwort-Features, Technologie und Anmeldeinformationsverwaltung.

|Inhaltstyp|Verweise|
|--------|-------|
|**Szenario-Dokumentation**|[Schutz Ihrer digitalen Identität](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**Vorgänge**|[Active Directory-Benutzer und-Computer](https://technet.microsoft.com/library/cc754217.aspx)|
|**Problembehandlung**|[Hier erfahren Sie, wenn das Kennwort abgelaufen ist \-Active Directory-PowerShell-Teamblog](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**Sicherheit**| Windows Server2008 R2 und Windows7 [Handbuch zu Bedrohungen und Gegenmaßnahmen: Kontorichtlinien](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />Richtlinien, um die [ändern und Erstellen sicherer Kennwörter](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)|
|**Tools und Einstellungen**|[Referenz zu Gruppenrichtlinieneinstellungen für Windows und Windows Server auf dem Microsoft Download Center](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**Community-Ressourcen**|[Schutz Ihrer digitalen Identität](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Windows8 mit einer Windows Live ID anmelden](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[Anmelden mit einem Bildcode](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[Optimieren der Sicherheit der Bild-Kennwort](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


