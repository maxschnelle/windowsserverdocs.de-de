---
title: Automatische Aktivierung virtueller Computer
TOCTitle: Automatic VM Activation
description: Aktivieren virtueller Computer unter Windows Server 2019, Windows Server 2016 und Windows Server 2012 R2
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
ms.openlocfilehash: 4d1cdcfe8325a246e2752e1d1f2a3ad536598658
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868571"
---
# <a name="automatic-virtual-machine-activation"></a>Automatische Aktivierung virtueller Computer

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2

Die automatische Aktivierung virtueller Maschinen (Automatic Virtual Machine Activation, AVMA) dient als Kaufnachweisverfahren, damit Sie sicherstellen können, dass Windows-Produkte gemäß den Produktnutzungsrechten und den Microsoft-Software-Lizenzbedingungen verwendet werden.

Mithilfe der automatischen Aktivierung virtueller Maschinen können Sie virtuelle Computer auf einem ordnungsgemäß aktivierten Windows-Server installieren, ohne dabei die Product Keys für die einzelnen virtuellen Computer verwalten zu müssen. Dies gilt auch für nicht verbundene Umgebungen. AVMA bindet die Aktivierung der virtuellen Computer an den lizenzierten Virtualisierungsserver und aktiviert den virtuellen Computer, wenn er gestartet wird. AVMA bietet darüber hinaus Echtzeitberichte zur Verwendung sowie Verlaufsdaten zum Lizenzstatus des virtuellen Computers. Auf dem Virtualisierungsserver stehen Berichterstellung und Nachverfolgungsdaten zur Verfügung.

## <a name="practical-applications"></a>Praktische Anwendungsfälle

Für Virtualisierungsserver, die per Volumenlizenzierung oder OEM-Lizenzierung aktiviert werden, bietet AVMA mehrere Vorteile.

Manager von Serverrechenzentren können AVMA für Folgendes verwenden:

  - Aktivieren virtueller Computer an Remotestandorten

  - Aktivieren virtueller Computer mit oder ohne Internetverbindung

  - Nachverfolgen der Verwendung virtueller Computer und Lizenzen auf dem Virtualisierungsserver. Dafür sind keine Zugriffsrechte auf den virtualisierten Systemen erforderlich.

Es müssen keine Product Keys verwaltet und keine Aufkleber auf den Servern gelesen werden. Der virtuelle Computer wird aktiviert und weiterhin ausgeführt, auch wenn er zu einem Array mit Virtualisierungsservern migriert wird.

Partner eines Dienstanbieter-Lizenzvertrags (SPLA) und andere Hostinganbieter müssen die Product Keys nicht an Mandanten weitergeben oder zur Aktivierung auf den virtuellen Computer eines Mandanten zugreifen. Die Aktivierung virtueller Computer ist für Mandanten leicht verständlich, wenn AVMA verwendet wird. Hostinganbieter können anhand der Serverprotokolle die Einhaltung der Lizenzvorschriften überprüfen und den Verlauf der Clientauslastung nachverfolgen.

## <a name="system-requirements"></a>Systemanforderungen

Für AVMA ist ein Microsoft-Virtualisierungsserver unter Windows Server 2019 Datacenter, Windows Server 2016 Datacenter oder Windows Server 2012 R2 erforderlich. 

Hier sind die Gäste aufgeführt, die von den verschiedenen Versionshosts aktiviert werden können:

|Serverhostversion|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|Windows Server 2019|X|X|X|
|Windows Server 2016| |X|X|
|Windows Server 2012 R2| ||X|

Beachte, dass diese alle Editionen (Datacenter, Standard oder Essentials) aktivieren.

Dieses Tool funktioniert nicht mit anderen Virtualisierungsservertechnologien.

## <a name="how-to-implement-avma"></a>Implementieren von AVMA

1.  Installiere und konfiguriere auf einem Virtualisierungsserver mit Windows Server Datacenter die Microsoft Hyper-V Server-Rolle. Weitere Informationen findest du unter [Installieren von Hyper-V Server](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md).

2.  [Erstelle einen virtuellen Computer](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md), und installiere darauf ein unterstütztes Serverbetriebssystem.

3.  Installieren Sie den AVMA-Schlüssel auf dem virtuellen Computer. Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus:
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

Vom virtuellen Computer wird die Lizenz für den Virtualisierungsserver automatisch aktiviert.


> [!TIP]
> Sie können die AVMA-Schlüssel auch in allen Unattend.exe-Setupdateien nutzen.


## <a name="avma-keys"></a>AVMA-Schüssel

Die folgenden AVMA-Schlüssel können für Windows Server 2019 verwendet werden:

|Edition|   AVMA-Schüssel|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|
|Essentials|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
Die folgenden AVMA-Schlüssel können für Windows Server, Version 1809, verwendet werden:

|Edition|   AVMA-Schüssel|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|

Die folgenden AVMA-Schlüssel können für Windows Server, Version 1803 und 1709, verwendet werden:

|Edition|AVMA-Schüssel|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


Die folgenden AVMA-Schlüssel können für Windows Server 2016 verwendet werden:

|Edition|AVMA-Schüssel|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|Essentials|B4YNW-62DX9-W8V6M-82649-MHBKQ|


Die folgenden AVMA-Schlüssel können für Windows Server 2012 R2 verwendet werden.

|Edition|AVMA-Schüssel|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|Standard|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|Essentials|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## <a name="reporting-and-tracking"></a>Berichterstellung und Nachverfolgung

Die Registrierung (KVP) auf dem Virtualisierungsserver stellt Echtzeit-Nachverfolgungsdaten für die Gastbetriebssysteme bereit. Da der Registrierungsschlüssel mit dem virtuellen Computer verknüpft ist, können Sie auch Lizenzinformationen abrufen. Standardmäßig werden vom KVP Informationen zum virtuellen Computer zurückgegeben, z. B.:

  - Vollqualifizierter Domänenname

  - Installiertes Betriebssystem und Service Packs

  - Prozessorarchitektur

  - IPv4- und IPv6-Netzwerkadressen

  - RDP-Adressen

Weitere Informationen dazu, wie du diese Informationen beschaffst, findest du unter [Hyper-V Skript: KVP-GuestIntrinsicExchangeItems](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx).


> [!NOTE]
> KVP-Daten sind nicht geschützt. Sie können geändert werden und werden nicht auf Änderungen überwacht.



> [!IMPORTANT]
> Sie sollten die KVP-Daten entfernen, wenn der AVMA-Schlüssel durch einen anderen Product Key (Verkaufs-, OEM- oder Volumenlizenzschlüssel) ersetzt wird.


Verlaufsdaten zu AVMA-Anforderungen sind in einer Protokolldatei auf dem Virtualisierungsserver verfügbar (EventID 12310).

Da der AVMA-Aktivierungsprozess transparent ist, werden keine Fehlermeldungen angezeigt. Die folgenden Ereignisse werden auf den virtuellen Computern jedoch in einer Protokolldatei erfasst (EventID 12309).

|Benachrichtigung|Beschreibung|
|-|-|
|AVMA Success (AVMA erfolgreich)|Der virtuelle Computer wurde aktiviert.|
|Invalid Host (Ungültiger Host)|Der Virtualisierungsserver reagiert nicht. Dies kann auftreten, wenn auf dem Server keine unterstützte Version von Windows ausgeführt wird.|
|Invalid Data (Ungültige Daten)|Dies liegt normalerweise an einem Fehler bei der Kommunikation zwischen dem Virtualisierungsserver und dem virtuellen Computer, wobei die Ursache häufig eine Beschädigung, Verschlüsselung oder ein Datenkonflikt ist.|
|Activation Denied (Aktivierung verweigert)|Das Gastbetriebssystem konnte vom Virtualisierungsserver nicht aktiviert werden, weil die AVMA-ID nicht übereinstimmte.|

