---
title: 'Kennwörter: Übersicht'
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869601"
---
# <a name="passwords-overview"></a>Kennwörter: Übersicht

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema für IT-Experten wird beschrieben, Kennwörter, wie in der Windows-Betriebssystemen und Links zu Dokumentationen und Diskussionen über die Verwendung von Kennwörtern in einem Verwaltungsstrategie für Anmeldeinformationen verwendet.

## <a name="BKMK_OVER"></a>Featurebeschreibung
Betriebssysteme und Anwendungen noch heute in Bezug auf Kennwörter entworfen werden, und selbst bei Verwendung von Smartcards oder biometrische Systeme alle Konten haben weiterhin die Kennwörter, und sie können weiterhin in einigen Fällen verwendet werden. Einige Konten, insbesondere verwendet zum Ausführen von Diensten, Konten müssen können auch keine Smartcards und biometrischen Token und daher ein Kennwort um zu authentifizieren. Windows schützt Kennwörter mithilfe von kryptografischen Hashes.

Weitere Informationen zu Windows-Kennwörtern finden Sie unter [technische Übersicht über Kennwörter](https://technet.microsoft.com/library/hh994558(WS.10).aspx).

## <a name="BKMK_APP"></a>Praktische Anwendungen
Ist in Windows und vielen anderen Betriebssystemen die am häufigsten verwendete Methode zum Authentifizieren der Identität eines Benutzers eine geheime Passphrase oder ein Kennwort verwenden. Sichern Ihre Netzwerkumgebung erfordert, dass sichere Kennwörter von allen Benutzern verwendet werden. Dadurch wird die Bedrohung durch böswillige Benutzer Erraten von Kennwörtern ein unsicheres Kennwort, sei es durch manuelle Methoden oder mithilfe von Tools zum Abrufen der Anmeldeinformationen eines Kontos gefährdeter Benutzer zu vermeiden. Dies gilt insbesondere für Administratorkonten. Wenn Sie ein komplexes Kennwort regelmäßig ändern, reduziert es die Wahrscheinlichkeit eines Kennwortangriffs diesem Konto gefährden.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
In Windows Server 2012 und Windows 8 sind bildcodes neu. Bildcodes sind eine Kombination aus einem ausgewählten Benutzer-Image zusammen mit einer Reihe von Aktionen. Bild von Passwörtern für Domäne deaktiviert ist\-Computern eingebunden sind. Links zu weiteren Informationen über bildcodes finden Sie in [Siehe auch](#BKMK_LINKS) unten.

Es wurden keine Änderungen an der Kennwortfunktionalität in Windows Server 2012 und Windows 8. Keine neuen gruppenrichtlinieneinstellungen wurden hinzugefügt. Jedoch, Verbesserungen und Erweiterungen wurden in Anmeldeinformationen \(und das Kennwort\) Verwaltung, z. B. mit bildcodes zu blockieren, das Schließfach für Anmeldeinformationen und Anmelden bei Windows 8 mit einem Microsoft-Konto, früher als Windows Live ID bezeichnet .

## <a name="BKMK_DEP"></a>Veraltete Funktionen
Kein Kennwortfunktionalität wurde in Windows Server 2012 und Windows 8 als veraltet markiert.

## <a name="BKMK_SOFT"></a>Softwareanforderungen
In unternehmensumgebungen ausgeführt werden werden die Kennwörter in der Regel mit Active Directory Domain Services verwaltet. Kennwörter können auch auf dem lokalen Computer, die mit den Einstellungen in die lokale Kennwortrichtlinie für die Sicherheitseinstellungen für Richtlinien für Konten, verwaltet werden.

## <a name="BKMK_LINKS"></a>Siehe auch
Diese Tabelle enthält zusätzliche Ressourcen für Kennwortfunktionen, Technologie und anmeldeinformationsverwaltung.

|Inhaltstyp|Verweise|
|--------|-------|
|**Szenario-Dokumentation**|[Schutz Ihrer digitalen Identität](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**Betrieb**|[Active Directory-Benutzer und-Computer](https://technet.microsoft.com/library/cc754217.aspx)|
|**Problembehandlung**|[Erfahren Sie, wenn das Kennwort abgelaufen \- Active Directory-PowerShell-Blog](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**Sicherheit**| Windows Server 2008 R2 und Windows 7 [Handbuch zu Bedrohungen und Gegenmaßnahmen: Kontorichtlinien](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />Anleitungen zum [ändern und erstellen Sie sichere Kennwörter](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)|
|**Tools und Einstellungen**|[Referenz zu Gruppenrichtlinieneinstellungen für Windows und Windows-Server im Microsoft Download Center](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**Communityressourcen**|[Schutz Ihrer digitalen Identität](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Anmelden bei Windows 8 mit einer Windows Live ID](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[Anmelden mit bildcode](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[Optimieren der Bild-kennwortsicherheit](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


