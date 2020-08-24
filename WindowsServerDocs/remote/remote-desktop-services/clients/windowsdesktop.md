---
title: Erste Schritte mit dem Windows-Desktopclient
description: Grundlegende Informationen zum Windows-Desktopclient.
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 08/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5bd3e1d5f06e5c415b4f300d9a2c8a9b390e5051
ms.sourcegitcommit: 8e5530ba7f7d3e2569590949e1f443d908683a17
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702829"
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

## <a name="provide-feedback"></a>Senden von Feedback

Hast du einen Vorschlag für eine Funktion, oder möchtest du ein Problem melden? Teile uns den Vorschlag über den [Feedback-Hub](feedback-hub://?tabid=2&contextid=883) mit. Du kannst über den Client auch auf den Feedback-Hub zugreifen:

1. Tippe im Connection Center auf die Option **Feedback senden** in der Befehlsleiste oben im Client, um die Feedback-Hub-App zu öffnen.
2. Gib die erforderlichen Informationen in die Felder **Zusammenfassung** und **Details** ein. Tippe auf **Weiter**, wenn du fertig bist.
3. Wähle aus, ob es sich um ein **Problem** oder einen **Vorschlag** handelt.
4. Überprüfe, ob sich die Kategorie unter **Apps** > **Remotedesktop** befindet. Wenn dies der Fall ist, tippe auf **Weiter**.
5. Schaue die vorhandenen Feedbackthemen durch, um festzustellen, ob das Problem bereits von einem anderen Benutzer gemeldet wurde. Wenn dies nicht der Fall ist, wähle **Neuen Fehler melden** aus, und tippe dann auf **Weiter**.
6. Auf der nächsten Seite kannst du weitere Informationen geben, damit wir dir helfen können, das Problem zu beheben. Du kannst detailliertere Informationen schreiben, Screenshots senden und sogar eine Aufnahme des Problems erstellen, um uns zu zeigen, was passiert ist. Um eine Aufnahme zu erstellen, wähle **Aufnahme starten** aus, und führe dann die Schritte aus, die zu dem Problem geführt haben. Wenn du fertig bist, kehre zum Feedback-Hub zurück, und wähle **Aufnahme beenden** aus.
7. Wenn du mit den Informationen zufrieden bist, tippe auf **Senden**.
8. Tippe auf der Seite „Vielen Dank für Ihr Feedback!“ auf **Feedback teilen**, um einen Link zu deinem Feedback zu generieren, den du bei Bedarf mit anderen teilen kannst.

### <a name="access-client-logs"></a>Zugreifen auf Clientprotokolle

Möglicherweise benötigst du die Clientprotokolle, wenn du ein Problem untersuchst.

So rufst du die Clientprotokolle ab:

1. Stellen Sie sicher, dass keine Sitzungen aktiv sind und der Clientprozess nicht im Hintergrund ausgeführt wird, indem Sie in der Taskleiste mit der rechten Maustaste auf das Symbol **Remotedesktop** klicken und dann **Alle Sitzungen trennen** auswählen.
2. Öffne den **Datei-Explorer**.
3. Navigiere zum Ordner **%temp%\DiagOutputDir\RdClientAutoTrace**.
