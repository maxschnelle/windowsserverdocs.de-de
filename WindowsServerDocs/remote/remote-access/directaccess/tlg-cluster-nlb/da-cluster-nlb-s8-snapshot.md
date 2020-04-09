---
title: 'Schritt 8: Momentaufnahme des DirectAccess-Clusters (NLB-Konfiguration)'
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 915ef7dd-169d-4d58-9174-438d8ffa3584
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 99804fb7746e0e45f586f7eaea307d8aac47d0ca
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818994"
---
# <a name="step-8-snapshot-the-directaccess-cluster-nlb-configuration"></a>Schritt 8: Momentaufnahme des DirectAccess-Clusters (NLB-Konfiguration)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dadurch wird die DirectAccess-Testumgebung abgeschlossen. Um diese Konfiguration zu speichern, sodass Sie schnell zu einer funktionierenden DirectAccess-Konfiguration mit NLB-Cluster Konfiguration zurückkehren können, mit der Sie andere Test Umgebungs Anleitungen für DirectAccess und Test Umgebungs Anleitungen testen können, oder für Ihr eigenes Experimentieren und lernen, führen Sie die folgenden Schritte aus: folgenden  
  
1.  Schließen Sie alle Fenster auf allen physischen oder virtuellen Computern in der Testumgebung, und fahren Sie die Computer dann normal herunter.  
  
2.  Wenn Ihre Testumgebung auf virtuellen Computern basiert, speichern Sie eine Momentaufnahme der einzelnen virtuellen Computer, und benennen Sie die Momentaufnahmen DirectAccess-Cluster und NLB. Wenn Ihr Lab physische Computer verwendet, erstellen Sie Datenträger Images, um die Konfiguration der DirectAccess-Testumgebung zu speichern.  
