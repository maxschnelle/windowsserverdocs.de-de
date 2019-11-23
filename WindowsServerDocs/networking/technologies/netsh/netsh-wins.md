---
title: Beispielbatchdatei für Network Shell (Netsh)
description: In diesem Thema erfahren Sie, wie Sie mithilfe von Netsh in Windows Server 2016 eine Batchdatei erstellen, die mehrere Aufgaben ausführt.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 86fbe66978f7c09a332bba16a27a13fa029cb5a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401918"
---
# <a name="network-shell-netsh-example-batch-file"></a>Netzwerkshell \(Netsh\) Beispiel Batch Datei

Gilt für: Windows Server 2016

In diesem Thema erfahren Sie, wie Sie mithilfe von Netsh in Windows Server 2016 eine Batchdatei erstellen, die mehrere Aufgaben ausführt. In dieser Beispiel Batchdatei wird der **Netsh WINS** -Kontext verwendet.

## <a name="example-batch-file-overview"></a>Beispiel für eine Batch Datei Übersicht

Sie können Netsh-Befehle für den Windows Internet Name Service \(WINS-\) in Batch Dateien und anderen Skripts verwenden, um Aufgaben zu automatisieren. Im folgenden Beispiel für eine Batchdatei wird veranschaulicht, wie Netsh-Befehle für WINS verwendet werden, um eine Reihe verwandter Aufgaben auszuführen.

In dieser Beispiel Batchdatei ist WINS\-a ein WINS-Server mit der IP-Adresse 192.168.125.30 und WINS\-B ist ein WINS-Server mit der IP-Adresse 192.168.0.189.

Die Beispiel Batchdatei führt die folgenden Aufgaben aus.

- Fügt einen dynamischen namens Daten Satz mit der IP-Adresse 192.168.0.205, My\_Record \[04h\], zu WINS\-a
- Legt\-B als Push/Pull-Replikations Partner von WINS\-a fest.
- Stellt eine Verbindung mit WINS\-B her und legt dann WINS\-a als Push/Pull Replication Partner of WINS\-B fest.
- Initiiert eine pushreplikation von WINS\-a zu WINS\-B
- Stellt eine Verbindung zu WINS\-B her, um zu überprüfen, ob der neue Datensatz, mein\_Datensatz, erfolgreich repliziert wurde

## <a name="netsh-example-batch-file"></a>Netsh-Beispiel Batchdatei

In der folgenden Beispiel Batchdatei werden Zeilen, die Kommentare enthalten, als Anmerkung vorangestellt. Netsh ignoriert Kommentare.

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>Netsh WINS-Befehle, die in der Beispiel Batchdatei verwendet werden

Der folgende Abschnitt listet die **Netsh WINS** -Befehle auf, die in diesem Beispiel Verfahren verwendet werden.

- **Server**. Verschiebt den aktuellen WINS-Befehl\-Zeilen Kontext auf den Server, der durch den Namen oder die IP-Adresse angegeben wird.
- **Name hinzufügen**. Registriert einen Namen auf dem WINS-Server.
- **Partner hinzufügen**. Fügt einen Replikations Partner auf dem WINS-Server hinzu.
- **Init Push**. Initiiert einen Push-triggerserver und sendet ihn an einen WINS-Server.
- **Name anzeigen**. Zeigt ausführliche Informationen zu einem bestimmten Datensatz in der WINS-Server Datenbank an.  

Weitere Informationen finden Sie unter [Network Shell (Netsh)](netsh.md).
