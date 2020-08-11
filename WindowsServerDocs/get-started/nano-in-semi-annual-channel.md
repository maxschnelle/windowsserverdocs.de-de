---
title: Änderungen bei Nano Server in Windows Server (halbjährlicher Kanal)
description: Im neuen Windows Server-Servicemodell ist Nano Server nur ein Container-Betriebssystem mit bestimmten Änderungen.
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: c1b25402a209bf460c130f4fd76928f95dc7c0a7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967917"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Änderungen bei Nano Server in Windows Server (halbjährlicher Kanal)

>Gilt für: Windows Server (halbjährlicher Kanal)

Wenn Sie bereits Nano Server ausführen, wird Ihnen das Servicemodell [Windows Server (halbjährlicher Kanal)](../get-started-19/servicing-channels-19.md) vertraut sein, da es vorher vom Current Branch for Business (CBB)-Modell bedient wurde. Der neue halbjährliche Kanal von Windows Server ist nur ein neuer Name für das gleiche Modell. In diesem Modell sind Featureupdateversionen von Nano Server zwei- bis dreimal pro Jahr zu erwarten.

Ab Windows Server, Version 1803, steht Nano Server jedoch nur als **Basis-Betriebssystemimage für Container** zur Verfügung. Sie müssen es als Container in einem Containerhost ausführen, wie beispielsweise als eine Server Core-Installation von Windows Server. Das Ausführen eines Containers basierend auf Nano Server in diesem Release unterscheidet sich von früheren Releases folgendermaßen:

- Nano Server wurde für .NET Core-Anwendungen optimiert.
- Nano Server ist noch kleiner als die Windows Server 2016-Version.
- PowerShell Core, .NET Core und WMI sind nicht mehr standardmäßig enthalten, Sie können jedoch [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) und [.NET Core](https://hub.docker.com/r/microsoft/dotnet/)-Container-Pakete einbeziehen, wenn Sie den Container erstellen.
- Der Bereitstellungsstapel ist nicht mehr in Nano Server enthalten. Microsoft veröffentlicht einen aktualisierten Nano-Container mit Docker Hub, den Sie erneut bereitstellen können.
- Docker kann zur Problembehandlung des neuen Nano-Containers verwendet werden.
- Sie können jetzt Nano-Container auf IoT Core ausführen.

## <a name="related-topics"></a>Zugehörige Themen

- [Dokumentation zu Windows-Containern](https://aka.ms/windowscontainers)
- [Übersicht: Windows Server, (halbjährlicher Kanal)](../get-started-19/servicing-channels-19.md)
