---
title: NTLM Overview
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-kerberos
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 972b5b8eb5e25382c2c9b7841cf0d0fe4db6e647
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181876"
---
# <a name="ntlm-overview"></a>NTLM Overview

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Experten werden NTLM, alle Änderungen an der Funktionalität beschrieben und Links zu technischen Ressourcen für die Windows-Authentifizierung und NTLM für Windows Server 2012 und frühere Versionen bereitstellt.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Funktionsbeschreibung
Die NTLM-Authentifizierung ist eine Familie von Authentifizierungs Protokollen, die in der Windows Msv1-0.dll enthalten sind \_ . Zu den NTLM-Authentifizierungsprotokollen gehören LAN-Manager Version 1 und 2 sowie NTLM Version 1 und 2. Die NTLM-Authentifizierungsprotokolle authentifizieren Benutzer und Computer auf der Grundlage eines Challenge \/ Response-Mechanismus, der einem Server oder einem Domänen Controller bestätigt, dass ein Benutzer das mit einem Konto verknüpfte Kennwort kennt. Bei Verwendung des NTLM-Protokolls muss ein Ressourcenserver eine der folgenden Aktionen ausführen, um die Identität eines Computers oder Benutzers zu überprüfen, wenn ein neues Zugriffstoken benötigt wird:

-   Kontaktieren eines Domänenauthentifizierungsdienstes auf dem Domänencontroller für die Kontodomäne des Computers oder Benutzers, wenn es sich um ein Domänenkonto handelt.

-   Nachschlagen des Computer- oder Benutzerkontos in der lokalen Kontendatenbank, wenn es sich um ein lokales Konto handelt.

## <a name="current-applications"></a><a name="BKMK_APP"></a>Praktische Anwendungsfälle
Die NTLM-Authentifizierung wird weiterhin unterstützt und muss für die Windows-Authentifizierung bei Systemen verwendet werden, die als Mitglied einer Arbeitsgruppe konfiguriert sind. Die NTLM-Authentifizierung wird auch für die lokale Anmelde Authentifizierung auf nicht- \- Domänen Controllern verwendet. Die Kerberos-Authentifizierung (Version 5) ist die bevorzugte Authentifizierungsmethode für Active Directory Umgebungen, aber eine nicht von \- Microsoft oder Microsoft verwendete Anwendung verwendet möglicherweise weiterhin NTLM.

Die Verwendung des NTLM-Protokolls in einer IT-Umgebung zu reduzieren, setzt sowohl Kenntnisse der für NTLM geltenden Anwendungsanforderungen als auch der Strategien und Schritte voraus, die erforderlich sind, um Computerumgebungen für die Verwendung anderer Protokolle zu konfigurieren. Neue Tools und Einstellungen helfen Ihnen, zu entdecken, wie NTLM verwendet wird, um den NTLM-Verkehr selektiv einzuschränken. Informationen dazu, wie Sie die Verwendung von NTLM in Ihren Umgebungen analysieren und einschränken, finden Sie unter [Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) , wo Sie auf Anleitungen zum Überwachen und Einschränken der Verwendung von NTLM zugreifen können.

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Es gibt keine Funktionsänderungen für NTLM für Windows Server 2012.

## <a name="removed-or-deprecated-functionality"></a><a name="BKMK_DEP"></a>Entfernte oder veraltete Funktionen
Für NTLM für Windows Server 2012 gibt es keine entfernten oder veralteten Funktionen.

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>Informationen zum Server-Manager
NTLM kann nicht über den Server-Manager konfiguriert werden. Sie können Sicherheitsrichtlinieneinstellungen oder Gruppenrichtlinien verwenden, um die Verwendung der NTLM-Authentifizierung zwischen Computersystemen zu verwalten. In einer Domäne ist Kerberos das Standardauthentifizierungsprotokoll.

## <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle sind relevante Ressourcen für NTLM und andere Windows-Authentifizierungstechnologien aufgeführt.

|Inhaltstyp|Referenzen|
|--------|-------|
|**Produktbewertung**|[Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653.aspx)<p>[Änderungen bei der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd566199.aspx)|
|**Planung**|[Handbuch zum Erstellen von Modellen zur Bedrohung der IT-Infrastruktur](https://technet.microsoft.com/library/dd941826.aspx)<p>[Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2003 und Windows XP](https://technet.microsoft.com/library/dd162275.aspx)<p>[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 und Windows Vista](https://technet.microsoft.com/library/dd349791.aspx)<p>[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 R2 und Windows 7](https://technet.microsoft.com/library/hh125921.aspx)|
|**Bereitstellung**|[Erweiterter Schutz für die Authentifizierung](https://support.microsoft.com/kb/968389)<p>[Handbuch zur Überwachung und Einschränkung der NTLM-Verwendung](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<p>[Ask the Directory Services Team: NTLM Blocking and You: Application Analysis and Auditing Methodologies in Windows 7](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<p>[Windows Authentication Blog](https://blogs.technet.com/authentication/)<p>[Konfigurieren von MaxConcurrentAPI für die NTLM-Pass-Through-Authentifizierung](https://support.microsoft.com/help/2688798/how-to-do-performance-tuning-for-ntlm-authentication-by-using-the-maxc)|
|**Entwicklung**|[Microsoft-NTLM- \( Fenster\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<p>[\[MS \- nlmp \] : NT LAN Manager \( NTLM \) Authentication Protocol Specification](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<p>[\[MS \- NNTP \] : NT LAN Manager \( NTLM- \) Authentifizierung: Network News Transfer-Protokoll \( NNTP- \) Erweiterung](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<p>[\[MS \- ntht \] : NTLM über HTTP-Protokollspezifikation](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Communityressourcen**|[Is this horse dead yet: NTLM Bottlenecks and the RPC runtime](https://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



