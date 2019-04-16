---
title: Create the Cfg.ini File
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-cfgini-file"></a>Create the Cfg.ini File

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Die Datei cfg.ini dient zum Automatisieren der Installation des Betriebssystems im folgenden Szenario:  
  
-   Beim Testen der Erfahrung der Endbenutzer bei einem vorinstallierten Abbild auf dem Zielcomputer wird der Initial Configuration Section verwendet, um die Installation in einem beaufsichtigten oder unbeaufsichtigten Modus zu durchlaufen. Informationen hierzu finden Sie unter [Erstellen der Initial Configuration Section](Create-the-Cfg.ini-File.md#BKMK_CreateInit2).  
  
##  <a name="BKMK_CreateInit2"></a>Erstellen Sie die Initial Configuration section  
 Verwenden Sie die Erstkonfiguration Abschnittin der Datei cfg.ini, um die Installation in einem beaufsichtigten oder unbeaufsichtigten Modus zu durchlaufen.  
  
#### <a name="to-define-the-initial-configuration-section"></a>Definieren der Initial Configuration section  
  
1.  Öffnen Sie die cfg.ini-Datei im Editor, wenn sie vorhanden ist; Erstellen Sie andernfalls eine neue Datei ein.  
  
2.  Fügen Sie den folgenden Text ein, um einen Abschnitt "InitialConfiguration" zu erstellen.  
  
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
    >  Eine Option zum Auswählen einer anderen Sprache während der Erstkonfiguration wird nicht bereitgestellt. Wenn das System zurückgesetzt wird, werden die Sprache des Betriebssystems die ursprünglich installiert wurde.  
  
    |Name des Parameters|Parameter Beschreibung|  
    |--------------------|---------------------------|  
    |*AcceptEula*|Gibt an, dass der Benutzer die Microsoft Software-Lizenzbedingungen akzeptiert. Der Wert kann "true" oder "false" ist, aber die Installation wird fortgesetzt, nur dann, wenn dies auf "true" festgelegt ist.|  
    |*AcceptOEMEula*|(Optional) Gibt an, dass der Benutzer die Partner-Lizenzbedingungen akzeptiert. Der Wert kann "true" oder "false" ist. Dieses Feld ist erforderlich, nur dann, wenn der Server von einem Partner gekauft wurde, der eine gesonderte Lizenzbedingungen anbietet.|  
    |*CompanyName*|(Optional) Name des Unternehmens. Den Namen Ihres Unternehmens wird auf den Server der Firma zuzuordnen und die Geschäftsberichte anzupassen verwendet. Dies kann bis zu 254 Zeichen lang sein.|  
    |*Land*|(Optional) Zeichenfolge, die das gewünschte Land/die Region darstellt. Beispiel: "US" für die USA.|  
    |*ServerName*|Den Namen des Servers wird der Server im Netzwerk eindeutig identifiziert. Der Name Ihres Servers muss die folgenden Kriterien erfüllen:<br /><br /> -Bis zu 15 Zeichen lang können sein.<br /><br /> -Kann Buchstaben, Zahlen und Bindestriche (-) enthalten.<br /><br /> – Darf nicht mit einem Bindestrich beginnen.<br /><br /> – Müssen keine Leerzeichen enthalten.<br /><br /> – Müssen nicht nur Zahlen enthalten.<br /><br /> Beispiel: ContosoServer.|  
    |*DNS-Name*|Eine interne Domäne gruppiert den Server und die Clientcomputer zusammen, um einer allgemeinen Datenbank mit Benutzernamen, Kennwörtern und anderen allgemeinen Informationen zu nutzen. Benutzer finden Sie unter diesem Namen aus, wenn sie sich an ihren Computern anmelden, aber es wird nur intern verwendet, und es nicht identisch mit einem Internetdomänennamen ist. Der interne Domänenname muss die gleichen Kriterien erfüllen, die für angegeben sind die *ServerName*.<br /><br /> Beispiel: "contoso.Local".|  
    |*NetbiosName*|Ein NetBIOS-Name wird verwendet, um Ressourcen zu identifizieren, die auf dem Server ausgeführt werden. Es kann bis zu 15 Zeichen lang sein. Beispiel: Contoso.|  
    |*Sprache*|(Optional) Gibt die Anzeigesprache an. Es kann nur eine der installierten Sprachen werden. Beispiel: En-us für Englisch in den Vereinigten Staaten verwendet.|  
    |*Gebietsschema*|(Optional) Gibt die Uhrzeit und Währungsformat mit einem *LocaleID* Format. Beispiel: En-us für Währung und Uhrzeit in Englisch angezeigt und formatiert nach den Standards in den Vereinigten Staaten verwendet.|  
    |*Tastatur*|Die Tastatur kann der beiden folgenden Formate aufweisen:<br /><br /> - **Eingabesprache: Tastatur-Layout.** Beispielsweise 0409: 00000409, wobei 0409 vor **:** ist die Eingabesprache und **00000409** ist das Tastaturlayout. Sie finden die Liste der Tastaturlayouts unter dem Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layouts**.<br /><br /> - **Eingabesprache: der IME-Bezeichner.** Im folgenden wird eine vollständige Liste der IME-IDs.<br /><br /> -{:{E429b25a-e5d3-4d1f-9be3-0c608477e3a1}{8f96574e-c86c-4bd6-9666-3f7327d4cbe8}) Amharisch Eingabemethode<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf79e35e} {fa550b04-5ad7-411f-a5ac-ca038ec515d7} Microsoft Pinyin – Simple Fast (Chinesisch vereinfacht)<br /><br /> -{531fdebf-9b4c-4a43-a2aa-960e8fcdc732} b2f9c502-1742-11D4-9790-0080c882687e} Chinesisch (traditionell) – neu (phonetisch)<br /><br /> -{531fdebf-9b4c-4a43-a2aa-960e8fcdc732} 4bdf9f03-c7d3-11D4-b2ab-0080c882687e} Chinesisch (traditionell) – ChangJie<br /><br /> -{531fdebf-9b4c-4a43-a2aa-960e8fcdc732} 6024b45f-5c54-11D4-b921-0080c882687e} Chinesisch (traditionell) - Quick<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{D38EFF65-AA46-4FD5-91A7-67845FB02F5B} Chinesisch traditionell Array<br /><br /> -{E429b25a-e5d3-4d1f-9be3-0c608477e3a1} 037b2c25-480c-4d7f-b027-d6ca6b69788a} Chinesisch traditionell DaYi<br /><br /> -{03b5835f-f03c-411b-9ce2-aa23e1171e36} {a76c93d9-5523-4e90-AAFA-4db112f9ac76} Microsoft-IME (Japanisch)<br /><br /> -{A028ae76-01b1-46c2-99c4-acd9858ae02f} {b5fe1f02-d5f2-4445-9c03-c568f23c99a1} Microsoft-IME (Koreanisch)<br /><br /> -{A1e2b86b-924a-4d43-80f6-8a820df7190f} {b60af051-257a-46bc-b9d3-84dad819bafb} Old Hangul-IME (Koreanisch)<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{409C8376-007B-4357-AE8E-26316EE3FB0D} Eingabemethode Yi<br /><br /> -{:{E429b25a-e5d3-4d1f-9be3-0c608477e3a1}{3cab88b7-cc3e-46a6-9765-b772ad7761ff}) Tigrinya Eingabemethode|  
    |*Einstellungen*|Legt die Benutzerauswahl für Updates fest. Verwenden Sie eine der folgenden Werte:<br /><br /> **-Alle** gleich empfohlene Einstellungen verwenden.<br /><br /> **– Dient zum Aktualisieren** gleich wichtige Updates installieren. nur<br /><br /> **-Keine** entspricht nicht auf Updates prüfen.|  
    |*Benutzername*|-Der Name des neuen Administratorkontos, das während des Setups erstellt wird. Administrator- und Standardbenutzer-Kontonamen müssen die folgenden Kriterien erfüllen:<br /><br /> -Höchstens 19 Zeichen lang kann sein.<br /><br /> -Nicht enthalten / \ [] & 124; < > + =;, ? *<br /><br /> – Müssen Sie nicht starten oder mit einem Punkt endet.<br /><br /> – Müssen keine zwei aufeinanderfolgenden Punkte enthalten.<br /><br /> – Nicht müssen den Servernamen oder den internen Domänennamen identisch sein werden.<br /><br /> -Nicht muss identisch mit einem vordefinierten Benutzernamen wie Administrator oder Gast sein werden.|  
    |*PlainTextPassword*|Dies ist das Kennwort für das neue Administratorkonto, das während des Setups erstellt wird.<br /><br /> -mindestens acht Zeichen lang muss sein.<br /><br /> – Muss mindestens drei der folgenden vier Zeichenkategorien enthält:<br /><br /> -Großbuchstaben.<br /><br /> -Kleinbuchstaben.<br /><br /> -Zahlen.<br /><br /> -Symbole.|  
    |*StdUserName*|Der Name des neuen Standardbenutzerkonto, das während des Setups erstellt wird. Weitere Informationen finden Sie unter der *Benutzername* Parameter für Anforderungen.|  
    |*StdUserPlainTextPassword*|Das Kennwort für das Standardbenutzerkonto, das während des Setups erstellt wird.|  
    |WebDomainName|(Optional) Konfigurieren Sie Internetdomänennamen des Servers. Diese Datei können Sie den Domänennamen entsprechend der für die manuelle Konfiguration im Assistenten Einrichten von Domänennamen verwendeten Methode konfigurieren.|  
    |TrustedCertFileName|(Optional) Konfigurieren Sie vertrauenswürdige Zertifikat für den Domänennamen. Dadurch können Sie platzieren Sie ein. PFX-Zertifikat, das den privaten Schlüssel enthält.|  
    |TrustedCertPassword|(Optional) Das Kennwort zum Importieren der. PFX.|  
    |EnableVPN|(Optional) Aktivieren Sie VPN standardmäßig.|  
    |VpnIPv4StartAddress|(Optional) Legen Sie die VPN-Startadresse.|  
    |VpnIPv4EndAddress|(Optional) Legen Sie die VPN-Endadresse.|  
    |VpnBaseIPv6Address|(Optional) IPV6-Basisadresse für VPN festgelegt.|  
    |VpnIPv6PrefixLength|(Optional) Legen Sie die Präfixlänge der VPN-IPv6-Adresse.|  
    |IsHosted|(Optional) Standardwert ist false, wenn nicht angegeben. Legen Sie diesen Wert, wenn Sie dies in einer hostumgebung einrichten. Es wird die Routerkonfiguration deaktiviert.|  
    |StaticIPv4Address|(Optional) Geben Sie statische IP-Adresse, wenn Sie statt einer dynamischen Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv4Gateway|(Optional) Geben Sie die Standardgatewayadresse, wenn Sie statt einer dynamischen Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv4SubnetMask|(Optional) Geben Sie die Subnetzmaske ein, wenn Sie statt einer dynamischen Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv6Address|(Optional) Geben Sie standardmäßige IP-Adresse, wenn Sie statt einer dynamischen Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv6SubnetPrefixLength|(Optional) Geben Sie standardmäßige IPV6-Subnetzpräfixlänge an, wenn Sie statt einer dynamischen Adresse eine statische IP-Adresse konfigurieren möchten.|  
    |StaticIPv6Gateway|(Optional) Geben Sie die Standardgatewayadresse, wenn Sie statt einer dynamischen eine statische IP-Adresse konfigurieren möchten.|  
    |ClientBackupOn|(Optional) Deaktivieren Sie Client Backup standardmäßig, wenn der Server neue Clients hinzugefügt.|  
    |FileHistoryOn|(Optional) Deaktivieren Sie den Dateiversionsverlauf Backup standardmäßig, wenn der Server neue Clients mit Windows8 Consumer Preview hinzugefügt.|  
    |EnableRWA|Es wird Remotewebzugriff aktiviert, bei der Installation von Windows Server Essentials wird jedoch übersprungen Routerkonfiguration. Dies ist nur bei einer Neuinstallation des Produkts unterstützt. Der Standardwert ist false.|  
    |IPv4DNSForwarder|Legen Sie die IPv4-DNS-Weiterleitung.|  
    |IPv6DNSForwarder|Legen Sie die IPv6-DNS-Weiterleitung.|  
    |LaunchPadHiddenTasks|-(Optional) Sie können den Sicherungseintrag ausblenden oder / und Admin-dashboardeintrag auf dem Launchpad.<br /><br /> -, Deaktivieren Sie das Dashboard: launchpadhiddentasks = Microsoft.Launchpad.admindashboard<br /><br /> -, Deaktivieren Sie die Sicherung: launchpadhiddentasks = Microsoft.Launchpad.Backup<br /><br /> -So deaktivieren Sie Sicherung und Dashboard: LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup,Microsoft.LaunchPad.AdminDashboard|  
  
3.  Speichern Sie die Datei. Stellen Sie sicher, dass Sie die Datei als cfg.ini, nicht cfg.ini.txt speichern.  
  
    > [!NOTE]
    >  Speichern Sie die Datei auf einem USB-Speicherstick, die für spezielle Phasen der Installation verwendet werden kann, oder die cfg.ini-Datei kann sich im Stamm einer beliebigen Festplatte auf dem Zielserver sein. Sie müssen sicherstellen, dass die Codierung für die Datei auf ANSI oder Unicode festgelegt ist, UTF-8 Codierung wird nicht unterstützt.  
  
> [!IMPORTANT]
>  Die Erstkonfiguration Teil der cfg.ini sollte nur vom Endbenutzer zum Personalisieren des Servers oder für eine Partnerinstallation zum Testen Sie der Benutzeroberfläche des Servers mithilfe einer Antwortdatei für die unbeaufsichtigte Installation verwendet werden. In diesem Abschnittder Datei dient nicht zum Erstellen des Abbilds verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  

 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erste Schritte mit Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

