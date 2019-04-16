---
title: Aktivierung automatische virtueller Computer
TOCTitle: Automatic VM Activation
description: So aktivieren Sie die virtuellen Computer in Windows Server 2019, Windows Server 2016 und Windows Server 2012 R2
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: 62873140c8e114ba537dc4fd3ff7c44868c33243
ms.sourcegitcommit: ca5c80bdb903b282e292488172a7cc92546574c0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2018
ms.locfileid: "4375487"
---
# Aktivierung automatische virtueller Computer

> Gilt für: Windows Server 2019, Windows Server, Semi-Annual Channel, WindowsServer 2016, Windows Server 2012 R2

Automatische virtuellen Computer Aktivierung (AVMA) fungiert als Quittung für den Einkauf Mechanismus, um zu gewährleisten, dass Windows-Produkte gemäß den Produkt Nutzungsrechte und Microsoft-Softwarelizenzbedingungen verwendet werden.

AVMA können Sie virtuelle Computer auf einem ordnungsgemäß aktivierten WindowsServer zu installieren, ohne Product Keys für jeden einzelnen virtuellen Computer selbst in nicht verbundene Umgebungen verwalten. AVMA bindet die Aktivierung virtueller Computer mit dem Virtualisierungsserver lizenzierte und aktiviert den virtuellen Computer beim Starten. AVMA bietet auch Berichte zur Verwendung und Verlaufsdaten auf den Lizenzstatus des virtuellen Computers in Echtzeit. Berichte und tracking-Daten ist auf dem Server Virtualization verfügbar.

## Praktische Anwendungsfälle

Auf Virtualisierungsservern, die mit Volumenlizenzierung oder OEM-Lizenzierung aktiviert sind, bietet AVMA verschiedene Vorteile.

Server Datacenter-Manager können AVMA verwenden, um die folgenden Schritte ausführen:

  - Aktivieren von virtuellen Computern an Remotestandorten

  - Aktivieren von virtuellen Computern mit oder ohne Internetzugang

  - Nachverfolgen von VM-Nutzung und Lizenzen vom Server Virtualization ohne Ansprüche Zugriff auf die virtualisierte Systeme

Es gibt keine Product Keys zu verwalten und keine Aufkleber auf den Servern zu lesen. Der virtuelle Computer aktiviert ist und weiterhin arbeiten, auch wenn sie über ein Array von Virtualisierung Server migriert wird.

Service Provider License Agreement (SPLA) Partner und andere Hostinganbieter keinen Product Keys für Mandanten freigeben und den Zugriff auf einen Mandanten virtuellen Computer, um es zu aktivieren. Aktivierung virtueller Computer ist für den Mandanten transparent, wenn AVMA verwendet wird. Hosten von Anbietern können der Server-Protokolle, Einhaltung der Lizenzen zu überprüfen und Verlauf der Client-Nutzung nachverfolgen.

## Systemanforderungen

AVMA erfordert ein Microsoft-Virtualisierung-Server unter Windows Server 2019 Datacenter, Windows Server 2016 Datacenter oder Windows Server 2012 R2. 

Hier sind die Gäste, die die andere Version Hosts aktivieren können:

|Server-Host-version|WindowsServer 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|WindowsServer 2019|X|X|X|
|Windows Server 2016| |X|X|
|Windows Server 2012 R2| ||X|

Beachten Sie, dass diese alle Editionen (Datacenter, Standard oder Essentials) aktivieren.

Dieses Tool funktioniert nicht mit anderen Technologien Virtualisierungsserver.

## Zum Implementieren von AVMA

1.  Auf einem Windows Server Datacenter-Virtualisierung-Server installieren und Konfigurieren der Microsoft Hyper-V-Serverrolle. Weitere Informationen finden Sie unter [Hyper-V-Server installieren](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md).

2.  [Erstellen eines virtuellen Computers](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md) und eine unterstützte Server-Betriebssystem darauf installieren.

3.  Installieren Sie den AVMA-Schlüssel auf dem virtuellen Computer. Führen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten den folgenden Befehl aus:
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

Der virtuelle Computer wird die Lizenz für die Virtualisierungsserver automatisch aktiviert.


> [!TIP]
> Sie können auch die AVMA Tasten in einer beliebigen Unattend.exe Setup-Datei einsetzen.


## AVMA Schlüssel

Die folgenden AVMA-Schlüssel können für Windows Server 2019 verwendet werden.

|Edition|   AVMA Schlüssel|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B - 2D 623-4GF74|
|Grundlagen|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
Die folgenden AVMA-Schlüssel können für Windows Server, Version 1809 verwendet werden.

|Edition|   AVMA Schlüssel|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B - 2D 623-4GF74|

Die folgenden AVMA-Schlüssel können für Windows Server, Version 1803 und 1709 verwendet werden.

|Edition|AVMA Schlüssel|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


Die folgenden AVMA-Schlüssel können für Windows Server 2016 verwendet werden.

|Edition|AVMA Schlüssel|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|Grundlagen|B4YNW-62DX9-W8V6M-82649-MHBKQ|


Die folgenden AVMA-Schlüssel können für Windows Server 2012 R2 verwendet werden.

|Edition|AVMA Schlüssel|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|Standard|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|Grundlagen|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## Berichte und Laufweite

Die Registrierung (KVP) auf dem Server Virtualization bereit die Gastbetriebssysteme in Echtzeit Tracking-Daten. Da der Registrierungsschlüssel mit dem virtuellen Computer verschoben wird, können Sie auch die Lizenzinformationen abrufen. Standardmäßig gibt die KVP Informationen zum virtuellen Computer, einschließlich der folgenden:

  - Vollqualifizierter Domänenname

  - Betriebssystem und installierte Servicepacks

  - Prozessorarchitektur

  - IPv4 und IPv6-Netzwerk-Adressen

  - RDP-Adressen

Weitere Informationen zum Abrufen dieser Informationen finden Sie unter [Hyper-V-Skript: KVP GuestIntrinsicExchangeItems professionellen](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx).


> [!NOTE]
> KVP-Daten ist nicht gesichert. Es kann geändert werden und wird nicht für Änderungen überwacht.



> [!IMPORTANT]
> KVP-Daten sollten entfernt werden, wenn der Schlüssel AVMA mit einem anderen Product Key (Einzelhandel oder OEM, Volume licensing-Taste) ersetzt wird.


Verlaufsdaten zu AVMA Anfragen ist in einer Protokolldatei auf dem Server Virtualization (EventID 12310) verfügbar.

Da des Aktivierungsprozesses AVMA transparent ist, werden keine Fehlermeldungen angezeigt. Allerdings werden die folgenden Ereignisse in einer Protokolldatei auf den virtuellen Computern (EventID 12309) erfasst.

|Benachrichtigung|Beschreibung|
|-|-|
|AVMA Erfolg|Der virtuelle Computer aktiviert wurde.|
|Ungültige Host|Der Virtualisierungsserver ist nicht mehr reagiert. Dies kann passieren, wenn der Server nicht auf eine unterstützte Version von Windows ausgeführt wird.|
|Ungültige Daten|Dies führt in der Regel nach einem Fehler bei der Kommunikation zwischen dem Server Virtualization und dem virtuellen Computer häufig durch eine Beschädigung oder Verschlüsselung, Daten Konflikt verursacht.|
|Aktivierung verweigert|Die Virtualisierungsserver konnte das Gastbetriebssystem nicht aktivieren, da die AVMA-ID nicht übereinstimmen.|

