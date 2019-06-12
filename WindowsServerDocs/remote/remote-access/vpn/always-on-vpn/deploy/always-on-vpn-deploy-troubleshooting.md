---
title: Problembehandlung bei Always On VPN
description: Dieses Thema enthält Anweisungen für die Überprüfung und Problembehandlung für die Always On-VPN-Bereitstellung in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d9e0efede39f5a8189dbb3d62033210c393c424d
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749646"
---
# <a name="troubleshoot-always-on-vpn"></a>Problembehandlung bei Always On VPN 

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

Wenn das Always On-VPN-Setup auf Clients eine Verbindung mit dem internen Netzwerk herstellen, ist die Ursache wahrscheinlich ein ungültiges VPN-Zertifikat, falsche NPS-Richtlinien oder Probleme mit der Client-Bereitstellungsskripts oder in Routing und RAS. Der erste Schritt bei der Problembehandlung und Tests Ihrer VPN-Verbindung wird die Kernkomponenten der Always On-VPN-Infrastruktur verstehen. 

Sie können Verbindungsprobleme auf verschiedene Weise zu behandeln. Clientseitige Probleme und Problembehandlung für allgemeine sind die Anwendungsprotokolle auf Clientcomputern von großer Bedeutung. Für die Authentifizierung-spezifische Probleme können die NPS-Protokolls auf dem NPS-Server Sie die Ursache des Problems zu ermitteln.

## <a name="error-codes"></a>Fehlercodes

### <a name="error-code-800"></a>Fehlercode: 800

- **Beschreibung des Fehlers.** Die Remoteverbindung wurde nicht erstellt werden, da die VPN-tunnelfehlern. Der VPN-Server möglicherweise nicht erreichbar. Wenn diese Verbindung versucht, einen L2TP/IPsec-Tunnel verwenden, müssen die Sicherheitsparametern, für IPsec-Aushandlung nicht ordnungsgemäß konfiguriert werden kann.

- **Mögliche Ursache.** Dieser Fehler tritt auf, wenn der Typ des VPN-Tunnel ist **automatische** und der Verbindungsversuch schlägt für alle VPN-Tunnel fehl.

- **Mögliche Lösungen:**

    - Wenn Sie wissen, welchen Tunnel ein, um für Ihre Bereitstellung verwenden, legen Sie den Typ des VPN auf diesen bestimmten Tunneltyp, auf dem VPN-Client.

    - Dazu eine VPN-Verbindung mit einem bestimmten Tunneltyp, die Verbindung werden weiterhin fehlerhaft sein, aber dies führt zu einem mehr Tunnel-spezifische Fehler (z. B. "GRE für PPTP blockiert.").

    - Dieser Fehler tritt auch auf, wenn der VPN-Server nicht erreicht werden oder die tunnelverbindung nicht möglich ist.

- **Stelle sicher:**

    - IKE-Ports (UDP-Ports 500 und 4500) werden nicht blockiert.

    - Die richtigen Zertifikate für IKE, die auf dem Client und dem Server vorhanden sind.

### <a name="error-code-809"></a>Fehlercode: 809

- **Beschreibung des Fehlers.**  Die Netzwerkverbindung zwischen Ihrem Computer und dem VPN-Server konnte nicht hergestellt werden, weil der Remoteserver nicht antwortet. Möglicherweise eine der Netzwerkgeräte (z. B. Firewalls, NAT-Router) zwischen Ihrem Computer und dem remote-Server nicht konfiguriert ist, um VPN-Verbindungen zu ermöglichen. Wenden Sie sich an Ihren Administrator oder Ihren Dienstanbieter, um zu bestimmen, welches Gerät möglicherweise das Problem verursachen.

- **Mögliche Ursache.** Dieser Fehler wird durch die blockierte UDP 500 oder 4500 Ports auf dem VPN-Server oder die Firewall verursacht.

- **Mögliche Lösung.** Stellen Sie sicher, dass UDP-Ports: 500 und 4500 über alle Firewalls zwischen dem Client und den RRAS-Server zulässig sind.

### <a name="error-code-812"></a>Fehlercode: 812

- **Beschreibung des Fehlers.** Keine Verbindung Always On-VPN. Die Verbindung wurde durch eine Richtlinie konfiguriert werden, auf dem RAS-/VPN-Server verhindert. Insbesondere die Authentifizierungsmethode der Server verwendet, um zu überprüfen, ob Ihr Benutzername und Kennwort möglicherweise nicht die in das Verbindungsprofil konfigurierte Authentifizierungsmethode überein. Bitte wenden Sie sich an den Administrator des RAS-Server, und benachrichtigen Sie ihm bzw. ihr für diesen Fehler zu.

- **Mögliche Ursachen:**

    - Die typische Ursache für diesen Fehler ist, dass der NPS eine Bedingung für die Authentifizierung angegeben ist, die der Client nicht erfüllen kann. Z. B. den NPS kann die Verwendung eines Zertifikats zum Sichern der PEAP-Verbindung angeben, aber der Client versucht, EAP-MSCHAP v2 zu verwenden.

    - Ereignisprotokoll 20276 wird in der Ereignisanzeige protokolliert werden, bei der die RRAS basierende VPN-Server-Authentifizierung-protokolleinstellung, die von der VPN-Clientcomputer nicht entspricht.

- **Mögliche Lösung.** Stellen Sie sicher, dass die Clientkonfiguration, das die Bedingungen erfüllt, die auf dem NPS-Server angegeben werden.

### <a name="error-code-13806"></a>Fehlercode: 13806

- **Beschreibung des Fehlers.** IKE wurde ein gültiges Zertifikat gefunden. Wenden Sie sich an Netzwerksicherheitsadministrator über ein gültiges Zertifikat in den entsprechenden Zertifikatspeicher installieren.

- **Mögliche Ursache.** Dieser Fehler tritt normalerweise auf, wenn kein Zertifikat, oder Computer Stammzertifikat auf dem VPN-Server vorhanden ist.

- **Mögliche Lösung.** Stellen Sie sicher, dass die Zertifikate beschrieben, die in dieser Bereitstellung auf dem Clientcomputer und dem VPN-Server installiert sind.

### <a name="error-code-13801"></a>Fehlercode: 13801

- **Beschreibung des Fehlers.** IKE-Authentifizierungsinformationen sind nicht akzeptabel.

- **Mögliche Ursachen.** Dieser Fehler tritt normalerweise auf eine der folgenden Fälle:

    - Das Zertifikat des Computers, für die IKEv2-Überprüfung auf dem RAS-Server verwendet keine **Serverauthentifizierung** unter **Enhanced Key Usage**.

    - Das Zertifikat des Computers auf dem RAS-Server ist abgelaufen.

    - Das Stammzertifikat zum Überprüfen des Zertifikats des RAS-Server nicht vorhanden ist, auf dem Clientcomputer.

    - Die VPN-Server auf dem Clientcomputer nicht entsprechen, die **SubjectName** des Serverzertifikats.

- **Mögliche Lösung.** Stellen Sie sicher, dass das Serverzertifikat enthält **Serverauthentifizierung** unter **Enhanced Key Usage**. Stellen Sie sicher, dass das Zertifikat noch gültig ist. Überprüfen Sie, dass die Zertifizierungsstelle verwendet unter ist **Trusted Root Certification Authorities** auf dem RRAS-Server. Stellen Sie sicher, dass der VPN-Client über den vollqualifizierten Domänennamen des VPN-Server, wie die Darstellung auf dem VPN-Zertifikat des Servers eine Verbindung herstellt.

### <a name="error-code-0x80070040"></a>Fehlercode: 0x80070040

- **Beschreibung des Fehlers.** Das Serverzertifikat verfügt nicht über **Serverauthentifizierung** als eines seiner Einträge der Zertifikat-Nutzung.

- **Mögliche Ursache.** Dieser Fehler kann auftreten, wenn kein Serverzertifikat für die Authentifizierung auf dem RAS-Server installiert ist.

- **Mögliche Lösung.** Stellen Sie sicher, dass das Zertifikat des Computers der RAS-Server für verwendet **IKEv2** hat **Serverauthentifizierung** als einer der Einträge für die Zertifikatverwendung.

### <a name="error-code-0x800b0109"></a>Fehlercode: 0x800B0109

Im Allgemeinen wird die VPN-Client-Computer mit der Active Directory basierende Domäne verknüpft. Wenn Sie Anmeldeinformationen für die Domäne verwenden, um den VPN-Server anmelden, wird das Zertifikat automatisch in der vertrauenswürdigen Stammzertifizierungsstellen installiert zu speichern. Wenn der Computer nicht mit der Domäne angehört, oder wenn Sie eine andere Zertifikatskette verwenden, können Sie jedoch dieses Problem auftreten.

- **Beschreibung des Fehlers.** Eine Zertifikatkette verarbeitet, aber in einem Stammzertifikat, das der Vertrauensanbieter nicht vertraut wird beendet.

- **Mögliche Ursache.** Dieser Fehler kann auftreten, wenn das entsprechende vertrauenswürdigen Stamm-CA-Zertifikat nicht, in der vertrauenswürdigen Stammzertifizierungsstellen installiert ist auf dem Clientcomputer zu speichern.

- **Mögliche Lösung.** Stellen Sie sicher, dass das Stammzertifikat auf dem Clientcomputer im Speicher vertrauenswürdiger Stammzertifizierungsstellen installiert ist.

## <a name="logs"></a>Protokolldateien

### <a name="application-logs"></a>Anwendungsprotokolle

Die Anwendungsprotokolle auf den Clientcomputern Notieren Sie die meisten auf höherer Ebene Details von Ereignissen für VPN-Verbindung.

Suchen Sie nach Ereignissen, aus der Quelle RasClient. Alle Fehlermeldungen zurück, den Fehlercode am Ende der Nachricht. Einige der häufigsten Fehlercodes werden unten genauer beschrieben, aber eine vollständige Liste finden Sie in [Routing und Remote Access-Fehlercodes](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx).

## <a name="nps-logs"></a>NPS-Protokolle

NPS erstellt und speichert die NPS-Accounting-Protokolle. Standardmäßig werden diese in %SystemRoot% gespeichert\\"System32"\\"LogFiles"\\ in eine Datei namens im*XXXX*txt., in denen *XXXX* ist das Datum, das erstellt wurde.

Standardmäßig diese Protokolle werden im CSV-Format, aber sie enthalten nicht, eine Zeile mit der Überschrift. Die Überschriftenzeile ist:

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

Wenn Sie diese Zeile mit der Überschrift als erste Zeile der Protokolldatei einfügen, klicken Sie dann die Datei in Microsoft Excel importieren, die Spalten korrekt mit der Bezeichnung.

Die NPS-Protokolle können bei der Diagnose von Problemen mit der Richtlinie hilfreich sein. Weitere Informationen zu NPS-Protokollen finden Sie unter [Interpretieren von NPS-Format Protokolldateien](https://technet.microsoft.com/library/cc771748.aspx).

## <a name="vpnprofileps1-script-issues"></a>VPN_Profile.ps1 Skriptproblemen

Sind am häufigsten auftretenden Probleme, wenn das VPN_ Profile.ps1-Skript manuell ausführen:

- Verwenden Sie ein Tool für die remote-Verbindung?  Stellen Sie sicher, dass RDP oder eine andere Methode der Remoteverbindung nicht verwenden, wie sie mit der Anmeldung von Benutzer verwirrt.

- Ist der Benutzer ein Administrator des lokalen Computers?  Stellen Sie sicher, dass beim Ausführen des VPN_Profile.ps1-Skripts, die der Benutzer über Administratorrechte verfügt.

- Haben Sie zusätzliche PowerShell-Sicherheitsfunktionen aktiviert? Stellen Sie sicher, dass die PowerShell-Ausführungsrichtlinie nicht durch das Skript blockiert wird. Sie sollten erwägen, eingeschränkten Sprachmodus deaktivieren, wenn vor dem Ausführen des Skripts aktiviert. Sie können die eingeschränkten Sprachmodus aktivieren, nachdem das Skript erfolgreich abgeschlossen wurde.

## <a name="always-on-vpn-client-connection-issues"></a>Always On-VPN-Client-Verbindungsprobleme

Eine kleine fehlerhafte Konfiguration kann dazu führen, dass die Clientverbindung fehlschlägt und kann schwierig sein, um die Ursache zu ermitteln.  Ein Always On-VPN-Client umfasst mehrere Schritte vor dem Herstellen einer Verbindung. Bei der Behandlung von Problemen mit Clientverbindungen, durchlaufen Sie den Prozess der Eliminierung von Duplikaten, durch den folgenden aus:

1. Werden extern Vorlagencomputers ist verbunden? Ein **Whatismyip** Überprüfung sollte eine öffentliche IP-Adresse, die nicht zu der Sie gehört angezeigt.

2. Können Sie den Servernamen der RAS/VPN-eine IP-Adresse auflösen? In **Systemsteuerung** > **Netzwerk** und **Internet** > **Netzwerkverbindungen**, öffnen Sie die Eigenschaften für Ihr VPN-Profil. Der Wert in der **allgemeine** Registerkarte muss öffentlich über DNS aufgelöst werden kann.

3. Können Sie den VPN-Server aus einem externen Netzwerk zugreifen? Öffnen Internet Control Message Protocol (ICMP), um die externe Schnittstelle und pingen den Namen des Remoteclients berücksichtigen. Nachdem ein Ping erfolgreich ist, können Sie entfernen, dass das ICMP-Zulassungsregel.

4. Haben Sie die internen und externen Netzwerkkarten auf dem VPN-Server ordnungsgemäß konfiguriert? Stellen sie in unterschiedlichen Subnetzen befinden? Stellt die externe NIC an die richtige Schnittstelle in Ihrer Firewall eine Verbindung her?

5. Sind UDP 500 und 4500 Ports geöffnet vom Client an externe Schnittstelle des VPN-Servers? Überprüfen Sie die Client-Firewall, Firewall des Servers und alle Hardwarefirewalls. IPSEC verwendet UDP-Port 500, also stellen Sie sicher, dass, die Sie keine IPSec an einer beliebigen Stelle blockiert oder deaktiviert haben.

6. Fehler Überprüfung des Zertifikats ist treten auf? Stellen Sie sicher, dass der NPS-Server verfügt über ein Serverauthentifizierungszertifikat, das IKE-Anforderungen verarbeitet werden können. Stellen Sie sicher, dass Sie die richtige VPN-Server IP-Adresse als NPS-Client angegeben haben. Stellen Sie sicher, dass Sie die Authentifizierung mit PEAP und Eigenschaften für geschütztes EAP sollten nur die Authentifizierung mit einem Zertifikat zulassen. Sie können die NPS-Ereignisprotokolle auf Fehler bei der Authentifizierung überprüfen. Weitere Informationen finden Sie unter [installieren und Konfigurieren der NPS-Server](vpn-deploy-nps.md)

7. Möchten Sie eine Verbindung herstellen, aber keinen Zugriff auf das Internet/lokale Netzwerk? Überprüfen Sie Ihre DHCP-/ VPN-Server-IP-Adresspools für Konfigurationsprobleme.

8. Werden Sie eine Verbindung herstellen und eine gültige interne IP-Adresse jedoch keinen Zugriff auf lokale Ressourcen?  Stellen Sie sicher, dass Clients wissen, wie auf diese Ressourcen zu erhalten. Sie können die VPN-Server zum Weiterleiten von Anforderungen verwenden.

## <a name="azure-ad-conditional-access-connection-issues"></a>Azure AD für bedingten Zugriff-Verbindungsprobleme

### <a name="oops---you-cant-get-to-this-yet"></a>Leider – Sie keinen Zugriff auf diese noch

- **Beschreibung des Fehlers.** Wenn die Richtlinie für bedingten Zugriff ist nicht zufrieden sind, blockieren die VPN-Verbindung, aber eine Verbindung herstellt, nachdem der Benutzer ausgewählt **X** um die Meldung zu schließen.  Auswählen von **OK** bewirkt, dass eine andere Authentifizierungsversuch, die in eine andere "Entschuldigung" endet. Diese Ereignisse werden im AAD-Operational-Ereignisprotokoll des Clients aufgezeichnet.

- **Mögliche Ursache**

  - Der Benutzer hat ein gültiges Clientauthentifizierungszertifikat in ihren persönlichen Zertifikatspeicher zu speichern, die nicht von Azure AD ausgestellt wurde.

  - Das VPN-Profil \<TLSExtensions\> Abschnitt ist, fehlt oder enthält keine enthalten die **\<EKUName\>AAD für den bedingten Zugriff\</EKUName\> \< EKUOID\>1.3.6.1.4.1.311.87 < / EKUOID\>\<EKUName > Bedingter Zugriff für AAD < / EKUName\>\<EKUOID\>1.3.6.1.4.1.311.87 < / EKUOID\>** Einträge. Die \<EKUName > und \<EKUOID > Einträge den VPN-Client informiert, welches Zertifikat aus dem Zertifikatspeicher des Benutzers abgerufen werden soll, wenn das Zertifikat an der VPN-Server übergeben. Der VPN-Client verwendet das gültiges Zertifikat zur Authentifizierung der Client im Zertifikatspeicher des Benutzers und Authentifizierung erfolgreich ist, ohne diesen Schritt. 

  - Der RADIUS-Server (NPS) wurde nicht zum nur Clientzertifikate annimmt, die enthalten konfiguriert die **AAD für den bedingten Zugriff** OID.

- **Mögliche Lösung.** Führen Sie folgende Schritte aus, um diese Schleife Escapezeichen zu versehen:

  1. Führen Sie in Windows PowerShell die **Get-WmiObject** Cmdlet, um die Konfiguration des VPN-Profils zu sichern. 
  2. Überprüfen Sie, ob die  **\<TLSExtensions >** ,  **\<EKUName >** , und  **\<EKUOID >** Abschnitte vorhanden, und zeigt die richtige Der Name "und" OID ".
      
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

  3. Um zu bestimmen, wenn gültige Zertifikate im Zertifikatspeicher des Benutzers vorhanden sind, führen die **Certutil** Befehl:

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
     >Wenn ein Zertifikat vom Aussteller **CN = Microsoft VPN-Stamm-CA-Generation 1** befindet sich im persönlichen Speicher des Benutzers, aber der Benutzer, die sich bereits Zugriff dazu **X** sammeln Sie zum Schließen der Nachricht Entschuldigung CAPI2-Ereignisprotokolle, um zu überprüfen das Zertifikat zur Authentifizierung verwendet wurde, ein gültiges Clientauthentifizierungszertifikat zur Authentifizierung von, das nicht von der Microsoft VPN-Stamm-CA ausgestellt wurde.

  4. Wenn ein gültiges Clientauthentifizierungszertifikat zur Authentifizierung der im privaten Speicher des Benutzers vorhanden ist, ein Verbindungsfehler auftritt (wie gewünscht), nachdem der Benutzer wählt die **X** und, wenn die  **\<TLSExtensions >** ,  **\<EKUName >** , und  **\<EKUOID >** Abschnitte vorhanden, und die richtige Informationen enthalten.
   
     Es wird eine Fehlermeldung mit dem Text "ein Zertifikat nicht gefunden werden konnte, die mit dem Extensible Authenticate-Protokoll verwendet werden können" angezeigt.

### <a name="unable-to-delete-the-certificate-from-the-vpn-connectivity-blade"></a>Beim Löschen des Zertifikats auf dem Blatt des VPN-Verbindung nicht möglich.

- **Beschreibung des Fehlers.** Zertifikate auf dem Blatt "VPN-Konnektivität" können nicht gelöscht werden.

- **Mögliche Ursache.** Das Zertifikat nastaven NA hodnotu **primären**.

- **Mögliche Lösung.**

    1. Wählen Sie das Zertifikat auf dem VPN-Konnektivität.
    2. Klicken Sie unter **primären**Option **keine**, und wählen Sie dann **speichern**.
    3. Wählen Sie das Zertifikat erneut aus, auf dem VPN-Konnektivität.
    4. Klicken Sie auf **Löschen**.
