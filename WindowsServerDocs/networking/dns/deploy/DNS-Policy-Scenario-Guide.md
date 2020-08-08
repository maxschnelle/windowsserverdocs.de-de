---
title: Handbuch zu DNS-Gruppenrichtlinienszenarien
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 50fdb08a-bbd8-4107-954a-6699672110ff
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ed28fe6dd472b505d2a39ac55c74c399ef63e068
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966657"
---
# <a name="dns-policy-scenario-guide"></a>Handbuch zu DNS-Gruppenrichtlinienszenarien

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Handbuch ist für die Verwendung durch DNS-, Netzwerk-und Systemadministratoren vorgesehen.

Die DNS-Richtlinie ist ein neues Feature für DNS in Windows Server &reg; 2016. In dieser Anleitung erfahren Sie, wie Sie mithilfe der DNS-Richtlinie steuern, wie ein DNS-Server namens Auflösungs Abfragen basierend auf anderen Parametern verarbeitet, die Sie in Richtlinien definieren.

Dieser Leitfaden enthält eine Übersicht über die DNS-Richtlinien sowie spezifische DNS-Richtlinien Szenarien, in denen Sie Anweisungen zum Konfigurieren des DNS-Server Verhaltens zum Erreichen ihrer Ziele finden, einschließlich der georedundantenbasierten Datenverkehrs Verwaltung für primäre und sekundäre DNS-Server, Hochverfügbarkeit von Anwendungen, Split-Brain-DNS und mehr.

Dieses Handbuch enthält die folgenden Abschnitte:

- [DNS-Richtlinien Übersicht](DNS-Policies-Overview.md)
- [Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit Primärservern](primary-geo-location.md)
- [Verwenden von DNS-Richtlinien für eine auf Geolocation basierende Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen](primary-secondary-geo-location.md)
- [Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit](dns-tod-intelligent.md)
- [DNS-Antworten basierend auf der Tageszeit mit einem Azure Cloud App-Server](dns-tod-azure-cloud-app-server.md)
- [Verwenden der DNS-Richtlinie für Split-Brain-DNS](split-brain-DNS-deployment.md)
- [Verwenden der DNS-Richtlinie für Split-Brain-DNS in Active Directory](dns-sb-with-ad.md)
- [Verwenden der DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen](apply-filters-on-dns-queries.md)
- [Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich](app-lb.md)
- [Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich mit Geolocation-Informationen](app-lb-geo.md)

