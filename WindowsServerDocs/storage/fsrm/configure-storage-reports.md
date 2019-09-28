---
title: Konfigurieren von Speicherberichten
description: In diesem Artikel wird beschrieben, wie Sie die Standardparameter für Speicherberichte konfigurieren
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: d3500f4ea4fc264f3cb663f17c3a50439b9cb454
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394263"
---
# <a name="configure-storage-reports"></a>Konfigurieren von Speicherberichten

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Sie können die Standardparametern für Speicherberichte konfigurieren. Diese Standardparameter werden für Schadensberichte verwendet, die generiert werden, wenn ein Kontingent- oder Dateiprüfungsereignis auftritt. Sie werden auch für geplante und bedarfsgesteuerte Berichte verwendet und Sie können die Standardparametern außerkraftsetzen, wenn Sie die spezifischen Eigenschaften dieser Berichte festlegen.

> [!Important]
> Wenn Sie die Standardparametern für einen Bericht ändern, wirkt sich dies auf alle Schadensberichte und alle vorhandenen geplanten Berichtsaufgaben aus, die die Standardwerte verwenden.

## <a name="to-configure-the-default-parameters-for-storage-reports"></a>Sie können Sie die Standardparametern für Speicherberichte konfigurieren

1. Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2. Wählen Sie auf der Registerkarte **Speicherberichte** unter **Konfigurieren von Standardparametern** den Typ des Berichts aus, den Sie ändern möchten.

3. Klicken Sie auf **Parameter bearbeiten**.

4. Je nach Art des Berichts, den Sie auswählen, stehen Ihnen unterschiedliche Berichtsparameter für die Bearbeitung zur Verfügung. Führen Sie alle notwendigen Änderungen durch, und klicken Sie dann auf **OK**, um den Standardparametern für diese Art Bericht zu speichern.

5.  Wiederholen Sie die Schritte 2 bis 4 für jede Art von Bericht, der geändert werden soll.

6. Um eine Liste mit den Standardparametern für alle Berichte anzuzeigen, klicken Sie auf **Berichte überprüfen**. Klicken Sie anschließend auf **Schließen**.

7.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Speicherberichtmanagement](storage-reports-management.md)