---
title: 'Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy-Schritt 3: Einrichten von Arbeits Ordnern'
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: 5a43b104-4d02-4d73-a385-da1cfb67e341
ms.openlocfilehash: 433d981d558cc49cd860a5c05a8d76996d9cdd30
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965742"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-3-set-up-work-folders"></a>Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird der dritte Schritt beim Bereitstellen von Arbeits Ordnern mit Active Directory-Verbunddienste (AD FS) (AD FS) und dem webanwendungsproxy beschrieben. Die anderen Schritte in diesem Prozess finden Sie in den folgenden Themen:  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 1, einrichten AD FS](deploy-work-folders-adfs-step1.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy: Schritt 2 AD FS arbeiten nach der Konfiguration](deploy-work-folders-adfs-step2.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 4](deploy-work-folders-adfs-step4.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
>   Die in diesem Abschnitt behandelten Anweisungen gelten für eine Windows Server 2019-oder Windows Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, befolgen Sie die [Anweisungen unter Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn747208(v=ws.11)).

Verwenden Sie zum Einrichten von Arbeits Ordnern die folgenden Prozeduren.  
  
## <a name="pre-installment-work"></a>Arbeit vor der \- Ausgabe  
Um Arbeitsordner zu installieren, müssen Sie über einen Server verfügen, der der Domäne hinzugefügt wird und Windows Server 2016 ausgeführt wird. Der Server muss über eine gültige Netzwerkkonfiguration verfügen.  
  
Fügen Sie für das Testbeispiel den Computer, auf dem Arbeitsordner ausgeführt werden, der Domäne von "Domäne" hinzu, und richten Sie die Netzwerkschnittstelle wie in den folgenden Abschnitten beschrieben ein. 

### <a name="set-the-server-ip-address"></a>Festlegen der Server-IP-Adresse  
Ändern Sie die IP-Adresse Ihres Servers in eine statische IP-Adresse. Verwenden Sie für das Testbeispiel IP Class A, d. h. 192.168.0.170/Subnetzmaske: 255.255.0.0/Default Gateway: 192.168.0.1/bevorzugtes DNS: 192.168.0.150 (die IP-Adresse Ihres Domänen Controllers). 
  
### <a name="create-the-cname-record-for-work-folders"></a>Erstellen des CNAME-Datensatzes für Arbeitsordner  
Führen Sie die folgenden Schritte aus, um den CNAME-Datensatz für Arbeitsordner zu erstellen:  
  
1.  Öffnen Sie auf dem Domänen Controller den **DNS-Manager**.  
  
2.  Erweitern Sie den Ordner Forward-Lookupzonen, klicken Sie mit der rechten Maustaste auf Ihre Domäne, und klicken Sie dann auf **Neuer Alias (CNAME)**.  
  
3.  Geben Sie im Fenster **neues Ressourcen Daten Satz** im Feld **Alias Name** den Alias für Arbeitsordner ein. Im Testbeispiel handelt es sich hierbei um **Arbeitsordner**.  
  
4.  Im Feld **voll qualifizierter Domänen Name** sollte der Wert **workfolders.contoso.com**lauten.  
  
5.  Geben Sie im Feld **voll qualifizierter Domänen Name für Zielhost den voll qualifizierten Domänen Namen** (FQDN) für den Arbeitsordner Server ein. Im Beispiel Test ist dies **2016-WF.contoso.com**.  
  
6.  Klicken Sie auf **OK**.  
  
Wenn Sie die entsprechenden Schritte über Windows PowerShell ausführen möchten, verwenden Sie den folgenden Befehl. Der Befehl muss auf dem Domänen Controller ausgeführt werden.  
  
```powershell  
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name workfolders -CName  -HostNameAlias 2016-wf.contoso.com   
```  
  
### <a name="install-the-ad-fs-certificate"></a>Installieren des AD FS Zertifikats  
Installieren Sie das AD FS Zertifikat, das während der AD FS Einrichtung erstellt wurde, in den Zertifikat Speicher des lokalen Computers, indem Sie die folgenden Schritte ausführen:  
  
1.  Klicken Sie im **Startmenü**auf **Ausführen**.  
  
2.  Geben Sie **MMC**ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**. Der Zertifikat-Snap-in-Assistent wird gestartet.  
  
5.  Wählen Sie **Computerkonto** aus, und klicken Sie dann auf **Weiter**.  
  
6.  Wählen Sie **lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird) aus**, und klicken Sie dann auf **Fertig**stellen.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Erweitern Sie die Ordner **Konsole root\zertifikate \( lokaler Computer) \personal\zertifikate**.  
  
9. Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **importieren**.  
  
10. Navigieren Sie zu dem Ordner, der das AD FS Zertifikat enthält, und befolgen Sie die Anweisungen im Assistenten, um die Datei zu importieren und im Zertifikat Speicher zu platzieren.

11. Erweitern Sie die Ordner **Konsole root\zertifikate \( lokaler Computer) \trusted Root Certification autorities\zertifikate**.  
  
12. Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **importieren**.  
  
13. Navigieren Sie zu dem Ordner, der das AD FS Zertifikat enthält, und befolgen Sie die Anweisungen im Assistenten, um die Datei zu importieren und im Speicher Vertrauenswürdige Stamm Zertifizierungsstellen zu platzieren.  
  
### <a name="create-the-work-folders-self-signed-certificate"></a>Erstellen des selbst signierten Zertifikats für Arbeitsordner  
Führen Sie die folgenden Schritte aus, um das selbst signierte Zertifikat für Arbeitsordner zu erstellen:  
  
1.  Laden Sie die Skripts im Blogbeitrag bereitstellen [von Arbeits Ordnern mit AD FS und webanwendungsproxy](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap/ba-p/425318) herunter, und kopieren Sie die Datei makecert.ps1 auf den Arbeitsordner Computer.  
  
2.  Öffnen Sie ein Windows PowerShell-Fenster mit Administratorrechten.  
  
3.  Legen Sie die Ausführungs Richtlinie auf "uneingeschränkt" fest:  
  
    ```powershell  
    PS C:\temp\scripts> Set-ExecutionPolicy -ExecutionPolicy Unrestricted   
    ```  
  
4.  Wechseln Sie in das Verzeichnis, in das Sie das Skript kopiert haben.  
  
5.  Führen Sie das MakeCert-Skript aus:  
  
    ```powershell  
    PS C:\temp\scripts> .\makecert.ps1  
    ```  
  
6.  Wenn Sie aufgefordert werden, das Zertifikat des Antragstellers zu ändern, geben Sie den neuen Wert für das Thema ein. In diesem Beispiel ist der Wert **workfolders.contoso.com**.  
  
7.  Wenn Sie aufgefordert werden, die Namen von alternativen Antragsteller Namen (Subject Alternative Name, San) einzugeben, drücken Sie Y, und geben Sie dann nacheinander die San-Namen ein.  
  
    Geben Sie für dieses Beispiel **workfolders.contoso.com**ein, und drücken Sie die EINGABETASTE. Geben Sie **2016-WF.contoso.com** ein, und drücken Sie die EINGABETASTE.  
  
    Wenn alle San-Namen eingegeben wurden, drücken Sie in einer leeren Zeile die EINGABETASTE.  
  
8.  Wenn Sie aufgefordert werden, die Zertifikate im Speicher der vertrauenswürdigen Stamm Zertifizierungsstelle zu installieren, drücken Sie Y.  
  
Beim Zertifikat für Arbeitsordner muss es sich um ein San-Zertifikat mit den folgenden Werten handeln:  
  
-   **Arbeitsordner**. **Domäne**  
  
-   **Computername**. **Domäne**  
  
Im Testbeispiel lauten die Werte wie folgt:  
  
-   **workfolders.contoso.com**  
  
-   **2016-WF.contoso.com**  
  
## <a name="install-work-folders"></a>Installieren von Arbeits Ordnern  
Um die Arbeitsordner Rolle zu installieren, führen Sie die folgenden Schritte aus:  
  
1.  Öffnen Sie **Server-Manager**, klicken Sie auf **Rollen und Features hinzufügen**, und klicken Sie auf **weiter**.  
  
2.  Wählen Sie auf der Seite **Installationstyp** die Option **rollenbasierte oder featurebasierte Installation**aus, und klicken Sie auf **weiter**.  
  
3.  Wählen Sie auf der Seite **Server Auswahl** den aktuellen Server aus, und klicken Sie auf **weiter**.  
  
4.  Erweitern Sie auf der Seite **Server Rollen** den Knoten **Datei-und Speicherdienste**, erweitern Sie **Datei-und iSCSI-Dienste**, und wählen Sie dann **Arbeitsordner**aus.  
  
5.  Klicken Sie auf der Seite **Assistent zum Hinzufügen von Rollen und Features** auf **Features hinzufügen**, und klicken Sie auf **weiter**.  
  
6.  Klicken Sie auf der Seite **Features** auf **weiter**.  
  
7.  Klicken Sie auf der Seite **Bestätigung** auf **Installieren**.  
  
## <a name="configure-work-folders"></a>Konfigurieren von Arbeitsordnern  
Um Arbeitsordner zu konfigurieren, führen Sie die folgenden Schritte aus:  
  
1.  Öffnen Sie **Server-Manager**.  
  
2.  Wählen Sie **Datei-und Speicherdienste**aus, und wählen Sie dann **Arbeitsordner**aus.  
  
3.  Starten Sie auf der Seite **Arbeitsordner** den **Assistenten für neue Synchronisierungs**Freigaben, und klicken Sie auf **weiter**.  
  
4.  Wählen Sie auf der Seite **Server und Pfad** den Server aus, auf dem die Synchronisierungs Freigabe erstellt werden soll, geben Sie einen lokalen Pfad ein, in dem die Arbeitsordner Daten gespeichert werden sollen, und klicken Sie auf **weiter**.  
  
    Wenn der Pfad nicht vorhanden ist, werden Sie aufgefordert, ihn zu erstellen. Klicken Sie auf **OK**.  
  
5.  Wählen Sie auf der Seite **Benutzerordner Struktur** die Option **Benutzeralias**aus, und klicken Sie dann auf **weiter**.  
  
6.  Geben Sie auf der Seite **Name der Synchronisierungs Freigabe** den Namen für die Synchronisierungs Freigabe ein. Für das Testbeispiel handelt es sich hierbei um **Arbeitsordner**. Klicken Sie auf **Weiter**.  
  
7.  Fügen Sie auf der Seite **Synchronisierungs Zugriff** die Benutzer oder Gruppen hinzu, die Zugriff auf die neue Synchronisierungs Freigabe haben werden. Gewähren Sie für das Testbeispiel allen Domänen Benutzern Zugriff. Klicken Sie auf **Weiter**.  
  
8.  Wählen Sie auf der Seite **PC-Sicherheitsrichtlinien** die Option **Arbeitsordner verschlüsseln** und **Seite automatisch sperren aus, und fordern Sie ein Kennwort**an. Klicken Sie auf **Weiter**.  
  
9. Klicken Sie auf der **Bestätigungs** Seite auf **Erstellen** , um den Konfigurationsprozess abzuschließen.  
  
## <a name="work-folders-post-configuration-work"></a>Arbeitsordner nach der Konfiguration  
Führen Sie die folgenden zusätzlichen Schritte aus, um die Einrichtung von Arbeits Ordnern abzuschließen:  
  
-   Binden des Arbeitsordner Zertifikats an den SSL-Port  
  
-   Konfigurieren von Arbeits Ordnern für die Verwendung AD FS Authentifizierung  
  
-   Exportieren des Arbeitsordner Zertifikats (bei Verwendung eines selbst signierten Zertifikats)  
  
### <a name="bind-the-certificate"></a>Binden des Zertifikats  
Arbeitsordner kommunizieren nur über SSL und benötigen das selbst signierte Zertifikat, das Sie zuvor erstellt haben (oder das von der Zertifizierungsstelle ausgestellt wurde), das an den Port gebunden ist.  
  
Es gibt zwei Methoden, mit denen Sie das Zertifikat über Windows PowerShell an den Port binden können: IIS-Cmdlets und Netsh.  
  
#### <a name="bind-the-certificate-by-using-netsh"></a>Binden des Zertifikats mithilfe von Netsh  
Um das Befehlszeilen-Skript Hilfsprogramm Netsh in Windows PowerShell zu verwenden, müssen Sie den Befehl an netsh übergeben. Im folgenden Beispielskript wird das Zertifikat mit dem Betreff **workfolders.contoso.com** gefunden und mithilfe von netsh an Port 443 gebunden:  
  
```powershell  
$subject = "workfolders.contoso.com"   
Try  
{  
#In case there are multiple certificates with the same subject, get the latest version   
$cert = Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match $subject} | sort $_.NotAfter -Descending | select -first 1    
$thumbprint = $cert.Thumbprint  
$Command = "http add sslcert ipport=0.0.0.0:443 certhash=$thumbprint appid={CE66697B-3AA0-49D1-BDBD-A25C8359FD5D} certstorename=MY"  
$Command | netsh  
}  
Catch  
{  
"     Error: unable to locate certificate for $($subject)"  
Exit  
}   
```  
  
#### <a name="bind-the-certificate-by-using-iis-cmdlets"></a>Binden des Zertifikats mithilfe von IIS-Cmdlets  
Sie können das Zertifikat auch mit den IIS-Verwaltungs-Cmdlets an den Port binden, die verfügbar sind, wenn Sie die IIS-Verwaltungs Tools und-Skripts installiert haben.  
  
> [!NOTE]  
> Die Installation der IIS-Verwaltungs Tools ermöglicht nicht die vollständige Version von Internetinformationsdienste (IIS) auf dem Arbeitsordner Computer. Es werden nur die-Verwaltungs-Cmdlets aktiviert. Dieses Setup kann einige Vorteile haben. Wenn Sie z. b. nach Cmdlets suchen, um die Funktionalität bereitzustellen, die Sie von Netsh erhalten. Wenn das Zertifikat über das Cmdlet New-webbinding an den Port gebunden ist, ist die Bindung in keiner Weise von IIS abhängig. Nachdem Sie die Bindung erstellt haben, können Sie sogar das Feature "Web-Mgmt-Console" entfernen, und das Zertifikat wird weiterhin an den Port gebunden. Sie können die Bindung über Netsh überprüfen, indem Sie **netsh http Show sslcert**eingeben.  
  
Im folgenden Beispiel wird das Cmdlet New-webbinding verwendet, um das Zertifikat mit dem Betreff **workfolders.contoso.com** zu suchen und an Port 443 zu binden:  
  
```powershell  
$subject = "workfolders.contoso.com"  
Try  
{  
#In case there are multiple certificates with the same subject, get the latest version   
$cert =Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match $subject } | sort $_.NotAfter -Descending | select -first 1   
$thumbprint = $cert.Thumbprint  
New-WebBinding -Name "Default Web Site" -IP * -Port 443 -Protocol https  
#The default IIS website name must be used for the binding. Because Work Folders uses Hostable Web Core and its own configuration file, its website name, 'ECSsite', will not work with the cmdlet. The workaround is to use the default IIS website name, even though IIS is not enabled, because the NewWebBinding cmdlet looks for a site in the default IIS configuration file.   
Push-Location IIS:\SslBindings  
Get-Item cert:\LocalMachine\MY\$thumbprint | new-item *!443  
Pop-Location  
}  
Catch  
{  
"     Error: unable to locate certificate for $($subject)"  
Exit  
}   
```  
  
### <a name="set-up-ad-fs-authentication"></a>Einrichten AD FS Authentifizierung  
Führen Sie die folgenden Schritte aus, um Arbeitsordner für die Verwendung von AD FS zur Authentifizierung zu konfigurieren:  
  
1.  Öffnen Sie **Server-Manager**.  
  
2.  Klicken Sie auf **Server**, und wählen Sie dann Ihren Arbeitsordner Server in der Liste aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Servernamen, und klicken Sie auf **Arbeitsordner Einstellungen**.  
  
4.  Wählen Sie im Fenster **Einstellungen für Arbeitsordner** die Option **Active Directory-Verbunddienste (AD FS)** aus, und geben Sie die Verbunddienst-URL ein. Klicken Sie auf **Anwenden**.  
  
    Im Testbeispiel lautet die URL **https://blueadfs.contoso.com** .  
  
Das Cmdlet zum Ausführen derselben Aufgabe über Windows PowerShell lautet wie folgt:  
  
```powershell  
Set-SyncServerSetting -ADFSUrl "https://blueadfs.contoso.com"   
```  
  
Wenn Sie AD FS mit selbst signierten Zertifikaten einrichten, erhalten Sie möglicherweise eine Fehlermeldung, die besagt, dass die Verbunddienst-URL falsch, nicht erreichbar oder eine Vertrauensstellung der vertrauenden Seite nicht eingerichtet wurde.  
  
Dieser Fehler kann auch auftreten, wenn das AD FS Zertifikat nicht auf dem Arbeitsordner Server installiert wurde oder wenn der CNAME für AD FS nicht ordnungsgemäß eingerichtet wurde. Sie müssen diese Probleme beheben, bevor Sie fortfahren.  
  
### <a name="export-the-work-folders-certificate"></a>Exportieren des Arbeitsordner Zertifikats  
Das selbst signierte Arbeitsordner Zertifikat muss exportiert werden, damit Sie es später auf den folgenden Computern in der Testumgebung installieren können:  
  
-   Der Server, der für den webanwendungsproxy verwendet wird  
  
-   Der in die Domäne eingebundener Windows-Client  
  
-   Der nicht in die Domäne eingebundenen Windows-Client  
  
Um das Zertifikat zu exportieren, führen Sie die Schritte aus, die Sie zuvor zum Exportieren des AD FS Zertifikats verwendet haben, wie unter Bereitstellen [von Arbeits Ordnern mit AD FS und webanwendungsproxy beschrieben: Schritt 2, AD FS nach der Konfiguration](deploy-work-folders-adfs-step2.md), Exportieren des AD FS Zertifikats.  
  
Nächster Schritt: [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 4](deploy-work-folders-adfs-step4.md)  
  
## <a name="see-also"></a>Weitere Informationen  
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)  
  
