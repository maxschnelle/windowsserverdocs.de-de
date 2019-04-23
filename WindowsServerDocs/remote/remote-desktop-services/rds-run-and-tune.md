---
title: RDS - ausführen und optimieren
description: Stellt die Verwaltungsdaten für Remote Desktop Services bereit.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 02/08/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79909767-a4c3-4ecf-8d3f-77d37a663153
author: spatnaik
manager: scottman
ms.openlocfilehash: 40f8dbd560da359e8764ed715e7776cc2d230a7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862181"
---
# <a name="run-and-tune-your-remote-desktop-services-environment"></a>Führen Sie aus und Optimieren Sie Ihrer Umgebung Remote Desktop Services

Optimieren Ihre Bereitstellung nimmt Zeit in Anspruch und erfordert die Instrumentierung und Überwachung. Verwenden Sie die folgenden Prozesse optimieren Ihrer remotedesktopbereitstellung, weiterhin ausführen, und aktivieren Sie die Skalierung, hoch- und Herunterskalieren, je nach Bedarf. 

Es hat sich bewährt, die ständig die Metriken und Lastenausgleich für die laufenden Kosten zu bewerten.

## <a name="management-and-monitoring"></a>Verwaltung und Überwachung

Sehen Sie sich [Verwalten von Benutzern in Ihrer Sammlung RDS](rds-user-management.md) für Informationen zum Verwalten des Zugriffs auf Ihre Desktops und Remoteressourcen.

Verwendung **Microsoft Operations Management Suite (OMS)** remotedesktopbereitstellungen für potenzielle Engpässe zu überwachen und verwalten sie mit einer der folgenden Methoden: 

- **Server Manager**: Verwenden Sie das RD-Verwaltungstool, das auf Windows Server zum Verwalten von Bereitstellungen mit bis zu 500 gleichzeitige remote Endbenutzer enthalten ist. 
- **PowerShell**: Verwenden Sie das RD-PowerShell-Modul auch in Windows Server integriert, um Bereitstellungen mit bis zu 5.000 gleichzeitiger remote Endbenutzern zu verwalten.

## <a name="scale-bigger-better-faster"></a>Skalierung: Größere, besser und schneller

Einblick in die Bereitstellung können Sie die Skalierungsgruppe mit einer höheren Genauigkeit steuern. Ganz einfach hinzufügen oder Remotedesktop-Hostservern, die je nach Anforderungen der Skalierungsgruppe zu entfernen. 

Remotedesktopbereitstellungen, die in Azure integriert sind möglich. Verwenden von Azure-Dienste wie Azure SQL, um automatisch nach Bedarf zu skalieren.

## <a name="automation-script-for-success"></a>Automation: Skript für den Erfolg

Warten eine ausgeführte Anwendung mit hoher Skalierung umfasst die Vorgänge in regelmäßigen Abständen zu wiederholen. Verwenden Sie Remote Desktop Services-PowerShell-Cmdlets und WMI-Anbieter zum Entwickeln von Skripts, die auf mehrere Bereitstellungen, bei Bedarf ausgeführt werden kann. Führen Sie Best Practice Analyzer (BPA)-Regeln für Remote Desktop Services, auf Ihre Bereitstellungen für Ihre Bereitstellungen zu optimieren.

## <a name="load-testing-avoid-surprises"></a>Laden Sie die Tests: Vermeiden Sie überraschungen

Die Bereitstellung mit Belastungstests und Simulation von realen Nutzung des Auslastungstests. Variieren Sie die Größe der Auslastung um überraschungen zu vermeiden! Stellen Sie sicher, dass die Reaktionsfähigkeit der benutzeranforderungen erfüllt und dass das gesamte System stabil ist. Erstellen Sie Auslastungstests mit simulationstools wie LoginVSI, die Überprüfen Ihrer Bereitstellung können Sie die Anforderungen der Benutzer erfüllen. 