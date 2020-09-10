---
title: 'Kennwörter: Übersicht'
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: 1b917691f931836605cfe044c725f5200925d2ca
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621885"
---
# <a name="passwords-overview"></a>Kennwörter: Übersicht

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Experten werden Kenn Wörter beschrieben, die in den Windows-Betriebssystemen verwendet werden, sowie Links zu Dokumentationen und Diskussionen über die Verwendung von Kenn Wörtern in einer Strategie zur Verwaltung von Anmelde Informationen.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Funktionsbeschreibung
Betriebssysteme und Anwendungen sind heute mit Kenn Wörtern entworfen, und auch wenn Sie Smartcards oder biometrische Systeme verwenden, haben alle Konten weiterhin Kenn Wörter und können in einigen Fällen weiterhin verwendet werden. Einige Konten, insbesondere Konten, die zum Ausführen von Diensten verwendet werden, können nicht einmal Smartcards und biometrische Token verwenden und müssen daher ein Kennwort für die Authentifizierung verwenden. Windows schützt Kenn Wörter mithilfe kryptografischer Hashes.

Weitere Informationen zu Windows-Kenn Wörtern finden Sie unter [Technische Übersicht](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh994558(v=ws.10))über Kenn Wörter.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
In Windows und vielen anderen Betriebssystemen ist die häufigste Methode zum Authentifizieren der Identität eines Benutzers die Verwendung einer geheimen Passphrase oder eines geheimen Kennworts. Zum Sichern Ihrer Netzwerkumgebung müssen von allen Benutzern sichere Kenn Wörter verwendet werden. Dadurch wird verhindert, dass böswillige Benutzer ein schwaches Kennwort erraten, ob durch manuelle Methoden oder mithilfe von Tools, um die Anmelde Informationen eines kompromittierten Benutzerkontos zu erhalten. Dies gilt insbesondere für Administrator Konten. Wenn Sie ein komplexes Kennwort regelmäßig ändern, verringert es die Wahrscheinlichkeit, dass ein Kenn Wort Angriff dieses Konto kompromittiert.

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
In Windows Server 2012 und Windows 8 sind Bild Kennwörter neu. Bild Kennwörter sind eine Kombination aus einem vom Benutzer ausgewählten Bild, das mit einer Reihe von Gesten verknüpft ist. Die Bild Kenn Wort Funktionalität ist auf Computern, die einer Domäne \- beigetreten sind Links zu weiteren Informationen zu Bild Kennwörtern finden Sie unter [Siehe auch](#BKMK_LINKS) weiter unten.

Die Kenn Wort Funktionalität in Windows Server 2012 und Windows 8 wurde nicht geändert. Es wurden keine neuen Gruppenrichtlinie Einstellungen hinzugefügt. Bei der Verwaltung von Anmelde Informationen und Kenn Wörtern wurden jedoch Verbesserungen und Verbesserungen vorgenommen \( \) , z. b. mit Bild Kennwörtern, dem Schließfach für Anmelde Informationen und der Anmeldung bei Windows 8 mit einer Microsoft-Konto, die zuvor als Windows Live ID bezeichnet wurde.

## <a name="deprecated-functionality"></a><a name="BKMK_DEP"></a>Veraltete Funktionen
In Windows Server 2012 und Windows 8 wurden keine Kenn Wort Funktionen als veraltet markiert.

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen
In Unternehmensumgebungen werden Kenn Wörter in der Regel mit Active Directory Domain Services verwaltet. Kenn Wörter können auch auf dem lokalen Computer mit den Einstellungen unter Lokale Sicherheitseinstellungen, Konto Richtlinien, Kenn Wort Richtlinie verwaltet werden.

## <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch
In dieser Tabelle werden zusätzliche Ressourcen für Kenn Wort Features, die Technologie und die Verwaltung von Anmelde Informationen aufgelistet.

|Inhaltstyp|Referenzen|
|--------|-------|
|**Dokumentation der Szenarien**|[Schutz Ihrer digitalen Identität](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**Vorgänge**|[Active Directory-Benutzer und -Computer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754217(v=ws.11))|
|**Problembehandlung**|[Ermitteln, wann Ihr Kennwort abläuft \- Active Directory PowerShell-Blog](https://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**Security**| [Leitfaden zu Bedrohungen und Gegenmaßnahmen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125920(v=ws.10)) für Windows Server 2008 R2 und Windows 7: Konto Richtlinien<p>Leitfaden zum [ändern und erstellen](https://www.microsoft.com/security/online-privacy/passwords-create.aspx) sicherer Kenn Wörter|
|**Tools und Einstellungen**|[Referenz zu Gruppenrichtlinie Einstellungen für Windows und Windows Server im Microsoft Download Center](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**Communityressourcen**|[Schutz Ihrer digitalen Identität](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<p>[Anmelden bei Windows 8 mit einer Windows Live ID](https://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<p>[Anmelden mit einem Bild Kennwort](/archive/blogs/b8/signing-in-with-a-picture-password)<p>[Optimieren der Bild Kenn Wort Sicherheit](/archive/blogs/b8/optimizing-picture-password-security)|