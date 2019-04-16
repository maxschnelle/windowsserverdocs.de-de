---
title: Endgültiges Löschen von Nutzungsdaten
description: Dieses Thema ist Teil des Handbuchs Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c41be119099aed4867df1bae1a55e2fbaa5c9064
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="purge-utilization-data"></a>Endgültiges Löschen von Nutzungsdaten

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zum Löschen von Nutzungsdaten aus der IPAM-Datenbank.  

Sie müssen ein Mitglied sein **IPAM-Administratoren**, dem lokalen Computer **Administratoren** Gruppe oder eine entsprechende Berechtigung, um dieses Verfahren auszuführen.

## <a name="to-purge-the-ipam-database"></a>Die IPAM-Datenbank gelöscht.  
1. Öffnen Sie Server-Manager, und suchen Sie anschließend die IPAM-Client-Benutzeroberfläche.
2. Suchen Sie einen der folgenden Speicherorte: **IP-Adressblöcke**, **IP-Adressbestand**, oder **IP-Adressbereichsgruppen**.  
3. Klicken Sie auf **Aufgaben**, und klicken Sie dann auf **Löschen von Nutzungsdaten**. Die **Löschen von Nutzungsdaten** Dialogfeld wird geöffnet.
4. In **löschen Sie alle Auslastung Daten am oder vor dem**, klicken Sie auf **wählen Sie ein Datum**.
5. Wählen Sie das Datum für das Sie alle Datensätze auf und vor diesem Zeitpunkt löschen möchten.
6. Klicken Sie auf **OK**. IPAM löscht alle Datensätze, die Sie angegeben haben.
