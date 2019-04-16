---
title: Konfigurieren von gemeinsam genutzten Verbindungen für alle Benutzer von Windows Admin Center-gateway
description: Erfahren Sie, wie Administratoren ihre Windows Admin Center (Projekt Honolulu)-Gateway einmal konfigurieren können, um alle Benutzer, die eine einzelne Liste von Verbindungen zu teilen können.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1bdafa0d23934666fc0f6985249502e4960dc38e
ms.sourcegitcommit: 74d9eee13386a039186a70cdc97dc0b82e74bbf4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/29/2019
ms.locfileid: "9271013"
---
# Konfigurieren von gemeinsam genutzten Verbindungen für alle Benutzer von Windows Admin Center-gateway

> Gilt für: Windows Admin Center Vorschau

Mit der Fähigkeit zum Konfigurieren von gemeinsam genutzten Verbindungen können Administratoren Gateway die Verbindungsliste einmal für alle Benutzer eines bestimmten Windows Admin Center-Gateways konfigurieren. 

Auf der Registerkarte **Freigegeben Verbindungen** von Windows Admin Center-Gateway Einstellungen können Gateway Administratoren Servern, Clustern und PC-Anschlüsse hinzufügen, wie Sie von der Seite alle Verbindungen angezeigt, einschließlich der Möglichkeit, Tag-Verbindungen. Alle Verbindungen und Tags, die in der Liste Verbindungen freigegeben hinzugefügt werden für alle Benutzer eines dieser Windows Admin Center-Gateway, aus deren alle Verbindungen Seiten angezeigt.
    ![](../media/shared-cnxns-1.png)

Wenn jeder Windows Admin Center-Benutzer die Seite "Alle Verbindungen" zugreift, nachdem freigegeben Verbindungen konfiguriert wurden, sehen sie die Verbindungen, die in zwei Abschnitte unterteilt: persönliche und Shared-Verbindungen. Die persönliche Gruppe eines bestimmten Benutzers Verbindung Liste und sitzungsübergreifend Browser des Benutzers beibehalten. Die Gruppe der freigegebenen Verbindungen ist in allen Benutzern identisch, und kann nicht von der Seite "alle Verbindungen" geändert werden.
![](../media/shared-cnxns-2.png)