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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847771"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Änderungen bei Nano Server in Windows Server Semi-Annual Channel

>Gilt für: WindowsServer Halbjährlicher Kanal


Wie unter [Windows Server Semi-Annual Channel (Übersicht)](semi-annual-channel-overview.md) beschrieben, ist Windows Server Version 1803 die neueste Version des Semi-Annual Channel.

Wenn Sie bereits Nano Server ausführen, ist dieses Dienstmodell vertraut, da es vorher vom Current Branch for Business (CBB)-Modell bedient wurde. Das neue Semi-Annual Channel von Windows Server ist nur ein neuer Name für das gleiche Modell. In diesem Modell sind Featureupdateversionen von Nano Server zwei- bis dreimal pro Jahr zu erwarten.

In dieser Version von Windows Server, Version 1803, ist Nano Server nur als **Basisimage des Betriebssystems für den Container**verfügbar. Sie müssen es als Container in einem Containerhost ausführen, wie beispielsweise als eine Server Core-Installation von Windows Server. Das Ausführen eines Containers basierend auf Nano Server in dieser Version unterscheidet sich von früheren Versionen folgendermaßen:

- Nano Server wurde für .NET Core-Anwendungen optimiert.
- Nano Server ist noch kleiner als die Windows Server 2016-Version.
- PowerShell Core, .NET Core und WMI sind nicht mehr standardmäßig enthalten, Sie können jedoch [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) und [.NET Core](https://hub.docker.com/r/microsoft/dotnet/)-Container-Pakete einbeziehen, wenn Sie den Container erstellen.
- Der Bereitstellungsstapel ist nicht mehr in Nano Server enthalten. Microsoft veröffentlicht einen aktualisierten Nano-Container mit Docker Hub, den Sie erneut bereitstellen können.
- Docker kann zur Problembehandlung des neuen Nano-Containers verwendet werden.
- Sie können jetzt Nano-Container auf IoT Core ausführen.

## <a name="related-topics"></a>Verwandte Themen
Wenn das Windows-Insider-Programm gestartet wird finden Sie weitere Informationen unter [Dokumentation zu Windows-Container](http://aka.ms/windowscontainers).
