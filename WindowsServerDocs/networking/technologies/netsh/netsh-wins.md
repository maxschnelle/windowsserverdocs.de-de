---
title: Beispielbatchdatei für Network Shell (Netsh)
description: In diesem Thema wird die Erstellung einer Batchdatei erläutert, die mehrere Aufgaben mit Netsh in Windows Server 2016 ausführt.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 86fbe66978f7c09a332bba16a27a13fa029cb5a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401918"
---
# <a name="network-shell-netsh-example-batch-file"></a>Beispielbatchdatei für Network Shell (\(Netsh\))

Gilt für: Windows Server 2016

In diesem Thema wird die Erstellung einer Batchdatei erläutert, die mehrere Aufgaben mit Netsh in Windows Server 2016 ausführt. In dieser Beispielbatchdatei wird der Kontext **netsh wins** verwendet.

## <a name="example-batch-file-overview"></a>Beispielbatchdatei – Übersicht

Du kannst Netsh-Befehle für Windows Internet Name Service \(WINS\) in Batchdateien und anderen Skripts verwenden, um Aufgaben zu automatisieren. Das folgende Batchdateibeispiel zeigt, wie Netsh-Befehle für WINS zur Ausführung einer Vielzahl von verwandten Aufgaben verwendet werden können.

In dieser Beispielbatchdatei ist WINS\-A ein WINS-Server mit der IP-Adresse 192.168.125.30 und WINS\-B ist ein WINS-Server mit der IP-Adresse 192.168.0.189.

Die Beispielbatchdatei erfüllt die folgenden Aufgaben.

- Fügt einen dynamischen Namendatensatz mit der IP-Adresse 192.168.0.205, MY\_RECORD \[04h\], zu WINS\-A hinzu
- Legt WINS\-B als Push/Pull-Replikationspartner von WINS\-A fest
- Stellt eine Verbindung mit WINS\-B her und legt dann WINS\-A als Push/Pull-Replikationspartner von WINS\-B fest
- Initiiert eine Push-Replikation von WINS\-A nach WINS\-B
- Stellt eine Verbindung mit WINS\-B her, um zu überprüfen, ob der neue Datensatz, MY\_RECORD, erfolgreich repliziert wurde

## <a name="netsh-example-batch-file"></a>Netsh-Beispielbatchdatei

In der folgenden Beispielbatchdatei wird Zeilen, die Kommentare enthalten, „rem“ als Hinweis vorangestellt. Netsh ignoriert Kommentare.

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

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>In der Beispielbatchdatei verwendete Netsh WINS-Befehle

Im folgenden Abschnitt werden die **Netsh WINS**-Befehle aufgelistet, die in diesem Beispielverfahren verwendet werden.

- **server**. Verschiebt den aktuellen WINS-Befehl\-Zeilenkontext auf den Server, der entweder durch seinen Namen oder seine IP-Adresse angegeben ist.
- **add name**. Registriert einen Namen auf dem WINS-Server.
- **add partner**. Fügt einen Replikationspartner auf dem WINS-Server hinzu.
- **init push**. Initiiert und sendet einen Push-Trigger an einen WINS-Server.
- **show name**. Zeigt ausführliche Informationen zu einem bestimmten Datensatz in der WINS-Serverdatenbank an.  

Weitere Informationen findest du unter [Network Shell (Netsh)](netsh.md).
