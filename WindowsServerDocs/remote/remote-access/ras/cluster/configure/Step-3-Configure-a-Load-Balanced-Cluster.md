---
title: Schritt 3 Konfigurieren Sie einen Cluster mit Lastenausgleich
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f000066e-7cf8-4085-82a3-4f4fe1cb3c5c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f835e27a80e661ff1f066af4779bd7c033cddc99
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446622"
---
# <a name="step-3-configure-a-load-balanced-cluster"></a>Schritt 3 Konfigurieren Sie einen Cluster mit Lastenausgleich

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nach dem Vorbereiten der Server für den Cluster, den Lastenausgleich auf die einzelnen Server zu konfigurieren, konfigurieren Sie die erforderlichen Zertifikate und Bereitstellung des Clusters.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[3.1 Konfigurieren Sie 3.1 das IPv6-Präfix](#BKMK_Prefix)|Ist die unternehmensumgebung IPv4 und IPv6, oder auf reines IPv6, auf dem einzelnen RAS-Server, sicherstellen, dass das IPv6-Präfix, das DirectAccess-Clientcomputer zugewiesen groß genug für alle Server in Ihrem Cluster behandelt wird.|  
|[3.2 Aktivieren des Lastenausgleichs](#BKMK_NLB)|Aktivieren Sie den Lastenausgleich für den RAS-Servers ein.|  
|[3.3 installieren Sie 3.3 das IP-HTTPS-Zertifikat](#BKMK_InstallIPHTTP)|Jeder Server im Cluster erfordert ein Serverzertifikat für IP-HTTPS-Verbindung zu authentifizieren.  Exportieren Sie des IP-HTTPS-Zertifikats aus der RAS-Servers und stellen Sie es auf jedem Server, die Sie dem Cluster hinzufügen möchten. Dies ist erforderlich, nur, wenn nicht selbst signierten Zertifikaten zu verwenden.|  
|[3.4 installieren Sie 3.4 das Zertifikat des Netzwerkadressenservers](#BKMK_NLS)|Wenn die einzelne Server den Netzwerkadressenserver, die lokal bereitgestellt hat, müssen Sie die Netzwerkadressenserver-Zertifikat auf jedem Server im Cluster bereitstellen. Wenn der Netzwerkadressenserver auf einem externen Server gehostet wird, ist ein Zertifikat auf jedem Server nicht erforderlich. Dies ist erforderlich, nur, wenn nicht selbst signierten Zertifikaten zu verwenden.|  
|[3.5 Server mit dem Cluster hinzufügen](#BKMK_Add)|Fügen Sie alle Server mit dem Cluster hinzu. Remote-Zugriff muss nicht konfiguriert werden, auf den Servern hinzugefügt werden.|  
|[3.6 Entfernen eines Servers aus dem cluster](#BKMK_remove)|Anweisungen zum Entfernen eines Servers aus dem Cluster.|  
|[3.7 Lastenausgleich deaktivieren](#BKBK_disable)|Anweisungen zum Deaktivieren des Lastenausgleichs.|  
  
> [!NOTE]  
> Die IP-Adresse, die für die DIP-Adresse ausgewählt ist, darf nicht auf die Netzwerkadapter der erste RAS-Servers im Cluster sein. Der DirectAccess-Bereitstellung mit VIP und DIP-Adresse hinzugefügt, die auf den Netzwerkadapter ab, führt zu Fehler.  
  
> [!NOTE]  
> Stellen Sie sicher, dass keine DIP-Adresse verwenden, die bereits auf einem anderen Computer im Netzwerk vorhanden ist.  
  
## <a name="BKMK_Prefix"></a>3.1 Konfigurieren Sie 3.1 das IPv6-Präfix  
  
### <a name="configDA"></a>So konfigurieren Sie das Präfix  
  
1.  Klicken Sie auf dem RAS-Server, auf **starten**, und klicken Sie dann auf **Remotezugriffsverwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**.  
  
3.  Im mittleren Bereich der Konsole in der **Schritt 2-DirectAccess-Server** Bereich, klicken Sie auf **bearbeiten**.  
  
4.  Klicken Sie auf **Präfixkonfiguration**. Auf der **Präfixkonfiguration** auf der Seite **IPv6-Präfix, die DirectAccess-Clientcomputer zugewiesen**, geben Sie das IPv6-Präfix zum DirectAccess-Clientcomputer mit der Länge Subnetz 59, z. B. **2001:db8:1:1000:: / 59**. Wenn VPN auch mit IPv6 aktiviert wurden, klicken Sie dann ein IPv6-Präfix angezeigt werden sollen, und die Länge des Subnetz bis 59 geändert werden muss. Klicken Sie auf **Weiter**.  
  
5.  Klicken Sie im mittleren Bereich der Konsole auf **Fertig stellen**.  
  
6.  Auf der **Remote Zugriffsüberprüfung** (Dialogfeld), überprüfen Sie die Konfigurationseinstellungen, und klicken Sie dann auf **übernehmen**. Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.  
  
## <a name="BKMK_NLB"></a>3.2 Aktivieren des Lastenausgleichs  
  
#### <a name="to-enable-load-balancing"></a>Aktivierung des Lastenausgleichs  
  
1.  Klicken Sie auf dem konfigurierten DirectAccess-Server auf **starten**, und klicken Sie dann auf **Remotezugriffsverwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole, klicken Sie im linken Bereich auf **Konfiguration**, und klicken Sie dann in der **Aufgaben** Bereich, klicken Sie auf **Lastenausgleich aktivieren**.  
  
3.  Klicken Sie in der Load Balancing Assistent zum Aktivieren, auf **Weiter**.  
  
4.  Je nachdem was Sie ausgewählt haben, bei der Planung der Schritte aus:  
  
    1.  Windows NLB: Auf der **Load Balancing-Methode** auf **verwenden Windows Network Load Balancing (NLB)** , und klicken Sie dann auf **Weiter**.  
  
    2.  Externer Load Balancer: Auf der **Load Balancing-Methode** auf **Verwenden eines externen Lastenausgleichs**, und klicken Sie dann auf **Weiter**.  
  
5.  In einer einzigen Netzwerk-Adapter-Bereitstellung auf die **dedizierte IP-Adressen** Seite gehen Sie folgendermaßen vor, und klicken Sie dann auf **Weiter**:  
  
    1.  In der **IPv4-Adresse** Feld Geben Sie die neue IPv4-Adresse für diesen Server Remotezugriff auf; die aktuellen IPv4-Adresse ist die virtuelle IP-Adresse (VIP) des Clusters mit Lastenausgleich. In der **Subnetzmaske** Geben Sie die Subnetzmaske ein.  
  
    2.  Ist die unternehmensumgebung systemeigene IPv6-Adresse, klicken Sie dann in der **IPv6-Adresse** Feld Geben Sie die neue IPv6-Adresse für diesen Server Remotezugriff auf; die aktuellen IPv6-Adresse ist die VIP-Adresse des Clusters mit Lastenausgleich. In der **Subnetzpräfixlänge** Geben Sie die Länge des Subnetzpräfixes.  
  
6.  In ein Netzwerk-Adapter-Bereitstellung auf die **externen dedizierte IP-Adressen** Seite gehen Sie folgendermaßen vor, und klicken Sie dann auf **Weiter**:  
  
    1.  In der **IPv4-Adresse** Feld Geben Sie die neue externe IPv4-Adresse für diesen Server Remotezugriff auf; die aktuellen IPv4-Adresse ist die virtuelle IP-Adresse (VIP) der Lastenausgleich-cluster. In der **Subnetzmaske** Geben Sie die Subnetzmaske ein.  
  
    2.  Wenn es derzeit systemeigene IPv6-Adressen, die auf dem Internet verbundenen Netzwerkadapter der RAS-Server, konfiguriert werden gibt, der **IPv6-Adresse** Geben Sie die neue externe IPv6-Adresse für den diese Remotezugriff auf Server; die aktuellen IPv6- Adresse wird die VIP-Adresse des NLB-Cluster. In der **Subnetzpräfixlänge** Geben Sie die Länge des Subnetzpräfixes.  
  
7.  In ein Netzwerk-Adapter-Bereitstellung auf die **internen dedizierte IP-Adressen** Seite gehen Sie folgendermaßen vor, und klicken Sie dann auf **Weiter**:  
  
    1.  In der **IPv4-Adresse** Feld Geben Sie die neue interne IPv4-Adresse für diesen Server Remotezugriff auf; die aktuellen IPv4-Adresse ist die VIP der Lastenausgleich-cluster. In der **Subnetzmaske** Geben Sie die Subnetzmaske ein.  
  
    2.  Ist die unternehmensumgebung systemeigene IPv6-Adresse, klicken Sie dann in der **IPv6-Adresse** Feld Geben Sie die neue internen IPv6-Adresse für diesen Server Remotezugriff auf; die aktuellen IPv6-Adresse ist die VIP der Lastenausgleich-cluster. In der **Subnetzpräfixlänge** Geben Sie die Länge des Subnetzpräfixes.  
  
8.  Auf der **Zusammenfassung** auf **Commit**.  
  
9. Auf der **Lastenausgleich aktivieren** Dialogfeld klicken Sie auf **schließen**.  
  
10. Klicken Sie in der Load Balancing Assistent zum Aktivieren, auf **schließen**.  
  
    > [!NOTE]  
    > Wenn der externe Lastenausgleich verwendet wird, beachten Sie die virtuelle IP-Adressen, und geben Sie sie auf die externen Load balancer.  
  
![Windows PowerShell](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Wenn Sie Windows NLB in die Planungsschritte verwenden möchten, führen Sie Folgendes:  
  
```  
Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress "2.1.1.20/255.255.255.0" -InternalDedicatedIPAddress @("10.1.1.30/255.255.255.0","3ffe::20/64") -InternetVirtualIPAddress @("2.1.1.1/255.255.255.0","2.1.1.2/255.255.255.0") -InternalVirtualIPAddress @("10.1.1.2/255.255.255.0","3ffe::2/64")  
```  
  
Wenn Sie einen Load Balancer in die Planungsschritte verwenden: Führen Sie Folgendes aus:  
  
```  
Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress "2.1.1.20/255.255.255.0" -InternalDedicatedIPAddress @("10.1.1.30/255.255.255.0","3ffe::20/64") -UseThirdPrtyLoadBalancer  
```  
  
> [!NOTE]  
> Es wird empfohlen, Änderungen an Einstellungen für die Load Balancer mit Änderungen an alle anderen Einstellungen, nicht eingeschlossen werden sollen, wenn Sie bereitstellungs-GPOs verwenden. Alle Änderungen an Einstellungen für Load Balancer müssen zuerst angewendet werden, und klicken Sie dann die andere konfigurationsänderungen vorgenommen werden sollten. Auch nach dem Konfigurieren der Load Balancer auf einem neuen DirectAccess-Server, warten Sie einige Zeit, bis die IP-Änderungen angewendet und für die DNS-Server im Unternehmen repliziert werden, bevor Sie andere DirectAccess-Einstellungen im Zusammenhang mit dem neuen Cluster ändern.  
  
## <a name="BKMK_InstallIPHTTP"></a>3.3 installieren Sie 3.3 das IP-HTTPS-Zertifikat  
Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft.  
  
### <a name="IPHTTPSCert"></a>So installieren Sie die IP-HTTPS-Zertifikats  
  
1.  Klicken Sie auf die konfigurierten RAS-Server auf **starten**, Typ **Mmc** und drücken Sie EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Auf der **hinzufügen oder Entfernen von-Snap-ins** Dialogfeld klicken Sie auf **Zertifikate**, klicken Sie auf **hinzufügen**, klicken Sie auf **Computerkonto**, klicken Sie auf  **Nächste**, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Navigieren Sie im linken Bereich der Konsole zu **Zertifikate (lokaler Computer) \Personal\Certificates**. Mit der rechten Maustaste in die IP-HTTPS-Zertifikat, zeigen Sie auf **alle Aufgaben** , und klicken Sie auf **exportieren**.  
  
5.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Privaten Schlüssel exportieren** auf **Ja, privaten Schlüssel exportieren**, und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Exportdateiformat** auf **privater Informationsaustausch – PKCS #12 (. PFX)** , und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Sicherheit** Seite die **Kennwort** Kontrollkästchen, geben Sie ein Kennwort in die **Kennwort** und bestätigen Sie das Kennwort, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **zu exportierende Datei** Seite Geben Sie einen Namen für die Zertifikatdatei, und speichern Sie es auf dem Desktop, und klicken Sie dann auf **Weiter**.  
  
10. Klicken Sie auf der Seite **Fertigstellen des Assistenten** auf **Fertig stellen**.  
  
11. Auf der **Zertifikatexport-Assistenten** Dialogfeld klicken Sie auf **OK**.  
  
12. Kopieren Sie das Zertifikat auf allen Servern, die Clustermitglieder sein sollen.  
  
13. Klicken Sie auf dem neuen DirectAccess-Server, auf **starten**, Typ **Mmc** und drücken Sie EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
14. Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
15. Auf der **hinzufügen oder Entfernen von-Snap-ins** Dialogfeld klicken Sie auf **Zertifikate**, klicken Sie auf **hinzufügen**, klicken Sie auf **Computerkonto**, klicken Sie auf  **Nächste**, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
16. Navigieren Sie im linken Bereich der Konsole zu **Zertifikate (lokaler Computer) \Personal\Certificates**. Klicken Sie mit der rechten Maustaste auf die **Zertifikate** Knoten, zeigen Sie auf **alle Aufgaben**, und klicken Sie dann auf **Import**.  
  
17. Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
18. Auf der **zu importierende Datei** auf **Durchsuchen** um das Zertifikat zu suchen. Wählen Sie das Zertifikat, und klicken Sie dann auf **Weiter**.  
  
19. Auf der **Schlüsselschutz** auf der Seite die **Kennwort** , geben Sie das Kennwort, und klicken Sie dann auf **Weiter**.  
  
20. Klicken Sie auf der Seite **Zertifikatspeicher** auf **Weiter**.  
  
21. Klicken Sie auf der Seite **Fertigstellen des Assistenten** auf **Fertig stellen**.  
  
22. Auf der **Zertifikatimport-Assistenten** Dialogfeld klicken Sie auf **OK**.  
  
23. Wiederholen Sie die Schritte 13 bis 22 für alle Server, die Clustermitglieder sein sollen.  
  
## <a name="BKMK_NLS"></a>3.4 installieren Sie 3.4 das Zertifikat des Netzwerkadressenservers  
Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft.  
  
#### <a name="to-install-a-certificate-for-network-location"></a>Zum Installieren eines Zertifikats für Netzwerkadressen  
  
1.  Klicken Sie auf dem RAS-Server, auf **starten**, Typ **Mmc**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie im Menü **Datei** auf **Snap-Ins hinzufügen bzw. entfernen**.  
  
3.  Klicken Sie auf **Zertifikate**, klicken Sie auf **hinzufügen**, klicken Sie auf **Computerkonto**, klicken Sie auf **Weiter**, klicken Sie auf **lokalen Computer**, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Auf der **Zertifikate anfordern** Seite, klicken Sie auf dem Webserver-Zertifikatvorlage und klicken Sie dann auf **zusätzliche Informationen für diese zertifikatsregistrierung benötigt**.  
  
    Wenn der Webserver-Zertifikatvorlage nicht angezeigt wird, stellen Sie sicher, dass das Computerkonto des RAS-Server verfügt über Berechtigungen für die Webserver-Zertifikatvorlage registrieren. Weitere Informationen finden Sie unter [Konfigurieren von Berechtigungen für die Webserver-Zertifikatvorlage](https://msdn.microsoft.com/library/ee649249.aspx).  
  
8.  Auf der **Betreff** auf der Registerkarte die **Zertifikateigenschaften** Dialogfeld **Antragstellername**, für **Typ**Option **allgemeine Namen**.  
  
9. In **Wert**, geben Sie den vollqualifizierten Domänennamen (FQDN) für den Intranetnamen, der die Netzwerkadressenserver-Website (z. B. nls.corp.contoso.com), und klicken Sie dann auf **hinzufügen**.  
  
10. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
11. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, dass ein neues Zertifikat mit dem vollqualifizierten Domänennamen unter **Serverauthentifizierung** mit der Option **Beabsichtigte Zwecke** registriert wurde.  
  
12. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und klicken Sie anschließend auf **Eigenschaften**.  
  
13. Geben Sie unter **Anzeigenamen** den Namen **Netzwerkadressenzertifikat** ein, und klicken Sie dann auf **OK**.  
  
    > [!TIP]  
    > Die Schritte 12 und 13 sind optional, aber es erleichtern Ihnen die Auswahl des Zertifikats für Netzwerkadressen beim Konfigurieren des Remotezugriffs.  
  
14. Wiederholen Sie dieses Verfahren auf allen Servern, die Clustermitglieder sein sollen.  
  
## <a name="BKMK_Add"></a>3.5 Server mit dem Cluster hinzufügen  
 
  
#### <a name="to-add-servers-to-the-cluster"></a>Zum Hinzufügen von Servern mit dem cluster  
  
1.  Klicken Sie auf dem konfigurierten DirectAccess-Server auf **starten**, und klicken Sie dann auf **Remotezugriffsverwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. In der **Aufgaben** Bereich unter **Load Balanced Cluster**, klicken Sie auf **hinzufügen oder Entfernen von Servern**.  
  
3.  Auf der **hinzufügen oder Entfernen von Servern** Dialogfeld klicken Sie auf **-Server hinzufügen**.  
  
4.  Auf der **Hinzufügen eines Servers** Dialogfeld auf die **Server auswählen** Seite Geben Sie den Namen der zusätzlichen RAS-Server, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Netzwerkadapter** Seite, gehen Sie wie im folgenden:  
  
    -   Wenn Sie eine Topologie mit zwei Netzwerkadaptern, in bereitstellen **externen Adapter**, wählen Sie den Adapter, der mit dem externen Netzwerk verbunden ist. In **des internen Adapters**, wählen Sie den Adapter, der mit dem internen Netzwerk verbunden ist.  
  
    -   Wenn Sie eine Topologie mit einem Netzwerkadapter im Bereitstellen **Netzwerkadapter**, wählen Sie den Adapter, der mit dem internen Netzwerk verbunden ist.  
  
6.  Auf der **Netzwerkadapter** auf der Seite **wählen Sie das Zertifikat zum Authentifizieren von IP-HTTPS-Verbindungen**, klicken Sie auf **Durchsuchen** zu suchen, und wählen Sie das IP-HTTPS-Zertifikat und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Netzwerkadressenserver** auf **Durchsuchen** wählen Sie das Zertifikat für die Netzwerkadressenserver-Website auf dem RAS-Server ausgeführt, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > Die **Netzwerkadressenserver** Seite angezeigt wird, nur, wenn die Netzwerkadressenserver-Website auf dem RAS-Server ausgeführt wird.  
  
    > [!NOTE]  
    > Wenn VPN auch auf dem RAS-Server konfiguriert wurden, würden Sie aufgefordert, die der VPN IP-Pool Adressinformationen an diesem Punkt hinzufügen.  
  
8.  Auf der **Zusammenfassung** auf **hinzufügen**.  
  
9. Klicken Sie auf der Seite **Abschluss des Vorgangs** auf **Schließen**.  
  
10. Wiederholen Sie diese Schritte für alle RAS-Server, auf dem Cluster hinzugefügt werden.  
  
11. Auf der **hinzufügen oder Entfernen von Servern** Dialogfeld klicken Sie auf **Commit**.  
  
12. Auf der **hinzufügen und Entfernen von Servern** Dialogfeld klicken Sie auf **schließen**.  
  
![Windows PowerShell](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Add-RemoteAccessLoadBalancerNode -RemoteAccessServer <server name>  
```  
  
> [!NOTE]  
> Wenn VPN in einem Cluster der Load-balanced nicht aktiviert wurde, sollten Sie keine VPN-Adressbereiche bereitstellen, wenn Sie einen neuen Server mithilfe von Windows PowerShell-Cmdlets mit dem Cluster hinzufügen. Wenn Sie versehentlich getan haben, entfernen Sie den Server aus dem Cluster, und fügen Sie es erneut zum Cluster hinzu, ohne die VPN-Adressbereiche.  
  
## <a name="BKMK_remove"></a>3.6 Entfernen eines Servers aus dem cluster  
 
  
#### <a name="to-remove-a-server-from-the-cluster"></a>Entfernen eines Servers aus dem cluster  
  
1.  Klicken Sie auf die konfigurierten RAS-Server auf **starten**, und klicken Sie dann auf **Remotezugriffsverwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. In der **Aufgaben** Bereich unter **Load Balanced Cluster**, klicken Sie auf **hinzufügen oder Entfernen von Servern**.  
  
3.  Auf der **hinzufügen oder Entfernen von Servern** Dialogfeld, wählen Sie die RAS-Server, die Sie entfernen möchten, und klicken Sie dann auf **Server entfernen**.  
  
4.  Auf der **Entfernen von Server-Warnung** im Dialogfeld stellen Sie sicher, dass Sie den richtigen Server auswählen, und klicken Sie dann auf **OK**.  
  
5.  Wiederholen Sie diese Schritte für alle RAS-Server aus dem Cluster entfernt werden soll.  
  
6.  Auf der **hinzufügen oder Entfernen von Servern** Dialogfeld klicken Sie auf **Commit**.  
  
7.  Auf der **hinzufügen und Entfernen von Servern** Dialogfeld klicken Sie auf **schließen**.  
  
![Windows PowerShell](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Remove-RemoteAccessLoadBalancerNode -RemoteAccessServer <server name>  
```  
  
## <a name="BKBK_disable"></a>3.7 Lastenausgleich deaktivieren  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell](assetId:///7a817ca0-2b4a-4476-9d28-9a63ff2453f9)  
  
#### <a name="to-disable-load-balancing"></a>So deaktivieren Sie den Lastenausgleich  
  
1.  Klicken Sie auf dem konfigurierten DirectAccess-Server auf **starten**, und klicken Sie dann auf **Remotezugriffsverwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. In der **Aufgaben** Bereich unter **Load Balanced Cluster**, klicken Sie auf **Lastenausgleich deaktivieren**.  
  
3.  Auf der **Lastenausgleich deaktivieren** Dialogfeld klicken Sie auf **Ok**.  
  
4.  Auf der **Lastenausgleich deaktivieren** Dialogfeld klicken Sie auf **schließen**.  
  
![Windows PowerShell](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
set-RemoteAccessLoadBalancer -disable  
```  
  
Deaktivieren des Lastenausgleichs entfernt Remotezugriffseinstellungen und NLB-Einstellungen (sofern konfiguriert) von allen Servern mit Ausnahme der von dem er ausgeführt wird. Klicken Sie auf dem RAS-Server NLB-Einstellungen (sofern sie konfiguriert wurde) werden entfernt, aber Remotezugriffseinstellungen bleibt.  
  
Auf **Konfigurationseinstellungen entfernen** entfernt Remotezugriff und NLB (sofern konfiguriert) von allen Servern in der Bereitstellung.  
  
> [!NOTE]  
> -   Wenn Remotezugriff deinstalliert wird, wenn Lastenausgleich bereitgestellt wird, bleiben alle Server mit DIPs. VIPs werden entfernt. Dadurch werden alle Routen im Unternehmensnetzwerk, die für die VIPs Adressen nicht bestimmt werden. Dies wirkt sich auch auf DNS-Einträge in der virtuellen IP-Adressen, z. B. der Network Location Serverzertifikat-Antragstellername aufgelöst wurden. Um dieses Problem zu vermeiden, deaktivieren Sie den Lastenausgleich, belässt die virtuellen IP-Adressen auf dem letzten RAS-Server, und deinstallieren Sie den Remotezugriff.  
> -   Nach der Verwendung der **Set-RemoteAccessLoadBalancer** -Cmdlet zum Deaktivieren des Lastenausgleichs, warten Sie, bis 2 Minuten, bevor Sie ein weiteres Cmdlets ausführen. Dies sollte auch in Skripts, die ein anderes Cmdlet ausgeführt wird, nachdem erfolgen die **Set-RemoteAccessLoadBalancer-deaktivieren** Cmdlet.  
> -   Änderungen für den Lastenausgleich für die virtuelle IP-Adresse des Clusters in eine dedizierte IP-Adresse wird deaktiviert. Jeder Vorgang, der für den Namen des Servers Abfragen schlägt daher fehl, bis zum Ablauf des zwischengespeicherten DNS-Eintrags auf dem Server. Stellen Sie sicher, dass Sie keine Remotezugriffs-PowerShell-Cmdlets ausgeführt werden, nach dem Deaktivieren des Lastenausgleichs, bis der Cache auf dem Server abgelaufen ist. Dieses Problem ist eher üblich, wenn Sie versuchen, deaktivieren den Lastenausgleich für einen Computer von einem anderen Computer, der in einer anderen Domäne befindet. Dies tritt auf, wenn Sie einen Lastenausgleich des aus der Remotezugriffs-Verwaltungskonsole zu deaktivieren und verhindern, die Konfiguration geladen dass können. Die Konfiguration wird geladen, nachdem der Cache abgelaufen ist oder geleert wurden wurde.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 4: Überprüfen den cluster](Step-4-Verify-the-Cluster.md)  
  


