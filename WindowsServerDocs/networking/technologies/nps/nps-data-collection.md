---
title: Benutzerdaten Sammlung für Netzwerk Richtlinien Server
description: Welche Informationen verwendet werden, um Benutzer bei der Authentifizierung von Benutzern durch den Netzwerk Richtlinien Server unter Windows Server 2016 zu unterstützen.
author: MicrosoftGuyJFlo
manager: mtillman
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: 05/01/2018
ms.openlocfilehash: def65c174ff608301f8d4f35ef1ce19818103e61
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859373"
---
# <a name="network-policy-server-user-data-collection"></a>Benutzerdaten Sammlung für Netzwerk Richtlinien Server

In diesem Dokument wird erläutert, wie Sie die vom Netzwerk Richtlinien Server (Network Policy Server, NPS) gesammelten Benutzerinformationen für das Ereignis ermitteln, das Sie entfernen möchten.

>[!Note]
>Wenn Sie personenbezogene Daten anzeigen oder löschen möchten, lesen Sie den Leitfaden von Microsoft in den [Windows-Datensubjekt Anforderungen für die](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-windows) dsgvo-Website. Allgemeine Informationen zur dsgvo finden Sie im Abschnitt zur dsgvo [des Dienst Vertrauensstellungs Portals](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="information-collected-by-nps"></a>Von NPS gesammelte Informationen

- Timestamp
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

Wenn Buchhaltungsdaten für SQL Server konfiguriert sind, Fragen Sie alle Datensätze ab, bei denen user_name = `'<username>'`ist.

Wenn Buchhaltungsdaten für eine Protokolldatei konfiguriert sind, suchen Sie in der Protokolldatei nach den `<username>`, um alle Protokolleinträge zu finden.

Die Ereignisprotokoll Einträge für Netzwerk Richtlinien-und Zugriffs Dienste gelten als Duplizierung der Buchhaltungsdaten und müssen nicht gesammelt werden.

Wenn die Buchhaltungsdaten nicht aktiviert sind, können Datensätze der NPS-Authentifizierungs Versuche eines Benutzers aus dem Ereignisprotokoll für die Netzwerk Richtlinien-und Zugriffs Dienste abgerufen werden, indem Sie nach dem `<username>`suchen.
