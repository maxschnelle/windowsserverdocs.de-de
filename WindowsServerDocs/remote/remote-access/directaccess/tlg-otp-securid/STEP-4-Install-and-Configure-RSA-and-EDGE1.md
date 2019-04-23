---
title: Schritt 4 installieren und Konfigurieren von RSA und EDGE1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d46ede6f-1a21-414d-b8c3-6b5c87344b9d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5bb28ff6131c371e4b2f668fd20ec0a6133a0099
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860001"
---
# <a name="step-4-install-and-configure-rsa-and-edge1"></a>Schritt 4 installieren und Konfigurieren von RSA und EDGE1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

RSA ist der RADIUS- und der OTP-Server, und vor dem Konfigurieren von RADIUS und OTP installiert ist.  
  
Sie führt die folgenden Schritte aus, um den RSA-Bereitstellung zu konfigurieren:  
  
1. Installieren des Betriebssystems auf dem RSA-Server an. Installieren Sie Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 auf der RSA-Server an.  
  
2. Konfigurieren von TCP/IP auf RSA. Konfigurieren Sie TCP/IP-Einstellungen auf der RSA-Server.  
  
3. Kopieren Sie Authentifizierungs-Manager-Installationsdateien auf den RSA-Server. Nach der Installation des Betriebssystems auf RSA, die Authentifizierungs-Manager Dateien auf den RSA-Computer kopieren.  
  
4. Fügen Sie den RSA-Server in der Domäne CORP an. Verknüpfen Sie RSA, mit der CORP-Domäne.  
  
5. Deaktivieren Sie die Windows-Firewall auf RSA. Deaktivieren Sie die Windows-Firewall auf den RSA-Server.  
  
6. Installieren Sie RSA Authentication Manager auf dem RSA-Server. RSA Authentication Manager zu installieren.  
  
7. Konfigurieren Sie RSA Authentication Manager. Konfigurieren Sie die Authentifizierungs-Manager.  
  
8. Erstellen Sie DAProbeUser. Erstellen Sie ein Benutzerkonto für den Test-Zwecke.  
  
9. Installieren Sie RSA SecurID-Software-Token auf "client1" an. Installieren Sie RSA SecurID-Software-Token auf "client1" an.  
  
10. Konfigurieren von EDGE1 als RSA Authentication Agent. Konfigurieren Sie auf EDGE1 RSA Authentication Agent.  
  
11. Konfigurieren von EDGE1 zu OTP-Authentifizierung unterstützen. Konfigurieren von Einmalkennwörtern für DirectAccess, und überprüfen Sie die Konfiguration.  
  
## <a name="InstallOS"></a>Installieren des Betriebssystems auf dem RSA-server  
  
1.  Starten Sie auf RSA die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 aus.  
  
2.  Führen Sie die Anweisungen zum Abschließen der Installations und geben Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administratorkonto an. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  Verbinden Sie RSA mit einem Netzwerk, das über Internetzugriff verfügt, und führen Sie Windows Update, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 installieren, und klicken Sie dann aus dem Internet zu trennen.  
  
4.  Verbinden Sie RSA, mit dem Subnetz "Corpnet".  
  
## <a name="TCP"></a>Konfigurieren von TCP/IP auf RSA  
  
1.  Aufgaben zur Erstkonfiguration, klicken Sie auf **Netzwerk konfigurieren**.  
  
2.  In **Netzwerkverbindungen**, mit der rechten Maustaste **LAN-Verbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie im Feld **IP-Adresse**die Adresse **10.0.0.5**ein. Geben Sie im Feld **Subnetzmaske**den Wert **255.255.255.0**ein. In **Standardgateway**, Typ **10.0.0.2**. Klicken Sie auf **verwenden Sie die folgenden DNS-Serveradressen**im **Bevorzugter DNS-Server**, Typ **10.0.0.1**.  
  
5.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
6.  In **DNS-Suffix für diese Verbindung**, Typ **"corp.contoso.com"**, und klicken Sie dann auf **OK** zweimal.  
  
7.  Auf der **Eigenschaften von LAN-Verbindung** Dialogfeld klicken Sie auf **schließen**.  
  
8.  Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="copyinstfiles"></a>Kopieren von Authentifizierungs-Manager-Installationsdateien auf den RSA-server  
  
1.  Erstellen Sie den Ordner C:\RSA-Installation, auf dem RSA-Server.  
  
2.  Kopieren Sie den Inhalt der Medien RSA Authentication Manager 7.1 SP4, in den C:\RSA-Installationsordner.  
  
3.  Erstellen Sie die Unterordner C:\RSA Installation\License und -Token.  
  
4.  Kopieren Sie die Lizenzdateien RSA C:\RSA Installation\License und Token.  
  
## <a name="JoinDomain"></a>Verknüpfen des RSA-Servers mit der CORP-Domäne  
  
1.  Mit der rechten Maustaste **Arbeitsplatz**, und klicken Sie auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Ändern**.  
  
3.  In **Computername**, Typ **RSA**. In **Mitglied**, klicken Sie auf **Domäne**, Typ **"corp.contoso.com"**, und klicken Sie auf **OK**.  
  
4.  Wenn Sie für einen Benutzernamen und Kennwort aufgefordert werden, geben Sie **"user1"** und dieses Kennwort, und die auf **OK**.  
  
5.  Klicken Sie auf der Domäne begrüßt im Dialogfeld auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Geben Sie nach dem Neustart des Computers, **"user1"** und das Kennwort ein, wählen Sie die CORP in die **melden Sie sich an:** Dropdown-Liste, und klicken Sie auf **OK**.  
  
## <a name="BKMK_Firewall"></a>Deaktivieren von Windows-Firewall auf RSA  
  
1.  Klicken Sie auf **starten**, klicken Sie auf **Systemsteuerung**, klicken Sie auf **System und Sicherheit**, und klicken Sie auf **Windows-Firewall**.  
  
2.  Klicken Sie auf **Windows-Firewall ein- oder ausschalten**.  
  
3.  **Deaktivieren Sie Windows-Firewall** für alle Einstellungen.  
  
4.  Klicken Sie auf **OK** und Windows-Firewall zu schließen.  
  
## <a name="install"></a>Installieren Sie RSA Authentication Manager auf dem RSA-Server.  
  
1.  Wenn Sie die Sicherheitswarnung-Nachricht zu einem beliebigen Zeitpunkt während des Prozesses angezeigt werden soll, klicken Sie auf **ausführen** um den Vorgang fortzusetzen.  
  
2.  Öffnen Sie den C:\RSA-Installationsordner, und doppelklicken Sie auf **autorun.exe**.  
  
3.  Klicken Sie auf **jetzt installieren**, klicken Sie auf **Weiter**, wählen Sie die Top-Option für Amerika, und klicken Sie auf **Weiter**.  
  
4.  Wählen Sie **ich stimme den Bedingungen des Lizenzvertrags**, und klicken Sie auf **Weiter**.  
  
5.  Wählen Sie **primäre Instanz**, und klicken Sie auf **Weiter**.  
  
6.  In der **Verzeichnisname:** Feldtyp **C:\RSA**, und klicken Sie auf **Weiter**.  
  
7.  Überprüfen Sie den Servernamen (RSA.corp.contoso.com) und die IP-Adresse richtig sind, und klicken Sie auf **Weiter**.  
  
8.  Navigieren Sie zu C:\RSA Installation\License und Token, und klicken Sie auf **Weiter**.  
  
9. Auf der **überprüfen Lizenzdatei** auf **Weiter**.  
  
10. In der **Benutzer-ID** Feldtyp **Administrator**, und klicken Sie in der **Kennwort** und **Kennwort bestätigen** Felder Geben Sie ein sicheres Kennwort ein. Klicken Sie auf **Weiter**.  
  
11. Klicken Sie auf dem Auswahlbildschirm des Protokolls, akzeptieren Sie die Standardeinstellungen, und klicken Sie auf **Weiter**.  
  
12. Klicken Sie auf dem Bildschirm mit der Zusammenfassung auf **installieren**.  
  
13. Nachdem die Installation abgeschlossen ist, klicken Sie auf **Fertig stellen**.  
  
## <a name="confiauthmgr"></a>RSA Authentication Manager konfigurieren  
  
1.  Wenn der RSA Security-Konsole nicht automatisch geöffnet wird, doppelklicken Sie dann auf den RSA-PC-Desktop auf "RSA Security-Konsole".  
  
2.  Wenn die Sicherheit Warnung Zertifikat / sicherheitswarnung angezeigt, klicken Sie auf **Laden dieser Website fortsetzen** oder klicken Sie auf **Ja** um fortzusetzen, und fügen Sie diese Website zu vertrauenswürdigen Sites gegebenenfalls.  
  
3.  In der **Benutzer-ID** Feldtyp **Administrator** , und klicken Sie auf **OK**.  
  
4.  In der **Kennwort** Feld das Kennwort für das Administratorkonto ein, und klicken Sie auf **anmelden**.  
  
5.  Fügen Sie die Token-Informationen.  
  
    1.  In der **RSA Security-Konsole** klicken Sie auf **Authentifizierung** , und klicken Sie auf **SecurID-Token**.  
  
    2.  Klicken Sie auf **Token Importauftrag**, und klicken Sie dann auf **Add New**.  
  
    3.  In der **Importoptionen** Abschnitt auf **Durchsuchen**. Navigieren Sie zu, und wählen Sie die Token-XML-Datei in die C:\ RSA Installation\License und Token-Ordner, und klicken Sie auf **öffnen**.  
  
    4.  Klicken Sie auf **Submit Job** am unteren Rand der Seite.  
  
6.  OTP-neuen Benutzer zu erstellen.  
  
    1.  In der **RSA Security-Konsole** klicken Sie auf die **Identität** auf **Benutzer**, und klicken Sie auf **Add New**.  
  
    2.  In der **Nachname:** Abschnitt Typ **Benutzer**, und klicken Sie in der **Benutzer-ID:** Abschnitt Typ **"user1"** (Benutzer-ID muss identisch mit der AD-Benutzername, der zum Dieses Lab).  In der **Kennwort:** und **Kennwort bestätigen:** Abschnitte geben Sie ein sicheres Kennwort ein. Deaktivieren der **"Muss der Benutzer sein Kennwort bei der nächsten Anmeldung ändern"** Kontrollkästchen und klicken Sie auf **speichern**.  
  
7.  Weisen Sie auf eines der importierten Token "user1" ein.  
  
    1.  Auf der **Benutzer** auf **"user1"** , und klicken Sie auf **SecurID-Token**.  
  
    2.  Klicken Sie auf **SecurID-Token** , und klicken Sie auf **Token zuweisen**.  
  
    3.  Unter den **Seriennummer** Überschrift klicken Sie auf die erste Zahl aufgeführt, und klicken Sie auf **weisen**.  
  
    4.  Klicken Sie auf das zugewiesene Token, und klicken Sie auf **bearbeiten**. In der **SecurID-PIN-Verwaltung** Abschnitt **Benutzer die Authentifizierungsanforderung**wählen **erfordern keine PIN (nur Tokencode)**.  
  
    5.  Klicken Sie auf **speichern und Verteilen von Token**.  
  
    6.  Auf der **Verteilen von Software-Token** auf der Seite die **Grundlagen** auf **Problem Token Datei (SDTID)**.  
  
    7.  Auf der **Verteilen von Software-Token** auf der Seite die **Token Dateioptionen** deaktivieren Sie im Abschnitt der **Kopierschutz aktivieren** Kontrollkästchen. Klicken Sie auf **kein Kennwort** und **Weiter**.  
  
    8.  Auf der **Verteilen von Software-Token** auf der Seite die **Herunterladen der Datei** auf **jetzt herunterladen**. Klicken Sie auf **Speichern**. Navigieren Sie zu C:\RSA-Installation, und klicken Sie auf **speichern** und **schließen**.  
  
    9. Minimieren der **RSA Security-Konsole** zur späteren Verwendung.  
  
8.  Konfigurieren Sie Authentifizierungs-Manager als RADIUS-Server.  
  
    1.  Klicken Sie auf den desktop Doppelklick des RSA-Computer **"RSA Security Operations-Konsole"**.  
  
    2.  Wenn die Sicherheit Warnung Zertifikat / sicherheitswarnung angezeigt, klicken Sie auf **Laden dieser Website fortsetzen** oder klicken Sie auf **Ja** fortfahren und diesen Standort zu vertrauenswürdigen Websites hinzufügen werden, wenn angefordert.  
  
    3.  Geben Sie den Benutzer-ID und das Kennwort ein, und klicken Sie auf **anmelden**.  
  
    4.  Klicken Sie auf **Bereitstellungskonfiguration - RADIUS - Konfiguration**.  
  
    5.  Auf der **zusätzliche Administratoranmeldeinformationen erforderlich** Seite Geben Sie den Administrator-Benutzer-ID und das Kennwort, und klicken Sie auf **OK**.  
  
    6.  Auf der **RADIUS-Server konfigurieren** Seite Geben Sie das gleiche Kennwort für den Administratorbenutzer für die **Geheimnisse** und **Masterkennwort**. Geben Sie den Administrator-Benutzer-ID und das Kennwort ein, und klicken Sie auf **konfigurieren**.  
  
    7.  Überprüfen Sie, ob die Nachricht **"wurde erfolgreich konfiguriert RADIUS-Server"** wird angezeigt. Klicken Sie auf **Fertig**. Schließen der **RSA-Betriebskonsole**.  
  
    8.  Wechseln Sie zurück zu den **"RSA Security-Konsole"**.  
  
    9. Auf der **RADIUS** Registerkarte auf **RADIUS-Servern**. Stellen Sie sicher, dass diese rsa.corp.contoso.com aufgeführt ist.  
  
9. Konfigurieren Sie RSA-Server als RSA-Authentifizierungsclient.  
  
    1.  Auf der **RADIUS** auf **RADIUS-Clients** und **Add New**.  
  
    2.  Klicken Sie auf die **ANY RADIUS-Client** Kontrollkästchen.  
  
    3.  Geben Sie ein sicheres Kennwort Ihrer Wahl in der **gemeinsamer geheimer Schlüssel** Feld. Sie werden später beim Konfigurieren von EDGE1 für OTP, das gleiche Kennwort verwenden.  
  
    4.  Lassen Sie die **IP-Adresse** Feld "Blank", und die **stellen / Modell** Eintrag als **Standard RADIUS**.  
  
    5.  Klicken Sie auf **speichern, ohne die RSA-Agent**.  
  
10. Erstellen Sie Dateien, die zum Konfigurieren von EDGE1 als RSA Authentication Agent erforderlich.  
  
    1.  Auf der **Zugriff** Registerkarte, markieren Sie **Authentifizierungs-Agents**, und klicken Sie auf **Add New**.  
  
    2.  Typ **EDGE1** in die **Hostname** ein, und klicken Sie auf **Auflösen von IP-**.  
  
    3.  Beachten Sie, die die IP-Adresse EDGE1 jetzt, in angezeigt wird der **IP-Adresse** Feld. Klicken Sie auf **Speichern**.  
  
11. Generieren Sie eine Konfigurationsdatei für den EDGE1-Server (AM_Config.zip).  
  
    1.  Auf der **Zugriff** Registerkarte, markieren Sie **Authentifizierungs-Agents**, und klicken Sie auf **Konfigurationsdatei generieren**.  
  
    2.  Auf der **Konfigurationsdatei generieren** auf **Config-Datei generieren**, und klicken Sie dann auf **jetzt herunterladen**.  
  
    3.  Klicken Sie auf **speichern**, navigieren Sie zu C:\ RSA-Installation, und klicken Sie auf **speichern**.  
  
    4.  Klicken Sie auf **schließen** auf die **Download beendet** Dialogfeld.  
  
12. Generiert eine geheimnisdatei von Knoten für den EDGE1-Server (EDGE1_NodeSecret.zip).  
  
    1.  Auf der **Zugriff** Registerkarte, markieren Sie **Authentifizierungs-Agents**, und klicken Sie auf **Verwalten vorhandener**.  
  
    2.  Klicken Sie auf den aktuellen konfigurierten Knoten EDGE1, und klicken Sie auf **geheimen Schlüssel Verwalten von Knoten**.  
  
    3.  Überprüfen Sie die **zufälligen Knoten neues Geheimnis erstellen und exportieren Sie den Knoten geheimen Schlüssel in eine Datei** Kontrollkästchen.  
  
    4.  Geben Sie das gleiche Kennwort für den Benutzer mit Administratorrechten in verwendet die **Verschlüsselungskennwort** und **Verschlüsselungskennwort bestätigen** Felder, und klicken Sie auf **speichern**.  
  
    5.  Auf der **Knoten Secret-Datei generiert** auf **jetzt herunterladen**.  
  
    6.  Auf der **Dateidownload** Dialogfeld auf **speichern**, navigieren Sie zu C:\RSA-Installation, und klicken Sie auf **speichern**. Klicken Sie auf **schließen** auf die **Download beendet** Dialogfeld.  
  
    7.  Aus den RSA Authentication Manager Media Kopie \auth_mgr\windows-x86_64\am\rsa-ace_nsload\win32-5.0-x86\agent_nsload.exe C:\RSA-Installation.  
  
## <a name="BKMK_DAProbeUser"></a>Erstellen von DAProbeUser  
  
1.  In der **RSA Security-Konsole** klicken Sie auf die **Identität** auf **Benutzer**, und klicken Sie auf **Add New**.  
  
2.  In der **Nachname:** Abschnitt Typ **Prüfpunkt**, und klicken Sie in der **Benutzer-ID:** Abschnitt Typ **DAProbeUser**. In der **Kennwort:** und **Kennwort bestätigen:** Abschnitte geben Sie ein sicheres Kennwort ein. Deaktivieren der **"Muss der Benutzer sein Kennwort bei der nächsten Anmeldung ändern"** Kontrollkästchen und klicken Sie auf **speichern**.  
  
## <a name="InstToken"></a>Installieren von RSA SecurID-Software-Token auf "client1"  
Verwenden Sie dieses Verfahren, um SecurID-Software-Token auf "client1" zu installieren.  
  
#### <a name="install-securid-software-token"></a>Installieren der SecurID-Software-token  
  
1.  Erstellen Sie den Ordner C:\RSA-Dateien, auf dem Computer "client1". Kopieren Sie die Datei Software_Tokens.zip C:\RSA-Installation auf dem Computer RSA C:\RSA Dateien ein. Extrahieren Sie die Datei User1_000031701832.SDTID C:\RSA Dateien auf CLIENT1 an.  
  
2.  Zugriff auf die Medienquelle RSA SecurID-Software token, und doppelklicken Sie auf RSASECURIDTOKEN410 in die **SecurID SoftwareToken-Client-app** Ordner, um die RSA SecurID-Installation zu starten. Wenn die **Datei öffnen - Sicherheitswarnung** Meldung angezeigt wird, klicken Sie dann auf **ausführen**.  
  
3.  Auf der **RSA SecurID-Software-Token - InstallShield-Assistent** Dialogfeld auf **Weiter** zweimal.  
  
4.  Akzeptieren Sie den Lizenzvertrag, und klicken Sie auf **Weiter**.  
  
5.  Auf der **Setuptyp** Dialogfeld **Standard**, klicken Sie auf **Weiter**, und klicken Sie auf **installieren**.  
  
6.  Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
7.  Wählen Sie die **starten RSA SecurID-Software-Token** , und klicken Sie auf **Fertig stellen**.  
  
8.  Klicken Sie auf **aus Datei importieren**.  
  
9. Klicken Sie auf **Durchsuchen**C:\RSA Files\User1_000031701832.SDTID auswählen, und klicken Sie auf **öffnen**.  
  
10. Klicken Sie zweimal auf **OK** .  
  
## <a name="configAuthAgt"></a>Konfigurieren von EDGE1 als einen RSA-Authentifizierungs-Agent  
Verwenden Sie dieses Verfahren zum Konfigurieren von EDGE1 zum Ausführen der RSA-Authentifizierung.  
  
#### <a name="configure-the-rsa-authentication-agent"></a>Konfigurieren Sie den RSA Authentication Agent  
  
1.  Öffnen Sie Windows Explorer, und erstellen Sie den Ordner C:\RSA-Dateien, auf EDGE1. Navigieren Sie zu den RSA-ACE-Installationsmedien.  
  
2.  Kopieren Sie die agent_nsload.exe Dateien, AM_Config.zip und EDGE1_NodeSecret.zip vom RSA-Medium auf C:\RSA-Dateien.  
  
3.  Extrahieren Sie den Inhalt der beiden Zip-Dateien in der folgenden Speicherorte:  
  
    1.  C:\Windows\system32\  
  
    2.  C:\Windows\SysWOW64\  
  
4.  Copy agent_nsload.exe to C:\Windows\SysWOW64\\.  
  
5.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und navigieren Sie zu C:\Windows\SysWOW64.  
  
6.  Typ **agent_nsload.exe -f nodesecret.rec -p <password>**  , in denen <password> das starke Kennwort, das Sie während der anfänglichen RSA-Konfiguration erstellt wird. Drücken Sie die EINGABETASTE.  
  
7.  Copy C:\Windows\SysWOW64\securid to C:\Windows\System32.  
  
## <a name="configOTP"></a>Konfigurieren von EDGE1 zu OTP-Authentifizierung unterstützen  
Verwenden Sie dieses Verfahren zum Konfigurieren von OTP für DirectAccess, und überprüfen Sie die Konfiguration.  
  
#### <a name="configure-otp-for-directaccess"></a>Konfigurieren von Einmalkennwörtern für DirectAccess  
  
1.  Klicken Sie auf EDGE1, öffnen Sie Server-Manager, und klicken Sie auf **RAS** im linken Bereich.  
  
2.  Mit der rechten Maustaste **EDGE1** in den Bereich "Server", und wählen **Remotezugriffsverwaltung**.  
  
3.  Klicken Sie auf **Konfiguration**.  
  
4.  In der **DirectAccess-Setup** Fenster unter **Schritt2: RAS-Server**, klicken Sie auf **bearbeiten**.  
  
5.  Klicken Sie auf **Weiter** dreimal aus, und klicken Sie in der **Authentifizierung** Abschnitt **zweistufige Authentifizierung** und **OTP verwenden**, und stellen sicher, dass **Computerzertifikate** aktiviert ist. Stellen Sie sicher, dass die Stammzertifizierungsstelle, um festgelegt ist **CN = corp-APP1-CA**. Klicken Sie auf **Weiter**.  
  
6.  In der **OTP RADIUS-Server** Abschnitt, doppelklicken Sie auf die leere **Servernamen** Feld.  
  
7.  In der **Hinzufügen eines RADIUS-Servers** Dialogfelds **RSA** in die **Servernamen** Feld. Klicken Sie auf **Änderung** neben der **gemeinsamer geheimer Schlüssel** ein, und geben Sie das gleiche Kennwort, die Sie beim Konfigurieren der RADIUS-Clients auf dem Server "RSA" in verwendet die **neuer geheimer** und  **Neuen geheimen Schlüssel bestätigen** Felder. Klicken Sie auf **OK** zweimal aus, und klicken Sie auf **Weiter**.  
  
    > [!NOTE]  
    > Wenn der RADIUS-Server in einer Domäne ist, anders als der RAS-Server ist, die **Servernamen** Feld muss den FQDN des RADIUS-Servers angeben.  
  
8.  In der **OTP-Zertifizierungsstellenserver** wählen APP1.corp.contoso.com Abschnitt, und klicken Sie auf **hinzufügen**. Klicken Sie auf **Weiter**.  
  
9. Auf der **OTP-Zertifikatvorlagen** auf **Durchsuchen** , wählen Sie eine Zertifikatvorlage, die verwendet wird, für die Registrierung von Zertifikaten, die ausgegeben werden, für die OTP-Authentifizierung, und auf die  **Zertifikatvorlagen** aktivieren Sie im Dialogfeld **DAOTPLogon**. Klicken Sie auf **OK**. Klicken Sie auf **Durchsuchen** , wählen Sie eine Zertifikatvorlage, die zum Registrieren von OTP-zertifikatregistrierungsanforderungen anmelden und auf die RAS-Server verwendeten Zertifikats verwendet die **Zertifikatvorlagen** (Dialogfeld) Wählen Sie **DAOTPRA**. Klicken Sie auf **OK**. Klicken Sie auf **Weiter**.  
  
10. Auf der **RAS-Server-Setup** auf **Fertig stellen**, und klicken Sie auf **Fertig stellen** auf die **Experten DirectAccess-Assistenten**.  
  
11. Auf der **Überprüfung des Remotezugriffs** Dialogfeld auf **übernehmen**, warten Sie, bis die DirectAccess-Richtlinie aktualisiert werden, und klicken Sie auf **schließen**.  
  
12. Auf der **starten** geben**powershell.exe**, mit der rechten Maustaste **Powershell**, klicken Sie auf **erweitert**, und klicken Sie auf **Ausführen als Administrator**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
13. Geben Sie in Windows PowerShell-Fenster **Gpupdate/force** und drücken Sie EINGABETASTE.  
  
14. Schließen und öffnen Sie die Remotezugriffs-Verwaltungskonsole, und stellen Sie sicher, dass alle OTP-Einstellungen richtig sind.  
  


