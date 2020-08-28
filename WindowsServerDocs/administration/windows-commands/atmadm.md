---
title: atmadm
description: Referenz Artikel für den atmadm-Befehl, der die Verbindungen und Adressen überwacht, die vom ATM-Telefon-Manager in einem Netzwerk mit einem asynchronen Übertragungsmodus (ATM) registriert werden.
ms.topic: reference
ms.assetid: 37156c2e-c4d4-4fd8-a03d-245fb60bf996
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b79ecdad00872cb67beb38b7cfe35bbd2c45379e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029268"
---
# <a name="atmadm"></a>atmadm

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überwacht die Verbindungen und Adressen, die vom ATM-Telefon-Manager in einem Netzwerk mit einem Netzwerk im asynchronen Übertragungsmodus (ATM) registriert werden. Sie können " **atmadm** " verwenden, um Statistiken für eingehende und ausgehende Aufrufe von atM-Adaptern anzuzeigen. **Atmadm** wird ohne Parameter verwendet und zeigt Statistiken zum Überwachen des Status aktiver atM-Verbindungen an.

## <a name="syntax"></a>Syntax

```
atmadm [/c][/a][/s]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| /C | Zeigt die Telefon Informationen für alle aktuellen Verbindungen mit dem auf diesem Computer installierten atM-Netzwerkadapter an. |
| /a | Zeigt die registrierte Netzwerkdienst-Netzwerkdienst-Netzwerkadresse (Network Service Access Point, NSAP) für jeden auf diesem Computer installierten Adapter an. |
| /s | Zeigt eine Statistik zum Überwachen des Status aktiver atM-Verbindungen an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="remarks"></a>Bemerkungen

- Der Befehl **atmadm/c** erzeugt eine Ausgabe ähnlich der folgenden:

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

    Die folgende Tabelle enthält Beschreibungen der einzelnen Elemente in der/c-Beispielausgabe von **atmadm** .

    | Datentyp | Bildschirm Anzeige | Beschreibung |
    | -------- | --------- | -------- |
    | Verbindungsinformationen | Ein/Aus | Die Richtung des Aufrufes. **In** ist der atM-Netzwerkadapter von einem anderen Gerät aus.  **Out** ist vom atM-Netzwerkadapter auf ein anderes Gerät. |
    | PMP | Punkt-zu-Multipoint-Aufrufe. |
    | p-p | Punkt-zu-Punkt-Aufrufe. |
    | SVC | Die Verbindung befindet sich in einer umschwechselten virtuellen Verbindung. |
    | Angebotene | Die Verbindung befindet sich in einer permanenten virtuellen Verbindung. |
    | VPI/VCI-Informationen | VPI/VCI | Virtueller Pfad und virtueller Kanal des eingehenden oder ausgehenden Aufrufes. |
    | Remote Adresse/Medien Parameter | 47000580ffe1000000f21a2e180000c110081500 | NSAP-Adresse des aufrufenden **(in)** oder aufgerufenen **(Out)** atM-Geräts. |
    | Llte | Der Parameter **TX** umfasst die folgenden drei Elemente:<ul><li>Der Standard-oder der angegebene Bitrate-Typ (UBR, CBR, VBR oder ABR)</li><li>Standard-oder angegebene Zeilen Geschwindigkeit</li><li>Die angegebene SDU-Größe (Service Data Unit).</li></ul> |
    | Rx | Der **RX** -Parameter umfasst die folgenden drei Elemente:<ul><li>Der Standard-oder der angegebene Bitrate-Typ (UBR, CBR, VBR oder ABR)</li><li>Standard-oder angegebene Zeilen Geschwindigkeit</li><li>Die angegebene SDU-Größe.</li></ul> |

- Der Befehl **atmadm/a** erzeugt eine Ausgabe ähnlich der folgenden:

    ```
    Windows atM call Manager Statistics
    atM addresses for Interface : [009] Olicom atM PCI 155 Adapter
    47000580FFE1000000F21A2E180000C110081500
    ```

- Der Befehl **atmadm/s** erzeugt eine Ausgabe ähnlich der folgenden:

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

    Die folgende Tabelle enthält Beschreibungen der einzelnen Elemente in der/s-Beispielausgabe von **atmadm** .

    | Statistik zum CallManager | Beschreibung |
    | ------------- | -------- |
    | Aktuelle aktive Aufrufe | Aufrufe, die zurzeit auf dem auf diesem Computer installierten atM-Adapter aktiv sind. |
    | Gesamtanzahl erfolgreicher eingehender Aufrufe | Aufrufe, die von anderen Geräten in diesem atM-Netzwerk erfolgreich empfangen wurden. |
    | Erfolgreiche ausgehende Aufrufe gesamt | Aufrufe wurden von diesem Computer aus an andere atM-Geräte in diesem Netzwerk erfolgreich abgeschlossen. |
    | Nicht erfolgreiche eingehende Aufrufe | Eingehende Aufrufe, bei denen keine Verbindung mit diesem Computer hergestellt werden konnte. |
    | Nicht erfolgreiche ausgehende Aufrufe | Ausgehende Aufrufe, bei denen keine Verbindung mit einem anderen Gerät im Netzwerk hergestellt werden konnte. |
    | Durch Remote geschlossene Aufrufe | Aufrufe, die von einem Remote Gerät im Netzwerk geschlossen werden. |
    | Lokal geschlossene Aufrufe | Aufrufe, die von diesem Computer geschlossen werden. |
    | Signalisierung und gesendete ILMI-Pakete | Anzahl der integrierten ILMI-Pakete (Local Management Interface), die an den Switch gesendet werden, mit dem dieser Computer eine Verbindung herstellt. |
    | Signalisierungs-und ILMI-Pakete empfangen | Anzahl der vom atM-Schalter empfangenen ILMI-Pakete. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Aufrufen von Informationen für alle aktuellen Verbindungen mit dem auf diesem Computer installierten atM-Netzwerkadapter anzuzeigen:

```
atmadm /c
```

Geben Sie Folgendes ein, um die registrierte NSAP-Adresse (Network Service Access Point) für die einzelnen Adapter anzuzeigen, die auf diesem Computer installiert sind:

```
atmadm /a
```

Geben Sie Folgendes ein, um Statistiken zum Überwachen des Status aktiver atM-Verbindungen anzuzeigen:

```
atmadm /s
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
