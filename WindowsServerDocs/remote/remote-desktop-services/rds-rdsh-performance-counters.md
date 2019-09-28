---
title: Verwenden von Leistungsindikatoren für die Diagnose von Problemen mit der Reaktionsfähigkeit von Anwendungen auf Remotedesktop-Sitzungshosts
description: Läuft Ihre Anwendung in Remotedesktopsitzungen langsam? Erfahren Sie, wie Sie Leistungsindikatoren für die Diagnose von Leistungsproblemen von Anwendungen auf RDSHs verwenden können
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 07/11/2019
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: b59d93d576967ee83b3efecc2630034eab919bf2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403903"
---
# <a name="use-performance-counters-to-diagnose-app-performance-problems-on-remote-desktop-session-hosts"></a>Verwenden von Leistungsindikatoren für die Diagnose von Leistungsproblemen von Anwendungen auf Remotedesktop-Sitzungshosts

> Gilt für: Windows Server 2019, Windows 10

Eins der schwierigsten Probleme in der Diagnose ist schlechte Anwendungsleistung – die Anwendungen laufen langsam oder reagieren nicht. In herkömmlicher Weise können Sie Ihre Diagnose beginnen, indem Sie Metriken zu CPU, Arbeitsspeicher, Datenträger-E/A und weiteren Punkten sammeln und dann Tools wie den Windows Performance Analyzer verwenden, um die Ursache des Problems zu ermitteln zu versuchen. Leider helfen diese Daten in den meisten Fällen nicht beim Bestimmen der Grundursache, da Indikatoren zum Ressourcenverbrauch viele und große Variationen aufweisen. Dadurch wird es schwierig, die Daten zu lesen und sie mit dem gemeldeten Problem in Beziehung zu setzen. Zur Unterstützung bei der schnellen Lösung von Problemen mit der Anwendungsleistung haben wir einige neue Leistungsindikatoren hinzugefügt (zum [Download](#download-windows-server-insider-software) über das [Windows Insider-Programm](https://insider.windows.com) verfügbar), die den Fluss von Benutzereingaben messen.

>[!NOTE]
>Der Indikator „User Input Delay“ (Benutzereingabeverzögerung) ist nur kompatibel mit:
> - Windows Server 2019 oder höher
> - Windows 10, Version 1809 oder höher

Der Indikator User Input Delay (Benutzereingabeverzögerung) kann Sie dabei unterstützen, schnell die Grundursache für schlechte Endbenutzer-RDP-Erfahrungen zu bestimmen. Dieser Indikator misst, wie lange jede Benutzereingabe (wie etwa Maus- oder Tastaturbetätigungen) in der Warteschlange verbleibt, bevor sie von einem Prozess aufgenommen wird, und der Indikator funktioniert sowohl in lokalen als auch in Remotesitzungen.

Die folgende Abbildung zeigt eine ungefähre Darstellung des Flusses von Benutzereingaben vom Client zur Anwendung.

![Remotedesktop: Fluss von Benutzereingaben vom Remotedesktopclient des Benutzers zur Anwendung](./media/rds-user-input.png)

Der User Input Delay-Indikator misst das maximale Delta (innerhalb eines Zeitintervalls) zwischen der Einstellung der Eingabe in die Warteschlange und ihrer Übernahme durch die Anwendung in einer [herkömmlichen Nachrichtenschleife](https://msdn.microsoft.com/library/windows/desktop/ms644927.aspx#loop), wie im folgenden Diagramm dargestellt:

![Remotedesktop: Fluss im User Input Delay-Leistungsindikator](./media/rds-user-input-delay.png)

Ein wichtiges Detail dieses Indikators besteht darin, dass er die maximale Verzögerung der Benutzereingabe innerhalb eines konfigurierbaren Intervalls meldet. Dies ist der längste Zeitraum, den eine Eingabe zum Erreichen der Anwendung benötigt, der sich auf die Geschwindigkeit wichtiger und sichtbarer Aktionen auswirken kann, z. B. der Eingabe.

Beispielsweise würde in der folgenden Tabelle die Verzögerung der Benutzereingabe innerhalb dieses Intervalls als 1.000 ms gemeldet. Der Indikator meldet die längste Verzögerung der Benutzereingabe im Intervall, da die Wahrnehmung des Benutzers als „langsam“ durch die längste erlebte Eingabezeit (das Maximum) bestimmt wird, nicht durch die mittlere Geschwindigkeit aller Eingaben.

|Number| 0 | 1 | 2 |
|------|---|---|---|
|Verzögerung |16 ms| 20 ms| 1\.000 ms|

## <a name="enable-and-use-the-new-performance-counters"></a>Aktivieren und Verwenden der neuen Leistungsindikatoren

Um diese neuen Leistungsindikatoren zu verwenden, müssen Sie zuerst einen Registrierungsschlüssel aktivieren, indem Sie den folgenden Befehl ausführen:

```
reg add "HKLM\System\CurrentControlSet\Control\Terminal Server" /v "EnableLagCounter" /t REG_DWORD /d 0x1 /f
```

>[!NOTE]
> Wenn Sie Windows 10, Version 1809 oder höher oder Windows Server 2019 oder höher verwenden, brauchen Sie den Registrierungsschlüssel nicht zu aktivieren.

Starten Sie dann den Server neu. Öffnen Sie anschließend den Systemmonitor, und wählen Sie das Pluszeichen (+) aus, wie im folgenden Screenshot dargestellt.

![Remotedesktop: Screenshot, der das Hinzufügen des User Input Delay-Leistungsindikators veranschaulicht](./media/rds-add-user-input-counter-screen.png)

Anschließend sollten Sie das Dialogfeld „Leistungsindikatoren hinzufügen“ sehen, in dem Sie **User Input Delay per Process** (Verzögerung der Benutzereingabe nach Prozess) oder **User Input Delay per Session** (Verzögerung der Benutzereingabe nach Sitzung) auswählen können.

![Remotedesktop: Screenshot, der das Hinzufügen von User Input Delay pro Sitzung veranschaulicht](./media/rds-user-delay-per-session.png)

![Remotedesktop: Screenshot, der das Hinzufügen von User Input Delay pro Prozess veranschaulicht](./media/rds-user-delay-per-process.png)

Wenn Sie **User Input Delay per Process** auswählen, sehen Sie die **Instances of the selected object** (Instanzen des ausgewählten Objekts, also anderes ausgedrückt: die Prozesse) im ```SessionID:ProcessID <Process Image>```-Format.

Wenn beispielsweise die Rechner-App in einer [Sitzung mit ID 1](https://msdn.microsoft.com/library/ms524326.aspx) ausgeführt wird, sehen Sie ```1:4232 <Calculator.exe>```.

> [!NOTE]
> Es werden nicht alle Prozesse dargestellt. Sie sehen keine Prozesse, die als SYSTEM ausgeführt werden.

Der Indikator beginnt sofort nach dem Hinzufügen, die Verzögerung der Benutzereingabe zu melden. Beachten Sie, dass der Maßstab standardmäßig auf ein Maximum von 100 ms festgelegt ist. 

![Remotedesktop: Beispiel für Aktivität für User Input Delay pro Prozess im Systemmonitor](./media/rds-sample-user-input-delay-perfmon.png)

Sehen wir uns als nächstes die **User Input Delay per Session** (Verzögerung der Benutzereingabe pro Sitzung) an. Es gibt Instanzen für jede Sitzungs-ID, und ihre Indikatoren zeigen die Verzögerung der Benutzereingabe jedes Prozesses innerhalb der angegebenen Sitzung. Darüber hinaus gibt es zwei Instanzen mit den Bezeichnungen „Max“ (die maximale Verzögerung der Benutzereingabe über alle Sitzungen) und „Average“ (Durchschnitt; der Durchschnittswert aus allen Sitzungen).

Diese Tabelle zeigt ein visuelles Beispiel dieser Instanzen. (Sie können die gleichen Informationen im Systemmonitor abrufen, indem Sie zum Diagrammtyp „Bericht“ wechseln.)

|Indikatortyp|Instanzenname|Gemeldete Verzögerung (ms)|
|---------------|-------------|-------------------|
|Verzögerung der Benutzereingabe pro Prozess|1:4232 <Calculator.exe>|  200|
|Verzögerung der Benutzereingabe pro Prozess|2:1000 <Calculator.exe>|  16|
|Verzögerung der Benutzereingabe pro Prozess|1:2000 <Calculator.exe>|  32|
|Verzögerung der Benutzereingabe pro Sitzung|1|    200|
|Verzögerung der Benutzereingabe pro Sitzung|2|    16|
|Verzögerung der Benutzereingabe pro Sitzung|Durchschnitt|  108|
|Verzögerung der Benutzereingabe pro Sitzung|Max.|  200|

## <a name="counters-used-in-an-overloaded-system"></a>Einsatz der Indikatoren in einem überlasteten System

Sehen wir uns jetzt an, wie der Bericht aussieht, wenn die Leistung für eine App herabgesetzt ist. Das folgende Diagramm zeigt Messwerte für Benutzer, die remote in Microsoft Word arbeiten. In diesem Fall lässt die Leistung des RDSH-Servers im Lauf der Zeit nach, wenn sich mehr Benutzer anmelden.

![Remotedesktop: Ein Leistungsdiagrammbeispiel für den RDSH-Server, der Microsoft Word ausführt](./media/rds-user-input-perf-graph.png)

So lesen sich die Linien des Diagramms:

- Die pinkfarbene Linie zeigt die Anzahl der Sitzungen, die beim Server angemeldet sind.
- Die rote Linie ist die CPU-Auslastung.
- Die grüne Linie ist die maximale Verzögerung der Benutzereingaben über alle Sitzungen.
- Die blaue Linie (in diesem Diagramm schwarz dargestellt) stellt die durchschnittliche Verzögerung der Benutzereingabe über alle Sitzungen dar.

Sie werden feststellen, dass ein Zusammenhang zwischen den Spitzen der CPU-Auslastung und der Verzögerung der Benutzereingabe besteht – wenn die CPU stärker ausgelastet wird, erhöht sich die Verzögerung der Benutzereingaben. Außerdem gelangt die CPU-Auslastung näher an 100 %, während dem System weitere Benutzer hinzugefügt werden, was zu häufigeren Spitzen bei der Verzögerung der Benutzereingaben führt. Dieser Indikator ist einerseits sehr nützlich in Fällen, in denen die Serverressourcen zur Neige gehen, andererseits können Sie ihn auch verwenden, um die Verzögerung der Benutzereingaben im Zusammenhang einer bestimmten Anwendung nachzuverfolgen.

## <a name="configuration-options"></a>Konfigurationsoptionen

Bei der Verwendung dieses Leistungsindikators ist zu beachten, dass er die Verzögerung der Benutzereingaben standardmäßig in einem Intervall von 1.000 ms meldet. Wenn Sie die Intervalleigenschaft des Leistungsindikatorbeispiels auf einen anderen Wert festlegen (wie im folgenden Screenshot dargestellt), ist der gemeldete Wert falsch.

![Remotedesktop: Die Eigenschaften Ihres Systemmonitors](./media/rds-user-input-perfmon-properties.png)

Um dies zu beheben, können Sie den folgenden Registrierungsschlüssel übereinstimmend mit dem Intervall festlegen (in Millisekunden), das Sie verwenden möchten. Wenn wir beispielsweise „Stichprobe alle x Sekunden“ auf 5 Sekunden festlegen, müssen wir diesen Schlüssel auf 5.000 ms festlegen.

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]

"LagCounterInterval"=dword:00005000
```

>[!NOTE]
>Wenn Sie Windows 10, Version 1809 oder höher, oder Windows Server 2019 oder höher verwenden, brauchen Sie LagCounterInterval nicht festzulegen, um den Leistungsindikator zu korrigieren.

Unter dem gleichen Registrierungsschlüssel haben wir außerdem zwei Schlüssel hinzugefügt, die Sie möglicherweise nützlich finden:

**LagCounterImageNameFirst**: Legen Sie diesen Schlüssel auf `DWORD 1` fest (Standardwert 0, oder der Schlüssel ist nicht vorhanden). Dadurch werden die Namen der Indikatoren in „Imagename <Sitzungs-ID:Prozess-ID>“ geändert. Beispiel: „explorer <1:7964>“. Dies ist nützlich, wenn Sie nach dem Imagenamen sortieren möchten.

**LagCounterShowUnknown**: Legen Sie diesen Schlüssel auf `DWORD 1` fest (Standardwert 0, oder der Schlüssel ist nicht vorhanden). Dies zeigt alle Prozesse an, die als Dienste oder SYSTEM ausgeführt werden. Einige Dienste werden mit „?“ als Wert für die Sitzung angezeigt.

So sieht es aus, wenn Sie beide Schlüssel aktivieren:

![Remotedesktop: Systemmonitor, wenn beide Schlüssel aktiviert sind](./media/rds-user-input-delay-with-two-counters.png)

## <a name="using-the-new-counters-with-non-microsoft-tools"></a>Verwenden der neuen Indikatoren mit nicht von Microsoft stammenden Tools

Überwachungstools können diesen Indikator mithilfe der [Perfmon-API](https://msdn.microsoft.com/library/windows/desktop/aa371903.aspx) nutzen.

## <a name="download-windows-server-insider-software"></a>Herunterladen von Windows Server Insider-Software

Registrierte Insider können direkt zur [Windows Server Insider-Vorschau-Downloadseite](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver) navigieren, um die aktuellsten Insider-Softwaredownloads abzurufen.  Informationen zum Registrieren als Insider finden Sie unter [Erste Schritte mit Server](https://insider.windows.com/en-us/for-business-getting-started-server/).

## <a name="share-your-feedback"></a>Teilen Sie Ihr Feedback mit

Sie können Feedback zu dieser Funktion über den Feedback-Hub senden. Wählen Sie **Apps > Alle anderen Apps** aus, und schließen Sie  „RDS-Leistungsindikatoren: Systemmonitor“ in den Titel Ihres Beitrags ein.

Ideen zu allgemeinen Funktionen können Sie auf der [RDS-UserVoice-Seite](https://aka.ms/uservoice-rds) anregen.
