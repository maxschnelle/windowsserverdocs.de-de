---
ms.assetid: ed3206b4-bbfc-4bc7-a43c-981b0544a50d
title: "Erforderliche Updates für Active Directory-Verbunddienste (AD FS)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 434bf65c9f5ec977318b5efcdeebd19a5f1ed475
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="required-updates-for-active-directory-federation-services-ad-fs-and-web-application-proxy-wap"></a>Erforderliche Updates für Active Directory-Verbunddienste (AD FS) und Web Application Proxy (WAP)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2 SP1

Ab Oktober 2016 werden alle Updates für alle Komponenten von Windows Server nur über Windows Update (WU) veröffentlicht.  Es gibt keine weitere Hotfixes oder einzelne Downloads.
Dies gilt für Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 SP1.

Diese Seite listet Sicherheitsrollup-Pakete von besonderem Interesse für AD FS und WAP als auch die historischen Liste der Hotfix-Updates für AD FS und WAP empfohlen.

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2016"></a>Updates für AD FS und WAP in WindowsServer 2016
Updates für Windows Server 2016 werden monatlich über Windows Update bereitgestellt und sind kumulativ. Das unten aufgeführte Updatepaket wird empfohlen, für alle AD FS und WAP 2016-Server und alle zuvor erforderlichen Updates sowie die neuesten Updates enthält.

|KB # |Beschreibung|Veröffentlichungsdatum
|----- | ----- |-----
|[4041688 (BS-Build 14393.1794)](https://support.microsoft.com/kb/4041688)|Dieser Patch behebt ein Problem, das zeitweise Autorität für die AD-Anforderungen an den falschen Identitätsanbieter aufgrund falscher Verhalten beim Zwischenspeichern misdirects. Dies kann Authentifizierungsfeatures wie Multi-Factor Authentication-Effekt. </br></br>Die Möglichkeit hinzugefügt für AAD Connect Health Bericht Integrität des AD FS-Servers mit der richtigen Genauigkeit (mit ausführlichen Überwachung) auf den gemischten WS2012R2 und WS2016 AD FS-Farmen.</br></br>Haben ein Problem behoben, in denen farm während des Upgrades von 2012 R2 AD FS zu AD FS 2016, schlägt das PowerShell-Cmdlet zum Auslösen von Verhalten Farmebene mit einem Timeout fehl, wenn viele der vertrauenden Seite Vertrauensstellungen vorhanden sind.</br></br>Behebt das Problem, dass die AD FS-Authentifizierungsfehler führt durch Ändern des Parameterwerts Wct bei den Verbund der Anfragen an andere Security Token Server (STS).|Oktober2017|
|[4038801 (BS-Build 14393.1737)](https://support.microsoft.com/kb/4038801)|Unterstützung für OIDC mit federated LDPs abmelden. Dadurch wird die "Kioskszenarios", in denen mehrere Benutzer möglicherweise seriell ein einzelnes Gerät angemeldet, liegt der Verbund mit einer "Ldp".</br></br>Wurde ein Problem Wohnsitzes CEP/CES Zertifikate mit gMSA-Konten funktionieren nicht WinHello behoben.</br></br>Behebt ein Problem, in denen nicht die Windows Internal Database (WID) für Windows Server2016 AD FS-Server synchronisieren einige Einstellungen, z.B. die ApplicationGroupId Spalten aus Tabellen IdentityServerPolicy.Scopes und IdentityServerPolicy.Clients) aufgrund von einem Fremdschlüssel Einschränkung. Solche Synchronisierungsfehler können dazu führen, dass andere Anspruch, Anspruchsregel Anbieter und die Anwendung Umgebungen zwischen Primär zu Sekundär AD FS-Server. Auch wenn die primäre WID-Rolle auf einen sekundären Knoten verschoben wird, werden Anwendungsgruppen nicht mehr in der AD FS-UX verwaltbare</br></br>Dieses Update behebt Probleme, in denen Multi-Factor Authentication funktioniert nicht richtig mit mobilen Geräten, die benutzerdefinierte Kultur-Definitionen verwenden|September2017|
|[4034661 (BS-Build 14393.1613)](https://support.microsoft.com/kb/4034661)|Behebt ein Problem steht für die IP-Adresse des Aufrufers Nog 411 Ereignisse im Sicherheitsereignisprotokoll von AD FS 4.0 protokollierter \ Windows Server2016 RS1 AD FS-Server auch nach der Aktivierung von "erfolgsüberwachungen" und "Fehlerüberwachungen".</br></br>Dieser Patch behebt ein Problem mit Azure Multi-Factor Authentication (MFA), wenn ein ADFX Server konfiguriert ist, einen HTTP-Proxy.</br></br>"Behebt das Problem, in denen eine abgelaufene oder gesperrte Zertifikat mit dem AD FS-Proxyserver Darstellung nicht Fehler an den Benutzer zurückgegeben wird."|August2017|
|[4034658 (BS-Build 14393.1593)](https://support.microsoft.com/kb/4034658)|Update für 2016 AD FS-Server zur Unterstützung von MFA-Zertifikatregistrierung für Windows Hello für Unternehmen für lokale Bereitstellung|August2017| 
|[4025334 (BS-Build 14393.1532)](https://support.microsoft.com/kb/4025334)|Behebt das Problem, auf denen der Token PkeyAuth-Handler eine Authentifizierung fehlschlägt konnte, wenn die Anforderung Pkeyauth falsche Daten enthält. Die Authentifizierung sollte weiterhin ohne Geräteauthentifizierung|Juli2017|
|[4022723 (BS-Build 14393.1378)](https://support.microsoft.com/kb/4022723)|[Web Application Proxy] Wert der Eigenschaft der DisableHttpOnlyCookieProtection-Konfiguration wird nicht vom WAP 2016 in gemischten 2012R2/2016-Bereitstellung abgeholt </br></br>[Web Application Proxy] Abrufen von Zugriffstoken für Benutzer von AD FS in EAS Prä-Auth Szenarien nicht möglich.</br></br>AD FS 2016: WSFED Abmeldung führt zu einer Ausnahme|Juni2017 
|[3213986](https://support.microsoft.com/kb/3213986)|Kumulatives Update für WindowsServer 2016 für X64 64-Systeme (KB3213986)| Januar 2017

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2012-r2"></a>Updates für AD FS und WAP in Windows Server 2012 R2
Im folgenden ist die Liste der Updates und Update-Rollups, die für Active Directory-Verbunddienste (AD FS) in Windows Server 2012 R2 veröffentlicht wurden.

|KB # |Beschreibung|Veröffentlichungsdatum
|----- | ----- |-----
|[4041685](https://support.microsoft.com/kb/4041685)|Behebt das Problem AD FS, in denen MSISConext Cookies im Anforderungsheader können schließlich die maximale Größe der Header Überlauf und dazu führen, dass Fehler bei der Authentifizierung mit HTTP-Statuscode 400 "Ungültige Anforderung – Header zu lang".</br></br>Wurde ein Problem behoben, in denen können AD FS nicht mehr ignorieren "prompt = Anmeldung" während der Authentifizierung. Eine Option "Deaktiviert" wurde hinzugefügt, um Szenarien wiederherstellen, in denen keine Kennwörter-Authentifizierung verwendet wird.|Oktober2017 Vorschau des Update-Rollup|
|[4019217](https://support.microsoft.com/kb/4019217)|Arbeitsordner-Clients mithilfe von Token Broker nicht funktionieren, wenn Sie einen Server2012 R2 AD FS-Server verwenden|Mai2017 Preview-Updaterollup| 
|[4015550](https://support.microsoft.com/kb/4015550)|Das Problem mit AD FS nicht authentifizieren von externen Benutzern und AD FS WAP nach dem Zufallsprinzip Fehler beim Weiterleiten der Anforderung wurde behoben.|April2017-Update-Rollup| 
|[4015547](https://support.microsoft.com/kb/4015547)|Das Problem mit AD FS nicht authentifizieren von externen Benutzern und AD FS WAP nach dem Zufallsprinzip Fehler beim Weiterleiten der Anforderung wurde behoben.|April2017 Sicherheitsupdate| 
|[4012216](https://support.microsoft.com/kb/4009970)|MS17-019 dieses Update behebt ein Sicherheitsrisiko in Active Directory Federation Services (ADFS). Das Sicherheitsrisiko kann Offenlegung von Informationen ermöglichen, wenn ein Angreifer eine spezielle Anforderung zu einem AD FS-Server sendet, kann der Angreifer ausnutzen und vertrauliche Informationen über das Zielsystem lesen.|März2017-Update-Rollup| 
|[3179574](https://support.microsoft.com/kb/3179574)|Behebt ein Problem mit AD FS extranet Kennwort aktualisieren. |Updaterollup August 2016
|[3172614](https://support.microsoft.com/kb/3172614)|Eingeführten Aufforderung = Anmeldung [unterstützen](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/ad-fs-faq#BKMK_7), haben das Problem mit dem AD FS-Verwaltungskonsole und AlwaysRequireAuthentication Einstellung. |Updaterollup Juli 2016
|[3163306](https://support.microsoft.com/kb/3163306)|Active Directory-Verbunddienste (AD FS) 3.0 kann keine Verbindung mit Lightweight Directory Access Protocol (LDAP)-Attributspeicher, die zur Verwendung von Secure Sockets Layer (SSL)-Port 636 oder 3269 in Verbindungszeichenfolge konfiguriert sind. |Updaterollup vom Juni 2016
|[3148533](https://support.microsoft.com/kb/3148533)|MFA alternative Authentifizierung ein Fehler auftritt, durch AD FS-Proxy in Windows Server 2012 R2 |Mai 2016
|[3134787](https://support.microsoft.com/kb/3134787)|AD FS-Protokolle enthalten keine Client-IP-Adresse für Konto-Sperre Szenarien in Windows Server 2012 R2 |Februar 2016
|[3134222](https://support.microsoft.com/kb/3134222)|MS16-020: Sicherheitsupdate für Active Directory Federation Services, Adresse Denial-of-Service: 9. Februar 2016|Februar 2016
|[3105881](https://support.microsoft.com/kb/3105881)|Anwendungen kann nicht zugegriffen werden, wenn Geräteauthentifizierung in Windows Server 2012 R2-basierten AD FS-Server aktiviert ist|Oktober 2015
|[3092003](https://support.microsoft.com/kb/3092003)|Seite lädt wiederholt und Authentifizierung schlägt fehl, wenn Benutzer in Windows Server 2012 R2 AD FS MFA verwenden|August 2015
|[3080778](https://support.microsoft.com/kb/3080778)|AD FS wird nicht OnError aufgerufen, wenn MFA-Adapter in Windows Server 2012 R2 eine Ausnahme auslöst|Juli 2015
|[3075610](https://support.microsoft.com/kb/3075610)|Vertrauensstellungen auf sekundären AD FS-Server verloren nach dem Hinzufügen oder Entfernen von Anspruchsanbieter in Windows Server 2012 R2|Juli 2015
|[3070080](https://support.microsoft.com/kb/3070080)|Home Realm Ermittlung nicht ordnungsgemäß funktioniert, Non-Claims-Aware Vertrauensstellungen der vertrauenden Seite Vertrauensstellung|Juni 2015
|[3052122](https://support.microsoft.com/kb/3052122)|Update fügt Unterstützung für zusammengesetzte ID Ansprüche in AD FS-Token in Windows Server 2012 R2|Mai 2015
|[3045711](https://support.microsoft.com/kb/3045711)|MS15-040: Sicherheitsrisiko in Active Directory Federation Services kann Offenlegung von Informationen ermöglichen.|April 2015
|[3042127](https://support.microsoft.com/kb/3042127)|"HTTP 400 - Ungültige Anforderung" Fehler beim Öffnen eines freigegebenen Postfachs über WAP in Windows Server 2012 R2|März 2015
|[3042121](https://support.microsoft.com/kb/3042121)|AD FS-token Replay-Schutz für Web Application Proxy Authentifizierungstoken in Windows Server 2012 R2|März 2015
|[3035025](https://support.microsoft.com/kb/3035025)|Hotfix für Aktualisieren des Kennworts verfügen, damit Benutzer nicht erforderlich sind, mit registrierten Gerät in Windows Server 2012 R2|Januar 2015
|[3033917](https://support.microsoft.com/kb/3033917)|AD FS konnte nicht unter Windows Server 2012 R2 SAML-Antwort verarbeitet werden.|Januar 2015
|[3025080](https://support.microsoft.com/kb/3025080)|Vorgang schlägt fehl, wenn Sie versuchen, speichern Sie eine Office-Datei per Webanwendungsproxy in Windows Server 2012 R2|Januar 2015
|[3025078](https://support.microsoft.com/kb/3025078)|Sie sind nicht für Benutzernamen erneut dazu aufgefordert werden, wenn Sie einen falschen Benutzernamen verwenden, um die Anmeldung bei Windows Server 2012 R2|Januar 2015
|[3020813](https://support.microsoft.com/kb/3020813)|Sie werden zur Authentifizierung aufgefordert, wenn Sie eine Anwendung in Windows Server 2012 R2 AD FS ausführen|Januar 2015
|[3020773](https://support.microsoft.com/kb/3020773)|Fehler bei der Timeout nach der ersten Bereitstellung von Device Registration Service in Windows Server 2012 R2|Januar 2015
|[3018886](https://support.microsoft.com/kb/3018886)|Sie werden zur Eingabe aufgefordert Benutzername und Kennwort zweimal beim Zugriff auf Windows Server 2012 R2 AD FS-Server über intranet|Januar 2015
|[3013769](https://support.microsoft.com/kb/3013769)|Windows Server 2012 R2 Update-Rollup|Dezember 2014
|[3000850](https://support.microsoft.com/kb/3000850)|Windows Server 2012 R2 Update-Rollup|November 2014
|[2975719](https://support.microsoft.com/kb/2975719)|Windows Server 2012 R2 Update-Rollup|August 2014
|[2967917](https://support.microsoft.com/kb/2967917)|Windows Server 2012 R2 Update-Rollup|Juli 2014
|[2962409](https://support.microsoft.com/kb/2962409)|Windows Server 2012 R2 Update-Rollup|Juni 2014
|[2955164](https://support.microsoft.com/kb/2955164)|Windows Server 2012 R2 Update-Rollup|Mai 2014
|[2919355](https://support.microsoft.com/kb/2919355)|Windows Server 2012 R2 Update-Rollup|April 2014

## <a name="updates-for-ad-fs-in-windows-server-2012-ad-fs-21-and-ad-fs-20"></a>Updates für AD FS unter WindowsServer 2012 (AD FS 2.1) und AD FS 2.0
Im folgenden ist die Liste der Updates und Update-Rollups, die für AD FS 2.0 und 2.1 veröffentlicht wurden.

|KB # |Beschreibung|Veröffentlichungsdatum|Gilt für:
|----- | ----- |-----|-----
|[3197878](https://support.microsoft.com/kb/3197878)|In Windows Server 2012 (Dies ist der allgemeinen Veröffentlichung von Hotfix 3094446) Authentifizierungsfehler über proxy|November 2016 Qualitätsrollup|AD FS 2.1
|[3197869](https://support.microsoft.com/kb/3197869)|In Windows Server 2008 R2 SP1 (Dies ist der allgemeinen Veröffentlichung von Hotfix 3094446) Authentifizierungsfehler über proxy|November 2016 Qualitätsrollup|AD FS 2.0
|[3094446](https://support.microsoft.com/kb/3094446)|In Windows Server 2012 oder Windows Server 2008 R2 SP1 Authentifizierungsfehler über proxy|September 2015|AD FS 2.0 und 2.1
|[3070078](https://support.microsoft.com/kb/3070078)|AD FS 2.1 löst eine Ausnahme aus, wenn Sie ein Verschlüsselungszertifikat in Windows Server 2012 authentifizieren|Juli 2015|AD FS 2.1
|[3062577](https://support.microsoft.com/kb/3062577)|MS15-062: Sicherheitsrisiko in Active Directory-Verbunddienste kann Erhöhung von Berechtigungen ermöglichen.|Juni 2015|AD FS 2.0 / 2.1
|[3003381](https://support.microsoft.com/kb/3003381)|MS14-077: Schwachstelle in Active Directory Federation Services kann Offenlegung von Informationen ermöglichen: 14. April 2015|November 2014|AD FS 2.0 / 2.1
|[2987843](https://support.microsoft.com/kb/2987843)|Speicherauslastung des AD FS-Verbundservers behält erhöhen, wenn viele Benutzer melden Sie sich eine Webanwendung in Windows Server 2012|Juli 2014|AD FS 2.1
|[2957619](https://support.microsoft.com/kb/2957619)|Die Vertrauensstellung der vertrauenden Seite in AD FS wird angehalten, wenn eine an AD FS für eine delegierte Token Anforderung|Mai 2014|AD FS 2.1
|[2926658](https://support.microsoft.com/kb/2926658)|SQL ADFS-Bereitstellung ein Fehler auftritt, wenn Sie nicht über die SQL-Berechtigungen verfügen|Oktober 2014|AD FS 2.1
|[2896713](https://support.microsoft.com/kb/2896713) oder [2989956](https://support.microsoft.com/kb/2989956)|Update ist verfügbar, die mehrere Probleme zu beheben, nach der Installation von Sicherheitsupdates 2843638 auf einem AD FS-server|November 2013</br></br>September 2014|AD FS 2.0 / 2.1
|[2877424](https://support.microsoft.com/kb/2877424)|Update können Sie ein Zertifikat für mehrere der vertrauenden Seite in einem AD FS-Farm 2.1 Vertrauensstellungen|Oktober 2013|AD FS 2.1
|[2873168](https://support.microsoft.com/kb/2873168)|Update: Ein Fehler auftritt, wenn Sie eine Drittanbieter-CSP und HSM verwenden und konfigurieren Sie dann eine Anspruchsanbieter-Vertrauensstellung im Updaterollup 3 für AD FS 2.0 unter Windows Server 2008 R2 Service Pack 1|September 2013|AD FS 2.0
|[2861090](https://support.microsoft.com/kb/2861090)|Ein Komma in den Antragstellernamen für ein Verschlüsselungszertifikat wird eine Ausnahme in Windows Server 2008 R2 SP1|August 2013|AD FS 2.0
|[2843639](https://support.microsoft.com/kb/2843639)|[Sicherheit] Sicherheitsanfälligkeit in Active Directory-Verbunddienste kann Offenlegung von Informationen ermöglichen.|November 2013|AD FS 2.1
|[2843638](https://support.microsoft.com/kb/2843638)|MS13-066: Beschreibung des Sicherheitsupdates für Active Directory-Verbunddienste 2.0: 13. August 2013|August 2013|AD FS 2.0
|[2827748](https://support.microsoft.com/kb/2827748)|FederationMetadata.XML-Datei enthält nicht die MEX-Endpunkt-Informationen für die WS-Trust und WS-Federation-Endpunkte in Windows Server 2012|Mai 2013|AD FS 2.1
|[2790338](https://support.microsoft.com/kb/2790338)|Hinweise zum Updaterollup 3 für Active Directory-Verbunddienste (AD FS) 2.0|März 2013|AD FS 2.0




