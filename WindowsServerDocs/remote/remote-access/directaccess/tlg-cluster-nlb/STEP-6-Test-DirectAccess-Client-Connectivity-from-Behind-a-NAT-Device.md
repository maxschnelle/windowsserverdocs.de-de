---
title: Schritt 6 Test DirectAccess-Clientkonnektivität hinter einem NAT-Gerät
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: Vorführen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aded2881-99ed-4f18-868b-b765ab926597
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d61bf2ec9abb6d54617f624f26680263d761e5b6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446081"
---
# <a name="step-6-test-directaccess-client-connectivity-from-behind-a-nat-device"></a>Schritt 6 Test DirectAccess-Clientkonnektivität hinter einem NAT-Gerät

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn ein DirectAccess-Client hinter einem NAT-Gerät oder einem Webproxyserver mit dem Internet verbunden wird, verwendet der DirectAccess-Client entweder Teredo oder IP-HTTPS zur Verbindungsherstellung mit dem RAS-Server. 

Wenn das NAT-Gerät ausgehenden UDP-Port 3544 den RAS-Servers öffentlichen IP-Adresse aktiviert wird, wird Teredo verwendet. Wenn kein Teredo-Zugriff verfügbar ist, fällt der DirectAccess-Client auf IP-HTTPS über den ausgehenden TCP-Port 443 zurück, wodurch der Zugriff durch Firewalls oder Webproxyserver über den herkömmlichen SSL-Port ermöglicht wird. 

Falls eine Authentifizierung für den Webproxy erforderlich ist, wird die IP-HTTPS-Verbindung fehlschlagen. IP-HTTPS-Verbindungen schlagen auch fehl, wenn vom Webproxy eine ausgehende SSL-Prüfung durchgeführt wird, da die HTTPS-Sitzung am Webproxy anstatt am RAS-Server beendet wird. In diesem Abschnitt führen Sie die gleichen Tests wie bei der Herstellung einer IP6-zu-IP4-Verbindung im vorherigen Abschnitt durch.  
  
Die folgenden Verfahren werden auf beiden Clientcomputern ausgeführt:  
  
1. Testen der Teredo-Konnektivität. Der erste Satz von Tests werden ausgeführt, wenn der DirectAccess-Client für Teredo konfiguriert ist. Das ist die automatische Einstellung, wenn das NAT-Gerät ausgehenden Zugriff auf den UDP-Port 3544 ermöglicht.  
  
2. Testen Sie IP-HTTPS-Verbindung. Die zweite Gruppe von Tests werden ausgeführt, wenn der DirectAccess-Client für IP-HTTPS konfiguriert ist. Um IP-HTTPS-Konnektivität vorzuführen, wird Teredo auf den Clientcomputern deaktiviert.  
  
> [!TIP]  
> Es wird empfohlen, dass Sie den Internet Explorer-Cache löschen, vor der Durchführung dieser Schritte, um sicherzustellen, dass Sie die Verbindung getestet werden und nicht die Webseiten aus dem Cache abgerufen.  
  
## <a name="prerequisites"></a>Vorraussetzungen

Vor der Durchführung dieser Tests trennen Sie CLIENT1 vom Internet-Switch, und verbinden Sie ihn mit dem Homenet-Switch. Auf die Frage hin, welche Art von Netzwerk Sie für das aktuelle Netzwerk definieren möchten, wählen Sie **Heimnetzwerk**.  
  
Starten Sie EDGE1 und EDGE2, sofern diese nicht bereits ausgeführt werden.  
  
## <a name="test-teredo-connectivity"></a>Testen der Teredo-Konnektivität  
  
1. Öffnen Sie auf CLIENT1 ein Windows PowerShell-Fenster mit erhöhten Rechten, geben **Ipconfig/all** und drücken Sie EINGABETASTE.  
  
2. Prüfen Sie die Ausgabe des Befehls "ipconfig".  
  
   CLIENT1 ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Wenn sich der DirectAccess-Client hinter einem NAT-Gerät befindet und eine private IPv4-Adresse zugeordnet wurde, wird Teredo als IPv6-Übergangstechnologie bevorzugt. Wenn Sie sich die Ausgabe des Befehls Ipconfig ansehen, sollten Sie sehen, dass einen Abschnitt für Tunneladapter Teredo Tunneling Pseudo-Interface, und klicken Sie dann eine Beschreibung Microsoft Teredo-Tunneling-Adapter, mit einer IP-Adresse, die mit 2001 beginnt: entsprechend einer Teredo Adresse. Wenn der Teredo-Abschnitt nicht angezeigt wird, aktivieren Sie Teredo mit dem Befehl **netsh interface Teredo set state enterpriseclient**, und wiederholen Sie anschließend den Befehl "ipconfig". Für den Teredo-Tunneladapter wird kein Standardgateway aufgeführt.  
  
3. Geben Sie in Windows PowerShell-Fenster **Ipconfig/flushdns** und drücken Sie EINGABETASTE.  
  
   Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Internet verbunden wurde.  
  
4. Geben Sie in Windows PowerShell-Fenster **Get-DnsClientNrptPolicy** und drücken Sie EINGABETASTE.  
  
   In der Ausgabe werden die aktuellen Einstellungen der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) angezeigt. Diese Einstellungen weisen darauf hin, dass alle Verbindungen zu .corp.contoso.com vom Remote-Access-DNS-Server mit der IPv6-Adresse "2001:db8:1::2" aufgelöst werden sollen. Beachten Sie außerdem den NRPT-Eintrag, dass eine Ausnahme für den Namen "nls.corp.contoso.com" vorhanden ist; Namen in der Ausnahmeliste werden vom Remote-Access-DNS-Server nicht beantwortet. Sie können einen Ping-Befehl an die IP-Adresse des Remote-Access-DNS-Servers senden, um die Konnektivität zum RAS-Server zu bestätigen. In diesem Beispiel können Sie einen Ping-Befehl an "2001:db8:1::2" senden.  
  
5. Geben Sie in Windows PowerShell-Fenster **ping app1** und drücken Sie EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
6. Geben Sie in Windows PowerShell-Fenster **ping app2** und drücken Sie EINGABETASTE. Sie sollten Antworten von der NAT64-Adresse erhalten, die von EDGE1 zu APP2 zugeordnet wurde (in diesem Fall "fdc9:9f4e:eb1b:7777::a00:4").  
  
7. Lassen Sie das Windows PowerShell-Fenster für den nächsten Vorgang geöffnet.  
  
8. Öffnen Sie Internet Explorer, in der Adressleiste von Internet Explorer, geben Sie **https://app1/** und drücken Sie EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
9. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** und drücken Sie EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
10. Auf der **starten** geben<strong>\\\App2\Files</strong>, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.  
  
## <a name="test-ip-https-connectivity"></a>IP-HTTPS-Konnektivität testen  
  
1. Öffnen Sie ein Windows PowerShell-Fenster mit erhöhten Rechten, geben **Netsh Interface Teredo festgelegt Zustand deaktiviert** und drücken Sie EINGABETASTE. Dadurch wird Teredo auf dem Clientcomputer deaktiviert. Der Clientcomputer kann sich nun selbst für IP-HTTPS konfigurieren. Nach Ausführung des Befehls wird die Antwort **OK** angezeigt.  
  
2. Geben Sie in Windows PowerShell-Fenster **Ipconfig/all** und drücken Sie EINGABETASTE.  
  
3. Prüfen Sie die Ausgabe des Befehls "ipconfig". Dieser Computer ist jetzt hinter einem NAT-Gerät mit dem Internet verbunden und hat eine private IPv4-Adresse erhalten. Teredo ist deaktiviert, und der DirectAccess-Client fällt auf IP-HTTPS zurück. Wenn Sie die Ausgabe des Befehls Ipconfig betrachten, sehen Sie einen Abschnitt für Tunneladapter Iphttpsinterface mit einer IP-Adresse, die mit 2001:db8:1:100 dabei wird eine IP-HTTPS-Adresse, die basierend auf dem Präfix, das konfiguriert wurde, beim Einrichten, konsistent beginnt DirectAccess. Für den IP-HTTPS-Tunneladapter wird kein Standardgateway aufgeführt.  
  
4. Geben Sie in Windows PowerShell-Fenster **Ipconfig/flushdns** und drücken Sie EINGABETASTE. Dadurch werden Namensauflösungseinträge geleert, die eventuell noch im Client-DNS-Cache vorhanden sind, seitdem der Clientcomputer mit dem Unternehmensnetzwerk verbunden war.  
  
5. Geben Sie in Windows PowerShell-Fenster **ping app1** und drücken Sie EINGABETASTE. Es sollten Antworten von der IPv6-Adresse von APP1 "2001:db8:1::3" angezeigt werden.  
  
6. Geben Sie in Windows PowerShell-Fenster **ping app2** und drücken Sie EINGABETASTE. Sie sollten Antworten von der NAT64-Adresse erhalten, die von EDGE1 zu APP2 zugeordnet wurde (in diesem Fall "fdc9:9f4e:eb1b:7777::a00:4").  
  
7. Öffnen Sie Internet Explorer, in der Adressleiste von Internet Explorer, geben Sie **https://app1/** und drücken Sie EINGABETASTE. Die Standard-IIS-Site auf APP1 wird angezeigt.  
  
8. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** und drücken Sie EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
9. Auf der **starten** geben<strong>\\\App2\Files</strong>, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei. Dadurch wird bewiesen, dass Sie eine Verbindung zu einem reinen IPv4-Server herstellen konnten, indem Sie mit SMB eine Ressource auf einem reinen IPv4-Host abgerufen haben.
