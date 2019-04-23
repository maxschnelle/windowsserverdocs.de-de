---
title: Mindestens ein Netzwerk für live Migration-Traffic müssen eine verbindungsgeschwindigkeit von mindestens 1 Gbit/s
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ef75f73bd934b863b146e93f4cdc7323e5d4c6fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837731"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>Mindestens ein Netzwerk für live Migration-Traffic müssen eine verbindungsgeschwindigkeit von mindestens 1 Gbit/s

>Gilt für: Windows Server 2016


  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Keines der Netzwerke für livemigrations-Datenverkehr über eine verbindungsgeschwindigkeit von mindestens 1 Gbit/s verfügen.*  
  
## <a name="impact"></a>Auswirkungen  
*Live-Migrationen können langsam, auftreten, die konnte die Netzwerkverbindung aufgrund eines Timeouts der TCP-Verbindung unterbrochen werden.*  
  
## <a name="resolution"></a>Auflösung  
*Konfigurieren Sie mindestens ein Netzwerk für live-Migration mit einer Geschwindigkeit von 1 Gbit/s oder schneller.*  
  
Finden Sie in der Dokumentation von Ihrem Netzwerk Hardware-Hersteller, um herauszufinden, ob Ihre vorhandenen Netzwerkadapter eine verbindungsgeschwindigkeit von mindestens 1 Gbit/s unterstützen können.  
  


