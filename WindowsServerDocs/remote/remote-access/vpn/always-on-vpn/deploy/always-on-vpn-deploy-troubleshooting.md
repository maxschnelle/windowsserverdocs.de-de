---
title: Problembehandlung bei immer auf VPN
description: Dieses Thema enthält Anweisungen für die Überprüfung und Problembehandlung bei der Always On VPN-Bereitstellung in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 47d22d566407f45fe6ac78931ffea7b5b2854a1c
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067375"
---
# Problembehandlung bei immer auf VPN 

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

Wenn Ihr Always On VPN-Setup fehlschlägt Clients mit dem internen Netzwerk zu verbinden, ist die Ursache wahrscheinlich ein ungültiges VPN-Zertifikat, falsch NPS-Richtlinien oder Probleme mit der Client-Bereitstellungsskripts oder im Routing- und RAS-Dienst. Der erste Schritt bei der Problembehandlung und das Testen Ihrer VPN-Verbindungs ist die Kernkomponenten der Always On VPN-Infrastruktur verstehen. 

Sie können auf verschiedene Arten von Verbindungsproblemen beheben. Für clientseitige Probleme und allgemeine Problembehandlung sind die Anwendungsprotokolle auf Clientcomputern von großer Bedeutung. Für die Authentifizierung-spezifische Fragen unterstützen das Protokoll NPS auf dem Netzwerkrichtlinienserver Sie die Quelle des Problems ermitteln.


## Fehlercodes


### Fehlercode: 800

-   **Beschreibung des Fehlers.** Die Remoteverbindung wurde nicht versucht, da die versuchten VPN-Tunnel fehlgeschlagen ist. Der VPN-Server ist möglicherweise nicht erreichbar. Wenn diese Verbindung versucht, eine L2TP/IPSec-Tunneling verwenden, erforderlich, die Sicherheitsparameter für IPsec-Aushandlung möglicherweise nicht ordnungsgemäß konfiguriert werden.


-   **Mögliche Ursache.** Dieser Fehler tritt auf, wenn der VPN-Tunneltyp **automatisch erfolgt** und keine Verbindung für alle VPN-Tunnel.

-   **Mögliche Lösungen:**

    -   Wenn Sie, welche Tunnel für Ihre Bereitstellung verwenden wissen, legen Sie den Typ des VPN auf diesem bestimmten Tunneltyp auf dem VPN-Client.

    -   Indem Sie eine VPN-Verbindung mit einem bestimmten Tunneltyp machen, die Verbindung weiterhin fehl, und es führt zu einem mehr Tunnel-spezifischen Fehler (z. B. "GRE für PPTP blockiert").

    -   Dieser Fehler tritt auch auf, wenn der VPN-Server kann nicht erreicht werden oder die tunnelverbindung fehlschlägt.

-   **Stelle sicher:**

    -   Die IKE-Ports (UDP-ports500 und 4500) werden nicht blockiert.

    -   Die richtigen Zertifikate für IKE sind auf dem Client und dem Server vorhanden.

### Fehlercode: 809

-   **Beschreibung des Fehlers.**  Die Netzwerkverbindung zwischen Ihrem Computer und dem VPN-Server konnte nicht hergestellt werden, da der Remoteserver nicht reagiert. Dies kann daran liegen eines der Netzwerkgeräte \ (z. B. Routers\ Firewalls, NAT) zwischen Ihrem Computer und dem remote-Server ist nicht so konfiguriert, dass VPN-Verbindungen. Wenden Sie sich an Ihren Administrator oder Dienstanbieter, um zu ermitteln, welches Gerät das Problem verursacht.

-   **Mögliche Ursache.** Dieser Fehler wird durch blockierten UDP 500 oder 4500 Ports auf dem VPN-Server oder die Firewall verursacht.

-   **Mögliche Lösung.** Stellen Sie sicher, dass UDP-ports500 und 4500 über alle Firewalls zwischen dem Client und dem RRAS-Server zulässig sind. 
    
    
### Fehlercode: 812

-   **Beschreibung des Fehlers.** Always On VPN kann keine Verbindung hergestellt werden. Die Verbindung wurde durch eine Richtlinie auf dem RAS-VPN-Server konfiguriert verhindert. Genauer gesagt: die Authentifizierungsmethode der Server verwendet, um Ihre Benutzernamen zu überprüfen und Kennwort entspricht möglicherweise nicht die Authentifizierungsmethode, die in Ihrem Verbindungsprofil konfiguriert. Wenden Sie sich an den Administrator des RAS-Servers, und benachrichtigen Sie gewarnt für diesen Fehler.

-   **Mögliche Ursachen:**

    -  Die übliche Ursache für diesen Fehler ist, dass der NPS eine Authentifizierung Bedingung angegeben hat, die der Client nicht erfüllen kann. Z. B. kann NPS die Verwendung eines Zertifikats zum Sichern der PEAP-Verbindung, aber der Client versucht, EAP-MSCHAPv2 verwenden.

    -  Ereignisprotokoll 20276 wird in der Ereignisanzeige protokolliert, wenn die Einstellung RRAS-basierten VPN-Server Authentication-Protokoll, die von den VPN-Clientcomputer übereinstimmt.

-   **Mögliche Lösung.** Stellen Sie sicher, dass die Clientkonfiguration die Bedingungen entspricht, die auf dem Netzwerkrichtlinienserver angegeben werden.


### Fehlercode: 13806

-   **Beschreibung des Fehlers.** IKE konnte kein gültiges Computerzertifikat finden. Wenden Sie sich an Ihre Netzwerksicherheits-Administrator über ein gültiges Zertifikat im Zertifikatspeicher entsprechenden installieren.

-   **Mögliche Ursache.** Dieser Fehler tritt meist auf, wenn kein Zertifikat oder Computer Stammzertifikat des VPN-Servers vorhanden ist.

-   **Mögliche Lösung.** Stellen Sie sicher, dass die Zertifikate in dieser Bereitstellung beschrieben auf dem Clientcomputer und der VPN-Server installiert sind.

### Fehlercode: 13801

-   **Beschreibung des Fehlers.** Anmeldeinformationen für die IKE-Authentifizierung werden nicht akzeptiert.

-   **Mögliche Ursachen.** Dieser Fehler tritt in der Regel in einem der folgenden Fälle:

    -   Das für IKEv2-Überprüfung auf dem RAS-Server verwendete Computerzertifikat keinen **Serverauthentifizierung** unter **Erweiterte Schlüsselverwendung**.

    -   Computerzertifikat auf dem RAS-Server ist abgelaufen.

    -   Das Stammzertifikat, das RAS-Server-Zertifikat überprüfen nicht auf dem Clientcomputer vorhanden ist.

    -   Den Namen der VPN-Server auf dem Clientcomputer entspricht nicht der **SubjectName** des Serverzertifikats.

-   **Mögliche Lösung.** Stellen Sie sicher, dass das Serverzertifikat **Serverauthentifizierung** unter **Erweiterte Schlüsselverwendung**enthält. Stellen Sie sicher, dass das Zertifikat noch gültig ist. Stellen Sie sicher, dass die Zertifizierungsstelle verwendet unter **Vertrauenswürdige Stammzertifizierungsstellen** auf dem RRAS-Server aufgeführt ist. Stellen Sie sicher, dass der VPN-Client eine Verbindung herstellt, wie mithilfe von den FQDN für den VPN-Server auf dem VPN-Server-Zertifikat dargestellt.


### Fehlercode: 0 x 80070040

-   **Beschreibung des Fehlers.** Das Serverzertifikat hat keine **Serverauthentifizierung** als eine seiner Zertifikat Nutzung Posten.

-   **Mögliche Ursache.** Dieser Fehler kann auftreten, wenn keine Serverauthentifizierungszertifikat auf dem RAS-Server installiert ist.

-   **Mögliche Lösung.** Stellen Sie sicher, dass der RAS-Server für **IKEv2** verwendete Computerzertifikat **Serverauthentifizierung** als einen der Einträge Nutzung Zertifikat verfügt.

### Fehlercode: 0x800B0109

Im Allgemeinen wird der VPN-Client-Computer mit der Active Directory-basierte Domäne verknüpft. Wenn Sie Anmeldeinformationen für Domänen verwenden, der VPN-Server anmelden, wird das Zertifikat automatisch in den vertrauenswürdige Stammzertifizierungsstellen installiert zu speichern. Wenn der Computer nicht mit der Domäne beigetreten ist oder wenn Sie eine andere Zertifikatskette verwenden, können Sie jedoch dieses Problem auftreten.

-   **Beschreibung des Fehlers.** Eine Zertifikatkette verarbeitet, aber in einem Stammzertifikat, das der Vertrauensstellung Anbieter nicht als vertrauenswürdig eingestuft wird beendet.

-   **Mögliche Ursache.** Dieser Fehler kann auftreten, wenn der entsprechende vertrauenswürdigen Stammzertifizierungsstelle nicht in den vertrauenswürdige Stammzertifizierungsstellen installiert ist auf dem Clientcomputer zu speichern.

-   **Mögliche Lösung.** Stellen Sie sicher, dass das Stammzertifikat auf dem Clientcomputer im Speicher für vertrauenswürdige Stammzertifizierungsstellen installiert ist.

## Protokolldateien

### Anwendungsprotokolle

Die Anwendungsprotokolle auf Clientcomputern Notieren Sie die meisten Details der VPN-Verbindungsereignisse auf höherer Ebene.

Suchen Sie nach Ereignissen aus der Quelle RasClient. Sämtliche Fehlermeldungen zurückgeben den Fehlercode am Ende der Nachricht. Eine vollständige Liste steht in [Routing und Remote Access-Fehlercodes](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx), jedoch einige der häufigeren Fehlercodes sind unten aufgeführt.

## NPS-Protokolle
NPS erstellt und speichert die NPS Kontoführungsprotokolle. In der Standardeinstellung werden diese in %SYSTEMROOT%\\System32\\Logfiles\\ in einer Datei namens gespeichert*XXXX.* TXT, wobei *XXXX* das Datum ist die Datei erstellt wurde.

Standardmäßig sind diese Protokolle im CSV-Format, nicht enthalten jedoch eine Überschriftenzeile. Die Kopfzeile ist:

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

Wenn Sie diese Zeile als erste Zeile der Protokolldatei einfügen, importieren die Datei anschließend in Microsoft Excel, die Spalten ordnungsgemäß gekennzeichnet.

Die NPS-Protokolle können bei der Diagnose von Problemen im Zusammenhang mit Gruppenrichtlinien hilfreich sein. Weitere Informationen zu NPS-Protokollen finden Sie unter [Interpretieren NPS Format Datenbankprotokolldateien](https://technet.microsoft.com/library/cc771748.aspx).

## VPN_Profile.ps1 Skript Probleme
Die am häufigsten auftretenden Probleme manuell VPN_ Profile.ps1 ausgeführt gehören:

- Verwenden Sie eine Remoteverbindung-Tool?  Achten Sie darauf, dass Sie nicht RDP oder eine andere Remoteverbindung Methode verwenden, wie sie mit der Benutzer Login Erkennung verwirrt.

- Ist der Benutzer ein Administrator des lokalen Computers?  Stellen Sie sicher, dass während der Ausführung des VPN_Profile.ps1-Skripts, die der Benutzer Administratorrechte verfügt.

- Haben Sie zusätzliche PowerShell-Sicherheitsfeatures aktiviert? Stellen Sie sicher, dass das Skript nicht von PowerShell-Ausführungsrichtlinie blockiert wird. Deaktivieren der eingeschränkten Sprachmodus, wenn aktiviert, bevor Sie das Skript ausführen, sollten. Sie können eingeschränkten Sprachmodus aktivieren, nachdem das Skript erfolgreich abgeschlossen wurde.

## Always On VPN-Client von Verbindungsproblemen
Eine kleine Fehlkonfiguration kann dazu führen, dass die Clientverbindung fehlschlägt und kann schwierig sein, um die Ursache zu ermitteln.  Ein Always On VPN-Client wird vor dem Herstellen einer Verbindung über mehrere Schritte. Bei der Behandlung von Problemen mit Clientverbindungen gehen Sie durch den Prozess der Löschung durch Folgendes:


1. Ist der Vorlage Computer extern verbunden? Eine Überprüfung **Whatismyip** sollte eine öffentliche IP-Adresse angezeigt, die nicht Ihnen gehört.

2. Kann den Namen des RAS/VPN-Servers in eine IP-Adresse werden aufgelöst? In der **Systemsteuerung** \> **Netzwerk** und **Internet** \> **Netzwerkverbindungen**, öffnen Sie die Eigenschaften für die VPN-Profil. Der Wert in der Registerkarte " **Allgemein** " muss öffentlich über DNS aufgelöst werden.

3. Können Sie den VPN-Server über ein externes Netzwerk zugreifen? Öffnen Internet Control Message Protocol (ICMP) in die externe Schnittstelle und den Namen aus der Remoteclient Ping berücksichtigen. Nachdem ein Ping erfolgreich ist, können Sie das ICMP entfernen Regel zulassen.

4. Haben Sie die interne und externe NICs auf dem VPN-Server ordnungsgemäß konfiguriert? Sind sie in unterschiedlichen Subnetzen? Werden die externe Netzwerkkarte kann auf die richtige Schnittstelle auf Ihre Firewall verbunden?

5. Sind UDP 500 und 4500 Ports geöffnet vom Client an externe Schnittstelle der VPN-Server? Überprüfen Sie die Client-Firewall, Server-Firewall und Hardwarefirewalls. IPSEC verwendet UDP-Port 500, so stellen Sie sicher, dass, die Sie nicht IPEC deaktiviert oder blockiert an einer beliebigen Stelle verfügen.

7. Fehlschlägt Überprüfung des Zertifikats? Stellen Sie sicher, dass der NPS-Server ein Serverauthentifizierungszertifikat verfügt, der IKE-Anfragen bedienen können. Stellen Sie sicher, dass Sie die richtigen VPN-Server angegebene IP-Adresse als NPS-Client verfügen. Stellen Sie sicher, dass Sie mit PEAP authentifiziert werden und die geschützte EAP-Eigenschaften sollten nur Authentifizierung mit einem Zertifikat zulassen. Sie können die NPS-Ereignisprotokolle für Authentifizierungsfehlern überprüfen. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von NPS-Servers](vpn-deploy-nps.md)

8. Möchten Sie die Verbindung jedoch haben keinen Zugriff auf das Internet/lokalen Netzwerk? Überprüfen Sie die DHCP-VPN-Server IP-Pools für Probleme mit der Konfiguration.

9.  Sind Sie eine Verbindung herstellen und verfügen über eine gültige interne IP-Adresse aber nicht auf lokale Ressourcen zugreifen?  Stellen Sie sicher, dass Clients auf diese Ressourcen zugreifen können. Sie können den VPN-Server die Weiterleitung von Anfragen verwenden.


## Azure AD bedingten Zugriff von Verbindungsproblemen

### Huch - erhalten Sie nicht auf diese noch

-   **Beschreibung des Fehlers.** Wenn die Richtlinie bedingten Zugriff nicht erfüllt ist, die VPN-Verbindung blockiert, aber nach verbindet klickt der Benutzer ein **X** , um die Nachricht zu schließen.  Durch Klicken auf **OK** wird ein weiterer Authentifizierungsversuch, die in einer anderen _Oops_ Nachricht endet. Diese Ereignisse werden im AAD Operational-Ereignisprotokoll des Clients aufgezeichnet. 

-   **Mögliche Ursache.** 

    - Der Benutzer hat eine gültige Client-Authentifizierungszertifikat in ihren persönlichen Zertifikat zu speichern, die nicht von Azure AD ausgestellt wurde.

    - Das VPN-Profil \ < TLSExtensions\ > Abschnitt ist, fehlt oder enthält keine enthalten die **\ < EKUName\ > AAD bedingte Access\ < / EKUName\ > \ < EKUOID\ > 1.3.6.1.4.1.311.87 < / EKUOID\ > \ < EKUName > AAD Bedingter Zugriff < / EKUName\ > \ < EKUOID\ > 1.3.6.1.4.1.311.87 < / EKUOID\ >** Einträge. Das \ < EKUName > und \ < EKUOID > Einträge feststellen dem VPN-Client das Zertifikat aus dem Zertifikatspeicher des Benutzers abzurufen, wenn das Zertifikat an den VPN-Server übergeben werden. Ohne diese der VPN-Client verwendet das gültiges Clientauthentifizierung Zertifikat im Zertifikatspeicher des Benutzers ist und Authentifizierung erfolgreich war. 

    - Der RADIUS-Server (NPS) wurde nicht konfiguriert, um nur Clientzertifikate akzeptieren, die den **Bedingten Zugriff AAD** OID enthalten.

-   **Mögliche Lösung.** Dieser Schleife zu vermeiden, führen Sie folgende Schritte aus:

    1. Führen Sie in Windows PowerShell das Cmdlet **Get-WmiObject** , um die Konfiguration des VPN-Profils zu sichern. 
    2. Überprüfen Sie, ob die **\ < TLSExtensions >**, **\ < EKUName >**, und **\ < EKUOID >** Abschnitte vorhanden sind, und zeigt den richtigen Namen und OID. 
        ```
        PS C:\> Get-WmiObject -Class MDM_VPNv2_01 -Namespace root\cimv2\mdm\dmmap

        __GENUS                 : 2
        __CLASS                 : MDM_VPNv2_01
        __SUPERCLASS            :
        __DYNASTY               : MDM_VPNv2_01
        __RELPATH               : MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VPNv2"
        __PROPERTY_COUNT        : 10
        __DERIVATION            : {}
        __SERVER                : DERS2
        __NAMESPACE             : root\cimv2\mdm\dmmap
        __PATH                  : \\DERS2\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VP
                                    Nv2"
        AlwaysOn                :
        ByPassForLocal          :
        DnsSuffix               :
        EdpModeId               :
        InstanceID              : AlwaysOnVPN
        LockDown                :
        ParentID                : ./Vendor/MSFT/VPNv2
        ProfileXML              : <VPNProfile><RememberCredentials>false</RememberCredentials><DeviceCompliance><Enabled>true</
                                    Enabled><Sso><Enabled>true</Enabled></Sso></DeviceCompliance><NativeProfile><Servers>derras2.
                                    corp.deverett.info;derras2.corp.deverett.info</Servers><RoutingPolicyType>ForceTunnel</Routin
                                    gPolicyType><NativeProtocolType>Ikev2</NativeProtocolType><Authentication><UserMethod>Eap</Us
                                    erMethod><MachineMethod>Eap</MachineMethod><Eap><Configuration><EapHostConfig
                                    xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config
                                    xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.
                                    com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.mic
                                    rosoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptFor
                                    ServerValidation>true</DisableUserPromptForServerValidation><ServerNames></ServerNames></Serv
                                    erValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Ea
                                    p xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type>
                                    <EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><Credenti
                                    alsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore
                                    ></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUse
                                    rPromptForServerValidation><ServerNames></ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b
                                    1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>fal
                                    se</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/E
                                    apTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://ww
                                    w.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</AcceptServerName><TLSExtens
                                    ions
                                    xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xml
                                    ns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><
                                    EKUName>AAD Conditional
                                    Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList
                                    Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></Client
                                    AuthEKUList></FilteringInfo></TLSExtensions></EapType></Eap><EnableQuarantineChecks>false</En
                                    ableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><Perfo
                                    rmServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"
                                    >false</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisionin
                                    g/MsPeapConnectionPropertiesV2">false</AcceptServerName></PeapExtensions></EapType></Eap></Co
                                    nfig></EapHostConfig></Configuration></Eap></Authentication></NativeProfile></VPNProfile>
        RememberCredentials     : False
        TrustedNetworkDetection :
        PSComputerName          : DERS2
        ```

    3. Um festzustellen, ob es im Zertifikatspeicher des Benutzers gültige Zertifikate sind, führen Sie den **Certutil** -Befehl aus:

       ```
       C:\>certutil -store -user My

        My "Personal"
        ================ Certificate 0 ================
        Serial Number: 32000000265259d0069fa6f205000000000026
        Issuer: CN=corp-DEDC0-CA, DC=corp, DC=deverett, DC=info
         NotBefore: 12/8/2017 8:07 PM
         NotAfter: 12/8/2018 8:07 PM
        Subject: E=winfed@deverett.info, CN=WinFed, OU=Users, OU=Corp, DC=corp, DC=deverett, DC=info
        Certificate Template Name (Certificate Type): User
        Non-root Certificate
        Template: User
        Cert Hash(sha1): a50337ab015d5612b7dc4c1e759d201e74cc2a93
          Key Container = a890fd7fbbfc072f8fe045e680c501cf_5834bfa9-1c4a-44a8-a128-c2267f712336
          Simple container name: te-User-c7bcc4bd-0498-4411-af44-da2257f54387
          Provider = Microsoft Enhanced Cryptographic Provider v1.0
        Encryption test passed
        
        ================ Certificate 1 ================
        Serial Number: 367fbdd7e6e4103dec9b91f93959ac56
        Issuer: CN=Microsoft VPN root CA gen 1
         NotBefore: 12/8/2017 6:24 PM
         NotAfter: 12/8/2017 7:29 PM
        Subject: CN=WinFed@deverett.info
        Non-root Certificate
        Cert Hash(sha1): 37378a1b06dcef1b4d4753f7d21e4f20b18fbfec
          Key Container = 31685cae-af6f-48fb-ac37-845c69b4c097
          Unique container name: bf4097e20d4480b8d6ebc139c9360f02_5834bfa9-1c4a-44a8-a128-c2267f712336
          Provider = Microsoft Software Key Storage Provider
        Private key is NOT exportable
        Encryption test passed
       ```
       >[!NOTE]
       >Wenn ein Zertifikat Ausstellers **CN = Microsoft VPN Stammzertifizierungsstelle Generation 1** ist im persönlichen Speicher des Benutzers, aber der Benutzer Administratorzugriff durch Klicken auf **X** schließen Sie die Nachricht Oops, sammeln CAPI2-Ereignisprotokolle überprüfen das Zertifikat zur Authentifizierung verwendet wurde ein gültige Clientauthentifizierung-Zertifikat, das nicht von der Microsoft-VPN-Stammzertifizierungsstelle ausgestellt wurde.

   4. Wenn ein gültiges Clientauthentifizierung Zertifikat im persönlichen Speicher des Benutzers vorhanden ist, die Verbindung fehlschlägt (wie gewünscht), nachdem der Benutzer auf die **X** klickt und, wenn die **\ < TLSExtensions >**, **\ < EKUName >**, und **\ < EKUOID >** Abschnitte vorhanden sind, und die richtige Informationen enthalten.<p>Die _ein Zertifikat konnte nicht gefunden werden, die mit dem Extensible authentifizieren Protokoll verwendet werden kann._ Fehlermeldung angezeigt wird.

### So löschen Sie das Zertifikat auf dem Blatt VPN-Verbindung nicht möglich

-   **Beschreibung des Fehlers.** Zertifikate auf das VPN-Konnektivität Blatt können nicht gelöscht werden.

-   **Mögliche Ursache.** Das Zertifikat wird auf **primären**festgelegt.

-   **Mögliche Lösung.** 

    1. Wählen Sie im Blatt VPN-Verbindung das Zertifikat.
    2. Wählen Sie unter **primäre** **Nein aus** , und klicken Sie auf **Speichern**.
    3. Wählen Sie das Zertifikat im VPN-Konnektivität Blatt erneut.
    4. Klicken Sie auf **Löschen**.


---
