---
title: Verwenden von Windows PowerShell zum Konfigurieren von Client Computern, die kein Domänen Mitglied sind
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 57fbe66168ccf1db5f4136d805206036405b3848
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964296"
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Verwenden von Windows PowerShell zum Konfigurieren von Client Computern, die kein Domänen Mitglied sind

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie einen BranchCache-Client Computer manuell für den Modus "verteilter Cache" oder den Modus "gehosteter Cache" konfigurieren.

> [!NOTE]
> Wenn Sie BranchCache-Client Computer mithilfe von Gruppenrichtlinie konfiguriert haben, überschreiben die Gruppenrichtlinie Einstellungen jegliche manuelle Konfiguration der Client Computer, auf die die Richtlinien angewendet werden.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>So aktivieren Sie den verteilten oder gehosteten BranchCache-Modus

1.  Führen Sie auf dem BranchCache-Client Computer, den Sie konfigurieren möchten, Windows PowerShell als Administrator aus, und führen Sie dann eine der folgenden Aktionen aus.

    -   Zum Konfigurieren des Client Computers für den BranchCache-Modus "verteilter Cache" geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

        `Enable-BCDistributed`

    -   Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um den Client Computer für den BranchCache-gehosteten Cache Modus zu konfigurieren.

        `Enable-BCHostedClient`

        > [!TIP]
        > Wenn Sie die verfügbaren gehosteten Cache Server angeben möchten, verwenden Sie den- `-ServerNames` Parameter mit einer durch Trennzeichen getrennten Liste der gehosteten Cache Server als Parameterwert. Wenn Sie z. b. über zwei gehostete Cache Server mit den Namen HCS1 und HCS2 verfügen, konfigurieren Sie den Client Computer für den gehosteten Cache Modus mit dem folgenden Befehl.
        >
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`



