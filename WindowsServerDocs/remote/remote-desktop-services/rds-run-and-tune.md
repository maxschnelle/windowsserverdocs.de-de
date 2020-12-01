---
title: 'RDS: Ausführen und Optimieren Ihrer Remotedesktopdienste-Umgebung'
description: Bietet Verwaltungsinformationen für Remotedesktopdienste.
ms.author: spatnaik
ms.date: 02/08/2017
ms.topic: article
ms.assetid: 79909767-a4c3-4ecf-8d3f-77d37a663153
author: spatnaik
manager: scottman
ms.openlocfilehash: 5a68569943ac540204fd3538719c2a0ef6c4c979
ms.sourcegitcommit: 3181fcb69a368f38e0d66002e8bc6fd9628b1acc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/30/2020
ms.locfileid: "96330432"
---
# <a name="run-and-tune-your-remote-desktop-services-environment"></a>Ausführen und Optimieren Ihrer Remotedesktopdienste-Umgebung

Das Optimieren Ihrer Bereitstellung nimmt Zeit in Anspruch und setzt Instrumentierung und Überwachung voraus. Verwenden Sie die unten dargestellten Prozesse, um Ihre Remotedesktopbereitstellung zu optimieren, ihren Betrieb aufrecht zu erhalten und sie nach Bedarf horizontal hoch- und herunterzuskalieren.

Es hat sich bewährt, die Kennzahlen fortlaufend auszuwerten und sie den laufenden Kosten gegenüber zu stellen.

## <a name="management-and-monitoring"></a>Verwaltung und Überwachung

Sehen Sie sich [Verwalten von Benutzern in Ihrer RDS-Sammlung](rds-user-management.md) an, um Informationen für das Verwalten des Zugriffs auf Ihre Desktops und Remoteressourcen zu erhalten.

Verwenden Sie die **Microsoft Operations Management Suite (OMS)** , um Remotedesktopbereitstellungen auf potenzielle Engpässe zu überprüfen und sie auf eine der folgenden Weisen zu verwalten:

- **Server Manager**: Verwenden Sie das in Windows Server integrierte RD-Verwaltungstool, um Bereitstellungen mit bis zu 500 gleichzeitigen Remote-Endbenutzern zu verwalten.
- **PowerShell**: Verwenden Sie das ebenfalls in Windows Server integrierte RD-PowerShell-Modul, um Bereitstellungen mit bis zu 500 gleichzeitigen Remote-Endbenutzern zu verwalten.

## <a name="scale-bigger-better-faster"></a>Skalierung: größer, besser, schneller

Dank der transparenten Bereitstellung können Sie die Skalierung mit größerer Präzision steuern. Fügen Sie ganz einfach Remotedesktop-Hostserver hinzu, oder entfernen Sie sie, wie es die Skalierung erfordert.

Remotedesktopbereitstellungen, die auf Azure aufgebaut sind, können Azure-Services, wie etwa Azure SQL, nutzen, um bei Bedarf automatisch zu skalieren.

## <a name="automation-script-for-success"></a>Automatisierung: mit Skripts zum Erfolg

Das Warten einer laufenden, hochgradig skalierten Anwendung bringt sich regelmäßig wiederholende Vorgänge mit sich. Verwenden Sie PowerShell-Cmdlets und WMI-Anbieter der Remotedesktopdienste, um Skripts zu entwickeln, die bei Bedarf in mehreren Bereitstellungen ausgeführt werden können. Führen Sie BPA-Regeln (Best Practice Analyzer) für Remotedesktopdienste in Ihren Bereitstellungen aus, um Ihre Bereitstellungen zu optimieren.

## <a name="load-testing-avoid-surprises"></a>Auslastungstests: Vermeiden Sie Überraschungen

Führen Sie Auslastungstests der Bereitstellung mit Belastungstests und Simulation der tatsächlichen Nutzung durch. Variieren Sie den Umfang der Last, um Überraschungen zu vermeiden! Stelle sicher, dass die Reaktionsfähigkeit die Anforderungen der Benutzer erfüllt und dass das gesamte System stabil ist. Erstelle Lasttests mit Simulationstools wie LoginVSI, die überprüfen, inwieweit deine Bereitstellung die Benutzeranforderungen erfüllt.
