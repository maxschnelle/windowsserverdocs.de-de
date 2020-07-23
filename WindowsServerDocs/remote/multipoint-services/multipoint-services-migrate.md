---
title: Migrieren zu Multipoint Services in Windows Server 2016
description: Erfahren Sie, wie Sie von einer früheren Version von Multipoint Services migrieren.
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 16c217ad-700a-48a3-8398-4a7f7e9edb52
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 1609ff02c8e1b1480d004104bdc7e37f1240729a
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959272"
---
# <a name="multipoint-services-migration-in-windows-server-2016"></a>Migration von Multipoint Services in Windows Server 2016
>Gilt für: Windows Server 2016

Sie können von einer früheren Version von Windows Server 2016 Multipoint Services zur RTM-Version von Multipoint Services migrieren. Die folgenden Informationen enthalten Informationen zur Vorbereitung sowie zu Migrations-und Überprüfungs Schritten.

Die Migrations Dokumentation und-Tools vereinfachen die Migration von Server Rollen Einstellungen und Daten von einem vorhandenen Server zu einem Zielserver, auf dem Windows Server 2016 ausgeführt wird. Mit dem in diesem Handbuch beschriebenen Prozess können Sie den Migrationsvorgang vereinfachen, die Migration beschleunigen, ihre Genauigkeit verbessern und mögliche Konflikte vermeiden, die andernfalls während der Migration auftreten können. 

## <a name="what-to-know-before-you-begin"></a>Was Sie wissen sollten, bevor Sie beginnen
Beachten Sie Folgendes, bevor Sie mit der Migration beginnen:

- Bei der Migration werden Einstellungen für Anwendungen in der Multipoint Services-Rolle nicht automatisch erfasst oder aufgezeichnet. Sie sollten einen angepassten Migrationsplan für alle Anwendungen erstellen, die Sie migrieren möchten. Dies gilt auch, wenn das Feature für virtuelle Desktops in Multipoint Services verwendet wird.
- Dieses Handbuch enthält keine Anleitungen zum Verschieben von Daten, die in Benutzer-oder freigegebenen Ordnern auf dem Multipoint-Server gespeichert sind. Dies gilt für reguläre Stationen und virtuelle Desktop Stationen.
- Dieses Handbuch enthält keine Anweisungen zum Migrieren, wenn auf dem Quell Server mehrere Rollen ausgeführt werden. Wenn auf dem Server mehrere Rollen ausgeführt werden, müssen Sie ein benutzerdefiniertes Migrationsverfahren entwerfen, das für Ihre Serverumgebung spezifisch ist, basierend auf Informationen, die in den Handbüchern für die Rollen Migration bereitgestellt werden.
- Dieses Handbuch enthält keine Informationen zum Migrieren von Remotedesktopdienste CALs. Informationen zu diesen Informationen finden Sie unter [Migrieren von Remotedesktopdienste Client Zugriffs Lizenzen (RDS-CALs)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd851844(v=ws.11)).

## <a name="supported-migration-scenarios-for-multipoint-services-in-windows-server-2016"></a>Unterstützte Migrationsszenarien für Multipoint Services in Windows Server 2016
Die Multipoint Service-Rollen Dienste sind in Windows Server 2016 Standard und Datacenter verfügbar. In diesem Migrations Handbuch wird beschrieben, wie Sie die Multipoint Services-Rollen Dienste von einem Quell Server unter Windows Server 2016 zu einem Zielserver migrieren, auf dem die gleiche Version ausgeführt wird.

## <a name="scenarios-that-are-not-supported"></a>Nicht unterstützte Szenarien

Die folgenden Migrationsszenarien werden nicht unterstützt:

- Migrieren oder Aktualisieren von Windows MultiPoint Server 2012 und 2011.
- Migrieren von einem Quell Server zu einem Zielserver, auf dem unter einem Betriebssystem ausgeführt wird, auf dem eine andere Benutzeroberflächen Sprache des Systems installiert ist.
- Migrieren des Multipoint Services-Rollen Diensts von physischen Servern zu virtuellen Maschinen.
- Migrieren von Anwendungen oder Anwendungseinstellungen vom Multipoint-Server.

## <a name="the-impact-of-migration-on-multipoint-services"></a>Auswirkungen der Migration auf Multipoint Services
Beachten Sie, dass die Multipoint Services-Rolle während der Migration nicht verfügbar ist. Planen Sie die Datenmigration für einen Zeitraum mit geringerer Auslastung, um die Ausfallzeit und die Auswirkungen auf Benutzer gering zu halten. Benachrichtigen Sie die Benutzer, dass die Ressourcen während dieser Zeit nicht verfügbar sind.

## <a name="migration-information-and-steps"></a>Migrations Informationen und-Schritte
Verwenden Sie die folgenden Informationen, um die Multipoint Services-Migration zu planen und auszuführen:

- [Sammeln Sie die Informationen, die Sie für die Migration benötigen.](multipoint-services-migration-preparation.md)
- [Migrieren Sie den Multipoint Services-Rollen Dienst.](multipoint-services-migration-steps.md)
- [Überprüfen der Migration und Ausführen von Bereinigungs Tasks nach der Migration](multipoint-services-post-migration-steps.md)
