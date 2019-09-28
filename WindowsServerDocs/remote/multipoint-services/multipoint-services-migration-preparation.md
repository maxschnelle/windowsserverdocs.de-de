---
title: Vorbereiten der Migration zu MultiPoint Services
description: Beschreibt Informationen, die vor der Migration zu Multipoint Services in Windows Server 2016 erfasst werden müssen.
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3060c531-98a2-4957-a02c-be273f25f493
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: d0f1fd22b00bdb2e5e3684a541dd14532fd885e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394648"
---
# <a name="prepare-to-migrate-to-multipoint-services-in-windows-server-2016"></a>Vorbereiten der Migration zu Multipoint Services in Windows Server 2016

>Gilt für: Windows Server 2016

Verwenden Sie die folgenden Informationen, um die Informationen zu sammeln, die Sie benötigen, um den Multipoint Services-Rollen Dienst von einem Quell Server mit einer früheren Version von Windows Server 2016 zu einem Zielserver mit Windows Server 2016 RTM zu migrieren.

Sie müssen mindestens Mitglied der Gruppe "Administratoren" auf dem Quell Server und dem Zielserver sein, um Multipoint Services zu installieren, zu entfernen oder einzurichten.

>[!NOTE]
> Die hier beschriebenen Schritte bieten keine Anleitungen zum Migrieren von Daten, die in Benutzer Ordnern oder freigegebenen Ordnern gespeichert sind. Stellen Sie sicher, dass die Benutzer Ihre Daten sichern, bevor Sie mit der Migration beginnen.

Verwenden Sie Multipoint Manager, um die für die Migration erforderlichen Informationen abzurufen. Sie benötigen die Server Administrator Berechtigung, um den Multipoint-Manager zu verwenden.

Notieren Sie den Multipoint-Server, den Benutzer und die Umgebungseinstellungen im [Arbeitsblatt für die Sammlung von Migrationsdaten](multipoint-services-migration-worksheet.md). Verwenden Sie die folgenden Schritte, um diese Informationen zu erfassen.

## <a name="multipoint-server-settings-for-the-local-server"></a>Multipoint-Servereinstellungen für den lokalen Server
1. Starten Sie den Multipoint-Manager.
2. Wählen Sie auf der Registerkarte **Startseite** den lokalen Server aus, und klicken Sie dann auf **Servereinstellungen bearbeiten.**
3. Notieren Sie die Einstellungen im Daten Arbeitsblatt.
4. Schließen Sie das Fenster Einstellungen.

## <a name="managed-servers-and-computers"></a>Verwaltete Server und Computer

Die Namen der verwalteten Server und Computer finden Sie auf der Registerkarte **Start** im Multipoint-Manager.

## <a name="station-settings"></a>Stations Einstellungen
Wenn die automatische Anmeldung oder Anzeige Ausrichtung für die Station konfiguriert ist, verwenden Sie die folgenden Schritte, um diese Informationen abzurufen. Andernfalls können Sie diesen Schritt überspringen.

So rufen Sie die Stations Einstellungen ab:

1. Wechseln Sie im Multipoint-Manager zur Registerkarte **Stationen** .
2. Suchen Sie in der Spalte für die **automatische Anmeldung** eine Station, die "yes" aufweist.
3. Wählen Sie diese Station aus, und klicken Sie dann auf **Station konfigurieren**.
4. Notieren Sie den Benutzer, der für die automatische Anmeldung verwendet wird.

Zum Abrufen der Einstellungen für die Anzeige Ausrichtung zeigen Sie die **Stations Einstellungen** für jede Station an.

## <a name="list-of-users"></a>Liste der Benutzer
1. Klicken Sie im Multipoint-Manager auf die Registerkarte **Benutzer** .
2. Notieren Sie sich die Benutzer Zugriffsrechte für **Administrator** und **Multipoint-Dashboard** .
3. Notieren Sie die Standardbenutzer.

## <a name="vdi-template-location"></a>Standort der VDI-Vorlage
 Wenn Sie zuvor die VDI-Vorlagen Funktion aktiviert haben, notieren Sie den Speicherort der VDI-Vorlage. Solange sich die Quell-und Zielserver im gleichen Netzwerk befinden, können Sie die Vorlage mithilfe von Multipoint Manager importieren.
 
## <a name="next-step"></a>Nächster Schritt
Sie sind jetzt bereit für die [Migration zu Multipoint Services](multipoint-services-migration-steps.md) in der RTM-Version von Windows Server 2016.