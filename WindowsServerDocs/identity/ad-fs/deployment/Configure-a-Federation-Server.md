---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Windows Server2012 R2 ADFS-Bereitstellungshandbuch
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13ce514dc5f3f70217a26c898cde6fe24d4967c6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-a-federation-server"></a>Konfigurieren eines Verbundservers

>Gilt für: Windows Server 2016, Windows Server2012 R2

Nachdem Sie die Active Directory Federation Services \(AD FS\)-Rollendienst auf dem Computer installieren, können Sie diesen Computer als Verbundserver konfigurieren. Sie können eine der folgenden Aktionen ausführen:  
  
-   [Konfigurieren des ersten Verbundservers in einer neuen Verbundserverfarm](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>Konfigurieren des ersten Verbundservers in einer neuen Verbundserverfarm  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>So konfigurieren Sie mithilfe des Assistenten zum Active Directory Federation Service Konfiguration des ersten Verbundservers in einer neuen Verbundserverfarm  
  
> [!NOTE]  
> Stellen Sie sicher, dass Sie verfügen über Domänenadministratorrechte oder Domänenadministrator-Anmeldeinformationen verfügbar sind, bevor Sie dieses Verfahren ausführen.  
  
1.  Auf den Server-Manager **Dashboard** auf die **Benachrichtigungen** kennzeichnen, und klicken Sie dann auf **konfigurieren Sie den Verbunddienst auf dem Server**.  
  
    Die **Active Directory Federation Service Konfigurations-Assistenten** wird geöffnet.  
  
2.  Auf der **Willkommen** Seite **Erstellen des ersten Verbundservers in einer Verbundserverfarm**, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **mit AD DS verbinden** Seite, geben Sie ein Konto mit Domänenadministrator-Berechtigungen für die \(AD\) Active Directory-Domäne, der dieser Computer hinzugefügt wird, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Diensteigenschaften angeben** Seite, gehen Sie folgendermaßen vor, und klicken Sie dann auf **Weiter**:  
  
    -   Importieren Sie die PFX-Datei mit der \(SSL\) Secure Socket Layer-Zertifikat und den Schlüssel, die Sie zuvor erhalten haben. In [Schritt2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md), haben Sie dieses Zertifikat abgerufen und kopiert diese auf dem Computer, die Sie als Verbundserver konfigurieren möchten. Klicken Sie zum Importieren der PFX-Datei mit dem Assistenten **importieren**, und wechseln Sie zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei, wenn Sie dazu aufgefordert werden.  
  
    -   Geben Sie einen Namen für den Verbunddienst. Beispielsweise **fs.contoso.com**. Dieser Name muss eines der Antragstellernamen oder alternativen Antragstellernamen des Zertifikats übereinstimmen.  
  
    -   Geben Sie einen Anzeigenamen für den Verbunddienst. Beispielsweise **Contoso Corporation**. Benutzer finden Sie unter diesem Namen auf die Active Directory Federation Services \(AD FS\) sign\-Seite.  
  
5.  Auf der **angeben des Dienstkontos** Seite, Angeben eines Dienstkontos. Sie können entweder erstellen oder eine vorhandene Gruppe Managed Service Account \(gMSA\) verwenden oder ein vorhandenes Domänenbenutzerkonto verwenden. Wenn Sie die Option zum Erstellen eines neuen gMSA-Kontos auswählen, geben Sie einen Namen für das neue Konto. Wenn Sie die Möglichkeit, eine vorhandene gMSA oder ein Domänenkonto verwenden, klicken Sie auf **wählen** ein Konto auswählen.  
  
    > [!NOTE]  
    > Der Vorteil der Verwendung eines gMSA-Kontos ist die Aktualisierungsfunktion Kennwort Automatisches ausgehandelt.  
  
    > [!WARNING]  
    > Wenn Sie ein gMSA-Konto verwenden möchten, müssen Sie mindestens einen Domänencontroller in Ihrer Umgebung verfügen, auf denen das Betriebssystem Windows Server2012 ausgeführt wird.  
    >   
    > Wenn die gMSA-Option ist deaktiviert, und Sie eine Fehlermeldung angezeigt, z.B. **Gruppenverwaltete Dienstkonten sind nicht verfügbar, da Sie den KDS-Stammschlüssel nicht festgelegt wurde**, können Sie gMSA in Ihrer Domäne aktivieren, indem Sie den folgenden Windows PowerShell-Befehl ausführen, auf einem Domänencontroller, der Windows Server2012 ausgeführt wird oder höher, in der Active Directory-Domäne:`Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Klicken Sie dann zurück zum Assistenten klicken Sie auf **zurück**, und klicken Sie dann auf **Weiter**, erneut-Geben Sie die **angeben des Dienstkontos** Seite. Die gMSA-Option sollten nun aktiviert sein. Sie können wählen Sie ihn, und geben Sie einen gMSA-Konto ein, den Sie verwenden möchten.  
  
6.  Auf der **angeben der Konfigurationsdatenbank** Seite Geben Sie eine AD FS-Konfigurationsdatenbank, und klicken Sie dann auf **Weiter**. Sie können entweder eine Datenbank auf diesem Computer erstellen, mithilfe von Windows Internal Database \(WID\), oder Sie können den Speicherort und den Instanznamen von Microsoft SQL Server angeben.  
  
    Weitere Informationen finden Sie unter [die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012 und SQL Server2014.  
  
7.  Auf der **Optionen prüfen** Seite, überprüfen Sie Ihre Konfigurationsauswahl, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **registrierungseintragswert erforderlichen Überprüfungen** sicher, dass alle voraussetzungsprüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **konfigurieren**.  
  
9. Auf der **Ergebnisse** Seite, überprüfen Sie die Ergebnisse und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen ist, und klicken Sie dann auf **nächsten Schrittezum Abschließen der Bereitstellung des Verbunddiensts**. Weitere Informationen finden Sie unter [nächste Schrittefür das Abschließen der AD FS-Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
### <a name="BKMK_3"></a>So konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm über Windows PowerShell  
Sie können eine neue Verbundserverfarm erstellen, mit einer neuen oder vorhandenen gMSA-Konto oder ein vorhandenes Domänenbenutzerkonto.  
  
-   **Wenn Sie einen neuen Verbundserver zu erstellen, indem Sie ein neues gMSA-Konto verwenden möchten, führen Sie folgende Schritteaus:**  
  
    > [!IMPORTANT]  
    > Sie müssen Domänenadministrator-Berechtigungen zum Erstellen des ersten Verbundservers in einer neuen Verbundserverfarm haben.  
  
    1.  Stellen Sie sicher, dass die erforderliche SSL-Zertifikat in importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\My Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie in der Windows PowerShell-Befehlsfenster den folgenden Befehl ausführen:`dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck in aufgeführt. die **lokalen Computer\\My Store** Verzeichnis.  
  
    2.  Auf dem Domänencontroller, öffnen Sie das Windows PowerShell-Befehlsfenster, und führen Sie folgenden Befehl überprüfen, ob die KDS-Stammschlüssel in der Domäne erstellt wurde:`Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Wenn es nicht erstellt wurde, damit die Ausgabe zeigt keine Informationen an, führen Sie den folgenden Befehl zum Erstellen des Schlüssels:`Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`.  
  
    3.  Öffnen Sie auf dem Computer, den Sie als Verbundserver konfigurieren möchten das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > Die `$`Anmelden am Ende des vorherigen Befehls ist erforderlich.  
  
        Der Wert für `<certificate_thumbprint>`führen `dir Cert:\LocalMachine\My`, und wählen Sie dann den Fingerabdruck des SSL-Zertifikats. Der Wert der `<federation_service_name>`ist der Name des Verbunddienst z.B. **fs.contoso.com**.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal, die Sie diesen Befehl ausführen ist, fügen Sie der `OverwriteConfiguration`Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt eine Windows-datenbankfarm. Wenn Sie eine SQL Server-Serverfarm erstellen möchten, müssen Sie eine Instanz von SQL Server bereits installiert und betriebsbereit verfügen.  
        >   
        > Sie können den folgenden Befehl zum ersten Verbundserver in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"`, in denen **< SQL\_Host\_Name >** ist der Name des Servers, auf dem SQL Server ausgeführt wird, und **< SQL\_instance\_name >** ist der Name der Instanz von SQL Server. Bei Verwendung die Standardinstanz von SQL Server verwenden ein **SQLConnectionString** Wert "**Daten Source\ = < SQL\_Host\_Name >; integrierte Sicherheit\ = True**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012.  
  
-   **Wenn Sie einen neuen Verbundserver zu erstellen, indem Sie ein vorhandenes Domänenbenutzerkonto verwenden möchten, führen Sie folgende Schritteaus:**  
  
    1.  Stellen Sie sicher, dass die erforderliche SSL-Zertifikat in importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\My Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie in der Windows PowerShell-Befehlsfenster den folgenden Befehl ausführen:`dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck in aufgeführt. die **lokalen Computer\\My Store** Verzeichnis.  
  
    2.  Auf dem Computer, die Sie als Verbundserver konfigurieren möchten, öffnen Sie das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl:`$fscred = Get-Credential`. Geben Sie die Anmeldeinformationen für das Domänenbenutzerkonto, die Sie für den Verbund-Dienstkonto im Format "Domäne\\Benutzer" Name verwenden möchten.  
  
    3.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        Der Wert für **< Certificate\_thumbprint >**führen `dir Cert:\LocalMachine\My`, und wählen Sie dann den Fingerabdruck des SSL-Zertifikats. Der Wert der **< Federation\_service\_name >** ist der Name der Verbunddienst z.B. fs.contoso.com.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal, die Sie diesen Befehl ausführen ist, fügen Sie der `OverwriteConfiguration`Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt eine Windows-datenbankfarm. Wenn Sie eine SQL Server-Farm erstellen möchten, müssen Sie die Instanz von SQL Server bereits installiert und betriebsbereit verfügen.  
        >   
        > Sie können den folgenden Befehl zum ersten Verbundserver in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, in denen **SQL\_Host\_Name** ist der Name des Servers, auf dem SQL Server ausgeführt wird, und **SQL\_instance\_name** ist der Name der Instanz von SQL Server. Bei Verwendung die Standardinstanz von SQL Server verwenden ein **SQLConnectionString** Wert "**Daten Source\ = < SQL\_Host\_Name >; integrierte Sicherheit\ = True**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012 und SQL Server2014.  
  
## <a name="BKMK_2"></a>Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie abgeschlossen haben [Schritt3: Installieren des AD FS-Rollendiensts](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md), bevor Sie eines der Verfahren in diesem Abschnittbeginnen.  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie einen gültigen SSL-Server-Authentifizierungszertifikat abgerufen haben, bevor Sie dieses Verfahren ausführen.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Hinzufügen ein Verbundservers zu einer vorhandenen Verbundserverfarm über den Active Directory Federation-Service-Assistenten  
  
1.  Auf den Server-Manager **Dashboard** auf die **Benachrichtigungen** kennzeichnen, und klicken Sie dann auf **konfigurieren Sie den Verbunddienst auf dem Server**.  
  
    Die **Active Directory Federation Service Konfigurations-Assistenten** wird geöffnet.  
  
2.  Auf der **Willkommen** Seite **Hinzufügen eines Verbundservers zu einer Verbundserverfarm**, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **mit AD DS verbinden** Seite, geben Sie ein Konto mit Domänenadministrator-Berechtigungen für die AD-Domäne, der dieser Computer hinzugefügt wird, und klicken Sie auf **Weiter**.  
  
4.  Auf der **Farm angeben** Seite, geben Sie den Namen des primären Verbundservers in einer Farm, die interne Windows-Datenbank verwendet, oder geben Sie die Datenbank-Hostnamen und der Name der Datenbankinstanz von einer vorhandenen Verbundserverfarm, die SQL Server verwendet wird.  
  
    > [!WARNING]  
    > In Windows Server® 2012 R2 ist eine Problemumgehung die Standardinstanz von SQL Server angeben. Die umgangen werden, die Benutzeroberfläche nicht verwenden. Verwenden Sie stattdessen die Schritteim [so konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm über Windows PowerShell](Configure-a-Federation-Server.md#BKMK_3).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012.  
  
5.  Auf der **SSL-Zertifikat angeben** Seite, importieren Sie die PFX-Datei, die enthält das SSL-Zertifikat und den Schlüssel, die Sie zuvor erhalten haben. Dieses Zertifikat ist das erforderliche dienstauthentifizierungszertifikat. In [Schritt2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md), haben Sie dieses Zertifikat abgerufen und kopiert diese auf den Computer, die Sie als Verbundserver konfigurieren möchten. Klicken Sie zum Importieren der PFX-Datei mit dem Assistenten **importieren** und navigieren Sie zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei, wenn Sie dazu aufgefordert werden.  
  
6.  Auf der **angeben des Dienstkontos** geben das gleiche Dienstkonto, das Sie beim Erstellen des ersten Verbundservers in der Farm konfiguriert. Sie können eine vorhandene Gruppe Managed Service Account oder ein vorhandenes Domänenbenutzerkonto verwenden.  
  
    > [!IMPORTANT]  
    > Die, das von Ihnen angegebene Konto muss dasselbe Konto wie das Konto, das auf dem primären Verbundserver in dieser Farm verwendet wurde.  
  
7.  Auf der **Optionen prüfen** Seite, überprüfen Sie Ihre Konfigurationsauswahl, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **registrierungseintragswert erforderlichen Überprüfungen** sicher, dass alle voraussetzungsprüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **konfigurieren**.  
  
9. Auf der **Ergebnisse** Seite, überprüfen Sie die Ergebnisse und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen ist, und klicken Sie dann auf **nächsten Schrittezum Abschließen der Bereitstellung des Verbunddiensts**. Weitere Informationen finden Sie unter [nächste Schrittefür das Abschließen der AD FS-Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Hinzufügen ein Verbundservers zu einer vorhandenen Verbundserverfarm über Windows PowerShell  
Sie können einen Verbundserver zu einer vorhandenen Farm hinzufügen, über ein vorhandenes gMSA-Konto oder ein vorhandenes Domänenbenutzerkonto.  
  
-   Wenn Sie einen Verbundserver zu einer Farm beitreten, mithilfe eines vorhandenen gMSA-Kontos möchten, führen Sie folgende Schritteaus:  
  
    1.  Stellen Sie sicher, dass die erforderliche SSL-Zertifikat in importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\My Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie in der Windows PowerShell-Befehlsfenster den folgenden Befehl ausführen:`dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck in aufgeführt. die **lokalen Computer\\My Store** Verzeichnis.  
  
    2.  Öffnen Sie auf dem Computer, den Sie als Verbundserver konfigurieren möchten das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>` Ist Ihre AD-Domäne und den Namen Ihres gMSA-Kontos in der Domäne. `<first_federation_server_hostname>` Ist der Hostname des primären Verbundserver in dieser Farm vorhandenen.  
  
        Sie können den Wert für abrufen `<certificate_thumbprint>`mit `dir Cert:\LocalMachine\My`im vorherigen Schritt.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal, die Sie diesen Befehl ausführen ist, fügen Sie der `OverwriteConfiguration`Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt einen WID-Farmknoten. Wenn Sie einen Server-Farmknoten des SQL Server-Computern zu erstellen möchten, müssen Sie die Instanz von SQL Server bereits installiert und betriebsbereit verfügen.  
        >   
        > Sie können den folgenden Befehl zum Hinzufügen eines Verbundservers zu einer vorhandenen Farm, die eine Instanz von SQL Server verwendet wird: `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, in denen **SQL\_Host\_Name** ist der Name des Servers, auf dem SQL Server ausgeführt wird, und **SQL\_instance\_name** ist der Name der Instanz von SQL Server. Bei Verwendung die Standardinstanz von SQL Server verwenden ein **SQLConnectionString** Wert "**Daten Source\ = < SQL\_Host\_Name >; integrierte Sicherheit\ = True**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012 und SQL Server2014.  
  
-   Wenn Sie einen Verbundserver zu einer Farm zu verknüpfen, indem Sie ein vorhandenes Domänenbenutzerkonto möchten, führen Sie folgende Schritteaus:  
  
    1.  Klicken Sie auf dem Computer, die Sie als Verbundserver konfigurieren möchten, öffnen Sie das Fenster Windows PowerShellcommand, und führen Sie den folgenden Befehl:`$fscred = get-credential`. Geben Sie die Anmeldeinformationen für das Domänenbenutzerkonto, die Sie für den Verbund-Dienstkonto im Format "Domäne\\Benutzer" Name verwenden möchten.  
  
    2.  Stellen Sie sicher, dass die erforderliche SSL-Zertifikat in importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\My Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, durch den folgenden Befehl in der Windows-PowerShellcommand Fenster ausführen:`dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck in aufgeführt. die **lokalen Computer\\My Store** Verzeichnis.  
  
    3.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal, die Sie diesen Befehl ausführen ist, fügen Sie der `OverwriteConfiguration`Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt einen WID-Farmknoten. Wenn Sie einen Server-Farmknoten des SQL Server-Computern zu erstellen möchten, müssen Sie die Instanz von SQL Server bereits installiert und betriebsbereit verfügen. Sie können den folgenden Befehl zum Hinzufügen eines Verbundservers zu einer vorhandenen Farm mithilfe einer Instanz von SQL Server: `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, in denen **SQL\_Host\_Name** ist der Name des Servers, auf dem die Instanz von SQL Server ausgeführt wird, und **SQL\_instance\_name** ist der Name der Instanz von SQL Server. Bei Verwendung die Standardinstanz von SQL Server verwenden ein **SQLConnectionString** Wert "**Daten Source\ = < SQL\_Host\_Name >; integrierte Sicherheit\ = True**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012 und SQL Server2014.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server2012 R2 ADFS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

