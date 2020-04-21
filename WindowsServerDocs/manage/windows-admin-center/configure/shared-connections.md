---
title: Konfigurieren von gemeinsam genutzten Verbindungen für alle Benutzer des Windows Admin Center-Gateways
description: Erfahren Sie, wie Administratoren ihr Windows Admin Center-Gateway (Project Honolulu) einmalig konfigurieren können, damit alle Benutzer eine einzige Verbindungsliste gemeinsam nutzen können.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 943830a2743f7cfd3192a474eb36d57f734d3d34
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269307"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Konfigurieren von gemeinsam genutzten Verbindungen für alle Benutzer des Windows Admin Center-Gateways

> Gilt für: Windows Admin Center-Vorschau, Windows Admin Center

Mit der Möglichkeit, gemeinsam genutzte Verbindungen zu konfigurieren, können Gatewayadministratoren die Verbindungsliste für alle Benutzer eines bestimmten Windows Admin Center-Gateways einmalig konfigurieren. Dieses Feature ist nur im Windows Admin Center-Dienstmodus verfügbar.

Auf der Registerkarte **Gemeinsam genutzte Verbindungen** in den Einstellungen des Windows Admin Center Gateways können Gatewayadministratoren Server, Cluster und PC-Verbindungen wie auf der Seite „Alle Verbindungen“ hinzufügen, einschließlich der Möglichkeit, Verbindungen mit Tags zu versehen. Alle zur Liste „Gemeinsam genutzte Verbindungen“ hinzugefügten Verbindungen und Tags werden für alle Benutzer dieses Windows Admin Center-Gateways auf der Seite „Alle Verbindungen“ angezeigt.
    ![](../media/shared-cnxns-1.png)

Wenn ein Windows Admin Center-Benutzer auf die Seite „Alle Verbindungen“ zugreift, nachdem gemeinsam genutzte Verbindungen konfiguriert wurden, werden ihre Verbindungen in zwei Abschnitte gruppiert: Persönliche und gemeinsam genutzte Verbindungen. Die Gruppe „Persönlich“ ist die Verbindungsliste eines bestimmten Benutzers und bleibt über die Browsersitzungen dieses Benutzers hinweg erhalten. Die Gruppe „Gemeinsam genutzte Verbindungen“ ist für alle Benutzer identisch und kann auf der Seite „Alle Verbindungen“ nicht geändert werden.
![](../media/shared-cnxns-2.png)