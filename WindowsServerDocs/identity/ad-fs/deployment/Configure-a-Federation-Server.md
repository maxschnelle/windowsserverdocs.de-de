---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c549b52f697db889bf638470aca03f02e1323ed5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359729"
---
# <a name="configure-a-federation-server"></a>Konfigurieren eines Verbundservers

Nachdem Sie den Active Directory-Verbunddienste (AD FS) \(AD FS\) -Rollen Dienst auf Ihrem Computer installiert haben, können Sie diesen Computer als Verbund Server konfigurieren. Sie können eine der folgenden Aktionen ausführen:  
  
-   [Konfigurieren des ersten Verbund Servers in einer neuen Verbund Serverfarm](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [Hinzufügen eines Verbund Servers zu einer vorhandenen Verbund Serverfarm](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>Konfigurieren des ersten Verbund Servers in einer neuen Verbund Serverfarm  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>So konfigurieren Sie den ersten Verbund Server in einer neuen Verbund Serverfarm mithilfe des Konfigurations-Assistenten für Active Directory Verbunddienst  
  
> [!NOTE]  
> Stellen Sie sicher, dass Sie über Domänen Administrator Berechtigungen verfügen oder über Domänen Administrator-Anmelde Informationen verfügen, bevor Sie dieses Verfahren ausführen  
  
1.  Klicken Sie auf der Seite **Dashboard** im Server-Manager auf das Kennzeichen **Benachrichtigungen** , und klicken Sie dann auf **Verbunddienst auf den Server konfigurieren**.  
  
    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Willkommen** **Erstellen des ersten Verbundservers in einer Verbundserverfarm**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **mit AD DS verbinden** ein Konto mithilfe von Domänen Administrator Berechtigungen für die \(Active Directory\) AD-Domäne an, der dieser Computer hinzugefügt wurde, und klicken Sie dann auf **weiter**.  
  
4.  Führen Sie auf der Seite **Diensteigenschaften angeben** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Importieren Sie die PFX-Datei, die das SSL \(\) -Zertifikat und den Schlüssel der Secure Socket Layer enthält, die Sie zuvor abgerufen haben. In [Schritt 2: Registrieren Sie ein SSL-Zertifikat für](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)AD FS. Sie haben dieses Zertifikat abgerufen und auf den Computer kopiert, den Sie als Verbund Server konfigurieren möchten. Um die PFX-Datei über den Assistenten zu importieren, klicken Sie auf **importieren**, und navigieren Sie dann zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei ein, wenn Sie dazu aufgefordert werden.  
  
    -   Geben Sie einen Namen für den Verbund Dienst an. Beispielsweise **FS.contoso.com**. Dieser Name muss mit einem der alternativen Antragsteller Namen oder alternativen Antragsteller Namen im Zertifikat identisch sein.  
  
    -   Geben Sie einen anzeigen Amen für den Verbund Dienst an. Beispiel: **CONSO Corporation**. Benutzern wird dieser Name auf der Active Directory-Verbunddienste (AD FS) \(AD FS\) Anmelde\-Seite angezeigt.  
  
5.  Geben Sie auf der Seite **Dienst Konto angeben** ein Dienst Konto an. Sie können entweder ein vorhandenes Gruppen verwaltetes Dienst Konto \(\) oder ein vorhandenes Domänen Benutzerkonto erstellen oder verwenden. Wenn Sie die Option zum Erstellen eines neuen GMSA-Kontos auswählen, geben Sie einen Namen für das neue Konto an. Wenn Sie die Option zum Verwenden eines vorhandenen GMSA-oder Domänen Kontos auswählen, klicken Sie auf **auswählen** , um ein Konto auszuwählen.  
  
    > [!NOTE]  
    > Der Vorteil der Verwendung eines GMSA-Kontos ist das\-automatisch ausgehandelte Kennwort-Update Feature.  
  
    > [!WARNING]  
    > Wenn Sie ein GMSA-Konto verwenden möchten, muss in Ihrer Umgebung mindestens ein Domänen Controller vorhanden sein, auf dem das Betriebssystem Windows Server 2012 ausgeführt wird.  
    >   
    > Wenn die GMSA-Option deaktiviert ist und eine Fehlermeldung angezeigt wird, z. b. Wenn **Gruppen verwaltete Dienst Konten nicht verfügbar sind, weil der KDS-Stamm Schlüssel nicht festgelegt**wurde, können Sie GMSA in Ihrer Domäne aktivieren, indem Sie den folgenden Windows PowerShell-Befehl für eine Domäne ausführen. Controller, auf dem Windows Server 2012 oder höher ausgeführt wird, in Ihrer Active Directory `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`Domäne:. Kehren Sie dann zum Assistenten zurück, **Klicken Sie auf**zurück, und klicken Sie\-dann auf **weiter** , um die Seite **Dienst Konto angeben** erneut einzugeben. Die GMSA-Option sollte jetzt aktiviert sein. Sie können es auswählen und einen Namen für das GMSA-Konto eingeben, das Sie verwenden möchten.  
  
6.  Geben Sie auf der Seite **Konfigurations Datenbank angeben** eine AD FS Konfigurations Datenbank an, und klicken Sie dann auf **weiter**. Sie können entweder eine Datenbank auf diesem Computer mithilfe der internen Windows-Datenbank \(-\)wid erstellen, oder Sie können den Speicherort und den Instanznamen Microsoft SQL Server angeben.  
  
    Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  
7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen** , und klicken Sie dann auf **Weiter**.  
  
8.  Überprüfen Sie auf der Seite **Voraussetzungs Prüfungen\-** , ob alle Voraussetzungs Prüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Konfigurieren**.  
  
9. Überprüfen Sie auf der Seite **Ergebnisse** die Ergebnisse, und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurde, und klicken Sie dann auf **weiter, um die Bereitstellung des Verbund Dienstanbieter abzuschließen**. Weitere Informationen finden Sie unter [Nächste Schritte zum Abschließen der AD FS Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.  
  
### <a name="BKMK_3"></a>So konfigurieren Sie den ersten Verbund Server in einer neuen Verbund Serverfarm über Windows PowerShell  
Sie können eine neue Verbund Serverfarm erstellen, indem Sie entweder ein neues oder ein vorhandenes GMSA-Konto oder ein vorhandenes Domänen Benutzerkonto verwenden.  
  
-   **Wenn Sie einen neuen Verbund Server mit einem neuen GMSA-Konto erstellen möchten, gehen Sie wie folgt vor:**  
  
    > [!IMPORTANT]  
    > Sie müssen über Domänen Administrator Berechtigungen verfügen, um den ersten Verbund Server in einer neuen Verbund Serverfarm zu erstellen.  
  
    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in das Verzeichnis " **mein Speicher" des lokalen Computers\\** importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell- `dir Cert:\LocalMachine\My`Befehlsfenster ausführen:. Das Zertifikat wird durch seinen Fingerabdruck im **lokalen Computer\\mein Speicher** Verzeichnis aufgelistet.  
  
    2.  Öffnen Sie auf dem Domänen Controller das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus, um zu überprüfen, ob der KDS `Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`-Stamm Schlüssel in Ihrer Domäne erstellt wurde:. Wenn Sie nicht erstellt wurde, sodass in der Ausgabe keine Informationen angezeigt werden, führen Sie den folgenden Befehl aus, um `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`den Schlüssel zu erstellen:.  
  
    3.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > Das `$` Vorzeichen am Ende des vorherigen Befehls ist erforderlich.  
  
        Um den Wert für zu `<certificate_thumbprint>`erhalten, `dir Cert:\LocalMachine\My`führen Sie aus, und wählen Sie dann den Fingerabdruck Ihres SSL-Zertifikats aus. Der Wert von `<federation_service_name>` ist der Name des Verbund Dienstanbieter, z. b. **FS.contoso.com**.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen `OverwriteConfiguration` Sie den-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird eine wid-Farm erstellt. Wenn Sie eine SQL Server Server Farm erstellen möchten, müssen Sie über eine Instanz von SQL Server verfügen, die bereits installiert und betriebsbereit ist.  
        >   
        > Sie können den folgenden Befehl verwenden, um den ersten Verbund Server in einer neuen Farm zu erstellen, die eine Instanz von `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"` SQL Server verwendet: wobei **< SQL\_-\_Hostname >** der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **< SQL\_-\_Instanzname >** ist der Name der Instanz von SQL Server. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von " **\=Data Source <\_SQL\_-Hostname >\=; integrierte Sicherheit true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.  
  
-   **Wenn Sie einen neuen Verbund Server unter Verwendung eines vorhandenen Domänen Benutzerkontos erstellen möchten, gehen Sie folgendermaßen vor:**  
  
    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in das Verzeichnis " **mein Speicher" des lokalen Computers\\** importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell- `dir Cert:\LocalMachine\My`Befehlsfenster ausführen:. Das Zertifikat wird durch seinen Fingerabdruck im **lokalen Computer\\mein Speicher** Verzeichnis aufgelistet.  
  
    2.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie dann den folgenden `$fscred = Get-Credential`Befehl aus:. Geben Sie die Anmelde Informationen für das Domänen Benutzerkonto ein, das Sie für das Verbund Dienst Konto\\im Format Domäne Benutzername verwenden möchten.  
  
    3.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        Wenn Sie den Wert für **< Zertifikat\_Fingerabdruck >** abrufen möchten `dir Cert:\LocalMachine\My`, führen Sie aus, und wählen Sie dann den Fingerabdruck Ihres SSL-Zertifikats aus. Der Wert von **<\_Verbund Dienst\_Name >** ist der Name Ihres Verbund Dienstanbieter, z. b. fs.contoso.com.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen `OverwriteConfiguration` Sie den-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird eine wid-Farm erstellt. Wenn Sie eine SQL Server-Farm erstellen möchten, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein.  
        >   
        > Sie können den folgenden Befehl verwenden, um den ersten Verbund Server in einer neuen Farm zu erstellen, die eine Instanz von `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` SQL Server verwendet: wobei der **SQL\_-Hostname\_** der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **SQL der Instanzname\_ist der Name der Instanz von SQL Server. \_** Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von " **\=Data Source <\_SQL\_-Hostname >\=; integrierte Sicherheit true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  
## <a name="BKMK_2"></a>Hinzufügen eines Verbund Servers zu einer vorhandenen Verbund Serverfarm  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass [Sie Schritt 3 abgeschlossen haben: Installieren Sie den AD FS-](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)Rollen Dienst, bevor Sie mit einem der in diesem Abschnitt beschriebenen Verfahren beginnen.  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie ein gültiges SSL-Server Authentifizierungszertifikat erhalten haben, bevor Sie dieses Verfahren ausführen.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>So fügen Sie einer vorhandenen Verbund Serverfarm mithilfe des Konfigurations-Assistenten für Active Directory Verbunddienst einen Verbund Server hinzu  
  
1.  Klicken Sie auf der Seite **Dashboard** im Server-Manager auf das Kennzeichen **Benachrichtigungen** , und klicken Sie dann auf **Verbunddienst auf den Server konfigurieren**.  
  
    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Willkommen** die Option Verbund **Server zu einer Verbund Serverfarm hinzufügen**aus, und klicken Sie dann auf **weiter**.  
  
3.  Geben Sie auf der Seite **mit AD DS verbinden** ein Konto mithilfe von Domänen Administrator Berechtigungen für die AD-Domäne an, der dieser Computer hinzugefügt wurde, und klicken Sie dann auf **weiter**.  
  
4.  Geben Sie auf der Seite **Farm angeben** den Namen des primären Verbund Servers in einer Farm an, die wid verwendet, oder geben Sie den Datenbank-Hostnamen und den Datenbankinstanznamen einer vorhandenen Verbund Server Farm an, die SQL Server verwendet.  
  
    > [!WARNING]  
    > In Windows Server® 2012 R2 gibt es eine Problem Umgehung, um die Standard Instanz von SQL Server anzugeben. Die Problem Umgehung besteht darin, die Benutzeroberfläche nicht zu verwenden. Verwenden Sie stattdessen die Schritte in [, um den ersten Verbund Server in einer neuen Verbund Serverfarm über Windows PowerShell zu konfigurieren](Configure-a-Federation-Server.md#BKMK_3).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.  
  
5.  Importieren Sie auf der Seite **SSL-Zertifikat angeben** die PFX-Datei mit dem SSL-Zertifikat und-Schlüssel, die Sie zuvor abgerufen haben. Dieses Zertifikat ist das erforderliche Dienstauthentifizierungszertifikat. In [Schritt 2: Registrieren Sie ein SSL-Zertifikat für](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)AD FS. Sie haben dieses Zertifikat abgerufen und auf den Computer kopiert, den Sie als Verbund Server konfigurieren möchten. Um die PFX-Datei über den Assistenten zu importieren, klicken Sie auf **importieren** , und navigieren Sie zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei ein, wenn Sie dazu aufgefordert werden.  
  
6.  Geben Sie auf der Seite **Dienst Konto angeben** das gleiche Dienst Konto an, das Sie beim Erstellen des ersten Verbund Servers in der Farm konfiguriert haben. Sie können ein vorhandenes Gruppen verwaltetes Dienst Konto oder ein vorhandenes Domänen Benutzerkonto verwenden.  
  
    > [!IMPORTANT]  
    > Das angegebene Konto muss mit dem Konto identisch sein, das auf dem primären Verbund Server in dieser Farm verwendet wurde.  
  
7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen** , und klicken Sie dann auf **Weiter**.  
  
8.  Überprüfen Sie auf der Seite **Voraussetzungs Prüfungen\-** , ob alle Voraussetzungs Prüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Konfigurieren**.  
  
9. Überprüfen Sie auf der Seite **Ergebnisse** die Ergebnisse, und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurde, und klicken Sie dann auf **weiter, um die Bereitstellung des Verbund Dienstanbieter abzuschließen**. Weitere Informationen finden Sie unter [Nächste Schritte zum Abschließen der AD FS Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>So fügen Sie einer vorhandenen Verbund Serverfarm mithilfe von Windows PowerShell einen Verbund Server hinzu  
Sie können einer vorhandenen Farm einen Verbund Server hinzufügen, indem Sie entweder ein vorhandenes GMSA-Konto oder ein vorhandenes Domänen Benutzerkonto verwenden.  
  
-   Gehen Sie folgendermaßen vor, wenn Sie einen Verbund Server mit einem vorhandenen GMSA-Konto zu einer Farm hinzufügen möchten:  
  
    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in das Verzeichnis " **mein Speicher" des lokalen Computers\\** importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell- `dir Cert:\LocalMachine\My`Befehlsfenster ausführen:. Das Zertifikat wird durch seinen Fingerabdruck im **lokalen Computer\\mein Speicher** Verzeichnis aufgelistet.  
  
    2.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>`ist Ihre AD-Domäne und der Name Ihres GMSA-Kontos in dieser Domäne. `<first_federation_server_hostname>`der Hostname des primären Verbund Servers in dieser vorhandenen Farm.  
  
        Sie können den Wert für `<certificate_thumbprint>` abrufen, indem Sie im vorherigen Schritt ausführen. `dir Cert:\LocalMachine\My`  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen `OverwriteConfiguration` Sie den-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird ein wid-Farm Knoten erstellt. Wenn Sie einen Serverfarm Knoten von Computern erstellen möchten, auf denen SQL Server ausgeführt wird, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein.  
        >   
        > Sie können den folgenden Befehl verwenden, um einer vorhandenen Farm einen Verbund Server hinzuzufügen, der eine Instanz von SQL Server verwendet `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` : wobei der **SQL\_-Hostname\_** der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **SQL der Instanzname\_ist der Name der Instanz von SQL Server. \_** Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von " **\=Data Source <\_SQL\_-Hostname >\=; integrierte Sicherheit true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  
-   Wenn Sie einen Verbund Server mithilfe eines vorhandenen Domänen Benutzerkontos zu einer Farm hinzufügen möchten, gehen Sie wie folgt vor:  
  
    1.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShellCommand-Fenster, und führen Sie dann den folgenden `$fscred = get-credential`Befehl aus:. Geben Sie die Anmelde Informationen für das Domänen Benutzerkonto ein, das Sie für das Verbund Dienst Konto\\im Format Domäne Benutzername verwenden möchten.  
  
    2.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in das Verzeichnis " **mein Speicher" des lokalen Computers\\** importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Fenster Windows PowerShellCommand ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck im **lokalen Computer\\mein Speicher** Verzeichnis aufgelistet.  
  
    3.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen `OverwriteConfiguration` Sie den-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird ein wid-Farm Knoten erstellt. Wenn Sie einen Serverfarm Knoten von Computern erstellen möchten, auf denen SQL Server ausgeführt wird, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein. Mit dem folgenden Befehl können Sie einen Verbund Server zu einer vorhandenen Farm hinzufügen, indem Sie eine Instanz von SQL Server `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` verwenden: wobei der **\_SQL-Hostname\_** der Name des Servers ist, auf dem die Instanz von SQL Server ausgeführt wird. **Der\_SQL\_-Instanzname** ist der Name der Instanz von SQL Server. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von " **\=Data Source <\_SQL\_-Hostname >\=; integrierte Sicherheit true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

