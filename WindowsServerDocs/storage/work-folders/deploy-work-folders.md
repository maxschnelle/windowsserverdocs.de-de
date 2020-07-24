---
ms.assetid: d2429185-9720-4a04-ad94-e89a9350cdba
title: Bereitstellen von Arbeitsordnern
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dongill
ms.author: jgerend
ms.date: 6/24/2017
description: Bereitstellen von Arbeits Ordnern, einschließlich der Installation der Server Rolle, der Erstellung von Synchronisierungs Freigaben und der Erstellung von DNS-Einträgen.
ms.openlocfilehash: 7335420a70a8872fb92aad5565dbf4b42c6b10b7
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86960012"
---
# <a name="deploying-work-folders"></a>Bereitstellen von Arbeitsordnern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

In diesem Thema werden die erforderlichen Schritte zum Bereitstellen von Arbeits Ordnern erläutert. Es wird vorausgesetzt, dass Sie bereits die [Planung einer Arbeitsordner Bereitstellung](plan-work-folders.md)gelesen haben.  
  
 Die Bereitstellung von Arbeitsordnern ist ein Prozess, der mehrere Server und Technologien beinhalten kann, und umfasst die im Folgenden beschriebenen Schritte.  
  
> [!TIP]
>  Die einfachste Arbeitsordnerbereitstellung ist ein einzelner Dateiserver (oft als Synchronisierungsserver bezeichnet), der keine Unterstützung für die Synchronisierung über das Internet bietet. Dieses Bereitstellungsmodell kann für eine Testumgebung hilfreich sein oder als Synchronisierungslösung für in eine Domäne eingebundene Clientcomputer eingesetzt werden. Zum Erstellen einer einfachen Bereitstellung müssen mindestens die folgenden Schritte ausgeführt werden: 
>  -   Schritt 1: Abrufen von SSL-Zertifikaten  
>  -   Schritt 2: Erstellen von DNS-Einträgen 
>  -   Schritt 3: Installieren von Arbeitsordnern auf Dateiservern  
>  -   Schritt 4: Binden des SSL-Zertifikats auf den Synchronisierungsservern
>  -   Schritt 5: Erstellen von Sicherheitsgruppen für Arbeitsordner  
>  -   Schritt 7: Erstellen von Synchronisierungsfreigaben für Benutzerdaten  
  
## <a name="step-1-obtain-ssl-certificates"></a>Schritt 1: Abrufen von SSL-Zertifikaten  
 Arbeitsordner verwenden HTTPS, um Dateien zwischen den Arbeitsordner Clients und dem Arbeitsordner Server sicher zu synchronisieren. Für die von Arbeitsordnern verwendeten SSL-Zertifikate gelten die folgenden Anforderungen:  
  
- Das Zertifikat muss von einer vertrauenswürdigen Stammzertifizierungsstelle ausgestellt sein. Für die meisten Arbeitsordnerimplementierungen wird eine öffentlich vertrauenswürdige Zertifizierungsstelle (ZS) empfohlen, da Zertifikate von internetbasierten Geräten verwendet werden, die keiner Domäne angehören.  
  
- Das Zertifikat muss gültig sein.  
  
- Der private Schlüssel des Zertifikats muss exportierbar sein (das Zertifikat muss auf mehreren Servern installiert werden).  
  
- Der Antragsteller Name des Zertifikats muss die URL der öffentlichen Arbeitsordner enthalten, die für die Ermittlung des Arbeitsordner diensdienstanbieter über das Internet verwendet wird. – muss im Format `workfolders.` *<domain_name>* vorliegen.  
  
- Im Zertifikat müssen alternative Antragstellernamen (SANs) vorhanden sein, die den Servernamen für jeden verwendeten Synchronisierungsserver auflisten.

  Der [Blog](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) "Arbeitsordner Zertifikat Verwaltung" enthält weitere Informationen zur Verwendung von Zertifikaten mit Arbeits Ordnern.
  
## <a name="step-2-create-dns-records"></a>Schritt 2: Erstellen von DNS-Einträgen  
 Damit Benutzer Ordner über das Internet synchronisieren können, müssen Sie einen Host (A)-Eintrag im öffentlichen DNS erstellen, um Internetclients das Auflösen der Arbeitsordner-URL zu ermöglichen. Dieser DNS-Eintrag muss in die externe Schnittstelle des Reverseproxyservers aufgelöst werden.  
  
 Erstellen Sie in Ihrem internen Netzwerk einen CNAME-Datensatz in DNS Namens workfolders, der in den FDQN eines Arbeitsordner Servers aufgelöst wird. Wenn für Arbeitsordner Clients die Auto Ermittlung verwendet wird, lautet die URL, die zum Ermitteln des Arbeitsordner Servers verwendet wird, https: \/ /workfolders.Domain.com. Wenn Sie die Auto Ermittlung verwenden möchten, muss der CNAME-Datensatz der Arbeitsordner in DNS vorhanden sein.  
  
## <a name="step-3-install-work-folders-on-file-servers"></a>Schritt 3: Installieren von Arbeitsordnern auf Dateiservern  
 Sie können Arbeitsordner mithilfe des Server-Managers oder mit Windows PowerShell lokal oder remote über das Netzwerk auf einem in eine Domäne eingebundenen Server installieren. Dies ist hilfreich, wenn Sie mehrere Synchronisierungsserver im Netzwerk konfigurieren.  
  
Gehen Sie wie folgt vor, um die Rolle im Server-Manager bereitzustellen:  
  
1.  Starten Sie den **Assistenten zum Hinzufügen von Rollen und Features**.  
  
2.  Wählen Sie auf der Seite **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus.  
  
3.  Wählen Sie auf der Seite **Zielserver auswählen** den Server aus, auf dem Sie Arbeitsordner installieren möchten.  
  
4.  Erweitern Sie auf der Seite **Serverrollen auswählen** die Knoten **Datei- und Speicherdienste** und **Datei- und iSCSI-Dienste**, und wählen Sie dann **Arbeitsordner** aus.  
  
5.  Wenn Sie gefragt werden, ob Sie den **hostfähigen IIS-Webkern** installieren möchten, klicken Sie auf **OK**, um die für Arbeitsordner mindestens erforderliche Version der Internetinformationsdienste (IIS) zu installieren.  
  
6.  Klicken Sie auf **Weiter**, bis Sie den Assistenten abgeschlossen haben.

Verwenden Sie zum Bereitstellen der Rolle mit Windows PowerShell das folgende Cmdlet:
  
```powershell  
Add-WindowsFeature FS-SyncShareService  
```

## <a name="step-4-binding-the-ssl-certificate-on-the-sync-servers"></a>Schritt 4: Binden des SSL-Zertifikats auf den Synchronisierungsservern
 Durch Arbeitsordner wird der hostfähige IIS-Webkern installiert, eine IIS-Komponente, die das Aktivieren von Webdiensten ohne vollständige IIS-Installation ermöglicht. Nach der Installation des hostfähigen IIS-Webkerns sollten Sie das SSL-Zertifikat für den Server an die Standardwebsite auf dem Dateiserver binden. Durch die Installation des hostfähigen IIS-Webkerns wird jedoch nicht die IIS-Verwaltungskonsole installiert.

 Zum Binden des Zertifikats an die Standardwebschnittstelle stehen zwei Optionen zur Auswahl. Wenn Sie eine der beiden Optionen verwenden möchten, müssen Sie den privaten Schlüssel für das Zertifikat im persönlichen Speicher des Computers installiert haben.

- Verwenden Sie die IIS-Verwaltungskonsole auf einem Server, auf dem sie installiert ist. Stellen Sie in der Konsole eine Verbindung mit dem gewünschten Dateiserver her, und wählen Sie dann die Standardwebsite für diesen Server aus. Die Standardwebseite wird deaktiviert angezeigt, es ist aber dennoch möglich, die Bindungen für die Website zu bearbeiten und das an die Website zu bindende Zertifikat auszuwählen.

- Verwenden Sie den Befehl %%amp;quot;netsh%%amp;quot;, um das Zertifikat an die HTTPS-Schnittstelle der Standardwebsite zu binden. Der Befehl lautet wie folgt:

    ```
    netsh http add sslcert ipport=<IP address>:443 certhash=<Cert thumbprint> appid={CE66697B-3AA0-49D1-BDBD-A25C8359FD5D} certstorename=MY
    ```

## <a name="step-5-create-security-groups-for-work-folders"></a>Schritt 5: Erstellen von Sicherheitsgruppen für Arbeitsordner
 Bevor Synchronisierungsfreigaben erstellt werden, muss ein Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; oder %%amp;quot;Organisations-Admins%%amp;quot; einige Sicherheitsgruppen in den Active Directory-Domänendiensten (AD DS) für Arbeitsordner erstellen (es können auch wie in Schritt 6 beschrieben Objektverwaltungsaufgaben zugewiesen werden). Die folgenden Gruppen sind erforderlich:

- Eine Gruppe pro Synchronisierungsfreigabe, um die zum Synchronisieren mit der Synchronisierungsfreigabe berechtigten Benutzer anzugeben

- Eine Gruppe für alle Arbeitsordner Administratoren, damit Sie ein Attribut für jedes Benutzerobjekt bearbeiten können, das den Benutzer mit dem richtigen Synchronisierungs Server verknüpft (wenn Sie mehrere Synchronisierungs Server verwenden möchten).

  Gruppen sollten gemäß den standardmäßigen Benennungskonventionen benannt und nur für Arbeitsordner verwendet werden, um potenzielle Konflikte mit anderen Sicherheitsanforderungen zu vermeiden.

  Führen Sie das folgende Verfahren zum Erstellen der entsprechenden Sicherheitsgruppen mehrmals aus – einmal für jede Synchronisierungsfreigabe und einmal optional zum Erstellen einer Gruppe für Dateiserveradministratoren.

#### <a name="to-create-security-groups-for-work-folders"></a>So erstellen Sie Sicherheitsgruppen für Arbeitsordner

1. Öffnen Sie Server-Manager auf einem Computer mit Windows Server 2012 R2 oder Windows Server 2016, auf dem Active Directory Verwaltungs Center installiert ist.

2.  Klicken Sie im Menü **Extras** auf die Option für das **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.

3.  Klicken Sie mit der rechten Maustaste auf den Container, in dem Sie die neue Gruppe erstellen möchten (z. B. der Container %%amp;quot;Benutzer%%amp;quot; der entsprechenden Domäne oder Organisationseinheit), klicken Sie auf **Neu** und anschließend auf **Gruppe**.

4.  Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:

    -   Geben Sie im Feld **Gruppenname** den Namen der Sicherheitsgruppe ein, z. B.: **Benutzer der Personal-Synchronisierungsfreigabe** oder **Arbeitsordneradministratoren**.  
  
    -   Klicken Sie im Abschnitt **Gruppenbereich** auf **Sicherheit** und anschließend auf **Global**.  
  
5.  Klicken Sie im Abschnitt **Mitglieder** auf **Hinzufügen**. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.  
  
6.  Geben Sie die Namen der Benutzer oder Gruppen ein, denen Sie Zugriff auf eine bestimmte Synchronisierungs Freigabe gewähren möchten (wenn Sie eine Gruppe zum Steuern des Zugriffs auf eine Synchronisierungs Freigabe erstellen), oder geben Sie die Namen der Arbeitsordner Administratoren ein (wenn Sie Benutzerkonten konfigurieren, um den entsprechenden Synchronisierungs Server automatisch zu ermitteln), klicken Sie auf **OK**, und klicken Sie dann erneut auf **OK** .

Verwenden Sie zum Erstellen einer Sicherheitsgruppe mit Windows PowerShell die folgenden Cmdlets:

```powershell  
$GroupName = "Work Folders Administrators"  
$DC = "DC1.contoso.com"  
$ADGroupPath = "CN=Users,DC=contoso,DC=com"  
$Members = "CN=Maya Bender,CN=Users,DC=contoso,DC=com","CN=Irwin Hume,CN=Users,DC=contoso,DC=com"  
  
New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:$GroupName -Path:$ADGroupPath -SamAccountName:$GroupName -Server:$DC  
Set-ADGroup -Add:@{'Member'=$Members} -Identity:$GroupName -Server:$DC
```

## <a name="step-6-optionally-delegate-user-attribute-control-to-work-folders-administrators"></a>Schritt 6: Zuweisen der Objektverwaltung für Benutzerattribute zu Arbeitsordneradministratoren (optional)  
 Wenn Sie mehrere Synchronisierungs Server bereitstellen und Benutzer automatisch an den richtigen Synchronisierungs Server weiterleiten möchten, müssen Sie ein Attribut für jedes Benutzerkonto in AD DS aktualisieren. Normalerweise erfordert dies jedoch, dass ein Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; oder %%amp;quot;Organisations-Admins%%amp;quot; die Attribute aktualisiert, was schnell lästig werden kann, wenn häufig Benutzer hinzugefügt oder zwischen Synchronisierungsservern verschoben werden müssen.  
  
 Aus diesem Grund kann ein Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; oder %%amp;quot;Organisations-Admins%%amp;quot; die Fähigkeit zum Ändern der msDS-SyncServerURL-Eigenschaft von Benutzerobjekten wie im folgenden Verfahren beschrieben der Gruppe %%amp;quot;Arbeitsordneradministratoren%%amp;quot; zuweisen, die Sie in Schritt 5 erstellt haben.  
  
#### <a name="delegate-the-ability-to-edit-the-msds-syncserverurl-property-on-user-objects-in-ad-ds"></a>Delegieren der Fähigkeit zum Bearbeiten der msDS-SyncServerURL-Eigenschaft von Benutzerobjekten in AD DS  
  
1.  Öffnen Sie Server-Manager auf einem Computer mit Windows Server 2012 R2 oder Windows Server 2016, auf dem Active Directory Benutzer und Computer installiert sind.  
  
2.  Klicken Sie im Menü **Extras** auf **Active Directory-Benutzer und -Computer**. %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; wird angezeigt.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, unter der sich sämtliche Benutzerobjekte für Arbeitsordner befinden (wenn Benutzer in mehreren Organisationseinheiten oder Domänen gespeichert sind, klicken Sie mit der rechten Maustaste auf den gemeinsamen Container aller Benutzer), und klicken Sie anschließend auf **Objektverwaltung zuweisen**. Der Assistent zum Zuweisen der Objektverwaltung wird angezeigt.  
  
4.  Klicken Sie auf der Seite **Benutzer oder Gruppen** auf **hinzufügen...** und geben Sie dann die Gruppe an, die Sie für Arbeitsordner Administratoren erstellt haben (z. b. **Arbeitsordner Administratoren**).  
  
5.  Klicken Sie auf der Seite **Zuzuweisende Aufgaben** auf **Benutzerdefinierte Aufgaben zum Zuweisen erstellen**.  
  
6.  Klicken Sie auf der Seite **Active Directory-Objekttyp** auf **Folgenden Objekten im Ordner**, und aktivieren Sie dann das Kontrollkästchen **BENUTZER-Objekte**.  
  
7.  Deaktivieren Sie auf der Seite **Berechtigungen** das Kontrollkästchen **Allgemein**, aktivieren Sie das Kontrollkästchen **Eigenschaftenspezifisch** und anschließend die Kontrollkästchen für **msDS-SyncServerUrl lesen** und **msDS-SyncServerUrl schreiben**.

Verwenden Sie zum Delegieren der Fähigkeit zum Bearbeiten der msDS-SyncServerURL-Eigenschaft von Benutzerobjekten mit Windows PowerShell das folgende Skript, in dem der Befehl %%amp;quot;DsAcls%%amp;quot; verwendet wird.
  
```powershell  
$GroupName = "Contoso\Work Folders Administrators"  
$ADGroupPath = "CN=Users,dc=contoso,dc=com"  
  
DsAcls $ADGroupPath /I:S /G ""$GroupName":RPWP;msDS-SyncServerUrl;user"  
```  
  
> [!NOTE]
>  In Domänen mit vielen Benutzern kann die Zuweisung etwas Zeit in Anspruch nehmen.  
  
## <a name="step-7-create-sync-shares-for-user-data"></a>Schritt 7: Erstellen von Synchronisierungsfreigaben für Benutzerdaten  
 An diesem Punkt können Sie einen Ordner auf dem Synchronisierungs Server festlegen, um die Dateien des Benutzers zu speichern. Dieser Ordner wird als Synchronisierungsfreigabe bezeichnet und kann anhand des folgenden Verfahrens erstellt werden.  
  
1. Wenn Sie nicht bereits über ein NTFS-Volume mit freiem Speicherplatz für die Synchronisierungs Freigabe und die darin enthaltenen Benutzer Dateien verfügen, erstellen Sie ein neues Volume, und formatieren Sie es mit dem NTFS-Dateisystem.  
  
2. Klicken Sie im Server-Manager auf **Datei- und Speicherdienste** und anschließend auf **Arbeitsordner**.  
  
3. Oben im Detailbereich wird eine Liste der vorhandenen Synchronisierungsfreigaben angezeigt. Klicken Sie zum Erstellen einer neuen Synchronisierungsfreigabe im Menü **Aufgaben** auf **Neue Synchronisierungsfreigabe**. Der Assistent für neue Synchronisierungsfreigaben wird angezeigt.  
  
4. Geben Sie auf der Seite **Server und Pfad auswählen** den gewünschten Speicherort für die Synchronisierungsfreigabe an. Wenn Sie bereits eine Dateifreigabe für diese Benutzerdaten erstellt haben, können Sie sie auswählen. Alternativ können Sie einen neuen Ordner erstellen.  
  
   > [!NOTE]
   >  Standardmäßig ist auf Synchronisierungs Freigaben nicht direkt über eine Dateifreigabe zugegriffen werden (es sei denn, Sie wählen eine vorhandene Dateifreigabe aus). Wenn Sie den Zugriff auf eine Synchronisierungsfreigabe über eine Dateifreigabe zulassen möchten, verwenden Sie die Kachel **Freigaben** im Server-Manager oder das Cmdlet [New-SmbShare](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB), um eine Dateifreigabe zu erstellen (möglichst mit aktivierter zugriffsbasierter Aufzählung).  
  
5. Wählen Sie auf der Seite **Struktur für Benutzerordner angeben** eine Benennungskonvention für Benutzerordner in der Synchronisierungsfreigabe aus. Es stehen zwei Optionen zur Verfügung:  
  
   - **Benutzeralias** erstellt Benutzerordner, die keinen Domänen Namen enthalten. Wählen Sie diese Benennungskonvention aus, wenn Sie eine Dateifreigabe verwenden, die bereits mit der Ordnerumleitung oder einer anderen Benutzerdatenlösung genutzt wird. Optional können Sie das Kontrollkästchen **Nur den folgenden Unterordner synchronisieren** aktivieren, um nur einen bestimmten Unterordner zu synchronisieren, z. B. den Ordner %%amp;quot;Dokumente%%amp;quot;.  
  
   - <strong>Benutzer alias@domain </strong> erstellt Benutzerordner, die einen Domänen Namen enthalten. Wenn Sie keine Dateifreigabe verwenden, die bereits mit der Ordner Umleitung oder einer anderen Benutzerdaten Lösung verwendet wird, wählen Sie diese Benennungs Konvention aus, um Ordner Benennungs Konflikte auszuschließen, wenn mehrere Benutzer der Freigabe identische Aliase haben (Dies kann vorkommen, wenn die Benutzer zu anderen Domänen gehören).  
  
6. Geben Sie auf der Seite **Name der Synchronisierungsfreigabe eingeben** einen Namen und eine Beschreibung für die Synchronisierungsfreigabe an. Dieser Name wird nicht im Netzwerk angekündigt, ist jedoch im Server-Manager und in Windows PowerShell sichtbar, um die Unterscheidung von Synchronisierungsfreigaben zu erleichtern.  
  
7. Geben Sie auf der Seite **Gruppen Synchronisierungszugriff gewähren** die von Ihnen erstellte Gruppe an, die die zur Verwendung dieser Synchronisierungsfreigabe berechtigten Benutzer enthält.  
  
   > [!IMPORTANT]
   >  Zum Verbessern der Leistung und Sicherheit sollten Sie nicht einzelnen Benutzern, sondern Gruppen Zugriff gewähren und dabei so spezifisch wie möglich sein. Vermeiden Sie z. B. allgemeine Gruppen wie %%amp;quot;Authentifizierte Benutzer%%amp;quot; und %%amp;quot;Domänenbenutzer%%amp;quot;. Wenn Sie Gruppen mit vielen Benutzern Zugriff gewähren, nimmt das Abfragen von AD DS durch Arbeitsordner mehr Zeit in Anspruch. Erstellen Sie im Fall einer großen Anzahl von Benutzern mehrere Synchronisierungsfreigaben, um die Last zu verteilen.  
  
8. Geben Sie auf der Seite **Geräterichtlinien angeben** an, ob Sicherheitseinschränkungen auf Clientcomputern und -geräten erforderlich sind. Die folgenden zwei Geräterichtlinien können einzeln ausgewählt werden:  
  
   -   **Arbeitsordner verschlüsseln** Anforderungen, dass Arbeitsordner auf Client-PCs und-Geräten verschlüsselt werden  
  
   -   **Bildschirm automatisch sperren und ein Kennwort anfordern** Fordert an, dass Client-PCs und-Geräte ihre Bildschirme nach 15 Minuten automatisch sperren, ein sechs Zeichen lang oder länger als Kennwort zum Entsperren des Bildschirms benötigen und nach 10 fehlgeschlagenen Wiederholungen einen Geräte Sperrmodus aktivieren.  
  
       > [!IMPORTANT]
       >  Wenn Sie Kennwortrichtlinien für Windows 7-PCs und für Nichtadministratoren auf Computern, die einer Domäne angehören, erzwingen möchten, sollten Sie stattdessen Gruppenrichtlinien-Kennwortrichtlinien für die Computerdomänen verwenden und diese Domänen von den Kennwortrichtlinien für Arbeitsordner ausschließen. Domänen können nach dem Erstellen der Synchronisierungsfreigabe mithilfe des Cmdlets [Set-Syncshare -PasswordAutoExcludeDomain](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) ausgeschlossen werden. Informationen zum Festlegen der Gruppenrichtlinien-Kennwortrichtlinien finden Sie unter [Kennwortrichtlinie](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh994572(v=ws.11)).  
  
9. Überprüfen Sie Ihre Einstellungen, und schließen Sie den Assistenten ab, um die Synchronisierungsfreigabe zu erstellen.

Sie können Synchronisierungsfreigaben mit dem Windows PowerShell-Cmdlet [New-SyncShare](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh994572(v=ws.11)) erstellen. Im Folgenden sehen Sie ein Beispiel für diese Methode:  
  
```powershell  
New-SyncShare "HR Sync Share" K:\Share-1 –User "HR Sync Share Users"  
```  
  
Im folgenden Beispiel wird eine neue Synchronisierungsfreigabe namens *Share01* am Pfad *K:\Share-1* erstellt und der Gruppe *Benutzer der Personal-Synchronisierungsfreigabe* Zugriff gewährt.  
  
> [!TIP]
>  Nachdem Sie Synchronisierungsfreigaben erstellt haben, können Sie die Daten in den Freigaben mit dem Ressourcen-Manager für Dateiserver verwalten. Sie können z. B. die Kachel **Kontingent** auf der Seite %%amp;quot;Arbeitsordner%%amp;quot; im Server-Manager verwenden, um Kontingente für die Benutzerordner festzulegen. Sie können auch die [Datei Untersuchung-Verwaltung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732074(v=ws.11)) verwenden, um die Dateitypen zu steuern, die von Arbeits Ordnern synchronisiert werden, oder Sie können die in [Dynamic Access Control](../../identity/solution-guides/dynamic-access-control--scenario-overview.md) beschriebenen Szenarien verwenden, um komplexere Datei Klassifizierungs Aufgaben auszuführen.  
  
## <a name="step-8-optionally-specify-a-tech-support-email-address"></a>Schritt 8: Angeben einer e-Mail-Adresse für den technischen Support   
 Nachdem Sie die Arbeitsordner auf einem Dateiserver installiert haben, möchten Sie wahrscheinlich eine e-Mail-Adresse für den administrativen Kontakt für den Server angeben. Verwenden Sie das folgende Verfahren, um eine e-Mail-Adresse hinzuzufügen:  
  
#### <a name="specifying-an-administrative-contact-email"></a>Angeben einer e-Mail-Adresse 
  
1.  Klicken Sie im Server-Manager auf **Datei- und Speicherdienste** und anschließend auf **Server**.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Synchronisierungsserver, und klicken Sie anschließend auf **Arbeitsordnereinstellungen**. Das Fenster %%amp;quot;Arbeitsordnereinstellungen%%amp;quot; wird angezeigt.  
  
3.  Klicken Sie im Navigationsbereich auf **Support-E-Mail-Adresse**, und geben Sie die E-Mail-Adresse(n) ein, die Benutzer bei Supportanfragen im Zusammenhang mit Arbeitsordnern verwenden sollen. Wenn Sie fertig sind, klicken Sie auf **OK** .  
  
     Benutzer von Arbeitsordnern können über einen Link in der Arbeitsordnersystemsteuerung eine E-Mail mit Diagnoseinformationen zum Clientcomputer an die hier angegebenen Adressen senden.  
  
## <a name="step-9-optionally-set-up-server-automatic-discovery"></a>Schritt 9: Einrichten der automatischen Serverermittlung (optional)  
 Wenn Sie in Ihrer Umgebung mehrere Synchronisierungsserver hosten, sollten Sie die automatische Serverermittlung konfigurieren, indem Sie die **msDS-SyncServerURL**-Eigenschaft in Benutzerkonten in AD DS auffüllen.  
  
>[!NOTE]
>Die MSDS-SyncServerURL-Eigenschaft in Active Directory sollte nicht für Remote Benutzer definiert werden, die über eine Reverseproxylösung wie den webanwendungsproxy oder Azure AD Anwendungs Proxy auf Arbeitsordner zugreifen. Wenn die MSDS-SyncServerURL-Eigenschaft definiert ist, versucht der Arbeitsordner Client, auf eine interne URL zuzugreifen, auf die über die Reverseproxylösung nicht zugegriffen werden kann. Bei Verwendung eines webanwendungsproxys oder Azure AD Anwendungs Proxys müssen Sie für jeden Arbeitsordner Server eindeutige Proxy Anwendungen erstellen. Weitere Informationen finden Sie unter Bereitstellen von [Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md) oder Bereitstellen von [Arbeits Ordnern mit Azure AD Anwendungs Proxy](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB).


 Bevor Sie dies tun können, müssen Sie einen Windows Server 2012 R2-Domänen Controller installieren oder die Gesamtstruktur und die Domänen Schemas mithilfe der `Adprep /forestprep` Befehle und aktualisieren `Adprep /domainprep` . Informationen zur sicheren Ausführung dieser Befehle finden Sie unter [Ausführen von %%amp;quot;Adprep exe%%amp;quot;](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)).  
  
 Wahrscheinlich möchten Sie auch eine Sicherheitsgruppe für Dateiserveradministratoren erstellen und ihnen delegierte Berechtigungen zum Ändern des entsprechenden Benutzerattributs erteilen (siehe Schritt 5 und Schritt 6). Wenn Sie diese Schritte nicht ausführen, müssen Sie ein Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; oder %%amp;quot;Organisations-Admins%%amp;quot; bitten, die automatische Ermittlung für jeden Benutzer zu konfigurieren.  
  
#### <a name="to-specify-the-sync-server-for-users"></a>So geben Sie die Synchronisierungsserver für Benutzer an  
  
1.  Öffnen Sie den Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungstools installiert sind.  
  
2.  Klicken Sie im Menü **Extras** auf die Option für das **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.  
  
3.  Navigieren Sie zum Container **Benutzer** in der entsprechenden Domäne, klicken Sie mit der rechten Maustaste auf den Benutzer, dem Sie eine Synchronisierungsfreigabe zuweisen möchten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie im Navigationsbereich auf **Erweiterungen**.  
  
5.  Klicken Sie auf die Registerkarte **Attribut-Editor**, wählen Sie **msDS-SyncServerUrl** aus, und klicken Sie anschließend auf **Bearbeiten**. Das Dialogfeld %%amp;quot;Editor für mehrwertige Zeichenfolgen%%amp;quot; wird angezeigt.  
  
6.  Geben Sie im Feld **Hinzuzufügender Wert** die URL des Synchronisierungsservers ein, mit dem dieser Benutzer Ordner synchronisieren soll, klicken Sie auf **Hinzufügen**, auf **OK** und dann noch einmal auf **OK**.  
  
    > [!NOTE]
    >  Die Synchronisierungsserver-URL lautet einfach `https://` oder `http://` (je nachdem, ob eine sichere Verbindung erforderlich ist) gefolgt vom vollqualifizierten Domänennamen des Synchronisierungsservers. Beispiel **: https: \/ /sync1.contoso.com**.

Verwenden Sie Active Directory-PowerShell, um das Attribut für mehrere Benutzer aufzufüllen. Im folgenden Beispiel wird das Attribut für alle Mitglieder der in Schritt 5 erörterten Gruppe *Benutzer der Personal-Synchronisierungsfreigabe* aufgefüllt.
  
```powershell  
$SyncServerURL = "https://sync1.contoso.com"  
$GroupName = "HR Sync Share Users"  
  
Get-ADGroupMember -Identity $GroupName |  
Set-ADUser –Add @{"msDS-SyncServerURL"=$SyncServerURL}  
  
```  
  
## <a name="step-10-optionally-configure-web-application-proxy-azure-ad-application-proxy-or-another-reverse-proxy"></a>Schritt 10: Konfigurieren des webanwendungsproxys, Azure AD Anwendungs Proxys oder einen anderen Reverseproxy  

Um Remote Benutzern den Zugriff auf Ihre Dateien zu ermöglichen, müssen Sie den Arbeitsordner Server über einen Reverseproxy veröffentlichen und die Arbeitsordner extern im Internet verfügbar machen. Sie können den webanwendungsproxy, Azure Active Directory-Anwendungsproxy oder eine andere Reverseproxylösung verwenden.  
  
Informationen zum Konfigurieren des Zugriffs auf Arbeitsordner mithilfe AD FS und webanwendungsproxys finden Sie unter Bereitstellen [von Arbeits Ordnern mit AD FS und webanwendungsproxy](deploy-work-folders-adfs-overview.md) Hintergrundinformationen zum webanwendungsproxy finden Sie unter [webanwendungsproxy in Windows Server 2016](../../remote/remote-access/web-application-proxy/web-application-proxy-windows-server.md). Ausführliche Informationen zum Veröffentlichen von Anwendungen wie z. b. Arbeits Ordnern im Internet mithilfe des webanwendungsproxys finden Sie unter [Veröffentlichen von Anwendungen mit AD FS Vorauthentifizierung](../../remote/remote-access/web-application-proxy/publishing-applications-using-ad-fs-preauthentication.md)
 
Informationen zum Konfigurieren des Zugriffs auf Arbeitsordner mithilfe von Azure Active Directory-Anwendungsproxy finden Sie unter [Aktivieren des Remote Zugriffs auf Arbeitsordner mithilfe Azure Active Directory-Anwendungsproxy](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) 
  
## <a name="step-11-optionally-use-group-policy-to-configure-domain-joined-pcs"></a>Schritt 11: Konfigurieren von in eine Domäne eingebundenen Computern mithilfe von Gruppenrichtlinien (optional)  

Wenn Sie für viele in eine Domäne eingebundene Computer Arbeitsordner bereitstellen möchten, können Sie die folgenden Konfigurationsaufgaben für Clientcomputer mithilfe von Gruppenrichtlinien durchführen:  
  
- Angeben der von Benutzern zu verwendenden Synchronisierungsserver  
  
- Erzwingen der automatischen Einrichtung von Arbeitsordnern anhand von Standardeinstellungen (lesen Sie vor dem Ausführen dieser Aufgabe die Informationen zu Gruppenrichtlinien im Thema [Entwerfen einer Arbeitsordnerimplementierung](plan-work-folders.md))  
  
  Erstellen Sie zum Steuern dieser Einstellungen ein neues Gruppenrichtlinienobjekt (Group Policy object, GPO) für Arbeitsordner, und konfigurieren Sie anschließend die folgenden Gruppenrichtlinieneinstellungen wie erforderlich:  
  
- Richtlinieneinstellung "Festlegen der Arbeitsordnereinstellungen" unter %%amp;quot;Benutzerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\WorkFolders%%amp;quot;  
  
- Richtlinien Einstellung "automatische Installation für alle Benutzer erzwingen" unter Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-komponents\workordner.  
  
> [!NOTE]
>  Diese Richtlinien Einstellungen sind nur verfügbar, wenn Sie Gruppenrichtlinie von einem Computer bearbeiten, auf dem Gruppenrichtlinie Management auf Windows 8.1, Windows Server 2012 R2 oder höher ausgeführt wird. In Versionen der Gruppenrichtlinienverwaltung von früheren Betriebssystemen sind diese Einstellungen nicht verfügbar. Diese Richtlinien Einstellungen gelten für Windows 7-PCs, auf denen die app " [Arbeitsordner für Windows 7](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) " installiert ist.  
  
##  <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch  
 Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:  
  
|Inhaltstyp|Referenzen|  
|------------------|----------------|  
|**Das Verstehen**|-   [Arbeitsordner](work-folders-overview.md)|  
|**Planung**|-   [Entwerfen einer Arbeitsordner Implementierung](plan-work-folders.md)|
|**Bereitstellung**|-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy (WAP)](deploy-work-folders-adfs-overview.md)<br />-   [Test Umgebungs Bereitstellung für Arbeitsordner](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (Blogbeitrag)<br />-   [Ein neues Benutzer Attribut für die Arbeitsordner Server-URL](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (Blogbeitrag)|  
|**Technische Referenz**|-   [Interaktive Anmeldung: Schwellenwert für Computer Kontosperrung](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj966264(v=ws.11))<br />-   [Synchronisierungs Freigabe-Cmdlets](/powershell/module/syncshare/?view=win10-ps)|
