---
title: Konfigurieren von freigegebenen Verbindungen für alle Benutzer des Windows Admin Center-Gateways
description: Erfahren Sie, wie Administratoren Ihr Windows Admin Center-Gateway (Project Honolulu) einmal konfigurieren können, damit alle Benutzer eine einzelne Liste von Verbindungen gemeinsam nutzen können.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 46075154a225590376458881768ae86f74a572ad
ms.sourcegitcommit: 286e3181ebd2cb9d7dc7fe651858a4e0d61d153f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300728"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Konfigurieren von freigegebenen Verbindungen für alle Benutzer des Windows Admin Center-Gateways

> Gilt für: Windows Admin Center Preview, Windows Admin Center

Mit der Möglichkeit, freigegebene Verbindungen zu konfigurieren, können gatewayadministratoren die Verbindungsliste für alle Benutzer eines bestimmten Windows Admin Center-Gateways einmal konfigurieren. 

Auf der Registerkarte frei **gegebene Verbindungen** in den Einstellungen des Windows Admin Center-Gateways können gatewayadministratoren Server, Cluster und PC-Verbindungen wie auf der Seite alle Verbindungen hinzufügen, einschließlich der Möglichkeit, Verbindungen zu markieren. Alle in der Liste Shared Connections hinzugefügten Verbindungen und Tags werden für alle Benutzer dieses Windows Admin Center-Gateways auf der Seite alle Verbindungen angezeigt.
    ![](../media/shared-cnxns-1.png)

Wenn ein Windows Admin Center-Benutzer auf die Seite "alle Verbindungen" zugreift, nachdem freigegebene Verbindungen konfiguriert wurden, sehen Sie, dass ihre Verbindungen in zwei Abschnitte gruppiert werden: Persönliche und freigegebene Verbindungen. Die Gruppe persönlich ist eine bestimmte Verbindungsliste eines Benutzers und bleibt in den Browsersitzungen dieses Benutzers erhalten. Die Gruppe "freigegebene Verbindungen" ist für alle Benutzer identisch und kann nicht auf der Seite "alle Verbindungen" geändert werden.
![](../media/shared-cnxns-2.png)