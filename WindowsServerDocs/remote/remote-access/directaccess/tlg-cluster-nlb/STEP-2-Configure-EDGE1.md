---
title: Schritt 2 Konfigurieren von EDGE1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: Vorführen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 03d7d85f730cf792238aef372337030861cd6a9d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281675"
---
# <a name="step-2-configure-edge1"></a>Schritt 2 Konfigurieren von EDGE1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Das folgende Verfahren wird auf dem DirectAccess-Server ausgeführt werden:

## <a name="to-configure-directaccess-on-edge1"></a>Zum Konfigurieren von DirectAccess auf EDGE1
  
1.  Auf der **starten** geben**RAMgmtUI.exe**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole, klicken Sie im linken Bereich auf **Konfiguration**.  
  
3.  Im mittleren Bereich der Konsole in der **Schritt 2 RAS-Server** Bereich, klicken Sie auf **bearbeiten**.  
  
4.  In der **RAS-Server-Setup** -Assistenten klicken Sie auf **Präfixkonfiguration**. Auf der **Präfixkonfiguration** auf der Seite **IPv6-Präfix, die DirectAccess-Clientcomputer zugewiesen**, geben Sie **2001:db8:1:1000:: / 59**, und klicken Sie dann auf **weiter** .  
  
5.  Klicken Sie auf **Fertig stellen**.  
  
6.  Klicken Sie im mittleren Bereich der Konsole auf **Fertig stellen**.  
  
7.  Auf der **Remote Zugriffsüberprüfung** (Dialogfeld), überprüfen Sie die Konfigurationseinstellungen, und klicken Sie dann auf **übernehmen**. Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.
