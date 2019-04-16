---
title: "NTLM (Übersicht)"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ntlm-overview"></a>NTLM (Übersicht)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten wird beschrieben, NTLM, Änderungen an der Funktionalität, und enthält Links zu technischen Ressourcen zu Windows-Authentifizierung und NTLM für Windows Server2012 und früheren Versionen.

## <a name="BKMK_OVER"></a>Featurebeschreibung
NTLM-Authentifizierung ist eine Reihe von Authentifizierungsprotokollen, die in der Windows-Msv1\_0.dll enthalten sind. Die NTLM-Authentifizierungsprotokollen gehören LAN-Manager Version 1 und 2 sowie NTLM Version 1 und 2. Die NTLM-Authentifizierungsprotokollen authentifiziert Benutzer und Computer, die auf einem Challenge\/Rückmeldung-Mechanismus, der auf einen Server oder Domänencontroller, der ein Benutzer das mit einem Konto verknüpfte Kennwort kennt nachweist. Wenn das NTLM-Protokoll verwendet wird, muss ein Ressourcenserver eine der folgenden Aktionen aus, um die Identität eines Computers oder Benutzers zu überprüfen, wenn ein neues Zugriffstoken benötigt wird:

-   Erhalten Sie eines domänenauthentifizierungsdienstes auf dem Domänencontroller die Kontodomäne des Computers oder Benutzers, wenn das Konto ein Domänenkonto ist.

-   Suchen des Computers oder Benutzers Konto in der lokalen Kontendatenbank, wenn das Konto ein lokales Konto handelt.

## <a name="BKMK_APP"></a>aktuellen Anwendungen
NTLM-Authentifizierung wird weiterhin unterstützt und muss für Windows-Authentifizierung verwendet werden, bei Systemen, die als Mitglied einer Arbeitsgruppe konfiguriert. NTLM-Authentifizierung wird auch für die lokale Anmeldeauthentifizierung auf-Domänencontrollern verwendet werden. Kerberos V5-Authentifizierung ist die bevorzugte Authentifizierungsmethode für Active Directory-Umgebungen verwendet eine von Microsoft oder Microsoft-Anwendung vielleicht weiterhin NTLM.

Reduzieren die Verwendung des NTLM-Protokolls in einer IT-Umgebung ist sowohl Kenntnisse anwendungsanforderungen auf NTLM und die anderer Protokolle Strategien und Schrittezum Konfigurieren von computerumgebungen erforderlich. Neue Tools und Einstellungen wurden hinzugefügt, um zu ermitteln, wie NTLM verwendet wird, um die NTLM-Verkehr selektiv einzuschränken. Informationen zur Vorgehensweise beim Analysieren und Einschränken der NTLM-Nutzung in Ihrer Umgebung finden Sie unter [Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) zu überwachen und Einschränken der NTLM-Benutzerhandbuch zugreifen.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Es gibt keine Änderungen an der Funktionalität für NTLM für Windows Server2012.

## <a name="BKMK_DEP"></a>Entfernte oder veraltete Funktionen
Es ist keine entfernten oder veralteten Funktionen für NTLM für Windows Server2012.

## <a name="BKMK_INSTALL"></a>Server-Manager-Informationen
NTLM kann über Server-Manager konfiguriert werden. Sie können sicherheitsrichtlinieneinstellungen oder Gruppenrichtlinien verwenden, Auslastung der NTLM-Authentifizierung zwischen Computersystemen zu verwalten. In einer Domäne ist Kerberos das Standardauthentifizierungsprotokoll.

## <a name="BKMK_LINKS"></a>Siehe auch
Die folgende Tabelle enthält die relevante Ressourcen für NTLM und andere Windows-authentifizierungstechnologien.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[Änderungen bei der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd566199.aspx)|
|**Planen der**|[IT-Infrastruktur Threat Modeling Guide](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2003 und Windows XP](https://technet.microsoft.com/library/dd162275.aspx)<br /><br />[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 und windowsvista](https://technet.microsoft.com/library/dd349791.aspx)<br /><br />[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server2008 R2 und Windows7](https://technet.microsoft.com/library/hh125921.aspx)|
|**Bereitstellung**|[Erweiterter Schutz für Authentifizierung](https://support.microsoft.com/kb/968389)<br /><br />[Überwachung und Einschränkung der NTLM-Benutzerhandbuch](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[Fragen Sie das Team für Verzeichnisdienste: NTLM blockieren und Sie: Analyse der Anwendung und Überwachung von Methoden in Windows7](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<br /><br />[Blog zur Windows-Authentifizierung](https://blogs.technet.com/authentication/)<br /><br />[Konfigurieren von MaxConcurrentAPI für Pass\ über NTLM-Authentifizierung](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**Entwicklung von Apps**|[Microsoft NTLM \(Windows\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[\[MS\-NLMP\]: Spezifikation NT LAN Manager-\(NTLM\)](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<br /><br />[\[MS\-NNTP\]: NT LAN Manager-\(NTLM\) Authentifizierung: Network News Transfer-Protokoll \(NNTP\) Erweiterung](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<br /><br />[\[MS\-NTHT\]: NTLM über HTTP-Protokoll-Spezifikation](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Community-Ressourcen**|[Ist diese Pferd tote noch: NTLM-Engpässe und der RPC-Laufzeit](http://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



