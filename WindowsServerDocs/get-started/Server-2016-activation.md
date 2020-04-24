---
title: Microsoft Server-Aktivierung
description: So wird Windows Server 2016 aktiviert.
ms.prod: windows-server
ms.date: 09/19/2018
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a45d5cc7a54
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: fd9ea63785e8de313d2177113a466fa67c17410b
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826643"
---
# <a name="windows-server-2016-activation"></a>Windows Server 2016-Aktivierung

Die folgenden Informationen erläutern die anfänglichen Planungsüberlegungen, die du zur Aktivierung der Schlüsselverwaltungsdienste (Key Management Services, KMS) für Windows Server 2016 überprüfen musst. Informationen zur KMS-Aktivierung im Zusammenhang mit älteren als den hier aufgeführten Betriebssystemen findest du unter [Schritt 1: Überprüfen und Auswählen von Aktivierungsmethoden](https://technet.microsoft.com/library/jj134256(WS.11).aspx).

KMS verwendet ein Client-Server-Modell zum Aktivieren von Clients. KMS-Clients werden zur Aktivierung mit einem KMS-Server, dem KMS-Host, verbunden. Der KMS-Host muss sich in Ihrem lokalen Netzwerk befinden.

KMS-Hosts müssen keine dedizierten Server sein, und KMS kann gleichzeitig mit anderen Diensten gehostet werden. Du kannst einen KMS-Host auf einem beliebigen physischen oder virtuellen System ausführen, auf dem Windows 10, Windows Server 2016, Windows Server 2012 R2, Windows 8.1 oder Windows Server 2012 ausgeführt wird.

Ein unter Windows 10 oder Windows 8.1 ausgeführter KMS-Host kann nur Computer aktivieren, auf denen Clientbetriebssysteme ausgeführt werden.
Die folgende Tabelle fasst die Anforderungen an KMS-Hosts und Clients für Netzwerke zusammen, die Windows Server 2016- und Windows 10-Clients enthalten.

> [!NOTE]
> Auf dem KMS-Server sind möglicherweise Updates erforderlich, um die Aktivierung dieser neueren Clients zu unterstützen. Wenn Sie Aktivierungsfehler erhalten, überprüfen Sie, ob die entsprechenden, unter dieser Tabelle aufgelisteten Updates vorhanden sind.

|Product Key-Gruppe|KMS kann gehostet werden auf|Windows-Versionen, die von diesem KMS-Host aktiviert wurden|  
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|  
|Volumenlizenz für Windows Server 2016|Windows Server 2012<p>Windows Server 2012 R2<p>Windows Server 2016<p>|Windows Server (Halbjährlicher Kanal) <br><br>Windows Server 2016 (alle Editionen)<p>Windows 10 LTSB (2015 und 2016)<p>Windows 10 Professional<p>Windows 10 Enterprise<p>Windows 10 Pro for Workstations<br><br>Windows 10 Education<br><br>Windows Server 2012 R2 (alle Editionen)<p>Windows 8.1 Professional<p>Windows 8.1 Enterprise<p>Windows Server 2012 (alle Editionen)<p>Windows Server 2008 R2 (alle Editionen)<p>Windows Server 2008 (alle Editionen)<p>Windows 7 Professional<p>Windows 7 Enterprise| 
|Volumenlizenz für Windows 10|Windows 7<p>Windows 8.1<p> Windows 10|Windows 10 Professional<p> Windows 10 Professional N<p> Windows 10 Enterprise<p> Windows 10 Enterprise N<p> Windows 10 Education<p> Windows 10 Education N<p> Windows 10 Enterprise LTSB (2015)<p> Windows 10 Enterprise LTSB N (2015)<p> Windows 10 Pro for Workstations<br><br>Windows 8.1 Professional<p> Windows 8.1 Enterprise<p> Windows 7 Professional<p> Windows 7 Enterprise<p>|  
|Volumenlizenz für Windows Server 2012 R2 für Windows 10|Windows Server 2008 R2<p> Windows Server 2012 Standard<p> Windows Server 2012 Datacenter<p> Windows Server 2012 R2 Standard<p>Windows Server 2012 R2 Datacenter|Windows 10 Professional<p> Windows 10 Enterprise<p>Windows 10 Enterprise LTSB (2015)<br><br>Windows 10 Pro for Workstations<br><br>Windows 10 Education<br><br> Windows Server 2012 R2 (alle Editionen)<p> Windows 8.1 Professional<p> Windows 8.1 Enterprise<p> Windows Server 2012 (alle Editionen)<p> Windows Server 2008 R2 (alle Editionen)<p>Windows Server 2008 (alle Editionen)<p> Windows 7 Professional<p> Windows 7 Enterprise|

> [!NOTE]  
> Abhängig vom Betriebssystem Ihres KMS-Servers und abhängig davon, welches Betriebssystem Sie aktivieren möchten, müssen Sie möglicherweise eines oder mehrere der folgenden Updates installieren:
> - Installationen von KMS unter Windows 7 oder Windows Server 2008 R2 müssen aktualisiert werden, um die Aktivierung von Clients zu unterstützen, auf denen Windows 10 ausgeführt wird. Weitere Informationen findest du unter  [Update, mit dem Windows 7- und Windows Server 2008 R2-KMS-Hosts Windows 10 aktivieren können](https://support.microsoft.com/help/3079821/update-that-enables-windows-7-and-windows-server-2008-r2-kms-hosts-to-activate-windows-10).  
> - Installationen von KMS unter Windows Server 2012 müssen aktualisiert werden, um die Aktivierung von Clients mit Windows 10 und Windows Server 2016 oder neueren Client- oder Serverbetriebssystemen zu unterstützen. Weitere Informationen findest du unter  [Updaterollup für Windows Server 2012 vom Juli 2016](https://support.microsoft.com/help/3172615/july-2016-update-rollup-for-windows-server-2012). 
> - Installationen von KMS unter Windows 8.1 oder Windows Server 2012 R2 müssen aktualisiert werden, um die Aktivierung von Clients mit Windows 10 und Windows Server 2016 oder neueren Client- oder Serverbetriebssystemen zu unterstützen. Weitere Informationen findest du unter  [Updaterollup für Windows 8.1 und Windows Server 2012 R2 vom Juli 2016](https://support.microsoft.com/help/3172614/july-2016-update-rollup-for-windows-8.1-and-windows-server-2012-r2).  
> - Windows Server 2008 R2 kann nicht aktualisiert werden, um die Aktivierung von Clients mit Windows Server 2016 oder neueren Betriebssystemen zu unterstützen. 

Ein einzelner KMS-Host kann eine unbegrenzte Anzahl von KMS-Clients unterstützen. Bei mehr als 50 Clients empfehlen wir, mindestens zwei KMS-Hosts einzusetzen, für den Fall, dass einer der KMS-Hosts nicht verfügbar ist. Für die meisten Organisationen sind nicht mehr als zwei KMS-Hosts für die gesamte Infrastruktur erforderlich.

## <a name="addressing-kms-operational-requirements"></a>KMS-Betriebsanforderungen
KMS kann physische und virtuelle Computer aktivieren. Zur Qualifikation für die KMS-Aktivierung muss in einem Netzwerk jedoch eine bestimmte Mindestanzahl von Computern (als Aktivierungsschwellenwert bezeichnet) vorhanden sein. KMS-Clients werden nur aktiviert, wenn der Schwellenwert nicht überschritten wird. Um sicherzustellen, dass der Aktivierungsschwellenwert nicht überschritten wird, zählt ein KMS-Host die Computer im Netzwerk, die eine Aktivierung anfordern.

KMS-Hosts zählen die Anzahl der neuesten Verbindungen. Wenn ein Client oder Server den KMS-Host kontaktiert, zählt der Host die Computer-ID als weiteren Computer und gibt dann die aktuelle Anzahl als Antwort zurück. Der Client oder Server wird aktiviert, wenn die Anzahl hoch genug ist. Clients werden aktiviert, wenn die Anzahl höher als 25 ist. Server und Volumenlizenzversionen von Microsoft Office-Produkten werden aktiviert, wenn die Anzahl fünf oder mehr ist. Der KMS zählt nur eindeutige Verbindungen der letzten 30 Tage und speichert nur die letzten 50 Kontakte.

KMS-Aktivierungen sind 180 Tage lang gültig – dieser Zeitraum wird als Aktivierungsgültigkeitsintervall bezeichnet. Damit sie aktiviert bleiben, müssen KMS-Clients ihre Aktivierung erneuern, indem sie mindestens einmal alle 180 Tage eine Verbindung mit dem KMS-Host herstellen. KMS-Clientcomputer versuchen standardmäßig alle sieben Tage, ihre Aktivierung zu erneuern. Sobald die Aktivierung eines Clients erneuert wurde, beginnt der Gültigkeitszeitraum der Aktivierung von vorne.

## <a name="addressing-kms-functional-requirements"></a>KMS-Funktionsanforderungen

Die KMS-Aktivierung erfordert eine TCP/IP-Verbindung. KMS-Hosts und -Clients sind standardmäßig für die Verwendung von Domain Name System (DNS) konfiguriert. KMS-Hosts verwenden standardmäßig dynamische DNS-Updates zum automatischen Veröffentlichen der erforderlichen Informationen, sodass KMS-Clients die Hosts erkennen und eine Verbindung mit ihnen herstellen können. Sie können diese Standardeinstellungen übernehmen oder KMS-Hosts und -Clients manuell konfigurieren, wenn Sie spezielle Anforderungen bezüglich der Netzwerk- und Sicherheitskonfigurationen haben.

Nach dem Aktivieren des ersten KMS-Hosts, kann der dazu verwendete KMS-Schlüssel zum Aktivieren von bis zu fünf weiteren KMS-Hosts in Ihrem Netzwerk verwendet werden. Nach dem Aktivieren eines KMS-Hosts können Administratoren diesen Host bis zu neun Mal mit demselben Schlüssel erneut aktivieren.

Wenn Ihre Organisation mehr als sechs KMS-Hosts benötigt, sollten Sie zusätzliche Aktivierungen für den KMS-Schlüssel Ihrer Organisation anfordern, z. B. wenn Sie über zehn physische Standorte und einen Volumenlizenzvertrag verfügen und möchten, dass für jeden Standort ein lokaler KMS-Host vorhanden ist.

> [!NOTE] 
> Wenden Sie sich an Ihr Activation Call Center, um diese Ausnahme anzufordern. Weitere Informationen finden Sie unter [Microsoft Volume Licensing]( https://www.microsoft.com/licensing).

Computer, auf denen Volumenlizenzeditionen von Windows 10, Windows Server 2016, Windows 8.1, Windows Server 2012 R2, Windows Server 2012, Windows 7 oder Windows Server 2008 R2 ausgeführt werden, sind standardmäßig KMS-Clients und benötigen keine zusätzliche Konfiguration.

Wenn für einen Computer die Umstellung von einem KMS-Host, einer MAK-Version oder einer Einzelhandelsversion von Windows auf einen KMS-Client durchgeführt werden soll, muss der entsprechende KMS-Clientsetupschlüssel installiert werden. Weitere Informationen findest du unter  [KMS-Clientsetupschlüssel](KMSclientkeys.md).
