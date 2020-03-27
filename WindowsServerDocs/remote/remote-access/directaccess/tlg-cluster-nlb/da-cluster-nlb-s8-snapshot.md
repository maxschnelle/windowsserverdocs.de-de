---
title: 'Schritt 8: Momentaufnahme des DirectAccess-Clusters (NLB-Konfiguration)'
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 915ef7dd-169d-4d58-9174-438d8ffa3584
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6848c3900e4dad389f40ce3c8c707bcf4ea30971
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310752"
---
# <a name="step-8-snapshot-the-directaccess-cluster-nlb-configuration"></a>Schritt 8: Momentaufnahme des DirectAccess-Clusters (NLB-Konfiguration)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dadurch wird die DirectAccess-Testumgebung abgeschlossen. Um diese Konfiguration zu speichern, sodass Sie schnell zu einer funktionierenden DirectAccess-Konfiguration mit NLB-Cluster Konfiguration zurückkehren können, mit der Sie andere Test Umgebungs Anleitungen für DirectAccess und Test Umgebungs Anleitungen testen können, oder für Ihr eigenes Experimentieren und lernen, führen Sie die folgenden Schritte aus: folgenden  
  
1.  Schließen Sie alle Fenster auf allen physischen oder virtuellen Computern in der Testumgebung, und fahren Sie die Computer dann normal herunter.  
  
2.  Wenn Ihre Testumgebung auf virtuellen Computern basiert, speichern Sie eine Momentaufnahme der einzelnen virtuellen Computer, und benennen Sie die Momentaufnahmen DirectAccess-Cluster und NLB. Wenn Ihr Lab physische Computer verwendet, erstellen Sie Datenträger Images, um die Konfiguration der DirectAccess-Testumgebung zu speichern.  
