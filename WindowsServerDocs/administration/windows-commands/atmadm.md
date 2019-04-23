---
title: atmadm
description: Windows-Befehle Thema **Atmadm** -Monitore Verbindungen und Adressen, die von einem Geldautomaten registriert werden, rufen Sie Manager in einem Netzwerk der asynchrone Übertragung-Modus (atM).
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37156c2e-c4d4-4fd8-a03d-245fb60bf996
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a8a8883bad9aa2abdc90d5db5702ef42f46c8a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831771"
---
# <a name="atmadm"></a>atmadm

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überwacht Verbindungen und Adressen, die von einem Geldautomaten registriert werden rufen eine asynchrone Übertragung Modus (atM) Netzwerk Manager. Sie können **Atmadm** zum Anzeigen von Statistiken für eingehende und ausgehende Aufrufe auf ATM-Netzwerkadaptern. Ohne Parameter verwendet **Atmadm** werden Statistiken für das Überwachen des Status von aktiven atM-Verbindungen angezeigt. 

## <a name="syntax"></a>Syntax

```
atmadm [/c][/a][/s]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|/c|Zeigt rufen Sie Informationen für alle aktuellen Verbindungen mit den atM-Netzwerkadapter, die auf diesem Computer installiert.|
|/a|Zeigt die registrierten atM-netzwerkdienstzugriff zeigen (NSAP)-Adresse für die einzelnen Adapter auf diesem Computer installiert.|
|/s|Zeigt Statistiken für das Überwachen des Status von aktiven atM-Verbindungen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Die **Atmadm/c** Befehl erzeugt eine Ausgabe ähnlich der folgenden:

    ```
    Windows atM call Manager Statistics
    atM Connections on Interface : [009] Olicom atM PCI 155 Adapter
       Connection   VPI/VCI   remote address/
                              Media Parameters (rates in bytes/sec)
       In  PMP SVC    0/193   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 0,Avg 0,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       Out P-P SVC    0/192   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       In  PMP SVC    0/191   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 0,Avg 0,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       Out P-P SVC    0/190   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       In  P-P SVC    0/475   47000580FFE1000000F21A2E180000C110081501
                              Tx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9188
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 9188
       Out PMP SVC    0/194   47000580FFE1000000F21A2E180000C110081501 (0)
                              Tx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9180
                              Rx:UBR,Peak 0,Avg 0,MaxSdu 0
       Out P-P SVC    0/474   4700918100000000613E5BFE010000C110081500
                              Tx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9188
                              Rx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9188
       In  PMP SVC    0/195   47000580FFE1000000F21A2E180000C110081500
                              Tx:UBR,Peak 0,Avg 0,MaxSdu 0
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 9180
    ```
    
    Die folgende Tabelle enthält Beschreibungen der einzelnen Elemente in der **Atmadm/c** Beispielausgabe.
    
    |Typ der Daten|Bildschirmanzeige|Beschreibung|
    |--------|---------|--------|
    |Verbindungsinformationen|Eingabe/Ausgabe|die Richtung des Aufrufs.  **In** atM-Netzwerkadapter von einem anderen Gerät ist.  **Out** liegt zwischen den atM-Netzwerkadapter und ein anderes Gerät.|
    ||PMP|Punkt-zu-Multipoint-Aufruf.|
    ||P-P|PPP-Aufruf.|
    ||SVC|Verbindung ist zu einer virtuellen switched-Verbindung.|
    ||PVC|Verbindung ist auf einen PVC.|
    |VPI/VCI-Informationen|VPI/VCI|Virtuellen Pfad und den Kanal des eingehenden oder ausgehenden aufrufen.|
    |Remote-Adresse/Media-Parameter|47000580FFE1000000F21A2E180000C110081500|NSAP-Adresse der aufrufenden **(In)** oder aufgerufen **(verkleinern)** atM Gerät.|
    ||**Tx**|Die **Tx** Parameter enthält die folgenden drei Elemente:<br /><br />– Default oder angegeben Bitrate (UBR, CBR, VBR oder ABR)<br />– Default oder Übertragungsrate der Leitung angegeben<br />-Die angegebenen Daten Einheitengröße (SDU)|
    ||**Rx**|Die **Rx** Parameter enthält die folgenden drei Elemente:<br /><br />– Default oder angegeben Bitrate (UBR, CBR, VBR oder ABR)<br />– Default oder Übertragungsrate der Leitung angegeben<br />-Die angegebenen SDU-Größe|
    
- Die **Atmadm/a** Befehl erzeugt eine Ausgabe ähnlich der folgenden:

    ```
    Windows atM call Manager Statistics
    atM addresses for Interface : [009] Olicom atM PCI 155 Adapter
    47000580FFE1000000F21A2E180000C110081500
    ```
    
- Die **Atmadm/s** Befehl erzeugt eine Ausgabe ähnlich der folgenden:

    ```
    Windows atM call Manager Statistics
    atM call Manager statistics for Interface : [009] Olicom atM PCI 155 Adapter
    Current active calls                        = 4
    Total successful Incoming calls             = 1332
    Total successful Outgoing calls             = 1297
    Unsuccessful Incoming calls                 = 1
    Unsuccessful Outgoing calls                 = 1
    calls Closed by remote                      = 1302
    calls Closed Locally                        = 1323
    Signaling and ILMI Packets Sent            = 33655
    Signaling and ILMI Packets Received        = 34989
    ```
    
    Die folgende Tabelle enthält Beschreibungen der einzelnen Elemente in der **Atmadm/s** Beispielausgabe.
    
    |Rufen Sie die Statistik für Manager|Beschreibung|
    |-------------|--------|
    |Aktuelle aktive Anrufe|Ruft die derzeit aktiven auf dem atM-Adapter auf diesem Computer installiert.|
    |Anzahl erfolgreicher|Aufrufe von anderen Geräten im Netzwerk ATM-erfolgreich empfangen.|
    |Anzahl erfolgreicher|Aufrufe, die mit anderen ATM-Geräten im Netzwerk auf diesem Computer erfolgreich abgeschlossen wurde.|
    |Erfolgr|Eingehende Anrufe, die Fehler bei der verbindungsherstellung mit diesem Computer.|
    |Erfolgr|Ausgehende Anrufe, die Fehler bei der verbindungsherstellung zu einem anderen Gerät im Netzwerk.|
    |Closed Aufrufen remote|Aufrufe, die von einem Remotegerät im Netzwerk geschlossen.|
    |Ruft lokal geschlossen|Aufrufe, die von diesem Computer beendet.|
    |Signalisierung und ILMI-Pakete|Anzahl der integrierten lokalen Verwaltung ILMI (Interface)-Pakete, die mit dem Switch gesendet, der diesen Computer versucht, eine Verbindung herstellen.|
    |Signalisierung und ILMI-Pakete|Anzahl der ILMI-Pakete aus dem ATM-Schalter.|
    
## <a name="BKMK_Examples"></a>Beispiele für

Zum Anzeigen von Aufrufinformationen für alle aktuellen Verbindungen zu den atM-Netzwerkadapter, die auf diesem Computer installiert, geben Sie Folgendes ein:

```
atmadm /c
```

Um die registrierten ATM-Dienst Zugriff Point (NSAP) Netzwerkadresse für die einzelnen Adapter auf diesem Computer installierten anzuzeigen, geben Sie Folgendes ein:

```
atmadm /a
```

Um Statistiken für das Überwachen des Status von aktiven atM-Verbindungen anzuzeigen, geben Sie Folgendes ein:

```
atmadm /s
```

## <a name="additional-references"></a>Weitere Verweise

- [Befehlszeilensyntax](command-line-syntax-key.md)
