---
title: Konfigurieren des Zertifikatregistrierungs-Webdiensts ür die Zertifikatschlüssel-basierte Erneuerung an einem benutzerdefinierten Port
author: Deland-Han
ms.author: delhan
manager: dcscontentpm
ms.date: 11/12/2019
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: 5b2da1858a7f0a3669accfdb2dda88a23f64edc0
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964252"
---
# <a name="configuring-certificate-enrollment-web-service-for-certificate-key-based-renewal-on-a-custom-port"></a>Konfigurieren des Zertifikatregistrierungs-Webdiensts ür die Zertifikatschlüssel-basierte Erneuerung an einem benutzerdefinierten Port

> Autoren: Jitesh Thakur, Meera muhideen, Technical Advisors bei der Windows-Gruppe.
Ankit Tyagi-Support Techniker mit der Windows-Gruppe

## <a name="summary"></a>Zusammenfassung

Dieser Artikel enthält Schritt-für-Schritt-Anleitungen zum Implementieren der Zertifikatregistrierungsrichtlinien-Webdienst (CEP) und Zertifikatregistrierungs-Webdienst (CES) an einem anderen benutzerdefinierten Port als 443 für die Zertifikat Schlüssel basierte Erneuerung, um das Feature für die automatische Erneuerung von CEP und CES zu nutzen.

In diesem Artikel wird auch erläutert, wie CEP und CES funktionieren, und es werden Setup Richtlinien bereitstellt.

> [!Note]
> Der in diesem Artikel enthaltene Workflow gilt für ein bestimmtes Szenario. Der gleiche Workflow funktioniert möglicherweise nicht für eine andere Situation. Die Prinzipien bleiben jedoch unverändert.
>
> Haftungsausschluss: dieses Setup wird für eine bestimmte Anforderung erstellt, bei der Sie Port 443 für die HTTPS-Standardkommunikation für CEP-und CES-Server nicht verwenden möchten. Obwohl diese Einrichtung möglich ist, ist die unter Stütz barkeit eingeschränkt. Kundendienste und Support können Ihnen am besten helfen, wenn Sie dieses Handbuch sorgfältig verwenden, indem Sie die minimale Abweichung von der bereitgestellten Webserver Konfiguration verwenden.

## <a name="scenario"></a>Szenario

In diesem Beispiel basieren die Anweisungen auf einer Umgebung, in der die folgende Konfiguration verwendet wird:

- Eine contoso.com-Gesamtstruktur, die über eine Public Key-Infrastruktur (PKI) für die Active Directory-Zertifikat Dienste (AD CS) verfügt.

- Zwei CEP/CES-Instanzen, die auf einem Server konfiguriert werden, der unter einem Dienst Konto ausgeführt wird. Eine Instanz verwendet Benutzername und Kennwort für die anfängliche Registrierung. Der andere verwendet die Zertifikat basierte Authentifizierung für die Schlüssel basierte Erneuerung im Erneuerungs Modus.

- Ein Benutzer verfügt über einen Arbeitsgruppen Computer oder einen Computer, der nicht Mitglied einer Domäne ist, für den er das Computer Zertifikat mithilfe von Anmelde Informationen für Benutzername und Kennwort anmelden soll.

- Die Verbindung zwischen dem Benutzer und CEP und CES über HTTPS erfolgt an einem benutzerdefinierten Port, z. b. 49999. (Dieser Port ist aus einem dynamischen Port Bereich ausgewählt und wird von keinem anderen Dienst als statischer Port verwendet.)

- Wenn die Gültigkeitsdauer des Zertifikats bald erreicht ist, verwendet der Computer die Zertifikat basierte, auf dem Zertifikat basierende Schlüssel basierte Erneuerung zum Erneuern des Zertifikats über denselben Kanal.

![deployment](media/certificate-enrollment-certificate-key-based-renewal-1.png)

## <a name="configuration-instructions"></a>Konfigurationsanweisungen

### <a name="overview"></a>Übersicht 

1. Konfigurieren Sie die Vorlage für die Schlüssel basierte Erneuerung.

2. Konfigurieren Sie als Voraussetzung einen CEP-und CES-Server für die Authentifizierung mit Benutzername und Kennwort.   
   In dieser Umgebung wird die Instanz als "CEPCES01" bezeichnet.

3.  Konfigurieren Sie eine andere CEP-und CES-Instanz mithilfe von PowerShell für die Zertifikat basierte Authentifizierung auf demselben Server. Die CES-Instanz verwendet ein Dienst Konto.

    In dieser Umgebung wird die Instanz als "CEPCES02" bezeichnet. Das verwendete Dienst Konto ist "cepcessvc".

4.  Konfigurieren Sie Client seitige Einstellungen.

### <a name="configuration"></a>Konfiguration

Dieser Abschnitt enthält die Schritte zum Konfigurieren der anfänglichen Registrierung.

> [!Note]
> Sie können auch ein beliebiges Benutzer Dienst Konto, MSA oder GMSA konfigurieren, damit CES funktioniert.

Als Voraussetzung müssen Sie CEP und CES auf einem Server konfigurieren, indem Sie die Benutzernamen-und Kenn Wort Authentifizierung verwenden.

#### <a name="configure-the-template-for-key-based-renewal"></a>Konfigurieren der Vorlage für die Schlüssel basierte Erneuerung

Sie können eine vorhandene Computer Vorlage duplizieren und die folgenden Einstellungen der Vorlage konfigurieren:

1. Vergewissern Sie sich, dass auf der Registerkarte "Antragsteller Name" der Zertifikat Vorlage die Optionen für die Anforderung und die Verwendung von **Antrags** Teller **Informationen aus vorhandenen Zertifikaten für die automatische Registrierung von Erneuerungs Anforderungen** ausgewählt sind.
   ![Neue Vorlagen](media/certificate-enrollment-certificate-key-based-renewal-2.png) 

2. Wechseln Sie zur Registerkarte Ausstellungs **Anforderungen** , und aktivieren Sie dann das Kontrollkästchen Zertifizierungsstellen- **Zertifikat-Manager-Genehmigung** .
   ![Ausstellungs Anforderungen](media/certificate-enrollment-certificate-key-based-renewal-3.png) 

3. Weisen Sie dem **cepcessvc** -Dienst Konto für diese Vorlage die Berechtigungen **Lesen** und **registrieren** zu.

4. Veröffentlichen Sie die neue Vorlage auf der Zertifizierungsstelle.

> [!Note]
> Stellen Sie sicher, dass die Kompatibilitäts Einstellungen für die Vorlage auf **Windows Server 2012 R2** festgelegt sind, da ein bekanntes Problem vorliegt, bei dem die Vorlagen nicht sichtbar sind, wenn die Kompatibilität auf Windows Server 2016 oder eine höhere Version festgelegt ist. Weitere Informationen finden [Sie unter kann keine mit Windows Server 2016 ZS kompatiblen Zertifikat Vorlagen von Windows Server 2016 oder höher basierten CAS oder CEP-Servern auswählen ](https://support.microsoft.com/en-in/help/4508802/cannot-select-certificate-templates-in-windows-server-2016).


#### <a name="configure-the-cepces01-instance"></a>Konfigurieren der CEPCES01-Instanz

##### <a name="step-1-install-the-instance"></a>Schritt 1: Installieren der Instanz

Verwenden Sie eine der folgenden Methoden, um die CEPCES01-Instanz zu installieren.

**Methode 1:**

In den folgenden Artikeln finden Sie eine Schritt-für-Schritt-Anleitung zum Aktivieren von CEP und CES für die Benutzernamen-und Kenn Wort Authentifizierung:

[Leitfaden Zertifikatregistrierungsrichtlinien-Webdienst](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831625(v=ws.11))

[Leitfaden Zertifikatregistrierungs-Webdienst](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831822(v=ws.11)#configure-a-ca-for-the-certificate-enrollment-web-service)

> [!Note]
> Stellen Sie sicher, dass Sie die Option "Schlüssel basierte Verlängerung aktivieren" nicht auswählen, wenn Sie sowohl die CEP-als auch die CES-Instanz von Benutzernamen-und Kenn Wort Authentifizierung konfigurieren.

**Methode 2:**

Sie können die folgenden PowerShell-Cmdlets verwenden, um die CEP-und CES-Instanzen zu installieren:

```PowerShell
Import-Module ServerManager
Add-WindowsFeature Adcs-Enroll-Web-Pol
Add-WindowsFeature Adcs-Enroll-Web-Svc
```

```PowerShell
Install-AdcsEnrollmentPolicyWebService -AuthenticationType Username -SSLCertThumbprint "sslCertThumbPrint"
```

Dieser Befehl installiert die Zertifikatregistrierungsrichtlinien-Webdienst (CEP), indem angegeben wird, dass ein Benutzername und ein Kennwort für die Authentifizierung verwendet werden. 

> [!Note]
> In diesem Befehl \<**SSLCertThumbPrint**\> ist der Fingerabdruck des Zertifikats, das zum Binden von IIS verwendet wird.

```PowerShell
Install-AdcsEnrollmentWebService -ApplicationPoolIdentity -CAConfig "CA1.contoso.com\contoso-CA1-CA" -SSLCertThumbprint "sslCertThumbPrint" -AuthenticationType Username
```

Mit diesem Befehl werden die Zertifikatregistrierungs-Webdienst (CES) installiert, um die Zertifizierungsstelle für den Computernamen CA1.contoso.com und den allgemeinen Namen der Zertifizierungsstelle von "" von " **CA1.contoso.com** " zu **verwenden.** Die Identität der CES ist als standardmäßige Anwendungs Pool Identität angegeben. Der Authentifizierungstyp ist " **username**". Sslcertthumbprint ist der Fingerabdruck des Zertifikats, das zum Binden von IIS verwendet wird.

##### <a name="step-2-check-the-internet-information-services-iis-manager-console"></a>Schritt 2 Überprüfen der Internetinformationsdienste (IIS)-Manager-Konsole

Nach einer erfolgreichen Installation erwarten Sie, dass die folgende Anzeige in der Internetinformationsdienste (IIS)-Manager-Konsole angezeigt wird.
![IIS-Manager](media/certificate-enrollment-certificate-key-based-renewal-4.png) 

Wählen Sie unter **Standard Website**die Option **ADPolicyProvider_CEP_UsernamePassword**aus, und öffnen Sie dann **Anwendungseinstellungen**. Notieren Sie sich die **ID** und den **URI**.

Sie können einen anzeigen **Amen** für die Verwaltung hinzufügen.

#### <a name="configure-the-cepces02-instance"></a>Konfigurieren der CEPCES02-Instanz

##### <a name="step-1-install-the-cep-and-ces-for-key-based-renewal-on-the-same-server"></a>Schritt 1: Installieren Sie das CEP und die CES für die Schlüssel basierte Erneuerung auf demselben Server. 

Führen Sie den folgenden Befehl in PowerShell aus:

```PowerShell
Install-AdcsEnrollmentPolicyWebService -AuthenticationType Certificate -SSLCertThumbprint "sslCertThumbPrint" -KeyBasedRenewal
```

Mit diesem Befehl wird die Zertifikatregistrierungsrichtlinien-Webdienst (CEP) installiert, und es wird angegeben, dass ein Zertifikat für die Authentifizierung verwendet wird. 

> [!Note]
> In diesem Befehl \<SSLCertThumbPrint\> ist der Fingerabdruck des Zertifikats, das zum Binden von IIS verwendet wird. 

Bei der Schlüssel basierten Erneuerung können Zertifikat Clients ihre Zertifikate erneuern, indem Sie den Schlüssel des vorhandenen Zertifikats für die Authentifizierung verwenden. Im Schlüssel basierten Erneuerungs Modus gibt der Dienst nur Zertifikat Vorlagen zurück, die für die Schlüssel basierte Erneuerung festgelegt sind.

```PowerShell
Install-AdcsEnrollmentWebService -CAConfig "CA1.contoso.com\contoso-CA1-CA" -SSLCertThumbprint "sslCertThumbPrint" -AuthenticationType Certificate -ServiceAccountName "Contoso\cepcessvc" -ServiceAccountPassword (read-host "Set user password" -assecurestring) -RenewalOnly -AllowKeyBasedRenewal
```

Mit diesem Befehl werden die Zertifikatregistrierungs-Webdienst (CES) installiert, um die Zertifizierungsstelle für den Computernamen CA1.contoso.com und den allgemeinen Namen der Zertifizierungsstelle von "" von " **CA1.contoso.com** " zu **verwenden.** 

In diesem Befehl wird die Identität des Zertifikatregistrierungs-Webdienst als **cepcessvc** -Dienst Konto angegeben. Der Authentifizierungstyp ist " **Certificate**". **Sslcertthumbprint** ist der Fingerabdruck des Zertifikats, das zum Binden von IIS verwendet wird.

Mit dem " **renewalonly** "-Cmdlet können Sie im Modus "nur erneuern" ausgeführt werden. Das **allowkeybasedrenewal** -Cmdlet gibt auch an, dass die CES Schlüssel basierte Erneuerungs Anforderungen für den Anmeldungsserver akzeptieren. Dabei handelt es sich um gültige Client Zertifikate für die Authentifizierung, die nicht direkt einem Sicherheits Prinzipal zugeordnet werden.

> [!Note]
> Das Dienst Konto muss Teil der **iisusers** -Gruppe auf dem Server sein.

##### <a name="step-2-check-the-iis-manager-console"></a>Schritt 2 Überprüfen der IIS-Manager-Konsole

Nach einer erfolgreichen Installation erwarten Sie, dass die folgende Anzeige in der IIS-Manager-Konsole angezeigt wird.
![IIS-Manager](media/certificate-enrollment-certificate-key-based-renewal-5.png) 

Wählen Sie **KeyBasedRenewal_ADPolicyProvider_CEP_Certificate** unter **Standard Website** aus, und öffnen Sie **Anwendungseinstellungen**. Notieren Sie sich die **ID** und den **URI**. Sie können einen anzeigen **Amen** für die Verwaltung hinzufügen.

> [!Note]
> Wenn die Instanz auf einem neuen Server installiert ist, überprüfen Sie die ID, um sicherzustellen, dass es sich bei der ID um dieselbe ID handelt, die in der CEPCES01-Instanz generiert wurde. Sie können den Wert direkt kopieren und einfügen, wenn er anders ist.

#### <a name="complete-certificate-enrollment-web-services-configuration"></a>Vervollständigen der Konfiguration der Webdienste für die Zertifikat Registrierung

Um das Zertifikat im Auftrag der CEP-und CES-Funktionalität registrieren zu können, müssen Sie das Computer Konto der Arbeitsgruppe in Active Directory konfigurieren und dann die eingeschränkte Delegierung für das Dienst Konto konfigurieren.

##### <a name="step-1-create-a-computer-account-of-the-workgroup-computer-in-active-directory"></a>Schritt 1: Erstellen eines Computer Kontos des Arbeitsgruppen Computers in Active Directory

Dieses Konto wird für die Authentifizierung bei der Schlüssel basierten Erneuerung und für die Option "in Active Directory veröffentlichen" in der Zertifikat Vorlage verwendet.

> [!Note]
> Der Client Computer muss nicht in die Domäne eingebunden werden. Dieses Konto wird bei der Zertifikat basierten Authentifizierung in KBR für dsmapper-Dienst angezeigt.

![Neues Objekt](media/certificate-enrollment-certificate-key-based-renewal-6.png) 
 
##### <a name="step-2-configure-the-service-account-for-constrained-delegation-s4u2self"></a>Schritt 2: Konfigurieren des Dienst Kontos für die eingeschränkte Delegierung (S4U2Self)

Führen Sie den folgenden PowerShell-Befehl aus, um die eingeschränkte Delegierung (S4U2Self oder beliebiges Authentifizierungsprotokoll) zu aktivieren

```PowerShell
Get-ADUser -Identity cepcessvc | Set-ADAccountControl -TrustedToAuthForDelegation $True
Set-ADUser -Identity cepcessvc -Add @{'msDS-AllowedToDelegateTo'=@('HOST/CA1.contoso.com','RPCSS/CA1.contoso.com')}
```

> [!Note]
> In diesem Befehl \<cepcessvc\> ist das Dienst Konto, und <CA1.contoso.com >ist die Zertifizierungsstelle.

> [!Important]
> Wir aktivieren das Flag "renewalonbehalof" für die Zertifizierungsstelle in dieser Konfiguration nicht, da wir die eingeschränkte Delegierung verwenden, um den gleichen Auftrag für uns durchzuführen. Dadurch wird verhindert, dass die Berechtigung für das Dienst Konto zur Sicherheit der Zertifizierungsstelle hinzugefügt wird.

##### <a name="step-3-configure-a-custom-port-on-the-iis-web-server"></a>Schritt 3: Konfigurieren eines benutzerdefinierten Ports auf dem IIS-Webserver

1. Wählen Sie in der IIS-Manager-Konsole die Option Standard Website aus.

2. Wählen Sie im Aktionsbereich die Option Site Bindung bearbeiten aus. 

3. Ändern Sie die Standard Port Einstellung von 443 in Ihren benutzerdefinierten Port. Der Beispiel Bildschirm zeigt die Port Einstellung 49999.
   ![Port ändern](media/certificate-enrollment-certificate-key-based-renewal-7.png) 

##### <a name="step-4-edit-the-ca-enrollment-services-object-on-active-directory"></a>Schritt 4: Bearbeiten des Objekts der Zertifizierungsstellen-Registrierungsdienste auf Active Directory

1. Öffnen Sie auf einem Domänen Controller ADSIEdit. msc.

2. Stellen Sie eine [Verbindung mit der Konfigurations Partition](/previous-versions/windows/it-pro/windows-server-2003/ff730188(v=ws.10))her, und navigieren Sie zu Ihrem Zertifizierungsstellen-Registrierungsdienst Objekt:
   
   CN = entca, CN = Registrierungsdienste, CN = Public Key Services, CN = Services, CN = Configuration, DC = ca. DC = com

3. Klicken Sie mit der rechten Maustaste, und bearbeiten Sie das Objekt Ändern Sie das **mspki-** Anmeldungs Server-Attribut, indem Sie den benutzerdefinierten Port mit ihren CEP-und CES-Server-URIs verwenden, die in den Anwendungseinstellungen gefunden wurden. Beispiel:

   ```
   140https://cepces.contoso.com:49999/ENTCA_CES_UsernamePassword/service.svc/CES0   
   181https://cepces.contoso.com:49999/ENTCA_CES_Certificate/service.svc/CES1
   ```
   
   ![ADSI-Editor](media/certificate-enrollment-certificate-key-based-renewal-8.png) 

#### <a name="configure-the-client-computer"></a>Konfigurieren des Clientcomputers

Richten Sie auf dem Client Computer die Registrierungsrichtlinien und die Richtlinie für die automatische Registrierung ein. Gehen Sie hierzu wie folgt vor:

1. Wählen Sie **Start**  >  **Ausführen**aus, und geben Sie dann **gpeer dit. msc**ein.

2. Wechseln Sie zu **Computer Konfiguration**  >  **Windows-Einstellungen**  >  **Sicherheitseinstellungen**, und klicken Sie dann auf **Richtlinien für öffentliche Schlüssel**.

3. Aktivieren Sie die **Richtlinie Zertifikat Dienst Client-automatische** Registrierung, um die Einstellungen im folgenden Screenshot zu erfüllen.
   ![Zertifikat Gruppenrichtlinie](media/certificate-enrollment-certificate-key-based-renewal-9.png)
 
4. Aktivieren Sie **Zertifikat Dienste Client-Zertifikat Registrierungs Richtlinie**.

   a) Klicken Sie auf **Hinzufügen** , um die Registrierungs Richtlinie hinzuzufügen, und geben Sie den CEP-URI mit **UserNamePassword** ein, den wir in ADSI
   
   b) Wählen Sie als **Authentifizierungstyp** **Benutzername/Kennwort**aus.
   
   c. Legen Sie die Priorität **10**fest, und überprüfen Sie dann den Richtlinien Server.
      ![Registrierungs Richtlinie](media/certificate-enrollment-certificate-key-based-renewal-10.png)

   > [!Note]
   > Stellen Sie sicher, dass die Portnummer zum URI hinzugefügt und für die Firewall zulässig ist.

5. Registrieren Sie das erste Zertifikat für den Computer über "certlm. msc".
   ![Registrierungs Richtlinie](media/certificate-enrollment-certificate-key-based-renewal-11.png)

   Wählen Sie die KBR-Vorlage aus, und registrieren Sie das Zertifikat.
   ![Registrierungs Richtlinie](media/certificate-enrollment-certificate-key-based-renewal-12.png)

6. Öffnen Sie " **gpeer dit. msc** " erneut. Bearbeiten Sie die **Richtlinie Zertifikat Dienst Client – Zertifikat Registrierungs Richtlinie**, und fügen Sie dann die Registrierungs Richtlinie für die Schlüssel basierte Erneuerung hinzu:

   a) Klicken Sie auf **Hinzufügen**, und geben Sie den CEP-URI mit dem in ADSI bearbeiteten **Zertifikat** ein. 
   
   b) Legen Sie eine Priorität von **1**fest, und überprüfen Sie dann den Richtlinien Server. Sie werden aufgefordert, sich zu authentifizieren und das von uns zuerst registrierte Zertifikat auszuwählen.

   ![Registrierungs Richtlinie](media/certificate-enrollment-certificate-key-based-renewal-13.png) 

> [!Note]
> Stellen Sie sicher, dass der Prioritätswert der Registrierungs Richtlinie für Schlüssel basierte Erneuerung niedriger ist als die Priorität der Richtlinien Priorität für die Kenn Wort Registrierung. Die erste Einstellung wird der niedrigsten Priorität zugewiesen.

## <a name="testing-the-setup"></a>Testen des Setups

Um sicherzustellen, dass die automatische Verlängerung funktioniert, überprüfen Sie, ob die manuelle Verlängerung funktioniert, indem Sie das Zertifikat mit dem gleichen Schlüssel mithilfe von MMC erneuern. Außerdem sollten Sie aufgefordert werden, ein Zertifikat während der Erneuerung auszuwählen. Sie können das zuvor registrierte Zertifikat auswählen. Die Eingabeaufforderung wird erwartet.

Öffnen Sie den persönlichen Zertifikat Speicher des Computers, und fügen Sie die Ansicht "Archivierte Zertifikate" hinzu. Fügen Sie dazu das Snap-in "Lokales Computer Konto" zu mmc.exe hinzu, **Markieren Sie** **Zertifikate (lokaler Computer)** , indem Sie darauf klicken, klicken Sie auf der **Registerkarte Aktion** rechts oder oben auf MMC, klicken Sie auf **Optionen anzeigen**, wählen Sie **Archivierte Zertifikate**aus, und klicken Sie dann auf **OK**.

### <a name="method-1"></a>Methode 1 

Führen Sie den folgenden Befehl aus:

```PowerShell
certreq -machine -q -enroll -cert <thumbprint> renew
```

![-Befehl.](media/certificate-enrollment-certificate-key-based-renewal-14.png)

### <a name="method-2"></a>Methode 2

Verschieben Sie das Datum und die Uhrzeit auf dem Client Computer in die Erneuerungszeit der Zertifikat Vorlage.

Die Zertifikat Vorlage verfügt beispielsweise über eine Einstellung von 2 Tagen und eine Einstellung für die Verlängerung von 8 Stunden. Das Beispiel Zertifikat wurde um 4:00 Uhr ausgegeben. am 18. Tag des Monats läuft um 4:00 Uhr am 20. Die Engine für die automatische Registrierung wird bei einem Neustart und bei jeweils 8 Stunden (ungefähr) ausgelöst.

Wenn Sie also die Zeit auf 8:10 Uhr verschieben. am 19. Nachdem das Erneuerungs Fenster in der Vorlage auf 8 Stunden festgelegt wurde, wird das Zertifikat durch Ausführen von certutil-Pulse (zum auslöst der AE-Engine) für Sie registriert.

![-Befehl.](media/certificate-enrollment-certificate-key-based-renewal-15.png)
 
Nachdem der Test abgeschlossen ist, setzen Sie die Zeiteinstellung auf den ursprünglichen Wert zurück, und starten Sie den Client Computer neu.

> [!Note]
> Der vorherige Screenshot zeigt, dass die automatische Registrierungs-Engine erwartungsgemäß funktioniert, da das Datum der Zertifizierungsstelle weiterhin auf den 18. Wert festgelegt ist. Aus diesem Grund werden weiterhin Zertifikate ausgestellt. In einer realen Situation tritt diese große Menge von Erneuerungen nicht auf.

## <a name="references"></a>References

[Test Lab Guide: Demonstrating Certificate Key-Based Renewal](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj590165(v%3dws.11))

[Zertifikatregistrierungs-Webdienste](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/Certificate-Enrollment-Web-Services/ba-p/397385)

[Install-adcsenrollmentpolicywebservice](/powershell/module/adcsdeployment/install-adcsenrollmentpolicywebservice?view=win10-ps)

[Install-adcsenrollmentwebservice](/powershell/module/adcsdeployment/install-adcsenrollmentwebservice?view=win10-ps)

Weitere Informationen

[Windows Server-Sicherheitsforum](https://aka.ms/adcsforum)

[Häufig gestellte Fragen (FAQs) zur Public Key-Infrastruktur (PKI) der Active Directory-Zertifikatdienste (AD CS)](https://aka.ms/adcsfaq)

[Windows PKI-Dokumentationsreferenz und -Bibliothek](https://social.technet.microsoft.com/wiki/contents/articles/987.windows-pki-documentation-reference-and-library.aspx)

[Windows PKI-Blog](/archive/blogs/pki/)

[Konfigurieren der eingeschränkten Kerberos-Delegierung (S4U2Proxy oder Kerberos) für ein benutzerdefiniertes Dienst Konto für Webanmeldungs-Proxy Seiten](https://support.microsoft.com/help/4494313/configuring-web-enrollment-proxy-for-s4u2proxy-constrained-delegation)
