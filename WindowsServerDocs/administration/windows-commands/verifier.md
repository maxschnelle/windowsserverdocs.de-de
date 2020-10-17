---
title: verifier
description: Referenz Artikel für den Verifier-Befehl, der das Treiber-Verifier-Manager-Hilfsprogramm ausführt.
ms.topic: reference
ms.assetid: 782173d6-f196-4bc4-a547-76109829453c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: df3a9826463ea4062fb661e04e8fb774275c09d7
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156268"
---
# <a name="verifier"></a>verifier

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Treiber Überprüfung überwacht Windows-Kernelmodustreiber und Grafiktreiber, um unzulässige Funktionsaufrufe oder Aktionen zu erkennen, die das System möglicherweise beschädigen. Die Treiber Überprüfung kann Windows-Treibern eine Vielzahl von Belastungen und Tests unterziehen, um das falsche Verhalten zu ermitteln. Sie können konfigurieren, welche Tests ausgeführt werden sollen. Dadurch können Sie einen Treiber durch hohe belastungsbelastungen oder durch optimierte Tests platzieren. Sie können die Treiber Überprüfung auch für mehrere Treiber gleichzeitig oder für einen Treiber gleichzeitig ausführen.

> [!IMPORTANT]
> Sie müssen sich in der Gruppe "Administratoren" auf dem Computer befinden, um die Treiber Überprüfung verwenden zu können.
> Das Ausführen der Treiber Überprüfung kann zum Absturz des Computers führen. Daher sollten Sie dieses Hilfsprogramm nur auf Computern ausführen, die zum Testen und Debuggen verwendet werden.

## <a name="syntax"></a>Syntax

```
verifier /standard /all
verifier /standard /driver NAME [NAME ...]
verifier /flags <options> /all
verifier /flags <options> /driver NAME [NAME ...]
verifier /rules [OPTION ...]
verifier /query
verifier /querysettings
verifier /bootmode [persistent | disableafterfail | oneboot]
verifier /reset
verifier /faults [Probability] [PoolTags] [Applications] [DelayMins]
verifier /faultssystematic [OPTION ...]
verifier /log LOG_FILE_NAME [/interval SECONDS]
verifier /volatile /flags <options>
verifier /volatile /adddriver NAME [NAME ...]
verifier /volatile /removedriver NAME [NAME ...]
verifier /volatile /faults [Probability] [PoolTags] [Applications] [DelayMins]
verifier /domain <types> <options> /driver ... [/logging | /livedump]
verifier /logging
verifier /livedump
verifier /?
verifier /help
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /all | Weist das Treiber Verifier-Hilfsprogramm an, alle installierten Treiber nach dem nächsten Start zu überprüfen. |
| /bootmode `[persistent | disableafterfail | oneboot | resetonunusualshutdown]` | Steuert, ob die Einstellungen für das Treiber Verifier-Hilfsprogramm nach einem Neustart aktiviert werden. Um diese Option festzulegen oder zu ändern, müssen Sie den Computer neu starten. Die folgenden Modi sind verfügbar:<ul><li>**permanent** : stellt sicher, dass die Treiber Verifier-Einstellungen über viele Neustarts hinweg beibehalten werden. Dies ist die Standardeinstellung.</li><li>**disableafterfail** : Wenn Windows nicht gestartet werden kann, wird durch diese Einstellung das Treiber Überprüfungs Programm für nachfolgende Neustarts deaktiviert.</li><li>**oneboot** : aktiviert nur die Treiber Überprüfungs Einstellungen, wenn der Computer das nächste Mal gestartet wird. Das Treiber Verifier-Hilfsprogramm ist für nachfolgende Neustarts deaktiviert.</li><li>**reabtonunusualshutdown** : das Treiber Überprüfungs Programm wird so lange beibehalten, bis ein ungewöhnliches Herunterfahren auftritt. Die zugehörige "Rous"-Abkürzung kann verwendet werden.</li></ul> |
| /Driver `<driverlist>` | Gibt einen oder mehrere Treiber an, die überprüft werden. Der **driverlist** -Parameter ist eine Liste von Treibern nach binär Name, wie z. b. *driver.sys*. Verwenden Sie ein Leerzeichen, um die Treiber Namen voneinander zu trennen. Platzhalter Werte (z `n*.sys` . b.) werden nicht unterstützt. |
| /driver.exclude `<driverlist>` | Gibt einen oder mehrere Treiber an, die von der Überprüfung ausgeschlossen werden. Dieser Parameter ist nur anwendbar, wenn alle Treiber für die Überprüfung ausgewählt wurden. Der **driverlist** -Parameter ist eine Liste von Treibern nach binär Name, wie z. b. *driver.sys*. Verwenden Sie ein Leerzeichen, um die Treiber Namen voneinander zu trennen. Platzhalter Werte (z `n*.sys` . b.) werden nicht unterstützt. |
| /faults | Aktiviert das **Simulations Feature "geringe Ressourcen** " im Treiber Überprüfungs Programm. Sie können **/Faults** anstelle von verwenden `/flags 0x4` . Sie können jedoch nicht `/flags 0x4` mit den **/Faults** -unter Parametern verwenden. Sie können die folgenden unter Parameter des/Faults-Parameters verwenden, um die Simulation mit geringer Ressourcen zu konfigurieren:<ul><li>**Wahrscheinlichkeit** : gibt die Wahrscheinlichkeit an, mit der das Treiber Überprüfungs Programm eine bestimmte Zuordnung misslingt. Geben Sie eine Zahl (in Dezimal oder hexadezimal) ein, die die Anzahl der Chancen in 10.000 darstellt, dass das Treiberüberprüfungs-Hilfsprogramm die Zuordnung nicht durchführt. Der Standardwert 600 bedeutet 600/10000 oder 6%.</li><li>**Pooltags** : schränkt die Zuordnungen ein, die das Treiberüberprüfungs-Hilfsprogramm für die Zuordnung mit den angegebenen Pooltags nicht ausführen kann. Sie können ein Platzhalter Zeichen (*) verwenden, um mehrere Pooltags darzustellen. Zum Auflisten mehrerer Pooltags trennen Sie die Tags durch Leerzeichen. Standardmäßig können alle Zuordnungen fehlschlagen. </li> <li> * * Anwendungen**: schränkt die Zuordnungen ein, die das Treiberüberprüfungs-Hilfsprogramm für das angegebene Programm nicht Zuordnungen ausführen kann. Geben Sie den Namen einer ausführbaren Datei ein. Um Programme aufzulisten, trennen Sie die Programmnamen durch Leerzeichen. Standardmäßig können alle Zuordnungen fehlschlagen.</li><li>**Delta mins** : gibt die Anzahl der Minuten nach dem Start an, während der das Treiberüberprüfungs-Hilfsprogramm nicht absichtlich fehlerhafte Zuweisungen verursacht. Dadurch können die Treiber geladen und das System vor Beginn des Tests stabilisiert werden. Geben Sie eine Zahl (in Dezimal oder hexadezimal) ein. Der Standardwert ist 7 (Minuten).</li></ul> |
| /faultssystematic | Gibt die Optionen für die systematische Simulation von **geringer Ressourcen** an. Verwenden Sie das- `0x40000` Flag, um die Simulations Option " **systematische niedrige Ressourcen** " auszuwählen. Die folgenden Optionen sind verfügbar:<ul><li>**enableboottime** : aktiviert Fehler Spritzen über Computer Neustarts hinweg.</li><li>**disableboottime** : deaktiviert die Fehler Injektion über Computer Neustarts hinweg (Dies ist die Standardeinstellung).</li><li>**recordboottime** : aktiviert Fehler Spritzen in Was ist, wenn der Computer neu gestartet wird.</li><li>**resetboottime** : deaktiviert die Fehler Injektion über Computer Neustarts und löscht die Stapel Ausschlussliste.</li><li>**enableruntime** : ermöglicht das dynamische Aktivieren von Fehler Spritzen.</li><li>**disableruntime** : deaktiviert die Fehler Injektion dynamisch.</li><li>**recordruntime** : aktiviert dynamisch Fehler Spritzen im was-wäre-wenn-Modus.</li><li>**resettruntime** : deaktiviert die Fehler Injektion dynamisch und löscht die zuvor faultierte Stapel Liste.</li><li>**querystatistics** : zeigt die aktuelle Fehler einschleusungs Statistik an.</li><li>**incrementcounter** -erhöht den Test Pass-Counter, mit dem ermittelt wird, wann ein Fehler eingefügt wurde.</li><li>**getstackid-Counter** : Ruft den anzeigen injizierten Stapel Bezeichner ab.</li><li>**excludestack stackId** : schließt den Stapel von Fault Injection aus.</li></ul> |
| /flags `<options>` | Aktiviert die angegebenen Optionen nach dem nächsten Neustart. Diese Zahl kann im Dezimal Format oder im hexadezimalen Format (mit dem Präfix "0x") eingegeben werden. Eine beliebige Kombination der folgenden Werte ist zulässig:<ul><li>**Wert: 1 oder 0x1 (Bit 0)**  -  Über [Prüfung des speziellen Pools](https://docs.microsoft.com/windows-hardware/drivers/devtest/special-pool)</li><li>**Wert: 2 oder 0x2 (Bit 1)**  -  [Erzwingen der unql-Prüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-irql-checking)</li><li>**Wert: 4 oder 0x4 (Bit 2)**  -  [Simulation mit geringer Ressourcen](https://docs.microsoft.com/windows-hardware/drivers/devtest/low-resources-simulation)</li><li>**Wert: 8 oder 0x8 (Bit 3)**  -  [Pool Nachverfolgung](https://docs.microsoft.com/windows-hardware/drivers/devtest/pool-tracking)</li><li>**Wert: 16 oder 0x10 (Bit 4)**  -  E [/a-Überprüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/i-o-verification)</li><li>**Wert: 32 oder 0x20 (Bit 5)**  -  [Deadlockerkennung](https://docs.microsoft.com/windows-hardware/drivers/devtest/deadlock-detection)</li><li>**Wert: 64 oder 0x40 (Bit 6)**  -  [Verbesserte e/a-Überprüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/enhanced-i-o-verification). Diese Option wird automatisch aktiviert, wenn Sie die e **/a-Überprüfung**auswählen.</li><li>**Wert: 128 oder 0x80 (Bit 7)**  -  [DMA](https://docs.microsoft.com/windows-hardware/drivers/devtest/dma-verification) -Überprüfung</li><li>**Wert: 256 oder 0x100 (Bit 8)**  -  [Sicherheitsüberprüfungen](https://docs.microsoft.com/windows-hardware/drivers/devtest/security-checks)</li><li>**Wert: 512 oder 0x200 (Bit 9)**  -  [Ausstehende e/a-Anforderungen erzwingen](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-pending-i-o-requests)</li><li>**Wert: 1024 oder 0x400 (Bit 10)**  -  [Unp-Protokollierung](https://docs.microsoft.com/windows-hardware/drivers/devtest/irp-logging)</li><li>**Wert: 2048 oder 0x800 (Bit 11)**  -  [Sonstige Überprüfungen](https://docs.microsoft.com/windows-hardware/drivers/devtest/miscellaneous-checks)</li><li>**Wert: 8192 oder 0x2000 (Bit 13)**  -  [Invariante MDL-Prüfung für Stapel](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-stack)</li><li>**Wert: 16384 oder 0x4000 (Bit 14)**  -  [Invariante MDL-Überprüfung für Treiber](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-driver)</li><li>**Wert: 32768 oder 0X8000 (Bit 15)**  -  [Power Framework-Verzögerungs fuzzingvorgang](https://docs.microsoft.com/windows-hardware/drivers/devtest/concurrency-stress-test)</li><li>**Wert: 65536 oder 0x10000 (Bit 16)** -Port-/miniportschnittstellenüberprüfung</li><li>**Wert: 131072 oder 0x20000 (Bit 17)**  -  [DDI](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking) -Kompatibilitätsprüfung</li><li>**Wert: 262144 oder 0x40000 (Bit 18)**  -  [Simulation von systematisch geringer Ressourcen](https://docs.microsoft.com/windows-hardware/drivers/devtest/systematic-low-resource-simulation)</li><li>**Wert: 524288 oder 0x80000 (Bit 19)**  -  [DDI-Kompatibilitäts Überprüfung (zusätzlich)](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)</li><li>**Wert: 2097152 oder 0x200000 (Bit 21)**  -  [NDIS/WiFi-Überprüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)</li><li>**Wert: 8388608 oder 0x800000 (Bit 23)**  -  Verzögerung beim Durchlaufen der [Kernel Synchronisierung](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)</li><li>**Wert: 16777216 oder 0x1000000 (Bit 24)**  -  Über [Prüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/vm-switch-verification) des virtuellen Computers</li><li>**Wert: 33554432 oder 0x2000000 (Bit 25)** -Code Integritätsprüfungen. Sie können diese Methode nicht verwenden, um die Optionen für die SCSI-Überprüfung oder die Storport-Überprüfung Weitere Informationen finden Sie unter [SCSI-Verifizierung](https://docs.microsoft.com/windows-hardware/drivers/devtest/scsi-verification) und [Storport](https://docs.microsoft.com/windows-hardware/drivers/devtest/dv-storport-verification)-Überprüfung.</li></ul> |
| /flags `<volatileoptions>` | Gibt die Optionen für das Treiber Überprüfungs Programm an, die sofort ohne Neustart geändert werden. Diese Zahl kann im Dezimal Format oder im hexadezimalen Format (mit dem Präfix "0x") eingegeben werden. Eine beliebige Kombination der folgenden Werte ist zulässig:<ul><li>**Wert: 1 oder 0x1 (Bit 0)** -spezieller Pool</li><li>**Wert: 2 oder 0x2 (Bit 1)** -erzwingen der Überprüfung von "unql"</li><li>**Wert: 4 oder 0x4 (Bit 2)** -Simulation mit geringer Ressourcen</li></ul> |
| `<probability>` | Zahl zwischen 1 und 10.000, die die Wahrscheinlichkeit für die Fehler Injektion angibt. Wenn Sie z. b. 100 angeben, wird eine Fehler einschleusungs Wahrscheinlichkeit von 1% (100/10000) angegeben.<p>Wenn dieser Parameter nicht angegeben wird, wird die Standard Wahrscheinlichkeit von 6% verwendet. |
| `<tags>` | Gibt die Pooltags an, die durch Leerzeichen getrennt eingefügt werden. Wenn dieser Parameter nicht angegeben wird, kann eine Pool Zuordnung mit Fehlern eingefügt werden. |
| `<apps>` | Gibt den Bilddateinamen der apps an, die mit Fehlern, getrennt durch Leerzeichen, eingefügt werden. Wenn dieser Parameter nicht angegeben wird, kann es vorkommen, dass eine geringe Ressourcen Simulation in jeder Anwendung stattfindet. |
| `<minutes>` | Eine positive Zahl, die die Länge des Zeitraums nach dem Neustart (in Minuten) angibt, in dem keine Fehler Injektion stattfindet. Wenn dieser Parameter nicht angegeben wird, wird die Standardlänge von *8 Minuten* verwendet. |
| /iolevel `<level>` | Gibt die Ebene der e/a-Überprüfung an. Der Wert von [Level] kann **1** sein: aktiviert die e/a-Überprüfung auf Ebene 1 (Standard) oder **2** -aktiviert die e/a-Überprüfung auf Ebene 1 und die e/a-Überprüfung auf Ebene 2. Wenn die e/a-Überprüfung nicht aktiviert ist (mithilfe von `/flags 0x10` ), wird **/IOLEVEL** ignoriert. |
| /log `<logfilename> [/intervalseconds]` | Erstellt eine Protokolldatei mit dem angegebenen Namen. Das Treiber Überprüfungs Programm schreibt regelmäßig Statistiken in diese Datei, basierend auf dem Intervall, das Sie optional festlegen. Das Standardintervall beträgt *30 Sekunden*.<p> Wenn ein Verifier **/Log** -Befehl in der Befehlszeile eingegeben wird, wird die Eingabeaufforderung nicht zurückgegeben. Um die Protokolldatei zu schließen und eine Eingabeaufforderung zurückzugeben, verwenden Sie die Tastenkombination **STRG + C** . Nachdem Sie einen Neustart erstellt haben, müssen Sie erneut den Befehl Verifier **/Log** senden, um ein Protokoll zu erstellen. |
| /Rules `<option>` | Optionen für Regeln, die deaktiviert werden können, einschließlich:<ul><li>**Abfrage** : zeigt den aktuellen Status von steuerbaren Regeln an.</li><li>**Reset** : setzt alle Regeln auf ihren Standardstatus zurück.</li><li>**Standard-ID** : legt die Regel-ID auf ihren Standardstatus fest. Für die unterstützten Regeln ist die Regel-ID der Wert der Fehlerüberprüfung 0xc4 (DRIVER_VERIFIER_DETECTED_VIOLATION) Parameter 1.</li><li>**ID deaktivieren** : deaktiviert die angegebene Regel-ID. Für die unterstützten Regeln ist die Regel-ID der Wert der Fehlerüberprüfung 0xc4 (DRIVER_VERIFIER_DETECTED_VIOLATION) Parameter 1.</li></ul> |
| /virtuelle | Aktiviert nach dem nächsten Neustart die Optionen "Standard" oder "Standardtreiber Überprüfung". Die Standardoptionen sind sonderpool, erzwingen der Überprüfung, Pool Verfolgung, e/a-Überprüfung, Deadlockerkennung, DMA-Verifizierung, Sicherheitsüberprüfungen, sonstige Überprüfungen und DDI-Kompatibilitätsprüfung. Dieser entspricht `/flags 0x209BB`.<p>[!NOTE] Ab Windows 10-Versionen nach 1803 wird die `/flags 0x209BB` WDF-Überprüfung nicht mehr automatisch durch die Verwendung von aktiviert. Verwenden Sie die **/virtuelle** -Syntax, um Standardoptionen zu aktivieren, die die WDF-Überprüfung enthalten. |
| /volatile | Ändert die Einstellungen, ohne den Computer neu zu starten. Flüchtige Einstellungen treten sofort in Kraft.<p>Sie können den **/volatile** -Parameter mit dem **/Flags** -Parameter verwenden, um einige Optionen zu aktivieren und zu deaktivieren, ohne neu gestartet zu werden. Sie können auch **/volatile** mit den Parametern **/adddriver** und **/removedriver** verwenden, um die Überprüfung eines Treibers ohne Neustart zu starten bzw. zu verhindern, auch wenn das Hilfsprogramm für die Treiber Überprüfung nicht ausgeführt wird. Weitere Informationen finden Sie unter [Verwenden von flüchtigen Einstellungen](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-volatile-settings). |
| /adddriver `<volatiledriverlist>` | Entfernt die angegebenen Treiber aus den flüchtigen Einstellungen. Um mehrere Treiber anzugeben, Listen Sie Ihre Namen durch Leerzeichen getrennt auf. Platzhalter Werte, z. b. *n.sys*, werden nicht unterstützt. |
| /removedriver `<volatiledriverlist>` |
| /reset | Löscht alle Einstellungen für das Treiber Verifier-Hilfsprogramm. Nach dem nächsten Neustart werden keine Treiber überprüft. |
| /querysettings | Zeigt eine Zusammenfassung der Optionen an, die aktiviert werden, und Treiber, die nach dem nächsten Start überprüft werden. Die Anzeige enthält keine Treiber und Optionen, die mit dem **/volatile** -Parameter hinzugefügt wurden. Weitere Möglichkeiten zum Anzeigen dieser Einstellungen finden Sie unter [Anzeigen von Einstellungen für Treiber Verifizierer](https://docs.microsoft.com/windows-hardware/drivers/devtest/viewing-driver-verifier-settings). |
| /Query "aus | Zeigt eine Zusammenfassung der aktuellen Aktivität des Treiber Verifier-Hilfsprogramms an. Das Feld **Ebene** in der Anzeige ist der hexadezimale Wert der Optionen, die mit dem **/volatile** -Parameter festgelegt werden. Erläuterungen zu den einzelnen statistischen Informationen finden Sie unter über [Wachen von globalen](https://docs.microsoft.com/windows-hardware/drivers/devtest/monitoring-global-counters) Leistungsindikatoren und über [Wachen einzelner](https://docs.microsoft.com/windows-hardware/drivers/devtest/monitoring-individual-counters)Leistungsindikatoren. |
| /Domain `<types> <options>` | Steuert die Einstellungen der verifizierererweiterung. Die folgenden verifizierererweiterungstypen werden unterstützt:<ul><li>**WDM** -aktiviert die verifizierererweiterung für WDM-Treiber.</li><li>**NDIS** -aktiviert die verifizierererweiterung für Netzwerktreiber.</li><li>**ert** : aktiviert die verifizierererweiterung für Kernel Modus-streamingtreiber.</li><li>**Audiofunktion** : aktiviert die verifizierererweiterung für Audiotreiber.</li></ul>. Die folgenden Erweiterungsoptionen werden unterstützt:<ul><li>**Rules. Default** : aktiviert Standard Validierungsregeln für die ausgewählte verifizierererweiterung.</li><li>**Rules. all** : aktiviert alle Validierungsregeln für die ausgewählte verifizierererweiterung.</li></ul> |
| /logging | Aktiviert die Protokollierung von Verletzungen, die von den ausgewählten verifizierererweiterungen erkannt werden. |
| /livedump | Aktiviert die Live-Speicher Abbild Erfassung für verletzte Regeln, die von den ausgewählten verifizierererweiterungen erkannt werden. |
| /? | Mit diesem Befehl wird die Befehlszeilenhilfe angezeigt. |

### <a name="return-codes"></a>Rückgabecodes

Nach dem Ausführen der Treiber Überprüfung werden folgende Werte zurückgegeben:

- 0: EXIT_CODE_SUCCESS

- 1: EXIT_CODE_ERROR

- 2: EXIT_CODE_REBOOT_NEEDED

#### <a name="remarks"></a>Hinweise

- Sie können den **/volatile** -Parameter mit einigen der **/Flags** -Optionen des Treibers Verifier-Hilfsprogramms und mit **/virtuelle**verwenden. Sie können **/volatile** nicht mit den **/Flags** -Optionen für die [DDI](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)-Kompatibilitäts Überprüfung, das [Verzögerungs fuzzingverfahren für Power Frameworks](https://docs.microsoft.com/windows-hardware/drivers/devtest/concurrency-stress-test), die über [Prüfung von storports](https://docs.microsoft.com/windows-hardware/drivers/devtest/dv-storport-verification)oder die [SCSI](https://docs.microsoft.com/windows-hardware/drivers/devtest/scsi-verification) Weitere Informationen finden Sie unter [Verwenden von flüchtigen Einstellungen](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-volatile-settings).

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Treiber Überprüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)

- [Steuern der Treiber Überprüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/controlling-driver-verifier)

- [Überwachen der Treiber Überprüfung](https://docs.microsoft.com/windows-hardware/drivers/devtest/monitoring-driver-verifier)

- [Verwenden von flüchtigen Einstellungen](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-volatile-settings)
