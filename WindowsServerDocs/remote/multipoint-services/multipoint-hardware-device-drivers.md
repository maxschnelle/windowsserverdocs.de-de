---
title: Erfassen von der für die Installation benötigten Hardware und Gerätetreiber
description: Informationen zu Treibern müssen Sie für MultiPoint Services installieren
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cf5fdbe-b871-4360-b003-d65ac43b491e
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: a9d902e2599cdcd69e156d1fabec87a067b1d8ea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833421"
---
# <a name="collect-hardware-and-device-drivers-needed-for-the-installation"></a>Erfassen von der für die Installation benötigten Hardware und Gerätetreiber
Bevor Sie beginnen, Ihre MultiPoint Services-System bereitstellen, benötigen Sie:  
  
-   **Hardware-Komponenten für den Server** – installieren Sie zu diesem Zeitpunkt zusätzlichen Videokarten oder anderen Systemkomponenten.  
  
-   **Hardware-Komponenten für die Stationen** – Weitere Informationen zur Planung von Stationen für Ihre Umgebung finden Sie unter [Auswählen der Hardware für Ihr MultiPoint Services-Systems](Selecting-Hardware-for-Your-MultiPoint-services-System.md).
-   **Die neuesten Treiber für Ihre Grafikkarten** – Wenn es sich bei Ihrem OEM oder Gerätehersteller diese nicht angegeben wurde, müssen Sie diese von der Website des Herstellers herunterladen.  
  
-   **Die neuesten USB-0 (null)-Client-Treiber** – Wenn Sie USB-0 (null) Client Stationen verwenden, müssen Sie die neuesten Client-Treiber von USB-0 (null) installieren.  
  
    > [!IMPORTANT]  
    > Für eine MultiPoint Services-Installation müssen Sie die 64-Bit-Version, der alle Treiber installieren.  
  
> [!TIP]  
> Bei Installation von MultiPoint Services auf einem Computer mit einer anderen Version von Windows bereits installiert sollten Sie herausfinden, Grafikkarte Fabrikat und Modell im Geräte-Manager vor der Installation von Windows Server und stellen Sie sicher, dass Sie Treiber erhalten können, sind für Windows Server 2016 verfügbar. Open-Geräte-Manager öffnen **Computerverwaltung** aus der **starten** Bildschirm. Klicken Sie in der Konsolenstruktur auf **-Geräte-Manager**.