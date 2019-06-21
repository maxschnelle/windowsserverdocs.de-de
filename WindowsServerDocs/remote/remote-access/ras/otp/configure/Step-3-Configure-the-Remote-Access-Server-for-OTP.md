---
title: Schritt 3 Konfigurieren der RAS-Servers für OTP
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df1e87f2-6a0f-433b-8e42-816ae75395f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 093877657f19006bba2b80c10b92db1fb3b40fde
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280865"
---
# <a name="step-3-configure-the-remote-access-server-for-otp"></a>Schritt 3 Konfigurieren der RAS-Servers für OTP

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nachdem der RADIUS-Server mit Software-Verteilung-Token konfiguriert wurde, Kommunikationsports geöffnet sind, ein gemeinsamen geheimen Schlüssel erstellt wurde, Benutzerkonten, die Active Directory entsprechen, auf dem RADIUS-Server erstellt wurden und wurde der RAS-Servers "als" konfiguriert ein RADIUS-Authentifizierungs-Agent, und klicken Sie dann die RAS-Server werden, um OTP zu unterstützen konfiguriert muss.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[3.1 benutzerausnahmen von OTP-Authentifizierung (optional)](#BKMK_Exempt)|Wenn bestimmte Benutzer von DirectAccess mit OTP-Authentifizierung ausgenommen werden werden, klicken Sie dann vorläufigen gehen Sie folgendermaßen vor.|  
|[3.2 Konfigurieren Sie 3.2 den RAS-Server zur Unterstützung von OTP](#BKMK_Config)|Aktualisieren Sie die RAS-Konfiguration zur Unterstützung einer zweistufigen OTP-Authentifizierung, auf dem RAS-Server.|  
|[3.3 Smartcards für zusätzliche Autorisierung](#BKMK_Smartcard)|Weitere Informationen zur Verwendung von Smartcards genutzt.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_Exempt"></a>3.1 benutzerausnahmen von OTP-Authentifizierung (optional)  
Wenn bestimmte Benutzer sind, die von OTP-Authentifizierung ausgenommen werden, müssen diese Schritte vor der Konfiguration des Remotezugriffs durchgeführt werden:  
  
> [!NOTE]  
> Sie müssen für die Replikation zwischen Domänen abgeschlossen, beim Konfigurieren der Gruppe der OTP-Ausnahme warten.  
  
#### <a name="create-user-exemption-security-group"></a>Erstellen Sie zur Sicherheitsgruppe für Benutzer  
  
1.  Erstellen Sie eine Sicherheitsgruppe in Active Directory für den Zweck OTP-Ausnahmen.  
  
2.  Fügen Sie alle Benutzer, die von OTP-Authentifizierung ausgenommen werden, der Sicherheitsgruppe hinzu.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass nur Benutzer, und keine Computerkonten, in der Sicherheitsgruppe für OTP-Ausnahmen.  
  
## <a name="BKMK_Config"></a>3.2 Konfigurieren Sie 3.2 den RAS-Server zur Unterstützung von OTP  
Verwenden Sie die folgenden Schritte aus, um Remotezugriff auf zwei-Faktor-Authentifizierung verwenden und OTP mit dem RADIUS-Server und die Bereitstellung von Serverzertifikaten aus den vorherigen Abschnitten zu konfigurieren:  
  
#### <a name="configure-remote-access-for-otp"></a>Konfigurieren des Remotezugriffs für OTP  
  
1.  Open **Remotezugriffsverwaltung** , und klicken Sie auf **Konfiguration**.  
  
2.  In der **DirectAccess-Setup** Fenster unter **Schritt2: RAS-Server**, klicken Sie auf **bearbeiten**.  
  
3.  Klicken Sie auf **Weiter** dreimal aus, und klicken Sie in der **Authentifizierung** Abschnitt wählen Sie beide **zweistufige Authentifizierung** und **OTP verwenden**, und stellen Sie sicher **Computerzertifikate** aktiviert ist.  
  
    > [!NOTE]  
    > Nachdem die OTP auf dem RAS-Server aktiviert wurde, wenn Sie OTP, wählen Sie hierzu von deaktivieren **OTP verwenden**, die ISAPI- und CGI-Erweiterungen auf dem Server deinstalliert werden.  
  
4.  Wenn Sie Windows 7-Unterstützung erforderlich ist, wählen Sie die **Aktivieren von Windows 7-Clientcomputer Verbindungen über DirectAccess zulassen** Kontrollkästchen. Hinweis: Wie im Planungsabschnitt erläutert wird, müssen Windows 7-Clients DCA 2.0 installiert, um DirectAccess mit OTP zu unterstützen.  
  
5.  Klicken Sie auf **Weiter**.  
  
6.  In der **OTP RADIUS-Server** Abschnitt, doppelklicken Sie auf die leere **Servernamen** Feld.  
  
7.  In der **ein RADIUS-Server hinzufügen** Dialogfeld Geben Sie den Namen des RADIUS-Servers in der **Servernamen** Feld. Klicken Sie auf **Änderung** neben der **gemeinsamer geheimer Schlüssel** ein, und geben Sie das gleiche Kennwort, die Sie beim Konfigurieren des RADIUS-Servers in verwendet die **neuer geheimer** und  **Neuen geheimen Schlüssel bestätigen** Felder. Klicken Sie auf **OK** zweimal aus, und klicken Sie auf **Weiter**.  
  
    > [!NOTE]  
    > Wenn der RADIUS-Server in einer Domäne ist, anders als der RAS-Server ist, die **Servernamen** Feld muss den FQDN des RADIUS-Servers angeben.  
  
8.  In der **OTP-Zertifizierungsstellenserver** Abschnitt wählen Sie die CA-Server für die Registrierung von OTP-Clientauthentifizierungszertifikate verwendet werden, und klicken Sie auf **hinzufügen**. Klicken Sie auf **Weiter**.  
  
9. In der **OTP-Zertifikatvorlagen** Abschnitt auf **Durchsuchen** , wählen Sie die Zertifikatvorlage, die verwendet werden, für die Registrierung von Zertifikaten, die für die OTP-Authentifizierung ausgegeben werden.  
  
    > [!NOTE]  
    > Die Zertifikatvorlage für OTP Zertifikate von der Zertifizierungsstelle des Unternehmens muss konfiguriert werden, ohne die Option "Sperrinformationen in ausgestellten Zertifikaten enthalten nicht". Wenn diese Option während der Erstellung des Zertifikat-Vorlage ausgewählt ist, schlägt OTP-Clientcomputern bei der Anmeldung ordnungsgemäß fehl.  
  
    Klicken Sie auf **Durchsuchen** , wählen Sie eine Zertifikatvorlage verwendet, um das Zertifikat wird von RAS-Servers zum Signieren von OTP-zertifikatregistrierungsanforderungen zu registrieren. Klicken Sie auf **OK**. Klicken Sie auf **Weiter**.  
  
10. Wenn gezielt bestimmte Benutzer von DirectAccess mit OTP erforderlich sind, wird dann in der **OTP-Ausnahmen** Abschnitt **erfordern keine Benutzer in der angegebenen Sicherheitsgruppe für die Authentifizierung mit einer zweistufigen Authentifizierung** . Klicken Sie auf **Sicherheitsgruppe** , und wählen Sie die Sicherheitsgruppe, die für die OTP-Ausnahmen erstellt wurde.  
  
11. Auf der **RAS-Server-Setup** auf **Fertig stellen**.  
  
12. In der **DirectAccess-Setup** Fenster unter **Schritt 3 – Infrastrukturserver**, klicken Sie auf **bearbeiten**.  
  
13. Klicken Sie auf **Weiter** doppelt so groß wie, und klicken Sie in der **Management** Abschnitt doppelklicken Sie auf die **Verwaltungsserver** Feld.  
  
14. Geben Sie die **Computername** oder **Adresse** des ZS-Servers, die konfiguriert wird, um die OTP-Zertifikate ausgestellt, und klicken Sie auf **OK**.  
  
15. In der **Remotezugriff einrichten** Windows klicken Sie auf **Fertig stellen**.  
  
16. Klicken Sie auf **Fertig stellen** auf die **Experten für DirectAccess-Assistenten**.  
  
17. Auf der **Überprüfung des Remotezugriffs** Dialogfeld auf **übernehmen**, warten Sie, bis die DirectAccess-Richtlinie aktualisiert werden, und klicken Sie auf **schließen**.  
  
18. Auf der **starten** geben**powershell.exe**, mit der rechten Maustaste **Powershell**, klicken Sie auf **erweitert**, und klicken Sie auf **Ausführen als Administrator**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
19. Geben Sie in Windows PowerShell-Fenster **Gpupdate/force** und drücken Sie EINGABETASTE.  
  
So konfigurieren Sie den Remotezugriff für OTP mithilfe von PowerShell-Befehle  
  
![Windows PowerShell](../../../../media/Step-3-Configure-the-Remote-Access-Server-for-OTP/PowerShellLogoSmall.gif)**gleichwertige Windows PowerShell-Befehle**  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So konfigurieren Sie die RAS, um die zweistufige Authentifizierung für eine Bereitstellung zu verwenden, die derzeit die Computerzertifikatauthentifizierung verwendet:  
  
```  
Set-DAServer -UserAuthentication TwoFactor  
```  
  
Zum Konfigurieren des Remotezugriffs um OTP-Authentifizierung mit den folgenden Einstellungen verwenden:  
  
-   Ein OTP-Server mit dem Namen OTP.corp.contoso.com aus.  
  
-   Ein CA-Server mit dem Namen APP1.corp.contoso.com\corp-APP1-CA1.  
  
-   Eine Zertifikatvorlage, die mit dem Namen DAOTPLogon verwendet für die Registrierung von Zertifikaten, die für die OTP-Authentifizierung ausgegeben werden.  
  
-   Eine Zertifikatvorlage, die mit dem Namen DAOTPRA verwendet, um die Registrierung Zertifizierungsstelle, die RAS-Servers für OTP zertifikatregistrierungsanforderungen anmelden zu registrieren.  
  
```  
Enable-DAOtpAuthentication -CertificateTemplateName 'DAOTPLogon' -SigningCertificateTemplateName 'DAOTPRA' -CAServer @('APP1.corp.contoso.com\corp-APP1-CA1') -RadiusServer OTP.corp.contoso.com -SharedSecret Abcd123$  
```  
  
Führen Sie nach dem Ausführen der PowerShell-Befehle die Schritte 12-19 aus dem vorherigen Verfahren zum Konfigurieren der RAS-Server, um OTP zu unterstützen.  
  
> [!NOTE]  
> Stellen Sie sicher, dass Sie die OTP-Einstellungen auf dem RAS-Server angewendet haben, bevor Sie einen Einstiegspunkt hinzufügen.  
  
## <a name="BKMK_Smartcard"></a>3.3 Smartcards für zusätzliche Autorisierung  
Auf der Seite Authentifizierung von Schritt2 in den Remotezugriffs-Setup-Assistenten können Sie die Verwendung von Smartcards für den Zugriff auf das interne Netzwerk festlegen. Wenn diese Option ausgewählt ist, konfiguriert den Remotezugriffs-Setup-Assistenten die IPsec-Verbindungssicherheitsregel für den intranettunnel auf dem DirectAccess-Server für die tunnelmodusautorisierung mit Smartcards erforderlich. Tunnelmodusautorisierung können Sie angeben, dass nur berechtigte Computer oder Benutzer einen eingehenden Tunnel aufbauen können.  
  
Um bei der IPsec-Tunnelmodusberechtigung für den Intranettunnel Smartcards zu verwenden, müssen Sie eine Public Key-Infrastruktur (PKI) für die Verwendung mit Smartcards bereitstellen.  
  
Da die DirectAccess-Clients für den Zugriff auf das Intranet Smartcards verwenden, können Sie auch authentifizierungsmechanismussicherung, ein Feature von Windows Server 2008 R2 verwenden, zum Steuern des Zugriffs auf Ressourcen wie Dateien, Ordner und Drucker, abhängig davon, ob die Benutzer mit einem smartcardbasierten Zertifikat angemeldet. Authentifizierungsmechanismuszusicherung ist eine Domänenfunktionsebene von Windows Server 2008 R2 erforderlich.  
  
### <a name="allowing-access-for-users-with-unusable-smart-cards"></a>Zugriffssteuerung für Benutzer mit unbrauchbaren Smartcards  
Gehen Sie wie folgt vor, um Benutzern mit unbrauchbaren Smartcards temporären Zugriff zu gestatten:  
  
1.  Erstellen Sie eine Active Directory-Sicherheitsgruppe mit den Benutzerkonten von Benutzern, die ihre Smartcards vorübergehend nicht verwenden können.  
  
2.  Konfigurieren Sie für den DirectAccess-Server Group Policy Object die globale IPsec-Einstellungen für die IPsec-tunnelautorisierung, und die Liste der autorisierten Benutzer, die Active Directory-Sicherheitsgruppe hinzugefügt.  
  
Um einem Benutzer, der seine Smartcard nicht verwenden kann, Zugriff zu gewähren, fügen Sie der Active Directory-Sicherheitsgruppe vorübergehend sein Benutzerkonto hinzu. Entfernen Sie das Benutzerkonto aus der Gruppe, sobald die Smartcard wieder verwendbar ist.  
  
### <a name="under-the-covers-smart-card-authorization"></a>Hintergrundinformationen: Smartcard-Autorisierung  
Die Smartcard-Autorisierung funktioniert, indem die Tunnelmodusautorisierung der Verbindungssicherheitsregel für den Intranettunnel zum DirectAccess-Server für eine bestimmte Kerberos-basierte Sicherheits-ID (SID) aktiviert wird. Bei der Smartcardautorisierung ist dies die bekannte SID (S-1-5-65-1), die smartcardbasierten Anmeldungen zuordnet ist. Diese SID ist in einem DirectAccess-Client-Kerberos-Token vorhanden und wird als "Dieses Organisationszertifikat" in den globalen IPsec konfiguriert Einstellungen Tunneln bezeichnet.  
  
Wenn Sie die smartcardautorisierung in Schritt2 des DirectAccess-Setup-Assistenten aktivieren, konfiguriert der DirectAccess-Setup-Assistent Autorisierung die globalen IPSec-Tunnel moduseinstellung mit dieser SID für das Gruppenrichtlinienobjekt des DirectAccess-Server an. Um diese Konfiguration in der Windows-Firewall mit erweiterter Sicherheit-Snap-in für das Gruppenrichtlinienobjekt des DirectAccess-Server anzuzeigen, führen Sie folgende Schritte aus:  
  
1.  Klicken Sie mit der rechten Maustaste auf die Windows-Firewall mit erweiterter Sicherheit, und klicken Sie dann auf Eigenschaften.  
  
2.  Klicken Sie auf der Registerkarte IPsec-Einstellungen in der IPsec-tunnelautorisierung klicken Sie auf "anpassen".  
  
3.  Klicken Sie auf der Registerkarte "Benutzer". Als autorisierter Benutzer sollte die "NT-autorität\dieses Organisationszertifikat" angezeigt werden.  
  


