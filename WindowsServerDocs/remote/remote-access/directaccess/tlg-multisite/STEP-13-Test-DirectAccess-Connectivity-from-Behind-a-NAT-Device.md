---
title: Schritt 13 Test DirectAccess-Clientkonnektivität hinter einem NAT-Gerät
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 796825c3-5e3e-4745-a921-25ab90b95ede
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2d1661d43cd45614dfabc66fd9a737c55ab388ed
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446921"
---
# <a name="step-13-test-directaccess-connectivity-from-behind-a-nat-device"></a>Schritt 13 Test DirectAccess-Clientkonnektivität hinter einem NAT-Gerät

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn ein DirectAccess-Client hinter einem NAT-Gerät oder einem Webproxyserver mit dem Internet verbunden wird, verwendet der DirectAccess-Client entweder Teredo oder IP-HTTPS zur Verbindungsherstellung mit dem RAS-Server. Wenn das NAT-Gerät ausgehenden UDP-Port 3544 den RAS-Servers öffentlichen IP-Adresse aktiviert wird, wird Teredo verwendet. Wenn kein Teredo-Zugriff verfügbar ist, fällt der DirectAccess-Client auf IP-HTTPS über den ausgehenden TCP-Port 443 zurück, wodurch der Zugriff durch Firewalls oder Webproxyserver über den herkömmlichen SSL-Port ermöglicht wird. Falls eine Authentifizierung für den Webproxy erforderlich ist, wird die IP-HTTPS-Verbindung fehlschlagen. IP-HTTPS-Verbindungen schlagen auch fehl, wenn vom Webproxy eine ausgehende SSL-Prüfung durchgeführt wird, da die HTTPS-Sitzung am Webproxy anstatt am RAS-Server beendet wird.  
  
Die folgenden Verfahren werden auf beiden Clientcomputern ausgeführt:  
  
1. Testen der Teredo-Konnektivität. Der erste Satz von Tests werden ausgeführt, wenn der DirectAccess-Client für Teredo konfiguriert ist. Das ist die automatische Einstellung, wenn das NAT-Gerät ausgehenden Zugriff auf den UDP-Port 3544 ermöglicht. Zunächst führen Sie die Tests auf "client1", und anschließend führen Sie die Tests aus, klicken Sie auf CLIENT2.  
  
2. Testen Sie IP-HTTPS-Verbindung. Die zweite Gruppe von Tests werden ausgeführt, wenn der DirectAccess-Client für IP-HTTPS konfiguriert ist. Um IP-HTTPS-Konnektivität vorzuführen, wird Teredo auf den Clientcomputern deaktiviert. Zunächst führen Sie die Tests auf "client1", und anschließend führen Sie die Tests aus, klicken Sie auf CLIENT2.  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Starten Sie EDGE1 und 2-EDGE1 aus, wenn sie noch nicht ausgeführt werden, und stellen Sie sicher, dass sie mit dem Internet-Subnetz verbunden sind.  
  
Trennen Sie vor der Durchführung dieser Tests CLIENT1 und CLIENT2 aus dem Internet-Switch, und verbinden Sie sie mit dem Homenet-Switch. Wenn Sie gefragt, welche Art von Netzwerk Sie möchten das aktuelle Netzwerk definieren, wählen Sie **Heimnetzwerk**.  
  
## <a name="TeredoCLIENT1"></a>Testen der Teredo-Konnektivität  
  
1. Öffnen Sie auf CLIENT1 ein Windows PowerShell-Fenster mit erhöhten Rechten aus.  
  
2. Aktivieren der Teredo-Adapter, Typ **legen Sie Netsh Interface Teredo State Enterpriseclient**, und drücken Sie dann die EINGABETASTE.  
  
3. Geben Sie in Windows PowerShell-Fenster **Ipconfig/all** und drücken Sie EINGABETASTE.  
  
4. Prüfen Sie die Ausgabe des Befehls "ipconfig".  
  
   Dieser Computer ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Wenn sich der DirectAccess-Client hinter einem NAT-Gerät befindet und eine private IPv4-Adresse zugeordnet wurde, wird Teredo als IPv6-Übergangstechnologie bevorzugt. Wenn Sie die Ausgabe des Befehls Ipconfig betrachten, sehen Sie einen Abschnitt für Tunneladapter Teredo Tunneling Pseudo-Interface und eine Beschreibung Microsoft Teredo-Tunneling-Adapter, mit einer IP-Adresse, die mit 2001: 0 entsprechend einer Teredo beginnt Adresse. Daraufhin sollte das Standardgateway aufgelistet, die für den Teredo-Tunneladapter als "::".  
  
5. Geben Sie in Windows PowerShell-Fenster **Ipconfig/flushdns** und drücken Sie EINGABETASTE.  
  
   Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Internet verbunden wurde.  
  
6. Geben Sie in Windows PowerShell-Fenster **ping app1** und drücken Sie EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
7. Geben Sie in Windows PowerShell-Fenster **ping app2** und drücken Sie EINGABETASTE. Daraufhin sollte die Antworten von der NAT64-Adresse, die von EDGE1 zu APP2 handelt es sich in diesem Fall fd zugewiesen**C9:9f4e:eb1b**: 7777::a00:4. Beachten Sie, dass die fett formatierten Werte variieren aufgrund wie die Adresse generiert wird.  
  
8. Geben Sie in Windows PowerShell-Fenster **Pingen 2-app1** und drücken Sie EINGABETASTE. Antworten von IPv6-Adresse der 2-APP1, 2001:db8:2::3 sollte angezeigt werden.  
  
9. Öffnen Sie Internet Explorer, in der Adressleiste von Internet Explorer, geben Sie **https://2-app1/** und drücken Sie EINGABETASTE. Es wird die standardmäßige IIS-Website auf 2-APP1 angezeigt.  
  
10. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** und drücken Sie EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
11. Auf der **starten** geben<strong>\\\App2\Files</strong>, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.  
  
12. Wiederholen Sie dieses Verfahren auf CLIENT2 ein.  
  
## <a name="IPHTTPS_CLIENT1"></a>Testen Sie die IP-HTTPS-Verbindung  
  
1. Öffnen Sie auf CLIENT1 ein erhöhtes Windows PowerShell-Fenster, und geben **Netsh Interface Teredo festgelegt Zustand deaktiviert** und drücken Sie EINGABETASTE. Dadurch wird Teredo auf dem Clientcomputer deaktiviert. Der Clientcomputer kann sich nun selbst für IP-HTTPS konfigurieren. Nach Ausführung des Befehls wird die Antwort **OK** angezeigt.  
  
2. Geben Sie in Windows PowerShell-Fenster **Ipconfig/all** und drücken Sie EINGABETASTE.  
  
3. Prüfen Sie die Ausgabe des Befehls "ipconfig". Dieser Computer ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Teredo ist deaktiviert, und der DirectAccess-Client fällt auf IP-HTTPS zurück. Wenn Sie die Ausgabe des Befehls Ipconfig betrachten, sehen Sie einen Abschnitt für Tunneladapter Iphttpsinterface mit einer IP-Adresse, die mit 2001:db8:1:1000 oder mit diesem wird eine IP-HTTPS-Adresse, die basierend auf der Präfixe, die konsistent 2001:db8:2:2000 beginnt Beim Einrichten von DirectAccess konfiguriert. Sie sehen keine Standardgateway für den Tunneladapter IPHTTPSInterface aufgeführt.  
  
4. Geben Sie in Windows PowerShell-Fenster **Ipconfig/flushdns** und drücken Sie EINGABETASTE. Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Unternehmensnetzwerk verbunden war.  
  
5. Geben Sie in Windows PowerShell-Fenster **ping app1** und drücken Sie EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
6. Geben Sie in Windows PowerShell-Fenster **ping app2** und drücken Sie EINGABETASTE. Daraufhin sollte die Antworten von der NAT64-Adresse, die von EDGE1 zu APP2 handelt es sich in diesem Fall fd zugewiesen**C9:9f4e:eb1b**: 7777::a00:4. Beachten Sie, dass die fett formatierten Werte variieren aufgrund wie die Adresse generiert wird.  
  
7. Geben Sie in Windows PowerShell-Fenster **Pingen 2-app1** und drücken Sie EINGABETASTE. Antworten von IPv6-Adresse der 2-APP1, 2001:db8:2::3 sollte angezeigt werden.  
  
8. Öffnen Sie Internet Explorer, in der Adressleiste von Internet Explorer, geben Sie **https://2-app1/** und drücken Sie EINGABETASTE. Es wird die standardmäßige IIS-Website auf 2-APP1 angezeigt.  
  
9. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** und drücken Sie EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
10. Auf der **starten** geben<strong>\\\App2\Files</strong>, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.  
  
11. Wiederholen Sie dieses Verfahren auf CLIENT2 ein.  
  


