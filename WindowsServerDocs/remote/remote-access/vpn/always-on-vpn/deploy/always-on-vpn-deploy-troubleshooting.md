---
title: Problembehandlung bei Always On VPN
description: Dieses Thema enthält Anweisungen für die Überprüfung und Problembehandlung Always on VPN-Bereitstellung in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.openlocfilehash: 209567ccd88f4b20f98caecc2a13cc671ef09072
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854023"
---
# <a name="troubleshoot-always-on-vpn"></a>Problembehandlung bei Always On VPN 

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

Wenn Ihr Always on VPN-Setup keine Verbindung zwischen Clients und Ihrem internen Netzwerk herstellt, ist wahrscheinlich ein ungültiges VPN-Zertifikat, falsche NPS-Richtlinien oder Probleme mit den Client Bereitstellungs Skripts oder dem Routing-und RAS-Zugriff aufgetreten. Der erste Schritt bei der Problembehandlung und dem Testen Ihrer VPN-Verbindung ist das Verständnis der Kernkomponenten der Always on-VPN-Infrastruktur. 

Sie können Verbindungsprobleme auf verschiedene Arten beheben. Bei Client seitigen Problemen und der allgemeinen Problembehandlung sind die Anwendungsprotokolle auf Client Computern von großer Bedeutung. Bei Authentifizierungs spezifischen Problemen kann das NPS-Protokoll auf dem NPS-Server Ihnen helfen, die Ursache des Problems zu bestimmen.

## <a name="error-codes"></a>Fehlercodes

### <a name="error-code-800"></a>Fehlercode: 800

- **Fehlerbeschreibung.** Die Remote Verbindung wurde nicht hergestellt, weil bei den versuchten VPN-Tunneln ein Fehler aufgetreten ist. Der VPN-Server ist möglicherweise nicht erreichbar. Wenn diese Verbindung versucht, einen L2TP/IPSec-Tunnel zu verwenden, sind die für die IPsec-Aushandlung erforderlichen Sicherheitsparameter möglicherweise nicht ordnungsgemäß konfiguriert.

- **Mögliche Ursache:** Dieser Fehler tritt auf, wenn der VPN-Tunneltyp **automatisch** ist und der Verbindungsversuch für alle VPN-Tunnel fehlschlägt.

- **Mögliche Lösungen:**

    - Wenn Sie wissen, welcher Tunnel für Ihre Bereitstellung verwendet werden soll, legen Sie den Typ des VPN auf den jeweiligen Tunneltyp auf der VPN-Clientseite fest.

    - Wenn Sie eine VPN-Verbindung mit einem bestimmten Tunneltyp herstellen, schlägt die Verbindung weiterhin fehl, dies führt jedoch zu einem fehlerhaften Tunnel spezifischen Fehler (z. b. "GRE blockiert für PPTP").

    - Dieser Fehler tritt auch auf, wenn der VPN-Server nicht erreicht werden kann oder die Tunnelverbindung nicht hergestellt werden kann.

- **Stelle sicher:**

    - IKE-Ports (UDP-Ports 500 und 4500) sind nicht blockiert.

    - Die richtigen Zertifikate für IKE sind sowohl auf dem Client als auch auf dem Server vorhanden.

### <a name="error-code-809"></a>Fehlercode: 809

- **Fehlerbeschreibung.**  Die Netzwerkverbindung zwischen Ihrem Computer und dem VPN-Server konnte nicht hergestellt werden, da der Remote Server nicht antwortet. Dies liegt möglicherweise daran, dass eines der Netzwerkgeräte (z. b. Firewalls, NAT, Router) zwischen Ihrem Computer und dem Remote Server nicht für das Zulassen von VPN-Verbindungen konfiguriert ist. Wenden Sie sich an Ihren Administrator oder an Ihren Dienstanbieter, um zu ermitteln, welches Gerät das Problem möglicherweise verursacht.

- **Mögliche Ursache:** Dieser Fehler wird durch blockierte UDP 500-oder 4500-Ports auf dem VPN-Server oder der Firewall verursacht.

- **Mögliche Lösung.** Stellen Sie sicher, dass die UDP-Ports 500 und 4500 durch alle Firewalls zwischen dem Client und dem RRAS-Server zulässig sind.

### <a name="error-code-812"></a>Fehlercode: 812

- **Fehlerbeschreibung.** Es kann keine Verbindung mit Always on VPN hergestellt werden. Die Verbindung wurde aufgrund einer Richtlinie, die auf Ihrem RAS/VPN-Server konfiguriert wurde, verhindert. Die Authentifizierungsmethode, die der Server zum Überprüfen Ihres Benutzernamens und Kennworts verwendet hat, stimmt möglicherweise nicht mit der Authentifizierungsmethode, die in Ihrem Verbindungsprofil konfiguriert wurde. Wenden Sie sich an den Administrator des RAS-Servers, und Benachrichtigen Sie ihn über diesen Fehler.

- **Mögliche Ursachen:**

    - Die typische Ursache für diesen Fehler ist, dass der NPS eine Authentifizierungs Bedingung angegeben hat, die der Client nicht erfüllen kann. Beispielsweise kann der NPS die Verwendung eines Zertifikats zum Sichern der PEAP-Verbindung angeben, aber der Client versucht, EAP-MSCHAPv2 zu verwenden.

    - Das Ereignisprotokoll 20276 wird in der Ereignisanzeige protokolliert, wenn die Einstellung RRAS-basiertes VPN-Server-Authentifizierungsprotokoll nicht mit der des VPN-Client Computers identisch ist.

- **Mögliche Lösung.** Stellen Sie sicher, dass Ihre Client Konfiguration mit den Bedingungen übereinstimmt, die auf dem NPS-Server angegeben sind.

### <a name="error-code-13806"></a>Fehlercode: 13806

- **Fehlerbeschreibung.** Ein gültiges Computer Zertifikat konnte von IKE nicht gefunden werden. Wenden Sie sich an den Netzwerk Sicherheitsadministrator, um ein gültiges Zertifikat im entsprechenden Zertifikat Speicher zu installieren.

- **Mögliche Ursache:** Dieser Fehler tritt normalerweise auf, wenn auf dem VPN-Server kein Computer Zertifikat oder Stamm Computer Zertifikat vorhanden ist.

- **Mögliche Lösung.** Stellen Sie sicher, dass die in dieser Bereitstellung beschriebenen Zertifikate sowohl auf dem Client Computer als auch auf dem VPN-Server installiert sind.

### <a name="error-code-13801"></a>Fehlercode: 13801

- **Fehlerbeschreibung.** Die Anmelde Informationen für die IKE-Authentifizierung sind unzulässig.

- **Mögliche Ursachen.** Dieser Fehler tritt in der Regel in einem der folgenden Fälle auf:

    - Das Computer Zertifikat, das für die IKEv2-Überprüfung auf dem RAS-Server verwendet wird, verfügt über keine **Server Authentifizierung** mit **Verbesserter Schlüssel Verwendung**

    - Das Computer Zertifikat auf dem RAS-Server ist abgelaufen.

    - Das Stamm Zertifikat zum Überprüfen des RAS-Serverzertifikats ist auf dem Client Computer nicht vorhanden.

    - Der auf dem Client Computer verwendete VPN-Servername stimmt nicht mit dem **subjetname** des Serverzertifikats identisch.

- **Mögliche Lösung.** Stellen Sie sicher, dass das Serverzertifikat unter **Erweiterte Schlüssel Verwendung**eine **Server Authentifizierung** enthält. Vergewissern Sie sich, dass das Serverzertifikat noch gültig ist. Vergewissern Sie sich, dass die verwendete Zertifizierungsstelle unter **Vertrauenswürdige Stamm Zertifizierungs** stellen auf dem RRAS-Server aufgeführt ist. Überprüfen Sie, ob der VPN-Client eine Verbindung mit dem voll qualifizierten Namen des VPN-Servers herstellt, wie im Zertifikat des VPN-Servers dargestellt.

### <a name="error-code-0x80070040"></a>Fehlercode: 0x80070040

- **Fehlerbeschreibung.** Das Serverzertifikat verfügt nicht über eine **Server Authentifizierung** als eine seiner Zertifikat Verwendungs Einträge.

- **Mögliche Ursache:** Dieser Fehler kann auftreten, wenn auf dem RAS-Server kein Server Authentifizierungszertifikat installiert ist.

- **Mögliche Lösung.** Stellen Sie sicher, dass das Computer Zertifikat, das der RAS-Server für **IKEv2** verwendet, als eine der Zertifikat Verwendungs Einträge **Server Authentifizierung** verwendet.

### <a name="error-code-0x800b0109"></a>Fehlercode: 0x800B0109

Im Allgemeinen wird der VPN-Client Computer mit der Active Directory – basierten Domäne verknüpft. Wenn Sie Domänen Anmelde Informationen für die Anmeldung beim VPN-Server verwenden, wird das Zertifikat automatisch im Speicher Vertrauenswürdige Stamm Zertifizierungsstellen installiert. Wenn der Computer jedoch nicht der Domäne hinzugefügt wird oder wenn Sie eine Alternative Zertifikat Kette verwenden, kann dieses Problem auftreten.

- **Fehlerbeschreibung.** Eine Zertifikat Kette wurde verarbeitet, aber in einem Stamm Zertifikat beendet, dem der Vertrauens Anbieter nicht vertraut.

- **Mögliche Ursache:** Dieser Fehler kann auftreten, wenn das entsprechende Zertifikat der vertrauenswürdigen Stamm Zertifizierungsstelle nicht im Speicher für vertrauenswürdige Stamm Zertifizierungsstellen auf dem Client Computer installiert ist.

- **Mögliche Lösung.** Stellen Sie sicher, dass das Stamm Zertifikat auf dem Client Computer im Speicher vertrauenswürdiger Stamm Zertifizierungsstellen installiert ist.

## <a name="logs"></a>Protokolle

### <a name="application-logs"></a>Anwendungsprotokolle

In den Anwendungs Protokollen auf Client Computern wird der größte Teil der Details der VPN-Verbindungs Ereignisse auf höherer Ebene aufgezeichnet.

Suchen Sie nach Ereignissen aus der Quelle RasClient. Alle Fehlermeldungen geben den Fehlercode am Ende der Nachricht zurück. Einige der gängigeren Fehlercodes sind unten aufgeführt, aber eine vollständige Liste ist in den [Routing-und RAS-Fehlercodes](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx)verfügbar.

## <a name="nps-logs"></a>NPS-Protokolle

NPS erstellt und speichert die NPS-Buchhaltungs Protokolle. Standardmäßig werden diese in% SystemRoot%\\System32\\Logfiles\\ in einer Datei namens in*xxxx*. txt gespeichert, wobei *xxxx* das Datum ist, an dem die Datei erstellt wurde.

Standardmäßig sind diese Protokolle im Format für durch Trennzeichen getrennte Werte enthalten, Sie enthalten jedoch keine Überschriften Zeile. Die Überschriften Zeile lautet:

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

Wenn Sie diese Überschriften Zeile als erste Zeile der Protokolldatei einfügen und die Datei dann in Microsoft Excel importieren, werden die Spalten ordnungsgemäß bezeichnet.

Die NPS-Protokolle können bei der Diagnose von Richtlinien bezogenen Problemen hilfreich sein. Weitere Informationen zu NPS-Protokollen finden Sie unter [Interpretieren von NPS-Daten Bank Format-Protokolldateien](https://technet.microsoft.com/library/cc771748.aspx).

## <a name="vpn_profileps1-script-issues"></a>VPN_Profile. ps1-Skript Probleme

Die häufigsten Probleme beim manuellen Ausführen des VPN_ Profile. ps1-Skripts umfassen Folgendes:

- Verwenden Sie ein Remote Verbindungs Tool?  Stellen Sie sicher, dass Sie RDP oder eine andere Remote Verbindungsmethode nicht verwenden, da Sie mit der Erkennung von Benutzer Anmelde Informationen verwendet wird.

- Ist der Benutzer ein Administrator dieses lokalen Computers?  Stellen Sie sicher, dass beim Ausführen des Skripts VPN_Profile. ps1, dass der Benutzer über Administratorrechte verfügt.

- Verfügen Sie über zusätzliche aktivierte PowerShell-Sicherheitsfeatures? Stellen Sie sicher, dass die PowerShell-Ausführungs Richtlinie das Skript nicht blockiert. Vor dem Ausführen des Skripts sollten Sie ggf. den eingeschränkten Modus deaktivieren. Sie können den eingeschränkten Sprachmodus aktivieren, nachdem das Skript erfolgreich abgeschlossen wurde.

## <a name="always-on-vpn-client-connection-issues"></a>VPN-Client Verbindungsprobleme Always on

Eine geringfügige Fehlkonfiguration kann dazu führen, dass die Client Verbindung fehlschlägt, und die Ursache ist möglicherweise schwierig zu ermitteln.  Ein Always on-VPN-Client durchläuft mehrere Schritte, bevor eine Verbindung hergestellt wird. Gehen Sie bei der Problembehandlung von Client Verbindungsproblemen wie folgt vor:

1. Ist der Vorlagen Computer extern verbunden? Ein **whatismyip** -Scan sollte eine öffentliche IP-Adresse anzeigen, die nicht zu Ihnen gehört.

2. Können Sie den Remote Zugriff/VPN-Servernamen in eine IP-Adresse auflösen? Öffnen Sie in der **Systemsteuerung** > **Netzwerk** -und **Internet** > **Netzwerkverbindungen**die Eigenschaften für das VPN-Profil. Der Wert auf der Registerkarte **Allgemein** sollte durch DNS öffentlich aufgelöst werden können.

3. Können Sie über ein externes Netzwerk auf den VPN-Server zugreifen? Öffnen Sie das ICMP (Internet Control Message Protocol) für die externe Schnittstelle, und Pingen Sie den Namen vom Remote Client. Nachdem ein Ping erfolgreich war, können Sie die ICMP-Zulassungs Regel entfernen.

4. Haben Sie die internen und externen NICs auf dem VPN-Server ordnungsgemäß konfiguriert? Befinden sich diese in unterschiedlichen Subnetzen? Stellt die externe NIC eine Verbindung mit der richtigen Schnittstelle Ihrer Firewall her?

5. Werden UDP 500-und 4500-Ports vom Client für die externe Schnittstelle des VPN-Servers geöffnet? Überprüfen Sie die Client Firewall, die Server Firewall und alle Hardware Firewalls. IPSec verwendet den UDP-Port 500. Stellen Sie daher sicher, dass die IPEC nicht deaktiviert oder an einem beliebigen Speicherort blockiert ist.

6. Schlägt die Zertifikats Überprüfung fehl? Vergewissern Sie sich, dass der NPS-Server über ein Server Authentifizierungszertifikat verfügt, das IKE-Anforderungen bedienen kann Stellen Sie sicher, dass Sie die richtige VPN-Server-IP-Adresse als NPS-Client angegeben haben. Stellen Sie sicher, dass Sie sich mit PEAP authentifizieren, und die geschützten EAP-Eigenschaften sollten nur die Authentifizierung mit einem Zertifikat zulassen. Sie können die NPS-Ereignisprotokolle auf Authentifizierungsfehler überprüfen. Weitere Informationen finden Sie unter [Installieren und Konfigurieren des NPS-Servers](vpn-deploy-nps.md) .

7. Stellen Sie eine Verbindung her, haben aber keinen Zugriff auf das Internet/lokales Netzwerk? Überprüfen Sie die IP-Pools des DHCP/VPN-Servers auf Konfigurationsprobleme.

8. Stellen Sie eine Verbindung her und haben eine gültige interne IP-Adresse, haben aber keinen Zugriff auf lokale Ressourcen?  Überprüfen Sie, ob Clients wissen, wie Sie zu diesen Ressourcen gelangen. Sie können den VPN-Server zum Weiterleiten von Anforderungen verwenden.

## <a name="azure-ad-conditional-access-connection-issues"></a>Azure AD Verbindungsprobleme mit bedingtem Zugriff

### <a name="oops---you-cant-get-to-this-yet"></a>Oops: Sie können dies noch nicht erreichen.

- **Fehlerbeschreibung.** Wenn die Richtlinie für bedingten Zugriff nicht erfüllt wird, wird die VPN-Verbindung blockiert, jedoch wird eine Verbindung hergestellt, nachdem der Benutzer **X** zum Schließen der Nachricht ausgewählt hat.  Wenn Sie **OK** auswählen, wird ein anderer Authentifizierungs Versuch ausgelöst, der in einer anderen "Oops"-Meldung endet. Diese Ereignisse werden im Aad-Betriebs Ereignisprotokoll des Clients aufgezeichnet.

- **Mögliche Ursache**

  - Der Benutzer verfügt über ein gültiges Client Authentifizierungszertifikat im persönlichen Zertifikat Speicher, das nicht von Azure AD ausgestellt wurde.

  - Der Abschnitt VPN-Profil \<tlsextensions\> ist entweder nicht vorhanden oder enthält nicht den **\<ekuname\>Aad Conditional Access\</EKUName\>\<ekuoid\>1.3.6.1.4.1.311.87 </EKUOID\>\<ekuname > Aad Conditional Access </EKUName\>\<ekuoid\>1.3.6.1.4.1.311.87 </EKUOID\>** Einträge. Mit den \<ekuname > und \<ekuoid-> Einträgen wird dem VPN-Client mitgeteilt, welches Zertifikat aus dem Zertifikat Speicher des Benutzers abgerufen werden soll, wenn das Zertifikat an den VPN-Server übergeben wird. Ohne diesen Vorgang verwendet der VPN-Client ein gültiges Client Authentifizierungszertifikat, das sich im Zertifikat Speicher des Benutzers befindet, und die Authentifizierung ist erfolgreich. 

  - Der RADIUS-Server (NPS) wurde nicht so konfiguriert, dass nur Client Zertifikate akzeptiert werden, die die ID des **bedingten Aad-Zugriffs** enthalten.

- **Mögliche Lösung.** Gehen Sie folgendermaßen vor, um diese Schleife zu verwenden:

  1. Führen Sie in Windows PowerShell das Cmdlet **Get-WMIObject** zum Sichern der VPN-Profil Konfiguration aus. 
  2. Vergewissern Sie sich, dass die Abschnitte **\<tlsextensions >** , **\<ekuname >** und **\<ekuoid >** vorhanden sind, und zeigen Sie den richtigen Namen und die OID an.
      
      ```powershell
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

  3. Führen Sie den **certutil** -Befehl aus, um zu bestimmen, ob gültige Zertifikate im Zertifikat Speicher des Benutzers vorhanden sind:

     ```powershell
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
     >Wenn ein Zertifikat vom Aussteller **CN = Microsoft VPN Root CA Gen 1** im persönlichen Speicher des Benutzers vorhanden ist, der Benutzer aber durch Auswählen von **X** zum Schließen der oops-Nachricht Zugriff erhalten hat, erfassen Sie CAPI2-Ereignisprotokolle, um zu überprüfen, ob das Zertifikat, das für die Authentifizierung verwendet wurde, ein gültiges Client Authentifizierungszertifikat war, das von der Microsoft-VPN-Stamm Zertifizierungsstelle

  4. Wenn ein gültiges Client Authentifizierungszertifikat im persönlichen Speicher des Benutzers vorhanden ist, tritt bei der Verbindung ein Fehler auf (wie), nachdem der Benutzer das **X** ausgewählt hat, und wenn die **\<tlsextensions >** , **\<ekuname >** und **\<ekuoid >** Abschnitte vorhanden sind und die richtigen Informationen enthalten.
   
     Es wird eine Fehlermeldung angezeigt, die besagt, dass ein Zertifikat nicht gefunden werden kann, das mit dem Extensible Authenticate-Protokoll verwendet werden kann.

### <a name="unable-to-delete-the-certificate-from-the-vpn-connectivity-blade"></a>Das Zertifikat kann nicht auf dem Blatt "VPN-Konnektivität" gelöscht werden.

- **Fehlerbeschreibung.** Zertifikate auf dem Blatt "VPN-Konnektivität" können nicht gelöscht werden.

- **Mögliche Ursache:** Das Zertifikat ist auf **primär**festgelegt.

- **Mögliche Lösung.**

    1. Wählen Sie auf dem Blatt VPN-Konnektivität das Zertifikat aus.
    2. Wählen Sie unter **primär**die Option **Nein**, und wählen Sie dann **Speichern**aus.
    3. Wählen Sie auf dem Blatt VPN-Konnektivität erneut das Zertifikat aus.
    4. Klicken Sie auf **Löschen**.
