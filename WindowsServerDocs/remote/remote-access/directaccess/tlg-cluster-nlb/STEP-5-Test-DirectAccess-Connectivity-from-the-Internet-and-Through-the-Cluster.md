---
title: Schritt 5 Testen der DirectAccess-Konnektivität über das Internet und über den Cluster
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8399bdfa-809a-45e4-9963-f9b6a631007f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1b5708e51b2653444fb3eb636baac6a165dfc55d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404849"
---
# <a name="step-5-test-directaccess-connectivity-from-the-internet-and-through-the-cluster"></a>Schritt 5 Testen der DirectAccess-Konnektivität über das Internet und über den Cluster

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

CLIENT1 ist jetzt für DirectAccess-Tests bereit.  
  
- Testen Sie die DirectAccess-Konnektivität über das Internet. Verbinden Sie CLIENT1 mit dem simulierten Internet. Wenn eine Verbindung mit dem simulierten Internet besteht, werden dem Client öffentliche IPv4-Adressen zugewiesen. Wenn einem DirectAccess-Client eine öffentliche IPv4-Adresse zugewiesen wird, versucht er, mithilfe einer IPv6-Übergangstechnologie eine Verbindung mit dem RAS-Server herzustellen.  
  
- Testen Sie die DirectAccess-Client Konnektivität über den Cluster. Testen Sie die Cluster Funktionalität. Bevor Sie mit dem Testen beginnen, wird empfohlen, dass Sie für mindestens fünf Minuten sowohl Edge1 als auch EDGE2 Herunterfahren. Hierfür gibt es eine Reihe von Gründen, einschließlich ARP-Cache Timeouts und Änderungen im Zusammenhang mit NLB. Wenn Sie die NLB-Konfiguration in einer Testumgebung überprüfen, benötigen Sie einen Patienten, da Änderungen an der Konfiguration nicht sofort in der Konnektivität widergespiegelt werden, bis eine Zeitspanne verstrichen ist. Dies ist wichtig, wenn Sie die folgenden Aufgaben durchführen.  
  
    > [!TIP]  
    > Es wird empfohlen, den Internet Explorer-Cache vor dem Ausführen dieses Verfahrens zu löschen und jedes Mal, wenn Sie die Verbindung über einen anderen RAS-Server testen, um sicherzustellen, dass Sie die Verbindung testen und nicht die Webseiten aus dem Cache abrufen.  
  
## <a name="test-directaccess-connectivity-from-the-internet"></a>Testen der DirectAccess-Konnektivität über das Internet  
  
1. Entfernen Sie die CLIENT1 vom Corpnet-Switch, und verbinden Sie Sie mit dem Internet-Switch. Warten Sie 30 Sekunden.  
  
2. Geben Sie in einem Windows PowerShell-Fenster mit erhöhten Rechten **ipconfig/flushdns** ein, und drücken Sie EINGABETASTE. Dadurch werden namens Auflösungs Einträge geleert, die möglicherweise noch im Client-DNS-Cache vorhanden sind, wenn der Client Computer mit dem Unternehmensnetzwerk verbunden war.  
  
3. Geben Sie im Windows PowerShell-Fenster **Get-dnsclientnrptpolicy** ein, und drücken Sie die EINGABETASTE.  
  
   In der Ausgabe werden die aktuellen Einstellungen der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) angezeigt. Diese Einstellungen geben an, dass alle Verbindungen zu. Corp.contoso.com vom RAS-DNS-Server mit der IPv6-Adresse "2001: db8:1:: 2" aufgelöst werden sollen. Beachten Sie außerdem den NRPT-Eintrag, dass eine Ausnahme für den Namen "nls.corp.contoso.com" vorhanden ist; Namen in der Ausnahmeliste werden vom Remote-Access-DNS-Server nicht beantwortet. Sie können an die IP-Adresse des RAS-DNS-Servers pingen, um die Konnektivität zum RAS-Server zu bestätigen. Beispielsweise können Sie den Ping 2001: db8:1:: 2 ausführen.  
  
4. Geben Sie im Windows PowerShell-Fenster **Ping App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse für App1 angezeigt werden. Dies ist in diesem Fall "2001: db8:1:: 3".  
  
5. Geben Sie im Windows PowerShell-Fenster **Ping App2** ein, und drücken Sie die EINGABETASTE. Sie sollten Antworten von der NAT64-Adresse erhalten, die von EDGE1 zu APP2 zugeordnet wurde (in diesem Fall "fdc9:9f4e:eb1b:7777::a00:4").  
  
   Die Möglichkeit zum Ping-APP2 ist wichtig, da der Erfolg anzeigt, dass Sie eine Verbindung mithilfe von NAT64/DNS64 herstellen konnten, da APP2 eine reine IPv4-Ressource ist.  
  
6. Lassen Sie das Windows PowerShell-Fenster für das nächste Verfahren geöffnet.  
  
7. Öffnen Sie Internet Explorer, geben Sie in der Internet Explorer-Adressleiste **https://app1/ ein** , und drücken Sie die EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
8. Geben Sie in der Internet Explorer-Adressleiste **https://app2/ ein** , und drücken Sie die EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
9. Geben Sie auf dem **Start** Bildschirm<strong>\\ \ App2\Files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei.  
  
    Dies zeigt, dass Sie eine Verbindung mit einem reinen IPv4-Server herstellen konnten, indem Sie SMB zum Abrufen einer Ressource in der Ressourcen Domäne verwenden.  
  
10. Geben Sie auf dem **Start** Bildschirm**WF. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
11. Beachten Sie in der Konsole **Windows-Firewall mit** erweiterter Sicherheit, dass nur das **private** oder **öffentliche Profil** aktiv ist. Die Windows-Firewall muss aktiviert sein, damit DirectAccess ordnungsgemäß funktioniert. Wenn die Windows-Firewall deaktiviert ist, funktioniert die DirectAccess-Konnektivität nicht.  
  
12. Erweitern Sie im linken Bereich der Konsole den Knoten **Überwachung** , und klicken Sie auf den Knoten **Verbindungs Sicherheitsregeln** . Die aktiven Verbindungs Sicherheitsregeln sollten angezeigt werden: **DirectAccess Policy-clientabcorp**, **DirectAccess Policy-ClientToDNS64NAT64PrefixExemption**, **DirectAccess Policy-Clientdie Infrastruktur**und **DirectAccess Policy-clienttonlaausgenommen**. Führen Sie im mittleren Bereich einen Bildlauf nach rechts durch, um die **ersten Authentifizierungsmethoden** und **2. Authentifizierungsmethoden** Spalten anzuzeigen. Beachten Sie, dass die erste Regel (clientescorp) Kerberos V5 verwendet, um den intranettunnel einzurichten, und die dritte Regel (clientesinfrastructure) verwendet NTLMv2, um den Infrastruktur Tunnel einzurichten.  
  
13. Erweitern Sie im linken Bereich der Konsole den Knoten **Sicherheits Zuordnungen** , und klicken Sie auf den Knoten **Hauptmodus** . Beachten Sie die Infrastruktur Tunnel-Sicherheits Zuordnungen mit NTLMv2 und der intranettunnel-Sicherheits Zuordnung mithilfe von Kerberos V5. Klicken Sie mit der rechten Maustaste auf den Eintrag, der **Benutzer (Kerberos V5)** als **2. Authentifizierungsmethode** anzeigt, und klicken Sie auf **Eigenschaften**. Beachten Sie, dass auf der Registerkarte **Allgemein** die **zweite lokale Authentifizierungs-ID** **corp\user1**lautet, die angibt, dass sich user1 erfolgreich bei der Corp-Domäne mithilfe von Kerberos authentifizieren konnte.  
  
## <a name="test-directaccess-client-connectivity-through-the-cluster"></a>Testen der DirectAccess-Client Konnektivität über den Cluster  
  
1. Führen Sie ein ordnungsgemäßes Herunterfahren auf EDGE2 aus.  
  
   Sie können den Netzwerk Lastenausgleich-Manager verwenden, um beim Ausführen dieser Tests den Status der Server anzuzeigen.  
  
2. Geben Sie auf CLIENT1 im Windows PowerShell-Fenster **ipconfig/flushdns** ein, und drücken Sie die EINGABETASTE. Dadurch werden namens Auflösungs Einträge geleert, die möglicherweise noch im Client-DNS-Cache vorhanden sind.  
  
3. Pingen Sie im Windows PowerShell-Fenster den Befehl App1 und APP2. Sie sollten Antworten von diesen beiden Ressourcen erhalten.  
  
4. Geben Sie auf dem **Start** Bildschirm<strong>\\ \ app2\files</strong>ein. Der Ordner "freigegeben" sollte auf dem Computer "APP2" angezeigt werden. Die Möglichkeit zum Öffnen der Dateifreigabe auf APP2 gibt an, dass der zweite Tunnel, der die Kerberos-Authentifizierung für den Benutzer erfordert, ordnungsgemäß funktioniert.  
  
5. Öffnen Sie Internet Explorer, und öffnen Sie dann die Websites https://app1/ und https://app2/. Die Möglichkeit, beide Websites zu öffnen, bestätigt, dass der erste und der zweite Tunnel aktiv sind und funktionsfähig sind. Schließen Sie Internet Explorer.  
  
6. Starten Sie den EDGE2-Computer.  
  
7. Auf Edge1 führen Sie ein ordnungsgemäßes Herunterfahren aus.  
  
8. Warten Sie fünf Minuten, und kehren Sie dann zu CLIENT1 zurück. Führen Sie die Schritte 2-5 aus. Dadurch wird bestätigt, dass CLIENT1 transparent ein Failover zu EDGE2 ausführen konnte, nachdem Edge1 nicht mehr zur Verfügung stand.
