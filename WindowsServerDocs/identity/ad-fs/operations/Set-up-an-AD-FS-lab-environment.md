---
ms.assetid: 276a7f7d-5faa-4c00-a51c-3fa511fe52f9
title: Einrichten einer AD FS-Laborumgebung
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 53d0e24f7fcb9efc64406dc6ed01f5bb1deb2277
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868081"
---
# <a name="set-up-an-ad-fs-lab-environment"></a>Einrichten einer AD FS-Laborumgebung

>Gilt für: Windows Server 2012 R2

In diesem Thema sind die Schritte für die Konfiguration einer Testumgebung aufgeführt, die für das Abschließen der explemplarischen Vorgehensweisen in den folgenden Handbüchern mit exemplarischer Vorgehensweise verwendet werden können:  
  
-   [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät](Walkthrough--Workplace-Join-with-an-iOS-Device.md)  
  
-   [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md)  
  
-   [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit der bedingten Zugriffssteuerung](Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)  
  
-   [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)  
  
> [!NOTE]  
> Sie sollten den Webserver und den Verbundserver nicht auf demselben Computer installieren.  
  
Führen Sie zum Einrichten dieser Testumgebung die folgenden Schritte durch:  
  
1.  [Schritt 1: Konfigurieren des Domänencontrollers (DC1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)  
  
2.  [Schritt 2: Konfigurieren des Verbundservers (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)  
  
3.  [Schritt 3: Konfigurieren des Webservers (WebServ1) und eine anspruchsbasierte beispielanwendung](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)  
  
4.  [Schritt 4: Konfigurieren des Clientcomputers (Client1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)  
  
## <a name="BKMK_1"></a>Schritt 1: Konfigurieren des Domänencontrollers (DC1)  
Für die Zwecke dieser testumgebung, können Sie die Active Directory-Stammdomäne Aufrufen **"contoso.com"** , und geben Sie **pass@word1** als Administratorkennwort.  
  
-   Installieren Sie die AD DS-Rollendienst, und installieren Sie Active Directory Domain Services (AD DS) auf Ihrem Computer einen Domänencontroller in Windows Server 2012 R2 vornehmen. Diese Aktion wird das AD DS-Schema als Teil der domänencontrollererstellung aktualisiert. Weitere Informationen und schrittweise Anleitungen finden Sie unter[ https://technet.microsoft.com/ Library/hh472162.aspx](https://technet.microsoft.com/library/hh472162.aspx).  
  
### <a name="BKMK_2"></a>Erstellen von Active Directory-Testkonten  
Nachdem der Domänencontroller funktionsfähig ist, können Sie eine Testgruppe und Testbenutzerkonten in dieser Domäne erstellen und das Benutzerkonto zum Gruppenkonto hinzufügen. Sie verwenden diese Konten, um die exemplarischen Vorgehensweisen in den Handbüchern mit exemplarischer Vorgehensweise abzuschließen, die zu Beginn dieses Themas aufgeführt sind.  
  
Erstellen Sie die folgenden Konten:  
  
-   Benutzer: **Robert Hatley** mit den folgenden Anmeldeinformationen: Benutzername: **RobertH** und das Kennwort: **P@ssword**  
  
-   Gruppe: **Finanzen**  
  
Weitere Informationen über das Erstellen von Benutzer- und Gruppenkonten in Active Directory (AD) finden Sie unter [ https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx ](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx).  
  
Fügen Sie das Konto **Robert Hatley** zur Gruppe **Finance** hinzu. Weitere Informationen zum Hinzufügen eines Benutzers zu einer Gruppe in Active Directory, finden Sie unter [ https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx ](https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx).  
  
### <a name="create-a-gmsa-account"></a>Erstellen eines GMSA-Kontos  
Das Gruppenkonto für Managed Service Account (GMSA) ist während der Installation der Active Directory-Verbunddienste (AD FS) und die Konfiguration erforderlich.  
  
##### <a name="to-create-a-gmsa-account"></a>So erstellen Sie ein GMSA-Konto  
  
1.  Öffnen Sie ein Windows PowerShell-Befehlsfenster, und geben Sie Folgendes ein:  
  
    ```  
    Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)  
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com  
  
    ```  
  
## <a name="BKMK_4"></a>Schritt 2: Konfigurieren des Verbundservers (ADFS1) mit dem Geräteregistrierungsdienst  
Um einen weiteren virtuellen Computer einzurichten, installieren Sie Windows Server 2012 R2, und verbinden es mit der Domäne **"contoso.com"**. Richten Sie den Computer, nachdem er der Domäne hinzugefügt haben, und klicken Sie dann zum Installieren und konfigurieren die AD FS-Serverrolle fortfahren.  
  
Ein Video hierzu finden Sie unter [Active Directory Federation Services Videoreihe mit exemplarischer Vorgehensweise: Installieren einer AD FS-Serverfarm](https://technet.microsoft.com/video/dn469436).  
  
### <a name="install-a-server-ssl-certificate"></a>Installieren eines SSL-Zertifikats  
Sie müssen ein Secure Socket Layer (SSL)-Serverzertifikat auf dem ADFS1-Server im lokalen Computerspeicher installieren. Das Zertifikat MUSS über die folgenden Attribute verfügen:  
  
-   Antragstellername (CN): adfs1.contoso.com  
  
-   Alternativer Antragstellername (DNS): adfs1.contoso.com  
  
-   Alternativer Antragstellername (DNS): enterpriseregistration.contoso.com  
  
Weitere Informationen zum Einrichten von SSL-Zertifikaten finden Sie unter [Configure SSL/TLS on a Web site in the domain with an Enterprise CA](https://social.technet.microsoft.com/wiki/contents/articles/12485.configure-ssltls-on-a-web-site-in-the-domain-with-an-enterprise-ca.aspx).  
  
[Active Directory-Verbunddienste Videoreihe mit exemplarischer Vorgehensweise: Aktualisieren von Zertifikaten](https://technet.microsoft.com/video/adfs-updating-certificates).  
  
### <a name="install-the-ad-fs-server-role"></a>Installieren der AD FS-Serverrolle  
  
##### <a name="to-install-the-federation-service-role-service"></a>So installieren Sie den Verbunddienst-Rollendienst  
  
1.  Melden Sie sich bei dem Server mithilfe des Domänenadministratorkontos administrator@contoso.com.  
  
2.  Starten Sie den Server-Manager. Klicken Sie zum Starten des Server-Managers auf dem Windows- **Startbildschirm** auf **Server-Manager** , oder klicken Sie in der Windows-Taskleiste auf dem Windows-Desktop auf **Server-Manager** . Klicken Sie auf der Seite **Dashboard** auf der Kachel **Willkommen** in der Registerkarte **Schnellstart** auf **Rollen und Features hinzufügen**. Alternativ können Sie im Menü **Verwalten** auf **Rollen und Features hinzufügen** klicken.  
  
3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  
  
5.  Klicken Sie auf der Seite  **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, überprüfen Sie, ob der Zielcomputer ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Verbunddienste**, und klicken Sie dann auf **Weiter**.  
  
7.  Klicken Sie auf der Seite **Features auswählen** auf **Weiter**.  
  
8.  Klicken Sie auf der Seite **Active Directory-Verbunddienst (AD FS)** auf **Weiter**.  
  
9. Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** überprüft haben, aktivieren Sie das Kontrollkästchen **Zielserver bei Bedarf automatisch neu starten** , und klicken Sie dann auf **Installieren**.  
  
10. Überprüfen Sie auf der Seite **Installationsfortschritt** , ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.  
  
### <a name="configure-the-federation-server"></a>Konfigurieren des Verbundservers  
Der nächste Schritt ist die Konfiguration des Verbundservers.  
  
##### <a name="to-configure-the-federation-server"></a>So konfigurieren Sie den Verbundserver  
  
1.  Klicken Sie auf der Seite **Dashboard** im Server-Manager auf das Kennzeichen **Benachrichtigungen** , und klicken Sie dann auf **Verbunddienst auf den Server konfigurieren**.  
  
    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Willkommen****Erstellen des ersten Verbundservers in einer Verbundserverfarm**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **Verbinden mit AD DS** ein Konto mit Domänenadministratorrechten für die Active Directory-Domäne **contoso.com** an, der dieser Computer angehört, und klicken Sie dann auf **Weiter**.  
  
4.  Führen Sie auf der Seite **Diensteigenschaften angeben** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Importieren Sie das SSL-Zertifikat, das Sie zuvor erhalten haben. Dieses Zertifikat ist das erforderliche Dienstauthentifizierungszertifikat. Navigieren Sie zum Speicherort Ihres SSL-Zertifikats.  
  
    -   Zum Bereitstellen eines Namens für Ihren Verbunddienst geben Sie **adfs1.contoso.com** ein. Das ist derselbe Wert, den Sie beim Registrieren eines SSL-Zertifikats bei den Active Directory-Zertifikatdiensten (AD CS) angegeben haben.  
  
    -   Geben Sie als Anzeigenamen für den Verbunddienst **Contoso Corporation**ein.  
  
5.  Wählen Sie auf der Seite **Dienstkonto angeben** die Option **Vorhandenes Domänenbenutzerkonto oder gruppenverwaltetes Dienstkonto verwenden**aus, und geben Sie dann das GMSA-Konto **fsgmsa** an, das Sie beim Erstellen des Domänencontrollers erstellt haben.  
  
6.  Wählen Sie auf der Seite **Angeben der Konfigurationsdatenbank** die Option **Erstellen einer Datenbank auf diesem Server mit der internen Windows-Datenbank**aus, und klicken Sie dann auf **Weiter**.  
  
7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen** , und klicken Sie dann auf **Weiter**.  
  
8.  Überprüfen Sie auf der Seite **Voraussetzungsprüfungen** , ob alle Voraussetzungsprüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Konfigurieren**.  
  
9. Überprüfen Sie die Ergebnisse auf der Seite **Ergebnisse** , prüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Weitere Schritte, die zum Abschluss der Bereitstellung des Verbunddiensts erforderlich sind**.  
  
### <a name="configure-device-registration-service"></a>Konfigurieren des Geräteregistrierungsdiensts  
Der nächste Schritt ist die Konfiguration des Geräteregistrierungsdiensts auf dem ADFS1-Server. Ein Video hierzu finden Sie unter [Active Directory Federation Services Videoreihe mit exemplarischer Vorgehensweise: Aktivieren des Geräteregistrierungsdiensts](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service).  
  
##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>So konfigurieren Sie den Geräteregistrierungsdienst für Windows Server 2012 RTM  
  
1.  > [!IMPORTANT]  
    > **Der folgende Schritt gilt für den Windows Server 2012 R2 RTM Build.**  
  
    Öffnen Sie ein Windows PowerShell-Befehlsfenster, und geben Sie Folgendes ein:  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
    Wenn Sie eines Dienstkontos aufgefordert werden, geben Sie **Contosofsgmsa$**.  
  
    Führen Sie jetzt das Windows PowerShell-Cmdlet.  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  Navigieren Sie auf dem ADFS1-Server in der **AD FS-Verwaltungskonsole** zu **Authentifizierungsrichtlinien**. Wählen Sie **Globale primäre Authentifizierung bearbeiten**aus. Aktivieren Sie das Kontrollkästchen neben **Geräteauthentifizierung aktivieren**, und klicken Sie dann auf **OK**.  
  
### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>Hinzufügen von Host- (A) und Aliasressourcendatensätzen (CNAME) zu DNS  
Auf DC1 müssen Sie sicherstellen, dass die folgenden DNS-Datensätze für den Geräteregistrierungsdienst erstellt werden.  
  
|Eingabe|Typ|Adresse|  
|---------|--------|-----------|  
|adfs1|Host (A)|IP-Adresse des AD FS-server|  
|enterpriseregistration|Alias (CNAME)|adfs1.contoso.com|  
  
Sie können wie folgt vorgehen, um einen Hostressourcendatensatz (A) zu DNS-Unternehmensnamenservern für den Verbundserver und den Geräteregistrierungsdienst hinzuzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe Administratoren oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren ausführen können. Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften finden Sie in der HYPERLINK "https://go.microsoft.com/fwlink/?LinkId=83477" Local and Domain Default Groups (https://go.microsoft.com/fwlink/p/?LinkId=83477).  
  
##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>So fügen Sie einen Host (A) und Aliasressourcendatensätze (CNAME) zu DNS für Ihren Verbundserver hinzu  
  
1.  Klicken Sie auf DC1 im Server-Manager im Menü **Extrax** auf **DNS**, um das DNS-Snap-In zu öffnen.  
  
2.  Erweitern Sie in der Konsolenstruktur DC1 und **Forward-Lookupzonen**, klicken Sie mit der rechten Maustaste auf **contoso.com**, und klicken Sie dann auf **Neuer Host (A oder AAAA)**.  
  
3.  Geben Sie unter **Name** den gewünschten Namen für Ihre AD FS-Farm ein. Geben Sie für diese exemplarische Vorgehensweise **adfs1**ein.  
  
4.  Geben Sie im Feld **IP-Adresse**die IP-Adresse des ADFS1-Servers ein. Klicken Sie auf **Host hinzufügen**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **contoso.com**, und klicken Sie dann auf **Neuer Alias (CNAME)**.  
  
6.  Geben Sie im Dialogfeld **Neuer Ressourcendatensatz****enterpriseregistration** in das Feld **Aliasname** ein.  
  
7.  Geben Sie das Feld für den vollqualifizierten Domänennamen (FQDN) auf dem Zielhost **adfs1.contoso.com** ein, und klicken Sie dann auf **OK**.  
  
    > [!IMPORTANT]  
    > Wenn Ihr Unternehmen in einer realen Bereitstellung über mehrere Benutzerprinzipalnamen-Suffixe (User Principal Name, UPN) verfügt, müssen Sie mehrere CNAME-Datensätze erstellen, jeweils einen für die UPN-Suffixe in DNS.  
  
## <a name="BKMK_5"></a>Schritt 3: Konfigurieren des Webservers (WebServ1) und einer ansprchsbasierten Beispielanwendung  
Richten Sie einen virtuellen Computer (WebServ1) ein, indem Sie die Installation des Betriebssystems Windows Server 2012 R2, und verbinden es mit der Domäne **"contoso.com"**. Nachdem der Computer der Domäne hinzugefügt ist, können Sie mit der Installation und Konfiguration der Webserverrolle fortfahren.  
  
Zum Abschließen der zu Beginn dieses Themas aufgeführten exemplarischen Vorgehensweisen müssen Sie eine Beispielanwendung haben, die von Ihrem Verbundserver (ADFS1) gesichert wird.  
  
Sie können Windows Identity Foundation SDK ([https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451), das eine anspruchsbasierte beispielanwendung enthält.  
  
Sie müssen die folgenden Schritte durchführen, um einen Webserver mit dieser anspruchsbasierten Beispielanwendung einzurichten.  
  
> [!NOTE]  
> Diese Schritte wurden auf einem Webserver getestet, die das Betriebssystem Windows Server 2012 R2 ausgeführt wird.  
  
1.  [Installieren der Webserverrolle und die Windows Identity Foundation](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)  
  
2.  [Install Windows Identity Foundation SDK](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)  
  
3.  [Konfigurieren der einfachen anspruchsanwendung in IIS](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)  
  
4.  [Erstellen Sie eine Vertrauensstellung der vertrauenden Seite, auf dem Verbundserver](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)  
  
### <a name="BKMK_15"></a>Installieren Sie die Rolle "Webserver" und Windows Identity Foundation  
  
1.  > [!NOTE]  
    > Benötigen Sie Zugriff auf die Windows Server 2012 R2-Installationsmedien an.  
  
    Melden Sie sich bei WebServ1 mit **administrator@contoso.com** und das Kennwort **pass@word1**.  
  
2.  Klicken Sie im Server-Manager auf der Seite **Dashboard** auf der Kachel **Willkommen** in der Registerkarte **Schnellstart** auf **Rollen und Features hinzufügen**. Alternativ können Sie im Menü **Verwalten** auf **Rollen und Features hinzufügen** klicken.  
  
3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  
  
5.  Klicken Sie auf der Seite  **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, überprüfen Sie, ob der Zielcomputer ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
6.  Aktivieren Sie auf der Seite **Serverrollen auswählen** das Kontrollkästchen neben **Webserver (IIS)**, und klicken Sie auf **Features hinzufügen**und dann auf **Weiter**.  
  
7.  Wählen Sie auf der Seite **Features auswählen** die Option **Windows Identity Foundation 3.5** aus, und klicken Sie dann auf **Weiter**.  
  
8.  Klicken Sie auf der Seite **Webserverrolle (IIS)** auf **Weiter**.  
  
9. Wählen Sie auf der Seite **Rollendienste auswählen****Anwendungsentwicklung** aus, und erweitern Sie die Option. Wählen Sie **ASP.NET 3.5**aus, und klicken Sie auf **Features hinzufügen**und dann auf **Weiter**.  
  
10. Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Alternativen Quellpfad angeben**. Geben Sie den Pfad zum Sxs-Verzeichnis, das in den Windows Server 2012 R2-Installationsmedien befindet. Beispiel: D:SourcesSxs. Klicken Sie auf **OK**und dann auf **Installieren**.  
  
### <a name="BKMK_13"></a>Installieren Sie Windows Identity Foundation-SDK  
  
1.  Führen Sie WindowsIdentityFoundation-SDK-3.5.msi aus, um Windows Identity Foundation SDK 3.5 zu installieren (https://www.microsoft.com/download/details.aspx?id=4451). Wählen Sie alle Standardoptionen aus.  
  
### <a name="BKMK_9"></a>Konfigurieren der einfachen anspruchsanwendung in IIS  
  
1.  Installieren Sie ein gültiges SSL-Zertifikat im Zertifikatspeicher des Computers. Das Zertifikat sollte den Namen Ihres Webservers, **webserv1.contoso.com**, enthalten.  
  
2.  Kopieren Sie den Inhalt der c: Dateien (x86) Windows Identity Foundation SDKv3.5SamplesQuick StartWeb ApplicationPassiveRedirectBasedClaimsAwareWebApp in C:InetpubClaimapp an.  
  
3.  Bearbeiten Sie die Datei **Default.aspx.cs** , damit keine Anspruchsfilterung stattfindet. Mit diesem Schritt wird sichergestellt, dass die Beispielanwendung alle Ansprüche anzeigt, die vom Verbundserver ausgegeben werden. Gehen Sie wie folgt vor:  
  
    1.  Öffnen Sie **Default.aspx.cs** in einem Text-Editor.  
  
    2.  Durchsuchen Sie die Datei nach der zweiten Instanz von `ExpectedClaims`.  
  
    3.  Kommentieren Sie die gesamte `IF` -Anweisung einschließlich der Klammern aus. Weisen Sie auf Kommentare hin, indem Sie am Anfang einer Zeile „//“ eingeben (ohne Anführungszeichen).  
  
    4.  Ihre `FOREACH` -Anweisung sollte jetzt wie im folgenden Codebeispiel aussehen.  
  
        ```  
        Foreach (claim claim in claimsIdentity.Claims)  
        {  
           //Before showing the claims validate that this is an expected claim  
           //If it is not in the expected claims list then don’t show it  
           //if (ExpectedClaims.Contains( claim.ClaimType ) )  
           // {  
              writeClaim( claim, table );  
           //}  
        }  
  
        ```  
  
    5.  Speichern und schließen Sie **Default.aspx.cs**.  
  
    6.  Öffenen Sie **web.config** in einem Text-Editor.  
  
    7.  Entfernen Sie den gesamten Abschnitt `<microsoft.identityModel>` . Entfernen Sie alles ab `including <microsoft.identityModel>` bis einschließlich `</microsoft.identityModel>`.  
  
    8.  Speichern und schließen Sie **web.config**.  
  
4.  **Konfigurieren von IIS-Manager**  
  
    1.  Öffnen Sie **Internetinformationsdienste-Manager (IIS)**.  
  
    2.  Navigieren Sie zu **Anwendungspools**, und klicken Sie mit der rechten Maustasge auf **DefaultAppPool**, um **Erweiterte Einstellungen** auszuwählen. Setzen Sie **Benutzerprofil laden** auf **True**, und klicken Sie dann auf **OK**.  
  
    3.  Klicken Sie mit der rechten Maustaste auf **DefaultAppPool** , um **Grundeinstellungen**auszuwählen. Ändern Sie **.NET CLR-Version** in **.NET CLR Version v2.0.50727**.  
  
    4.  Klicken Sie mit der rechten Maustaste auf **Standardwebsite** , um **Bindungen bearbeiten**auszuwählen.  
  
    5.  Fügen Sie eine **HTTPS**-Bindung zu Port **443** mit dem von Ihnen installierten SSL-Zertifikat hinzu.  
  
    6.  Klicken Sie mit der rechten Maustaste auf **Standardwebsite**, um **Anwendung hinzufügen** auszuwählen.  
  
    7.  Legen Sie den Alias zu **Claimapp** und den physischen Pfad zur **C:inetpubclaimapp**.  
  
5.  Gehen Sie wie folgt vor, um **claimapp** für die Zusammenarbeit mit Ihrem Verbundserver zu konfigurieren:  
  
    1.  Führen Sie FedUtil.exe, die sich im befindet **c: Dateien (x86) Windows Identity Foundation SDKv3.5**.  
  
    2.  Legen Sie den Speicherort der Anwendungskonfiguration auf **C:inetputclaimappweb.config** und legen Sie den Anwendungs-URI, an die URL für Ihre Website  **https://webserv1.contoso.com /claimapp /**. Klicken Sie auf **Weiter**.  
  
    3.  Wählen Sie **vorhandenen STS verwenden** , und navigieren Sie zur Metadaten-URL Ihres AD FS-Servers **https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml**. Klicken Sie auf **Weiter**.  
  
    4.  Wählen Sie **Überprüfung der Zertifikatkette deaktivieren**aus, und klicken Sie dann auf **Weiter**.  
  
    5.  Wählen Sie **Keine Verschlüsselung**aus, und klicken Sie auf **Weiter**. Klicken Sie auf der Seite **Angebotene Ansprüche** auf **Weiter**.  
  
    6.  Aktivieren Sie das Kontrollkästchen neben **Planen einer Aufgabe zur Durchführung täglicher WS-Verbundmetadatenupdates**. Klicken Sie auf **Fertig stellen**.  
  
    7.  Ihre Beispielanwendung ist jetzt konfiguriert. Wenn Sie die Anwendungs-URL testen **https://webserv1.contoso.com/claimapp**, es soll Sie zu Ihrem Verbundserver umleiten. Der Verbundserver sollte eine Fehlerseite anzeigen, da Sie die Vertrauensstellung der vertrauenden Seite noch nicht konfiguriert haben. Das heißt, müssen Sie diese testanwendung von AD FS nicht gesichert.  
  
Sie müssen jetzt Ihre beispielanwendung sichern, die auf dem Webserver mit AD FS ausgeführt wird. Dies erreichen Sie, indem Sie eine Vertrauensstellung der vertrauenden Seite auf Ihrem Verbundserver (ADFS1) hinzufügen. Ein Video hierzu finden Sie unter [Active Directory Federation Services Videoreihe mit exemplarischer Vorgehensweise: Hinzufügen einer Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust).  
  
### <a name="BKMK_11"></a>Erstellen Sie eine Vertrauensstellung der vertrauenden Seite, auf dem Verbundserver  
  
1.  Navigieren Sie auf Ihrem Verbundserver (ADFS1) in der **AD FS-Verwaltungskonsole** zu **Vertrauensstellungen der vertrauenden Seite**, und klicken Sie dann auf **Vertrauensstellung der vertrauenden Seite hinzufügen**.  
  
2.  Wählen Sie auf der Seite **Auswählen einer Datenquelle** die Option **Online oder in einem lokalen Netzwerk veröffentlichte Daten über die vertrauende Seite importieren**aus, geben Sie die Metadaten-URL für **claimapp**ein, und klicken Sie dann auf **Weiter**. Bei der Ausführung von FedUtil.exe wurde eine Metadaten-XML-Datei erstellt. Sie befindet sich unter   
    **https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml**.  
  
3.  Geben Sie auf der Seite **Anzeigenamen angeben** den **Anzeigenamen** für Ihre Vertrauensstellung der vertrauenden Seite ( **claimapp**) an, und klicken Sie dann auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Jetzt mehrstufige Authentifizierung konfigurieren?** die Option **Ich möchte jetzt keine mehrstufige Authentifizierungseinstellung für diese Vertrauensstellung der vertrauenden Seite angeben**, und klicken Sie auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Auswählen von Ausstellungsautorisierungsregeln** die Option **Allen Benutzern Zugriff auf diese vertrauende Seite gewähren**, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter**.  
  
7.  Klicken Sie im Dialogfeld **Anspruchsregeln bearbeiten** auf **Regel hinzufügen**.  
  
8.  Wählen Sie auf der Seite **Auswählen eines Regeltyps** die Option **Senden von Ansprüchen mit benutzerdefinierter Regel**aus, und klicken Sie dann auf **Weiter**.  
  
9. Geben Sie auf der Seite **Konfigurieren einer Anspruchsregel** in das Feld **Name der Anspruchsregel****All Claims** ein. Geben Sie im Feld **Benutzerdefinierte Regel** die folgende Anspruchsregel ein.  
  
    ```  
    c:[ ]  
    => issue(claim = c);  
  
    ```  
  
10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
## <a name="BKMK_10"></a>Schritt 4: Konfigurieren des Clientcomputers (Client1)  
Richten Sie einen anderen virtuellen Computer aus, und installieren Sie Windows 8.1. Dieser virtuelle Computer muss sich im selben virtuellen Netzwerk befinden wie die anderen Computer. Dieser Computer sollte NICHT zur Contoso-Domäne hinzugefügt werden.  
  
Der Client muss das SSL-Zertifikat, das für den Verbundserver (ADFS1), die Sie verwendet wird in einrichten vertrauen [Schritt2: Konfigurieren des Verbundservers (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4). Darüber hinaus muss er die Zertifikatsperrinformationen für das Zertifikat validieren können.  
  
Sie müssen außerdem ein Microsoft-Konto einrichten und verwenden, um sich bei Client1 anzumelden.  
  
## <a name="see-also"></a>Siehe auch  
[Active Directory-Verbunddienste Videoreihe mit exemplarischer Vorgehensweise: Installieren einer AD FS-Serverfarm](https://technet.microsoft.com/video/dn469436)  
[Active Directory-Verbunddienste Videoreihe mit exemplarischer Vorgehensweise: Aktualisieren von Zertifikaten](https://technet.microsoft.com/video/adfs-updating-certificates)  
[Active Directory-Verbunddienste Videoreihe mit exemplarischer Vorgehensweise: Hinzufügen einer Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust)  
[Active Directory-Verbunddienste Videoreihe mit exemplarischer Vorgehensweise: Aktivieren des Geräteregistrierungsdiensts](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service)  
[Active Directory-Verbunddienste Videoreihe mit exemplarischer Vorgehensweise: Installieren des Webanwendungsproxys](https://technet.microsoft.com/video/dn469438)  
  
