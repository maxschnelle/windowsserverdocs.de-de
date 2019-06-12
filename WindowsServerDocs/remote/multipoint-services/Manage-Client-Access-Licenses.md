---
title: Verwalten der Clientzugriffslizenzen
description: Informationen Sie zum Arbeiten mit in MultiPoint Services-CALs
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 675e089e-d841-401e-bba7-69f3929ef609
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: f5f78d3d2387d3b95177a6a8a40fb9b16d8ed8e2
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446118"
---
# <a name="manage-client-access-licenses"></a>Verwalten der Clientzugriffslizenzen
Jede Station, die eine Verbindung mit einem MultiPoint Services-System, einschließlich des Computers mit MultiPoint-Dienste, die als Station verwendet wird, müssen einen gültigen benutzerspezifische Remotedesktop *-Clientzugriffslizenz (CAL)* .

Wenn Sie virtuelle desktopstationen anstelle von physischen Stationen verwenden, müssen Sie eine Clientzugriffslizenz für jede Station virtuellen Desktop installieren.  
  
1.  Erwerben Sie eine Clientzugriffslizenz für jede Station, die mit Ihrem MultiPoint Services-Computer oder Server verbunden ist. Weitere Informationen über den Erwerb von CALs finden Sie auf die Dokumentation für die Remotedesktop-Lizenzierung. <!--@Liza: add link to RDS licensing here-->

2.  Von der **starten** öffnen **MultiPoint-Manager**.  
  
3.  Klicken Sie auf die **Startseite** Registerkarte, und klicken Sie dann auf **Clientzugriffslizenzen hinzufügen**.  Dadurch wird das Verwaltungstool für CAL-Lizenzierung geöffnet.

# <a name="set-the-licensing-mode-manually"></a>Legen Sie den Lizenzierungsmodus manuell fest.
Wenn nicht ordnungsgemäß konfiguriert das MultiPoint Services-Setup eine Benachrichtigung über die Toleranzperiode abgelaufen wird fordert. Um den Lizenzierungsmodus festgelegt, gehen Sie wie folgt vor:

1. Starten Sie **Editor für lokale Gruppenrichtlinien** (gpedit.msc).

2. Navigieren Sie im linken Bereich zu **Richtlinien für Lokaler Computer -> Computerkonfiguration-> Administrative Vorlagen -> Windows-Komponenten -> Remote Desktop Services - > Remote Desktop Session Host-Lizenzierung >** .

3. Klicken Sie im rechten Bereich mit der rechten Maustaste **verwenden Sie die angegebenen Remotedesktop-Lizenzserver** , und wählen Sie **bearbeiten**:
   - Wählen Sie im Editor-Dialogfeld **aktiviert**
   - Geben Sie den Namen des lokalen Computers in die **zu verwendende Lizenzserver** Feld.
   - Wählen Sie **OK**
  
4. Klicken Sie im rechten Bereich mit der rechten Maustaste **legen Sie den Remotedesktop-Lizenzierungsmodus** , und wählen Sie **bearbeiten**
   - Wählen Sie im Editor-Dialogfeld **aktiviert**
   - Legen Sie die **Lizenzierungsmodus** um pro Gerät / pro Benutzer
   - Wählen Sie **OK** 

  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Systemaufgaben mithilfe des MultiPoint-Managers](Manage-System-Tasks-Using-MultiPoint-Manager.md)
