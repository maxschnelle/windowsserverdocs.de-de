---
title: NTLM Overview
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 74e6e05df037041b6c80239e26b39b5566474326
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949756"
---
# <a name="ntlm-overview"></a>NTLM Overview

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema für IT-Experten werden NTLM, alle Änderungen an der Funktionalität beschrieben und Links zu technischen Ressourcen für die Windows-Authentifizierung und NTLM für Windows Server 2012 und frühere Versionen bereitstellt.

## <a name="BKMK_OVER"></a>Featurebeschreibung
Die NTLM-Authentifizierung ist eine Familie von Authentifizierungs Protokollen, die in der Windows Msv1-\_0. dll enthalten sind. Zu den NTLM-Authentifizierungsprotokollen gehören LAN-Manager Version 1 und 2 sowie NTLM Version 1 und 2. Die NTLM-Authentifizierungsprotokolle authentifizieren Benutzer und Computer basierend auf einer Herausforderung\/Response-Mechanismus, der einem Server oder einem Domänen Controller bestätigt, dass ein Benutzer das mit einem Konto verknüpfte Kennwort kennt. Bei Verwendung des NTLM-Protokolls muss ein Ressourcenserver eine der folgenden Aktionen ausführen, um die Identität eines Computers oder Benutzers zu überprüfen, wenn ein neues Zugriffstoken benötigt wird:

-   Kontaktieren eines Domänenauthentifizierungsdienstes auf dem Domänencontroller für die Kontodomäne des Computers oder Benutzers, wenn es sich um ein Domänenkonto handelt.

-   Nachschlagen des Computer- oder Benutzerkontos in der lokalen Kontendatenbank, wenn es sich um ein lokales Konto handelt.

## <a name="BKMK_APP"></a>Aktuelle Anwendungen
Die NTLM-Authentifizierung wird weiterhin unterstützt und muss für die Windows-Authentifizierung bei Systemen verwendet werden, die als Mitglied einer Arbeitsgruppe konfiguriert sind. Die NTLM-Authentifizierung wird auch für die lokale Anmelde Authentifizierung auf nicht\-Domänen Controllern verwendet. Die Kerberos-Authentifizierung (Version 5) ist die bevorzugte Authentifizierungsmethode für Active Directory Umgebungen, aber eine nicht\-Microsoft-oder Microsoft-Anwendung verwendet möglicherweise weiterhin NTLM.

Die Verwendung des NTLM-Protokolls in einer IT-Umgebung zu reduzieren, setzt sowohl Kenntnisse der für NTLM geltenden Anwendungsanforderungen als auch der Strategien und Schritte voraus, die erforderlich sind, um Computerumgebungen für die Verwendung anderer Protokolle zu konfigurieren. Neue Tools und Einstellungen helfen Ihnen, zu entdecken, wie NTLM verwendet wird, um den NTLM-Verkehr selektiv einzuschränken. Informationen dazu, wie Sie die Verwendung von NTLM in Ihren Umgebungen analysieren und einschränken, finden Sie unter [Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) , wo Sie auf Anleitungen zum Überwachen und Einschränken der Verwendung von NTLM zugreifen können.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Es gibt keine Funktionsänderungen für NTLM für Windows Server 2012.

## <a name="BKMK_DEP"></a>Entfernte oder veraltete Funktionen
Für NTLM für Windows Server 2012 gibt es keine entfernten oder veralteten Funktionen.

## <a name="BKMK_INSTALL"></a>Server-Manager Informationen
NTLM kann nicht über den Server-Manager konfiguriert werden. Sie können Sicherheitsrichtlinieneinstellungen oder Gruppenrichtlinien verwenden, um die Verwendung der NTLM-Authentifizierung zwischen Computersystemen zu verwalten. In einer Domäne ist Kerberos das Standardauthentifizierungsprotokoll.

## <a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle sind relevante Ressourcen für NTLM und andere Windows-Authentifizierungstechnologien aufgeführt.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[Änderungen bei der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd566199.aspx)|
|**Planung**|[Leitfaden zur Bedrohungsmodellierung](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2003 und Windows XP](https://technet.microsoft.com/library/dd162275.aspx)<br /><br />[Leitfaden zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 und Windows Vista](https://technet.microsoft.com/library/dd349791.aspx)<br /><br />[Leitfaden zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 R2 und Windows 7](https://technet.microsoft.com/library/hh125921.aspx)|
|**Bereitstellung**|[Erweiterter Schutz für die Authentifizierung](https://support.microsoft.com/kb/968389)<br /><br />[Leitfaden zur Überwachung und Einschränkung der NTLM-Verwendung](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[Fragen Sie das Verzeichnisdienst Team: NTLM-Blockierung und Sie: Anwendungs Analyse-und-Überwachungsmethoden in Windows 7](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<br /><br />[Blog zur Windows-Authentifizierung](https://blogs.technet.com/authentication/)<br /><br />[Konfigurieren von "MaxConcurrentApi" für NTLM-Pass\-durch Authentifizierung](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**Entwicklung**|[Microsoft NTLM-\(Windows\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[\[MS\-nlmp\]: NT LAN Manager \(NTLM\) Authentication Protocol Specification](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<br /><br />[\[MS\-NNTP\]: NT-LAN-Manager \(NTLM\) Authentifizierung: Network News Transfer Protocol \(NNTP-\) Erweiterung](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<br /><br />[\[MS\-ntht\]: NTLM over HTTP-Protokollspezifikation](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Communityressourcen**|[Ist das Pferd noch tot: NTLM-Engpässe und die RPC-Laufzeit](https://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



