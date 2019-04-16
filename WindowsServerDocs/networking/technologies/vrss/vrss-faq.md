---
title: vRSS häufig gestellte Fragen
description: In diesem Thema finden Sie, dass einige häufig gestellte Fragen und Antworten Fragen, über die Verwendung von vRSS.
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133816"
---
# vRSS häufig gestellte Fragen

In diesem Thema finden Sie, dass einige häufig gestellte Fragen und Antworten Fragen, über die Verwendung von vRSS.

## Was sind die Anforderungen für den physischen Netzwerkadaptern, die ich mit vRSS verwenden?

Netzwerkadapter müssen müssen mit dem virtuellen Computer Warteschlange \(VMQ\) kompatibel sein und eine Verknüpfung Geschwindigkeit von 10 Gbit/s oder mehr.

Weitere Informationen finden Sie in [die Verwendung von vRSS planen](vrss-plan.md).

## Funktioniert vRSS mit Hyper-threaded Prozessorkerne?

Nein. Ignorieren Hyper-threaded Prozessorkerne, vRSS und VMQ.

## Funktioniert vRSS für Host-virtuelle NICs \(vNICs\)?

Ja Verwenden Sie den **ManagementOS -** Parameter anstelle der Name des virtuellen Computers \(VM\) auf den **Satz-VMNetworkAdapter** Windows PowerShell-Befehl ", und" **Enable-NetAdapterRss** auf die Host-vNIC.

Weitere Informationen finden Sie unter [Windows PowerShell-Befehlen für RSS- und vRSS](vrss-wps.md).

## Muss ein virtuellen Computer wie viele logischen Prozessoren vRSS verwenden?

Virtuelle Computer benötigen mindestens zwei logischen Prozessoren \(LPs\) vRSS verwenden können.

Weitere Informationen finden Sie in [die Verwendung von vRSS planen](vrss-plan.md).

## Ist vRSS mit NIC-Teamvorgang kompatibel?

Ja Wenn Sie NIC-Teamvorgang verwenden, ist es wichtig, dass Sie ordnungsgemäß VMQ funktioniert mit den NIC-Teaming-Einstellungen konfigurieren. Ausführliche Informationen zur NIC-Teamvorgang Bereitstellung und Verwaltung finden Sie in der [NIC-Teamvorgang](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming).

## ist vRSS aktiviert, aber wie erkenne ich, ob es funktioniert? 

Sie müssen möglicherweise mitteilen, dass vRSS funktioniert, indem Sie im Task-Manager in einem virtuellen Computer öffnen und die Nutzung des virtuellen Prozessors anzeigen. Wenn mehrere Verbindungen eingerichtet, um den virtuellen Computer vorhanden sind, sehen Sie mehrere Core oben Nutzung von 0 %.

Da eine einzelne TCP-Sitzung Lastenausgleich über mehrere logische Prozessorkerne sein kann, muss Ihre virtuellen Computer mehrere TCP empfangen Sitzungen, bevor Sie feststellen können, ob vRSS arbeitet.

Wenn der virtuelle Computer mehrere TCP-Sitzungen erhält, aber nicht mehr als eine – ZIELSEITE Core oben Nutzung von 0 % angezeigt, stellen Sie sicher, dass Sie alle Vorbereitungsschritte zur im Thema [Planen Sie die Verwendung von vRSS](vrss-plan.md)abgeschlossen haben.

## Ich erhalte die Meldung der Host betrachten und nicht alle Prozessoren verwendet werden. Es sieht wie jede andere eine übersprungen wird.
  
Überprüfen Sie, ob Hyperthreading aktiviert ist. VMQ und vRSS dienen zur Hyper-threaded Kerne überspringen.

## Gibt es verschiedene Windows PowerShell-Befehlen für RSS- und vRSS?

Ja und Nein. Während Sie die gleichen Befehle für RSS in systemeigenen Hosts und RSS in virtuellen Computern verwenden, erfordert vRSS auch VMQ auf der physischen NIC - und für die virtuellen Computer und vRSS aktiviert werden, bei den Switch-Port aktiviert werden müssen.

Weitere Informationen finden Sie unter [Windows PowerShell-Befehlen für RSS- und vRSS](vrss-wps.md).

---
