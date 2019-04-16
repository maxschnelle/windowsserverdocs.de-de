---
title: Neues in DNS-Client unter Windows Server
description: Dieses Thema enthält eine Übersicht über neue Funktionen in DNS-Client in Windows Server und Windows10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: defe88fe2a1e4f5393be4d5d5938d9f5bfbfb5d6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Neues in DNS-Client unter WindowsServer 2016

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema wird beschrieben, die Funktionalität der Domain Name System (DNS)-Clients die neuen oder geänderten in Windows10 und Windows Server2016 und höheren Versionen dieser Betriebssysteme.
  
## <a name="updates-to-dns-client"></a>Updates für DNS-Client

**DNS-Client die Bindung**: In Windows 10 der DNS-Clientdienst eine verbesserte Unterstützung von Computern mit mehr als einer Netzwerkschnittstelle. DNS-Auflösung ist für mehrfach vernetzten Computer auf folgende Weise optimiert:  
  
-   Wenn ein DNS-Server, der für eine bestimmte Schnittstelle konfiguriert ist zum Auflösen einer DNS-Abfrage verwendet wird, wird der DNS-Clientdienst vor dem Senden der DNS-Abfrage für diese Schnittstelle gebunden.  
  
    Binden an eine bestimmte Schnittstelle, die DNS-Client kann deutlich Geben Sie die Schnittstelle, in der namensauflösung auftritt, Aktivierung von Anwendungen zur Optimierung der Kommunikation mit der DNS-Client über das Netzwerk-Schnittstelle.  
  
-   Wenn der DNS-Server, der verwendet wird, die durch eine Gruppenrichtlinie auf den Namen NRPT Resolution Policy Table () festgelegt wird, wird der DNS-Clientdienst nicht auf eine bestimmte Schnittstelle binden.  
  
> [!NOTE]  
> Änderungen an den DNS-Clientdienst in Windows10 sind auch auf Computern unter Windows Server2016 und höheren Versionen vorhanden.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Neues in DNS-Server unter WindowsServer 2016](What-s-New-in-DNS-Server.md)  
  

