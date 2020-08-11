---
title: 'Schritt 4: Konfigurieren von Gruppenrichtlinien für „Automatische Updates“'
description: 'Thema zu Windows Server Update Service (WSUS): „Konfigurieren von Gruppenrichtlinieneinstellungen für ‚Automatische Updates‘“ ist Schritt 4 in einem vierstufigen Verfahren zum Bereitstellen von WSUS'
ms.topic: article
ms.assetid: 62177d05-d832-4ea8-bca4-47a8cd34a19c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca59369cda4c38af111b9ccd3141219b1516cbd7
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991098"
---
# <a name="step-4-configure-group-policy-settings-for-automatic-updates"></a>Schritt 4: Konfigurieren von Gruppenrichtlinien für „Automatische Updates“

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In einer Active Directory-Umgebung können Sie mithilfe von Gruppenrichtlinien definieren, wie Computer und Benutzer (in diesem Dokument als WSUS-Clients bezeichnet) mit Windows-Updates interagieren können, um automatische Updates von Windows Server Update Services (WSUS) zu beziehen.

Dieses Thema enthält zwei Hauptabschnitte:

[Gruppenrichtlinieneinstellungen für WSUS-Clientupdates](#group-policy-settings-for-wsus-client-updates). Hier finden Sie vorgeschriebene Vorgehensweisen und Verhaltensdetails zu den Gruppenrichtlinieneinstellungen für Windows Update und „Wartungszeitplan“, die steuern, wie WSUS-Clients mit Windows Update interagieren können, um automatische Updates zu erhalten.

[Zusätzliche Informationen](#supplemental-information) enthält die folgenden Abschnitte:

-   [Zugreifen auf die Windows Update-Einstellungen in Gruppenrichtlinien](#accessing-the-windows-update-settings-in-group-policy). Hier finden Sie allgemeine Hinweise zur Verwendung des Gruppenrichtlinienverwaltungs-Editors und Informationen zum Zugriff auf die Richtlinienerweiterungen „Updatedienste“ und Einstellungen für „Wartungszeitplan“ in Gruppenrichtlinien.

-   [Für diese Anleitung relevante Änderungen an WSUS](#changes-to-wsus-relevant-to-this-guide): Für Administratoren, die mit WSUS 3.2 und früheren Versionen vertraut sind, enthält dieser Abschnitt eine kurze Zusammenfassung der wichtigsten Unterschiede zwischen der aktuellen und früheren Versionen von WSUS, die für diesen Leitfaden relevant sind.

-   [Begriffe und Definitionen](#terms-and-definitions): Definitionen für verschiedene Begriffe im Zusammenhang mit WSUS und Updatediensten, die in diesem Leitfaden verwendet werden.

## <a name="group-policy-settings-for-wsus-client-updates"></a>Gruppenrichtlinieneinstellungen für WSUS-Clientupdates
Dieser Abschnitt enthält Informationen zu drei Gruppenrichtlinienerweiterungen. In diesen Erweiterungen finden Sie die Einstellungen, die Sie verwenden können, um zu konfigurieren, wie WSUS-Clients mit Windows Update interagieren können, um automatische Updates zu erhalten.

-   [Computerkonfiguration &gt; Windows Update (Richtlinieneinstellungen)](#computer-configuration--windows-update-policy-settings)

-   [Computerkonfiguration &gt; Wartungszeitplan (Richtlinieneinstellungen)](#computer-configuration--maintenance-scheduler-policy-settings)

-   [Benutzerkonfiguration &gt; Windows Update (Richtlinieneinstellungen)](#user-configuration--windows-update-policy-settings)

> [!NOTE]
> In diesem Thema wird davon ausgegangen, dass Sie bereits mit Gruppenrichtlinien vertraut sind und damit arbeiten. Wenn Sie mit Gruppenrichtlinien nicht vertraut sind, wird empfohlen, die Informationen im Abschnitt [Zusätzliche Informationen](#supplemental-information) in diesem Dokument zu lesen, bevor Sie versuchen, Richtlinieneinstellungen für WSUS zu konfigurieren.

### <a name="computer-configuration--windows-update-policy-settings"></a>Computerkonfiguration > Windows Update (Richtlinieneinstellungen)
Dieser Abschnitt enthält Details zu den folgenden computerbasierten Richtlinieneinstellungen:

-   [Automatische Updates sofort installieren](#allow-automatic-updates-immediate-installation)

-   [Nichtadministratoren gestatten, Updatebenachrichtigungen zu erhalten](#allow-non-administrators-to-receive-update-notifications)

-   [Signierte Updates aus einem Intranetspeicherort für Microsoft-Updatedienste zulassen](#allow-signed-updates-from-an-intranet-microsoft-update-service-location)

-   [Suchhäufigkeit für automatische Updates](#automatic-updates-detection-frequency)

-   [Automatische Updates konfigurieren](#configure-automatic-updates)

-   [Neustart für geplante Installationen verzögern](#delay-restart-for-scheduled-installations)

-   [Die Standardoption „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anpassen](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [Option „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anzeigen](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Clientseitige Zielzuordnung aktivieren](#enable-client-side-targeting)

-   [Windows Update-Energieverwaltung aktivieren, um das System zur Installation von geplanten Updates automatisch zu reaktivieren](#enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates)

-   [Keinen automatischen Neustart für geplante Installationen automatischer Updates durchführen, wenn Benutzer angemeldet sind](#no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations)

-   [Erneut zu einem Neustart für geplante Installationen auffordern](#re-prompt-for-restart-with-scheduled-installations)

-   [Geplante Installationen automatischer Updates erneut planen](#reschedule-automatic-updates-scheduled-installations)

-   [Internen Pfad für den Microsoft Updatedienst angeben](#specify-intranet-microsoft-update-service-location)

-   [Empfohlene Updates über automatische Updates aktivieren](#turn-on-recommended-updates-via-automatic-updates)

-   [Softwarebenachrichtigungen aktivieren](#turn-on-software-notifications)

Im Gruppenrichtlinienverwaltungs-Editor befinden sich Windows Update-Richtlinien für die computerbasierte Konfiguration im folgenden Pfad: *Richtlinienname* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**.

> [!NOTE]
> Standardmäßig sind diese Einstellungen nicht konfiguriert.

#### <a name="allow-automatic-updates-immediate-installation"></a>Automatische Updates sofort installieren
Gibt an, ob das Feature „Automatische Updates“ Updates automatisch installiert, die Windows-Dienste nicht unterbrechen oder Windows neu starten.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ auf **Deaktiviert** festgelegt ist, hat diese Richtlinie keine Auswirkung.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Updates nicht sofort installiert werden. Lokale Administratoren können diese Einstellung mithilfe des Editors für lokale Gruppenrichtlinien ändern.|
|**Aktiviert**|Gibt an, dass das Feature „Automatische Updates“ Updates sofort installiert, nachdem Sie heruntergeladen wurden und für die Installation bereit sind.|
|**Deaktiviert**|Gibt an, dass Updates nicht sofort installiert werden.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="allow-non-administrators-to-receive-update-notifications"></a>Nichtadministratoren gestatten, Updatebenachrichtigungen zu erhalten
Gibt an, ob Benutzer, die keine Administratoren sind, Updatebenachrichtigungen auf Grundlage der Richtlinieneinstellung „Automatische Updates konfigurieren“ erhalten.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|Weitere Informationen finden Sie in der folgenden Tabelle.|

> [!NOTE]
> Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert oder nicht konfiguriert ist, hat diese Richtlinieneinstellung keine Auswirkung.

> [!IMPORTANT]
> Ab Windows 8 und Windows RT ist diese Richtlinieneinstellung standardmäßig aktiviert. In allen früheren Versionen von Windows ist sie standardmäßig deaktiviert.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Benutzern immer das Fenster zur Kontensteuerung angezeigt wird und erhöhte Berechtigungen für diese Aufgaben erforderlich sind. Lokale Administratoren können diese Einstellung mithilfe des Editors für lokale Gruppenrichtlinien ändern.|
|**Aktiviert**|Gibt an, dass für „Windows Update – automatische Updates“ und „Microsoft Update“ Nichtadministratoren einbezogen werden, wenn festgelegt wird, welcher angemeldete Benutzer Updatebenachrichtigungen empfängt. Benutzer, die keine Administratoren sind, können alle optionalen, empfohlenen und WICHTIGEN Update-Inhalte installieren, für die sie eine Benachrichtigung empfangen haben. Benutzern wird das Fenster „Benutzerkontensteuerung“ nicht angezeigt, und sie benötigen keine erhöhten Berechtigungen zum Installieren dieser Updates. Ausnahmen sind Updates, die Änderungen an den Einstellungen für Benutzeroberfläche, Endbenutzer-Lizenzvertrag oder Windows Update enthalten.<p>Es gibt zwei Situationen, in denen die Auswirkung dieser Einstellung vom ausgeführten Computer abhängt:<p>1.  **Ausblenden** oder **Wiederherstellen** von Updates<br />2.  **Abbrechen** der Installation eines Updates<p>Wenn diese Richtlinieneinstellung unter Windows Vista oder Windows XP aktiviert ist, wird Benutzern das Fenster „Benutzerkontensteuerung“ nicht angezeigt. Sie benötigen keine erhöhten Berechtigungen zum Ausblenden, Wiederherstellen oder Abbrechen von Updates.<p>Wenn diese Richtlinieneinstellung unter Windows Vista aktiviert ist, wird Benutzern das Fenster „Benutzerkontensteuerung“ nicht angezeigt. Sie benötigen keine erhöhten Berechtigungen zum Ausblenden, Wiederherstellen oder Abbrechen von Updates. Wenn diese Richtlinieneinstellung nicht aktiviert ist, wird Benutzern das Fenster „Benutzerkontensteuerung“ stets angezeigt. Sie benötigen erhöhte Berechtigungen zum Ausblenden, Wiederherstellen oder Abbrechen von Updates.<p>Unter Windows 7 hat diese Richtlinieneinstellung keine Auswirkungen. Benutzern wird immer das Fenster zur Kontensteuerung angezeigt, und sie benötigen erhöhte Berechtigungen für diese Aufgaben.<p>Unter Windows 8 und Windows RT hat diese Richtlinieneinstellung keine Auswirkungen.|
|**Deaktiviert**|Gibt an, dass nur angemeldete Administratoren Updatebenachrichtigungen erhalten. **Hinweis:** Unter Windows 8 und Windows RT ist diese Richtlinieneinstellung standardmäßig aktiviert. In allen früheren Versionen von Windows ist sie standardmäßig deaktiviert.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="allow-signed-updates-from-an-intranet-microsoft-update-service-location"></a>Signierte Updates aus einem Intranetspeicherort für Microsoft-Updatedienste zulassen
Gibt an, ob das Feature „Automatische Updates“ Updates akzeptiert, die von anderen Entitäten als Microsoft signiert wurden, wenn das Update an einem Speicherort des Microsoft Update-Diensts im Intranet gefunden wird.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|Windows RT|

> [!NOTE]
> Updates von einem anderen Dienst als dem Microsoft Update-Dienst im Intranet müssen immer von Microsoft signiert sein und sind von dieser Richtlinieneinstellung nicht betroffen.

> [!NOTE]
> Unter Windows RT wird diese Richtlinie nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

**Optionen:** Es gibt keine Optionen für diese Einstellung.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Updates aus einem Speicherort für den Microsoft Update-Dienst im Intranet von Microsoft signiert werden müssen.|
|**Aktiviert**|Gibt an, dass das Feature „Automatische Updates“ Updates akzeptiert, die über einen Speicherort für den Microsoft Update-Dienst im Intranet empfangen wurden, wenn sie durch ein Zertifikat signiert sind, das sich im Zertifikatspeicher „Vertrauenswürdige Herausgeber“ des lokalen Computers befindet.|
|**Deaktiviert**|Gibt an, dass Updates aus einem Speicherort für den Microsoft Update-Dienst im Intranet von Microsoft signiert werden müssen.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="always-automatically-restart-at-the-scheduled-time"></a>Neustart immer automatisch zur geplanten Zeit durchführen
Gibt an, ob ein Neustartzeitgeber immer sofort beginnt, nachdem Windows Update wichtige Updates installiert hat, anstatt zuerst die Benutzer für mindestens zwei Tage auf dem Anmeldebildschirm zu benachrichtigen.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Wenn die Richtlinieneinstellung „Keinen automatischen Neustart für geplante Installationen automatischer Updates durchführen, wenn Benutzer angemeldet sind“ aktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Windows Update das Neustartverhalten des Computers nicht ändert.|
|**Aktiviert**|Gibt an, dass ein Neustartzeitgeber immer sofort beginnt, nachdem Windows Update wichtige Updates installiert hat, anstatt zuerst die Benutzer für mindestens zwei Tage auf dem Anmeldebildschirm zu benachrichtigen.<p>Der Neustartzeitgeber kann so konfiguriert werden, dass er mit einem beliebigen Wert von 15 bis 180 Minuten beginnt. Wenn der Zeitgeber ausgeführt wird, wird der Neustart auch dann fortgesetzt, wenn Benutzer am Computer angemeldet sind.|
|**Deaktiviert**|Gibt an, dass Windows Update das Neustartverhalten des Computers nicht ändert.|

**Optionen:** Wenn diese Einstellung aktiviert ist, können Sie den Zeitraum angeben, nach dem Updates installiert werden, bevor ein Computerneustart erzwungen wird.

#### <a name="automatic-updates-detection-frequency"></a>Suchhäufigkeit für automatische Updates
Gibt die Stunden an, die Windows wartet, bis es nach verfügbaren Updates sucht. Die genaue Wartezeit wird festgelegt, indem die hier angegebenen Stunden minus 0 bis 20 % der angegebenen Stunden verwendet werden. Wenn diese Richtlinie beispielsweise verwendet wird, um eine Suchhäufigkeit von 20 Stunden anzugeben, suchen alle Clients, für die diese Richtlinie angewendet wird, in einer beliebigen Häufigkeit von 16 bis 20 Stunden nach Updates.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|Windows RT|

> [!NOTE]
> Die Einstellung „Internen Pfad für den Microsoft Updatedienst angeben“ muss aktiviert sein, damit diese Richtlinie wirksam wird.
>
> Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert ist, hat diese Richtlinie keine Auswirkung.

> [!NOTE]
> Unter Windows RT wird diese Richtlinie nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Windows im Standardintervall von 22 Stunden auf verfügbare Updates prüfen soll.|
|**Aktiviert**|Gibt an, dass Windows im angegebenen Intervall auf verfügbare Updates prüfen soll.|
|**Deaktiviert**|Gibt an, dass Windows im Standardintervall von 22 Stunden auf verfügbare Updates prüfen soll.|

**Optionen:** Wenn diese Einstellung aktiviert ist, können Sie das Zeitintervall (in Stunden) festlegen, das Windows Update wartet, bevor nach Updates gesucht wird.

#### <a name="configure-automatic-updates"></a>Automatische Updates konfigurieren
Gibt an, ob automatische Updates auf diesem Computer aktiviert sind.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|Windows RT|

Wenn diese Option aktiviert ist, müssen Sie eine der vier Optionen auswählen, die in dieser Gruppenrichtlinieneinstellung angegeben sind.

Um diese Einstellung zu verwenden, wählen Sie **Aktiviert** und dann unter **Optionen** unter **Automatische Updates konfigurieren** eine der Optionen (2, 3, 4 oder 5) aus.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass die Verwendung automatischer Updates nicht auf Gruppenrichtlinienebene angegeben ist. Ein Computeradministrator kann jedoch weiterhin in der Systemsteuerung automatische Updates konfigurieren.|
|**Aktiviert**|Gibt an, dass Windows erkennt, wann der Computer online ist, und verwendet seine Internetverbindung, um Windows Update nach verfügbaren Updates zu durchsuchen.<p>Wenn diese Option aktiviert ist, können lokale Administratoren mithilfe der Windows Update-Systemsteuerung eine Konfigurationsoption ihrer Wahl auswählen. Lokale Administratoren dürfen jedoch die Konfiguration für das Feature „Automatische Updates“ nicht deaktivieren.<p>-   **2: Vor Herunterladen und Installation benachrichtigen**<br />    Wenn Windows Update Updates findet, die für den Computer gelten, werden Benutzer darüber informiert, dass Updates zum Download bereit stehen. Benutzer können dann Windows Update ausführen, um alle verfügbaren Updates herunterzuladen und zu installieren.<br />-   **3: Autom. Herunterladen, aber vor Installation benachrichtigen** (Standardeinstellung)<br />    Windows Update findet anwendbare Updates und lädt sie im Hintergrund herunter. Der Benutzer wird während des Vorgangs nicht benachrichtigt oder unterbrochen. Wenn die Downloads abgeschlossen sind, werden Benutzer benachrichtigt, dass Updates zur Installation bereit stehen. Benutzer können dann Windows Update ausführen, um die heruntergeladenen Updates zu installieren.<br />-   **4: Autom. Herunterladen und laut Zeitplan installieren**<br />    Sie können den Zeitplan mithilfe der Optionen in dieser Gruppenrichtlinieneinstellung angeben. Wenn kein Zeitplan angegeben ist, sieht der Standardzeitplan für alle Installationen täglich 03:00 Uhr vor. Wenn für Updates ein Neustart erforderlich ist, um die Installation abzuschließen, startet Windows den Computer automatisch neu. (Falls ein Benutzer beim Computer angemeldet ist, wenn Windows neu gestartet werden kann, wird der Benutzer benachrichtigt und erhält die Möglichkeit, den Neustart zu verzögern.) **Hinweis:** Ab Windows 8 können Sie Updates so festlegen, dass sie während der automatischen Wartung installiert werden, anstatt einen bestimmten an Windows Update gekoppelten Zeitplan zu verwenden. Bei der automatischen Wartung werden Updates installiert, wenn der Computer nicht verwendet wird. Es wird vermieden, dass Updates installiert werden, wenn der Computer im Akkubetrieb ist. Wenn die automatische Wartung innerhalb weniger Tage keine Updates installieren kann, installiert Windows Update die Updates sofort. Benutzer werden dann über einen anstehenden Neustart benachrichtigt. Ein anstehender Neustart erfolgt nur dann, wenn kein Potenzial für einen versehentlichen Datenverlust besteht.    Sie können Zeitplanoptionen in den Einstellungen unter „Wartungszeitplan“ im Gruppenrichtlinienverwaltungs-Editor angeben. Diese befinden sich im Pfad *Richtlinienname* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Wartungszeitplan** > **Aktivierungsgrenze für automatische Wartung**. Weitere Informationen zu Einstellungsdetails findest du im Abschnitt des folgenden Verweises: [Einstellungen für den Wartungszeitplan](#computer-configuration--maintenance-scheduler-policy-settings).    **5: Lokalem Administrator ermöglichen, Einstellung auszuwählen**<br />Gibt an, ob lokale Administratoren die Systemsteuerung für „Automatische Updates“ verwenden dürfen, um eine Konfigurationsoption ihrer Wahl auszuwählen, z. B. ob lokale Administratoren eine geplante Installationsuhrzeit wählen können.<br />    Lokalen Administratoren wird nicht gestattet, die Konfiguration für „Automatische Updates“ zu deaktivieren.|
|**Deaktiviert**|Gibt an, dass alle Clientupdates, die über den öffentlichen Windows Update-Dienst verfügbar sind, manuell aus dem Internet heruntergeladen und installiert werden müssen.|

#### <a name="delay-restart-for-scheduled-installations"></a>Neustart für geplante Installationen verzögern
Gibt die Zeitspanne an, die „Automatische Updates“ warten soll, bis mit einem geplanten Neustart fortgefahren wird.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn „Automatische Updates“ für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert ist, hat diese Richtlinie keine Auswirkung.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass nach der Installation von Updates die Standardwartezeit von 15 Minuten abläuft, bevor ein geplanter Neustart stattfindet.|
|**Aktiviert**|Gibt an, dass nach Abschluss der Installation ein geplanter Neustart erfolgt, nachdem die angegebene Anzahl von Minuten abgelaufen ist.|
|**Deaktiviert**|Gibt an, dass nach der Installation von Updates die Standardwartezeit von 15 Minuten abläuft, bevor ein geplanter Neustart stattfindet.|

**Optionen:** Wenn diese Einstellung aktiviert ist, können Sie diese Option verwenden, um die Zeitspanne (in Minuten) anzugeben, die „Automatische Updates“ warten soll, bevor mit einem geplanten Neustart fortgefahren wird.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog"></a>Die Standardoption „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anpassen
Mit dieser Richtlinieneinstellung können Sie festlegen, ob die Option **Updates installieren und herunterfahren** als Standardoption im Dialogfeld **Windows herunterfahren** zulässig ist.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Richtlinieneinstellung hat keine Auswirkung, wenn die Richtlinieneinstellung *Richtlinienname* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update** > **Option „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anzeigen** aktiviert ist.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass **Updates installieren und herunterfahren** die Standardoption im Dialogfeld **Windows herunterfahren** wird, wenn Updates für die Installation zu dem Zeitpunkt verfügbar sind, zu dem der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|
|**Aktiviert**|Wenn Sie diese Richtlinieneinstellung aktivieren, ist die letzte Option des Benutzers zum Herunterfahren (z. B. „Ruhezustand“ oder „Neu starten“) die Standardoption im Dialogfeld **Windows herunterfahren**, und zwar unabhängig davon, ob die Option **Updates installieren und herunterfahren** im Menü **Wählen Sie einen Vorgang aus** verfügbar ist.|
|**Deaktiviert**|Gibt an, dass **Updates installieren und herunterfahren** die Standardoption im Dialogfeld **Windows herunterfahren** wird, wenn Updates für die Installation zu dem Zeitpunkt verfügbar sind, zu dem der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="do-not-connect-to-any-windows-update-internet-locations"></a>Keine Verbindungen mit Windows Update-Internetadressen herstellen
Auch wenn Windows Update für das Empfangen von Updates von einem internen Updatedienst konfiguriert ist, wird es in regelmäßigen Abständen Informationen vom öffentlichen Windows Update-Dienst abrufen, um zukünftige Verbindungen mit Windows Update und anderen Diensten wie Microsoft Update oder Microsoft Store zu ermöglichen.

Wenn Sie diese Richtlinie aktivieren, wird die Funktionalität zum regelmäßigen Abrufen von Informationen aus den öffentlichen Windows Server Update Services deaktiviert. Dies kann dazu führen, dass die Verbindung mit öffentlichen Diensten wie Microsoft Store nicht mehr funktioniert.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme ab Windows Server 2012 R2 , Windows 8.1 oder Windows RT 8.1, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn der Computer so konfiguriert ist, dass eine Verbindung mit einem internen Updatedienst über die Richtlinieneinstellung „Internen Pfad für den Microsoft Updatedienst angeben“ hergestellt wird.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Das Standardverhalten zum Abrufen von Informationen aus den öffentlichen Windows Server Update Services bleibt erhalten.|
|**Aktiviert**|Gibt an, dass Computer keine Informationen aus den öffentlichen Windows Server Update Services abrufen.|
|**Deaktiviert**|Das Standardverhalten zum Abrufen von Informationen aus den öffentlichen Windows Server Update Services bleibt erhalten.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog"></a>Option "Updates installieren und herunterfahren" im Dialogfeld "Windows herunterfahren" nicht anzeigen
Gibt an, ob die Option **Updates installieren und herunterfahren** im Dialogfeld **Windows herunterfahren** angezeigt wird.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass die Option **Updates installieren und herunterfahren** im Dialogfeld **Windows herunterfahren** verfügbar ist, wenn Updates verfügbar sind, wenn der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt. Ein lokaler Administrator kann diese Einstellung mithilfe einer lokalen Richtlinie ändern.|
|**Aktiviert**|Gibt an, dass **Updates installieren und herunterfahren** nicht als Option im Dialogfeld **Windows herunterfahren** angezeigt wird, selbst wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|
|**Deaktiviert**|Gibt an, dass die Option **Updates installieren und herunterfahren** die Standardoption im Dialogfeld **Windows herunterfahren** wird, wenn Updates für die Installation zu dem Zeitpunkt verfügbar sind, zu dem der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="enable-client-side-targeting"></a>Clientseitige Zielzuordnung aktivieren
Gibt die Namen der Zielgruppen an, die in der WSUS-Konsole konfiguriert werden und die Updates von WSUS empfangen sollen.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|Windows RT|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn dieser Computer so konfiguriert ist, dass er die angegebenen Zielgruppennamen im WSUS unterstützt. Wenn der Zielgruppenname im WSUS nicht vorhanden ist, wird er bis zur Erstellung ignoriert. Wenn die Richtlinieneinstellung „Internen Pfad für den Microsoft Updatedienst angeben“ deaktiviert oder nicht konfiguriert ist, hat diese Richtlinie keine Auswirkung.

> [!NOTE]
> Unter Windows RT wird diese Richtlinie nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass keine Zielgruppeninformationen an WSUS gesendet werden. Ein lokaler Administrator kann diese Einstellung mithilfe einer lokalen Richtlinie ändern.|
|**Aktiviert**|Gibt an, dass die angegebenen Zielgruppeninformationen an WSUS gesendet werden. Sie dienen zum Bestimmen, welche Updates auf diesem Computer bereitgestellt werden sollen. Wenn WSUS mehrere Zielgruppen unterstützt, können Sie mit dieser Richtlinie mehrere durch Semikolon getrennte Gruppennamen angeben, sofern Sie die Zielgruppennamen der Computergruppenliste in WSUS hinzugefügt haben. Andernfalls muss eine einzelne Gruppe angegeben werden.|
|**Deaktiviert**|Gibt an, dass keine Zielgruppeninformationen an WSUS gesendet werden.|

**Optionen:** Verwenden Sie diesen Bereich, um einen oder mehrere Zielgruppennamen anzugeben.

#### <a name="enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates"></a>Windows Update-Energieverwaltung aktivieren, um das System zur Installation von geplanten Updates automatisch zu reaktivieren
Gibt an, ob Windows Update die Features „Windows-Energieverwaltung“ oder „Energieoptionen“ verwendet, um den Computer automatisch aus dem Ruhezustand zu aktivieren, wenn Updates für die Installation geplant sind.

Der Computer wird nur dann automatisch aktiviert, wenn Windows Update für die automatische Installation von Updates konfiguriert ist. Wenn sich der Computer im Ruhezustand befindet, während die geplante Installationszeit eintritt, und es Updates gibt, die angewendet werden müssen, verwendet Windows Update die Features „Windows-Energieverwaltung“ oder „Energieoptionen“, um den Computer automatisch zu aktivieren und die Updates zu installieren. Windows Update aktiviert auch den Computer und installiert ein Update, wenn eine Installationsfrist festgelegt ist.

Der Computer wird nur aktiviert, wenn es zu installierende Updates gibt. Wenn der Computer im Akkubetrieb ist und Windows Update ihn aktiviert, werden keine Updates installiert, und der Computer kehrt nach zwei Minuten automatisch in den Ruhezustand zurück.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme ab Windows Vista und Windows Server 2008 (Windows 7), die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Windows Update aktiviert den Computer nicht aus dem Ruhezustand, um Updates zu installieren. Ein lokaler Administrator kann diese Einstellung mithilfe einer lokalen Richtlinie ändern.|
|**Aktiviert**|Windows Update aktiviert den Computer aus dem Ruhezustand, um unter den zuvor genannten Bedingungen Updates zu installieren.|
|**Deaktiviert**|Windows Update aktiviert den Computer nicht aus dem Ruhezustand, um Updates zu installieren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations"></a>Keinen automatischen Neustart für geplante Installationen automatischer Updates durchführen, wenn Benutzer angemeldet sind
Gibt an, dass „Automatische Updates“ zum Abschluss einer geplanten Installation darauf wartet, dass der Computer von einem angemeldeten Benutzer neu gestartet wird, anstatt einen automatischen Neustart des Computers zu bewirken.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn „Automatische Updates“ für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert ist, hat diese Richtlinie keine Auswirkung.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass „Automatische Updates“ den Benutzer benachrichtigt, dass der Computer zum Abschließen der Installation in fünf Minuten automatisch neu gestartet wird.|
|**Aktiviert**|Einige Updates erfordern einen Neustart des Computers, bevor die Updates wirksam werden. Wenn der Status auf „Aktiviert“ festgelegt ist, startet „Automatische Updates“ einen Computer während einer geplanten Installation nicht automatisch neu, wenn ein Benutzer am Computer angemeldet ist. Stattdessen benachrichtigt „Automatische Updates“ den Benutzer, dass er den Computer neu starten soll.|
|**Deaktiviert**|Gibt an, dass „Automatische Updates“ den Benutzer benachrichtigt, dass der Computer zum Abschließen der Installation in fünf Minuten automatisch neu gestartet wird.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="re-prompt-for-restart-with-scheduled-installations"></a>Erneut zu einem Neustart für geplante Installationen auffordern
Gibt die Zeitspanne an, die „Automatische Updates“ warten soll, ehe der Benutzer zu einem geplanten Neustart aufgefordert wird.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|Windows RT|

> [!IMPORTANT]
> Diese Richtlinie gilt nur, wenn „Automatische Updates“ für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert ist, hat diese Richtlinie keine Auswirkung.

> [!NOTE]
> Diese Richtlinie hat keine Auswirkungen auf Computer, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Ein geplanter Neustart erfolgt zehn Minuten, nachdem die Aufforderung zum Neustart der Nachricht verworfen wurde. Ein lokaler Administrator kann diese Einstellung mithilfe einer lokalen Richtlinie ändern.|
|**Aktiviert**|Gibt an, dass nach der Verschiebung der vorherigen Aufforderung zum Neustart ein geplanter Neustart nach Ablauf der angegebenen Anzahl von Minuten erfolgt.|
|**Deaktiviert**|Ein geplanter Neustart erfolgt zehn Minuten, nachdem die Aufforderung zum Neustart der Nachricht verworfen wurde.|

**Optionen:** Falls aktiviert, können Sie mit dieser Einstellungsoption die Zeitspanne (in Minuten) angeben, die vergeht, bis Benutzer erneut zu einem geplanten Neustart aufgefordert werden.

#### <a name="reschedule-automatic-updates-scheduled-installations"></a>Geplante Installationen automatischer Updates erneut planen
Gibt die Zeitspanne an, die „Automatische Updates“ nach dem Start des Computers warten muss, bevor mit einer geplanten Installation fortgefahren wird, die zuvor ausgelassen wurde.

Wenn der Status auf **Nicht konfiguriert** festgelegt ist, wird eine ausgelassene geplante Installation eine Minute nach dem nächsten Start des Computers ausgeführt.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn „Automatische Updates“ für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert ist, hat diese Richtlinie keine Auswirkung.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass eine ausgelassene geplante Installation eine Minute nach dem nächsten Start des Computers ausgeführt wird.|
|**Aktiviert**|Gibt an, dass eine geplante Installation, die nicht früher erfolgt ist, in der angegebenen Anzahl von Minuten nach dem nächsten Start des Computers erfolgt.|
|**Deaktiviert**|Gibt an, dass bei der nächsten geplanten Installation eine ausgelassene geplante Installation durchgeführt wird.|

**Optionen:** Wenn diese Richtlinieneinstellung aktiviert ist, können Sie damit eine Anzahl von Minuten nach dem nächsten Start des Computers festlegen, damit eine geplante Installation, die zuvor nicht stattgefunden hat, durchgeführt wird.

#### <a name="specify-intranet-microsoft-update-service-location"></a>Internen Pfad für den Microsoft Updatedienst angeben
Gibt einen alternativen Intranetserver zum Hosten von Updates von Microsoft Update an. Sie können dann WSUS verwenden, um Computer in Ihrem Netzwerk automatisch zu aktualisieren.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|Windows RT.|

Mit dieser Einstellung können Sie einen WSUS-Server in Ihrem Netzwerk angeben, der als interner Updatedienst fungiert. Anstatt Microsoft Updates im Internet zu verwenden, durchsuchen WSUS-Clients diesen Dienst nach geeigneten Updates.

Zum Verwenden dieser Einstellung müssen Sie zwei Servernamenwerte festlegen: den Server, auf dem der Client Updates erkennt und herunterlädt, und den Server, auf den aktualisierte Arbeitsstationen Statistiken hochladen. Die Werte müssen nicht unterschiedlich sein, wenn beide Dienste auf demselben Server konfiguriert sind.

> [!NOTE]
> Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert ist, hat diese Richtlinie keine Auswirkung.

> [!NOTE]
> Unter Windows RT wird diese Richtlinie nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Wenn „Automatische Updates“ nicht per Richtlinie oder Benutzervoreinstellung deaktiviert sind, stellt der Client eine direkte Verbindung mit der Windows Update-Website im Internet her.|
|**Aktiviert**|Gibt an, dass sich der Client anstatt mit Windows Update mit dem angegebenen WSUS-Server verbindet, um Updates zu suchen und herunterzuladen. Die Aktivierung dieser Einstellung bedeutet, dass Endbenutzer in Ihrer Organisation zum Abrufen von Updates keine Firewall überwinden müssen. Außerdem erhalten Sie die Möglichkeit, Updates vor deren Bereitstellung zu testen.|
|**Deaktiviert**|Wenn „Automatische Updates“ nicht per Richtlinie oder Benutzervoreinstellung deaktiviert sind, stellt der Client eine direkte Verbindung mit der Windows Update-Website im Internet her.|

**Optionen:** Wenn diese Richtlinieneinstellung aktiviert ist, müssen Sie den Updatedienst im Intranet angeben, den WSUS-Clients zum Auffinden von Updates verwenden, und den Statistikserver im Internet, auf den aktualisierte WSUS-Clients Statistiken hochladen. Beispielwerte:


|                    Einstellungsoption:                    |    Beispielwert:    |
|-------------------------------------------------------|----------------------|
| Interner Updatedienst zum Ermitteln von Updates |  http://wsus01:8530  |
|          Intranetserver für die Statistik           | http://IntranetUpd01 |

#### <a name="turn-on-recommended-updates-via-automatic-updates"></a>Empfohlene Updates über automatische Updates aktivieren
Gibt an, ob „Automatische Updates“ WICHTIGE und empfohlene Updates von WSUS bereitstellt.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme ab Windows Vista, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass „Automatische Updates“ weiterhin WICHTIGE Updates bereitstellt, sofern das Feature bereits dafür konfiguriert sind.|
|**Aktiviert**|Gibt an, dass „Automatische Updates“ empfohlene und WICHTIGE Updates von WSUS bereitstellt.|
|**Deaktiviert**|Gibt an, dass „Automatische Updates“ weiterhin WICHTIGE Updates bereitstellt, sofern das Feature bereits dafür konfiguriert sind.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="turn-on-software-notifications"></a>Softwarebenachrichtigungen aktivieren
Mit dieser Richtlinieneinstellung können Sie steuern, ob Benutzer detaillierte optimierte Benachrichtigungen über vom Microsoft Update-Dienst vorgestellte Software angezeigt bekommen. Optimierte Benachrichtigungen vermitteln den Nutzen und fördern die Installation und Verwendung von optionaler Software. Diese Richtlinieneinstellung ist für die Verwendung in nicht so streng verwalteten Umgebungen vorgesehen, in denen Sie dem Endbenutzer den Zugriff auf den Microsoft Update-Dienst ermöglichen.

Wenn Sie den Microsoft Update-Dienst nicht verwenden, hat die Richtlinieneinstellung „Softwarebenachrichtigungen“ keine Auswirkung.

Wenn die Richtlinieneinstellung „Automatische Updates konfigurieren“ deaktiviert oder nicht konfiguriert ist, hat die Richtlinieneinstellung „Softwarebenachrichtigungen“ keine Auswirkung.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme ab Windows Server 2008 (Windows Vista) und Windows 7, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Richtlinieneinstellung ist standardmäßig deaktiviert.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Benutzern auf Computern mit Windows 7 werden keine Benachrichtigungen zu optionalen Anwendungen angeboten. Benutzern auf Computern mit Windows Vista werden keine Benachrichtigungen zu optionalen Anwendungen oder Updates angeboten. Ein lokaler Administrator kann diese Einstellung in der Systemsteuerung oder mithilfe einer lokalen Richtlinie ändern.|
|**Aktiviert**|Wenn Sie diese Richtlinieneinstellung aktivieren, wird eine Benachrichtigung auf dem Computer des Benutzers angezeigt, sobald die vorgestellte Software verfügbar ist. Der Benutzer kann auf die Benachrichtigung klicken, um Windows Update zu öffnen und weitere Informationen über die Software zu erhalten oder sie zu installieren. Der Benutzer kann auch auf **Diese Nachricht schließen** oder **Später anzeigen** klicken, um die Benachrichtigung entsprechend zurückzustellen.<p>Unter Windows 7 werden von dieser Richtlinieneinstellung nur detaillierte Benachrichtigungen für optionale Anwendungen gesteuert. Unter Windows Vista werden von dieser Richtlinieneinstellung detaillierte Benachrichtigungen für optionale Anwendungen und Updates gesteuert.|
|**Deaktiviert**|Gibt an, dass Benutzern von Windows 7 keine detaillierten Benachrichtigungen für optionale Anwendungen und Benutzern von Windows Vista keine detaillierten Benachrichtigungen zu optionalen Anwendungen oder optionalen Updates angeboten werden.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

### <a name="computer-configuration--maintenance-scheduler-policy-settings"></a>Computerkonfiguration > Wartungszeitplan (Richtlinieneinstellungen)
In der Einstellung „Automatische Updates konfigurieren“ haben Sie die Option **4: Autom. Herunterladen und laut Zeitplan installieren** ausgewählt. Sie können die Einstellungen für den Wartungszeitplan auf Computern mit Windows 8 und Windows RT in der Gruppenrichtlinien-Verwaltungskonsole angeben. Wenn Sie in der Einstellung „Automatische Updates konfigurieren“ nicht Option 4 ausgewählt haben, müssen Sie diese Einstellungen nicht für automatische Updates konfigurieren. Die Einstellungen für den Wartungszeitplan befinden sich in folgendem Pfad: *Richtlinienname* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Wartungszeitplan**. Die Gruppenrichtlinienerweiterung „Wartungszeitplan“ enthält die folgenden Einstellungen:

-   [Aktivierungsgrenze für automatische Wartung](#automatic-maintenance-activation-boundary)

-   [Zufällige Verzögerung für automatische Wartung](#automatic-maintenance-random-delay)

-   [Richtlinie für die Aktivierung der automatischen Wartung](#automatic-wakeup-policy)

#### <a name="automatic-maintenance-activation-boundary"></a>Aktivierungsgrenze für automatische Wartung
Mit dieser Richtlinie können Sie die Einstellung „Aktivierungsgrenze für automatische Wartung“ konfigurieren.

Die Aktivierungsgrenze für die Wartung ist die täglich geplante Uhrzeit des Starts der automatischen Wartung.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Einstellung bezieht sich auf Option 4 in **Automatische Updates konfigurieren**. Wenn Sie in **Automatische Updates konfigurieren** Option 4 nicht ausgewählt haben, müssen Sie diese Einstellung nicht konfigurieren.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Wenn diese Richtlinieneinstellung nicht konfiguriert ist, gilt für Clientcomputer die in der Systemsteuerung unter **Info-Center** > **Automatische Wartung** angegebene tägliche geplante Uhrzeit.|
|**Aktiviert**|Wenn Sie diese Richtlinieneinstellung aktivieren, werden alle Standard- oder geänderten Einstellungen überschrieben, die auf Clientcomputern in **Systemsteuerung** > **Info-Center** > **Automatische Wartung** (oder bei einigen Clientversionen **Wartung**) konfiguriert sind.|
|**Deaktiviert**|Wenn Sie diese Richtlinieneinstellung auf **Deaktiviert** festlegen, gilt für Clientcomputer die in der Systemsteuerung unter **Info-Center** > **Automatische Wartung** angegebene tägliche geplante Uhrzeit.|

#### <a name="automatic-maintenance-random-delay"></a>Zufällige Verzögerung für automatische Wartung
Mit dieser Richtlinie können Sie die Einstellung „Zufällige Verzögerung für automatische Wartung“ konfigurieren.

Die zufällige Verzögerung der Wartung ist die Zeitspanne, bis zu der die automatische Wartung ab ihrer Aktivierungsgrenze verzögert wird. Diese Einstellung ist nützlich für virtuelle Computer, bei denen eine zufällige Wartung eine Leistungsanforderung sein kann.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Einstellung bezieht sich auf Option 4 in **Automatische Updates konfigurieren**. Wenn Sie in **Automatische Updates konfigurieren** Option 4 nicht ausgewählt haben, müssen Sie diese Einstellung nicht konfigurieren.

Falls aktiviert, wird die regelmäßige Wartungsverzögerung standardmäßig auf **PT4H** festgelegt.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Eine vierstündige zufällige Verzögerung wird **Automatische Wartung** zugeordnet.|
|**Aktiviert**|Die automatische Wartung verzögert den Start ab ihrer Aktivierungsgrenze bis um die angegebene Zeitspanne.|
|**Deaktiviert**|„Automatische Wartung“ wird keine zufällige Verzögerung zugeordnet.|

#### <a name="automatic-wakeup-policy"></a>Richtlinie für die Aktivierung der automatischen Wartung
Mit dieser Richtlinie können Sie die Einstellung „Richtlinie für die Aktivierung der automatischen Wartung“ konfigurieren.

Die Richtlinie für die Aktivierung der Wartung gibt an, ob „Automatische Wartung“ eine Aktivierungsanforderung an den ausgeführten Computer für die tägliche geplante Wartung richten soll.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Wenn die Aktivierungsrichtlinie des ausgeführten Computers explizit deaktiviert ist, hat diese Einstellung keine Auswirkung.

> [!NOTE]
> Diese Einstellung bezieht sich auf Option 4 in **Automatische Updates konfigurieren**. Wenn Sie in **Automatische Updates konfigurieren** Option 4 nicht ausgewählt haben, müssen Sie diese Einstellung nicht konfigurieren.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Wenn Sie diese Richtlinieneinstellung auf nicht konfigurieren, gilt die in der Systemsteuerung unter **Info-Center** > **Automatische Wartung** angegebene Aktivierungseinstellung.|
|**Aktiviert**|Wenn Sie diese Richtlinieneinstellung aktivieren, versucht „Automatische Wartung“, eine Aktivierungsrichtlinie für das Betriebssystem festzulegen und bei Bedarf eine Aktivierungsanforderung für die tägliche geplante Uhrzeit zu stellen.|
|**Deaktiviert**|Wenn Sie diese Richtlinieneinstellung deaktivieren, gilt die in der Systemsteuerung unter **Info-Center** > **Automatische Wartung** angegebene Aktivierungseinstellung.|

### <a name="user-configuration--windows-update-policy-settings"></a>Benutzerkonfiguration > Windows Update (Richtlinieneinstellungen)
Dieser Abschnitt enthält Details zu den folgenden benutzerbasierten Richtlinieneinstellungen:

-   [Option „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anzeigen](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Die Standardoption „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anpassen](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [Zugriff auf alle Windows Update-Funktionen entfernen](#remove-access-to-use-all-windows-update-features)

In der Gruppenrichtlinien-Verwaltungskonsole befinden sich die Benutzereinstellungen für automatische Computerupdates im folgenden Pfad: *Richtlinienname* > **Benutzerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**. Die Einstellungen werden in der gleichen Reihenfolge aufgelistet, in der sie in den Gruppenrichtlinienerweiterungen „Computerkonfiguration“ und „Benutzerkonfiguration“ angezeigt werden, wenn die Registerkarte **Einstellungen** der Windows Update-Richtlinie so ausgewählt ist, dass die Einstellungen alphabetisch sortiert werden.

> [!NOTE]
> Standardmäßig sind diese Einstellungen, sofern nicht anders angegeben, nicht konfiguriert.

> [!TIP]
> Für jede dieser Einstellungen können Sie die folgenden Schritte ausführen, um die Einstellungen zu aktivieren, zu deaktivieren oder zwischen ihnen zu wechseln:

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog-box"></a>Option „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anzeigen
Gibt an, ob die Option **Updates installieren und herunterfahren** im Dialogfeld **Windows herunterfahren** angezeigt wird.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass die Option **Updates installieren und herunterfahren** im Dialogfeld **Windows herunterfahren** angezeigt wird, wenn Updates verfügbar sind, wenn der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|
|**Aktiviert**|Das Aktivieren dieser Richtlinieneinstellung bewirkt, dass **Updates installieren und herunterfahren** nicht als Option im Dialogfeld **Windows herunterfahren** angezeigt wird, selbst wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|
|**Deaktiviert**|Gibt an, dass die Option **Updates installieren und herunterfahren** im Dialogfeld **Windows herunterfahren** angezeigt wird, wenn Updates verfügbar sind, wenn der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog-box"></a>Die Standardoption „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anpassen
Gibt an, ob die Option **Updates installieren und herunterfahren** im Dialogfeld **Windows herunterfahren** als Standardoption zulässig ist.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

> [!NOTE]
> Diese Richtlinieneinstellung hat keine Auswirkung, wenn *Richtlinienname* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update** > **Option „Updates installieren und herunterfahren“ im Dialogfeld „Windows herunterfahren“ nicht anzeigen** aktiviert ist.

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, ob die Option **Updates installieren und herunterfahren** die Standardoption im Dialogfeld **Windows herunterfahren** wird, wenn Updates für die Installation zu dem Zeitpunkt verfügbar sind, zu dem der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|
|**Aktiviert**|Gibt an, ob die letzte Option des Benutzers zum Herunterfahren (z. B. „Ruhezustand“ oder „Neu starten“) die Standardoption im Dialogfeld **Windows herunterfahren** ist, und zwar unabhängig davon, ob die Option **Updates installieren und herunterfahren** im Menü **Wählen Sie einen Vorgang aus** verfügbar ist.|
|**Deaktiviert**|Gibt an, ob die Option **Updates installieren und herunterfahren** die Standardoption im Dialogfeld **Windows herunterfahren** wird, wenn Updates für die Installation zu dem Zeitpunkt verfügbar sind, zu dem der Benutzer die Option „Herunterfahren“ zum Herunterfahren des Computers auswählt.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="remove-access-to-use-all-windows-update-features"></a>Zugriff auf alle Windows Update-Funktionen entfernen
Mit dieser Einstellung können Sie den WSUS-Clientzugriff auf Windows Update aufheben.

|Unterstützt für:|Ausnahme:|
|---------|-------|
|Windows-Betriebssysteme, die sich noch innerhalb ihres [Lebenszyklus für den Support von Microsoft-Produkten](https://support.microsoft.com/gp/lifeselect) befinden.|ungültig|

|||
|-|-|
|**Status der Richtlinieneinstellung**|**Verhalten**|
|**Nicht konfiguriert**|Benutzer können eine Verbindung mit der Windows Update-Website herstellen.|
|**Aktiviert**|**WICHTIG:** Falls aktiviert, werden alle Windows Update-Features entfernt. Dazu gehört das Blockieren des Zugriffs auf die Windows Update-Website unter https://windowsupdate.microsoft.com, über den Windows Update-Link im Startmenü oder auf dem Startbildschirm und auch das Menü **Extras** in Internet Explorer. Die automatische Aktualisierung von Windows ist ebenfalls deaktiviert. Der Benutzer wird weder über wichtige Updates von Windows Update informiert noch erhält er diese. Diese Einstellung verhindert auch, dass der Geräte-Manager automatisch Treiberupdates von der Windows Update-Website installiert.<p>Falls aktiviert, können Sie eine der folgenden Benachrichtigungsoptionen konfigurieren:<p>-   **0: Keine Benachrichtigungen anzeigen**<br />    Durch diese Einstellung wird der gesamte Zugriff auf Windows Update-Features entfernt, und es werden keine Benachrichtigungen angezeigt.<br />-   **1: Benachrichtigungen über erforderlichen Neustart anzeigen**<br />    Diese Einstellung zeigt Benachrichtigungen zu Neustarts an, die zum Abschluss einer Installation erforderlich sind. **Hinweis:** Auf Computern mit Windows 8 und Windows RT werden bei aktivierter Richtlinie nur Benachrichtigungen über Neustarts und zur Tatsache angezeigt, dass Updates nicht erkannt werden können. Die Benachrichtigungsoptionen werden nicht unterstützt. Benachrichtigungen auf dem Anmeldebildschirm werden immer angezeigt.|
|**Deaktiviert**|Benutzer können eine Verbindung mit der Windows Update-Website herstellen.|

**Optionen:** Siehe **Aktiviert** in der Tabelle für diese Einstellung.

## <a name="supplemental-information"></a>Zusätzliche Informationen
Dieser Abschnitt bietet zusätzliche Informationen zum Öffnen und Speichern von WSUS-Einstellungen in Gruppenrichtlinien sowie Definitionen für die in diesem Leitfaden verwendeten Begriffe. Für Administratoren, die mit früheren Versionen von WSUS (3.2 und früher) vertraut sind, gibt es eine Tabelle, in der die Unterschiede zwischen WSUS-Versionen kurz zusammengefasst sind.

### <a name="accessing-the-windows-update-settings-in-group-policy"></a>Zugriff auf die Windows Update-Einstellungen in Gruppenrichtlinien
Nachfolgend wird beschrieben, wie Sie die Gruppenrichtlinien-Verwaltungskonsole auf Ihrem Domänencontroller öffnen. Anschließend wird beschrieben, wie Sie entweder ein bestehendes Gruppenrichtlinienobjekt auf Domänenebene zur Bearbeitung öffnen oder ein neues Gruppenrichtlinienobjekt auf Domänenebene erstellen und zur Bearbeitung öffnen.

> [!NOTE]
> Sie müssen Mitglied der Gruppe **Domänen-Admins** o. ä. sein, um diese Schritte ausführen zu können.

##### <a name="to-open-or-add-and-open-a-group-policy-object"></a>So können Sie ein Gruppenrichtlinienobjekt öffnen oder hinzufügen

1.  Wechseln Sie auf Ihrem Domänencontroller zu **Server-Manager** > **Tools** > **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.

2.  Erweitern Sie im linken Bereich Ihre Gesamtstruktur. Doppelklicken Sie beispielsweise auf **Gesamtstruktur: example.com**.

3.  Doppelklicken Sie im linken Bereich auf **Domänen** und dann auf die Domäne, für die Sie ein Gruppenrichtlinienobjekt verwalten möchten. Doppelklicken Sie beispielsweise auf **example.com**.

4.  Führen Sie eines der folgenden Verfahren aus:

    -  **Um ein bestehendes Gruppenrichtlinienobjekt auf Domänenebene zur Bearbeitung zu öffnen**, doppelklicken Sie auf die Domäne, die das zu verwaltende Gruppenrichtlinienobjekt enthält. Klicken Sie mit der rechten Maustaste auf die zu verwaltende Domänenrichtlinie, und klicken Sie dann auf **Bearbeiten**. Der Gruppenrichtlinienverwaltungs-Editor wird geöffnet.

    -  **So können Sie ein neues Gruppenrichtlinienobjekt erstellen und zur Bearbeitung öffnen**
        1.  Klicken Sie mit der rechten Maustaste auf die Domäne, für die Sie ein neues Gruppenrichtlinienobjekt erstellen möchten, und klicken Sie dann auf **Gruppenrichtlinienobjekt hier erstellen und verknüpfen**.

        2.  Geben Sie in **Neues Gruppenrichtlinienobjekt** in das Feld **Name** den Namen des neuen Gruppenrichtlinienobjekts ein, und klicken Sie dann auf **OK**.

        3.  Klicken Sie mit der rechten Maustaste auf Ihr neues Gruppenrichtlinienobjekt, und klicken Sie dann auf **Bearbeiten**. Der Gruppenrichtlinienverwaltungs-Editor wird geöffnet.

##### <a name="to-open-the-windows-update-or-maintenance-scheduler-extensions-of-group-policy"></a>So öffnen Sie die Gruppenrichtlinienerweiterungen „Windows Update“ oder „Wartungszeitplan“

1.  Führen Sie im Gruppenrichtlinienverwaltungs-Editor eine der folgenden Aktionen aus:

    -   **Öffnen Sie die Gruppenrichtlinienerweiterung „Computerkonfiguration > Windows Update“** . Navigieren Sie zu: *Richtlinienname* > **Computerkonfiguration** > **Richtlinien** / **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**.

    -   **Öffnen Sie die Gruppenrichtlinienerweiterung „Benutzerkonfiguration > Windows Update“** . Navigieren Sie zu: *Richtlinienname* > **Benutzerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**.

    -   **Öffnen Sie die Gruppenrichtlinienerweiterung „Computerkonfiguration> Wartungszeitplan“** . Navigieren Sie im Gruppenrichtlinienobjekt-Editor zu *Richtlinienname* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Wartungszeitplan**.

Weitere Informationen zu Gruppenrichtlinien finden Sie unter [Übersicht über Gruppenrichtlinien](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831791(v=ws.11)).

> [!TIP]
> Nachdem Sie die gewünschte Gruppenrichtlinienerweiterung geöffnet haben, können Sie mit den folgenden Schritten die Einstellungen aktivieren, deaktivieren oder zwischen ihnen wechseln:

##### <a name="to-configure-group-policy-settings"></a>So konfigurieren Sie Gruppenrichtlinieneinstellungen

1.  Doppelklicken Sie in *ExtensionOfGroupPolicy* auf die Einstellung, die Sie anzeigen oder ändern möchten.

2.  Führen Sie zum Konfigurieren der Einstellung einen der folgenden Schritte aus:

    -   Um den standardmäßig nicht angegebenen Status der Einstellung beizubehalten, wählen Sie **Nicht konfiguriert** aus.

    -   Um die Einstellung zu aktivieren, wählen Sie **Aktiviert** aus.

    -   Um die Einstellung zu deaktivieren, wählen Sie **Deaktiviert** aus.

3.  Wenn unter **Optionen** Optionen aufgeführt sind, behalten Sie die Standardwerte bei, oder ändern Sie sie nach Bedarf.

4.  Führen Sie eines der folgenden Verfahren aus:

    -   Um Ihre Änderungen zu speichern und mit der nächsten Einstellung fortzufahren, klicken Sie auf **Übernehmen** und dann auf **Nächste Einstellung**.

    -   Klicken Sie auf **OK**, um die Änderungen zu speichern und das Dialogfeld zu schließen.

    -   Klicken Sie auf **OK**, um die Änderungen zu speichern und das Dialogfeld zu schließen.

### <a name="changes-to-wsus-relevant-to-this-guide"></a>Für diesen Leitfaden relevante Änderungen an WSUS
In der folgenden Tabelle sind die wichtigsten Unterschiede zwischen der aktuellen und früheren Version von WSUS zusammengefasst, die für diesen Leitfaden relevant sind.

|Windows Server- und WSUS-Versionen|Beschreibung|
|------------------|--------|
| Windows Server 2012 R2 mit WSUS 6.0 und nachfolgende Versionen|Ab Windows Server 2012 ist die Serverrolle „WSUS“ in das Betriebssystem integriert, und die zugehörigen Gruppenrichtlinieneinstellungen für WSUS-Clients sind standardmäßig in Gruppenrichtlinien enthalten.|
| Windows Server 2008 (und frühere Versionen von Windows Server) mit WSUS 3 2 und früher|Unter Windows Server 2008 (und früheren Versionen von Windows Server) mit WSUS-Versionen 3.2 (und früher) sind die Gruppenrichtlinieneinstellungen zum Steuern von WSUS-Clients in diesen Windows Server-Betriebssystemen nicht enthalten. Die Richtlinieneinstellungen befinden sich in der administrativen WSUS-Vorlage **wuau.adm**. Bei diesen Serverversionen muss die administrative WSUS-Vorlage zunächst der Gruppenrichtlinien-Verwaltungskonsole hinzugefügt werden, bevor die WSUS-Clienteinstellungen konfiguriert werden können.|

### <a name="terms-and-definitions"></a>Begriffe und Definitionen
Es folgt eine Liste der in diesem Leitfaden verwendeten Begriffe.

|Begriff|Definition|
|----|-------|
|Automatische Updates|**Ein Dienst, der auf Windows-Computern ausgeführt wird** (Automatische Updates): Die Clientcomputerkomponente, die in die Microsoft-Betriebssysteme Windows Vista, Windows Server 2003, Windows XP und Windows 2000 mit SP3 integriert ist, um Updates von Microsoft Update oder Windows Update zu beziehen.<p>**Modern** (Automatische Updates): Der Begriff wird verwendet, um zu beschreiben, dass der Windows Update-Agent Updates automatisch plant und herunterlädt.|
|Autonomer Server|Ein Downstreamserver mit Windows Server Update Services (WSUS), auf dem Administratoren WSUS-Komponenten verwalten können.|
|Downstreamserver|Ein Server mit Windows Server Update Services (WSUS), der Updates von einem anderen WSUS-Server anstatt von Microsoft Update oder Windows Update bezieht.|
|Gruppenrichtlinienerweiterung (und: Erweiterung von Gruppenrichtlinie)|Eine Sammlung von Einstellungen in Gruppenrichtlinien, mit denen gesteuert wird, wie Benutzer und Computer (für die die Richtlinien gelten) verschiedene Windows-Dienste und -Funktionen konfigurieren und nutzen können. Administratoren können WSUS mit Gruppenrichtlinien für die clientseitige Konfiguration des Clients für „Automatische Updates“ verwenden, um sicherzustellen, dass Endbenutzer unternehmensweite Updaterichtlinien nicht deaktivieren oder umgehen können.<p>WSUS erfordert nicht den Einsatz von Active Directory oder Gruppenrichtlinien. Die Clientkonfiguration kann auch über eine lokale Gruppenrichtlinie oder durch Ändern der Windows-Registrierung angewendet werden.|
|Interner Updatedienst|Eine Netzwerkinfrastruktur, in der Updates mithilfe eines oder mehrerer WSUS-Server verteilt werden.|
|Replikatserver|Ein Downstreamserver mit Windows Server Update Services (WSUS), der die Genehmigungen und Einstellungen auf dem Upstreamserver spiegelt, mit dem er verbunden ist. Sie können WSUS nicht auf einem Replikatserver verwalten.|
|Microsoft Update|**Eine Microsoft-Downloadwebsite im Internet:** Eine Microsoft-Website im Internet, die Updates für Windows-Computer (Gerätetreiber), Windows-Betriebssysteme und andere Microsoft-Softwareprodukte speichert und verteilt.|
|Software Update Services (SUS)|SUS war das Vorgängerprodukt von Windows Server Update Services (WSUS).|
|Aktualisierungen|Eine Sammlung von Softwarerevisionen, Hotfixes, Service Packs, Feature Packs und Gerätetreibern, die auf einem Computer installiert werden können, um die Funktionalität zu erweitern oder Leistung und Sicherheit zu verbessern.|
|Updatedateien|Die Dateien, die zur Installation eines Updates auf einem Computer erforderlich sind.|
|Updateinformationen (auch als Metadaten für Updates bezeichnet):|Die Informationen über ein Update im Gegensatz zu dessen Binärdateien in einem Updatepaket. Metadaten bieten beispielsweise Informationen über die Eigenschaften eines Updates und ermöglichen es Ihnen so herauszufinden, wofür das Update nützlich ist. Zu den Metadaten gehören auch die Microsoft-Software-Lizenzbedingungen. Das Metadatenpaket, das für ein Update heruntergeladen wird, ist in der Regel wesentlich kleiner als das eigentliche Updatedateipaket.|
|Updatequelle|Der Speicherort, mit dem ein WSUS-Server (Windows Server Update Services) synchronisiert wird, um Updatedateien abzurufen. Dieser Speicherort kann entweder Microsoft Update oder ein Upstreamserver mit WSUS sein.|
|Upstreamserver|Ein WSUS-Server (Windows Server Update Services), der Updatedateien für einen anderen WSUS-Server bereitstellt, der wiederum als Downstreamserver bezeichnet wird.|
|Windows Server Update Services (WSUS)|Ein Serverrollenprogramm, das auf einem oder mehreren Windows Server-Computern in einem Unternehmensnetzwerk ausgeführt wird. Eine WSUS-Infrastruktur ermöglicht Ihnen, die Installation von Updates für Computer in Ihrem Netzwerk zu verwalten.<p>Mit WSUS können Sie Updates vor der Freigabe genehmigen oder ablehnen, die Installation von Updates bis zu einem bestimmten Datum erzwingen und umfangreiche Berichte darüber erhalten, welche Updates die einzelnen Computer in Ihrem Netzwerk benötigen. Sie können WSUS so konfigurieren, dass bestimmte Updateklassen automatisch genehmigt werden (kritische Updates, Sicherheitsupdates, Service Packs, Treiber usw.). WSUS ermöglicht Ihnen auch, Updates nur für die „Erkennung“ zu genehmigen, sodass Sie sehen können, welche Computer ein bestimmtes Update benötigen, ohne die Updates installieren zu müssen.<p>Bei einer WSUS-Implementierung muss mindestens ein WSUS-Server im Netzwerk eine Verbindung mit Microsoft Update herstellen, um verfügbare Updates herunterladen zu können. Basierend auf der Netzwerksicherheit und -konfiguration kann der Administrator bestimmen, wie viele andere Server sich direkt mit Microsoft Update verbinden.<p>Sie können einen WSUS-Server so konfigurieren, dass Updates über das Internet aus folgenden Quellen abgerufen werden können:<p>öffentliches Microsoft Update<br />öffentliches Windows Update<br />Microsoft Store|
|Windows Update|**Eine Microsoft-Downloadwebsite im Internet:** Eine Microsoft-Website im Internet, die Updates für Windows-Computer (Gerätetreiber) und Windows-Betriebssysteme speichert und verteilt.<p>**Computerdienst:** Der Name des Windows Update-Diensts, der auf Computern ausgeführt wird. Windows Update erkennt, lädt und installiert Updates auf Windows-Computern.<p>Je nach Computer- und Richtlinienkonfiguration kann der Windows Update-Agent Updates aus folgenden Quellen herunterladen:<p>Microsoft Update<br />Windows Update<br />Microsoft Store<br />Einem Updatedienst (WSUS) im Internet (Netzwerk)<p>Computer, die nicht in einer WSUS-basierten Umgebung verwaltet werden, verwenden in der Regel Windows Update, um sich direkt (über das Internet) mit Windows Update, Microsoft Update oder Microsoft Store zu verbinden und Updates zu beziehen.|
|WSUS-Client|Ein Computer, der Updates von einem WSUS-Updatedienst im Intranet erhält.<p>Bei Gruppenrichtlinieneinstellungen, die die Interaktion des Endbenutzers mit „Automatische Updates“ steuern: ein Benutzer eines Computers in einer WSUS-Umgebung.|