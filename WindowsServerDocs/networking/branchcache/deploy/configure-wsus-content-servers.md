---
title: Konfigurieren von Inhaltsservern von Windows Server Update Services (WSUS)
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e8576282be92f02daf716da82ea75eddc755ee5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873841"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Konfigurieren von Inhaltsservern von Windows Server Update Services (WSUS)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nach dem Installieren der BranchCache-Funktion, und starten den BranchCache-Dienst, müssen WSUS-Server konfiguriert werden, um Updatedateien auf dem lokalen Computer zu speichern. 

Wenn Sie WSUS-Server konfigurieren, um Updatedateien auf dem lokalen Computer zu speichern, werden dadurch sowohl die Updatemetadaten als auch die Updatedateien heruntergeladen und direkt auf dem WSUS-Server gespeichert. Dadurch wird sichergestellt, dass BranchCache-Clientcomputer Microsoft-Produktupdatedateien vom WSUS-Server empfangen anstatt direkt von der Microsoft Update-Website.  
  
Weitere Informationen zur Synchronisierung von WSUS finden Sie unter [Update-Synchronisierung einrichten](https://technet.microsoft.com/library/mt612311.aspx)  