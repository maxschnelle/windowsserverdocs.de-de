---
title: Konfigurieren von Inhaltsservern von Windows Server Update Services (WSUS)
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das veranschaulicht, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2993c78e85609ac720fd208971dda7ed67a3610d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319165"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Konfigurieren von Inhaltsservern von Windows Server Update Services (WSUS)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Nachdem Sie das BranchCache-Feature installiert und den BranchCache-Dienst gestartet haben, müssen WSUS-Server konfiguriert werden, um Update Dateien auf dem lokalen Computer zu speichern. 

Wenn Sie WSUS-Server konfigurieren, um Updatedateien auf dem lokalen Computer zu speichern, werden dadurch sowohl die Updatemetadaten als auch die Updatedateien heruntergeladen und direkt auf dem WSUS-Server gespeichert. Dadurch wird sichergestellt, dass BranchCache-Clientcomputer Microsoft-Produktupdatedateien vom WSUS-Server empfangen anstatt direkt von der Microsoft Update-Website.  
  
Weitere Informationen zur WSUS-Synchronisierung finden [Sie unter Einrichten von Update Synchronisierungen](https://technet.microsoft.com/library/mt612311.aspx) .  