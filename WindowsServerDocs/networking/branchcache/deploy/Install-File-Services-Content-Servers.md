---
title: Installieren von Dateidienst-Inhaltsservern
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1b62e18a1ca90008a2fb9b0d52d5a634f13c6dd5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952644"
---
# <a name="install-file-services-content-servers"></a>Installieren von Dateidienst-Inhaltsservern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Zum Bereitstellen von Inhaltsservern, die die Serverrolle Dateidienste ausführen, müssen Sie den BranchCache-Rollendienst für Netzwerkdateien der Serverrolle Dateidienste installieren. Außerdem müssen Sie BranchCache auf Dateifreigaben entsprechend Ihren Anforderungen aktivieren.

Während der Konfiguration des Inhaltsservers können Sie BranchCache-Inhaltsveröffentlichung für alle Dateifreigaben zulassen, oder Sie können eine Teilmenge von Dateifreigaben zur Veröffentlichung auswählen.

> [!NOTE]
> Beim Bereitstellen eines BranchCache-fähigen Dateiservers oder Webservers als Inhalts Server werden die Inhaltsinformationen jetzt offline berechnet, bevor ein BranchCache-Client eine Datei anfordert. Aufgrund dieser Verbesserung müssen Sie die Hash Veröffentlichung für Inhalts Server nicht wie in der vorherigen Version von BranchCache konfigurieren.
>
> Diese automatische Hash Generierung sorgt für eine schnellere Leistung und mehr Bandbreiten Einsparungen, da Inhaltsinformationen für den ersten Client bereit sind, der den Inhalt anfordert, und Berechnungen bereits durchgeführt wurden.

Weitere Informationen zur Bereitstellung von Inhaltsservern finden Sie in den folgenden Themen.

-   [Konfigurieren der Dateidienst-Serverrolle](../../branchcache/deploy/Configure-the-File-Services-server-role.md)

-   [Aktivieren der Hash Veröffentlichung für Dateiserver](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)

-   [Aktivieren Sie BranchCache auf einer Dateifreigabe &#40;optional&#41;](../../branchcache/deploy/enable-bc-on-file-share.md)



