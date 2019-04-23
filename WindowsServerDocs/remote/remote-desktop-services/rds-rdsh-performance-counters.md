---
title: Verwenden von Leistungsindikatoren zur diagnose von Problemen von Anwendung Reaktionsfähigkeit auf Remote Desktop Session Hosts
description: Wird Ihre app langsam auf RDS ausgeführt? Erfahren Sie mehr über Leistungsindikatoren, die Sie zum Diagnostizieren von app-Leistungsprobleme für RDSH verwenden können
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 09/19/2018
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 241b2b776a68cf5aec68a4d331201a07f0e5ea53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844651"
---
# <a name="use-performance-counters-to-diagnose-app-performance-problems-on-remote-desktop-session-hosts"></a>Verwenden von Leistungsindikatoren zur diagnose von app-Leistungsprobleme für Remote Desktop Session Hosts

Eines der schwierigsten Probleme diagnostizieren der Leistung der Anwendung ist, die Anwendungen sind langsam oder reagiert nicht. Sie können in der Vergangenheit Starten der Diagnose durch das Sammeln von CPU, Arbeitsspeicher, Datenträger-e/a und andere Metriken und verwenden Sie Tools wie Windows Performance Analyzer, um zu ermitteln, die Ursache des Problems. Leider können nicht in den meisten Fällen diese Daten Sie die Ursache zu ermitteln, da Resource Consumption Leistungsindikatoren häufige und große Variationen aufweisen. Dadurch wird es schwierig ist, lesen Sie die Daten und korrelieren sie mit das gemeldete Problem. Können Sie weitere Ihrer app-Leistungsprobleme schnell zu beheben, haben wir einige neue Leistungsindikatoren hinzugefügt (verfügbaren [herunterladen](#download-windows-server-insider-software) über die [Windows Insider-Programm](https://insider.windows.com)) dieses Measure Benutzereingaben Flows.

Der Zähler für die Eingabe Benutzerverzögerung können Sie die Hauptursache für fehlerhafte Benutzer schnell zu identifizieren, die RDP-Umgebungen. Dieser Leistungsindikator misst, wie lange (z. B. Maus oder Tastatur Nutzung) Eingabe durch den Benutzer in der Warteschlange bleibt, bevor sie von einem Prozess übernommen wird, und der Indikator kann in lokale und remote-Sitzungen.

Die folgende Abbildung zeigt eine grobe Darstellung der Eingabe benutzerflow vom Client, Anwendung.

![Remotedesktop - Benutzereingaben fließen über den Remotedesktopclient für Benutzer der Anwendung](.\media\rds-user-input.png)

Der Eingabe Benutzerverzögerung-Indikator misst das maximale Delta (innerhalb einer bestimmten Zeitspanne) zwischen der Eingabe, die in die Warteschlange gestellt und wenn sie in von der app übernommen wird eine [herkömmliche Nachrichtenschleife](https://msdn.microsoft.com/library/windows/desktop/ms644927.aspx#loop), wie im folgenden Flussdiagramm dargestellt:

![Remotedesktop - Eingabe Benutzer Verzögerung Performance Counter-flow](.\media\rds-user-input-delay.png)

Ein wichtiges Detail in dieses Indikators ist, dass die maximale Verzögerung Eingabe innerhalb eines konfigurierbaren Zeitraums gemeldet. Dies ist die am längsten dauert es für eine Eingabe für die Anwendung erreicht ist, die die Geschwindigkeit von wichtig und sichtbar Aktionen wie die Eingabe auswirken kann.

Beispielsweise würde in der folgenden Tabelle, die Eingabe benutzerverzögerung als 1.000 ms innerhalb dieses Intervalls gemeldet werden. Der Leistungsindikator erfasst die langsamste Benutzereingabe Verzögerung im Intervall da Wahrnehmung des Benutzers, der "langsam" durch die am langsamsten Eingabezeit bestimmt wird (Maximalwert) es kommen, nicht die durchschnittliche Geschwindigkeit, der alle insgesamt Eingaben.

|Number| 0 | 1 | 2 |
|------|---|---|---|
|Verzögerung |16 ms| 20 ms| 1.000 ms|

## <a name="enable-and-use-the-new-performance-counters"></a>Aktivieren Sie und verwenden Sie die neue Leistungsindikatoren

Um diesen neuen Leistungsindikatoren verwenden zu können, müssen Sie zuerst einen Registrierungsschlüssel mit dem folgenden Befehl aktivieren:

```
reg add "HKLM\System\CurrentControlSet\Control\Terminal Server" /v "EnableLagCounter" /t REG_DWORD /d 0x1 /f
```

>[!NOTE]
> Wenn Sie Windows 10, Version 1809 oder höher oder WindowsServer 2019 (oder höher) verwenden, müssen Sie wird nicht den Registrierungsschlüssel zu aktivieren.

Als Nächstes starten Sie den Server neu. Klicken Sie dann öffnen Sie den Systemmonitor, und wählen Sie das Pluszeichen (+) aus, wie im folgenden Screenshot gezeigt.

![Remote Desktop – dieser Screenshot zeigt die Vorgehensweise beim Hinzufügen des Benutzers Eingabe-Leistungsindikator "Verzögerung"](.\media\rds-add-user-input-counter-screen.png)

Danach sollte das Dialogfeld "Leistungsindikatoren hinzufügen", in dem Sie auswählen können **Eingabe Benutzerverzögerung pro Prozess** oder **Eingabe Benutzerverzögerung pro Sitzung**.

![Remote Desktop – dieser Screenshot zeigt die Eingabe Benutzerverzögerung pro Sitzung hinzufügen](.\media\rds-user-delay-per-session.png)

![Remote Desktop – dieser Screenshot zeigt die Eingabe Benutzerverzögerung pro Prozess hinzufügen](.\media\rds-user-delay-per-process.png)

Bei Auswahl von **Eingabe Benutzerverzögerung pro Prozess**, sehen Sie die **Instanzen des ausgewählten Objekts** (das heißt, die Prozesse) in ```SessionID:ProcessID <Process Image>``` Format.

Angenommen, die Rechner-Anwendung ausgeführt wird, einem [Sitzungs-ID 1](https://msdn.microsoft.com/library/ms524326.aspx), sehen Sie ```1:4232 <Calculator.exe>```.

> [!NOTE]
> Nicht alle Prozesse sind enthalten. Alle Prozesse, die als SYSTEM ausgeführt werden, nicht angezeigt werden.

Der Indikator wird gestartet, Eingabe benutzerverzögerung reporting, sobald Sie ihn hinzufügen. Beachten Sie, dass die maximale Dezimalstellen standardmäßig auf 100 (ms) festgelegt ist. 

![Remote Desktop – ein Beispiel der Aktivität für die Eingabe Benutzerverzögerung pro Prozess im Systemmonitor](.\media\rds-sample-user-input-delay-perfmon.png)

Als Nächstes sehen wir uns die **Eingabe Benutzerverzögerung pro Sitzung**. Instanzen für jede Sitzungs-ID vorhanden sind, und die Indikatoren des Prozesses der Eingabe benutzerverzögerung innerhalb der angegebenen Sitzungs angezeigt. Darüber hinaus stehen zwei Instanzen, die als "Max" (der maximale Eingabe Verzögerung in alle Sitzungen) und "Average" (alle Sitzungen über die durchschnittliche Acorss) bezeichnet.

Diese Tabelle zeigt ein Beispiel dieser Instanzen. (Sie können die gleiche Informationen in Perfmon abrufen durch den Wechsel zu den Graph-Berichtstyp.)

|Typ eines Indikators|Instanzenname|Gemeldete Verzögerung (ms)|
|---------------|-------------|-------------------|
|Eingabe Benutzerverzögerung pro Prozess|1:4232 < Calculator.exe >|  200|
|Eingabe Benutzerverzögerung pro Prozess|2:1000 < Calculator.exe >|  16|
|Eingabe Benutzerverzögerung pro Prozess|1:2000 < Calculator.exe >|  32|
|Eingabe Benutzerverzögerung pro Sitzung|1|    200|
|Eingabe Benutzerverzögerung pro Sitzung|2|    16|
|Eingabe Benutzerverzögerung pro Sitzung|Durchschnitt|  108|
|Eingabe Benutzerverzögerung pro Sitzung|Max.|  200|

## <a name="counters-used-in-an-overloaded-system"></a>Leistungsindikatoren, die in einem überladenen System verwendet

Jetzt sehen wir uns im Bericht angezeigt, wenn die Leistung für eine app beeinträchtigt wird. Das folgende Diagramm zeigt die Messwerte für die Remote-Benutzer in Microsoft Word. In diesem Fall nimmt die Leistung des RDSH-Servers im Laufe der Zeit ab, wie weitere Benutzer angemeldet haben.

![Remote Desktop – eine Beispiel-Leistungsdiagramm für die Ausführung von Microsoft Word RDSH-Servers](.\media\rds-user-input-perf-graph.png)

Hier ist das Diagramm Zeilen lesen:

- Die rosa Linie zeigt die Anzahl der Sitzungen, die auf dem Server angemeldet.
- Die rote Linie ist die CPU-Auslastung.
- Die grüne Linie ist die maximale Verzögerung Eingabe für alle Sitzungen.
- Die blaue Linie (angezeigt als Schwarz in diesem Diagramm) stellt die durchschnittliche Eingabe benutzerverzögerung in allen Sitzungen dar.

Sie werden feststellen, dass eine Korrelation zwischen der CPU-Spitzen und Eingabe benutzerverzögerung vorhanden ist, wie die CPU weitere Nutzung abruft, die Benutzereingabe Verzögerung erhöht. Wenn weitere Benutzer mit dem System hinzugefügt werden, ruft CPU-Auslastung auch näher an 100 %, führt zu häufigeren User input Verzögerung Spitzen ab. Während dieser Leistungsindikator in Fällen sehr nützlich ist, in dem der Server nicht über ausreichende Ressourcen ausgeführt wird, auch können sie Sie zum Nachverfolgen von Eingabe benutzerverzögerung im Zusammenhang mit einer bestimmten Anwendung.

## <a name="configuration-options"></a>Konfigurationsoptionen

Ein wichtig zu beachten, wenn Sie diesen Leistungsindikator zu verwenden ist, dass die Eingabe benutzerverzögerung standardmäßig in einem Intervall von 1000 ms gemeldet. Wenn Sie die Performance Counter-Beispiel Interval-Eigenschaft (wie im folgenden Screenshot gezeigt), etwas anderes festlegen, wird bei dem gemeldete Wert falsch sein.

![Remote Desktop – die Eigenschaften für Ihre Leistung überwachen](.\media\rds-user-input-perfmon-properties.png)

Um dieses Problem zu beheben, können Sie festlegen, den folgenden Registrierungsschlüssel mit das Intervall (in Millisekunden) übereinstimmen, das Sie verwenden möchten. Wenn wir Beispiel alle X Sekunden in 5 Sekunden ändern, müssen wir z. B. diesen Schlüssel auf 5000 ms festlegen.

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]

"LagCounterInterval"=dword:00005000
```

>[!NOTE]
>Wenn Sie Windows 10, Version 1809 oder höher oder WindowsServer 2019 (oder höher) verwenden, müssen Sie nicht LagCounterInterval, beheben Sie den Leistungsindikator festlegen.

Wir haben außerdem eine Reihe von Schlüsseln hinzugefügt, die unter dem gleichen Registrierungsschlüssel hilfreich sein können:

**LagCounterImageNameFirst** – legen Sie diesen Schlüssel auf `DWORD 1` (Standardwert ist 0 oder Schlüssel ist nicht vorhanden). Dadurch wird die Indikatornamen in "Name des Bilds < SessionID:ProcessId >." geändert. Z. B. "Explorer < 1:7964 >." Dies ist hilfreich, wenn nach Bildnamen sortiert werden soll.

**LagCounterShowUnknown** – legen Sie diesen Schlüssel auf `DWORD 1` (Standardwert ist 0 oder Schlüssel ist nicht vorhanden). Dies zeigt alle Prozesse, die als Dienste oder das SYSTEM ausgeführt werden. Einige Prozesse mit jeweils Sitzung als festgelegt angezeigt "?."

Dies ist, wie es Wenn Sie beide Schlüssel einschalten aussieht:

![Remotedesktop - Systemmonitor mit den beiden Schlüsseln auf](.\media\rds-user-input-delay-with-two-counters.png)

## <a name="using-the-new-counters-with-non-microsoft-tools"></a>Verwenden die neuen Indikatoren mit nicht-Microsoft-tools

Tools zur Überwachung dieser Leistungsindikator erzeugen kann, indem die [Perfmon-API](https://msdn.microsoft.com/library/windows/desktop/aa371903.aspx).

## <a name="download-windows-server-insider-software"></a>Windows Server Insider-Software herunterladen

Registrierte Insider können direkt zu navigieren, die [Windows Server Insider Preview-Download-Seite](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver) auf die neuesten Insider Software herunterlädt.  Vorgehensweise: Registrieren Sie als Insider finden Sie unter [erste Schritte mit Server](https://insider.windows.com/en-us/for-business-getting-started-server/).

## <a name="share-your-feedback"></a>Teilen Sie uns Ihre Meinung

Sie können Feedback für dieses Feature über den Feedback-Hub senden. Wählen Sie **Apps > alle anderen apps** und umfassen "RDS-Leistungsindikatoren – Leistungsüberwachung" in Ihren Beitrag für den Titel.

Allgemeine funktionsideen finden Sie auf die [RDS-UserVoice-Seite](https://aka.ms/uservoice-rds).
