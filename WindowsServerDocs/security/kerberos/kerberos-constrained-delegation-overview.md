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
ms.openlocfilehash: d77dd6f6f310ae71a4d9e2d52b44cc9b1bef6401
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821931"
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos Constrained Delegation Overview

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Übersichtsthema für IT-Experten werden neue Funktionen für die eingeschränkte Kerberos-Delegierung in Windows Server 2012 R2 und Windows Server 2012 beschrieben.

**Featurebeschreibung**

Die eingeschränkte Kerberos-Delegierung wurde in Windows Server 2003 eingeführt, um eine sicherere Form der Delegierung bereitzustellen, die von Diensten verwendet werden kann. Wenn dieses Feature konfiguriert ist, beschränkt die eingeschränkte Delegierung die Dienste, für die ein angegebener Server im Auftrag eines Benutzers agieren kann. Dies erfordert Domänenadministratorrechte zum Konfigurieren eines Domänenkontos für einen Dienst und beschränkt das Konto auf eine einzige Domäne. In modernen Unternehmen sind Front-End-Dienste nicht konzipiert, der Integration von nur Dienste in ihrer Domäne beschränkt werden sollen.

In früheren Betriebssystemversionen, in denen der Dienst vom Domänenadministrator konfiguriert wurde, konnte der Dienstadministrator nicht ohne Weiteres feststellen, welche an die Ressourcendienste delegierten Front-End-Dienste ihm gehörten. Und zudem stellte jeder Front-End-Dienst, der an einen Ressourcendienst delegieren konnte, einen potenziellen Angriffspunkt dar. Wurde ein zum Delegieren an Ressourcendienste konfigurierter Server, der einen Front-End-Dienst hostete, gefährdet, konnten auch die Ressourcendienste gefährdet werden.

In Windows Server 2012 R2 und Windows Server 2012 wurde die Möglichkeit zum Konfigurieren der eingeschränkten Delegierung für den Dienst vom Domänenadministrator an den Dienstadministrator übertragen. Dadurch erhält der Back-End-Dienstadministrator die Möglichkeit, Front-End-Dienste zuzulassen oder abzulehnen.

Ausführliche Informationen zu der in Windows Server 2003 eingeführten eingeschränkten Delegierung finden Sie unter [Kerberos-Protokollübergang und eingeschränkte Delegierung](https://technet.microsoft.com/library/cc739587(v=ws.10)).

Die Windows Server 2012 R2 und Windows Server 2012-Implementierung des Kerberos-Protokolls beinhaltet spezielle Erweiterungen für eingeschränkte Delegierung.  Service-for-User-to-Proxy (S4U2Proxy) ermöglicht es einem Dienst, mithilfe seines Kerberos-Diensttickets für einen Benutzer ein Dienstticket aus dem Schlüsselverteilungscenter (Key Distribution Center, KDC) für einen Back-End-Dienst abzurufen. Diese Erweiterungen ermöglichen die eingeschränkte Delegierung für die Back-End-Dienst-Konto konfiguriert werden, die in einer anderen Domäne werden kann. Weitere Informationen zu diesen Erweiterungen finden Sie unter [ \[MS-SFU\]: Kerberos-Protokollerweiterungen: Service for-User und eingeschränkte Delegierung Protokollspezifikation](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx) in der MSDN Library.

**Praktische Anwendungen**

Eingeschränkte Delegierung ermöglicht Dienstadministratoren die Möglichkeit zu geben und anwendungsvertrauensstellungsgrenzen erzwingen, indem Sie den Bereich, in dem Anwendungsdienste im Auftrag eines Benutzers handeln können, einschränken. Dienstadministratoren können konfigurieren, welche Front-End-Dienstkonten die Authentifizierung an ihre Back-End-Dienste delegieren können.

Durch die Unterstützung der eingeschränkten Delegierung für Domänen in Windows Server 2012 R2 und Windows Server 2012, z. B. Microsoft Internet Security and Acceleration (ISA) Server, Microsoft Forefront Threat Management Gateway, Microsoft Exchange-Front-End-Dienste Outlook Web Access (OWA) und Microsoft SharePoint Server können für die um eingeschränkten Delegierung zu verwenden, um die Authentifizierung bei Servern in anderen Domänen konfiguriert werden. So können domänenübergreifende Dienstlösungen mit einer vorhandenen Kerberos-Infrastruktur unterstützt werden. Die eingeschränkte Kerberos-Delegierung kann von Domänenadministratoren oder Dienstadministratoren verwaltet werden.

## <a name="resource-based-constrained-delegation-across-domains"></a>Domänenübergreifende, ressourcenbasierte eingeschränkte Delegierung

Mithilfe der eingeschränkten Kerberos-Delegierung kann eine eingeschränkte Delegierung bereitgestellt werden, wenn sich der Front-End-Dienst und die Ressourcendienste nicht in der gleichen Domäne befinden. Dienstadministratoren können die neue Delegierung konfigurieren, indem sie die Domänenkonten der Front-End-Dienste angeben, die die Identität von Benutzern für die Kontoobjekte der Ressourcendienste annehmen können.

**Welchen Nutzen bietet diese Änderung?**

Durch die Unterstützung der domänenübergreifenden eingeschränkten Delegierung können Dienste so konfiguriert werden, dass sie für die Authentifizierung bei Servern in anderen Domänen anstelle der uneingeschränkten Delegierung die eingeschränkte Delegierung verwenden. So kann anhand einer vorhandenen Kerberos-Infrastruktur Authentifizierungsunterstützung für domänenübergreifende Dienstlösungen bereitgestellt werden, ohne Front-End-Diensten für die Delegierung an einen Dienst vertrauen zu müssen.

Dies wird auch die Entscheidung, ob ein Server die Quelle des delegierten Identitäten von Delegierung vom Domänenadministrator an, der Besitzer der Ressource als vertrauenswürdig behandeln soll verlagert.

**Worin bestehen die Unterschiede?**

Eine Änderung im zugrunde liegenden Protokoll ermöglicht die domänenübergreifende eingeschränkte Delegierung. Die Windows Server 2012 R2 und Windows Server 2012-Implementierung des Kerberos-Protokolls beinhaltet Erweiterungen des Service für Benutzer, Proxy (S4U2Proxy)-Protokolls. Diese Erweiterungen des Kerberos-Protokolls ermöglichen es einem Dienst, mithilfe seines Kerberos-Diensttickets für einen Benutzer ein Dienstticket aus dem Schlüsselverteilungscenter für einen Back-End-Dienst abzurufen.

Weitere Informationen zur Implementierung dieser Erweiterungen, finden Sie unter [ \[MS-SFU\]: Kerberos-Protokollerweiterungen: Service for-User und eingeschränkte Delegierung Protokollspezifikation](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx) in MSDN.

Weitere Informationen zur grundlegenden nachrichtensequenz für die Kerberos-Delegierung mit einem weitergeleiteten Ticket-granting Ticket (TGT) im Vergleich zu Service für User (S4U)-Erweiterungen finden Sie im Abschnitt [1.3.3 Übersicht über das Protokoll](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx) in [MS-SFU]: Kerberos-Protokollerweiterungen: Protokollspezifikation für Service-for-User und eingeschränkte Delegierung.

**Sicherheitsauswirkungen der ressourcenbasierte eingeschränkte Delegierung**

Ressourcenbasierte eingeschränkte Delegierung setzt Control Delegierung in die Hände von dem Administrator, Besitzer der Ressource, auf die zugegriffen wird. Es hängt die Attribute des Ressourcendiensts statt auf den Dienst um zu delegieren vertrauenswürdig. Daher kann ressourcenbasierte eingeschränkter Delegierung nicht das Bit für die vertrauenswürdige-zu-Authentifizierung-für-Delegierung verwenden, die zuvor Protokollübergang gesteuert. Das KDC kann immer Protokollübergang beim Ausführen von ressourcenbasierte eingeschränkte Delegierung genutzt, als ob das Bit festgelegt wurden.

Da das KDC Protokollübergang nicht begrenzt, zwei neue bekannte SIDs wurden eingeführt, um dieses Steuerelement an dem Ressourcenadministrator zu gewähren.  Diese SIDs ermitteln, ob Protokollübergang ist aufgetreten, und kann mit standard-Zugriffssteuerungslisten verwendet werden, zu gewähren oder Einschränken des Zugriffs nach Bedarf.

|SID|Beschreibung|
|-------|--------|
|AUTHENTICATION_AUTHORITY_ASSERTED_IDENTITY<br />S-1-18-1|Eine SID an, das bedeutet, die Identität des Clients dass wird durch den eine authentifizierungsautorisierungsstelle basierend auf den Nachweis des rechtmäßigen Besitzes Clientanmeldeinformationen übergeben.|
|SERVICE_ASSERTED_IDENTITY<br />S-1-18-2|Eine SID an, das bedeutet, die Identität des Clients dass wird von einem Dienst übergeben.|

Ein Back-End-Dienst kann die standard-ACL-Ausdrücke verwenden, um zu bestimmen, wie der Benutzer authentifiziert wurde.

**Wie konfigurieren Sie die ressourcenbasierte eingeschränkte Delegierung?**

Verwenden Sie Windows PowerShell-Cmdlets, um einen Ressourcendienst zum Zulassen des Front-End-Dienstzugriffs im Auftrag von Benutzern zu konfigurieren.

-   Verwenden Sie zum Abrufen einer Liste von Prinzipalen die **Get-ADComputer**, **Get-ADServiceAccount**, und **Get-ADUser** Cmdlets mit der **Eigenschaften PrincipalsAllowedToDelegateToAccount** Parameter.

-   Verwenden Sie zum Konfigurieren des Ressourcendiensts die **New-ADComputer**, **New-ADServiceAccount**, **New-ADUser**, **Set-ADComputer**,  **Set-ADServiceAccount**, und **Set-ADUser** Cmdlets mit der **PrincipalsAllowedToDelegateToAccount** Parameter.

## <a name="BKMK_SOFT"></a>Softwareanforderungen
Ressourcenbasierte eingeschränkter Delegierung kann nur auf einem Domänencontroller unter Windows Server 2012 R2 und Windows Server 2012 konfiguriert werden, aber in einer Gesamtstruktur mit gemischtem Modus angewendet werden.

Sie müssen den folgenden Hotfix installieren, auf allen Domänencontrollern unter Windows Server 2012-Benutzer Kontodomänen im Weiterleitungspfad zwischen den Front-End- und Back-End-Domänen, die älter als Windows Server-Betriebssystemen:  Ressourcenbasierte eingeschränkte Delegierung KDC_ERR_POLICY-Fehler in Umgebungen mit Windows Server 2008 R2-basierten Domänencontrollern.
