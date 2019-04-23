---
title: Problembehandlung bei Authentifizierungsfehlern
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71307757-f8f4-4f82-b8b3-ffd4fd8c5d6d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ff1dd94db3e433235a87fd6809459283fc439d0d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855741"
---
# <a name="troubleshooting-authentication-issues"></a>Problembehandlung bei Authentifizierungsfehlern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Problembehandlungsinformationen für Probleme im Zusammenhang mit Problemen, dass der Benutzer möglicherweise beim Versuch, eine Verbindung mit DirectAccess mit OTP-Authentifizierung. DirectAccerss OTP bezogene Ereignisse werden protokolliert, auf dem Clientcomputer in der Ereignisanzeige unter **Applications and Services Logs/Microsoft/Windows/OtpCredentialProvider**. Stellen Sie sicher, dass dieses Protokoll bei der Behandlung von Problemen mit DirectAccess-OTP aktiviert ist.  
  
## <a name="failed-to-access-the-ca-that-issues-otp-certificates"></a>Fehler bei die Zertifizierungsstelle, die OTP-Zertifikate ausstellt, den Zugriff auf  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). OTP-zertifikatregistrierung für Benutzer <username> auf Zertifizierungsstellenserver < CA_name >, Anforderungsfehlern fehlgeschlagene, mögliche Fehlerursachen: CA-Servername kann nicht aufgelöst werden kann, CA-Server kann nicht über die ersten DirectAccess-Tunnel zugegriffen werden, oder die Verbindung mit dem CA-Server kann nicht hergestellt werden.  
  
**Ursache**  
  
Vom Benutzer bereitgestellten ein gültiger Einmalkennwort und der DirectAccess-Server signiert die zertifikatanforderung; Allerdings kann nicht der Clientcomputer die Zertifizierungsstelle wenden Sie sich an, die OTP-Zertifikate, um den Registrierungsprozess abzuschließen ausstellt.  
  
**Lösung**  
  
Führen Sie auf dem DirectAccess-Server die folgenden Windows PowerShell-Befehle ein:  
  
1.  Ruft die Liste der konfigurierten OTP ausstellende Zertifizierungsstellen, und überprüfen Sie den Wert von "ZS"-Server: `Get-DAOtpAuthentication`  
  
2.  Stellen Sie sicher, dass die Zertifizierungsstellen als einen Verwaltungsserver konfiguriert sind: `Get-DAMgmtServer -Type All`  
  
3.  Stellen Sie sicher, dass der Clientcomputer den infrastrukturtunnel eingerichtet hat: Erweitern Sie in der Windows-Firewall mit erweiterter Sicherheit-Konsole, **Überwachung/Sicherheitszuordnungen**, klicken Sie auf **Hauptmodus**, und stellen Sie sicher, dass die IPsec-sicherheitszuordnungen mit dem richtigen Remoterepository angezeigt werden. Adressen für die DirectAccess-Konfiguration.  
  
## <a name="directaccess-server-connectivity-issues"></a>DirectAccess-Server-Verbindungsprobleme  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls)  
  
Eine der folgenden Fehler:  
  
-   Eine Verbindung kann nicht mit RAS-Server < DirectAccess_server_hostname > mit Basispfad < OTP_authentication_path > und < OTP_authentication_port >-Port hergestellt werden. Fehlercode: < Internal_error_code >.  
  
-   Anmeldeinformationen des Benutzers können nicht auf dem RAS-Server < DirectAccess_server_hostname > mit Basispfad < OTP_authentication_path > und < OTP_authentication_port >-Port gesendet werden. Fehlercode: < Internal_error_code >.  
  
-   Eine Antwort wurde nicht vom RAS-Server < DirectAccess_server_hostname > mit Basispfad < OTP_authentication_path > und < OTP_authentication_port >-Port empfangen. Fehlercode: < Internal_error_code >.  
  
**Ursache**  
  
Der Clientcomputer kann nicht den DirectAccess-Server über das Internet durch entweder Netzwerkprobleme oder durch einen falsch konfigurierten IIS-Server, auf dem DirectAccess-Server zugreifen.  
  
**Lösung**  
  
Stellen Sie sicher, dass die Internetverbindung auf dem Clientcomputer ausgeführt wird, und stellen Sie sicher, dass der DirectAccess-Dienst über das Internet ausgeführt werden und zugänglich ist.  
  
## <a name="failed-to-enroll-for-the-directaccess-otp-logon-certificate"></a>Fehler bei der Registrierung für das Zertifikat für die DirectAccess-OTP-Anmeldung  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). Fehler bei der Registrierung von Zertifikaten von Zertifizierungsstellen < CA_name >. Die Anforderung nicht wie erwartet vom OTP-Signaturzertifikat signiert wurde, oder der Benutzer verfügt nicht über die Berechtigung zum Registrieren von.  
  
**Ursache**  
  
Die vom Benutzer bereitgestellte Einmalkennwort war richtig, aber die ausstellende Zertifizierungsstelle (CA) zum Ausstellen des Zertifikats für die OTP-Anmeldung abgelehnt. Die zertifikatanforderung ist möglicherweise nicht ordnungsgemäß signiert mit den richtigen EKU (Anwendung-OTP Registrierungsrichtlinie Authority) oder der Benutzer verfügt nicht über die Berechtigung "Registrieren" auf der DA OTP-Vorlage.  
  
**Lösung**  
  
Stellen Sie sicher, dass DirectAccess-OTP-Benutzern die Berechtigung zum Registrieren für das Zertifikat für die DirectAccess-OTP-Anmeldung und die richtige "Anwendungsrichtlinie" in die DA OTP-Registrierungsstelle, die Anmeldung der Vorlage enthalten ist. Außerdem stellen Sie sicher, dass der DirectAccess-registrierungsstellenzertifikats auf dem RAS-Server gültig ist. 3.2 Planung der OTP-Zertifikatvorlage und 3.3 Planen der registrierungsstellenzertifikats angezeigt.  
  
## <a name="missing-or-invalid-computer-account-certificate"></a>Computer-Kontozertifikat fehlt oder ist ungültig  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls).  OTP-Authentifizierung kann nicht abgeschlossen werden, da für OTP erforderliche Computerzertifikat im Zertifikatspeicher des lokalen Computers nicht gefunden werden kann.  
  
**Ursache**  
  
DirectAccess-OTP-Authentifizierung muss ein Clientzertifikat für die Computer zum Herstellen einer SSL-Verbindung mit dem DirectAccess-Server; Allerdings wird das Clientcomputerzertifikat wurde nicht gefunden oder ist ungültig, z. B. wenn das Zertifikat abgelaufen.  
  
**Lösung**  
  
Stellen Sie sicher, dass das Computerzertifikat vorhanden und gültig ist:  
  
1.  Öffnen Sie auf dem Clientcomputer in der Konsole des MMC-Zertifikate, für das lokale Computerkonto **persönlich/Zertifikate**.  
  
2.  Stellen Sie sicher, dass ein Zertifikat, der mit übereinstimmt den Computernamen ausgestellt vorhanden ist, und doppelklicken Sie auf das Zertifikat.  
  
3.  Auf der **Zertifikat** Dialogfeld auf die **Zertifikatpfad** Registerkarte **Zertifikatstatus**, stellen Sie sicher, dass dieser sagt "dieses Zertifikat ist gültig."  
  
Wenn Sie ein gültiges Zertifikat nicht gefunden wird, löschen Sie die ungültigen Zertifikats (falls vorhanden) und erneut registrieren, für das Zertifikat des Computers durch entweder die Ausführung `gpupdate /Force` über eine Eingabeaufforderung mit erhöhten Rechten oder Neustart des Clientcomputers.  
  
## <a name="missing-ca-that-issues-otp-certificates"></a>Fehlende Zertifizierungsstelle, die OTP-Zertifikate ausstellt  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). OTP-Authentifizierung kann nicht abgeschlossen werden, weil der Directaccess-Server keine Adresse einer ausstellenden Zertifizierungsstelle zurückgegeben hat.  
  
**Ursache**  
  
Es sind keine Zertifizierungsstellen, die konfigurierte OTP-Zertifikate ausstellen oder alle konfigurierten CAs, die OTP-Zertifikate ausstellen sind nicht mehr reagiert.  
  
**Lösung**  
  
1.  Verwenden Sie den folgenden Befehl zum Abrufen der Liste der Zertifizierungsstellen, die OTP-Zertifikate ausstellen (die ZS-Name wird im ZS-Server dargestellt): `Get-DAOtpAuthentication`.  
  
2.  Wenn keine Zertifizierungsstellen konfiguriert sind:  
  
    1.  Verwenden Sie entweder den Befehl `Set-DAOtpAuthentication` oder die Remotezugriffs-Verwaltungskonsole zum Konfigurieren der Zertifizierungsstellen, die die DirectAccess-OTP Anmeldung Zertifikat ausstellen.  
  
    2.  Die neue Konfiguration anzuwenden und zu erzwingen, dass die Clients aktualisieren Sie die Einstellungen des DirectAccess-Gruppenrichtlinienobjekte mit `gpupdate /Force` über eine Eingabeaufforderung mit erhöhten Rechten oder der Clientcomputer neu gestartet.  
  
3.  Stellen Sie CAs konfiguriert sind, sicher, dass sie online und reagiert auf registrierungsanforderungen sind.  
  
## <a name="misconfigured-directaccess-server-address"></a>Falsch konfigurierte Adresse des DirectAccess-Servers  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). OTP-Authentifizierung nicht wie erwartet abgeschlossen werden. Der Name oder die Adresse des RAS-Server kann nicht bestimmt werden.  Fehlercode: < Error_code >. DirectAccess-Einstellungen sollten vom Serveradministrator überprüft werden.  
  
**Ursache**  
  
Die Adresse des DirectAccess-Servers ist nicht ordnungsgemäß konfiguriert.  
  
**Lösung**  
  
Überprüfen Sie die konfigurierte DirectAccess Server Adresse mit `Get-DirectAccess` und korrigieren Sie die Adresse ein, wenn sie falsch ist.  
  
Stellen Sie sicher, dass die aktuellen Einstellungen auf dem Clientcomputer bereitgestellt werden, indem Sie ausführen `gpupdate /force` aus einer Eingabeaufforderung mit erhöhten Rechten oder starten Sie den Clientcomputer.  
  
## <a name="failed-to-generate-the-otp-logon-certificate-request"></a>Fehler beim Generieren der zertifikatanforderung von OTP-Anmeldung  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). Die zertifikatanforderung für OTP-Authentifizierung kann nicht initialisiert werden. Entweder ein privater Schlüssel kann nicht generiert werden, oder Benutzer <username> Zertifikatvorlage < OTP_template_name > auf dem Domänencontroller kann nicht zugegriffen werden kann.  
  
**Ursache**  
  
Es gibt zwei mögliche Ursachen für diesen Fehler aus:  
  
-   Der Benutzer verfügt nicht über die Berechtigung zum Lesen der Vorlage der OTP-Anmeldung.  
  
-   Den Domänencontroller kann nicht von dem Computer des Benutzers aufgrund von Netzwerkproblemen zugreifen.  
  
**Lösung**  
  
-   Überprüfen Sie die Berechtigungen, die in der Vorlage der OTP-Anmeldung festlegen, und stellen Sie sicher, dass alle Benutzer, die für DirectAccess-OTP bereitgestellt "Leseberechtigung".  
  
-   Stellen Sie sicher, dass der Domänencontroller wie ein Verwaltungsserver konfiguriert ist, dass Client-Computer den Domänencontroller über den infrastrukturtunnel erreichbar sind. Planen Sie die OTP-Zertifikatvorlage finden Sie unter 3.2.  
  
## <a name="no-connection-to-the-domain-controller"></a>Keine Verbindung mit dem Domänencontroller  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). Eine Verbindung mit dem Domänencontroller für die OTP-Authentifizierung kann nicht hergestellt werden. Fehlercode: < Error_code >.  
  
**Ursache**  
  
Es gibt zwei mögliche Ursachen für diesen Fehler aus:  
  
-   Dem Computer des Benutzers über keine Netzwerkverbindung verfügt.  
  
-   Der Domänencontroller nicht zugegriffen werden kann, über den infrastrukturtunnel.  
  
**Lösung**  
  
-   Stellen Sie sicher, dass der Domänencontroller wie ein Verwaltungsserver konfiguriert ist, durch den folgenden Befehl an einer PowerShell-Eingabeaufforderung ausführen: `Get-DAMgmtServer -Type All`.  
  
-   Stellen Sie sicher, dass der Client-Computer den Domänencontroller über den infrastrukturtunnel erreichbar sind.  
  
## <a name="otp-provider-requires-challengeresponse"></a>OTP-Anbieter erfordert die Abfrage/Rückmeldung  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). OTP-Authentifizierung mit RAS-Server (< DirectAccess_server_name >) für den Benutzer (<username>) eine Aufforderung des Benutzers erforderlich.  
  
**Ursache**  
  
Der OTP-Anbieter verwendet, muss der Benutzer zusätzliche Berechtigungen in Form einer RADIUS-Abfrage/Rückmeldung-Exchange zu erstellen, die von Windows Server 2012 DirectAccess-OTP nicht unterstützt wird.  
  
**Lösung**  
  
Konfigurieren des OTP-Anbieters, um die Abfrage/Rückmeldung in jedem Szenario nicht erforderlich.  
  
## <a name="incorrect-otp-logon-template-used"></a>Falsch verwendete OTP-anmelden-Vorlage  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). Die zertifizierungsstellenvorlage, aus denen die Benutzer <username> angefordert wird, ein Zertifikat ist nicht für das Ausstellen von Zertifikaten für OTP konfiguriert.  
  
**Ursache**  
  
Die DirectAccess-OTP-anmelden-Vorlage ersetzt wurde, und der Clientcomputer für die Authentifizierung mit einer älteren Vorlage versucht.  
  
**Lösung**  
  
Stellen Sie sicher, dass der Clientcomputer die neueste OTP-Konfiguration verwendet wird, indem Sie eine der folgenden ausführen:  
  
-   Aktualisierung der Gruppenrichtlinie zu erzwingen, indem Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen: `gpupdate /Force`.  
  
-   Starten Sie den Clientcomputer neu.  
  
## <a name="missing-otp-signing-certificate"></a>OTP-Signaturzertifikat fehlt  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls). Ein OTP-Signaturzertifikat wurde nicht gefunden. Der OTP-zertifikatregistrierungsanforderung werden nicht signiert.  
  
**Ursache**  
  
Der DirectAccess-OTP-Signaturzertifikat auf dem RAS-Server wurde nicht gefunden; aus diesem Grund kann nicht die zertifikatanforderung für Benutzer von RAS-Server signiert werden. Es gibt kein Signaturzertifikat oder das Signaturzertifikat ist abgelaufen und wurde nicht verlängert.  
  
**Lösung**  
  
Führen Sie diese Schritte aus, auf dem RAS-Server.  
  
1.  Überprüfen Sie die konfigurierten OTP Signieren den Namen der Zertifikatvorlage durch Ausführen des PowerShell-Cmdlets `Get-DAOtpAuthentication` und überprüfen Sie den Wert der `SigningCertificateTemplateName`.  
  
2.  Verwenden Sie das Zertifikate-MMC-Snap-in, um sicherzustellen, dass ein gültiges Zertifikat, das aus dieser Vorlage registriert auf dem Computer vorhanden ist.  
  
3.  Wenn kein Zertifikat vorhanden ist, Löschen von abgelaufenen Zertifikats (falls vorhanden), und registrieren Sie ein neues Zertifikat auf Basis dieser Vorlage.  
  
Die OTP-Signatur erstellen Zertifikatvorlage finden Sie unter 3.3 Plan Zertifikat der Registrierung.  
  
## <a name="missing-or-incorrect-upndn-for-the-user"></a>Fehlende oder falsche UPN/DN für den Benutzer  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Ereignisprotokolls)  
  
Eine der folgenden Fehler:  
  
-   Benutzer <username> mit OTP nicht authentifiziert werden können. Stellen Sie sicher, dass ein UPN für den Benutzernamen in Active Directory definiert ist. Fehlercode: < Error_code >.  
  
-   Benutzer <username> mit OTP nicht authentifiziert werden können. Stellen Sie sicher, dass ein DN für den Benutzernamen in Active Directory definiert ist. Fehlercode: < Error_code >.  
  
**Fehler** (Server-Ereignisprotokoll)  
  
Der Benutzername <username> angegeben, für die OTP-Authentifizierung nicht vorhanden ist.  
  
**Ursache**  
  
Der Benutzer verfügt nicht über die Benutzer Benutzerprinzipalname (UPN) oder Distinguished Name (DN) Attribute ordnungsgemäß festgelegt, das Benutzerkonto, diese Eigenschaften sind für das ordnungsgemäße Funktionieren von DirectAccess-OTP erforderlich.  
  
**Lösung**  
  
Verwenden Sie die Konsole Active Directory-Benutzer und-Computer auf dem Domänencontroller, um sicherzustellen, dass beide Attribute für den authentifizierenden Benutzer ordnungsgemäß festgelegt sind.  
  
## <a name="otp-certificate-is-not-trusted-for-login"></a>OTP-Zertifikat ist nicht vertrauenswürdig für die Anmeldung  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Ursache**  
  
Die Zertifizierungsstelle, die OTP-Zertifikate ausstellt, ist nicht in der Enterprise NTAuth-Speicher; aus diesem Grund können die Registrierung von Zertifikaten für die Anmeldung verwendet werden. Dies kann in Umgebungen mit mehreren Domäne und mit mehreren Gesamtstrukturen auftreten, in denen domänenübergreifende Vertrauensstellungen zwischen Zertifizierungsstellen nicht hergestellt wird.  
  
**Lösung**  
  
Stellen Sie sicher, dass das Zertifikat des Stamms der Hierarchie, die OTP-Zertifikate ausstellt, in der Enterprise NTAuth-Zertifikat zu speichern, von der Domäne installiert ist, zu dem der Benutzer versucht, zu authentifizieren.  
  
## <a name="windows-could-not-verify-user-credentials"></a>Windows konnte Anmeldeinformationen des Benutzers nicht überprüft werden.  
**Szenario**. Benutzer nicht authentifizieren, Fehler OTP mit: "Fehler bei der Authentifizierung aufgrund eines internen Fehlers"  
  
**Fehler** (Client-Computer). Es ist leider während Windows Ihre Anmeldeinformationen überprüft wurde. Versuchen Sie es erneut, oder bitten Sie Ihren Administrator um Hilfe zu erhalten.  
  
**Ursache**  
  
Das Kerberos-Authentifizierungsprotokoll funktioniert nicht, wenn das Zertifikat für die DirectAccess-OTP-Anmeldung keine Zertifikatsperrliste enthalten ist. Das Zertifikat für die DirectAccess-OTP-Anmeldung ist eine CRL nicht enthalten, da entweder:  
  
-   Die Vorlage der DirectAccess-OTP-Anmeldung konfiguriert wurde, mit der Option **beinhalten keine Informationen zum Widerrufen in ausgestellten Zertifikaten**.  
  
-   Die Zertifizierungsstelle ist nicht zum Veröffentlichen von Zertifikatsperrlisten konfiguriert.  
  
**Lösung**  
  
1.  Um die Ursache für diesen Fehler, in der Remotezugriffs-Verwaltungskonsole, zu bestätigen **Schritt 2 RAS-Server**, klicken Sie auf **bearbeiten**, und klicken Sie dann in der **RAS-Server-Setup** Assistenten, klicken Sie auf **OTP-Zertifikatvorlagen**. Notieren Sie sich von der Zertifikatvorlage, die verwendet werden, für die Registrierung von Zertifikaten, die für die OTP-Authentifizierung ausgegeben werden. Öffnen der Zertifizierungsstellen-Verwaltungskonsole im linken Bereich, klicken Sie auf **Zertifikatvorlagen**, doppelklicken Sie auf die OTP-Zertifikats für die Anmeldung zum Anzeigen der Eigenschaften der Zertifikatvorlage.  
  
    Um dieses Problem zu beheben, konfigurieren Sie ein Zertifikat für das Zertifikat für die OTP-Anmeldung, und aktivieren Sie nicht die **beinhalten keine Informationen zum Widerrufen in ausgestellten Zertifikaten** auf das Kontrollkästchen der **Server** Registerkarte der Vorlage Dialogfeld "Eigenschaften".  
  
2.  Auf dem Zertifizierungsstellenserver an, öffnen Sie die Zertifizierungsstellen-MMC, klicken Sie mit der rechten Maustaste auf die ausstellende Zertifizierungsstelle aus, und klicken Sie auf **Eigenschaften**. Auf der **Erweiterungen** Registerkarte stellen Sie sicher, dass die Veröffentlichung der Zertifikatsperrliste ordnungsgemäß konfiguriert ist.  
  


