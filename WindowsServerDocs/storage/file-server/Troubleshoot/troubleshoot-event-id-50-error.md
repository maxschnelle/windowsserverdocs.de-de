---
title: Beheben der Fehlermeldung mit der Ereignis-ID 50
description: Beschreibt, wie die Fehlermeldung mit der Ereignis-ID 50 behoben wird.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 7ce3551b60450a3720c9350b5c55f396368490c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815233"
---
# <a name="troubleshoot-the-event-id-50-error-message"></a>Beheben der Fehlermeldung mit der Ereignis-ID 50

##  <a name="symptoms"></a>Symptome

Wenn Informationen auf den physischen Datenträger geschrieben werden, werden möglicherweise die folgenden beiden Ereignismeldungen im System Ereignisprotokoll protokolliert: 

```
Event ID: 50 
Event Type: Warning 
Event Source: Ftdisk 
Description: {Lost Delayed-Write Data} The system was attempting to transfer file data from buffers to \Device\HarddiskVolume4. The write operation failed, and only some of the data may have been written to the file.
Data: 
0000: 00 00 04 00 02 00 56 00 
0008: 00 00 00 00 32 00 04 80 
0010: 00 00 00 00 00 00 00 00 
0018: 00 00 00 00 00 00 00 00 
0020: 00 00 00 00 00 00 00 00 
0028: 11 00 00 80 
```

```
Event ID: 26 
Event Type: Information
Event Source: Application Popup
Description: Windows - Delayed Write Failed : Windows was unable to save all the data for the file \Device\HarddiskVolume4\Program Files\Microsoft SQL Server\MSSQL$INSTANCETWO\LOG\ERRORLOG. The data has been lost. This error may be caused by a failure of your computer hardware or network connection.

Please try to save this file elsewhere.
```

Diese Ereignis-ID-Meldungen bedeuten genau dasselbe und werden aus denselben Gründen generiert. Für den Zweck dieses Artikels wird nur die Meldung Ereignis-ID 50 beschrieben.

> [!NOTE] 
> Das Gerät und der Pfad in der Beschreibung und die spezifischen hexadezimalen Daten variieren. 

##  <a name="more-information"></a>Weitere Informationen

Eine Meldung mit Ereignis-ID 50 wird protokolliert, wenn ein generischer Fehler auftritt, wenn Windows versucht, Informationen auf den Datenträger zu schreiben. Dieser Fehler tritt auf, wenn von Windows versucht wird, Daten aus dem Dateisystem-Cache-Manager (nicht dem Hardware Level-Cache) auf den physischen Datenträger zu übertragen Dieses Verhalten ist Teil der Speicherverwaltung von Windows. Wenn ein Programm z. b. eine Schreib Anforderung sendet, wird die Schreib Anforderung vom Cache-Manager zwischengespeichert, und dem Programm wird mitgeteilt, dass der Schreibvorgang erfolgreich abgeschlossen wurde. Der Cache-Manager versucht zu einem späteren Zeitpunkt, die Daten auf den physischen Datenträger zu schreiben. Wenn der Cache-Manager versucht, die Daten auf die Festplatte zu übertragen, tritt beim Schreiben der Daten ein Fehler auf, und die Daten werden aus dem Cache geleert und verworfen. Die Rück schreibe Speicherung verbessert die Systemleistung, aber der Verlust von Datenverlusten und der volumeintegrität kann aufgrund verlorener verzögerter Schreibfehler auftreten.

Beachten Sie, dass nicht alle e/a-Vorgänge von Cache-Manager gepufferte e/a-Vorgänge sind. Programme können ein FILE_FLAG_NO_BUFFERING Flag festlegen, das den Cache-Manager umgeht. Wenn SQL kritische Schreibvorgänge in einer Datenbank durchführt, wird dieses Flag festgelegt, um sicherzustellen, dass die Transaktion direkt auf dem Datenträger abgeschlossen wird. Beispielsweise führen nicht kritische Schreibvorgänge in Protokolldateien gepufferte e/a-Vorgänge aus, um die Gesamtleistung zu verbessern. Eine Meldung mit der Ereignis-ID 50 ergibt niemals eine nicht gepufferte e/a.

Es gibt mehrere verschiedene Quellen für eine Meldung mit der Ereignis-ID 50. Eine Ereignis-ID 50-Nachricht, die von einer MRxSmb-Quelle protokolliert wird, tritt beispielsweise auf, wenn ein Problem mit der Netzwerkverbindung mit dem Redirector vorliegt. Um zu vermeiden, dass falsche Schritte zur Problembehandlung ausgeführt werden, sollten Sie die Meldung Ereignis-ID 50 überprüfen, um zu bestätigen, dass Sie auf ein Datenträger-e/a-Problem verweist und dass dieser Artikel

Eine Meldung mit der Ereignis-ID 50 ähnelt der Ereignis-ID 9 und der Meldung Ereignis-ID 11. Obwohl der Fehler nicht so ernst ist wie der von der Ereignis-ID 9 und der Meldung Ereignis-ID 11 dargestellte Fehler, können Sie dieselben Problem Behandlungstechniken für eine Meldung mit der Ereignis-ID 50 verwenden, wie bei der Ereignis-ID 9 und der Meldung "Ereignis-ID 11". Denken Sie jedoch daran, dass alles im Stapel verlorene Schreibvorgänge verursachen kann, z. b. Filtertreiber und Mini Port Treiber. 

Sie können die Binärdaten verwenden, die mit einem begleitenden "Disk"-Fehler (angegeben durch die Ereignis-ID 9, 11, 51-Fehlermeldung oder andere Meldungen) verknüpft sind, um Sie bei der Identifizierung des Problems zu unterstützen.

###  <a name="how-to-decode-the-data-section-of-an-event-id-50-event-message"></a>Decodieren des Daten Abschnitts einer Ereignismeldung mit Ereignis-ID 50 

Wenn Sie den Daten Abschnitt im Beispiel für eine Meldung mit Ereignis-ID 50 decodieren, die im Abschnitt "Zusammenfassung" enthalten ist, sehen Sie, dass der Versuch, einen Schreibvorgang auszuführen, fehlgeschlagen ist, da das Gerät ausgelastet war und die Daten verloren gingen. In diesem Abschnitt wird beschrieben, wie Sie diese Ereignis-ID 50-Nachricht decodieren. 

In der folgenden Tabelle wird beschrieben, was jeder Offset dieser Nachricht darstellt: 

|Offsetlängen Values|Länge|Werte|
|-----------|------------|---------|
|0x00|2|Nicht verwendet|
|0x02|2|Sicherungsdaten Größe = 0x0004|
|0x04|2|Anzahl von Zeichen folgen = 0x0002|
|0x06|2|Offset in Zeichen folgen|
|0x08|2|Ereigniskategorie|
|0x0c|4|NTSTATUS-Fehler Code = 0x80040032 = IO_LOST_DELAYED_WRITE|
|0x10|8|Nicht verwendet|
|0x18|8|Nicht verwendet|
|0x20|8|Nicht verwendet|
|0x28|4|NT-Status-Fehlercode|

#### <a name="key-sections-to-decode"></a>Zu decodierende Schlüsselabschnitte

**Der Fehler Code**

Im Beispiel im Abschnitt "Zusammenfassung" wird der Fehlercode in der zweiten Zeile aufgeführt. Diese Zeile beginnt mit "0008:" und enthält die letzten vier Bytes in dieser Zeile: 0008:00 00 00 00 32 00 04 80 in diesem Fall lautet der Fehlercode 0x80040032. Der folgende Code ist der Code für den Fehler 50, der für alle Ereignis-ID 50-Meldungen identisch ist: IO_LOST_DELAYED_WRITEWARNINGNote Wenn Sie die hexadezimal Daten in der Ereignis-ID in den Statuscode umwandelt, beachten Sie, dass die Werte im Little-Endian-Format dargestellt werden.

**Ziel Datenträger**

Sie können den Datenträger, auf den der Schreibvorgang durchgeführt wurde, mithilfe der symbolischen Verknüpfung ermitteln, die auf dem Laufwerk im Abschnitt "Beschreibung" der Ereignis-ID-Nachricht aufgeführt ist, z. b.: \Device\HarddiskVolume4. Weitere Informationen zum Identifizieren des Laufwerks erhalten Sie, indem Sie auf die folgende Artikelnummer klicken, um den Artikel in der Microsoft Knowledge Base anzuzeigen: [159865](/EN-US/help/159865) unterscheiden eines physischen Datenträgers von einer Ereignismeldung

**Der endgültige Status Code**

Der endgültige Statuscode ist die wichtigste Information in der Ereignis-ID 50-Nachricht. Dies ist der Fehlercode, der zurückgegeben wird, wenn die e/a-Anforderung erfolgt ist, und ist die wichtigste Informationsquelle. Im Beispiel im Abschnitt "Summary" (Zusammenfassung) ist der abschließende Statuscode bei 0x28, der sechsten Zeile, die mit "0028:" beginnt, und enthält die einzigen vier Oktette in dieser Zeile: 

```
0028: 11 00 00 80 
```

In diesem Fall ist der endgültige Status "0x80000011". Dieser Statuscode wird STATUS_DEVICE_BUSY zugeordnet und impliziert, dass das Gerät momentan ausgelastet ist.

>[!NOTE] 
> Beachten Sie beim Umrechnen der hexadezimalen Daten in der Ereignis-ID 50-Nachricht in den Statuscode, dass die Werte im Little-Endian-Format dargestellt werden. Da der Statuscode die einzige Information ist, an der Sie interessiert sind, ist es möglicherweise einfacher, die Daten im Wörter Format anstelle von Bytes anzuzeigen. Wenn Sie dies tun, weisen die Bytes das richtige Format auf, und die Daten können schneller interpretiert werden.

Klicken Sie hierzu im Fenster **Ereignis Eigenschaften** auf **Wörter** . In der Ansicht Daten Wörter würde das Beispiel im Abschnitt "Symptome" wie folgt lauten: Data: 

```
() Bytes (.) 
Words 0000: 00040000 00560002 00000000 80040032 0010: 00000000 00000000 00000000 00000000 0020: 00000000 00000000 80000011
```

Informationen zum Abrufen einer Liste von Windows NT-Statuscodes finden Sie unter NTSTATUS. H im Windows Software Developer Kit (SDK).