---
title: Schritt 13 Testen der DirectAccess-Konnektivität hinter einem NAT-Gerät
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 796825c3-5e3e-4745-a921-25ab90b95ede
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9422f3840899edc7dad6b51dd42a95eafb3856a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860343"
---
# <a name="step-13-test-directaccess-connectivity-from-behind-a-nat-device"></a>Schritt 13 Testen der DirectAccess-Konnektivität hinter einem NAT-Gerät

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Wenn ein DirectAccess-Client hinter einem NAT-Gerät oder einem Webproxyserver mit dem Internet verbunden wird, verwendet der DirectAccess-Client entweder Teredo oder IP-HTTPS zur Verbindungsherstellung mit dem RAS-Server. Wenn das NAT-Gerät ausgehenden UDP-Port 3544 für die öffentliche IP-Adresse des RAS-Servers aktiviert, wird Teredo verwendet. Wenn kein Teredo-Zugriff verfügbar ist, fällt der DirectAccess-Client auf IP-HTTPS über den ausgehenden TCP-Port 443 zurück, wodurch der Zugriff durch Firewalls oder Webproxyserver über den herkömmlichen SSL-Port ermöglicht wird. Falls eine Authentifizierung für den Webproxy erforderlich ist, wird die IP-HTTPS-Verbindung fehlschlagen. IP-HTTPS-Verbindungen schlagen auch fehl, wenn vom Webproxy eine ausgehende SSL-Prüfung durchgeführt wird, da die HTTPS-Sitzung am Webproxy anstatt am RAS-Server beendet wird.  
  
Die folgenden Verfahren werden auf beiden Clientcomputern ausgeführt:  
  
1. Testen Sie die Teredo-Konnektivität. Der erste Satz von Tests wird ausgeführt, wenn der DirectAccess-Client für die Verwendung von Teredo konfiguriert ist. Das ist die automatische Einstellung, wenn das NAT-Gerät ausgehenden Zugriff auf den UDP-Port 3544 ermöglicht. Führen Sie zuerst die Tests auf CLIENT1 aus, und führen Sie dann die Tests auf CLIENT2 aus.  
  
2. Testen Sie die IP-HTTPS-Konnektivität. Die zweite Testreihe wird durchgeführt, wenn der DirectAccess-Client für die Verwendung von IP-HTTPS konfiguriert ist. Um IP-HTTPS-Konnektivität vorzuführen, wird Teredo auf den Clientcomputern deaktiviert. Führen Sie zuerst die Tests auf CLIENT1 aus, und führen Sie dann die Tests auf CLIENT2 aus.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Starten Sie Edge1 und 2 Edge1, wenn Sie nicht bereits ausgeführt werden, und stellen Sie sicher, dass Sie mit dem Internet-Subnetz verbunden sind.  
  
Bevor Sie diese Tests durchführen, entfernen Sie CLIENT1 und CLIENT2 vom Internet-Switch, und verbinden Sie Sie mit dem homenet-Switch. Wenn Sie gefragt werden, welche Art von Netzwerk Sie für das aktuelle Netzwerk definieren möchten, wählen Sie **Heimnetzwerk**aus.  
  
## <a name="test-teredo-connectivity"></a><a name="TeredoCLIENT1"></a>Testen der Teredo-Konnektivität  
  
1. Öffnen Sie auf CLIENT1 ein Windows PowerShell-Fenster mit erhöhten Rechten.  
  
2. Aktivieren Sie den Teredo-Adapter, geben Sie **Netsh Interface Teredo Set State enterpriseclient**ein, und drücken Sie dann die EINGABETASTE.  
  
3. Geben Sie im Windows PowerShell-Fenster **ipconfig/all** ein, und drücken Sie die EINGABETASTE.  
  
4. Prüfen Sie die Ausgabe des Befehls "ipconfig".  
  
   Dieser Computer ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Wenn sich der DirectAccess-Client hinter einem NAT-Gerät befindet und eine private IPv4-Adresse zugeordnet wurde, wird Teredo als IPv6-Übergangstechnologie bevorzugt. Wenn Sie sich die Ausgabe des Befehls ipconfig ansehen, sollte ein Abschnitt für Tunnel Adapter Teredo Tunneling Pseudo Schnittstelle und dann eine Beschreibung für den Microsoft Teredo-Tunneling-Adapter mit einer IP-Adresse angezeigt werden, die mit 2001:0 mit einem Teredo-Wert beginnt. Adresse. Das Standard Gateway für den Teredo-Tunnel Adapter sollte als "::" aufgeführt werden.  
  
5. Geben Sie im Windows PowerShell-Fenster **ipconfig/flushdns** ein, und drücken Sie die EINGABETASTE.  
  
   Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Internet verbunden wurde.  
  
6. Geben Sie im Windows PowerShell-Fenster **Ping App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
7. Geben Sie im Windows PowerShell-Fenster **Ping App2** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der NAT64-Adresse angezeigt werden, die von Edge1 zu APP2 zugewiesen wird. in diesem Fall lautet der Wert FD**C9:9f4e: eb1b**: 7777:: A00:4. Beachten Sie, dass die fett formatierten Werte variieren, weil die Adresse generiert wird.  
  
8. Geben Sie im Windows PowerShell-Fenster **Ping 2-App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse "2-App1, 2001: db8:2:: 3" angezeigt werden.  
  
9. Öffnen Sie Internet Explorer, geben Sie in der Internet Explorer-Adressleiste **https://2-app1/** ein, und drücken Sie die EINGABETASTE. Die IIS-Standard Website wird unter 2-App1 angezeigt.  
  
10. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** ein, und drücken Sie die EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
11. Geben Sie auf dem **Start** Bildschirm<strong>\\\app2\files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.  
  
12. Wiederholen Sie diesen Vorgang auf client2.  
  
## <a name="test-ip-https-connectivity"></a><a name="IPHTTPS_CLIENT1"></a>Testen von IP-HTTPS-Konnektivität  
  
1. Öffnen Sie auf CLIENT1 ein Windows PowerShell-Fenster mit erhöhten Rechten, geben Sie **Netsh Interface Teredo Set State deaktiviert** ein, und drücken Sie die EINGABETASTE. Dadurch wird Teredo auf dem Clientcomputer deaktiviert. Der Clientcomputer kann sich nun selbst für IP-HTTPS konfigurieren. Nach Ausführung des Befehls wird die Antwort **OK** angezeigt.  
  
2. Geben Sie im Windows PowerShell-Fenster **ipconfig/all** ein, und drücken Sie die EINGABETASTE.  
  
3. Prüfen Sie die Ausgabe des Befehls "ipconfig". Dieser Computer ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Teredo ist deaktiviert, und der DirectAccess-Client fällt auf IP-HTTPS zurück. Wenn Sie sich die Ausgabe des Befehls "ipconfig" ansehen, sehen Sie einen Abschnitt für Tunnel Adapter iphttpsinterface mit einer IP-Adresse, die mit "2001: db8:1: 1000" oder "2001: db8:2: 2000" übereinstimmt. Dies ist eine IP-HTTPS-Adresse basierend auf den Präfixen, die konfiguriert beim Einrichten von DirectAccess. Für den iphttpsinterface-Tunnel Adapter wird kein Standard Gateway aufgeführt.  
  
4. Geben Sie im Windows PowerShell-Fenster **ipconfig/flushdns** ein, und drücken Sie die EINGABETASTE. Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Unternehmensnetzwerk verbunden war.  
  
5. Geben Sie im Windows PowerShell-Fenster **Ping App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
6. Geben Sie im Windows PowerShell-Fenster **Ping App2** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der NAT64-Adresse angezeigt werden, die von Edge1 zu APP2 zugewiesen wird. in diesem Fall lautet der Wert FD**C9:9f4e: eb1b**: 7777:: A00:4. Beachten Sie, dass die fett formatierten Werte variieren, weil die Adresse generiert wird.  
  
7. Geben Sie im Windows PowerShell-Fenster **Ping 2-App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse "2-App1, 2001: db8:2:: 3" angezeigt werden.  
  
8. Öffnen Sie Internet Explorer, geben Sie in der Internet Explorer-Adressleiste **https://2-app1/** ein, und drücken Sie die EINGABETASTE. Die IIS-Standard Website wird unter 2-App1 angezeigt.  
  
9. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** ein, und drücken Sie die EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
10. Geben Sie auf dem **Start** Bildschirm<strong>\\\app2\files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.  
  
11. Wiederholen Sie diesen Vorgang auf client2.  
  


