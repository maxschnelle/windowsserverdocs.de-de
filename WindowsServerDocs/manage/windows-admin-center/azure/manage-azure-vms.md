---
title: Verwalten von virtuellen Azure-IaaS-Computern
description: Verwalten von Azure-IaaS-VMS mit Windows Admin Center (Project Honolulu)
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03ba06ca66c95825f13ff633d5b2bfac99acaa4c
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997452"
---
# <a name="manage-azure-iaas-virtual-machines-with-windows-admin-center"></a>Verwalten von virtuellen Azure IaaS-Computern mit Windows Admin Center

Mit Windows Admin Center kannst du deine virtuellen Azure-Computer und lokalen Computer verwalten. Es sind verschiedene Konfigurationen möglich. Wählen Sie die Konfiguration aus, die für Ihre Umgebung sinnvoll ist:
- [Verwalten von Azure-VMS über ein lokales Windows Admin Center-Gateway](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Verwalten von Azure-VMS über ein auf einem virtuellen Azure-Computer installiertes Windows Admin Center](#use-a-windows-admin-center-gateway-deployed-in-azure)

## <a name="manage-with-an-on-premises-windows-admin-center-gateway"></a>Verwalten mit einem lokalen Windows Admin Center-Gateway

Wenn Sie Windows Admin Center bereits auf einem lokalen Gateway (entweder unter Windows 10 oder Windows Server 2016) installiert haben, können Sie dieses Gateway zum Verwalten von virtuellen Computern unter Windows 10 oder Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 in Azure verwenden.

### <a name="connecting-to-vms-with-a-public-ip"></a>Herstellen einer Verbindung mit VMS mit einer öffentlichen IP-Adresse

Wenn Ihre Ziel-VMS (die VMs, die Sie mit Windows Admin Center verwalten möchten) über öffentliche IPS verfügen, fügen Sie Sie Ihrem Windows Admin Center-Gateway über die IP-Adresse oder den FQDN hinzu. Beachten Sie die folgenden Punkte:

- Sie müssen den WinRM-Zugriff auf den virtuellen Zielcomputer aktivieren, indem Sie den folgenden Befehl in PowerShell oder die Eingabeaufforderung auf der Ziel-VM ausführen:`winrm quickconfig`
- Wenn Sie nicht der Azure-VM angehören, verhält sich der virtuelle Computer wie ein Server in der Arbeitsgruppe. Daher müssen Sie sicherstellen, dass Sie das [Windows Admin Center in einer Arbeitsgruppe verwenden](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).
- Sie müssen auch eingehende Verbindungen mit Port 5985 für WinRM über HTTP aktivieren, damit Windows Admin Center die Ziel-VM verwalten kann:
  1. Führen Sie das folgende PowerShell-Skript auf der Ziel-VM aus, um eingehende Verbindungen mit Port 5985 auf dem Gast Betriebssystem zu ermöglichen:`Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

  2. Sie müssen den Port auch in Azure-Netzwerken öffnen:

     - Wählen Sie Ihren virtuellen Azure-Computer aus, klicken Sie auf **Netzwerk**und dann auf **eingehende Port Regel**
     - Stellen Sie sicher, dass im oberen Bereich des Bereichs **Eingangs Sicherheitsregel hinzufügen** die Option **einfach** ausgewählt ist.
     - Geben Sie im Feld **Port Bereiche** den Wert **5985**ein.

     Wenn Ihr Windows Admin Center-Gateway über eine statische IP-Adresse verfügt, können Sie auswählen, dass nur eingehender WinRM-Zugriff von Ihrem Windows Admin Center-Gateway aus für zusätzliche Sicherheit zulässig ist.
     Wählen Sie hierzu im oberen Bereich des Bereichs **Eingangs Sicherheitsregel hinzufügen** die Option **erweitert** aus.

     Wählen Sie unter **Quelle**die Option **IP-Adressen**aus, und geben Sie dann die IP-Quelladresse Ihres Windows Admin Center-Gateways ein.

     - Wählen Sie als **Protokoll** **TCP**aus.
     - Der Rest kann als Standard belassen werden.

> [!NOTE]
> Sie müssen eine benutzerdefinierte Portregel erstellen. Die von Azure-Netzwerken bereitgestellte WinRM-Portregel verwendet Port 5986 (über HTTPS) anstelle von 5985 (über HTTP).

### <a name="connecting-to-vms-without-a-public-ip"></a>Herstellen einer Verbindung mit virtuellen Computern ohne öffentliche IP-Adresse

Wenn Ihre virtuellen Azure-Zielcomputer nicht über öffentliche IP-Adressen verfügen und Sie diese virtuellen Computer über ein Windows Admin Center-Gateway verwalten möchten, das in Ihrem lokalen Netzwerk bereitgestellt wird, müssen Sie das lokale Netzwerk so konfigurieren, dass es eine Verbindung mit dem vnet herstellen kann, mit dem die Ziel-VMS verbunden sind. Hierfür gibt es drei Möglichkeiten: expressroute, Site-to-Site-VPN oder Punkt-zu-Standort-VPN. [Erfahren Sie, welche Konnektivitätsoption in Ihrer Umgebung sinnvoll ist.](/azure/vpn-gateway/vpn-gateway-plan-design)

>[!TIP]
>Wenn Sie ein Point-to-Site-VPN zum Verbinden Ihres Windows Admin Center-Gateways mit einem Azure-vnet verwenden möchten, um virtuelle Azure-Computer in diesem vnet zu verwalten, können Sie die [Azure-Netzwerk Adapter](https://aka.ms/WACNetworkAdapter) Funktion im Windows Admin Center verwenden. Stellen Sie dazu eine Verbindung mit dem Server her, auf dem Windows Admin Center installiert ist, navigieren Sie zum Netzwerk Tool, und wählen Sie "Azure-Netzwerk Adapter hinzufügen" aus. Wenn Sie die erforderlichen Details angeben und auf "einrichten" klicken, wird von Windows Admin Center ein Punkt-zu-Standort-VPN für das von Ihnen angegebene Azure-vnet konfiguriert. Anschließend können Sie über Ihr lokales Windows Admin Center-Gateway eine Verbindung mit virtuellen Azure-Computern herstellen und diese verwalten.

Stellen Sie sicher, dass WinRM auf ihren Ziel-VMS ausgeführt wird, indem Sie Folgendes in PowerShell oder über die Eingabeaufforderung auf dem virtuellen Zielcomputer ausführen:`winrm quickconfig`

Wenn Sie nicht der Azure-VM angehören, verhält sich der virtuelle Computer wie ein Server in der Arbeitsgruppe. Daher müssen Sie sicherstellen, dass Sie das [Windows Admin Center in einer Arbeitsgruppe verwenden](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).

Wenn Probleme auftreten, finden Sie unter Problembehandlung bei [Windows Admin Center](../support/troubleshooting.md) weitere Schritte, die für die Konfiguration erforderlich sind (z. b. Wenn Sie eine Verbindung mit einem lokalen Administrator Konto herstellen oder nicht mit der Domäne verknüpft sind).

## <a name="use-a-windows-admin-center-gateway-deployed-in-azure"></a>Verwenden eines in Azure bereitgestellten Windows Admin Center-Gateways

Sie können virtuelle Azure-Computer ohne lokale Abhängigkeit verwalten, indem Sie das Windows Admin Center in dem vnet bereitstellen, mit dem Ihre Ziel-VMS verbunden sind.

Zum Verwalten von virtuellen Computern außerhalb des vnets, auf dem das Windows Admin Center-Gateway bereitgestellt wird, müssen Sie eine vnet-zu-vnet-Konnektivität zwischen dem vnet des Windows Admin Center-Gateways und dem vnet der Zielserver einrichten. Sie können diese Konnektivität mit vnet-Peering, vnet-zu-vnet-Verbindung oder einer Site-to-Site-Verbindung herstellen. [Erfahren Sie mehr darüber, welche vnet-zu-vnet-Konnektivitätsoption in Ihrer Umgebung sinnvoll ist.](/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

Windows Admin Center kann auf einem vorhandenen oder neu bereitgestellten virtuellen Computer in Ihrer Umgebung installiert werden. Der virtuelle Computer, den Sie für die Installation des Windows Admin Centers auswählen, muss über eine öffentliche IP und einen DNS-Namen verfügen.

[Weitere Informationen zum Bereitstellen eines Windows Admin Center-Gateways in Azure](deploy-wac-in-azure.md)