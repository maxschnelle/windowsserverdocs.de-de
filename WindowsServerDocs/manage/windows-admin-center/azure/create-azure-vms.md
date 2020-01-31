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
ms.openlocfilehash: 551f97d257b7ea3d05cdded73421d2e5c088171e
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76830616"
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

## <a name="requirements"></a>Anforderungen

Zum Erstellen eines neuen virtuellen Azure-Computers innerhalb des Windows Admin Centers benötigen Sie Folgendes:

- Ein [Azure-Abonnement](https://azure.microsoft.com).
- Ein [Windows Admin Center-Gateway, das bei Azure registriert](azure-integration.md) ist
- Eine vorhandene [Azure-Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) , für die Sie über die Berechtigung erstellen verfügen.
- Eine vorhandene [Azure-Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) und ein Subnetz.
- Eine [Azure Express Route](https://azure.microsoft.com/services/expressroute/) -oder [Azure-VPN-Lösung](https://azure.microsoft.com/services/vpn-gateway/) , die an das virtuelle Netzwerk und Subnetz gebunden ist und die Konnektivität von Azure-VMS mit Ihren lokalen Clients, Domänen Controllern, dem Windows Admin Center-Computer und allen Servern zulässt, die im Rahmen einer workloadbereitstellung mit diesem virtuellen Computer kommunizieren müssen. Wenn Sie z. b. den Speicher Migrationsdienst zum Migrieren von Speicher zu einem virtuellen Azure-Computer verwenden möchten, müssen der Orchestrator-Computer und der Quellcomputer beide in der Lage sein, eine Verbindung mit dem virtuellen Azure-Zielcomputer aufzunehmen, zu dem

## <a name="usage"></a>Usage

Azure-VM-Bereitstellungs Schritte und-Assistenten variieren je nach Szenario. Ausführliche Informationen zum Gesamtszenario finden Sie in der Dokumentation der Arbeitsauslastung.

### <a name="deploying-azure-vms-as-part-of-storage-migration-service"></a>Bereitstellen von Azure-VMS als Teil des Speicher Migrations Dienstanbieter

Führen Sie über das Tool " *Storage Migration Service* " im Windows Admin Center eine Inventur von mindestens einem Quell Server durch. Wenn Sie sich in der *Übertragungsdaten* Phase befinden, wählen Sie auf der Seite *Ziel angeben* die Option **neuen virtuellen Azure** -Computer erstellen aus, und klicken Sie dann auf **VM erstellen**. Dadurch wird ein schrittweises Erstellungs Tool gestartet, mit dem ein Windows Server 2012 R2-, Windows Server 2016-oder Windows Server 2019-virtueller Azure-Computer als Ziel für die Migration ausgewählt wird. Storage Migration Service bietet Empfohlene VM-Größen für Ihre Quelle, Sie können Sie jedoch außer Kraft setzen, indem Sie auf **alle Größen**anzeigen klicken. Quell Serverdaten werden auch verwendet, um Ihre verwalteten Datenträger und Ihre Dateisysteme automatisch zu konfigurieren und ihren neuen virtuellen Azure-Computer mit Ihrer Active Directory Domäne zu verknüpfen. Wenn es sich bei der VM um Windows Server 2019 (was wir empfehlen) handelt, installiert das Windows Admin Center die Proxy Funktion des Storage-Migrations Dienstanbieter. Nachdem die Azure-VM erstellt wurde, kehrt das Windows Admin Center zum normalen Übertragungs Workflow für den Speicher Migrationsdienst zurück.  


### <a name="deploying-azure-vms-as-part-of-storage-replica"></a>Bereitstellen von virtuellen Azure-Computern

Klicken Sie im Windows Admin Center *auf dem* *Speicher Replikat* Tool auf **neu** , und klicken Sie dann unter *Replizieren mit einem anderen Server* auf **neuen virtuellen Azure** -Computer verwenden, und klicken Sie dann auf **weiter**. Geben Sie Quell Server Informationen und Replikations Gruppenname an, und klicken Sie dann auf **weiter**. Dadurch wird ein Prozess gestartet, bei dem automatisch ein virtueller Azure-Computer unter Windows Server 2016 oder Windows Server 2019 als Ziel für die Migrations Quelle ausgewählt wird. Storage Migration Service empfiehlt VM-Größen, die ihrer Quelle entsprechen. Sie können dies jedoch überschreiben, indem Sie **alle Größen**anzeigen auswählen. Inventur Daten werden verwendet, um Ihre verwalteten Datenträger und Ihre Dateisysteme automatisch zu konfigurieren und ihre neue Azure-VM mit Ihrer Active Directory Domäne zu verknüpfen. Nachdem das Windows Admin Center die Azure-VM erstellt hat, geben Sie einen Replikations Gruppennamen an, und klicken Sie auf **Erstellen** Das Windows Admin Center beginnt dann mit der erst Synchronisierung des normalen Speicher Replikats, um die Daten zu schützen.


### <a name="deploying-a-new-standalone-azure-vm"></a>Bereitstellen einer neuen eigenständigen Azure-VM

Wechsle in Windows Admin Center von der Seite *Alle Verbindungen* zu **Hinzufügen**, und wähle unter **Azure VM** **Neu erstellen** aus. Dadurch wird ein schrittweises Erstellungs Tool gestartet, mit dem Sie einen virtuellen Windows Server 2012 R2-, Windows Server 2016-oder Windows Server 2019-virtuellen Azure-Computer auswählen, eine Größe auswählen, verwaltete Datenträger hinzufügen und optional Ihrer Active Directory Domäne beitreten können.
