---
ms.assetid: d2429185-9720-4a04-ad94-e89a9350cdba
title: Bereitstellen von Arbeitsordnern
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dongill
ms.author: jgerend
ms.date: 6/24/2017
description: "Arbeitsordner bereitstellen, einschließlich der Installation der Serverrolle, der Erstellung von Synchronisierungsfreigaben und von DNS-Einträgen."
ms.openlocfilehash: 13570b65ba4e15bffd8d57a9df52150a66608a79
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="deploying-work-folders"></a>Bereitstellen von Arbeitsordnern

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

In diesem Thema werden die erforderlichen Schritte zum Implementieren von Arbeitsordnern erläutert. Es wird vorausgesetzt, dass Sie das Thema [Planen einer Arbeitsordnerbereitstellung](plan-work-folders.md) bereits gelesen haben.  
  
 Die Bereitstellung von Arbeitsordnern ist ein Prozess, der mehrere Server und Technologien beinhalten kann, und umfasst die im Folgenden beschriebenen Schritte.  
  
> [!TIP]
>  Die einfachste Arbeitsordnerbereitstellung ist ein einzelner Dateiserver (oft als Synchronisierungsserver bezeichnet) ohne Unterstützung der Synchronisierung über das Internet, die eine hilfreiche Bereitstellung für eine Testumgebung oder als Synchronisierungslösung für Clientcomputer sein kann, die der Domäne beigetreten sind. Zum Erstellen einer einfachen Bereitstellung müssen mindestens die folgenden Schritte ausgeführt werden: 
>  -   Schritt1: Abrufen von SSL-Zertifikaten  
>  -   Schritt2: Erstellen von DNS-Einträgen 
>  -   Schritt3: Installieren von Arbeitsordnern auf Dateiservern  
>  -   Schritt4: Binden des SSL-Zertifikats auf den Synchronisierungsservern
>  -   Schritt 5: Erstellen von Sicherheitsgruppen für Arbeitsordner  
>  -   Schritt7: Erstellen von Synchronisierungsfreigaben für Benutzerdaten  
  
## <a name="step-1-obtain-ssl-certificates"></a>Schritt1: Abrufen von SSL-Zertifikaten  
 Die Arbeitsordner verwenden HTTPS, um Dateien zwischen den Arbeitsordner-Clients und den Arbeitsordner-Servern sicher zu synchronisieren. Für die von Arbeitsordnern verwendeten SSL-Zertifikate gelten die folgenden Anforderungen:  
  
-   Das Zertifikat muss von einer vertrauenswürdigen Stammzertifizierungsstelle ausgestellt sein. Für die meisten Arbeitsordnerimplementierungen wird eine öffentlich vertrauenswürdige Zertifizierungsstelle (ZS) empfohlen, da Zertifikate von internetbasierten Geräten verwendet werden, die keiner Domäne angehören.  
  
-   Das Zertifikat muss gültig sein.  
  
-   Der private Schlüssel des Zertifikats muss exportierbar sein (das Zertifikat muss auf mehreren Servern installiert werden).  
  
-   Der Antragstellername des Zertifikats muss die öffentliche Arbeitsordner-URL enthalten, die verwendet wird, um den Arbeitsordnerdienst über das Internet zu ermitteln. Die URL muss das Format `workfolders.`*<domain_name>* aufweisen.  
  
-   Im Zertifikat müssen alternative Antragstellernamen (SANs) vorhanden sein, die den Servernamen für jeden verwendeten Synchronisierungsserver auflisten.

 Im [Blog](https://blogs.technet.microsoft.com/filecab/2013/08/09/work-folders-certificate-management/) „Zertifikatverwaltung der Arbeitsordner” finden Sie weitere Informationen zum Verwenden von Zertifikaten mit Arbeitsordner.
  
## <a name="step-2-create-dns-records"></a>Schritt2: Erstellen von DNS-Einträgen  
 Damit Benutzer Ordner über das Internet synchronisieren können, müssen Sie einen Host (A)-Eintrag im öffentlichen DNS erstellen, um Internetclients das Auflösen der Arbeitsordner-URL zu ermöglichen. Dieser DNS-Eintrag muss in die externe Schnittstelle des Reverseproxyservers aufgelöst werden.  
  
 Erstellen Sie im internen Netzwerk einen Arbeitsordner „CNAME-Eintrag in DNS”, in dem der FDQN des Arbeitsordnerservers aufgelöst wird. Wenn Arbeitsordner-Clients die AutoErmittlung verwenden, ist die URL zum Entdecken des Arbeitsordner-Servers https://workfolders.Domain.com. Wenn Sie die AutoErmittlung verwenden möchten, muss der Workfolders „CNAME-Eintrag” in DNS vorhanden sein.  
  
## <a name="step-3-install-work-folders-on-file-servers"></a>Schritt3: Installieren von Arbeitsordnern auf Dateiservern  
 Sie können Arbeitsordner mithilfe des Server-Managers oder mit WindowsPowerShell lokal oder remote über das Netzwerk auf einem in eine Domäne eingebundenen Server installieren. Dies ist hilfreich, wenn Sie mehrere Synchronisierungsserver im Netzwerk konfigurieren.  
  
Gehen Sie wie folgt vor, um die Rolle im Server-Manager bereitzustellen:  
  
1.  Starten Sie den **Assistenten zum Hinzufügen von Rollen und Features**.  
  
2.  Wählen Sie auf der Seite **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus.  
  
3.  Wählen Sie auf der Seite **Zielserver auswählen** den Server aus, auf dem Sie Arbeitsordner installieren möchten.  
  
4.  Erweitern Sie auf der Seite **Serverrollen auswählen** die Knoten **Datei- und Speicherdienste** und **Datei- und iSCSI-Dienste**, und wählen Sie dann **Arbeitsordner** aus.  
  
5.  Wenn Sie gefragt werden, ob Sie den **hostfähigen IIS-Webkern** installieren möchten, klicken Sie auf **OK**, um die für Arbeitsordner mindestens erforderliche Version der Internetinformationsdienste (IIS) zu installieren.  
  
6.  Klicken Sie auf **Weiter**, bis Sie den Assistenten abgeschlossen haben.

Verwenden Sie zum Bereitstellen der Rolle mit WindowsPowerShell das folgende Cmdlet:
  
```powershell  
Add-WindowsFeature FS-SyncShareService  
```

## <a name="step-4-binding-the-ssl-certificate-on-the-sync-servers"></a>Schritt4: Binden des SSL-Zertifikats auf den Synchronisierungsservern
 Durch Arbeitsordner wird der hostfähige IIS-Webkern installiert, eine IIS-Komponente, die das Aktivieren von Webdiensten ohne vollständige IIS-Installation ermöglicht. Nach der Installation des hostfähigen IIS-Webkerns sollten Sie das SSL-Zertifikat für den Server an die Standardwebsite auf dem Dateiserver binden. Durch die Installation des hostfähigen IIS-Webkerns wird jedoch nicht die IIS-Verwaltungskonsole installiert.

 Zum Binden des Zertifikats an die Standardwebschnittstelle stehen zwei Optionen zur Auswahl. Bei beiden Optionen muss der private Schlüssel für das Zertifikat im persönlichen Speicher des Computers installiert worden sein.

- Verwenden Sie die IIS-Verwaltungskonsole auf einem Server, auf dem sie installiert ist. Stellen Sie in der Konsole eine Verbindung mit dem gewünschten Dateiserver her, und wählen Sie dann die Standardwebsite für diesen Server aus. Die Standardwebseite wird deaktiviert angezeigt, es ist aber dennoch möglich, die Bindungen für die Website zu bearbeiten und das an die Website zu bindende Zertifikat auszuwählen.

- Verwenden Sie den Befehl „netsh” um das Zertifikat an die HTTPS-Schnittstelle der Standardwebsite zu binden. Der Befehl lautet wie folgt:

    ```
    netsh http add sslcert ipport=<IP address>:443 certhash=<Cert thumbprint> appid={CE66697B-3AA0-49D1-BDBD-A25C8359FD5D} certstorename=MY
    ```

## <a name="step-5-create-security-groups-for-work-folders"></a>Schritt 5: Erstellen von Sicherheitsgruppen für Arbeitsordner
 Bevor Synchronisierungsfreigaben erstellt werden, muss ein Mitglied der Gruppe "Domänen-Admins" oder "Organisations-Admins" einige Sicherheitsgruppen in den Active Directory Domain Services (AD DS) für Arbeitsordner erstellen (es können auch wie in Schritt6 beschrieben Objektverwaltungsaufgaben zugewiesen werden). Die folgenden Gruppen sind erforderlich:

- Eine Gruppe pro Synchronisierungsfreigabe, um die zum Synchronisieren mit der Synchronisierungsfreigabe berechtigten Benutzer anzugeben

- Eine Gruppe für alle Arbeitsordneradministratoren, damit sie für jedes Benutzerobjekt ein Attribut bearbeiten können, durch das der Benutzer mit dem richtigen Synchronisierungsserver verknüpft wird (sofern mehrere Synchronisierungsserver verwendet werden)

 Gruppen sollten gemäß den standardmäßigen Benennungskonventionen benannt und nur für Arbeitsordner verwendet werden, um potenzielle Konflikte mit anderen Sicherheitsanforderungen zu vermeiden.

 Führen Sie das folgende Verfahren zum Erstellen der entsprechenden Sicherheitsgruppen mehrmals aus – einmal für jede Synchronisierungsfreigabe und einmal optional zum Erstellen einer Gruppe für Dateiserveradministratoren.

#### <a name="to-create-security-groups-for-work-folders"></a>So erstellen Sie Sicherheitsgruppen für Arbeitsordner

1. Öffnen Sie den Server-Manager auf einem Computer mit Windows Server 2012 R2 oder Windows Server 2016, auf dem das Active Directory-Verwaltungscenter installiert ist.

2.  Klicken Sie im Menü **Extras** auf die Option für das **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.

3.  Klicken Sie mit der rechten Maustaste auf den Container, in dem Sie die neue Gruppe erstellen möchten (z.B. der Container "Benutzer" der entsprechenden Domäne oder Organisationseinheit), klicken Sie auf **Neu** und anschließend auf **Gruppe**.

4.  Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:

    -   Geben Sie im Dialogfeld **Gruppenname** den Namen der Sicherheitsgruppe ein, z.B.: **Benutzer der Personal-Synchronisierungsfreigabe** oder **Arbeitsordneradministratoren**.  
  
    -   Klicken Sie im Abschnitt **Gruppenbereich** auf **Sicherheit** und anschließend auf **Global**.  
  
5.  Klicken Sie im Abschnitt **Mitglieder** auf **Hinzufügen**. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.  
  
6.  Geben Sie die Namen der Benutzer oder Gruppen ein, denen Sie Zugriff auf eine bestimmte Synchronisierungsfreigabe gewähren möchten (wenn Sie eine Gruppe zum Steuern des Zugriffs auf eine Synchronisierungsfreigabe erstellen), oder geben Sie die Namen der Arbeitsordneradministratoren ein (wenn Sie Benutzerkonten zum automatischen Ermitteln des richtigen Synchronisierungsservers konfigurieren), und klicken Sie auf **OK** und anschließend erneut auf **OK**.

Verwenden Sie zum Erstellen einer Sicherheitsgruppe mit WindowsPowerShell die folgenden Cmdlets:

```powershell  
$GroupName = "Work Folders Administrators"  
$DC = "DC1.contoso.com"  
$ADGroupPath = "CN=Users,DC=contoso,DC=com"  
$Members = "CN=Maya Bender,CN=Users,DC=contoso,DC=com","CN=Irwin Hume,CN=Users,DC=contoso,DC=com"  
  
New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:$GroupName -Path:$ADGroupPath -SamAccountName:$GroupName -Server:$DC  
Set-ADGroup -Add:@{'Member'=$Members} -Identity:$GroupName -Server:$DC
```

## <a name="step-6-optionally-delegate-user-attribute-control-to-work-folders-administrators"></a>Schritt6: Zuweisen der Objektverwaltung für Benutzerattribute zu Arbeitsordneradministratoren (optional)  
 Wenn Sie mehrere Synchronisierungsserver bereitstellen und Benutzer automatisch an den richtigen Synchronisierungsserver weiterleiten möchten, müssen Sie ein Attribut in jedem Benutzerkonto in AD DS aktualisieren. Normalerweise erfordert dies jedoch, dass ein Mitglied der Gruppe "Domänen-Admins" oder "Organisations-Admins" die Attribute aktualisiert, was schnell lästig werden kann, wenn häufig Benutzer hinzugefügt oder zwischen Synchronisierungsservern verschoben werden müssen.  
  
 Aus diesem Grund kann ein Mitglied der Gruppe "Domänen-Admins" oder "Organisations-Admins" die Fähigkeit zum Ändern der msDS-SyncServerURL-Eigenschaft von Benutzerobjekten wie im folgenden Verfahren beschrieben der Gruppe "Arbeitsordneradministratoren" zuweisen, die Sie in Schritt5 erstellt haben.  
  
#### <a name="delegate-the-ability-to-edit-the-msds-syncserverurl-property-on-user-objects-in-ad-ds"></a>Delegieren der Fähigkeit zum Bearbeiten der msDS-SyncServerURL-Eigenschaft von Benutzerobjekten in AD DS  
  
1.  Öffnen Sie den Server-Manager auf einem Computer mit Windows Server 2012 R2 oder Windows Server 2016, auf dem Active Directory-Benutzer und -Computer installiert ist.  
  
2.  Klicken Sie im Menü **Extras** auf **Active Directory-Benutzer und -Computer**. "Active Directory-Benutzer und -Computer" wird angezeigt.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, unter der sich sämtliche Benutzerobjekte für Arbeitsordner befinden (wenn Benutzer in mehreren Organisationseinheiten oder Domänen gespeichert sind, klicken Sie mit der rechten Maustaste auf den gemeinsamen Container aller Benutzer), und klicken Sie anschließend auf **Objektverwaltung zuweisen**. Der Assistent zum Zuweisen der Objektverwaltung wird angezeigt.  
  
4.  Klicken Sie auf der Seite **Benutzer und Gruppen** auf **Hinzufügen**. und geben Sie dann die Gruppe an, die Sie für Arbeitsordneradministratoren erstellt haben (z.B. **Arbeitsordneradministratoren**).  
  
5.  Klicken Sie auf der Seite **Zuzuweisende Aufgaben** auf **Benutzerdefinierte Aufgaben zum Zuweisen erstellen**.  
  
6.  Klicken Sie auf der Seite **Active Directory-Objekttyp** auf **Folgenden Objekten im Ordner**, und aktivieren Sie dann das Kontrollkästchen **Benutzerobjekte**.  
  
7.  Deaktivieren Sie auf der Seite **Berechtigungen** das Kontrollkästchen **Allgemein**, aktivieren Sie das Kontrollkästchen **Eigenschaftenspezifisch** und anschließend die Kontrollkästchen für **msDS-SyncServerUrl lesen** und **msDS-SyncServerUrl schreiben**.

Verwenden Sie zum Delegieren der Fähigkeit zum Bearbeiten der msDS-SyncServerURL-Eigenschaft von Benutzerobjekten mit WindowsPowerShell das folgende Skript, in dem der Befehl "DsAcls" verwendet wird.
  
```powershell  
$GroupName = "Contoso\Work Folders Administrators"  
$ADGroupPath = "CN=Users,dc=contoso,dc=com"  
  
DsAcls $ADGroupPath /I:S /G ""$GroupName":RPWP;msDS-SyncServerUrl;user"  
```  
  
> [!NOTE]
>  In Domänen mit vielen Benutzern kann die Zuweisung etwas Zeit in Anspruch nehmen.  
  
## <a name="step-7-create-sync-shares-for-user-data"></a>Schritt7: Erstellen von Synchronisierungsfreigaben für Benutzerdaten  
 Jetzt können Sie einen Ordner auf dem Synchronisierungsserver angeben, in dem die Dateien der Benutzer gespeichert werden sollen. Dieser Ordner wird als Synchronisierungsfreigabe bezeichnet und kann anhand des folgenden Verfahrens erstellt werden.  
  
1.  Wenn Sie noch nicht über ein NTFS-Volume mit freiem Speicherplatz für die Synchronisierungsfreigabe und die darin enthaltenen Benutzerdateien verfügen, erstellen Sie ein neues Volume, das Sie mit dem NTFS-Dateisystem formatieren.  
  
2.  Klicken Sie im Server-Manager auf **Datei- und Speicherdienste** und anschließend auf **Arbeitsordner**.  
  
3.  Oben im Detailbereich wird eine Liste der vorhandenen Synchronisierungsfreigaben angezeigt. Klicken Sie zum Erstellen einer neuen Synchronisierungsfreigabe im Menü **Aufgaben** auf **Neue Synchronisierungsfreigabe**. Der Assistent für neue Synchronisierungsfreigaben wird angezeigt.  
  
4.  Geben Sie auf der Seite **Server und Pfad auswählen** den gewünschten Speicherort für die Synchronisierungsfreigabe an. Wenn Sie bereits eine Dateifreigabe für diese Benutzerdaten erstellt haben, können Sie sie auswählen. Alternativ können Sie einen neuen Ordner erstellen.  
  
    > [!NOTE]
    >  Standardmäßig ist der direkte Zugriff auf Synchronisierungsfreigaben über eine Dateifreigabe nicht möglich (sofern Sie keine vorhandene Dateifreigabe auswählen). Wenn Sie den Zugriff auf eine Synchronisierungsfreigabe über eine Dateifreigabe zulassen möchten, verwenden Sie die Kachel **Freigeben** im Server-Manager oder das Cmdlet [New-SmbShare](http://technet.microsoft.com/library/jj635722.aspx), um eine Dateifreigabe zu erstellen (möglichst mit aktivierter zugriffsbasierter Aufzählung).  
  
5.  Wählen Sie auf der Seite **Struktur für Benutzerordner angeben** eine Benennungskonvention für Benutzerordner in der Synchronisierungsfreigabe aus. Zwei Optionen stehen zur Verfügung:  
  
    -   **Benutzeralias** erstellt Benutzerordner, die keinen Domänennamen enthalten. Wählen Sie diese Benennungskonvention aus, wenn Sie eine Dateifreigabe verwenden, die bereits mit der Ordnerumleitung oder einer anderen Benutzerdatenlösung genutzt wird. Optional können Sie das Kontrollkästchen **Nur den folgenden Unterordner synchronisieren** aktivieren, um nur einen bestimmten Unterordner zu synchronisieren, z.B. den Ordner „Dokumente“.  
  
    -   **Benutzer alias@domain** erstellt Benutzerordner, die einen Domänennamen enthalten. Wählen Sie diese Benennungskonvention aus, wenn Sie keine bereits mit der Ordnerumleitung oder einer anderen Benutzerdatenlösung genutzte Dateifreigabe verwenden. Durch diese Einstellung werden Konflikte bei der Ordnerbenennung verhindert, wenn mehrere Benutzer der Freigabe identische Aliase haben (dies kann passieren, wenn die Benutzer unterschiedlichen Domänen angehören).  
  
6.  Geben Sie auf der Seite **Name der Synchronisierungsfreigabe eingeben** einen Namen und eine Beschreibung für die Synchronisierungsfreigabe an. Dieser Name wird nicht im Netzwerk angekündigt, ist jedoch im Server-Manager und in WindowsPowerShell sichtbar, um die Unterscheidung von Synchronisierungsfreigaben zu erleichtern.  
  
7.  Geben Sie auf der Seite **Gruppen Synchronisierungszugriff gewähren** die von Ihnen erstellte Gruppe an, die die zur Verwendung dieser Synchronisierungsfreigabe berechtigten Benutzer enthält.  
  
    > [!IMPORTANT]
    >  Zum Verbessern der Leistung und Sicherheit sollten Sie nicht einzelnen Benutzern, sondern Gruppen Zugriff gewähren und dabei so spezifisch wie möglich sein. Vermeiden Sie z.B. allgemeine Gruppen wie "Authentifizierte Benutzer" und "Domänenbenutzer". Wenn Sie Gruppen mit vielen Benutzern Zugriff gewähren, nimmt das Abfragen von AD DS durch Arbeitsordner mehr Zeit in Anspruch. Erstellen Sie im Fall einer großen Anzahl von Benutzern mehrere Synchronisierungsfreigaben, um die Last zu verteilen.  
  
8.  Geben Sie auf der Seite **Geräterichtlinien angeben** an, ob Sicherheitseinschränkungen auf Clientcomputern und -geräten erforderlich sind. Die folgenden zwei Geräterichtlinien können einzeln ausgewählt werden:  
  
    -   **Arbeitsordner verschlüsseln**: Arbeitsordner müssen auf Clientcomputern und -geräten verschlüsselt werden  
  
    -   **Bildschirm automatisch sperren und ein Kennwort anfordern**: Der Bildschirm von Clientcomputern und -geräten wird nach 15Minuten automatisch gesperrt und muss durch Eingabe eines mindestens sechs Zeichen langen Kennworts entsperrt werden. Zudem wird nach 10fehlgeschlagenen Versuchen der Sperrmodus des Geräts aktiviert.  
  
        > [!IMPORTANT]
        >  Wenn Sie Kennwortrichtlinien für Windows 7-PCs und für Nichtadministratoren auf Computern, die einer Domäne angehören, erzwingen möchten, sollten Sie stattdessen Gruppenrichtlinien-Kennwortrichtlinien für die Computerdomänen verwenden und diese Domänen von den Kennwortrichtlinien für Arbeitsordner ausschließen. Domänen können nach dem Erstellen der Synchronisierungsfreigabe mithilfe des Cmdlets [Set-Syncshare -PasswordAutoExcludeDomain](http://technet.microsoft.com/library/dn296649\(v=wps.630\).aspx) ausgeschlossen werden. Informationen zum Festlegen der Gruppenrichtlinien-Kennwortrichtlinien finden Sie unter [Kennwortrichtlinie](https://technet.microsoft.com/library/hh994572(v=ws.11).aspx).  
  
9. Überprüfen Sie Ihre Einstellungen, und schließen Sie den Assistenten ab, um die Synchronisierungsfreigabe zu erstellen.

Sie können Synchronisierungsfreigaben mit dem WindowsPowerShell-Cmdlet [New-SyncShare](http://technet.microsoft.com/library/dn296635.aspx) erstellen. Im Folgenden sehen Sie ein Beispiel für diese Methode:  
  
```powershell  
New-SyncShare "HR Sync Share" K:\Share-1 –User "HR Sync Share Users"  
```  
  
Im folgenden Beispiel wird eine neue Synchronisierungsfreigabe namens *Share01* am Pfad *K:\Share-1* erstellt und der Gruppe *Benutzer der Personal-Synchronisierungsfreigabe* Zugriff gewährt.  
  
> [!TIP]
>  Nachdem Sie Synchronisierungsfreigaben erstellt haben, können Sie die Daten in den Freigaben mit dem Ressourcen-Manager für Dateiserver verwalten. Sie können z.B. die Kachel **Kontingent** auf der Seite "Arbeitsordner" im Server-Manager verwenden, um Kontingente für die Benutzerordner festzulegen. Zudem können Sie mit [Dateiprüfungsverwaltung](http://technet.microsoft.com/library/cc732074.aspx) die Dateitypen steuern, die von Arbeitsordnern synchronisiert werden, oder wie in den Szenarien unter [Dynamische Zugriffssteuerung](https://technet.microsoft.com/windows-server-docs/identity/solution-guides/dynamic-access-control--scenario-overview) beschrieben komplexere Dateiklassifizierungen vornehmen.  
  
## <a name="step-8-optionally-specify-a-tech-support-email-address"></a>Schritt8: Geben Sie optional eine E-Mail-Adresse für den technischen Support ein   
 Nach der Installation von Arbeitsordnern auf einem Dateiserver möchten Sie wahrscheinlich eine administrative E-Mail-Adresse für den Server angeben. Gehen Sie wie folgt vor, um eine E-Mail-Adresse hinzuzufügen:  
  
#### <a name="specifying-an-administrative-contact-email"></a>Angeben einer Administratorkontakt-E-Mail-Adresse 
  
1.  Klicken Sie im Server-Manager auf **Datei- und Speicherdienste** und anschließend auf **Server**.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Synchronisierungsserver, und klicken Sie anschließend auf **Arbeitsordnereinstellungen**. Das Fenster "Arbeitsordnereinstellungen" wird angezeigt.  
  
3.  Klicken Sie im Navigationsbereich auf **Support-E-Mail-Adresse**, und geben Sie die E-Mail-Adresse(n) ein, die Benutzer bei Supportanfragen im Zusammenhang mit Arbeitsordnern verwenden sollen. Klicken Sie anschließend auf **OK**.  
  
     Benutzer von Arbeitsordnern können über einen Link in der Arbeitsordnersystemsteuerung eine E-Mail mit Diagnoseinformationen zum Clientcomputer an die hier angegebenen Adressen senden.  
  
## <a name="step-9-optionally-set-up-server-automatic-discovery"></a>Schritt9: Einrichten der automatischen Serverermittlung (optional)  
 Wenn Sie in Ihrer Umgebung mehrere Synchronisierungsserver hosten, sollten Sie die automatische Serverermittlung konfigurieren, indem Sie die **msDS-SyncServerURL**-Eigenschaft in Benutzerkonten in AD DS auffüllen.  
  
>[!NOTE]
>Die msDS-SyncServerURL-Eigenschaft im Active Directory sollte nicht für Remotebenutzer definiert werden, die über eine Reverseproxylösung wie beispielsweise Web Application Proxy oder Azure AD-Anwendungsproxy auf Arbeitsordner zugreifen. Wenn die msDS-SyncServerURL-Eigenschaft definiert ist, versucht der Arbeitsordner-Client auf eine interne URL zuzugreifen, auf die nicht über die Reverseproxylösung zugegriffen werden kann. Bei Verwendung des Webanwendungsproxys oder Azure AD-Anwendungsproxy müssen Sie eindeutige E-Mail-Anwendungen für jeden Arbeitsordner-Server erstellen. Weitere Informationen finden Sie unter [Bereitstellen von Arbeitsordnern mit AD FS und Web Application Proxy: Übersicht](deploy-work-folders-adfs-overview.md) oder [Bereitstellen von Arbeitsordnern mit Azure AD-Anwendungsproxy](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/).


 Zuvor müssen Sie einen Windows Server 2012 R2-Domänencontroller installieren oder mithilfe der Befehle `Adprep /forestprep` und `Adprep /domainprep` die Gesamtstruktur und die Domänenschemas aktualisieren. Informationen zur sicheren Ausführung dieser Befehle finden Sie unter [Ausführen von Adprep](http://technet.microsoft.com/library/dd464018.aspx).  
  
 Wahrscheinlich möchten Sie auch eine Sicherheitsgruppe für Dateiserveradministratoren erstellen und ihnen delegierte Berechtigungen zum Ändern des entsprechenden Benutzerattributs erteilen (siehe Schritt5 und Schritt6). Wenn Sie diese Schritte nicht ausführen, müssen Sie ein Mitglied der Gruppe "Domänen-Admins" oder "Organisations-Admins" bitten, die automatische Ermittlung für jeden Benutzer zu konfigurieren.  
  
#### <a name="to-specify-the-sync-server-for-users"></a>So geben Sie die Synchronisierungsserver für Benutzer an  
  
1.  Öffnen Sie den Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungstools installiert sind.  
  
2.  Klicken Sie im Menü **Extras** auf die Option für das **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.  
  
3.  Navigieren Sie zum Container **Benutzer** in der entsprechenden Domäne, klicken Sie mit der rechten Maustaste auf den Benutzer, dem Sie eine Synchronisierungsfreigabe zuweisen möchten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie im Navigationsbereich auf **Erweiterungen**.  
  
5.  Klicken Sie auf die Registerkarte **Attribut-Editor**, wählen Sie **msDS-SyncServerUrl** aus, und klicken Sie anschließend auf **Bearbeiten**. Das Dialogfeld "Editor für mehrwertige Zeichenfolgen" wird angezeigt.  
  
6.  Geben Sie im Dialogfeld **Hinzuzufügender Wert** die URL des Synchronisierungsservers ein, mit dem dieser Benutzer Ordner synchronisieren soll, klicken Sie auf **Hinzufügen**, auf **OK** und dann noch einmal auf **OK**.  
  
    > [!NOTE]
    >  Die Synchronisierungsserver-URL lautet einfach `https://` oder `http://` (je nachdem, ob eine sichere Verbindung erforderlich ist) gefolgt vom vollqualifizierten Domänennamen des Synchronisierungsservers. Beispiel: **https://sync1.contoso.com**.

Verwenden Sie Active Directory-PowerShell, um das Attribut für mehrere Benutzer aufzufüllen. Im folgenden Beispiel wird das Attribut für alle Mitglieder der in Schritt5 erörterten Gruppe *Benutzer der Personal-Synchronisierungsfreigabe* aufgefüllt.
  
```powershell  
$SyncServerURL = "https://sync1.contoso.com"  
$GroupName = "HR Sync Share Users"  
  
Get-ADGroupMember -Identity $GroupName |  
Set-ADUser –Add @{"msDS-SyncServerURL"=$SyncServerURL}  
  
```  
  
## <a name="step-10-optionally-configure-web-application-proxy-azure-ad-application-proxy-or-another-reverse-proxy"></a>Schritt10: Konfigurieren Sie optionale einen Webanwendungsproxy, einen Azure AD-Anwendungsproxy oder einen anderen Reverseproxy  

Um Remotebenutzern den Zugriff auf die Arbeitsordner zu ermöglichen, müssen Sie Arbeitsordner-Server über einen Reverseproxy veröffentlichen, sodass Arbeitsordner extern im Internet verfügbar sind. Verwenden Sie dazu Webanwendungsproxy, Azure Active Directory-Anwendungsproxy oder eine andere Reverseproxylösung.  
  
Informationen zum Einrichten des Zugriffs auf Arbeitsordner mithilfe von AD FS und Webanwendungsproxy finden Sie unter [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy (WAP)](deploy-work-folders-adfs-overview.md). Hintergrundinformationen zum Webanwendungsproxy finden Sie unter [Webanwendungsproxy: Übersicht in Windows Server 2016](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server). Ausführliche Informationen zum Veröffentlichen von Anwendungen wie Arbeitsordner auf dem Internet unter Verwendung des Webanwendungsproxys finden Sie unter [Veröffentlichen von Anwendungen mit AD FS-Vorauthentifizierung](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/publishing-applications-using-ad-fs-preauthentication).
 
Informationen zum Einrichten des Zugriffs auf Arbeitsordner mithilfe von Azure Active Directory-Anwendungsproxy finden Sie unter [Aktivieren des Remotezugriffs auf Arbeitsordner mithilfe von Azure Active Directory-Anwendungsproxy](https://blogs.technet.microsoft.com/filecab/?p=7945) 
  
## <a name="step-11-optionally-use-group-policy-to-configure-domain-joined-pcs"></a>Schritt11: Konfigurieren von in eine Domäne eingebundenen Computern mithilfe von Gruppenrichtlinien (optional)  

Wenn Sie für viele in eine Domäne eingebundene Computer Arbeitsordner bereitstellen möchten, können Sie die folgenden Konfigurationsaufgaben für Clientcomputer mithilfe von Gruppenrichtlinien durchführen:  
  
-   Angeben der von Benutzern zu verwendenden Synchronisierungsserver  
  
-   Erzwingen der automatischen Einrichtung von Arbeitsordnern anhand von Standardeinstellungen (lesen Sie vor dem Ausführen dieser Aufgabe die Informationen zu Gruppenrichtlinien im Thema [Entwerfen einer Arbeitsordnerimplementierung](plan-work-folders.md))  
  
 Erstellen Sie zum Steuern dieser Einstellungen ein neues Gruppenrichtlinienobjekt (Group Policy object, GPO) für Arbeitsordner, und konfigurieren Sie anschließend die folgenden Gruppenrichtlinieneinstellungen wie erforderlich:  
  
-   Richtlinieneinstellung „Arbeitsordnereinstellungen festlegen“ unter „Benutzerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\WorkFolders“  
  
-   Richtlinieneinstellung „Automatisches Setup für alle Benutzer erzwingen“ unter „Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\WorkFolders“  
  
> [!NOTE]
>  Diese Richtlinieneinstellungen sind nur verfügbar, wenn Sie Gruppenrichtlinien auf einem Computer bearbeiten, auf dem die Gruppenrichtlinienverwaltung unter Windows 8.1, Windows Server 2012 R2 oder höher ausgeführt wird. In Versionen der Gruppenrichtlinienverwaltung von früheren Betriebssystemen sind diese Einstellungen nicht verfügbar. Diese Richtlinieneinstellungen gelten für Windows 7-PCs auf dem die App [Arbeitsordner für Windows 7](http://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) installiert wurde.  
  
##  <a name="BKMK_LINKS"></a> Weitere Informationen  
 Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:  
  
|Inhaltstyp|Verweise|  
|------------------|----------------|  
|**Grundlegendes**|-   [Arbeitsordner](work-folders-overview.md)|  
|**Planen**|-   [Entwerfen einer Arbeitsordnerimplementierung](plan-work-folders.md)|
|**Bereitstellung**|-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy (WAP)](deploy-work-folders-adfs-overview.md)<br />-   [Bereitstellung von Arbeitsordnern in einer Testumgebung](http://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) (Blogbeitrag)<br />-   [Neues Benutzerattribut für die Arbeitsordnerserver-URL](http://blogs.technet.com/b/filecab/archive/2013/10/09/a-new-user-attribute-for-work-folders-server-url.aspx) (Blogbeitrag)|  
|**Technische Referenz**|-   [Interaktive Anmeldung: Schwellenwert für Computerkontosperrung](https://technet.microsoft.com/library/jj966264(v=ws.11).aspx)<br />-   [Cmdlets für Synchronisierungsfreigaben](https://technet.microsoft.com/itpro/powershell/windows/sync-share)|