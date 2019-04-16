---
title: RAS-Gateway für SDN
description: In diesem Thema können Sie weitere Informationen zu RAS-Gateway, ein softwarebasierter ist, mehrinstanzenfähiger, Border Gateway Protocol (BGP)-fähigen Router in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a32357a5-ab1a-4a4c-848a-7a4ed65b1921
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 052911dcd52df82ef4e259de0c64078c54f00195
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="ras-gateway-for-sdn"></a>RAS-Gateway für SDN

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zu RAS-Gateway, die ein softwarebasierter, mehrinstanzenfähiger, Border Gateway Protocol (BGP) fähigen Router in Windows Server2016 ist, die für Clouddienstanbieter (CSPs) und Unternehmen, die mehrere Mandanten virtuelle Netzwerke mithilfe von Hyper-V-Netzwerkvirtualisierung hosten entwickelt wurde.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema sind die folgenden RAS-Gateway-Themen zur Verfügung.  
>   
> -   [Neuerungen beim RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS-Gateway: Bereitstellungsarchitektur](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS-Gateway: hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [Border Gateway Protocol & 40; BGP & 41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell-Befehlsreferenz](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
In Windows Server2016 leitet die RAS-Gateway Netzwerkdatenverkehr zwischen dem physischen Netzwerk und VM-Netzwerkressourcen, unabhängig davon, wo sich die Ressourcen befinden. RAS-Gateway können Sie Netzwerkdatenverkehr zwischen physischen und virtuellen Netzwerken an demselben physischen Standort oder an vielen verschiedenen physischen Standorten über das Internet weiterzuleiten.  
  
Mehrinstanzenfähigkeit bezeichnet die Fähigkeit einer Cloud-Infrastruktur, um die Arbeitsauslastungen virtueller Computer mehrerer Mandanten zu unterstützen, noch zu isolieren sie voneinander, während alle Arbeitslasten auf der gleichen Infrastruktur ausgeführt. Mehrere Arbeitsauslastungen eines einzelnen Mandanten können interconnect und Remote verwaltet werden, aber diese Systeme werden nicht mit den Arbeitsauslastungen anderer Mandanten interconnect, noch können andere Mandanten Remote verwalten.  
  
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>Voraussetzungen für die Installation von RAS-Gateway für SDN  
Die Windows-Benutzeroberfläche können Sie um RAS-Dienst zu installieren, wenn Sie im mehrinstanzenmodus für die Verwendung mit SDN RAS-Gateway bereitstellen möchten. Stattdessen müssen Sie Windows PowerShell verwenden.  
  
Aber bevor Sie RAS-Gateway mit Windows PowerShell installieren können, müssen Sie Windows PowerShell verwenden, um Hinzufügen der **RemoteAccess** Windows-Feature. Führen Sie dazu den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung.  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
Mit diesem Befehl wird die **RemoteAccess** Feature und die Windows PowerShell-Befehle für das Feature.  
  
Nach dem Hinzufügen **RemoteAccess** an den Server Remotezugriff als RAS-Gateway mit mehrinstanzenmodus und Border Gateway Protocol (BGP) installieren.  
  
Weitere Informationen finden Sie im Windows PowerShell-Referenzthema [Install-RemoteAccess](https://technet.microsoft.com/library/hh918408.aspx).  
  
## <a name="ras-gateway-features"></a>RAS-Gateway-Funktionen  
Folgende RAS-Gateway-Funktionen in Windows Server2016 werden. Sie können RAS-Gateway in Pools mit hoher Verfügbarkeit bereitstellen, die alle diese Features gleichzeitig verwenden.  
  
-   **Standort-zu-Standort-VPN-**. Dieses Feature RAS-Gateway können Sie zwei Netzwerken an verschiedenen physischen Standorten über das Internet zu verbinden, indem Sie eine Standort-zu-Standort-VPN-Verbindung. CSPs, die viele Mandanten in ihren Rechenzentren hosten, bietet RAS-Gateway eine Lösung mehrinstanzenfähige Mandanten zugreifen und ihre Ressourcen über Standort-zu-Standort-VPN-Verbindungen von Remotestandorten verwalten und, mit der Fluss von Netzwerkdatenverkehr zwischen virtuellen Ressourcen in Ihrem Rechenzentrum und ihre physischen Netzwerk.  
  
-   **Punkt-zu-Standort-VPN-**. Dieses Feature RAS-Gateway kann Mitarbeiter des Unternehmens oder Administratoren von Remotestandorten aus eine Verbindung mit dem Netzwerk Ihrer Organisation.  Zur Bereitstellung von mehrinstanzenfähigen können Mandanten Netzwerkadministratoren Punkt-zu-Standort-VPN-Verbindungen Sie Ressourcen im CSP-Datencenter im virtuellen Netzwerk zugreifen.  
  
-   **GRE-Tunneling**. Generic Routing Encapsulation (GRE)-basierte Tunnel ermöglichen Verbindungen zwischen virtuellen mandantennetzwerken und externen Netzwerken. Da das GRE-Protokoll Lightweight und Unterstützung für GRE auf die meisten Netzwerkgeräte verfügbar ist, wird es perfekt für das Tunneling, in denen keine Verschlüsselung von Daten erforderlich ist. GRE-Unterstützung für Standort-zu-Standort (S2S)-Tunnel behebt das Problem der Weiterleitung zwischen virtuellen mandantennetzwerken und externen mandantennetzwerken über ein mehrinstanzenfähiges Gateway, wie weiter unten in diesem Thema beschrieben.  
  
-   **Dynamisches Routing mit Border Gateway Protocol (BGP)**. BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da er ein dynamisches Routingprotokoll ist, lernt automatisch Routen zwischen Standorten, die mithilfe von Standort-zu-Standort-VPN-Verbindungen verbunden sind. Wenn Ihre Organisation mehrere Standorte, die verfügt mithilfe von BGP-fähigen Routern, z.B. RAS-Gateway verbunden sind, kann BGP die Router automatisch berechnet und gültige Routen miteinander im Fall einer Störung des Netzwerks oder Fehler verwenden. Weitere Informationen finden Sie unter [RFC 4271](https://tools.ietf.org/html/rfc4271).  
  

  


