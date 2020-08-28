---
title: fsutil-Verhalten
description: Referenz Artikel für den Befehl "bsutil Behavior", der das NTFS-volumeverhalten abfragt oder festlegt.
manager: dmoss
ms.author: toklima
author: toklima
ms.topic: reference
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b
ms.openlocfilehash: 223a326a5ac60dfdb88c20ca3541b0128cf0943e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030168"
---
# <a name="fsutil-behavior"></a>fsutil-Verhalten

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Fragt das NTFS-volumeverhalten ab oder legt es fest, einschließlich:

- Erstellen der 8,3-Dateinamen für die Zeichen Länge.

- Erweitern der Zeichen Verwendung in 8,3 kurzen Dateinamen mit Zeichen Länge auf NTFS-Volumes.

- Aktualisieren des Zeitstempels des **letzten Zugriffs** , wenn Verzeichnisse auf NTFS-Volumes aufgelistet sind.

- Die Häufigkeit, mit der Kontingent Ereignisse in das System Protokoll und den nicht auslagerten NTFS-Pool und die Speicher Cache Ebenen für nicht auslagerbare NTFS-Pools geschrieben werden.

- Die Größe der Master dateitabellenzone (MFT-Zone).

- Automatisches Löschen von Daten, wenn das System auf einem NTFS-Volume beschädigt ist.

- Datei Lösch Benachrichtigung (auch als Trim oder unmap bezeichnet).

## <a name="syntax"></a>Syntax

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<volumepath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <value> | [<volumepath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <frequency> | symlinkevaluation <symboliclinktype> | disabledeletenotify {1|0}}
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |------------ |
| Abfrage | Fragt die Verhaltensparameter des Dateisystems ab. |
| set | Ändert die Verhaltensparameter des Dateisystems. |
| Zuordnung `{1|0}` | Ermöglicht (**1**) oder verweigert (**0**) Zeichen aus dem erweiterten Zeichensatz (einschließlich diakritischer Zeichen), der in 8,3-kurzen Dateinamen auf NTFS-Volumes verwendet werden soll.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| Bugcheckonbeschädigt `{1|0}` | Ermöglicht (**1**) oder nicht die Generierung einer Fehlerüberprüfung (**0**), wenn auf einem NTFS-Volume eine Beschädigung vorliegt. Diese Funktion kann verwendet werden, um zu verhindern, dass NTFS Daten im Hintergrund löscht, wenn Sie mit der Funktion für die Selbstreparatur von NTFS verwendet werden.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| disable8dot3 [ <volumepath> ] `{1|0}` | Deaktiviert (**1**) oder aktiviert (**0**) die Erstellung von Dateinamen mit einer Länge von 8,3 Zeichen in FAT-und NTFS-formatierten Volumes. Optional können Sie den *volumepath* als Laufwerk Namen, gefolgt von einem Doppelpunkt oder einer GUID, als Präfix angeben. |
| disablecompression `{1|0}` | Deaktiviert **(1)** oder aktiviert **(0)** NTFS-Komprimierung.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| disablecompressionlimit `{1|0}` | Deaktiviert **(1)** oder aktiviert **(0)** NTFS-Komprimierungs Limit für das NTFS-Volume. Wenn eine komprimierte Datei eine bestimmte Fragmentierung erreicht, anstatt die Datei zu erweitern, beendet NTFS die Komprimierung zusätzlicher Blöcke der Datei. Dies wurde durchgeführt, damit komprimierte Dateien größer sind als normal. Wenn dieser Wert auf **true** festgelegt wird, wird diese Funktion deaktiviert, wodurch die Größe der komprimierten Dateien auf dem System beschränkt wird. Es wird nicht empfohlen, diese Funktion zu deaktivieren.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| DisableEncryption `{1|0}` | Deaktiviert **(1)** oder aktiviert **(0)** die Verschlüsselung von Ordnern und Dateien auf NTFS-Volumes.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| disablefilemetadataoptimization `{1|0}` | Deaktiviert **(1)** oder aktiviert **(0)** die Datei-metadatenoptimierung. NTFS hat eine Beschränkung für die Anzahl von Blöcken, die eine bestimmte Datei aufweisen kann. Komprimierte und sparsesdateien können stark fragmentiert werden. Standardmäßig komprimiert NTFS seine internen Metadatenstrukturen in regelmäßigen Abständen, um mehr fragmentierte Dateien zu ermöglichen. Wenn dieser Wert auf **true** festgelegt wird, wird diese interne Optimierung deaktiviert. Es wird nicht empfohlen, diese Funktion zu deaktivieren.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| disablelastaccess `{1|0}` | Deaktiviert (**1**) oder aktiviert (**0**) Aktualisierungen des letzten Zugriffszeit Stempels in jedem Verzeichnis, wenn Verzeichnisse auf einem NTFS-Volume aufgelistet sind.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| disablespotkorruptionhandling `{1|0}` | Deaktiviert **(1)** oder aktiviert **(0)** Beschädigung der Beschädigung. Ermöglicht Systemadministratoren außerdem das Ausführen von CHKDSK, um den Status eines Volumes zu analysieren, ohne es offline schalten zu müssen. Es wird nicht empfohlen, diese Funktion zu deaktivieren.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| disabletxf `{1|0}` | Deaktiviert **(1)** oder aktiviert **(0)** TxF auf dem angegebenen NTFS-Volume. TxF ist ein NTFS-Feature, das Transaktionen wie Semantik für Dateisystem Vorgänge bereitstellt. TxF ist derzeit veraltet, aber die Funktionalität ist weiterhin verfügbar. Es wird nicht empfohlen, diese Funktion auf dem Volume "C:" zu deaktivieren.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| disableschreiteautotiering `{1|0}` | Deaktiviert die automatische Aktivierung von refs v2 für mehrstufige Volumes.<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| verschlüsseltpagingfile `{1|0}` | Verschlüsselt (**1**) oder verschlüsselt die Speicher Auslagerungs Datei im Windows-Betriebssystem nicht (**0**).<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| MF-Datei `<value>` | Legt die Größe der MFT-Zone fest und wird als Vielfaches von 200-MB-Einheiten angegeben. Legen Sie den Wert auf eine Zahl von **1** fest (der Standardwert ist 200 MB) bis **4** (der höchst *Wert* beträgt 800 MB).<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| memoryusage `<value>` | Konfiguriert die internen Cache Ebenen für den Speicher des NTFS-Auslagerungs Pools und den Speicher für nicht auslagerbare NTFS-Pools. Legen Sie auf **1** oder **2**fest. Wenn der Wert auf **1** festgelegt ist (Standardeinstellung), verwendet NTFS die Standardgröße des Arbeitsspeichers für Auslagerungs Pools. Wenn der Wert auf **2**festgelegt ist, vergrößert NTFS die Größe seiner Lookaside-Listen und Arbeitsspeicher Schwellenwerte. (Eine Lookaside-Liste ist ein Pool von Speicher Puffern fester Größe, die der Kernel und die Gerätetreiber als private Speicher Caches für Dateisystem Vorgänge erstellen, z. b. das Lesen einer Datei.)<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| quotanotify `<frequency>` | Konfiguriert, wie oft NTFS-Kontingent Verletzungen im System Protokoll gemeldet werden. Gültige Werte für liegen im Bereich von **0 – 4294967295**. Die Standard Häufigkeit beträgt **3600** Sekunden (eine Stunde).<p>Sie müssen den Computer neu starten, damit dieser Parameter wirksam wird. |
| symlinkevaluation `<symboliclinktype>` | Steuert die Art von symbolischen Verknüpfungen, die auf einem Computer erstellt werden können. Folgende Optionen sind gültig:<ul><li>**1** -lokale und lokale symbolische Links, `L2L:{0|1}`</li><li>**2** -lokale zu-Remote-symbolische Verknüpfungen, `L2R:{1|0}`</li><li>**3** : Symbol Verknüpfungen für Remote-zu-lokal `R2R:{1|0}`</li><li>**4** -symbolische Links zu Remote-zu-Remote `R2L:{1|0}`</li></ul> |
| disabledeletenotify | Deaktiviert (**1**) oder aktiviert (**0**) Benachrichtigungen löschen. DELETE-Benachrichtigungen (auch als Trim oder unmap bezeichnet) ist ein Feature, das das zugrunde liegende Speichergerät von Clustern benachrichtigt, die aufgrund eines Datei Löschvorgangs freigegeben wurden. Außerdem:<ul><li>Für Systeme, die refs v2 verwenden, ist Trim standardmäßig deaktiviert.</li><li>Für Systeme, die refs v1 verwenden, ist Trim standardmäßig aktiviert.</li><li>Für Systeme, die NTFS verwenden, ist Trim standardmäßig aktiviert, es sei denn, Sie werden von einem Administrator deaktiviert.</li><li>Wenn Ihr Festplattenlaufwerk oder San meldet, dass Trim nicht unterstützt wird, erhalten die Festplatte und die Sans keine Trim-Benachrichtigungen.</li><li>Die Aktivierung oder Deaktivierung erfordert keinen Neustart.</li><li>Trim ist wirksam, wenn der nächste aufheben-Befehl ausgegeben wird.</li><li>Vorhandene Flight-e/a sind von der Registrierungs Änderung nicht betroffen.</li><li>Erfordert keinen Dienst Neustart, wenn Sie Trim aktivieren oder deaktivieren.</li></ul> |

#### <a name="remarks"></a>Bemerkungen

- Die MFT-Zone ist ein reservierter Bereich, der es ermöglicht, dass die Master Dateitabelle (MFT) nach Bedarf erweitert wird, um die MFT-Fragmentierung zu verhindern. Wenn die durchschnittliche Dateigröße auf dem Volume 2 KB oder weniger beträgt, kann es vorteilhaft sein, den **mftzone** -Wert auf **2**festzulegen. Wenn die durchschnittliche Dateigröße auf dem Volume mindestens 1 KB beträgt, kann es vorteilhaft sein, den **mftzone** -Wert auf **4**festzulegen.

- Wenn **disable8dot3** auf **0**festgelegt ist, erstellt NTFS jedes Mal, wenn Sie eine Datei mit einem langen Dateinamen erstellen, einen zweiten Datei Eintrag mit einem Dateinamen, der aus 8,3 Zeichen besteht. Wenn NTFS Dateien in einem Verzeichnis erstellt, muss es die 8,3-Dateinamen nachschlagen, die den langen Dateinamen zugeordnet sind. Mit diesem Parameter wird der Registrierungsschlüssel " **hklm\system\currentcontrolset\control\filesystem\ntfsdisable8dot3namecreations** " aktualisiert.

- Mit dem Parameter " **zugswextchar** " wird der Registrierungsschlüssel " **hklm\system\currentcontrolset\control\filesystem\ntf-Name** " aktualisiert.

- Der **disablelastaccess** -Parameter reduziert die Auswirkungen der Protokollierung von Aktualisierungen auf den Zeitstempel des **letzten Zugriffs** auf Dateien und Verzeichnisse. Durch das Deaktivieren der **Zeit des letzten Zugriffs Zeitraums** wird die Geschwindigkeit des Datei-und Verzeichniszugriffs verbessert. Mit diesem Parameter wird der Registrierungsschlüssel " **hklm\system\currentcontrolset\control\filesystem\ntfsdisablelastaccessupdate** " aktualisiert.

    **Hinweise:**

    - Dateibasierte Zeit für den Zugriff auf den **letzten Zugriff** ist auch dann korrekt, wenn alle Werte auf dem Datenträger nicht aktuell sind. NTFS gibt den korrekten Wert für Abfragen zurück, da der genaue Wert im Arbeitsspeicher gespeichert wird.

    - Eine Stunde ist die maximale Zeitspanne, die NTFS die Aktualisierung des **letzten Zugriffs** auf dem Datenträger verzögern kann. Wenn NTFS andere Dateiattribute aktualisiert, wie z. b. die **Uhrzeit der letzten Änderung**, und ein **Zeitpunkt des letzten Zugriffs** auf das Update aussteht, aktualisiert NTFS den **Zeitpunkt des letzten Zugriffs** mit den anderen Updates ohne zusätzliche Beeinträchtigung der Leistung.

    - Der **disablelastaccess** -Parameter kann sich auf Programme wie z. b. die Sicherung und den Remote Speicher auswirken, die von diesem Feature abhängen.

- Wenn Sie den physischen Speicher vergrößern, erhöht sich nicht immer der für NTFS verfügbare Auslagerungs Pool. Durch Festlegen von **memoryusage** auf **2** wird das Limit für den auslagerungspoolarbeitsspeicher erhöht. Dies kann die Leistung verbessern, wenn Ihr System viele Dateien im gleichen Dateisatz öffnet und schließt und Sie nicht bereits große Mengen an System Arbeitsspeicher für andere apps oder den Cache Speicher verwenden. Wenn Ihr Computer bereits große Mengen an System Arbeitsspeicher für andere apps oder den Cache Speicher verwendet, verringert sich der verfügbare Pool Arbeitsspeicher für andere Prozesse, wenn Sie das Limit für den Auslagerungs-und nicht-Auslagerungs Pool von NTFS erhöhen. Dies kann die Gesamtleistung des Systems beeinträchtigen. Mit diesem Parameter wird der Registrierungsschlüssel " **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage** " aktualisiert.

- Der im **mftzone** -Parameter angegebene Wert ist ein Näherungswert für die anfängliche Größe des MFT zuzüglich der MFT-Zone auf einem neuen Volume und wird beim Bereitstellungs Zeitpunkt für jedes Dateisystem festgelegt. Wenn Speicherplatz auf dem Volume verwendet wird, passt NTFS den für das zukünftige MFT-Wachstum reservierten Speicherplatz an. Wenn die MFT-Zone bereits groß ist, ist die vollständige MFT-Zonen Größe nicht erneut reserviert. Da die MFT-Zone auf dem zusammenhängenden Bereich liegt, der hinter dem Ende der MFT liegt, verkleinert Sie sich, wenn der Speicherplatz verwendet wird.

    Das Dateisystem bestimmt nicht den neuen Speicherort der MFT-Zone, bis die aktuelle MFT-Zone vollständig genutzt wird. Beachten Sie, dass dies nie auf einem typischen System auftritt.

- Bei einigen Geräten treten Leistungseinbußen auf, wenn die Funktion zum Löschen von Benachrichtigungen aktiviert ist. Verwenden Sie in diesem Fall die Option **disabledeletenotify** , um das Benachrichtigungs Feature zu deaktivieren.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das "8.3-namens Verhalten" für ein mit der GUID angegebene Datenträger Volume ({928842df-5a01-11de-a85c-806e6f6e6963}) abzufragen:

```
fsutil behavior query disable8dot3 volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

Sie können das 8.3-namens Verhalten auch Abfragen, indem Sie den Unterbefehl **8dot3name** verwenden.

Um das System abzufragen, ob Trim aktiviert ist, geben Sie Folgendes ein:

```
fsutil behavior query DisableDeleteNotify
```

Dies ergibt eine Ausgabe ähnlich der folgenden:

```
NTFS DisableDeleteNotify = 1
ReFS DisableDeleteNotify is not currently set
```

Um das Standardverhalten für Trim (disabledeletenotify) für Refs v2 zu überschreiben, geben Sie Folgendes ein:

```
fsutil behavior set disabledeletenotify ReFS 0
```

Um das Standardverhalten für Trim (disabledeletenotify) für NTFS und Refs V1 zu überschreiben, geben Sie Folgendes ein:

```
fsutil behavior set disabledeletenotify 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [fsutil 8dot3name](fsutil-8dot3name.md)
