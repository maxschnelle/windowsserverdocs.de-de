---
title: Schritt 3 Konfigurieren des Remote Zugriffs Servers für OTP
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df1e87f2-6a0f-433b-8e42-816ae75395f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 41cc5cc2df5ac9709818536df8fff098d2a0c297
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404340"
---
# <a name="step-3-configure-the-remote-access-server-for-otp"></a>Schritt 3 Konfigurieren des Remote Zugriffs Servers für OTP

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Nachdem der RADIUS-Server mit Software Verteilungs Token konfiguriert wurde, sind die Kommunikationsports geöffnet, ein gemeinsamer geheimer Schlüssel wurde erstellt, Benutzerkonten, die Active Directory entsprechen, wurden auf dem RADIUS-Server erstellt, und der RAS-Server hat der RAS-Server muss für die Unterstützung von OTP konfiguriert werden, wenn er als RADIUS-Authentifizierungs-Agent konfiguriert wurde.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[3,1 Benutzer von OTP-Authentifizierung ausgenommen (optional)](#BKMK_Exempt)|Wenn bestimmte Benutzer von DirectAccess mit OTP-Authentifizierung ausgenommen werden, führen Sie die folgenden Schritte aus.|  
|[3,2 Konfigurieren des Remote Zugriffs Servers für die Unterstützung von OTP](#BKMK_Config)|Aktualisieren Sie auf dem Remote Zugriffs Server die Konfiguration des Remote Zugriffs, um die zweistufige Authentifizierung von OTP zu unterstützen.|  
|[3,3 Smartcards für zusätzliche Autorisierung](#BKMK_Smartcard)|Weitere Informationen zur Verwendung von Smartcards.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_Exempt"></a>3,1 Benutzer von OTP-Authentifizierung ausgenommen (optional)  
Wenn bestimmte Benutzer von der OTP-Authentifizierung ausgenommen werden sollen, müssen diese Schritte vor der Konfiguration des Remote Zugriffs ausgeführt werden:  
  
> [!NOTE]  
> Beim Konfigurieren der OTP-Ausnahme Gruppe müssen Sie auf den Abschluss der Replikation zwischen Domänen warten.  
  
#### <a name="create-user-exemption-security-group"></a>Benutzer Ausnahme-Sicherheitsgruppe erstellen  
  
1.  Erstellen Sie eine Sicherheitsgruppe in Active Directory für die OTP-Ausnahme.  
  
2.  Fügen Sie alle Benutzer, die von der OTP-Authentifizierung ausgenommen werden sollen, der Sicherheitsgruppe hinzu.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass nur Benutzerkonten und keine Computer Konten in der Sicherheitsgruppe "OTP" ausgenommen sind.  
  
## <a name="BKMK_Config"></a>3,2 Konfigurieren des Remote Zugriffs Servers für die Unterstützung von OTP  
Führen Sie die folgenden Schritte aus, um den Remote Zugriff für die Verwendung von zweistufiger Authentifizierung und OTP mit dem RADIUS-Server und der Zertifikat Bereitstellung aus den vorherigen Abschnitten zu konfigurieren:  
  
#### <a name="configure-remote-access-for-otp"></a>Konfigurieren des Remote Zugriffs für OTP  
  
1.  Öffnen Sie **Remote Zugriffs Verwaltung** , und klicken Sie auf **Konfiguration**.  
  
2.  Klicken Sie im Fenster **DirectAccess-Setup** unter **Schritt 2-RAS-Server**auf **Bearbeiten**.  
  
3.  Klicken Sie dreimal auf **weiter** , und wählen Sie im Abschnitt **Authentifizierung** beide **zwei** stufige Authentifizierung **aus, und vergewissern Sie sich,** dass die Option **Computer Zertifikate verwenden** aktiviert ist.  
  
    > [!NOTE]  
    > Wenn Sie OTP auf dem RAS-Server aktiviert haben, werden die ISAPI-und CGI-Erweiterungen auf dem Server deinstalliert, wenn Sie OTP durch Deaktivieren der **Verwendung von OTP**deaktivieren.  
  
4.  Wenn Windows 7-Unterstützung erforderlich ist, aktivieren Sie das Kontrollkästchen **Windows 7-Client Computer zum Herstellen einer Verbindung über DirectAccess aktivieren** . Hinweis: wie im Abschnitt zur Planung erläutert, muss für Windows 7-Clients DCA 2,0 installiert sein, damit DirectAccess mit OTP unterstützt werden kann.  
  
5.  Klicken Sie auf **Weiter**.  
  
6.  Doppelklicken Sie im Abschnitt " **OTP RADIUS-Server** " auf das Feld "leerer **Server Name** ".  
  
7.  Geben Sie im Dialogfeld **RADIUS-Server hinzufügen** den Namen des RADIUS-Servers in das Feld **Server Name** ein. Klicken Sie neben dem Feld **gemeinsamer geheimer** Schlüssel auf **ändern** , und geben Sie das Kennwort ein, das Sie beim Konfigurieren des RADIUS-Servers in den **neuen geheimen** Schlüsseln und **bestätigen neuer geheimer** Schlüssel verwendet haben. Klicken Sie zweimal auf **OK** , und klicken Sie auf **weiter**.  
  
    > [!NOTE]  
    > Wenn sich der RADIUS-Server in einer anderen Domäne als der RAS-Server befindet, muss im Feld **Server Name** der voll qualifizierte Domänen Name des RADIUS-Servers angegeben werden.  
  
8.  Wählen Sie im Abschnitt **OTP** -Zertifizierungsstellen Server die Zertifizierungsstellen Server aus, die für die Registrierung von OTP-Client Authentifizierungs Zertifikaten verwendet werden sollen, und klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  
  
9. Klicken Sie im Abschnitt **OTP-Zertifikat Vorlagen** auf **Durchsuchen** , um die Zertifikat Vorlage auszuwählen, die für die Registrierung von Zertifikaten verwendet wird, die für die OTP-Authentifizierung ausgestellt werden.  
  
    > [!NOTE]  
    > Die Zertifikat Vorlage für OTP-Zertifikate, die von der Unternehmens Zertifizierungsstelle ausgestellt wurde, muss ohne die Option "keine Sperrinformationen in ausgestellten Zertifikaten einschließen" konfiguriert werden. Wenn diese Option während der Erstellung der Zertifikat Vorlage ausgewählt wird, können sich die OTP-Client Computer nicht ordnungsgemäß anmelden.  
  
    Klicken Sie auf **Durchsuchen** , um eine Zertifikat Vorlage auszuwählen, die zum Registrieren des Zertifikats verwendet wird, das vom RAS-Server zum Signieren von OTP-Zertifikat Registrierungsanforderungen verwendet wird. Klicken Sie auf **OK**. Klicken Sie auf **Weiter**.  
  
10. Wenn die Angabe bestimmter Benutzer von DirectAccess mit OTP erforderlich ist, wählen Sie im Abschnitt " **OTP-Ausnahmen** " die Option **Benutzer in der angegebenen Sicherheitsgruppe darf nicht mithilfe der zweistufigen Authentifizierung authentifizieren**aus. Klicken Sie auf **Sicherheitsgruppe** , und wählen Sie die Sicherheitsgruppe aus, die für OTP-Ausnahmen erstellt wurde.  
  
11. Klicken Sie auf der Seite **Setup des Remote Zugriffs Servers** auf **Fertig**stellen.  
  
12. Klicken Sie im Fenster **DirectAccess-Setup** unter **Schritt 3-Infrastruktur Server**auf **Bearbeiten**.  
  
13. Klicken Sie zweimal auf **weiter** , und doppelklicken Sie im Abschnitt **Verwaltung** auf das Feld **Verwaltungs Server** .  
  
14. Geben Sie den **Computer Namen** oder die **Adresse** des Zertifizierungsstellen Servers ein, der für das Ausstellen von OTP-Zertifikaten konfiguriert ist, und klicken Sie auf **OK**.  
  
15. Klicken Sie im Fenster **Remote Zugriffs Einrichtung** auf **Fertig**stellen.  
  
16. Klicken Sie im **DirectAccess-Experten-Assistenten**auf **Fertig** stellen.  
  
17. Klicken Sie im Dialogfeld **Remote Zugriffs Überprüfung** auf über **nehmen, warten Sie,** bis die DirectAccess-Richtlinie aktualisiert wurde, und klicken Sie dann auf **Schließen**.  
  
18. Geben Sie im **Start** Bildschirm**PowerShell. exe**ein, klicken Sie mit der rechten Maustaste auf **PowerShell**, klicken Sie auf **erweitert**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
19. Geben Sie im Windows PowerShell-Fenster **gpupdate/force** ein, und drücken Sie die EINGABETASTE.  
  
So konfigurieren Sie den Remote Zugriff für OTP mithilfe von PowerShell-Befehlen:  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-3-Configure-the-Remote-Access-Server-for-OTP/PowerShellLogoSmall.gif)**Befehle in Windows PowerShell**  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So konfigurieren Sie den Remote Zugriff für die Verwendung der zweistufigen Authentifizierung für eine Bereitstellung, die derzeit die Computer Zertifikat Authentifizierung verwendet:  
  
```  
Set-DAServer -UserAuthentication TwoFactor  
```  
  
So konfigurieren Sie den Remote Zugriff, um die OTP-Authentifizierung mit den folgenden Einstellungen zu verwenden:  
  
-   Ein OTP-Server mit dem Namen OTP.Corp.contoso.com.  
  
-   Ein Zertifizierungsstellen Server mit dem Namen App1. Corp. ca. com\corp-App1-CA1.  
  
-   Eine Zertifikat Vorlage mit dem Namen daotplogon, die für die Registrierung von Zertifikaten verwendet wird, die für die OTP-Authentifizierung ausgestellt werden.  
  
-   Eine Zertifikat Vorlage namens daotpra, mit der das Registrierungsstellen Zertifikat registriert wird, das vom RAS-Server zum Signieren von OTP-Zertifikat Registrierungsanforderungen verwendet wird.  
  
```  
Enable-DAOtpAuthentication -CertificateTemplateName 'DAOTPLogon' -SigningCertificateTemplateName 'DAOTPRA' -CAServer @('APP1.corp.contoso.com\corp-APP1-CA1') -RadiusServer OTP.corp.contoso.com -SharedSecret Abcd123$  
```  
  
Nachdem Sie die PowerShell-Befehle ausgeführt haben, führen Sie die Schritte 12-19 aus dem vorherigen Verfahren zum Konfigurieren des RAS-Servers für die Unterstützung von OTP aus  
  
> [!NOTE]  
> Stellen Sie sicher, dass Sie die OTP-Einstellungen auf dem RAS-Server angewendet haben, bevor Sie einen Einstiegspunkt hinzufügen.  
  
## <a name="BKMK_Smartcard"></a>3,3 Smartcards für zusätzliche Autorisierung  
Auf der Seite Authentifizierung von Schritt 2 im Setup-Assistenten für Remote Zugriff können Sie die Verwendung von Smartcards für den Zugriff auf das interne Netzwerk vorschreiben. Wenn diese Option ausgewählt ist, konfiguriert der Remote Zugriffs-Setup-Assistent die IPSec-Verbindungs Sicherheitsregel für den intranettunnel auf dem DirectAccess-Server so, dass eine Tunnel Modus-Autorisierung mit Smartcards erforderlich ist. Mithilfe der Tunnelmodusautorisierung können Sie angeben, dass nur autorisierte Computer oder Benutzer einen eingehenden Tunnel einrichten können.  
  
Um bei der IPsec-Tunnelmodusberechtigung für den Intranettunnel Smartcards zu verwenden, müssen Sie eine Public Key-Infrastruktur (PKI) für die Verwendung mit Smartcards bereitstellen.  
  
Da Ihre DirectAccess-Clients Smartcards für den Zugriff auf das Intranet verwenden, können Sie auch die Authentifizierungsmechanismus-Sicherung, ein Feature von Windows Server 2008 R2, verwenden, um den Zugriff auf Ressourcen wie Dateien, Ordner und Drucker zu steuern, je nachdem, ob Benutzer, der mit einem smartcardbasierten Zertifikat angemeldet ist. Die Authentifizierung des Authentifizierungsmechanismus erfordert eine Domänen Funktionsebene von Windows Server 2008 R2.  
  
### <a name="allowing-access-for-users-with-unusable-smart-cards"></a>Zugriffssteuerung für Benutzer mit unbrauchbaren Smartcards  
Gehen Sie wie folgt vor, um Benutzern mit unbrauchbaren Smartcards temporären Zugriff zu gestatten:  
  
1.  Erstellen Sie eine Active Directory-Sicherheitsgruppe mit den Benutzerkonten von Benutzern, die ihre Smartcards vorübergehend nicht verwenden können.  
  
2.  Konfigurieren Sie für das Gruppenrichtlinie Objekt des DirectAccess-Servers globale IPsec-Einstellungen für die IPSec-Tunnel Autorisierung, und fügen Sie der Liste der autorisierten Benutzer die Active Directory Sicherheitsgruppe hinzu.  
  
Um einem Benutzer, der seine Smartcard nicht verwenden kann, Zugriff zu gewähren, fügen Sie der Active Directory-Sicherheitsgruppe vorübergehend sein Benutzerkonto hinzu. Entfernen Sie das Benutzerkonto aus der Gruppe, sobald die Smartcard wieder verwendbar ist.  
  
### <a name="under-the-covers-smart-card-authorization"></a>Im folgenden Abschnitt: Smartcard-Autorisierung  
Die Smartcard-Autorisierung funktioniert, indem die Tunnelmodusautorisierung der Verbindungssicherheitsregel für den Intranettunnel zum DirectAccess-Server für eine bestimmte Kerberos-basierte Sicherheits-ID (SID) aktiviert wird. Bei der Smartcardautorisierung ist dies die bekannte SID (S-1-5-65-1), die smartcardbasierten Anmeldungen zuordnet ist. Diese SID ist im Kerberos-Token eines DirectAccess-Clients vorhanden und wird als "dieses Organisations Zertifikat" bezeichnet, wenn Sie in den globalen IPsec-tunnelmodusautorisierungs-Einstellungen konfiguriert ist.  
  
Wenn Sie die Smartcard-Autorisierung in Schritt 2 des DirectAccess-Setup-Assistenten aktivieren, konfiguriert der DirectAccess-Setup-Assistent die globale IPsec-tunnelmodusautorisierungseinstellung mit dieser sid für das Gruppenrichtlinie Objekt des DirectAccess-Servers. Führen Sie die folgenden Schritte aus, um diese Konfiguration im Snap-in "Windows-Firewall mit erweiterter Sicherheit" für das Objekt "DirectAccess-Server Gruppenrichtlinie" anzuzeigen:  
  
1.  Klicken Sie mit der rechten Maustaste auf Windows-Firewall mit erweiterter Sicherheit und dann auf Eigenschaften.  
  
2.  Klicken Sie auf der Registerkarte IPsec-Einstellungen unter IPsec-Tunnel Autorisierung auf anpassen.  
  
3.  Klicken Sie auf die Registerkarte Benutzer. Als autorisierter Benutzer sollte "NT-Autorität \ dieses Organisations Zertifikat" angezeigt werden.  
  


