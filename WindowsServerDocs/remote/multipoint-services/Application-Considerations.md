---
title: Überlegungen zu Anwendungen
description: Compatibility-Informationen für apps in MultiPoint Services
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 445e6184-4e1e-4f10-ad3c-042f2a6c2f5f
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 400f87c09f1b2e897d67f94e9b7ac12ae0a1e799
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839831"
---
# <a name="application-considerations"></a>Überlegungen zu Anwendungen
  
## <a name="application-compatibility"></a>Anwendungskompatibilität

Jede Anwendung, die Sie in einem MultiPoint Services-System ausführen möchten, muss die folgenden Anforderungen erfüllen:
  
- Es sollte installieren und Ausführen unter Windows Server 2016 
- Es muss Sitzung bewusst sein, damit jeder Benutzer eine Instanz der app in einem MultiPoint-System ausgeführt werden kann.
  
Wenn die Anwendung diese Anforderung angegeben ist, empfehlen wir, versuchen die Anwendung zu installieren und verwenden in einer Remotedesktopsitzung. 

## <a name="addressing-application-compatibility-problems"></a>Probleme mit Adressierung der Anwendungskompatibilität  
MultiPoint Services bietet die Option zum Verknüpfen von Stationen mit vollständigen Instanzen von Windows 10 Enterprise-Editionen, die praktisch auf demselben Hostcomputer ausgeführt werden. Für kritische Anwendungen, die mehrere Instanzen für mehrere Benutzer werden nicht ausgeführt oder werden nicht auf einem 64-Bit-Betriebssystem installiert ist, kann dies eine Lösung sein. Bereitstellen von Desktops auf diese Weise müssen mithilfe der Registerkarte virtuelle Desktops im MultiPoint-Manager:  
  
-   Virtuelle Desktops aktivieren  
-   Erstellen einer Vorlage für Desktops  
-   Passen Sie die Vorlage mit der problemanwendung  
-   Zuordnen von Stationen mit der angepassten Vorlage  

Jede Station beginnt mit der gleichen Vorlage, damit jedes Mal alle Änderungen gelöscht werden, wenn der Computer gestartet wird.  
  
>[!NOTE] 
>Es ist wichtig, überprüfen die lizenzanforderungen für die Anwendungen auf einem MultiPoint ausführen möchten. Obwohl Sie installieren möglicherweise eine Kopie von Anwendungen die Lizenzierung pro Benutzer.  
  
