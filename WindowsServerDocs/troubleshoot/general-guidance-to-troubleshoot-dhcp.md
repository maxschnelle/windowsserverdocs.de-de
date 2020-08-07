---
title: Allgemeine Richtlinien zur Problembehandlung bei DHCP
description: Diese Artilce führt Allgemeine Anleitungen für die Problembehandlung von DHCP ein.
ms.service: na
manager: dcscontentpm
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 92b76748153f19419733c32c08a24d48e53d5647
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970047"
---
# <a name="general-guidance-to-troubleshoot-dhcp"></a>Allgemeine Richtlinien zur Problembehandlung bei DHCP

Überprüfen Sie die folgenden Elemente, bevor Sie mit der Problembehandlung beginnen. Diese können Ihnen helfen, die Ursache des Problems zu finden.

## <a name="checklist"></a>Checkliste

  - Wann fing das Problem an?

  - Gibt es Fehlermeldungen?

  - War der DHCP-Server zuvor funktionsfähig oder hat er nie funktioniert?
    Wenn zuvor gearbeitet wurde, hat sich vor dem Start des Problems etwas geändert. Wurde beispielsweise ein Update installiert? Wurde eine Änderung an der Infrastruktur vorgenommen?

  - Ist das Problem persistent oder zeitweilig? Wenn es sich um einen zeitweiligen Zeitpunkt handelt

  - Treten Fehler bei der Adress Lease für alle Clients oder nur für bestimmte Clients, z. b. ein Subnetz mit einem einzelnen Bereich, auf?

  - Befinden sich Clients im gleichen Netzwerksubnetz wie der DHCP-Server?

  - Wenn sich Clients im gleichen Netzwerksubnetz befinden, können Sie IP-Adressen abrufen?

  - Wenn sich Clients nicht im gleichen Netzwerksubnetz befinden, werden die Router oder VLAN-Switches ordnungsgemäß für DHCP-Relay-Agents (auch als IP-Hilfsprogramme bezeichnet) konfiguriert?

  - Ist der DHCP-Server eigenständig oder für hohe Verfügbarkeit konfiguriert, z. b. Split-Scope oder DHCP-Failover?

  - Überprüfen Sie die zwischen Geräte auf Features wie z. b. VRRP/HSRP, dynamische ARP-Überprüfung oder DHCP-Spionage, die bekanntermaßen Probleme verursachen.
