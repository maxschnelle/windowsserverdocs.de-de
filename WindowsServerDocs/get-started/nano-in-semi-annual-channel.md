---
title: Änderungen bei Nano Server in Windows Server Semi-Annual Channel
description: Im neuen Windows Server-Wartungsmodell ist Nano Server nur ein Container-Betriebssystem mit bestimmten Änderungen.
ms.prod: Windows Server
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: medium
ms.date: 05/02/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: 7e68d292c32ce58c786a3242203330fcae985913
ms.sourcegitcommit: 4b9b21ca1f366388a78ead7413cb581f2b23d4c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "2711955"
---
# Änderungen bei Nano Server in Windows Server Semi-Annual Channel

>Gilt für: Windows Server, Semi-Annual Channel


Wie unter [Windows Server Semi-Annual Channel (Übersicht)](semi-annual-channel-overview.md) beschrieben, ist Windows Server Version 1803 die neueste Version des Semi-Annual Channel.

Wenn Sie bereits Nano Server ausführen, ist dieses Dienstmodell vertraut, da es vorher vom Current Branch for Business (CBB)-Modell bedient wurde. Das neue Semi-Annual Channel von Windows Server ist nur ein neuer Name für das gleiche Modell. In diesem Modell sind Versionen der Funktionsupdates von Nano Server zwei- bis dreimal pro Jahr zu erwarten.

In dieser Version von Windows Server, Version 1803, ist Nano Server nur als **Basisimage des Betriebssystems für den Container**verfügbar. Sie müssen es als Container in einem Containerhost ausführen, wie beispielsweise als eine Server Core-Installation von Windows Server. Das Ausführen eines Containers basierend auf Nano Server in dieser Version unterscheidet sich von früheren Versionen folgendermaßen:

- Nano Server wurde für .NET Core-Anwendungen optimiert.
- Nano Server ist noch kleiner als die Windows Server2016-Version.
- PowerShell Core, .NET Core und WMI sind nicht mehr standardmäßig enthalten, Sie können jedoch [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) und [.NET Core](https://hub.docker.com/r/microsoft/dotnet/)-Container-Pakete einbeziehen, wenn Sie den Container erstellen.
- Der Bereitstellungsstapel ist nicht mehr in Nano Server enthalten. Microsoft veröffentlicht einen aktualisierten Nano-Container mit Docker Hub, den Sie erneut bereitstellen können.
- Docker kann zur Problembehandlung des neuen Nano-Containers verwendet werden.
- Sie können jetzt Nano-Container auf IoT Core ausführen.

## Verwandte Themen
Wenn das Windows-Insider-Programm gestartet wird finden Sie weitere Informationen unter [Dokumentation zu Windows-Container](http://aka.ms/windowscontainers).
