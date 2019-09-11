---
title: klist
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4689b4a9-1740-47dd-9240-02105efca428
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a8f574b65ec8c123379e1b02ee1571cc9f21fa1
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867055"
---
# <a name="klist"></a>klist



Zeigt eine Liste der derzeit zwischengespeicherten Kerberos-Tickets an. Diese Informationen gelten für Windows Server 2012. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
klist [-lh <LogonId.HighPart>] [-li <LogonId.LowPart>] tickets | tgt | purge | sessions | kcd_cache | get | add_bind | query_bind | purge_bind
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-LH|Gibt den hohen Teil des lokalen eindeutigen Bezeichners (LUID) des Benutzers an, ausgedrückt als hexadezimal. Wenn weder – LH noch – Li vorhanden ist, wird für den Befehl standardmäßig die LUID des aktuell angemeldeten Benutzers verwendet.|
|-Li|Gibt den unteren Teil des lokalen eindeutigen Bezeichners (LUID) des Benutzers an, ausgedrückt als hexadezimal. Wenn weder – LH noch – Li vorhanden ist, wird für den Befehl standardmäßig die LUID des aktuell angemeldeten Benutzers verwendet.|
|Tickets|Listet die derzeit zwischengespeicherten Ticket-Zuteilungs Tickets (TGTs) und Dienst Tickets der angegebenen Anmelde Sitzung auf. Dies ist die Standardoption.|
|TGT|Zeigt das erste Kerberos-TGT an.|
|Löschen|Hiermit können Sie alle Tickets der angegebenen Anmelde Sitzung löschen.|
|Besessenheit|Zeigt eine Liste der Anmelde Sitzungen auf diesem Computer an.|
|kcd_cache|Zeigt die Informationen zur eingeschränkten Kerberos-Delegierung im Cache an.|
|get|Ermöglicht das Anfordern eines Tickets für den Zielcomputer, der durch den Dienst Prinzipal Namen (SPN) angegeben wird.|
|add_bind|Ermöglicht es Ihnen, einen bevorzugten Domänen Controller für die Kerberos-Authentifizierung anzugeben.|
|query_bind|Zeigt eine Liste der zwischengespeicherten bevorzugten Domänen Controller für jede Domäne an, mit der Kerberos eine Verbindung hergestellt hat.|
|purge_bind|Entfernt die zwischengespeicherten bevorzugten Domänen Controller für die angegebenen Domänen.|
|kdcoptions|Zeigt die in RFC 4120 angegebenen Optionen für das Schlüsselverteilungscenter (KDC) an.|
|/?|Zeigt die Hilfe für diesen Befehl an.|

## <a name="remarks"></a>Hinweise

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins**oder einer entsprechenden Gruppe sein, um alle Parameter dieses Befehls ausführen zu können.

Wenn keine Parameter bereitgestellt werden, ruft klist alle Tickets für den aktuell angemeldeten Benutzer ab.

In den Parametern werden die folgenden Informationen angezeigt:
-   **Tickets**

    Listet die derzeit zwischengespeicherten Tickets von Diensten auf, für die Sie sich seit der Anmeldung authentifiziert haben. Zeigt die folgenden Attribute aller zwischengespeicherten Tickets an:  
    -   Anmelde-ID: Die LUID
    -   Client: Die Verkettung des Client namens und des Domänen Namens des Clients
    -   Server: Die Verkettung des Dienst namens und des Domänen Namens des Dienstanbieter
    -   Kerbticket-Verschlüsselungstyp: Der Verschlüsselungstyp, der zum Verschlüsseln des Kerberos-Tickets verwendet wird.
    -   Ticket-Flags: Die Kerberos-Ticket-Flags
    -   Startzeit: Der Zeitpunkt, ab dem das Ticket gültig ist.
    -   Endzeit: Der Zeitpunkt, zu dem das Ticket nicht mehr gültig ist. Wenn ein Ticket zu diesem Zeitpunkt abgelaufen ist, kann es nicht mehr verwendet werden, um sich bei einem Dienst zu authentifizieren oder für die Verlängerung zu verwenden.
    -   Erneuerungszeit: Der Zeitpunkt, zu dem eine neue anfängliche Authentifizierung erforderlich ist.
    -   Sitzungs Schlüsseltyp: Der Verschlüsselungsalgorithmus, der für den Sitzungsschlüssel verwendet wird.
-   **TGT**

    Listet das erste Kerberos-TGT und die folgenden Attribute des aktuell zwischengespeicherten Tickets auf:  
    -   Anmelde-ID: Identifiziert in Hexadezimal Zahl
    -   ServiceName: krbtgt
    -   TargetName \<-SPN >: krbtgt
    -   Domain Name Der Name der Domäne, die das TGT ausgibt.
    -   TargetDomainName: Die Domäne, für die das TGT ausgestellt wurde.
    -   Alttargetdomainname: Die Domäne, für die das TGT ausgestellt wurde.
    -   Ticket-Flags: Address-und Target-Aktionen und-Typ
    -   Sitzungsschlüssel: Schlüssellänge und Verschlüsselungsalgorithmus
    -   StartTime Uhrzeit des lokalen Computers, an dem das Ticket angefordert wurde
    -   EndTime Uhrzeit, zu der das Ticket nicht mehr gültig ist. Wenn ein Ticket zu diesem Zeitpunkt abgelaufen ist, kann es nicht mehr zum Authentifizieren bei einem Dienst verwendet werden.
    -   Erneuteste Verlängerung: Stichtag für die Verlängerung des Tickets
    -   Timeskew: Zeitunterschied mit dem Schlüsselverteilungscenter (KDC)
    -   Encode-Ticket: Codiertes Ticket
-   **ungs**

    Ermöglicht das Löschen eines bestimmten Tickets. Wenn Sie Tickets löschen, werden alle von Ihnen zwischengespeicherten Tickets zerstört. verwenden Sie daher dieses Attribut mit Vorsicht. Möglicherweise werden Sie nicht mehr in der Lage sein, sich bei Ressourcen zu authentifizieren. Wenn dies der Fall ist, müssen Sie sich ab-und wieder anmelden.  
    -   Anmelde-ID: Identifiziert in Hexadezimal Zahl
-   **Besessenheit**

    Ermöglicht das Auflisten und Anzeigen der Informationen für alle Anmelde Sitzungen auf diesem Computer.  
    -   Anmelde-ID: Wenn angegeben, wird die Anmelde Sitzung nur durch den angegebenen Wert angezeigt. Wenn nicht angegeben, werden alle Anmelde Sitzungen auf diesem Computer angezeigt.
-   **kcd_cache**

    Hiermit können Sie die Informationen zum eingeschränkten Kerberos-Delegierungs Cache anzeigen.  
    -   Anmelde-ID: Wenn angegeben, werden die Cache Informationen für die Anmelde Sitzung mit dem angegebenen Wert angezeigt. Wenn nicht angegeben, werden die Cache Informationen für die Anmelde Sitzung des aktuellen Benutzers angezeigt.
-   **get**

    Ermöglicht es Ihnen, ein Ticket für das vom SPN angegebene Ziel anzufordern.  
    -   Anmelde-ID: Wenn angegeben, wird ein Ticket angefordert, indem die Anmelde Sitzung mit dem angegebenen Wert verwendet wird. Wenn nicht angegeben, fordert ein Ticket mithilfe der Anmelde Sitzung des aktuellen Benutzers an.
    -   kdcoptions: Fordert ein Ticket mit den angegebenen KDC-Optionen an.
-   **add_bind**

    Ermöglicht es Ihnen, einen bevorzugten Domänen Controller für die Kerberos-Authentifizierung anzugeben.
-   **query_bind**

    Ermöglicht das Anzeigen von zwischengespeicherten, bevorzugten Domänen Controllern für die Domänen.
-   **purge_bind**

    Ermöglicht das Entfernen von zwischengespeicherten, bevorzugten Domänen Controllern für die Domänen.
-   **kdcoptions**

    Die aktuelle Liste der Optionen und deren Erläuterungen finden Sie unter [RFC 4120](http://www.ietf.org/rfc/rfc4120.txt).

**Weitere Überlegungen**
-   "Klist. exe" ist in Windows Server 2012 und Windows 8 verfügbar und erfordert keine besondere Installation.

## <a name="BKMK_Examples"></a>Beispiele

1. Wenn Sie die Ereignis-ID 27 bei der Verarbeitung einer TGS-Anforderung (Ticket Gewährung Service) für den Zielserver diagnostizieren, verfügt das Konto nicht über einen passenden Schlüssel zum Generieren eines Kerberos-Tickets. Sie können klist verwenden, um den Kerberos-Ticket Cache abzufragen, um zu bestimmen, ob Tickets fehlen, ob der Zielserver oder das Konto fehlerhaft ist oder ob der Verschlüsselungstyp nicht unterstützt wird.  
   ```
   klist 
   ```  
   ```
   klist –li 0x3e7
   ```  
2. Wenn Sie Fehler diagnostizieren und die Besonderheiten der auf dem Computer für eine Anmelde Sitzung auf dem Computer zwischengespeicherten Ticket Erstellungs Tickets kennen möchten, können Sie mit klist die TGT-Informationen anzeigen.  
   ```
   klist tgt
   ```  
3. Wenn Sie keine Verbindung herstellen können und die Diagnose möglicherweise zu lange dauert, können Sie den Kerberos-Ticket Cache bereinigen, sich abmelden und dann wieder anmelden.  
   ```
   klist purge
   ```  
   ```
   klist purge –li 0x3e7
   ```  
4. Wenn Sie eine Anmelde Sitzung für einen Benutzer oder einen Dienst diagnostizieren möchten, können Sie den folgenden Befehl verwenden, um die Anmelde-ID zu suchen, die in anderen klist-Befehlen verwendet wird.  
   ```
   klist sessions
   ```  
5. Wenn Sie den Fehler bei der eingeschränkten Kerberos-Delegierung diagnostizieren möchten, können Sie den folgenden Befehl verwenden, um den zuletzt aufgetretenen Fehler zu ermitteln.  
   ```
   klist kcd_cache
   ```  
6. Wenn Sie diagnostizieren möchten, ob ein Benutzer oder ein Dienst ein Ticket an einen Server übernehmen kann, können Sie diesen Befehl verwenden, um ein Ticket für einen bestimmten SPN anzufordern.  
   ```
   klist get host/%computername%
   ```  
7. Bei der Diagnose von Replikations Problemen zwischen Domänen Controllern benötigen Sie in der Regel den Client Computer als Ziel für einen bestimmten Domänen Controller. In diesen Fällen können Sie den folgenden Befehl verwenden, um den Client Computer an diesen bestimmten Domänen Controller zu richten.  
   ```
   klist add_bind CONTOSO KDC.CONTOSO.COM
   ```  
   ```
   klist add_bind CONTOSO.COM KDC.CONTOSO.COM
   ```  
8. Sie können den folgenden Befehl verwenden, um zu Fragen, von welchen Domänen Controllern der Computer zuletzt kontaktiert wurde.  
   ```
   klist query_bind
   ```  
9. Wenn Sie möchten, dass Kerberos Domänen Controller wiederentdeckt, können Sie den folgenden Befehl verwenden. Dieser Befehl kann auch verwendet werden, um den Cache zu leeren, bevor neue Domänen Controller Bindungen mit klist add_bind erstellt werden.  
   ```
   klist purge_bind
   ```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)