---
title: Verwenden von Windows Admin Center zum Verwalten von Betriebssystem-Updates mit der Azure-Updateverwaltung
description: Verwenden Sie Windows Admin Center (Projekt Honolulu) Azure-Updateverwaltung einrichten, zum Verwalten von Betriebssystem-updates.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 5ba81968f8baa81176ad646fb2a97961ddc49fda
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296916"
---
# Verwenden von Windows Admin Center zum Verwalten von Betriebssystem-Updates mit der Azure-Updateverwaltung

[Weitere Informationen über die Integration von Azure finden Sie im Windows Admin Center.](../plan/azure-integration-options.md)

Azure-Updateverwaltung ist eine Lösung in Azure-Benutzeroberflächenautomatisierung, die Sie Updates und Patches für mehrere Computer von einem zentralen Punkt, anstatt auf pro Server verwalten können. Mit Azure-Updateverwaltung können Sie schnell den Status der verfügbaren Updates zu bewerten, Planen der Updateinstallation erforderlich und überprüfen Bereitstellung Ergebnisse, um Updates zu überprüfen, die erfolgreich angewendet. Dies ist möglich, ob Ihre Computer Azure-VMs, die von anderen Anbietern Cloud oder lokal gehostet werden. [Weitere Informationen zu Azure-Updateverwaltung.](https://docs.microsoft.com/azure/automation/automation-update-management)

Mit Windows Admin Center können Sie ganz einfach einrichten und Verwenden von Azure-Updateverwaltung auf um die verwalteten Servern auf dem neuesten Stand zu halten. Wenn Sie bereits über einen Log Analytics-Arbeitsbereich in Ihrem Azure-Abonnement besitzen, Windows Admin Center automatisch den Server konfigurieren und erstellen die erforderlichen Azure Ressourcen in das Abonnement und am angegebenen Speicherort. Wenn Sie einen vorhandenen Log Analytics-Arbeitsbereich haben, können Windows Admin Center den Server für Updates von Azure-Updateverwaltung nutzen automatisch konfigurieren.  

Um zu beginnen, wechseln Sie zu dem Update-Tool in Verbindung mit einem und wählen Sie "Einrichten von jetzt", und Ihre Einstellungen für die zugehörigen Azure-Ressourcen. 

Nachdem Sie Ihre Server von Azure-Updateverwaltung verwaltet werden konfiguriert haben, können Sie die Azure-Updateverwaltung zugreifen, mit dem Link im Tool Updates bereitgestellt. 

[Erfahren Sie, wie zum Beenden der Verwendung von Azure aktualisieren Management, um Ihre Server zu aktualisieren.](azure-monitor.md#disabling-monitoring)

Beachten Sie, dass [das Windows Admin Center-Gateway mit Azure registrieren](..\configure\azure-integration.md) Sie vor dem Einrichten von Azure-Updateverwaltung müssen.

