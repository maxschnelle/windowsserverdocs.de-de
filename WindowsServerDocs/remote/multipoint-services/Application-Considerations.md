---
title: Überlegungen zu Anwendungen
description: Kompatibilitätsinformationen für apps in Multipoint Services
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 21531273b1dd6d643df3f816a880a0efb3117c70
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405129"
---
# <a name="application-considerations"></a>Überlegungen zu Anwendungen
  
## <a name="application-compatibility"></a>Anwendungskompatibilität

Alle Anwendungen, die Sie in einem Multipoint Services-System ausführen möchten, müssen die folgenden Anforderungen erfüllen:
  
- Es sollte auf Windows Server 2016 installiert und ausgeführt werden. 
- Er muss Sitzungs fähig sein, damit jeder Benutzer eine Instanz der app in einem Multipoint-System ausführen kann.
  
Wenn die Anwendung diese Anforderung angibt, empfiehlt es sich, zu versuchen, die Anwendung zu installieren und in einer Remote Desktop Sitzung zu verwenden. 

## <a name="addressing-application-compatibility-problems"></a>Adressieren von Anwendungs Kompatibilitätsproblemen  
Multipoint Services bietet die Option, Stationen vollständigen Instanzen von Windows 10 Enterprise Edition zuzuordnen, die virtuell auf demselben Host Computer ausgeführt werden. Bei kritischen Anwendungen, die nicht mehrere-Instanzen für mehrere Benutzer ausführen oder nicht auf einem 64-Bit-Betriebssystem installiert werden, kann dies eine Lösung sein. Wenn Sie Desktops auf diese Weise bereitstellen, müssen Sie die Registerkarte virtuelle Desktops im Multipoint-Manager für Folgendes  
  
-   Virtuelle Desktops aktivieren  
-   Erstellen einer Desktop Vorlage  
-   Anpassen der Vorlage mit der Problem Anwendung  
-   Ordnen Sie Stationen der angepassten Vorlage zu.  

Jede Station beginnt mit derselben Vorlage, sodass alle Änderungen bei jedem Start des Computers gelöscht werden.  
  
>[!NOTE] 
>Es ist wichtig, die Lizenzierungsanforderungen für die Anwendungen zu überprüfen, die Sie auf einem Multipoint ausführen möchten. Obwohl Sie eine Kopier Anwendung installieren, ist möglicherweise eine Lizenzierung pro Benutzer erforderlich.  
  
