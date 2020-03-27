---
title: Problembehandlung bei Authentifizierungsfehlern
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71307757-f8f4-4f82-b8b3-ffd4fd8c5d6d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 74e332fff194374c6f3a5eeae5e26e8e4f5cfb42
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313452"
---
# <a name="troubleshooting-authentication-issues"></a>Problembehandlung bei Authentifizierungsfehlern

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Informationen zur Problembehandlung bei Problemen im Zusammenhang mit Problemen, die Benutzer möglicherweise bei der Verbindungs Herstellung mit DirectAccess mithilfe der OTP-Authentifizierung haben. Directaccerss OTP-bezogene Ereignisse werden auf dem Client Computer in Ereignisanzeige unter **Anwendungs-und Dienst Protokolle/Microsoft/Windows/otpkredentialprovider**protokolliert. Stellen Sie sicher, dass dieses Protokoll bei der Behandlung von Problemen mit DirectAccess OTP aktiviert ist.  
  
## <a name="failed-to-access-the-ca-that-issues-otp-certificates"></a>Fehler beim Zugriff auf die Zertifizierungsstelle, die OTP-Zertifikate ausgibt.  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Fehler bei der OTP-Zertifikat Registrierung für die Benutzer <username> auf dem Zertifizierungsstellen Server < CA_name >, Anforderung fehlgeschlagen, mögliche Ursachen für Fehler: der ZS-Servername kann nicht aufgelöst werden. der Zugriff auf den Zertifizierungsstellen Server ist über den ersten DirectAccess-Tunnel nicht möglich, oder die Verbindung mit dem Zertifizierungsstellen Server kann nicht  
  
**Ursache**  
  
Der Benutzer hat ein gültiges einmal Kennwort angegeben, und der DirectAccess-Server hat die Zertifikat Anforderung signiert. der Client Computer kann jedoch keine Verbindung mit der Zertifizierungsstelle hergestellt werden, die OTP-Zertifikate ausgibt, um den Registrierungsvorgang abzuschließen.  
  
**Lösung**  
  
Führen Sie auf dem DirectAccess-Server die folgenden Windows PowerShell-Befehle aus:  
  
1.  Hier finden Sie die Liste der konfigurierten OTP-ausstellenden Zertifizierungsstellen und den Wert von "caserver": `Get-DAOtpAuthentication`  
  
2.  Stellen Sie sicher, dass die Zertifizierungsstellen als Verwaltungs Server konfiguriert sind: `Get-DAMgmtServer -Type All`  
  
3.  Stellen Sie sicher, dass der Client Computer den Infrastruktur Tunnel eingerichtet hat: Erweitern Sie in der Konsole Windows-Firewall mit erweiterter Sicherheit den Knoten **Überwachung/Sicherheits Zuordnungen**, klicken Sie auf **Hauptmodus**, und stellen Sie sicher, dass die IPSec-Sicherheits Zuordnungen mit den korrekten Remote Adressen für die DirectAccess-Konfiguration angezeigt werden  
  
## <a name="directaccess-server-connectivity-issues"></a>Konnektivitätsprobleme beim DirectAccess-Server  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler empfangen** (Client Ereignisprotokoll)  
  
Einer der folgenden Fehler:  
  
-   Es kann keine Verbindung mit dem RAS-Server hergestellt werden, < DirectAccess_server_hostname > mithilfe von Basispfad < OTP_authentication_path > und Port < OTP_authentication_port >. Fehlercode: < internal_error_code >.  
  
-   Benutzer Anmelde Informationen können nicht an den RAS-Server gesendet werden < DirectAccess_server_hostname > mithilfe von Basispfad < OTP_authentication_path > und Port < OTP_authentication_port >. Fehlercode: < internal_error_code >.  
  
-   Es wurde keine Antwort vom RAS-Server < DirectAccess_server_hostname > mithilfe von Basispfad < OTP_authentication_path > und Port < OTP_authentication_port > empfangen. Fehlercode: < internal_error_code >.  
  
**Ursache**  
  
Der Client Computer kann aufgrund von Netzwerkproblemen oder eines falsch konfigurierten IIS-Servers auf dem DirectAccess-Server nicht über das Internet auf den DirectAccess-Server zugreifen.  
  
**Lösung**  
  
Stellen Sie sicher, dass die Internet Verbindung auf dem Client Computer funktioniert, und stellen Sie sicher, dass der DirectAccess-Dienst ausgeführt wird und über das Internet erreichbar ist.  
  
## <a name="failed-to-enroll-for-the-directaccess-otp-logon-certificate"></a>Fehler beim Registrieren für das Anmeldezertifikat für das DirectAccess-OTP.  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Fehler bei der Zertifikat Registrierung von der Zertifizierungsstelle < CA_name >. Die Anforderung wurde vom OTP-Signaturzertifikat nicht erwartungsgemäß signiert, oder der Benutzer verfügt nicht über die Berechtigung, sich zu registrieren.  
  
**Ursache**  
  
Das vom Benutzer bereitgestellte einmalige Kennwort war richtig, aber die ausstellende Zertifizierungsstelle hat das Ausstellen des OTP-Anmelde Zertifikats verweigert. Die Zertifikat Anforderung ist möglicherweise nicht ordnungsgemäß mit der richtigen EKU-Anwendungs Richtlinie (OTP-Registrierungsstelle) signiert, oder der Benutzer verfügt nicht über die Berechtigung "registrieren" für die Vorlage "da OTP".  
  
**Lösung**  
  
Stellen Sie sicher, dass DirectAccess-OTP-Benutzer über die Berechtigung zum Registrieren für das Registrierungszertifikat für das DirectAccess-OTP verfügen, und dass die richtige "Anwendungs Richtlinie" in der Signatur Vorlage der Registrierungsstelle für die Registrierungsstelle enthalten ist. Stellen Sie außerdem sicher, dass das DirectAccess-Registrierungsstellen Zertifikat auf dem RAS-Server gültig ist. Weitere Informationen finden Sie unter 3,2 Planen der OTP-Zertifikat Vorlage und 3,3 Planen des Registrierungsstellen Zertifikats.  
  
## <a name="missing-or-invalid-computer-account-certificate"></a>Fehlendes oder ungültiges Computer Konto Zertifikat  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll).  Die OTP-Authentifizierung kann nicht abgeschlossen werden, da das für OTP erforderliche Computer Zertifikat im Zertifikat Speicher des lokalen Computers nicht gefunden werden kann.  
  
**Ursache**  
  
Für die DirectAccess-OTP-Authentifizierung ist ein Client Computer Zertifikat erforderlich, um eine SSL-Verbindung mit dem DirectAccess-Server herzustellen. das Zertifikat des Client Computers wurde jedoch nicht gefunden oder ist ungültig, z. b. wenn das Zertifikat abgelaufen ist.  
  
**Lösung**  
  
Stellen Sie sicher, dass das Computer Zertifikat vorhanden und gültig ist:  
  
1.  Öffnen Sie auf dem Client Computer in der MMC-Zertifikat Konsole für das lokale Computer Konto " **persönlich/Zertifikate**".  
  
2.  Stellen Sie sicher, dass ein Zertifikat ausgestellt wurde, das mit dem Computernamen übereinstimmt, und doppelklicken Sie auf das Zertifikat.  
  
3.  Vergewissern Sie sich, dass im Dialogfeld **Zertifikat** auf der Registerkarte **Zertifikat Pfad** unter **Zertifikat Status**die Meldung "dieses Zertifikat ist OK" angezeigt wird.  
  
Wenn kein gültiges Zertifikat gefunden wird, löschen Sie das ungültige Zertifikat (sofern vorhanden), und melden Sie sich erneut für das Computer Zertifikat an, indem Sie `gpupdate /Force` an einer Eingabeaufforderung mit erhöhten Rechten ausführen oder den Client Computer neu starten.  
  
## <a name="missing-ca-that-issues-otp-certificates"></a>Fehlende Zertifizierungsstelle, die OTP-Zertifikate ausgibt  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Die OTP-Authentifizierung kann nicht abgeschlossen werden, da der da-Server keine Adresse einer ausstellenden Zertifizierungsstelle zurückgegeben hat.  
  
**Ursache**  
  
Entweder gibt es keine Zertifizierungsstellen, die OTP-Zertifikate ausstellen, oder alle konfigurierten Zertifizierungsstellen, die OTP-Zertifikate ausstellen, werden nicht reagiert.  
  
**Lösung**  
  
1.  Verwenden Sie den folgenden Befehl, um die Liste der Zertifizierungsstellen zu erhalten, die OTP-Zertifikate ausstellen (der Name der Zertifizierungsstelle wird unter caserver angezeigt): `Get-DAOtpAuthentication`.  
  
2.  Wenn keine Zertifizierungsstellen konfiguriert sind:  
  
    1.  Verwenden Sie entweder den Befehl `Set-DAOtpAuthentication` oder die Remote Zugriffs-Verwaltungskonsole, um die Zertifizierungsstellen zu konfigurieren, die das Registrierungszertifikat für das DirectAccess-OTP ausstellen.  
  
    2.  Wenden Sie die neue Konfiguration an, und erzwingen Sie, dass die Clients die DirectAccess-GPO-Einstellungen aktualisieren, indem Sie `gpupdate /Force` über eine Eingabeaufforderung mit erhöhten Rechten ausführen oder den Client Computer neu starten.  
  
3.  Wenn CAS konfiguriert sind, stellen Sie sicher, dass Sie online sind und auf Registrierungsanforderungen reagieren.  
  
## <a name="misconfigured-directaccess-server-address"></a>Falsch konfigurierte DirectAccess-Server Adresse  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Die OTP-Authentifizierung kann nicht wie erwartet ausgeführt werden. Der Name oder die Adresse des Remote Zugriffs Servers kann nicht bestimmt werden.  Fehlercode: < error_code >. Die DirectAccess-Einstellungen sollten vom Server Administrator überprüft werden.  
  
**Ursache**  
  
Die Adresse des DirectAccess-Servers ist nicht ordnungsgemäß konfiguriert.  
  
**Lösung**  
  
Überprüfen Sie die konfigurierte DirectAccess-Server Adresse mithilfe `Get-DirectAccess`, und korrigieren Sie die Adresse, wenn Sie falsch konfiguriert ist.  
  
Stellen Sie sicher, dass die neuesten Einstellungen auf dem Client Computer bereitgestellt werden, indem Sie `gpupdate /force` über eine Eingabeaufforderung mit erhöhten Rechten ausführen oder den Client Computer neu starten.  
  
## <a name="failed-to-generate-the-otp-logon-certificate-request"></a>Die OTP-Anmeldezertifikat Anforderung konnte nicht generiert werden.  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Die Zertifikat Anforderung für die OTP-Authentifizierung kann nicht initialisiert werden. Ein privater Schlüssel kann nicht generiert werden, oder Benutzer <username> nicht auf die Zertifikat Vorlage zugreifen können < OTP_template_name > auf dem Domänen Controller.  
  
**Ursache**  
  
Für diesen Fehler gibt es zwei mögliche Ursachen:  
  
-   Der Benutzer verfügt nicht über die Berechtigung zum Lesen der OTP-Anmeldevorlage.  
  
-   Der Computer des Benutzers kann aufgrund von Netzwerkproblemen nicht auf den Domänen Controller zugreifen.  
  
**Lösung**  
  
-   Überprüfen Sie die Berechtigungseinstellung für die OTP-Anmeldevorlage, und stellen Sie sicher, dass alle Benutzer, die für DirectAccess OTP bereitgestellt wurden, über die Berechtigung Lesen verfügen.  
  
-   Stellen Sie sicher, dass der Domänen Controller als Management Server konfiguriert ist und dass der Client Computer den Domänen Controller über den Infrastruktur Tunnel erreichen kann. Weitere Informationen finden Sie unter 3,2 Planen der OTP-Zertifikat Vorlage.  
  
## <a name="no-connection-to-the-domain-controller"></a>Keine Verbindung mit dem Domänen Controller  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Eine Verbindung mit dem Domänen Controller zum Zweck der OTP-Authentifizierung kann nicht hergestellt werden. Fehlercode: < error_code >.  
  
**Ursache**  
  
Für diesen Fehler gibt es zwei mögliche Ursachen:  
  
-   Der Computer des Benutzers verfügt über keine Netzwerk Konnektivität.  
  
-   Der Domänen Controller ist über den Infrastruktur Tunnel nicht erreichbar.  
  
**Lösung**  
  
-   Stellen Sie sicher, dass der Domänen Controller als Management Server konfiguriert ist, indem Sie den folgenden Befehl an einer PowerShell-Eingabeaufforderung ausführen: `Get-DAMgmtServer -Type All`.  
  
-   Stellen Sie sicher, dass der Client Computer den Domänen Controller über den Infrastruktur Tunnel erreichen kann.  
  
## <a name="otp-provider-requires-challengeresponse"></a>Der OTP-Anbieter erfordert Challenge/Response.  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Die OTP-Authentifizierung mit dem Remote Zugriffs Server (< DirectAccess_server_name >) für den Benutzer (<username>) erforderte eine Herausforderung des Benutzers.  
  
**Ursache**  
  
Der verwendete OTP-Anbieter erfordert, dass der Benutzer zusätzliche Anmelde Informationen in Form eines RADIUS-Challenge/Antwort-Austauschs bereitstellt, der von Windows Server 2012 DirectAccess OTP nicht unterstützt wird.  
  
**Lösung**  
  
Konfigurieren Sie den OTP-Anbieter so, dass in keinem Szenario Challenge/Response erforderlich ist.  
  
## <a name="incorrect-otp-logon-template-used"></a>Falsche OTP-Anmeldevorlage verwendet  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Die Zertifizierungsstellen Vorlage, von der die Benutzer <username> ein Zertifikat angefordert hat, ist nicht für das Ausstellen von OTP-Zertifikaten konfiguriert.  
  
**Ursache**  
  
Die "DirectAccess OTP"-Anmeldevorlage wurde ersetzt, und der Client Computer versucht, sich mit einer älteren Vorlage zu authentifizieren.  
  
**Lösung**  
  
Stellen Sie sicher, dass der Client Computer die neueste OTP-Konfiguration verwendet, indem Sie eine der folgenden Aktionen ausführen:  
  
-   Erzwingen Sie eine Gruppenrichtlinie Aktualisierung, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen: `gpupdate /Force`.  
  
-   Starten Sie den Clientcomputer neu.  
  
## <a name="missing-otp-signing-certificate"></a>Fehlendes OTP-Signaturzertifikat  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Ereignisprotokoll). Ein OTP-Signaturzertifikat wurde nicht gefunden. Die OTP-Zertifikat Registrierungs Anforderung kann nicht signiert werden.  
  
**Ursache**  
  
Das Registrierungszertifikat für den DirectAccess-OTP wurde auf dem Remote Zugriffs Server nicht gefunden. Daher kann die Benutzerzertifikat Anforderung nicht vom RAS-Server signiert werden. Entweder ist kein Signaturzertifikat vorhanden, oder das Signaturzertifikat ist abgelaufen und wurde nicht erneuert.  
  
**Lösung**  
  
Führen Sie diese Schritte auf dem Remote Zugriffs Server aus.  
  
1.  Überprüfen Sie den Namen der konfigurierten OTP-Signaturzertifikat Vorlage, indem Sie das PowerShell-Cmdlet `Get-DAOtpAuthentication` ausführen und den Wert `SigningCertificateTemplateName`überprüfen.  
  
2.  Verwenden Sie das MMC-Snap-in Zertifikate, um sicherzustellen, dass auf dem Computer ein gültiges Zertifikat vorhanden ist, das bei dieser Vorlage registriert ist.  
  
3.  Wenn ein solches Zertifikat nicht vorhanden ist, löschen Sie das abgelaufene Zertifikat (sofern vorhanden), und registrieren Sie sich für ein neues Zertifikat auf der Grundlage dieser Vorlage.  
  
Informationen zum Erstellen der OTP-Signaturzertifikat Vorlage finden Sie unter 3,3 Planen des Registrierungsstellen Zertifikats.  
  
## <a name="missing-or-incorrect-upndn-for-the-user"></a>Fehlender oder falscher UPN/DN für den Benutzer.  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler empfangen** (Client Ereignisprotokoll)  
  
Einer der folgenden Fehler:  
  
-   Benutzer <username> können nicht mit OTP authentifiziert werden. Stellen Sie sicher, dass ein UPN für den Benutzernamen in Active Directory definiert ist. Fehlercode: < error_code >.  
  
-   Benutzer <username> können nicht mit OTP authentifiziert werden. Stellen Sie sicher, dass für den Benutzernamen in Active Directory ein DN definiert ist. Fehlercode: < error_code >.  
  
**Fehler empfangen** (Server Ereignisprotokoll)  
  
Der für die OTP-Authentifizierung angegebene Benutzername <username> nicht vorhanden.  
  
**Ursache**  
  
Der Benutzer verfügt nicht über die ordnungsgemäße Festlegung der Benutzer Prinzipal Namen (UPN) oder DN-Attribute (DN) im Benutzerkonto. diese Eigenschaften sind für eine ordnungsgemäße Funktionsweise von DirectAccess OTP erforderlich.  
  
**Lösung**  
  
Überprüfen Sie mithilfe der Konsole Active Directory Benutzer und Computer auf dem Domänen Controller, ob beide Attribute ordnungsgemäß für den authentifizier enden Benutzer festgelegt sind.  
  
## <a name="otp-certificate-is-not-trusted-for-login"></a>OTP-Zertifikat ist für die Anmeldung nicht vertrauenswürdig.  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Ursache**  
  
Die Zertifizierungsstelle, die OTP-Zertifikate ausgibt, befindet sich nicht im Enterprise NTAuth-Speicher. Daher können registrierte Zertifikate nicht für die Anmeldung verwendet werden. Dies kann in Umgebungen mit mehreren Domänen und mehreren Gesamtstrukturen vorkommen, in denen keine Domänen übergreifende Zertifizierungsstellen-Vertrauensstellung eingerichtet ist  
  
**Lösung**  
  
Stellen Sie sicher, dass das Zertifikat des Stamms der Zertifizierungsstellen Hierarchie, von der OTP-Zertifikate ausgestellt werden, im NTAuth-Zertifikat Speicher des Unternehmens der Domäne installiert ist, zu der der Benutzer eine Authentifizierung durchführen soll.  
  
## <a name="windows-could-not-verify-user-credentials"></a>Die Benutzer Anmelde Informationen konnten nicht überprüft werden.  
**Szenario**. Der Benutzer kann sich nicht mit OTP authentifizieren, weil der folgende Fehler aufgetreten ist: "Authentifizierung aufgrund eines internen Fehlers fehlgeschlagen"  
  
**Fehler** (Client Computer). Es ist ein Fehler aufgetreten, während Windows Ihre Anmelde Informationen überprüfte. Versuchen Sie es erneut, oder bitten Sie Ihren Administrator um Hilfe.  
  
**Ursache**  
  
Das Kerberos-Authentifizierungsprotokoll funktioniert nicht, wenn das Registrierungszertifikat für den DirectAccess-OTP keine CRL enthält. Das Registrierungszertifikat für das DirectAccess-OTP enthält keine CRL:  
  
-   Die "DirectAccess OTP"-Anmeldevorlage wurde mit der Option " **keine Sperrinformationen in ausgestellten Zertifikaten einschließen**" konfiguriert.  
  
-   Die Zertifizierungsstelle ist so konfiguriert, dass keine CRLs veröffentlicht werden.  
  
**Lösung**  
  
1.  Um die Ursache für diesen Fehler zu überprüfen, klicken Sie in der Remote Zugriffs-Verwaltungskonsole in **Schritt 2**RAS-Server auf **Bearbeiten**, und klicken Sie dann im Setup-Assistenten für den **Remote Zugriffs Server** auf **OTP-Zertifikat Vorlagen**. Notieren Sie sich die Zertifikat Vorlage, die für die Registrierung von Zertifikaten verwendet wird, die für die OTP-Authentifizierung ausgestellt werden. Öffnen Sie die Zertifizierungsstellen Konsole, klicken Sie im linken Bereich auf **Zertifikat Vorlagen**, doppelklicken Sie auf das OTP-Anmeldezertifikat, um die Eigenschaften der Zertifikat Vorlage anzuzeigen.  
  
    Um dieses Problem zu beheben, konfigurieren Sie ein Zertifikat für das OTP-Anmeldezertifikat, und aktivieren Sie im Dialogfeld Vorlagen Eigenschaften auf der Registerkarte **Server** das Kontrollkästchen keine Sperr **Informationen in ausgestellten Zertifikaten einschließen** .  
  
2.  Öffnen Sie auf dem Zertifizierungsstellen Server die MMC der Zertifizierungsstelle, klicken Sie mit der rechten Maustaste auf die ausstellende Zertifizierungsstelle **und klicken** Vergewissern Sie sich auf der Registerkarte **Erweiterungen** , dass die CRL-Veröffentlichung ordnungsgemäß konfiguriert ist.  
  


