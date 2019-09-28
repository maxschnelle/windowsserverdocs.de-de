---
title: Endgültiges Löschen von Nutzungsdaten
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9e1db31e4d2d714c358f2a67c2165aef91b314ba
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405609"
---
# <a name="purge-utilization-data"></a>Endgültiges Löschen von Nutzungsdaten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie Verwendungs Daten aus der IPAM-Datenbank löschen.  

Sie müssen Mitglied der Gruppe " **IPAM-Administratoren**", der Gruppe "lokale Computer **Administratoren** " oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

## <a name="to-purge-the-ipam-database"></a>So löschen Sie die IPAM-Datenbank  
1. Öffnen Sie Server-Manager, und navigieren Sie zur IPAM-Client Schnittstelle.
2. Suchen Sie einen der folgenden Speicherorte: **IP-Adress Blöcke**, **IP-Adress bestand**und **IP-Adress Bereichs Gruppen**.  
3. Klicken Sie auf **Tasks**, und klicken Sie dann auf **Verwendungs Daten**bereinigen. Das Dialogfeld **Verwendungs Daten** löschen wird geöffnet.
4. Klicken Sie unter **alle Auslastungs Daten löschen unter oder vor auf** **Datum auswählen**.
5. Wählen Sie das Datum aus, an dem Sie alle Datenbankdaten Sätze sowohl am als auch vor diesem Datum löschen möchten.
6. Klicken Sie auf **OK**. IPAM löscht alle Datensätze, die Sie angegeben haben.
