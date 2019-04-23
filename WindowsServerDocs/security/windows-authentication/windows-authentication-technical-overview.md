---
title: 'Windows-Authentifizierung: Technische Übersicht'
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 286d3e41-434f-4703-9320-706d06ebda51
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 1be96846596900c7b2eb2d9d5da93e75572aac98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879251"
---
# <a name="windows-authentication-technical-overview"></a>Windows-Authentifizierung: Technische Übersicht

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema für IT-Experten enthält Links zu Themen, die technische Übersicht über Windows-Authentifizierung. Windows-Authentifizierung ist der Prozess, um die Authentizität eines Benutzers oder Diensts, den Zugriff von Windows auf zu bestätigen.

Diese Sammlung von Themen wird beschrieben, die Architektur der Windows-Authentifizierung und die zugehörigen Komponenten.

Klicken Sie zum digitalen Speichern oder Drucken von Seiten aus dieser Bibliothek auf **Exportieren** (oben rechts auf der Seite), und folgen Sie dann den Anweisungen.

-   [Unterschiede bei der Windows-Authentifizierung zwischen Windows-Betriebssystemen](https://technet.microsoft.com/library/dn169017.aspx)

    Beschreibt die wesentlichen Unterschiede bei der authentifizierungsarchitektur und Prozesse.

-   [Windows-Authentifizierungskonzepte](https://technet.microsoft.com/library/dn169018.aspx)

    Beschreibt die Konzepte, die auf der, die Windows-Authentifizierung basiert.

-   [Authentifizierungsszenarien für Windows-Anmeldung](https://technet.microsoft.com/library/dn169020.aspx)

    Fasst die verschiedenen Szenarien für die Anmeldung an.

-   [Architektur der Windows-Authentifizierung](https://technet.microsoft.com/library/dn169024.aspx)

    Beschreibt die wichtigsten Unterschiede in die authentifizierungsarchitektur und Prozesse für Windows-Betriebssysteme.

    -   [Sicherheitsarchitektur für die Schnittstelle von Support-Anbieter](https://technet.microsoft.com/library/dn169026.aspx)

        Beschreibt die SSPI-Architektur.

    -   [Anmeldeinformationen-Prozesse bei der Windows-Authentifizierung](https://technet.microsoft.com/library/dn169014.aspx)

        Beschreibt die verschiedenen Anmeldeinformationen-Management-Prozesse.

-   [Bei der Windows-Authentifizierung verwendete Gruppenrichtlinien](https://technet.microsoft.com/library/dn169021.aspx)

    Beschreibt die Verwendung und die Auswirkungen von Gruppenrichtlinien bei der Authentifizierung.

## <a name="what-is-not-covered"></a>Was nicht behandelt wird
Diese Sammlung von Themen werden Verfahren zum Entwerfen, implementieren und Überwachen Ihrer authentifizierungstechnologien in einer Windows-Umgebung nicht behandelt.

-   Informationen zum Entwurf zu Windows-autorisierungsstrategien, finden Sie unter [Entwurf einer Ressourcenautorisierungsstrategie](https://technet.microsoft.com/library/cc783368.aspx).

-   Informationen zum Entwurf für Windows-Authentifizierung-Strategien, finden Sie unter [Entwerfen einer Authentifizierungsstrategie](https://technet.microsoft.com/library/cc758124.aspx).

-   Informationen zum Entwurf für Implementierungsstrategien für Windows-public Key-Infrastruktur, finden Sie unter [Entwerfen einer Public Key-Infrastruktur](https://technet.microsoft.com/library/cc773138.aspx).

-   Konfiguration und Überwachung der Sicherheit, einschließlich der Authentifizierung in Ihrer Windows-Umgebung finden Sie unter:

    -   [Windows XP-Sicherheitshandbuch](https://www.microsoft.com/download/details.aspx?id=962)

    -   [Windows Vista Security Baseline](https://technet.microsoft.com/library/dd450978.aspx)

    -   [Windows Server 2003-Sicherheitsbaseline](https://technet.microsoft.com/library/cc163140.aspx) und [Handbuch zu Bedrohungen und Gegenmaßnahmen](https://technet.microsoft.com/library/dd162275.aspx)

    -   [Windows Server 2008-Sicherheitshandbuch](https://www.microsoft.com/download/details.aspx?id=17606)

    -   [Windows Server 2008 R2 Security Baseline](https://technet.microsoft.com/library/gg236605.aspx)

-   Weitere Informationen zur Überwachung der Anmeldung und Authentifizierung Ereignisse in Windows finden Sie unter [Überwachen von Sicherheitsereignissen](https://technet.microsoft.com/library/cc776394.aspx).


