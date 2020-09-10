---
title: 'Windows-Authentifizierung: Technische Übersicht'
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 286d3e41-434f-4703-9320-706d06ebda51
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: c64df4b76c67f1dd0dbe696812d79d83b5997813
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638681"
---
# <a name="windows-authentication-technical-overview"></a>Windows-Authentifizierung: Technische Übersicht

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema für IT-Experten enthält Links zu Themen für die technische Übersicht über die Windows-Authentifizierung. Die Windows-Authentifizierung ist der Prozess, mit dem die Authentizität eines Benutzers oder dienstanzversuchs nachgewiesen werden kann, der auf Windows

In dieser Sammlung von Themen werden die Architektur der Windows-Authentifizierung und deren Komponenten beschrieben.

Klicken Sie zum digitalen Speichern oder Drucken von Seiten aus dieser Bibliothek auf **Exportieren** (oben rechts auf der Seite), und folgen Sie dann den Anweisungen.

-   [Unterschiede bei der Windows-Authentifizierung zwischen Windows-Betriebssystemen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169017(v=ws.10))

    Beschreibt die wesentlichen Unterschiede in der Authentifizierungs Architektur und den Prozessen.

-   [Windows-Authentifizierungskonzepte](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169018(v=ws.10))

    Beschreibt die Konzepte, auf denen die Windows-Authentifizierung basiert.

-   [Szenarien für die Windows-Anmelde Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169020(v=ws.10))

    Fasst die verschiedenen Anmelde Szenarien zusammen.

-   [Architektur der Windows-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169024(v=ws.10))

    Beschreibt die wesentlichen Unterschiede in der Authentifizierungs Architektur und den Prozessen für Windows-Betriebssysteme.

    -   [Architektur der Security Support Provider-Schnittstelle](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169026(v=ws.10))

        Beschreibt die SSPI-Architektur.

    -   [Anmeldeinformationen-Prozesse in der Windows-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169014(v=ws.10))

        Beschreibt die verschiedenen Prozesse zur Verwaltung von Anmelde Informationen.

-   [Bei der Windows-Authentifizierung verwendete Gruppenrichtlinien](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169021(v=ws.10))

    Beschreibt die Verwendung und Auswirkung von Gruppenrichtlinien in den Authentifizierungsprozess.

## <a name="what-is-not-covered"></a>Was nicht behandelt wird
Diese Themensammlung behandelt keine Prozeduren für das Entwerfen, implementieren oder Überwachen von Authentifizierungs Technologien innerhalb einer Windows-Umgebung.

-   Entwurfs Informationen zu Windows-Autorisierungs Strategien finden Sie unter [Entwerfen einer Ressourcen Autorisierungs Strategie](/previous-versions/windows/it-pro/windows-server-2003/cc783368(v=ws.10)).

-   Entwurfs Informationen zu Windows-Authentifizierungs Strategien finden Sie unter [Entwerfen einer Authentifizierungs Strategie](/previous-versions/windows/it-pro/windows-server-2003/cc758124(v=ws.10)).

-   Entwurfs Informationen zu den Implementierungs Strategien für die Public Key-Infrastruktur von Windows finden Sie unter [Entwerfen einer Public Key-Infrastruktur](/previous-versions/windows/it-pro/windows-server-2003/cc773138(v=ws.10)).

-   Informationen zum Konfigurieren und Überwachen der Sicherheit, einschließlich der Authentifizierung, in Ihrer Windows-Umgebung finden Sie unter:

    -   [Windows XP-Sicherheitshandbuch](https://www.microsoft.com/download/details.aspx?id=962)

    -   [Windows Vista-Sicherheitsbaseline](/previous-versions/tn-archive/dd450978(v=technet.10))

    -   [Windows Server 2003-Sicherheitsbaseline](/previous-versions/tn-archive/cc163140(v=technet.10)) und das [Handbuch zu Bedrohungen und Gegenmaßnahmen](/previous-versions/tn-archive/dd162275(v=technet.10))

    -   [Windows Server 2008-Sicherheitsleitfaden](https://www.microsoft.com/download/details.aspx?id=17606)

    -   [Windows Server 2008 R2-Sicherheitsbaseline](/previous-versions/tn-archive/gg236605(v=technet.10))

-   Informationen zum Überwachen von Anmelde-und Authentifizierungs Ereignissen in Windows finden Sie unter Überwachen von [Sicherheits Ereignissen](/previous-versions/windows/it-pro/windows-server-2003/cc776394(v=ws.10)).