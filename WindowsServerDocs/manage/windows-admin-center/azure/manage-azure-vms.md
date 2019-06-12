---
title: Verwalten von Azure IaaS-Computer
description: Verwalten von Azure IaaS-VMs mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ac98f42c4ad5606cc8d2b142f209f9bdb2b9611c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445899"
---
# <a name="manage-azure-iaas-virtual-machines-with-windows-admin-center"></a>Verwalten von Azure-IaaS-virtuellen Computern mit Windows Admin Center

Sie können Windows Admin Center verwenden, zum Verwalten Ihrer virtuellen Azure-Computern sowie auf lokalen Computern. Es sind mehrere unterschiedliche Konfigurationen möglich – wählen Sie die Konfiguration, die für Ihre Umgebung sinnvoll ist:
- [Verwalten von Azure-VMs über ein Gateway des lokalen Windows Admin Center](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Verwalten von Azure-VMs über ein Windows Admin Center-Gateway auf einer Azure-VM installiert](#use-a-windows-admin-center-gateway-deployed-in-azure)

## <a name="manage-with-an-on-premises-windows-admin-center-gateway"></a>Mit einem Gateway des lokalen Windows Admin Center verwalten

Wenn Sie bereits Windows Admin Center auf einem lokalen Gateway (entweder unter Windows 10 oder Windows Server 2016) installiert haben, können Sie diese dasselbe Gateway verwenden, zum Verwalten von Windows 10 oder Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 Virtuelle Computer in Azure. 

### <a name="connecting-to-vms-with-a-public-ip"></a>Herstellen einer Verbindung mit virtuellen Computern mit einer öffentlichen IP-Adresse

Wenn Ihr Ziel-VMs (die virtuellen Computer mit Windows Admin Center verwalten möchten), öffentliche IP-Adressen verfügen, fügen sie IP-Adresse oder FQDN mit dem Windows Admin Center-Gateway hinzu. Es gibt einige Überlegungen zu berücksichtigen:

- Sie müssen WinRM-Zugriffs auf Ihre Ziel-VM aktivieren, durch Ausführen des folgenden Befehls in PowerShell oder die Eingabeaufforderung auf dem virtuellen Zielcomputer: `winrm quickconfig`
- Wenn Sie mit der Azure-VM domänenverknüpfung nicht getan haben, der virtuellen Computer verhält sich wie ein Server in einer Arbeitsgruppe, damit Sie sicherstellen, dass Sie berücksichtigen müssen [mithilfe von Windows Admin Center in einer Arbeitsgruppe](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).
- Sie müssen auch eingehende Verbindungen an Port 5985 für WinRM in der Reihenfolge für Windows Admin Center zum Verwalten der Ziels-VM über HTTP aktivieren:
  1. Führen Sie das folgende PowerShell-Skript auf der Ziel-VM, um eingehende Verbindungen an Port 5985 unter dem Gastbetriebssystem zu aktivieren:   
     `Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

  2. Darüber hinaus müssen Sie den Port in Azure-Netzwerken öffnen:

     - Wählen Sie Ihre Azure-VM, **Networking**, klicken Sie dann **hinzufügen eingehender Portregel**. 
     - Stellen Sie sicher **grundlegende** ausgewählt ist, am oberen Rand der **eingangssicherheitsregel hinzufügen** Bereich.
     - In der **Port Bereiche** Feld **5985**.
    
     Wenn Ihr Gateway Windows Admin Center eine statische IP-Adresse verfügt, können Sie auswählen, um nur eingehenden Zugriffs auf WinRM von Ihrem Windows Admin Center-Gateway zur Erhöhung der Sicherheit zu ermöglichen.
     Wählen Sie zu diesem Zweck **erweitert** am oberen Rand der **eingangssicherheitsregel hinzufügen** Bereich.

     Für **Quelle**Option **IP-Adressen**, geben Sie dann auf die Quell-IP-Adresse, die mit dem Gateway Windows Admin Center entspricht.

     - Für **Protokoll** wählen **TCP**.
     - Die übrigen kann als Standard übernommen werden.

> [!NOTE]
> Sie müssen eine benutzerdefinierte Portregel erstellen. Die WinRM-Port-Regel bereitgestellt, die von Azure-Netzwerke verwendet Port 5986 (HTTPS) anstelle von 5985 (über HTTP). 

### <a name="connecting-to-vms-without-a-public-ip"></a>Herstellen einer Verbindung mit virtuellen Computern ohne eine öffentliche IP-Adresse

Wenn Ihr Ziel Azure-VMs nicht öffentliche IP-Adressen, und Sie diese virtuellen Computer über ein Gateway für Windows Admin Center in Ihrem lokalen Netzwerk verwalten möchten, müssen Sie zum Konfigurieren Ihres lokalen Netzwerks über eine Verbindung mit dem VNet, auf denen die Ziel-VMs sind, verfügen verbunden. Es gibt 3 Möglichkeiten, die Sie dies tun können: ExpressRoute-Standort-zu-Standort-VPN- oder Punkt-zu-Standort-VPN. [Erfahren Sie, welche Verbindungsoption in Ihrer Umgebung sinnvoll ist.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>Wenn Sie möchten ein Punkt-zu-Standort-VPN zum Verbinden Ihres Windows Admin Center-Gateways mit einem Azure-VNet zum Verwalten von Azure-VMs, VNet, Sie verwenden können, verwenden die [Netzwerkadapter für die Azure](https://aka.ms/WACNetworkAdapter) -Feature in Windows Admin Center. Zu diesem Zweck Verbinden mit dem Server, auf dem Windows Admin Center installiert ist, navigieren Sie zu der Netzwerk-Tool aus, und wählen Sie "Azure – Netzwerkadapter hinzufügen". Wenn Sie die erforderlichen Details bereitzustellen, und klicken Sie auf "einrichten", Windows Admin Center wird ein Punkt-zu-Standort-VPN mit dem Azure-VNet, das Sie angeben, nach dem, Sie können Herstellen einer Verbindung mit und Verwalten von Azure-VMs von Ihrem lokalen Windows Admin Center-Gateway konfigurieren.

Stellen Sie sicher, dass WinRM auf dem Zielcomputer VMs durch Ausführen des folgenden Befehls in PowerShell oder die Eingabeaufforderung auf dem virtuellen Zielcomputer ausgeführt wird: `winrm quickconfig`

Wenn Sie mit der Azure-VM domänenverknüpfung nicht getan haben, der virtuellen Computer verhält sich wie ein Server in einer Arbeitsgruppe, damit Sie sicherstellen, dass Sie berücksichtigen müssen [mithilfe von Windows Admin Center in einer Arbeitsgruppe](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).

Wenn Probleme auftreten, wenden Sie sich an [Problembehandlung Windows Admin Center](../support/troubleshooting.md) um festzustellen, ob zusätzliche Schritte für die Konfiguration erforderlich sind (z. B., wenn Sie eine Verbindung mit einem lokalen Administratorkonto an, oder sind nicht mit domänenverknüpfung).

## <a name="use-a-windows-admin-center-gateway-deployed-in-azure"></a>Verwenden von Gateways in Azure bereitgestellten Windows Admin Center

Sie können Azure-VMs ohne eine Abhängigkeit lokal verwalten, durch die Bereitstellung von Windows Admin Center im VNet, in dem Ihre Ziel-VMs verbunden sind. 

Zum Verwalten von VMs außerhalb des VNet auf dem das Gateway Windows Admin Center bereitgestellt wird, müssen Sie die VNet-zu-VNet-Konnektivität zwischen dem VNet des Gateways Windows Admin Center und dem VNet der Zielserver einrichten. Sie können diese Konnektivität mit VNet-Peering, VNet-zu-VNet-Verbindung oder eine Standort-zu-Standort-Verbindung herstellen. [Erfahren Sie mehr über die VNet-zu-VNet-Konnektivität Option in Ihrer Umgebung sinnvoll ist.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

Windows Admin Center kann auf einem vorhandenen oder neu bereitgestellte Computer in Ihrer Umgebung installiert werden. Der virtuelle Computer, die Sie für die Installation von Windows Admin Center auswählen, müssen einen öffentlichen IP-Adresse und DNS-Namen.

[Weitere Informationen zum Bereitstellen eines Windows Admin Center-Gateways in Azure](deploy-wac-in-azure.md)