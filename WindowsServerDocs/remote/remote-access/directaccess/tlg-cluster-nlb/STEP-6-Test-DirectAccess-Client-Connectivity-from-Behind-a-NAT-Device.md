---
title: Schritt 6 Testen der DirectAccess-Client Konnektivität hinter einem NAT-Gerät
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: aded2881-99ed-4f18-868b-b765ab926597
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 93c7fba89645a22370ce294c2ce0ec220afc853a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819173"
---
# <a name="step-6-test-directaccess-client-connectivity-from-behind-a-nat-device"></a>Schritt 6 Testen der DirectAccess-Client Konnektivität hinter einem NAT-Gerät

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Wenn ein DirectAccess-Client hinter einem NAT-Gerät oder einem Webproxyserver mit dem Internet verbunden wird, verwendet der DirectAccess-Client entweder Teredo oder IP-HTTPS zur Verbindungsherstellung mit dem RAS-Server. 

Wenn das NAT-Gerät ausgehenden UDP-Port 3544 für die öffentliche IP-Adresse des RAS-Servers aktiviert, wird Teredo verwendet. Wenn kein Teredo-Zugriff verfügbar ist, fällt der DirectAccess-Client auf IP-HTTPS über den ausgehenden TCP-Port 443 zurück, wodurch der Zugriff durch Firewalls oder Webproxyserver über den herkömmlichen SSL-Port ermöglicht wird. 

Falls eine Authentifizierung für den Webproxy erforderlich ist, wird die IP-HTTPS-Verbindung fehlschlagen. IP-HTTPS-Verbindungen schlagen auch fehl, wenn vom Webproxy eine ausgehende SSL-Prüfung durchgeführt wird, da die HTTPS-Sitzung am Webproxy anstatt am RAS-Server beendet wird. In diesem Abschnitt führen Sie die gleichen Tests wie bei der Herstellung einer IP6-zu-IP4-Verbindung im vorherigen Abschnitt durch.  
  
Die folgenden Verfahren werden auf beiden Clientcomputern ausgeführt:  
  
1. Testen Sie die Teredo-Konnektivität. Der erste Satz von Tests wird ausgeführt, wenn der DirectAccess-Client für die Verwendung von Teredo konfiguriert ist. Das ist die automatische Einstellung, wenn das NAT-Gerät ausgehenden Zugriff auf den UDP-Port 3544 ermöglicht.  
  
2. Testen Sie die IP-HTTPS-Konnektivität. Die zweite Testreihe wird durchgeführt, wenn der DirectAccess-Client für die Verwendung von IP-HTTPS konfiguriert ist. Um IP-HTTPS-Konnektivität vorzuführen, wird Teredo auf den Clientcomputern deaktiviert.  
  
> [!TIP]  
> Es wird empfohlen, den Internet Explorer-Cache zu löschen, bevor Sie diese Prozeduren ausführen, um sicherzustellen, dass Sie die Verbindung testen und nicht die Website Seiten aus dem Cache abrufen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten

Vor der Durchführung dieser Tests trennen Sie CLIENT1 vom Internet-Switch, und verbinden Sie ihn mit dem Homenet-Switch. Auf die Frage hin, welche Art von Netzwerk Sie für das aktuelle Netzwerk definieren möchten, wählen Sie **Heimnetzwerk**.  
  
Starten Sie EDGE1 und EDGE2, sofern diese nicht bereits ausgeführt werden.  
  
## <a name="test-teredo-connectivity"></a>Testen der Teredo-Konnektivität  
  
1. Öffnen Sie auf CLIENT1 ein Windows PowerShell-Fenster mit erhöhten Rechten, geben Sie **ipconfig/all** ein, und drücken Sie EINGABETASTE.  
  
2. Prüfen Sie die Ausgabe des Befehls "ipconfig".  
  
   CLIENT1 ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Wenn sich der DirectAccess-Client hinter einem NAT-Gerät befindet und eine private IPv4-Adresse zugeordnet wurde, wird Teredo als IPv6-Übergangstechnologie bevorzugt. In der Ausgabe des Befehls "ipconfig" sollten ein Abschnitt für Tunneladapter Teredo Tunneling Pseudo-Interface und die Beschreibung Microsoft-Teredo-Tunneling-Adapter mit einer IP-Adresse angezeigt werden, die entsprechend einer Teredo-Adresse mit "2001:" beginnt. Wenn der Teredo-Abschnitt nicht angezeigt wird, aktivieren Sie Teredo mit dem Befehl **netsh interface Teredo set state enterpriseclient**, und wiederholen Sie anschließend den Befehl "ipconfig". Für den Teredo-Tunneladapter wird kein Standardgateway aufgeführt.  
  
3. Geben Sie im Windows PowerShell-Fenster **ipconfig/flushdns** ein, und drücken Sie die EINGABETASTE.  
  
   Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Internet verbunden wurde.  
  
4. Geben Sie im Windows PowerShell-Fenster **Get-dnsclientnrptpolicy** ein, und drücken Sie die EINGABETASTE.  
  
   In der Ausgabe werden die aktuellen Einstellungen der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) angezeigt. Diese Einstellungen weisen darauf hin, dass alle Verbindungen zu .corp.contoso.com vom Remote-Access-DNS-Server mit der IPv6-Adresse "2001:db8:1::2" aufgelöst werden sollen. Beachten Sie außerdem den NRPT-Eintrag, dass eine Ausnahme für den Namen "nls.corp.contoso.com" vorhanden ist; Namen in der Ausnahmeliste werden vom Remote-Access-DNS-Server nicht beantwortet. Sie können einen Ping-Befehl an die IP-Adresse des Remote-Access-DNS-Servers senden, um die Konnektivität zum RAS-Server zu bestätigen. In diesem Beispiel können Sie einen Ping-Befehl an "2001:db8:1::2" senden.  
  
5. Geben Sie im Windows PowerShell-Fenster **Ping App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
6. Geben Sie im Windows PowerShell-Fenster **Ping App2** ein, und drücken Sie die EINGABETASTE. Sie sollten Antworten von der NAT64-Adresse erhalten, die von EDGE1 zu APP2 zugeordnet wurde (in diesem Fall "fdc9:9f4e:eb1b:7777::a00:4").  
  
7. Lassen Sie das Windows PowerShell-Fenster für das nächste Verfahren geöffnet.  
  
8. Öffnen Sie Internet Explorer, geben Sie in der Internet Explorer-Adressleiste **https://app1/** ein, und drücken Sie die EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
9. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** ein, und drücken Sie die EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
10. Geben Sie auf dem **Start** Bildschirm<strong>\\\app2\files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.  
  
## <a name="test-ip-https-connectivity"></a>IP-HTTPS-Konnektivität testen  
  
1. Öffnen Sie ein Windows PowerShell-Fenster mit erhöhten Rechten, geben Sie **Netsh Interface Teredo Set State deaktiviert** ein, und drücken Sie EINGABETASTE Dadurch wird Teredo auf dem Clientcomputer deaktiviert. Der Clientcomputer kann sich nun selbst für IP-HTTPS konfigurieren. Nach Ausführung des Befehls wird die Antwort **OK** angezeigt.  
  
2. Geben Sie im Windows PowerShell-Fenster **ipconfig/all** ein, und drücken Sie die EINGABETASTE.  
  
3. Prüfen Sie die Ausgabe des Befehls "ipconfig". Dieser Computer ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Teredo ist deaktiviert, und der DirectAccess-Client fällt auf IP-HTTPS zurück. In der Ausgabe des Befehls "ipconfig" wird der Abschnitt Tunneladapter iphttpsinterface mit einer IP-Adresse angezeigt, die entsprechend einer IP-HTTPS-Adresse mit "2001:db8:1:100" beginnt. Grundlage hierfür ist das Präfix, das beim Einrichten von DirectAccess konfiguriert wurde. Für den IP-HTTPS-Tunneladapter wird kein Standardgateway aufgeführt.  
  
4. Geben Sie im Windows PowerShell-Fenster **ipconfig/flushdns** ein, und drücken Sie die EINGABETASTE. Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Unternehmensnetzwerk verbunden war.  
  
5. Geben Sie im Windows PowerShell-Fenster **Ping App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
6. Geben Sie im Windows PowerShell-Fenster **Ping App2** ein, und drücken Sie die EINGABETASTE. Sie sollten Antworten von der NAT64-Adresse erhalten, die von EDGE1 zu APP2 zugeordnet wurde (in diesem Fall "fdc9:9f4e:eb1b:7777::a00:4").  
  
7. Öffnen Sie Internet Explorer, geben Sie in der Internet Explorer-Adressleiste **https://app1/** ein, und drücken Sie die EINGABETASTE. Die Standard-IIS-Site auf APP1 wird angezeigt.  
  
8. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** ein, und drücken Sie die EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
9. Geben Sie auf dem **Start** Bildschirm<strong>\\\app2\files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.
