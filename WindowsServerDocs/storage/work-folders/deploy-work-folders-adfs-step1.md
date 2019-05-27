---
title: Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy -Schritt 1, Einrichten von AD FS
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 10/18/2018
ms.assetid: 938cdda2-f17e-4964-9218-f5868fd96735
ms.openlocfilehash: a26b784c18049ee473a191abc7bfa0a5d253d15e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883031"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-1-set-up-ad-fs"></a>Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 1: Einrichten von AD FS

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird der erste Schritt bei der Bereitstellung von Arbeitsordnern mit Active Directory-Verbunddiensten (AD FS) und Webanwendungsproxy beschrieben. Weitere Schritte des Prozesses finden Sie in folgenden Themen:  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Übersicht über die](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 2, und AD FS-Konfiguration nach der Arbeit](deploy-work-folders-adfs-step2.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 3, Einrichten von Arbeitsordnern](deploy-work-folders-adfs-step3.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 4: Einrichten des Webanwendungsproxys](deploy-work-folders-adfs-step4.md)  
  
-   [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 5, richten Sie Clients](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
>   Die in diesem Abschnitt enthaltenen Anweisungen gelten für eine Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, folgen Sie den [Anweisungen für Windows Server 2012 R2](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx).

Gehen Sie folgendermaßen vor, um AD FS für die Verwendung mit Arbeitsordnern einzurichten.  
  
## <a name="pre-installment-work"></a>Installations\-vorbereitung  
Wenn Sie die in dieser Anweisung erstellte Testumgebung für die Produktion einrichten möchten, sollten Sie vor Beginn zwei Dinge durchführen:  
  
-   Richten Sie ein Active Directory-Domänenadministratorkonto ein, auf dem Sie die AD FS-Dienste ausführen.
  
-   Erhalten Sie ein SSL-SAN-Zertifikat für die Authentifizierung des Servers. Verwenden Sie ein öffentlich vertrauenswürdiges Zertifikat für das Testbeispiel und ein selbstsigniertes Zertifikat für die Produktion.  
  
Das Abrufen dieser Elemente kann je nach Richtlinien Ihres Unternehmens einige Zeit dauern. Daher sollten Sie den Anforderungsprozess für diese Elemente vor dem Erstellen der Testumgebung einleiten.  
  
Es gibt viele kommerziellen Zertifizierungsstellen (CAs), von denen Sie das Zertifikat erwerben können. Sie können unter [Knowledge Base-Artikel 931125](https://support.microsoft.com/kb/931125) ebenfalls eine Liste der Zertifizierungsstellen erhalten, denen Microsoft vertraut. Alternativ können Sie ein Zertifikat von der Zertifizierungsstelle Ihres Unternehmens erhalten.  
  
Verwenden Sie für die Testumgebung ein selbstsigniertes Zertifikat, das von einem bereitgestellten Skript erstellt wird.  
  
> [!NOTE]  
> AD FS unterstützt keine Cryptography Next Generation (CNG)-Zertifikate, d. h. Sie können nicht mithilfe des Windows PowerShell-Cmdlets „New-SelfSignedCertificate” selbstsignierte Zertifikat erstellen. Sie können allerdings das Skript „makecert.ps1” verwenden, das im Blogpost [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy (WAP)](https://blogs.technet.microsoft.com/filecab/2014/03/03/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap) enthalten ist. Dieses Skript erstellt ein selbst\-signiertes Zertifikat, das mit AD FS und Anweisungen für die SAN-Namen funktioniert, die zur Erstellung der Zertifikate benötigt werden.  
  
Führen Sie dann die in den folgenden Abschnitten beschriebenen Installationsvorbereitungen aus.  
  
### <a name="create-an-ad-fs-self-signed-certificate"></a>Erstellen eines AD FS-selbst\-signiertes Zertifikats  
Um ein selbstsigniertes AD FS-Zertifikat zu erstellen, gehen Sie folgendermaßen vor:  
  
1.  Laden Sie die im Blogbeitrag [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy (WAP)](https://blogs.technet.microsoft.com/filecab/2014/03/03/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap) bereitgestellten Skripts herunter und kopieren Sie anschließend die Datei makecert.ps1 auf den AD FS-Computer.  
  
2.  Öffnen Sie ein Windows PowerShell-Fenster mit Administratorberechtigungen.  
  
3.  Legen Sie die -Ausführungsrichtlinie auf „unbeschränkt” fest.  
  
    ```powershell  
    Set-ExecutionPolicy –ExecutionPolicy Unrestricted   
    ```  
  
4.  Wechseln Sie zum Verzeichnis, in das Sie das Skript kopiert haben.  
  
5.  Führen Sie das Skript makecert aus:  
  
    ```powershell  
    .\makecert.ps1  
    ```  
  
6.  Wenn Sie aufgefordert werden, das Zertifikat des Antragstellers zu ändern, geben Sie den neuen Wert für den Antragssteller ein. In diesem Beispiel ist der Wert **blueadfs.contoso.com**.  
  
7.  Wenn Sie aufgefordert werden, geben Sie die SAN-Namen ein, drücken Sie Y und geben Sie die einzelnen SAN-Namen ein.  
  
    Geben Sie in diesem Beispiel **blueadfs.contoso.com** ein und drücken Sie die EINGABETASTE. Geben Sie anschließend **2016-adfs.contoso.com** ein und drücken Sie die EINGABETASTE. Geben Sie anschließend **enterpriseregistration.contoso.com** ein und drücken Sie die EINGABETASTE.  
  
    Wenn Sie alle SAN-Namen eingegeben haben, drücken Sie auf einer leeren Zeile die EINGABETASTE.  
  
8.  Wenn Sie aufgefordert werden, die Zertifikate im Speicher für vertrauenswürdige Stammzertifizierungsstellen zu installieren, drücken Sie Y.  
  
Das AD FS-Zertifikat muss ein SAN-Zertifikat mit folgenden Werten sein:  

-   AD FS service name.domain

-   enterpriseregistration.domain

-   AD FS server name.domain

Im Testbeispiel sind diese Werte wie folgt:  
  
-   **blueadfs.contoso.com**
  
-   **enterpriseregistration.contoso.com**
  
-   **2016-adfs.contoso.com**
  
Der „Enterpriseregistration”-SAN ist für Workplace Join erforderlich.  
  
### <a name="set-the-server-ip-address"></a>Legen Sie die IP-Adresse des -Servers fest  
Ändern Sie die IP-Adresse des Servers in eine statische IP-Adresse. Verwenden Sie für das Testbeispiel-IP-Klasse ein, die 192.168.0.160 / Subnetzmaske: 255.255.0.0 / Standard-Gateway: 192.168.0.1 / bevorzugte DNS: 192.168.0.150 (die IP-Adresse des Domänencontrollers\).  
  
## <a name="install-the-ad-fs-role-service"></a>Installieren des AD FS-Rollendiensts  
Führen Sie folgende Schritte aus, um AD FS zu installieren:  
  
1.  Melden Sie sich auf dem physischen oder virtuellen Computer an, auf dem Sie AD FS installieren möchten, öffnen Sie **Server Manager** und starten Sie den Assistenten zum Hinzufügen von Rollen und Features.  
  
2.  Klicken Sie auf der Seite **Serverrollen** auf die Rolle **Active Directory-Verbunddienste (AD FS)** und klicken Sie dann auf **Weiter**.  
  
3.  Auf der Seite **Active Directory-Verbunddienste (AD FS)** erscheint eine Meldung, dass die Webanwendungsproxy-Rolle nicht auf demselben Computer wie AD FS installiert werden kann. Klicken Sie auf **Weiter**.  
  
4.  Klicken Sie auf der Seite „Bestätigung” auf **Installieren**.  
  
Um die entsprechende Installation von AD FS über Windows PowerShell auszuführen, geben Sie diese Befehle ein:  
  
```powershell  
Add-WindowsFeature RSAT-AD-Tools  
Add-WindowsFeature ADFS-Federation –IncludeManagementTools  
```  
  
## <a name="configure-ad-fs"></a>Konfigurieren von AD FS  
Konfigurieren Sie anschließend AD FS mithilfe von Server Manager oder Windows PowerShell.  
  
### <a name="configure-ad-fs-by-using-server-manager"></a>Konfigurieren von AD FS mit Server Manager  
Gehen Sie folgendermaßen vor, um AD FS mit Server-Manager zu konfigurieren:  
  
1.  Öffnen Sie den Server-Manager.  
  
2.  Klicken Sie auf das Kennzeichen **Benachrichtigungen** oben im Server Manager-Fenster und anschließend auf **Verbunddienst auf den Server konfigurieren**.  
  
3.  Der Konfigurations-Assistent für Active Directory-Verbunddienste (AD FS) wird geöffnet. Geben Sie auf der Seite **Mit AD DS verbinden** das Domänenadministratorkonto ein, das Sie verwenden als AD FS-Konto verwenden möchten und klicken Sie auf **Weiter**.  
  
4.  Geben Sie auf der Seite **Diensteigenschaften angeben** den Antragstellernamen des SSL-Zertifikats für die AD FS-Kommunikation ein. In diesem Testbeispiel ist der Wert **blueadfs.contoso.com**.  
  
5.  Geben Sie den Verbunddienstnamen ein. In diesem Testbeispiel ist der Wert **blueadfs.contoso.com**. Klicken Sie auf **Weiter**.  
  
    > [!NOTE]  
    > Der Verbunddienstname kann nicht der Namen eines vorhandenen Servers in der Umgebung sein. Wenn Sie den Namen eines vorhandenen Servers verwenden, schlägt die AD FS-Installation fehl und muss neu gestartet werden.  
  
6.  Geben Sie auf der Seite **Angeben des Dienstkontos** den Namen ein, den Sie für die verwaltete Dienstkonto verwenden möchten. Wählen Sie für das Testbeispiel **Gruppenverwaltetes Dienstkonto erstellen** und geben Sie unter **Kontoname** **ADFSService** ein. Klicken Sie auf **Weiter**.  
  
7.  Wählen Sie auf der Seite **Angeben der Konfigurationsdatenbank** die Option **Erstellen einer Datenbank auf diesem Server mit der internen Windows-Datenbank** aus und klicken Sie auf **Weiter**.  
  
8.  Auf der Seite **Überprüfungsoptionen** sehen Sie eine Übersicht über die Optionen, die Sie ausgewählt haben. Klicken Sie auf **Weiter**.  
  
9. Auf der Seite **Voraussetzungsprüfungen** sehen Sie, ob alle erforderlichen Komponenten erfolgreich überprüft wurden. Wenn keine Probleme vorliegen, klicken Sie auf **Konfigurieren**.  
  
    > [!NOTE]  
    > Wenn Sie den Namen des AD FS-Servers oder eines anderen vorhandenen Rechners als Verbunddienstname verwendet haben, wird eine Fehlermeldung angezeigt. Sie müssen die Installation dann neu beginnen und den Namen eines vorhandenen Computers auswählen.  
  
10. Wenn die Konfiguration erfolgreich abgeschlossen wurde, wird auf der Seite **Ergebnisse** bestätigt, dass AD FS erfolgreich konfiguriert wurde.  
  
### <a name="configure-ad-fs-by-using-powershell"></a>Konfigurieren von AD FS mit PowerShell  
Um die entsprechende Konfiguration von AD FS mit Windows PowerShell durchzuführen, geben Sie folgende Befehle ein.  
  
So installieren Sie AD FS:  
  
```powershell  
Add-WindowsFeature RSAT-AD-Tools  
Add-WindowsFeature ADFS-Federation -IncludeManagementTools   
```  
  
So erstellen Sie ein verwaltetes Dienstkonto:  
  
```powershell  
New-ADServiceAccount "ADFSService"-Server 2016-DC.contoso.com -Path "CN=Managed Service Accounts,DC=Contoso,DC=COM" -DNSHostName 2016-ADFS.contoso.com -ServicePrincipalNames HTTP/2016-ADFS,HTTP/2016-ADFS.contoso.com  
```  
  
Nachdem Sie AD FS konfiguriert haben, müssen Sie eine AD FS-Farm über das im vorherigen Schritt erstellte verwaltete Dienstkonto einrichten und mithilfe des Zertifikats, das Sie in den Schritten vor der Konfiguration erstellt haben.  
  
So richten Sie eine AD FS-Farm ein:  
  
```powershell  
$cert = Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match blueadfs.contoso.com} | sort $_.NotAfter -Descending | select -first 1    
$thumbprint = $cert.Thumbprint  
Install-ADFSFarm -CertificateThumbprint $thumbprint -FederationServiceDisplayName "Contoso Corporation" –FederationServiceName blueadfs.contoso.com -GroupServiceAccountIdentifier contoso\ADFSService$ -OverwriteConfiguration -ErrorAction Stop  
```  
  
Nächster Schritt: [Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy: Schritt 2, und AD FS-Konfiguration nach der Arbeit](deploy-work-folders-adfs-step2.md)  
  
## <a name="see-also"></a>Siehe auch  
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)  
  

