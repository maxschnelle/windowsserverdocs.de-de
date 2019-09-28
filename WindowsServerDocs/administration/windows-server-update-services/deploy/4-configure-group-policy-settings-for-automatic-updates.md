---
title: 'Schritt 4: Konfigurieren von Gruppenrichtlinie Einstellungen für automatische Updates'
description: 'Thema zu Windows Server Update Service (WSUS): Konfigurieren von Gruppenrichtlinie Einstellungen für automatische Updates ist Schritt 4 in einem vierstufigen Verfahren zum Bereitstellen von WSUS'
ms.prod: windows-server
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
ms.openlocfilehash: a01d8881e8f0f7ca6feff691938f926a12460db0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361661"
---
# <a name="step-4-configure-group-policy-settings-for-automatic-updates"></a>Schritt 4: Konfigurieren von Gruppenrichtlinie Einstellungen für automatische Updates

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In einer Active Directory-Umgebung können Sie mit Gruppenrichtlinie definieren, wie Computer und Benutzer (in diesem Dokument als WSUS-Clients bezeichnet) mit Windows-Updates interagieren können, um automatische Updates von Windows Server Update Services (WSUS) abzurufen.

Dieses Thema enthält zwei Hauptabschnitte:

[Gruppenrichtlinie Einstellungen für WSUS-Client Updates](#group-policy-settings-for-wsus-client-updates), die ausführliche Leitfäden und Verhaltens Details zu den Windows Update und Wartungszeit Planungs Einstellungen von Gruppenrichtlinie bereitstellen, mit denen gesteuert wird, wie WSUS-Clients mit Windows Update interagieren können Abrufen von automatischen Updates.

[Ergänzende Informationen](#supplemental-information) sind in den folgenden Abschnitten aufgeführt:

-   [Der Zugriff auf die Windows Update Einstellungen in Gruppenrichtlinie](#accessing-the-windows-update-settings-in-group-policy), die allgemeine Anleitungen zur Verwendung von Gruppenrichtlinie Management Editor bietet, sowie Informationen zum Zugreifen auf die Update Services-Richtlinien Erweiterungen und die Wartungsplaner-Einstellungen in der Gruppe. Policy.

-   [Änderungen an WSUS, die für dieses Handbuch relevant](#changes-to-wsus-relevant-to-this-guide)sind: für Administratoren, die mit WSUS 3,2 und früheren Versionen vertraut sind, enthält dieser Abschnitt eine kurze Zusammenfassung der wichtigsten Unterschiede zwischen der aktuellen und der früheren Version von WSUS, die für dieses Handbuch relevant sind.

-   [Begriffe und Definitionen](#terms-and-definitions): Definitionen für verschiedene Begriffe im Zusammenhang mit WSUS und Update Diensten, die in diesem Handbuch verwendet werden.

## <a name="group-policy-settings-for-wsus-client-updates"></a>Gruppenrichtlinie Einstellungen für WSUS-Client Updates
Dieser Abschnitt enthält Informationen zu drei Erweiterungen Gruppenrichtlinie. In diesen Erweiterungen finden Sie die Einstellungen, die Sie verwenden können, um zu konfigurieren, wie WSUS-Clients mit Windows Update interagieren können, um automatische Updates zu erhalten.

-   [Computerkonfiguration &gt; Windows Update Richtlinien Einstellungen](#computer-configuration--windows-update-policy-settings)

-   [Computerkonfiguration &gt; Wartungsplaner Richtlinien Einstellungen](#computer-configuration--maintenance-scheduler-policy-settings)

-   [Benutzerkonfiguration &gt; Windows Update Richtlinien Einstellungen](#user-configuration--windows-update-policy-settings)

> [!NOTE]
> In diesem Thema wird davon ausgegangen, dass Sie bereits verwenden und mit Gruppenrichtlinie vertraut sind. Wenn Sie mit Gruppenrichtlinie nicht vertraut sind, sollten Sie die Informationen im Abschnitt [zusätzliche Informationen](#supplemental-information) in diesem Dokument lesen, bevor Sie versuchen, die Richtlinien Einstellungen für WSUS zu konfigurieren.

### <a name="computer-configuration--windows-update-policy-settings"></a>Computer Konfiguration > Windows Update Richtlinien Einstellungen
Dieser Abschnitt enthält Details zu den folgenden computerbasierten Richtlinien Einstellungen:

-   [Sofortige Installation automatische Updates zulassen](#allow-automatic-updates-immediate-installation)

-   [Nicht Administratoren erlauben, Update Benachrichtigungen zu empfangen](#allow-non-administrators-to-receive-update-notifications)

-   [Signierte Updates von einem Intranet-Speicherort für den Microsoft Update Dienst zulassen](#allow-signed-updates-from-an-intranet-microsoft-update-service-location)

-   [Häufigkeit der automatische Updates Erkennung](#automatic-updates-detection-frequency)

-   [Konfigurieren von Automatische Updates](#configure-automatic-updates)

-   [Verzögerter Neustart für geplante Installationen](#delay-restart-for-scheduled-installations)

-   [Passen Sie die Standardoption "Updates installieren und Herunterfahren" im Dialogfeld "Windows Herunterfahren" nicht an.](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [Option "Updates installieren und Herunterfahren" im Dialogfeld "Windows Herunterfahren" nicht anzeigen](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Client seitige Ziel Ausrichtung aktivieren](#enable-client-side-targeting)

-   [Aktivieren der Windows Update Energie Verwaltung zum automatischen Reaktivieren des Computers zur Installation geplanter Updates](#enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates)

-   [Kein automatischer Neustart mit angemeldeten Benutzern für geplante Installationen von automatischen Updates](#no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations)

-   [Erneut zum Neustart bei geplanten Installationen auffordern](#re-prompt-for-restart-with-scheduled-installations)

-   [Planen Sie automatische Updates geplanten Installationen neu.](#reschedule-automatic-updates-scheduled-installations)

-   [Intranetspeicherort für Microsoft Update Dienst angeben](#specify-intranet-microsoft-update-service-location)

-   [Empfohlene Updates über automatische Updates aktivieren](#turn-on-recommended-updates-via-automatic-updates)

-   [Software Benachrichtigungen aktivieren](#turn-on-software-notifications)

In der GPME befinden sich Windows Update Richtlinien für die computerbasierte Konfiguration im folgenden Pfad: *PolicyName* > **Computer Konfiguration** > -**Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**.

> [!NOTE]
> Standardmäßig sind diese Einstellungen nicht konfiguriert.

#### <a name="allow-automatic-updates-immediate-installation"></a>Automatische Updates sofort installieren
Gibt an, ob automatische Updates Updates automatisch installiert, die Windows-Dienste nicht unterbrechen oder Windows neu starten.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Wenn die Richtlinien Einstellung "configure automatische Updates" auf " **deaktiviert**" festgelegt ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Updates nicht sofort installiert werden. Lokale Administratoren können diese Einstellung mithilfe des lokalen Gruppenrichtlinie-Editors ändern.|
|**Enabled**|Gibt an, dass automatische Updates Updates sofort installiert, nachdem Sie heruntergeladen und bereit für die Installation sind.|
|**Deaktiviert**|Gibt an, dass Updates nicht sofort installiert werden.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="allow-non-administrators-to-receive-update-notifications"></a>Nicht Administratoren erlauben, Update Benachrichtigungen zu empfangen
Gibt an, ob Benutzer, die nicht Administratoren sind, Update Benachrichtigungen auf der Grundlage der Richtlinien Einstellung Automatische Updates konfigurieren erhalten.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Weitere Informationen finden Sie in der folgenden Tabelle.|

> [!NOTE]
> Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert oder nicht konfiguriert ist, hat diese Richtlinien Einstellung keine Auswirkungen.

> [!IMPORTANT]
> ab Windows 8 und Windows RT ist diese Richtlinien Einstellung standardmäßig aktiviert. In allen früheren Versionen von Windows ist es standardmäßig deaktiviert.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Benutzern immer ein Fenster für die Konto Steuerung angezeigt wird und erweiterte Berechtigungen für diese Aufgaben erforderlich sind. Ein lokaler Administrator kann diese Einstellung mithilfe des lokalen Gruppenrichtlinie-Editors ändern.|
|**Enabled**|Gibt an, dass automatische Windows-Updates und-Microsoft Update nicht-Administratoren enthalten, wenn festgelegt wird, welcher angemeldete Benutzer Update Benachrichtigungen empfängt. Benutzer, die nicht Administratoren sind, können alle optionalen, empfohlenen und wichtigen Update Inhalte installieren, für die Sie eine Benachrichtigung erhalten haben. Benutzern wird kein Fenster "Benutzerkontensteuerung" angezeigt, und Sie benötigen keine erhöhten Berechtigungen zum Installieren dieser Updates, außer bei Updates, die die Benutzeroberfläche, den Endbenutzer-Lizenzvertrag oder Windows Update Einstellungsänderungen enthalten.<br /><br />Es gibt zwei Situationen, in denen die Auswirkung dieser Einstellung vom Betriebs Computer abhängt:<br /><br />1.  **Ausblenden** oder **Wiederherstellen** von Updates<br />2.  **Abbrechen** einer Update Installation<br /><br />Wenn diese Richtlinien Einstellung in Windows Vista oder Windows XP aktiviert ist, wird Benutzern das Fenster "Benutzerkontensteuerung" nicht angezeigt, und Sie benötigen keine erhöhten Berechtigungen zum Ausblenden, wiederherstellen oder Abbrechen von Updates.<br /><br />Wenn diese Richtlinien Einstellung aktiviert ist, wird Benutzern in Windows Vista kein Fenster "Benutzerkontensteuerung" angezeigt, und Sie benötigen keine erhöhten Berechtigungen zum Ausblenden, wiederherstellen oder Abbrechen von Updates. Wenn diese Richtlinien Einstellung nicht aktiviert ist, wird Benutzern immer ein Fenster für die Konto Steuerung angezeigt, und Sie benötigen erweiterte Berechtigungen, um Updates auszublenden, wiederherzustellen oder abzubrechen.<br /><br />In Windows 7 hat diese Richtlinien Einstellung keine Auswirkungen. Benutzern wird immer ein Fenster für die Konto Steuerung angezeigt, und Sie benötigen erweiterte Berechtigungen, um diese Aufgaben auszuführen.<br /><br />In Windows 8 und Windows rt hat diese Richtlinien Einstellung keine Auswirkungen.|
|**Deaktiviert**|Gibt an, dass nur angemeldete Administratoren Update Benachrichtigungen erhalten. **Hinweis**: In Windows 8 und Windows RT ist diese Richtlinien Einstellung standardmäßig aktiviert. In allen früheren Versionen von Windows ist es standardmäßig deaktiviert.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="allow-signed-updates-from-an-intranet-microsoft-update-service-location"></a>Signierte Updates aus einem Intranetspeicherort für Microsoft-Updatedienste zulassen
Gibt an, ob automatische Updates Updates akzeptiert, die von anderen Entitäten als Microsoft signiert werden, wenn das Update an einem Intranet-Speicherort für den Microsoft Update Dienst gefunden wird.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Windows RT|

> [!NOTE]
> Updates von einem anderen Dienst als einem Intranet-Microsoft Update-Dienst müssen immer von Microsoft signiert werden und sind von dieser Richtlinien Einstellung nicht betroffen.

> [!NOTE]
> Diese Richtlinie wird in Windows RT nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

**Optionen:** Es gibt keine Optionen für diese Einstellung.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Updates von einem Intranet-Speicherort für den Microsoft Update Dienst von Microsoft signiert werden müssen.|
|**Enabled**|Gibt an, dass automatische Updates Updates akzeptiert, die über einen Intranet-Speicherort für den Microsoft Update-Dienst empfangen wurden, wenn Sie durch ein Zertifikat signiert sind, das sich im Zertifikat Speicher "Vertrauenswürdige Herausgeber" des|
|**Deaktiviert**|Gibt an, dass Updates von einem Intranet-Speicherort für den Microsoft Update Dienst von Microsoft signiert werden müssen.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="always-automatically-restart-at-the-scheduled-time"></a>Neustart immer automatisch zur geplanten Zeit durchführen
Gibt an, ob ein Neustartzeit Geber immer sofort beginnt, nachdem Windows Update wichtige Updates installiert hat, anstatt zuerst die Benutzer für mindestens zwei Tage auf dem Anmeldebildschirm zu benachrichtigen.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Wenn die Richtlinien Einstellung "kein automatischer Neustart mit angemeldeten Benutzern für geplante automatische Updates" aktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Windows Update das Neustart Verhalten des Computers nicht ändert.|
|**Enabled**|Gibt an, dass ein Neustartzeit Geber immer sofort beginnt, nachdem Windows Update wichtige Updates installiert hat, anstatt zuerst die Benutzer für mindestens zwei Tage auf dem Anmeldebildschirm zu benachrichtigen.<br /><br />Der Zeitgeber für den Neustart kann so konfiguriert werden, dass er mit einem beliebigen Wert zwischen 15 und 180 Minuten beginnt. Wenn der Zeitgeber ausgeführt wird, wird der Neustart auch dann fortgesetzt, wenn sich der Computer angemeldet hat.|
|**Deaktiviert**|Gibt an, dass Windows Update das Neustart Verhalten des Computers nicht ändert.|

**Optionen:** wenn diese Einstellung aktiviert ist, können Sie den Zeitraum angeben, nach dem Updates installiert werden, bevor ein erzwungener Computer neu gestartet wird.

#### <a name="automatic-updates-detection-frequency"></a>Suchhäufigkeit für automatische Updates
Gibt die Stunden an, die Windows verwendet, um zu bestimmen, wie lange gewartet wird, bevor nach verfügbaren Updates gesucht wird. Die genaue Wartezeit wird festgelegt, indem die hier angegebenen Stunden minus 0 bis 20 Prozent der angegebenen Stunden verwendet werden. Wenn diese Richtlinie z. b. verwendet wird, um eine Erkennungs Häufigkeit von 20 Stunden anzugeben, wird von allen Clients, auf die diese Richtlinie angewendet wird, eine Überprüfung auf Updates zwischen 16 und 20 Stunden durchgeführt.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Windows RT|

> [!NOTE]
> Die Einstellung "Intranetspeicherort für den Microsoft-Update Dienst angeben" muss aktiviert sein, damit diese Richtlinie wirksam wird.
>
> Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie wird in Windows RT nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass Windows im Standardintervall von 22 Stunden auf verfügbare Updates prüfen soll.|
|**Enabled**|Gibt an, dass Windows im angegebenen Intervall auf verfügbare Updates prüfen soll.|
|**Deaktiviert**|Gibt an, dass Windows im Standardintervall von 22 Stunden auf verfügbare Updates prüfen soll.|

**Optionen:** wenn diese Einstellung aktiviert ist, können Sie das Zeitintervall (in Stunden) festlegen, das Windows Update wartet, bevor nach Updates gesucht wird.

#### <a name="configure-automatic-updates"></a>Automatische Updates konfigurieren
Gibt an, ob auf diesem Computer automatische Updates aktiviert sind.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Windows RT|

Wenn diese Option aktiviert ist, müssen Sie eine der vier Optionen auswählen, die in dieser Gruppenrichtlinie Einstellung angegeben sind.

Um diese Einstellung zu verwenden, wählen Sie **aktiviert**aus, und wählen Sie dann in **Optionen** unter **Automatische Aktualisierung konfigurieren**eine der Optionen (2, 3, 4 oder 5) aus.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass die Verwendung von automatischen Updates auf Gruppenrichtlinie Ebene nicht angegeben wird. Ein Computer Administrator kann jedoch weiterhin automatische Updates in der Systemsteuerung konfigurieren.|
|**Enabled**|Gibt an, dass Windows erkennt, wenn der Computer online ist und die Internet Verbindung verwendet, um Windows Update nach verfügbaren Updates zu suchen.<br /><br />Wenn diese Option aktiviert ist, können lokale Administratoren mithilfe der Windows Update-Systemsteuerung eine Konfigurationsoption Ihrer Wahl auswählen. Lokale Administratoren können die Konfiguration für automatische Updates jedoch nicht deaktivieren.<br /><br />-   **2: zum Herunterladen Benachrichtigen und zur Installation benachrichtigen**<br />    Wenn Windows Update Updates findet, die für den Computer gelten, werden Benutzer darüber informiert, dass Updates zum Download bereit sind. Benutzer können dann Windows Update ausführen, um alle verfügbaren Updates herunterzuladen und zu installieren.<br />-   **3-automatische Download-und Benachrichtigungs Installation** (Standardeinstellung)<br />    Windows Update findet anwendbare Updates und lädt Sie im Hintergrund herunter. der Benutzer wird während des Vorgangs nicht benachrichtigt oder unterbrochen. Wenn die Downloads abgeschlossen sind, werden Benutzer benachrichtigt, dass Updates zur Installation bereit sind. Benutzer können dann Windows Update ausführen, um die heruntergeladenen Updates zu installieren.<br />-   **4: Automatisches herunterladen und Planen der Installation**<br />    Sie können den Zeitplan mit den Optionen in dieser Gruppenrichtlinie Einstellung angeben. Wenn kein Zeitplan angegeben ist, wird der Standard Zeitplan für alle Installationen jeden Tag um 3:00 Uhr Wenn für Updates ein Neustart erforderlich ist, um die Installation abzuschließen, startet Windows den Computer automatisch neu. (wenn ein Benutzer beim Computer angemeldet ist, wenn Windows neu gestartet werden kann, wird der Benutzer benachrichtigt und erhält die Möglichkeit, den Neustart zu verzögern.) **Hinweis:** ab Windows 8 können Sie Updates festlegen, die während der automatischen Wartung installiert werden sollen, anstatt einen bestimmten Zeitplan zu verwenden, der an Windows Update gebunden ist. Bei der automatischen Wartung werden Updates installiert, wenn der Computer nicht verwendet wird, und es wird vermieden, dass Updates installiert werden, wenn der Computer im Akku Betrieb ausgeführt wird. Wenn die automatische Wartung Updates nicht innerhalb von Tagen installieren kann, werden Windows Update Updates sofort installieren. Benutzer werden dann über einen ausstehenden Neustart benachrichtigt. Ein ausstehender Neustart wird nur durchgeführt, wenn es kein Potenzial für versehentliche Datenverluste gibt.    Sie können Zeit Plan Optionen in den GPME-Wartungsplaner-Einstellungen angeben, die sich im Pfad, *PolicyName* > **Computer Configuration** > **Richtlinien** > **Administrative Vorlagen** >  **befinden. Windows-Komponenten** > **Wartungsplaner**1**Automatische Wartung Aktivierungs Grenze**. Weitere Informationen finden Sie im Abschnitt dieses Verweises: [Einstellungen für Wartungsplaner](#computer-configuration--maintenance-scheduler-policy-settings)zum Festlegen von Details.    **5: lokalen Administrator die Wahl der Einstellung gestatten**<br />: Hiermit wird angegeben, ob lokale Administratoren die automatische Updates Systemsteuerung verwenden dürfen, um eine Konfigurationsoption Ihrer Wahl auszuwählen, z. b. ob lokale Administratoren eine geplante Installationszeit auswählen können.<br />    Lokale Administratoren dürfen die Konfiguration für automatische Updates nicht deaktivieren.|
|**Deaktiviert**|Gibt an, dass alle Client Updates, die über den öffentlichen Windows Update-Dienst verfügbar sind, manuell aus dem Internet heruntergeladen und installiert werden müssen.|

#### <a name="delay-restart-for-scheduled-installations"></a>Verzögerter Neustart für geplante Installationen
Gibt die Zeitspanne an, die automatische Updates warten soll, bis mit einem geplanten Neustart fortgefahren wird.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn automatische Updates für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass nach der Installation von Updates die Standard Wartezeit von 15 Minuten abläuft, bevor ein geplanter Neustart stattfindet.|
|**Enabled**|Gibt an, dass nach Abschluss der Installation ein geplanter Neustart erfolgt, nachdem die angegebene Anzahl von Minuten abgelaufen ist.|
|**Deaktiviert**|Gibt an, dass nach der Installation von Updates die Standard Wartezeit von 15 Minuten abläuft, bevor ein geplanter Neustart stattfindet.|

**Optionen:** wenn diese Einstellung aktiviert ist, können Sie mit dieser Option angeben, wie lange (in Minuten) automatische Updates warten soll, bis mit einem geplanten Neustart fortgefahren wird.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog"></a>Standardoption zum Installieren von Updates und Herunterfahren im Dialogfeld "Windows Herunterfahren" nicht anpassen
Mit dieser Richtlinien Einstellung können Sie angeben, ob die Option **Updates installieren und herunter** fahren als Standardoption im Dialogfeld **Windows herunter** fahren zulässig ist.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Diese Richtlinien Einstellung hat keine Auswirkung, wenn die Richtlinien *Name* > -**Computerkonfiguration** > -**Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**@no_ in _T-11 wird die**Option "Updates installieren und Herunterfahren" in der Einstellung Windows-Dialogfeld "Herunterfahren" nicht angezeigt** .

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass das **Installieren von Updates und das herunter** fahren die Standardoption im Dialogfeld **Windows herunter** fahren ist, wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|
|**Enabled**|Wenn Sie diese Richtlinien Einstellung aktivieren, ist die Option letztes Herunterfahren des Benutzers (z. b. Ruhezustand oder Neustart) die Standardoption im Dialogfeld **Windows herunter** fahren, unabhängig davon, ob die Option **Updates installieren und herunter** fahren verfügbar ist. **Was soll der Computer tun?** stehen.|
|**Deaktiviert**|Gibt an, dass das **Installieren von Updates und das herunter** fahren die Standardoption im Dialogfeld **Windows herunter** fahren ist, wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="do-not-connect-to-any-windows-update-internet-locations"></a>Keine Verbindungen mit Windows Update-Internetadressen herstellen
Auch wenn Windows Update so konfiguriert ist, dass Updates von einem Intranet-Aktualisierungs Dienst empfangen werden, werden in regelmäßigen Abständen Informationen aus dem öffentlichen Windows Update-Dienst abgerufen, um zukünftige Verbindungen mit Windows Update und anderen Diensten wie Microsoft Update zu ermöglichen. oder Microsoft Store.

Wenn Sie diese Richtlinie aktivieren, werden die Funktionen für das regelmäßige Abrufen von Informationen aus dem öffentlichen Windows Server Update-Dienst deaktiviert, und es kann dazu führen, dass die Verbindung mit öffentlichen Diensten wie Microsoft Store nicht mehr funktioniert.

|Unterstützt für:|EU|
|---------|-------|
|ab Windows Server 2012 R2, Windows 8.1 oder Windows RT 8,1 werden die Windows-Betriebssysteme, die weiterhin in Ihren Microsoft-Produkten sind, den [Lebenszyklus unterstützen](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn der Computer für die Verbindung mit einem Intranet-Aktualisierungs Dienst konfiguriert ist, indem Sie die Richtlinien Einstellung "Intranet-Microsoft-Update Dienst angeben" verwenden.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Das Standardverhalten zum Abrufen von Informationen aus dem öffentlichen Windows Server Update-Dienst bleibt bestehen.|
|**Enabled**|Gibt an, dass Computer keine Informationen aus dem öffentlichen Windows Server Update-Dienst abrufen.|
|**Deaktiviert**|Das Standardverhalten zum Abrufen von Informationen aus dem öffentlichen Windows Server Update-Dienst bleibt bestehen.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog"></a>Option "Updates installieren und Herunterfahren" im Dialogfeld "Windows Herunterfahren" nicht anzeigen
Gibt an, ob die Option **Updates installieren und herunter** fahren im Dialogfeld **Windows herunter** fahren angezeigt wird.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass die Option **Updates installieren und herunter** fahren im Dialogfeld **Windows herunter** fahren verfügbar ist, wenn Updates verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren. Ein lokaler Administrator kann diese Einstellung mithilfe der lokalen Richtlinie ändern.|
|**Enabled**|Gibt an, dass Updates **Installieren und herunter** fahren im Dialogfeld **Windows herunter** fahren nicht als Auswahl angezeigt werden, auch wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option Herunterfahren zum Herunterfahren des Computers auswählt.|
|**Deaktiviert**|Gibt an, dass die Option **Updates installieren und herunter** fahren die Standardoption im Dialogfeld **Windows herunter** fahren ist, wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="enable-client-side-targeting"></a>Clientseitige Zielzuordnung aktivieren
Gibt die Namen der Zielgruppen an, die in der WSUS-Konsole konfiguriert werden, die Updates von WSUS empfangen sollen.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Windows RT|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn dieser Computer für die Unterstützung der angegebenen Zielgruppen Namen in WSUS konfiguriert ist. Wenn der Name der Zielgruppe in WSUS nicht vorhanden ist, wird er ignoriert, bis er erstellt wird. Wenn die Richtlinien Einstellung "Intranetspeicherort für den Microsoft-Update Dienst angeben" deaktiviert oder nicht konfiguriert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie wird in Windows RT nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass keine zielgruppeninformationen an WSUS gesendet werden. Ein lokaler Administrator kann diese Einstellung mithilfe einer lokalen Richtlinie ändern.|
|**Enabled**|Gibt an, dass die angegebenen zielgruppeninformationen an WSUS gesendet werden, um zu bestimmen, welche Updates auf diesem Computer bereitgestellt werden sollen. Wenn WSUS mehrere Zielgruppen unterstützt, können Sie diese Richtlinie verwenden, um mehrere Gruppennamen anzugeben, die durch Semikolons getrennt sind, wenn Sie die Zielgruppen Namen in der Computer Gruppenliste in WSUS hinzugefügt haben. Andernfalls muss eine einzelne Gruppe angegeben werden.|
|**Deaktiviert**|Gibt an, dass keine zielgruppeninformationen an WSUS gesendet werden.|

**Optionen:** Verwenden Sie diesen Bereich, um einen oder mehrere Zielgruppen Namen anzugeben.

#### <a name="enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates"></a>Aktivieren der Windows Update Energie Verwaltung zum automatischen Reaktivieren des Computers zur Installation geplanter Updates
Gibt an, ob Windows Update die Funktionen der Windows-Energie Verwaltung oder der Energieoptionen verwendet, um den Computer automatisch aus dem Ruhezustand zu reaktivieren, wenn Updates für die Installation geplant sind.

Der Computer wird nur dann automatisch aktiviert, wenn Windows Update für die automatische Installation von Updates konfiguriert ist. Wenn sich der Computer im Ruhezustand befindet, wenn die geplante Installation stattfindet und Updates angewendet werden müssen, werden Windows Update die Windows-Energie Verwaltungs-oder Energie Options Features verwenden, um den Computer für die Installation der Updates automatisch zu aktivieren. Windows Update wird den Computer auch aktivieren und ein Update installieren, wenn ein Installations Stichtag auftritt.

Der Computer wird nur aktiviert, wenn Updates installiert werden müssen. Wenn sich der Computer im Akku Betrieb befindet, werden bei der Aktivierung Windows Update keine Updates installiert, und der Computer wird innerhalb von zwei Minuten automatisch in den Ruhezustand zurückversetzt.

|Unterstützt für:|EU|
|---------|-------|
|ab Windows Vista und Windows Server 2008 (Windows 7) unterstützen Windows-Betriebssysteme, die weiterhin in Ihren Microsoft-Produkten sind, den [Lebenszyklus](https://support.microsoft.com/gp/lifeselect).|Null|

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Windows Update aktiviert den Computer nicht aus dem Ruhezustand, um Updates zu installieren. Ein lokaler Administrator kann diese Einstellung mithilfe einer lokalen Richtlinie ändern.|
|**Enabled**|Windows Update aktiviert den Computer aus dem Ruhezustand, um Updates unter den zuvor aufgeführten Bedingungen zu installieren.|
|**Deaktiviert**|Windows Update aktiviert den Computer nicht aus dem Ruhezustand, um Updates zu installieren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations"></a>Keinen automatischen Neustart für geplante Installationen automatischer Updates durchführen, wenn Benutzer angemeldet sind
Gibt an, dass automatische Updates zum Durchführen einer geplanten Installation darauf wartet, dass der Computer von einem angemeldeten Benutzer neu gestartet wird, anstatt dass der Computer automatisch neu gestartet wird.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn automatische Updates für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass automatische Updates den Benutzer darüber informiert, dass der Computer in fünf Minuten automatisch neu gestartet wird, um die Installation abzuschließen.|
|**Enabled**|Einige Updates erfordern, dass der Computer neu gestartet wird, bevor die Aktualisierungen wirksam werden. Wenn der Status auf Aktiviert festgelegt ist, startet automatische Updates einen Computer während einer geplanten Installation nicht automatisch neu, wenn ein Benutzer am Computer angemeldet ist. Stattdessen wird der Benutzer von Automatische Updates benachrichtigt, den Computer neu zu starten.|
|**Deaktiviert**|Gibt an, dass automatische Updates den Benutzer darüber informiert, dass der Computer in fünf Minuten automatisch neu gestartet wird, um die Installation abzuschließen.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="re-prompt-for-restart-with-scheduled-installations"></a>Erneut zu einem Neustart für geplante Installationen auffordern
Gibt die Zeitspanne an, die automatische Updates gewartet werden soll, bevor erneut eine Aufforderung mit einem geplanten Neustart angezeigt wird.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Windows RT|

> [!IMPORTANT]
> Diese Richtlinie gilt nur, wenn automatische Updates für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie hat keine Auswirkungen auf Computer, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Ein geplanter Neustart erfolgt zehn Minuten, nachdem die Aufforderung zum Neustart der Nachricht verworfen wurde. Ein lokaler Administrator kann diese Einstellung mithilfe einer lokalen Richtlinie ändern.|
|**Enabled**|Gibt an, dass nach dem Verschieben der vorherigen Aufforderung zum Neustart ein geplanter Neustart erfolgt, nachdem die angegebene Anzahl von Minuten abgelaufen ist.|
|**Deaktiviert**|Ein geplanter Neustart erfolgt zehn Minuten, nachdem die Aufforderung zum Neustart der Nachricht verworfen wurde.|

**Optionen:** Wenn diese Einstellung aktiviert ist, können Sie mit dieser Einstellungs Option (in Minuten) den Zeitraum angeben, nach dem die Benutzer erneut zu einem geplanten Neustart aufgefordert werden.

#### <a name="reschedule-automatic-updates-scheduled-installations"></a>Geplante Installationen automatischer Updates erneut planen
Gibt die Zeitspanne an, für die automatische Updates nach dem Starten des Computers gewartet werden soll, bevor Sie mit einer geplanten Installation fortfahren, die zuvor ausgelassen wurde.

Wenn der Status auf **nicht konfiguriert**festgelegt ist, wird eine verpasste geplante Installation eine Minute nach dem nächsten Starten des Computers ausgeführt.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Diese Richtlinie gilt nur, wenn automatische Updates für die Ausführung geplanter Installationen von Updates konfiguriert ist. Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass eine verpasste geplante Installation eine Minute nach dem nächsten Start des Computers stattfindet.|
|**Enabled**|Gibt an, dass eine geplante Installation, die nicht früher erfolgt ist, die angegebene Anzahl von Minuten nach dem nächsten Start des Computers findet.|
|**Deaktiviert**|Gibt an, dass bei der nächsten geplanten Installation eine verpasste geplante Installation nicht ausgeführt wird.|

**Optionen:** Wenn diese Richtlinien Einstellung aktiviert ist, können Sie Sie dazu verwenden, eine Anzahl von Minuten nach dem nächsten Start des Computers anzugeben, dass eine geplante Installation stattfindet.

#### <a name="specify-intranet-microsoft-update-service-location"></a>Intranetspeicherort für Microsoft Update Dienst angeben
Gibt einen alternativen Intranetserver zum Hosten von Updates von Microsoft Update an. Anschließend können Sie WSUS verwenden, um Computer in Ihrem Netzwerk automatisch zu aktualisieren.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Windows RT.|

Diese Einstellung ermöglicht es Ihnen, einen WSUS-Server in Ihrem Netzwerk anzugeben, der als interner Aktualisierungs Dienst fungieren soll. Anstatt Microsoft-Updates im Internet zu verwenden, durchsuchen WSUS-Clients diesen Dienst nach Updates, die angewendet werden.

Um diese Einstellung verwenden zu können, müssen Sie zwei Servernamen Werte festlegen: den Server, von dem der Client Updates erkennt und herunterlädt, und der Server, auf dem die Arbeitsstationen aktualisierte Arbeitsstationen hochladen. Die Werte müssen nicht anders sein, wenn beide Dienste auf demselben Server konfiguriert sind.

> [!NOTE]
> Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert ist, hat diese Richtlinie keine Auswirkungen.

> [!NOTE]
> Diese Richtlinie wird in Windows RT nicht unterstützt. Die Aktivierung dieser Richtlinie wirkt sich nicht auf Computer aus, auf denen Windows RT ausgeführt wird.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Wenn automatische Updates nicht durch die Richtlinie oder die Benutzereinstellung deaktiviert ist, gibt diese Richtlinie an, dass Clients eine direkte Verbindung mit dem Windows Update Standort im Internet herstellen.|
|**Enabled**|Gibt an, dass der Client eine Verbindung mit dem angegebenen WSUS-Server herstellt, statt Windows Update, um nach Updates zu suchen und diese herunterzuladen. Wenn Sie diese Einstellung aktivieren, müssen Endbenutzer in Ihrer Organisation keine Firewall durchlaufen, um Updates zu erhalten, und Sie haben die Möglichkeit, Updates vor deren Bereitstellung zu testen.|
|**Deaktiviert**|Wenn automatische Updates nicht durch die Richtlinie oder die Benutzereinstellung deaktiviert ist, gibt diese Richtlinie an, dass Clients eine direkte Verbindung mit dem Windows Update Standort im Internet herstellen.|

**Optionen:** Wenn diese Richtlinien Einstellung aktiviert ist, müssen Sie den Intranetupdatedienst angeben, den WSUS-Clients beim Erkennen von Updates verwenden werden, und den Internet Statistikserver, auf dem aktualisierte WSUS-Clients Statistiken hochladen. Beispielwerte:


|                    Einstellungs Option:                    |    Beispiel Wert:    |
|-------------------------------------------------------|----------------------|
| Einrichten des intranetaktualisierungs Dienstanbieter |  http://wsus01:8530  |
|          Festlegen des intranetstatistik-Servers           | http://IntranetUpd01 |

#### <a name="turn-on-recommended-updates-via-automatic-updates"></a>Empfohlene Updates über automatische Updates aktivieren
Gibt an, ob automatische Updates wichtige und empfohlene Updates von WSUS bereitstellt.

|Unterstützt für:|EU|
|---------|-------|
|ab Windows Vista unterstützen Windows-Betriebssysteme, die weiterhin in Ihren Microsoft-Produkten arbeiten, den [Lebenszyklus](https://support.microsoft.com/gp/lifeselect).|Null|

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass automatische Updates weiterhin wichtige Updates bereitstellt, sofern diese bereits konfiguriert sind.|
|**Enabled**|Gibt an, dass von Automatische Updates Empfohlene Updates und wichtige Updates von WSUS installiert werden.|
|**Deaktiviert**|Gibt an, dass automatische Updates weiterhin wichtige Updates bereitstellt, sofern diese bereits konfiguriert sind.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="turn-on-software-notifications"></a>Software Benachrichtigungen aktivieren
Mit dieser Richtlinien Einstellung können Sie steuern, ob Benutzern ausführliche erweiterte Benachrichtigungs Meldungen über die von der Microsoft Update-Dienst vorgestellte Software angezeigt werden. Erweiterte Benachrichtigungs Meldungen vermitteln den Wert und Stufen die Installation und Verwendung optionaler Software herauf. Diese Richtlinien Einstellung ist für die Verwendung in Lose verwalteten Umgebungen vorgesehen, in denen der Endbenutzer Zugriff auf den Microsoft Update-Dienst hat.

Wenn Sie den Microsoft Update-Dienst nicht verwenden, hat die Richtlinien Einstellung "Software Benachrichtigungen" keine Auswirkung.

Wenn die Richtlinien Einstellung "configure automatische Updates" deaktiviert oder nicht konfiguriert ist, hat die Richtlinien Einstellung "Software Benachrichtigungen" keine Auswirkung.

|Unterstützt für:|EU|
|---------|-------|
|ab Windows Server 2008 (Windows Vista) und Windows 7 unterstützen Windows-Betriebssysteme, die weiterhin in Ihren Microsoft-Produkten arbeiten, den [Lebenszyklus](https://support.microsoft.com/gp/lifeselect).|Null|

> [!NOTE]
> Diese Richtlinieneinstellung ist standardmäßig deaktiviert.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Benutzern auf Computern, auf denen Windows 7 ausgeführt wird, werden keine Nachrichten für optionale Anwendungen angeboten. Benutzern auf Computern, auf denen Windows Vista ausgeführt wird, werden keine Nachrichten für optionale Anwendungen oder Updates angeboten. Ein lokaler Administrator kann diese Einstellung über die Systemsteuerung oder eine lokale Richtlinie ändern.|
|**Enabled**|Wenn Sie diese Richtlinien Einstellung aktivieren, wird eine Benachrichtigungs Meldung auf dem Computer des Benutzers angezeigt, wenn eine verfügbare Software verfügbar ist. Der Benutzer kann auf die Benachrichtigung klicken, um Windows Update zu öffnen und weitere Informationen zur Software zu erhalten oder zu installieren. Der Benutzer kann auch auf **Diese Meldung schließen** oder **später anzeigen** klicken, um die Benachrichtigung nach Bedarf zu verschieben.<br /><br />In Windows 7 werden von dieser Richtlinien Einstellung nur detaillierte Benachrichtigungen für optionale Anwendungen gesteuert. In Windows Vista steuert diese Richtlinien Einstellung detaillierte Benachrichtigungen für optionale Anwendungen und Updates.|
|**Deaktiviert**|Gibt an, dass Benutzern mit Windows 7 keine detaillierten Benachrichtigungs Meldungen für optionale Anwendungen angeboten werden und Benutzern, die Windows Vista ausführen, keine detaillierten Benachrichtigungs Meldungen zu optionalen Anwendungen oder optionalen Updates angeboten werden.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

### <a name="computer-configuration--maintenance-scheduler-policy-settings"></a>Richtlinien Einstellungen für die Computer Konfiguration > Wartungsplaner
In der Einstellung Automatische Updates konfigurieren haben Sie die Option **4-Automatisches herunterladen und Planen der Installation**ausgewählt. Sie können die Einstellungen für Wartungsplaner planen in der GPMC für Computer unter Windows 8 und Windows RT angeben. Wenn Sie in der Einstellung "configure automatische Updates" Option 4 nicht ausgewählt haben, müssen Sie diese Einstellungen nicht für automatische Updates konfigurieren. Die Wartungsplaner-Einstellungen befinden sich im folgenden Pfad: *PolicyName* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Wartungsplaner**. Die wartungsplanererweiterung von Gruppenrichtlinie enthält die folgenden Einstellungen:

-   [Aktivierungs Grenze für automatische Wartung](#automatic-maintenance-activation-boundary)

-   [Zufällige Verzögerung für automatische Wartung](#automatic-maintenance-random-delay)

-   [Automatische Aktivierungs Richtlinie](#automatic-wakeup-policy)

#### <a name="automatic-maintenance-activation-boundary"></a>Aktivierungsgrenze für automatische Wartung
Mit dieser Richtlinie können Sie die Einstellung "automatische Wartung der Aktivierungs Grenze" konfigurieren.

Die Wartungs Aktivierungs Grenze ist die tägliche geplante Zeit, zu der die automatische Wartung gestartet wird.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Diese Einstellung bezieht sich auf Option 4 in **configure automatische Updates**. Wenn Sie in **configure automatische Updates**nicht die Option 4 ausgewählt haben, ist es nicht erforderlich, diese Einstellung zu konfigurieren.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Wenn diese Richtlinien Einstellung nicht konfiguriert ist, wird die tägliche geplante Zeit, die auf Client Computern in der Systemsteuerung "**Wartungs** **Center** > " angegeben ist, angewendet.|
|**Enabled**|Wenn Sie diese Richtlinien Einstellung aktivieren, werden alle Standardeinstellungen oder geänderten Einstellungen außer Kraft gesetzt, die auf Client Computern in der **Systemsteuerung** > -**Aktions Center** > -**Automatische Wartung** (oder in einigen Client Versionen und **Wartung**) konfiguriert sind.|
|**Deaktiviert**|Wenn Sie diese Richtlinien Einstellung auf **deaktiviert**festlegen, wird die tägliche geplante Zeit, die im Wartungs **Center** > **Automatische Wartung**angegeben ist, in der Systemsteuerung angewendet.|

#### <a name="automatic-maintenance-random-delay"></a>Zufällige Verzögerung für automatische Wartung
Mit dieser Richtlinien Einstellung können Sie die zufällige Verzögerung für die automatische Wartung konfigurieren.

Die zufällige Verzögerung für die Wartung ist die Zeitspanne, bis zu der die automatische Wartung ab der Aktivierungs Grenze verzögert wird. Diese Einstellung ist nützlich für virtuelle Computer, bei denen eine zufällige Wartung eine Leistungsanforderung sein könnte.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Diese Einstellung bezieht sich auf Option 4 in **configure automatische Updates**. Wenn Sie in **configure automatische Updates**nicht die Option 4 ausgewählt haben, ist es nicht erforderlich, diese Einstellung zu konfigurieren.

Wenn diese Einstellung aktiviert ist, wird die zufällige Verzögerung für die reguläre Wartung auf **PT4H**festgelegt.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Eine 4-stündige zufällige Verzögerung wird auf **automatisch**angewendet.|
|**Enabled**|Die automatische Wartung wird von der Aktivierungs Grenze bis zum angegebenen Zeitraum verzögert.|
|**Deaktiviert**|Es wird keine zufällige Verzögerung auf die automatische Wartung angewendet.|

#### <a name="automatic-wakeup-policy"></a>Automatische Aktivierungs Richtlinie
Mit dieser Richtlinien Einstellung können Sie die Aktivierungs Richtlinie für die automatische Wartung konfigurieren.

Die Aktivierungs Richtlinie für die Wartung gibt an, ob die automatische Wartung eine Reaktivierungs Anforderung an den Betriebs Computer für die tägliche geplante Wartung durchführen soll.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Wenn die Energie Aktivierungs Richtlinie des Betriebs Computers explizit deaktiviert ist, hat diese Einstellung keine Auswirkungen.

> [!NOTE]
> Diese Einstellung bezieht sich auf Option 4 in **configure automatische Updates**. Wenn Sie in **configure automatische Updates**nicht die Option 4 ausgewählt haben, ist es nicht erforderlich, diese Einstellung zu konfigurieren.

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Wenn Sie diese Richtlinien Einstellung nicht konfigurieren, wird die in der Systemsteuerung "**Wartungs** **Center** > " angegebene Reaktivierungs Einstellung angewendet.|
|**Enabled**|Wenn Sie diese Richtlinien Einstellung aktivieren, versucht die automatische Wartung, eine Aktivierungs Richtlinie für das Betriebssystem festzulegen und ggf. eine Aktivierungs Anforderung für die tägliche geplante Zeit vorzunehmen.|
|**Deaktiviert**|Wenn Sie diese Richtlinien Einstellung deaktivieren, wird die in der Systemsteuerung "**Wartungs** **Center** > " angegebene Reaktivierungs Einstellung angewendet.|

### <a name="user-configuration--windows-update-policy-settings"></a>Richtlinien Einstellungen für die Benutzerkonfiguration > Windows Update
Dieser Abschnitt enthält Details zu den folgenden benutzerbasierten Richtlinien Einstellungen:

-   [Option "Updates installieren und Herunterfahren" im Dialogfeld "Fenster Herunterfahren" nicht anzeigen](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Passen Sie die Standardoption "Updates installieren und Herunterfahren" im Dialogfeld "Fenster Herunterfahren" nicht an.](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [Entfernen Sie den Zugriff, um alle Windows Update Features zu verwenden.](#remove-access-to-use-all-windows-update-features)

In der GPMC befinden sich die Benutzereinstellungen für automatische Computer Updates im folgenden Pfad: *PolicyName* > -**Benutzerkonfiguration** > -**Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**. Die Einstellungen werden in der Reihenfolge aufgelistet, in der Sie in den Erweiterungen Computerkonfiguration und Benutzerkonfiguration in Gruppenrichtlinie angezeigt werden, wenn die Registerkarte **Einstellungen** der Windows Update Richtlinie ausgewählt ist, um die Einstellungen alphabetisch zu sortieren.

> [!NOTE]
> Standardmäßig sind diese Einstellungen nicht konfiguriert, sofern nichts anderes angegeben ist.

> [!TIP]
> für jede dieser Einstellungen können Sie die folgenden Schritte ausführen, um die Einstellungen zu aktivieren, zu deaktivieren oder zwischen Ihnen zu navigieren:

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog-box"></a>Option "Updates installieren und Herunterfahren" im Dialogfeld "Fenster Herunterfahren" nicht anzeigen
Gibt an, ob die Option **Updates installieren und herunter** fahren im Dialogfeld **Windows herunter** fahren angezeigt wird.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, dass die Option **Updates installieren und herunter** fahren im Dialogfeld **Windows herunter** fahren angezeigt wird, wenn Updates verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|
|**Enabled**|Wenn Sie diese Richtlinien Einstellung aktivieren, werden **Updates installieren und herunter** fahren nicht als Auswahl im Dialogfeld **Windows herunter** fahren angezeigt, auch wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|
|**Deaktiviert**|Gibt an, dass die Option **Updates installieren und herunter** fahren im Dialogfeld **Windows herunter** fahren angezeigt wird, wenn Updates verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog-box"></a>Passen Sie die Standardoption "Updates installieren und Herunterfahren" im Dialogfeld "Fenster Herunterfahren" nicht an.
Gibt an, ob die Option **Updates installieren und herunter** fahren als Standardoption im Dialogfeld **Windows herunter** fahren zulässig ist.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

> [!NOTE]
> Diese Richtlinien Einstellung hat keine Auswirkung, wenn die Richtlinien *Name* > -Richtlinien für die**Benutzerkonfiguration** > -**Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**@no__ in t-11 wird die**Option "Updates installieren und Herunterfahren" im Dialogfeld "Windows Herunterfahren" nicht angezeigt** .

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Gibt an, ob die Option **Updates installieren und herunter** fahren die Standardoption im Dialogfeld **Windows herunter** fahren ist, wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|
|**Enabled**|Gibt an, ob die letzte Option zum Herunterfahren des Benutzers (z. b. Ruhezustand oder Neustart) die Standardoption im Dialogfeld **Windows herunter** fahren ist, unabhängig davon, ob die **Option Updates installieren und herunter** fahren in **der möchten Sie den Computer ausführen?** stehen.|
|**Deaktiviert**|Gibt an, ob die Option **Updates installieren und herunter** fahren die Standardoption im Dialogfeld **Windows herunter** fahren ist, wenn Updates für die Installation verfügbar sind, wenn der Benutzer die Option Herunterfahren auswählt, um den Computer herunterzufahren.|

**Optionen:** Es gibt keine Optionen für diese Einstellung.

#### <a name="remove-access-to-use-all-windows-update-features"></a>Zugriff auf alle Windows Update-Funktionen entfernen
Mit dieser Einstellung können Sie den WSUS-Client Zugriff auf Windows Update entfernen.

|Unterstützt für:|EU|
|---------|-------|
|Windows-Betriebssysteme, die noch nicht in Ihren Microsoft-Produkten sind, [unterstützen Lebenszyklus](https://support.microsoft.com/gp/lifeselect)|Null|

|||
|-|-|
|**Status der Richtlinien Einstellung**|**Verhalten**|
|**Nicht konfiguriert**|Benutzer können eine Verbindung mit der Windows Update-Website herstellen.|
|**Enabled**|**Wichtig:** wenn enable, werden alle Windows Update Features entfernt. Dies umfasst das Blockieren des Zugriffs auf die Windows Update Website auf https://windowsupdate.microsoft.com, über den Windows Update Hyperlink im Startmenü oder auf dem Startbildschirm und auch über **das Menü Extras** in Internet Explorer. Die automatische Windows-Aktualisierung ist ebenfalls deaktiviert. der Benutzer wird weder benachrichtigt, noch werden wichtige Updates von Windows Update empfangen. Mit dieser Einstellung wird auch verhindert, dass Treiber Updates von der Windows Update Website automatisch von Geräte-Manager installiert werden.<br /><br />Wenn diese Option aktiviert ist, können Sie eine der folgenden Benachrichtigungs Optionen konfigurieren:<br /><br />-   **0-keine Benachrichtigungen anzeigen**<br />    Mit dieser Einstellung wird der gesamte Zugriff auf Windows Update Features entfernt, und es werden keine Benachrichtigungen angezeigt.<br />-   **1-Benachrichtigungen für Neustart erforderlich anzeigen**<br />    Diese Einstellung zeigt Benachrichtigungen zu Neustarts an, die zum Abschluss einer-Installation erforderlich sind. **Hinweis**: Wenn diese Richtlinie aktiviert ist, werden auf Computern, auf denen Windows 8 und Windows RT ausgeführt wird, nur Benachrichtigungen zu Neustarts und zum Erkennen von Aktualisierungen nicht angezeigt. Die Benachrichtigungs Optionen werden nicht unterstützt. Benachrichtigungen auf dem Anmeldebildschirm werden immer angezeigt.|
|**Deaktiviert**|Benutzer können eine Verbindung mit der Windows Update-Website herstellen.|

**Optionen:** Weitere **Informationen finden Sie** in der Tabelle für diese Einstellung.

## <a name="supplemental-information"></a>Zusätzliche Informationen
In diesem Abschnitt finden Sie zusätzliche Informationen zum Öffnen und Speichern von WSUS-Einstellungen in Gruppenrichtlinien sowie Definitionen für Begriffe, die in diesem Handbuch verwendet werden. Für Administratoren, die mit früheren Versionen von WSUS (WSUS 3,2 und früheren Versionen) vertraut sind, gibt es eine Tabelle, in der die Unterschiede zwischen WSUS-Versionen kurz zusammengefasst werden.

### <a name="accessing-the-windows-update-settings-in-group-policy"></a>Zugreifen auf die Windows Update Einstellungen in Gruppenrichtlinie
In der folgenden Vorgehensweise wird beschrieben, wie Sie die GPMC auf Ihrem Domänen Controller öffnen. Anschließend wird beschrieben, wie Sie entweder ein vorhandenes GPO (Domain-Level Gruppenrichtlinie Object) für die Bearbeitung öffnen oder ein neues GPO auf Domänen Ebene erstellen und zum Bearbeiten öffnen.

> [!NOTE]
> Sie müssen Mitglied der Gruppe " **Domänen-Admins** " oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

##### <a name="to-open-or-add-and-open-a-group-policy-object"></a>So öffnen oder öffnen Sie ein Gruppenrichtlinie Objekt und öffnen es

1.  Wechseln Sie auf Ihrem Domänen Controller zu **Server-Manager**, > **Tools**, > **Gruppenrichtlinie Verwaltung**. Der Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.

2.  Erweitern Sie im linken Bereich die Gesamtstruktur. Doppelklicken Sie z. b. auf **Forest: example.com**.

3.  Doppelklicken Sie im linken Bereich auf **Domänen**, und doppelklicken Sie dann auf die Domäne, für die Sie ein Gruppenrichtlinie Objekt verwalten möchten. Beispiel: Doppelklicken Sie auf **example.com**.

4.  Führen Sie eines der folgenden Verfahren aus:

    -  **Um ein vorhandenes Gruppenrichtlinien Objekt auf Domänen Ebene für die Bearbeitung zu öffnen**, doppelklicken Sie auf die Domäne mit dem Gruppenrichtlinie Objekt, das Sie verwalten möchten, klicken Sie mit der rechten Maustaste auf die zu verwaltende Domänen Richtlinie, und klicken Sie dann auf **Bearbeiten**. Gruppenrichtlinie Management-Editor (GPME) wird geöffnet.

    -  **So erstellen Sie ein neues Gruppenrichtlinie Objekt und öffnen es zum Bearbeiten**:
        1.  Klicken Sie mit der rechten Maustaste auf die Domäne, für die Sie ein neues Gruppenrichtlinie Objekt erstellen möchten, und klicken Sie dann auf Gruppenrichtlinien Objekt **in dieser Domäne erstellen und verknüpfen**.

        2.  Geben Sie im **neuen GPO**unter **Name**einen Namen für das neue Gruppenrichtlinie Objekt ein, und klicken Sie dann auf **OK**.

        3.  Klicken Sie mit der rechten Maustaste auf das neue Gruppenrichtlinie Objekt, und klicken Sie dann auf **Bearbeiten**. Die GPME wird geöffnet.

##### <a name="to-open-the-windows-update-or-maintenance-scheduler-extensions-of-group-policy"></a>So öffnen Sie die Windows Update-oder Wartungsplaner-Erweiterungen von Gruppenrichtlinie

1.  Führen Sie im Gruppenrichtlinie-Verwaltungs-Editor einen der folgenden Schritte aus:

    -   **Öffnen Sie die Computerkonfiguration > Windows Update Erweiterung von Gruppenrichtlinie**. Navigieren Sie zu: *PolicyName* > **Computerkonfiguration** > -**Richtlinien** / **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**.

    -   **Öffnen Sie die Benutzerkonfiguration > Windows Update Erweiterung von Gruppenrichtlinie**. Navigieren Sie zu: *PolicyName* > -**Benutzerkonfiguration** > -**Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**.

    -   **Öffnen Sie die Computerkonfiguration > Wartungsplaner Erweiterung Gruppenrichtlinie**. Navigieren Sie in GPOE zu *PolicyName* > **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Wartung Scheduler**.

Weitere Informationen zum Gruppenrichtlinie finden Sie unter [Gruppenrichtlinie Übersicht](https://technet.microsoft.com/library/hh831791.aspx(v=ws.12)).

> [!TIP]
> Nachdem Sie die Erweiterung der gewünschten Gruppenrichtlinie geöffnet haben, können Sie die folgenden Schritte ausführen, um die Einstellungen zu aktivieren, zu deaktivieren oder zwischen Ihnen zu navigieren:

##### <a name="to-configure-group-policy-settings"></a>So konfigurieren Sie Gruppenrichtlinieneinstellungen

1.  Doppelklicken Sie unter *extensionofgrouppolicy*auf die Einstellung, die Sie anzeigen oder ändern möchten.

2.  Führen Sie einen der folgenden Schritte aus, um die Einstellung zu konfigurieren:

    -   Wählen Sie **nicht konfiguriert**aus, um den nicht angegebenen Standardzustand der Einstellung beizubehalten.

    -   Wählen Sie **aktiviert**aus, um die Einstellung zu aktivieren.

    -   Wählen Sie **deaktiviert**aus, um die Einstellung zu deaktivieren.

3.  Behalten Sie die Standardwerte unter **Optionen**bei, oder ändern Sie Sie bei Bedarf.

4.  Führen Sie eines der folgenden Verfahren aus:

    -   Um die Änderungen zu speichern und mit der nächsten Einstellung fortzufahren, **Klicken Sie auf**übernehmen, und klicken Sie dann auf **nächste Einstellung**.

    -   Um die Änderungen zu speichern und das Dialogfeld zu schließen, klicken Sie auf **OK**.

    -   Um alle nicht gespeicherten Änderungen zu verwerfen und das Dialogfeld zu schließen, klicken Sie auf **Abbrechen**.

### <a name="changes-to-wsus-relevant-to-this-guide"></a>Änderungen an WSUS, die für dieses Handbuch relevant sind
In der folgenden Tabelle werden die wichtigsten Unterschiede zwischen der aktuellen und früheren Version von WSUS zusammengefasst, die für dieses Handbuch relevant sind.

|Windows Server-und WSUS-Versionen|Beschreibung|
|------------------|--------|
| Windows Server 2012 R2 mit WSUS 6,0 und nachfolgende Versionen|ab Windows Server 2012 ist die WSUS-Server Rolle in das Betriebssystem integriert, und die zugehörigen Gruppenrichtlinie Einstellungen für WSUS-Clients sind standardmäßig in Gruppenrichtlinie enthalten.|
| Windows Server 2008 (und frühere Versionen von Windows Server) mit WSUS 3,2 und früher|In Windows Server 2008 (und früheren Versionen von Windows Server), die WSUS-Versionen 3,2 (und früher) verwenden, sind die Gruppenrichtlinie Einstellungen, die die WSUS-Clients Regeln, nicht in diesen Windows Server-Betriebssystemen enthalten. Die Richtlinien Einstellungen befinden sich in der WSUS-verwaltungsvorlage **wuau. adm**. In diesen Serverversionen muss die WSUS-administrative Vorlage zunächst dem Gruppenrichtlinien-Verwaltungskonsole (GPMC) hinzugefügt werden, bevor die WSUS-Client Einstellungen konfiguriert werden können.|

### <a name="terms-and-definitions"></a>Begriffe und Definitionen
Im folgenden finden Sie eine Liste der in diesem Handbuch verwendeten Begriffe.

|Begriff|Definition|
|----|-------|
|Automatische Updates|**Ein Dienst, der auf Windows-Computern** ausgeführt wird (automatische Updates): Bezieht sich auf die Client Computerkomponente, die in die Betriebssysteme Microsoft Windows Vista, Windows Server 2003, Windows XP und Windows 2000 mit SP3 integriert ist, um Updates von Microsoft Update oder Windows Update zu erhalten.<br /><br />**Gelegentliche Referenz** (automatische Updates): Der Begriff, mit dem beschrieben wird, wann Updates vom Windows Update-Agent automatisch geplant und heruntergeladen werden.|
|Autonome Server|Verwenden Sie, um auf einen WSUS-Server (Downstream Windows Server Update Services) zu verweisen, auf dem Administratoren die WSUS-Komponenten verwalten können.|
|Downstream-Server|Verwenden Sie, um auf einen WSUS-Server (Windows Server Update Services) zu verweisen, der Updates von einem anderen WSUS-Server und nicht von Microsoft Update oder Windows Update abruft.|
|Gruppenrichtlinie Erweiterung (und: Erweiterung von Gruppenrichtlinie|Eine Sammlung von Einstellungen in Gruppenrichtlinie, mit denen gesteuert wird, wie Benutzer und Computer (auf die die Richtlinien zutreffen) verschiedene Windows-Dienste und-Features konfigurieren und verwenden können. Administratoren können WSUS mit Gruppenrichtlinie für die Client seitige Konfiguration des automatische Updates Clients verwenden, um sicherzustellen, dass Endbenutzer keine Richtlinien für Unternehmens Updates deaktivieren oder umgehen können.<br /><br />Für WSUS ist die Verwendung von Active Directory oder Gruppenrichtlinie nicht erforderlich. Die Client Konfiguration kann auch über eine lokale Gruppenrichtlinie oder durch Ändern der Windows-Registrierung angewendet werden.|
|Interner Aktualisierungs Dienst|Eine gelegentliche Referenz zu einer Netzwerkinfrastruktur, in der Updates mithilfe eines oder mehrerer WSUS-Server verteilt werden.|
|Replikat Server|Verwenden Sie, um auf einen WSUS-Server (Downstream Windows Server Update Services) zu verweisen, der die Genehmigungen und Einstellungen auf dem Upstreamserver widerspiegelt, mit dem er verbunden ist. Sie können WSUS auf einem Replikat Server nicht verwalten.|
|Microsoft Update|**Eine Internet basierte Microsoft-Download Site:** Eine Microsoft-Internet Site, die Updates für Windows-Computer (Gerätetreiber), Windows-Betriebssysteme und andere Microsoft-Softwareprodukte speichert und verteilt.|
|Software Update Dienste (SUS)|SUS war das Vorgängerprodukt für Windows Server Update Services (WSUS).|
|Aktualisierungen|Eine beliebige Sammlung von Software Revisionen, Hotfixes, Service Packs, Featurepaketen und Gerätetreibern, die auf einem Computer installiert werden können, um die Funktionalität zu erweitern oder die Leistung und Sicherheit zu verbessern.|
|Aktualisieren von Dateien|Die Dateien, die zum Installieren eines Updates auf einem Computer erforderlich sind.|
|Aktualisierungsinformationen (auch als Update Metadaten bezeichnet)|Die Informationen zu einem Update, im Gegensatz zu den Update-Binärdateien in einem Update Paket. Metadaten liefern z. b. Informationen für die Eigenschaften eines Updates, sodass Sie ermitteln können, was das Update nützlich ist. Metadaten enthalten auch die Microsoft-Software-Lizenzbedingungen. Das für ein Update heruntergeladene Metadatenpaket ist in der Regel viel kleiner als das tatsächliche Update Dateipaket.|
|Update Quelle|Der Speicherort, an dem ein WSUS-Server (Windows Server Update Services) synchronisiert wird, um Update Dateien zu erhalten. Dieser Speicherort kann entweder Microsoft Update oder ein WSUS-Upstream-Server sein.|
|Upstreamserver|Ein WSUS-Server (Windows Server Update Services), der Update Dateien für einen anderen WSUS-Server bereitstellt, der wiederum als Downstreamserver bezeichnet wird.|
|Windows Server Update Services (WSUS)|Ein Server rollenprogramm, das auf einem oder mehreren Windows Server-Computern in einem Unternehmensnetzwerk ausgeführt wird. Mithilfe einer WSUS-Infrastruktur können Sie Updates für Computer in Ihrem Netzwerk für die Installation von verwalten.<br /><br />Sie können WSUS verwenden, um Updates vor der Freigabe zu genehmigen oder abzulehnen, um zu erzwingen, dass Updates an einem bestimmten Datum installiert werden, und um umfangreiche Berichte zu den Updates für die einzelnen Computer in Ihrem Netzwerk zu erhalten. Sie können WSUS so konfigurieren, dass bestimmte Klassen von Aktualisierungen automatisch genehmigt werden (wichtige Updates, Sicherheitsupdates, Service Packs, Treiber usw.). Mithilfe von WSUS können Sie auch nur Updates für "Erkennung" genehmigen, damit Sie sehen können, welche Computer ein bestimmtes Update benötigen, ohne dass die Updates installiert werden müssen.<br /><br />Bei einer WSUS-Implementierung muss mindestens ein WSUS-Server im Netzwerk eine Verbindung mit Microsoft Update herstellen können, um verfügbare Updates zu erhalten. Basierend auf der Netzwerksicherheit und-Konfiguration kann der Administrator bestimmen, wie viele andere Server eine direkte Verbindung mit Microsoft Update herstellen.<br /><br />Sie können einen WSUS-Server so konfigurieren, dass über das Internet Updates von folgenden Stellen abgerufen werden:<br /><br />-der öffentliche Microsoft Update<br />-der öffentliche Windows Update<br />-Microsoft Store|
|Windows Update|**Eine Internet basierte Microsoft-Download Site:** Eine Microsoft-Internet Website, auf der Updates für Windows-Computer (Gerätetreiber) und Windows-Betriebssysteme gespeichert und verteilt werden.<br /><br />**Computerdienst:** Der Name des Windows Update Dienstanbieter, der auf Computern ausgeführt wird. Windows Update erkennt, lädt und installiert Updates auf Windows-Computern.<br /><br />Abhängig von Computer-und Richtlinien Konfigurationen können vom Windows Update-Agent Updates heruntergeladen werden von:<br /><br />-Microsoft Update<br />-Windows Update<br />-Microsoft Store<br />-Ein Internet Dienst (Network) Update Service (WSUS)<br /><br />Computer, die nicht in einer WSUS-basierten Umgebung verwaltet werden, verwenden normalerweise Windows Update, um eine direkte Verbindung über das Internet herzustellen Windows Update, Microsoft Update oder Microsoft Store, um Updates zu erhalten.|
|WSUS-Client|Ein Computer, der Updates von einem WSUS-Intranet-Aktualisierungs Dienst empfängt.<br /><br />Im Fall von Gruppenrichtlinie Einstellungen, die die Interaktion von Endbenutzern mit automatische Updates steuern: ein Benutzer eines Computers in einer WSUS-Umgebung.|
