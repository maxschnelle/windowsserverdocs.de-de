---
title: Installieren und Konfigurieren von Inhaltsservern
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: e753c56b-8902-4610-9c53-381e77bf29ab
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c1efeb5d63be8ce5b91c814825b68f9f43ae4049
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954116"
---
# <a name="install-and-configure-content-servers"></a>Installieren und Konfigurieren von Inhaltsservern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie BranchCache im Modus "verteilter Cache" oder im Modus "gehosteter Cache" bereitstellen, müssen Sie mindestens einen Inhalts Server in der Hauptniederlassung oder in der Cloud bereitstellen. Inhalts Server, bei denen es sich um Webserver oder Anwendungsserver handelt, verwenden das BranchCache-Feature. Inhalts Server, bei denen es sich um Dateiserver handelt, verwenden den Rollen Dienst "BranchCache für Netzwerkdateien" der Server Rolle "Dateidienste" in Windows Server 2016.

Weitere Informationen zur Bereitstellung von Inhaltsservern finden Sie in den folgenden Themen.

-   [Installieren von Inhalts Servern, die die BranchCache-Funktion verwenden](../../branchcache/deploy/Install-Content-Servers-that-Use-the-BranchCache-Feature.md)

-   [Installieren von Datei Dienst-Inhalts Servern](../../branchcache/deploy/Install-File-Services-Content-Servers.md)



