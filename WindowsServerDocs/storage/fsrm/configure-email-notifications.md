---
title: Konfigurieren von E-Mail-Benachrichtigungen
description: In diesem Artikel wird beschrieben, wie Sie E-Mail-Benachrichtigungen konfigurieren
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9fef24dccc71eab49fa8c77f0f80d5ec3b3a9327
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402023"
---
# <a name="configure-e-mail-notifications"></a>Konfigurieren von E-Mail-Benachrichtigungen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Beim Erstellen von Kontingenten und Dateibildschirmen haben Sie die Option, E-Mail-Benachrichtigungen an Benutzer zu senden, wenn ihre Kontingentbegrenzung erreicht wird oder nachdem sie versucht haben, gesperrte Dateien zu speichern. Wenn Sie Speicherberichte generieren, können Sie die Berichte per E-Mail an bestimmte Empfänger senden. Wenn Sie bestimmte Administratoren routinemäßig über Kontingent- und Dateiprüfungsereignisse benachrichtigen oder Speicherberichte senden möchten, können Sie einen oder mehrere standardmäßige Empfänger konfigurieren.

Zum Senden dieser Benachrichtigungen und der Speicherberichte müssen Sie den zum Weiterleiten der E-Mails verwendeten SMTP-Server angeben.

## <a name="to-configure-e-mail-options"></a>So konfigurieren Sie E-Mail-Optionen neu

1. Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2. Geben Sie auf der Registerkarte **E-Mail-Benachrichtigungen** unter **SMTP-Servername oder IP-Adresse** den Hostnamen oder die IP-Adresse für den SMTP-Server ein, der E-Mail-Benachrichtigungen oder Speicherberichte weiterleiten soll.

3. Wenn Sie bestimmte Administratoren routinemäßig über Kontingent- oder Dateiprüfungsereignisse benachrichtigen oder Speicherberichte per E-Mail senden möchten, geben Sie unter **Standardadministratorempfänger** jede E-Mail-Adresse ein.

   Verwenden Sie das Format <em>account@domain</em>. Trennen Sie mehrere Konten durch Semikolons.

4. Um eine andere „Von”-Adresse für E-Mail-Benachrichtigungen und Berichte zu verwenden, die vom Ressourcen-Manager für Dateiserver gesendet werden, klicken Sie geben Sie in der **Standard-E-Mail-Adresse des Absenders** die E-Mail-Adresse ein, die Sie in der Nachricht angezeigt werden soll.

5. Klicken Sie zum Testen Ihrer Einstellungen auf **Test-E-Mail senden**.

6. Klicken Sie auf **OK**.


## <a name="see-also"></a>Siehe auch

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)