---
title: Fsutil-Verhalten
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b
ms.openlocfilehash: 4593739f25c356e72ea39947c67f3e1301573137
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838271"
---
# <a name="fsutil-behavior"></a>Fsutil-Verhalten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Abfragen, oder legt diesen fest NTFS-Volume-Verhalten, das enthält:

-   Die Erstellung der 8.3-Dateinamen Zeichen

-   Verwenden von Sonderzeichen in 8.3 Zeichen kurze Dateinamen auf NTFS-volumes

-   Das Aktualisieren des Stempels Zeitpunkt des letzten Zugriffs, wenn Verzeichnisse auf NTFS-Volumes aufgeführt sind

-   Die Häufigkeit, mit der, die Vorgabe Ereignisse im Systemprotokoll und NTFS-geschrieben werden, ausgelagertem und NTFS nicht ausgelagertem Poolspeicher Arbeitsspeicher Cache-Ebenen

-   Die Größe der Datei "master" Tabelle Zone (MFT-Zone)

-   Automatische Löschen von Daten, wenn das System auf einem NTFS-Volume beschädigt auftritt.

-   Datei löschen Notification (auch bekannt als kürzen oder die Zuordnung aufheben)

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<VolumePath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <Value> | [<VolumePath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <Frequency> | symlinkevaluation <SymbolicLinkType> | disabledeletenotify {1|0}}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|query|Fragt die Parameter Verhalten des Dateisystems an.|
|set|Ändert die Parameter Verhalten des Dateisystems an.|
|allowextchar {1&#124;0}|Ermöglicht (**1**) zugelassen oder verweigert (**0**) Zeichen aus erweiterten Zeichensatz festlegen (z. B. diakritische Zeichen) in 8.3 Zeichen kurze Dateinamen auf NTFS-Volumes verwendet werden.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|Bugcheckoncorrupt {1&#124;0}|Ermöglicht (**1**) zugelassen oder verweigert (**0**) Generierung eine fehlerüberprüfung, wenn auf einem NTFS-Volume beschädigt ist. Diese Funktion kann verwendet werden, um zu verhindern, dass NTFS im Hintergrund Löschen von Daten, wenn Sie mit der NTFS-Selbstreparaturfunktion--Funktion verwendet werden kann.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.<br /><br />Dieser Parameter gilt für:  Windows Server 2008 R2 und Windows 7.|
|disable8dot3 [<VolumePath>] {1&#124;0}|Deaktiviert (**1**) oder aktiviert (**0**) die Erstellung von 8.3 Zeichen-Dateinamen auf FAT- und NTFS-formatierten Datenträgern. Optional, mit dem Präfix die *%VolumePath* als Laufwerkname gefolgt von einem Doppelpunkt oder GUID angegeben.|
|Disablecompression {1&#124;0}|Deaktiviert die **(1)** oder aktiviert **(0)** NTFS-Komprimierung.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|disablecompressionlimit {1&#124;0}| Deaktiviert die **(1)** oder aktiviert **(0)** Grenzwert von NTFS-Komprimierung auf NTFS-Volume. Wenn eine komprimierte Datei, ein gewisses Maß an die Fragmentierung statt erweitern Sie die Datei nicht erreicht, beendet NTFS komprimiert zusätzliche Blöcke der Datei. Dies erfolgte, um komprimierte Dateien, die nicht größer als normal zu ermöglichen. Festlegen dieses Werts auf "true" verhindert diese Funktion die schränkt die Größe der komprimierten Dateien auf dem System. Wir empfehlen nicht, diese Funktion deaktivieren.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|disableencryption {1&#124;0}|Deaktiviert die **(1)** oder aktiviert **(0)** die Verschlüsselung von Ordnern und Dateien auf NTFS-Volumes.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|Disablefilemetadataoptimization {1&#124;0}|Deaktiviert die **(1)** oder aktiviert **(0)** Datei Metadaten-Optimierung. NTFS ist begrenzt, für wie viele Blöcke aufrechtzuerhalten, die eine bestimmte Datei haben kann. Komprimiert und Ersatzteile Dateien können sehr fragmentiert werden. Standardmäßig komprimiert NTFS in regelmäßigen Abständen seine interne Systemmetadaten-Strukturen, um mehr fragmentiert Dateien zu ermöglichen. Wenn dieser Wert auf "true" verhindert diese interne Optimierung. Wir empfehlen nicht, diese Funktion deaktivieren.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|disablelastaccess {1&#124;0}|Deaktiviert (**1**) oder aktiviert (**0**) bis zum letzten Zeitstempel für den Zugriff auf die einzelnen Verzeichnisse bei aktualisiert Verzeichnisse auf einem NTFS-Volume aufgeführt sind.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|Disablespotcorruptionhandling {1&#124;0}|Deaktiviert die **(1)** oder aktiviert **(0)** Erkennen von Beschädigungen behandeln. Einer der in Windows 8 und Windows Server 2012 eingeführten neuen Funktionen ist ein neues Formular für hohe Verfügbarkeit von CHKDSK aus. Dieses Feature ermöglicht es Systemadministratoren, führen Sie CHKDSK aus, um den Status eines Volumes zu analysieren, ohne es offline zu schalten. Wir empfehlen nicht, diese Funktion deaktivieren.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|disabletxf {1&#124;0}|Deaktiviert die **(1)** oder aktiviert **(0)** Txf auf dem angegebenen NTFS-Volume. TxF ist ein NTFS-Feature, Transaktion wie die Semantik für Dateisystemvorgänge bereitstellt. TxF ist gegenwärtig Deprected, obwohl die Funktionalität weiterhin verfügbar ist. Wir empfehlen nicht, Deaktivieren dieses Feature auf dem Volume "c:".<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|disablewriteautotiering {1&#124;0}|Deaktiviert die ReFS v2 automatische tiering Logik für mehrstufige Volumes.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|encryptpagingfile {1&#124;0}|Verschlüsselt (**1**) oder nicht verschlüsselt (**0**) die Arbeitsspeicher-Paging-Datei im Windows-Betriebssystem.<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|mftzone <Value>|Legt die Größe der MFT-Zone fest, und wird als ein Vielfaches von 200MB Einheiten ausgedrückt. Legen Sie *Wert* in eine Zahl von **1** (der Standardwert ist 200 MB) auf **4** (800 MB liegt).<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|memoryusage <Value>|Konfiguriert die internen Cache-Ebenen der NTFS-Poolspeicher und nicht ausgelagerten Poolspeicher NTFS. Legen Sie auf **1** oder **2**. Bei Festlegung auf **1** (Standardeinstellung), NTFS verwendet die Standarddauer ausgelagerten Poolspeicher zur Verfügung. Bei Festlegung auf **2**, NTFS erhöht die Größe der Lookaside Listen und Schwellenwerte für den Speicher. (Eine Lookaside-Liste ist ein Pool mit fester Größe Speicherpuffer, die der Kernel und von Gerätetreibern zu erstellen, wie private Zwischenspeicher für Dateisystemvorgänge wie z. B. das Lesen einer Datei.)<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|quotanotify <Frequency>|Konfiguriert die Häufigkeit kontingentverletzungen NTFS im Systemprotokoll gemeldet werden. Gültige Werte für liegen im Bereich 0 bis 4294967295. Das Standardintervall ist 3600 Sekunden (eine Stunde).<br /><br />Sie müssen Ihren Computer für diesen Parameter wirksam neu starten.|
|symlinkevaluation <SymbolicLinkType>|Steuert die Art der symbolische Verknüpfungen, die auf einem Computer erstellt werden können. Gültige Optionen sind:<br /><br />1.  Lokal auf dem lokalen symbolische Verknüpfungen, L2L: {0&#124;1}<br />2.  Lokale remote symbolische Verknüpfungen, L2R: {0&#124;1}<br />3.  Remoteinstanz durch, um lokale symbolische Verknüpfungen, R2R: {0&#124;1}<br />4.  Remoteinstanz durch, um remote symbolische Verknüpfungen, R2L: {0&#124;1}|
|DisableDeleteNotify|Deaktiviert die \( **1** \) oder aktiviert \( **0** \) Benachrichtigungen zu löschen. Benachrichtigung zum Löschen \(auch zuschneiden oder aufheben\) wird der Löschvorgang für einer Funktion, die das zugrunde liegenden Speichergerät der Cluster benachrichtigt, die aufgrund einer Datei freigegeben wurden. Beachten Sie auch Folgendes:<br /><br />– Für Systeme mit ReFS ist trim v2 standardmäßig deaktiviert. Gilt für WindowsServer 2016.<br />– Für Systeme mit ReFS ist trim v1 standardmäßig aktiviert. Gilt für WindowsServer 2012, Windows Server 2012 R2 und WindowsServer 2016.<br />– Für Systeme mit NTFS ist Trim standardmäßig aktiviert, es sei denn, ein Administrator deaktiviert.<br />– Wenn Ihr Festplattenlaufwerk oder SAN, meldet er unterstützt keine in der trim, und dann Ihr Festplattenlaufwerk und den SANs zuschnittbenachrichtigungen nicht abgerufen.<br />-Aktivieren oder deaktivieren, ist kein Neustart erforderlich.<br />-Trim ist effektiv, wenn es sich bei der nächsten aufheben Befehl ausgegeben wird.<br />– Vorhandene in-Flight e/a sind durch die Änderung der Registrierung nicht betroffen.<br />-Alle Neustart des Diensts erfordert keine, wenn Sie aktivieren oder deaktivieren trim.<br /><br />Dieser Parameter wurde in Windows Server 2008 R2 und Windows 7 eingeführt. | 

## <a name="remarks"></a>Hinweise

-   Die MFT-Zone ist ein reservierter Bereich, der es die Masterdateitabelle (MFT) ermöglicht, um nach Bedarf, um zu verhindern, dass bei der MFT-Fragmentierung zu erweitern. Wenn die durchschnittliche Größe der Dateien auf dem Volume 2 KB oder weniger beträgt, es vorteilhaft sein kann, legen Sie die **Mftzone** Wert auf 2. Wenn die durchschnittliche Größe der Dateien auf dem Volume 1 KB oder weniger, es vorteilhaft sein kann, legen Sie die **Mftzone** Wert 4.

-   Wenn **disable8dot3** nastaven NA hodnotu **0**, jedes Mal, erstellen Sie eine Datei mit einem langen Dateinamen, NTFS erstellt einen zweiten Eintrag zur Datei, die ein 8.3 Dateiname für die Zeichen aufweist. Wenn NTFS-Dateien in einem Verzeichnis erstellt, muss es die 8.3 Dateinamen Zeichen gesucht, die mit der langen Dateinamen verknüpft sind. Dieser Parameter aktualisiert die **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation** Registrierungsschlüssel.

-   Die **Allowextchar** parameterupdates der **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsAllowExtendedCharacterIn8dot3Name** Registrierungsschlüssel.

-   Die **Disablelastaccess** Parameter Reduzieren der Auswirkungen von Updates der Protokollierung zum Zeitpunkt des letzten Zugriffs Stempel für Dateien und Verzeichnisse. Deaktivieren der **Zeitpunkt des letzten Zugriffs** Feature verbessert die Geschwindigkeit von Datei- und Access. Dieser Parameter aktualisiert die **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate** Registrierungsschlüssel.

    Hinweise:

    -   Dateibasierte **Zeitpunkt des letzten Zugriffs** Abfragen sind genau, selbst wenn alle Werte der auf dem Datenträger nicht aktuell sind. NTFS Gibt den korrekten Wert für Abfragen, da der genaue Wert im Arbeitsspeicher gespeichert wird.

    -   Eine Stunde beträgt die maximale Zeitspanne NTFS Aktualisierung verzögert **Zeitpunkt des letzten Zugriffs** auf dem Datenträger. Wenn NTFS sonstige Dateiattribute wie z. B. aktualisiert **letzte Änderungszeit**, und ein **Zeitpunkt des letzten Zugriffs** Update steht, NTFS-Updates **Zeitpunkt des letzten Zugriffs** mit den anderen Updates ohne Weitere Leistungseinbußen.

    -   Die **Disablelastaccess** Parameter kann Programme z. B. Sicherung und Remotespeicher, die auf dieses Feature verlassen beeinflussen.

-   Erhöhen der physischen Speicher wird nicht immer der ausgelagerten Pool verfügbaren Arbeitsspeichermenge in NTFS erhöht. Festlegen von **Memoryusage** zu **2** löst den Grenzwert von ausgelagerten Poolspeicher zur Verfügung. Dies kann die Leistung verbessern, wenn Ihr System wird geöffnet, und Schließen von vielen Dateien in der gleichen Datei festgelegt und ist noch nicht verwenden große Mengen an Arbeitsspeicher für andere Anwendungen oder für den Cachespeicher. Wenn Ihr Computer bereits große Mengen an Arbeitsspeicher für andere Anwendungen oder für den Cachespeicher verwendet wird, erhöht den Grenzwert von NTFS ausgelagerten und nicht ausgelagerten Poolspeicher reduziert den verfügbaren Speicher für andere Prozesse. Dies kann die gesamtleistung des Systems reduzieren. Dieser Parameter aktualisiert die **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage** Registrierungsschlüssel.

-   Der Wert im angegebenen die **Mftzone** -Parameter ist eine Approximation der MFT plus die MFT-Zone auf einem neuen Volume die ursprüngliche Größe und zum Zeitpunkt der Bereitstellung für jedes Dateisystem festgelegt ist. Da Speicherplatz auf dem Volume verwendet wird, passt NTFS der Platz für zukünftiges Wachstum der MFT reserviert ist. Wenn die MFT-Zone groß ist, ist die Gesamtgröße der MFT-Zone nicht erneut reserviert. Da die MFT-Zone auf dem zusammenhängenden Bereich nach dem Ende der MFT basiert, wird es reduziert, wie der Speicherplatz verwendet wird.

    Das Dateisystem wird nicht den neuen Speicherort der MFT-Zone bestimmt, bis die aktuelle MFT-Zone vollständig verwendet wird. Beachten Sie, dass dies niemals in einem typischen System auftritt.

-   Einige Geräte können Leistungseinbußen auftreten, wenn die Funktion für die Delete-Benachrichtigung aktiviert ist. In diesem Fall verwenden Sie die **Disabledeletenotify** Option aus, um die Funktion für die Benachrichtigung deaktivieren.

### <a name="BKMK_examples"></a>Beispiele für
Die Abfrage für das Deaktivieren 8.3-Name-Verhalten für ein Datenträgervolume, angegeben durch die GUID, {928842df-5a01-11de-a85c-806e6f6e6963}, geben Sie Folgendes ein:

```
fsutil behavior query disable8dot3 Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

Sie können auch das Verhalten der 8.3-Namen mithilfe von Abfragen die **8dot3name** Unterbefehl.

Um die Abfrage an das System, um festzustellen, ob das Kürzen aktiviert ist, geben Sie Folgendes ein:

```
fsutil behavior query DisableDeleteNotify
```
Dies ergibt eine Ausgabe wie folgt:

    NTFS DisableDeleteNotify = 1
    ReFS DisableDeleteNotify is not currently set

Überschreiben Sie das Standardverhalten für TRIM \(Disabledeletenotify\) ReFS v2 eingeben:

```
fsutil behavior set DisableDeleteNotify ReFS 0
```

Überschreiben Sie das Standardverhalten für TRIM \(Disabledeletenotify\) NTFS und ReFS v1 eingeben:
```
fsutil behavior set DisableDeleteNotify 1
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Fsutil 8dot3name](Fsutil-8dot3name.md)


