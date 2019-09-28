---
title: Schritt 4 installieren und Konfigurieren von RSA und Edge1
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d46ede6f-1a21-414d-b8c3-6b5c87344b9d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3519e9d6e89b26a733b6b0178334f86e284bddfb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404760"
---
# <a name="step-4-install-and-configure-rsa-and-edge1"></a>Schritt 4 installieren und Konfigurieren von RSA und Edge1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

RSA ist der RADIUS-und OTP-Server und wird vor dem Konfigurieren von RADIUS und OTP installiert.  
  
Zum Konfigurieren der RSA-Bereitstellung führen Sie die folgenden Schritte aus:  
  
1. Installieren Sie das Betriebssystem auf dem RSA-Server. Installieren Sie Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 auf dem RSA-Server.  
  
2. Konfigurieren von TCP/IP auf RSA Konfigurieren Sie die TCP/IP-Einstellungen auf dem RSA-Server.  
  
3. Kopieren Sie die Authentifizierungs-Manager-Installationsdateien auf den RSA-Server. Nachdem Sie das Betriebssystem auf RSA installiert haben, kopieren Sie die Authentifizierungs-Manager-Dateien auf den RSA-Computer.  
  
4. Fügen Sie den RSA-Server der Corp-Domäne hinzu. Verknüpfen Sie RSA mit der Corp-Domäne.  
  
5. Deaktivieren Sie die Windows-Firewall auf RSA. Deaktivieren Sie die Windows-Firewall auf dem RSA-Server.  
  
6. Installieren Sie den RSA Authentication Manager auf dem RSA-Server. Installieren Sie den RSA Authentication Manager.  
  
7. Konfigurieren Sie den RSA Authentication Manager. Konfigurieren Sie den Authentifizierungs-Manager.  
  
8. Erstellen Sie daprobeuser. Erstellen Sie ein Benutzerkonto zu Testzwecken.  
  
9. Installieren Sie das RSA SecurID-Software Token auf CLIENT1. Installieren Sie das RSA SecurID-Software Token auf CLIENT1.  
  
10. Konfigurieren Sie Edge1 als RSA-Authentifizierungs-Agent. Konfigurieren Sie den RSA-Authentifizierungs-Agent auf Edge1.  
  
11. Konfigurieren Sie Edge1 zur Unterstützung der OTP-Authentifizierung. Konfigurieren Sie OTP für DirectAccess, und überprüfen Sie die Konfiguration.  
  
## <a name="InstallOS"></a>Installieren des Betriebssystems auf dem RSA-Server  
  
1.  Starten Sie unter RSA die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
2.  Befolgen Sie die Anweisungen, um die Installation abzuschließen, indem Sie Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administrator Konto angeben. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  Verbinden Sie RSA mit einem Netzwerk, das über Internet Zugriff verfügt, und führen Sie Windows Update aus, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 zu installieren, und trennen Sie dann die Verbindung mit dem Internet.  
  
4.  Stellen Sie eine Verbindung mit dem Subnetz "Corpnet" her.  
  
## <a name="TCP"></a>Konfigurieren von TCP/IP auf RSA  
  
1.  Klicken Sie in Aufgaben zur Erstkonfiguration auf **Netzwerk konfigurieren**.  
  
2.  Klicken Sie unter **Netzwerkverbindungen**mit der rechten Maustaste auf LAN- **Verbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie im Feld **IP-Adresse**die Adresse **10.0.0.5**ein. Geben Sie im Feld **Subnetzmaske**den Wert **255.255.255.0**ein. Geben Sie unter **Standard Gateway**den Namen **10.0.0.2**ein. Klicken Sie auf **folgende DNS-Serveradressen verwenden**, geben Sie unter **Bevorzugter DNS-Server**den Namen **10.0.0.1**ein.  
  
5.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
6.  Geben Sie unter **DNS-Suffix für diese Verbindung** **Corp.contoso.com**ein, und klicken Sie dann zweimal auf **OK** .  
  
7.  Klicken Sie im Dialogfeld Eigenschaften von LAN- **Verbindung** auf **Schließen**.  
  
8.  Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="copyinstfiles"></a>Kopieren von Authentifizierungs-Manager-Installationsdateien auf den RSA-Server  
  
1.  Erstellen Sie auf dem RSA-Server den Ordner "c:\rsa-Installation".  
  
2.  Kopieren Sie den Inhalt des RSA Authentication Manager 7,1 SP4-Mediums in den Installationsordner "c:\rsa".  
  
3.  Erstellen Sie den Unterordner c:\rsa installation\license und Token.  
  
4.  Kopieren Sie die RSA-Lizenzdateien nach c:\rsa installation\license und Token.  
  
## <a name="JoinDomain"></a>Fügen Sie den RSA-Server der Corp-Domäne hinzu.  
  
1.  Klicken Sie mit der rechten Maustaste auf **Arbeitsplatz**und dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf der Registerkarte **Computername** auf **Ändern**.  
  
3.  Geben Sie unter **Computer Name den Namen** **RSA**ein. Klicken Sie unter **Mitglied von**auf **Domäne**, geben Sie **Corp.contoso.com**ein, und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie **User1** und sein Kennwort ein, und klicken Sie auf **OK**.  
  
5.  Klicken Sie im Dialogfeld Domäne Willkommen auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Nachdem der Computer neu gestartet wurde, geben Sie **User1** und das Kennwort ein, wählen Sie Corp in der Dropdown Liste **Anmelden an:** aus, und klicken Sie auf **OK**.  
  
## <a name="BKMK_Firewall"></a>Deaktivieren der Windows-Firewall auf RSA  
  
1.  Klicken Sie auf **Start**, klicken Sie auf System **Steuerung**, klicken Sie auf **System und Sicherheit**und dann auf **Windows-Firewall**.  
  
2.  Klicken Sie **auf Windows-Firewall aktivieren oder deaktivieren**.  
  
3.  **Deaktivieren** Sie die Windows-Firewall für alle Einstellungen.  
  
4.  Klicken Sie auf **OK** , und schließen Sie Windows-Firewall.  
  
## <a name="install"></a>Installieren Sie den RSA Authentication Manager auf dem RSA-Server.  
  
1.  Wenn die Sicherheits Warnmeldung während des Vorgangs zu einem beliebigen Zeitpunkt angezeigt wird, klicken Sie auf **Ausführen** , um fortzufahren.  
  
2.  Öffnen Sie den Installationsordner c:\rsa, und doppelklicken Sie auf **Autorun. exe**.  
  
3.  Klicken Sie auf **jetzt installieren**, klicken Sie auf **weiter**, wählen Sie die Top-Option für die Americas aus, und klicken Sie auf **weiter**  
  
4.  Wählen Sie **Ich akzeptiere die Bedingungen des Lizenzvertrags aus**, und klicken Sie auf **weiter**.  
  
5.  Wählen Sie **primäre Instanz**aus, und klicken Sie auf **weiter**.  
  
6.  Geben Sie im Feld **Verzeichnis Name:** **c:\rsa**ein, und klicken Sie auf **weiter**.  
  
7.  Überprüfen Sie, ob der Servername (RSA.Corp.contoso.com) und die IP-Adresse richtig sind, und klicken Sie auf **weiter**.  
  
8.  Navigieren Sie zu c:\rsa installation\license und Token, und klicken Sie auf **weiter**.  
  
9. Klicken Sie auf der Seite **Lizenzdatei überprüfen** auf **weiter**.  
  
10. Geben Sie in das Feld **Benutzer-ID** **ein, und**geben Sie in die Felder **Kennwort** und **Kennwort bestätigen** ein sicheres Kennwort ein. Klicken Sie auf **Weiter**.  
  
11. Übernehmen Sie auf dem Bildschirm Protokoll Auswahl die Standardeinstellungen, und klicken Sie auf **weiter**.  
  
12. Klicken Sie auf dem Bildschirm Zusammenfassung auf **Installieren**.  
  
13. Klicken Sie nach Abschluss der Installation auf **Fertig**stellen.  
  
## <a name="confiauthmgr"></a>Konfigurieren des RSA-Authentifizierungs-Managers  
  
1.  Wenn die RSA-Sicherheits Konsole nicht automatisch geöffnet wird, doppelklicken Sie auf dem RSA-Computer Desktop auf "RSA Security Console".  
  
2.  Wenn das Sicherheitszertifikat Warnung/Sicherheitswarnung angezeigt wird, klicken Sie **auf diese Website fortsetzen** , oder klicken Sie auf **Ja** , um den Vorgang fortzusetzen, und fügen Sie diese Website den vertrauenswürdigen Sites hinzu.  
  
3.  Geben Sie **Administrator** im Feld **Benutzer-ID** ein, und klicken Sie auf **OK**.  
  
4.  Geben Sie im Feld **Kennwort** das Kennwort für das Administrator Konto ein, und klicken Sie auf **Anmelden**.  
  
5.  Fügt Tokeninformationen ein.  
  
    1.  Klicken Sie in der **RSA-Sicherheits Konsole** auf **Authentifizierung** , und klicken Sie auf **SecurID Tokens**.  
  
    2.  Klicken Sie auf **Token importieren Auftrag**, und klicken Sie dann auf **neue hinzufügen**.  
  
    3.  Klicken Sie im Abschnitt **Import Optionen** auf **Durchsuchen**. Navigieren Sie zu der XML-Token-Datei in C:\. Ordner RSA installation\license und Token, und klicken Sie auf **Öffnen**.  
  
    4.  Klicken Sie unten auf der Seite auf **Auftrag übermitteln** .  
  
6.  Erstellen Sie einen neuen OTP-Benutzer.  
  
    1.  Klicken Sie in der **RSA-Sicherheits Konsole** auf die Registerkarte **Identität** , klicken Sie auf **Benutzer**und dann auf **neue hinzufügen**.  
  
    2.  Im **Nachnamen:** Abschnitt **User**und im Abschnitt **User ID:** Section Type **User1** (UserID muss mit dem für dieses Lab verwendeten AD-Benutzernamen identisch sein).  Geben Sie in den Abschnitten **Kennwort:** und **Kennwort bestätigen:** ein sicheres Kennwort ein. Deaktivieren Sie das Kontrollkästchen **"Benutzer muss Kennwort bei der nächsten Anmeldung ändern",** und klicken Sie auf **Speichern**.  
  
7.  Weisen Sie user1 einem der importierten Token zu.  
  
    1.  Klicken Sie auf der Seite **Benutzer** auf **User1** , und klicken Sie auf **SecurID Tokens**.  
  
    2.  Klicken Sie auf **SecurID Tokens** , und klicken Sie auf **Token zuweisen**.  
  
    3.  Klicken Sie unter der Überschrift **Seriennummer** auf die erste aufgeführte Zahl, und klicken Sie auf **zuweisen**.  
  
    4.  Klicken Sie auf das zugewiesene Token, und klicken Sie auf **Bearbeiten**. Wählen Sie im Abschnitt **SecurID-PIN-Verwaltung** für **Benutzer Authentifizierungsanforderung**die Option **PIN nicht erforderlich (nur Tokencode)** aus.  
  
    5.  Klicken Sie auf **Token Speichern und verteilen**.  
  
    6.  Klicken Sie im Abschnitt **Grundlagen** auf der Seite **Software Token verteilen** auf **Issue Token File (sdtid)** .  
  
    7.  Deaktivieren Sie auf der Seite **Software Token verteilen** im Abschnitt **tokendateioptionen** das Kontrollkästchen **Kopierschutz aktivieren** . Klicken Sie auf **kein Kennwort** und **weiter**.  
  
    8.  Klicken Sie im Abschnitt **Downloaddatei** auf der Seite **Software Token verteilen** auf **jetzt herunterladen**. Klicken Sie auf **Speichern**. Navigieren Sie zu c:\rsa-Installation, und klicken Sie auf **Speichern** und **Schließen**.  
  
    9. Minimieren Sie die **RSA-Sicherheits Konsole** für die spätere Verwendung.  
  
8.  Konfigurieren Sie den Authentifizierungs-Manager als RADIUS-Server.  
  
    1.  Doppelklicken Sie auf dem RSA-Computer Desktop auf **"RSA-Sicherheits Betriebs Konsole"** .  
  
    2.  Wenn das Sicherheitszertifikat Warnung/Sicherheitswarnung angezeigt wird, klicken Sie **auf diese Website fortsetzen** , oder klicken Sie auf **Ja** , um den Vorgang fortzusetzen, und fügen Sie diese Website den vertrauenswürdigen Sites hinzu  
  
    3.  Geben Sie Benutzer-ID und Kennwort ein, und klicken Sie **auf Anmelden**.  
  
    4.  Klicken Sie auf **Bereitstellungs Konfiguration-RADIUS-Server konfigurieren**.  
  
    5.  Geben Sie auf der Seite **zusätzliche Anmelde Informationen erforderlich** die Benutzer-ID und das Kennwort des Administrators ein, **und klicken Sie**  
  
    6.  Geben Sie auf der Seite **RADIUS-Server konfigurieren** dasselbe Kennwort ein, das für den Administrator Benutzer für die **geheimen** Schlüssel und das **Master Kennwort**verwendet wurde Geben Sie die Administrator Benutzer-ID und das Kennwort ein, und klicken Sie auf **Konfigurieren**  
  
    7.  Vergewissern Sie sich, dass die Meldung **"der RADIUS-Server wurde erfolgreich konfiguriert"** angezeigt wird. Klicken Sie auf **Fertig**. Schließen Sie die **RSA-Betriebs Konsole**.  
  
    8.  Wechseln Sie zurück zur **"RSA-Sicherheits Konsole"** .  
  
    9. Klicken Sie auf der Registerkarte **RADIUS** auf **RADIUS-Server**. Vergewissern Sie sich, dass RSA.Corp.contoso.com aufgeführt ist.  
  
9. Konfigurieren Sie den RSA-Server als RSA-Authentifizierungs Client.  
  
    1.  Klicken Sie auf der Registerkarte **RADIUS** auf **RADIUS-Clients** , und **fügen Sie neue hinzu**.  
  
    2.  Aktivieren Sie das Kontrollkästchen **beliebiger RADIUS-Client** .  
  
    3.  Geben Sie im Feld **gemeinsamer geheimer** Schlüssel ein sicheres Kennwort Ihrer Wahl ein. Dieses Kennwort wird später beim Konfigurieren von Edge1 für OTP verwendet.  
  
    4.  Lassen Sie das Feld **IP-Adresse** leer, und **Erstellen** Sie den Eintrag als **Standard-RADIUS**.  
  
    5.  Klicken Sie auf **ohne RSA-Agent speichern**.  
  
10. Erstellen Sie Dateien, die zum Konfigurieren von Edge1 als RSA-Authentifizierungs-Agent erforderlich sind.  
  
    1.  Markieren Sie auf der Registerkarte **Zugriff** die **Authentifizierungs-Agents**, und klicken Sie auf **neue hinzufügen**.  
  
    2.  Geben Sie **Edge1** in das Feld **Hostname** ein, und klicken Sie auf **IP auflösen**.  
  
    3.  Beachten Sie, dass die IP-Adresse für Edge1 jetzt im Feld **IP-Adresse** angezeigt wird. Klicken Sie auf **Speichern**.  
  
11. Generieren Sie eine Konfigurationsdatei für den Edge1-Server (AM_Config. zip).  
  
    1.  Markieren Sie auf der Registerkarte **Zugriff** die **Authentifizierungs-Agents**, und klicken Sie auf **Konfigurationsdatei generieren**.  
  
    2.  Klicken Sie auf der Seite **Konfigurationsdatei generieren** auf **Konfigurationsdatei generieren**, und klicken Sie dann auf **jetzt herunterladen**.  
  
    3.  Klicken Sie auf **Speichern**, navigieren Sie zu C:\. RSA-Installation, und klicken Sie auf **Speichern**.  
  
    4.  Klicken Sie im Dialogfeld **Download abgeschlossen** auf **Schließen** .  
  
12. Generieren Sie eine geheime Knoten Datei für den Edge1-Server (EDGE1_NodeSecret. zip).  
  
    1.  Markieren Sie auf der Registerkarte **Zugriff** die **Authentifizierungs-Agents**, und klicken Sie auf **vorhandene verwalten**.  
  
    2.  Klicken Sie auf den aktuell konfigurierten Knoten Edge1, und klicken Sie auf **Knoten Geheimnis verwalten**.  
  
    3.  Aktivieren Sie das Kontrollkästchen **neuen zufälligen Knoten erstellen, und exportieren Sie das Knoten Geheimnis in eine Datei** .  
  
    4.  Geben Sie das Kennwort ein, das für den Administrator Benutzer in den Feldern **Verschlüsselungs Kennwort** und **Verschlüsselungs Kennwort bestätigen** verwendet wird, und klicken Sie auf **Speichern**.  
  
    5.  Klicken Sie auf der Seite für die Datei mit dem **geheimen Knoten Schlüssel** auf **Download Now**  
  
    6.  Klicken Sie im Dialogfeld **Datei Download** auf **Speichern**, navigieren Sie zu c:\rsa-Installation, und klicken Sie auf **Speichern**. Klicken Sie im Dialogfeld **Download abgeschlossen** auf **Schließen** .  
  
    7.  Über den RSA Authentication Manager Media Copy \auth_mgr\windows-x86_64\am\rsa-ace_nsload\win32-5.0-x86\agent_nsload.exe to c:\rsa Installation.  
  
## <a name="BKMK_DAProbeUser"></a>Erstellen von daprobeuser  
  
1.  Klicken Sie in der **RSA-Sicherheits Konsole** auf die Registerkarte **Identität** , klicken Sie auf **Benutzer**und dann auf **neue hinzufügen**.  
  
2.  Geben Sie im Abschnitt **Nachname die Bezeichnung** Type **Probe**ein, und geben Sie im Abschnitt **User ID:** den Typ **daprobeuser**ein. Geben Sie in den Abschnitten **Kennwort:** und **Kennwort bestätigen:** ein sicheres Kennwort ein. Deaktivieren Sie das Kontrollkästchen **"Benutzer muss Kennwort bei der nächsten Anmeldung ändern",** und klicken Sie auf **Speichern**.  
  
## <a name="InstToken"></a>Installieren des RSA SecurID-Software Tokens auf CLIENT1  
Verwenden Sie dieses Verfahren, um das SecurID-Software Token auf CLIENT1 zu installieren.  
  
#### <a name="install-securid-software-token"></a>SecurID-Software Token installieren  
  
1.  Erstellen Sie auf dem Computer Client1 den Ordner c:\rsa-Dateien. Kopieren Sie die Datei Software_Tokens. zip aus der c:\rsa-Installation auf dem RSA-Computer in c:\rsa-Dateien. Extrahieren Sie die Datei User1_000031701832. sdtid in c:\rsa-Dateien auf CLIENT1.  
  
2.  Greifen Sie auf die RSA SecurID-Software Token-Medienquelle zu, und doppelklicken Sie im Ordner **SecurID Softwaretoken Client App** auf RSASECURIDTOKEN410, um die RSA SecurID-Installation zu starten. Wenn die Meldung **Datei öffnen-Sicherheitswarnung** angezeigt wird, klicken Sie auf **Ausführen**.  
  
3.  Klicken Sie im Dialogfeld **RSA SecurID Software Token-InstallShield Wizard** zweimal auf **weiter** .  
  
4.  Akzeptieren Sie den Lizenzvertrag, und klicken Sie auf **weiter**.  
  
5.  Wählen Sie im Dialogfeld **Installationstyp** die Option **typisch**aus, klicken Sie auf **weiter und dann**auf **Installieren**.  
  
6.  Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
7.  Aktivieren Sie das Kontrollkästchen **RSA SecurID-Software Token starten** , und klicken Sie auf **Fertig**stellen.  
  
8.  Klicken Sie auf **aus Datei importieren**.  
  
9. Klicken Sie auf **Durchsuchen**, wählen Sie c:\rsa Files\User1_000031701832.SDTID, und klicken Sie auf **Öffnen**.  
  
10. Klicken Sie zweimal auf **OK** .  
  
## <a name="configAuthAgt"></a>Konfigurieren von Edge1 als RSA-Authentifizierungs-Agent  
Verwenden Sie dieses Verfahren, um Edge1 zum Ausführen der RSA-Authentifizierung zu konfigurieren.  
  
#### <a name="configure-the-rsa-authentication-agent"></a>Konfigurieren des RSA-Authentifizierungs-Agents  
  
1. Öffnen Sie auf Edge1 Windows-Explorer, und erstellen Sie den Ordner c:\rsa-Dateien. Navigieren Sie zu den RSA ACE-Installationsmedien.  
  
2. Kopieren Sie die Dateien agent_nsload. exe, AM_Config. zip und EDGE1_NodeSecret. zip aus dem RSA-Medium in c:\rsa-Dateien.  
  
3. Extrahieren Sie den Inhalt der beiden ZIP-Dateien an die folgenden Speicherorte:  
  
   1.  C:\Windows\System32  
  
   2.  C:\windows\syswow64\  
  
4. Kopieren Sie agent_nsload. exe nach c:\windows\SysWOW64 @ no__t-0.  
  
5. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und navigieren Sie zu c:\windows\SysWOW64.  
  
6. Geben Sie **agent_nsload. exe-f nodesecret. rec-p <password>** ein, wobei <password> das starke Kennwort ist, das Sie bei der ersten RSA-Konfiguration erstellt haben. Drücken Sie die EINGABETASTE.  
  
7. Kopieren Sie c:\windows\syswow64\securid nach c:\Windows\System32.  
  
## <a name="configOTP"></a>Konfigurieren von Edge1 für die Unterstützung der OTP-Authentifizierung  
Verwenden Sie dieses Verfahren, um OTP für DirectAccess zu konfigurieren und die Konfiguration zu überprüfen.  
  
#### <a name="configure-otp-for-directaccess"></a>Konfigurieren von OTP für DirectAccess  
  
1.  Öffnen Sie auf Edge1 Server-Manager, und klicken Sie im linken Bereich auf **Remote Zugriff** .  
  
2.  Klicken Sie im Bereich Server mit der rechten Maustaste auf **Edge1** , und wählen Sie **Remote Zugriffs Verwaltung**aus.  
  
3.  Klicken Sie auf **Konfiguration**.  
  
4.  Klicken Sie im Fenster **DirectAccess-Setup** unter **Schritt 2-RAS-Server**auf **Bearbeiten**.  
  
5.  Klicken Sie dreimal auf **weiter** , und wählen Sie im Abschnitt **Authentifizierung** die Option **zweistufige Authentifizierung** aus, und vergewissern **Sie sich,** dass die Option **Computer Zertifikate verwenden** aktiviert ist. Vergewissern Sie sich, dass die Stamm Zertifizierungsstelle auf **CN = Corp-App1-ca**festgelegt ist. Klicken Sie auf **Weiter**.  
  
6.  Doppelklicken Sie im Abschnitt " **OTP RADIUS-Server** " auf das Feld "leerer **Server Name** ".  
  
7.  Geben Sie im Dialogfeld **RADIUS-Server hinzufügen** **RSA** in das Feld **Server Name** ein. Klicken Sie neben dem Feld **gemeinsamer geheimer** Schlüssel auf **ändern** , und geben Sie das Kennwort ein, das Sie beim Konfigurieren der RADIUS-Clients auf dem RSA-Server in den Feldern **neuer geheimer** Schlüssel und **neues Geheimnis bestätigen** verwendet haben. Klicken Sie zweimal auf **OK** , und klicken Sie auf **weiter**.  
  
    > [!NOTE]  
    > Wenn sich der RADIUS-Server in einer anderen Domäne als der RAS-Server befindet, muss im Feld **Server Name** der voll qualifizierte Domänen Name des RADIUS-Servers angegeben werden.  
  
8.  Wählen Sie im Abschnitt **OTP** -Zertifizierungsstellen Server App1.Corp.contoso.com aus, und klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  
  
9. Klicken Sie auf der Seite **OTP-Zertifikat Vorlagen** auf **Durchsuchen** , um eine Zertifikat Vorlage auszuwählen, die für die Registrierung von Zertifikaten verwendet wird, die für die OTP-Authentifizierung ausgestellt wurden, und wählen Sie im Dialogfeld **Zertifikat Vorlagen** die Option **daotplogon.** . Klicken Sie auf **OK**. Klicken Sie auf **Durchsuchen** , um eine Zertifikat Vorlage auszuwählen, die zum Registrieren des vom RAS-Server verwendeten Zertifikats zum Signieren von OTP-Zertifikat Registrierungsanforderungen verwendet wird, und wählen Sie im Dialogfeld **Zertifikat Vorlagen** die Option **daotpra**aus. Klicken Sie auf **OK**. Klicken Sie auf **Weiter**.  
  
10. Klicken Sie auf der Seite **Setup des Remote Zugriffs Servers** auf **Fertig**stellen, und klicken Sie dann auf **Fertig** stellen im **Assistenten für DirectAccess-Experten**  
  
11. Klicken Sie im Dialogfeld **Remote Zugriffs Überprüfung** auf über **nehmen, warten Sie,** bis die DirectAccess-Richtlinie aktualisiert wurde, und klicken Sie dann auf **Schließen**.  
  
12. Geben Sie im **Start** Bildschirm**PowerShell. exe**ein, klicken Sie mit der rechten Maustaste auf **PowerShell**, klicken Sie auf **erweitert**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
13. Geben Sie im Windows PowerShell-Fenster **gpupdate/force** ein, und drücken Sie die EINGABETASTE.  
  
14. Schließen Sie die Remote Zugriffs-Verwaltungskonsole, und öffnen Sie Sie erneut. Vergewissern Sie sich, dass alle OTP-Einstellungen  
  


