---
title: Schritt 7 Testen der Konnektivität bei der Rückkehr zum Unternehmensnetzwerk
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 5a7252d0-6db8-4a9d-98ee-75082ecd2929
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 479ac48bbb04186f97d25e6744e8630b4dc6a51e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819123"
---
# <a name="step-7-test-connectivity-when-returning-to-the-corpnet"></a>Schritt 7 Testen der Konnektivität bei der Rückkehr zum Unternehmensnetzwerk

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Viele Ihrer Benutzer wechseln zwischen Remote Standorten und dem Unternehmensnetzwerk. Daher ist es wichtig, wenn Sie zum Unternehmensnetzwerk zurückkehren, dass Sie auf Ressourcen zugreifen können, ohne Änderungen an der Konfiguration vornehmen zu müssen. Der Remote Zugriff ermöglicht dies, weil der DirectAccess-Client beim zurückkehren zum Corpnet eine Verbindung mit dem Netzwerkadressen Server herstellen kann. Nachdem die HTTPS-Verbindung erfolgreich mit dem Netzwerkadressen Server hergestellt wurde, deaktiviert der DirectAccess-Client die DirectAccess-Client Konfiguration und verwendet eine direkte Verbindung mit Corpnet.  
  
### <a name="test-connectivity-on-client1"></a>Testen der Konnektivität auf CLIENT1  
  
1. Beenden Sie CLIENT1, und entfernen Sie dann CLIENT1 aus dem Subnetz homenet oder dem virtuellen Switch, und verbinden Sie es mit dem Subnetz "Corpnet" oder dem virtuellen Switch. Aktivieren Sie CLIENT1, und melden Sie sich als corp\user1 an.  
  
2. Öffnen Sie ein Windows PowerShell-Fenster mit erhöhten Rechten, geben Sie **ipconfig/all**ein, und drücken Sie EINGABETASTE Die Ausgabe zeigt an, dass CLIENT1 über eine lokale IP-Adresse verfügt und dass kein aktiver IPv6-zu-IPv4-, Teredo-oder IP-HTTPS-Tunnel vorhanden ist.  
  
3. Testen Sie die Konnektivität mit der Netzwerkfreigabe auf APP2. Geben Sie auf dem **Start** Bildschirm<strong>\\\app2\files</strong>ein, und drücken Sie dann die EINGABETASTE. Sie können die Datei in diesem Ordner öffnen.  
  


