---
title: Änderungen bei Nano Server in Windows Server Semi-Annual Channel
description: Im neuen Windows Server-Wartungsmodell ist Nano Server nur ein Container-Betriebssystem mit bestimmten Änderungen.
ms.prod: Windows Server
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: c9fede02b90e285803a8bcdbc983f264d65a4589
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976514"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Änderungen bei Nano Server in Windows Server Semi-Annual Channel

>Gilt für: WindowsServer Halbjährlicher Kanal

Wenn Sie bereits einsetzen, Nano Server-Instanz, die [Fenster Server Halbjährlicher Kanal](..\get-started-19\servicing-channels-19.md) servicing-Modell vertraut sein, da es von der Current Branch for Business (CBB)-Modell zuvor verarbeitet wurde. Windows Server Halbjährlicher Kanal ist nur für einen neuen Namen für das gleiche Modell an. In diesem Modell sind Featureupdateversionen von Nano Server zwei- bis dreimal pro Jahr zu erwarten.

Ab Version 1803 Windows Server, Nano Server-Instanz steht jedoch nur als eine **Basis Containerbetriebssystem-Image**. Sie müssen es als Container in einem Containerhost ausführen, wie beispielsweise als eine Server Core-Installation von Windows Server. Das Ausführen eines Containers basierend auf Nano Server in dieser Version unterscheidet sich von früheren Versionen folgendermaßen:

- Nano Server wurde für .NET Core-Anwendungen optimiert.
- Nano Server ist noch kleiner als die Windows Server 2016-Version.
- PowerShell Core, .NET Core und WMI sind nicht mehr standardmäßig enthalten, Sie können jedoch [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) und [.NET Core](https://hub.docker.com/r/microsoft/dotnet/)-Container-Pakete einbeziehen, wenn Sie den Container erstellen.
- Der Bereitstellungsstapel ist nicht mehr in Nano Server enthalten. Microsoft veröffentlicht einen aktualisierten Nano-Container mit Docker Hub, den Sie erneut bereitstellen können.
- Docker kann zur Problembehandlung des neuen Nano-Containers verwendet werden.
- Sie können jetzt Nano-Container auf IoT Core ausführen.

## <a name="related-topics"></a>Verwandte Themen

- [Dokumentation zu Windows-Container](http://aka.ms/windowscontainers)
- [Übersicht über die Fenster Server Halbjährlicher Kanal](..\get-started-19\servicing-channels-19.md)
