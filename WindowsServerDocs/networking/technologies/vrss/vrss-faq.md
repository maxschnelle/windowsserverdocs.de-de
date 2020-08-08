---
title: häufig gestellte Fragen zu vrss
description: In diesem Thema finden Sie einige häufig gestellte Fragen und Antworten zur Verwendung von vrss.
ms.topic: article
ms.assetid: 61ae242e-82a8-430d-b07d-52b86c01e686
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f703c11be44e8f55d96ee0a06332554dec6947cf
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996799"
---
# <a name="vrss-frequently-asked-questions"></a>häufig gestellte Fragen zu vrss

In diesem Thema finden Sie einige häufig gestellte Fragen und Antworten zur Verwendung von vrss.

## <a name="what-are-the-requirements-for-the-physical-network-adapters-that-i-use-with-vrss"></a>Welche Anforderungen gelten für die physischen Netzwerkadapter, die ich mit vrss verwende?

Netzwerkadapter müssen mit Warteschlange für virtuelle Computer \( VMQ kompatibel sein \) und eine Verbindungsgeschwindigkeit von 10 Gbit/s oder mehr aufweisen.

Weitere Informationen finden Sie unter [Planen der Verwendung von vrss](vrss-plan.md).

## <a name="does-vrss-work-with-hyper-threaded-processor-cores"></a>Funktioniert vrss mit \- hyperthreadprozessor-Kernen?

Nein Sowohl von vrss als auch von VMQ werden \- hyperthreadprozessor-Kerne ignoriert.

## <a name="does-vrss-work-for-host-virtual-nics-vnics"></a>Funktioniert vrss für virtuelle Host-NICs- \( vNICs \) ?

Ja. Verwenden Sie den Parameter " **-managementos** " anstelle des VM-namens des virtuellen Computers \( \) im Windows PowerShell-Befehl " **Set-vmnetworkadapter** " und " **enable-netadapterrss** " auf der Host-vNIC.

Weitere Informationen finden Sie unter [Windows PowerShell-Befehle für RSS und vrss](vrss-wps.md).

## <a name="how-many-logical-processors-does-a-vm-need-to-use-vrss"></a>Wie viele logische Prozessoren benötigt ein virtueller Computer vrss?

VMs benötigen mindestens zwei logische Prozessoren ( \( LPs) \) , damit Sie vrss verwenden können.

Weitere Informationen finden Sie unter [Planen der Verwendung von vrss](vrss-plan.md).

## <a name="is-vrss-compatible-with-nic-teaming"></a>Ist vrss mit dem NIC-Team Vorgang kompatibel?

Ja. Wenn Sie NIC-Team Vorgänge verwenden, ist es wichtig, dass Sie VMQ ordnungsgemäß konfigurieren, damit Sie mit den NIC-Team Vorgangs Einstellungen arbeiten können. Ausführliche Informationen zur Bereitstellung und Verwaltung von NIC-Teaming finden Sie unter [NIC](../nic-teaming/nic-teaming.md)-Team Vorgang.

## <a name="vrss-is-enabled-but-how-do-i-know-if-it-is-working"></a>vrss ist aktiviert, aber woher weiß ich, ob Sie funktioniert?

Sie können feststellen, dass vrss funktioniert, indem Sie den Task-Manager auf Ihrer VM öffnen und die Auslastung des virtuellen Prozessors anzeigen. Wenn mehrere Verbindungen mit dem virtuellen Computer hergestellt wurden, können Sie mehr als einen Kern mit einer Auslastung von mehr als 0% sehen.

Da für eine einzelne TCP-Sitzung kein Lastenausgleich über mehrere logische Prozessorkerne möglich ist, muss der virtuelle Computer mehrere TCP-Sitzungen empfangen, bevor Sie überprüfen können, ob vrss funktioniert.

Wenn der virtuelle Computer mehrere TCP-Sitzungen empfängt, aber nicht mehr als ein LP-Kern mit einer Auslastung von mehr als 0% angezeigt wird, stellen Sie sicher, dass Sie alle Vorbereitungsschritte im Thema [Planen der Verwendung von vrss](vrss-plan.md)abgeschlossen haben.

## <a name="im-looking-at-the-host-and-not-all-of-the-processors-are-being-used-it-looks-like-every-other-one-is-being-skipped"></a>Ich sehe den Host, und es werden nicht alle Prozessoren verwendet. Anscheinend wird jeder zweite Prozessor übersprungen.

Überprüfen Sie, ob Hyperthreading aktiviert ist. VMQ und vrss sind so konzipiert, dass \- hyperthreadkerne übersprungen werden.

## <a name="are-there-different-windows-powershell-commands-for-rss-and-vrss"></a>Gibt es unterschiedliche Windows PowerShell-Befehle für RSS und vrss?

Ja und Nein. Während Sie dieselben Befehle sowohl für RSS in systemeigenen Hosts als auch für RSS auf VMS verwenden, erfordert vrss auch, dass VMQ auf der physischen NIC aktiviert ist und dass der virtuelle Computer und vrss auf dem Switchport aktiviert werden.

Weitere Informationen finden Sie unter [Windows PowerShell-Befehle für RSS und vrss](vrss-wps.md).

---