---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13ce514dc5f3f70217a26c898cde6fe24d4967c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847381"
---
# <a name="configure-a-federation-server"></a>Konfigurieren eines Verbundservers

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Nach der Installation der Active Directory-Verbunddienste \(AD FS\) -Rollendienst auf dem Computer, sind Sie bereit sind, diesen Computer als Verbundserver konfigurieren. Sie können eine der folgenden Aktionen ausführen:  
  
-   [Konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>Konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>So konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm mithilfe des Active Directory Federation Konfigurations-Assistenten  
  
> [!NOTE]  
> Stellen Sie sicher, dass Sie Domänenadministrator-Berechtigungen oder Domänenadministrator-Anmeldeinformationen verfügen, bevor Sie dieses Verfahren ausführen.  
  
1.  Klicken Sie auf der Seite **Dashboard** im Server-Manager auf das Kennzeichen **Benachrichtigungen** , und klicken Sie dann auf **Verbunddienst auf den Server konfigurieren**.  
  
    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Willkommen****Erstellen des ersten Verbundservers in einer Verbundserverfarm**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **mit AD DS verbinden** Seite, geben Sie ein Konto mit Domänenadministratorberechtigungen für die Active Directory \(AD\) Domäne, der diesen Computer hinzugefügt wird, und klicken Sie dann auf **Weiter**.  
  
4.  Führen Sie auf der Seite **Diensteigenschaften angeben** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Importieren der PFX-Datei, die das Secure Socket Layer enthält \(SSL\) Zertifikat und den Schlüssel, die Sie zuvor abgerufen haben. In [Schritt 2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md), haben Sie dieses Zertifikat abgerufen und kopiert diese auf dem Computer, die Sie als Verbundserver konfigurieren möchten. Klicken Sie zum Importieren der PFX-Datei mithilfe des Assistenten auf **importieren**, und suchen Sie dann den Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei, wenn Sie aufgefordert werden.  
  
    -   Geben Sie einen Namen für den Verbunddienst an. Z. B. **"FS.contoso.com"**. Dieser Name muss eine mit dem Antragstellernamen oder alternativen Antragstellernamen im Zertifikat übereinstimmen.  
  
    -   Geben Sie einen Anzeigenamen für den Verbunddienst an. Z. B. **Contoso Corporation**. Benutzern wird dieser Name angezeigt, auf die Active Directory Federation Services \(AD FS\) anmelden\-auf.  
  
5.  Auf der **angeben des Dienstkontos** Seite, ein Dienstkonto angeben. Sie können entweder erstellen oder einen vorhandenen gruppenverwalteten Dienstkontos \(gMSA\) oder ein vorhandenes Domänenbenutzerkonto verwenden. Wenn Sie die Option zum Erstellen eines neuen gmsas auswählen, geben Sie einen Namen für das neue Konto. Wenn Sie die Option zum Verwenden eines vorhandenen Gmsas oder Domänenkontos auswählen, klicken Sie auf **wählen** , ein Konto auszuwählen.  
  
    > [!NOTE]  
    > Der Vorteil der Verwendung eines gMSA-Kontos ist die automatische\-Kennwort Updatefunktion ausgehandelt.  
  
    > [!WARNING]  
    > Wenn Sie ein gMSA-Konto verwenden möchten, müssen Sie mindestens ein Domänencontroller in Ihrer Umgebung verfügen, die das Betriebssystem Windows Server 2012 ausgeführt wird.  
    >   
    > Wenn die gMSA-Option ist deaktiviert, und Sie eine Fehlermeldung angezeigt, wie z. B. sehen **Gruppenverwaltete Dienstkonten sind nicht verfügbar, weil der KDS-Stammschlüssel nicht festgelegt wurde**, Sie können gMSA in Ihrer Domäne aktivieren, indem Sie Ausführung der folgenden Windows PowerShell-Befehl auf einem Domänencontroller, auf denen Windows Server 2012 ausgeführt wird, oder höher in Ihrer Active Directory-Domäne: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Klicken Sie dann zurück zum Assistenten, klicken Sie auf **zurück**, und klicken Sie dann auf **Weiter** zum re\-Geben Sie die **angeben des Dienstkontos** Seite. Die gMSA-Option sollte jetzt aktiviert werden. Sie können es auswählen, und geben Sie ein gMSA-Kontonamen ein, die Sie verwenden möchten.  
  
6.  Auf der **angeben der Konfigurationsdatenbank** Seite Geben Sie eine AD FS-Konfigurationsdatenbank, und klicken Sie dann auf **Weiter**. Sie können entweder eine Datenbank auf diesem Computer erstellen, mithilfe von Windows Internal Database \(WID\), oder Sie können den Speicherort und den Instanznamen von Microsoft SQL Server angeben.  
  
    Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern Ihrer Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012 und SQL Server 2014.  
  
7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen** , und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **vor\-Prüfung auf erforderliche Software** Seite, stellen Sie sicher, dass alle voraussetzungsprüfungen erfolgreich abgeschlossen wurde, und klicken Sie dann auf **konfigurieren**.  
  
9. Auf der **Ergebnisse** Seite überprüfen Sie die Ergebnisse und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen ist, und klicken Sie dann auf **nächste Schritte zum Abschließen der Bereitstellung des Verbunddiensts**. Weitere Informationen finden Sie unter [nächste Schritte zum Abschließen der AD FS-Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.  
  
### <a name="BKMK_3"></a>So konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm über Windows PowerShell  
Sie können eine neue Verbundserverfarm erstellen, mit einer neuen oder vorhandenen gMSA-Konto oder ein vorhandenes Domänenbenutzerkonto verwenden.  
  
-   **Wenn Sie einen neuen Verbundserver unter Verwendung eines neuen gmsas erstellen möchten, führen Sie folgende Schritte aus:**  
  
    > [!IMPORTANT]  
    > Sie benötigen Domänenadministratorberechtigungen, um den ersten Verbundserver in einer neuen Verbundserverfarm zu erstellen.  
  
    1.  Stellen Sie sicher, dass auf das erforderliche SSL-Zertifikat importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\Meine Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, mithilfe des folgenden Befehls in Windows PowerShell-Befehlsfenster: `dir Cert:\LocalMachine\My`. Das Zertifikat aufgelistet, mit seinem Fingerabdruck unter der **lokalen Computer\\Meine Store** Verzeichnis.  
  
    2.  Auf Ihrem Domänencontroller, öffnen Sie Windows PowerShell-Befehlsfenster, und führen den folgenden Befehl aus, um zu überprüfen, ob der KDS-Stammschlüssel in Ihrer Domäne erstellt wurde: `Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Wenn sie nicht erstellt wurde, damit die Ausgabe keine Informationen angezeigt, führen Sie den folgenden Befehl zum Erstellen des Schlüssels: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`.  
  
    3.  Klicken Sie auf dem Computer, den Sie als Verbundserver konfigurieren möchten, öffnen Sie Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > Die `$` -Zeichen am Ende des vorherigen Befehls ist erforderlich.  
  
        Zum Abrufen des Werts für `<certificate_thumbprint>`führen `dir Cert:\LocalMachine\My`, und wählen Sie dann den Fingerabdruck des SSL-Zertifikats. Der Wert des `<federation_service_name>` ist der Name Ihres Verbunddiensts beispielsweise **"FS.contoso.com"**.  
  
        > [!NOTE]  
        > Wenn dies nicht der ersten, die Sie mit diesem Befehl ausführen ist, fügen Sie der `OverwriteConfiguration` Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt eine WID-Farm. Wenn Sie eine SQL Server-Serverfarm erstellen möchten, müssen Sie eine Instanz von SQL Server bereits installierten und funktionstüchtigen verfügen.  
        >   
        > Sie können den folgenden Befehl auf um den ersten Verbundserver in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet wird: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"` , in dem **< SQL\_Host\_Name >** ist der Name des Servers, auf dem SQL Server ausgeführt wird, und **< SQL\_Instanz\_Name >** ist der Name der Instanz von SQL Server. Verwenden, wenn Sie die Standardinstanz von SQL Server verwenden, eine **SQLConnectionString** Wert von "**Datenquelle\=< SQL\_Host\_Name >; Integrated Security\=" true "** ".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.  
  
-   **Wenn Sie einen neuen Verbundserver zu erstellen, indem Sie ein vorhandenes Domänenbenutzerkonto verwenden möchten, führen Sie folgende Schritte aus:**  
  
    1.  Stellen Sie sicher, dass auf das erforderliche SSL-Zertifikat importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\Meine Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, mithilfe des folgenden Befehls in Windows PowerShell-Befehlsfenster: `dir Cert:\LocalMachine\My`. Das Zertifikat aufgelistet, mit seinem Fingerabdruck unter der **lokalen Computer\\Meine Store** Verzeichnis.  
  
    2.  Klicken Sie auf dem Computer, die Sie als Verbundserver konfigurieren möchten, öffnen Sie Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl: `$fscred = Get-Credential`. Geben Sie die Anmeldeinformationen des Domänenbenutzers-Konto, das Sie für das Konto des Verbunddiensts in das Format Domäne verwenden möchten\\Benutzernamen ein.  
  
    3.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        Zum Abrufen des Werts für **< Zertifikat\_Fingerabdruck >** führen `dir Cert:\LocalMachine\My`, und wählen Sie dann den Fingerabdruck des SSL-Zertifikats. Der Wert des **< Verbund\_Service\_Name >** ist der Name des Verbunddiensts, z. B. "FS.contoso.com".  
  
        > [!NOTE]  
        > Wenn dies nicht der ersten, die Sie mit diesem Befehl ausführen ist, fügen Sie der `OverwriteConfiguration` Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt eine WID-Farm. Wenn Sie eine SQL Server-Farm erstellen möchten, müssen Sie die Instanz von SQL Server bereits installierten und funktionstüchtigen verfügen.  
        >   
        > Können Sie den folgenden Befehl auf um den ersten Verbundserver in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet wird: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` , in denen **SQL\_Host\_Namen** ist der Name des Servers, auf dem SQL Server ist. ausgeführt, und **SQL\_Instanz\_Namen** ist der Name der Instanz von SQL Server. Verwenden, wenn Sie die Standardinstanz von SQL Server verwenden, eine **SQLConnectionString** Wert von "**Datenquelle\=< SQL\_Host\_Name >; Integrated Security\=" true "** ".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern Ihrer Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012 und SQL Server 2014.  
  
## <a name="BKMK_2"></a>Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie abgeschlossen haben [Schritt 3: Installieren der AD FS-Rollendiensts](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md), bevor Sie eines der Verfahren in diesem Abschnitt beginnen.  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie einen gültigen SSL-Server Serverauthentifizierungszertifikat abgerufen haben, bevor Sie dieses Verfahren abzuschließen.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Zum Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm mithilfe des Active Directory Federation Konfigurations-Assistenten  
  
1.  Klicken Sie auf der Seite **Dashboard** im Server-Manager auf das Kennzeichen **Benachrichtigungen** , und klicken Sie dann auf **Verbunddienst auf den Server konfigurieren**.  
  
    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.  
  
2.  Auf der **Willkommen** Seite **Hinzufügen eines Verbundservers zu einer Verbundserverfarm**, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **mit AD DS verbinden** Seite, geben Sie ein Konto mit Domänenadministratorberechtigungen für die AD-Domäne, zu der dieser Computer ist Mitglied, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Farm angeben** Seite, geben Sie den Namen des primären Verbundservers in einer Farm, die WID verwendet, oder geben Sie den Hostnamen für die Datenbank und den Namen der Datenbankinstanz von einer vorhandenen Verbundserverfarm, die SQL Server verwendet.  
  
    > [!WARNING]  
    > In Windows Server® 2012 R2 ist eine problemumgehung für die Standardinstanz von SQL Server anzugeben. Die problemumgehung besteht darin, die Benutzeroberfläche nicht verwenden. Verwenden Sie stattdessen die Schritte im [so konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm über Windows PowerShell](Configure-a-Federation-Server.md#BKMK_3).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.  
  
5.  Auf der **SSL-Zertifikat angeben** Seite, importieren Sie die PFX-Datei mit dem SSL-Zertifikat und Schlüssel, den Sie zuvor abgerufen haben. Dieses Zertifikat ist das erforderliche Dienstauthentifizierungszertifikat. In [Schritt 2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md), haben Sie dieses Zertifikat abgerufen und kopiert diese auf dem Computer, die Sie als Verbundserver konfigurieren möchten. Klicken Sie zum Importieren der PFX-Datei mithilfe des Assistenten auf **importieren** und navigieren Sie zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei, wenn Sie aufgefordert werden.  
  
6.  Auf der **angeben des Dienstkontos** Seite, die das gleiche Dienstkonto, die Sie konfiguriert werden, bei der Erstellung des ersten Verbundservers in der Farm angeben. Sie können ein vorhandenes gruppenverwaltetes Dienstkonto oder ein vorhandenes Domänenbenutzerkonto verwenden.  
  
    > [!IMPORTANT]  
    > Das Konto, das Sie angeben, muss es sich um dasselbe Konto wie das Konto sein, auf dem primären Verbundserver in dieser Farm verwendet wurde.  
  
7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen** , und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **vor\-Prüfung auf erforderliche Software** Seite, stellen Sie sicher, dass alle voraussetzungsprüfungen erfolgreich abgeschlossen wurde, und klicken Sie dann auf **konfigurieren**.  
  
9. Auf der **Ergebnisse** Seite überprüfen Sie die Ergebnisse und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen ist, und klicken Sie dann auf **nächste Schritte zum Abschließen der Bereitstellung des Verbunddiensts**. Weitere Informationen finden Sie unter [nächste Schritte zum Abschließen der AD FS-Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Zum Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm mithilfe von Windows PowerShell  
Sie können einen Verbundserver zu einer vorhandenen Farm hinzufügen, mithilfe eines vorhandenen Gruppenverwalteten Dienstkontos oder ein vorhandenes Domänenbenutzerkonto verwenden.  
  
-   Wenn Sie einer Farm einen Verbundserver unter Verwendung eines vorhandenen Gruppenverwalteten Dienstkontos hinzuzufügen möchten, führen Sie folgende Schritte aus:  
  
    1.  Stellen Sie sicher, dass auf das erforderliche SSL-Zertifikat importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\Meine Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, mithilfe des folgenden Befehls in Windows PowerShell-Befehlsfenster: `dir Cert:\LocalMachine\My`. Das Zertifikat aufgelistet, mit seinem Fingerabdruck unter der **lokalen Computer\\Meine Store** Verzeichnis.  
  
    2.  Klicken Sie auf dem Computer, den Sie als Verbundserver konfigurieren möchten, öffnen Sie Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl.  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>` ist Ihre AD-Domäne und den Namen des Gruppenverwalteten Dienstkontos in der Domäne. `<first_federation_server_hostname>` ist der Hostname des primären Verbundservers in der vorhandenen Farm.  
  
        Sie erhalten den Wert für `<certificate_thumbprint>` mit `dir Cert:\LocalMachine\My` im vorherigen Schritt.  
  
        > [!NOTE]  
        > Wenn dies nicht der ersten, die Sie mit diesem Befehl ausführen ist, fügen Sie der `OverwriteConfiguration` Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt eine WID-farmknoten. Wenn Sie eine Server-farmknoten von SQL Server-Computern erstellen möchten, müssen Sie die Instanz von SQL Server bereits installierten und funktionstüchtigen verfügen.  
        >   
        > Sie können den folgenden Befehl zum Hinzufügen eines Verbundservers zu einer vorhandenen Farm, die eine Instanz von SQL Server verwendet wird: `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` , in denen **SQL\_Host\_Namen** ist der Name des Servers auf dem SQL Server ausgeführt, und **SQL\_Instanz\_Namen** ist der Name der Instanz von SQL Server. Verwenden, wenn Sie die Standardinstanz von SQL Server verwenden, eine **SQLConnectionString** Wert von "**Datenquelle\=< SQL\_Host\_Name >; Integrated Security\=" true "** ".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern Ihrer Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012 und SQL Server 2014.  
  
-   Wenn Sie einen Verbundserver zu einer Farm zu verknüpfen, indem Sie ein vorhandenes Domänenbenutzerkonto möchten, führen Sie folgende Schritte aus:  
  
    1.  Auf dem Computer, die Sie als Verbundserver konfigurieren möchten, öffnen Sie das Windows-PowerShellcommand-Fenster, und führen Sie den folgenden Befehl: `$fscred = get-credential`. Geben Sie die Anmeldeinformationen des Domänenbenutzers-Konto, das Sie für das Konto des Verbunddiensts in das Format Domäne verwenden möchten\\Benutzernamen ein.  
  
    2.  Stellen Sie sicher, dass auf das erforderliche SSL-Zertifikat importiert wurde, auf dem Computer, die Sie als Verbundserver konfigurieren möchten, die **lokalen Computer\\Meine Store** Verzeichnis. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, mithilfe des folgenden Befehls im Fenster Windows PowerShellcommand: `dir Cert:\LocalMachine\My`. Das Zertifikat aufgelistet, mit seinem Fingerabdruck unter der **lokalen Computer\\Meine Store** Verzeichnis.  
  
    3.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein.  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > Wenn dies nicht der ersten, die Sie mit diesem Befehl ausführen ist, fügen Sie der `OverwriteConfiguration` Parameter.  
  
        > [!NOTE]  
        > Der vorherige Befehl erstellt eine WID-farmknoten. Wenn Sie eine Server-farmknoten von SQL Server-Computern erstellen möchten, müssen Sie die Instanz von SQL Server bereits installierten und funktionstüchtigen verfügen. Sie können den folgenden Befehl zu einer vorhandenen Farm einen Verbundserver hinzuzufügen, mit einer Instanz von SQL Server: `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` , in denen **SQL\_Host\_Namen** ist der Name des Servers, auf dem SQL-Instanz Server ausgeführt wird, und **SQL\_Instanz\_Namen** ist der Name der Instanz von SQL Server. Verwenden, wenn Sie die Standardinstanz von SQL Server verwenden, eine **SQLConnectionString** Wert von "**Datenquelle\=< SQL\_Host\_Name >; Integrated Security\=" true "** ".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern Ihrer Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012 und SQL Server 2014.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS-Bereitstellung geführt.](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

