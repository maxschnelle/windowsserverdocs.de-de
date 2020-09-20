---
title: NTLM Overview
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: d12e61fac3ba6c44dbcac35ea3097e95db54752a
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766783"
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

Die Verwendung des NTLM-Protokolls in einer IT-Umgebung zu reduzieren, setzt sowohl Kenntnisse der für NTLM geltenden Anwendungsanforderungen als auch der Strategien und Schritte voraus, die erforderlich sind, um Computerumgebungen für die Verwendung anderer Protokolle zu konfigurieren. Neue Tools und Einstellungen helfen Ihnen, zu entdecken, wie NTLM verwendet wird, um den NTLM-Verkehr selektiv einzuschränken. Informationen dazu, wie Sie die Verwendung von NTLM in Ihren Umgebungen analysieren und einschränken, finden Sie unter [Einführung der Einschränkung der NTLM-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560653(v=ws.10)) , wo Sie auf Anleitungen zum Überwachen und Einschränken der Verwendung von NTLM zugreifen können.

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
|**Produktbewertung**|[Einführung der Einschränkung der NTLM-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560653(v=ws.10))<p>[Änderungen bei der NTLM-Authentifizierung](/previous-versions/windows/it-pro/windows-7/dd566199(v=ws.10))|
|**Planung**|[Handbuch zum Erstellen von Modellen zur Bedrohung der IT-Infrastruktur](/previous-versions/tn-archive/dd941826(v=technet.10))<p>[Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2003 und Windows XP](/previous-versions/tn-archive/dd162275(v=technet.10))<p>[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 und Windows Vista](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd349791(v=ws.10))<p>[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 R2 und Windows 7](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125921(v=ws.10))|
|**Bereitstellung**|[Erweiterter Schutz für die Authentifizierung](https://support.microsoft.com/kb/968389)<p>[Handbuch zur Überwachung und Einschränkung der NTLM-Verwendung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/jj865674(v=ws.10))<p>[Ask the Directory Services Team: NTLM Blocking and You: Application Analysis and Auditing Methodologies in Windows 7](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<p>[Windows Authentication Blog](https://blogs.technet.com/authentication/)<p>[Konfigurieren von MaxConcurrentAPI für die NTLM-Pass-Through-Authentifizierung](https://support.microsoft.com/help/2688798/how-to-do-performance-tuning-for-ntlm-authentication-by-using-the-maxc)|
|**Entwicklung**|[Microsoft-NTLM- \( Fenster\)](/windows/win32/secauthn/microsoft-ntlm)<p>[\[MS \- nlmp \] : NT LAN Manager \( NTLM \) Authentication Protocol Specification](/openspecs/windows_protocols/ms-nlmp/b38c36ed-2804-4868-a9ff-8dd3182128e4)<p>[\[MS \- NNTP \] : NT LAN Manager \( NTLM- \) Authentifizierung: Network News Transfer-Protokoll \( NNTP- \) Erweiterung](/openspecs/windows_protocols/ms-nntp/73ae7d96-30fe-4750-807c-bfe7c38b3a0a)<p>[\[MS \- ntht \] : NTLM über HTTP-Protokollspezifikation](/openspecs/windows_protocols/ms-ntht/f09cf6e1-529e-403b-a8a5-7368ee096a6a)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Communityressourcen**|[Is this horse dead yet: NTLM Bottlenecks and the RPC runtime](https://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|