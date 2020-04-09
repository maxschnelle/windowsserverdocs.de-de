---
title: Erfassen von der für die Installation benötigten Hardware und Gerätetreiber
description: Informationen zu Treibern, die für Multipoint Services installiert werden müssen
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 4cf5fdbe-b871-4360-b003-d65ac43b491e
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 57e47b357d5b6311c69cf54a74e3eaff7913da53
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858723"
---
# <a name="collect-hardware-and-device-drivers-needed-for-the-installation"></a>Erfassen von der für die Installation benötigten Hardware und Gerätetreiber
Bevor Sie mit der Bereitstellung Ihres Multipoint Services-Systems beginnen, benötigen Sie Folgendes:  
  
-   **Hardware Komponenten für den Server** : Installieren Sie zu diesem Zeitpunkt alle zusätzlichen Grafikkarten oder anderen Systemkomponenten.  
  
-   **Hardwarekomponenten für die Stationen** : Informationen zum Planen von Stationen für Ihre Umgebung finden Sie unter [Auswählen von Hardware für Ihr Multipoint Services-System](Selecting-Hardware-for-Your-MultiPoint-services-System.md).
-   **Die neuesten Treiber für ihre Grafikkarten** : Wenn Ihr OEM-oder Gerätehersteller diese nicht bereitgestellt hat, müssen Sie Sie von der Website des Geräteherstellers herunterladen.  
  
-   **Die neuesten USB Zero-Client Treiber** : Wenn Sie USB-Client Stationen verwenden, müssen Sie die neuesten USB-Client Treiber installieren.  
  
    > [!IMPORTANT]  
    > Für eine Multipoint Services-Installation müssen Sie die 64-Bit-Version der Treiber installieren.  
  
> [!TIP]  
> Wenn Sie Multipoint Services auf einem Computer installieren, auf dem bereits eine andere Version von Windows installiert ist, sollten Sie vor dem Starten der Windows Server-Installation das Videokarten-und-Modell in Geräte-Manager finden und sicherstellen, dass Sie Treiber abrufen können, die für Windows Server 2016 verfügbar sind. Öffnen Sie Geräte-Manager, und öffnen Sie die **Computer Verwaltung** über den **Start** Bildschirm. Klicken Sie dann in der Konsolen Struktur auf **Geräte-Manager**.