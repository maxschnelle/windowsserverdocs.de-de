---
title: Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy - Schritt 3, Einrichten von Arbeitsordnern
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: 5a43b104-4d02-4d73-a385-da1cfb67e341
ms.openlocfilehash: 81f30a7a4d50423a68719343fec3032cc6a1602e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854711"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-3-set-up-work-folders"></a>Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 3: Einrichten von Arbeitsordnern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird der dritte Schritt bei der Bereitstellung von Arbeitsordnern mit Active Directory-Verbunddiensten (AD FS) und Webproxyanwendung beschrieben. Weitere Schritte des Prozesses finden Sie in folgenden Themen:  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Übersicht über die](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 1: Einrichten der AD FS](deploy-work-folders-adfs-step1.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 2, und AD FS-Konfiguration nach der Arbeit](deploy-work-folders-adfs-step2.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 4: Einrichten des Webanwendungsproxys](deploy-work-folders-adfs-step4.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 5, richten Sie Clients](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
>   Die in diesem Abschnitt enthaltenen Anweisungen gelten für eine Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, folgen Sie den [Anweisungen für Windows Server 2012 R2](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx).

Wenn Sie Arbeitsordner einrichten möchten, gehen Sie folgendermaßen vor.  
  
## <a name="pre-installment-work"></a>Installations\-vorbereitung  
Um Arbeitsordner zu installieren, müssen Sie über einen Server verfügen, der mit der Domäne verbunden ist und auf dem Windows Server 2016 ausgeführt wird. Der Server muss über eine gültige Netzwerkkonfiguration verfügen.  
  
Verknüpfen Sie für das Testbeispiel den Computer, auf dem der Arbeitsordner ist mit der Contoso-Domäne und richten Sie die Netzwerkschnittstelle wie in den folgenden Abschnitten beschrieben ein. 

### <a name="set-the-server-ip-address"></a>Legen Sie die IP-Adresse des -Servers fest  
Ändern Sie die IP-Adresse des Servers in eine statische IP-Adresse. Verwenden Sie für das Testbeispiel-IP-Klasse ein, die 192.168.0.170 / Subnetzmaske: 255.255.0.0 / Standard-Gateway: 192.168.0.1 / bevorzugte DNS: 192.168.0.150 (die IP-Adresse des Domänencontrollers). 
  
### <a name="create-the-cname-record-for-work-folders"></a>Erstellen Sie den CNAME-Eintrag für Arbeitsordner  
Um den CNAME-Eintrag für Arbeitsordner zu erstellen, gehen Sie folgendermaßen vor:  
  
1.  Öffnen Sie auf dem Domänencontroller den **DNS-Manager**.  
  
2.  Erweitern Sie den Forward-Lookupzonen-Ordner, klicken Sie mit der rechten Maustaste auf die Domäne und wählen Sie **Neuer Alias (CNAME)** aus.  
  
3.  Geben Sie im Dialogfeld **Neuer Ressourcendatensatz** im Fenster **Aliasname** den Alias für Arbeitsordner ein. Im Testbeispiel ist dies **workfolders**.  
  
4.  Im Dialogfeld **Vollqualifizierter Domänenname** sollte der Wert **workfolders.contoso.com** sein.  
  
5.  Geben Sie im Dialogfeld **Vollqualifizierter Domänenname für Ziel-Host** den vollqualifizierten Domänennamen für den Arbeitsordner ein. Im Testbeispiel ist dies **2016-WF.contoso.com**.  
  
6.  Klicken Sie auf **OK**.  
  
Verwenden Sie den folgenden Befehl, um die entsprechenden Schritte mit Windows PowerShell durchzuführen. Der Befehl muss auf dem Domänencontroller ausgeführt werden.  
  
```powershell  
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name workfolders -CName  -HostNameAlias 2016-wf.contoso.com   
```  
  
### <a name="install-the-ad-fs-certificate"></a>Installieren Sie das AD FS-Zertifikat  
Installieren Sie anhand von folgenden Schritte das AD FS-Zertifikat, das im Zertifikatspeicher des lokalen Computers während der Installation von AD FS erstellt wurde:  
  
1.  Klicken Sie auf **Start** und dann auf **Ausführen**.  
  
2.  Geben Sie **MMC** ein.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Wählen Sie in der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und klicken Sie auf **Hinzufügen**. Der Zertifikate-Snap-In-Assistent wird gestartet.  
  
5.  Wählen Sie **Computerkonto** aus, und klicken Sie auf **Weiter**.  
  
6.  Wählen Sie **Lokaler Computer: (Computer, auf dem diese Konsole ausgeführt wird)** und klicken Sie auf **Finish**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Erweitern Sie den Ordner **Console Root\Certificates\(Local Computer)\Personal\Certificates**.  
  
9. Klicken Sie mit der rechten Maustaste auf **Zertifikate** und dann auf **Alle Aufgaben** und **Importieren**.  
  
10. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Zertifikatspeicher.

11. Erweitern Sie den Ordner **Console Root\Certificates\(Local Computer)\Trusted Root Certification Authorities\Certificates**.  
  
12. Klicken Sie mit der rechten Maustaste auf **Zertifikate** und dann auf **Alle Aufgaben** und **Importieren**.  
  
13. Wechseln Sie zu dem Ordner, der das AD FS-Zertifikat enthält, führen Sie die Schritte im Assistenten zum Importieren der Datei aus und platzieren Sie diese in den Vertrauenswürdige Stammzertifizierungsstellen-Speicher.  
  
### <a name="create-the-work-folders-self-signed-certificate"></a>Erstellen Sie das selbstsignierte Zertifikat für den Arbeitsordner  
Um das selbstsignierte Zertifikat für den Arbeitsordner zu erstellen, gehen Sie folgendermaßen vor:  
  
1.  Laden Sie die im Blogbeitrag [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy (WAP)](https://blogs.technet.microsoft.com/filecab/2014/03/03/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap) bereitgestellten Skripts herunter und kopieren Sie anschließend die Datei makecert.ps1 auf den Arbeitsordner-Computer.  
  
2.  Öffnen Sie ein Windows PowerShell-Fenster mit Administratorberechtigungen.  
  
3.  Legen Sie die -Ausführungsrichtlinie auf „unbeschränkt” fest.  
  
    ```powershell  
    PS C:\temp\scripts> Set-ExecutionPolicy -ExecutionPolicy Unrestricted   
    ```  
  
4.  Wechseln Sie zum Verzeichnis, in das Sie das Skript kopiert haben.  
  
5.  Führen Sie das Skript makecert aus:  
  
    ```powershell  
    PS C:\temp\scripts> .\makecert.ps1  
    ```  
  
6.  Wenn Sie aufgefordert werden, das Zertifikat des Antragstellers zu ändern, geben Sie den neuen Wert für den Antragssteller ein. In diesem Beispiel ist der Wert **workfolders.contoso.com**.  
  
7.  Wenn Sie aufgefordert werden, geben Sie die SAN-Namen ein, drücken Sie Y und geben Sie die einzelnen SAN-Namen ein.  
  
    Geben Sie in diesem Beispiel **workfolders.contoso.com** ein und drücken Sie die EINGABETASTE. Geben Sie anschließend **2016-WF.contoso.com** ein, und drücken Sie die EINGABETASTE.  
  
    Wenn Sie alle SAN-Namen eingegeben haben, drücken Sie auf einer leeren Zeile die EINGABETASTE.  
  
8.  Wenn Sie aufgefordert werden, die Zertifikate im Speicher für vertrauenswürdige Stammzertifizierungsstellen zu installieren, drücken Sie Y.  
  
Das Arbeitsordner-Zertifikat muss ein SAN-Zertifikat mit folgenden Werten sein:  
  
-   **workfolders**.**domain**  
  
-   **machine name**.**domain**  
  
Im Testbeispiel sind diese Werte wie folgt:  
  
-   **workfolders.contoso.com**  
  
-   **2016-WF.contoso.com**  
  
## <a name="install-work-folders"></a>Installieren von Arbeitsordnern  
Gehen Sie folgendermaßen vor, um die Arbeitsordnerrolle zu installieren:  
  
1.  Öffnen Sie **Server Manager**, und klicken Sie dann auf **Rollen und Features hinzufügen** und **Weiter**.  
  
2.  Wählen Sie auf der Seite **Installationsart** die Option **Rollenbasierte oder Featurebasierte Installation** aus, und klicken Sie anschließend auf **Weiter**.  
  
3.  Wählen Sie auf der Seite **Serverauswahl** den aktuellen Server aus und klicken Sie auf **Weiter**.  
  
4.  Erweitern Sie auf der Seite **Serverrollen** die Knoten **Datei- und Speicherdienste** und **Datei- und iSCSI-Dienste**, und wählen Sie dann **Arbeitsordner** aus.  
  
5.  Klicken Sie auf der Seite **Assistent zum Hinzufügen von Rollen und Features** auf **Features hinzufügen**, und klicken Sie auf **Weiter**.  
  
6.  Klicken Sie auf der Seite der **Features** auf **Weiter**.  
  
7.  Klicken Sie auf der Seite **Bestätigung** auf **Installieren**.  
  
## <a name="configure-work-folders"></a>Konfigurieren von Arbeitsordnern  
Gehen Sie folgendermaßen vor, um Arbeitsordner zu konfigurieren:  
  
1.  Öffnen Sie den **Server Manager**.  
  
2.  Wählen Sie **Datei- und Speicherdienste** und anschließend **Arbeitsordner** aus.  
  
3.  Auf der Seite **Arbeitsordner** starten Sie den **Assistent für neue Synchronisierungsfreigaben** und klicken Sie auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Server und Pfad** den Server aus, auf dem die Synchronisierung erstellt werden soll, geben Sie einen lokalen Pfad an, in dem die Arbeitsordner-Daten gespeichert werden, und klicken Sie auf **Weiter**.  
  
    Wenn der Pfad nicht vorhanden ist, werden Sie aufgefordert, ihn zu erstellen. Klicken Sie auf **OK**.  
  
5.  Wählen Sie auf der Seite **Ordnerstruktur** **Benutzeralias** aus und klicken Sie dann auf **Weiter**.  
  
6.  Geben Sie auf der Seite **Name der Synchronisierungsfreigabe** den Namen der Synchronisierungsfreigabe ein. Im Testbeispiel ist dies **WorkFolders**. Klicken Sie auf **Weiter**.  
  
7.  Fügen Sie auf der Seite **Synchronisierungszugriff** die Benutzer oder Gruppen hinzu, die auf die neue Synchronisierung Zugriff haben. Gewähren Sie für dieses Testbeispiel allen Domänenbenutzer Zugriff. Klicken Sie auf **Weiter**.  
  
8.  Wählen Sie auf der Seite **PC-Sicherheitsrichtlinien** **Arbeitsordner verschlüsseln** und **Bildschirm automatisch sperren und ein Kennwort anfordern** aus. Klicken Sie auf **Weiter**.  
  
9. Klicken Sie auf der Seite **Bestätigung** auf **Erstellen**, um den Konfigurationsprozess abzuschließen.  
  
## <a name="work-folders-post-configuration-work"></a>Nach der Konfiguration von Arbeitsordnern auszuführende Aufgaben  
Führen Sie diese zusätzlichen Schritte aus, um das Einrichten der Arbeitsordner abzuschließen:  
  
-   Das Arbeitsordner-Zertifikat an den SSL-Port binden  
  
-   Arbeitsordner zum Verwenden von AD FS-Authentifizierungen konfigurieren  
  
-   Das Arbeitsordner-Zertifikat exportieren (wenn Sie ein selbstsigniertes Zertifikat verwenden)  
  
### <a name="bind-the-certificate"></a>Das Zertifikat binden  
Arbeitsordner kommunizieren nur über SSLs und müssen das an den Port gebundene selbstsignierte Zertifikat besitzen, das Sie zuvor erstellt haben (oder das von der Zertifizierungsstelle ausgestellt wurde).  
  
Es gibt zwei Methoden, die Sie zum Binden des Zertifikats an den Port, über Windows PowerShell verwenden können: IIS-Cmdlets "und" Netsh ".  
  
#### <a name="bind-the-certificate-by-using-netsh"></a>Das Zertifikat mithilfe von Netsh binden  
Um das Befehlszeilen-Skripthilfsprogramm Netsh in Windows PowerShell zu verwenden, müssen Sie den Befehl auf Netsh umleiten. Das folgende Beispielskript findet das Zertifikat mit dem Betreff **workfolders.contoso.com** und bindet es an den Port 443 mit Netsh:  
  
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
  
#### <a name="bind-the-certificate-by-using-iis-cmdlets"></a>Das Zertifikat mithilfe von IIS-Cmdlets binden  
Sie können das Zertifikat auch mithilfe von IIS-Management-Cmdlets an den Port binden, die verfügbar sind, wenn Sie IIS-Verwaltungstools und Skripts installiert haben.  
  
> [!NOTE]  
> Die Installation der IIS-Verwaltungstools aktiviert nicht die Vollversion von IIS auf dem Arbeitsordner-Computer, sondern nur die Management-Cmdlets. Diese Art der Installation hat einige Vorteile. Wenn Sie beispielsweise Cmdlets benötigen, die die Funktionen bereitstellen, die Sie von Netsh erhalten. Wenn das Zertifikat über das Cmdlet New-WebBinding an den Port gebunden wird, ist die Bindung nicht von IIS abhängig. Nachdem Sie die Bindung durchgeführt haben, können Sie das Web-Management-Konsole Feature entfernen und das Zertifikat bleibt trotzdem an den Port gebunden. Sie können die Bindung über Netsh durch die Eingabe **netsh http show sslcert** überprüfen.  
  
Im folgenden Beispiel wird das Cmdlet New-WebBinding verwendet, um das Zertifikat mit dem Betreff **workfolders.contoso.com** zu finden und an den Port 443 zu binden:  
  
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
  
### <a name="set-up-ad-fs-authentication"></a>Einrichten der AD FS-Authentifizierung  
Gehen Sie folgendermaßen vor, um Arbeitsordner zum Verwenden von AD FS zur Authentifizierung zu konfigurieren:  
  
1.  Öffnen Sie den **Server Manager**.  
  
2.  Klicken Sie auf **Server** und wählen Sie dann Ihre Arbeitsordner-Server aus der Liste aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Servernamen und klicken Sie anschließend auf **Arbeitsordnereinstellungen**.  
  
4.  Wählen Sie im Dialogfenster **Arbeitsordnereinstellungen** **Active Directory-Verbunddienste** und geben Sie eine Verbunddienst-URL ein. Klicken Sie auf **Übernehmen**.  
  
    Im Testbeispiel die URL ist **https://blueadfs.contoso.com**.  
  
So führen Sie dieselbe Aufgabe mit Windows PowerShell-Cmdlet aus:  
  
```powershell  
Set-SyncServerSetting -ADFSUrl "https://blueadfs.contoso.com"   
```  
  
Wenn Sie AD FS mit selbstsignierten Zertifikaten einrichten, wird möglicherweise eine Fehlermeldung angezeigt, dass die Verbunddienst-URL nicht korrekt oder nicht erreichbar ist oder keine Vertrauensstellung der vertrauenden Seite eingerichtet ist.  
  
Dieser Fehler kann auch auftreten, wenn das AD FS-Zertifikat auf dem Arbeitsordner-Server installiert oder der CNAME-Eintrag für AD FS nicht korrekt festgelegt wurde. Sie müssen diese Probleme beheben, bevor Sie fortfahren können.  
  
### <a name="export-the-work-folders-certificate"></a>Das Zertifikat Arbeitsordner exportieren  
Das selbstsigniertes Arbeitsordner-Zertifikat muss exportiert werden, damit Sie es später auf den folgenden Computern in der Testumgebung installieren können:  
  
-   Der Server, der für die Webanwendungsproxy verwendet wird  
  
-   Der mit einer Domäne verknüpfte Windows-Client  
  
-   Der nicht mit einer Domäne verknüpfte Windows-Client  
  
Um das Zertifikat zu exportieren, führen Sie die gleichen Schritte, die Sie zum zuvor exportieren Sie das AD FS-Zertifikat verwendet, wie in beschrieben [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 2, und AD FS-Konfiguration nach der Arbeit](deploy-work-folders-adfs-step2.md), exportieren Sie das AD FS-Zertifikat.  
  
Nächster Schritt: [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 4: Einrichten des Webanwendungsproxys](deploy-work-folders-adfs-step4.md)  
  
## <a name="see-also"></a>Siehe auch  
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)  
  

