---
title: Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy-Schritt 2 AD FS Arbeitsaufgaben nach der Konfiguration
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 06/06/2019
ms.assetid: 0a48852e-48cc-4047-ae58-99f11c273942
ms.openlocfilehash: 84ff335514b4b9251ffa1518b613120f3b3e2869
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946193"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-2-ad-fs-post-configuration-work"></a>Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy: Schritt 2 AD FS arbeiten nach der Konfiguration

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird der zweite Schritt beim Bereitstellen von Arbeits Ordnern mit Active Directory-Verbunddienste (AD FS) (AD FS) und dem webanwendungsproxy beschrieben. Die anderen Schritte in diesem Prozess finden Sie in den folgenden Themen:

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 1, einrichten AD FS](deploy-work-folders-adfs-step1.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern](deploy-work-folders-adfs-step3.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 4](deploy-work-folders-adfs-step4.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients](deploy-work-folders-adfs-step5.md)

> [!NOTE]
> Die in diesem Abschnitt behandelten Anweisungen gelten für eine Windows Server 2019-oder Windows Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, befolgen Sie die [Anweisungen unter Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn747208(v=ws.11)).

In Schritt 1 haben Sie AD FS installiert und konfiguriert. Nun müssen Sie die folgenden Schritte zur nach Konfiguration für AD FS ausführen.

## <a name="configure-dns-entries"></a>Konfigurieren von DNS-Einträgen

Sie müssen für AD FS zwei DNS-Einträge erstellen. Dabei handelt es sich um die gleichen zwei Einträge, die in den Schritten vor der Installation verwendet wurden, als Sie das San-Zertifikat (Subject Alternative Name) erstellt haben.

Die DNS-Einträge lauten in der folgenden Form:

-   AD FS Dienst Name. Domäne

-   enterpriseregistration. Domäne

-   AD FS Servername. Domain (DNS-Eintrag sollte bereits vorhanden sein. z. b. 2016-ADFS.contoso.com)

Im Testbeispiel lauten die Werte wie folgt:

-   **blueadfs.contoso.com**

-   **enterpriseregistration.contoso.com**

## <a name="create-the-a-and-cname-records-for-ad-fs"></a>Erstellen Sie die A-und CNAME-Einträge für AD FS

Führen Sie die folgenden Schritte aus, um einen-und CNAME-Eintrag für AD FS zu erstellen:

1.  Öffnen Sie auf dem Domänen Controller den DNS-Manager.

2.  Erweitern Sie den Ordner Forward-Lookupzonen, klicken Sie mit der rechten Maustaste auf Ihre Domäne, und wählen Sie **neuer Host (A)** aus.

3.  Das **neue Host** Fenster wird geöffnet. Geben Sie im Feld **Name** den Alias für den AD FS Dienstnamen ein. Im Testbeispiel ist dies **blueadfs**.

    Der Alias muss mit dem Betreff im Zertifikat identisch sein, das für die AD FS verwendet wurde. Wenn der Betreff z. b. "ADFS.contoso.com" lautet, wäre der hier eingegebene Alias " **ADFS**".

    > [!IMPORTANT]
    > Wenn Sie AD FS mithilfe der Windows Server-Benutzeroberfläche (UI) anstelle von Windows PowerShell einrichten, müssen Sie einen A-Datensatz anstelle eines CNAME-Einsatzes für AD FS erstellen. Der Grund hierfür ist, dass der Dienst Prinzipal Name (Service Principal Name, SPN), der über die Benutzeroberfläche erstellt wird, nur den Alias enthält, der zum Einrichten des AD FS Diensts als Host verwendet wird.

4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den AD FS Server ein. Im Beispiel Test ist dies **192.168.0.160**. Klicken Sie auf **Host hinzufügen**.

5.  Klicken Sie im Ordner Forward-Lookupzonen mit der rechten Maustaste erneut auf die Domäne, und wählen Sie **Neuer Alias (CNAME)** aus.

6.  Fügen Sie im Fenster **neues Ressourcen Daten Satz** den Aliasnamen **enterpriseregistration** hinzu, und geben Sie den voll qualifizierten Domänen Namen für den AD FS Server ein. Dieser Alias wird für den Geräte Beitritt verwendet und muss als **enterpriseregistration**bezeichnet werden.

7.  Klicken Sie auf **OK**.

Wenn Sie die entsprechenden Schritte über Windows PowerShell ausführen möchten, verwenden Sie den folgenden Befehl. Der Befehl muss auf dem Domänen Controller ausgeführt werden.

```Powershell
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name blueadfs -A -IPv4Address 192.168.0.160
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name enterpriseregistration -CName  -HostNameAlias 2016-ADFS.contoso.com
```

## <a name="set-up-the-ad-fs-relying-party-trust-for-work-folders"></a>Einrichten der AD FS Vertrauensstellung der vertrauenden Seite für Arbeitsordner

Sie können die Vertrauensstellung der vertrauenden Seite für Arbeitsordner einrichten und konfigurieren, auch wenn noch keine Arbeitsordner eingerichtet wurden. Die Vertrauensstellung der vertrauenden Seite muss so eingerichtet werden, dass Arbeitsordner AD FS verwenden können. Da Sie gerade AD FS einrichten, ist jetzt ein guter Zeitpunkt, diesen Schritt durchzuführen.

So richten Sie die Vertrauensstellung der vertrauenden Seite ein:

1.  Öffnen Sie **Server-Manager**klicken Sie **im Menü Extras** auf **AD FS Verwaltung**.

2.  Klicken Sie im rechten Bereich unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.

3.  Wählen Sie auf der Seite **Willkommen** die Option **Ansprüche beachten** aus, und klicken Sie auf **starten**.

4.  Wählen Sie auf der Seite **Datenquelle auswählen** die Option **Daten über die**vertrauende Seite manuell eingeben aus, und klicken Sie dann auf **weiter**.

5.  Geben Sie im Feld **Anzeige Name den Namen** **Arbeitsordner**ein, und klicken Sie dann auf **weiter**.

6.  Klicken Sie auf der Seite **Zertifikat konfigurieren** auf **weiter**. Die tokenverschlüsselungszertifikate sind optional und werden für die Testkonfiguration nicht benötigt.

7.  Klicken Sie auf der Seite **URL konfigurieren** auf **weiter**.

8. Fügen Sie auf der Seite Bezeichner **Konfigurieren** den folgenden Bezeichner hinzu: `https://windows-server-work-folders/V1` . Dieser Bezeichner ist ein hart codierter Wert, der von Arbeits Ordnern verwendet wird und der vom Arbeitsordner Dienst gesendet wird, wenn er mit AD FS kommuniziert. Klicken Sie auf **Weiter**.

9. Wählen Sie auf der Seite Richtlinie für Access Control auswählen die Option **Alle zulassen**aus, und klicken Sie dann auf **weiter**.

10. Klicken Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter**.

11. Nachdem die Konfiguration abgeschlossen ist, zeigt die letzte Seite des Assistenten an, dass die Konfiguration erfolgreich war. Aktivieren Sie das Kontrollkästchen zum Bearbeiten der Anspruchs Regeln, und klicken Sie auf **Schließen**.

12. Wählen Sie im Snap-in "AD FS" die **Arbeitsordner** -Vertrauensstellung der vertrauenden Seite aus, und klicken Sie unter "Aktionen" auf " **Richtlinie**

13. Das Fenster **Anspruchs Ausstellungs Richtlinie für Arbeitsordner bearbeiten** wird geöffnet. Klicken Sie auf **Regel hinzufügen**.

14. Wählen Sie in der Dropdown Liste **Anspruchs Regel Vorlage** die Option **LDAP-Attribute als Ansprüche senden**aus, und klicken Sie auf **weiter**.

15. Geben Sie auf der Seite **Anspruchs Regel konfigurieren** im Feld **Anspruchs Regel Name** den Namen **Arbeitsordner**ein.

16. Wählen Sie in der Dropdown Liste **Attribut Speicher** die Option **Active Directory**aus.

17. Geben Sie in der Tabelle Mapping die folgenden Werte ein:

    -   Benutzer Prinzipal Name: UPN

    -   Anzeige Name: Name

    -   Nachname: Nachname

    -   Vorname: Vorname: Vorname

18. Klicken Sie auf **Fertig stellen**. Die Regel "Arbeitsordner" wird auf der Registerkarte Ausstellungs Transformationsregeln aufgelistet, und klicken Sie auf **OK**.

### <a name="set-relying-part-trust-options"></a>Vertrauens Optionen für vertrauenswürdige Teile festlegen

Nachdem die Vertrauensstellung der vertrauenden Seite für AD FS eingerichtet wurde, müssen Sie die Konfiguration abschließen, indem Sie fünf Befehle in Windows PowerShell ausführen. Mit diesen Befehlen werden Optionen festgelegt, die für die erfolgreiche Kommunikation von Arbeits Ordnern mit AD FS erforderlich sind und nicht über die Benutzeroberfläche festgelegt werden können. Die Optionen sind:

-   Aktivieren der Verwendung von JSON-webtoken (jwts)

-   Verschlüsselte Ansprüche deaktivieren

-   Automatische \- Aktualisierung aktivieren

-   Legen Sie die Ausgabe von OAuth-Aktualisierungs Token auf alle Geräte fest.

-   Gewähren des Zugriffs auf die Vertrauensstellung der vertrauenden Seite

Verwenden Sie die folgenden Befehle, um diese Optionen festzulegen:

```powershell
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -EnableJWT $true
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -Encryptclaims $false
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -AutoupdateEnabled $true
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -IssueOAuthRefreshTokensTo AllDevices
Grant-AdfsApplicationPermission -ServerRoleIdentifier "https://windows-server-work-folders/V1" -AllowAllRegisteredClients -ScopeNames openid,profile
```

## <a name="enable-workplace-join"></a>Aktivieren von Workplace Join

Das Aktivieren von Workplace Join ist optional, kann jedoch nützlich sein, wenn Sie möchten, dass Benutzer Ihre persönlichen Geräte für den Zugriff auf Arbeitsplatz Ressourcen verwenden können.

Zum Aktivieren der Geräteregistrierung für Workplace Join müssen Sie die folgenden Windows PowerShell-Befehle ausführen, mit denen die Geräteregistrierung konfiguriert und die globale Authentifizierungs Richtlinie festgelegt wird:

```powershell
Initialize-ADDeviceRegistration -ServiceAccountName <your AD FS service account>
    Example: Initialize-ADDeviceRegistration -ServiceAccountName contoso\adfsservice$
Set-ADFSGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true
```

## <a name="export-the-ad-fs-certificate"></a>Exportieren des AD FS Zertifikats

Exportieren Sie als nächstes das selbst \- signierte AD FS Zertifikat, damit es auf den folgenden Computern in der Testumgebung installiert werden kann:

-   Der Server, der für Arbeitsordner verwendet wird.

-   Der Server, der für den webanwendungsproxy verwendet wird

-   Der in die Domäne eingebundener Windows-Client

-   Der nicht in die Domäne eingebundenen Windows-Client

Führen Sie die folgenden Schritte aus, um das Zertifikat zu exportieren:

1.  Klicken Sie im **Startmenü**auf **Ausführen**.

2.  Geben Sie **MMC**ein.

3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.

4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**. Der Zertifikat-Snap-in-Assistent wird gestartet.

5.  Wählen Sie **Computerkonto** aus, und klicken Sie dann auf **Weiter**.

6.  Wählen Sie **lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird) aus**, und klicken Sie dann auf **Fertig**stellen.

7.  Klicken Sie auf **OK**.

8.  Erweitern Sie die Ordner **Konsole root\zertifikate \( lokaler Computer) \personal\zertifikate**.

9.  Klicken Sie mit der rechten Maustaste auf das **AD FS Zertifikat**, klicken Sie auf **Alle Tasks**, und klicken Sie dann auf **exportieren.**

10. Der Zertifikatexport-Assistent wird geöffnet. Wählen Sie **Ja, privaten Schlüssel exportieren**aus.

11. Belassen Sie auf der Seite Format der zu **exportierenden Datei** die Standardoptionen ausgewählt, und klicken Sie auf **weiter**.

12. Erstellen Sie ein Kennwort für das Zertifikat. Dies ist das Kennwort, das Sie später verwenden, wenn Sie das Zertifikat auf andere Geräte importieren. Klicken Sie auf **Weiter**.

13. Geben Sie einen Speicherort und Namen für das Zertifikat ein, und klicken Sie dann auf **Fertig**stellen.

Die Installation des Zertifikats wird später im Bereitstellungs Verfahren behandelt.

## <a name="manage-the-private-key-setting"></a>Verwalten der Einstellung für den privaten Schlüssel

Sie müssen dem AD FS-Dienst Konto die Berechtigung zum Zugriff auf den privaten Schlüssel des neuen Zertifikats erteilen. Sie müssen diese Berechtigung erneut erteilen, wenn Sie das Kommunikations Zertifikat ersetzen, nachdem es abläuft. Führen Sie die folgenden Schritte aus, um Berechtigungen zu erteilen:

1.  Klicken Sie im **Startmenü**auf **Ausführen**.

2.  Geben Sie **MMC**ein.

3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.

4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**. Der Zertifikat-Snap-in-Assistent wird gestartet.

5.  Wählen Sie **Computerkonto** aus, und klicken Sie dann auf **Weiter**.

6.  Wählen Sie **lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird) aus**, und klicken Sie dann auf **Fertig**stellen.

7.  Klicken Sie auf **OK**.

8.  Erweitern Sie die Ordner **Konsole root\zertifikate \( lokaler Computer) \personal\zertifikate**.

9.  Klicken Sie mit der rechten Maustaste auf das **AD FS Zertifikat**, klicken Sie auf **Alle Tasks**und dann auf **private Schlüssel verwalten**.

10. Klicken Sie im Fenster **Berechtigungen** auf **Hinzufügen**.

11. Wählen Sie im Fenster **Objekttypen** die Option **Dienst Konten**aus, und klicken Sie dann auf **OK**.

12. Geben Sie den Namen des Kontos ein, das AD FS ausgeführt wird. Im Testbeispiel lautet dies adtsservice. Klicken Sie auf **OK**.

13. Legen Sie im Fenster **Berechtigungen** dem Konto mindestens Leseberechtigungen zu, und klicken Sie auf **OK**.

Wenn Sie nicht über die Option zum Verwalten von privaten Schlüsseln verfügen, müssen Sie möglicherweise den folgenden Befehl ausführen:`certutil -repairstore my *`

## <a name="verify-that-ad-fs-is-operational"></a>Überprüfen, ob AD FS betriebsbereit ist

Öffnen Sie ein Browserfenster, und wechseln Sie zu, um zu überprüfen, ob AD FS funktionstüchtig ist, und `https://blueadfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` Ändern Sie die URL entsprechend Ihrer Umgebung.

Im Browserfenster werden die Verbund Server Metadaten ohne Formatierung angezeigt. Wenn die Daten ohne SSL-Fehler oder-Warnungen angezeigt werden, ist der Verbund Serverbetriebs bereit.

Nächster Schritt: [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern](deploy-work-folders-adfs-step3.md)

## <a name="see-also"></a>Weitere Informationen
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)
