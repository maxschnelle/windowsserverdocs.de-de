---
title: Alle Netzwerke für den Live Migrations Datenverkehr sollten eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s aufweisen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 89411b63-bec8-463d-b486-107548ed440e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: adb16b1c4618e0874f48f4715440a9d903f5bc9f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857843"
---
# <a name="all-networks-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>Alle Netzwerke für den Live Migrations Datenverkehr sollten eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s aufweisen.

>Gilt für: Windows Server 2016


  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Keines der Netzwerke für den Live Migrations Datenverkehr hat eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s.*  
  
## <a name="impact"></a>Auswirkungen  
*Live Migrationen können langsam erfolgen, was die Netzwerkverbindung aufgrund eines TCP-Verbindungs Timeouts stören könnte.*  
  
## <a name="resolution"></a>Auflösung  
*Konfigurieren Sie mindestens ein Live Migrationsnetzwerk mit einer Geschwindigkeit von 1 Gbit/s oder schneller.*  
  
Sehen Sie sich die Dokumentation Ihres Netzwerkhardware Herstellers an, um herauszufinden, ob vorhandene Netzwerkadapter eine Verbindungsgeschwindigkeit von mindestens 1 Gbit/s unterstützen können.  
  


