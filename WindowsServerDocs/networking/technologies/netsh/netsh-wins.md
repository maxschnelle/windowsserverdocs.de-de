---
title: Beispielbatchdatei für Network Shell (Netsh)
description: Sie können in diesem Thema verwenden, erfahren Sie, wie eine Batchdatei erstellen, die mehrere Aufgaben, die mithilfe von Netsh in Windows Server 2016 ausgeführt werden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b0528cfaef201ba30e00e30f56a763be39a6b828
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880171"
---
# <a name="network-shell-netsh-example-batch-file"></a>Netzwerk-Shell \(Netsh\) Beispielbatchdatei

Gilt für: Windows Server 2016

Sie können in diesem Thema verwenden, um zu erfahren, wie Sie eine Batchdatei erstellen, die mehrere Aufgaben ausführt, mithilfe von Netsh in Windows Server 2016. In dieser Beispiel-Batchdatei die **Netsh Wins** Kontext verwendet wird.

## <a name="example-batch-file-overview"></a>Beispiel für Batch File (Übersicht)

Sie können den Netsh-Befehle verwenden, für Windows Internet Name Service \(WINS\) in Batchdateien und anderen Skripts zum Automatisieren von Aufgaben. In der folgenden Batch wird veranschaulicht die Netsh-Befehle für WINS zu verwenden, um eine Vielzahl von Aufgaben ausführen.

In diesem Beispielbatchdatei WINS\-A ist ein WINS-Server mit der IP-Adresse 192.168.125.30 und WINS\-B ist ein WINS-Server mit der IP-Adresse 192.168.0.189.

Die Beispiel-Batchdatei führt die folgenden Aufgaben.

- Fügt einen Datensatz der dynamischen Namen mit der IP-Adresse 192.168.0.205, MY\_Datensatz \[04h\], um WINS\-ein
- Legt WINS\-B als Push-/Pull-Replikationspartner von WINS\-ein
- Eine Verbindung mit WINS\-B und dann legt WINS\-ein als Push-/Pull-Replikationspartner von WINS\-B
- Initiiert eine Push-Replikation von WINS\-A, um WINS\-B
- Eine Verbindung mit WINS\-B, um zu überprüfen, ob der neue Datensatz, MY\_Datensatz wurde erfolgreich repliziert

## <a name="netsh-example-batch-file"></a>Netsh-Beispielbatchdatei

In der folgenden Beispielbatchdatei werden Zeilen, die Kommentare enthalten für Anmerkung "Rem," vorangestellt. Netsh Kommentare werden ignoriert.

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>Netsh-WINS-Befehle, die in der Beispiel-Batchdatei verwendet

Im folgenden Abschnitt listet die **Netsh Wins** Befehle, die in diesem Beispiel verwendet werden.

- **Server**. Verschiebt den aktuellen WINS-Befehl\-Zeile Kontext an den Server, mit dessen Namen oder IP-Adresse angegeben.
- **Fügen Sie Namen**. Registriert einen Namen für den WINS-Server an.
- **Partner hinzufügen**. Fügt einen Replikationspartner in der WINS-Server hinzu.
- **Init-Push**. Initiiert und einen Push-Trigger auf einem WINS-Server sendet.
- **Namen anzeigen**. Zeigt detaillierte Informationen für einen bestimmten Datensatz in der WINS-Server-Datenbank.  

Weitere Informationen finden Sie unter [Netzwerkshell (Netsh)](netsh.md).
