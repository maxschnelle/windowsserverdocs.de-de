---
title: Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy-Schritt 1, einrichten AD FS
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 10/18/2018
ms.assetid: 938cdda2-f17e-4964-9218-f5868fd96735
ms.openlocfilehash: 6b8e9d6885184e2b40a87cae0dc8b8b82f4983fb
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965802"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-1-set-up-ad-fs"></a>Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 1, Setup AD FS

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird der erste Schritt beim Bereitstellen von Arbeits Ordnern mit Active Directory-Verbunddienste (AD FS) (AD FS) und dem webanwendungsproxy beschrieben. Die anderen Schritte in diesem Prozess finden Sie in den folgenden Themen:  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht](deploy-work-folders-adfs-overview.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy: Schritt 2 AD FS arbeiten nach der Konfiguration](deploy-work-folders-adfs-step2.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern](deploy-work-folders-adfs-step3.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 4](deploy-work-folders-adfs-step4.md)  
  
-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
>   Die in diesem Abschnitt behandelten Anweisungen gelten für eine Windows Server 2019-oder Windows Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, befolgen Sie die [Anweisungen unter Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn747208(v=ws.11)).

Verwenden Sie die folgenden Verfahren, um AD FS für die Verwendung mit Arbeits Ordnern einzurichten.  
  
## <a name="pre-installment-work"></a>Arbeit vor der \- Ausgabe  
Wenn Sie die Testumgebung, die Sie mit diesen Anweisungen einrichten, in die Produktion konvertieren möchten, können Sie vor dem Starten zwei Dinge tun:  
  
-   Richten Sie ein Active Directory Domänen Administrator Konto ein, das zum Ausführen des AD FS Dienstanbieter verwendet werden soll.
  
-   Rufen Sie ein Secure Sockets Layer (SSL)-San-Zertifikat (Subject Alternative Name) für die Server Authentifizierung ab. Für das Testbeispiel verwenden Sie ein selbst signiertes Zertifikat, aber für die Produktion sollten Sie ein öffentlich vertrauenswürdiges Zertifikat verwenden.  
  
Das Abrufen dieser Elemente kann einige Zeit in Anspruch nehmen, je nach den Richtlinien Ihres Unternehmens. Daher kann es vorteilhaft sein, den Anforderungs Prozess für die Elemente zu starten, bevor Sie mit dem Erstellen der Testumgebung beginnen.  
  
Es gibt viele kommerzielle Zertifizierungsstellen (CAS), von denen Sie das Zertifikat erwerben können. Eine Liste der Zertifizierungsstellen, die von Microsoft als vertrauenswürdig eingestuft werden, finden Sie im [KB-Artikel 931125](https://support.microsoft.com/kb/931125). Eine weitere Alternative besteht darin, ein Zertifikat von der Unternehmens Zertifizierungsstelle Ihres Unternehmens zu erhalten.  
  
Für die Testumgebung verwenden Sie ein selbst signiertes Zertifikat, das von einem der bereitgestellten Skripts erstellt wird.  
  
> [!NOTE]  
> AD FS unterstützt keine CNG-Zertifikate (Cryptography Next Generation), was bedeutet, dass Sie das selbst signierte Zertifikat nicht mithilfe des Windows PowerShell-Cmdlets New-selfsignedcertificate erstellen können. Sie können jedoch das makecert.ps1 Skript verwenden, das im Blogbeitrag bereitstellen [von Arbeits Ordnern mit AD FS und webanwendungsproxy](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap/ba-p/425318) enthalten ist. Dieses Skript erstellt ein selbst \- signiertes Zertifikat, das mit AD FS verwendet werden kann, und fordert die San-Namen an, die zum Erstellen des Zertifikats benötigt werden.  
  
Führen Sie als nächstes die zusätzlichen Aufgaben vor der Ausgabe aus, die in den folgenden Abschnitten beschrieben werden.  
  
### <a name="create-an-ad-fs-self-signed-certificate"></a>Erstellen eines AD FS selbst \- signierten Zertifikats  
Führen Sie die folgenden Schritte aus, um ein AD FS selbst signiertes Zertifikat zu erstellen:  
  
1.  Laden Sie die Skripts im Blogbeitrag bereitstellen [von Arbeits Ordnern mit AD FS und webanwendungsproxy](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap/ba-p/425318) herunter, und kopieren Sie die Datei makecert.ps1 auf den AD FS Computer.  
  
2.  Öffnen Sie ein Windows PowerShell-Fenster mit Administratorrechten.  
  
3.  Legen Sie die Ausführungs Richtlinie auf "uneingeschränkt" fest:  
  
    ```powershell  
    Set-ExecutionPolicy –ExecutionPolicy Unrestricted   
    ```  
  
4.  Wechseln Sie in das Verzeichnis, in das Sie das Skript kopiert haben.  
  
5.  Führen Sie das MakeCert-Skript aus:  
  
    ```powershell  
    .\makecert.ps1  
    ```  
  
6.  Wenn Sie aufgefordert werden, das Zertifikat des Antragstellers zu ändern, geben Sie den neuen Wert für das Thema ein. In diesem Beispiel ist der Wert **blueadfs.contoso.com**.  
  
7.  Wenn Sie zur Eingabe von San-Namen aufgefordert werden, drücken Sie Y, und geben Sie dann nacheinander die San-Namen ein.  
  
    Geben Sie für dieses Beispiel **blueadfs.contoso.com** ein, drücken Sie die EINGABETASTE, geben Sie **2016-ADFS.contoso.com** ein, drücken Sie die EINGABETASTE, geben Sie **enterpriseregistration.contoso.com** ein, und drücken Sie  
  
    Wenn alle San-Namen eingegeben wurden, drücken Sie in einer leeren Zeile die EINGABETASTE.  
  
8.  Wenn Sie aufgefordert werden, die Zertifikate im Speicher der vertrauenswürdigen Stamm Zertifizierungsstelle zu installieren, drücken Sie Y.  
  
Das AD FS Zertifikat muss ein San-Zertifikat mit den folgenden Werten sein:  

-   AD FS Dienst Name. Domäne

-   enterpriseregistration. Domäne

-   AD FS Servername. Domäne

Im Testbeispiel lauten die Werte wie folgt:  
  
-   **blueadfs.contoso.com**
  
-   **enterpriseregistration.contoso.com**
  
-   **2016-adfs.contoso.com**
  
Das San "enterpriseregistration" ist für Workplace Join erforderlich.  
  
### <a name="set-the-server-ip-address"></a>Festlegen der Server-IP-Adresse  
Ändern Sie die IP-Adresse Ihres Servers in eine statische IP-Adresse. Verwenden Sie für das Testbeispiel IP Class A, d. h. 192.168.0.160/Subnetzmaske: 255.255.0.0/Default Gateway: 192.168.0.1/bevorzugtes DNS: 192.168.0.150 (die IP-Adresse Ihres Domänen Controllers) \) .  
  
## <a name="install-the-ad-fs-role-service"></a>Installieren Sie den AD FS-Rollen Dienst.  
Um AD FS zu installieren, führen Sie die folgenden Schritte aus:  
  
1.  Melden Sie sich bei dem physischen oder virtuellen Computer an, auf dem Sie AD FS installieren möchten, öffnen Sie **Server-Manager**, und starten Sie den Assistenten zum Hinzufügen von Rollen und Features.  
  
2.  Wählen Sie auf der Seite **Server Rollen** die **Active Directory-Verbunddienste (AD FS)** Rolle aus, und klicken Sie dann auf **weiter**.  
  
3.  Auf der Seite **Active Directory-Verbunddienste (AD FS) (AD FS)** wird eine Meldung angezeigt, die besagt, dass die webanwendungsproxy-Rolle nicht auf dem gleichen Computer wie AD FS installiert werden kann. Klicken Sie auf **Weiter**.  
  
4.  Klicken Sie auf der Bestätigungsseite auf **Installieren** .  
  
Um die entsprechende Installation von AD FS über Windows PowerShell zu erreichen, verwenden Sie die folgenden Befehle:  
  
```powershell  
Add-WindowsFeature RSAT-AD-Tools  
Add-WindowsFeature ADFS-Federation –IncludeManagementTools  
```  
  
## <a name="configure-ad-fs"></a>Konfigurieren von AD FS  
Als Nächstes konfigurieren Sie AD FS mithilfe von Server-Manager oder Windows PowerShell.  
  
### <a name="configure-ad-fs-by-using-server-manager"></a>Konfigurieren von AD FS mithilfe von Server-Manager  
Führen Sie die folgenden Schritte aus, um AD FS mithilfe von Server-Manager zu konfigurieren:  
  
1.  Öffnen Sie den Server-Manager.  
  
2.  Klicken Sie oben im Fenster Server-Manager auf das **Benachrichtigungs** Kennzeichen, und klicken Sie dann **auf Verbund Dienst auf diesem Server konfigurieren**.  
  
3.  Der Active Directory-Verbunddienste (AD FS) Konfigurations-Assistent wird gestartet. Geben Sie auf der Seite **mit AD DS verbinden** das Domänen Administrator Konto ein, das Sie als AD FS Konto verwenden möchten, und klicken Sie auf **weiter**.  
  
4.  Geben Sie auf der Seite **Dienst Eigenschaften angeben** den Antragsteller Namen des SSL-Zertifikats ein, das für die AD FS Kommunikation verwendet werden soll. Im Beispiel Test ist dies **blueadfs.contoso.com**.  
  
5.  Geben Sie den Namen des Verbunddienst ein. Im Beispiel Test ist dies **blueadfs.contoso.com**. Klicken Sie auf **Weiter**.  
  
    > [!NOTE]  
    > Der Verbunddienst Name darf nicht den Namen eines vorhandenen Servers in der Umgebung verwenden. Wenn Sie den Namen eines vorhandenen Servers verwenden, schlägt die AD FS Installation fehl und muss neu gestartet werden.  
  
6.  Geben Sie auf der Seite **Dienst Konto angeben** den Namen ein, den Sie für das verwaltete Dienst Konto verwenden möchten. Wählen Sie für das Beispiel Test die Option **Gruppen verwaltetes Dienst Konto erstellen**aus, und geben Sie unter **Kontoname den Namen** **adtsservice**ein. Klicken Sie auf **Weiter**.  
  
7.  Wählen Sie auf der Seite **Konfigurations Datenbank angeben** die Option **Datenbank auf diesem Server mit interner Windows-Datenbank erstellen**aus, und klicken Sie auf **weiter**.  
  
8.  Auf der Seite **Optionen prüfen** wird eine Übersicht über die Optionen angezeigt, die Sie ausgewählt haben. Klicken Sie auf **Weiter**.  
  
9. Auf der Seite **Voraussetzungs Prüfungen** wird angegeben, ob alle Voraussetzungs Prüfungen erfolgreich abgeschlossen wurden. Wenn keine Probleme vorliegen, klicken Sie auf **Konfigurieren**.  
  
    > [!NOTE]  
    > Wenn Sie den Namen des AD FS Servers oder eines anderen vorhandenen Computers als Verbunddienst Namen verwendet haben, wird eine Fehlermeldung angezeigt. Sie müssen die Installation erneut starten und einen anderen Namen als den Namen eines vorhandenen Computers auswählen.  
  
10. Nachdem die Konfiguration erfolgreich abgeschlossen wurde, wird auf der Seite **Ergebnisse** bestätigt, dass AD FS erfolgreich konfiguriert wurde.  
  
### <a name="configure-ad-fs-by-using-powershell"></a>Konfigurieren von AD FS mithilfe von PowerShell  
Verwenden Sie die folgenden Befehle, um die entsprechende Konfiguration von AD FS über Windows PowerShell durchzuführen.  
  
So installieren Sie AD FS:  
  
```powershell  
Add-WindowsFeature RSAT-AD-Tools  
Add-WindowsFeature ADFS-Federation -IncludeManagementTools   
```  
  
So erstellen Sie das verwaltete Dienst Konto:  
  
```powershell  
New-ADServiceAccount "ADFSService"-Server 2016-DC.contoso.com -Path "CN=Managed Service Accounts,DC=Contoso,DC=COM" -DNSHostName 2016-ADFS.contoso.com -ServicePrincipalNames HTTP/2016-ADFS,HTTP/2016-ADFS.contoso.com  
```  
  
Nachdem Sie AD FS konfiguriert haben, müssen Sie mit dem verwalteten Dienst Konto, das Sie im vorherigen Schritt erstellt haben, und dem Zertifikat, das Sie in den Schritten vor der Konfiguration erstellt haben, eine AD FS Farm einrichten.  
  
So richten Sie eine AD FS-Farm ein:  
  
```powershell  
$cert = Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match blueadfs.contoso.com} | sort $_.NotAfter -Descending | select -first 1    
$thumbprint = $cert.Thumbprint  
Install-ADFSFarm -CertificateThumbprint $thumbprint -FederationServiceDisplayName "Contoso Corporation" –FederationServiceName blueadfs.contoso.com -GroupServiceAccountIdentifier contoso\ADFSService$ -OverwriteConfiguration -ErrorAction Stop  
```  
  
Nächster Schritt: bereitstellen [von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 2, AD FS Arbeitsaufgaben nach der Konfiguration](deploy-work-folders-adfs-step2.md)  
  
## <a name="see-also"></a>Weitere Informationen  
[Übersicht: Arbeitsordner](Work-Folders-Overview.md)  
  
