---
title: Neues in DNS-Client unter WindowsServer
description: Dieses Thema bietet einen Überblick über die neuen Funktionen in DNS-Client unter Windows Server und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 34b1a64465e217fbd7e6b3ae55e89832a7a4e48c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860561"
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Neues im DNS-Client unter Windows Server 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt die Clientfunktionalität der Domain Name System (DNS)-die neuen oder geänderten in Windows 10 und Windows Server 2016 und höhere Versionen dieser Betriebssysteme.
  
## <a name="updates-to-dns-client"></a>Updates für DNS-Client

**DNS-Client-dienstbindung**: In Windows 10 bietet der DNS-Clientdienst die verbesserte Unterstützung für Computer mit mehr als eine Netzwerkschnittstelle. Bei mehrfach vernetzten Computern ist der DNS-Auflösung auf folgende Weise optimiert:  
  
-   Wenn ein DNS-Server, der auf eine bestimmte Schnittstelle konfiguriert ist, lösen eine DNS-Abfrage verwendet wird, wird der DNS-Clientdienst vor dem Senden der DNS-Abfrage für diese Schnittstelle binden.  
  
    Geben Sie die Schnittstelle, in der namensauflösung auftritt, Aktivierung von Anwendungen zur Optimierung der Kommunikation mit dem DNS-Client über dieses Netzwerk-Schnittstelle, durch die Bindung auf eine bestimmte Schnittstelle, die DNS-Client kann deutlich.  
  
-   Wenn der DNS-Server, der verwendet wird, die durch eine Gruppenrichtlinien-Einstellung aus der NRPT Name Resolution Policy Table () festgelegt ist, wird der DNS-Clientdienst nicht auf eine bestimmte Schnittstelle binden.  
  
> [!NOTE]  
> Änderungen an den DNS-Clientdienst in Windows 10 sind auch auf Computern unter Windows Server 2016 und höher vorhanden.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Neues in DNS-Server unter WindowsServer 2016](What-s-New-in-DNS-Server.md)  
  

