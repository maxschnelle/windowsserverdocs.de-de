---
title: Schritt 2 Konfigurieren von EDGE1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: Vorführen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6c31e65fc7210849564bd0541085322a7a6c284e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838581"
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
