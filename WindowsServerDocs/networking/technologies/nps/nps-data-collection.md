---
title: Network Policy Server Sammlung von Benutzerdaten
description: Welche Informationen zur Authentifizierung von Benutzern vom Netzwerkrichtlinienserver unter Windows Server 2016 verwendet wird.
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
ms.openlocfilehash: 5bddd22c9c2f954435cc6ce37347d18c76ee7de3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888741"
---
# <a name="network-policy-server-user-data-collection"></a>Network Policy Server Sammlung von Benutzerdaten

In diesem Dokument wird erläutert, wie Sie Benutzer erfassten Daten durch die (Network Policy Server, NPS) den Fall, dass Sie sie entfernen möchten.

>[!Note]
>Wenn Sie anzeigen oder Löschen von personenbezogenen Daten interessiert sind, finden Sie in Microsoft Anweisungen in der [Windows Data Subject Requests, die dsgvo](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-windows) Standort. Wenn Sie allgemeine Informationen zur Datenschutz-Grundverordnung suchen, finden Sie unter den [DSGVO-Abschnitt des Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="information-collected-by-nps"></a>Vom NPS erfassten Daten

- Zeitstempel
- Ereigniszeitstempel
- Benutzername
- Vollständige qualifizierten Benutzernamen
- Client-IP-Adresse
- Client-Anbieter
- Client-Anzeigename
- Authentifizierungstyp
- Zahlreiche andere Felder, die über das RADIUS-Protokoll

## <a name="gather-data-from-nps"></a>Sammeln von Daten von NPS

Wenn Buchhaltungsdaten aktiviert und konfiguriert ist, können von SQL Server oder die Protokolldateien, abhängig von der Konfiguration Datensätze der NPS-Authentifizierungsversuche des Benutzers abgerufen werden. 

Wenn Buchhaltungsdaten für SQL Server konfiguriert ist, handelt es sich bei der Abfrage für alle zeichnet, in denen User_Name = `'<username>'`.

Wenn für eine Protokolldatei Buchhaltungsdaten konfiguriert ist, suchen Sie dann auf die Protokolldatei für die `<username>` finden alle Protokolleinträge.

Die Netzwerkrichtlinien- und Zugriffsdienste Ereignisprotokolleinträge gelten für die Buchhaltungsdaten vervielfältigten und nicht gesammelt werden müssen.

Wenn Buchhaltungsdaten nicht aktiviert ist, Datensätze der NPS-Authentifizierungsversuche des Benutzers aus dem die Netzwerkrichtlinien- und Zugriffsdienste-Ereignisprotokoll abgerufen werden können, durch Suchen nach den `<username>`.
