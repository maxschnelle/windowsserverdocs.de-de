---
title: Erstellen der Datei "Cfg.ini"
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 93a73556-22ef-402d-b8d4-582b74c22bcf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 52a4af1e5cadcec1bae46aacb4ac4624c3ecc584
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267651"
---
# <a name="create-the-cfgini-file"></a>Erstellen der Datei "Cfg.ini"

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Die Datei "cfg.ini" dient zum automatischen Installieren des Betriebssystems in folgendem Szenario:  
  
-   Beim Testen der Benutzerfreundlichkeit bei einem vorinstallierten Abbild auf dem Zielcomputer wird der Abschnitt "InitialConfiguration" verwendet, um die Installation in einem beaufsichtigten oder unbeaufsichtigten Modus zu durchlaufen. Informationen zur Vorgehensweise finden Sie unter [Erstellen des Abschnitts "InitialConfiguration"](Create-the-Cfg.ini-File.md#BKMK_CreateInit2).  
  
##  <a name="create-the-initial-configuration-section"></a><a name="BKMK_CreateInit2"></a>Erstellen des Abschnitts "anfängliche Konfiguration"  
 Verwenden Sie den Abschnitt "InitialConfiguration" in der Datei "Cfg.ini", um die Installation in einem beaufsichtigten oder unbeaufsichtigten Modus zu durchlaufen.  
  
#### <a name="to-define-the-initial-configuration-section"></a>So definieren Sie den Abschnitt "InitialConfiguration"  
  
1.  Öffnen Sie die Datei "Cfg.ini", falls vorhanden, in Editor. Erstellen Sie andernfalls eine neue Datei.  
  
2.  Fügen Sie den folgenden Text hinzu, um den Abschnitt "InitialConfiguration" zu erstellen.  
  
    ```  
  
    [InitialConfiguration]  
    ;Optional, display language can only be one of the installed language  
    Language=en-us  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
    ;Optional  
    Locale=en-us  
    ;Optional  
    Country=US  
    ;Optional  
    Keyboard=0409:00000409  
    AcceptEula=true  
    ;This is only required on a server where an OEM EULA has been specified   
    ;by using the OOBE.xml file  
    AcceptOEMEula=true  
    ;Optional. Example: My Company Name  
    CompanyName=EnterCompanyName  
    ServerName=EnterServerName  
    ; Example: CONTOSO  
    NetbiosName=EnterNetbiosDomainName  
    ; Example: contoso.local  
    DNSName=EnterDNSDomain   
    ; Used to set the user name for the domain admin  
    UserName=EnterDomainAdminUserName  
    ;The password has to be strong and at least 8 characters  
    PlainTextPassword=EnterAdminPassword  
    ;. Used to set the user name for the domain standard user account. Ignored in migration mode.  
    StdUserName=EnterDomainStandardUserName  
    ;. The password for the domain standard user account has to be strong and at least 8 characters  
    StdUserPlainTextPassword=EnterStandardUserPassword  
    ;Controls the Watson and automatic update settings  
    Settings=All or Updates or None  
    WebDomainName=www.abc.com  
    TrustedCertFileName=c:\cert\a.pfx  
    TrustedCertPassword=Enteryourpassword  
    EnableVPN=true  
    EnableRWA=true  
    IPv4DNSForwarder=<IPV4Address,IPV4Address,¦>  
    IPv6DNSForwarder=<IPV6Address,IPV6Address,¦>  
    VpnIPv4StartAddress=<IPV4Address>  
    VpnIPv4EndAddress=<IPV4Address>  
    VpnBaseIPv6Address=<IPV6Address>  
    VpnIPv6PrefixLength=<number>  
    ;All these section are optional.  
     [PostOSInstall]  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
  
    IsHosted=true  
    StaticIPv4Address=<IPV4Address>  
    StaticIPv4Gateway=<IPV4Address>  
    StaticIPv4SubnetMask=<IPV4SubnetMask>   
    StaticIPv6Address=<IPV6Address>  
    StaticIPv6SubnetPrefixLength=<number>  
    StaticIPv6Gateway=<IPV6Address>  
    ClientBackupOn=true  
    FileHistoryOn=true  
    LaunchPadHiddenTasks=<Microsoft.LaunchPad.AdminDashboard,Microsoft.LaunchPad.Backup>  
  
    ```  
  
    > [!NOTE]
    >  Die Wahl einer anderen Sprache während der Erstkonfiguration ist nicht möglich. Wenn das System zurückgesetzt wird, ist die Sprache des Betriebssystems wieder diejenige, die ursprünglich installiert wurde.  
  
    |Parametername|Beschreibung des Parameters|  
    |--------------------|---------------------------|  
    |*AcceptEula*|Gibt an, dass der Benutzer die Microsoft-Software-Lizenzbedingungen akzeptiert. Der Wert kann "True" oder "False" sein. Die Installation wird aber nur bei "True" fortgesetzt.|  
    |*AcceptOEMEula*|(Optional) Gibt an, dass der Benutzer die Partner-Lizenzbedingungen akzeptiert. Der Wert kann "True" oder "False" sein. Dieses Feld ist nur erforderlich, wenn der Server bei einem Partner gekauft wurde, der gesonderte Lizenzbedingungen anbietet.|  
    |*CompanyName*|(Optional) Name der Firma. Der Firmenname wird verwendet, um den Server der Firma zuzuordnen und die Geschäftsberichte anzupassen. Er darf höchstens 254 Zeichen lang sein.|  
    |*Country*|(Optional) Zeichenfolge, die das gewünschte Land bzw. die gewünschte Region angibt. Beispiel: "US" für die USA.|  
    |*ServerName*|Mit dem Servernamen wird der Server im Netzwerk eindeutig identifiziert. Der Servername muss die folgenden Kriterien erfüllen:<br /><br /> -Kann bis zu 15 Zeichen lang sein.<br /><br /> -Kann Buchstaben, Ziffern und Bindestriche (-) enthalten.<br /><br /> -Darf nicht mit einem Bindestrich beginnen.<br /><br /> -Darf keine Leerzeichen enthalten.<br /><br /> -Darf nicht nur Ziffern enthalten.<br /><br /> Beispiel: ContosoServer.|  
    |*DNSName*|Eine interne Domäne gruppiert den Server und die Clientcomputer zur gemeinsamen Nutzung einer allgemeinen Datenbank mit Benutzernamen, Kennwörtern und anderen allgemeinen Informationen. Den Benutzern wird der Name zwar angezeigt, wenn sie sich an ihren Computern anmelden, aber er wird nur intern verwendet und darf nicht mit einem Internetdomänennamen verwechselt werden. Der interne Domänenname muss die gleichen Kriterien erfüllen, die für *ServerName* angegeben sind.<br /><br /> Beispiel: contoso.local.|  
    |*NetbiosName*|Mit einem NetBIOS-Namen werden Ressourcen identifiziert, die auf dem Server ausgeführt werden. Er darf höchstens 15 Zeichen lang sein. Beispiel: Contoso.|  
    |*Sprache*|(Optional) Gibt die Anzeigesprache an. Es kann nur eine der installierten Sprachen verwendet werden. Beispiel: "en-us" für Englisch, wie es in den USA verwendet wird.|  
    |*Gebietsschema*|(Optional) Gibt das Datums- und Währungsformat mit einem *LocaleID*-Format an. Beispiel "en-us" für die Anzeige von Währung und Uhrzeit in Englisch und formatiert nach den in den USA geltenden Standards.|  
    |*Tastatur*|Die Tastatur kann eines der beiden folgenden Formate aufweisen:<br /><br /> - **Eingabe Sprache: Tastaturlayout.** Beispielsweise 0409:00000409, wobei "0409" vor dem **:** der Eingabesprache und **00000409** dem Tastaturlayout entsprechen. Die Liste der Tastaturlayouts finden Sie unter dem Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layouts**.<br /><br /> - **Eingabe Sprache: die IME-ID.** Nachstehend finden Sie eine vollständige Liste der IME-IDs.<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {8F 96574e-c86c-4bd6-9666-3F 7327d4cbe8} amharin Input-Methode<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf 79e35e} {FA550B04-5AD7-411F-A5AC-CA038EC515D7} Microsoft Pinyin-Simple fast (Chinesisch vereinfacht)<br /><br /> -{531f -9b4c-4a43-a2aa-960e8f cdc732} {B2F9C502-1742-11D4-9790-0080C882687E} Chinesisch (traditionell)-neues phonetisch<br /><br /> -{531f -9b4c-4a43-a2aa-960e8f cdc732} {4bdf9f 03-c7d3-11D4-B2ab-0080c882687e} Chinesisch (traditionell)-ChangJie<br /><br /> -{531f -9b4c-4a43-a2aa-960e8f cdc732} {6024b45f -5c54-11D4-b921-0080c882687e} Chinesisch (traditionell)-schnell<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {D38EFF65-AA46-4FD5-91A7-67845FB02F5B} traditionelles Chinesisch (traditionell)<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {037b2c25-480c-4d7b027-b69788d6ca6b a} Chinesisch herkömmliches DaYi<br /><br /> -{03b5835l-f 03c-411b-9ce2-aa23e1171e36} {A76C93D9-5523-4E90-AAFA-4DB112F9AC76} Microsoft IME (Japanisch)<br /><br /> -{A028AE76-01B1-46C2-99C4-ACD9858AE02F} {B5FE1F02-D5F2-4445-9C03-C568F23C99A1} Microsoft IME (Koreanisch)<br /><br /> -{A1E2B86B-924A-4D43-80F6-8A820DF7190F} {B60AF051-257A-46BC-B9D3-84DAD819BAFB} Alter Hangul IME (Koreanisch)<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {409c8376-007b-4357-AE8E-26316ee3sb0d} Eingabemethode "Yi"<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {3cab88b7-cc3e-46a6-9765-b772ad7761ff} Eingabemethode "Tigrinya"|  
    |*Einstellungen*|Legt die Benutzerauswahl für Updates fest. Verwenden Sie einen der folgenden Werte:<br /><br /> **-"All** " verwendet Empfohlene Einstellungen.<br /><br /> **-Updates** entsprechen wichtige Updates installieren. Machine Learning<br /><br /> **-None** ist nicht auf Updates überprüfen.|  
    |*User*|: Der Name des neuen Administrator Kontos, das während des Setups erstellt wird. Die Namen von Administrator- und Standardbenutzerkonten müssen die folgenden Kriterien erfüllen:<br /><br /> -Kann bis zu 19 Zeichen lang sein.<br /><br /> -Kann/\ []  &#124; < > + =; nicht enthalten. , ? *<br /><br /> -Darf nicht mit einem-Zeitraum beginnen oder enden.<br /><br /> -Darf nicht zwei aufeinander folgende Zeiträume enthalten.<br /><br /> -Darf nicht mit dem Servernamen oder dem internen Domänen Namen identisch sein.<br /><br /> -Darf nicht mit einem vordefinierten Benutzernamen wie "Administrator" oder "Gast" identisch sein.|  
    |*PlainTextPassword*|Dies ist das Kennwort für das neue Administratorkonto, das während des Setups erstellt wird.<br /><br /> -Muss mindestens acht Zeichen lang sein.<br /><br /> -Muss mindestens drei der vier folgenden Kategorien enthalten:<br /><br /> -Großbuchstaben.<br /><br /> -Kleinbuchstaben.<br /><br /> Zahlen.<br /><br /> MB.|  
    |*StdUserName*|Der Name des neuen Standardbenutzerkontos, das während des Setups erstellt wird. Die Anforderungen finden Sie unter dem *UserName*-Parameter.|  
    |*StdUserPlainTextPassword*|Das Kennwort für das neue Standardbenutzerkonto, das während des Setups erstellt wird.|  
    |WebDomainName|(Optional) Konfigurieren Sie den Internetdomänennamen des Servers. Mit dieser Datei können Sie den Domänennamen entsprechend der für die manuelle Konfiguration verwendeten Methode im Assistenten zum Einrichten von Domänennamen konfigurieren.|  
    |TrustedCertFileName|(Optional) Konfigurieren Sie das vertrauenswürdige Zertifikat für den Domänennamen. Dadurch können Sie ein PFX-Zertifikat hinzufügen, das den privaten Schlüssel enthält.|  
    |TrustedCertPassword|(Optional) Das Kennwort zum Importieren des PFX-Zertifikats.|  
    |EnableVPN|(Optional) Aktivieren Sie VPN standardmäßig.|  
    |VpnIPv4StartAddress|(Optional) Legen Sie die VPN-Startadresse fest.|  
    |VpnIPv4EndAddress|(Optional) Legen Sie die VPN-Endadresse fest.|  
    |VpnBaseIPv6Address|(Optional) Legen Sie die IPV6-Basisadresse für VPN fest.|  
    |VpnIPv6PrefixLength|(Optional) Legen Sie die Präfixlänge der VPN-Adresse (IPv6) fest.|  
    |IsHosted|(Optional) Der Standardwert lautet "False", sofern er nicht angegeben ist. Legen Sie diesen Wert fest, wenn Sie dies in einer Hostumgebung einrichten. Dadurch wird die Routerkonfiguration deaktiviert.|  
    |StaticIPv4Address|(Optional) Geben Sie die statische IP-Adresse an, wenn Sie statt einer dynamischen IP-Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv4Gateway|(Optional) Geben Sie die Standardgatewayadresse an, wenn Sie statt einer dynamischen Adresse eine statische Adresse konfigurieren möchten.|  
    |StaticIPv4SubnetMask|(Optional) Geben Sie die Subnetzmaske an, wenn Sie statt einer dynamischen IP-Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv6Address|(Optional) Geben Sie die IP-Standardadresse an, wenn Sie statt einer dynamischen Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv6SubnetPrefixLength|(Optional) Geben Sie die standardmäßige IPV6-Subnetzpräfixlänge an, wenn Sie statt einer dynamischen eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv6Gateway|(Optional) Geben Sie die Standardgatewayadresse an, wenn Sie statt einer dynamischen eine statische IP-Adresse konfigurieren möchten.|  
    |ClientBackupOn|(Optional) Aktivieren Sie standardmäßig die Clientsicherung, die ausgeführt wird, wenn dem Server neue Clients hinzugefügt werden.|  
    |FileHistoryOn|(Optional) Deaktivieren Sie standardmäßig die Sicherung des Dateiverlaufs, die ausgeführt wird, wenn dem Server neue Clients mit Windows 8 Consumer Preview hinzugefügt werden.|  
    |EnableRWA|Bei der Installation von Windows Server Essentials wird Remote Webzugriff aktiviert, die Routerkonfiguration wird jedoch übersprungen. Dies wird nur bei einer Neuinstallation des Produkts unterstützt. Der Standardwert ist „FALSE“.|  
    |IPv4DNSForwarder|Legen Sie die IPv4-DNS-Weiterleitung fest.|  
    |IPv6DNSForwarder|Legen Sie die IPv6-DNS-Weiterleitung fest.|  
    |LaunchPadHiddenTasks|-(Optional) Sie können den Eintrag "Sicherungs Eintrag" oder "/und Administrator Dashboard" in Launchpad ausblenden.<br /><br /> -So deaktivieren Sie das Dashboard: launchpadhiddentasks = Microsoft. launchpad. admindashboard<br /><br /> -So deaktivieren Sie die Sicherung: launchpadhiddentasks = Microsoft. launchpad. Backup<br /><br /> -So deaktivieren Sie die Sicherung und das Dashboard: launchpadhiddentasks = Microsoft. launchpad. Backup, Microsoft. launchpad. admindashboard|  
  
3.  Speichern Sie die Datei . Stellen Sie sicher, dass Sie die Datei unter dem Namen "Cfg.ini" und nicht unter dem Namen "Cfg.ini.txt" speichern.  
  
    > [!NOTE]
    >  Sie können die Datei auf einem USB-Speicherstick speichern, der für spezielle Phasen der Installation verwendet werden kann. Alternativ können Sie die Datei "Cfg.ini" im Stamm einer beliebigen Festplatte auf dem Zielserver ablegen. Die Codierung für die Datei muss auf ANSI oder Unicode festgelegt werden; UTF-8-Verschlüsselung wird nicht unterstützt.  
  
> [!IMPORTANT]
>  Der Abschnitt "InitialConfiguration" der Datei "Cfg.ini" sollte nur vom Endbenutzer zum Personalisieren des Servers oder für eine Partnerinstallation zum Testen der Benutzerfreundlichkeit des Servers mithilfe einer Antwortdatei für unbeaufsichtigtes Setup verwendet werden. Dieser Abschnitt der Datei dient nicht zum Erstellen des Abbilds.  
  
## <a name="see-also"></a>Weitere Informationen  

 [Einführung in das Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Bilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

