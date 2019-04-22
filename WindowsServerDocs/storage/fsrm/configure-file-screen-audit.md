---
title: Dateiprüfungsberichte konfigurieren
description: In diesem Artikel wird beschrieben, wie Dateiprüfungsberichte konfiguriert werden, um einen einen Dateiprüfungsüberwachungs-Bericht zu erstellen
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 89592a9e1f61374d2d909678a91dc4a06e0b1972
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824471"
---
# <a name="configure-file-screen-audit"></a>Dateiprüfungsberichte konfigurieren

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Mithilfe des Ressourcen-Managers für Dateiserver können Sie die Dateiprüfungsaktivität in einer Überwachungsdatenbank aufzeichnen. Die in dieser Datenbank gespeicherten Informationen dienen zum Generieren des Dateiprüfungsüberwachungs-Berichts.

> [!Important]
> Wenn das Kontrollkästchen **Dateiprüfungsaktivität in einer Überwachungsdatenbank aufzeichnen** nicht aktiviert ist, enthalten die Dateiprüfungsüberwachungs-Berichte keine Informationen.

## <a name="to-configure-file-screen-audit"></a>So konfigurieren Sie Dateiprüfungsberichte

1.  Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2.  Wählen Sie auf der Registerkarte **Dateiprüfungsberichte** das Kontrollkästchen **Dateiprüfungsaktivität in einer Überwachungsdatenbank aufzeichnen**.

3.  Klicken Sie auf **OK**. Alle Dateiprüfungsaktivität werden jetzt in der Überwachungsdatenbank gespeichert und können durch Ausführen eines Dateiprüfungsüberwachungs-Berichts angezeigt werden.

## <a name="see-also"></a>Siehe auch

-   [Einstellung File Server Resource Manager-Optionen](setting-file-server-resource-manager-options.md)
-   [Speicherverwaltung für Berichte](storage-reports-management.md)