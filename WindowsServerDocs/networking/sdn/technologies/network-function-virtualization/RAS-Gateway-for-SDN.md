---
title: RAS-Gateway für SDN
description: Sie können in diesem Thema erfahren Sie RAS-Gateway, ein softwarebasierter ist, mehrinstanzenfähiger, Border Gateway Protocol (BGP)-fähiger Router in Windows Server 2016 verwenden.
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
ms.openlocfilehash: 4f1ad0b3f0b5921a53faa8a45baae9f0b8711873
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856271"
---
# <a name="ras-gateway-for-sdn"></a>RAS-Gateway für SDN

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016 ## RAS-Gateway für SDN  


RAS-Gateway ist eine softwarebasierte, mehrinstanzenfähige, werden Border Gateway Protocol (BGP)-fähiger Router für Clouddienstanbieter (CSPs) und Unternehmen, Hosten mehrerer Mandanten virtueller Netzwerke mithilfe der Hyper-V-Netzwerkvirtualisierung. RAS-Gateways, leitet Netzwerkdatenverkehr zwischen dem physischen Netzwerk und VM-Netzwerkressourcen weiter, unabhängig davon, wo. Sie können den Netzwerkdatenverkehr am am selben physischen Standort oder an vielen unterschiedlichen Standorten weiterleiten.   

Mehrinstanzenfähigkeit ist die Fähigkeit einer Cloud-Infrastruktur zur Unterstützung von arbeitsauslastungen virtueller Computer mehrerer Mandanten isolieren sie noch voneinander, während alle arbeitsauslastungen in der gleichen Infrastruktur ausgeführt. Mehrere Arbeitsauslastungen eines einzelnen Mandanten können miteinander verbunden und remote verwaltet werden. Es gibt jedoch keine Verbindung zwischen diesen Systemen und den Arbeitsauslastungen anderer Mandanten, und auch die Remoteverwaltung durch andere Mandanten ist nicht möglich.

  
> [!NOTE]  
> Zusätzlich zu diesem Thema sind die folgenden Themen der RAS-Gateway verfügbar.  
>   
> -   [Neuerungen beim RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS-Gateway: Bereitstellungsarchitektur](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS-Gateway: Hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [Border Gateway Protocol &#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP Windows PowerShell-Befehlsreferenz](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
    
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>Voraussetzungen für die Installation von RAS-Gateway für SDN  
Sie können nicht die Windows-Schnittstelle verwenden, um Remotezugriff zu installieren, wenn RAS-Gateway im mehrinstanzenmodus für die Verwendung mit SDN bereitgestellt werden soll. Stattdessen müssen Sie Windows PowerShell verwenden.  
  
Aber bevor Sie die RAS-Gateway mithilfe von Windows PowerShell installieren können, müssen Sie Windows PowerShell verwenden, Hinzufügen der **RemoteAccess** Windows-Funktion. Zu diesem Zweck führen Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung aus.  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
Dieser Befehl fügt die **RemoteAccess** Feature und die Windows PowerShell-Befehle für die Funktion.  
  
Nachdem Sie hinzugefügt haben **RemoteAccess** mit Ihrem Server Remotezugriff als RAS-Gateway mit den mehrinstanzenmodus und Border Gateway Protocol (BGP) installieren.  
  
Weitere Informationen finden Sie im Referenzthema für die Windows PowerShell [Install-RemoteAccess--](https://technet.microsoft.com/library/hh918408.aspx).  
  
## <a name="ras-gateway-features"></a>RAS-Gateway – Features  
Im folgenden werden RAS-Gateway-Funktionen in Windows Server 2016. Sie können die RAS-Gateway in Pools für hohe Verfügbarkeit bereitstellen, die alle diese Funktionen gleichzeitig verwenden.  
  
-   **Standort-zu-Standort-VPN-**. Dieses Feature für die RAS-Gateway können Sie zwei Netzwerke an verschiedenen physischen Standorten mit einer Standort-zu-Standort-VPN-Verbindung über das Internet zu verbinden. Für CSPs, die viele Mandanten in ihren Rechenzentren hosten, stellt der RAS-Gateway eine mehrinstanzenfähige gatewaylösung Mandanten zugreifen auf und verwalten ihre Ressourcen über Standort-zu-Standort-VPN-Verbindungen von Remotestandorten aus, und, mit der Fluss von Netzwerkdatenverkehr zwischen virtuellen Ressourcen in Ihrem Datencenter und dem physischen Netzwerk.  
  
-   **Punkt-zu-Standort-VPN-**. Dieses Feature für die RAS-Gateway kann Mitarbeiter des Unternehmens "oder" Administratoren ", von Remotestandorten aus eine Verbindung mit dem Netzwerk Ihrer Organisation.  Bei mehrinstanzenfähigen Bereitstellungen können Netzwerk Mandantenadministratoren Punkt-zu-Standort-VPN-Verbindungen Sie Ressourcen des virtuellen Netzwerks im CSP-Datencenter zugreifen.  
  
-   **GRE-Tunneling**. Generic Routing Encapsulation (GRE) basierte Tunnel ermöglichen Verbindungen zwischen virtuellen mandantennetzwerken und externen Netzwerken. Da es sich beim GRE-Protokoll um ein Lightweight-Protokoll handelt und die meisten Netzwerkgeräte GRE-Unterstützung bieten, ist es perfekt für das Tunneling geeignet, wenn keine Datenverschlüsselung erforderlich ist. GRE-Unterstützung (S2S)-Standort-zu-Standort-Tunnel löst das Problem der Weiterleitung zwischen virtuellen mandantennetzwerken und externen mandantennetzwerken über ein Gateway mit mehreren Mandanten an, wie weiter unten in diesem Thema beschrieben.  
  
-   **Dynamisches routing mit Border Gateway Protocol (BGP)**. BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da es ein dynamisches Routingprotokoll ist, das automatisch Routen zwischen Standorten lernt, die über die Standort-zu-Standort-VPN-Verbindungen verbunden sind. Wenn Ihre Organisation über mehrere Standorte, die verfügt mithilfe von BGP-fähigen Routern, z. B. RAS-Gateway verbunden sind, kann BGP die Router automatisch berechnen und verwenden die gültige Routen miteinander im Falle einer Störung des Netzwerks oder Fehler. Weitere Informationen finden Sie unter [RFC 4271](https://tools.ietf.org/html/rfc4271).  
  

  


