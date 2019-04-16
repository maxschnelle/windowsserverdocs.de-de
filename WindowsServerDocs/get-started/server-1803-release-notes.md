---
title: Anmerkungen zu dieser Version – wichtige Probleme in Windows Server, Version 1803
description: Erfahren Sie mehr über bekannte Probleme, Einschränkungen oder andere Informationen, die Sie vor der Installation von Windows Server, Version 1803
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
ms.openlocfilehash: e9bd860769ec375a6d89ac452e3430b791fff3ad
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339318"
---
# Anmerkungen zu dieser Version: Wichtige Probleme in Windows Server, Version 1803

>Gilt für: Windows Server, Semi-Annual Channel

Diese Anmerkungen zu dieser Version zusammengefasst, die wichtigsten Probleme in der Windows Server-Betriebssystem, einschließlich Methoden zum vermeiden und bekannte Probleme zu umgehen. Weitere Informationen zu neuen Features in dieser Version finden Sie in der [Neuigkeiten in Windows Server Version 1803](whats-new-in-windows-server-1803.md). Sehen Sie sich [über Windows-Container](https://docs.microsoft.com/virtualization/windowscontainers/about/) , wenn Sie sich mit einem Windows Server, Version 1803, Container interessieren. 

Sofern nicht anders angegeben, gelten alle aufgeführten Probleme für alle Editionen und Installationsoptionen von Windows Server, Version 1803.  

Kontinuierlich aktualisieren wir in diesem Artikel. Wenn bekannten Probleme erkannt werden, werden wir diese hier dokumentiert. 


## Software-defined datacenter

Software-defined Datacenter-Features wie "direkte Speicherplätze", Software-defined networking und abgeschirmte virtuelle Computer sind nicht enthalten in Windows Server, Version 1803. Wie in [Windows Server Semi-Annual Channel update](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/)beschrieben, die Windows Server Semi-Annual Channel konzentriert sich Container und Anwendungsszenarien, die von schneller Innovation profitieren. 

Wenn Sie Infrastruktur-Rollen benötigen, verwenden Sie eine Long-term Servicing Channel-Version: Windows Server 2016 (zurzeit verfügbar) oder [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (später in diesem Jahr bald).

Wir setzen uns für die optimale Plattform für hyperkonvergenten Infrastrukturen erstellen, und wir weiterhin an neue Features zu entwickeln und vorhandene basierend auf Ihr Feedback zu verbessern. Vielen Dank für Ihren Beitrag zu [mehr als 10.000 Cluster von direkte Speicherplätze](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum)gelangen! Wir freuen uns, mit der Freigabe von mehr später in diesem Jahr.