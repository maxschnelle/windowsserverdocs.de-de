---
title: Verwalten von Azure IaaS virtuellen Computern
description: Verwalten von Azure IaaS-VMs mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6f162294076d7e12df09f31b0bbd7d9244abe679
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297015"
---
# Verwalten von Azure IaaS virtuellen Computern mit Windows Admin Center

Windows Admin Center können Sie um Ihre Azure-VMs sowie lokalen Computer zu verwalten. Es gibt verschiedene Konfigurationen möglich – wählen Sie die Konfiguration, die für Ihre Umgebung sinnvoll ist:
- [Verwalten von Azure-VMs aus einer lokalen Windows Admin Center-gateway](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Verwalten von Azure-VMs aus dem Windows Admin Center Gateway auf Azure-VM installiert](#use-a-windows-admin-center-gateway-deployed-in-azure)

## Verwalten von mit einem lokalen Windows Admin Center-gateway

Wenn Sie bereits Windows Admin Center auf lokale Gateway (entweder auf Windows 10 oder Windows Server 2016) installiert haben, können Sie dieses gleichen Gateway verwenden, zum Verwalten von Windows 10 oder Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 VMs in Azure. 

### Herstellen einer Verbindung mit virtuellen Computern mit einem öffentliche IP-Adresse

Wenn Ihr Ziel virtuellen Computern (VMs mit Windows Admin Center verwaltet werden sollen) öffentliche IP-Adressen haben, fügen sie Ihrem Windows Admin Center-Gateway hinzu, indem IP-Adresse oder FQDN. Es gibt verschiedene Aspekte berücksichtigt werden:

- Sie müssen WinRM Zugriff durch Ausführen des folgenden in PowerShell- oder die auf den Ziel-VM an Ihr Ziel-VM aktivieren: `winrm quickconfig`
- Wenn Sie die Azure-VM Domäne nicht geschehen, verhält sich die VM wie einem Server in einer Arbeitsgruppe, daher müssen Sie sicherstellen, dass Sie für die [Verwendung von Windows Admin Center in einer Arbeitsgruppe](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)berücksichtigen.
- Sie müssen auch eingehende Verbindungen mit Port 5985 für WinRM über HTTP in der Reihenfolge für Windows Admin Center zum Verwalten der Ziel-VM aktivieren:
   1. Führen Sie das folgende PowerShell-Skript auf den Ziel-VM auf eingehende Verbindungen Port 5985 das Gastbetriebssystem zu aktivieren:   
`Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

   2. Darüber hinaus müssen Sie den Port Azure-Netzwerks öffnen:

    - Wählen Sie Ihre Azure-VM, wählen Sie die **Netzwerke**, dann **eingehende Portregel hinzufügen**. 
    - Stellen Sie sicher, dass am oberen Rand des Bereichs **eingehende Sicherheit-Regel hinzufügen** **grundlegende** ausgewählt ist.
    - Geben Sie im Feld **Portbereichen** **5985**.
    
    Wenn Ihre Windows Admin Center-Gateway eine statische IP-Adresse verfügt, können Sie auswählen, damit nur eingehende WinRM Zugriff auf über das Windows Admin Center-Gateway für zusätzliche Sicherheit.
    Wählen Sie zu diesem Zweck **Erweitert** am oberen Rand des Bereichs **eingehende Sicherheit-Regel hinzufügen** .

    Wählen Sie für **Quelle**die **IP-Adressen**, und geben Sie die Quell-IP-Adresse, die das Windows Admin Center-Gateway entspricht.

    - Wählen Sie für das **Protokoll** **TCP**.
    - Der Rest kann als Standard gelassen werden.

> [!NOTE]
> Sie müssen eine benutzerdefinierte Portregel erstellen. Die WinRM Portregel von Azure Networking bereitgestellten verwendet Port 5986 (über HTTPS) anstelle von 5985 (über HTTP). 

### Herstellen einer Verbindung mit virtuellen Computern ohne eine öffentliche IP-Adresse

Wenn Ihr Ziel Azure-VMs nicht öffentliche IP-Adressen haben und Sie diese VMs von Windows Admin Center Gateway bereitgestellt in Ihrem lokalen Netzwerk verwalten möchten, müssen Sie Ihrem lokalen Netzwerk um Konnektivität mit dem vnet angefügt wird, auf dem Ziel VMs sind, konfigurieren verbunden. Es gibt 3 Möglichkeiten, die Sie dazu: ExpressRoute, Standort-zu-Standort-VPN oder Punkt-zu-Standort-VPN. [Erfahren Sie, welche Konnektivitätsoption in Ihrer Umgebung sinnvoll ist.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>Wenn Sie ein Punkt-zu-Standort-VPN verwenden, um das Windows Admin Center-Gateway mit einer Azure vnet angefügt wird zum Verwalten von Azure-VMs in diesem vnet angefügt wird eine Verbindung herstellen möchten, können Sie das [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter) -Feature in Windows Admin Center verwenden. Zu diesem Zweck Verbinden mit dem Server, auf dem Windows Admin Center installiert ist, navigieren Sie zu der Netzwerk-Tool aus, und wählen Sie "Hinzufügen von Azure-Netzwerkadapter". Wenn Sie die erforderlichen Details bereit, und klicken Sie auf "Set up", Windows Admin Center wird ein Punkt-zu-Standort-VPN mit der Azure vnet angefügt wird Sie angeben, nach denen, Sie können an und Verwalten von Azure-VMs aus Ihrer lokalen Windows Admin Center-Gateway zu konfigurieren.

Stellen Sie sicher, dass WinRM durch Ausführen des folgenden in PowerShell- oder die auf den Ziel-VM auf Ihr Ziel virtuellen Computer ausgeführt wird: `winrm quickconfig`

Wenn Sie die Azure-VM Domäne nicht geschehen, verhält sich die VM wie einem Server in einer Arbeitsgruppe, daher müssen Sie sicherstellen, dass Sie für die [Verwendung von Windows Admin Center in einer Arbeitsgruppe](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)berücksichtigen.

Wenn Sie Probleme auftreten, finden Sie in [Problembehandlung Windows Admin Center](../support/troubleshooting.md) , um festzustellen, ob zusätzliche Schritte für die Konfiguration erforderlich sind (z. B., wenn Sie eine Verbindung herstellen mithilfe eines lokalen Administratorkontos oder sind nicht-domänenverbundenen).

## Verwenden Sie Windows Admin Center Gateway bereitgestellt in Azure

Sie können Azure-VMs ohne alle lokalen Abhängigkeit verwalten, durch die Bereitstellung von Windows Admin Center in der vnet angefügt wird, in denen Ihre VMs Ziel verbunden sind. 

Zum Verwalten von VMs außerhalb der vnet angefügt wird auf dem Windows Admin Center-Gateway bereitgestellt wird, müssen Sie vnet angefügt wird vnet angefügt wird Konnektivität zwischen den vnet angefügt wird von Windows Admin Center-Gateway und die vnet angefügt wird der Zielserver herstellen. Sie können diese Konnektivität mit Peering vnet angefügt wird, vnet angefügt wird vnet angefügt wird, oder eine Standort-zu-Standort-Verbindung einrichten. [Erfahren Sie mehr über die Konnektivität vnet angefügt wird vnet angefügt wird Option in Ihrer Umgebung sinnvoll ist.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

Windows Admin Center kann auf eine vorhandene oder neu bereitgestellten virtuellen Computer in Ihrer Umgebung installiert werden. Der virtuelle Computer, die Sie für die Installation von Windows Admin Center auswählen müssen einen öffentliche IP-Adresse und DNS-Namen.

[Weitere Informationen zum Bereitstellen von Windows Admin Center Gateway in Azure](deploy-wac-in-azure.md)