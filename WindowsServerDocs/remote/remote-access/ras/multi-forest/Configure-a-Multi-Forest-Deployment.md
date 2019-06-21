---
title: Configure a Multi-Forest Deployment
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einer Umgebung mit mehreren Gesamtstrukturen in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c8feff2-cae1-4376-9dfa-21ad3e4d5d99
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bf9222293dfd22b6f32cf00021f34b44c555e340
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281104"
---
# <a name="configure-a-multi-forest-deployment"></a>Configure a Multi-Forest Deployment

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird beschrieben, wie Sie eine Remotezugriffsbereitstellung mit mehreren Gesamtstrukturen in verschiedenen möglichen Szenarien konfigurieren. In allen Szenarien wird davon ausgegangen, dass DirectAccess gegenwärtig in einer einzigen Gesamtstruktur mit dem Namen %%amp;quot;Forest1%%amp;quot; bereitgestellt ist und Sie DirectAccess für eine neue Gesamtstruktur mit dem Namen %%amp;quot;Forest2%%amp;quot; konfigurieren.  
  
## <a name="AccessForest2"></a>Zugreifen auf Ressourcen in Forest2  
In diesem Szenario ist DirectAccess bereits in %%amp;quot;Forest1%%amp;quot; bereitgestellt und so konfiguriert, dass Clients aus %%amp;quot;Forest1%%amp;quot; auf das Unternehmensnetzwerk zugreifen können. Clients, die eine Verbindung über DirectAccess herstellen, können standardmäßig nur auf Ressourcen in %%amp;quot;Forest1%%amp;quot; zugreifen und haben keinen Zugriff auf Server in %%amp;quot;Forest2%%amp;quot;.  
  
#### <a name="to-enable-directaccess-clients-to-access-resources-from-forest2"></a>So ermöglichen Sie DirectAccess-Clients den Zugriff auf Ressourcen in %%amp;quot;Forest2%%amp;quot;  
  
1.  Wenn das DNS-Suffix von %%amp;quot;Forest2%%amp;quot; nicht Teil des DNS-Suffix von %%amp;quot;Forest1%%amp;quot; ist, fügen Sie NRPT-Regeln mit den Suffixen der Domänen in %%amp;quot;Forest2%%amp;quot; hinzu, und fügen Sie optional die Suffixe der Domänen in %%amp;quot;Forest2%%amp;quot; der DNS-Suffixsuchliste hinzu.  
  
2.  Fügen Sie die entsprechenden internen IPv6-Präfixe in %%amp;quot;Forest2%%amp;quot; hinzu, wenn IPv6 im internen Netzwerk bereitgestellt ist.  
  
## <a name="EnableForest2DA"></a>Ermöglichen Sie Clients forest2 Verbindungen über DirectAccess zulassen  
In diesem Szenario konfigurieren Sie die Remotezugriffsbereitstellung so, dass Clients in %%amp;quot;Forest2%%amp;quot; auf das Unternehmensnetzwerk zugreifen können. Es wird vorausgesetzt, dass Sie die erforderlichen Sicherheitsgruppen für Clientcomputer in %%amp;quot;Forest2%%amp;quot; erstellt haben.   
  
#### <a name="to-allow-clients-from-forest2-to-access-the-corporate-network"></a>So ermöglichen Sie Clients in %%amp;quot;Forest2%%amp;quot; den Zugriff auf das Unternehmensnetzwerk  
  
1.  Fügen Sie die Sicherheitsgruppe der Clients in %%amp;quot;Forest2%%amp;quot; hinzu.  
  
2.  Ist das DNS-Suffix des Forest2 nicht Teil des DNS-Suffixes Forest1, Hinzufügen von NRPT-Regeln mit den Suffixen der der Domäne der Clients in Forest2 zum Aktivieren des Zugriffs auf die Domänencontroller für die Authentifizierung und optional die Suffixe der Domänen in Forest2 hinzufügen, um die DNS-suf Beheben Sie die Suchliste. 
  
3.  Fügen Sie die internen IPv6-Präfixe in %%amp;quot;Forest2%%amp;quot; hinzu, damit DirectAccess den IPsec-Tunnel zu den Domänencontrollern für die Authentifizierung erstellen kann.  
  
4.  Aktualisieren Sie die Liste der Verwaltungsserver.  
  
## <a name="AddEPForest2"></a>Hinzufügen von Einstiegspunkten forest2  
In diesem Szenario ist DirectAccess in einer Konfiguration für mehrere Standorte in %%amp;quot;Forest1%%amp;quot; bereitgestellt und Sie möchten einen RAS-Server mit dem Namen %%amp;quot;DA2%%amp;quot; in %%amp;quot;Forest2%%amp;quot; als Einstiegspunkt zur vorhandenen DirectAccess-Bereitstellung für mehrere Standorte hinzufügen.  
  
#### <a name="to-add-a-remote-access-server-from-forest2-as-an-entry-point"></a>So fügen Sie einen RAS-Server in %%amp;quot;Forest2%%amp;quot; als Einstiegspunkt hinzu  
  
1.  Stellen Sie sicher, dass der Remotezugriffsadministrator über ausreichende Berechtigungen zum Schreiben von GPOs in der Domäne von %%amp;quot;DA2%%amp;quot; verfügt und ein lokaler Administrator auf %%amp;quot;DA2%%amp;quot; ist.  
  
2.  Fügen Sie DA2 als Einstiegspunkt hinzu.   
  
3.  Fügen Sie NRPT-Regeln mit den Suffixen der Domänen in %%amp;quot;Forest2%%amp;quot; hinzu, um den Zugriff auf die Domänencontroller für die Authentifizierung zu ermöglichen, und fügen Sie optional die Suffixe der Domänen in %%amp;quot;Forest2%%amp;quot; der DNS-Suffixsuchliste hinzu.  
  
4.  Fügen Sie ggf. die entsprechenden internen IPv6-Präfixe in %%amp;quot;Forest2%%amp;quot; hinzu, um dem Remotezugriff das Erstellen des IPsec-Tunnels zu den Unternehmensressourcen zu ermöglichen und sicherzustellen, dass NCSI-Tests korrekt funktionieren.  
  
5.  Aktualisieren Sie die Liste der Verwaltungsserver.  
  
## <a name="OTPMultiForest"></a>Konfigurieren von Einmalkennwörtern in einer Bereitstellung mit mehreren Gesamtstrukturen  
Folgende Begriffe sind beim Konfigurieren von OTP (One-Time Password = Einmalkennwort) in einer Bereitstellung mit mehreren Gesamtstrukturen wichtig:  
  
-   Stamm-CA-die Gesamtstrukturen PKI-Struktur.  
  
-   Enterprise-Zertifizierungsstelle und alle anderen Zertifizierungsstellen.  
  
-   Ressourcen-Gesamtstruktur die Gesamtstruktur, die die Stammzertifizierungsstelle enthält, und gilt als "Verwalten von Forest\domain".  
  
-   Account-Gesamtstruktur und alle anderen Gesamtstrukturen in der Topologie.  
  
Für dieses Verfahren ist das PowerShell-Skript %%amp;quot;PKISync.ps1%%amp;quot; erforderlich. Finden Sie unter [AD CS: Amp;quot;pkisync.ps1%%amp;quot; für die gesamtstrukturübergreifende Zertifikatregistrierung](https://technet.microsoft.com/library/ff961506.aspx).  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
### <a name="BKMK_CertPub"></a>Konfigurieren von Zertifizierungsstellen als Zertifikatherausgeber  
  
1.  Aktivieren Sie die LDAP-Weiterleitungsunterstützung für alle Unternehmenszertifizierungsstellen in allen Gesamtstrukturen, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen:  
  
    ```  
    certutil -setreg Policy\EditFlags +EDITF_ENABLELDAPREFERRALS  
    ```  
  
2.  Fügen Sie alle Unternehmenszertifizierungsstellen-Computerkonten der Active Directory-Sicherheitsgruppe %%amp;quot;Zertifikatherausgeber%%amp;quot; in jeder der Kontengesamtstrukturen hinzu.  
  
3.  Starten Sie alle Zertifikatdienste (certsvc) auf allen Zertifizierungsstellencomputern in allen Gesamtstrukturen neu, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen:  
  
    ```  
    net stop certsvc && net start certsvc  
    ```  
  
4.  Extrahieren Sie das Stammzertifizierungsstellenzertifikat, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen.  
  
    ```  
    certutil -config <Computer-Name>\<Root-CA-Name> -ca.cert <root-ca-cert-filename.cer>  
    ```  
  
    (Wenn Sie den Befehl auf dem stammzertifizierungsstellencomputer ausführen, können Sie die Verbindungsinformationen, - Config < Computername > weglassen\\< Stamm-ZS-Name >)  
  
    1.  Importieren Sie das Stammzertifizierungsstellenzertifikat aus dem vorherigen Schritt auf der Zertifizierungsstelle der Kontengesamtstruktur, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen:  
  
        ```  
        certutil -dspublish -f <root-ca-cert-filename.cer> RootCA  
        ```  
  
    2.  GRANT-Ressourcengesamtstruktur Lese-/Schreibberechtigungen für Zertifikatvorlagen, die \<Kontogesamtstruktur\>\\< Administratorkonto\>.  
  
    3.  Extrahieren Sie alle Unternehmenszertifizierungsstellenzertifikate der Ressourcengesamtstruktur, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen.  
  
        ```  
        certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>  
        ```  
  
        (Wenn Sie den Befehl auf dem stammzertifizierungsstellencomputer ausführen, können Sie die Verbindungsinformationen, - Config < Computername > weglassen\\< Stamm-ZS-Name >)  
  
    4.  Importieren Sie die Unternehmenszertifizierungsstellenzertifikate aus dem vorherigen Schritt auf der Zertifizierungsstelle der Kontengesamtstruktur, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen:  
  
        ```  
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> NTAuthCA  
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> SubCA  
        ```  
  
    5.  Entfernen Sie OTP-Zertifikatvorlagen der Kontengesamtstruktur aus der Liste ausgestellter Zertifikatvorlagen.  
  
### <a name="BKMK_DelImp"></a>Löschen und Importieren von OTP-Zertifikatvorlagen  
  
1.  Löschen Sie OTP-Zertifikatvorlagen aus der Kontengesamtstruktur, d. h. aus %%amp;quot;Forest2%%amp;quot;.  
  
2.  Kopieren Sie mithilfe der folgenden PowerShell-Befehle Zertifikatvorlagen und OID-Objekte aus der Ressourcengesamtstruktur in jede der Kontengesamtstrukturen:  
  
    ```  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <DA OTP registration authority template common name>.  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <Secure DA OTP logon certificate template common name>.  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Oid -f  
    ```  
  
### <a name="BKMK_Publish"></a>Veröffentlichen von OTP-Zertifikatvorlagen  
  
-   Stellen Sie die neu importierten Zertifikatvorlagen auf allen Zertifizierungsstellen der Kontengesamtstrukturen aus.  
  
### <a name="BKMK_Extract"></a>Extrahieren und Synchronisieren der Zertifizierungsstelle  
  
1.  Extrahieren Sie alle Unternehmenszertifizierungsstellenzertifikate aus den Kontengesamtstrukturen, indem Sie die folgenden Befehle an einer Eingabeaufforderung mit erhöhten Rechten ausführen:  
  
    ```  
    certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>  
    ```  
  
2.  Synchronisieren Sie Zertifizierungsstellen aus den Kontengesamtstrukturen mithilfe des folgenden PowerShell-Befehls gesamtstrukturübergreifend mit der Ressourcengesamtstruktur:  
  
    ```  
    .\PKISync.ps1 -sourceforest <account forest DNS> -targetforest <resource forest DNS> -type CA -cn <enterprise CA sanitized name> -f  
    ```  
  
3.  Synchronisieren Sie Zertifizierungsstellen aus der Ressourcengesamtstruktur mithilfe des folgenden PowerShell-Befehls gesamtstrukturübergreifend mit den Kontengesamtstrukturen:  
  
    ```  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type CA -cn <enterprise CA sanitized name> -f  
    ```  
  
## <a name="configuration-procedures"></a>Konfigurationsverfahren  
In den folgenden Abschnitten werden die Konfigurationsverfahren für die Bereitstellungen in den obigen Szenarien beschrieben. Kehren Sie nach dem Ausführen eines Verfahrens zum Szenario zurück, um damit fortzufahren.  
  
### <a name="NRPT_DNSSearchSuffix"></a>Fügen Sie NRPT-Regeln und DNS-Suffixe hinzu  
Clients, die über DirectAccess eine Verbindung mit dem Unternehmensnetzwerk herstellen, verwenden die Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT), um zu ermitteln, welcher DNS-Server zum Auflösen der Adresse verschiedener Ressourcen verwendet werden sollte. Dies ermöglicht es dem Client, Adressen von Unternehmensressourcen aufzulösen und die für die einwandfreie Funktion von DirectAccess erforderliche Klassifizierung für Ressourcen innerhalb/außerhalb des Unternehmens aufrecht zu erhalten. Die DirectAccess-Konfigurationstools erkennen das DNS-Stammsuffix von %%amp;quot;Forest1%%amp;quot; automatisch und fügen es der NRPT-Tabelle hinzu. Die Suffixe des vollqualifizierten Domänennamens (Fully Qualified Domain Name, FQDN) von %%amp;quot;Forest2%%amp;quot; werden der NRPT-Tabelle jedoch nicht automatisch hinzugefügt und müssen manuell vom Remotezugriffsadministrator hinzugefügt werden.  
  
Die DNS-Suffixsuchliste ermöglicht es den Clients, anstelle von FQDNs Kurznamen zu verwenden. Die Remotezugriffs-Konfigurationstools fügen der DNS-Suffixsuchliste automatisch alle Domänen in %%amp;quot;Forest1%%amp;quot; hinzu. Wenn Clients in der Lage sein sollen, Kurznamen für Ressourcen in %%amp;quot;Forest2%%amp;quot; zu verwenden, müssen Sie sie manuell hinzufügen.  
  
##### <a name="to-add-a-dns-suffix-to-the-nrpt-table-and-domain-suffixes-to-the-dns-suffix-search-list"></a>So fügen Sie der NRPT-Tabelle ein DNS-Suffix und der DNS-Suffixsuchliste Domänensuffixe hinzu  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 3 Infrastrukturserver** auf **Bearbeiten**.  
  
2.  Klicken Sie auf der Seite **Netzwerkadressenserver** auf **Weiter**.  
  
3.  Geben Sie auf der Seite **DNS** in der Tabelle alle zusätzlichen Namenssuffixe ein, die Teil des Unternehmensnetzwerks in %%amp;quot;Forest2%%amp;quot; sind. Geben Sie in **DNS-Serveradresse** die Adresse des DNS-Servers manuell ein, oder klicken Sie auf **Erkennen**. Wenn Sie die Adresse nicht eingeben, werden die neuen Einträge als NRPT-Ausnahmen angewendet. Klicken Sie dann auf **Weiter**.  
  
4.  Optional: Fügen Sie auf der Seite **DNS-Suffixsuchliste** DNS-Suffixe hinzu, indem Sie das Suffix in das Feld **Neues Suffix** eingeben und dann auf **Hinzufügen** klicken. Klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Verwaltung** auf **Fertig stellen**.  
  
6.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole auf **Fertig stellen**.  
  
7.  Klicken Sie im Dialogfeld **Überprüfung des Remotezugriffs** auf **Anwenden**.  
  
8.  Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.  
  
### <a name="IPv6Prefix"></a>Interne IPv6-Präfix hinzufügen  
  
> [!NOTE]  
> Das Hinzufügen eines internen IPv6-Präfix ist nur erforderlich, wenn IPv6 im internen Netzwerk bereitgestellt ist.  
  
Der Remotezugriff verwaltet eine Liste von IPv6-Präfixen für Unternehmensressourcen. Clients, die über DirectAccess eine Verbindung herstellen, können nur auf Ressourcen mit diesen IPv6-Präfixen zugreifen. Da die Remotezugriffs-Verwaltungskonsole und Windows PowerShell-Befehlen automatisch die IPv6-Präfixe Forest1 hinzugefügt, und die Präfixe anderer Gesamtstrukturen möglicherweise aber nicht hinzugefügt, müssen Sie alle fehlenden Präfixe von Forest2 manuell hinzufügen.  
  
##### <a name="to-add-an-ipv6-prefix"></a>So fügen Sie ein IPv6-Präfix hinzu  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 2 RAS-Server** auf **Bearbeiten**.  
  
2.  Klicken Sie im Setup-Assistenten für den RAS-Server auf **Präfixkonfiguration**.  
  
3.  Fügen Sie auf der Seite **Präfixkonfiguration** unter **IPv6-Präfixe des internen Netzwerks** alle zusätzlichen IPv6-Präfixe durch Semikolons getrennt hinzu (z. B. 2001:db8:1::/64;2001:db8:2::/64). Klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Authentifizierung** auf **Fertig stellen**.  
  
5.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole auf **Fertig stellen**.  
  
6.  Klicken Sie im Dialogfeld **Überprüfung des Remotezugriffs** auf **Anwenden**.  
  
7.  Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.  
  
### <a name="SGs"></a>Hinzufügen von clientsicherheitsgruppen  
Um Windows 8-Clientcomputer forest2 über DirectAccess auf Ressourcen zugreifen können, müssen Sie der Sicherheitsgruppe "forest2 %% für die remotezugriffsbereitstellung hinzufügen.  
  
##### <a name="to-add-windows-8-client-security-groups"></a>So fügen Sie Windows 8-Clientsicherheitsgruppen hinzu  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 1 Remoteclients** auf **Bearbeiten**.  
  
2.  Klicken Sie im Assistenten zum Einrichten des DirectAccess-Clients auf **Gruppen auswählen**, und klicken Sie dann auf der Seite **Gruppen auswählen** auf **Hinzufügen**.  
  
3.  Wählen Sie im Dialogfeld **Gruppen auswählen** die Sicherheitsgruppen aus, die DirectAccess-Clientcomputer enthalten. Klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Netzwerkkonnektivitäts-Assistent** auf **Fertig stellen**.  
  
5.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole auf **Fertig stellen**.  
  
6.  Klicken Sie im Dialogfeld **Überprüfung des Remotezugriffs** auf **Anwenden**.  
  
7.  Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.  
  
Zum Aktivieren von Windows 7-Clientcomputer forest2 Zugriff auf Ressourcen über DirectAccess, wenn für mehrere Standorte aktiviert ist, müssen Sie der Sicherheitsgruppe "forest2 für die remotezugriffsbereitstellung für jeden Einstiegspunkt hinzufügen. Informationen zum Hinzufügen von Windows 7-Sicherheitsgruppen finden Sie in die Beschreibung des der **Clientunterstützung** Seite 3.6. Aktivieren Sie die Bereitstellung für mehrere Standorte.  
  
### <a name="RefreshMgmtServers"></a>Aktualisieren der Liste der Verwaltungsserver  
Der Remotezugriff erkennt automatisch die Infrastrukturserver in allen Gesamtstrukturen, die GPOs für die DirectAccess-Konfiguration enthalten. Wenn DirectAccess auf einem Server in %%amp;quot;Forest1%%amp;quot; bereitgestellt wurde, wird das Server-GPO in seine Domäne in %%amp;quot;Forest1%%amp;quot; geschrieben. Nachdem Sie den Zugriff auf DirectAccess für Clients in %%amp;quot;Forest2%%amp;quot; aktiviert haben, wird das Client-GPO in eine Domäne in %%amp;quot;Forest2%%amp;quot; geschrieben.  
  
Die automatische Erkennung von Infrastrukturservern ist erforderlich, um über DirectAccess den Zugriff auf die Domänencontroller und System Center Configuration Manager zu ermöglichen. Sie müssen den Erkennungsprozess manuell starten.  
  
##### <a name="to-refresh-the-management-servers-list"></a>So aktualisieren Sie die Liste der Verwaltungsserver  
  
1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration** und dann im Bereich **Aufgaben** auf **Verwaltungsserver aktualisieren**.  
  
2.  Klicken Sie im Dialogfeld **Aktualisieren von Verwaltungsservern** auf **Schließen**.  
  


