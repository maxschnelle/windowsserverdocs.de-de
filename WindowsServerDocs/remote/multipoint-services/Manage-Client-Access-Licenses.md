---
title: Verwalten der Clientzugriffslizenzen
description: Erfahren Sie mehr über das Arbeiten mit CALs in Multipoint Services
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4d809ab1bf2a18dff537bf63620623d576c0b25d
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949884"
---
# <a name="manage-client-access-licenses"></a>Verwalten der Clientzugriffslizenzen
Jede Station, die eine Verbindung mit einem Multipoint Services-System herstellt, einschließlich des Computers, auf dem Multipoint Services ausgeführt wird und als Station verwendet wird, muss über eine gültige benutzerspezifische Remotedesktop *Client Zugriffslizenz (CAL)* verfügen.

Wenn Sie virtuelle Station-Desktops anstelle physischer Stationen verwenden, müssen Sie für jeden virtuellen Computer der Station eine Client Zugriffslizenz (CAL) installieren.  
  
1.  Erwerben Sie eine Client Lizenz für jede Station, die mit Ihrem Multipoint Services-Computer oder-Server verbunden ist. Weitere Informationen zum Erwerb von CALs finden Sie in der Dokumentation zur Remotedesktop Lizenzierung. 

2.  Öffnen Sie auf dem **Start** Bildschirm den **Multipoint-Manager**.  
  
3.  Klicken Sie auf die Registerkarte **Start** , und klicken Sie dann auf **Client Zugriffs Lizenzen hinzufügen**.  Dadurch wird das Verwaltungs Tool für die CAL-Lizenzierung geöffnet.

## <a name="set-the-licensing-mode-manually"></a>Manuelles Festlegen des Lizenzierungs Modus
Wenn diese Einstellung nicht ordnungsgemäß konfiguriert ist, wird bei der Einrichtung von Multipoint Services eine Benachrichtigung über den Ablauf der Toleranz Periode angezeigt. Führen Sie diese Schritte aus, um den Lizenzierungs Modus festzulegen:

1. Starten Sie **Editor für lokale Gruppenrichtlinien** (gpeer dit. msc).

2. Navigieren Sie im linken Bereich zu " **lokaler Computer Richtlinien-> Computer Konfiguration-> Administrative Vorlagen-> Windows-Komponenten-> Remotedesktopdienste**> Remotedesktop-Sitzungshost >-Lizenzierung.

3. Klicken Sie im rechten Bereich mit der rechten Maustaste auf **die angegebenen Remotedesktop Lizenzserver verwenden** , und wählen Sie dann **Bearbeiten**aus:
   - Wählen Sie im Dialogfeld Gruppenrichtlinien-Editor die **Option aktiviert** aus.
   - Geben Sie im Feld **zu verwendende Lizenzserver** den Namen des lokalen Computers ein.
   - Wählen Sie **OK** aus
  
4. Klicken Sie im rechten Bereich mit der rechten Maustaste auf **Remotedesktop Lizenzierungs Modus festlegen** , und wählen Sie **Bearbeiten** aus.
   - Wählen Sie im Dialogfeld Gruppenrichtlinien-Editor die **Option aktiviert** aus.
   - Legen Sie den **Lizenzierungs Modus** auf pro Gerät/pro Benutzer fest.
   - Wählen Sie **OK** aus 

  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Systemaufgaben mithilfe des MultiPoint-Managers](Manage-System-Tasks-Using-MultiPoint-Manager.md)
