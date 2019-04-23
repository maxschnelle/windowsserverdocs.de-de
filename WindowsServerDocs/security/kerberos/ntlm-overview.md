---
title: 'NTLM: Übersicht'
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 523fb71304ae55d17203cab4d1c5a17551bf8fdf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890641"
---
# <a name="ntlm-overview"></a>NTLM: Übersicht

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema für IT-Experten wird beschrieben, NTLM und funktionsänderungen, und enthält Links zu technischen Ressourcen für Windows-Authentifizierung und NTLM für Windows Server 2012 und früheren Versionen.

## <a name="BKMK_OVER"></a>Featurebeschreibung
NTLM-Authentifizierung ist eine Familie von Authentifizierungsprotokollen, die in der Windows-Msv1 enthalten sind\_0.dll. Zu den NTLM-Authentifizierungsprotokollen gehören LAN-Manager Version 1 und 2 sowie NTLM Version 1 und 2. Die NTLM-Authentifizierungsprotokollen Authentifizieren von Benutzern und Computern basierend auf einer Herausforderung\/oder-Antwortmechanismus, das beweist, die auf einem Server oder Domänencontroller, der ein Benutzer das mit einem Konto verknüpfte Kennwort kennt. Bei Verwendung des NTLM-Protokolls muss ein Ressourcenserver eine der folgenden Aktionen ausführen, um die Identität eines Computers oder Benutzers zu überprüfen, wenn ein neues Zugriffstoken benötigt wird:

-   Kontaktieren eines Domänenauthentifizierungsdienstes auf dem Domänencontroller für die Kontodomäne des Computers oder Benutzers, wenn es sich um ein Domänenkonto handelt.

-   Nachschlagen des Computer- oder Benutzerkontos in der lokalen Kontendatenbank, wenn es sich um ein lokales Konto handelt.

## <a name="BKMK_APP"></a>Aktuelle Anwendungen
Die NTLM-Authentifizierung wird weiterhin unterstützt und muss für die Windows-Authentifizierung bei Systemen verwendet werden, die als Mitglied einer Arbeitsgruppe konfiguriert sind. NTLM-Authentifizierung wird auch verwendet, für die lokale Anmeldeauthentifizierung auf nicht\-Domänencontroller. Kerberos V5-Authentifizierung ist die bevorzugte Authentifizierungsmethode für Active Directory-Umgebungen, aber eine nicht\-Microsoft oder Microsoft NTLM Anwendungen weiterhin verwenden.

Die Verwendung des NTLM-Protokolls in einer IT-Umgebung zu reduzieren, setzt sowohl Kenntnisse der für NTLM geltenden Anwendungsanforderungen als auch der Strategien und Schritte voraus, die erforderlich sind, um Computerumgebungen für die Verwendung anderer Protokolle zu konfigurieren. Neue Tools und Einstellungen helfen Ihnen, zu entdecken, wie NTLM verwendet wird, um den NTLM-Verkehr selektiv einzuschränken. Informationen dazu, wie Sie die Verwendung von NTLM in Ihren Umgebungen analysieren und einschränken, finden Sie unter [Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) , wo Sie auf Anleitungen zum Überwachen und Einschränken der Verwendung von NTLM zugreifen können.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Es sind keine Änderungen funktionsänderungen für NTLM für Windows Server 2012.

## <a name="BKMK_DEP"></a>Entfernten oder veralteten Funktionen
Es gibt keine entfernten oder veralteten Funktionen für NTLM für Windows Server 2012.

## <a name="BKMK_INSTALL"></a>Informationen zur Server-Manager
NTLM kann nicht über den Server-Manager konfiguriert werden. Sie können Sicherheitsrichtlinieneinstellungen oder Gruppenrichtlinien verwenden, um die Verwendung der NTLM-Authentifizierung zwischen Computersystemen zu verwalten. In einer Domäne ist Kerberos das Standardauthentifizierungsprotokoll.

## <a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle sind relevante Ressourcen für NTLM und andere Windows-Authentifizierungstechnologien aufgeführt.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[Änderungen bei der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd566199.aspx)|
|**Planung**|[Handbuch für die IT-Infrastruktur Bedrohungsmodellierung](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in WindowsServer 2003 und Windows XP](https://technet.microsoft.com/library/dd162275.aspx)<br /><br />[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in WindowsServer 2008 und Windows Vista](https://technet.microsoft.com/library/dd349791.aspx)<br /><br />[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 R2 und Windows 7](https://technet.microsoft.com/library/hh125921.aspx)|
|**Bereitstellung**|[Erweiterter Schutz für Authentifizierung](https://support.microsoft.com/kb/968389)<br /><br />[Überwachung und Einschränkung der NTLM-Benutzerhandbuch](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[Stellen Sie das Team für Verzeichnisdienste: NTLM Blocking and You: Application Analysis and Auditing Methodologies in Windows 7](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<br /><br />[Blog der Windows-Authentifizierung](https://blogs.technet.com/authentication/)<br /><br />[Konfigurieren von "MaxConcurrentApi" für die NTLM-Pass\-über die Authentifizierung](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**Entwicklung**|[Microsoft NTLM \(Windows\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[\[MS\-NLMP\]: NT-LAN-Manager \(NTLM\) Authentication Protocol-Spezifikation](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<br /><br />[\[MS\-NNTP\]: NT-LAN-Manager \(NTLM\) Authentifizierung: Network News Transfer Protocol \(NNTP\) Erweiterung](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<br /><br />[\[MS\-NTHT\]: NTLM über HTTP-Protokoll-Spezifikation](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Communityressourcen**|[Ist Sie Warteschlange für unzustellbare Nachrichten noch diese Pferd: NTLM-Engpässen und die RPC-Laufzeit](http://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



