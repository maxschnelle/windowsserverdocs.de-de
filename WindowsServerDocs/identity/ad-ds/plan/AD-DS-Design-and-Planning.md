---
ms.assetid: a91339ef-6ad4-445f-8ecc-a95fbcc04296
title: AD DS-Entwurf und -Planung
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.openlocfilehash: b735852f8e2428c3d6375a3168f204e403a461f5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941456"
---
# <a name="ad-ds-design-and-planning"></a>AD DS-Entwurf und -Planung

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Durch die Bereitstellung von Windows Server Active Directory Domain Services (AD DS) in Ihrer Umgebung können Sie die Vorteile des zentralisierten, Delegierten Verwaltungsmodells und der Single Sign-On-Funktion (SSO) nutzen, die von AD DS bereitgestellt wird. Nachdem Sie die Bereitstellungs Aufgaben und die aktuelle Umgebung für Ihre Organisation ermittelt haben, können Sie die AD DS Bereitstellungs Strategie erstellen, die den Anforderungen Ihrer Organisation entspricht.

## <a name="about-this-guide"></a>Über diesen Leitfaden

Dieses Handbuch enthält Empfehlungen, die Ihnen helfen, eine AD DS Bereitstellungs Strategie basierend auf den Anforderungen Ihrer Organisation und dem jeweiligen Entwurf zu entwickeln, den Sie erstellen möchten. Dieser Leitfaden ist für Infrastrukturspezialisten oder Systemarchitekten gedacht. Bevor Sie dieses Handbuch lesen, sollten Sie wissen, wie AD DS auf einer Funktionsebene funktioniert. Außerdem sollten Sie über ein gutes Verständnis der Organisations Anforderungen verfügen, die in Ihrer AD DS Bereitstellungs Strategie berücksichtigt werden.

In dieser Anleitung werden die Aufgaben für verschiedene mögliche Ausgangspunkte einer Windows Server 2008-AD DS Bereitstellung beschrieben. Mithilfe dieses Leitfadens können Sie die am besten geeignete Bereitstellungsstrategie für Ihre Umgebung ermitteln.

Obwohl die in diesem Handbuch vorgestellten Strategien für fast alle Server-Betriebssystem Bereitstellungen geeignet sind, wurden Sie speziell für Umgebungen getestet und überprüft, die weniger als 100.000 Benutzer und weniger als 1.000 Standorte enthalten, wobei die Netzwerkverbindungen mindestens 28,8 kbit pro Sekunde (Kbit/s) betragen. Wenn Ihre Umgebung diese Kriterien nicht erfüllt, empfiehlt es sich, ein Beratungsunternehmen zu verwenden, das AD DS in komplexeren Umgebungen bereitstellt.

Weitere Informationen zum Testen des AD DS Bereitstellungs Prozesses finden Sie im Artikel [Testen und Überprüfen des Bereitstellungs Prozesses](/previous-versions/windows/it-pro/windows-server-2003/cc772722(v=ws.10)).

## <a name="in-this-guide"></a>Inhalt dieser Anleitung

[Grundlegendes zum AD DS-Entwurf](Understanding-AD-DS-Design.md)

[Bestimmen der AD DS-Entwurfs- und -Bereitstellungsanforderungen](Identifying-Your-AD-DS-Design-and-Deployment-Requirements.md)

[Zuordnen Ihrer Anforderungen zu einer AD DS-Bereitstellungsstrategie](Mapping-Your-Requirements-to-an-AD-DS-Deployment-Strategy.md)

[Entwerfen der logischen Struktur für Windows Server 2008 AD DS](Designing-the-Logical-Structure.md)

[Entwerfen der Standort Topologie für Windows Server 2008 AD DS](Designing-the-Site-Topology.md)

[Aktivieren erweiterter Funktionen für die AD DS](Enabling-Advanced-Features-for-AD-DS.md)

[Bewerten der AD DS-Bereitstellungsstrategie: Beispiele](Evaluating-AD-DS-Deployment-Strategy-Examples.md)

[Anhang A: Die wichtigsten AD DS-Begriffe](Appendix-A--Reviewing-Key-AD-DS-Terms.md)
