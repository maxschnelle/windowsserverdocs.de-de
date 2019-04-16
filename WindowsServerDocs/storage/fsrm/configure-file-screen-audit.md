---
title: "Dateiprüfungsberichte konfigurieren"
description: "In diesem Artikel wird beschrieben, wie Dateiprüfungsberichte konfiguriert werden, um einen einen Dateiprüfungsüberwachungs-Bericht zu erstellen"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 89592a9e1f61374d2d909678a91dc4a06e0b1972
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="configure-file-screen-audit"></a>Dateiprüfungsberichte konfigurieren

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Mithilfe des Ressourcen-Managers für Dateiserver können Sie die Dateiprüfungsaktivität in einer Überwachungsdatenbank aufzeichnen. Die in dieser Datenbank gespeicherten Informationen dienen zum Generieren des Dateiprüfungsüberwachungs-Berichts.

> [!Important]
> Wenn das Kontrollkästchen **Dateiprüfungsaktivität in einer Überwachungsdatenbank aufzeichnen** nicht aktiviert ist, enthalten die Dateiprüfungsüberwachungs-Berichte keine Informationen.

## <a name="to-configure-file-screen-audit"></a>So konfigurieren Sie Dateiprüfungsberichte

1.  Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2.  Wählen Sie auf der Registerkarte **Dateiprüfungsberichte** das Kontrollkästchen **Dateiprüfungsaktivität in einer Überwachungsdatenbank aufzeichnen**.

3.  Klicken Sie auf **OK**. Alle Dateiprüfungsaktivität werden jetzt in der Überwachungsdatenbank gespeichert und können durch Ausführen eines Dateiprüfungsüberwachungs-Berichts angezeigt werden.

## <a name="see-also"></a>Weitere Informationen:

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Speicherberichtmanagement](storage-reports-management.md)