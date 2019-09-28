---
title: Konfigurieren der Benachrichtigungsgrenze
description: In diesem Artikel wird beschrieben, wie Sie den verschiedene Arten von Benachrichtigungen Zeitlimits hinzufügen können
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4a33b7f125479da1e7b701f5427a0f15903caf66
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401945"
---
# <a name="configure-notification-limits"></a>Konfigurieren der Benachrichtigungsgrenze

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Um die Anzahl der sich wiederholenden, gesammelten Benachrichtigungen zu reduzieren, die einen Schwellenwert überschreiten, oder die versuchen, nicht autorisierte Datei zu speichern, setzt der Ressourcen-Manager für Dateiserver Zeitlimits für die folgenden Benachrichtigungstypen fest:

-   E-Mail
-   Ereignisprotokoll
-   Befehl
-   Bericht

Jedes Limit gibt einen Zeitraum an, bevor eine weitere konfigurierte Benachrichtigung desselben Typs für ein identisches Problem generiert wird.

Standardmäßig ist 60 Minuten für jeden Benachrichtigungstyp festgelegt, Sie können diese Grenzwerte allerdings ändern. Das Limit gilt für bestimmte Arten von Benachrichtigungen, egal ob sie über Kontingentschwellenwerte oder Dateiprüfungsereignisse generiert werden.

## <a name="to-specify-a-standard-notification-limit-for-each-notification-type"></a>So setzen Sie ein standardmäßiges Benachrichtigungslimit für jeden Benachrichtigungstyp fest

1.  Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2.  Geben Sie auf der Registerkarte **Benachrichtigungslimit** einen Wert in Minuten für jeden Benachrichtigungstyp ein, der angezeigt wird.

3.  Klicken Sie auf **OK**.

> [!Note]
> Um Zeitlimits individuell anzupassen, die Benachrichtigungen für ein bestimmtes Kontingent oder für eine Dateiprüfung zugeordnet sind, können Sie die Befehlszeilentools des Ressourcen-Manager für Dateiservers **Dirquota.exe** und **Filescrn.exe** oder die Cmdlets des [Ressourcen-Manager für Dateiservers](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager) verwenden.

## <a name="see-also"></a>Siehe auch

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Befehlszeilentools](command-line-tools.md)