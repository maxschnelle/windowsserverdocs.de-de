---
title: Kerberos Constrained Delegation Overview
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51923b0a-0c1a-47b2-93a0-d36f8e295589
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 02677c8d9db4129ebbd7edd79027e0a6348372b5
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544616"
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos Constrained Delegation Overview

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Übersichts Thema für IT-Experten werden neue Funktionen für die eingeschränkte Kerberos-Delegierung in Windows Server 2012 R2 und Windows Server 2012 beschrieben.

**Funktionsbeschreibung**

Die eingeschränkte Kerberos-Delegierung wurde in Windows Server 2003 eingeführt, um eine sicherere Form der Delegierung bereitzustellen, die von Diensten verwendet werden kann. Wenn dieses Feature konfiguriert ist, beschränkt die eingeschränkte Delegierung die Dienste, für die ein angegebener Server im Auftrag eines Benutzers agieren kann. Dies erfordert Domänenadministratorrechte zum Konfigurieren eines Domänenkontos für einen Dienst und beschränkt das Konto auf eine einzige Domäne. In den heutigen Unternehmen sind Front-End-Dienste nicht auf die Integration in Dienste in Ihrer Domäne beschränkt.

In früheren Betriebssystemversionen, in denen der Dienst vom Domänenadministrator konfiguriert wurde, konnte der Dienstadministrator nicht ohne Weiteres feststellen, welche an die Ressourcendienste delegierten Front-End-Dienste ihm gehörten. Und zudem stellte jeder Front-End-Dienst, der an einen Ressourcendienst delegieren konnte, einen potenziellen Angriffspunkt dar. Wurde ein zum Delegieren an Ressourcendienste konfigurierter Server, der einen Front-End-Dienst hostete, gefährdet, konnten auch die Ressourcendienste gefährdet werden.

In Windows Server 2012 R2 und Windows Server 2012 wurde die Möglichkeit zum Konfigurieren der eingeschränkten Delegierung für den Dienst vom Domänen Administrator an den Dienst Administrator übertragen. Dadurch erhält der Back-End-Dienstadministrator die Möglichkeit, Front-End-Dienste zuzulassen oder abzulehnen.

Ausführliche Informationen zu der in Windows Server 2003 eingeführten eingeschränkten Delegierung finden Sie unter [Kerberos-Protokollübergang und eingeschränkte Delegierung](https://technet.microsoft.com/library/cc739587(v=ws.10)).

Die Implementierung des Kerberos-Protokolls in Windows Server 2012 R2 und Windows Server 2012 umfasst Erweiterungen speziell für die eingeschränkte Delegierung.  Service-for-User-to-Proxy (S4U2Proxy) ermöglicht es einem Dienst, mithilfe seines Kerberos-Diensttickets für einen Benutzer ein Dienstticket aus dem Schlüsselverteilungscenter (Key Distribution Center, KDC) für einen Back-End-Dienst abzurufen. Diese Erweiterungen ermöglichen die Konfiguration der eingeschränkten Delegierung für das Konto des Back-End-Dienstanbieter, das sich in einer anderen Domäne befinden kann. Weitere Informationen zu diesen Erweiterungen finden [ \[Sie unter MS-SFU\]: Kerberos-Protokollerweiterungen: Protokollspezifikation](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx) für Service for User und eingeschränkte Delegierung in der MSDN Library.

**Praktische Anwendungen**

Die eingeschränkte Delegierung bietet Dienst Administratoren die Möglichkeit, Anwendungs Vertrauensstellungs Grenzen anzugeben und zu erzwingen, indem Sie den Bereich einschränken, in dem Anwendungsdienste im Auftrag eines Benutzers agieren können. Dienstadministratoren können konfigurieren, welche Front-End-Dienstkonten die Authentifizierung an ihre Back-End-Dienste delegieren können.

Durch die Unterstützung der Domänen übergreifenden eingeschränkten Delegierung in Windows Server 2012 R2 und Windows Server 2012, Front-End-Dienste wie Microsoft Internet Security and Acceleration (ISA) Server, Microsoft Forefront Threat Management Gateway, Microsoft Exchange Outlook Webzugriff (OWA) und Microsoft SharePoint Server können für die Verwendung der eingeschränkten Delegierung für die Authentifizierung bei Servern in anderen Domänen konfiguriert werden. So können domänenübergreifende Dienstlösungen mit einer vorhandenen Kerberos-Infrastruktur unterstützt werden. Die eingeschränkte Kerberos-Delegierung kann von Domänenadministratoren oder Dienstadministratoren verwaltet werden.

## <a name="resource-based-constrained-delegation-across-domains"></a>Domänenübergreifende, ressourcenbasierte eingeschränkte Delegierung

Mithilfe der eingeschränkten Kerberos-Delegierung kann eine eingeschränkte Delegierung bereitgestellt werden, wenn sich der Front-End-Dienst und die Ressourcendienste nicht in der gleichen Domäne befinden. Dienstadministratoren können die neue Delegierung konfigurieren, indem sie die Domänenkonten der Front-End-Dienste angeben, die die Identität von Benutzern für die Kontoobjekte der Ressourcendienste annehmen können.

**Welchen Nutzen bietet diese Änderung?**

Durch die Unterstützung der domänenübergreifenden eingeschränkten Delegierung können Dienste so konfiguriert werden, dass sie für die Authentifizierung bei Servern in anderen Domänen anstelle der uneingeschränkten Delegierung die eingeschränkte Delegierung verwenden. So kann anhand einer vorhandenen Kerberos-Infrastruktur Authentifizierungsunterstützung für domänenübergreifende Dienstlösungen bereitgestellt werden, ohne Front-End-Diensten für die Delegierung an einen Dienst vertrauen zu müssen.

Dadurch wird auch die Entscheidung verlagert, ob ein Server der Quelle einer Delegierten Identität vom Domänen Administrator delegieren an den Ressourcen Besitzer vertrauen soll.

**Worin bestehen die Unterschiede?**

Eine Änderung im zugrunde liegenden Protokoll ermöglicht die domänenübergreifende eingeschränkte Delegierung. Die Implementierung des Kerberos-Protokolls in Windows Server 2012 R2 und Windows Server 2012 umfasst Erweiterungen des Dienstanbieter für das Benutzer-zu-Proxy-Protokoll (S4U2Proxy). Diese Erweiterungen des Kerberos-Protokolls ermöglichen es einem Dienst, mithilfe seines Kerberos-Diensttickets für einen Benutzer ein Dienstticket aus dem Schlüsselverteilungscenter für einen Back-End-Dienst abzurufen.

Implementierungs Informationen zu diesen Erweiterungen finden [ \[Sie unter MS-SFU\]: Kerberos-Protokollerweiterungen: Protokollspezifikation](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx) für Service for User und eingeschränkte Delegierung in MSDN.

Weitere Informationen zur grundlegenden Nachrichten Sequenz für die Kerberos-Delegierung mit einem weitergeleiteten Ticket Erstellungs Ticket (TGT) im Vergleich zu Service for User-Erweiterungen (S4U) finden Sie im Abschnitt " [1.3.3 Protocol Overview](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx) " im [MS-SFU]: Kerberos-Protokollerweiterungen: Protokollspezifikation für Service-for-User und eingeschränkte Delegierung.

**Sicherheitsauswirkungen der ressourcenbasierten eingeschränkten Delegierung**

Die ressourcenbasierte eingeschränkte Delegierung legt die Kontrolle über die Delegierung an den Administrator, der die Ressource besitzt, auf die zugegriffen wird. Dies hängt von den Attributen des Ressourcen Dienstanbieter und nicht vom Dienst ab, der als vertrauenswürdig eingestuft wird. Daher kann die ressourcenbasierte eingeschränkte Delegierung nicht das "Trusted-to-Authenticate-for-Delegation"-Bit verwenden, das zuvor den Protokoll Übergang gesteuert hat. Der KDC lässt beim Durchführen einer ressourcenbasierten eingeschränkten Delegierung immer den Protokoll Übergang zu, als wäre das Bit festgelegt.

Da das KDC den Protokoll Übergang nicht einschränkt, wurden zwei neue Bekannte SIDs eingeführt, um diesem Steuerelement den Ressourcen Administrator zu übergeben.  Diese SIDs ermitteln, ob der Protokoll Übergang erfolgt ist, und können mit standardmäßigen Zugriffs Steuerungs Listen verwendet werden, um den Zugriff nach Bedarf zu erteilen oder einzuschränken.

|SID|Beschreibung|
|-------|--------|
|AUTHENTICATION_AUTHORITY_ASSERTED_IDENTITY<br />S-1-18-1|Eine SID, die bedeutet, dass die Identität des Clients durch eine Authentifizierungs Stelle bestätigt wird, die auf dem Nachweis des Besitzes von Client Anmelde Informationen basiert.|
|SERVICE_ASSERTED_IDENTITY<br />S-1-18-2|Eine SID, die bedeutet, dass die Identität des Clients von einem Dienst bestätigt wird.|

Ein Back-End-Dienst kann Standard-ACL-Ausdrücke verwenden, um die Authentifizierung des Benutzers zu bestimmen.

**Wie konfiguriere ich die ressourcenbasierte eingeschränkte Delegierung?**

Verwenden Sie Windows PowerShell-Cmdlets, um einen Ressourcendienst zum Zulassen des Front-End-Dienstzugriffs im Auftrag von Benutzern zu konfigurieren.

-   Zum Abrufen einer Liste von Prinzipale verwenden Sie die Cmdlets **Get-adcomputer**, **Get-ADServiceAccount**und **Get-ADUser** mit dem Parameter **principalsallowedtodelegatetoaccount** .

-   Um den Ressourcen Dienst zu konfigurieren, verwenden Sie die Cmdlets **New**-adcomputer, **New-ADServiceAccount**, **New-ADUser**, **Set-adcomputer**, **Set-ADServiceAccount**und **Set-ADUser** mit dem  **Principalsallowedtodelegatetoaccount** -Parameter.

## <a name="BKMK_SOFT"></a>Software Anforderungen
Die ressourcenbasierte eingeschränkte Delegierung kann nur auf einem Domänen Controller unter Windows Server 2012 R2 und Windows Server 2012 konfiguriert werden, kann jedoch in einer Gesamtstruktur mit gemischtem Modus angewendet werden.

Sie müssen den folgenden Hotfix auf allen Domänen Controllern unter Windows Server 2012 in Benutzerkonto Domänen auf dem Referenz Pfad zwischen den Front-End-und Back-End-Domänen anwenden, auf denen Betriebssysteme vor Windows Server ausgeführt werden:  Ressourcenbasierte eingeschränkte Delegierung KDC_ERR_POLICY Fehler in Umgebungen mit Windows Server 2008 R2-basierten Domänen Controllern https://support.microsoft.com/en-gb/help/2665790/resource-based-constrained-delegation-kdc-err-policy-failure-in-enviro) (.
