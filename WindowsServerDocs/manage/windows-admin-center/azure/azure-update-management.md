---
title: Verwenden des Windows Admin Centers zum Verwalten von Betriebssystemupdates mit Azure Updateverwaltung
description: Verwenden Sie das Windows Admin Center (Project Honolulu) zum Einrichten von Azure Updateverwaltung zum Verwalten von Betriebssystemupdates.
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.openlocfilehash: 3818e06780ac22f56ed3d44209041f58c1070409
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940061"
---
# <a name="use-windows-admin-center-to-manage-operating-system-updates-with-azure-update-management"></a>Verwenden des Windows Admin Centers zum Verwalten von Betriebssystemupdates mit Azure Updateverwaltung

[Erfahren Sie mehr über die Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

Bei Azure Updateverwaltung handelt es sich um eine Lösung in Azure Automation, mit der Sie Updates und Patches für mehrere Computer von einem einzigen Ort aus verwalten können und nicht auf Server Basis. Mit Azure-Updateverwaltung kannst du den Status verfügbarer Updates schnell bewerten, die Installation der erforderlichen Updates planen und die Ergebnisse der Bereitstellung überprüfen, um sicherzustellen, dass Updates erfolgreich angewendet werden. Dies ist möglich, unabhängig davon, ob Ihre Computer Azure-VMS sind, von anderen cloudanbietern oder lokal gehostet werden. [Erfahren Sie mehr über Azure Updateverwaltung.](https://docs.microsoft.com/azure/automation/automation-update-management)

Mithilfe des Windows Admin Centers können Sie problemlos Azure Updateverwaltung einrichten und verwenden, um Ihre verwalteten Server auf dem neuesten Stand zu halten. Wenn Sie noch nicht über einen Log Analytics Arbeitsbereich in Ihrem Azure-Abonnement verfügen, wird der Server automatisch von Windows Admin Center konfiguriert und die erforderlichen Azure-Ressourcen in dem von Ihnen angegebenen Abonnement und Speicherort erstellt. Wenn Sie über einen vorhandenen Log Analytics Arbeitsbereich verfügen, kann das Windows Admin Center Ihren Server automatisch so konfigurieren, dass Updates von Azure Updateverwaltung genutzt werden.

Wechseln Sie zunächst zum Update-Tool in einer Server Verbindung, und wählen Sie "jetzt einrichten" aus, und geben Sie die Einstellungen für die zugehörigen Azure-Ressourcen an.

Nachdem Sie den Server so konfiguriert haben, dass er von Azure Updateverwaltung verwaltet wird, können Sie über den im Update-Tool bereitgestellten Hyperlink auf Azure Updateverwaltung zugreifen.

[Erfahren Sie, wie Sie die Verwendung von Azure Updateverwaltung zum Aktualisieren Ihres Servers aufheben.](azure-monitor.md#disabling-monitoring)

Beachten Sie, dass Sie [Ihr Windows Admin Center-Gateway bei Azure registrieren](../configure/azure-integration.md) müssen, bevor Sie Azure Updateverwaltung einrichten.

