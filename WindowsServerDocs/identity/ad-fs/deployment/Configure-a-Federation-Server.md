---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b4cf161d9dfcbeeb467ccb0a83cc260c5299057e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855523"
---
# <a name="configure-a-federation-server"></a>Konfigurieren eines Verbundservers


Nachdem Sie die Active Directory-Verbunddienste (AD FS) \(AD FS\) Rollen Dienst auf Ihrem Computer installiert haben, können Sie diesen Computer als Verbund Server konfigurieren. Sie können eine der folgenden Aktionen ausführen:  
  
-   [Konfigurieren des ersten Verbund Servers in einer neuen Verbund Serverfarm](Configure-a-Federation-Server.md#configure-the-first-federation-server-in-a-new-federation-server-farm)  
  
-   [Hinzufügen eines Verbund Servers zu einer vorhandenen Verbund Serverfarm](Configure-a-Federation-Server.md#add-a-federation-server-to-an-existing-federation-server-farm)  
  
## <a name="configure-the-first-federation-server-in-a-new-federation-server-farm"></a>Konfigurieren des ersten Verbundservers in einer neuen Verbundserverfarm  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>So konfigurieren Sie den ersten Verbund Server in einer neuen Verbund Serverfarm mithilfe des Konfigurations-Assistenten für Active Directory Verbunddienst  
  
> [!NOTE]  
> Stellen Sie sicher, dass Sie über Domänen Administrator Berechtigungen verfügen oder über Domänen Administrator-Anmelde Informationen verfügen, bevor Sie dieses Verfahren ausführen  
  
1.  Klicken Sie im Server-Manager auf der Seite **Dashboard** auf das **Benachrichtigungs**-Flag und dann auf **Konfigurieren Sie den Verbunddienst auf diesem Server**.  
  
    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Willkommen** **Erstellen des ersten Verbundservers in einer Verbundserverfarm** aus, und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **mit AD DS verbinden** ein Konto an, indem Sie Domänen Administrator Berechtigungen für den Active Directory \(AD\) Domäne verwenden, der dieser Computer hinzugefügt wurde, und klicken Sie dann auf **weiter**.  
  
4.  Führen Sie auf der Seite **Diensteigenschaften angeben** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Importieren Sie die PFX-Datei, die die Secure Socket Layer-\(SSL\) Zertifikat und den Schlüssel enthält, die Sie zuvor abgerufen haben. In [Schritt 2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)haben Sie dieses Zertifikat abgerufen und auf den Computer kopiert, den Sie als Verbund Server konfigurieren möchten. Um die PFX-Datei über den Assistenten zu importieren, klicken Sie auf **importieren**, und navigieren Sie dann zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei ein, wenn Sie dazu aufgefordert werden.  
  
    -   Geben Sie einen Namen für den Verbunddienst an. Beispielsweise **fs.contoso.com**. Dieser Name muss mit dem Antragstellernamen oder alternativen Antragstellernamen im Zertifikat übereinstimmen.  
  
    -   Geben Sie einen Anzeigenamen für den Verbunddienst an. Beispielsweise **Contoso Corporation**. Benutzern wird dieser Name auf der Seite Active Directory-Verbunddienste (AD FS) \(AD FS\) anmelden\-angezeigt.  
  
5.  Geben Sie auf der Seite **Dienstkonto angeben** ein Dienstkonto an. Sie können entweder ein vorhandenes Gruppen verwaltetes Dienst Konto \(GMSA\) erstellen oder verwenden oder ein vorhandenes Domänen Benutzerkonto verwenden. Wenn Sie die Option zum Erstellen eines neuen GMSA-Kontos auswählen, geben Sie einen Namen für das neue Konto an. Wenn Sie die Option zum Verwenden eines vorhandenen GMSA-oder Domänen Kontos auswählen, klicken Sie auf **auswählen** , um ein Konto auszuwählen.  
  
    > [!NOTE]  
    > Der Vorteil der Verwendung eines GMSA-Kontos ist die automatische\-aushandeltes Update Feature.  
  
    > [!WARNING]  
    > Wenn Sie ein GMSA-Konto verwenden möchten, muss in Ihrer Umgebung mindestens ein Domänen Controller vorhanden sein, auf dem das Betriebssystem Windows Server 2012 ausgeführt wird.  
    >   
    > Wenn die GMSA-Option deaktiviert ist und eine Fehlermeldung angezeigt wird, z. b. Wenn **Gruppen verwaltete Dienst Konten nicht verfügbar sind, weil der KDS-Stamm Schlüssel nicht festgelegt**wurde, können Sie GMSA in Ihrer Domäne aktivieren, indem Sie den folgenden Windows PowerShell-Befehl auf einem Domänen Controller mit Windows Server 2012 oder höher in Ihrer Active Directory Domäne ausführen: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Kehren Sie dann zum Assistenten zurück, **Klicken Sie auf**zurück, und klicken Sie dann auf **weiter** , um erneut\-die Seite **Dienst Konto angeben** einzugeben. Die GMSA-Option sollte jetzt aktiviert sein. Sie können es auswählen und einen Namen für das GMSA-Konto eingeben, das Sie verwenden möchten.  
  
6.  Geben Sie auf der Seite **Konfigurations Datenbank angeben** eine AD FS Konfigurations Datenbank an, und klicken Sie dann auf **weiter**. Sie können auf diesem Computer eine Datenbank erstellen, indem Sie die interne Windows-Datenbank \(wid\)verwenden, oder Sie können den Speicherort und den Instanznamen Microsoft SQL Server angeben.  
  
    Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  
7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen**, und klicken Sie dann auf **Weiter**.  
  
8.  Überprüfen Sie auf der Seite **Voraussetzungs Prüfungen\-** , ob alle Voraussetzungs Prüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Konfigurieren**.  
  
9. Überprüfen Sie auf der Seite **Ergebnisse** die Ergebnisse, und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurde, und klicken Sie dann auf **weiter, um die Bereitstellung des Verbund Dienstanbieter abzuschließen**. Weitere Informationen finden Sie unter [Nächste Schritte zum Abschließen der AD FS Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-via-windows-powershell"></a>So konfigurieren Sie den ersten Verbundserver in einer neuen Verbundserverfarm über Windows PowerShell  
Sie können eine neue Verbund Serverfarm erstellen, indem Sie entweder ein neues oder ein vorhandenes GMSA-Konto oder ein vorhandenes Domänen Benutzerkonto verwenden.  
  
-   **Wenn Sie einen neuen Verbund Server mit einem neuen GMSA-Konto erstellen möchten, gehen Sie wie folgt vor:**  
  
    > [!IMPORTANT]  
    > Sie benötigen Domänenadministratorberechtigungen, um den ersten Verbundserver in einer neuen Verbundserverfarm zu erstellen.  
  
    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell-Befehlsfenster ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.  
  
    2.  Öffnen Sie auf dem Domänen Controller das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus, um zu überprüfen, ob der KDS-Stamm Schlüssel in Ihrer Domäne erstellt wurde: `Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Wenn Sie nicht erstellt wurde, sodass in der Ausgabe keine Informationen angezeigt werden, führen Sie den folgenden Befehl aus, um den Schlüssel zu erstellen: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`.  
  
    3.  Öffnen Sie auf dem Computer, den Sie als Verbundserver konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie folgenden Befehl aus:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > Das `$` Vorzeichen am Ende des vorherigen Befehls ist erforderlich.  
  
        Um den Wert für `<certificate_thumbprint>`abzurufen, führen Sie `dir Cert:\LocalMachine\My`aus, und wählen Sie dann den Fingerabdruck Ihres SSL-Zertifikats aus. Der Wert von `<federation_service_name>` entspricht dem Namen des Verbunddiensts, z. B. **fs.contoso.com**.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird eine wid-Farm erstellt. Wenn Sie eine SQL Server Server Farm erstellen möchten, müssen Sie über eine Instanz von SQL Server verfügen, die bereits installiert und betriebsbereit ist.  
        >   
        > Sie können den folgenden Befehl verwenden, um den ersten Verbund Server in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"`, wobei **< SQL\_Host\_Name** > der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **< SQL\_Instanz\_Name >** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.  
  
-   **Wenn Sie einen neuen Verbund Server unter Verwendung eines vorhandenen Domänen Benutzerkontos erstellen möchten, gehen Sie folgendermaßen vor:**  
  
    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell-Befehlsfenster ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.  
  
    2.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie dann den folgenden Befehl aus: `$fscred = Get-Credential`. Geben Sie die Anmelde Informationen für das Domänen Benutzerkonto ein, das Sie für das Verbund Dienst Konto im Format Domäne\\Benutzername verwenden möchten.  
  
    3.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus:  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        Wenn Sie den Wert für **< Zertifikat\_Fingerabdruck >** abrufen möchten, führen Sie `dir Cert:\LocalMachine\My`aus, und wählen Sie dann den Fingerabdruck des SSL-Zertifikats aus. Der Wert **< Verbund\_Dienst\_Name >** ist der Name Ihres Verbund Dienstanbieter, z. b. fs.contoso.com.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird eine wid-Farm erstellt. Wenn Sie eine SQL Server-Farm erstellen möchten, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein.  
        >   
        > Sie können den folgenden Befehl verwenden, um den ersten Verbund Server in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, wobei **SQL\_Host\_Name** der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **SQL\_instance\_Name** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  
## <a name="add-a-federation-server-to-an-existing-federation-server-farm"></a>Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie [Schritt 3: Installieren des AD FS Rollen Dienstanbieter](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)abgeschlossen haben, bevor Sie mit einem der in diesem Abschnitt beschriebenen Verfahren beginnen.  
  
> [!IMPORTANT]  
> Stellen Sie sicher, dass Sie ein gültiges SSL-Server Authentifizierungszertifikat erhalten haben, bevor Sie dieses Verfahren ausführen.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>So fügen Sie einer vorhandenen Verbundserverfarm mithilfe des Konfigurations-Assistenten für Active Directory-Verbunddienste einen Verbundserver hinzu  
  
1.  Klicken Sie im Server-Manager auf der Seite **Dashboard** auf das **Benachrichtigungs**-Flag und dann auf **Konfigurieren Sie den Verbunddienst auf diesem Server**.  
  
    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Willkommen** die Option Verbund **Server zu einer Verbund Serverfarm hinzufügen**aus, und klicken Sie dann auf **weiter**.  
  
3.  Geben Sie auf der Seite **mit AD DS verbinden** ein Konto mithilfe von Domänen Administrator Berechtigungen für die AD-Domäne an, der dieser Computer hinzugefügt wurde, und klicken Sie dann auf **weiter**.  
  
4.  Geben Sie auf der Seite **Farm angeben** den Namen des primären Verbund Servers in einer Farm an, die wid verwendet, oder geben Sie den Datenbank-Hostnamen und den Datenbankinstanznamen einer vorhandenen Verbund Server Farm an, die SQL Server verwendet.  
  
    > [!WARNING]  
    > In Windows Server&reg; 2012 R2 gibt es eine Problem Umgehung, um die Standard Instanz von SQL Server anzugeben. bei der die Benutzeroberfläche umgangen wird. Verwenden Sie stattdessen die Schritte in [, um den ersten Verbund Server in einer neuen Verbund Serverfarm über Windows PowerShell zu konfigurieren](Configure-a-Federation-Server.md#BKMK_3).  
  
    > [!IMPORTANT]  
    > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.  
  
5.  Importieren Sie auf der Seite **SSL-Zertifikat angeben** die PFX-Datei mit dem SSL-Zertifikat und-Schlüssel, die Sie zuvor abgerufen haben. Dieses Zertifikat ist das erforderliche Dienstauthentifizierungszertifikat. In [Schritt 2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)haben Sie dieses Zertifikat abgerufen und auf den Computer kopiert, den Sie als Verbund Server konfigurieren möchten. Um die PFX-Datei über den Assistenten zu importieren, klicken Sie auf **importieren** , und navigieren Sie zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei ein, wenn Sie dazu aufgefordert werden.  
  
6.  Geben Sie auf der Seite **Dienst Konto angeben** das gleiche Dienst Konto an, das Sie beim Erstellen des ersten Verbund Servers in der Farm konfiguriert haben. Sie können ein vorhandenes gruppenverwaltetes Dienstkonto oder ein vorhandenes Domänenbenutzerkonto verwenden.  
  
    > [!IMPORTANT]  
    > Das angegebene Konto muss mit dem Konto identisch sein, das auf dem primären Verbund Server in dieser Farm verwendet wurde.  
  
7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen**, und klicken Sie dann auf **Weiter**.  
  
8.  Überprüfen Sie auf der Seite **Voraussetzungs Prüfungen\-** , ob alle Voraussetzungs Prüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Konfigurieren**.  
  
9. Überprüfen Sie auf der Seite **Ergebnisse** die Ergebnisse, und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurde, und klicken Sie dann auf **weiter, um die Bereitstellung des Verbund Dienstanbieter abzuschließen**. Weitere Informationen finden Sie unter [Nächste Schritte zum Abschließen der AD FS Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>So fügen Sie einer vorhandenen Verbundserverfarm mithilfe von Windows PowerShell einen Verbundserver hinzu  
Sie können einer vorhandenen Farm einen Verbund Server hinzufügen, indem Sie entweder ein vorhandenes GMSA-Konto oder ein vorhandenes Domänen Benutzerkonto verwenden.  
  
-   Gehen Sie folgendermaßen vor, wenn Sie einen Verbund Server mit einem vorhandenen GMSA-Konto zu einer Farm hinzufügen möchten:  
  
    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell-Befehlsfenster ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.  
  
    2.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>` ist Ihre Active Directory-Domäne und der Name des GMSA-Kontos in dieser Domäne. `<first_federation_server_hostname>` ist der Hostname des primären Verbund Servers in dieser vorhandenen Farm.  
  
        Sie können den Wert für `<certificate_thumbprint>` abrufen, indem Sie im vorherigen Schritt `dir Cert:\LocalMachine\My` ausführen.  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird ein wid-Farm Knoten erstellt. Wenn Sie einen Serverfarm Knoten von Computern erstellen möchten, auf denen SQL Server ausgeführt wird, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein.  
        >   
        > Sie können den folgenden Befehl verwenden, um einer vorhandenen Farm einen Verbund Server hinzuzufügen, der eine Instanz von SQL Server verwendet: `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, wobei **SQL\_Host\_Name** der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **SQL\_instance\_Name** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  
-   Wenn Sie einen Verbund Server mithilfe eines vorhandenen Domänen Benutzerkontos zu einer Farm hinzufügen möchten, gehen Sie wie folgt vor:  
  
    1.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShellCommand-Fenster, und führen Sie dann den folgenden Befehl aus: `$fscred = get-credential`. Geben Sie die Anmelde Informationen für das Domänen Benutzerkonto ein, das Sie für das Verbund Dienst Konto im Format Domäne\\Benutzername verwenden möchten.  
  
    2.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Fenster Windows PowerShellCommand ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.  
  
    3.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.  
  
        > [!NOTE]  
        > Mit dem vorherigen Befehl wird ein wid-Farm Knoten erstellt. Wenn Sie einen Serverfarm Knoten von Computern erstellen möchten, auf denen SQL Server ausgeführt wird, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein. Sie können den folgenden Befehl verwenden, um einer vorhandenen Farm einen Verbund Server hinzuzufügen, indem Sie eine Instanz von SQL Server verwenden: `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, wobei **SQL\_Host\_Name** der Name des Servers ist, auf dem die Instanz von SQL Server ausgeführt wird, und **SQL\_instance\_Name** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".  
  
        > [!IMPORTANT]  
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.  
  

Nachdem Sie die Active Directory-Verbunddienste (AD FS) \(AD FS\) Rollen Dienst auf Ihrem Computer installiert haben, können Sie diesen Computer als Verbund Server konfigurieren. Sie können eine der folgenden Aktionen ausführen:

-   [Konfigurieren des ersten Verbund Servers in einer neuen Verbund Serverfarm](Configure-a-Federation-Server.md#BKMK_1)

-   [Hinzufügen eines Verbund Servers zu einer vorhandenen Verbund Serverfarm](Configure-a-Federation-Server.md#BKMK_2)

## <a name="configure-the-first-federation-server-in-a-new-federation-server-farm"></a><a name="BKMK_1"></a>Konfigurieren des ersten Verbund Servers in einer neuen Verbund Serverfarm

### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>So konfigurieren Sie den ersten Verbund Server in einer neuen Verbund Serverfarm mithilfe des Konfigurations-Assistenten für Active Directory Verbunddienst

> [!NOTE]
> Stellen Sie sicher, dass Sie über Domänen Administrator Berechtigungen verfügen oder über Domänen Administrator-Anmelde Informationen verfügen, bevor Sie dieses Verfahren ausführen

1.  Klicken Sie im Server-Manager auf der Seite **Dashboard** auf das **Benachrichtigungs**-Flag und dann auf **Konfigurieren Sie den Verbunddienst auf diesem Server**.

    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.

2.  Wählen Sie auf der Seite **Willkommen** **Erstellen des ersten Verbundservers in einer Verbundserverfarm** aus, und klicken Sie dann auf **Weiter**.

3.  Geben Sie auf der Seite **mit AD DS verbinden** ein Konto an, indem Sie Domänen Administrator Berechtigungen für den Active Directory \(AD\) Domäne verwenden, der dieser Computer hinzugefügt wurde, und klicken Sie dann auf **weiter**.

4.  Führen Sie auf der Seite **Diensteigenschaften angeben** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:

    -   Importieren Sie die PFX-Datei, die die Secure Socket Layer-\(SSL\) Zertifikat und den Schlüssel enthält, die Sie zuvor abgerufen haben. In [Schritt 2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)haben Sie dieses Zertifikat abgerufen und auf den Computer kopiert, den Sie als Verbund Server konfigurieren möchten. Um die PFX-Datei über den Assistenten zu importieren, klicken Sie auf **importieren**, und navigieren Sie dann zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei ein, wenn Sie dazu aufgefordert werden.

    -   Geben Sie einen Namen für den Verbunddienst an. Beispielsweise **fs.contoso.com**. Dieser Name muss mit dem Antragstellernamen oder alternativen Antragstellernamen im Zertifikat übereinstimmen.

    -   Geben Sie einen Anzeigenamen für den Verbunddienst an. Beispielsweise **Contoso Corporation**. Benutzern wird dieser Name auf der Seite Active Directory-Verbunddienste (AD FS) \(AD FS\) anmelden\-angezeigt.

5.  Geben Sie auf der Seite **Dienstkonto angeben** ein Dienstkonto an. Sie können entweder ein vorhandenes Gruppen verwaltetes Dienst Konto \(GMSA\) erstellen oder verwenden oder ein vorhandenes Domänen Benutzerkonto verwenden. Wenn Sie die Option zum Erstellen eines neuen GMSA-Kontos auswählen, geben Sie einen Namen für das neue Konto an. Wenn Sie die Option zum Verwenden eines vorhandenen GMSA-oder Domänen Kontos auswählen, klicken Sie auf **auswählen** , um ein Konto auszuwählen.

    > [!NOTE]
    > Der Vorteil der Verwendung eines GMSA-Kontos ist die automatische\-aushandeltes Update Feature.

    > [!WARNING]
    > Wenn Sie ein GMSA-Konto verwenden möchten, muss in Ihrer Umgebung mindestens ein Domänen Controller vorhanden sein, auf dem das Betriebssystem Windows Server 2012 ausgeführt wird.
    >
    > Wenn die GMSA-Option deaktiviert ist und eine Fehlermeldung angezeigt wird, z. b. Wenn **Gruppen verwaltete Dienst Konten nicht verfügbar sind, weil der KDS-Stamm Schlüssel nicht festgelegt**wurde, können Sie GMSA in Ihrer Domäne aktivieren, indem Sie den folgenden Windows PowerShell-Befehl auf einem Domänen Controller mit Windows Server 2012 oder höher in Ihrer Active Directory Domäne ausführen: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Kehren Sie dann zum Assistenten zurück, **Klicken Sie auf**zurück, und klicken Sie dann auf **weiter** , um erneut\-die Seite **Dienst Konto angeben** einzugeben. Die GMSA-Option sollte jetzt aktiviert sein. Sie können es auswählen und einen Namen für das GMSA-Konto eingeben, das Sie verwenden möchten.

6.  Geben Sie auf der Seite **Konfigurations Datenbank angeben** eine AD FS Konfigurations Datenbank an, und klicken Sie dann auf **weiter**. Sie können auf diesem Computer eine Datenbank erstellen, indem Sie die interne Windows-Datenbank \(wid\)verwenden, oder Sie können den Speicherort und den Instanznamen Microsoft SQL Server angeben.

    Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).

    > [!IMPORTANT]
    > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.

7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen**, und klicken Sie dann auf **Weiter**.

8.  Überprüfen Sie auf der Seite **Voraussetzungs Prüfungen\-** , ob alle Voraussetzungs Prüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Konfigurieren**.

9. Überprüfen Sie auf der Seite **Ergebnisse** die Ergebnisse, und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurde, und klicken Sie dann auf **weiter, um die Bereitstellung des Verbund Dienstanbieter abzuschließen**. Weitere Informationen finden Sie unter [Nächste Schritte zum Abschließen der AD FS Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.

### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-via-windows-powershell"></a><a name="BKMK_3"></a>So konfigurieren Sie den ersten Verbund Server in einer neuen Verbund Serverfarm über Windows PowerShell
Sie können eine neue Verbund Serverfarm erstellen, indem Sie entweder ein neues oder ein vorhandenes GMSA-Konto oder ein vorhandenes Domänen Benutzerkonto verwenden.

-   **Wenn Sie einen neuen Verbund Server mit einem neuen GMSA-Konto erstellen möchten, gehen Sie wie folgt vor:**

    > [!IMPORTANT]
    > Sie benötigen Domänenadministratorberechtigungen, um den ersten Verbundserver in einer neuen Verbundserverfarm zu erstellen.

    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell-Befehlsfenster ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.

    2.  Öffnen Sie auf dem Domänen Controller das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus, um zu überprüfen, ob der KDS-Stamm Schlüssel in Ihrer Domäne erstellt wurde: `Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`. Wenn Sie nicht erstellt wurde, sodass in der Ausgabe keine Informationen angezeigt werden, führen Sie den folgenden Befehl aus, um den Schlüssel zu erstellen: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`.

    3.  Öffnen Sie auf dem Computer, den Sie als Verbundserver konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie folgenden Befehl aus:

        ```
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$
        ```

        > [!WARNING]
        > Das `$` Vorzeichen am Ende des vorherigen Befehls ist erforderlich.

        Um den Wert für `<certificate_thumbprint>`abzurufen, führen Sie `dir Cert:\LocalMachine\My`aus, und wählen Sie dann den Fingerabdruck Ihres SSL-Zertifikats aus. Der Wert von `<federation_service_name>` entspricht dem Namen des Verbunddiensts, z. B. **fs.contoso.com**.

        > [!NOTE]
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.

        > [!NOTE]
        > Mit dem vorherigen Befehl wird eine wid-Farm erstellt. Wenn Sie eine SQL Server Server Farm erstellen möchten, müssen Sie über eine Instanz von SQL Server verfügen, die bereits installiert und betriebsbereit ist.
        >
        > Sie können den folgenden Befehl verwenden, um den ersten Verbund Server in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"`, wobei **< SQL\_Host\_Name** > der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **< SQL\_Instanz\_Name >** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".

        > [!IMPORTANT]
        > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.

-   **Wenn Sie einen neuen Verbund Server unter Verwendung eines vorhandenen Domänen Benutzerkontos erstellen möchten, gehen Sie folgendermaßen vor:**

    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell-Befehlsfenster ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.

    2.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie dann den folgenden Befehl aus: `$fscred = Get-Credential`. Geben Sie die Anmelde Informationen für das Domänen Benutzerkonto ein, das Sie für das Verbund Dienst Konto im Format Domäne\\Benutzername verwenden möchten.

    3.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus:

        ```
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred
        ```

        Wenn Sie den Wert für **< Zertifikat\_Fingerabdruck >** abrufen möchten, führen Sie `dir Cert:\LocalMachine\My`aus, und wählen Sie dann den Fingerabdruck des SSL-Zertifikats aus. Der Wert **< Verbund\_Dienst\_Name >** ist der Name Ihres Verbund Dienstanbieter, z. b. fs.contoso.com.

        > [!NOTE]
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.

        > [!NOTE]
        > Mit dem vorherigen Befehl wird eine wid-Farm erstellt. Wenn Sie eine SQL Server-Farm erstellen möchten, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein.
        >
        > Sie können den folgenden Befehl verwenden, um den ersten Verbund Server in einer neuen Farm zu erstellen, die eine Instanz von SQL Server verwendet: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, wobei **SQL\_Host\_Name** der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **SQL\_instance\_Name** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".

        > [!IMPORTANT]
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.

## <a name="add-a-federation-server-to-an-existing-federation-server-farm"></a><a name="BKMK_2"></a>Hinzufügen eines Verbund Servers zu einer vorhandenen Verbund Serverfarm

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie [Schritt 3: Installieren des AD FS Rollen Dienstanbieter](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)abgeschlossen haben, bevor Sie mit einem der in diesem Abschnitt beschriebenen Verfahren beginnen.

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie ein gültiges SSL-Server Authentifizierungszertifikat erhalten haben, bevor Sie dieses Verfahren ausführen.

### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>So fügen Sie einer vorhandenen Verbundserverfarm mithilfe des Konfigurations-Assistenten für Active Directory-Verbunddienste einen Verbundserver hinzu

1.  Klicken Sie im Server-Manager auf der Seite **Dashboard** auf das **Benachrichtigungs**-Flag und dann auf **Konfigurieren Sie den Verbunddienst auf diesem Server**.

    Der **Konfigurations-Assistent für Active Directory-Verbunddienste** wird geöffnet.

2.  Wählen Sie auf der Seite **Willkommen** die Option Verbund **Server zu einer Verbund Serverfarm hinzufügen**aus, und klicken Sie dann auf **weiter**.

3.  Geben Sie auf der Seite **mit AD DS verbinden** ein Konto mithilfe von Domänen Administrator Berechtigungen für die AD-Domäne an, der dieser Computer hinzugefügt wurde, und klicken Sie dann auf **weiter**.

4.  Geben Sie auf der Seite **Farm angeben** den Namen des primären Verbund Servers in einer Farm an, die wid verwendet, oder geben Sie den Datenbank-Hostnamen und den Datenbankinstanznamen einer vorhandenen Verbund Server Farm an, die SQL Server verwendet.

    > [!WARNING]
    > In Windows Server&reg; 2012 R2 gibt es eine Problem Umgehung, um die Standard Instanz von SQL Server anzugeben. bei der die Benutzeroberfläche umgangen wird. Verwenden Sie stattdessen die Schritte in [, um den ersten Verbund Server in einer neuen Verbund Serverfarm über Windows PowerShell zu konfigurieren](Configure-a-Federation-Server.md#BKMK_3).

    > [!IMPORTANT]
    > Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.

5.  Importieren Sie auf der Seite **SSL-Zertifikat angeben** die PFX-Datei mit dem SSL-Zertifikat und-Schlüssel, die Sie zuvor abgerufen haben. Dieses Zertifikat ist das erforderliche Dienstauthentifizierungszertifikat. In [Schritt 2: Registrieren eines SSL-Zertifikats für AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)haben Sie dieses Zertifikat abgerufen und auf den Computer kopiert, den Sie als Verbund Server konfigurieren möchten. Um die PFX-Datei über den Assistenten zu importieren, klicken Sie auf **importieren** , und navigieren Sie zum Speicherort der Datei. Geben Sie das Kennwort für die PFX-Datei ein, wenn Sie dazu aufgefordert werden.

6.  Geben Sie auf der Seite **Dienst Konto angeben** das gleiche Dienst Konto an, das Sie beim Erstellen des ersten Verbund Servers in der Farm konfiguriert haben. Sie können ein vorhandenes gruppenverwaltetes Dienstkonto oder ein vorhandenes Domänenbenutzerkonto verwenden.

    > [!IMPORTANT]
    > Das angegebene Konto muss mit dem Konto identisch sein, das auf dem primären Verbund Server in dieser Farm verwendet wurde.

7.  Überprüfen Sie Ihre Konfigurationsauswahl auf der Seite **Optionen prüfen**, und klicken Sie dann auf **Weiter**.

8.  Überprüfen Sie auf der Seite **Voraussetzungs Prüfungen\-** , ob alle Voraussetzungs Prüfungen erfolgreich abgeschlossen wurden, und klicken Sie dann auf **Konfigurieren**.

9. Überprüfen Sie auf der Seite **Ergebnisse** die Ergebnisse, und überprüfen Sie, ob die Konfiguration erfolgreich abgeschlossen wurde, und klicken Sie dann auf **weiter, um die Bereitstellung des Verbund Dienstanbieter abzuschließen**. Weitere Informationen finden Sie unter [Nächste Schritte zum Abschließen der AD FS Installation](https://go.microsoft.com/fwlink/p/?LinkId=286704). Klicken Sie auf **Schließen**, um den Assistenten zu beenden.

### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>So fügen Sie einer vorhandenen Verbundserverfarm mithilfe von Windows PowerShell einen Verbundserver hinzu
Sie können einer vorhandenen Farm einen Verbund Server hinzufügen, indem Sie entweder ein vorhandenes GMSA-Konto oder ein vorhandenes Domänen Benutzerkonto verwenden.

-   Gehen Sie folgendermaßen vor, wenn Sie einen Verbund Server mit einem vorhandenen GMSA-Konto zu einer Farm hinzufügen möchten:

    1.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Windows PowerShell-Befehlsfenster ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.

    2.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus.

        ```
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>
        ```

        `<domain>\<GMSA_name>` ist Ihre Active Directory-Domäne und der Name des GMSA-Kontos in dieser Domäne. `<first_federation_server_hostname>` ist der Hostname des primären Verbund Servers in dieser vorhandenen Farm.

        Sie können den Wert für `<certificate_thumbprint>` abrufen, indem Sie im vorherigen Schritt `dir Cert:\LocalMachine\My` ausführen.

        > [!NOTE]
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.

        > [!NOTE]
        > Mit dem vorherigen Befehl wird ein wid-Farm Knoten erstellt. Wenn Sie einen Serverfarm Knoten von Computern erstellen möchten, auf denen SQL Server ausgeführt wird, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein.
        >
        > Sie können den folgenden Befehl verwenden, um einer vorhandenen Farm einen Verbund Server hinzuzufügen, der eine Instanz von SQL Server verwendet: `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, wobei **SQL\_Host\_Name** der Name des Servers ist, auf dem SQL Server ausgeführt wird, und **SQL\_instance\_Name** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".

        > [!IMPORTANT]
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.

-   Wenn Sie einen Verbund Server mithilfe eines vorhandenen Domänen Benutzerkontos zu einer Farm hinzufügen möchten, gehen Sie wie folgt vor:

    1.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShellCommand-Fenster, und führen Sie dann den folgenden Befehl aus: `$fscred = get-credential`. Geben Sie die Anmelde Informationen für das Domänen Benutzerkonto ein, das Sie für das Verbund Dienst Konto im Format Domäne\\Benutzername verwenden möchten.

    2.  Stellen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, sicher, dass das erforderliche SSL-Zertifikat in den **lokalen Computer\\mein Speicher** Verzeichnis importiert wurde. Sie können überprüfen, ob das SSL-Zertifikat importiert wurde, indem Sie den folgenden Befehl im Fenster Windows PowerShellCommand ausführen: `dir Cert:\LocalMachine\My`. Das Zertifikat wird durch seinen Fingerabdruck auf dem **lokalen Computer\\meinem Speicher** Verzeichnis aufgelistet.

    3.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus.

        ```
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>
        ```

        > [!NOTE]
        > Wenn dies nicht das erste Mal ist, dass Sie diesen Befehl ausführen, fügen Sie den `OverwriteConfiguration`-Parameter hinzu.

        > [!NOTE]
        > Mit dem vorherigen Befehl wird ein wid-Farm Knoten erstellt. Wenn Sie einen Serverfarm Knoten von Computern erstellen möchten, auf denen SQL Server ausgeführt wird, muss die Instanz von SQL Server bereits installiert und betriebsbereit sein. Sie können den folgenden Befehl verwenden, um einer vorhandenen Farm einen Verbund Server hinzuzufügen, indem Sie eine Instanz von SQL Server verwenden: `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`, wobei **SQL\_Host\_Name** der Name des Servers ist, auf dem die Instanz von SQL Server ausgeführt wird, und **SQL\_instance\_Name** der Name der Instanz von SQL Server ist. Wenn Sie die Standard Instanz von SQL Server verwenden, verwenden Sie einen **sqlConnectionString** -Wert von "**Data Source\=< SQL\_Host\_Name >; Integrated Security\=true**".

        > [!IMPORTANT]
        > Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012 und SQL Server 2014.

## <a name="see-also"></a>Weitere Informationen

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)



