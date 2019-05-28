---
title: 'Schritt 4: Konfigurieren der Gruppenrichtlinieneinstellungen für automatische Updates'
description: Windows Server Update Service (WSUS)-Thema – Konfigurieren von Gruppenrichtlinieneinstellungen für automatische Updates wird im vierten Schritt in vier Schritten für die Bereitstellung von WSUS
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62177d05-d832-4ea8-bca4-47a8cd34a19c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 69b433ee3e0f57398db1e7814d2de24df7dd1696
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222924"
---
# <a name="step-4-configure-group-policy-settings-for-automatic-updates"></a>Schritt 4: Konfigurieren der Gruppenrichtlinieneinstellungen für automatische Updates

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

In einer active Directory-Umgebung können Sie die Gruppenrichtlinie zum Definieren der Interaktion zwischen Computer und Benutzer (bezeichnet in diesem Dokument als WSUS-Clients) und Windows-Updates, um automatische Updates von Windows Server Update Services (WSUS) zu erhalten.

Dieses Thema enthält zwei Hauptabschnitte:

[Gruppenrichtlinieneinstellungen für die WSUS-Clientupdates](#group-policy-settings-for-wsus-client-updates), die ausführliche Leitfäden bietet und Verhalten details zu den Windows Update und Wartungsplanungsmodul Einstellungen der Gruppenrichtlinie, die Steuern wie WSUS-Clients mit Windows Update interagieren können um automatische Updates zu erhalten.

[Zusätzliche Informationen](#supplemental-information) enthält die folgenden Abschnitte:

-   [Zugreifen auf die Windows Update-Einstellungen in der Gruppenrichtlinie](#accessing-the-windows-update-settings-in-group-policy), dem bietet es sich um allgemeine Anleitungen zur Verwendung von Gruppenrichtlinien-Editor, und Informationen zum Zugreifen auf den Erweiterungen der Update Services-Richtlinie und die Wartungsplanungsmodul-Einstellungen in Die Gruppenrichtlinie.

-   [Ändert sich in dieser Anleitung für WSUS](#changes-to-wsus-relevant-to-this-guide): für Administratoren mit WSUS 3.2 und früheren Versionen vertraut sind, dieser Abschnitt enthält eine kurze Zusammenfassung der wichtigsten Unterschiede zwischen der aktuellen und früheren Version von WSUS zu diesem Handbuch relevante.

-   [Begriffe und Definitionen](#terms-and-definitions): Definitionen für verschiedene Begriffe, die für WSUS und Update-Dienste, die in diesem Handbuch verwendet werden.

## <a name="group-policy-settings-for-wsus-client-updates"></a>Gruppenrichtlinieneinstellungen Sie für die WSUS-Client-updates
Dieser Abschnitt enthält Informationen zu drei Erweiterungen von Gruppenrichtlinie. In diesen Erweiterungen finden Sie die Einstellungen, die Sie verwenden können, so konfigurieren Sie die Interaktion zwischen WSUS-Clients und Windows-Update für automatische Updates zu erhalten.

-   [Computer Konfiguration &gt; Windows Update-Richtlinieneinstellungen](#computer-configuration--windows-update-policy-settings)

-   [Computer Konfiguration &gt; Wartungsplanungsmodul-Richtlinieneinstellungen](#computer-configuration--maintenance-scheduler-policy-settings)

-   [Benutzerkonfiguration &gt; Windows Update-Richtlinieneinstellungen](#user-configuration--windows-update-policy-settings)

> [!NOTE]
> In diesem Thema wird davon ausgegangen, dass Sie bereits nutzen, und klicken Sie mit der Gruppenrichtlinie vertraut sind. Wenn Sie nicht mit der Gruppenrichtlinie vertraut sind, sollten Sie überprüfen, dass die Informationen in den [Zusatzinformationen](#supplemental-information) Abschnitt dieses Dokuments vor dem Konfigurieren der Richtlinieneinstellungen für WSUS.

### <a name="computer-configuration--windows-update-policy-settings"></a>Computerkonfiguration > Windows Update-Richtlinieneinstellungen
Dieser Abschnitt enthält Informationen über die folgenden Computer basierenden Richtlinieneinstellungen:

-   [Sofortige Installation von Automatische Updates zulassen](#allow-automatic-updates-immediate-installation)

-   [Zulassen von nicht-Administratoren zum Empfangen von aktualisierungsbenachrichtigungen](#allow-non-administrators-to-receive-update-notifications)

-   [Mit Updates von einem Intranetspeicherort für Microsoft-Updatedienst zulassen](#allow-signed-updates-from-an-intranet-microsoft-update-service-location)

-   [Häufigkeit der Suche nach automatische Updates](#automatic-updates-detection-frequency)

-   [Konfigurieren Sie automatische Updates](#configure-automatic-updates)

-   [Neustart der Verzögerung für geplante Installationen](#delay-restart-for-scheduled-installations)

-   [Standardoption auf "Installieren Sie Updates und Herunterfahren" im Dialogfeld "nach unten Windows herunterfahren" werden nicht angepasst](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [Option "Installieren von Updates und Herunterfahren nach unten" nicht in schließen Sie die Windows-Dialogfeld anzeigen](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Die clientseitige zielzuordnung aktivieren](#enable-client-side-targeting)

-   [Aktivieren von Windows Update-Energieverwaltung auf dem Computer installieren geplanter Updates automatisch reaktiviert](#enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates)

-   [Keinen automatischen Neustart durchführen, angemeldete Benutzer für die geplante automatische updates von Installationen](#no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations)

-   [Für den Neustart durchführen, wenn geplante Installationen erneut aufgefordert.](#re-prompt-for-restart-with-scheduled-installations)

-   [Plant geplante Installationen von Automatische Updates](#reschedule-automatic-updates-scheduled-installations)

-   [Intranet-Microsoft-Updatedienst angeben](#specify-intranet-microsoft-update-service-location)

-   [Aktivieren Sie empfohlene Updates über automatische Updates](#turn-on-recommended-updates-via-automatic-updates)

-   [Software-Benachrichtigungen aktivieren](#turn-on-software-notifications)

Windows Update-Richtlinien für Computer-basierte Konfiguration befinden sich im Gruppenrichtlinienverwaltungs-Editor in dem Pfad: *PolicyName* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen**  >  **Windows-Komponenten** > **Windows Update**.

> [!NOTE]
> Standardmäßig sind diese Einstellungen nicht konfiguriert.

#### <a name="allow-automatic-updates-immediate-installation"></a>Sofortige Installation von Automatische Updates zulassen
Gibt an, ob automatische Updates automatisch Updates installiert werden, die nicht Windows-Diensten unterbrochen oder starten Sie Windows neu.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Wenn die richtlinieneinstellung "Automatische Updates konfigurieren", um festgelegt ist **deaktiviert**, diese Richtlinie hat keine Auswirkungen.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass Updates nicht sofort installiert werden. Lokale Administratoren können diese Einstellung ändern, mit dem lokalen Gruppenrichtlinien-Editor.|
|**Enabled**|Gibt an, dass automatische Updates sofort Updates installiert, nachdem sie heruntergeladen und zur Installation bereit sind.|
|**Deaktiviert**|Gibt an, dass Updates nicht sofort installiert werden.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="allow-non-administrators-to-receive-update-notifications"></a>Zulassen von nicht-Administratoren zum Empfangen von aktualisierungsbenachrichtigungen
Gibt an, ob es sich bei Benutzern ohne Administratorenberechtigungen basierte auf der richtlinieneinstellung konfigurieren Sie automatische Updates updatebenachrichtigungen erhält.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Erfahren Sie in der folgenden Tabelle.|

> [!NOTE]
> Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist oder nicht konfiguriert ist, hat diese Einstellung keine Auswirkungen.

> [!IMPORTANT]
> ab Windows 8 und Windows RT, ist mit dieser richtlinieneinstellung wird standardmäßig aktiviert. In allen früheren Versionen von Windows ist es standardmäßig deaktiviert.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass Benutzer immer ein Fenster "Benutzerkontensteuerung" angezeigt und erfordern erweiterte Berechtigungen zum Durchführen dieser Aufgaben können. Ein lokaler Administrator kann diese Einstellung ändern, mit dem lokalen Gruppenrichtlinien-Editor.|
|**Enabled**|Gibt an, dass Windows automatische Update und Microsoft Update nicht-Administratoren werden beim bestimmen, welche angemeldeten Benutzer updatebenachrichtigungen erhält. Nicht-Administratoren werden alle Inhalte für optionale empfohlene und wichtige Updates zu installieren, für die sie eine Benachrichtigung erhalten. Benutzer sehen kein Fenster "Benutzerkontensteuerung", und benötigen keinen erweiterte Berechtigungen zum Installieren dieser Updates, außer im Fall von Updates, die einstellungsänderungen der Benutzeroberfläche, End User License Agreement oder Windows Update-enthalten.<br /><br />Es gibt zwei Situationen, in denen die Auswirkung dieser Einstellung auf dem Computer Betriebssystem abhängig ist:<br /><br />1.  **Ausblenden** oder **wiederherstellen** Updates<br />2.  **Abbrechen** Installation eines Updates<br /><br />In Windows Vista oder Windows XP Wenn diese richtlinieneinstellung aktiviert ist, werden ein Fenster "Benutzerkontensteuerung" von Benutzern nicht angezeigt, und benötigen keinen erweiterte Berechtigungen zum Ausblenden, wiederherstellen oder Abbrechen von Updates.<br /><br />In Windows Vista Wenn diese richtlinieneinstellung aktiviert ist, Benutzer sehen kein Fenster "Benutzerkontensteuerung", und benötigen nicht erweiterte Berechtigungen zum Ausblenden, wiederherstellen oder Abbrechen von Updates. Wenn diese richtlinieneinstellung nicht aktiviert ist, Benutzern wird immer ein Fenster "Benutzerkontensteuerung" angezeigt, und sie erfordern erweiterte Berechtigungen zum Ausblenden, wiederherstellen oder Abbrechen von Updates.<br /><br />In Windows 7 hat diese richtlinieneinstellung keine Auswirkungen. Benutzern wird immer ein Fenster "Benutzerkontensteuerung" angezeigt, und sie erfordern erweiterte Berechtigungen zum Durchführen dieser Aufgaben können.<br /><br />In Windows 8 und Windows RT hat diese Einstellung keine Auswirkungen.|
|**Deaktiviert**|Gibt an, dass nur angemeldeten Administratoren auch updatebenachrichtigungen erhalten. **Hinweis**: In Windows 8 und Windows RT ist mit dieser richtlinieneinstellung wird standardmäßig aktiviert. In allen früheren Versionen von Windows ist es standardmäßig deaktiviert.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="allow-signed-updates-from-an-intranet-microsoft-update-service-location"></a>Signierte Updates aus einem Intranetspeicherort für Microsoft-Updatedienste zulassen
Gibt an, ob automatische Updates mit Updates akzeptiert, die von Entitäten als Microsoft signiert sind, wenn das Update auf einem Intranetspeicherort für Microsoft Update gefunden wird.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!NOTE]
> Updates von einem Dienst als eine Intranet-Microsoft Update-Dienst müssen immer von Microsoft signiert sein, und sie sind nicht betroffen von dieser richtlinieneinstellung wird festgelegt.

> [!NOTE]
> Diese Richtlinie wird auf Windows RT nicht unterstützt. Durch Aktivieren dieser Richtlinie wird auf Computern unter Windows RT sind nicht

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass Updates von einem Intranetspeicherort für Microsoft-Updatedienst von Microsoft signiert werden müssen.|
|**Enabled**|Gibt an, dass automatische Updates akzeptiert, Updates, die über ein Intranet-Speicherort für Microsoft Update empfangen, wenn sie von einem Zertifikat finden Sie unter "Vertrauenswürdige Herausgeber"-Zertifikatspeicher des lokalen Computers angemeldet sind.|
|**Deaktiviert**|Gibt an, dass Updates von einem Intranetspeicherort für Microsoft-Updatedienst von Microsoft signiert werden müssen.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="always-automatically-restart-at-the-scheduled-time"></a>Neustart immer automatisch zur geplanten Zeit durchführen
Gibt an, ob ein Neustart Timer immer beginnt sofort nach der Installation von Windows-Update wichtige Updates, anstelle der ersten benachrichtigen Benutzer auf dem Bildschirm "Anmeldung" für mindestens zwei Tage.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Wenn die richtlinieneinstellung "Installation" keinen automatischen Neustart durchführen, angemeldete Benutzer für die geplante automatische updates "aktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass es sich bei Windows Update Verhalten bei Neustart des Computers nicht geändert werden.|
|**Enabled**|Gibt an, dass ein Neustart Timer immer beginnt sofort nach der Installation von Windows-Update wichtige Updates, anstelle der ersten benachrichtigen Benutzer auf dem Bildschirm "Anmeldung" für mindestens zwei Tage.<br /><br />Zeitgeber für den Neustart kann konfiguriert werden, um einen Wert zwischen 15 und 180 Minuten zu starten. Wenn der Zeitgeber abläuft, wird der Neustart fortgesetzt, selbst wenn der Computer angemeldete Benutzer verfügt.|
|**Deaktiviert**|Gibt an, dass es sich bei Windows Update Verhalten bei Neustart des Computers nicht geändert werden.|

**Optionen:** Wenn diese Einstellung aktiviert ist, können Sie angeben, dass die Zeitspanne, die verstreicht, nachdem Updates installiert wurden, bevor ein erzwungener Neustart erfolgt.

#### <a name="automatic-updates-detection-frequency"></a>Suchhäufigkeit für automatische Updates
Gibt die Stunden an, die Windows verwendet, um zu bestimmen, wie lange gewartet wird, bevor nach verfügbaren Updates gesucht wird. Die genaue Wartezeit wird festgelegt, indem die hier angegebenen Stunden minus 0 bis 20 Prozent der angegebenen Stunden verwendet werden. Wenn diese Richtlinie verwendet wird, um eine Häufigkeit der Suche nach 20 Stunden anzugeben, werden alle Clients, die auf die diese Richtlinie angewendet wird z. B. für Updates an einer beliebigen Stelle zwischen 16 und 20 Stunden überprüfen.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!NOTE]
> Die Einstellung "Geben Sie an Intranet-Speicherort für Microsoft-Updatedienst" muss aktiviert sein, für diese Richtlinie angewendet werden kann.
>
> Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie wird auf Windows RT nicht unterstützt. Durch Aktivieren dieser Richtlinie wird auf Computern unter Windows RT sind nicht

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass Windows nach verfügbaren Updates auf dem Standardintervall von 22 Stunden überprüft wird.|
|**Enabled**|Gibt an, dass Windows nach verfügbaren Updates im angegebenen Intervall überprüft wird.|
|**Deaktiviert**|Gibt an, dass Windows nach verfügbaren Updates auf dem Standardintervall von 22 Stunden überprüft wird.|

**Optionen:** Wenn diese Einstellung aktiviert ist, können Sie angeben, dass das Zeitintervall (in Stunden), die Windows Update wartet, bevor nach Updates gesucht wird.

#### <a name="configure-automatic-updates"></a>Automatische Updates konfigurieren
Gibt an, gibt an, ob automatische Updates auf diesem Computer aktiviert sind.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Windows RT|

Wenn aktiviert, müssen Sie eine der vier Optionen zur Verfügung gestellt, in der Gruppenrichtlinien-Einstellung auswählen.

Wählen Sie für die Verwendung dieser Einstellung **aktiviert**, und klicken Sie dann im **Optionen** unter **automatische Updates konfigurieren**, wählen Sie eine der Optionen (2, 3, 4 oder 5).

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass die Verwendung der automatischen Updates nicht auf der Ebene der Gruppenrichtlinie angegeben ist. Ein Computeradministrator kann jedoch weiterhin automatische Updates in der Systemsteuerung konfigurieren.|
|**Enabled**|Gibt an, dass es sich bei Windows erkennt, wenn der Computer online ist und die Internetverbindung verwendet, um Windows Update nach verfügbaren Updates zu suchen.<br /><br />Wenn aktiviert, lokale Administratoren können die Windows Update-Systemsteuerung verwenden, um eine Konfigurationsoption ihrer Wahl zu auszuwählen. Lokale Administratoren werden jedoch nicht zulässig sein, um die Konfiguration für automatische Updates zu deaktivieren.<br /><br />-   **2 – für Download und Installation benachrichtigen**<br />    Wenn Windows Update Updates, die für den Computer gelten findet, werden die Benutzer informiert werden, dass Updates zum Download bereit sind. Benutzer können Sie Windows Update zum Herunterladen und installieren alle verfügbaren Updates ausführen.<br />-   **3 – Autom. herunterladen und vor Installation benachrichtigen** (Standardeinstellung)<br />    Windows Update sucht nach anwendbaren Updates und im Hintergrund herunterlädt. der Benutzer benachrichtigt oder unterbrochen wird, während des Prozesses nicht. Wenn die Downloads abgeschlossen sind, werden Benutzer benachrichtigt, dass Updates zur Installation bereit. Benutzer können Sie Windows Update zum Installieren der heruntergeladenen Updates ausführen.<br />-   **4 – Autom. herunterladen und laut Zeitplan installieren**<br />    Sie können den Zeitplan angeben, mit den Optionen in dieser Gruppenrichtlinieneinstellung wird festgelegt. Wenn kein Zeitplan angegeben ist, wird der Standardzeitplan für alle Installationen werden täglich um 03:00 Uhr Wenn Updates einen Neustart zum Abschließen der Installation erforderlich ist, wird Windows den Computer automatisch neu gestartet. (wenn ein Benutzer auf dem Computer Windows neu gestartet werden kann angemeldet ist, die Benutzer benachrichtigt und erhalten die Möglichkeit, den Neustart zu verzögern.) **Hinweis:** ab Windows 8, können Sie festlegen, Updates, die während der automatischen Wartung anstelle von einem bestimmten Zeitplan gebunden, die auf Windows Update installiert. Automatische Wartung werden Updates installieren, wenn der Computer nicht verwendet wird, und vermeiden die Updates zu installieren, wenn der Computer im Akkubetrieb ausgeführt wird. Wenn automatische Wartung zum Installieren von Updates innerhalb von Tagen nicht möglich ist, wird auf Windows Update Updates sofort installiert werden. Benutzer werden dann über einen ausstehenden Neustart benachrichtigt. Ein ausstehender Neustart wird nur stattfinden, wenn ohne Potenzial für eine versehentliche Datenverluste vorhanden ist.    Sie können Optionen angeben, in den Wartungsplanungsmodul Gruppenrichtlinienverwaltungs-Editor-Einstellungen, die sich im Pfad befinden, *PolicyName* > **Computer Konfiguration**  >  **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Wartung Scheduler** > **automatische Wartung Aktivierung Grenze**. Finden Sie im Abschnitt dieses Verweises mit dem Titel: [Scheduler-wartungseinstellungen](#computer-configuration--maintenance-scheduler-policy-settings), für die Details festlegen.    **5 – ermöglichen Sie lokalen Administrator, Einstellung auszuwählen**<br />– Gibt an, ob lokale Administratoren sind, die Systemsteuerung für automatische Updates verwenden, wählen Sie z. B. eine Konfigurationsoption ihrer Wahl, ob lokale Administratoren einen geplanten Installationszeitpunkt auswählen können.<br />    Lokale Administratoren dürfen die Konfiguration für automatische Updates nicht deaktivieren.|
|**Deaktiviert**|Gibt an, dass alle Clientupdates, die von der öffentlichen Windows-Update-Dienst zur Verfügung stehen müssen manuell aus dem Internet heruntergeladen und installiert werden.|

#### <a name="delay-restart-for-scheduled-installations"></a>Neustart der Verzögerung für geplante Installationen
Gibt die Zeitspanne, die automatische Updates, bevor Sie mit der ein geplanter Neustart gewartet wird an.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn automatische Updates konfiguriert ist, um geplante Installationen von Updates auszuführen. Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, nachdem Updates installiert werden, die Standard-Wartezeit von 15 Minuten verstreicht, bevor die alle Geplanter Neustart stattfindet.|
|**Enabled**|Gibt an, wenn die Installation abgeschlossen ist, ein geplanter Neustart ausgeführt wird, wenn die angegebene Anzahl von Minuten abgelaufen ist.|
|**Deaktiviert**|Gibt an, nachdem Updates installiert werden, die Standard-Wartezeit von 15 Minuten verstreicht, bevor die alle Geplanter Neustart stattfindet.|

**Optionen:** Wenn diese Einstellung aktiviert ist, können Sie diese Option verwenden, um anzugeben, die Menge der au-Zeit (in Minuten) wartet, bevor Sie mit der ein geplanter Neustart.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog"></a>Standardoption zum Installieren von Updates und Herunterfahren im Dialogfeld "nach unten Windows herunterfahren" werden nicht angepasst
Mit dieser richtlinieneinstellung können Sie angeben, ob die **Updates installieren "und" Herunterfahren** Option wird zugelassen, als die Standardauswahl in der **schließen Sie Windows** im Dialogfeld.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Mit dieser richtlinieneinstellung hat keine Auswirkungen, wenn die *PolicyName* > **Computer Konfiguration** > **Richtlinien**  >  **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update** > **nicht anzeigen " Installieren von Updates "und" Herunterfahren"Option schließen Sie die Windows-Dialogfeld** richtlinieneinstellung aktiviert ist.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass **Updates installieren "und" Herunterfahren** werden die Standardoption in der **schließen Sie Windows** im Dialogfeld, wenn Updates zur Installation, die zum Zeitpunkt sind der Benutzer wählt die Option "Herunterfahren", der Computer wird heruntergefahren.|
|**Enabled**|Wenn Sie diese richtlinieneinstellung aktivieren, wird eines Benutzers letzten Herunterfahren Ihrer Wahl (z. B. Ruhezustand oder neu starten), ist die Standardoption in der **schließen Sie Windows** (Dialogfeld), unabhängig davon, ob die **Updates installieren und Herunterfahren**  Option steht in der **Was möchten Sie vorgehen?** Menü.|
|**Deaktiviert**|Gibt an, dass **Updates installieren "und" Herunterfahren** werden die Standardoption in der **schließen Sie Windows** im Dialogfeld, wenn Updates zur Installation, die zum Zeitpunkt sind der Benutzer wählt die Option "Herunterfahren", der Computer wird heruntergefahren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="do-not-connect-to-any-windows-update-internet-locations"></a>Keine Verbindungen mit Windows Update-Internetadressen herstellen
Auch wenn Windows Update konfiguriert ist Updates aus einem Intranet-Update-Dienst zu erhalten, werden sie in regelmäßigen Abständen Informationen aus der öffentlichen Windows Update-Dienst erstellen, um zukünftige Verbindungen mit Windows Update zu aktivieren und andere Dienste wie Microsoft Update abgerufen oder Microsoft Store.

Durch Aktivieren dieser Richtlinie wird die Funktionalität zum Abrufen von Informationen aus der öffentlichen Windows Server Update Service in regelmäßigen Abständen deaktiviert, und es kann dazu führen, dass Verbindung öffentliche Dienste wie z. B. Microsoft Store nicht mehr funktioniert.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|beginnend mit Windows Server 2012 R2, Windows 8.1 oder Windows RT 8.1, Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Richtlinie gilt nur wenn der Computer konfiguriert ist, ein Intranet-Update-Dienst herstellen, mit der richtlinieneinstellung "Intranet Microsoft Updatedienst angeben".

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Das Standardverhalten zum Abrufen von Informationen aus der öffentlichen Windows Server Update Service weiterhin besteht.|
|**Enabled**|Gibt an, dass der Computer die Informationen aus der öffentlichen Windows Server Update Service nicht abgerufen werden.|
|**Deaktiviert**|Das Standardverhalten zum Abrufen von Informationen aus der öffentlichen Windows Server Update Service weiterhin besteht.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog"></a>Updates installieren und die Option "Herunterfahren" nicht in schließen Sie die Windows-Dialogfeld anzeigen
Gibt an, ob die **Updates installieren "und" Herunterfahren** Option wird angezeigt, der **schließen Sie Windows** Dialogfeld.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass die **Updates installieren "und" Herunterfahren** Option steht in der **schließen Sie Windows** im Dialogfeld, wenn Updates verfügbar sind, wenn der Benutzer die Option "Herunterfahren" zum Herunterfahren des Computers auswählt. Ein lokaler Administrator kann diese Einstellung ändern, lokale Richtlinie.|
|**Enabled**|Gibt an, dass **Updates installieren "und" Herunterfahren** erscheinen nicht als Option in der **unten Windows herunterfahren** Dialogfeld, selbst wenn Sie Updates für die Installation verfügbar sind, bei der Auswahl der Option "Herunterfahren", der Computer wird heruntergefahren.|
|**Deaktiviert**|Gibt an, dass die **Updates installieren "und" Herunterfahren** Option werden die Standardoption in der **schließen Sie Windows** im Dialogfeld, wenn Updates zur Installation, die zum Zeitpunkt der Benutzer auswählt sind, das Herunterfahren Option zum Herunterfahren des Computers.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="enable-client-side-targeting"></a>Clientseitige Zielzuordnung aktivieren
Gibt an, der Ziel-Gruppenname oder Namen, die in der WSUS-Konsole konfiguriert werden, die von WSUS Updates zu erhalten.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn dieser Computer konfiguriert ist, um die angegebene Ziel-Gruppennamen in WSUS zu unterstützen. Wenn es sich bei der Zielgruppennamen in WSUS nicht vorhanden ist, wird es ignoriert werden, bis zur Erstellung. Wenn die richtlinieneinstellung "Geben Sie an Intranet-Speicherort für Microsoft Update" deaktiviert oder nicht konfiguriert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie wird auf Windows RT nicht unterstützt. Durch Aktivieren dieser Richtlinie wird auf Computern unter Windows RT sind nicht

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass keine Gruppeninformationen zu WSUS gesendet wird. Ein lokaler Administrator kann diese Einstellung ändern, mit einer lokalen Richtlinie.|
|**Enabled**|Gibt an, die Informationen zur angegebenen Ziel an WSUS, gesendet wird, die verwendet wird, um zu bestimmen, welche Updates auf diesem Computer bereitgestellt werden sollen. Wenn mehrere Zielgruppen von WSUS unterstützt wird, können Sie diese Richtlinie, an mehrere Gruppennamen, die durch Semikolons getrennt werden, wenn Sie die Ziel-Gruppennamen in der Liste in der WSUS-Gruppe hinzugefügt haben. Andernfalls muss eine einzelne Gruppe angegeben werden.|
|**Deaktiviert**|Gibt an, dass keine Gruppeninformationen zu WSUS gesendet wird.|

**Optionen:** Verwenden Sie diesen Bereich, um eine oder mehrere Namen von Ziel anzugeben.

#### <a name="enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates"></a>Aktivieren von Windows Update-Energieverwaltung auf dem Computer installieren geplanter Updates automatisch reaktiviert
Gibt an, ob Windows Update die Windows-Energieverwaltung oder Energieoptionen Funktionen verwendet werden, auf dem Computer aus dem Ruhezustand automatisch reaktiviert wird, wenn Updates für die Installation geplant sind.

Der Computer wird automatisch aktiviert werden, nur dann, wenn Windows Update für die automatische Installation von Updates konfiguriert ist. Wenn der Computer in den Ruhezustand, ist wenn die Geplante Installationszeit tritt ein, und aktualisiert werden, wird Windows Update Ruhezustand des Computers zum Installieren der Updates automatisch die Funktionen von Windows Power Management "oder" Power-Optionen verwenden. Windows Update wird auch den Computer aktivieren und ein Update installieren, wenn ein Installationszeitlimit auftritt.

Der Computer wird nicht aktiviert werden, es sei denn, es sind Updates installiert werden. Wenn der Computer im Akkubetrieb, beim Windows Update reaktivieren, werden Updates nicht installiert, und der Computer wird automatisch in den Ruhezustand in zwei Minuten zurück.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|ab Windows Vista und Windows Server 2008 (Windows 7), Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Windows Update wird nicht den Computer aus dem Ruhezustand zum Installieren von Updates zu aktivieren. Ein lokaler Administrator kann diese Einstellung ändern, mit einer lokalen Richtlinie.|
|**Enabled**|Windows Update aktiviert den Computer aus dem Ruhezustand zum Installieren von Updates unter den zuvor genannten Bedingungen.|
|**Deaktiviert**|Windows Update wird nicht den Computer aus dem Ruhezustand zum Installieren von Updates zu aktivieren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations"></a>Keinen automatischen Neustart für geplante Installationen automatischer Updates durchführen, wenn Benutzer angemeldet sind
Gibt an, um eine geplante Installation abzuschließen, automatische Updates gewartet wird, für den Computer von einem Benutzer neu gestartet werden, wer angemeldet ist und den Computer nicht automatisch neu gestartet werden.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn automatische Updates konfiguriert ist, um geplante Installationen von Updates auszuführen. Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass automatische Updates dem Benutzer benachrichtigt, dass der Computer in fünf Minuten zum Abschließen der Installation automatisch neu gestartet wird.|
|**Enabled**|Einige Updates erfordern, den Computer neu gestartet werden, bevor die Updates wirksam werden. Wenn der Status auf aktiviert festgelegt ist, werden automatische Updates kein Computers automatisch während einer geplanten Installation neu gestartet, wenn ein Benutzer auf dem Computer angemeldet ist. Stattdessen benachrichtigt Automatische Updates den Benutzer den Computer neu starten.|
|**Deaktiviert**|Gibt an, dass automatische Updates dem Benutzer benachrichtigt, dass der Computer in fünf Minuten zum Abschließen der Installation automatisch neu gestartet wird.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="re-prompt-for-restart-with-scheduled-installations"></a>Erneut zu einem Neustart für geplante Installationen auffordern
Gibt die Zeitspanne für automatische Updates warten soll, bevor Sie erneut mit der ein geplanter Neustart aufgefordert.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!IMPORTANT]
> Diese Richtlinie gilt nur, wenn automatische Updates konfiguriert ist, um geplante Installationen von Updates auszuführen. Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie wirkt sich nicht auf Computern unter Windows RT.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Ein geplanter Neustart tritt auf, zehn Minuten nach dem Neustart von der Eingabeaufforderung für die Nachricht geschlossen wird. Ein lokaler Administrator kann diese Einstellung ändern, mit einer lokalen Richtlinie.|
|**Enabled**|Gibt an, nachdem die vorherige Aufforderung zum Neustart verschoben wurde, ein geplanter Neustart nach der angegebenen Anzahl von Minuten ablaufen ausgeführt wird.|
|**Deaktiviert**|Ein geplanter Neustart tritt auf, zehn Minuten nach dem Neustart von der Eingabeaufforderung für die Nachricht geschlossen wird.|

**Optionen:** Wenn aktiviert, können Sie diese Einstellungsoption, die Zeitdauer (in Minuten) angeben, die verstreicht, bevor die Benutzer über ein geplanter Neustart erneut aufgefordert werden.

#### <a name="reschedule-automatic-updates-scheduled-installations"></a>Geplante Installationen automatischer Updates erneut planen
Gibt die Zeitspanne für automatische Updates nach einem Starten des Computers, bevor Sie mit der eine geplante Installation warten, die zuvor nicht erfasst wurde.

Wenn der Status, um festgelegt wird **nicht konfiguriert**, eine verpasste geplante Installation erfolgt eine Minute, nachdem der Computer weiter wird gestartet.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn automatische Updates konfiguriert ist, um geplante Installationen von Updates auszuführen. Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass eine verpasste geplante Installation, dass eine Minute ausgeführt wird, nachdem der Computer weiter wird gestartet.|
|**Enabled**|Gibt an, dass eine geplante Installation, die zuvor nicht stattgefunden hat die angegebene Anzahl von Minuten nach dem nächsten des Computers Start ausgeführt wird.|
|**Deaktiviert**|Gibt an, dass eine verpasste geplante Installation mit der nächsten geplanten Installation ausgeführt wird.|

**Optionen:** Wenn diese richtlinieneinstellung aktiviert ist, können sie eine Anzahl von Minuten nach dem nächsten des Computers Start angeben, platzieren eine geplante Installation, die keinen zuvor erfolgt.

#### <a name="specify-intranet-microsoft-update-service-location"></a>Intranet-Microsoft-Updatedienst angeben
Gibt einen alternativen Intranetserver zum Hosten von Updates von Microsoft Update an. Dann können Sie WSUS verwenden, um Computer in Ihrem Netzwerk automatisch zu aktualisieren.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Windows RT.|

Mit dieser Einstellung können Sie einen WSUS-Server im Netzwerk angeben, die als interner Updatedienst funktionieren. Anstelle von Microsoft-Updates im Internet, werden WSUS-Clients diesen Dienst nach Updates suchen, die angewendet werden.

Um diese Einstellung verwenden zu können, müssen Sie zwei Server Name-Werte festlegen: der Server, von dem der Client erkennt und lädt Updates herunter, und der Server, auf das aktualisierte Arbeitsstationen Statistiken hochladen. Die Werte müssen nicht unterscheiden, wenn beide Dienste auf dem gleichen Server konfiguriert sind.

> [!NOTE]
> Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie wird auf Windows RT nicht unterstützt. Durch Aktivieren dieser Richtlinie wird auf Computern unter Windows RT sind nicht

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Wenn automatische Updates nicht von Richtlinie oder einer benutzereinstellung deaktiviert ist, gibt diese Richtlinie an, dass Clients direkt auf die Windows Update-Website im Internet eine Verbindung herstellen.|
|**Enabled**|Gibt an, dass der Client eine mit dem angegebenen WSUS-Server anstelle von Windows Update Verbindung, suchen und Herunterladen von Updates. Aktivieren diese Einstellung bedeutet, dass Benutzer in Ihrer Organisation nicht über eine Firewall zum Abrufen von Updates zu wechseln müssen, und es Ihnen die Möglichkeit bietet, Updates vor der Bereitstellung zu testen.|
|**Deaktiviert**|Wenn automatische Updates nicht von Richtlinie oder einer benutzereinstellung deaktiviert ist, gibt diese Richtlinie an, dass Clients direkt auf die Windows Update-Website im Internet eine Verbindung herstellen.|

**Optionen:** Wenn diese richtlinieneinstellung aktiviert ist, müssen Sie angeben, dass Updatedienst, WSUS-Clients werden bei der Erkennung von Updates und Internet Statistiken Servers, auf dem WSUS-Clients aktualisiert, die Statistiken hochladen möchten. Beispielwerte:

|Festlegen der Option:|Beispielwert:|
|----------|---------|
|Legen Sie den Intranet-Update-Dienst zum Ermitteln von updates|http://wsus01:8530|
|Legen Sie den Intranet-Statistik-server|http://IntranetUpd01|

#### <a name="turn-on-recommended-updates-via-automatic-updates"></a>Aktivieren Sie empfohlene Updates über automatische Updates
Gibt an, ob automatische Updates wichtige übermittelt und empfohlene Updates von WSUS.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|ab Windows Vista, Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass automatische Updates wichtige Updates zu übermitteln weiterhin, wenn er bereits konfiguriert ist, zu diesem Zweck.|
|**Enabled**|Gibt an, dass automatische Updates, empfohlene Updates und andere wichtige Updates installiert wird von WSUS.|
|**Deaktiviert**|Gibt an, dass automatische Updates wichtige Updates zu übermitteln weiterhin, wenn er bereits konfiguriert ist, zu diesem Zweck.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="turn-on-software-notifications"></a>Software-Benachrichtigungen aktivieren
Mit dieser richtlinieneinstellung können Sie steuern, ob Benutzer die ausführliche verbesserte Benachrichtigungen über ausgewählte Software von Microsoft Update-Dienst finden Sie unter. Verbesserte Benachrichtigungen vermitteln des Werts und fördern die Installation und Verwendung von optionalen Software. Mit dieser richtlinieneinstellung wird, dient zur Verwendung in lose verwalteten Umgebungen, in der Sie die Endbenutzerzugriff auf den Microsoft Update-Dienst zulassen.

Wenn Sie Microsoft Update-Dienst nicht verwenden, hat die richtlinieneinstellung "Benachrichtigungen" Software "keine Auswirkungen.

Wenn die richtlinieneinstellung "Automatische Updates konfigurieren" deaktiviert ist oder nicht konfiguriert ist, hat die richtlinieneinstellung "Benachrichtigungen" Software "keine Auswirkungen.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|ab Windows Server 2008 (Windows Vista) und Windows 7, Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Richtlinieneinstellung ist standardmäßig deaktiviert.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Benutzer auf dem Computer, auf denen Windows 7 ausführen, werden keine Nachrichten für optionale Anwendungen angeboten. Benutzer auf Computern, auf denen Windows Vista ausgeführt werden, werden keine Nachrichten für optionale Anwendungen oder Updates angeboten. Ein lokaler Administrator kann diese Einstellung mithilfe der Systemsteuerung oder eine lokale Richtlinie ändern.|
|**Enabled**|Wenn Sie diese richtlinieneinstellung aktivieren, erscheint eine Benachrichtigung auf dem Computer des Benutzers empfohlen, dass die Software zur Verfügung steht. Der Benutzer kann die Benachrichtigung, öffnen Sie Windows Update erhalten weitere Informationen zur Software und installieren Sie es dann. Außerdem kann der Benutzer klicken **schließen Sie diese Meldung** oder **später anzeigen** auf die Benachrichtigung nach Bedarf zu verzögern.<br /><br />In Windows 7 wird über diese richtlinieneinstellung wird nur detaillierte Benachrichtigungen für optionale Anwendungen steuern. Diese richtlinieneinstellung steuert in Windows Vista ausführliche Benachrichtigungen für optionale Anwendungen und Updates.|
|**Deaktiviert**|Gibt an, dass Benutzer, die mit Windows 7 werden keine ausführliche Benachrichtigungen für optionale Anwendungen angeboten, und Benutzern, die mit Windows Vista wird nicht ausführliche Benachrichtigungen für optionale Anwendungen oder optionale Updates angeboten.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

### <a name="computer-configuration--maintenance-scheduler-policy-settings"></a>Computer-Konfiguration > Wartungsplanungsmodul-Richtlinieneinstellungen
In der Einstellung für automatische Updates konfigurieren Sie die Option ausgewählt **4 – Autom. herunterladen und laut Zeitplan installieren**, können Sie angeben, zeitplaneinstellungen Wartungsplanungsmodul in der Gruppenrichtlinien-Verwaltungskonsole für Computer unter Windows 8 und Windows RT. Wenn Sie Option 4 nicht in der Einstellung "Automatische Updates konfigurieren" ausgewählt haben, müssen Sie nicht zum Konfigurieren dieser Einstellungen für automatische Updates. Scheduler-wartungseinstellungen befinden sich im Pfad: *PolicyName* > **Computer Konfiguration** > **Richtlinien** > **Administrative Vorlagen**  >  **Windows-Komponenten** > **Wartungsplanungsmodul**. Die Wartungsplanungsmodul Erweiterung der Gruppenrichtlinie enthält die folgenden Einstellungen:

-   [Automatische Wartung Aktivierung Grenze](#automatic-maintenance-activation-boundary)

-   [Automatische Wartung zufällige Verzögerung](#automatic-maintenance-random-delay)

-   [Automatische WakeUp-Richtlinie](#automatic-wakeup-policy)

#### <a name="automatic-maintenance-activation-boundary"></a>Aktivierungsgrenze für automatische Wartung
Diese Richtlinie können Sie zum Konfigurieren der Einstellung "Automatische Wartung Aktivierung Grenze".

Die Wartung Aktivierung Grenze ist der täglich geplanten Zeitpunkt an dem automatische Wartung beginnt.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Einstellung bezieht sich auf die Option "4" in **automatische Updates konfigurieren**. Wenn Sie die Option "4" in nicht ausgewählt haben **automatische Updates konfigurieren**, es ist nicht erforderlich, diese Einstellung zu konfigurieren.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Wenn diese richtlinieneinstellung nicht konfiguriert ist, geplante des täglichen Zeit angegeben, auf den Clientcomputern in der **Wartungscenter** > **automatische Wartung** Systemsteuerung gelten.|
|**Enabled**|Diese richtlinieneinstellung aktiviert überschreibt alle Standard- oder Änderung von Einstellungen, die auf den Clientcomputern konfiguriert **Systemsteuerung** > **Wartungscenter**  >   **Automatische Wartung** (oder in einigen Clientversionen **Wartung**).|
|**Deaktiviert**|Wenn Sie diese richtlinieneinstellung auf **deaktiviert**, wird die tägliche geplante Uhrzeit gemäß der **Wartungscenter** > **automatische Wartung**, im Steuerelement Bereich gelten.|

#### <a name="automatic-maintenance-random-delay"></a>Automatische Wartung zufällige Verzögerung
Mit dieser richtlinieneinstellung können Sie die zufällige Verzögerung für automatische Wartung Aktivierung zu konfigurieren.

Die zufällige Verzögerung für Wartung ist die Zeitspanne, die bis zu dem automatische Wartung verzögert die Begrenzung für die Aktivierung ab. Diese Einstellung ist nützlich für virtuelle Computer, in zufälligen Wartung eine leistungsfunktion möglicherweise.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Einstellung bezieht sich auf die Option "4" in **automatische Updates konfigurieren**. Wenn Sie die Option "4" in nicht ausgewählt haben **automatische Updates konfigurieren**, es ist nicht erforderlich, diese Einstellung zu konfigurieren.

Standardmäßig, wenn aktiviert, die zufällige Verzögerung für regelmäßige Wartung wird auf festgelegt **PT4H**.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Eine zufällige Verzögerung von vier Stunden gilt für **automatische**.|
|**Enabled**|Automatische Wartung wird verzögert, die Aktivierung Begrenzung von bis zu die angegebene Zeitspanne ab.|
|**Deaktiviert**|Keine zufällige Verzögerung wird für automatische Wartung übernommen.|

#### <a name="automatic-wakeup-policy"></a>Automatische WakeUp-Richtlinie
Mit dieser richtlinieneinstellung können Sie die Richtlinie für die automatische Wartung Aktivierungsproxy zu konfigurieren.

Die Richtlinie für die Wartung Aktivierungsproxy gibt an, ob automatische Wartung eine Aktivierungsproxy-Anforderung mit dem Betriebssystemen Computer für die tägliche geplante Wartung.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Wenn es sich bei der Betriebssystem Computer Power-Aktivierung ist Richtlinie ist explizit deaktiviert werden, diese Einstellung hat keine Auswirkungen.

> [!NOTE]
> Diese Einstellung bezieht sich auf die Option "4" in **automatische Updates konfigurieren**. Wenn Sie die Option "4" in nicht ausgewählt haben **automatische Updates konfigurieren**, es ist nicht erforderlich, diese Einstellung zu konfigurieren.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Wenn Sie diese richtlinieneinstellung nicht konfigurieren, legen Sie als aktivierungspakete angegeben, der **Wartungscenter** > **automatische Wartung** Systemsteuerung gelten.|
|**Enabled**|Wenn Sie diese richtlinieneinstellung aktivieren, versucht automatische Wartung, legen Sie eine Reaktivierung betriebssystemrichtlinie und stellen eine Aktivierungsproxy-Anforderung für die tägliche geplante Zeit, falls erforderlich.|
|**Deaktiviert**|Wenn Sie diese richtlinieneinstellung deaktivieren, legen Sie als aktivierungspakete angegeben, der **Wartungscenter** > **automatische Wartung** Systemsteuerung gelten.|

### <a name="user-configuration--windows-update-policy-settings"></a>Benutzerkonfiguration > Windows Update-Richtlinieneinstellungen
Dieser Abschnitt enthält Details zu den folgenden benutzerbasierte Richtlinieneinstellungen:

-   ["Installieren Sie Updates und Option" Herunterfahren"" nicht in schließen Sie die Windows-Dialogfeld anzeigen](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Passen Sie im Dialogfeld schließen Sie die Windows nicht Standardoption auf "Installieren Sie Updates und Herunterfahren"](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [Entfernen Sie den Zugriff auf alle Windows Update-Funktionen](#remove-access-to-use-all-windows-update-features)

In der Gruppenrichtlinien-Verwaltungskonsole befinden sich die Einstellungen für automatische Updates im Pfad: *PolicyName* > **Benutzerkonfiguration** > **Richtlinien** > **Administrative Vorlagen**  >  **Windows-Komponenten** > **Windows Update**. Die Einstellungen sind in der gleichen Reihenfolge aufgeführt, wie sie in den Computer Configuration und User Configuration-Erweiterungen in den Gruppenrichtlinien angezeigt werden bei der **Einstellungen** die Windows Update-Richtlinie auf der Registerkarte ausgewählt ist, um die Einstellungen zu sortieren. alphabetisch sortiert.

> [!NOTE]
> In der Standardeinstellung sind, sofern nichts anderes angegeben ist, diese Einstellungen nicht konfiguriert.

> [!TIP]
> für jede dieser Einstellungen können Sie die folgenden Schritte aus, aktivieren, deaktivieren, oder Navigieren zwischen Einstellungen:

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog-box"></a>Option "Updates installieren und Herunterfahren" im Dialogfeld schließen Sie die Windows nicht anzeigen
Gibt an, ob die **Updates installieren "und" Herunterfahren** Option wird angezeigt, der **schließen Sie Windows** Dialogfeld.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, dass die **Updates installieren "und" Herunterfahren** Option wird angezeigt, der **schließen Sie Windows** im Dialogfeld, wenn Updates verfügbar sind, wenn der Benutzer die Option "Herunterfahren" zum Herunterfahren des Computers auswählt.|
|**Enabled**|Wenn Sie diese richtlinieneinstellung aktivieren **Updates installieren "und" Herunterfahren** erscheinen nicht als Option in der **schließen Sie Windows** Dialogfeld, selbst wenn Sie Updates für die Installation verfügbar sind, wenn der Benutzer auswählt der Beenden Sie die Option zum Herunterfahren des Computers.|
|**Deaktiviert**|Gibt an, dass die **Updates installieren "und" Herunterfahren** Option wird angezeigt, der **schließen Sie Windows** im Dialogfeld, wenn Updates verfügbar sind, wenn der Benutzer die Option "Herunterfahren" zum Herunterfahren des Computers auswählt.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog-box"></a>Passen Sie im Dialogfeld schließen Sie die Windows nicht Standardoption auf "Installieren Sie Updates und Herunterfahren"
Gibt an, ob die **Updates installieren "und" Herunterfahren** -Option ist zulässig, als die Standardauswahl in der **schließen Sie die Windows** im Dialogfeld.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Mit dieser richtlinieneinstellung hat keine Auswirkungen, wenn die *PolicyName* > **Benutzerkonfiguration** > **Richtlinien**  >   **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update** > **nicht anzeigen " Im Dialogfeld "nach unten Windows herunterfahren" die Option "Installieren von Updates" und "Herunterfahren"** aktiviert ist.

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Gibt an, ob die **Updates installieren "und" Herunterfahren** Option werden die Standardoption in der **schließen Sie Windows** im Dialogfeld, wenn Updates zur Installation, die zum Zeitpunkt sind der Benutzer das Herunterfahren wählt Klicken Sie unten die Option zum Herunterfahren des Computers.|
|**Enabled**|Gibt an, ob des Benutzers letzten Herunterfahren Ihrer Wahl (z. B. "Ruhezustand" oder "Neustart") die Standardoption in der **schließen Sie Windows** (Dialogfeld), unabhängig davon, ob die **Option"Updatesinstallieren"und"Herunterfahren"** finden Sie in der **Was möchten Sie vorgehen?** Menü.|
|**Deaktiviert**|Gibt an, ob die **Updates installieren "und" Herunterfahren** Option werden die Standardoption in der **schließen Sie Windows** im Dialogfeld, wenn Updates zur Installation, die zum Zeitpunkt sind der Benutzer das Herunterfahren wählt Klicken Sie unten die Option zum Herunterfahren des Computers.|

**Optionen:** Es gibt keine Optionen für diese Einstellung aus.
    
#### <a name="remove-access-to-use-all-windows-update-features"></a>Zugriff auf alle Windows Update-Funktionen entfernen
Mit dieser Einstellung können Sie WSUS-Client den Zugriff auf Windows Update zu entfernen.

|Unterstützt auf:|Ausschließen:|
|---------|-------|
|Windows-Betriebssysteme, die sich innerhalb ihrer [Supportlebenszyklus für Microsoft-Produkte](https://support.microsoft.com/gp/lifeselect).|Null|

|||
|-|-|
|**Einstellung des Richtlinienstatus**|**Behavior**|
|**Nicht konfiguriert**|Benutzer können Verbindung mit der Windows Update-Website zur Verfügung.|
|**Enabled**|**Wichtig:** Wenn aktivieren, um alle Windows Update-Funktionen werden entfernt. Dies schließt den Zugriff auf die Windows Update-Website unter blockiert https://windowsupdate.microsoft.com, aus den Windows Update-Link auf der Startseite im Menü "oder" starten, sowie für die **Tools** in Internet Explorer im Menü. Automatische Aktualisierung von Windows ist auch deaktiviert; der Benutzer weder benachrichtigt werden über noch kritische Updates über Windows Update empfangen. Diese Einstellung verhindert, dass Geräte-Manager automatische Installation von Updates für Treiber von der Windows Update-Website.<br /><br />Wenn aktiviert, können Sie eine der folgenden Benachrichtigungsoptionen konfigurieren:<br /><br />-   **0 – anzeigen keine Benachrichtigungen**<br />    Diese Einstellung werden alle Zugriffe auf Windows Update-Funktionen zu entfernen und keine Benachrichtigungen angezeigt werden.<br />-   **1 – anzeigen neustartbenachrichtigungen erforderlichen**<br />    Diese Einstellung zeigt Benachrichtigungen zu Neustarts, die zum Abschluss einer Installation erforderlich sind. **Hinweis**: Auf Computern wird Windows 8 und Windows RT ausgeführt, wenn diese Richtlinie aktiviert ist, nur Benachrichtigungen in Zusammenhang mit neu gestartet wird und der Unfähigkeit zum Ermitteln von Updates angezeigt. Die Benachrichtigungsoptionen werden nicht unterstützt. Benachrichtigungen auf dem Anmeldebildschirm werden immer angezeigt.|
|**Deaktiviert**|Benutzer können Verbindung mit der Windows Update-Website zur Verfügung.|

**Optionen:** Finden Sie unter **aktiviert** für diese Einstellung in der Tabelle.

## <a name="supplemental-information"></a>Zusätzliche Informationen
Dieser Abschnitt enthält Informationen zur Verwendung von öffnen und Speichern von WSUS-Einstellungen im Gruppenrichtlinien- und -Definitionen für Begriffe, die in diesem Handbuch verwendet. Für Administratoren, die mit früheren Versionen von WSUS (WSUS 3.2 und früheren Versionen) vertraut sind ist eine Tabelle, die Unterschiede zwischen WSUS-Versionen kurz zusammengefasst.

### <a name="accessing-the-windows-update-settings-in-group-policy"></a>Zugreifen auf die Windows Update-Einstellungen in der Gruppenrichtlinie
Die folgenden Prozedur wird beschrieben, wie zum Öffnen der Gruppenrichtlinien-Verwaltungskonsole auf dem Domänencontroller wird. Anschließend wird beschrieben, wie eine vorhandene auf Domänenebene Gruppenrichtlinienobjekt (GPO) für die Bearbeitung zu öffnen oder erstellen ein neues GPO der Domänenebene und zur Bearbeitung öffnen, werden.

> [!NOTE]
> Sie müssen Mitglied der **Domänen-Admins** Gruppe oder äquivalent, um dieses Verfahren auszuführen.

##### <a name="to-open-or-add-and-open-a-group-policy-object"></a>Zum Öffnen oder hinzufügen, und öffnen Sie ein Gruppenrichtlinienobjekt

1.  Wechseln Sie auf dem Domänencontroller zu **Server-Manager**, > **Tools**, > **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.

2.  Erweitern Sie im linken Bereich der Gesamtstruktur aus. Doppelklicken Sie z. B. **Gesamtstruktur: "example.com"** .

3.  Doppelklicken Sie im linken Bereich auf **Domänen**, und doppelklicken Sie dann auf die Domäne, die für die Sie ein Gruppenrichtlinienobjekt verwalten möchten. Doppelklicken Sie z. B. **"example.com"** .

4.  Führen Sie eines der folgenden Verfahren aus:

    -  **Öffnen Sie ein vorhandenes GPO der Domänenebene für die Bearbeitung**, doppelklicken klicken Sie auf die Domäne, die das Gruppenrichtlinienobjekt, die Sie verwalten möchten enthält, mit der rechten Maustaste der Domänenrichtlinie, die Sie verwalten möchten, und klicken Sie dann auf **bearbeiten**. Group Policy Management Editor (Gruppenrichtlinienverwaltungs-Editor) wird geöffnet.

    -  **Erstellen ein neues Gruppenrichtlinienobjekt, und öffnen zum Bearbeiten von**:
        1.  Mit der rechten Maustaste in der Domäne für die Sie erstellen ein neues Gruppenrichtlinienobjekt, und klicken Sie dann auf möchten **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**.

        2.  In **neues Gruppenrichtlinienobjekt**im **Namen**, geben Sie einen Namen für das neue Gruppenrichtlinienobjekt, und klicken Sie dann auf **OK**.

        3.  Mit der rechten Maustaste in des neuen Gruppenrichtlinienobjekts, und klicken Sie dann auf **bearbeiten**. Gruppenrichtlinienverwaltungs-Editor wird geöffnet.

##### <a name="to-open-the-windows-update-or-maintenance-scheduler-extensions-of-group-policy"></a>Um die Windows Update oder Wartungsplanungsmodul Erweiterungen von Gruppenrichtlinien zu öffnen.

1.  Führen Sie eine der folgenden Schritte aus, im Gruppenrichtlinien-Editor:

    -   **Öffnen Sie den Computer Configuration > Windows Update-Erweiterung der Gruppenrichtlinie**. Navigieren Sie zu: *PolicyName* > **Computer Konfiguration** > **Richtlinien** / **Administrative Vorlagen**  >  **Windows-Komponenten** > **Windows Update**.

    -   **Öffnen Sie die Benutzerkonfiguration > Windows Update-Erweiterung der Gruppenrichtlinie**. Navigieren Sie zu: *PolicyName* > **Benutzerkonfiguration** > **Richtlinien** > **Administrative Vorlagen**  >  **Windows-Komponenten** > **Windows Update**.

    -   **Öffnen Sie den Computer Configuration > Wartungsplanungsmodul Erweiterung der Gruppenrichtlinie**. Navigieren Sie im GPOE, zu *PolicyName* > **Computer Konfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Wartungsplanungsmodul**.

Weitere Informationen zu Gruppenrichtlinien finden Sie unter [Group Policy Overview](https://technet.microsoft.com/library/hh831791.aspx(v=ws.12)).

> [!TIP]
> Wenn Sie die Erweiterung der Gruppenrichtlinie geöffnet haben, die Sie möchten, können Sie die folgenden Schritte aus zu aktivieren, deaktivieren, oder Navigieren zwischen Einstellungen:

##### <a name="to-configure-group-policy-settings"></a>So konfigurieren Sie Gruppenrichtlinieneinstellungen

1.  In *ExtensionOfGroupPolicy*, doppelklicken Sie auf die Einstellung, die Sie anzeigen oder ändern möchten.

2.  Führen Sie eine der folgenden Schritte aus, um die Einstellung zu konfigurieren:

    -   Die Standardeinstellung beibehalten unspecified Status der Einstellung der Option **nicht konfiguriert**.

    -   Um die Einstellung zu aktivieren, wählen **aktiviert**.

    -   Wählen Sie zum Deaktivieren der Einstellung, **deaktiviert**.

3.  In **Optionen**, wenn keine Optionen aufgelistet werden, die Standardwerte beibehalten oder ändern sie nach Bedarf.

4.  Führen Sie eines der folgenden Verfahren aus:

    -   Um die Änderungen zu speichern, und fahren Sie mit der nächsten Einstellung, klicken Sie auf **übernehmen**, und klicken Sie dann auf **nächste Einstellung**.

    -   Um die Änderungen zu speichern und schließen Sie das Dialogfeld, klicken Sie auf **OK**.

    -   Um alle nicht gespeicherten Änderungen verwerfen und das Dialogfeld zu schließen, klicken Sie auf **Abbrechen**.

### <a name="changes-to-wsus-relevant-to-this-guide"></a>Änderungen an dieser Anleitung für WSUS
Die folgende Tabelle enthält die wichtigsten Unterschiede zwischen den aktuellen und früheren Versionen von WSUS, die zu diesem Handbuch relevant sind.

|Windows Server und WSUS-Versionen|Beschreibung|
|------------------|--------|
| Windows Server 2012 R2 mit WSUS 6.0 und spätere Versionen|ab Windows Server 2012 können die WSUS-Serverrolle ist mit dem Betriebssystem integriert und die zugehörigen gruppenrichtlinieneinstellungen für die WSUS-Clients sind, standardmäßig in der Gruppenrichtlinie enthalten.|
| Windows Server 2008 (und früheren Versionen von Windows Server) mit WSUS 3.2 und früher|In Windows Server 2008 (und früheren Versionen von Windows Server) mithilfe von WSUS-Version 3.2 (und früher) sind die gruppenrichtlinieneinstellungen, die steuern, WSUS-Clients nicht in diesen Windows Server-Betriebssystemen enthalten. Die Richtlinieneinstellungen werden in der WSUS-Administrative Vorlage **wuau.adm**. Bei diesen Serverversionen muss die WSUS-Administrative Vorlage zunächst in der Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC) hinzugefügt werden, bevor die WSUS-Client-Einstellungen konfiguriert werden können.|

### <a name="terms-and-definitions"></a>Begriffe und Definitionen
Es folgt eine Liste der in dieser Anleitung verwendeten Begriffen.

|Begriff|Definition|
|----|-------|
|Automatische Updates|**Ein Dienst, der auf Windows-Computern ausgeführt wird** (Automatische Updates): Bezieht sich auf die Computer-Clientkomponente, die in der Microsoft Windows Vista, Windows Server 2003, Windows XP und Windows 2000 mit SP3-Betriebssystemen Updates aus Microsoft Update oder Windows Update abrufen erstellt.<br /><br />**Gelegentliche Verweis** (automatische Updates): Der Begriff verwendet, um beim Beschreiben der Windows Update-Agent automatisch plant und downloads von Updates.|
|autonome server|Können Sie an einen Downstreamserver mit Windows Server Update Services (WSUS) finden Sie auf dem WSUS-Komponenten Administratoren verwaltet werden können.|
|Downstreamserver|Verwenden Sie, um auf einem Windows Server Update Services (WSUS)-Server verweisen, die Updates von einem anderen WSUS-Server und nicht über Microsoft Update oder Windows-Updates abruft.|
|Gruppieren Sie die Erweiterung der Gruppenrichtlinie (und: Erweiterung der Gruppenrichtlinie|Eine Auflistung von Einstellungen in der Gruppenrichtlinie, die zum Steuern, wie Benutzer und -Computer (für die die Richtlinien gelten) konfigurieren und verwenden Sie verschiedene Windows-Dienste und Funktionen können verwendet werden. Administratoren können WSUS mithilfe der Gruppenrichtlinie für die clientseitige Konfiguration von Clients für automatische Updates, um sicherzustellen, dass Endbenutzer nicht deaktiviert oder umgangen werden Richtlinien für Unternehmen.<br /><br />WSUS erfordert die Verwendung von active Directory oder die Gruppenrichtlinie nicht. Client-Konfiguration kann auch mit lokalen Gruppenrichtlinien oder durch Ändern der Windows-Registrierung angewendet werden.|
|Interner Updatedienst|Ein casual Verweis an der Netzwerkinfrastruktur, die einen oder mehrere WSUS-Server verwendet, um Updates zu verteilen.|
|Replikatserver|Verwenden Sie, um auf einen Downstreamserver mit Windows Server Update Services (WSUS) verweisen, die spiegelt die Genehmigungen und Einstellungen auf dem Upstreamserver, der mit dem sie verbunden ist. Sie können keine WSUS auf einem Replikatserver verwalten.|
|Microsoft Update|**Ein Internet-basierte Microsoft-Download-Website:** Eine Microsoft Internet-Website, die gespeichert und verteilt Updates für Windows-Computern (Gerätetreiber), Windows-Betriebssysteme und andere Microsoft-Softwareprodukte.|
|Software Update Services (SUS)|SUS war der Vorgänger-Produkt für Windows Server Update Services (WSUS).|
|Aktualisierungen|Alle einer Auflistung von Softwareversionen, Hotfixes, Servicepacks, Feature Packs und Gerätetreiber, die installiert werden können, auf einem Computer aus, um Funktionalität zu erweitern oder Verbessern von Leistung und Sicherheit.|
|Updatedateien|Die Dateien erforderlich, um ein Update auf einem Computer installieren.|
|Updateinformationen (auch bekannt als Metadaten)|Die Informationen zu einer Aktualisierung im Gegensatz zu den Binärdateien für Updates in einer Updatepaket. Beispielsweise liefert Metadaten Informationen für die Eigenschaften eines Updates, sodass Sie herausfinden, welche das Update nützlich ist. Metadaten umfassen auch die Microsoft Software-Lizenzbedingungen. Für ein Update heruntergeladene Metadatenpaket ist in der Regel viel kleiner ist als das eigentliche Updatedateipaket.|
|Updatequelle|Der Speicherort, den ein Server für Windows Server Update Services (WSUS) synchronisiert wird, um Updatedateien abzurufen. Dieser Speicherort kann entweder Microsoft Update oder einen upstream-WSUS-Server sein.|
|Upstream-server|Ein Windows Server Update Services (WSUS)-Server, der Updatedateien an einem anderen WSUS-Server bereitstellt, die wiederum als einen Downstreamserver bezeichnet wird.|
|Windows Server Update Services (WSUS)|Ein Server-Rolle-Programm, das auf eine oder mehrere Windows Server-Computer in einem Unternehmensnetzwerk ausgeführt wird. Eine WSUS-Infrastruktur können Sie zum Verwalten von Updates für Computer in Ihrem Netzwerk installieren.<br /><br />Können Sie WSUS verwenden, zu genehmigen oder ablehnen von Updates vor, um Updates zu installieren, indem Sie ein bestimmtes Datum, zu erzwingen, und um erhalten umfangreiche Berichte auf jedem Computer in Ihrem Netzwerk, welche updates erfordert. Sie können WSUS so konfigurieren, bestimmte Klassen von Updates automatisch genehmigen (wichtige Updates, Sicherheitsupdates, Servicepacks, Treibern usw.). WSUS ermöglicht Ihnen so genehmigen Sie Updates für die "Erkennung", auch, damit Sie sehen, welche Computer eine Aktualisierung benötigen, ohne die Updates zu installieren.<br /><br />In einer WSUS-Implementierung muss mindestens ein WSUS-Server im Netzwerk für die Verbindung zu Microsoft Update, um verfügbare Updates herunterzuladen. Auf der Grundlage der Netzwerksicherheit und-Konfiguration kann der Administrator ermittelt, wie viele andere Server direkt mit Microsoft Update zu verbinden.<br /><br />Sie können einen WSUS-Server zum Abrufen von Updates über das Internet aus solchen Quellen als konfigurieren:<br /><br />-der öffentlichen Microsoft-Updates<br />-der öffentlichen Windows-Updates<br />-   Microsoft Store|
|Windows Update|**Ein Internet-basierte Microsoft-Download-Website:** Eine Microsoft Internet-Website, die gespeichert und verteilt Updates für Windows-Computer (Gerätetreiber) und Windows-Betriebssysteme.<br /><br />**Computer-Dienst:** Der Name des Windows Update-Diensts, die auf Computern ausgeführt wird. Windows Update erkennt, downloads und Updates auf Windows-Computern installiert.<br /><br />Je nach Computer und Konfigurationen für Gruppenrichtlinien können die Windows Update-Agent Updates herunterladen:<br /><br />-Microsoft-Updates<br />-Windows Update<br />-   Microsoft Store<br />: Eine Internet (Netzwerk)-Update-Dienst (WSUS)<br /><br />Computer, die nicht in einer Umgebung mit WSUS verwaltet werden in der Regel verwenden Windows Update die Verbindung direkt – über das Internet – mit Windows Update, Microsoft Update oder Microsoft Store, um Updates herunterzuladen.|
|WSUS-Client|Ein Computer, der Updates von einem WSUS-Intranet-Update-Dienst empfängt.<br /><br />Im Fall von Gruppenrichtlinien-Einstellungen zur Steuerung der Interaktion durch den Endbenutzer, bei denen automatische Updates: ein Benutzer eines Computers in einer WSUS-Umgebung.|
