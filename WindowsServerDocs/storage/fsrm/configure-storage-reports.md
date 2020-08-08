---
title: Konfigurieren von Speicherberichten
description: In diesem Artikel wird beschrieben, wie Sie die Standardparameter für Speicher Berichte konfigurieren.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8b9d6a53b5f34c0c053de860895f5c4e48b07c83
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961494"
---
# <a name="configure-storage-reports"></a>Konfigurieren von Speicherberichten

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Sie können die Standardparameter für Speicher Berichte konfigurieren. Diese Standardparameter werden für die Vorfall Berichte verwendet, die generiert werden, wenn ein Kontingent oder ein Datei Überprüfungs Ereignis auftritt. Sie werden auch für geplante und Bedarfs gesteuerte Berichte verwendet, und Sie können die Standardparameter überschreiben, wenn Sie die spezifischen Eigenschaften dieser Berichte definieren.

> [!Important]
> Wenn Sie die Standardparameter für einen Berichtstyp ändern, wirken sich die Änderungen auf alle Vorfall Berichte und alle vorhandenen geplanten Berichts Tasks aus, die die Standardwerte verwenden.

## <a name="to-configure-the-default-parameters-for-storage-reports"></a>So konfigurieren Sie die Standardparameter für Speicher Berichte

1. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Datei Server Ressourcen-Manager**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2. Wählen Sie auf der Registerkarte **Speicher Berichte** unter **Standardparameter konfigurieren**den Berichtstyp aus, den Sie ändern möchten.

3. Klicken Sie auf **Parameter bearbeiten**.

4. Je nach ausgewähltem Berichtstyp stehen verschiedene Berichts Parameter zur Bearbeitung zur Verfügung. Führen Sie alle erforderlichen Änderungen aus, und klicken Sie dann auf **OK** , um Sie als Standardparameter für diesen Berichtstyp zu speichern.

5.  Wiederholen Sie die Schritte 2 bis 4 für jeden Berichtstyp, den Sie bearbeiten möchten.

6. Klicken Sie auf **Berichte überprüfen**, um eine Liste der Standardparameter für alle Berichte anzuzeigen. Klicken Sie anschließend auf **Schließen**.

7.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Speicherberichtmanagement](storage-reports-management.md)