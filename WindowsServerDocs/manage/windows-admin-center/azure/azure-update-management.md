---
title: Verwenden von Windows Admin Center zum Verwalten von Betriebssystem-Updates mit der Azure-Updateverwaltung
description: Verwenden von Windows Admin Center (Projekt Honolulu) die Verwaltung von Azure zum Verwalten von Betriebssystem einrichten aktualisiert.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 79b18e9963fba0993a7f34b1409edba6abfd48f0
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452542"
---
# <a name="use-windows-admin-center-to-manage-operating-system-updates-with-azure-update-management"></a>Verwenden von Windows Admin Center zum Verwalten von Betriebssystem-Updates mit der Azure-Updateverwaltung

[Weitere Informationen zu Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

Verwaltung von Azure ist eine Lösung in Azure Automation, die Ihnen ermöglicht, Updates und Patches für mehrere Computer an einem zentralen Ort, und nicht auf eine einzelne Server verwalten. Mit der Azure-Updateverwaltung können Sie schnell den Status verfügbarer Updates bewerten, Installation von erforderlichen Updates planen und Bereitstellungsergebnisse überprüfen um sicherzustellen, dass Updates, die erfolgreich angewendet. Dies ist möglich, ob Ihre Computer für Azure-VMs, die von anderen cloudanbietern oder lokal gehostet werden. [Weitere Informationen zur Verwaltung von Azure.](https://docs.microsoft.com/azure/automation/automation-update-management)

Mit Windows Admin Center können Sie ganz einfach einrichten und verwenden die Verwaltung von Azure, um den verwalteten Servern auf dem neuesten Stand zu halten. Wenn Sie bereits über einen Log Analytics-Arbeitsbereich im Azure-Abonnement haben, Windows Admin Center automatisch konfigurieren Sie den Server und die erforderlichen Azure-Ressourcen im Abonnement und am angegebenen Speicherort zu erstellen. Wenn Sie einen vorhandenen Log Analytics-Arbeitsbereich verfügen, können den Server, um Updates von Azure-Updateverwaltung Nutzen von Windows Admin Center automatisch konfigurieren.  

Informationen zum Einstieg finden Sie unter der Updates-Tool in einer Server-Verbindung und wählen Sie "Jetzt einrichten" und geben Sie Ihre Einstellungen für die zugehörigen Azure-Ressourcen. 

Nachdem Sie Ihren Server für die Verwaltung durch die Verwaltung von Azure konfiguriert haben, können Sie die Verwaltung von Azure zugreifen, mithilfe des Links in der Updates-Tool bereitgestellt. 

[Informationen Sie zum Beenden der Verwendung von Azure-Updateverwaltung auf um Ihrem Server zu aktualisieren.](azure-monitor.md#disabling-monitoring)

Beachten Sie, dass Sie müssen [Registrieren Ihres Windows Admin Center-Gateways mit Azure](../configure/azure-integration.md) vor dem Einrichten der Verwaltung von Azure.

