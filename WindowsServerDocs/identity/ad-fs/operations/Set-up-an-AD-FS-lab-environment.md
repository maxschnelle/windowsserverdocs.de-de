---
ms.assetid: 276a7f7d-5faa-4c00-a51c-3fa511fe52f9
title: Einrichten einer AD FS-laborumgebung
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 53d0e24f7fcb9efc64406dc6ed01f5bb1deb2277
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="set-up-an-ad-fs-lab-environment"></a>Einrichten einer AD FS-laborumgebung

>Gilt für: Windows Server 2012 R2

In diesem Thema werden die Schrittezur Konfiguration einer Testumgebung, die verwendet werden können, um die exemplarischen Vorgehensweisen in den folgenden Handbüchern mit exemplarischer Vorgehensweise abzuschließen:  
  
-   [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät](Walkthrough--Workplace-Join-with-an-iOS-Device.md)  
  
-   [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md)  
  
-   [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit Steuerung des bedingten Zugriffs](Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)  
  
-   [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)  
  
> [!NOTE]  
> Wir empfehlen nicht, dass Sie den Webserver und dem Verbundserver auf demselben Computer installieren.  
  
Informationen zum Einrichten dieser Testumgebung führen Sie die folgenden Schritteaus:  
  
1.  [Schritt1: Konfigurieren des Domänencontrollers (DC1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)  
  
2.  [Schritt2: Konfigurieren des Verbundservers (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)  
  
3.  [Schritt3: Konfigurieren des Webservers (WebServ1) und einer anspruchsbasierten beispielanwendung](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)  
  
4.  [Schritt4: Konfigurieren des Clientcomputers (Client1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)  
  
## <a name="BKMK_1"></a>Schritt1: Konfigurieren des Domänencontrollers (DC1)  
Für die Zwecke dieser Testumgebung, rufen Sie die Active Directory-Stammdomäne **contoso.com**, und geben Sie **pass@word1**als Administratorkennwort.  
  
-   Installieren Sie die AD DS-Rollendienst, und installieren Sie Active Directory-Domänendienste (AD DS) auf Ihrem Computer als Domänencontroller unter Windows Server2012 R2 machen. Diese Aktion wird das AD DS-Schema als Teil der domänencontrollererstellung aktualisiert. Weitere Informationen und schrittweise Anleitungen finden Sie unter[https://technet.microsoft.com/library/hh472162.aspx ](https://technet.microsoft.com/library/hh472162.aspx).  
  
### <a name="BKMK_2"></a>Erstellen von Active Directory-Testkonten  
Nachdem der Domänencontroller funktionsfähig ist, können Sie einen Testbenutzer und Testbenutzerkonten Konten in dieser Domäne erstellen und das Benutzerkonto zum Gruppenkonto hinzufügen. Sie verwenden diese Konten, um die exemplarischen Vorgehensweisen in den Handbüchern mit exemplarischer Vorgehensweise abzuschließen, die weiter oben in diesem Thema verwiesen wird.  
  
Erstellen Sie die folgenden Konten:  
  
-   Benutzer: **Robert Hatley** mit den folgenden Anmeldeinformationen: Benutzername: **RobertH** und das Kennwort:**P@ssword**  
  
-   Gruppe: **Finanzen**  
  
Informationen zur Vorgehensweise beim Erstellen von Benutzer- und Gruppenkonten in Active Directory (AD) finden Sie unter [https://technet.microsoft.com/library/cc783323%28V=ws.10%29.aspx ](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx).  
  
Hinzufügen der **Robert Hatley** Konto die **Finanzen** Gruppe. Informationen zum Hinzufügen eines Benutzers zu einer Gruppe in Active Directory finden Sie unter [https://technet.microsoft.com/library/cc737130%28V=ws.10%29.aspx ](https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx).  
  
### <a name="create-a-gmsa-account"></a>Erstellen Sie ein GMSA-Konto  
Das Konto der Gruppe Managed Service Account (GMSA) ist während der Installation der Active Directory-Verbunddienste (AD FS) und Konfiguration erforderlich.  
  
##### <a name="to-create-a-gmsa-account"></a>Zum Erstellen eines GMSA-Kontos  
  
1.  Öffnen Sie eine Windows PowerShell-Befehlsfenster, und geben:  
  
    ```  
    Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)  
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com  
  
    ```  
  
## <a name="BKMK_4"></a>Schritt2: Konfigurieren des Verbundservers (ADFS1) mit Device Registration Service  
Um einen weiteren virtuellen Computer eingerichtet haben, installieren Sie Windows Server2012 R2, und verbinden Sie ihn mit der Domäne **contoso.com**. Richten Sie den Computer, nachdem er der Domäne hinzugefügt haben, und fahren Sie mit der AD FS-Rolle installieren und konfigurieren.  
  
Ein Video hierzu finden Sie unter [Active Directory Federation Services Videoreihe: Installieren einer AD FS-Serverfarm ](https://technet.microsoft.com/video/dn469436).  
  
### <a name="install-a-server-ssl-certificate"></a>Installieren eines SSL-Zertifikats  
Sie müssen ein Serverzertifikat für Secure Socket Layer (SSL) auf dem ADFS1-Server im lokalen Computerspeicher installieren. Das Zertifikat muss die folgenden Attribute aufweisen:  
  
-   Antragstellername (CN): adfs1.contoso.com  
  
-   Alternativer Antragstellername (DNS): adfs1.contoso.com  
  
-   Alternativer Antragstellername (DNS): enterpriseregistration.contoso.com  
  
Weitere Informationen zum Einrichten von SSL-Zertifikaten finden Sie unter [Konfigurieren von SSL/TLS auf einer Website in der Domäne mit einer Unternehmenszertifizierungsstelle ](https://social.technet.microsoft.com/wiki/contents/articles/12485.configure-ssltls-on-a-web-site-in-the-domain-with-an-enterprise-ca.aspx).  
  
[Active Directory-Verbunddienste – Videoreihe: Aktualisieren von Zertifikaten ](https://technet.microsoft.com/video/adfs-updating-certificates).  
  
### <a name="install-the-ad-fs-server-role"></a>Installieren der AD FS-Serverrolle  
  
##### <a name="to-install-the-federation-service-role-service"></a>So installieren Sie den Verbunddienst-Rollendienst  
  
1.  Melden Sie sich bei dem Server mit dem Domänenadministratorkonto administrator@contoso.com.  
  
2.  Starten Sie Server-Manager. Klicken Sie zum Starten des Server-Managers auf **Server-Manager** auf der Windows **starten** Bildschirm, oder klicken Sie auf **Server-Manager** auf der Windows-Taskleiste auf dem Windows-Desktop. Auf der **Quick Start** auf der Registerkarte der **Willkommen** Kachel auf der **Dashboard** auf **Hinzufügen von Rollen und Features **. Alternativ können Sie klicken **Hinzufügen von Rollen und Features** auf die **verwalten** Menü.  
  
3.  Auf der **vor dem Beginn** auf **Weiter**.  
  
4.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, stellen Sie sicher, dass der Zielcomputer ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** auf **Active Directory Federation Services**, und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Features auswählen** auf **Weiter**.  
  
8.  Auf der **Active Directory-Verbunddienste (AD FS)** auf **Weiter **.  
  
9. Nachdem Sie die Informationen auf Überprüfen der **Installationsauswahl bestätigen** Seite auf die **Zielserver bei Bedarf automatisch neu** , und klicken Sie dann auf **installieren**.  
  
10. Auf der **Installationsstatus** Seite, stellen Sie sicher, dass alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **schließen**.  
  
### <a name="configure-the-federation-server"></a>Konfigurieren des Verbundservers  
Im nächste Schrittwird den Verbundserver konfigurieren.  
  
##### <a name="to-configure-the-federation-server"></a>Konfigurieren des Verbundservers  
  
1.  Auf den Server-Manager **Dashboard** auf die **Benachrichtigungen** kennzeichnen, und klicken Sie dann auf **konfigurieren Sie den Verbunddienst auf dem Server**.  
  
    Die **Active Directory Federation Service Konfigurations-Assistenten** wird geöffnet.  
  
2.  Auf der **Willkommen** Seite **Erstellen des ersten Verbundservers in einer Verbundserverfarm**, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **mit AD DS verbinden** Seite, geben Sie ein Konto mit Domänenadministratorrechten für die **contoso.com** Active Directory-Domäne, der dieser Computer angehört, und klicken Sie dann auf **Weiter **.  
  
4.  Auf der **Diensteigenschaften angeben** Seite, gehen Sie folgendermaßen vor, und klicken Sie dann auf **Weiter**:  
  
    -   Importieren Sie das SSL-Zertifikat, das Sie zuvor erhalten haben. Dieses Zertifikat ist das erforderliche dienstauthentifizierungszertifikat. Navigieren Sie zum Speicherort Ihres SSL-Zertifikats.  
  
    -   Geben Sie einen Namen für den Verbunddienst **adfs1.contoso.com**. Dieser Wert ist derselbe Wert, den Sie bereitgestellt werden, wenn Sie ein SSL-Zertifikat in Active Directory-Zertifikatdienste (AD CS) registriert.  
  
    -   Um einen Anzeigenamen für den Verbunddienst anzugeben, geben Sie **Contoso Corporation **.  
  
5.  Auf der **angeben des Dienstkontos** Seite **verwenden Sie ein vorhandenes Domänenbenutzerkonto oder Gruppenverwaltetes Dienstkonto**, und geben Sie dann das GMSA-Konto **Fsgmsa**, dass Sie bei der Erstellung des Domänencontrollers erstellt.  
  
6.  Auf der **angeben der Konfigurationsdatenbank** Seite **erstellen Sie eine Datenbank auf diesem Server mit Windows Internal Database**, und klicken Sie dann auf **Weiter **.  
  
7.  Auf der **Optionen prüfen** Seite, überprüfen Sie Ihre Konfigurationsauswahl, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Voraussetzungsprüfungen** Seite, stellen Sie sicher, dass alle voraussetzungsprüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **konfigurieren **.  
  
9. Auf der **Ergebnisse** Seite, überprüfen Sie die Ergebnisse, überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurde, und klicken Sie dann auf **nächsten Schrittezum Abschließen der Bereitstellung des Verbunddiensts **.  
  
### <a name="configure-device-registration-service"></a>Konfigurieren des Geräteregistrierungsdiensts  
Der nächste Schrittbesteht darin Device Registration Service auf dem ADFS1-Server konfigurieren. Ein Video hierzu finden Sie unter [Active Directory Federation Services Videoreihe: Aktivieren des Geräteregistrierungsdiensts ](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service).  
  
##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>So konfigurieren Sie Device Registration Service für Windows Server2012 RTM  
  
1.  > [!IMPORTANT]  
    > **Der folgende Schrittgilt für die Windows Server2012 R2 RTM Build.**  
  
    Öffnen Sie eine Windows PowerShell-Befehlsfenster, und geben:  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
    Wenn Sie eines Dienstkontos aufgefordert werden, geben Sie **Contosofsgmsa$**.  
  
    Führen Sie jetzt das Windows PowerShell-Cmdlet.  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  Auf dem ADFS1-Server in der **AD FS-Verwaltungs** -Konsole, navigieren Sie zu **Authentifizierungsrichtlinien **. Wählen Sie **globale primäre Authentifizierung bearbeiten **. Aktivieren Sie das Kontrollkästchen neben **Geräteauthentifizierung aktivieren**, und klicken Sie dann auf **OK **.  
  
### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>Hinzufügen von Host-(A) und Alias (CNAME)-Ressourceneinträge in DNS  
Auf DC1 müssen Sie sicherstellen, dass die folgenden Datensätze des Domain Name System (DNS) für den Geräteregistrierungsdienst erstellt werden.  
  
|Eintrag|Typ|Adresse|  
|---------|--------|-----------|  
|adfs1|Host (A)|IP-Adresse des AD FS-Server|  
|enterpriseregistration|Alias (CNAME)|adfs1.contoso.com|  
  
Das folgende Verfahren können DNS-unternehmensnamenservern, für den Verbundserver und Device Registration Service einen Hostressourceneintrag (A) hinzu.  
  
Die Mindestanforderung zum Ausführen dieses Verfahrens ist die Mitgliedschaft in der Gruppe "Administratoren" oder einer ähnlichen. Überprüfen Sie die Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften in den HYPERLINK "https://go.microsoft.com/fwlink/?LinkId=83477" Local and Domain Default Groups (https://go.microsoft.com/fwlink/p/?LinkId=83477).  
  
##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>Um einen Host (A) und Alias (CNAME)-Ressourceneinträge in DNS für Ihren Verbundserver hinzufügen  
  
1.  Auf DC1 im Server-Manager auf den **Tools** Menü klicken Sie auf **DNS** um das DNS-Snap-In zu öffnen.  
  
2.  Erweitern Sie in der Konsolenstruktur DC1, dann **Forward-Lookupzonen**, mit der rechten Maustaste **contoso.com**, und klicken Sie dann auf **neuer Host (A oder AAAA)**.  
  
3.  In **Namen** Geben Sie den Namen, die Sie für Ihre AD FS-Farm verwenden möchten. Geben Sie in dieser exemplarischen Vorgehensweise **adfs1**.  
  
4.  In **IP-Adresse**, geben Sie die IP-Adresse des ADFS1-Servers. Klicken Sie auf **Host hinzufügen**.  
  
5.  Mit der rechten Maustaste **contoso.com**, und klicken Sie dann auf **neuer Alias (CNAME)**.  
  
6.  In der **neuer Ressourcendatensatz** , geben Sie im Dialogfeld **Enterpriseregistration** in der **Aliasnamen** Feld.  
  
7.  Geben Sie in der vollständig qualifizierten Domänennamen (FQDN) des Felds Host Ziel, **adfs1.contoso.com**, und klicken Sie dann auf **OK **.  
  
    > [!IMPORTANT]  
    > Wenn Ihr Unternehmen mehrere Suffixe für Benutzerprinzipalnamen (UPN), verfügt, müssen Sie in einer realen Bereitstellung mehrere CNAME-Datensätze, jeweils einen für die UPN-Suffixe in DNS erstellen.  
  
## <a name="BKMK_5"></a>Schritt3: Konfigurieren des Webservers (WebServ1) und einer anspruchsbasierten beispielanwendung  
Richten Sie einen virtuellen Computer (WebServ1), indem Sie die Installation des Betriebssystems Windows Server2012 R2, und verbinden Sie ihn mit der Domäne **contoso.com**. Nachdem sie der Domäne angehört, können Sie zum Installieren und Konfigurieren der Webserverrolle fortfahren.  
  
Zum Abschließen der exemplarischen Vorgehensweise, die weiter oben in diesem Thema aufgeführten benötigen Sie eine beispielanwendung, die von Ihrem Verbundserver (ADFS1) gesichert ist.  
  
Sie können Windows Identity Foundation SDK herunterladen ([https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451), das eine anspruchsbasierte beispielanwendung enthält.  
  
Sie müssen die folgenden Schritteaus, um einen Webserver mit dieser anspruchsbasierten beispielanwendung einzurichten.  
  
> [!NOTE]  
> Diese Schrittewurden auf einem Webserver getestet, die das Betriebssystem Windows Server2012 R2 ausgeführt wird.  
  
1.  [Installieren der Webserverrolle und Windows Identity Foundation](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)  
  
2.  [Installieren von Windows Identity Foundation SDK](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)  
  
3.  [Konfigurieren der einfachen anspruchsanwendung in IIS](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)  
  
4.  [Erstellen einer Vertrauensstellung der vertrauenden Seite auf dem Verbundserver](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)  
  
### <a name="BKMK_15"></a>Installieren der Webserverrolle und Windows Identity Foundation  
  
1.  > [!NOTE]  
    > Sie müssen Zugriff auf die Windows Server2012 R2-Installationsmedien haben.  
  
    Melden Sie sich bei WebServ1 mit **administrator@contoso.com**und das Kennwort **pass@word1**.  
  
2.  Server-Manager auf den **Quick Start** auf der Registerkarte der **Willkommen** Kachel auf der **Dashboard** auf **Hinzufügen von Rollen und Features **. Alternativ können Sie klicken **Hinzufügen von Rollen und Features** auf die **verwalten** Menü.  
  
3.  Auf der **vor dem Beginn** auf **Weiter**.  
  
4.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, stellen Sie sicher, dass der Zielcomputer ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** Seite, aktivieren Sie das Kontrollkästchen neben **Webserver (IIS)**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter **.  
  
7.  Auf der **Features auswählen** Seite **Windows Identity Foundation 3.5**, und klicken Sie dann auf **Weiter **.  
  
8.  Auf der **Webserverrolle (IIS)** auf **Weiter**.  
  
9. Auf der **Rollendienste auswählen** Seite aus, und erweitern **Anwendungsentwicklung **. Wählen Sie **ASP.NET 3.5**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter **.  
  
10. Auf der **Installationsauswahl bestätigen** auf **alternativen Quellpfad angeben **. Geben Sie den Pfad zum Sxs-Verzeichnis, das sich auf den Windows Server2012 R2-Installationsmedien befindet. Beispielsweise D:SourcesSxs. Klicken Sie auf **OK**, und klicken Sie dann auf **installieren **.  
  
### <a name="BKMK_13"></a>Installieren von Windows Identity Foundation SDK  
  
1.  Führen Sie WindowsIdentityFoundation-SDK-3.5.msi aus, um Windows Identity Foundation SDK 3.5 (https://www.microsoft.com/download/details.aspx?id=4451) installieren. Wählen Sie alle Standardoptionen.  
  
### <a name="BKMK_9"></a>Konfigurieren der einfachen anspruchsanwendung in IIS  
  
1.  Installieren Sie ein gültiges SSL-Zertifikat im Zertifikatspeicher Computers. Das Zertifikat sollte enthalten den Namen Ihres Webservers **webserv1.contoso.com **.  
  
2.  Kopieren Sie den Inhalt des c: Dateien (x86) Windows Identity Foundation SDKv3.5SamplesQuick StartWeb ApplicationpassiveRedirectBasedClaimsAwareWebApp in C:InetpubClaimapp.  
  
3.  Bearbeiten der **Default.aspx.cs** Datei, damit keine anspruchsfilterung stattfindet. Dieser Schrittwird ausgeführt, um sicherzustellen, dass die beispielanwendung alle Ansprüche anzeigt, die vom Verbundserver ausgestellt werden. Führen Sie die folgenden:  
  
    1.  Öffnen **Default.aspx.cs** in einem Text-Editor.  
  
    2.  Durchsuchen Sie die Datei für die zweite Instanz des `ExpectedClaims`.  
  
    3.  Kommentieren Sie die gesamte `IF` -Anweisung und ihre Klammern. Geben Sie Kommentare eingeben "/ /" (ohne Anführungszeichen) an den Anfang einer Zeile.  
  
    4.  Ihre `FOREACH` -Anweisung sollte jetzt wie in diesem Codebeispiel aussehen.  
  
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
  
    5.  Speichern und schließen Sie **Default.aspx.cs **.  
  
    6.  Öffnen **"Web.config"** in einem Text-Editor.  
  
    7.  Entfernen Sie den gesamten `<microsoft.identityModel>`Abschnitt. Entfernen Sie alles ab `including <microsoft.identityModel>`und bis zu und einschließlich `</microsoft.identityModel>`.  
  
    8.  Speichern und schließen Sie **"Web.config"**.  
  
4.  **Konfigurieren von IIS-Manager**  
  
    1.  Öffnen **Internetinformation Services (IIS)-Manager **.  
  
    2.  Wechseln Sie zu **Anwendungspools**, mit der rechten Maustaste **DefaultAppPool** auswählen **Erweiterte Einstellungen **. Legen Sie **Benutzerprofil laden** auf **True**, und klicken Sie dann auf **OK **.  
  
    3.  Mit der rechten Maustaste **DefaultAppPool** auswählen **Grundeinstellungen **. Ändern der **.NET CLR-Version** auf **.NET CLR Version v2.0.50727**.  
  
    4.  Mit der rechten Maustaste **Standardwebsite** auswählen **Bindungen bearbeiten **.  
  
    5.  Hinzufügen einer **HTTPS** -Bindung zu Port **443** mit dem SSL-Zertifikat, das Sie installiert haben.  
  
    6.  Mit der rechten Maustaste **Standardwebsite** auswählen **Anwendung hinzufügen **.  
  
    7.  Legen Sie den Alias auf **Claimapp** und den physischen Pfad auf **C:inetpubclaimapp**.  
  
5.  So konfigurieren Sie **Claimapp** um mit dem Verbundserver arbeiten, gehen Sie folgendermaßen vor:  
  
    1.  Ausführung von FedUtil.exe, die sich im befindet **c: Dateien (x86) Windows Identity Foundation SDKv3.5**.  
  
    2.  Legen Sie den Speicherort der Anwendungskonfiguration auf **C:inetputclaimappweb.config** und den Anwendungs-URI auf die URL Ihrer Website **https://webserv1.contoso.com /claimapp/**. Klicken Sie auf **Weiter**.  
  
    3.  Wählen Sie **vorhandenen STS verwenden**, und navigieren Sie zur Metadaten-URL Ihres AD FS-Servers **https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml **. Klicken Sie auf **Weiter**.  
  
    4.  Wählen Sie **Überprüfung der Zertifikatkette deaktivieren**, und klicken Sie dann auf **Weiter **.  
  
    5.  Wählen Sie **keine Verschlüsselung**, und klicken Sie dann auf **Weiter **. Auf der **angebotene Ansprüche** auf **Weiter **.  
  
    6.  Aktivieren Sie das Kontrollkästchen neben **Planen einer Aufgabe zum Ausführen täglicher Updates von WS-Federation-Metadaten **. Klicken Sie auf **Fertig stellen**.  
  
    7.  Ihre beispielanwendung ist jetzt konfiguriert. Wenn Sie die URL der Anwendung testen **https://webserv1.contoso.com/claimapp**, sollten sie Sie zu Ihrem Verbundserver umleiten. Der Verbundserver sollte eine Fehlerseite anzeigen, da Sie nicht die Vertrauensstellung der vertrauenden Seite konfiguriert haben. Anders ausgedrückt, haben Sie diese testanwendung von AD FS nicht gesichert.  
  
Sie müssen jetzt Ihre beispielanwendung sichern, die auf dem Webserver mit AD FS ausgeführt wird. Hierzu können Sie eine Vertrauensstellung der vertrauenden Seite auf Ihrem Verbundserver (ADFS1) hinzufügen. Ein Video hierzu finden Sie unter [Active Directory Federation Services Videoreihe: Hinzufügen einer der vertrauenden Seite Vertrauensstellung](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust).  
  
### <a name="BKMK_11"></a>Erstellen einer Vertrauensstellung der vertrauenden Seite auf dem Verbundserver  
  
1.  Auf Ihrem Verbundserver (ADFS1) in der **AD FS-Verwaltungskonsole**, navigieren Sie zu **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf **Party Vertrauensstellung der vertrauenden Seite hinzufügen **.  
  
2.  Auf der **Auswählen einer Datenquelle** Seite **online oder in einem lokalen Netzwerk veröffentlichte Daten über die vertrauende Seite importieren**, geben Sie die Metadaten-URL für **Claimapp**, und klicken Sie dann auf **Weiter **. Ausführung von FedUtil.exe erstellt eine XML-Datei mit Metadaten. Es befindet sich unter   
    **https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml**.  
  
3.  Auf der **Anzeigenamen angeben** geben die **Anzeigename** für Ihre Vertrauensstellung für vertrauende Seiten, **Claimapp**, und klicken Sie dann auf **Weiter **.  
  
4.  Auf der **jetzt mehrstufige Authentifizierung konfigurieren? **Seite **ich möchte nicht Multi-Factor Authentication für diese Vertrauensstellung der vertrauenden Seite zu diesem Zeitpunkt angeben**, und klicken Sie dann auf **Weiter **.  
  
5.  Auf der **auswählen von Ausstellungsautorisierungsregeln** Seite **allen Benutzern Zugriff auf diese vertrauende**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter**.  
  
7.  Auf der **Anspruchsregeln bearbeiten** Dialogfeld, klicken Sie auf **Regel hinzufügen**.  
  
8.  Auf der **Auswählen eines Regeltyps** Seite **Senden von Ansprüchen mit benutzerdefinierter Regel**, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Anspruchsregel konfigurieren** Seite der **Name der Anspruchsregel** geben **alle Ansprüche**. In der **benutzerdefinierte Regel** Geben Sie die folgende Anspruchsregel.  
  
    ```  
    c:[ ]  
    => issue(claim = c);  
  
    ```  
  
10. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
## <a name="BKMK_10"></a>Schritt4: Konfigurieren des Clientcomputers (Client1)  
Richten Sie einen weiteren virtuellen Computer, und installieren Sie Windows8.1. Diese virtuelle Maschine muss sich im selben virtuellen Netzwerk wie die anderen Computer. Dieser Computer sollte nicht zur Contoso-Domäne hinzugefügt werden.  
  
Der Client muss das SSL-Zertifikat, das für den Verbundserver (ADFS1) verwendet wird, im eingerichtet vertrauen [Schritt2: Konfigurieren des Verbundservers (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4). Sie müssen auch Zertifikatsperrinformationen für das Zertifikat validieren können.  
  
Sie müssen auch einrichten und verwenden ein Microsoft-Konto, sich an Client1 anzumelden.  
  
## <a name="see-also"></a>Siehe auch  
[Active Directory Federation Services Videoreihe: Installieren einer AD FS-Serverfarm](https://technet.microsoft.com/video/dn469436)  
[Active Directory-Verbunddienste – Videoreihe: Aktualisieren von Zertifikaten](https://technet.microsoft.com/video/adfs-updating-certificates)  
[Active Directory Federation Services Videoreihe: Hinzufügen einer Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust)  
[Active Directory-Verbunddienste – Videoreihe: Aktivieren des Geräteregistrierungsdiensts](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service)  
[Active Directory-Verbunddienste – Videoreihe: Installieren the Web Application Proxy](https://technet.microsoft.com/video/dn469438)  
  
