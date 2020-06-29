---
title: Konfigurieren von Speicherberichten
description: In diesem Artikel wird beschrieben, wie Sie die Standardparameter für Speicher Berichte konfigurieren.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 94d1b75bba4edac5ad8df80adb13d95a7b8dec39
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474157"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Speicherberichtmanagement](storage-reports-management.md)