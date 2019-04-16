---
title: Network Shell (Netsh) Beispielbatchdatei
description: Sie können in diesem Thema erfahren Sie, wie Sie eine Stapelverarbeitungsdatei erstellen, die mehrere Aufgaben mithilfe von Netsh in Windows Server 2016 verwenden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b0528cfaef201ba30e00e30f56a763be39a6b828
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-shell-netsh-example-batch-file"></a>Network Shell \(Netsh\)-Batch-Beispieldatei

Gilt für: Windows Server 2016

Sie können in diesem Thema erfahren Sie, wie Sie eine Stapelverarbeitungsdatei erstellen, die mehrere Aufgaben mithilfe von Netsh in Windows Server 2016 verwenden. In diesem Beispiel Batch-Datei die **Netsh Wins** Kontext verwendet wird.

## <a name="example-batch-file-overview"></a>Beispiel-Stapel (Übersicht)

Sie können Netsh-Befehle für Windows Internet Name Service-\(WINS\) Batch-Dateien und anderen Skripts zum Automatisieren von Aufgaben verwenden. Im folgenden Stapel wird veranschaulicht, wie Netsh-Befehle für WINS zu verwenden, um eine Reihe von verwandten Aufgaben auszuführen.

In diesem Beispielbatchdatei WINS\ ein WINS-Server mit der IP-Adresse 192.168.125.30 und WINS\-B ist ein WINS-Server mit der IP-Adresse 192.168.0.189.

Die Beispiel-Batchdatei führt die folgenden Aufgaben aus.

- Fügt eine dynamische Namen Datensatz mit IP-Adresse 192.168.0.205 MY\_RECORD \[04h\], zu WINS\ ein
- Festlegen von WINS\-B als Push-/Pull-Replikationspartner WINS\ a
- Wird eine Verbindung mit WINS\ B und legt dann WINS\-A als Push-/Pull-Replikationspartner von WINS\ B
- Initiiert eine Push-Replikation von WINS\ A WINS\ B
- Wird eine Verbindung mit WINS\-B, um sicherzustellen, dass der neue Datensatz, MY\_RECORD, erfolgreich repliziert wurde

## <a name="netsh-example-batch-file"></a>Netsh-Beispiel-Batch-Datei

Im folgenden Beispiel-Batch-Datei sind Zeilen, die Kommentare enthalten für Hinweis "Rem" vorangestellt. Kommentare werden von Netsh ignoriert.

    rem: Begin example batch file.
    
    rem two WINS servers:
    
    rem (WINS-A) 192.168.125.30
    
    rem (WINS-B) 192.168.0.189
    
    rem 1. Connect to (WINS-A), and add the dynamic name MY\_RECORD \[04h\] to the (WINS-A) database.
    
    netsh wins server 192.168.125.30 add name Name=MY\_RECORD EndChar=04 IP={192.168.0.205}
    
    rem 2. Connect to (WINS-A), and set (WINS-B) as a push/pull replication partner of (WINS-A).
    
    netsh wins server 192.168.125.30 add partner Server=192.168.0.189 Type=2
    
    rem 3. Connect to (WINS-B), and set (WINS-A) as a push/pull replication partner of (WINS-B).
    
    netsh wins server 192.168.0.189 add partner Server=192.168.125.30 Type=2
    
    rem 4. Connect back to (WINS-A), and initiate a push replication to (WINS-B).
    
    netsh wins server 192.168.125.30 init push Server=192.168.0.189 PropReq=0
    
    rem 5. Connect to (WINS-B), and check that the record MY\_RECORD \[04h\] was replicated successfully.
    
    netsh wins server 192.168.0.189 show name Name=MY\_RECORD EndChar=04
    
    rem 6. End example batch file.

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>Netsh-Befehle für WINS in der Beispiel-Batchdatei verwendet

Im folgenden Abschnitt Listen der **Netsh Wins** Befehle, die im folgenden Beispiel verwendet werden.

- **Server**. Verschiebt den aktuellen Kontext der WINS-Befehlszeile mit dem Server, die entweder durch den Namen oder IP-Adresse angegeben.
- **Geben Sie**. Ein Name auf dem WINS-Server registriert.
- **Hinzufügen von Partner**. Fügt einen Replikationspartner des WINS-Servers hinzu.
- **Init Push**. Initiiert und einen Push-Trigger an einen WINS-Server gesendet.
- **Anzeigen der Namen**. Zeigt detaillierte Informationen für einen bestimmten Eintrag in der WINS-Server-Datenbank.  

Weitere Informationen finden Sie unter [Netzwerkshell (Netsh)](netsh.md).
