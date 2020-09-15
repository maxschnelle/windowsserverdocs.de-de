---
title: Erste Schritte mit dem Windows-Desktopclient
description: Grundlegende Informationen zum Windows-Desktopclient.
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 09/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: cb1c519e6da55bb6ee8187db4b388870f1d4b42f
ms.sourcegitcommit: 34f9577ef32cbdc7ef96040caabc9d83517f9b79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/08/2020
ms.locfileid: "89554467"
---
# <a name="get-started-with-the-windows-desktop-client"></a>Erste Schritte mit dem Windows-Desktopclient

>Gilt für: Windows 10, Windows 10 IoT Enterprise und Windows 7

Du kannst den Remotedesktopclient für Windows-Desktop verwenden, um Windows-Apps und -Desktops über ein anderes Windows-Gerät per Remotezugriff zu nutzen.

> [!NOTE]
> - Diese Dokumentation bezieht sich nicht auf den Remotedesktopverbindungs-Client (MSTSC), der mit Windows geliefert wird. Sie bezieht sich auf den neuen Remotedesktopclient (MSRDC).
> - Dieser Client unterstützt derzeit nur den Zugriff auf Remote-Apps und -Desktops aus dem [virtuellen Windows-Desktop](https://aka.ms/wvd).
> - Möchtest du mehr über die neuen Versionen für den Windows-Desktopclient erfahren? [Neuigkeiten im Windows-Desktopclient](windowsdesktop-whatsnew.md) ansehen

## <a name="install-the-client"></a>Installieren des Clients

Wähle den Client aus, der der Windows-Version entspricht. Der neue Remotedesktopclient (MSRDC) unterstützt Windows 10-, Windows 10 IoT Enterprise- und Windows 7-Clientgeräte.

- [Windows 64-Bit](https://go.microsoft.com/fwlink/?linkid=2068602)
- [Windows 32-Bit](https://go.microsoft.com/fwlink/?linkid=2098960)
- [Windows ARM64](https://go.microsoft.com/fwlink/?linkid=2098961)

Du kannst den Client für den aktuellen Benutzer installieren – dafür sind keine Administratorrechte erforderlich –, oder dein Administrator kann den Client installieren und ihn so konfigurieren, dass alle Benutzer des Geräts darauf zugreifen können.

Nachdem Du den Client installiert hast, kannst du ihn aus dem Startmenü starten, indem du nach **Remotedesktop** suchst.

## <a name="update-the-client"></a>Update des Clients

Du wirst benachrichtigt, wenn eine neue Version des Clients verfügbar ist, sofern Benachrichtigungen nicht durch deinen Administrator deaktiviert wurden. Die Benachrichtigung wird entweder im Connection Center oder im Windows Info-Center angezeigt. Um deinen Client zu aktualisieren, wähle die Benachrichtigung einfach aus.

Du kannst außerdem manuell nach neuen Updates für den Client suchen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) in der Befehlsleiste am oberen Rand des Clients.
2. Wähle im Dropdownmenü **Info** aus.
3. Der Client sucht automatisch nach Updates.
4. Wenn ein Update verfügbar ist, tippe auf **Update installieren**, um ein Update des Clients auszuführen.

## <a name="workspaces"></a>Arbeitsbereiche

Rufe die Liste der verwalteten Ressourcen ab, auf die du Zugriff hast, wie etwa Apps und Desktops, indem du den Arbeitsbereich abonnierst, den der Administrator für dich bereitgestellt hat. Wenn du abonnierst, werden die Ressourcen auf deinem lokalen PC verfügbar. Der Windows-Desktopclient unterstützt aktuell Ressourcen, die vom virtuellen Windows-Desktop veröffentlicht wurden.

### <a name="subscribe-to-a-workspace"></a>Abonnieren eines Arbeitsbereichs

Es gibt zwei Möglichkeiten zum Abonnieren eines Arbeitsbereichs. Der Client kann versuchen, die Ressourcen, die dir über dein Geschäfts- oder Schul-/Unikonto zur Verfügung stehen, zu ermitteln, oder du kannst die URL, unter der deine Ressourcen zu finden sind, direkt angeben, falls der Client sie nicht finden kann. Sobald du einen Arbeitsbereich abonniert hast, kannst du Ressourcen mit einer der folgenden Methoden starten:

- Wechsle zum Connection Center, und doppelklicke auf eine Ressource, um sie zu starten.
- Alternativ kannst du zum Startmenü navigieren und nach einem Ordner mit dem Namen des Arbeitsbereichs suchen oder den Namen der Ressource in die Suchleiste eingeben.

#### <a name="subscribe-with-a-user-account"></a>Abonnieren eines Benutzerkontos

1. Tippe auf der Hauptseite des Clients auf **Abonnieren**.
2. Melde dich bei entsprechender Aufforderung mit deinem Benutzerkonto an.
3. Die Ressourcen werden im Connection Center nach Arbeitsbereich gruppiert angezeigt.

#### <a name="subscribe-with-url"></a>Abonnieren mit URL

1. Tippe auf der Hauptseite des Clients auf **Mit URL abonnieren**.
2. Gib die Arbeitsbereichs-URL oder deine E-Mail-Adresse ein:
   - Verwende im Fall einer **Arbeitsbereichs-URL** diejenige, die du vom Administrator erhalten hast. Wenn du auf Ressourcen von Windows Virtual Desktop zugreifst, kannst du eine der folgenden URLs verwenden:
     - Windows Virtual Desktop (klassisch): `https://rdweb.wvd.microsoft.com/api/feeddiscovery/webfeeddiscovery.aspx`
     - Windows Virtual Desktop: `https://rdweb.wvd.microsoft.com/api/arm/feeddiscovery`
   - Um **E-Mail** zu verwenden, gib deine E-Mail-Adresse ein. Dies weist den Client an, nach einer URL zu suchen, die deiner E-Mail-Adresse zugeordnet ist, sofern der Administrator die [E-Mail-Ermittlung](../rds-email-discovery.md) eingerichtet hat.
3. Tippen Sie auf **Weiter**.
4. Melde dich bei entsprechender Aufforderung mit deinem Benutzerkonto an.
5. Die Ressourcen werden im Connection Center nach Arbeitsbereich gruppiert angezeigt.

### <a name="workspace-details"></a>Arbeitsbereichsdetails

Nach dem Abonnieren kannst du weitere Informationen zu einem Arbeitsbereich im Bereich „Details“ anzeigen:

- Den Namen des Arbeitsbereichs
- Die zum Abonnieren verwendete URL und den Benutzernamen
- Die Anzahl der Apps und Desktops
- Das Datum und die Uhrzeit der letzten Aktualisierung
- Den Status der letzten Aktualisierung

Zugriff auf den Bereich „Details“:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben dem Arbeitsbereich.
2. Wähle im Dropdownmenü **Details** aus.
3. Der Bereich „Details“ wird auf der rechten Seite des Clients angezeigt.

Nach dem Abonnieren wird der Arbeitsbereich automatisch regelmäßig aktualisiert. Da bei können Ressourcen hinzugefügt, geändert oder entfernt werden, basierend auf Änderungen, die von deinem Administrator vorgenommen werden.

Du kannst bei Bedarf auch manuell nach Updates suchen, indem du im Detailbereich **Aktualisieren** auswählst.

### <a name="refreshing-a-workspace"></a>Aktualisieren eines Arbeitsbereichs

Du kannst einen Arbeitsbereich manuell aktualisieren, indem du im Überlaufmenü ( **...** ) neben dem Arbeitsbereich **Aktualisieren** auswählst.

### <a name="unsubscribe-from-a-workspace"></a>Beenden des Abonnements eines Arbeitsbereichs

In diesem Abschnitt erfährst du, wie du das Abonnement eines Arbeitsbereichs beendest. Du kannst das Abonnement beenden, um entweder erneut mit einem anderen Konto zu abonnieren oder um deine Ressourcen vom System zu entfernen.

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben dem Arbeitsbereich.
2. Wähle im Dropdownmenü **Abonnement kündigen** aus.
3. Überprüfe das Dialogfeld, und wähle **Fortfahren** aus.

## <a name="managed-desktops"></a>Verwaltete Desktops

Arbeitsbereiche können mehrere verwaltete Ressourcen enthalten, einschließlich Desktops. Wenn du auf einen verwalteten Desktop zugreifst, hast du Zugriff auf alle Apps, die von deinem Administrator installiert wurden.

### <a name="desktop-settings"></a>Desktopeinstellungen

Du kannst einige der Einstellungen für Desktopressourcen konfigurieren, um sicherzustellen, dass die Oberfläche deinen Anforderungen entspricht. Um auf die Liste der verfügbaren Einstellungen zuzugreifen, klicke mit der rechten Maustaste auf die Desktopressource, und wähle dann **Einstellungen** aus.

Der Client verwendet die von deinem Administrator konfigurierten Einstellungen, es sei denn, du deaktivierst die Option **Standardeinstellungen verwenden**. Auf diese Weise kannst du die folgenden Optionen konfigurieren:

- **Anzeigekonfiguration** wählt aus, welche Anzeigen für die Desktopsitzung verwendet werden sollen, und beeinflusst, welche zusätzlichen Einstellungen verfügbar sind.
  - **Alle Anzeigen** stellt sicher, dass in der Sitzung immer alle lokalen Anzeigen verwendet werden, auch wenn einige davon später hinzugefügt oder entfernt werden.
  - **Single display** (Einzelne Anzeige) stellt sicher, dass in der Sitzung immer eine einzelne Anzeige verwendet wird, und ermöglicht, ihre Eigenschaften zu konfigurieren.
  - **Select displays** (Anzeigen auswählen) ermöglicht dir, die für die Sitzung zu verwendenden Anzeigen auszuwählen und die Liste der Anzeigen während der Sitzung dynamisch zu ändern.
- **Anzeigen auswählen, die für die Sitzung verwendet werden sollen** gibt an, welche lokalen Anzeigen für die Sitzung verwendet werden sollen. Alle ausgewählten Anzeigen müssen nebeneinander liegen. Diese Einstellung ist nur im Modus **Select displays** (Anzeigen auswählen) verfügbar.
- **Maximize to current displays** (Für die aktuellen Anzeigen maximieren) legt fest, welche Anzeigen in der Sitzung im Vollbildmodus verwendet werden. Bei Aktivierung wechselt die Sitzung dynamisch auf den Anzeigen mit dem Sitzungsfenster in den Vollbildmodus. Dadurch kannst du die Anzeige während der Sitzung ändern. Wenn diese Option deaktiviert ist, wird die Sitzung im Vollbildmodus auf denselben Anzeigen angezeigt wie beim letzten Mal. Diese Einstellung ist nur im Modus **Select displays** (Anzeigen auswählen) verfügbar und andernfalls deaktiviert.
- **Single display when windowed** (Einzelne Anzeige im Fenstermodus) legt fest, welche Anzeigen beim Beenden des Vollbildmodus in der Sitzung verfügbar sind. Wenn diese Option aktiviert ist, wechselt die Sitzung im Fenstermodus zu einer einzelnen Anzeige. Ist sie deaktiviert, behält die Sitzung im Fenstermodus dieselben Anzeigen wie im Vollbildmodus bei. Diese Einstellung ist nur in den Modi **Alle Anzeigen** und **Select displays** (Anzeigen auswählen) verfügbar und andernfalls deaktiviert.
- **Im Vollbildmodus starten** legt fest, ob die Sitzung im Vollbild- oder im Fenstermodus gestartet wird. Diese Einstellung ist nur im Modus **Single display** (Einzelne Anzeige) verfügbar und andernfalls aktiviert.
- **Sitzung an Fenster anpassen** bestimmt, wie die Sitzung angezeigt wird, wenn die Auflösung des Remotedesktops von der Größe des lokalen Fensters abweicht. Wenn die Option aktiviert ist, wird die Größe der Sitzungsinhalte innerhalb des Fensters passend geändert, wobei das Seitenverhältnis der Sitzung beibehalten wird. Ist sie deaktiviert, werden Scrollleisten oder schwarze Bereiche angezeigt, wenn Auflösung und Fenstergröße nicht übereinstimmen. Diese Einstellung ist in allen Modi verfügbar.
- **Update the resolution on resize** (Auflösung bei Größenänderung aktualisieren) bewirkt, dass die Remotedesktopauflösung automatisch aktualisiert wird, wenn die Größe der Sitzung im Fenstermodus geändert wird. Wenn diese Option deaktiviert ist, verwendet die Sitzung immer die Auflösung, die unter **Auflösung** angegeben wird. Diese Einstellung ist nur im Modus **Single display** (Einzelne Anzeige) verfügbar und andernfalls aktiviert.
- In **Auflösung** kannst du die Auflösung des Remotedesktops festlegen. Die Sitzung behält diese Auflösung für ihre gesamte Dauer bei. Diese Einstellung ist nur im Modus **Single display** (Einzelne Anzeige) und bei deaktivierter Option **Update the resolution on resize** (Auflösung bei Größenänderung aktualisieren) verfügbar.
- **Größe von Text und Apps ändern** gibt die Größe der Inhalte der Sitzung an. Diese Einstellung gilt nur für Verbindungen mit Windows 8.1 und höher oder Windows Server 2012 R2 und höher. Diese Einstellung ist nur im Modus **Single display** (Einzelne Anzeige) und bei deaktivierter Option **Update the resolution on resize** (Auflösung bei Größenänderung aktualisieren) verfügbar.

## <a name="give-us-feedback"></a>Geben Sie uns Feedback

Hast du einen Vorschlag für eine Funktion, oder möchtest du ein Problem melden? Teilen Sie uns den Vorschlag oder Informationen zum Problem über den [Feedback-Hub](https://aka.ms/rddesktopfeedback) mit.

Sie können uns auch Feedback senden, indem Sie in der Client-App die Schaltfläche auswählen, die wie ein Smiley-Emoticon aussieht, wie in der folgenden Abbildung gezeigt:

> [!div class="mx-imgBorder"]
> ![Screenshot des Smiley-Emoticons, das Sie zum Feedback-Hub führt.](../media/smiley-face-icon.png)

>[!NOTE]
>Um Ihnen bestmöglich helfen zu können, benötigen wir von Ihnen möglichst detaillierte Informationen zu diesem Thema. Sie können z. B. Screenshots oder eine Aufzeichnung der Aktionen hinzufügen, die zu diesem Problem geführt haben. Weitere Tipps, wie Sie hilfreiches Feedback senden können, finden Sie unter [Feedback](/windows-insider/at-home/feedback#add-new-feedback).

### <a name="access-client-logs"></a>Zugreifen auf Clientprotokolle

Möglicherweise benötigst du die Clientprotokolle, wenn du ein Problem untersuchst.

So rufst du die Clientprotokolle ab:

1. Stellen Sie sicher, dass keine Sitzungen aktiv sind und der Clientprozess nicht im Hintergrund ausgeführt wird, indem Sie in der Taskleiste mit der rechten Maustaste auf das Symbol **Remotedesktop** klicken und dann **Alle Sitzungen trennen** auswählen.
2. Öffne den **Datei-Explorer**.
3. Navigiere zum Ordner **%temp%\DiagOutputDir\RdClientAutoTrace**.
