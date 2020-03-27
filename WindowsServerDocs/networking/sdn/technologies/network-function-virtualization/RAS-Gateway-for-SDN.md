---
title: RAS-Gateway für SDN
description: In diesem Thema erfahren Sie mehr über das RAS-Gateway, ein softwarebasierter, mehr Instanzen fähiger Border Gateway Protocol (BGP)-fähiger Router in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a32357a5-ab1a-4a4c-848a-7a4ed65b1921
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 415a5f4728b1b08e59630935e47f22d74b0267e8
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312933"
---
# <a name="ras-gateway-for-sdn"></a>RAS-Gateway für SDN

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016 # # RAS-Gateway für Sdn  


RAS-Gateway ist ein softwarebasierter, mehr Instanzen fähiger, Border Gateway Protocol (BGP)-fähiger Router für clouddienstanbieter (Cloud Service Providers, CSPs) und Unternehmen, die mehrere virtuelle Mandanten Netzwerke mithilfe der Hyper-V-Netzwerkvirtualisierung hosten. RAS-Gateways leiten Netzwerk Datenverkehr zwischen dem physischen Netzwerk und VM-Netzwerkressourcen weiter, unabhängig vom Standort. Sie können den Netzwerk Datenverkehr an demselben physischen Standort oder an vielen verschiedenen Speicherorten weiterleiten.   

Mehr Instanzen Fähigkeit ist die Fähigkeit einer cloudinfrastruktur, die Arbeits Auslastungen virtueller Computer mehrerer Mandanten zu unterstützen, Sie aber voneinander zu isolieren, während alle Arbeits Auslastungen in der gleichen Infrastruktur ausgeführt werden. Mehrere Arbeitsauslastungen eines einzelnen Mandanten können miteinander verbunden und remote verwaltet werden. Es gibt jedoch keine Verbindung zwischen diesen Systemen und den Arbeitsauslastungen anderer Mandanten, und auch die Remoteverwaltung durch andere Mandanten ist nicht möglich.

  
> [!NOTE]  
> Zusätzlich zu diesem Thema sind die folgenden Themen zum RAS-Gateway verfügbar.  
>   
> -   [Neues beim RAS-Gateway](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [RAS-Gateway-Bereitstellungs Architektur](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [RAS-Gateway: Hohe Verfügbarkeit](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [Border Gateway Protocol &#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [BGP-Befehlsreferenz für Windows PowerShell](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
    
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>Voraussetzungen für die Installation des RAS-Gateways für Sdn  
Sie können den Remote Zugriff nicht mithilfe der Windows-Benutzeroberfläche installieren, wenn Sie das RAS-Gateway im mehr Instanzen fähigen Modus für die Verwendung mit Sdn bereitstellen möchten. Stattdessen müssen Sie Windows PowerShell verwenden.  
  
Aber bevor Sie das RAS-Gateway mithilfe von Windows PowerShell installieren können, müssen Sie Windows PowerShell verwenden, um das Windows-Feature " **remoteaccess** " hinzuzufügen. Führen Sie hierzu den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung aus.  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
Mit diesem Befehl werden die Funktionen **remoteaccess** und die Windows PowerShell-Befehle für das Feature hinzugefügt.  
  
Nachdem Sie dem Server **remoteaccess** hinzugefügt haben, können Sie den Remote Zugriff als RAS-Gateway mit dem mehr Instanzen fähigen Modus und Border Gateway Protocol (BGP) installieren.  
  
Weitere Informationen finden Sie im Windows PowerShell-Referenz Thema [install-remoteaccess](https://technet.microsoft.com/library/hh918408.aspx).  
  
## <a name="ras-gateway-features"></a>RAS-Gatewayfeatures  
Im folgenden finden Sie RAS-Gatewayfeatures in Windows Server 2016. Sie können das RAS-Gateway in Pools mit hoher Verfügbarkeit bereitstellen, die alle diese Features gleichzeitig verwenden.  
  
-   **Site-to-Site-VPN**. Diese RAS-Gatewayfunktion ermöglicht es Ihnen, zwei Netzwerke an verschiedenen physischen Standorten über das Internet mithilfe einer Site-to-Site-VPN-Verbindung zu verbinden. Für CSPs, die viele Mandanten in Ihrem Rechenzentrum hosten, bietet das RAS-Gateway eine mehrinstanzfähige Gatewaylösung, die ihren Mandanten den Zugriff auf und die Verwaltung Ihrer Ressourcen über Standort-zu-Standort-VPN-Verbindungen von Remote Standorten ermöglicht und den Netzwerk Datenverkehr zwischen virtuelle Ressourcen in Ihrem Daten Center und in Ihrem physischen Netzwerk.  
  
-   **Punkt-zu-Standort-VPN**. Diese RAS-Gatewayfunktion ermöglicht es Organisations Mitarbeitern oder Administratoren, von Remote Standorten aus eine Verbindung mit dem Netzwerk Ihrer Organisation herzustellen.  Für bereit Stellungen mit mehreren Mandanten können Mandanten Netzwerkadministratoren Punkt-zu-Standort-VPN-Verbindungen verwenden, um auf virtuelle Netzwerkressourcen im CSP-Daten Center zuzugreifen.  
  
-   **GRE-Tunnelung**. Durch GRE-basierte Tunnel (Generic Routing Kapselung) können Verbindungen zwischen virtuellen Mandanten Netzwerken und externen Netzwerken ermöglicht werden. Da es sich beim GRE-Protokoll um ein Lightweight-Protokoll handelt und die meisten Netzwerkgeräte GRE-Unterstützung bieten, ist es perfekt für das Tunneling geeignet, wenn keine Datenverschlüsselung erforderlich ist. Die GRE-Unterstützung in Standort-zu-Standort-Tunneln (S2S) löst das Problem der Weiterleitung zwischen virtuellen Mandanten Netzwerken und externen Mandanten Netzwerken mithilfe eines mehr Instanzen fähigen Gateways, wie weiter unten in diesem Thema beschrieben.  
  
-   **Dynamisches Routing mit Border Gateway Protocol (BGP)** . BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da es ein dynamisches Routingprotokoll ist, das automatisch Routen zwischen Standorten lernt, die über die Standort-zu-Standort-VPN-Verbindungen verbunden sind. Wenn Ihre Organisation über mehrere Standorte verfügt, die mithilfe von BGP-fähigen Routern wie RAS-Gateway verbunden sind, ermöglicht BGP den Routern die automatische Berechnung und Verwendung gültiger Routen untereinander im Falle einer Netzwerk Unterbrechung oder eines Fehlers. Weitere Informationen finden Sie unter [RFC 4271](https://tools.ietf.org/html/rfc4271).  
  

  


