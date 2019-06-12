---
title: klist
description: 'Windows-Befehle Thema ***- '
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
ms.openlocfilehash: d0b77aed5970c74181ba03da5e57e9b230313a15
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438110"
---
# <a name="klist"></a>klist



Zeigt eine Liste der derzeit zwischengespeicherten Kerberos-Tickets. Diese Informationen gelten für Windows Server 2012. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
klist [-lh <LogonId.HighPart>] [-li <LogonId.LowPart>] tickets | tgt | purge | sessions | kcd_cache | get | add_bind | query_bind | purge_bind
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-lh|Gibt an, der obere Bereich des Benutzers lokal eindeutige Kennung (LUID), im Hexadezimalformat ausgedrückt. Wenn weder lh – oder – li vorhanden sind, verwendet der Befehl die LUID des aktuell angemeldeten Benutzers.|
|-li|Gibt den unteren Teil des Benutzers lokal eindeutige Kennung (LUID), im Hexadezimalformat ausgedrückt. Wenn weder lh – oder – li vorhanden sind, verwendet der Befehl die LUID des aktuell angemeldeten Benutzers.|
|Tickets|Listet die derzeit zwischengespeicherten Ticket-granting-Tickets (TGTs) und Service-Tickets, der die angegebene anmeldesitzung. Dies ist die Standardoption.|
|tgt|Zeigt die anfängliche Kerberos TGT.|
|Löschen|Können Sie alle der angegebenen anmeldesitzung-Tickets zu löschen.|
|Sitzungen|Zeigt eine Liste der anmeldesitzungen auf diesem Computer.|
|kcd_cache|Zeigt die Kerberos eingeschränkte Delegierung Cacheinformationen.|
|get|Können Sie ein Ticket an den Zielcomputer angegeben, indem Sie den Dienstprinzipalnamen (SPN) anfordern.|
|add_bind|Ermöglicht es Ihnen, einen bevorzugten Domänencontroller für die Kerberos-Authentifizierung anzugeben.|
|query_bind|Zeigt eine Liste der zwischengespeicherten bevorzugten Domänencontroller für jede Domäne, die Kerberos kontaktiert hat.|
|purge_bind|Entfernt die bevorzugte die zwischengespeicherten Domänencontroller für die angegebenen Domänen.|
|kdcoptions|Zeigt die Schlüsselverteilungscenter (Key Distribution Center, KDC)-Optionen, die in RFC 4120 angegeben.|
|/?|Zeigt die Hilfe für diesen Befehl.|

## <a name="remarks"></a>Hinweise

Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe sein, um alle Parameter mit diesem Befehl ausführen.

Wenn keine Parameter bereitgestellt werden, werden alle Tickets für den derzeit angemeldeten Benutzer Klist abgerufen werden.

Die Parameter werden die folgenden Informationen an:
-   **tickets**

    Listet die derzeit zwischengespeicherten Tickets von Diensten, die Sie seit der Anmeldung authentifiziert haben. Zeigt die folgenden Attribute von alle zwischengespeicherten Tickets an:  
    -   LogonID: Die LUID
    -   Client: Die Verkettung der Clientname und der Domänenname des-Clients
    -   Server: Die Verkettung von den Dienstnamen und den Domänennamen des Diensts
    -   KerbTicket Verschlüsselungstyp: Der Verschlüsselungstyp, der zum Verschlüsseln des Kerberos-Tickets verwendet wird
    -   Ticket-Flags: Die Kerberos-Ticket-flags
    -   Startzeit: Die Zeit, die von der das Ticket gültig sein soll
    -   Endzeit: Die Zeit, die das Ticket nicht mehr gültig ist. Wenn ein Ticket nach dieser Zeit ist, kann es nicht mehr verwendet werden zu einem Dienst zu authentifizieren oder zur Verlängerung verwendet werden
    -   Erneuern Sie Mal: Die Zeit, die eine neue erste Authentifizierung erforderlich ist.
    -   Wichtige Sitzungstyp: Der Verschlüsselungsalgorithmus, der für den Sitzungsschlüssel verwendet wird
-   **tgt**

    Sind die ersten Kerberos-TGT und die folgenden Attribute des aktuell zwischengespeicherten Tickets aufgeführt:  
    -   LogonID: Im Hexadezimalformat
    -   ServiceName: krbtgt
    -   TargetName \<SPN >: Krbtgt
    -   DomainName: Name der Domäne, die das TGT ausgibt.
    -   TargetDomainName: Domäne, die das TGT für ausgestellt wird
    -   AltTargetDomainName: Domäne, die das TGT für ausgestellt wird
    -   Ticket-Flags: Adresse und -Aktionen und Typ
    -   Sitzungsschlüssel: Kennwortlänge und verschlüsselungsanforderungen Schlüsselalgorithmus
    -   StartTime: Uhrzeit des lokalen Computers, der das Ticket angefordert wurde
    -   "EndTime": Zeitpunkt, zu das Ticket nicht mehr gültig ist. Wenn ein Ticket nach dieser Zeit ist, kann es ohne mehr verwendet werden, einen Dienst zu authentifizieren.
    -   RenewUntil: Stichtag für Benutzerticket
    -   TimeSkew: Der Zeitunterschied mit dem Schlüsselverteilungscenter (KDC)
    -   EncodedTicket: Codierte ticket
-   **purge**

    Können Sie einer bestimmten Ticket löschen. Löschen von Tickets zerstört alle Tickets, die Sie zwischengespeichert haben, verwenden Sie dieses Attribut daher mit Vorsicht. Sie können Sie beenden, können Authentifizierung gegenüber Ressourcen verwendet. In diesem Fall müssen Sie sich abmelden und erneut anmelden.  
    -   LogonID: Im Hexadezimalformat
-   **sessions**

    Ermöglicht Ihnen das Auflisten und Anzeigen von Informationen für alle anmeldesitzungen auf diesem Computer.  
    -   LogonID: Wenn angegeben, zeigt der anmeldesitzung nur durch den angegebenen Wert. Wenn nicht angegeben, wird die anmeldesitzungen auf diesem Computer angezeigt.
-   **kcd_cache**

    Können Sie die eingeschränkte Kerberos-Delegierung Cache-Informationen anzuzeigen.  
    -   LogonID: Wenn angegeben, zeigt die Cacheinformationen für die Sitzung durch den angegebenen Wert. Wenn nicht angegeben ist, zeigt die Informationen für die Sitzung des aktuellen Benutzers zwischengespeichert werden.
-   **get**

    Können Sie ein Ticket für das Ziel anfordern, die durch den SPN angegeben wird.  
    -   LogonID: Wenn angegeben, fordert ein Ticket, indem Sie mithilfe der anmeldesitzung den angegebenen Wert. Wenn nicht angegeben ist, fordert ein Ticket, mit der Sitzung des aktuellen Benutzers.
    -   Kdcoptions: Fordert ein Ticket mit den angegebenen KDC-Optionen
-   **add_bind**

    Ermöglicht es Ihnen, einen bevorzugten Domänencontroller für die Kerberos-Authentifizierung anzugeben.
-   **query_bind**

    Können Sie zwischengespeicherte und bevorzugten Domänencontroller für die Domänen angezeigt.
-   **purge_bind**

    Können Sie zwischengespeicherte und bevorzugten Domänencontroller für die Domänen zu entfernen.
-   **kdcoptions**

    Die aktuelle Liste der Optionen und deren Beschreibungen, finden Sie unter [RFC 4120](http://www.ietf.org/rfc/rfc4120.txt).

**Weitere Überlegungen**
-   Klist.exe ist in Windows Server 2012 und Windows 8 verfügbar und erfordert keine besondere Installation.

## <a name="BKMK_Examples"></a>Beispiele für

1. Wenn Sie eine Ereignis-ID 27 während der Verarbeitung diagnostizieren ein Ticket-granting Service (TGS) Anforderung für den Zielserver, das Konto nicht über die passenden Schlüssel zum Generieren eines Kerberos-Tickets verfügt. Klist können zum Abfragen der Kerberos-Ticket-Cache zu bestimmen, ob Tickets fehlen, sind, wenn die Ziel-Server oder das Konto fehlerhaft ist oder wenn der Verschlüsselungstyp nicht unterstützt wird.  
   ```
   klist 
   ```  
   ```
   klist –li 0x3e7
   ```  
2. Beim Diagnostizieren von Fehlern und Sie wissen möchten, die Einzelheiten der einzelnen-Ticket-granting-Ticket, die auf dem Computer, die für eine anmeldesitzung zwischengespeichert werden, können Sie Klist verwenden, um die TGT-Informationen anzuzeigen.  
   ```
   klist tgt
   ```  
3. Wenn Sie zum Herstellen einer Verbindung und Diagnose zu lange dauern könnte, können Sie den Kerberos-Ticket-Cache zu löschen, melden Sie sich ab und dann wieder anmelden.  
   ```
   klist purge
   ```  
   ```
   klist purge –li 0x3e7
   ```  
4. Wenn Sie eine anmeldesitzung für einen Benutzer oder ein Dienst diagnostizieren möchten, können Sie den folgenden Befehl verwenden, finden Sie in anderen Klist-Befehlen die LogonID, das verwendet wird.  
   ```
   klist sessions
   ```  
5. Wenn Sie die eingeschränkte Kerberos-Delegierungsfehler diagnostizieren möchten, können Sie den folgenden Befehl aus, um den letzten Fehler zu finden, der aufgetreten ist.  
   ```
   klist kcd_cache
   ```  
6. Wenn Sie eine diagnose, wenn ein Benutzer oder ein Dienst kann ein Ticket an einem Server abrufen, können Sie mit diesem Befehl, um ein Ticket für einen bestimmten SPN anzufordern.  
   ```
   klist get host/%computername%
   ```  
7. Wenn Probleme bei der Replikation auf Domänencontrollern diagnostizieren zu können, benötigen Sie in der Regel dem Clientcomputer verfügen, die einen bestimmten Domänencontroller als Ziel. In diesen Fällen können Sie den folgenden Befehl auf dem Clientcomputer verfügen, die diesen bestimmten Domänencontroller als Ziel verwenden.  
   ```
   klist add_bind CONTOSO KDC.CONTOSO.COM
   ```  
   ```
   klist add_bind CONTOSO.COM KDC.CONTOSO.COM
   ```  
8. Um welche Domänencontroller dieser Computer zuletzt kontaktiert abzufragen, können Sie den folgenden Befehl verwenden.  
   ```
   klist query_bind
   ```  
9. Bei der Kerberos-Domänencontroller ermittlungsaktionen ermittelt werden sollen, können Sie den folgenden Befehl verwenden. Mit diesem Befehl kann auch verwendet werden, um den Cache zu leeren, bevor Sie neue Domäne-Controller-Bindungen mit Klist Add_bind erstellen.  
   ```
   klist purge_bind
   ```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)