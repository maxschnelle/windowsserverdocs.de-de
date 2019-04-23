---
title: Schritte zum Migrieren von MultiPoint Services
description: Führt Sie durch die Schritte zum Migrieren zu MultiPoint Services in Windows Server 2016
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ee77efa-7cc5-4ddf-aaff-b5634a717014
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: b63ef4bf63ce990aa0b0ba7624905ba8f14dde98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854811"
---
# <a name="migrate-to--multipoint-services-in-windows-server-2016"></a>Migrieren Sie zu MultiPoint Services unter WindowsServer 2016

>Gilt für: Windows Server 2016

Verwenden Sie die folgenden Schritte sowie die Informationen, die Sie in das Arbeitsblatt für die Migration planen, zu MultiPoint Services in Windows Server 2016 zu migrieren gesammelt haben.

## <a name="transfer-server-settings"></a>Übertragen von servereinstellungen
Öffnen Sie MultiPoint-Manager, auf dem Zielserver. Klicken Sie auf **Bearbeiten von servereinstellungen**. Wenden Sie die Einstellungen entsprechend dem Arbeitsblatt für die Planung der Migration.

> [!NOTE]
> Wenn Sie zum Aktivieren des datenträgerschutzes auf dem Zielserver müssen, warten Sie bis nach dem MultiPoint Services konfigurieren.

## <a name="transfer-station-settings"></a>Übertragen von stationseinstellungen
Stellen Sie sicher, dass die Stationen, auf dem Zielserver und alle zugeordnet verbunden sind, bevor Sie die stationseinstellungen anwenden. Die Stationen werden automatisch erkannt. Befolgen Sie die Anweisungen auf den einzelnen Bildschirmen Station, um die Server-Zuordnung von Benutzerkonsolen und angeschlossene USB-Geräte zu definieren. Wenden Sie Ihre bevorzugte stationseinstellungen, wie im Arbeitsblatt für die Planung Migration beschrieben.

## <a name="migrate-the-vdi-template"></a>Migrieren Sie die VDI-Vorlage

Bevor Sie die VDI-Vorlage des Quellservers importieren können, können Sie virtuelle Desktops auf dem Zielserver mithilfe von MultiPoint-Manager aktiviert:

1. Wechseln Sie zu der **virtuelle Desktops** Registerkarte im MultiPoint-Manager.
2. Klicken Sie auf **aktiviert virtuelle Desktops**. Der Server wird die Hyper-V-Rolle installieren und dann neu starten.
3. Öffnen Sie MultiPoint-Manager, und navigieren Sie zurück zur **virtuelle Desktops**.
4. Klicken Sie auf **Import-Vorlage für virtuelle Desktops**. Führen Sie die Anweisungen, um die Vorlage vom Quellserver zu importieren.

> [!NOTE]
> Wenn Sie eine Vorlage für virtuelle Desktops importieren, werden bei Anpassungen auf die Vorlage angewendet zurückgesetzt. 

## <a name="next-step"></a>Nächster Schritt
[Überprüfen Sie die neue MultiPoint Services-Bereitstellung.](multipoint-services-post-migration-steps.md)