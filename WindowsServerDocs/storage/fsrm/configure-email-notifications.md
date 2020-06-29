---
title: E-Mail-Benachrichtigungen
description: Dieser Artikel beschreibt das Konfigurieren von e-Mail-Benachrichtigungen.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b80aef85d6f4a1d6bd8c05b56d7c1a12b456d1ed
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474187"
---
# <a name="configure-e-mail-notifications"></a>E-Mail-Benachrichtigungen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Beim Erstellen von Kontingenten und Datei Bildschirmen haben Sie die Möglichkeit, e-Mail-Benachrichtigungen an Benutzer zu senden, wenn Ihre Kontingent Grenze fast erreicht wird oder nachdem Sie versucht haben, blockierte Dateien zu speichern. Beim Generieren von Speicher Berichten haben Sie die Möglichkeit, die Berichte per e-Mail an bestimmte Empfänger zu senden. Wenn Sie bestimmte Administratoren routinemäßig über Kontingent-und Datei Prüfungs Ereignisse benachrichtigen oder Speicher Berichte senden möchten, können Sie einen oder mehrere Standard Empfänger konfigurieren.

Zum Senden dieser Benachrichtigungen und Speicher Berichte müssen Sie den SMTP-Server angeben, der für die Weiterleitung der e-Mail-Nachrichten verwendet werden soll.

## <a name="to-configure-e-mail-options"></a>Konfigurieren von e-Mail-Optionen

1. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Datei Server Ressourcen-Manager**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2. Geben Sie auf der Registerkarte **e-Mail-Benachrichtigungen** unter **SMTP-Servername oder IP-Adresse**den Hostnamen oder die IP-Adresse des SMTP-Servers ein, der e-Mail-Benachrichtigungen und Speicher Berichte weitergibt.

3. Wenn Sie bestimmte Administratoren routinemäßig über Kontingent-oder Datei Prüfungs Ereignisse oder e-Mail-Speicher Berichte benachrichtigen möchten, geben Sie unter **Standard Administrator Empfänger**jede e-Mail-Adresse ein.

   Verwenden Sie das Format <em>account@domain</em> . Verwenden Sie Semikolons zum Trennen mehrerer Konten.

4. Geben Sie unter der **Standard-e-Mail-Adresse**die e-Mail-Adresse ein, die in der Nachricht angezeigt werden soll, um eine andere "from"-Adresse für e-Mail-Benachrichtigungen und Speicher Berichte anzugeben, die vom Datei Server Ressourcen-Manager gesendet werden.

5. Klicken Sie zum Testen der Einstellungen auf **Test-e-Mail senden**.

6. Klicken Sie auf **OK**.


## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)