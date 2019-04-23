---
title: vRSS häufig gestellte Fragen
description: In diesem Thema finden Sie einige häufig Fragen und Antworten aufgefordert, Informationen zu vRSS verwenden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 61ae242e-82a8-430d-b07d-52b86c01e686
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3fafe6c39285e65a9d39a76cc6b652dac5c3efbd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840241"
---
# <a name="vrss-frequently-asked-questions"></a>vRSS häufig gestellte Fragen

In diesem Thema finden Sie einige häufig Fragen und Antworten aufgefordert, Informationen zu vRSS verwenden.

## <a name="what-are-the-requirements-for-the-physical-network-adapters-that-i-use-with-vrss"></a>Was sind die Anforderungen für den physischen Netzwerkadaptern, die ich mit vRSS verwenden?

Netzwerkadapter müssen mit Virtual Machine Queue kompatibel sein \(VMQ\) und eine verbindungsgeschwindigkeit von 10 Gbit/s oder mehr benötigen.

Weitere Informationen finden Sie unter [planen die Verwendung von vRSS](vrss-plan.md).

## <a name="does-vrss-work-with-hyper-threaded-processor-cores"></a>Funktioniert vRSS mit hyper\-Prozessorkerne Thread?

Nein. Sowohl vRSS und VMQ ignorieren hyper\-Prozessorkerne Thread.

## <a name="does-vrss-work-for-host-virtual-nics-vnics"></a>VRSS kann verwendet werden, für die virtuelle host-NICs \(vNICs\)?

Ja. Verwenden der **- ManagementOS** -Parameter, anstatt die virtuelle Maschine \(VM\) Namen auf die **Set-VMNetworkAdapter** Windows PowerShell-Befehl und  **Enable-NetAdapterRss** für die Host-vNIC.

Weitere Informationen finden Sie unter [Windows PowerShell-Befehle für RSS und vRSS](vrss-wps.md).

## <a name="how-many-logical-processors-does-a-vm-need-to-use-vrss"></a>Wie viele logische Prozessoren muss ein virtuellen Computer mit vRSS?

Virtuelle Computer benötigen Sie zwei oder mehreren logische Prozessoren \(LPs\) vRSS verwenden können.

Weitere Informationen finden Sie unter [planen die Verwendung von vRSS](vrss-plan.md).

## <a name="is-vrss-compatible-with-nic-teaming"></a>Ist Sie vRSS mit NIC-Teamvorgang kompatibel?

Ja. Wenn Sie NIC-Teamvorgang verwenden, ist es wichtig, dass Sie ordnungsgemäß VMQ für die Arbeit mit den NIC-Teamvorgang-Einstellungen konfigurieren. Ausführliche Informationen zur NIC-Teamvorgang-Bereitstellung und Verwaltung finden Sie unter [NIC-Teamvorgang](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming).

## <a name="vrss-is-enabled-but-how-do-i-know-if-it-is-working"></a>ist vRSS aktiviert, aber wie weiß ich, wenn dies funktioniert? 

Sie werden erkennen Sie, dass vRSS funktioniert, indem Sie den Task-Manager auf dem virtuellen Computer öffnen und die Auslastung des virtuellen Prozessors anzeigen können. Wenn es mehrere Verbindungen mit dem virtuellen Computer sind, sehen Sie mehrere Kerne über 0 % Auslastung.

Da eine einzelne TCP-Sitzung mit Lastenausgleich über mehrere logische Prozessorkerne sein kann, muss Ihr virtueller Computer mehrere TCP empfangen Sitzungen, bevor Sie beobachten können, und zwar unabhängig davon, ob vRSS arbeitet.

Wenn der virtuelle Computer mehrere TCP-Sitzungen erhält, aber nicht mehr als einen Kern von LP über 0 % Auslastung angezeigt, stellen Sie sicher, dass Sie alle Vorbereitungsschritte zur des Themas haben [planen die Verwendung von vRSS](vrss-plan.md).

## <a name="im-looking-at-the-host-and-not-all-of-the-processors-are-being-used-it-looks-like-every-other-one-is-being-skipped"></a>Ich sehe auf dem Host, dass nicht alle Prozessoren verwendet werden. Anscheinend wird jeder zweite Prozessor übersprungen.
  
Überprüfen Sie, ob Hyperthreading aktiviert ist. Sowohl VMQ vRSS sind darauf ausgelegt, übersprungen\-Thread Kerne.

## <a name="are-there-different-windows-powershell-commands-for-rss-and-vrss"></a>Gibt es verschiedene Windows PowerShell-Befehle für RSS und vRSS?

Ja und Nein. Obwohl Sie die gleichen Befehle für RSS in systemeigenen Hosts und RSS auf virtuellen Computern verwenden, erfordert vRSS auch VMQ auf die physische NIC - und für den virtuellen Computer und vRSS aktiviert werden, auf dem Switchport aktiviert werden.

Weitere Informationen finden Sie unter [Windows PowerShell-Befehle für RSS und vRSS](vrss-wps.md).

---
