---
title: Bidirektionaler TCP-Handshake-Fehler während der SMB-Verbindung
description: Führt den TCP-drei-Wege-Hand Shake Fehler während der SMB-Verbindung ein.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: cb88fa89344172cfc1ed036865a4496ed73e9a22
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815323"
---
# <a name="tcp-three-way-handshake-failure-during-smb-connection"></a>Bidirektionaler TCP-Handshake-Fehler während der SMB-Verbindung

Wenn Sie eine Netzwerk Ablauf Verfolgung analysieren, bemerken Sie, dass ein TCP-Fehler (Transmission Control Protocol) mit drei-Wege-Handshake auftritt, der das SMB-Problem verursacht. In diesem Artikel wird beschrieben, wie Sie dieses Problem beheben.

## <a name="troubleshooting"></a>Problembehandlung

Im Allgemeinen ist die Ursache eine lokale oder Infrastruktur Firewall, die den Datenverkehr blockiert. Dieses Problem kann in einem der folgenden Szenarien auftreten:

## <a name="scenario-1"></a>Szenario 1

Das TCP-SYN-Paket wird auf dem SMB-Server empfangen, aber der SMB-Server gibt kein TCP-SYN-ACK-Paket zurück.

Führen Sie die folgenden Schritte aus, um dieses Szenario zu beheben.

### <a name="step-1"></a>Schritt 1

Führen Sie **netstat** oder **Get-nettcpconnection** aus, um sicherzustellen, dass ein Listener an TCP-Port 445 vorhanden ist, der im Besitz des System Prozesses sein sollte.

```cmd
netstat -ano | findstr :445
```

```PowerShell
Get-NetTcpConnection -LocalPort 445
```

### <a name="step-2"></a>Schritt 2

Stellen Sie sicher, dass der Server Dienst gestartet ist und ausgeführt wird.

### <a name="step-3"></a>Schritt 3

Erstellen Sie eine Windows Filtering Platform (WFP)-Erfassung, um zu bestimmen, welche Regel oder welches Programm den Datenverkehr löscht. Führen Sie hierzu den folgenden Befehl in einem Eingabe Aufforderungs Fenster aus:

```cmd
netsh wfp capture start
```

Reproduzieren Sie das Problem, und führen Sie dann den folgenden Befehl aus:

```cmd
netsh wfp capture stop
```

Führen Sie eine Szenario-Ablauf Verfolgung aus, und suchen Sie im SMB-Datenverkehr (an TCP-Port 445) nach WFP-Daten

Optional können Sie die Antivirussoftware entfernen, da Sie nicht immer WFP-basiert sind.

### <a name="step-4"></a>Schritt 4

Wenn die Windows-Firewall aktiviert ist, können Sie die Firewallprotokollierung aktivieren, um zu bestimmen, ob ein Datenverkehr in der

Stellen Sie sicher, dass die entsprechenden Regeln für die Datei-und Druckerfreigabe (SMB eingehend) in der **Windows-Firewall mit** erweiterter Sicherheit \> **eingehenden Regeln**aktiviert sind.

> [!NOTE]
> Abhängig davon, wie der Computer eingerichtet ist, kann "Windows-Firewall" als "Windows Defender Firewall" bezeichnet werden.

## <a name="scenario-2"></a>Szenario 2

Das TCP-SYN-Paket kommt nie auf dem SMB-Server an.

In diesem Szenario müssen Sie die Geräte auf dem Netzwerkpfad untersuchen. Sie können auf jedem Gerät erfasste Netzwerk Ablauf Verfolgungen analysieren, um zu bestimmen, welches Gerät den Datenverkehr blockiert.
