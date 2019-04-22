---
title: Erstellen der Datei "Cfg.ini"
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93a73556-22ef-402d-b8d4-582b74c22bcf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 967db5f36ea27fb04eab9a6682a106ba0072d45d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820121"
---
# <a name="create-the-cfgini-file"></a>Erstellen der Datei "Cfg.ini"

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Die Datei "cfg.ini" dient zum automatischen Installieren des Betriebssystems in folgendem Szenario:  
  
-   Beim Testen der Benutzerfreundlichkeit bei einem vorinstallierten Abbild auf dem Zielcomputer wird der Abschnitt "InitialConfiguration" verwendet, um die Installation in einem beaufsichtigten oder unbeaufsichtigten Modus zu durchlaufen. Weitere Informationen zur Vorgehensweise finden Sie unter [Create the Initial Configuration section](Create-the-Cfg.ini-File.md#BKMK_CreateInit2).  
  
##  <a name="BKMK_CreateInit2"></a> Erstellen der Abschnitts "Initialconfiguration"  
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
  
    |Name des Parameters|Beschreibung des Parameters|  
    |--------------------|---------------------------|  
    |*AcceptEula*|Gibt an, dass der Benutzer die Microsoft-Software-Lizenzbedingungen akzeptiert. Der Wert kann "True" oder "False" sein. Die Installation wird aber nur bei "True" fortgesetzt.|  
    |*AcceptOEMEula*|(Optional) Gibt an, dass der Benutzer die Partner-Lizenzbedingungen akzeptiert. Der Wert kann "True" oder "False" sein. Dieses Feld ist nur erforderlich, wenn der Server bei einem Partner gekauft wurde, der gesonderte Lizenzbedingungen anbietet.|  
    |*CompanyName*|(Optional) Name der Firma. Der Firmenname wird verwendet, um den Server der Firma zuzuordnen und die Geschäftsberichte anzupassen. Er darf höchstens 254 Zeichen lang sein.|  
    |*Country*|(Optional) Zeichenfolge, die das gewünschte Land bzw. die gewünschte Region angibt. Beispiel: "US" für die USA.|  
    |*ServerName*|Mit dem Servernamen wird der Server im Netzwerk eindeutig identifiziert. Der Servername muss die folgenden Kriterien erfüllen:<br /><br /> – Bis zu 15 Zeichen lang Sie können sein.<br /><br /> – Sie können Buchstaben, Zahlen und Bindestriche (-) enthalten.<br /><br /> -Muss nicht mit einem Bindestrich beginnen.<br /><br /> -Muss keine Leerzeichen enthalten.<br /><br /> -Muss nicht nur Zahlen enthalten.<br /><br /> Beispiel: ContosoServer.|  
    |*DNSName*|Eine interne Domäne gruppiert den Server und die Clientcomputer zur gemeinsamen Nutzung einer allgemeinen Datenbank mit Benutzernamen, Kennwörtern und anderen allgemeinen Informationen. Den Benutzern wird der Name zwar angezeigt, wenn sie sich an ihren Computern anmelden, aber er wird nur intern verwendet und darf nicht mit einem Internetdomänennamen verwechselt werden. Der interne Domänenname muss die gleichen Kriterien erfüllen, die für *ServerName* angegeben sind.<br /><br /> Beispiel: contoso.local.|  
    |*NetbiosName*|Mit einem NetBIOS-Namen werden Ressourcen identifiziert, die auf dem Server ausgeführt werden. Er darf höchstens 15 Zeichen lang sein. Beispiel: Contoso.|  
    |*Sprache*|(Optional) Gibt die Anzeigesprache an. Es kann nur eine der installierten Sprachen verwendet werden. Beispiel: "en-us" für Englisch, wie es in den USA verwendet wird.|  
    |*Locale*|(Optional) Gibt das Datums- und Währungsformat mit einem *LocaleID* -Format an. Beispiel "en-us" für die Anzeige von Währung und Uhrzeit in Englisch und formatiert nach den in den USA geltenden Standards.|  
    |*Tastatur*|Die Tastatur kann eines der beiden folgenden Formate aufweisen:<br /><br /> - **Eingabe: Tastaturlayout.** Beispielsweise 0409:00000409, wobei "0409" vor dem **:** der Eingabesprache und **00000409** dem Tastaturlayout entsprechen. Die Liste der Tastaturlayouts finden Sie unter dem Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layouts**.<br /><br /> - **Eingabesprache: die IME-ID..** Nachstehend finden Sie eine vollständige Liste der IME-IDs.<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{8F96574E-C86C-4bd6-9666-3F7327D4CBE8} Amharisch Eingabe-Methode<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf79e35e} {fa550b04-5ad7-411f-a5ac-ca038ec515d7} Microsoft Pinyin – Simple Fast (Chinesisch-vereinfacht)<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{B2F9C502-1742-11D4-9790-0080C882687E} Chinesisch (traditionell) – neue phonetische<br /><br /> - {531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{4BDF9F03-C7D3-11D4-B2AB-0080C882687E}          Chinese (Traditional) - ChangJie<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{6024B45F-5C54-11D4-B921-0080C882687E} Chinesisch (traditionell) – Schnellstart<br /><br /> - {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{D38EFF65-AA46-4FD5-91A7-67845FB02F5B}            Chinese Traditional Array<br /><br /> - {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{037B2C25-480C-4D7F-B027-D6CA6B69788A}            Chinese Traditional DaYi<br /><br /> -{03B5835F-F03C-411B-9CE2-AA23E1171E36}{A76C93D9-5523-4E90-AAFA-4DB112F9AC76} Microsoft IME (Japanisch)<br /><br /> -{A028AE76-01B1-46C2-99C4-ACD9858AE02F}{B5FE1F02-D5F2-4445-9C03-C568F23C99A1} Microsoft IME (Koreanisch)<br /><br /> -{A1E2B86B-924A-4D43-80F6-8A820DF7190F}{B60AF051-257A-46BC-B9D3-84DAD819BAFB} Old Hangul IME (Koreanisch)<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{409C8376-007B-4357-AE8E-26316EE3FB0D} Yi-Eingabe-Methode<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{3CAB88B7-CC3E-46A6-9765-B772AD7761FF} Tigrinya Eingabe-Methode|  
    |*Einstellungen*|Legt die Benutzerauswahl für Updates fest. Verwenden Sie einen der folgenden Werte:<br /><br /> **– Alle** gleich empfohlene Einstellungen verwenden.<br /><br /> **-Aktualisiert die** entspricht nur wichtige Updates. only<br /><br /> **– None** Equals nicht nach Updates suchen.|  
    |*UserName*|– Der Name des neuen Administratorkontos, das während des Setups erstellt wird. Die Namen von Administrator- und Standardbenutzerkonten müssen die folgenden Kriterien erfüllen:<br /><br /> – Bis zu 19 Zeichen lang Sie können sein.<br /><br /> -Dürfen nicht / \ [] &#124; < > + =; , ? *<br /><br /> -Muss Sie nicht starten oder mit einem Punkt enden.<br /><br /> -Muss keine zwei aufeinanderfolgenden Punkte enthalten.<br /><br /> – Der Servername oder die internen Domänennamen identisch sein.<br /><br /> -Identisch mit einem vordefinierten Benutzernamen wie z. B. Administrator oder vom Gast muss nicht.|  
    |*PlainTextPassword*|Dies ist das Kennwort für das neue Administratorkonto, das während des Setups erstellt wird.<br /><br /> -Mindestens acht Zeichen lang muss sein.<br /><br /> -Muss mindestens drei der vier folgenden Kategorien enthalten:<br /><br /> -Großbuchstaben.<br /><br /> -Kleinbuchstaben.<br /><br /> -Zahlen.<br /><br /> -Symbole.|  
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
    |EnableRWA|Sie können bei der Installation von Windows Server Essentials Remote Web Access wird Routerkonfiguration jedoch übersprungen. Dies wird nur bei einer Neuinstallation des Produkts unterstützt. Der Standardwert lautet "False".|  
    |IPv4DNSForwarder|Legen Sie die IPv4-DNS-Weiterleitung fest.|  
    |IPv6DNSForwarder|Legen Sie die IPv6-DNS-Weiterleitung fest.|  
    |LaunchPadHiddenTasks|– (Optional) Sie können den Sicherungseintrag ausblenden oder / und Admin-dashboardeintrag auf dem Launchpad.<br /><br /> – Zum Dashboard zu deaktivieren: LaunchPadHiddenTasks=Microsoft.LaunchPad.AdminDashboard<br /><br /> – Zum Deaktivieren der Sicherung: LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup<br /><br /> -So deaktivieren Sie Sicherung und dashboard LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup,Microsoft.LaunchPad.AdminDashboard|  
  
3.  Speichern Sie die Datei. Stellen Sie sicher, dass Sie die Datei unter dem Namen "Cfg.ini" und nicht unter dem Namen "Cfg.ini.txt" speichern.  
  
    > [!NOTE]
    >  Sie können die Datei auf einem USB-Speicherstick speichern, der für spezielle Phasen der Installation verwendet werden kann. Alternativ können Sie die Datei "Cfg.ini" im Stamm einer beliebigen Festplatte auf dem Zielserver ablegen. Die Codierung für die Datei muss auf ANSI oder Unicode festgelegt werden; UTF-8-Verschlüsselung wird nicht unterstützt.  
  
> [!IMPORTANT]
>  Der Abschnitt "InitialConfiguration" der Datei "Cfg.ini" sollte nur vom Endbenutzer zum Personalisieren des Servers oder für eine Partnerinstallation zum Testen der Benutzerfreundlichkeit des Servers mithilfe einer Antwortdatei für unbeaufsichtigtes Setup verwendet werden. Dieser Abschnitt der Datei dient nicht zum Erstellen des Abbilds.  
  
## <a name="see-also"></a>Siehe auch  

 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erste Schritte mit Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

