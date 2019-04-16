---
title: Konfigurieren von DirectAccess in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cc336dcd2a5418aa79254108c941a02147112e8f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Konfigurieren von DirectAccess in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Thema enthält eine schrittweise Anleitung zum Konfigurieren von DirectAccess in Windows Server Essentials um mobilen Mitarbeiter Verbindung nahtlos mit Ihrer Organisation s von einem beliebigen Remotestandort mit Internetanschluss ohne Herstellen einer Verbindung virtuelles privates Netzwerk (VPN) ermöglichen. DirectAccess können mobile Mitarbeiter, die gleiche netzwerkanbindung innerhalb und außerhalb des Büros auf ihren Windows 8.1, Windows 8 und Windows 7-Computern anbieten.  
  
 In Windows Server Essentials Wenn eine Domäne mehr als einen Windows Server Essentials-Server muss DirectAccess auf dem Domänencontroller konfiguriert werden.  
  
> [!NOTE]
>  Dieses Thema enthält Anweisungen zum Konfigurieren von DirectAccess, wenn Ihre Windows Server Essentials-Server der Domänencontroller ist. Wenn der Windows Server Essentials-Server Mitglied einer Domäne ist, folgen Sie den Anweisungen zum Konfigurieren von DirectAccess auf einem Domänenmitglied in [Hinzufügen von DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN) Bereitstellung](https://technet.microsoft.com/library/jj574220.aspx) stattdessen.  
  
## <a name="process-overview"></a>Übersicht über den Prozess  
 Führen Sie die folgenden Schritte aus, um DirectAccess in Windows Server Essentials zu konfigurieren.  
  
> [!IMPORTANT]
>  Bevor Sie die Verfahren in diesem Handbuch zum Konfigurieren von DirectAccess in Windows Server Essentials verwenden, müssen Sie VPN auf dem Server aktivieren. Anweisungen finden Sie unter [Verwalten des VPN](Manage-VPN-in-Windows-Server-Essentials.md).  
  
-   [Schritt 1: Hinzufügen von Remoteserver-Verwaltungstools auf dem server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)  
  
-   [Schritt 2: Ändern der Netzwerkadapteradresse des Servers zu einer statischen IP-Adresse](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)  
  
-   [Schritt 3: Vorbereiten eines Zertifikats und DNS-Eintrags für den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)  
  
    -   [Schritt 3a: Zuweisen uneingeschränkter Berechtigungen auf authentifizierte Benutzer für die Webserver s-Zertifikatvorlage](#BKMK_GrantFullPermissions)  
  
    -   [Schritt 3: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann,](#BKMK_EnrollaCertificate)  
  
    -   [Schritt 3c: Hinzufügen eines neues Hosts auf dem DNS-Server und zuordnen, die Windows Server Essentials-Serveradresse](#BKMK_MapNewHosttoServerAddress)  
  
-   [Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Clientcomputer](#BKMK_AddSecurityGroup)  
  
-   [Schritt 5: Aktivieren und Konfigurieren von DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)  
  
    -   [Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
    -   [Schritt 5 b: Entfernen Sie die ungültigen IPv6Prefix im RRAS-Gruppenrichtlinienobjekt (nur Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
    -   [Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess](#BKMK_Step4cWindows7Setup)  
  
    -   [Schritt 5D: Konfigurieren Sie den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
    -   [Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten des IPsec-Kanals](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
-   [Schritt 6: Konfigurieren von Name Resolution Policy Table-Einstellungen für den DirectAccess-server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)  
  
-   [Schritt 7: Konfigurieren von TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)  
  
-   [Schritt 8: Ändern der DNS64-Konfigurations zum Abhören der IP-HTTPS-Schnittstelle](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)  
  
-   [Schritt 9: Reservieren von Ports für des WinNat-Diensts](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)  
  
-   [Schritt 10: Neustarten des WinNat-Diensts](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)  
  
> [!NOTE]
>  [Anhang: Einrichten von DirectAccess mithilfe von Windows PowerShell](#BKMK_AppendixBPowerShellScript) bietet ein Windows PowerShell-Skript, mit denen Sie die DirectAccess-Setup ausführen.  
  
##  <a name="BKMK_AddRAM"></a>Schritt 1: Hinzufügen von Remoteserver-Verwaltungstools auf dem server  
  
#### <a name="to-add-remote-access-management-tools"></a>Remoteserver-Verwaltungstools hinzufügen  
  
1.  Klicken Sie auf dem Server, in der unteren linken Ecke der Startseite, auf die **Server-Manager** Symbol.  
  
     In Windows Server Essentials müssen Sie die Suche für Server-Manager, um es zu öffnen. Geben Sie auf der Startseite **Server-Manager**, und klicken Sie dann auf **Server-Manager** in den Suchergebnissen angezeigt. Zum Server-Manager an die Startseite anheften, mit der rechten Maustaste Server-Manager in den Suchergebnissen, und klicken Sie auf **auf Startseite**.  
  
2.  Wenn ein **User Account Control** Warnmeldung angezeigt wird, klicken Sie auf **Ja**.  
  
3.  Klicken Sie auf dem Server-Manager-Dashboard auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**.  
  
4.  Hinzufügen von Rollen und Features Assistenten führen Sie folgende Schritte aus:  
  
    1.  Auf der **Installationstyp** auf **rollenbasierte oder featurebasierte Installation**.  
  
    2.  Auf der **Serverauswahl** (oder die **Zielserver auswählen** Seite in Windows Server Essentials), klicken Sie auf **wählen Sie einen Server aus dem Serverpool**.  
  
    3.  Auf der **Features** Seite, erweitern Sie **Remoteserver-Verwaltungstools (installiert)**, erweitern Sie **Remotezugriffsverwaltung (installiert)**, erweitern Sie **Rollenverwaltungstools (installiert)**, erweitern Sie **Remotezugriffsverwaltung**, und wählen Sie dann **Remotezugriffs-GUI und Befehlszeilentools**.  
  
    4.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
##  <a name="BKMK_AddStaticIP"></a>Schritt 2: Ändern der Netzwerkadapteradresse des Servers zu einer statischen IP-Adresse  
 DirectAccess erfordert einen Adapter mit einer statischen IP-Adresse. Sie müssen die IP-Adresse für den lokalen Netzwerkadapter auf dem Server zu ändern.  
  
#### <a name="to-add-a-static-ip-address"></a>So fügen Sie eine statische IP-Adresse hinzu  
  
1.  Öffnen Sie auf der Startseite **Systemsteuerung**.  
  
2.  Klicken Sie auf **Netzwerk und Internet**, und klicken Sie dann auf **Netzwerkstatus und-Aufgaben anzeigen**.  
  
3.  Im Aufgabenbereich, der die **Netzwerk- und Freigabecenter**, klicken Sie auf **adaptereinstellungen ändern**.  
  
4.  Maustaste auf den lokalen Netzwerkadapter, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Auf der **Netzwerk** auf **Internet Protocol Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
6.  Auf der **allgemeine** auf **verwenden Sie die folgende IP-Adresse**, und geben Sie dann die IP-Adresse, die Sie verwenden möchten.  
  
     Ein Standardwert für die Subnetzmaske wird automatisch im der **Subnetzmaske** Feld. Übernehmen Sie den Standardwert, oder geben Sie den Subnetzmaskenwert, den Sie verwenden möchten.  
  
7.  In der **Standardgateway** geben die IP-Adresse des Standardgateways.  
  
8.  In der **Bevorzugter DNS-Server** geben die IP-Adresse Ihres DNS-Servers.  
  
    > [!NOTE]
    >  Verwenden Sie die IP-Adresse, die Ihre Netzwerkadapter von DHCP (z. B. 192.168.X.X) anstatt eines Loopback-Netzwerks (z. B. 127.0.0.1) zugewiesen ist. Um die zugewiesene IP-Adresse herauszufinden, führen **Ipconfig** an einer Eingabeaufforderung.  
  
9. In der **alternativer DNS-Server** geben die IP-Adresse des alternativen DNS-Servers, falls vorhanden.  
  
10. Klicken Sie auf **OK**, und klicken Sie dann auf **schließen**.  
  
> [!IMPORTANT]
>  Stellen Sie sicher, dass Sie den Router für die Weiterleitung der Ports 80 und 443 an die neue statische IP-Adresse des Servers konfigurieren.  
  
##  <a name="BKMK_DNS"></a>Schritt 3: Vorbereiten eines Zertifikats und DNS-Eintrags für den Netzwerkadressenserver  
 Um ein Zertifikat und den DNS-Eintrag für den Netzwerkadressenserver vorzubereiten, müssen führen Sie die folgenden Aufgaben aus:  
  
-   [Schritt 3a: Zuweisen uneingeschränkter Berechtigungen auf authentifizierte Benutzer für die Webserver s-Zertifikatvorlage](#BKMK_GrantFullPermissions)  
  
-   [Schritt 3: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann,](#BKMK_EnrollaCertificate)  
  
-   [Schritt 3c: Hinzufügen eines neues Hosts auf dem DNS-Server und die Windows Server Essentials-Serveradresse zuordnen.](#BKMK_MapNewHosttoServerAddress)  
  
###  <a name="BKMK_GrantFullPermissions"></a>Schritt 3a: Zuweisen uneingeschränkter Berechtigungen auf authentifizierte Benutzer für die Webserver s-Zertifikatvorlage  
 Die erste Aufgabe besteht vollständige Berechtigungen zum Authentifizieren von Benutzern für die Webserver s-Zertifikatvorlage in der Zertifizierungsstelle zu gewähren.  
  
####  <a name="BKMK_ToGrantFullPermissions"></a>Gewähren von uneingeschränkten Berechtigungen an authentifizierte Benutzer für den Webserver s-Zertifikatvorlage  
  
1.  Auf der **starten** geöffnete Seite **Zertifizierungsstelle**.  
  
2.  In der Konsolenstruktur unter **Zertifizierungsstelle (lokal)**, erweitern Sie **< Servername\ >-Zertifizierungsstelle**, mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie dann auf **verwalten**.  
  
3.  In **Zertifizierungsstelle (lokal)**, mit der rechten Maustaste **Webserver**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  In den Eigenschaften der Webserver auf die **Security** auf **authentifizierte Benutzer**, wählen **Vollzugriff**, und klicken Sie dann auf **OK**.  
  
5.  Starten Sie neu **Active Directory-Zertifikatdienste**. Öffnen Sie in der Systemsteuerung **lokale Dienste anzeigen**. In der Liste der Dienste, mit der rechten Maustaste **Active Directory Certificate Services**, und klicken Sie dann auf **neu starten**.  
  
###  <a name="BKMK_EnrollaCertificate"></a>Schritt 3: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann,  
 Anschließend registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann.  
  
####  <a name="BKMK_ToEnrollaCertificate"></a>So registrieren Sie ein Zertifikat für den Netzwerkadressenserver  
  
1.  Auf der **starten** geöffnete Seite **Mmc** (Microsoft Management Console).  
  
2.  Wenn ein **User Account Control** Warnmeldung angezeigt wird, klicken Sie auf **Ja**.  
  
     Die Microsoft Management Console (MMC) wird geöffnet.  
  
3.  Auf der **Datei** Menü klicken Sie auf **hinzufügen/entfernen-Snap-ins**.  
  
4.  In der **hinzufügen oder Remote-Snap-ins** auf **Zertifikate**, und klicken Sie dann auf **hinzufügen**.  
  
5.  Auf der **Zertifikat-Snap-in** auf **Computerkonto**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Computer auswählen** auf **lokalen Computer**, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
7.  Erweitern Sie in der Konsolenstruktur **Zertifikate (lokaler Computer)**, erweitern Sie **persönliche**, mit der rechten Maustaste **Zertifikate**, und klicken Sie dann auf **alle Aufgaben**, klicken Sie auf **neues Zertifikat anfordern**.  
  
8.  Wenn der Zertifikatregistrierungs-Assistent angezeigt wird, klicken Sie auf **Weiter**.  
  
9. Auf der **Zertifikatregistrierungsrichtlinie auswählen** auf **Weiter**.  
  
10. Auf der **Zertifikate anfordern** Seite auf die **Webserver** , und klicken Sie dann auf **zusätzliche Informationen für diese zertifikatsregistrierung benötigt**.  
  
11. In der **Zertifikateigenschaften** Geben Sie die folgenden Einstellungen für **Antragstellername**:  
  
    1.  Für **Typ**Option **allgemeiner Name**.  
  
    2.  Für **Wert**, geben Sie den Namen des Netzwerkadressenservers (z. B. DirectAccess-NLS.contoso.local), und klicken Sie dann auf **hinzufügen**.  
  
    3.  Klicken Sie auf **OK**, und klicken Sie dann auf **registrieren**.  
  
12. Klicken Sie nach Abschluss der Registrierung von Zertifikaten auf **Fertig stellen**.  
  
###  <a name="BKMK_MapNewHosttoServerAddress"></a>Schritt 3c: Hinzufügen eines neues Hosts auf dem DNS-Server und zuordnen, die Windows Server Essentials-Serveradresse  
 Zum Abschließen der DNS-Konfigurations fügen Sie einen neuen Host auf dem DNS-Server und die Windows Server Essentials-Serveradresse zuordnen.  
  
####  <a name="BKMK_ToMapNewHosttoServerAddress"></a>Um einen neuen Host zur Windows Server Essentials-Serveradresse zuzuordnen.  
  
1.  Öffnen Sie auf der Startseite DNS-Manager. Suchen Sie zum Öffnen des DNS-Managers für **dnsmgmt.msc**, und klicken Sie dann auf **dnsmgmt.msc** in den Ergebnissen.  
  
2.  In der Konsolenstruktur des DNS-Manager, erweitern Sie den lokalen Server und **Forward-Lookupzonen**mit der rechten Maustaste auf die Zone mit dem Domänensuffix des Servers, und klicken Sie dann auf **neuer Host (A oder AAAA)**.  
  
3.  Geben Sie den Namen und IP-Adresse des Servers (z. B. DirectAccess-NLS.contoso.local) und die entsprechende Serveradresse (z. B. 192.168.x.x).  
  
4.  Klicken Sie auf **Host hinzufügen**, klicken Sie auf **OK**, und klicken Sie dann auf **Fertig**.  
  
##  <a name="BKMK_AddSecurityGroup"></a>Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Clientcomputer  
 Als Nächstes erstellen Sie eine Sicherheitsgruppe für DirectAccess-Clientcomputer verwenden, und klicken Sie dann fügen Sie die Computerkonten der Gruppe hinzu.  
  
#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>Hinzufügen eine Sicherheitsgruppe für Clientcomputer, die Verwendung von DirectAccess  
  
1.  Klicken Sie auf dem Server-Manager-Dashboard auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**.  
  
    > [!NOTE]
    >  Wenn Sie nicht angezeigt werden **Active Directory-Benutzer und-Computer** auf die **Tools** Menü, müssen Sie das Feature installieren. Um Active Directory-Benutzer und Gruppen zu installieren, führen Sie das folgende Windows PowerShell-Cmdlet als Administrator: `Install-WindowsFeature RSAT-ADDS-Tools`. Weitere Informationen finden Sie unter [installieren oder Entfernen von Remote Server Administration Tools Pack](https://technet.microsoft.com/library/cc730825.aspx).  
  
2.  Erweitern Sie in der Konsolenstruktur den Server, mit der rechten Maustaste **Benutzer**, klicken Sie auf **neu**, und klicken Sie dann auf **Gruppe**.  
  
3.  Geben Sie den Gruppennamen, den Gruppenbereich und Gruppentyp (Erstellen einer Sicherheitsgruppe), und klicken Sie dann auf **OK**.  
  
 Die neue Sicherheitsgruppe wird hinzugefügt, um die **Benutzer** Ordner.  
  
#### <a name="to-add-computer-accounts-to-the-security-group"></a>So fügen Sie Computerkonten zur Sicherheitsgruppe  
  
1.  Klicken Sie auf dem Server-Manager-Dashboard auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**.  
  
2.  In der Konsolenstruktur, erweitern Sie den Server, und klicken Sie dann auf **Benutzer**.  
  
3.  In der Liste der Benutzerkonten und Sicherheitsgruppen auf dem Server, mit der Maustaste der Sicherheitsgruppe, die Sie für DirectAccess erstellt haben, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **Mitglieder** auf **hinzufügen**.  
  
5.  Geben Sie im Dialogfeld die Namen der Computerkonten, die Sie der Gruppe, trennen die Namen durch ein Semikolon (;) hinzufügen möchten. Klicken Sie dann auf **Namen überprüfen**.  
  
6.  Nachdem die Computerkonten überprüft wurden, klicken Sie auf **OK**. Klicken Sie dann auf **OK** erneut.  
  
> [!NOTE]
>  Sie können auch die **Mitglied** Registerkarte in den Eigenschaften eines Computerkontos, das Konto der Sicherheitsgruppe hinzuzufügen.  
  
##  <a name="BKMK_EnableConfigureDA"></a>Schritt 5: Aktivieren und Konfigurieren von DirectAccess  
 Zum Aktivieren und Konfigurieren von DirectAccess in Windows Server Essentials, müssen Sie die folgenden Schritte ausführen:  
  
-   [Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
-   [Schritt 5 b: Entfernen Sie die ungültigen IPv6Prefix im RRAS-Gruppenrichtlinienobjekt (nur Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
-   [Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess](#BKMK_Step4cWindows7Setup)  
  
-   [Schritt 5D: Konfigurieren Sie den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
-   [Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten des IPsec-Kanals](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
###  <a name="BKMK_EnableDA"></a>Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Aktivieren von DirectAccess in Windows Server Essentials. Wenn Sie VPN auf dem Server noch nicht konfiguriert haben, sollten Sie dies tun, bevor Sie mit diesem Verfahren beginnen. Anweisungen finden Sie unter [Verwalten des VPN](Manage-VPN-in-Windows-Server-Essentials.md).  
  
##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>Zum Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole  
  
1.  Öffnen Sie auf der Startseite **Remotezugriffsverwaltung**.  
  
2.  Führen Sie im Assistenten zum Aktivieren von DirectAccess folgende Schritte aus:  
  
    1.  Überprüfung **Voraussetzungen für DirectAccess**, und klicken Sie auf **Weiter**.  
  
    2.  Auf der **Gruppen auswählen** Registerkarte, die Sicherheitsgruppe, die Sie zuvor erstellt, für DirectAccess-Clients haben hinzufügen. (Wenn Sie die Sicherheitsgruppe nicht erstellt haben, finden Sie unter [Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Client Computern](#BKMK_AddSecurityGroup) Anweisungen.)  
  
    3.  Auf der **Gruppen auswählen** auf **Aktivieren von DirectAccess ausschließlich für mobile Computer** Wenn Sie DirectAccess mit der Remotezugriff auf des Servers, und klicken Sie dann auf mobile Computer aktivieren möchten **Weiter**.  
  
    4.  In **Netzwerktopologie**, wählen Sie die Topologie des Servers, und klicken Sie dann auf **Weiter**.  
  
    5.  In **DNS-Suffixsuchliste**, das zusätzliche DNS-Suffix für die Clientcomputer bei Bedarf hinzuzufügen, und klicken Sie dann auf **Weiter**.  
  
        > [!NOTE]
        >  Standardmäßig fügt der Assistent zum Aktivieren von DirectAccess bereits das DNS-Suffix für die aktuelle Domäne hinzu. Allerdings können Sie weitere hinzufügen, falls erforderlich.  
  
    6.  Überprüfen Sie die Gruppenrichtlinienobjekte (GPOs), die angewendet werden, und sie bei Bedarf zu ändern.  
  
    7.  Klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen**.  
  
    8.  Modus mit erhöhten Rechten den folgenden Windows PowerShell-Befehl aus, um den Remotezugriffs-Dienst neu zu starten:  
  
        ```powershell  
        Restart-Service RaMgmtSvc   
        ```  
  
###  <a name="BKMK_RemoveIPv6"></a>Schritt 5 b: Entfernen Sie die ungültigen IPv6Prefix im RRAS-Gruppenrichtlinienobjekt (nur Windows Server Essentials)  
  Dieser Abschnitt gilt für einen Server mit Windows Server Essentials.  
  
 Öffnen Sie Windows PowerShell als Administrator, und führen Sie die folgenden Befehle:  
  
```powershell  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
```  
  
###  <a name="BKMK_Step4cWindows7Setup"></a>Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess  
 Wenn Sie Clientcomputer mit Windows 7 Enterprise haben, führen Sie das folgende Verfahren zum Aktivieren von DirectAccess auf diesen Computern.  
  
##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>So aktivieren Sie Windows 7 Enterprise-Computer für DirectAccess  
  
1.  Öffnen Sie auf der Startseite Server s **Remotezugriffsverwaltung**.  
  
2.  In der Remotezugriffs-Verwaltungskonsole, klicken Sie auf **Konfiguration**. Klicken Sie auf die **Einstellungsdetails** Bereich unter **Schritt2**, klicken Sie auf **bearbeiten**.  
  
     Der Remote Access Server-Setup-Assistent wird geöffnet.  
  
3.  Auf der **Authentifizierung** Registerkarte, und wählen Sie Zertifizierungsstellenzertifikat (CA) an, die das vertrauenswürdige Stammzertifikat werden (Sie können das Zertifizierungsstellenzertifikat des Windows Server Essentials-Servers). Klicken Sie auf **aktivieren Windows 7-Clientcomputer Verbindungen über DirectAccess zulassen**, und klicken Sie dann auf **Weiter**.  
  
4.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
> [!IMPORTANT]
>  Es ist ein bekanntes Problem für Windows 7 Enterprise-Computer, die über DirectAccess eine Verbindung herstellen, wenn die Windows Server Essentials-Server nicht ur1 auf vorinstalliert geliefert wurde. Um DirectAccess-Verbindungen in dieser Umgebung zu aktivieren, müssen Sie die folgenden zusätzlichen Schritte ausführen:  
>   
>  1.  Installieren Sie den Hotfix im beschrieben [Microsoft Knowledge Base-Artikel 2796394](https://support.microsoft.com/kb/2796394) auf dem Windows Server Essentials-Server. Klicken Sie dann starten Sie den Server neu.  
> 2.  Installieren Sie den in beschriebenen Hotfix [Microsoft Knowledge Base-Artikel 2615847](https://support.microsoft.com/kb/2615847) auf jedem Windows 7-Computer.  
>   
>      Dieses Problem wurde in Windows Server Essentials behoben.  
  
###  <a name="BKMK_NLS"></a>Schritt 5D: Konfigurieren Sie den Netzwerkadressenserver  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Konfigurieren der Server netzwerkadresseinstellungen.  
  
> [!NOTE]
>  Bevor Sie beginnen, kopieren Sie den Inhalt des Ordners \inetpub\wwwroot < SystemDrive\ > auf < SystemDrive\ > \Program Files\Windows server\bin\webapps\site\insideoutside%%amp;quot Ordner. Kopieren Sie auch die Datei default.aspx aus dem < SystemDrive\ > \Program Server\Bin\WebApps\Site-Ordner, in den < SystemDrive\ > \Program Files\Windows server\bin\webapps\site\insideoutside%%amp;quot Ordner.  
  
##### <a name="to-configure-the-network-location-server"></a>So konfigurieren Sie den Netzwerkadressenserver  
  
1.  Öffnen Sie auf der Startseite **Remotezugriffsverwaltung**.  
  
2.  In der Remotezugriffs-Verwaltungskonsole, klicken Sie auf **Konfiguration**, und in der **RAS-Setup** Detailbereich **Schritt 3**, klicken Sie auf **bearbeiten**.  
  
3.  In der RAS-Server-Setup-Assistent auf die **Netzwerkadressenserver** Registerkarte **der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt**, und wählen Sie dann das Zertifikat, das zuvor ausgegeben wurde (in [Schritt 3: Vorbereiten eines Zertifikats und DNS-Eintrag für den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)).  
  
4.  Führen Sie die Anweisungen, um den Assistenten abzuschließen, und klicken Sie dann auf **Fertig stellen**.  
  
###  <a name="BKMK_CA"></a>Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten des IPsec-Kanals  
 Im nächste Schritt ist die Konfiguration des Servers, damit die CA-Zertifizierung zu umgehen, wenn ein IPsec-Kanal eingerichtet wird.  
  
##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>Hinzufügen ein Registrierungsschlüssels zur Umgehung der CA-Zertifizierung  
  
1.  Öffnen Sie auf der Startseite **Regedit** (den Registrierungs-Editor).  
  
2.  Erweitern Sie den Registrierungs-Editor **HKEY_LOCAL_MACHINE**, erweitern Sie **System**, erweitern Sie **CurrentControlSet**, erweitern Sie **Dienste**, und erweitern Sie **IKEEXT**.  
  
3.  Klicken Sie unter **IKEEXT**, mit der rechten Maustaste **Parameter**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit) Wert**.  
  
4.  Benennen Sie den neu hinzugefügten Wert zu **Ikeflags**.  
  
5.  Doppelklicken Sie auf **Ikeflags**, legen die **Typ** auf **hexadezimale**, legen Sie den Wert **8000**, und klicken Sie dann auf **OK**.  
  
> [!NOTE]
>  Im Modus mit erhöhten Rechten können den folgenden Windows PowerShell-Befehl Registrierungsschlüssel hinzufügen:  
>   
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`  
  
##  <a name="BKMK_NRPT"></a>Schritt 6: Konfigurieren von Name Resolution Policy Table-Einstellungen für den DirectAccess-server  
 Dieser Abschnitt enthält Anweisungen zum Bearbeiten der Name Resolution Policy Tabelle Schnittstellenadresse Einträge für interne Adressen (z. B. Einträge mit dem Suffix "contoso.Local") für DirectAccess-Client-Gruppenrichtlinienobjekte, und legen Sie dann die IPHTTPS-Schnittstellenadresse.  
  
#### <a name="to-configure-name-resolution-policy-table-entries"></a>So konfigurieren Sie Name Resolution Policy Table-Einträge  
  
1.  Öffnen Sie auf der Startseite **Gruppenrichtlinienverwaltung**.  
  
2.  Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole auf die standardmäßige Gesamtstruktur und Domäne, mit der rechten Maustaste **DirectAccess-Clienteinstellungen**, und klicken Sie dann auf **bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfigurationen**, klicken Sie auf **Richtlinien**, klicken Sie auf **Windows-Einstellungen**, und klicken Sie dann auf **Namensauflösungsrichtlinie**. Wählen Sie den Eintrag, der den Namespace an, die mit Ihrem DNS-Suffix identisch ist, und klicken Sie dann auf **Regel bearbeiten**.  
  
4.  Klicken Sie auf die **DNS-Einstellungen für DirectAccess** Registerkarte; Wählen Sie dann **DNS-Einstellungen aktivieren für DirectAccess in dieser Regel**. Fügen Sie die IPv6-Adresse für die IP-HTTPS-Schnittstelle in der Liste der DNS-Server hinzu.  
  
    > [!NOTE]
    >  Sie können den folgenden Windows PowerShell-Befehl zum Abrufen der IPv6-Adresse verwenden:  
    >   
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`  
  
##  <a name="BKMK_TCPUDP"></a>Schritt 7: Konfigurieren von TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Konfigurieren der TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers.  
  
#### <a name="to-configure-firewall-rules"></a>Konfigurieren von Firewallregeln  
  
1.  Öffnen Sie auf der Startseite **Gruppenrichtlinienverwaltung**.  
  
2.  Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole auf die standardmäßige Gesamtstruktur und Domäne, mit der rechten Maustaste **DirectAccess-servereinstellungen**, und klicken Sie dann auf **bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**, klicken Sie auf **Richtlinien**, klicken Sie auf **Windows-Einstellungen**, klicken Sie auf **Sicherheitseinstellungen**, klicken Sie auf **Windows-Firewall mit erweiterter Sicherheit**, klicken Sie auf die nächste Ebene **Windows-Firewall mit erweiterter Sicherheit**, und klicken Sie dann auf **eingehende Regeln**. Mit der rechten Maustaste **Domänennamenserver (TCP eingehend)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf die **Bereich** Registerkarte und in der **lokale IP-Adresse** aufgelistet, die IPv6-Adresse der IP-HTTPS-Schnittstelle.  
  
5.  Wiederholen Sie dieselbe Verfahren für **Domänennamenserver (UDP eingehend)**.  
  
##  <a name="BKMK_DNS64"></a>Schritt 8: Ändern der DNS64-Konfigurations zum Abhören der IP-HTTPS-Schnittstelle  
 Sie müssen die DNS64-Konfiguration zum Abhören der IP-HTTPS-Schnittstelle mithilfe des folgenden Windows PowerShell-Befehls ändern.  
  
```powershell  
Set-NetDnsTransitionConfiguration  �AcceptInterface IPHTTPSInterface  
```  
  
##  <a name="BKMK_ExemptPort"></a>Schritt 9: Reservieren von Ports für des WinNat-Diensts  
 Verwenden Sie den folgenden Windows PowerShell-Befehl, um Ports für des WinNat-Diensts zu reservieren. Ersetzen Sie "192.168.1.100" durch die tatsächliche IPv4-Adresse des Windows Server Essentials-Servers.  
  
```powershell  
Set-NetNatTransitionConfiguration  �IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
```  
  
> [!IMPORTANT]
>  Um Portkonflikte mit Anwendungen zu vermeiden, achten Sie darauf, dass der Portbereich, den Sie für des WinNat-Diensts zu reservieren nicht Port 6602 enthält.  
  
##  <a name="BKMK_WinNAT"></a>Schritt 10: Neustarten des WinNat-Diensts  
 Mit dem folgenden Windows PowerShell-Befehl, um die Windows NAT-Treiberdienst (WinNat) neu zu starten.  
  
```powershell  
Restart-Service winnat  
```  
  
##  <a name="BKMK_AppendixBPowerShellScript"></a>Anhang: Einrichten von DirectAccess mithilfe von Windows PowerShell  
 Dieser Abschnitt beschreibt die Vorgehensweise zum Einrichten und Konfigurieren von DirectAccess mithilfe von Windows PowerShell.  
  
### <a name="preparation"></a>Vorbereitung  
 Bevor Sie die Konfiguration des Servers für DirectAccess beginnen, müssen Sie folgende Schritte ausführen:  
  
1.  Gehen Sie wie in [Schritt 3: Vorbereiten eines Zertifikats und DNS-Eintrag für den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS) zum Registrieren eines Zertifikats mit dem Namen **DirectAccess-NLS.contoso.com** (wo **"contoso.com"** durch den tatsächlichen internen Domänennamen ersetzt wird), und ein DNS-Eintrags für den Netzwerkadressenserver (NLS) hinzuzufügen.  
  
2.  Hinzufügen einer Sicherheitsgruppe mit dem Namen **DirectAccessClients** in Active Directory, und fügen Sie Clientcomputer für die Sie die DirectAccess-Funktionalität bereitstellen möchten hinzu. Weitere Informationen finden Sie unter [Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Client Computern](#BKMK_AddSecurityGroup).  
  
### <a name="commands"></a>Befehle  
  
> [!IMPORTANT]
>  In Windows Server Essentials müssen Sie sich nicht um das unnötige IPv6-Präfix-Gruppenrichtlinienobjekt zu entfernen. Löschen Sie den Codeabschnitt mit der folgenden Beschriftung: `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`.  
  
```powershell  
# Add Remote Access role if not installed yet  
$ra = Get-WindowsFeature RemoteAccess  
If ($ra.Installed -eq $FALSE) { Add-WindowsFeature RemoteAccess }  
  
# Server may need to restart if you installed RemoteAccess role in the above step  
  
# Set the internet domain name to access server, replace contoso.com below with your own domain name  
$InternetDomain = "www.contoso.com"  
#Set the SG name which you create for DA clients  
$DaSecurityGroup = "DirectAccessClients"  
#Set the internal domain name  
$InternalDomain = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().Name  
  
# Set static IP and DNS settings  
$NetConfig = Get-WmiObject Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true"  
$CurrentIP = $NetConfig.IPAddress[0]  
$SubnetMask = $NetConfig.IPSubnet | Where-Object{$_ -like "*.*.*.*"}  
$NetConfig.EnableStatic($CurrentIP, $SubnetMask)  
$NetConfig.SetGateways($NetConfig.DefaultIPGateway)  
$NetConfig.SetDNSServerSearchOrder($CurrentIP)  
  
# Get physical adapter name and the certificate for NLS server  
$Adapter = (Get-WmiObject -Class Win32_NetworkAdapter -Filter "NetEnabled=$true").NetConnectionId  
$Certs = dir cert:\LocalMachine\My  
$nlscert = $certs | Where-Object{$_.Subject -like "*CN=DirectAccess-NLS*"}  
  
# Add regkey to bypass CA cert for IPsec authentication  
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000  
  
# Install DirectAccess.   
Install-RemoteAccess -NoPrerequisite -DAInstallType FullInstall -InternetInterface $Adapter -InternalInterface $Adapter -ConnectToAddress $InternetDomain -nlscertificate $nlscert -force  
  
#Restart Remote Access Management service  
Restart-Service RaMgmtSvc  
  
# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO   
  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
  
# Enable client computers running Windows 7 to use DirectAccess  
$allcertsinroot = dir cert:\LocalMachine\root  
$rootcert = $allcertsinroot | Where-Object{$_.Subject -like "*-CAA*"}  
Set-DAServer  �IPSecRootCertificate $rootcert[0]  
Set  �DAClient  �OnlyRemoteComputers Disabled -Downlevel Enabled  
  
#Set the appropriate security group used for DA client computers. Replace the group name below with the one you created for DA clients  
Add-DAClient -SecurityGroupNameList $DaSecurityGroup   
Remove-DAClient -SecurityGroupNameList "Domain Computers"  
  
# Gather DNS64 IP address information  
$Remoteaccess = get-remoteaccess  
$IPinterface = get-netipinterface -InterfaceAlias IPHTTPSInterface | get-netipaddress -PrefixLength 128  
$DNS64IP=$IPInterface[1].IPaddress  
$Natconfig = Get-NetNatTransitionConfiguration  
  
# Configure TCP and UDP firewall rules for the DirectAccess server GPO  
$GpoName = 'GPO:'+$InternalDomain+'\DirectAccess Server Settings'  
Get-NetFirewallRule -PolicyStore $GpoName -Displayname "Domain Name Server (TCP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
Get-NetFirewallrule -PolicyStore $GpoName -Displayname "Domain Name Server (UDP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
  
# Configure the name resolution policy settings for the DirectAccess server, replace the DNS suffix below with the one in your domain  
$Suffix = '.' + $InternalDomain  
set-daclientdnsconfiguration -DNSsuffix $Suffix -DNSIPAddress $DNS64IP  
  
# Change the DNS64 configuration to listen to IP-HTTPS interface  
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface  
  
# Copy the necessary files to NLS site folder  
XCOPY 'C:\inetpub\wwwroot' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /E /Y  
XCOPY 'C:\Program Files\Windows Server\Bin\WebApps\Site\Default.aspx' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /Y  
  
# Reserve ports for the WinNat service  
Set-NetNatTransitionConfiguration  �IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
  
# Restart the WinNat service  
Restart-Service winnat  
```  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Zugriff überall](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
