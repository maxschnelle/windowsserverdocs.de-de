---
title: Handbuch zu DNS-Gruppenrichtlinienszenarien
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 50fdb08a-bbd8-4107-954a-6699672110ff
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8fab127fcd524526a515752871c1a3db92047c46
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406223"
---
# <a name="dns-policy-scenario-guide"></a>Handbuch zu DNS-Gruppenrichtlinienszenarien

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Handbuch ist für die Verwendung durch DNS-, Netzwerk-und Systemadministratoren vorgesehen.  
  
Die DNS-Richtlinie ist ein neues Feature für DNS in Windows Server&reg; 2016. In dieser Anleitung erfahren Sie, wie Sie mithilfe der DNS-Richtlinie steuern, wie ein DNS-Server namens Auflösungs Abfragen basierend auf anderen Parametern verarbeitet, die Sie in Richtlinien definieren.   
  
Dieser Leitfaden enthält eine Übersicht über die DNS-Richtlinien sowie spezifische DNS-Richtlinien Szenarien, in denen Sie Anweisungen zum Konfigurieren des DNS-Server Verhaltens zum Erreichen ihrer Ziele finden, einschließlich der georeduntbasierten Datenverkehrs Verwaltung für primäre und sekundäre DNS-Server, Hochverfügbarkeit von Anwendungen, Split-Brain-DNS und mehr.  
  
Dieses Handbuch enthält die folgenden Abschnitte:  
  
- [DNS-Richtlinien Übersicht](DNS-Policies-Overview.md)  
- [Verwenden der DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung mit primären Servern](primary-geo-location.md)  
- [Verwenden der DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung mit primären sekundären bereit Stellungen](primary-secondary-geo-location.md)  
- [Verwenden der DNS-Richtlinie für intelligente DNS-Antworten basierend auf der Tageszeit](dns-tod-intelligent.md)
- [DNS-Antworten basierend auf der Tageszeit mit einem Azure Cloud App-Server](dns-tod-azure-cloud-app-server.md)
- [Verwenden der DNS-Richtlinie für Split-Brain-DNS](split-brain-DNS-deployment.md)
- [Verwenden der DNS-Richtlinie für Split-Brain-DNS in Active Directory](dns-sb-with-ad.md)
- [Verwenden der DNS-Richtlinie zum Anwenden von Filtern auf DNS-Abfragen](apply-filters-on-dns-queries.md)
- [Verwenden der DNS-Richtlinie für den Anwendungs Lastenausgleich](app-lb.md)
- [Verwenden der DNS-Richtlinie für den Anwendungs Lastenausgleich mit georedundanstand](app-lb-geo.md)

