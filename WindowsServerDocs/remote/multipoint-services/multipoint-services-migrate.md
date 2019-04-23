---
title: Migrieren Sie zu MultiPoint Services unter WindowsServer 2016
description: Erfahren Sie, wie Sie von einer früheren Version von MultiPoint Services migrieren
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16c217ad-700a-48a3-8398-4a7f7e9edb52
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 24c35c31bf920c41bafa16901ee30a023565dad8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861201"
---
# <a name="multipoint-services-migration-in-windows-server-2016"></a>MultiPoint Server-Migration in Windows Server 2016
>Gilt für: Windows Server 2016

Sie können auf die RTM-Version von MultiPoint Services von einer früheren Version von Windows Server 2016 MultiPoint Services migrieren. Die folgende Informationen enthält zur Vorbereitung die Informationen und Migrations-und Überprüfungsschritte.

Migrationsdokumentation und-Tools vereinfachen die Migration von serverrolleneinstellungen und Daten von einem vorhandenen Server zu einem Zielserver, auf der Windows Server 2016 ausgeführt wird. Mit dem in diesem Handbuch beschriebenen Prozess können Sie den Migrationsvorgang vereinfachen, die Migration beschleunigen, ihre Genauigkeit verbessern und mögliche Konflikte vermeiden, die andernfalls während der Migration auftreten können. 

## <a name="what-to-know-before-you-begin"></a>Was Sie wissen sollten, bevor Sie beginnen
Bevor Sie während der Migration beginnen, beachten Sie Folgendes:

- Während der Migration zu sammeln und Aufzeichnen von Einstellungen für Anwendungen auf dem MultiPoint Services-Rolle automatisch. Sie sollten einen benutzerdefinierten Migrationsplan für alle Anwendungen erstellen, die Sie migrieren möchten. Dies gilt auch, wenn das Feature für den virtuellen Desktops im MultiPoint Services verwenden.
- Dieses Handbuch bietet keine Anleitung zum Verschieben von Daten in der Benutzer gespeichert oder freigegebene Ordner auf dem MultiPoint-Server. Dies gilt für reguläre Stationen und virtuellen Desktops Stationen.
- Dieses Handbuch enthält keine Anweisungen zum Migrieren, wenn der Quellserver mehrere Rollen ausgeführt werden. Wenn Ihr Server mehrere Rollen ausgeführt wird, müssen Sie ein benutzerdefiniertes Migrationsverfahren entwerfen, das für die serverumgebung, basierend auf Informationen in den Handbüchern spezifisch sind.
- Dieses Handbuch enthält keine Informationen für die Migration von Remotedesktopdiensten CALS. Weitere Informationen finden Sie unter [migrieren Remote Desktop Services Client Access Licenses (RDS-CALs)](https://technet.microsoft.com/library/dd851844.aspx).

## <a name="supported-migration-scenarios-for-multipoint-services-in-windows-server-2016"></a>Unterstützte Migrationsszenarien für MultiPoint-Dienste in Windows Server 2016
Die Rollendienste für MultiPoint-Dienst ist in Windows Server 2016 Standard und Datacenter verfügbar. Diesem Migrationshandbuch wird beschrieben, wie Sie die Multipoint Services-Rollendienste von einem Quellserver unter Windows Server 2016 auf einem Zielserver unter der gleichen Version migrieren.

## <a name="scenarios-that-are-not-supported"></a>Szenarien, die nicht unterstützt werden

Die folgenden Migrationsszenarien werden nicht unterstützt:

- Migrieren aus, oder Aktualisieren von Windows MultiPoint Server 2012 und 2011.
- Migrieren von einem Quellserver zu einem Zielserver, die auf dem Betriebssystem mit einem anderen System installierte Sprache der Benutzeroberfläche ausgeführt wird.
- Migrieren der MultiPoint Services-Rolle von physischen Servern zu virtuellen Computern.
- Migrieren von Anwendungen oder Anwendungseinstellungen vom MultiPoint-Server an.

## <a name="the-impact-of-migration-on-multipoint-services"></a>Die Auswirkungen der Migration in MultiPoint Services
Denken Sie daran, dass die MultiPoint Services-Rolle während der Migration nicht verfügbar ist. Planen Sie die Datenmigration für einen Zeitraum mit geringerer Auslastung, um die Ausfallzeit und die Auswirkungen auf Benutzer gering zu halten. Benachrichtigen Sie die Benutzer, dass die Ressourcen während dieser Zeit nicht verfügbar sind.

## <a name="migration-information-and-steps"></a>Informationen zur Migration und Schritte
Verwenden Sie die folgende Informationen zum Planen und Ihre MultiPoint Services-Migration auszuführen:

- [Sammeln Sie die Informationen, die Sie für die Migration müssen.](multipoint-services-migration-preparation.md)
- [Migrieren der MultiPoint Services-Rolle.](multipoint-services-migration-steps.md)
- [Überprüfen der Migrations, und führen Sie Aufgaben nach der Migration bereinigen](multipoint-services-post-migration-steps.md)