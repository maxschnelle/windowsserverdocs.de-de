---
title: Konfigurieren der Benachrichtigungsgrenze
description: In diesem Artikel wird beschrieben, wie Sie verschiedenen Benachrichtigungs Typen Zeitlimits hinzufügen.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5b9bda5ffb225cc05df7d45e8b611e0154f9e582
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961532"
---
# <a name="configure-notification-limits"></a>Konfigurieren der Benachrichtigungsgrenze

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Um die Anzahl der Benachrichtigungen zu verringern, die sich für das wiederholte überschreiten eines Kontingent Schwellenwerts oder des Versuchs, eine nicht autorisierte Datei zu speichern, wendet der Datei Server Ressourcen-Manager Zeitlimits auf die folgenden Benachrichtigungs Typen an

-   E-Mail
-   Ereignisprotokoll
-   Befehl
-   Bericht

Jede Grenze gibt einen Zeitraum an, bevor eine andere konfigurierte Benachrichtigung desselben Typs für ein identisches Problem generiert wird.

Für jeden Benachrichtigungstyp wird ein Standard Limit von 60 Minuten festgelegt. Sie können diese Limits jedoch ändern. Das Limit gilt für alle Benachrichtigungen eines bestimmten Typs, unabhängig davon, ob Sie durch Kontingent Schwellenwerte oder durch Datei Überprüfungs Ereignisse generiert werden.

## <a name="to-specify-a-standard-notification-limit-for-each-notification-type"></a>So geben Sie ein Standard Benachrichtigungs Limit für jeden Benachrichtigungstyp an

1.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Datei Server Ressourcen-Manager**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2.  Geben Sie auf der Registerkarte **Benachrichtigungs Limits** für jeden angezeigten Benachrichtigungstyp einen Wert in Minuten ein.

3.  Klicken Sie auf **OK**.

> [!Note]
> Zum Anpassen von Zeitlimits, die Benachrichtigungen für ein bestimmtes Kontingent oder einen bestimmten Datei Bildschirm zugeordnet sind, können Sie den Dateiserver Ressourcen-Manager Befehlszeilen Tools **Dirquota.exe** und **Filescrn.exe**verwenden oder die [Dateiserver Ressourcen-Manager](/powershell/module/fileserverresourcemanager/?view=win10-ps) -Cmdlets verwenden.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Befehlszeilentools](command-line-tools.md)
