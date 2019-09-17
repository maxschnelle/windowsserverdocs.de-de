---
title: 'Anmerkungen zu dieser Version: Wichtige Probleme in Windows Server, Version 1803'
description: Erfahren Sie mehr über bekannte Probleme, Einschränkungen oder andere Informationen, die Sie vor der Installation von Windows Server, Version 1803, benötigen
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 05/07/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 506236cbb3893fe200b39aa1d58ed44cdbd9704a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868378"
---
# <a name="release-notes-important-issues-in-windows-server-version-1803"></a>Versionshinweise: Wichtige Probleme in Windows Server, Version 1803

>Gilt für: Windows Server (Semi-Annual Channel)

In diesen Anmerkungen zur Version sind die wichtigsten Probleme zusammengefasst, die im Windows Server-Betriebssystem auftreten können, und Sie erfahren, wie Sie diese Probleme gegebenenfalls umgehen können. Weitere Informationen zu neuen Features in diesem Release finden Sie unter [Neuerungen in Windows Server, Version 1803](whats-new-in-windows-server-1803.md). Ziehen Sie die [Informationen zu Windows-Containern](https://docs.microsoft.com/virtualization/windowscontainers/about/) zurate, wenn Sie daran interessiert sind, einen Windows Server-Container, Version 1803, auszuführen. 

Sofern es nicht anders angegeben ist, gelten alle aufgeführten Probleme für alle Editionen und Installationsoptionen von Windows Server, Version 1803.  

Dieser Artikel wird fortlaufend aktualisiert. Wenn Probleme bekannt werden, werden diese hier dokumentiert. 


## <a name="software-defined-datacenter"></a>Softwaredefiniertes Rechenzentrum

Features des softwaredefinierten Rechenzentrums, wie z.B. „Direkte Speicherplätze“, Software-Defined Networking und geschützte virtuelle Computer, sind in Windows Server, Version 1803, nicht enthalten. Wie unter [Update für Windows Server (halbjährlicher Kanal)](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/) beschrieben, konzentriert sich der halbjährliche Kanal von Windows Server auf Container- und Anwendungsszenarien, die von schnelleren Innovationen profitieren. 

Wenn Sie die Infrastrukturrollen benötigen, verwenden Sie ein Long Term Servicing Channel-Release: Windows Server 2016 (jetzt verfügbar) oder [Windows Server-2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (später in diesem Jahr verfügbar).

Wir setzen uns für die Entwicklung der besten Plattform für hyperkonvergente Infrastruktur ein und entwickeln ständig neue Features und verbessern vorhandene basierend auf Ihrem Feedback. Vielen Dank für Ihre Unterstützung, dank derer wir [die Marke von 10.000 Clustern von „Direkte Speicherplätze“ überschritten haben](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum)! Wir freuen uns darauf, noch in diesem Jahr mehr darüber bekannt zu geben.