---
title: Endgültiges Löschen von Nutzungsdaten
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8ac13abad7b55e3bb592efc63b8d05d85c13f41d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944682"
---
# <a name="purge-utilization-data"></a>Endgültiges Löschen von Nutzungsdaten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie Verwendungs Daten aus der IPAM-Datenbank löschen.

Sie müssen Mitglied der Gruppe " **IPAM-Administratoren**", der Gruppe "lokale Computer **Administratoren** " oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

## <a name="to-purge-the-ipam-database"></a>So löschen Sie die IPAM-Datenbank
1. Öffnen Sie Server-Manager, und navigieren Sie zur IPAM-Client Schnittstelle.
2. Navigieren Sie zu einem der folgenden Speicherorte: **IP-Adress Blöcke**, **IP-Adress bestand**und **IP-Adress Bereichs Gruppen**.
3. Klicken Sie auf **Tasks**, und klicken Sie dann auf **Verwendungs Daten**bereinigen. Das Dialogfeld **Verwendungs Daten** löschen wird geöffnet.
4. Klicken Sie unter **alle Auslastungs Daten löschen unter oder vor auf** **Datum auswählen**.
5. Wählen Sie das Datum aus, an dem Sie alle Datenbankdaten Sätze sowohl am als auch vor diesem Datum löschen möchten.
6. Klicken Sie auf **OK**. IPAM löscht alle Datensätze, die Sie angegeben haben.
