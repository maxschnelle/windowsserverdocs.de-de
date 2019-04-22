---
title: Schritt 5 Test DirectAccess-Konnektivität über das Internet und durch den Cluster
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
ms.assetid: 8399bdfa-809a-45e4-9963-f9b6a631007f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 49b3f6f68bf30ff197b51643f9f1b8f36cc76f19
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825971"
---
# <a name="step-5-test-directaccess-connectivity-from-the-internet-and-through-the-cluster"></a>Schritt 5 Test DirectAccess-Konnektivität über das Internet und durch den Cluster

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

"Client1" ist jetzt für DirectAccess-Tests bereit.  
  
- Testen der DirectAccess-Konnektivität aus dem Internet. Verbinden Sie CLIENT1 mit dem simulierten Internet. Wenn mit dem simulierten Internet verbunden ist, wird der Client eine öffentliche IPv4-Adressen zugewiesen. Wenn ein DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wird, versucht, eine Verbindung mit eine IPv6-übergangstechnologie verwenden RAS-Server herzustellen.  
  
- Testen der DirectAccess-Clientkonnektivität über den Cluster. Testen Sie die Funktionen des Clusters. Bevor Sie mit dem Testen beginnen, empfehlen wir, dass Sie sowohl EDGE1 und EDGE2 für mindestens fünf Minuten einstellen. Es gibt zahlreiche Gründe, die ARP-Cache-Timeouts und Änderungen in Bezug auf NLB enthalten. Wenn NLB-Konfiguration in einer testumgebung überprüfen möchten, müssen Sie Patienten, die Änderungen in der Konfiguration nicht sofort Konnektivität bis wiedergegeben werden, nachdem eine bestimmte Zeitspanne verstrichen ist. Dies ist wichtig zu bedenken, wenn Sie die folgenden Aufgaben ausführen.  
  
    > [!TIP]  
    > Es wird empfohlen, dass Sie Internet Explorer-Cache löschen, bevor Sie dieses Verfahren durchführen, und jedes Mal Sie die Verbindung über einen anderen RAS-Server testen, um sicherzustellen, dass Sie die Verbindung testen und nicht die Webseiten aus dem Cache abgerufen.  
  
## <a name="test-directaccess-connectivity-from-the-internet"></a>Testen der DirectAccess-Konnektivität über das Internet  
  
1.  Trennen Sie CLIENT1 aus dem Corpnet-Switch, und verbinden Sie es mit dem Internet-Switch. Warten Sie 30 Sekunden.  
  
2.  Geben Sie in einer Windows PowerShell-Fenster mit erhöhten Rechten, **Ipconfig/flushdns** und drücken Sie EINGABETASTE. Dies leert Name Resolution-Einträge, die noch im Cache DNS-Client auftreten können, wenn der Clientcomputer mit dem Unternehmensnetzwerk verbunden war.  
  
3.  Geben Sie in Windows PowerShell-Fenster **Get-DnsClientNrptPolicy** und drücken Sie EINGABETASTE.  
  
    In der Ausgabe werden die aktuellen Einstellungen der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) angezeigt. Diese Einstellungen weisen darauf hin, die alle Verbindungen zu. "corp.contoso.com" durch den Remote-Access-DNS-Server, mit der IPv6-Adresse 2001:db8:1::2 gelöst werden sollen. Beachten Sie außerdem den NRPT-Eintrag, dass eine Ausnahme für den Namen "nls.corp.contoso.com" vorhanden ist; Namen in der Ausnahmeliste werden vom Remote-Access-DNS-Server nicht beantwortet. Sie können die Remote Access-DNS-Server IP-Adresse, um zu überprüfen, ob Konnektivität zum RAS-Server pingen. Sie können z. B. 2001:db8:1::2 pingen.  
  
4.  Geben Sie in Windows PowerShell-Fenster **ping app1** und drücken Sie EINGABETASTE. Sie sollten finden Sie Antworten von der IPv6-Adresse für APP1, das in diesem Fall 2001:db8:1::3.  
  
5.  Geben Sie in Windows PowerShell-Fenster **ping app2** und drücken Sie EINGABETASTE. Sie sollten Antworten von der NAT64-Adresse erhalten, die von EDGE1 zu APP2 zugeordnet wurde (in diesem Fall "fdc9:9f4e:eb1b:7777::a00:4").  
  
    Die Möglichkeit, ping APP2 ist wichtig, da der Vorgang erfolgreich war, dass Sie eine Verbindung mithilfe von NAT64/DNS64 verwendet werden, herstellen, da APP2 eine einzige IPv4-Ressourcen ist konnten.  
  
6.  Lassen Sie das Windows PowerShell-Fenster für den nächsten Vorgang geöffnet.  
  
7.  Öffnen Sie Internet Explorer, in der Adressleiste von Internet Explorer, geben Sie **https://app1/** und drücken Sie EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
8.  Geben Sie in der Internet Explorer-Adressleiste **https://app2/** und drücken Sie EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
9. Auf der **starten** geben**\\\App2\Files**, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei.  
  
    Dies zeigt, dass Sie die Verbindung mit einem reinen IPv4-Server mit SMB zum Abrufen einer Ressource in der Ressourcendomäne konnten.  
  
10. Auf der **starten** geben**wf.msc**, und drücken Sie dann die EINGABETASTE.  
  
11. In der **Windows-Firewall mit erweiterter Sicherheit** -Konsole, beachten Sie, dass nur die **Private** oder **öffentliches Profil** aktiv ist. Die Windows-Firewall muss aktiviert sein, für DirectAccess ordnungsgemäß funktioniert. Wenn die Windows-Firewall deaktiviert ist, funktioniert die DirectAccess-Konnektivität nicht.  
  
12. Erweitern Sie im linken Bereich der Konsole die **Überwachung** Knoten, und klicken Sie auf die **Verbindungssicherheitsregeln** Knoten. Die aktiven Verbindungssicherheitsregeln sollte angezeigt werden: **DirectAccess Policy-ClientToCorp**, **DirectAccess Policy-ClientToDNS64NAT64PrefixExemption**, **DirectAccess Policy-ClientToInfra**, und **DirectAccess Policy-ClientToNlaExempt-**. Scrollen Sie im mittleren Bereich nach rechts, um das Anzeigen der **1. Authentifizierungsmethoden** und **2. Authentifizierungsmethoden** Spalten. Beachten Sie, dass die erste Regel (ClientToCorp) Kerberos V5 verwendet, um den intranettunnel einzurichten und die dritte Regel (ClientToInfra) verwendet NTLMv2, um den infrastrukturtunnel herzustellen.  
  
13. Erweitern Sie im linken Bereich der Konsole die **Sicherheitszuordnungen** Knoten, und klicken Sie auf die **Hauptmodus** Knoten. Beachten Sie die Infrastruktur-Tunnel-sicherheitszuordnungen NTLMv2 verwenden und die sicherheitszuordnung der Intranet-Tunnel mit Kerberos V5. Mit der rechten Maustaste in des Eintrags, der zeigt, **Benutzer (Kerberos V5)** als die **2. Authentifizierungsmethode** , und klicken Sie auf **Eigenschaften**. Auf der **allgemeine** Registerkarte, beachten Sie, dass die **zweite Authentifizierung lokale ID** ist **"corp\user1"**, gibt an, dass "user1" für die CORP-Domäne mit authentifiziert werden konnte Kerberos.  
  
## <a name="test-directaccess-client-connectivity-through-the-cluster"></a>Testen der DirectAccess-Clientkonnektivität im Cluster  
  
1.  Führen Sie ein ordnungsgemäßes Herunterfahren auf EDGE2 an.  
  
    Sie können den Netzwerklastenausgleich-Manager verwenden, um den Status der Server anzuzeigen, beim Ausführen dieser Tests.  
  
2.  Geben Sie auf CLIENT1 in Windows PowerShell-Fenster **Ipconfig/flushdns** und drücken Sie EINGABETASTE. Dies leert Name Resolution-Einträge, die eventuell noch im Client-DNS-Cache vorhanden sind.  
  
3.  Pingen Sie im Windows PowerShell-Fenster APP1 und APP2 aus. Sie sollten Antworten von beide Ressourcen erhalten.  
  
4.  Auf der **starten** geben**\\\app2\files**. Den freigegebenen Ordner sollte auf dem APP2-Computer angezeigt werden. Die Möglichkeit, öffnen die Dateifreigabe auf APP2 gibt an, dass der zweite Tunnel, der Kerberos-Authentifizierung für den Benutzer erforderlich ist, ordnungsgemäß funktioniert.  
  
5.  Öffnen Sie Internet Explorer, und öffnen Sie dann auf die Websites https://app1/ und https://app2/. Die Möglichkeit, beide Websites öffnen wird bestätigt, dass die erste und zweite Tunnel betriebsbereit sind und funktionieren. Schließen Sie Internet Explorer.  
  
6.  Starten Sie den EDGE2-Computer.  
  
7.  Führen Sie auf EDGE1 ein ordnungsgemäßes Herunterfahren.  
  
8.  Warten Sie 5 Minuten, und klicken Sie dann auf "client1" zurückgegeben. Führen Sie die Schritte 2 bis 5. Dadurch wird bestätigt, dass "client1" konnte für das transparente EDGE2 Failover nach EDGE1 nicht mehr verfügbar war.
