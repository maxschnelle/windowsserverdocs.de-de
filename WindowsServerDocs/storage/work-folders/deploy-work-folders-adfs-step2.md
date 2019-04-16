---
title: Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy - Schritt2, Konfigurationsaufgaben nach dem Einrichten von AD FS
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: 0a48852e-48cc-4047-ae58-99f11c273942
ms.openlocfilehash: 2a07f31e3040f63edfb8c73d454b6301aad46583
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-2-ad-fs-post-configuration-work"></a>Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt2, Konfigurationsaufgaben nach dem Einrichten von AD FS

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird der zweite Schritt bei der Bereitstellung von Arbeitsordnern mit Active Directory-Verbunddiensten (AD FS) und Webanwendungsproxy beschrieben. Weitere Schritte des Prozesses finden Sie in folgenden Themen:  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt1, Einrichten von ADFS](deploy-work-folders-adfs-step1.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt3, Einrichten von Arbeitsordnern](deploy-work-folders-adfs-step3.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt4, Einrichten des Webanwendungsproxy](deploy-work-folders-adfs-step4.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt5, Einrichten des Clients](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
>   Die in diesem Abschnitt enthaltenen Anweisungen gelten für eine Server2016-Umgebung. Wenn Sie Windows Server2012 R2 verwenden, folgen Sie den [Anweisungen für Windows Server2012 R2](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx).

In Schritt1 wurde AD FS installiert und konfiguriert. Jetzt müssen Sie folgende Schritte nach der Konfiguration für AD FS durchführen.  
  
## <a name="configure-dns-entries"></a>Konfigurieren von DNS-Einträgen  
Sie müssen zwei DNS-Einträge für AD FS erstellen. Hierbei handelt es sich um die gleichen zwei Einträge, die in den Schrittenvor der Installation bei der Erstellung des Zertifikats der alternativen Antragstellernamen (SAN) erstellt wurden.  
  
DNS-Einträge haben folgende Form:  
  
-   AD FS service name.domain  
  
-   enterpriseregistration.domain  
  
-   AD FS server name.domain   (DNS-Eintrag sollte bereits vorhanden sein. z.B. 2016-ADFS.contoso.com)
  
Im Testbeispiel sind diese Werte wie folgt:  
  
-   **blueadfs.contoso.com**  
  
-   **enterpriseregistration.contoso.com**  
  
## <a name="create-the-a-and-cname-records-for-ad-fs"></a>Erstellen Sie die A und CNAME-Einträge für AD FS  
Zum Erstellen von A und CNAME-Einträgen für AD FS, gehen Sie folgendermaßen vor:  
  
1.  Öffnen Sie auf dem Domänencontroller den DNS-Manager.  
  
2.  Erweitern Sie den Forward-Lookupzonen-Ordner, klicken Sie mit der rechten Maustaste auf die Domäne und wählen Sie **Neuer Host (A)** aus.  
  
3.  Das Fenster **Neuer Host** wird geöffnet. Geben Sie in das Dialogfeld **Name** den Alias für den AD FS-Dienstnamen ein. Im Testbeispiel ist dies **Blueadfs**.  
  
    Der Alias muss mit dem Betreff des Zertifikats identisch sein, das für AD FS verwendet wurde. Wenn der Betreff beispielsweise adfs.contoso.com wäre, müsste der hier eingegebene Alias **adfs** sein.  
  
    > [!IMPORTANT]  
    > Wenn Sie AD FS mithilfe der Windows Server-Benutzeroberfläche (UI) anstelle von Windows PowerShell einrichten, müssen Sie den Eintrag A anstelle des Eintrags CNAME für AD FS erstellen. Der Grund hierfür ist, dass der Dienstprinzipalname (SPN), der über die Benutzeroberfläche erstellt wird nur den Alias enthält, der zum Einrichten des AD FS-Diensts als Host verwendet wird.  
    >   
4.  Geben Sie unter **IP-Adresse** die IP-Adresse für den AD FS-Server ein. Im Testbeispiel ist dies **192.168.0.160**. Klicken Sie auf **Host hinzufügen**.  
  
5.  Klicken Sie im Forward-Lookupzonen-Ordner mit der rechten Maustaste erneut auf die Domäne und wählen Sie **Neuer Alias (CNAME)**.  
  
6.  Fügen Sie im Fenster **Neuer Ressourcendatensatz** den Aliasnamen **enterpriseregistration** ein und geben Sie den vollqualifizierten Domänennamen für den AD FS-Server. Dieser Alias dient zum Verknüpfen von Geräten und muss **enterpriseregistration** heißen.
  
7.  Klicken Sie auf **OK**.  
  
Verwenden Sie den folgenden Befehl, um die entsprechenden Schritte mit Windows PowerShell durchzuführen. Der Befehl muss auf dem Domänencontroller ausgeführt werden.  
  
```powershell  
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name blueadfs -A -IPv4Address 192.168.0.160   
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name enterpriseregistration -CName  -HostNameAlias 2016-ADFS.contoso.com   
```  
  
## <a name="set-up-the-ad-fs-relying-party-trust-for-work-folders"></a>Die AD FS-Vertrauensstellung der vertrauenden Seite für Arbeitsordner einrichten  
Sie können die Vertrauensstellung der vertrauenden Seite für Arbeitsordner einrichten und konfigurieren, auch wenn Arbeitsordner noch nicht eingerichtet wurden. Zur Verwendung von AD FS muss die Vertrauensstellung der vertrauenden Seite für Arbeitsordner eingerichtet sein. Da Sie die erforderlichen Schritte zum Einrichten von AD FS gerade durchführen, ist jetzt ein guter Zeitpunkt dafür.  
  
So richten Sie die Vertrauensstellung der vertrauenden Seite ein:  
  
1.  Öffnen Sie **Server-Manager** im Menü **Tools** und wählen Sie **AD FS Verwaltung** aus.  
  
2.  Klicken Sie im rechten Bereich unter **Aktionen** auf **Ansprüche nicht unterstützende Vertrauensstellung der vertrauenden Seite hinzufügen**.  
  
3.  Wählen Sie auf der **Willkommen**-Seite **Ansprüche unterstützen** und klicken Sie auf **Start**.  
  
4.  Wählen Sie auf der Seite **Datenquelle auswählen** **Daten über die vertrauende Seite manuell eingeben** und klicken Sie anschließend auf **Weiter**.  
  
5.  Geben Sie im Dialogfeld **Anzeigename** den **Arbeitsordner** ein und klicken Sie auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Zertifikat konfigurieren** auf **Weiter**. Die Tokenentschlüsselungszertifikate sind optional und nicht für die Testkonfiguration erforderlich.  
  
7.  Klicken Sie auf der Seite **URL konfigurieren** auf **Weiter**.  
  
8. Fügen Sie auf der Seite **Konfigurieren von Bezeichnern** die folgenden Bezeichner hinzu: **https://windows-server-work-folders/V1**. Dieser Bezeichner ist eine hartcodierter Wert, der von den Arbeitsordnern verwendet wird und wird durch den Arbeitsordnerdienst gesendet wird, wenn er mit AD FS kommuniziert. Klicken Sie auf **Weiter**.  
  
9. Wählen Sie auf der Seite „Zugriffssteuerungsrichtlinie” **Jeder** und klicken Sie dann auf **Weiter**.  
  
10. Klicken Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter**.  
  
11. Nachdem die Konfiguration abgeschlossen ist, wird auf der letzten Seite des Assistenten der erfolgreiche Abschluss der Konfiguration angezeigt. Aktivieren Sie das Kontrollkästchen für die Bearbeitung von Anspruchsregeln und klicken Sie auf **Schließen**.  
  
12. Wählen Sie in der AD FS-Snap-In die Vertrauensstellung der vertrauenden Seite für den **Arbeitsordner** aus und klicken Sie unter Aktionen auf **Anspruch auf Ausstellungsrichtlinie bearbeiten**.

13. Das Fenster **Anspruch auf Ausstellungsrichtlinie für WorkFolders bearbeiten** wird geöffnet. Klicken Sie auf **Regel hinzufügen...**.  
  
14. Wählen Sie aus der Dropdown-Liste **Anspruchsvorlage** **LDAP-Attribute als Ansprüche senden** und klicken Sie auf **Weiter**.  
  
15. Geben Sie auf der Seite **Konfigurieren einer Anspruchsregel** in das Dialogfeld **Name der Anspruchsregel** den **Arbeitsordner** ein.  
  
16. Wählen Sie aus der Dropdown-Liste **Attributspeicher** **Active Directory** aus.  
  
17. Geben Sie in der Zuordnungstabelle diese Werte ein:  
  
    -   Benutzerprinzipalname: UPN  
  
    -   Anzeigename: Name  
  
    -   Nachname: Nachname  
  
    -   Der angegebene Name: Vorname  
  
18. Klicken Sie auf **Fertig stellen**. In der Registerkarte für Ausstellungstransformationsregeln sehen Sie die Regel der Arbeitsordner. Klicken Sie auf **OK**.  
  
### <a name="set-relying-part-trust-options"></a>Optionen der Vertrauensstellung der vertrauenden Seite festlegen  
Nachdem die Vertrauensstellung der vertrauenden Seite für AD FS eingerichtet wurde, müssen Sie die Konfiguration abschließen, indem Sie fünf Befehle in Windows PowerShell ausführen. Diese Befehle legen Optionen fest, die für die erfolgreiche Kommunikation Arbeitsordner mit AD FS erforderlich sind und können nicht über die Benutzeroberfläche festgelegt werden. Die Optionen sind:  
  
-   Verwendung von JSON Web Token (JWT) aktivieren  
  
-   Verschlüsselte Ansprüche deaktivieren  
  
-   Automatisches Update aktivieren  
  
-   Ausgabe der OAuth-Aktualisierungstoken für alle Geräte festlegen  

-   Clients Zugriff auf die Vertrauensstellung der vertrauenden Seite gewähren

Um diese Optionen festzulegen, verwenden Sie folgende Befehle:  
  
```powershell  
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -EnableJWT $true   
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -Encryptclaims $false   
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -AutoupdateEnabled $true   
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -IssueOAuthRefreshTokensTo AllDevices
Grant-AdfsApplicationPermission -ServerRoleIdentifier "https://Windows-Server-Work-Folders/V1" -AllowAllRegisteredClients  
```  
  
## <a name="enable-workplace-join"></a>Aktivieren Sie Workplace Join  
Das Aktivieren von Workplace Join ist optional, es kann jedoch hilfreich sein, wenn Sie möchten, dass Benutzer mit ihren persönlichen Geräten auf Arbeitsplatzressourcen zugreifen können.  
  
Zum Aktivieren der Geräteregistrierung für Workplace Join führen Sie folgende Windows PowerShell-Befehle aus, die die Geräteregistrierung konfigurieren und die globalen Authentifizierungsrichtlinien festlegen:  
  
```powershell  
Initialize-ADDeviceRegistration -ServiceAccountName <your AD FS service account>
    Example: Initialize-ADDeviceRegistration -ServiceAccountName contoso\adfsservice$
Set-ADFSGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true   
```  
  
## <a name="export-the-ad-fs-certificate"></a>Exportieren Sie das AD FS-Zertifikat.  
Exportieren Sie anschließend das selbstsignierte AD FS-Zertifikat, damit es auf den folgenden Computern in der Testumgebung installiert werden kann:  
  
-   Der Server, der für Arbeitsordner verwendet wird  
  
-   Der Server, der für die Webanwendungsproxy verwendet wird  
  
-   Der mit einer Domäne verknüpfte Windows-Client  
  
-   Der nicht mit einer Domäne verknüpfte Windows-Client  
  
Gehen Sie folgendermaßen vor, um das Zertifikat zu exportieren:  
  
1.  Klicken Sie auf **Start**und dann auf **Ausführen**.  
  
2.  Geben Sie **MMC** ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Wählen Sie aus der Liste **Verfügbare Snap-Ins** **Zertifikate** aus und klicken Sie auf **Hinzufügen**. Der Zertifikate-Snap-In-Assistent wird gestartet.  
  
5.  Wählen Sie **Computerkonto** aus, und klicken Sie auf **Weiter**.  
  
6.  Wählen Sie **Lokaler Computer: (Computer, auf dem diese Konsole ausgeführt wird)** und klicken Sie auf **Finish**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Erweitern Sie den Ordner **Konsolenstamm\Zertifikate\(Lokaler Computer)\Persönlich\Zertifikate**.  
  
9.  Klicken Sie mit der rechten Maustaste auf das **AD FS-Zertifikat**, und klicken Sie dann auf **Alle Aufgaben** und **Exportieren...**.  
  
10. Der Zertifikatexport-Assistent wird geöffnet. Wählen Sie **Ja, privaten Schlüssel exportieren**aus.  
  
11. Lassen Sie auf der Seite **Format der zu exportierenden Datei** die Standardoptionen ausgewählt und klicken Sie auf **Weiter**.  
  
12. Erstellen Sie ein Kennwort für das Zertifikat. Dies ist das Kennwort, das Sie später verwenden, wenn Sie das Zertifikat auf anderen Geräten importieren. Klicken Sie auf **Weiter**.  
  
13. Geben Sie einen Speicherort und Namen für das Zertifikat ein und klicken Sie dann auf **Fertig**.  
  
Die Installation des Zertifikats wird später im Bereitstellungsverfahren behandelt.  
  
## <a name="manage-the-private-key-setting"></a>Die Einstellung des private Schlüssels verwalten  
Sie müssen dem AD FS-Dienstkonto Zugriff auf den privaten Schlüssel des neuen Zertifikats erteilen. Sie müssen diese Berechtigung erneut gewähren, wenn Sie das Kommunikationszertifikat ersetzen, nachdem es abgelaufen ist. Um die Berechtigung zu erteilen, gehen Sie folgendermaßen vor:  
  
1.  Klicken Sie auf **Start**und dann auf **Ausführen**.  
  
2.  Geben Sie **MMC** ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Wählen Sie aus der Liste **Verfügbare Snap-Ins** **Zertifikate** aus und klicken Sie auf **Hinzufügen**. Der Zertifikate-Snap-In-Assistent wird gestartet.  
  
5.  Wählen Sie **Computerkonto** aus, und klicken Sie auf **Weiter**.  
  
6.  Wählen Sie **Lokaler Computer: (Computer, auf dem diese Konsole ausgeführt wird)** und klicken Sie auf **Finish**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Erweitern Sie den Ordner **Konsolenstamm\Zertifikate\(Lokaler Computer)\Persönlich\Zertifikate**.  
  
9.  Klicken Sie mit der rechten Maustaste auf das **AD FS-Zertifikat**, und klicken Sie dann auf **Alle Aufgaben** und **Private Schlüssel verwalten**.  
  
10. Klicken Sie im Fenster **Berechtigungen** auf **Hinzufügen**.  
  
11. Wählen Sie im Fenster **Objekttypen** den Objekttyp **Dienstkonten** aus, und klicken Sie dann auf **OK**.  
  
12. Geben Sie den Namen des Kontos ein, auf dem AD FS ausgeführt wird. Im Testbeispiel ist dies ADFSService. Klicken Sie auf **OK**.  
  
13. Geben Sie im Fenster **Berechtigungen** dem Konto mindestens Leseberechtigungen und klicken Sie auf **OK**.  
  
Wenn Ihnen die Option zum Verwalten der private Schlüssel nicht zur Verfügung steht, müssen Sie den folgenden Befehl ausführen: `certutil -repairstore my *`  
  
## <a name="verify-that-ad-fs-is-operational"></a>Stellen Sie sicher, dass AD FS betriebsbereit ist  
Um sicherzustellen, dass AD FS betriebsbereit ist, öffnen Sie ein Browserfenster und wechseln Sie zu https://blueadfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml 
  
Im Browser-Fenster werden die Verbundservermetadaten ohne Formatierung angezeigt. Wenn die Daten ohne SSL-Fehler oder -Warnungen angezeigt wird, ist Ihr Verbundserver betriebsbereit.  
  
Nächster Schritt: [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt3, Einrichten von Arbeitsordnern](deploy-work-folders-adfs-step3.md)  
  
## <a name="see-also"></a>Weitere Informationen  
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)  
  

