---
title: Schritt 12 Test DirectAccess-Konnektivität
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
ms.assetid: 65ac1c23-3a47-4e58-888d-9dde7fba1586
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 767d9e0760f29023aaf049ad108792f17dac309f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856961"
---
# <a name="step-12-test-directaccess-connectivity"></a>Schritt 12 Test DirectAccess-Konnektivität

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bevor Sie sie befinden sich die Internet- oder Homenet Netzwerke Verbindungen von den Clientcomputern testen können, müssen Sie sicherstellen, dass sie die richtigen gruppenrichtlinieneinstellungen verfügen.  
  
- Um zu überprüfen, ist die Richtlinie für die richtige Gruppe über Clients verfügen.  
  
- Testen der DirectAccess-Konnektivität aus dem Internet über EDGE1  
  
- Verschieben von CLIENT2 die Win7_Clients_Site2-Sicherheitsgruppe  
  
- Testen der DirectAccess-Konnektivität über das Internet über 2-EDGE1  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Verbinden Sie beide Clientcomputer mit dem Corpnet-Netzwerk, und wiederholen Sie die beiden Clientcomputern ausgeführt werden.  
  
## <a name="policy"></a>Stellen Sie sicher, dass Clients die Richtlinie für die richtige Gruppe können  
  
1.  Klicken Sie auf CLIENT1 auf **starten**, Typ **powershell.exe**, mit der rechten Maustaste **Powershell**, klicken Sie auf **erweitert**, und klicken Sie dann auf **Als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Geben Sie in Windows PowerShell-Fenster **Ipconfig** und drücken Sie EINGABETASTE.  
  
    Stellen Sie sicher, dass die "Corpnet" Adapter IPv4-Adresse mit 10.0.0 beginnt.  
  
3.  In den Typ der Windows PowerShell-Fenster **Get-DnsClientNrptPolicy** und drücken Sie EINGABETASTE. Die Einträge in der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) für Direct Access werden angezeigt.  
  
    -   . "corp.contoso.com": Diese Einstellungen weisen darauf hin, dass alle Verbindungen auf "corp.contoso.com" von einem der DirectAccess DNS-Server, mit der IPv6-Adresse 2001:db8:1::2 oder 2001:db8:2::20 gelöst werden sollen.  
  
    -   Diese NLS.corp.contoso.com Einstellungen anzugeben, dass eine Ausnahme für der Name nls.corp.contoso.com.  
  
4.  Lassen Sie das Windows PowerShell-Fenster für den nächsten Vorgang geöffnet.  
  
5.  Klicken Sie auf CLIENT2 **starten**, klicken Sie auf **Programme**, klicken Sie auf **Zubehör**, klicken Sie auf **Windows PowerShell**, mit der rechten Maustaste **Windows PowerShell**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
6.  Geben Sie in Windows PowerShell-Fenster **Ipconfig** und drücken Sie EINGABETASTE.  
  
    Stellen Sie sicher, dass die "Corpnet" Adapter IPv4-Adresse mit 10.0.0 beginnt.  
  
7.  Geben Sie in Windows PowerShell-Fenster **Netsh Namespace anzeigen Richtlinie** und drücken Sie EINGABETASTE.  
  
    In der Ausgabe muss zwei Abschnitte:  
  
    -   . "corp.contoso.com": Diese Einstellungen weisen darauf hin, dass alle Verbindungen auf "corp.contoso.com" von dem DirectAccess-DNS-Server mit der IPv6-Adresse 2001:db8:1::2 aufgelöst werden sollten.  
  
    -   Diese NLS.corp.contoso.com Einstellungen anzugeben, dass eine Ausnahme für der Name nls.corp.contoso.com.  
  
8.  Lassen Sie das Windows PowerShell-Fenster für den nächsten Vorgang geöffnet.  
  
## <a name="EDGE1"></a>Testen der DirectAccess-Konnektivität aus dem Internet über EDGE1  
  
1.  Trennen Sie 2-EDGE1 über das Internet-Netzwerk aus.  
  
2.  Trennen Sie CLIENT1 und CLIENT2 aus dem Corpnet-Switch, und verbinden Sie sie mit dem Internet-Switch. Warten Sie 30 Sekunden.  
  
3.  Geben Sie auf CLIENT1 in Windows PowerShell-Fenster **Ipconfig/all** und drücken Sie EINGABETASTE.  
  
4.  Überprüfen Sie die Ausgabe des Befehls Ipconfig.  
  
    Der Clientcomputer ist jetzt mit dem Internet verbunden und besitzt eine öffentliche IPv4-Adresse. Wenn der DirectAccess-Client eine öffentliche IPv4-Adresse verfügt, wird die Teredo oder IP-HTTPS-IPv6-übergangstechnologien zum Tunneln von IPv6-Nachrichten über ein IPv4-Internet zwischen dem DirectAccess-Clients und RAS-Server. Beachten Sie, dass die Teredo-übergangstechnologie die bevorzugte ist.  
  
5.  Geben Sie in Windows PowerShell-Fenster **Ipconfig/flushdns** und drücken Sie EINGABETASTE. Dies leert Name Resolution-Einträge, die noch im Cache DNS-Client auftreten können, wenn der Clientcomputer mit dem Unternehmensnetzwerk verbunden war.  
  
6.  Deaktivieren Sie die Teredo-Schnittstelle, um sicherzustellen, dass der Clientcomputer IP-HTTPS verwendet, für die Verbindung zum Unternehmensnetzwerk mit dem folgenden Befehl ein:  
  
    ```  
    netsh interface teredo set state disable  
    ```  
  
7.  Stellen Sie sicher, dass Sie über EDGE1 verbunden sind. Typ **Netsh Interface Httpstunnel Schnittstellen anzeigen** und drücken Sie EINGABETASTE.  
  
    Die Ausgabe sollte die URL enthält: https://edge1.contoso.com:443/IPHTTPS.  
  
    > [!TIP]  
    > Klicken Sie auf "client1" können Sie auch den folgenden Windows PowerShell-Befehl ausführen: **Get-NetIPHTTPSConfiguration**. Die Ausgabe zeigt die verfügbaren Server-URL-Verbindungen und das aktive Profil.  
  
8.  Geben Sie in Windows PowerShell-Fenster **ping app1** und drücken Sie EINGABETASTE. Antworten von der IPv6-Adresse, die auf dem App1-Computer zu zugewiesen, wobei es sich in diesem Fall um den 2001:db8:1::3 sollte angezeigt werden.  
  
9. Geben Sie in Windows PowerShell-Fenster **Pingen 2-app1** und drücken Sie EINGABETASTE. Antworten von der IPv6-Adresse zugewiesen, 2-APP1, d.h. in diesem Fall 2001:db8:2::3 sollte angezeigt werden.  
  
10. Geben Sie in Windows PowerShell-Fenster **ping app2** und drücken Sie EINGABETASTE. Daraufhin sollte die Antworten von der NAT64-Adresse, die von EDGE1 zu APP2 handelt es sich in diesem Fall fd zugewiesen**C9:9f4e:eb1b**: 7777::a00:4. Beachten Sie, dass die fett formatierten Werte variieren aufgrund wie die Adresse generiert wird.  
  
    Die Möglichkeit, ping APP2 ist wichtig, da der Vorgang erfolgreich war, dass Sie eine Verbindung mithilfe von NAT64/DNS64 verwendet werden, herstellen, da APP2 eine einzige IPv4-Ressourcen ist konnten.  
  
11. Öffnen Sie Internet Explorer, in der Adressleiste von Internet Explorer, geben Sie **https://app1/** und drücken Sie EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
12. Geben Sie in der Internet Explorer-Adressleiste **https://2-app1/** und drücken Sie EINGABETASTE. Es wird die Standardwebsite auf 2-APP1 angezeigt.  
  
13. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** und drücken Sie EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
14. Auf der **starten** geben**\\\2-App1\Files**, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die Beispiel-Textdatei.  
  
    Dies zeigt, dass Sie bei der Herstellung einer Verbindung mit dem Dateiserver in der Domäne corp2.corp.contoso.com, wenn Sie über EDGE1 verbunden waren.  
  
15. Auf der **starten** geben**\\\App2\Files**, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei.  
  
    Dies zeigt, dass Sie die Verbindung mit einem reinen IPv4-Server mit SMB zum Abrufen einer Ressource in der Ressourcendomäne konnten.  
  
16. Auf der **starten** geben**wf.msc**, und drücken Sie dann die EINGABETASTE.  
  
17. In der **Windows-Firewall mit erweiterter Sicherheit** -Konsole, beachten Sie, dass nur die **öffentliches Profil** aktiv ist. Die Windows-Firewall muss aktiviert sein, für DirectAccess ordnungsgemäß funktioniert. Wenn die Windows-Firewall deaktiviert ist, funktioniert die DirectAccess-Konnektivität nicht.  
  
18. Erweitern Sie im linken Bereich der Konsole die **Überwachung** Knoten, und klicken Sie auf die **Verbindungssicherheitsregeln** Knoten. Die aktiven Verbindungssicherheitsregeln sollte angezeigt werden: **DirectAccess Policy-ClientToCorp**, **DirectAccess Policy-ClientToDNS64NAT64PrefixExemption**, **DirectAccess Policy-ClientToInfra**, und **DirectAccess Policy-ClientToNlaExempt-**. Scrollen Sie im mittleren Bereich nach rechts, um das Anzeigen der **1. Authentifizierungsmethoden** und **2. Authentifizierungsmethoden** Spalten. Beachten Sie, dass die erste Regel (ClientToCorp) Kerberos V5 verwendet, um den intranettunnel einzurichten und die dritte Regel (ClientToInfra) verwendet NTLMv2, um den infrastrukturtunnel herzustellen.  
  
19. Erweitern Sie im linken Bereich der Konsole die **Sicherheitszuordnungen** Knoten, und klicken Sie auf die **Hauptmodus** Knoten. Beachten Sie die Infrastruktur-Tunnel-sicherheitszuordnungen NTLMv2 verwenden und die sicherheitszuordnung der Intranet-Tunnel mit Kerberos V5. Mit der rechten Maustaste in des Eintrags, der zeigt, **Benutzer (Kerberos V5)** als die **2. Authentifizierungsmethode** , und klicken Sie auf **Eigenschaften**. Auf der **allgemeine** Registerkarte, beachten Sie, dass die **zweite Authentifizierung lokale ID** ist **"corp\user1"**, gibt an, dass "user1" für die CORP-Domäne mit authentifiziert werden konnte Kerberos.  
  
20. Wiederholen Sie diesen Vorgang aus Schritt 3 auf CLIENT2 ein.  
  
## <a name="secgroup"></a>Verschieben von CLIENT2 die Win7_Clients_Site2-Sicherheitsgruppe  
  
1.  Klicken Sie auf DC1 auf **starten**, Typ **dsa.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie in der Konsole Active Directory-Benutzer und-Computer **corp.contoso.com/Users** und doppelklicken Sie auf **Win7_Clients_Site1**.  
  
3.  Auf der **Win7_Clients_Site1 Eigenschaften** Dialogfeld klicken Sie auf der **Mitglieder** auf **CLIENT2**, klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie dann auf **OK**.  
  
4.  Doppelklicken Sie auf **Win7_Clients_Site2**, und klicken Sie dann auf die **Win7_Clients_Site2 Eigenschaften** Dialogfeld klicken Sie auf der **Mitglieder** Registerkarte.  
  
5.  Klicken Sie auf **hinzufügen**, und klicken Sie auf die **Auswahl von Benutzern, Kontakten, Computern oder Dienstkonten** Dialogfeld klicken Sie auf **Objekttypen**Option **Computer**, und klicken Sie dann auf **OK**.  
  
6.  In **Geben Sie die zu verwendenden Objektnamen**, Typ **CLIENT2**, und klicken Sie dann auf **OK**.  
  
7.  Starten von CLIENT2 aus, und melden Sie sich mit dem Konto corp / "user1".  
  
8.  Öffnen Sie auf CLIENT2 ein Windows PowerShell-Fenster mit erhöhten Rechten, geben **Netsh Namespace anzeigen Richtlinie** und drücken Sie EINGABETASTE.  
  
    In der Ausgabe muss zwei Abschnitte:  
  
    -   . "corp.contoso.com": Diese Einstellungen weisen darauf hin, dass alle Verbindungen auf "corp.contoso.com" von dem DirectAccess-DNS-Server mit der IPv6-Adresse 2001:db8:2::20 aufgelöst werden sollten.  
  
    -   Diese NLS.corp.contoso.com Einstellungen anzugeben, dass eine Ausnahme für der Name nls.corp.contoso.com.  
  
## <a name="DAConnect"></a>Testen der DirectAccess-Konnektivität über das Internet über 2-EDGE1  
  
1.  Verbinden Sie 2-EDGE1 mit dem Internet-Netzwerk.  
  
2.  Trennen Sie EDGE1 über das Internet-Netzwerk ein.  
  
3.  Öffnen Sie auf CLIENT1 ein Windows PowerShell-Fenster mit erhöhten Rechten aus.  
  
4.  Geben Sie in Windows PowerShell-Fenster **Ipconfig/flushdns** und drücken Sie EINGABETASTE. Dies leert Name Resolution-Einträge, die noch im Cache DNS-Client auftreten können, wenn der Clientcomputer mit dem Unternehmensnetzwerk verbunden war.  
  
5.  Stellen Sie sicher, dass Sie über 2-EDGE1 verbunden sind. Typ **Netsh Interface Httpstunnel Schnittstellen anzeigen** und drücken Sie EINGABETASTE.  
  
    Die Ausgabe sollte die URL enthält: https://2-edge1.contoso.com:443/IPHTTPS.  
  
    > [!TIP]  
    > Klicken Sie auf "client1" können Sie auch den folgenden Befehl ausführen: **Get-NetIPHTTPSConfiguration**. Die Ausgabe zeigt die verfügbaren Server-URL-Verbindungen und das aktive Profil.  
  
    > [!NOTE]  
    > "Client1" ändert sich automatisch auf den Server, die über dem Unternehmensressourcen Verbindung aus. Wenn die Ausgabe des Befehls eine Verbindung zum EDGE1 angezeigt wird, warten Sie etwa fünf Minuten und versuchen Sie es dann erneut.  
  
6.  Geben Sie in Windows PowerShell-Fenster **ping app1** und drücken Sie EINGABETASTE. Antworten von der IPv6-Adresse, die auf dem App1-Computer zu zugewiesen, wobei es sich in diesem Fall um den 2001:db8:1::3 sollte angezeigt werden.  
  
7.  Geben Sie in Windows PowerShell-Fenster **Pingen 2-app1** und drücken Sie EINGABETASTE. Antworten von der IPv6-Adresse zugewiesen, 2-APP1, d.h. in diesem Fall 2001:db8:2::3 sollte angezeigt werden.  
  
8.  Geben Sie in Windows PowerShell-Fenster **ping app2** und drücken Sie EINGABETASTE. Daraufhin sollte die Antworten von der NAT64-Adresse, die von EDGE1 zu APP2 handelt es sich in diesem Fall fd zugewiesen**C9:9f4e:eb1b**: 7777::a00:4. Beachten Sie, dass die fett formatierten Werte variieren aufgrund wie die Adresse generiert wird.  
  
    Die Möglichkeit, ping APP2 ist wichtig, da der Vorgang erfolgreich war, dass Sie eine Verbindung mithilfe von NAT64/DNS64 verwendet werden, herstellen, da APP2 eine einzige IPv4-Ressourcen ist konnten.  
  
9. Öffnen Sie Internet Explorer, in der Adressleiste von Internet Explorer, geben Sie **https://app1/** und drücken Sie EINGABETASTE. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
10. Geben Sie in der Internet Explorer-Adressleiste **https://2-app1/** und drücken Sie EINGABETASTE. Die Standardwebsite auf APP2 wird angezeigt.  
  
11. Geben Sie in der Internet Explorer-Adressleiste **https://app2/** und drücken Sie EINGABETASTE. Es wird die Standardwebsite auf APP3 angezeigt.  
  
12. Auf der **starten** geben**\\\App1\Files**, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die Beispiel-Textdatei.  
  
    Dies zeigt, dass Sie bei der Herstellung einer Verbindung mit dem Dateiserver in der Domäne "corp.contoso.com", wenn Sie über ein 2-EDGE1 verbunden waren.  
  
13. Auf der **starten** geben**\\\App2\Files**, und drücken Sie dann die EINGABETASTE. Doppelklicken Sie auf die neue Textdokumentdatei.  
  
    Dies zeigt, dass Sie die Verbindung mit einem reinen IPv4-Server mit SMB zum Abrufen einer Ressource in der Ressourcendomäne konnten.  
  
14. Wiederholen Sie dieses Verfahren auf CLIENT2 aus Schritt 3 ein.  
  


