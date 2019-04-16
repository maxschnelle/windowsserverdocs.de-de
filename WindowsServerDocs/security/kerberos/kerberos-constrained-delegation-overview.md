---
title: "Eingeschränkte Kerberos-Delegierung (Übersicht)"
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
ms.openlocfilehash: e90aa5e395fa43a3f94cccb13444fd6991ac1074
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="kerberos-constrained-delegation-overview"></a>Eingeschränkte Kerberos-Delegierung (Übersicht)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Übersichtsthema für IT-Experten werden neue Funktionen für die eingeschränkte Kerberos-Delegierung in Windows Server 2012 R2 und Windows Server 2012 beschrieben.

## <a name="feature-description"></a>Featurebeschreibung
Die eingeschränkte Kerberos-Delegierung wurde eingeführt, in Windows Server 2003, um eine sicherere Form der Delegierung bereitzustellen, die von Diensten verwendet werden kann. Wenn es konfiguriert ist, beschränkt die eingeschränkte Delegierung die Dienste, die der angegebene Server im Auftrag eines Benutzers agieren kann. Dies erfordert Domänenadministratorrechte so konfigurieren Sie ein Domänenkonto für einen Dienst und das Konto auf eine einzelne Domäne beschränkt. In modernen Unternehmen sind Front-End-Dienste nicht vorgesehen, auf die Integration mit Diensten in ihrer Domäne beschränkt werden sollen.

In früheren Betriebssystemversionen, in denen der Domänenadministrator der Dienst so konfiguriert, konnte der Dienstadministrator keinerlei hilfreich zu wissen, welche Front-End-Dienste, die an die ressourcendienste, die sie im Besitz delegiert. Und jeder Front-End-Dienst, der an einen Ressourcendienst delegieren konnte einen potenziellen Angriffspunkt dargestellt. Wenn ein Server, der ein Front-End-Dienst gehostet wurde beschädigt, und Delegieren an ressourcendienste konfiguriert wurde, können auch die ressourcendienste gefährdet werden.

In Windows Server 2012 R2 und Windows Server 2012 wurde die Möglichkeit zum Konfigurieren der eingeschränkten Delegierung für den Dienst vom Domänenadministrator vom Dienstadministrator übertragen. Auf diese Weise kann der Back-End-Dienstadministrator gewähren oder Verweigern von Front-End-Dienste.

Ausführliche Informationen zur eingeschränkten Delegierung in Windows Server 2003 eingeführten finden Sie unter [Kerberos-Protokollübergang und eingeschränkte Delegierung](https://technet.microsoft.com/library/cc739587(v=ws.10)).

Die Windows Server 2012 R2 und Windows Server 2012-Implementierung des Kerberos-Protokolls beinhaltet spezielle Erweiterungen für die eingeschränkte Delegierung.  Dienst für Benutzer Proxy (S4U2Proxy) ermöglicht einem Dienst mithilfe seines Kerberos-Diensttickets für einen Benutzer ein Dienstticket aus dem Schlüsselverteilungscenter (KDC) für einen Back-End-Dienst abzurufen. Diese Erweiterungen können die eingeschränkte Delegierung auf dem Back-End-Dienstkonto konfiguriert werden, die in einer anderen Domäne sein kann. Weitere Informationen zu diesen Erweiterungen finden Sie unter [\[MS-SFU\]: Kerberos-Protokollerweiterungen: Dienst für User und eingeschränkte Delegierung](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx) in der MSDN Library.

## <a name="practical-applications"></a>In der Praxis
Die eingeschränkte Delegierung ermöglicht Dienstadministratoren festlegen und erzwingen, durch das Einschränken des Bereichs, in dem Anwendungsdienste im Auftrag des Benutzers reagieren können. Dienstadministratoren können konfigurieren, die Front-End-Dienstkonten an ihre Back-End-Dienste delegieren können.

Durch die Unterstützung der eingeschränkten Delegierung für Domänen in Windows Server 2012 R2 und Windows Server 2012, können Front-End-Dienste wie Microsoft Internet Security und Acceleration (ISA) Server, Microsoft Forefront Threat Management Gateway, Microsoft Exchange Outlook Web Access (OWA) und Microsoft SharePoint Server für die um eingeschränkten Delegierung zu verwenden, um die Authentifizierung bei Servern in anderen Domänen konfiguriert werden. Dies bietet Unterstützung für domänenübergreifende dienstlösungen mit einer vorhandenen Kerberos-Infrastruktur. Eingeschränkte Kerberos-Delegierung kann von Domänenadministratoren oder Dienstadministratoren verwaltet werden.

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität
**Ressourcenbasierte eingeschränkte Delegierung über Domänengrenzen hinweg**

Eingeschränkten Delegierung bereitgestellt werden, wenn der Front-End-Dienst und die ressourcendienste nicht in derselben Domäne befinden, kann die eingeschränkte Kerberos-Delegierung verwendet werden. Dienstadministratoren können durch Angabe der Domänenkonten für Front-End-Dienste, die Benutzern für die Kontoobjekte der ressourcendienste annehmen können die neue Delegierung konfigurieren.

**Hinzufügen der Wert diese Änderung?**

Durch die Unterstützung der eingeschränkten Delegierung über Domänengrenzen hinweg, können Dienste für die um eingeschränkten Delegierung zu verwenden, um die Authentifizierung bei Servern in anderen Domänen anstelle uneingeschränkte Delegierung konfiguriert werden. Dadurch authentifizierungsunterstützung für domänenübergreifende dienstlösungen mit einer vorhandenen Kerberos-Infrastruktur ohne Front-End-Dienste für die Delegierung an einen Dienst vertrauen.

**Worin bestehen die Unterschiede?**

Eine Änderung im zugrunde liegenden Protokoll ermöglicht die eingeschränkte Delegierung über Domänengrenzen hinweg. Die Windows Server 2012 R2 und Windows Server 2012-Implementierung des Kerberos-Protokolls beinhaltet Erweiterungen des Diensts für Benutzer Proxy (S4U2Proxy)-Protokoll. Dies ist eine Gruppe von Erweiterungen für das Kerberos-Protokoll, das ermöglicht es einen Dienst, mithilfe seines Kerberos-Diensttickets für einen Benutzer zu verwenden, um ein Dienstticket aus dem Schlüsselverteilungscenter (KDC) für einen Back-End-Dienst abzurufen.

Implementierungsinformationen zu diesen Erweiterungen finden Sie [\[MS-SFU\]: Kerberos-Protokollerweiterungen: Dienst für User und eingeschränkte Delegierung](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx) in MSDN.

Weitere Informationen zur grundlegenden nachrichtensequenz für die Kerberos-Delegierung mit einem weitergeleiteten Ticket-granting Ticket (TGT) im Vergleich zu Service für Erweiterungen User (S4U) finden Sie im Abschnitt [1.3.3 Übersicht über das Protokoll](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx) in [MS-SFU]: Kerberos-Protokollerweiterungen: Dienst für User und eingeschränkte Delegierung.

Verwenden Sie Windows PowerShell-Cmdlets, um einen Ressourcendienst zum Zulassen einer Front-End-Dienst den Zugriffs auf den Namen der Benutzer zu konfigurieren.

-   Verwenden Sie zum Abrufen einer Liste von Prinzipalen die **Get-ADComputer**, **Get-ADServiceAccount**, und **Get-ADUser** Cmdlets mit der **Properties PrincipalsAllowedToDelegateToAccount** Parameter.

-   Verwenden Sie zum Konfigurieren der Ressource die **New-ADComputer**, **New-ADServiceAccount**, **New-ADUser**, **Set-ADComputer**, **Set-ADServiceAccount**, und **Set-ADUser** Cmdlets mit der **PrincipalsAllowedToDelegateToAccount** Parameter.

## <a name="BKMK_SOFT"></a>Anforderungen der Clientsoftware
Ressourcenbasierte eingeschränkte Delegierung kann nur auf einem Domänencontroller unter Windows Server 2012 R2 und Windows Server 2012 konfiguriert werden, aber in einer Gesamtstruktur mit gemischtem Modus angewendet werden.

Müssen Sie den folgenden Hotfix auf allen Domänencontrollern unter Windows Server 2012 Benutzer Kontodomänen im Weiterleitungspfad zwischen den Front-End- und Back-End-Domänen, die älter als Windows Server-Betriebssystemen anwenden: ressourcenbasierte eingeschränkte Delegierung KDC_ERR_POLICY-Fehler in Umgebungen mit Windows Server 2008 R2-basierten Domänencontrollern.
