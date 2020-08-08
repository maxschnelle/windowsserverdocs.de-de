---
title: Schritte zum Migrieren von Multipoint Services
description: Führt Sie durch die Schritte zum Migrieren zu Multipoint Services in Windows Server 2016.
ms.date: 07/29/2016
ms.topic: article
ms.assetid: 3ee77efa-7cc5-4ddf-aaff-b5634a717014
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 0d76e3518801829b852c94d0b112b906abbd92c0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948933"
---
# <a name="migrate-to--multipoint-services-in-windows-server-2016"></a>Migrieren zu Multipoint Services in Windows Server 2016

>Gilt für: Windows Server 2016

Führen Sie die folgenden Schritte aus, zuzüglich der Informationen, die Sie im Arbeitsblatt zur Migrationsplanung gesammelt haben, um zu Multipoint Services in Windows Server 2016 zu migrieren.

## <a name="transfer-server-settings"></a>Servereinstellungen übertragen
Öffnen Sie auf dem Zielserver den Multipoint-Manager. Klicken Sie auf **Servereinstellungen bearbeiten**. Übernehmen Sie die Einstellungen gemäß dem Arbeitsblatt für die Migrationsplanung.

> [!NOTE]
> Wenn Sie den Datenträger Schutz auf dem Zielserver aktivieren müssen, warten Sie, bis Sie Multipoint Services konfiguriert haben.

## <a name="transfer-station-settings"></a>Übertragungs Stations Einstellungen
Stellen Sie sicher, dass die Stationen mit dem Zielserver verbunden sind und alle zugeordnet sind, bevor Sie die Stations Einstellungen anwenden. Die Stationen werden automatisch erkannt. Befolgen Sie die Anweisungen auf den einzelnen Stations Bildschirm, um die Server Zuordnung von Benutzer Stationen und verbundenen USB-Geräten zu definieren. Wenden Sie die im Arbeitsblatt für die Migrationsplanung aufgeführten bevorzugten Stations Einstellungen an.

## <a name="migrate-the-vdi-template"></a>Migrieren der VDI-Vorlage

Bevor Sie die VDI-Vorlage vom Quell Server importieren können, können Sie virtuelle Desktops auf dem Zielserver mithilfe von Multipoint Manager aktivieren:

1. Wechseln Sie im Multipoint-Manager zur Registerkarte **virtuelle Desktops** .
2. Klicken Sie auf **aktivierte virtuelle Desktops**. Der Server installiert die Hyper-V-Rolle und startet dann neu.
3. Öffnen Sie den Multipoint-Manager, und navigieren Sie zurück zu **virtuelle Desktops**.
4. Klicken Sie auf **Vorlage für virtuellen Desktop importieren**. Befolgen Sie die Anweisungen, um die Vorlage vom Quell Server zu importieren.

> [!NOTE]
> Wenn Sie eine Vorlage für virtuelle Desktops importieren, werden alle Anpassungen, die auf die Vorlage angewendet werden, zurückgesetzt.

## <a name="next-step"></a>Nächster Schritt
[Überprüfen Sie die neue Multipoint Services-Bereitstellung.](multipoint-services-post-migration-steps.md)