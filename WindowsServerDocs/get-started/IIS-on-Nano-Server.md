---
title: IIS unter Nano Server
description: Details zum Konfigurieren von IIS unter Nano Server
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.topic: article
ms.date: 09/06/2017
ms.assetid: 16984724-2d77-4d7b-9738-3dff375ed68c
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: d2522dc94c0d3b68c75e14fec19466529256aad0
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826863"
---
# <a name="iis-on-nano-server"></a>IIS unter Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Ab Windows Server, Version 1709, steht Nano Server nur als [Basis-Betriebssystemimage für Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sieh dir [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahre, was dies bedeutet. 

Sie können die Internet Information Services-Serverrolle (IIS) unter Nano Server installieren, indem Sie den Parameter „-Package“ mit „Microsoft-NanoServer-IIS-Package“ verwenden. Informationen zum Konfigurieren von Nano Server einschließlich der Installation von Paketen finden Sie unter [Install Nano Server (Installieren von Nano Server)](Getting-Started-with-Nano-Server.md).  

In diesem Release von Nano Server sind die folgenden IIS-Features verfügbar:  

|Feature|Standardmäßig aktiviert|  
|-----------|----------------------|  
|**Allgemeine HTTP-Features**||  
|Standarddokument|x|  
|Verzeichnissuche|x|  
|HTTP-Fehler|x|  
|Statischer Inhalt|x|  
|HTTP-Umleitung||  
|**Integrität und Diagnose**||  
|HTTP-Protokollierung|x|  
|Benutzerdefinierte Protokollierung||  
|Anforderungsüberwachung||  
|Ablaufverfolgung||  
|**Leistung**||  
|Komprimierung statischer Inhalte|x|  
|Komprimierung dynamischer Inhalte||  
|**Sicherheit**||  
|Anforderungsfilterung|x|  
|Standardauthentifizierung||  
|Authentifizierung durch Clientzertifikatszuordnung||  
|Digestauthentifizierung||  
|Authentifizierung durch IIS-Clientzertifikatszuordnung||  
|Einschränkungen für IP-Adressen und Domänen||  
|URL-Autorisierung||  
|Windows-Authentifizierung||  
|**Anwendungsentwicklung**||  
|Anwendungsinitialisierung||  
|CGI||  
|ISAPI-Erweiterungen||  
|ISAPI-Filter||  
|Serverseitige Includes||  
|WebSocket-Protokoll||  
|**Verwaltungstools**||  
|IISAdministration-Modul für Windows PowerShell|x|  

Eine Reihe von Artikeln zu anderen Konfigurationen von IIS (z. B. mithilfe von ASP.NET, PHP und Java) sowie andere relevante Inhalte findest du unter [http://iis.net/learn](https://iis.net/learn).  

## <a name="installing-iis-on-nano-server"></a>Installieren von IIS unter Nano Server  
Sie können diese Serverrolle entweder offline (Nano Server deaktiviert) oder online (Nano Server ausgeführt) installieren, aber die Offlineinstallation ist die empfohlene Option.  

Fügen Sie für die Offlineinstallation das Paket mit dem Parameter „-Package“ von „New-NanoServerImage“ wie im folgenden Beispiel hinzu:  

`New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1.vhd -ComputerName Nano1 -Package Microsoft-NanoServer-IIS-Package`  

Wenn Sie über eine vorhandene VHD-Datei verfügen, können Sie IIS offline mit „DISM.exe“ installieren, indem Sie die virtuelle Festplatte einbinden und dann die Option **Add-Package** verwenden.   
In den folgenden Beispielschritten wird davon ausgegangen, dass die Ausführung aus dem durch die Option „BasePath“ angegebenen Verzeichnis erfolgt, das nach der Ausführung von New-NanoServerImage erstellt wurde.  

1.  mkdir mountdir
2.  .\Tools\dism.exe /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
3.  .\Tools\dism.exe /Add-Package /PackagePath:.\packages\Microsoft-NanoServer-IIS-Package.cab /Image:.\mountdir
4.  .\Tools\dism.exe /Add-Package /PackagePath:.\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab /Image:.\mountdir
5.  .\Tools\dism.exe /Unmount-Image /MountDir:.\MountDir /Commit


> [!NOTE]  
> Beachten Sie, dass Schritt 4 das Language Pack hinzufügt (in diesem Beispiel wird EN-US installiert).  

Sie können Nano Server nun mit IIS starten.  

### <a name="installing-iis-on-nano-server-online"></a>Onlineinstallation von IIS unter Nano Server  
Obwohl die Offlineinstallation der Serverrolle empfohlen wird, müssen Sie sie möglicherweise online (bei ausgeführtem Nano Server) in Containerszenarios installieren. Gehen Sie hierzu folgendermaßen vor:  

1.  Kopieren Sie den Ordner „Packages“ vom Installationsmedium lokal auf den Server, auf dem Nano Server ausgeführt wird (z.B. nach „C:\packages“).  

2.  Erstellen Sie eine neue Datei „Unattend.xml“ auf einem anderen Computer, und kopieren Sie diese auf den Nano Server. Sie können diesen XML-Inhalt in die XML-Datei kopieren und einfügen, die Sie erstellt haben:  



```  

    <unattend xmlns=urn:schemas-microsoft-com:unattend>  
    <servicing>  
        <package action=install>  
            <assemblyIdentity name=Microsoft-NanoServer-IIS-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral />  
            <source location=c:\packages\Microsoft-NanoServer-IIS-Package.cab />  
        </package>  
        <package action=install>  
            <assemblyIdentity name=Microsoft-NanoServer-IIS-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=en-US />  
            <source location=c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab />  
        </package>  
    </servicing>  
    <cpi:offlineImage cpi:source= xmlns:cpi=urn:schemas-microsoft-com:cpi />  
</unattend>  
```  




3. Ändern Sie in der neuen, von Ihnen erstellten (bzw. kopierten) XML-Datei den Eintrag „C:\packages“ in das Verzeichnis, in das Sie den Inhalt des Ordners „Packages“ kopiert haben.  

4. Wechseln Sie zu dem Verzeichnis mit der neu erstellten XML-Datei, und führen Sie Folgendes aus:  

   **dism /online /apply-unattend:.\unattend.xml**  


5. Vergewissern Sie sich, dass das IIS-Paket und das zugehörige Language Pack ordnungsgemäß installiert wurden, indem Sie Folgendes ausführen:  

   **dism /online /get-packages**  

   Du solltest den Text „Package Identity: Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~~10.0.14393.1000“ zweimal sehen, einmal für den Versionstyp (Release Type) „Language Pack“ und einmal für den Versionstyp „Feature Pack“.  

6. Starten Sie den W3SVC-Dienst entweder mit **net start w3svc** oder durch einen Neustart des Nano Servers.  

## <a name="starting-iis"></a>Starten von IIS  
Sobald IIS installiert ist und ausgeführt wird, können Webanfragen bedient werden. Stellen Sie sicher, dass IIS ausgeführt wird, indem Sie die IIS-Standardwebseite unter http://\<IP-Adresse des Nano Servers> durchsuchen. Auf einem physischen Computer können Sie die IP-Adresse ermitteln, indem Sie die Wiederherstellungskonsole verwenden. Auf einem virtuellen Computer erhalten Sie die IP-Adresse, indem Sie über die Windows PowerShell-Eingabeaufforderung Folgendes ausführen:  

`Get-VM -name <VM name> | Select -ExpandProperty networkadapters | select IPAddresses`  

Wenn Sie nicht auf die IIS-Standardwebseite zugreifen können, überprüfen Sie erneut die IIS-Installation direkt im Verzeichnis **C:\inetpub** auf dem Nano Server.  

## <a name="enabling-and-disabling-iis-features"></a>Aktivieren und Deaktivieren von IIS-Features  
Eine Reihe von IIS-Features sind standardmäßig aktiviert, wenn Sie die IIS-Rolle installieren (siehe die Tabelle im Abschnitt „Übersicht über IIS unter Nano Server“ in diesem Thema). Sie können zusätzliche Features mithilfe von „DISM.exe“ (de)aktivieren.

Jedes Feature von IIS besteht aus einer Reihe von Konfigurationselementen. Die Windows-Authentifizierung umfasst z.B. diese Elemente:  

|Abschnitt|Konfigurationselemente|  
|-----------|--------------------------|  
|`<globalModules>`|`<add name=WindowsAuthenticationModule image=%windir%\System32\inetsrv\authsspi.dll`|  
|`<modules>`|`<add name=WindowsAuthenticationModule lockItem=true \/>`|  
|`<windowsAuthentication>`|`<windowsAuthentication enabled=false authPersistNonNTLM\=true><providers><add value=Negotiate /><add value=NTLM /><br /></providers><br /></windowsAuthentication>`|  

Der vollständige Satz an untergeordneten IIS-Features ist in Anhang 1 enthalten und die entsprechenden Konfigurationselemente befinden sich in Anhang 2, beide in diesem Thema.  


### <a name="example-installing-windows-authentication"></a>Beispiel: Installieren der Windows-Authentifizierung  

1.  Öffnen Sie auf dem Nano Server eine Konsole für eine Remotesitzung von Windows PowerShell.  

2.  Verwenden Sie `DISM.exe`, um das Modul für die Windows-Authentifizierung zu installieren:

    ```
    dism /Enable-Feature /online /featurename:IIS-WindowsAuthentication /all
    ```

    Der `/all`-Switch installiert alle Features, von denen das ausgewählte Feature abhängt.

### <a name="example-uninstalling-windows-authentication"></a>Beispiel: Deinstallieren der Windows-Authentifizierung  

1.  Öffnen Sie auf dem Nano Server eine Konsole für eine Remotesitzung von Windows PowerShell.  

2.  Verwenden Sie `DISM.exe`, um das Modul für die Windows-Authentifizierung zu deinstallieren:

    ```
    dism /Disable-Feature /online /featurename:IIS-WindowsAuthentication
    ```

## <a name="other-common-iis-configuration-tasks"></a>Andere häufige Aufgaben bei der IIS-Konfiguration  
**Erstellen von Websites**  

Verwenden Sie das folgende Cmdlet:  

`PS D:\> New-IISSite -Name TestSite -BindingInformation *:80:TestSite -PhysicalPath c:\test`  

Sie können anschließend `Get-IISSite` ausführen, um den Zustand der Website zu überprüfen (gibt den Namen der Website, die ID, den Status, den physischen Pfad und die Bindungen zurück).  

**Löschen von Websites**  

Führen Sie `Remove-IISSite -Name TestSite -Confirm:$false` aus.  

**Erstellen virtueller Verzeichnisse**  

Sie können die virtuellen Verzeichnisse mithilfe des von Get-IISServerManager zurückgegebenen IISServerManager-Objekts erstellen, das die Microsoft.Web.Administration.ServerManager-API von .NET verfügbar macht. In diesem Beispiel greifen die Befehle auf das Element „Default Web Site“ der Sammlung „Sites“ und das Stammanwendungselement (/) des Abschnitts „Applications“ zu. Sie rufen anschließend die Add()-Methode der Sammlung „VirtualDirectories“ für dieses Anwendungselement auf, um das neue Verzeichnis zu erstellen:  

```  
PS C:\> $sm = Get-IISServerManager  
PS C:\> $sm.Sites[Default Web Site].Applications[/].VirtualDirectories.Add(/DemoVirtualDir1, c:\test\virtualDirectory1)  
PS C:\> $sm.Sites[Default Web Site].Applications[/].VirtualDirectories.Add(/DemoVirtualDir2, c:\test\virtualDirectory2)  
PS C:\> $sm.CommitChanges()  
```  

**Erstellen von Anwendungspools**  

Sie können Get-IISServerManager ebenso für die Erstellung von Anwendungspools verwenden:  

```  
PS C:\> $sm = Get-IISServerManager  
PS C:\> $sm.ApplicationPools.Add(DemoAppPool)  
```  

**Konfigurieren von HTTPS und Zertifikaten**  

Verwenden Sie das Dienstprogramm „Certoc.exe“ wie in diesem Beispiel zum Importieren von Zertifikaten, wo das Konfigurieren von HTTPS für eine Website auf einem Nano Server gezeigt wird:  

1.  Erstellen Sie auf einem anderen Computer, auf dem Nano Server nicht ausgeführt wird, ein Zertifikat (mit Ihrem eigenen Zertifikatnamen und Kennwort), und exportieren Sie es anschließend nach „C:\temp\test.pfx“.  

    `$newCert = New-SelfSignedCertificate -DnsName www.foo.bar.com -CertStoreLocation cert:\LocalMachine\my`  

    `$mypwd = ConvertTo-SecureString -String YOUR_PFX_PASSWD -Force -AsPlainText`  

    `Export-PfxCertificate -FilePath c:\temp\test.pfx -Cert $newCert -Password $mypwd`  

2.  Kopieren Sie die test.pfx-Datei auf den Nano Server-Computer.  

3.  Importieren Sie das Zertifikat auf dem Nano Server mit diesem Befehl in den Speicher „My“:  

    **certoc.exe -ImportPFX -p YOUR_PFX_PASSWD My c:\temp\test.pfx**  

4.  Rufen Sie den Fingerabdruck dieses neuen Zertifikats (in diesem Beispiel 61E71251294B2A7BB8259C2AC5CF7BA622777E73) mit `Get-ChildItem Cert:\LocalMachine\my` ab.  

5.  Fügen Sie die HTTPS-Bindung mithilfe dieser Windows PowerShell-Befehle auf der Standardwebsite (oder einer anderen Website, auf der Sie die Bindung hinzufügen möchten) hinzu:  

    ```  
    $certificate = get-item Cert:\LocalMachine\my\61E71251294B2A7BB8259C2AC5CF7BA622777E73  
    # Use your actual thumbprint instead of this example  
    $hash = $certificate.GetCertHash()  

    Import-Module IISAdministration  
    $sm = Get-IISServerManager  
    $sm.Sites[Default Web Site].Bindings.Add(*:443:, $hash, My, 0)    # My is the certificate store name  
    $sm.CommitChanges()  
    ```  

    Du kannst auch die Servernamensanzeige (Server Name Indication, SNI) mit einem bestimmten Hostnamen mit der folgenden Syntax verwenden: `$sm.Sites[Default Web Site].Bindings.Add(*:443:www.foo.bar.com, $hash, My, Sni.`.  

## <a name="appendix-1-list-of-iis-sub-features"></a>Anhang 1: Liste der untergeordneten IIS-Features

- IIS-WebServer
- IIS-CommonHttpFeatures
- IIS-StaticContent
- IIS-DefaultDocument
- IIS-DirectoryBrowsing
- IIS-HttpErrors
- IIS-HttpRedirect
- IIS-ApplicationDevelopment
- IIS-CGI
- IIS-ISAPIExtensions
- IIS-ISAPIFilter
- IIS-ServerSideIncludes
- IIS-WebSockets
- IIS-ApplicationInit
- IIS-Security
- IIS-BasicAuthentication
- IIS-WindowsAuthentication
- IIS-DigestAuthentication
- IIS-ClientCertificateMappingAuthentication
- IIS-IISCertificateMappingAuthentication
- IIS-URLAuthorization
- IIS-RequestFiltering
- IIS-IPSecurity
- IIS-CertProvider
- IIS-Performance
- IIS-HttpCompressionStatic
- IIS-HttpCompressionDynamic
- IIS-HealthAndDiagnostics
- IIS-HttpLogging
- IIS-LoggingLibraries
- IIS-RequestMonitor
- IIS-HttpTracing
- IIS-CustomLogging

## <a name="appendix-2-elements-of-http-features"></a>Anhang 2: Elemente von HTTP-Features  
Jedes Feature von IIS besteht aus einer Reihe von Konfigurationselementen. In diesem Anhang werden die Konfigurationselemente aller Features dieser Nano Server-Version aufgeführt.  

### <a name="common-http-features"></a>Allgemeine HTTP-Features  
**Standarddokument**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=DefaultDocumentModule image=%windir%\System32\inetsrv\defdoc.dll />`|  
|`<modules>`|`<add name=DefaultDocumentModule lockItem=true />`|  
|`<handlers>`|`<add name=StaticFile path=* verb=* modules=DefaultDocumentModule resourceType=EiSecther requireAccess=Read />`|  
|`<defaultDocument>`|`<defaultDocument enabled=true><br /><files><br /> <add value=Default.htm /><br />        <add value=Default.asp /><br />        <add value=index.htm /><br />        <add value=index.html /><br />        <add value=iisstart.htm /><br />    </files><br /></defaultDocument>`|  

Der Eintrag `StaticFile <handlers>` ist möglicherweise bereits vorhanden. Fügen Sie dem Attribut \<modules> in diesem Fall einfach durch ein Komma getrennt „DefaultDocumentModule“ hinzu.  

**Verzeichnissuche**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name=DirectoryListingModule image=%windir%\System32\inetsrv\dirlist.dll />`|  
|`<modules>`|`<add name=DirectoryListingModule lockItem=true />`|  
|`<handlers>`|`<add name=StaticFile path=* verb=* modules=DirectoryListingModule resourceType=Either requireAccess=Read />`|  

Der Eintrag `StaticFile <handlers>` ist möglicherweise bereits vorhanden. Fügen Sie dem Attribut \<modules> in diesem Fall einfach durch ein Komma getrennt „DirectoryListingModule“ hinzu.  

**HTTP-Fehler**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name=CustomErrorModule image=%windir%\System32\inetsrv\custerr.dll />`|  
|`<modules>`|`<add name=CustomErrorModule lockItem=true />`|  
|`<httpErrors>`|`<httpErrors lockAttributes=allowAbsolutePathsWhenDelegated,defaultPath><br />    <error statusCode=401    prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=401.htm ><br />    <error statusCode=403 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=403.htm /><br />    <error statusCode=404 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=404.htm /><br />    <error statusCode=405 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=405.htm /><br />    <error statusCode=406 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=406.htm /><br />    <error statusCode=412 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=412.htm /><br />    <error statusCode=500 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=500.htm /><br />    <error statusCode=501 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=501.htm /><br />    <error statusCode=502 prefixLanguageFilePath=%SystemDrive%\inetpub\custerr path=502.htm /><br /></httpErrors>`|  

**Statischer Inhalt**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=StaticFileModule image=%windir%\System32\inetsrv\static.dll />`|  
|`<modules>`|`<add name=StaticFileModule lockItem=true />`|  
|`<handlers>`|`<add name=StaticFile path=* verb=* modules=StaticFileModule resourceType=Either requireAccess=Read />`|  

Der Eintrag `StaticFile \<handlers>` ist möglicherweise bereits vorhanden. Fügen Sie dem Attribut \<modules> in diesem Fall einfach durch ein Komma getrennt „StaticFileModule“ hinzu.  

**HTTP-Umleitung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name=HttpRedirectionModule image=%windir%\System32\inetsrv\redirect.dll />`|  
|`<modules>`|`<add name=HttpRedirectionModule lockItem=true />`|  
|`<httpRedirect>`|`<httpRedirect enabled=false />`|  

### <a name="health-and-diagnostics"></a>Integrität und Diagnose  
**HTTP-Protokollierung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name=HttpLoggingModule image=%windir%\System32\inetsrv\loghttp.dll />`|  
|`<modules>`|`<add name=HttpLoggingModule lockItem=true />`|  
|`<httpLogging>`|`<httpLogging dontLog=false />`|  

**Benutzerdefinierte Protokollierung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=CustomLoggingModule image=%windir%\System32\inetsrv\logcust.dll />`|  
|`<modules>`|`<add name=CustomLoggingModule lockItem=true />`|  

**Anforderungsüberwachung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=RequestMonitorModule image=%windir%\System32\inetsrv\iisreqs.dll />`|  

**Ablaufverfolgung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=TracingModule image=%windir%\System32\inetsrv\iisetw.dll \/><br /><add name=FailedRequestsTracingModule image=%windir%\System32\inetsrv\iisfreb.dll />`|  
|`<modules>`|`<add name=FailedRequestsTracingModule lockItem=true />`|  
|`<traceProviderDefinitions>`|`<traceProviderDefinitions><br />    <add name=WWW Server guid\={3a2a4e84-4c21-4981-ae10-3fda0d9b0f83}><br />        <areas><br />            <clear /><br />            <add name=Authentication value=2 /><br />            <add name=Security value=4 /><br />            <add name=Filter value=8 /><br />            <add name=StaticFile value=16 /><br />            <add name=CGI value=32 /><br />            <add name=Compression value=64 /><br />            <add name=Cache value=128 /><br />            <add name=RequestNotifications value=256 /><br />            <add name=Module value=512 /><br />            <add name=FastCGI value=4096 /><br />            <add name=WebSocket value=16384 /><br />        </areas><br />    </add><br />    <add name=ISAPI Extension guid={a1c2040e-8840-4c31-ba11-9871031a19ea}><br />        <areas><br />            <clear /><br />        </areas><br />    </add><br /></traceProviderDefinitions>`|  

### <a name="performance"></a>Leistung  
**Komprimierung statischer Inhalte**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=StaticCompressionModule image=%windir%\System32\inetsrv\compstat.dll />`|  
|`<modules>`|`<add name=StaticCompressionModule lockItem=true />`|  
|`<httpCompression>`|`<httpCompression directory=%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files><br />    <scheme name=gzip dll=%Windir%\system32\inetsrv\gzip.dll /><br />   <staticTypes><br />        <add mimeType=text/* enabled=true /><br />        <add mimeType=message/* enabled=true /><br />        <add mimeType=application/javascript enabled=true \/><br />        <add mimeType=application/atom+xml enabled=true /><br />        <add mimeType=application/xaml+xml enabled=true /><br />        <add mimeType=\*\* enabled=false /><br />    </staticTypes><br /></httpCompression>`|  

**Komprimierung dynamischer Inhalte**  

|Abschnitt|Konfigurationselemente|  
|-----------|--------------------------|  
|`<globalModules>`|`<add name=DynamicCompressionModule image=%windir%\System32\inetsrv\compdyn.dll />`|  
|`<modules>`|`<add name=DynamicCompressionModule lockItem=true />`|  
|`<httpCompression>`|`<httpCompression directory\=%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files><br />    <scheme name=gzip dll=%Windir%\system32\inetsrv\gzip.dll \/><br />    \<dynamicTypes><br />        <add mimeType=text/* enabled=true \/><br />        <add mimeType=message/* enabled=true /><br />        <add mimeType=application/x-javascript enabled=true /><br />        <add mimeType=application/javascript enabled=true /><br />        <add mimeType=*/* enabled=false /><br />    <\/dynamicTypes><br /></httpCompression>`|  

### <a name="security"></a>Sicherheit  
**Anforderungsfilterung**  


|       Abschnitt        |                                                                                                                                        Konfigurationselemente                                                                                                                                        |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  `<globalModules>`   |                                                                                                        `<add name=RequestFilteringModule image=%windir%\System32\inetsrv\modrqflt.dll />`                                                                                                        |
|     `<modules>`      |                                                                                                                       `<add name=RequestFilteringModule lockItem=true />`                                                                                                                        |
| \`<requestFiltering> | `<requestFiltering><br />    <fileExtensions allowUnlisted=true applyToWebDAV=true /><br />    <verbs allowUnlisted=true applyToWebDAV=true /><br />    <hiddenSegments applyToWebDAV=true><br />        <add segment=web.config /><br />    </hiddenSegments><br /></requestFiltering>` |

**Standardauthentifizierung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name=BasicAuthenticationModule image=%windir%\System32\inetsrv\authbas.dll />`|  
|`<modules>`|`<add name=WindowsAuthenticationModule lockItem=true />`|  
|`<basicAuthentication>`|`<basicAuthentication enabled=false />`|  

**Authentifizierung durch Clientzertifikatszuordnung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=CertificateMappingAuthentication image=%windir%\System32\inetsrv\authcert.dll />`|  
|`<modules>`|`<add name=CertificateMappingAuthenticationModule lockItem=true />`|  
|`<clientCertificateMappingAuthentication>`|`<clientCertificateMappingAuthentication enabled=false />`|  

**Digestauthentifizierung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=DigestAuthenticationModule image=%windir%\System32\inetsrv\authmd5.dll />`|  
|`<modules>`|`<add name=DigestAuthenticationModule lockItem=true />`|  
|`<other>`|`<digestAuthentication enabled=false />`|  

**Authentifizierung durch IIS-Clientzertifikatszuordnung**  


|                  Abschnitt                   |                                         Konfigurationselemente                                         |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------|
|             `<globalModules>`              | `<add name=CertificateMappingAuthenticationModule image=%windir%\System32\inetsrv\authcert.dll />` |
|                `<modules>`                 |               `<add name=CertificateMappingAuthenticationModule lockItem=true `/>\`                |
| `<clientCertificateMappingAuthentication>` |                      `<clientCertificateMappingAuthentication enabled=false />`                      |

**Einschränkungen für IP-Adressen und Domänen**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|```<add name=IpRestrictionModule image=%windir%\System32\inetsrv\iprestr.dll /><br /><add name=DynamicIpRestrictionModule image=%windir%\System32\inetsrv\diprestr.dll />```|  
|`<modules>`|`<add name=IpRestrictionModule lockItem=true \/><br /><add name=DynamicIpRestrictionModule lockItem=true \/>`|  
|`<ipSecurity>`|`<ipSecurity allowUnlisted=true />`|  

**URL-Autorisierung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=UrlAuthorizationModule image=%windir%\System32\inetsrv\urlauthz.dll />`|  
|`<modules>`|`<add name=UrlAuthorizationModule lockItem=true />`|  
|`<authorization>`|`<authorization><br />    <add accessType=Allow users=* /><br /></authorization>`|  

**Windows-Authentifizierung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name=WindowsAuthenticationModule image=%windir%\System32\inetsrv\authsspi.dll />`|  
|`<modules>`|`<add name=WindowsAuthenticationModule lockItem=true />`|  
|`<windowsAuthentication>`|`<windowsAuthentication enabled=false authPersistNonNTLM\=true><br />    <providers><br />        <add value=Negotiate /><br />        <add value=NTLM /><br />    <\providers><br /><\windowsAuthentication><windowsAuthentication enabled=false authPersistNonNTLM\=true><br />    <providers><br />        <add value=Negotiate /><br />        <add value=NTLM /><br />    <\/providers><br /><\/windowsAuthentication>`|  

### <a name="application-development"></a>Anwendungsentwicklung  
**Anwendungsinitialisierung**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=ApplicationInitializationModule image=%windir%\System32\inetsrv\warmup.dll />`|  
|`<modules>`|`<add name=ApplicationInitializationModule lockItem=true />`|  

**CGI**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name=CgiModule image=%windir%\System32\inetsrv\cgi.dll /><br /><add name=FastCgiModule image=%windir%\System32\inetsrv\iisfcgi.dll />`|  
|`<modules>`|`<add name=CgiModule lockItem=true /><br /><add name=FastCgiModule lockItem=true />`|  
|`<handlers>`|`<add name=CGI-exe path=*.exe verb=\* modules=CgiModule resourceType=File requireAccess=Execute allowPathInfo=true />`|  

**ISAPI-Erweiterungen**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name=IsapiModule image=%windir%\System32\inetsrv\isapi.dll />`|  
|`<modules>`|`<add name=IsapiModule lockItem=true />`|  
|`<handlers>`|`<add name=ISAPI-dll path=*.dll verb=* modules=IsapiModule resourceType=File requireAccess=Execute allowPathInfo=true />`|  

**ISAPI-Filter**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name=IsapiFilterModule image=%windir%\System32\inetsrv\filter.dll />`|  
|`<modules>`|`<add name=IsapiFilterModule lockItem=true />`|  

**Serverseitige Include-Dateien**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|  
|`<globalModules>`|<`add name=ServerSideIncludeModule image=%windir%\System32\inetsrv\iis_ssi.dll />`|  
|`<modules>`|`<add name=ServerSideIncludeModule lockItem=true />`|  
|`<handlers>`|`<add name=SSINC-stm path=*.stm verb=GET,HEAD,POST modules=ServerSideIncludeModule resourceType=File \/><br /><add name=SSINC-shtm path=*.shtm verb=GET,HEAD,POST modules=ServerSideIncludeModule resourceType=File /><br /><add name=SSINC-shtml path=*.shtml verb=GET,HEAD,POST modules=ServerSideIncludeModule resourceType=File />`|  
|`<serverSideInclude>`|`<serverSideInclude ssiExecDisable=false />`|  

**WebSocket-Protokoll**  

|Abschnitt|Konfigurationselemente|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name=WebSocketModule image=%windir%\System32\inetsrv\iiswsock.dll />`|  
|`<modules>`|`<add name=WebSocketModule lockItem=true />`|  