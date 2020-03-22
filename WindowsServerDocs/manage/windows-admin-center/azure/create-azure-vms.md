---
title: Bereitstellen von Azure-Virtual Machines mithilfe des Windows Admin Centers
description: Bereitstellen virtueller Azure-Computer mit Windows Admin Center. Konfigurieren von virtuellen Azure-Computern als Teil der von Windows Admin Center verwalteten Szenarien
ms.technology: manage
ms.topic: article
author: nedpyle
ms.author: nedpyle
manager: jgerend
ms.date: 01/28/2020
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 08135ed3454bb22db1c2b0fa3a14a8342fbc2dab
ms.sourcegitcommit: 8b801bd86e2ddf8255899b11f547daa920e5f651
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80110663"
---
# <a name="deploy-azure-virtual-machines-from-within-windows-admin-center"></a>Bereitstellen von virtuellen Azure-Computern innerhalb des Windows Admin Centers

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In Windows Admin Center, Version 1910, können Sie virtuelle Azure-Computer bereitstellen. Dadurch wird die VM-Bereitstellung in von Windows Admin Center verwaltete Workloads wie [Speicher Migrationsdienst](../../../storage/storage-migration-service/overview.md) und [Speicher Replikat](../../../storage/storage-replica/storage-replica-overview.md)integriert. Anstatt vor dem Bereitstellen der Arbeitsauslastung neue Server und VMS im Azure-Portal zu entwickeln, und möglicherweise Fehlende erforderliche Schritte und Konfiguration: das Windows Admin Center kann den virtuellen Azure-Computer bereitstellen, seinen Speicher konfigurieren, ihn Ihrer Domäne hinzufügen, Rollen installieren und richten Sie dann Ihr verteiltes System ein. Sie können auch neue virtuelle Azure-Computer ohne Arbeitsauslastung auf der Windows Admin Center-Verbindungs Seite bereitstellen.

Windows Admin Center verwaltet auch eine Vielzahl von Azure-Diensten. [Erfahren Sie mehr über die Azure-Integrationsoptionen, die im Windows Admin Center verfügbar sind](../plan/azure-integration-options.md).

## <a name="scenarios"></a>Szenarien

Windows Admin Center Version 1910 die Azure-VM-Bereitstellung unterstützt die folgenden Szenarien:

- [Speicher Migrationsdienst](../../../storage/storage-migration-service/overview.md)
- [Speicherreplikat](../../../storage/storage-replica/storage-replica-overview.md)
- [Neuer eigenständiger Server (ohne Rollen)](index.md#extend-on-premises-capacity-with-azure)

## <a name="requirements"></a>Voraussetzungen

Zum Erstellen eines neuen virtuellen Azure-Computers innerhalb des Windows Admin Centers benötigen Sie Folgendes:

- Ein [Azure-Abonnement](https://azure.microsoft.com).
- Ein [Windows Admin Center-Gateway, das bei Azure registriert](azure-integration.md) ist
- Eine vorhandene [Azure-Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) , für die Sie über die Berechtigung erstellen verfügen.
- Eine vorhandene [Azure-Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) und ein Subnetz.
- Eine [Azure Express Route](https://azure.microsoft.com/services/expressroute/) -oder [Azure-VPN-Lösung](https://azure.microsoft.com/services/vpn-gateway/) , die an das virtuelle Netzwerk und Subnetz gebunden ist und die Konnektivität von Azure-VMS mit Ihren lokalen Clients, Domänen Controllern, dem Windows Admin Center-Computer und allen Servern zulässt, die im Rahmen einer workloadbereitstellung mit diesem virtuellen Computer kommunizieren müssen. Wenn Sie z. b. den Speicher Migrationsdienst zum Migrieren von Speicher zu einem virtuellen Azure-Computer verwenden möchten, müssen der Orchestrator-Computer und der Quellcomputer beide in der Lage sein, eine Verbindung mit dem virtuellen Azure-Zielcomputer aufzunehmen, zu dem

## <a name="usage"></a>Verwendung

Azure-VM-Bereitstellungs Schritte und-Assistenten variieren je nach Szenario. Ausführliche Informationen zum Gesamtszenario finden Sie in der Dokumentation der Arbeitsauslastung.

### <a name="deploying-azure-vms-as-part-of-storage-migration-service"></a>Bereitstellen von Azure-VMS als Teil des Speicher Migrations Dienstanbieter

1. Führen Sie über das Tool " *Storage Migration Service* " im Windows Admin Center eine Inventur von mindestens einem Quell Server durch.
2. Wenn Sie sich in der *Übertragungsdaten* Phase befinden, wählen Sie auf der Seite *Ziel angeben* die Option **neuen virtuellen Azure** -Computer erstellen aus, und klicken Sie dann auf **VM erstellen**.<br><br>
Dadurch wird ein schrittweises Erstellungs Tool gestartet, mit dem ein Windows Server 2012 R2-, Windows Server 2016-oder Windows Server 2019-virtueller Azure-Computer als Ziel für die Migration ausgewählt wird. Storage Migration Service bietet Empfohlene VM-Größen für Ihre Quelle, Sie können Sie jedoch außer Kraft setzen, indem Sie auf **alle Größen**anzeigen klicken.
<br><br>Quell Serverdaten werden auch verwendet, um Ihre verwalteten Datenträger und Ihre Dateisysteme automatisch zu konfigurieren und ihren neuen virtuellen Azure-Computer mit Ihrer Active Directory Domäne zu verknüpfen. Wenn es sich bei der VM um Windows Server 2019 (was wir empfehlen) handelt, installiert das Windows Admin Center die Proxy Funktion des Storage-Migrations Dienstanbieter. Nachdem die Azure-VM erstellt wurde, kehrt das Windows Admin Center zum normalen Übertragungs Workflow für den Speicher Migrationsdienst zurück.  

### <a name="deploying-azure-vms-as-part-of-storage-replica"></a>Bereitstellen von virtuellen Azure-Computern

1. Wählen Sie aus dem *Speicher Replikat* Tool im Windows Admin Center auf der Registerkarte *Partnerschaften* die Option **neu** aus, **und klicken Sie**dann unter *Replikation mit einem anderen Server* auf **neuen virtuellen Azure** -Computer verwenden.
2. Geben Sie die Quell Server Informationen und den Replikations Gruppennamen an, und klicken Sie dann auf **weiter**.<br><br>
Dadurch wird ein Prozess gestartet, bei dem automatisch ein virtueller Azure-Computer unter Windows Server 2016 oder Windows Server 2019 als Ziel für die Migrations Quelle ausgewählt wird. Storage Migration Service empfiehlt VM-Größen, die ihrer Quelle entsprechen. Sie können dies jedoch überschreiben, indem Sie **alle Größen**anzeigen auswählen. Inventur Daten werden verwendet, um Ihre verwalteten Datenträger und Ihre Dateisysteme automatisch zu konfigurieren und ihre neue Azure-VM mit Ihrer Active Directory Domäne zu verknüpfen. 
3. Nachdem das Windows Admin Center die Azure-VM erstellt hat, geben Sie einen Replikations Gruppennamen an, und wählen Sie dann **Erstellen** Das Windows Admin Center beginnt dann mit der erst Synchronisierung des normalen Speicher Replikats, um die Daten zu schützen.

Im folgenden Video wird gezeigt, wie Sie das Speicher Replikat für die Migration zu Azure-VMS verwenden.

> [!VIDEO https://www.youtube-nocookie.com/embed/_VqD7HjTewQ] 

### <a name="deploying-a-new-standalone-azure-vm"></a>Bereitstellen einer neuen eigenständigen Azure-VM

1. Wählen Sie auf der Seite *alle Verbindungen* im Windows Admin Center die Option **Hinzufügen**aus.
2. Wählen Sie im Abschnitt *Azure-VM* die Option **neu erstellen**aus.<br><br> Dadurch wird ein schrittweises Erstellungs Tool gestartet, mit dem Sie einen virtuellen Windows Server 2012 R2-, Windows Server 2016-oder Windows Server 2019-virtuellen Azure-Computer auswählen, eine Größe auswählen, verwaltete Datenträger hinzufügen und optional Ihrer Active Directory Domäne beitreten können.

Im folgenden Video wird gezeigt, wie Sie Windows Admin Center zum Erstellen von virtuellen Azure-Computern verwenden.

> [!VIDEO https://www.youtube-nocookie.com/embed/__A8J9aC_Jk] 
