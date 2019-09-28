---
title: Schritt 12. Testen der DirectAccess-Konnektivität
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65ac1c23-3a47-4e58-888d-9dde7fba1586
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bd0f8ba10536a28479269abafadaaacaffd3d0a8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388384"
---
# <a name="step-12-test-directaccess-connectivity"></a>Schritt 12. Testen der DirectAccess-Konnektivität

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Bevor Sie die Konnektivität von Client Computern testen können, wenn Sie sich im Internet oder in homenet-Netzwerken befinden, müssen Sie sicherstellen, dass Sie über die richtigen Gruppenrichtlinien Einstellungen verfügen.  
  
- So überprüfen Sie, ob Clients die richtige Gruppenrichtlinie haben  
  
- Testen der DirectAccess-Konnektivität über das Internet über Edge1  
  
- Verschieben von CLIENT2 in die Win7_Clients_Site2-Sicherheitsgruppe  
  
- Testen der DirectAccess-Konnektivität über das Internet bis 2 Edge1  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Verbinden Sie beide Client Computer mit dem Netzwerk "Corpnet", und starten Sie beide Client Computer neu.  
  
## <a name="policy"></a>Überprüfen, ob Clients über die richtige Gruppenrichtlinie verfügen  
  
1.  Klicken Sie auf CLIENT1 auf **Start**, geben Sie **PowerShell. exe**ein, klicken Sie mit der rechten Maustaste auf **PowerShell**, klicken Sie auf **erweitert**und dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Geben Sie im Windows PowerShell-Fenster **ipconfig** ein, und drücken Sie die EINGABETASTE.  
  
    Stellen Sie sicher, dass die IPv4-Adresse des Corpnet-Adapters mit 10.0.0 beginnt.  
  
3.  Geben Sie im Windows PowerShell-Fenster **Get-dnsclientnrptpolicy** ein, und drücken Sie die EINGABETASTE. Die Einträge in der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) für Direct Access werden angezeigt.  
  
    -   . Corp.contoso.com: Diese Einstellungen geben an, dass alle Verbindungen mit Corp.contoso.com von einem der DirectAccess-DNS-Server mit der IPv6-Adresse 2001: db8:1:: 2 oder 2001: db8:2:: 20 aufgelöst werden sollten.  
  
    -   NLS.Corp.contoso.com: Diese Einstellungen geben an, dass eine Ausnahme für den Namen nls.Corp.contoso.com vorliegt.  
  
4.  Lassen Sie das Windows PowerShell-Fenster für das nächste Verfahren geöffnet.  
  
5.  Klicken Sie auf CLIENT2 auf **Start**, **Alle Programme**, **Zubehör**, **Windows PowerShell**, klicken Sie mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
6.  Geben Sie im Windows PowerShell-Fenster **ipconfig** ein, und drücken Sie die EINGABETASTE.  
  
    Stellen Sie sicher, dass die IPv4-Adresse des Corpnet-Adapters mit 10.0.0 beginnt.  
  
7.  Geben Sie im Windows PowerShell-Fenster **netsh Namespace Show Policy** ein, und drücken Sie die EINGABETASTE.  
  
    In der Ausgabe sollten zwei Abschnitte vorhanden sein:  
  
    -   . Corp.contoso.com: Diese Einstellungen geben an, dass alle Verbindungen mit Corp.contoso.com vom DirectAccess-DNS-Server mit der IPv6-Adresse "2001: db8:1:: 2" aufgelöst werden sollen.  
  
    -   NLS.Corp.contoso.com: Diese Einstellungen geben an, dass eine Ausnahme für den Namen nls.Corp.contoso.com vorliegt.  
  
8.  Lassen Sie das Windows PowerShell-Fenster für das nächste Verfahren geöffnet.  
  
## <a name="EDGE1"></a>Testen der DirectAccess-Konnektivität über das Internet über Edge1  
  
1. UnPlug 2: Edge1 aus dem Internet Netzwerk.  
  
2. Entfernen Sie CLIENT1 und CLIENT2 vom Corpnet-Switch, und verbinden Sie Sie mit dem Internet-Switch. Warten Sie 30 Sekunden.  
  
3. Geben Sie auf CLIENT1 im Windows PowerShell-Fenster **ipconfig/all** ein, und drücken Sie die EINGABETASTE.  
  
4. Überprüfen Sie die Ausgabe des Befehls "ipconfig".  
  
   Der Client Computer ist jetzt mit dem Internet verbunden und verfügt über eine öffentliche IPv4-Adresse. Wenn der DirectAccess-Client über eine öffentliche IPv4-Adresse verfügt, verwendet er die IPv6-Übergangs Technologien Teredo oder IP-HTTPS, um die IPv6-Nachrichten über ein IPv4-Internet zwischen dem DirectAccess-Client und dem Remote Zugriffs Server zu Tunneln. Beachten Sie, dass Teredo die bevorzugte Übergangstechnologie ist.  
  
5. Geben Sie im Windows PowerShell-Fenster **ipconfig/flushdns** ein, und drücken Sie die EINGABETASTE. Dadurch werden namens Auflösungs Einträge geleert, die möglicherweise noch im Client-DNS-Cache vorhanden sind, wenn der Client Computer mit dem Unternehmensnetzwerk verbunden war.  
  
6. Deaktivieren Sie die Teredo-Schnittstelle, um sicherzustellen, dass der Client Computer mit dem folgenden Befehl IP-HTTPS verwendet, um eine Verbindung mit Corpnet herzustellen:  
  
   ```  
   netsh interface teredo set state disable  
   ```  
  
7. Stellen Sie sicher, dass Sie über Edge1 verbunden sind. Geben Sie **netsh interface httpstunnel Show Interfaces Show Interfaces** ein, und drücken Sie die EINGABETASTE.  
  
   Die Ausgabe sollte URL: https://edge1.contoso.com:443/IPHTTPS enthalten.  
  
   > [!TIP]  
   > Auf CLIENT1 können Sie auch den folgenden Windows PowerShell-Befehl ausführen: **Get-matiphttpsconfiguration**. In der Ausgabe werden die verfügbaren Server-URL-Verbindungen und das derzeit aktive Profil angezeigt.  
  
8. Geben Sie im Windows PowerShell-Fenster **Ping App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse angezeigt werden, die App1 zugewiesen ist, in diesem Fall "2001: db8:1:: 3".  
  
9. Geben Sie im Windows PowerShell-Fenster **Ping 2-App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse, die 2-App1 zugewiesen ist, angezeigt werden, in diesem Fall "2001: db8:2:: 3".  
  
10. Geben Sie im Windows PowerShell-Fenster **Ping App2** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der NAT64-Adresse angezeigt werden, die von Edge1 zu APP2 zugewiesen wird. in diesem Fall lautet der Wert FD**C9:9f4e: eb1b**: 7777:: A00:4. Beachten Sie, dass die fett formatierten Werte variieren, weil die Adresse generiert wird.  
  
    Die Möglichkeit zum Ping-APP2 ist wichtig, da der Erfolg anzeigt, dass Sie eine Verbindung mithilfe von NAT64/DNS64 herstellen konnten, da APP2 eine reine IPv4-Ressource ist.  
  
11. Öffnen Sie Internet Explorer, geben Sie in der Internet Explorer-Adressleiste **https://app1/ ein** , und drücken Sie die EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
12. Geben Sie in der Internet Explorer-Adressleiste **https://2-app1/ ein** , und drücken Sie die EINGABETASTE. Die Standard Website wird unter 2-App1 angezeigt.  
  
13. Geben Sie in der Internet Explorer-Adressleiste **https://app2/ ein** , und drücken Sie die EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
14. Geben Sie auf dem **Start** Bildschirm<strong>\\ \ 2-App1\Files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die Beispiel Textdatei.  
  
    Dadurch wird veranschaulicht, dass Sie eine Verbindung mit dem Dateiserver in der corp2.Corp.contoso.com-Domäne herstellen konnten, wenn eine Verbindung über Edge1 besteht.  
  
15. Geben Sie auf dem **Start** Bildschirm<strong>\\ \ App2\Files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei.  
  
    Dies zeigt, dass Sie eine Verbindung mit einem reinen IPv4-Server herstellen konnten, indem Sie SMB zum Abrufen einer Ressource in der Ressourcen Domäne verwenden.  
  
16. Geben Sie auf dem **Start** Bildschirm**WF. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
17. Beachten Sie in der Konsole **Windows-Firewall mit** erweiterter Sicherheit, dass nur das **öffentliche Profil** aktiv ist. Die Windows-Firewall muss aktiviert sein, damit DirectAccess ordnungsgemäß funktioniert. Wenn die Windows-Firewall deaktiviert ist, funktioniert die DirectAccess-Konnektivität nicht.  
  
18. Erweitern Sie im linken Bereich der Konsole den Knoten **Überwachung** , und klicken Sie auf den Knoten **Verbindungs Sicherheitsregeln** . Die aktiven Verbindungs Sicherheitsregeln sollten angezeigt werden: **DirectAccess Policy-clientabcorp**, **DirectAccess Policy-ClientToDNS64NAT64PrefixExemption**, **DirectAccess Policy-Clientdie Infrastruktur**und **DirectAccess Policy-clienttonlaausgenommen**. Führen Sie im mittleren Bereich einen Bildlauf nach rechts durch, um die **ersten Authentifizierungsmethoden** und **2. Authentifizierungsmethoden** Spalten anzuzeigen. Beachten Sie, dass die erste Regel (clientescorp) Kerberos V5 verwendet, um den intranettunnel einzurichten, und die dritte Regel (clientesinfrastructure) verwendet NTLMv2, um den Infrastruktur Tunnel einzurichten.  
  
19. Erweitern Sie im linken Bereich der Konsole den Knoten **Sicherheits Zuordnungen** , und klicken Sie auf den Knoten **Hauptmodus** . Beachten Sie die Infrastruktur Tunnel-Sicherheits Zuordnungen mit NTLMv2 und der intranettunnel-Sicherheits Zuordnung mithilfe von Kerberos V5. Klicken Sie mit der rechten Maustaste auf den Eintrag, der **Benutzer (Kerberos V5)** als **2. Authentifizierungsmethode** anzeigt, und klicken Sie auf **Eigenschaften**. Beachten Sie, dass auf der Registerkarte **Allgemein** die **zweite lokale Authentifizierungs-ID** **corp\user1**lautet, die angibt, dass sich user1 erfolgreich bei der Corp-Domäne mithilfe von Kerberos authentifizieren konnte.  
  
20. Wiederholen Sie diesen Vorgang aus Schritt 3 auf client2.  
  
## <a name="secgroup"></a>Verschieben von CLIENT2 in die Win7_Clients_Site2-Sicherheitsgruppe  
  
1.  Klicken Sie auf DC1 auf **Start**, geben Sie **DSA. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie **Corp.contoso.com/users** in der Konsole Active Directory Benutzer und Computer, und doppelklicken Sie auf **Win7_Clients_Site1**.  
  
3.  Klicken Sie im Dialogfeld **Win7_Clients_Site1-Eigenschaften** auf die Registerkarte **Mitglieder** , klicken Sie auf **client2**, klicken Sie auf **Entfernen**, klicken Sie auf **Ja**und dann auf **OK**.  
  
4.  Doppelklicken Sie auf **Win7_Clients_Site2**, und klicken Sie dann im Dialogfeld **Win7_Clients_Site2-Eigenschaften** auf die Registerkarte **Mitglieder** .  
  
5.  Klicken Sie auf **Hinzufügen**, klicken Sie im Dialogfeld **Benutzer, Kontakte, Computer oder Dienst Konten auswählen** auf **Objekttypen**, wählen Sie **Computer**aus, und klicken Sie dann auf **OK**.  
  
6.  Geben Sie unter **Geben Sie die zu ausgewäfnenden Objektnamen ein den Namen** **client2**ein, und klicken Sie auf **OK**  
  
7.  Starten Sie CLIENT2 neu, und melden Sie sich mit dem Konto Corp/user1 an.  
  
8.  Öffnen Sie auf CLIENT2 ein Windows PowerShell-Fenster mit erhöhten Rechten, geben Sie **netsh Namespace Show Policy** ein, und drücken Sie EINGABETASTE.  
  
    In der Ausgabe sollten zwei Abschnitte vorhanden sein:  
  
    -   . Corp.contoso.com: Diese Einstellungen geben an, dass alle Verbindungen mit Corp.contoso.com vom DirectAccess-DNS-Server mit der IPv6-Adresse 2001: db8:2:: 20 aufgelöst werden sollen.  
  
    -   NLS.Corp.contoso.com: Diese Einstellungen geben an, dass eine Ausnahme für den Namen nls.Corp.contoso.com vorliegt.  
  
## <a name="DAConnect"></a>Testen der DirectAccess-Konnektivität über das Internet bis 2 Edge1  
  
1. Verbinden Sie 2 Edge1 mit dem Internet Netzwerk.  
  
2. Entfernen Sie Edge1 aus dem Internet Netzwerk.  
  
3. Öffnen Sie auf CLIENT1 ein Windows PowerShell-Fenster mit erhöhten Rechten.  
  
4. Geben Sie im Windows PowerShell-Fenster **ipconfig/flushdns** ein, und drücken Sie die EINGABETASTE. Dadurch werden namens Auflösungs Einträge geleert, die möglicherweise noch im Client-DNS-Cache vorhanden sind, wenn der Client Computer mit dem Unternehmensnetzwerk verbunden war.  
  
5. Stellen Sie sicher, dass Sie über 2-Edge1 verbunden sind. Geben Sie **netsh interface httpstunnel Show Interfaces Show Interfaces** ein, und drücken Sie die EINGABETASTE.  
  
   Die Ausgabe sollte URL: https://2-edge1.contoso.com:443/IPHTTPS enthalten.  
  
   > [!TIP]  
   > Auf CLIENT1 können Sie auch den folgenden Befehl ausführen: **Get-matiphttpsconfiguration**. In der Ausgabe werden die verfügbaren Server-URL-Verbindungen und das derzeit aktive Profil angezeigt.  
  
   > [!NOTE]  
   > CLIENT1 ändert automatisch den Server, über den die Verbindung mit Unternehmensressourcen hergestellt wird. Wenn in der Ausgabe des Befehls eine Verbindung mit Edge1 angezeigt wird, warten Sie ca. fünf Minuten, und versuchen Sie es dann erneut.  
  
6. Geben Sie im Windows PowerShell-Fenster **Ping App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse angezeigt werden, die App1 zugewiesen ist, in diesem Fall "2001: db8:1:: 3".  
  
7. Geben Sie im Windows PowerShell-Fenster **Ping 2-App1** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der IPv6-Adresse, die 2-App1 zugewiesen ist, angezeigt werden, in diesem Fall "2001: db8:2:: 3".  
  
8. Geben Sie im Windows PowerShell-Fenster **Ping App2** ein, und drücken Sie die EINGABETASTE. Es sollten Antworten von der NAT64-Adresse angezeigt werden, die von Edge1 zu APP2 zugewiesen wird. in diesem Fall lautet der Wert FD**C9:9f4e: eb1b**: 7777:: A00:4. Beachten Sie, dass die fett formatierten Werte variieren, weil die Adresse generiert wird.  
  
   Die Möglichkeit zum Ping-APP2 ist wichtig, da der Erfolg anzeigt, dass Sie eine Verbindung mithilfe von NAT64/DNS64 herstellen konnten, da APP2 eine reine IPv4-Ressource ist.  
  
9. Öffnen Sie Internet Explorer, geben Sie in der Internet Explorer-Adressleiste **https://app1/ ein** , und drücken Sie die EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
10. Geben Sie in der Internet Explorer-Adressleiste **https://2-app1/ ein** , und drücken Sie die EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
11. Geben Sie in der Internet Explorer-Adressleiste **https://app2/ ein** , und drücken Sie die EINGABETASTE. Die Standard Website wird auf APP3 angezeigt.  
  
12. Geben Sie auf dem **Start** Bildschirm<strong>\\ \ App1\Files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die Beispiel Textdatei.  
  
    Dadurch wird veranschaulicht, dass Sie eine Verbindung mit dem Dateiserver in der Corp.contoso.com-Domäne herstellen konnten, wenn eine Verbindung über 2-Edge1 besteht.  
  
13. Geben Sie auf dem **Start** Bildschirm<strong>\\ \ App2\Files</strong>ein, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei.  
  
    Dies zeigt, dass Sie eine Verbindung mit einem reinen IPv4-Server herstellen konnten, indem Sie SMB zum Abrufen einer Ressource in der Ressourcen Domäne verwenden.  
  
14. Wiederholen Sie diesen Vorgang auf CLIENT2 aus Schritt 3.  
  


