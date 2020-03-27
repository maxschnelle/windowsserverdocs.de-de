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
ms.author: lizross
author: eross-msft
ms.openlocfilehash: eea83bd9788ffd704b6169c140adc68465f9325d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310843"
---
# <a name="step-2-configure-edge1"></a>Schritt 2 Edge1 konfigurieren

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Das folgende Verfahren wird auf dem DirectAccess-Server ausgeführt:

## <a name="to-configure-directaccess-on-edge1"></a>So konfigurieren Sie DirectAccess auf Edge1
  
1.  Geben Sie auf dem **Start** Bildschirm**ramgmtui. exe**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole im linken Bereich auf **Konfiguration**.  
  
3.  Klicken Sie im mittleren Bereich der Konsole im Bereich **Schritt 2** RAS-Server auf **Bearbeiten**.  
  
4.  Klicken Sie im Setup-Assistenten für den **Remote Zugriffs Server** auf **Präfix Konfiguration**. Geben Sie auf der Seite **Präfix Konfiguration** unter **IPv6-Präfix, das DirectAccess-Client Computern zugewiesen**ist Folgendes ein **: 2001: db8:1: 1000::/59**, und klicken Sie dann auf **weiter**.  
  
5.  Klicken Sie auf **Fertig stellen**.  
  
6.  Klicken Sie im mittleren Bereich der Konsole auf **Fertig**stellen.  
  
7.  Überprüfen Sie im Dialogfeld **Remote Zugriffs Überprüfung** die Konfigurationseinstellungen, und klicken Sie **dann auf über**nehmen. Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.
