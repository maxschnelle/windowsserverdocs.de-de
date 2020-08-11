---
title: Konfigurieren von gemeinsam genutzten Verbindungen für alle Benutzer des Windows Admin Center-Gateways
description: Erfahren Sie, wie Administratoren ihr Windows Admin Center-Gateway (Project Honolulu) einmalig konfigurieren können, damit alle Benutzer eine einzige Verbindungsliste gemeinsam nutzen können.
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: eea0e467629a6110d38ed3081a1320e002496cfb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970877"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Konfigurieren von gemeinsam genutzten Verbindungen für alle Benutzer des Windows Admin Center-Gateways

> Gilt für: Windows Admin Center-Vorschau, Windows Admin Center

Mit der Möglichkeit, gemeinsam genutzte Verbindungen zu konfigurieren, können Gatewayadministratoren die Verbindungsliste für alle Benutzer eines bestimmten Windows Admin Center-Gateways einmalig konfigurieren. Dieses Feature ist nur im Windows Admin Center-Dienstmodus verfügbar.

Auf der Registerkarte **Gemeinsam genutzte Verbindungen** in den Einstellungen des Windows Admin Center Gateways können Gatewayadministratoren Server, Cluster und PC-Verbindungen wie auf der Seite „Alle Verbindungen“ hinzufügen, einschließlich der Möglichkeit, Verbindungen mit Tags zu versehen. Alle zur Liste „Gemeinsam genutzte Verbindungen“ hinzugefügten Verbindungen und Tags werden für alle Benutzer dieses Windows Admin Center-Gateways auf der Seite „Alle Verbindungen“ angezeigt.

![Windows Admin Center – Seite „Freigegebene Verbindungen“](../media/shared-cnxns-1.png)

Wenn ein Windows Admin Center-Benutzer auf die Seite „Alle Verbindungen“ zugreift, nachdem gemeinsam genutzte Verbindungen konfiguriert wurden, werden ihre Verbindungen in zwei Abschnitte gruppiert: Persönliche und gemeinsam genutzte Verbindungen. Die Gruppe „Persönlich“ ist die Verbindungsliste eines bestimmten Benutzers und bleibt über die Browsersitzungen dieses Benutzers hinweg erhalten. Die Gruppe „Gemeinsam genutzte Verbindungen“ ist für alle Benutzer identisch und kann auf der Seite „Alle Verbindungen“ nicht geändert werden.

![Windows Admin Center – Seite „Alle Verbindungen“](../media/shared-cnxns-2.png)