---
title: Konfigurieren von Inhaltsservern von Windows Server Update Services (WSUS)
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das veranschaulicht, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0836c91948b13d2e6bac540294a55cb49523158d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406418"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Konfigurieren von Inhaltsservern von Windows Server Update Services (WSUS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Nachdem Sie das BranchCache-Feature installiert und den BranchCache-Dienst gestartet haben, müssen WSUS-Server konfiguriert werden, um Update Dateien auf dem lokalen Computer zu speichern. 

Wenn Sie WSUS-Server konfigurieren, um Updatedateien auf dem lokalen Computer zu speichern, werden dadurch sowohl die Updatemetadaten als auch die Updatedateien heruntergeladen und direkt auf dem WSUS-Server gespeichert. Dadurch wird sichergestellt, dass BranchCache-Clientcomputer Microsoft-Produktupdatedateien vom WSUS-Server empfangen anstatt direkt von der Microsoft Update-Website.  
  
Weitere Informationen zur WSUS-Synchronisierung finden [Sie unter Einrichten von Update Synchronisierungen](https://technet.microsoft.com/library/mt612311.aspx) .  