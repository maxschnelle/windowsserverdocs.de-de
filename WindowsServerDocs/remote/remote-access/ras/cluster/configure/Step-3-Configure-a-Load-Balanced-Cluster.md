---
title: 'Schritt 3: Konfigurieren eines Clusters mit Lastenausgleich'
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f000066e-7cf8-4085-82a3-4f4fe1cb3c5c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 19a87762e19dd763376f50c7c5b04da3f2187874
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308355"
---
# <a name="step-3-configure-a-load-balanced-cluster"></a>Schritt 3: Konfigurieren eines Clusters mit Lastenausgleich

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Nachdem Sie die Server für den Cluster vorbereitet haben, konfigurieren Sie den Lastenausgleich auf dem einzelnen Server, konfigurieren Sie die erforderlichen Zertifikate, und stellen Sie den Cluster bereit.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[3,1 Konfigurieren des IPv6-Präfixes](#BKMK_Prefix)|Wenn die Unternehmensumgebung IPv4 + IPv6 oder nur IPv6 ist, stellen Sie auf dem einzelnen RAS-Server sicher, dass das IPv6-Präfix, das DirectAccess-Client Computern zugewiesen ist, groß genug ist, um alle Server im Cluster abzudecken.|  
|[3,2 Aktivieren des Lasten Ausgleichs](#BKMK_NLB)|Aktivieren Sie den Lastenausgleich auf dem einzelnen Remote Zugriffs Server.|  
|[3,3 Installieren des IP-HTTPS-Zertifikats](#BKMK_InstallIPHTTP)|Jeder Server im Cluster erfordert ein Serverzertifikat zur Authentifizierung der IP-HTTPS-Verbindung.  Exportieren Sie das IP-HTTPS-Zertifikat vom einzelnen RAS-Server, und stellen Sie es auf jedem Server bereit, den Sie dem Cluster hinzufügen. Dies ist nur erforderlich, wenn nicht selbst signierte Zertifikate verwendet werden.|  
|[3,4 Installieren des Netzwerkadressen Server-Zertifikats](#BKMK_NLS)|Wenn der Netzwerkadressen Server auf dem einzelnen Server lokal bereitgestellt wird, müssen Sie das Netzwerkadressen Server-Zertifikat auf jedem Server im Cluster bereitstellen. Wenn der Netzwerkadressen Server auf einem externen Server gehostet wird, ist ein Zertifikat auf jedem Server nicht erforderlich. Dies ist nur erforderlich, wenn nicht selbst signierte Zertifikate verwendet werden.|  
|[3,5 Hinzufügen von Servern zum Cluster](#BKMK_Add)|Fügen Sie alle Server zum Cluster hinzu. Der Remote Zugriff darf auf den Servern, die hinzugefügt werden sollen, nicht konfiguriert werden.|  
|[3,6 Entfernen eines Servers aus dem Cluster](#BKMK_remove)|Anweisungen zum Entfernen eines Servers aus dem Cluster.|  
|[3,7 Deaktivieren des Lasten Ausgleichs](#BKBK_disable)|Anweisungen zum Deaktivieren des Lasten Ausgleichs.|  
  
> [!NOTE]  
> Die für die DIP-Adresse ausgewählte IP-Adresse darf nicht auf den Netzwerkadaptern des ersten Remote Zugriffs Servers im Cluster verwendet werden. Das Starten der DirectAccess-Bereitstellung mit VIP und DIP, die dem Netzwerkadapter hinzugefügt werden, führt zu einem Fehler.  
  
> [!NOTE]  
> Stellen Sie sicher, dass Sie keine DIP verwenden, die bereits auf einem anderen Computer im Netzwerk vorhanden ist.  
  
## <a name="31-configure-the-ipv6-prefix"></a><a name="BKMK_Prefix"></a>3,1 Konfigurieren des IPv6-Präfixes  
  
### <a name="to-configure-the-prefix"></a><a name="configDA"></a>So konfigurieren Sie das Präfix  
  
1.  Klicken Sie auf dem Remote Zugriffs Server auf **Start**, und klicken Sie dann auf **Remote Zugriffs Verwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**.  
  
3.  Klicken Sie im mittleren Bereich der Konsole im Bereich **Schritt 2 DirectAccess-Server** auf **Bearbeiten**.  
  
4.  Klicken Sie auf **Präfix Konfiguration**. Geben Sie auf der Seite **Präfix Konfiguration** unter **IPv6-Präfix, das DirectAccess-Client Computern zugewiesen**ist das IPv6-Präfix ein, das für DirectAccess-Client Computer mit der Subnetzlänge 59 verwendet wird, z. b. **2001: db8:1: 1000::/59**. Wenn VPN auch mit IPv6 aktiviert wurde, wird ein IPv6-Präfix angezeigt, und die Subnetzlänge muss in 59 geändert werden. Klicken Sie auf **Weiter**.  
  
5.  Klicken Sie im mittleren Bereich der Konsole auf **Fertig**stellen.  
  
6.  Überprüfen Sie im Dialogfeld **Remote Zugriffs Überprüfung** die Konfigurationseinstellungen, und klicken Sie **dann auf über**nehmen. Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.  
  
## <a name="32-enable-load-balancing"></a><a name="BKMK_NLB"></a>3,2 Aktivieren des Lasten Ausgleichs  
  
#### <a name="to-enable-load-balancing"></a>So aktivieren Sie den Lastenausgleich  
  
1.  Klicken Sie auf dem konfigurierten DirectAccess-Server auf **Start**, und klicken Sie dann auf **Remote Zugriffs Verwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole im linken Bereich auf **Konfiguration**, und klicken Sie dann im Bereich **Tasks** auf **Lastenausgleich aktivieren**.  
  
3.  Klicken Sie im Assistenten zum Aktivieren des Lasten Ausgleichs auf **weiter**.  
  
4.  Je nachdem, was Sie in den Planungsschritten gewählt haben:  
  
    1.  Windows-NLB: Klicken Sie auf der Seite **Lasten Ausgleichs Methode** auf **Windows-Netzwerk Lastenausgleich (NLB) verwenden**, und klicken Sie dann auf **weiter**.  
  
    2.  Externer Load Balancer: Klicken Sie auf der Seite **Lasten Ausgleichs Methode** auf **externen Load Balancer verwenden**, und klicken Sie dann auf **weiter**.  
  
5.  Führen Sie in einer einzelnen Netzwerkadapter Bereitstellung auf der Seite **dedizierte IP-Adressen** die folgenden Schritte aus, und klicken Sie dann auf **weiter**:  
  
    1.  Geben Sie im Feld **IPv4-Adresse** die neue IPv4-Adresse für diesen RAS-Server ein. bei der aktuellen IPv4-Adresse handelt es sich um die virtuelle IP-Adresse (VIP) des Clusters mit Lastenausgleich. Geben Sie im Feld **Subnetzmaske** die Subnetzmaske ein.  
  
    2.  Wenn es sich bei der Unternehmensumgebung um native IPv6 handelt, geben Sie im Feld **IPv6-Adresse** die neue IPv6-Adresse für diesen RAS-Server ein. bei der aktuellen IPv6-Adresse handelt es sich um die VIP des Clusters mit Lastenausgleich. Geben Sie im Feld **Subnetzpräfix-Länge** die Länge des Subnetzpräfixes ein.  
  
6.  Führen Sie in einer Bereitstellung mit zwei Netzwerkadaptern auf der Seite **externe dedizierte IP-Adressen** die folgenden Schritte aus, und klicken Sie dann auf **weiter**:  
  
    1.  Geben Sie im Feld **IPv4-Adresse** die neue externe IPv4-Adresse für diesen RAS-Server ein. bei der aktuellen IPv4-Adresse handelt es sich um die virtuelle IP-Adresse (VIP) des Lasten Ausgleichs Clusters. Geben Sie im Feld **Subnetzmaske** die Subnetzmaske ein.  
  
    2.  Wenn derzeit systemeigene IPv6-Adressen auf dem Netzwerkadapter des Remote Zugriffs Servers mit Internet Zugriff konfiguriert sind, geben Sie im Feld **IPv6-Adresse** die neue externe IPv6-Adresse für diesen RAS-Server ein. bei der aktuellen IPv6-Adresse handelt es sich um die VIP des Lasten Ausgleichs Clusters. Geben Sie im Feld **Subnetzpräfix-Länge** die Länge des Subnetzpräfixes ein.  
  
7.  Führen Sie in einer Bereitstellung mit zwei Netzwerkadaptern auf der Seite **interne dedizierte IP-Adressen** die folgenden Schritte aus, und klicken Sie dann auf **weiter**:  
  
    1.  Geben Sie im Feld **IPv4-Adresse** die neue interne IPv4-Adresse für diesen RAS-Server ein. bei der aktuellen IPv4-Adresse handelt es sich um die VIP des Lasten Ausgleichs Clusters. Geben Sie im Feld **Subnetzmaske** die Subnetzmaske ein.  
  
    2.  Wenn es sich bei der Unternehmensumgebung um native IPv6 handelt, geben Sie im Feld **IPv6-Adresse** die neue interne IPv6-Adresse für diesen RAS-Server ein. bei der aktuellen IPv6-Adresse handelt es sich um die VIP des Lasten Ausgleichs Clusters. Geben Sie im Feld **Subnetzpräfix-Länge** die Länge des Subnetzpräfixes ein.  
  
8.  Klicken Sie auf der Seite **Zusammenfassung** auf **Commit**.  
  
9. Klicken Sie im Dialogfeld **Lastenausgleich aktivieren** auf **Schließen**.  
  
10. Klicken Sie im Assistenten zum Aktivieren des Lasten Ausgleichs auf **Schließen**.  
  
    > [!NOTE]  
    > Wenn externer Lastenausgleich verwendet wird, notieren Sie sich die virtuellen IPS, und stellen Sie Sie als auf den externen Lasten Ausgleichs Modulen bereit.  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
Wenn Sie sich für die Verwendung von Windows NLB in den Planungsschritten entschieden haben, führen Sie Folgendes aus:  
  
```  
Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress "2.1.1.20/255.255.255.0" -InternalDedicatedIPAddress @("10.1.1.30/255.255.255.0","3ffe::20/64") -InternetVirtualIPAddress @("2.1.1.1/255.255.255.0","2.1.1.2/255.255.255.0") -InternalVirtualIPAddress @("10.1.1.2/255.255.255.0","3ffe::2/64")  
```  
  
Wenn Sie sich für die Verwendung eines externen Load Balancers in den Planungsschritten entschieden haben, führen Sie Folgendes aus:  
  
```  
Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress "2.1.1.20/255.255.255.0" -InternalDedicatedIPAddress @("10.1.1.30/255.255.255.0","3ffe::20/64") -UseThirdPrtyLoadBalancer  
```  
  
> [!NOTE]  
> Es wird empfohlen, keine Änderungen an den Einstellungen des Load Balancers mit Änderungen an anderen Einstellungen einzuschließen, wenn Sie staginggruppen Richtlinien Objekte verwenden. Alle Änderungen an den Einstellungen des Load Balancers müssen zuerst angewendet werden, und dann sollten andere Konfigurationsänderungen vorgenommen werden. Nachdem Sie den Lastenausgleich auf einem neuen DirectAccess-Server konfiguriert haben, sollten Sie außerdem einige Zeit für die Anwendung von IP-Änderungen auf die DNS-Server im Unternehmen zulassen, bevor Sie andere DirectAccess-Einstellungen ändern, die sich auf den neuen Cluster beziehen.  
  
## <a name="33-install-the-ip-https-certificate"></a><a name="BKMK_InstallIPHTTP"></a>3,3 Installieren des IP-HTTPS-Zertifikats  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Berechtigung erforderlich.  
  
### <a name="to-install-the-ip-https-certificate"></a><a name="IPHTTPSCert"></a>So installieren Sie das IP-HTTPS-Zertifikat  
  
1.  Klicken Sie auf dem konfigurierten RAS-Server auf **Start**, geben Sie **MMC** ein, und drücken Sie EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** auf **Zertifikate**, klicken Sie auf **Hinzufügen**, klicken Sie auf **Computer Konto**, klicken Sie auf **weiter**, klicken Sie auf **Fertig**stellen und dann auf **OK**.  
  
4.  Navigieren Sie im linken Bereich der Konsole zu **Zertifikate (lokaler Computer) \personal\zertifikate**. Klicken Sie mit der rechten Maustaste auf das IP-HTTPS-Zertifikat, zeigen **Sie auf** **Alle Tasks** , und klicken Sie auf  
  
5.  Klicken Sie auf der Seite **Zertifikatexport-Assistent – Willkommen** auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Privaten Schlüssel exportieren** auf **Ja, privaten Schlüssel exportieren**, und klicken Sie dann auf **Weiter**.  
  
7.  Klicken Sie auf der Seite **Format der exportierbare Datei** auf privater **Informationsaustausch-PKCS-#12 (). PFX)** , und klicken Sie dann auf **weiter**.  
  
8.  Aktivieren Sie auf der Seite **Sicherheit** das Kontrollkästchen **Kennwort** , geben Sie ein Kennwort in das Feld **Kennwort** ein, und bestätigen Sie das Kennwort, und klicken Sie dann auf **weiter**.  
  
9. Geben Sie auf der Seite **zu exportierendes Datei** einen Namen für die Zertifikat Datei ein, und speichern Sie Sie auf dem Desktop, und klicken Sie dann auf **weiter**.  
  
10. Klicken Sie auf der Seite **Fertigstellen des Assistenten** auf **Fertig stellen**.  
  
11. Klicken Sie im Dialogfeld **Zertifikat Export-Assistent** auf **OK**.  
  
12. Kopieren Sie das Zertifikat auf alle Server, die Sie als Cluster Mitglieder gruppieren möchten.  
  
13. Klicken Sie auf dem neuen DirectAccess-Server auf **Start**, geben Sie **MMC** ein, und drücken Sie EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
14. Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
15. Klicken Sie im Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** auf **Zertifikate**, klicken Sie auf **Hinzufügen**, klicken Sie auf **Computer Konto**, klicken Sie auf **weiter**, klicken Sie auf **Fertig**stellen und dann auf **OK**.  
  
16. Navigieren Sie im linken Bereich der Konsole zu **Zertifikate (lokaler Computer) \personal\zertifikate**. Klicken Sie mit der rechten Maustaste auf den Knoten **Zertifikate** , zeigen Sie auf **Alle Tasks**, und klicken Sie auf **importieren**.  
  
17. Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
18. Klicken Sie auf der Seite **zu importierende Datei** auf **Durchsuchen** , um das Zertifikat zu suchen. Wählen Sie das Zertifikat aus, und klicken Sie auf **weiter**.  
  
19. Geben Sie auf der Seite Schutz für den **privaten Schlüssel** im Feld **Kennwort** das Kennwort ein, und klicken Sie dann auf **weiter**.  
  
20. Klicken Sie auf der Seite **Zertifikatspeicher** auf **Weiter**.  
  
21. Klicken Sie auf der Seite **Abschließen des Zertifikatimport-Assistenten** auf **Fertig stellen**.  
  
22. Klicken Sie im Dialogfeld **Zertifikat Import-Assistent** auf **OK**.  
  
23. Wiederholen Sie die Schritte 13-22 auf allen Servern, bei denen es sich um Cluster Mitglieder handeln soll.  
  
## <a name="34-install-the-network-location-server-certificate"></a><a name="BKMK_NLS"></a>3,4 Installieren des Netzwerkadressen Server-Zertifikats  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Berechtigung erforderlich.  
  
#### <a name="to-install-a-certificate-for-network-location"></a>So installieren Sie ein Zertifikat für den Netzwerk Speicherort  
  
1.  Klicken Sie auf dem Remote Zugriffs Server auf **Start**, geben Sie **MMC**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie im Menü **Datei** auf **Snap-Ins hinzufügen bzw. entfernen**.  
  
3.  Klicken Sie auf **Zertifikate**, **Hinzufügen**, **Computer Konto**, **weiter**, klicken Sie auf **lokaler Computer**, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter**.  
  
7.  Klicken Sie auf der Seite **Zertifikate anfordern** auf die Vorlage Webserver Zertifikat, und klicken Sie dann auf **Weitere Informationen sind erforderlich, um sich für dieses Zertifikat zu registrieren**.  
  
    Wenn die Vorlage für das Webserver Zertifikat nicht angezeigt wird, stellen Sie sicher, dass das Remote Zugriffs Server-Computer Konto über die Berechtigung "registrieren" für die Webserver-Zertifikat Vorlage verfügt. Weitere Informationen finden Sie unter [Konfigurieren von Berechtigungen für die Webserver-Zertifikat Vorlage](https://msdn.microsoft.com/library/ee649249.aspx).  
  
8.  Wählen Sie im Dialogfeld **Zertifikat Eigenschaften** **auf der Register** Karte Antragsteller unter Antragsteller **Name**für **Typ**die Option allgemeiner **Name**aus.  
  
9. Geben Sie unter **Wert**den voll qualifizierten Domänen Namen (FQDN) für den Intranetnamen der Netzwerkadressen Server-Website ein (z. b. nls.Corp.contoso.com), und klicken Sie dann auf **Hinzufügen**.  
  
10. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
11. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, dass ein neues Zertifikat mit dem vollqualifizierten Domänennamen unter **Serverauthentifizierung** mit der Option **Beabsichtigte Zwecke** registriert wurde.  
  
12. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und klicken Sie anschließend auf **Eigenschaften**.  
  
13. Geben Sie unter **Anzeigenamen** den Namen **Netzwerkadressenzertifikat** ein, und klicken Sie dann auf **OK**.  
  
    > [!TIP]  
    > Die Schritte 12 und 13 sind optional, erleichtern es Ihnen jedoch, das Zertifikat für den Netzwerk Speicherort beim Konfigurieren des Remote Zugriffs auszuwählen.  
  
14. Wiederholen Sie diesen Vorgang auf allen Servern, für die Sie Cluster Mitglieder sein möchten.  
  
## <a name="35-add-servers-to-the-cluster"></a><a name="BKMK_Add"></a>3,5 Hinzufügen von Servern zum Cluster  
 
  
#### <a name="to-add-servers-to-the-cluster"></a>So fügen Sie dem Cluster Server hinzu  
  
1.  Klicken Sie auf dem konfigurierten DirectAccess-Server auf **Start**, und klicken Sie dann auf **Remote Zugriffs Verwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. Klicken Sie im Bereich **Tasks** unter **Cluster mit Lasten**Ausgleich auf **Server hinzufügen oder entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Server hinzufügen oder entfernen** auf **Server hinzufügen**.  
  
4.  Geben Sie im Dialogfeld **Server hinzufügen** auf der Seite **Server auswählen** den Namen des zusätzlichen Remote Zugriffs Servers ein, und klicken Sie dann auf **weiter**.  
  
5.  Führen Sie auf der Seite **Netzwerkadapter** einen der folgenden Schritte aus:  
  
    -   Wenn Sie eine Topologie mit zwei Netzwerkadaptern bereitstellen, wählen Sie in **externer Adapter**den Adapter aus, der mit dem externen Netzwerk verbunden ist. Wählen Sie unter **interner Adapter**den Adapter aus, der mit dem internen Netzwerk verbunden ist.  
  
    -   Wenn Sie eine Topologie mit einem Netzwerkadapter bereitstellen, wählen Sie unter **Netzwerkadapter**den Adapter aus, der mit dem internen Netzwerk verbunden ist.  
  
6.  Klicken Sie auf der Seite **Netzwerkadapter** unter **Wählen Sie das zum Authentifizieren von IP-HTTPS-Verbindungen verwendete Zertifikat**auf **Durchsuchen** , um das IP-HTTPS-Zertifikat zu suchen und auszuwählen, und klicken Sie dann auf **weiter**.  
  
7.  Klicken Sie auf der Seite **Netzwerkadressen Server** auf **Durchsuchen** , um das Zertifikat für die Netzwerkadressen Server-Website auszuwählen, die auf dem Remote Zugriffs Server ausgeführt wird, und klicken Sie dann auf **weiter**.  
  
    > [!NOTE]  
    > Die Seite **Netzwerkadressen Server** wird nur angezeigt, wenn die Netzwerkadressen Server-Website auf dem Remote Zugriffs Server ausgeführt wird.  
  
    > [!NOTE]  
    > Wenn auch VPN auf dem RAS-Server konfiguriert wurde, werden Sie aufgefordert, an dieser Stelle die Informationen zum VPN-IP-Adresspool hinzuzufügen.  
  
8.  Klicken Sie auf der Seite **Zusammenfassung** auf **Hinzufügen**.  
  
9. Klicken Sie auf der Seite **Abschluss des Vorgangs** auf **Schließen**.  
  
10. Wiederholen Sie diesen Vorgang für alle Remote Zugriffs Server, die dem Cluster hinzugefügt werden sollen.  
  
11. Klicken Sie im Dialogfeld **Server hinzufügen oder entfernen** auf **Commit**.  
  
12. Klicken Sie im Dialogfeld zum **Hinzufügen und Entfernen von Servern** auf **Schließen**.  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
Add-RemoteAccessLoadBalancerNode -RemoteAccessServer <server name>  
```  
  
> [!NOTE]  
> Wenn VPN nicht in einem Cluster mit Lastenausgleich aktiviert wurde, sollten Sie keine VPN-Adressbereiche angeben, wenn Sie dem Cluster mithilfe von Windows PowerShell-Cmdlets einen neuen Server hinzufügen. Wenn dies versehentlich erfolgt ist, entfernen Sie den Server aus dem Cluster, und fügen Sie ihn erneut dem Cluster hinzu, ohne die VPN-Adressbereiche anzugeben.  
  
## <a name="36-remove-a-server-from-the-cluster"></a><a name="BKMK_remove"></a>3,6 Entfernen eines Servers aus dem Cluster  
 
  
#### <a name="to-remove-a-server-from-the-cluster"></a>So entfernen Sie einen Server aus dem Cluster  
  
1.  Klicken Sie auf dem konfigurierten Remote Zugriffs Server auf **Start**, und klicken Sie dann auf **Remote Zugriffs Verwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. Klicken Sie im Bereich **Tasks** unter **Cluster mit Lasten**Ausgleich auf **Server hinzufügen oder entfernen**.  
  
3.  Wählen Sie im Dialogfeld **Server hinzufügen oder entfernen** den Remote Zugriffs Server aus, den Sie entfernen möchten, und klicken Sie dann auf **Server entfernen**.  
  
4.  Stellen Sie im Dialogfeld **Server Warnung entfernen** sicher, dass Sie den richtigen Server ausgewählt haben, und klicken Sie dann auf **OK**.  
  
5.  Wiederholen Sie diesen Vorgang für alle Remote Zugriffs Server, die aus dem Cluster entfernt werden sollen.  
  
6.  Klicken Sie im Dialogfeld **Server hinzufügen oder entfernen** auf **Commit**.  
  
7.  Klicken Sie im Dialogfeld zum **Hinzufügen und Entfernen von Servern** auf **Schließen**.  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
Remove-RemoteAccessLoadBalancerNode -RemoteAccessServer <server name>  
```  
  
## <a name="37-disable-load-balancing"></a><a name="BKBK_disable"></a>3,7 Deaktivieren des Lasten Ausgleichs  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///7a817ca0-2b4a-4476-9d28-9a63ff2453f9)  
  
#### <a name="to-disable-load-balancing"></a>So deaktivieren Sie den Lastenausgleich  
  
1.  Klicken Sie auf dem konfigurierten DirectAccess-Server auf **Start**, und klicken Sie dann auf **Remote Zugriffs Verwaltung**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. Klicken Sie im Bereich **Tasks** unter **Cluster mit Lasten**Ausgleich auf **Lastenausgleich deaktivieren**.  
  
3.  Klicken Sie im Dialogfeld **Lastenausgleich deaktivieren** auf **OK**.  
  
4.  Klicken Sie im Dialogfeld " **Lastenausgleich deaktivieren** " auf **Schließen**.  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-3-Configure-a-Load-Balanced-Cluster/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
set-RemoteAccessLoadBalancer -disable  
```  
  
Durch das Deaktivieren des Lasten Ausgleichs werden Remote Zugriffs Einstellungen und NLB-Einstellungen (sofern konfiguriert) von allen Servern außer dem Server entfernt, von dem aus Sie ausgeführt werden. Auf diesem RAS-Server werden NLB-Einstellungen entfernt (sofern konfiguriert), aber die Remote Zugriffs Einstellungen bleiben erhalten.  
  
Wenn Sie auf **Konfigurationseinstellungen entfernen** klicken, werden Remote Zugriff und NLB (sofern konfiguriert) von allen Servern in der Bereitstellung entfernt.  
  
> [!NOTE]  
> -   Wenn der Remote Zugriff beim Bereitstellen des Lasten Ausgleichs deinstalliert wird, verbleiben alle Server mit Dips. Die VIPs werden entfernt. Dies bewirkt, dass alle Routen im Unternehmensnetzwerk, die für die VIPs-Adressen vorgesehen sind, fehlschlagen. Dies wirkt sich auch auf DNS-Einträge aus, die zu den VIPs aufgelöst wurden, wie z. b. den Antragsteller Namen des Netzwerkadressen Servers Um dieses Problem zu vermeiden, deaktivieren Sie den Lastenausgleich, bei dem die VIPs auf dem letzten RAS-Server belassen werden, und deinstallieren Sie dann den Remote Zugriff.  
> -   Nachdem Sie das Cmdlet " **Set-remoteaccessloadbalancer** " zum Deaktivieren des Lasten Ausgleichs verwendet haben, warten Sie zwei Minuten, bevor Sie ein beliebiges anderes Cmdlet ausführen. Dies sollte auch in allen Skripts erfolgen, die nach dem **Set-remoteaccessloadbalancer-deaktivierte** Cmdlet ein anderes Cmdlet ausführen.  
> -   Durch die Deaktivierung des Lasten Ausgleichs wird die virtuelle IP-Adresse des Clusters in eine dedizierte IP-Adresse geändert. Daher schlägt jeder Vorgang, bei dem der Name des Servers abgefragt wird, so lange fehl, bis der zwischengespeicherte DNS-Eintrag auf dem Server abläuft. Stellen Sie sicher, dass Sie keine PowerShell-Cmdlets für den Remote Zugriff ausführen, nachdem Sie den Lastenausgleich deaktiviert haben, bis der Cache auf dem Server abgelaufen ist. Dieses Problem ist häufiger, wenn Sie versuchen, den Lastenausgleich auf einem Computer von einem anderen Computer in einer anderen Domäne zu deaktivieren. Dies geschieht auch, wenn Sie den Lastenausgleich über die Remote Zugriffs-Verwaltungskonsole deaktivieren und das Laden der Konfiguration möglicherweise verhindern. Die Konfiguration wird geladen, nachdem der Cache abgelaufen ist oder geleert wurde.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 4: Überprüfen des Clusters](Step-4-Verify-the-Cluster.md)  
  


