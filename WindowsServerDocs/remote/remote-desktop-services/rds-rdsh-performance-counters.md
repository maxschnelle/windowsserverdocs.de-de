---
title: Verwenden Sie Leistungsindikatoren Anwendung Reaktionsfähigkeit auf Remote Desktop Session Hosts Diagnose von
description: Ist Ihre app auf RDS langsam ausgeführt? Erfahren Sie mehr über Leistungsindikatoren, die Sie verwenden können, um Leistungsprobleme mit RDSH app zu diagnostizieren
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133716"
---
# Verwenden Sie Leistungsindikatoren app Leistungsprobleme auf Remote Desktop Session Hosts Diagnose

Eines der schwierigsten Probleme zu diagnostizieren Leistung der Anwendung ist – die Anwendungen langsam ausgeführt werden oder nicht reagieren. In der Regel Ihre Diagnose durch Sammeln von CPU, Arbeitsspeicher, Datenträger/o und andere Metriken starten und verwenden Sie Tools wie Windows Performance Analyzer, um herauszufinden, was das Problem verursacht. Leider helfen nicht in den meisten Fällen diese Daten Ihnen die Ursache zu identifizieren, da Ressource Verbrauch Leistungsindikatoren häufige und große Varianten aufweisen. Dadurch können nur schwer zu lesen der Markerdaten mit dem gemeldeten Problem zu korrelieren. Damit Sie schnell Ihrer app beheben können, haben wir einige neue Leistungsindikatoren (verfügbar [zum Herunterladen von](#download-windows-server-insider-software) über das [Windows-Insider-Programm](https://insider.windows.com)) hinzugefügt, die Benutzereingaben fließen zu messen.

Der Benutzer Eingabe Verzögerung Zähler helfen Ihnen die Ursache für fehlerhafte Endbenutzer schnell zu identifizieren, die RDP-Erfahrungen. Dieser Leistungsindikator misst, wie lange eine Benutzereingabe (z. B. Maus oder Tastatur Nutzung) in der Warteschlange bleibt, bevor es von einem Prozess ausgewählt wird, und der Zähler funktioniert in lokal und remote-Sitzungen.

Die folgende Abbildung zeigt eine grobe Darstellung der Eingabe Ablauf der Benutzer vom Client Anwendung.

![Remotedesktop - Benutzereingaben fließen vom Benutzer Remotedesktop-Client an die Anwendung](.\media\rds-user-input.png)

Der Benutzer Eingabe Verzögerung Indikator misst das maximale Delta (innerhalb eines Zeitintervalls) zwischen die Eingabe in die Warteschlange eingereiht wird und wenn es von der app in eine [herkömmliche Nachrichtenschleife](https://msdn.microsoft.com/library/windows/desktop/ms644927.aspx#loop)Zielarray abgerufen wird, wie im folgenden Flussdiagramm dargestellt:

![Remotedesktop - Eingabe Benutzer Verzögerung Leistung Zähler Fluss](.\media\rds-user-input-delay.png)

Eine wichtige Detail der Zähler wird, dass sie die maximale Benutzer Eingabe Verzögerung in einem konfigurierbaren Intervall meldet. Dies ist die längste Zeitaufwand für die Eingabe für die Anwendung zu erreichen, die sich die Geschwindigkeit der wichtige und sichtbar Aktionen wie das eingeben auswirken können.

Beispielsweise würde in der folgenden Tabelle, die Benutzer Eingabe Verzögerung als 1.000 ms innerhalb dieses Zeitraums gemeldet werden. Der Zähler meldet langsamsten Benutzereingaben Verzögerung in das Intervall da durch die langsamste Zeit bei der Eingabe des Benutzers Wahrnehmung von "slow" bestimmt wird (das Maximum) auftreten, nicht die durchschnittliche Geschwindigkeit des gesamten Eingaben.

|Zahl| 0 | 1 | 2 |
|------|---|---|---|
|Verzögerung |16 ms| 20 ms| 1.000 ms|

## Aktivieren Sie und verwenden Sie die neue Leistungsindikatoren

Um diese neue Leistungsindikatoren verwenden zu können, müssen Sie zunächst einen Registrierungsschlüssel durch Ausführen dieses Befehls aktivieren:

```
reg add "HKLM\System\CurrentControlSet\Control\Terminal Server" /v "EnableLagCounter" /t REG_DWORD /d 0x1 /f
```

>[!NOTE]
> Wenn Sie Windows 10, Version 1809 oder höher oder Windows Server 2019 oder höher ist, Sie nicht den Registrierungsschlüssel aktivieren müssen.

Als Nächstes starten Sie den Server neu. Anschließend öffnen Sie den Performance Monitor, und wählen Sie das Pluszeichen (+), wie im folgenden Screenshot gezeigt.

![Remotedesktop - einen Screenshot zeigt, wie Sie den Benutzer hinzufügen Eingabe Verzögerung-Leistungsindikator](.\media\rds-add-user-input-counter-screen.png)

Nach der, sollten Sie das Dialogfeld "Leistungsindikatoren hinzufügen" sehen, in denen können Sie **Benutzer Eingabe Verzögerung pro Prozess** oder **Benutzer Eingabe Verzögerung pro Sitzung**auswählen.

![Remotedesktop - einen Screenshot zeigt, wie Sie die Benutzer Eingabe Verzögerung pro Sitzung hinzufügen](.\media\rds-user-delay-per-session.png)

![Remotedesktop - einen Screenshot zeigt, wie Sie die Benutzer Eingabe Verzögerung pro Prozess hinzufügen](.\media\rds-user-delay-per-process.png)

Wenn Sie **Benutzer Eingabe Verzögerung pro Prozess**ausgewählt haben, sehen Sie die **Instanzen des ausgewählten Objekts** (mit anderen Worten: die Prozesse) in ```SessionID:ProcessID <Process Image>``` Format.

Beispielsweise, wenn die Rechner-app in einer [Sitzung ID 1](https://msdn.microsoft.com/library/ms524326.aspx)ausgeführt wird, sehen Sie ```1:4232 <Calculator.exe>```.

> [!NOTE]
> Nicht alle Prozesse sind enthalten. Keine Prozesse angezeigt, die als SYSTEM ausgeführt werden.

Der Zähler wird gestartet, Benutzer Eingabe Verzögerung reporting, sobald Sie ihn hinzufügen. Beachten Sie, dass die maximale Skalierung auf 100 (in Millisekunden) standardmäßig festgelegt ist. 

![Remotedesktop - ein Beispiel für Aktivität für die Benutzer Eingabe Verzögerung pro Prozess im Systemmonitor](.\media\rds-sample-user-input-delay-perfmon.png)

Als Nächstes sehen wir uns die **Benutzer Eingabe Verzögerung pro Sitzung**. Instanzen für jede Sitzung-ID vorhanden sind, und ihre Indikatoren Anzeigen der Benutzer Eingabe Verzögerung von einem beliebigen Prozess innerhalb der angegebenen Sitzung. Darüber hinaus sind zwei Instanzen "Max." (die maximale Benutzer Eingabe Verzögerung alle sitzungsübergreifend) und "Durchschnittlichen" (alle Sitzungen über die durchschnittliche Acorss).

Diese Tabelle zeigt ein Beispiel für diese Instanzen. (Sie können die gleiche Informationen im Systemmonitor abrufen wechseln zu den Typ des Berichts Graph.)

|Typ der Zähler|Name der Instanz|Gemeldeten Verzögerung (in Millisekunden)|
|---------------|-------------|-------------------|
|Benutzer Eingabe Verzögerung pro Prozess|1:4232 < Calculator.exe >|  200|
|Benutzer Eingabe Verzögerung pro Prozess|2:1000 < Calculator.exe >|  16|
|Benutzer Eingabe Verzögerung pro Prozess|1:2000 < Calculator.exe >|  32|
|Benutzer Eingabe Verzögerung pro Sitzung|1|    200|
|Benutzer Eingabe Verzögerung pro Sitzung|2|    16|
|Benutzer Eingabe Verzögerung pro Sitzung|Mittelmäßig|  108|
|Benutzer Eingabe Verzögerung pro Sitzung|Max|  200|

## Leistungsindikatoren in eine überladene System verwendet

Jetzt sehen wir uns, was Sie im Bericht sehen, wenn die Leistung für eine app verringert wird. Das folgende Diagramm zeigt die Messwerte für Remote-Benutzer in Microsoft Word. In diesem Fall verringert sich die Leistung des RDSH-Servers im Laufe der Zeit, als weitere Benutzer anmelden.

![Remotedesktop - ein Beispiel Leistungsdiagramm des RDSH-Servers, die mit Microsoft Word](.\media\rds-user-input-perf-graph.png)

Hier ist das Diagramm Zeilen lesen:

- Die violette Linie zeigt die Anzahl der Sitzungen auf dem Server angemeldet.
- Die rote Linie ist die CPU-Auslastung.
- Die grüne Linie gibt die maximale Benutzer Eingabe über alle Sitzungen hinweg.
- Die blaue Zeile (als Schwarz in diesem Diagramm angezeigt) stellt alle sitzungsübergreifend durchschnittlichen Benutzer Eingabe Verzögerung dar.

Sie werden feststellen, dass eine Beziehung zwischen CPU-Auslastung und Benutzer Eingabe Verzögerung – wie die CPU weitere Nutzung erhält, Benutzereingaben Verzögerung erhöht. Darüber hinaus weitere Benutzer mit dem System hinzugefügt, nähert CPU-Auslastung auf 100 %, zu häufigere Benutzer Eingabe Verzögerung Spitzen. Während dieser Zähler in Fällen sehr nützlich ist, in denen der Server nicht genügend Ressourcen verfügt, können Sie es auch verwenden, Benutzer Eingabe Verzögerung im Zusammenhang mit einer bestimmten Anwendung verfolgen.

## Konfigurationsoptionen

Wichtig zu beachten bei Verwendung dieser Leistungsindikator ist, dass Benutzer Eingabe Verzögerung in einem Intervall von 1.000 ms standardmäßig meldet. Wenn Sie die Leistung Counter-Beispiel Intervall-Eigenschaft (wie im folgenden Screenshot gezeigt) auf einen anderen Wert festlegen, wird der gemeldete Wert falsch sein.

![Remotedesktop - Eigenschaften für Ihre Systemmonitor](.\media\rds-user-input-perfmon-properties.png)

Um dieses Problem zu beheben, können Sie festlegen, den folgenden Registrierungsschlüssel auf das Intervall (in Millisekunden) übereinstimmen, das Sie verwenden möchten. Wenn wir Beispiel für alle X Sekunden auf 5 Sekunden ändern, müssen wir z. B. dieser Schlüssel auf 5000 ms festgelegt.

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]

"LagCounterInterval"=dword:00005000
```

>[!NOTE]
>Wenn Sie Windows 10, Version 1809 oder höher oder Windows Server 2019 oder höher ist, Sie nicht LagCounterInterval den Leistungsindikator beheben festlegen müssen.

Wir haben auch eine Reihe von Schlüsseln hinzugefügt, die Sie unter dem gleichen Registrierungsschlüssel hilfreich sein können:

**LagCounterImageNameFirst** – dieser Schlüssel als `DWORD 1` (Standardwert 0 oder Schlüssel ist nicht vorhanden). Dadurch werden die Namen der Leistungsindikatoren "Image Name < SessionID:ProcessId >". Z. B. "Explorer < 1:7964 >." Dies ist hilfreich, wenn Sie nach Bildname sortieren möchten.

**LagCounterShowUnknown** – dieser Schlüssel als `DWORD 1` (Standardwert 0 oder Schlüssel ist nicht vorhanden). Dies zeigt alle Prozesse, die als Dienste oder SYSTEM ausgeführt werden. Einige Prozesse werden angezeigt, mit der Sitzung als "?."

Dies sieht es wie wenn Sie beide Schlüssel aktivieren:

![Remotedesktop - der Performance Monitor mit beider Schlüssel auf](.\media\rds-user-input-delay-with-two-counters.png)

## Verwenden die neuen Indikatoren mit nicht-Microsoft-tools

Überwachungstools kann sich dieser Zähler mithilfe der [Systemmonitor-API](https://msdn.microsoft.com/library/windows/desktop/aa371903.aspx)verwenden.

## Windows Server-Insider-Software herunterladen

Registrierte Insider können direkt auf die [Windows Server Insider Preview herunterladen Seite](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver) zum Abrufen der neuesten Insider Softwaredownloads navigieren.  Weitere Informationen zur Registrierung als Insider finden Sie in der [Erste Schritte mit dem Server](https://insider.windows.com/en-us/for-business-getting-started-server/).

## Feedback mitteilen

Sie können Feedback für diese Funktion über die Feedback-Hub übermitteln. Wählen Sie **Apps > alle anderen apps** und umfassen "RDS-Leistungsindikatoren – Systemmonitor" in Ihren Beitrag Titel.

Funktion "Allgemein" Ideen finden Sie auf der [Seite "RDS UserVoice"](https://aka.ms/uservoice-rds).
