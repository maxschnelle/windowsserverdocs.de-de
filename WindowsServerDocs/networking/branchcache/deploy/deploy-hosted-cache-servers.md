---
title: Bereitstellen von gehosteten Cacheserver (Optional)
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 75f82b660edeac538bda511d71526aacc2433b5b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964246"
---
# <a name="deploy-hosted-cache-servers-optional"></a>Bereitstellen von gehosteten Cacheserver (Optional)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Verfahren zum Installieren und Konfigurieren von BranchCache-gehosteten Cache Servern verwenden, die sich in Zweigniederlassungen befinden, in denen Sie den BranchCache-Modus für gehostete Caches bereitstellen möchten. Mit BranchCache in Windows Server 2016 können Sie mehrere gehostete Cache Server in einer Zweigstelle bereitstellen.

> [!IMPORTANT]
> Dieser Schritt ist optional, da der Modus für verteilte Caches keinen gehosteten Cache Server Computer in Zweigniederlassungen erfordert. Wenn Sie nicht beabsichtigen, den Modus für gehostete Caches in Zweigstellen bereitzustellen, müssen Sie keinen gehosteten Cache Server bereitstellen, und Sie müssen die Schritte in diesem Verfahren nicht ausführen.

Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

### <a name="to-install-and-configure-a-hosted-cache-server"></a>So installieren und konfigurieren Sie einen gehosteten Cache Server

1.  Führen Sie auf dem Computer, den Sie als gehosteten Cache Server konfigurieren möchten, den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung aus, um das BranchCache-Feature zu installieren.

    `Install-WindowsFeature BranchCache -IncludeManagementTools`

2.  Konfigurieren Sie den Computer als gehosteten Cache Server, indem Sie einen der folgenden Befehle verwenden:

    -   Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE, um einen Computer zu konfigurieren, der nicht der Domäne beigetreten ist.

        `Enable-BCHostedServer`

    -   Geben Sie an der Windows PowerShell-Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um einen in die Domäne eingebundener Computer als gehosteten Cache Server zu konfigurieren und einen Dienst Verbindungspunkt in Active Directory für die automatische gehostete Cache Server Ermittlung durch Client Computer zu registrieren.

        `Enable-BCHostedServer -RegisterSCP`

3.  Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE, um die korrekte Konfiguration des gehosteten Cache Servers zu überprüfen.

    `Get-BCStatus`

    > [!NOTE]
    > Nachdem Sie diesen Befehl ausgeführt **haben, ist im Abschnitt "**" "" "" "" " **HostedCacheServerIsEnabled** " "" "" "" " **True**" "" "" "" "" "" " Wenn Sie einen in die Domäne eingebundener gehosteten Cache Server für die Registrierung eines Dienst Verbindungs Punkts (Service Connection Point, SCP) in Active Directory konfiguriert haben, lautet der Wert für **hostedcachescpregistrationaktiviert** **true**.


