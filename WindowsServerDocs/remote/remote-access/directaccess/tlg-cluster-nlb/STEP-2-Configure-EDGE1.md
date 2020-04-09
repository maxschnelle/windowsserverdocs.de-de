---
title: Schritt 2 Edge1 konfigurieren
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8705e69debec2f0a19f5cc010ed5ca254cc56741
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819313"
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
