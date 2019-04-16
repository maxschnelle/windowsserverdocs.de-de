---
title: Konfigurieren von Windows Server Update Services (WSUS)-Inhaltsserver
description: Dieses Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8200a0905f7bc5c403288a22faece5f84eac8af9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Konfigurieren von Windows Server Update Services (WSUS)-Inhaltsserver

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Nach dem Installieren der BranchCache-Funktion und den BranchCache-Dienst starten, müssen WSUS-Server zum Speichern von Updatedateien auf dem lokalen Computer konfiguriert werden. 

Wenn Sie WSUS-Server zum Speichern von Updatedateien auf dem lokalen Computer konfigurieren, werden sowohl die Updatemetadaten als auch die Updatedateien heruntergeladen und direkt auf dem WSUS-Server gespeichert. Dadurch wird sichergestellt, dass die BranchCache-Clientcomputer Microsoft-produktupdatedateien vom WSUS-Server nicht direkt von der Website von Microsoft Update empfangen.  
  
Weitere Informationen zu WSUS-Synchronisierung finden Sie unter [Update-Synchronisierung einrichten](https://technet.microsoft.com/en-us/library/mt612311.aspx)  