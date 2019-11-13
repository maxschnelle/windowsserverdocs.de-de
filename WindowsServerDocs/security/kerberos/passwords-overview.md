---
title: 'Kennwörter: Übersicht'
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 27d456dd274b917233f0484f055b679dc8c73214
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403511"
---
# <a name="passwords-overview"></a>Kennwörter: Übersicht

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema für IT-Experten werden Kenn Wörter beschrieben, die in den Windows-Betriebssystemen verwendet werden, sowie Links zu Dokumentationen und Diskussionen über die Verwendung von Kenn Wörtern in einer Strategie zur Verwaltung von Anmelde Informationen.

## <a name="BKMK_OVER"></a>Funktionsbeschreibung
Betriebssysteme und Anwendungen sind heute mit Kenn Wörtern entworfen, und auch wenn Sie Smartcards oder biometrische Systeme verwenden, haben alle Konten weiterhin Kenn Wörter und können in einigen Fällen weiterhin verwendet werden. Einige Konten, insbesondere Konten, die zum Ausführen von Diensten verwendet werden, können nicht einmal Smartcards und biometrische Token verwenden und müssen daher ein Kennwort für die Authentifizierung verwenden. Windows schützt Kenn Wörter mithilfe kryptografischer Hashes.

Weitere Informationen zu Windows-Kenn Wörtern finden Sie unter [Technische Übersicht](https://technet.microsoft.com/library/hh994558(WS.10).aspx)über Kenn Wörter.

## <a name="BKMK_APP"></a>Praktische Anwendungen
In Windows und vielen anderen Betriebssystemen ist die häufigste Methode zum Authentifizieren der Identität eines Benutzers die Verwendung einer geheimen Passphrase oder eines geheimen Kennworts. Zum Sichern Ihrer Netzwerkumgebung müssen von allen Benutzern sichere Kenn Wörter verwendet werden. Dadurch wird verhindert, dass böswillige Benutzer ein schwaches Kennwort erraten, ob durch manuelle Methoden oder mithilfe von Tools, um die Anmelde Informationen eines kompromittierten Benutzerkontos zu erhalten. Dies gilt insbesondere für Administrator Konten. Wenn Sie ein komplexes Kennwort regelmäßig ändern, verringert es die Wahrscheinlichkeit, dass ein Kenn Wort Angriff dieses Konto kompromittiert.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
In Windows Server 2012 und Windows 8 sind Bild Kennwörter neu. Bild Kennwörter sind eine Kombination aus einem vom Benutzer ausgewählten Bild, das mit einer Reihe von Gesten verknüpft ist. Die Bild Kenn Wort Funktionalität ist auf Domänen\-Computern deaktiviert. Links zu weiteren Informationen zu Bild Kennwörtern finden Sie unter [Siehe auch](#BKMK_LINKS) weiter unten.

Die Kenn Wort Funktionalität in Windows Server 2012 und Windows 8 wurde nicht geändert. Es wurden keine neuen Gruppenrichtlinie Einstellungen hinzugefügt. Es wurden jedoch Verbesserungen und Verbesserungen an den Anmelde Informationen \(und der Kenn Wort\) Verwaltung vorgenommen, wie z. b. mit Bild Kennwörtern, locker für Anmelde Informationen und Anmelden bei Windows 8 mit einem Microsoft-Konto, früher als Windows Live ID bezeichnet.

## <a name="BKMK_DEP"></a>Veraltete Funktionen
In Windows Server 2012 und Windows 8 wurden keine Kenn Wort Funktionen als veraltet markiert.

## <a name="BKMK_SOFT"></a>Software Anforderungen
In Unternehmensumgebungen werden Kenn Wörter in der Regel mit Active Directory Domain Services verwaltet. Kenn Wörter können auch auf dem lokalen Computer mit den Einstellungen unter Lokale Sicherheitseinstellungen, Konto Richtlinien, Kenn Wort Richtlinie verwaltet werden.

## <a name="BKMK_LINKS"></a>Siehe auch
In dieser Tabelle werden zusätzliche Ressourcen für Kenn Wort Features, die Technologie und die Verwaltung von Anmelde Informationen aufgelistet.

|Inhaltstyp|Verweise|
|--------|-------|
|**Szenariodokumentation**|[Schutz Ihrer digitalen Identität](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**Betrieb**|[Active Directory von Benutzern und Computern](https://technet.microsoft.com/library/cc754217.aspx)|
|**Problembehandlung**|[Ermitteln, wann Ihr Kennwort abläuft \- Active Directory PowerShell-Blog](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**Sicherheit**| [Leitfaden zu Bedrohungen und Gegenmaßnahmen](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx) für Windows Server 2008 R2 und Windows 7: Konto Richtlinien<br /><br />Leitfaden zum [ändern und erstellen](https://www.microsoft.com/security/online-privacy/passwords-create.aspx) sicherer Kenn Wörter|
|**Tools und Einstellungen**|[Referenz zu Gruppenrichtlinie Einstellungen für Windows und Windows Server im Microsoft Download Center](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**Communityressourcen**|[Schutz Ihrer digitalen Identität](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Anmelden bei Windows 8 mit einer Windows Live ID](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[Anmelden mit einem Bild Kennwort](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[Optimieren der Bild Kenn Wort Sicherheit](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


