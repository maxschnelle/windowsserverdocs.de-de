---
title: Verwalten der Clientzugriffslizenzen
description: Erfahren Sie mehr über das Arbeiten mit CALs in Multipoint Services
ms.topic: article
ms.assetid: 675e089e-d841-401e-bba7-69f3929ef609
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 9519739eef348ca5db044319f7967a10996bbeaf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970597"
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

2. Navigieren Sie im linken Bereich zu " **lokaler Computer Richtlinien->Computer Konfiguration->administrative Vorlagen->Windows-Komponenten->Remotedesktopdienste**>Remotedesktop-Sitzungshost >-Lizenzierung.

3. Klicken Sie im rechten Bereich mit der rechten Maustaste auf **die angegebenen Remotedesktop Lizenzserver verwenden** , und wählen Sie dann **Bearbeiten**aus:
   - Wählen Sie im Dialogfeld Gruppenrichtlinien-Editor die **Option aktiviert** aus.
   - Geben Sie im Feld **zu verwendende Lizenzserver** den Namen des lokalen Computers ein.
   - Klicken Sie auf **OK**.

4. Klicken Sie im rechten Bereich mit der rechten Maustaste auf **Remotedesktop Lizenzierungs Modus festlegen** , und wählen Sie **Bearbeiten** aus.
   - Wählen Sie im Dialogfeld Gruppenrichtlinien-Editor die **Option aktiviert** aus.
   - Legen Sie den **Lizenzierungs Modus** auf pro Gerät/pro Benutzer fest.
   - Klicken Sie auf **OK**.


## <a name="see-also"></a>Weitere Informationen
[Verwalten von Systemaufgaben mithilfe des MultiPoint-Managers](Manage-System-Tasks-Using-MultiPoint-Manager.md)
