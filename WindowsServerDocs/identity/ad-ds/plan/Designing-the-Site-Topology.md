---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: Entwerfen der Standorttopologie
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 663b25631d1df81cceb5c25fc33bb7081ae350ae
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069292"
---
# <a name="designing-the-site-topology"></a>Entwerfen der Standorttopologie

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eine Verzeichnisdienst-Standort Topologie ist eine logische Darstellung ihres physischen Netzwerks. Das Entwerfen einer Standort Topologie für Active Directory Domain Services (AD DS) umfasst das Planen der Platzierung von Domänen Controllern und das Entwerfen von Standorten, Subnetzen, Standort Verknüpfungen und Standort Verknüpfungs Brücken, um eine effiziente Weiterleitung von Abfrage-und Replikations

Das Entwerfen einer Standort Topologie hilft Ihnen, Client Abfragen und Active Directory Replikations Datenverkehr effizient weiterzuleiten. Eine gut entworfene Standort Topologie unterstützt Ihre Organisation bei der Erzielung der folgenden Vorteile:

-   Minimieren Sie die Kosten für die Replikation Active Directory Daten.

-   Minimieren Sie den administrativen Aufwand, der für die Verwaltung der Standort Topologie erforderlich ist.

-   Planen Sie die Replikation, mit der Standorte mit langsamen oder einwählenden Netzwerkverbindungen Active Directory Daten außerhalb der Spitzenzeiten repliziert werden können.

-   Optimieren Sie die Fähigkeit von Client Computern, die nächstgelegenen Ressourcen zu finden, z. b. Domänen Controller und verteiltes Dateisystem (DFS)-Server. Dies trägt dazu bei, den Netzwerk Datenverkehr über langsame WAN-Verbindungen (Wide Area Network) zu reduzieren, Anmelde-und Abmelde Prozesse zu verbessern und Datei Download Vorgänge zu beschleunigen.

Bevor Sie mit dem Entwerfen der Standort Topologie beginnen, müssen Sie die physische Netzwerkstruktur kennen. Außerdem müssen Sie zunächst Ihre Active Directory logische Struktur entwerfen, einschließlich der administrativen Hierarchie, des Gesamtstruktur Plans und des Domänen Plans für jede Gesamtstruktur. Außerdem müssen Sie den Domain Name System-Infrastruktur Entwurf (DNS) für AD DS vervollständigen. Weitere Informationen zum Entwerfen der logischen Active Directory logischen Struktur und der DNS-Infrastruktur finden Sie unter [Entwerfen der logischen Struktur für Windows Server 2008 AD DS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770806(v=ws.10)).

Nachdem Sie den Entwurf Ihrer Standort Topologie vervollständigt haben, müssen Sie sicherstellen, dass Ihre Domänen Controller die Hardwareanforderungen für Windows Server 2008 Standard, Windows Server 2008 Enterprise und Windows Server 2008 Datacenter erfüllen.

## <a name="in-this-guide"></a>Inhalt dieser Anleitung

-   [Grundlegendes zur Active Directory-Standorttopologie](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)

-   [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md)

-   [Planen der Domänencontrollerplatzierung](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)

-   [Erstellen eines Standortentwurfs](../../ad-ds/plan/Creating-a-Site-Design.md)

-   [Erstellen eines Standortverknüpfungsentwurfs](../../ad-ds/plan/Creating-a-Site-Link-Design.md)

-   [Erstellen eines Entwurfs für Standortverknüpfungsbrücken](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)

-   [Suchen zusätzlicher Ressourcen für den Entwurf von Windows Server 2008 Active Directory-Standort Topologie](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)

