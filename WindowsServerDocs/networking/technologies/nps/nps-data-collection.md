---
title: Benutzerdaten Sammlung für Netzwerk Richtlinien Server
description: Welche Informationen verwendet werden, um Benutzer bei der Authentifizierung von Benutzern durch den Netzwerk Richtlinien Server unter Windows Server 2016 zu unterstützen.
author: MicrosoftGuyJFlo
manager: mtillman
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.date: 05/01/2018
ms.openlocfilehash: cd145402ed70aa52da7188dee9dd64ce17fea155
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871877"
---
# <a name="network-policy-server-user-data-collection"></a>Benutzerdaten Sammlung für Netzwerk Richtlinien Server

In diesem Dokument wird erläutert, wie Sie die vom Netzwerk Richtlinien Server (Network Policy Server, NPS) gesammelten Benutzerinformationen für das Ereignis ermitteln, das Sie entfernen möchten.

>[!Note]
>Wenn Sie personenbezogene Daten anzeigen oder löschen möchten, lesen Sie den Leitfaden von Microsoft in den [Windows-Datensubjekt Anforderungen für die](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-windows) dsgvo-Website. Allgemeine Informationen zur dsgvo finden Sie im Abschnitt zur dsgvo [des Dienst Vertrauensstellungs Portals](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="information-collected-by-nps"></a>Von NPS gesammelte Informationen

- Zeitstempel
- Ereigniszeitstempel
- Benutzername
- Voll qualifizierter Benutzername
- Client-IP-Adresse
- Client Hersteller
- Anzeige Name des Clients
- Authentifizierungstyp
- Zahlreiche andere Felder für das RADIUS-Protokoll

## <a name="gather-data-from-nps"></a>Sammeln von Daten aus NPS

Wenn Buchhaltungsdaten aktiviert und konfiguriert sind, können die Datensätze der NPS-Authentifizierungs Versuche eines Benutzers abhängig von der Konfiguration von SQL Server oder den Protokolldateien abgerufen werden. 

Wenn Buchhaltungsdaten für SQL Server konfiguriert sind, Fragen Sie alle Datensätze ab, `'<username>'`in denen user_name = ist.

Wenn Buchhaltungsdaten für eine Protokolldatei konfiguriert sind, suchen `<username>` Sie in der Protokolldatei nach allen Protokoll Einträgen.

Die Ereignisprotokoll Einträge für Netzwerk Richtlinien-und Zugriffs Dienste gelten als Duplizierung der Buchhaltungsdaten und müssen nicht gesammelt werden.

Wenn die `<username>`Kontoführungs Daten nicht aktiviert sind, können Datensätze der NPS-Authentifizierungs Versuche eines Benutzers aus dem Ereignisprotokoll der Netzwerk Richtlinien-und Zugriffs Dienste abgerufen werden, indem Sie nach suchen.
