---
title: Vorbereiten der Migration zu MultiPoint Services
description: Enthält Informationen zum Sammeln von vor der Migration zu MultiPoint Services in Windows Server 2016
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3060c531-98a2-4957-a02c-be273f25f493
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 9650ebcae7e6207a226617d401d892049405901f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824381"
---
# <a name="prepare-to-migrate-to-multipoint-services-in-windows-server-2016"></a>Vorbereiten der Migration mit MultiPoint Services in Windows Server 2016

>Gilt für: Windows Server 2016

Verwenden Sie die folgende Informationen, die Informationen, die Sie benötigen zum Migrieren von der MultiPoint Services-Rolle von einem Quellserver unter einer früheren Version von Windows Server 2016 auf einem Zielserver unter Windows Server 2016 RTM zu sammeln.

Zumindest müssen Sie Mitglied der Gruppe "Administratoren" auf dem Quellserver und dem Zielserver zu installieren, entfernen oder Einrichten von MultiPoint Services sein.

>[!NOTE]
> Die hier beschriebenen Schritte bieten keine Anleitungen für die Migration von Daten in Benutzerordner gespeichert oder freigegebene Ordner. Stellen Sie sicher, dass Benutzer ihre Daten sichern, bevor Sie mit die Migration beginnen.

Verwenden Sie zum Abrufen der Informationen, die für die Migration Erforderlicher MultiPoint-Manager. Sie benötigen die Server Administrator eine Zugriffsberechtigung für MultiPoint-Manager verwenden.

Notieren Sie die MultiPoint Server, Benutzer und -Umgebung Einstellungen in der [Arbeitsblatts zur Erfassung von Migration](multipoint-services-migration-worksheet.md). Verwenden Sie die folgenden Schritte aus, um diese Informationen sammeln.

## <a name="multipoint-server-settings-for-the-local-server"></a>MultiPoint Server-Einstellungen für den lokalen server
1. Start MultiPoint Manager.
2. Auf der **Startseite** , wählen Sie den lokalen Server, und klicken Sie dann auf **Bearbeiten von servereinstellungen.**
3. Notieren Sie die Einstellungen im Datenarbeitsblatt.
4. Schließen Sie das Einstellungsfenster.

## <a name="managed-servers-and-computers"></a>Verwaltete Server und Computer

Die Namen von verwalteten Servern und Computern finden Sie auf die **Startseite** Registerkarte im MultiPoint-Manager.

## <a name="station-settings"></a>Stationseinstellungen
Wenn die automatische Anmeldung oder Anzeige Ausrichtung für die Station konfiguriert sind, verwenden Sie die folgenden Schritte aus, um diese Informationen abzurufen. Andernfalls können Sie diesen Schritt überspringen.

So rufen Sie die stationseinstellungen ab

1. Wechseln Sie zu der **Stationen** Registerkarte im MultiPoint-Manager.
2. Suchen Sie eine Station, die "yes" in der **automatische Anmeldung** Spalte.
3. Wählen Sie diese Station, und klicken Sie dann auf **konfigurieren Station**.
4. Notieren Sie den Benutzer, der für die automatische Anmeldung verwendet wird.

Zeigen Sie zum Abrufen der Anzeigeeinstellungen für die Ausrichtung der **stationseinstellungen** für jede Station.

## <a name="list-of-users"></a>Liste der Benutzer
1. Klicken Sie auf die **Benutzer** Registerkarte im MultiPoint-Manager.
2. Datensatz der **Administrator** und **MultiPoint-Dashboardbenutzer** Accoutns.
3. Notieren Sie die standard-Benutzer.

## <a name="vdi-template-location"></a>Speicherort der VDI-Vorlage
 Wenn Sie die VDI-Vorlagenfeature zuvor aktiviert haben, notieren Sie den Speicherort der Vorlage für VDI. Solange die Quelle und Ziel-Server im selben Netzwerk befinden, können Sie die Vorlage importieren, mit dem MultiPoint-Manager.
 
## <a name="next-step"></a>Nächster Schritt
Sie können nun [Migrieren zu MultiPoint Services](multipoint-services-migration-steps.md) in der RTM-Version von Windows Server 2016.