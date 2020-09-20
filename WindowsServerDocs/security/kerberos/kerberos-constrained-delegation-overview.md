---
title: Kerberos Constrained Delegation Overview
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 51923b0a-0c1a-47b2-93a0-d36f8e295589
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: cdee2aaecf8710b9801b689b141b16d0dbacc691
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766793"
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos Constrained Delegation Overview

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Übersichts Thema für IT-Experten werden neue Funktionen für die eingeschränkte Kerberos-Delegierung in Windows Server 2012 R2 und Windows Server 2012 beschrieben.

**Funktionsbeschreibung**

Die eingeschränkte Kerberos-Delegierung wurde in Windows Server 2003 eingeführt, um eine sicherere Form der Delegierung bereitzustellen, die von Diensten verwendet werden kann. Wenn dieses Feature konfiguriert ist, beschränkt die eingeschränkte Delegierung die Dienste, für die ein angegebener Server im Auftrag eines Benutzers agieren kann. Dies erfordert Domänenadministratorrechte zum Konfigurieren eines Domänenkontos für einen Dienst und beschränkt das Konto auf eine einzige Domäne. In den heutigen Unternehmen sind Front-End-Dienste nicht auf die Integration in Dienste in Ihrer Domäne beschränkt.

In früheren Betriebssystemversionen, in denen der Dienst vom Domänenadministrator konfiguriert wurde, hatte der Dienstadministrator keine praktische Möglichkeit herauszufinden, welche Front-End-Dienste an die Ressourcendienste delegierten, die sich in ihrem Besitz befanden. Jeder Front-End-Dienst, der an einen Ressourcendienst delegieren konnte, bot einen potenziellen Angriffspunkt. Wenn ein Server kompromittiert wurde, der einen Front-End-Dienst hostete, und wenn dieser Server für die Delegierung an Ressourcendienste konfiguriert war, wurden möglicherweise auch die Ressourcendienste kompromittiert.

In Windows Server 2012 R2 und Windows Server 2012 wurde die Möglichkeit zum Konfigurieren der eingeschränkten Delegierung für den Dienst vom Domänen Administrator an den Dienst Administrator übertragen. Auf diese Weise kann der Back-End-Dienstadministrator Front-End-Dienste erlauben oder verweigern.

Ausführliche Informationen zu der in Windows Server 2003 eingeführten eingeschränkten Delegierung finden Sie unter [Kerberos-Protokollübergang und eingeschränkte Delegierung](/previous-versions/windows/it-pro/windows-server-2003/cc739587(v=ws.10)).

Die Implementierung des Kerberos-Protokolls in Windows Server 2012 R2 und Windows Server 2012 umfasst Erweiterungen speziell für die eingeschränkte Delegierung.  Service-for-User-to-Proxy (S4U2Proxy) ermöglicht es einem Dienst, mithilfe seines Kerberos-Diensttickets für einen Benutzer ein Dienstticket aus dem Schlüsselverteilungscenter (Key Distribution Center, KDC) für einen Back-End-Dienst abzurufen. Diese Erweiterungen ermöglichen die Konfiguration der eingeschränkten Delegierung für das Konto des Back-End-Dienstanbieter, das sich in einer anderen Domäne befinden kann. Weitere Informationen zu diesen Erweiterungen finden Sie in der MSDN Library unter [ \[ MS-SFU \] : Kerberos-Protokoll Erweiterungen: Dienst für Benutzer und eingeschränkte Delegierungs Protokollspezifikation](/openspecs/windows_protocols/ms-sfu/3bff5864-8135-400e-bdd9-33b552051d94) .

**Praktische Anwendung**

Die eingeschränkte Delegierung bietet Dienst Administratoren die Möglichkeit, Anwendungs Vertrauensstellungs Grenzen anzugeben und zu erzwingen, indem Sie den Bereich einschränken, in dem Anwendungsdienste im Auftrag eines Benutzers agieren können. Dienstadministratoren können konfigurieren, welche Front-End-Dienstkonten die Authentifizierung an ihre Back-End-Dienste delegieren können.

Durch die Unterstützung der Domänen übergreifenden eingeschränkten Delegierung in Windows Server 2012 R2 und Windows Server 2012 können Front-End-Dienste wie Microsoft Internet Security and Acceleration (ISA) Server, Microsoft Forefront Threat Management Gateway, Microsoft Exchange Outlook Webzugriff (OWA) und Microsoft SharePoint Server für die Verwendung der eingeschränkten Delegierung für die Authentifizierung bei Servern in anderen Domänen konfiguriert werden. So können domänenübergreifende Dienstlösungen mit einer vorhandenen Kerberos-Infrastruktur unterstützt werden. Die eingeschränkte Kerberos-Delegierung kann von Domänenadministratoren oder Dienstadministratoren verwaltet werden.

## <a name="resource-based-constrained-delegation-across-domains"></a>Domänenübergreifende, ressourcenbasierte eingeschränkte Delegierung

Mithilfe der eingeschränkten Kerberos-Delegierung kann eine eingeschränkte Delegierung bereitgestellt werden, wenn sich der Front-End-Dienst und die Ressourcendienste nicht in der gleichen Domäne befinden. Dienstadministratoren können die neue Delegierung konfigurieren, indem sie die Domänenkonten der Front-End-Dienste angeben, die die Identität von Benutzern für die Kontoobjekte der Ressourcendienste annehmen können.

**Welchen Nutzen bietet diese Änderung?**

Durch die Unterstützung der domänenübergreifenden eingeschränkten Delegierung können Dienste so konfiguriert werden, dass sie für die Authentifizierung bei Servern in anderen Domänen anstelle der uneingeschränkten Delegierung die eingeschränkte Delegierung verwenden. So kann anhand einer vorhandenen Kerberos-Infrastruktur Authentifizierungsunterstützung für domänenübergreifende Dienstlösungen bereitgestellt werden, ohne Front-End-Diensten für die Delegierung an einen Dienst vertrauen zu müssen.

Dadurch wird auch die Entscheidung verlagert, ob ein Server der Quelle einer Delegierten Identität vom Domänen Administrator delegieren an den Ressourcen Besitzer vertrauen soll.

**Worin bestehen die Unterschiede?**

Eine Änderung im zugrunde liegenden Protokoll ermöglicht die domänenübergreifende eingeschränkte Delegierung. Die Implementierung des Kerberos-Protokolls in Windows Server 2012 R2 und Windows Server 2012 umfasst Erweiterungen des Dienstanbieter für das Benutzer-zu-Proxy-Protokoll (S4U2Proxy). Diese Erweiterungen des Kerberos-Protokolls ermöglichen es einem Dienst, mithilfe seines Kerberos-Diensttickets für einen Benutzer ein Dienstticket aus dem Schlüsselverteilungscenter für einen Back-End-Dienst abzurufen.

Implementierungs Informationen zu diesen Erweiterungen finden Sie unter [ \[ MS-SFU \] : Kerberos-Protokoll Erweiterungen: Dienst für Benutzer und eingeschränkte Delegierungs Protokollspezifikation](/openspecs/windows_protocols/ms-sfu/3bff5864-8135-400e-bdd9-33b552051d94) in MSDN.

Weitere Informationen zur grundlegenden Nachrichtensequenz für die Kerberos-Delegierung mit einem weitergeleiteten Ticket-Granting Ticket (TGT) im Vergleich zu Service-for-User-Erweiterungen (S4U) finden Sie im Abschnitt [1.3.3 Übersicht über das Protokoll](/openspecs/windows_protocols/ms-sfu/1fb9caca-449f-4183-8f7a-1a5fc7e7290a) in [MS-SFU]: Kerberos-Protokollerweiterungen: Protokollspezifikation für Service-for-User und eingeschränkte Delegierung.

**Sicherheitsauswirkungen der ressourcenbasierten eingeschränkten Delegierung**

Die ressourcenbasierte eingeschränkte Delegierung legt die Kontrolle über die Delegierung an den Administrator, der die Ressource besitzt, auf die zugegriffen wird. Dies hängt von den Attributen des Ressourcen Dienstanbieter und nicht vom Dienst ab, der als vertrauenswürdig eingestuft wird. Daher kann die ressourcenbasierte eingeschränkte Delegierung nicht das "Trusted-to-Authenticate-for-Delegation"-Bit verwenden, das zuvor den Protokoll Übergang gesteuert hat. Der KDC lässt beim Durchführen einer ressourcenbasierten eingeschränkten Delegierung immer den Protokoll Übergang zu, als wäre das Bit festgelegt.

Da das KDC den Protokoll Übergang nicht einschränkt, wurden zwei neue Bekannte SIDs eingeführt, um diesem Steuerelement den Ressourcen Administrator zu übergeben.  Diese SIDs ermitteln, ob der Protokoll Übergang erfolgt ist, und können mit standardmäßigen Zugriffs Steuerungs Listen verwendet werden, um den Zugriff nach Bedarf zu erteilen oder einzuschränken.

|SID|BESCHREIBUNG|
|-------|--------|
|AUTHENTICATION_AUTHORITY_ASSERTED_IDENTITY<br />S-1-18-1|Eine SID, die bedeutet, dass die Identität des Clients durch eine Authentifizierungs Stelle bestätigt wird, die auf dem Nachweis des Besitzes von Client Anmelde Informationen basiert.|
|SERVICE_ASSERTED_IDENTITY<br />S-1-18-2|Eine SID, die bedeutet, dass die Identität des Clients von einem Dienst bestätigt wird.|

Ein Back-End-Dienst kann Standard-ACL-Ausdrücke verwenden, um die Authentifizierung des Benutzers zu bestimmen.

**Wie konfiguriere ich die ressourcenbasierte eingeschränkte Delegierung?**

Verwenden Sie Windows PowerShell-Cmdlets, um einen Ressourcendienst zum Zulassen des Front-End-Dienstzugriffs im Auftrag von Benutzern zu konfigurieren.

-   Zum Abrufen einer Liste von Prinzipale verwenden Sie die Cmdlets **Get-adcomputer**, **Get-ADServiceAccount**und **Get-ADUser** mit dem Parameter **principalsallowedtodelegatetoaccount** .

-   Um den Ressourcen Dienst zu konfigurieren, verwenden Sie die Cmdlets **New-adcomputer**, **New-ADServiceAccount**, **New-ADUser**, **Set-adcomputer**, **Set-ADServiceAccount**und **Set-ADUser** mit dem **principalsallowedtodelegatetoaccount** -Parameter.

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Software Anforderungen
Die ressourcenbasierte eingeschränkte Delegierung kann nur auf einem Domänen Controller unter Windows Server 2012 R2 und Windows Server 2012 konfiguriert werden, kann jedoch in einer Gesamtstruktur mit gemischtem Modus angewendet werden.

Sie müssen den folgenden Hotfix auf allen Domänen Controllern unter Windows Server 2012 in Benutzerkonten Domänen im Weiterleitungs Pfad zwischen den Front-End-und Back-End-Domänen anwenden, auf denen ältere Betriebssysteme als Windows Server ausgeführt werden: ressourcenbasierte eingeschränkte Delegierung KDC_ERR_POLICY Fehler in Umgebungen mit Windows Server 2008 R2-basierten Domänen Controllern () https://support.microsoft.com/en-gb/help/2665790/resource-based-constrained-delegation-kdc-err-policy-failure-in-enviro) .