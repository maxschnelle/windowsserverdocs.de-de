---
title: Schritt 2 Edge1 konfigurieren
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b9eb37433e26c174ccae85482163c976577ff479
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388510"
---
# <a name="step-2-configure-edge1"></a>Schritt 2 Edge1 konfigurieren

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Das folgende Verfahren wird auf dem DirectAccess-Server ausgeführt:

## <a name="to-configure-directaccess-on-edge1"></a>So konfigurieren Sie DirectAccess auf Edge1
  
1.  Geben Sie auf dem **Start** Bildschirm**ramgmtui. exe**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole im linken Bereich auf **Konfiguration**.  
  
3.  Klicken Sie im mittleren Bereich der Konsole im Bereich **Schritt 2** RAS-Server auf **Bearbeiten**.  
  
4.  Klicken Sie im Setup-Assistenten für den **Remote Zugriffs Server** auf **Präfix Konfiguration**. Geben Sie auf der Seite **Präfix Konfiguration** unter **IPv6-Präfix, das DirectAccess-Client Computern zugewiesen**ist Folgendes ein **: 2001: db8:1: 1000::/59**, und klicken Sie dann auf **weiter**.  
  
5.  Klicken Sie auf **Fertig stellen**.  
  
6.  Klicken Sie im mittleren Bereich der Konsole auf **Fertig**stellen.  
  
7.  Überprüfen Sie im Dialogfeld **Remote Zugriffs Überprüfung** die Konfigurationseinstellungen, und klicken Sie **dann auf über**nehmen. Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.
