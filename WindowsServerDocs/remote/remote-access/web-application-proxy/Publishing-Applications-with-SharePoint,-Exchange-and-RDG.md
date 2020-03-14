---
ms.assetid: 61ed00fd-51c7-4728-91fa-8501de9d8f28
title: Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG
description: ''
author: billmath
manager: mtillman
ms.author: billmath
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows-server
ms.technology: web-app-proxy
ms.openlocfilehash: 3852baf866dae20d1d1d08219841295aa976c626
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79319934"
---
# <a name="publishing-applications-with-sharepoint-exchange-and-rdg"></a>Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG

> Gilt für: Windows Server 2016

**Diese Inhalte sind für die lokale Version des webanwendungsproxys relevant. Informationen zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie in den [Azure AD Anwendungs Proxy-Inhalt](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/).**

In diesem Thema werden die erforderlichen Aufgaben zum Veröffentlichen von SharePoint Server, Exchange Server oder Remotedesktop Gateway (RDP) über den webanwendungsproxy beschrieben.

> [!NOTE]
> Diese Informationen werden unverändert bereitgestellt.  Remotedesktopdienste unterstützt und empfiehlt [die Verwendung Azure-App Proxys, um sicheren Remote Zugriff auf lokale Anwendungen bereitzustellen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="BKMK_6.1"></a>Veröffentlichen von SharePoint Server
Sie können eine SharePoint-Website mithilfe des webanwendungsproxys veröffentlichen, wenn die SharePoint-Website für die Anspruchs basierte Authentifizierung oder die integrierte Windows-Authentifizierung konfiguriert ist. Wenn Sie Active Directory-Verbunddienste (AD FS) (AD FS) für die Vorauthentifizierung verwenden möchten, müssen Sie eine vertrauende Seite mithilfe eines der Assistenten konfigurieren.

-   Wenn die SharePoint-Website die anspruchsbasierte Authentifizierung verwendet, müssen Sie den Assistenten zum Hinzufügen der Vertrauensstellung der vertrauenden Seite für die Anwendung verwenden.

-   Wenn die SharePoint-Website die integrierte Windows-Authentifizierung verwendet, müssen Sie den nicht anspruchsbasierten Assistenten zum Hinzufügen der Vertrauensstellung der vertrauenden Seite für die Anwendung verwenden. IWA kann mit einer anspruchsbasierten Webanwendung genutzt werden, sofern KDC entsprechend konfiguriert ist.

    Um Benutzern die Authentifizierung mithilfe der integrierten Windows-Authentifizierung zu ermöglichen, muss der webanwendungsproxy-Server einer Domäne hinzugefügt werden.

    Sie müssen die Anwendung zur Unterstützung der eingeschränkten Kerberos-Delegierung konfigurieren. Diese Konfiguration kann auf dem Domänencontroller für jede Anwendung vorgenommen werden. Sie können die Anwendung auch direkt auf dem Back-End-Server konfigurieren, wenn Sie unter Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11)). Außerdem müssen Sie sicherstellen, dass die webanwendungsproxy-Server für die Delegierung der Dienst Prinzipal Namen der Back-End-Server konfiguriert sind. Eine exemplarische Vorgehensweise zum Konfigurieren des webanwendungsproxys zum Veröffentlichen einer Anwendung mithilfe der integrierten Windows-Authentifizierung finden Sie unter [Konfigurieren eines Standorts für die Verwendung der integrierten Windows](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/dn308246(v=ws.11))-Authentifizierung.

Wenn die SharePoint-Website mithilfe alternativer Zugriffszuordnungen (AAM) oder hostbenannter Websitesammlungen konfiguriert ist, können Sie jeweils verschiedene URLs der externen und Back-End-Server zur Veröffentlichung Ihrer Anwendung verwenden. Wenn die SharePoint-Website jedoch nicht mithilfe von AAM oder hostbenannten Websitesammlungen konfiguriert ist, müssen Sie jeweils die gleichen externen und Back-End-Server-URLs verwenden.

## <a name="BKMK_6.2"></a>Veröffentlichen von Exchange Server
In der folgenden Tabelle werden die Exchange-Dienste beschrieben, die Sie über den webanwendungsproxy veröffentlichen können, sowie die unterstützte Vorauthentifizierung für diese Dienste:


|    Exchange-Dienst    |                                                                            Vorauthentifizierung                                                                            |                                                                                                                                       Hinweise                                                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Outlook Web App     | -AD FS mit nicht Anspruchs basierter Authentifizierung<br />-Pass-Through<br />-AD FS verwenden der Anspruchs basierten Authentifizierung für lokales Exchange 2013 Service Pak 1 (SP1) |                                                                  Weitere Informationen finden Sie unter: [Verwenden anspruchsbasierter Authentifizierung von AD FS mit Outlook Web App und EAC](https://go.microsoft.com/fwlink/?LinkId=393723)                                                                  |
| Exchange-Systemsteuerung |                                                                               Pass-Through                                                                               |                                                                                                                                                                                                                                                                                    |
|    Outlook Anywhere    |                                                                               Pass-Through                                                                               | Zur ordnungsgemäßen Funktion müssen drei URLs für Outlook Anywhere veröffentlicht werden:<br /><br />: Die automatische Erkennung-URL.<br />-Der externe Hostname des Exchange-Servers. Das heißt, die URL, die für Clients zum Herstellen einer Verbindung konfiguriert ist.<br />: Der interne voll qualifizierte Namen des Exchange-Servers. |
|  Exchange ActiveSync   |                                                     Pass-Through<br/> AD FS mithilfe des HTTP-Standard Autorisierungs Protokolls                                                      |                                                                                                                                                                                                                                                                                    |

Um Outlook Web App mithilfe der integrierten Windows-Authentifizierung zu veröffentlichen, müssen Sie den nicht anspruchsbasierten Assistenten zum Hinzufügen der Vertrauensstellung der vertrauenden Seite für die Anwendung verwenden.

Um Benutzern die Authentifizierung mithilfe der eingeschränkten Kerberos-Delegierung zu ermöglichen, muss der webanwendungsproxy-Server einer Domäne hinzugefügt werden.

Sie müssen die Anwendung so konfigurieren, dass die Kerberos-Authentifizierung unterstützt wird. Außerdem müssen Sie einen Dienst Prinzipal Namen (Service Principal Name, SPN) für das Konto registrieren, unter dem der Webdienst ausgeführt wird. Dies ist auf dem Domänen Controller oder auf den Back-End-Servern möglich. In einer Exchange-Umgebung mit Lastenausgleich erfordert dies die Verwendung des alternativen Dienst Kontos. Weitere Informationen finden Sie unter [Konfigurieren der Kerberos-Authentifizierung für Client Zugriffs Server mit Lasten](https://docs.microsoft.com/exchange/configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help) Ausgleich.

Sie können die Anwendung auch direkt auf dem Back-End-Server konfigurieren, wenn Sie unter Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11)). Außerdem müssen Sie sicherstellen, dass die webanwendungsproxy-Server für die Delegierung der Dienst Prinzipal Namen der Back-End-Server konfiguriert sind.

## <a name="publishing-remote-desktop-gateway-through-web-application-proxy"></a>Veröffentlichen Remotedesktop Gateways über den webanwendungsproxy
Wenn Sie den Zugriff auf das Remote Zugriffs Gateway einschränken und die Vorauthentifizierung für den Remote Zugriff hinzufügen möchten, können Sie es über den webanwendungsproxy ausführen. Dies ist eine sehr gute Möglichkeit, um sicherzustellen, dass Sie über eine umfassende Vorauthentifizierung für RDG einschließlich MFA verfügen. Die Veröffentlichung ohne Vorauthentifizierung ist ebenfalls eine Option und bietet einen einzigen Einstiegspunkt in Ihre Systeme.

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-pass-through-authentication"></a>Veröffentlichen einer Anwendung in RDG mithilfe der Proxy-Passthrough-Authentifizierung für den webanwendungsproxy

1. Die Installation unterscheidet sich abhängig davon, ob sich die Rollen für RD-Webzugriff (/RDWeb) und RD-Gateway (RPC) auf demselben Server oder auf unterschiedlichen Servern befinden.

2. Wenn die RD-Webzugriff und RD-Gateway Rollen auf demselben RDG-Server gehostet werden, können Sie einfach den Stamm-FQDN im webanwendungsproxy wie https://rdg.contoso.com/veröffentlichen.

   Sie können die beiden virtuellen Verzeichnisse auch einzeln veröffentlichen, z. b.<https://rdg.contoso.com/rdweb/> und https://rdg.contoso.com/rpc/.

3. Wenn die RD-Webzugriff und die RD-Gateway auf separaten RDG-Servern gehostet werden, müssen Sie die beiden virtuellen Verzeichnisse einzeln veröffentlichen. Sie können dieselben oder andere externe voll qualifizierte Namen (z. b. https://rdweb.contoso.com/rdweb/ und https://gateway.contoso.com/rpc/) verwenden.

4. Wenn sich der externe und interne voll qualifizierte Dateityp unterscheiden, sollten Sie die Übersetzung der Anforderungs Kopfzeile für die RDWeb-Veröffentlichungs Regel nicht deaktivieren. Dies kann durch Ausführen des folgenden PowerShell-Skripts auf dem webanwendungsproxy-Server erreicht werden, sollte jedoch standardmäßig aktiviert werden.

   ```PowerShell
   Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false
   ```

   > [!NOTE]
   > Wenn Sie umfangreiche Clients wie RemoteApp-und Desktop Verbindungen oder IOS-Remotedesktop Verbindungen unterstützen müssen, unterstützen diese keine Vorauthentifizierung, sodass Sie RDG mithilfe der Passthrough-Authentifizierung veröffentlichen müssen.

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-with-pre-authentication"></a>Veröffentlichen einer Anwendung in RDG mithilfe des webanwendungsproxys mit Vorauthentifizierung

1.  Die Vorauthentifizierung des webanwendungsproxys bei RDG funktioniert, indem das von Internet Explorer erhaltene vorauthentifizierungs Cookie an den Remotedesktopverbindung-Client (mstsc. exe) übergeben wird. Diese wird dann vom Remotedesktopverbindung Client (mstsc. exe) verwendet. Diese wird dann von Remotedesktopverbindung Client als Authentifizierungs Nachweis verwendet.

    Im folgenden Verfahren wird der Sammlungs Server aufgefordert, die erforderlichen benutzerdefinierten RDP-Eigenschaften in den RDP-Dateien der Remote-app einzuschließen, die an Clients gesendet werden. Diese weisen den Client an, dass eine Vorauthentifizierung erforderlich ist, und dass die Cookies für die Server Adresse für die Vorauthentifizierung an Remotedesktopverbindung Client (mstsc. exe) übergeben werden. In Verbindung mit der Deaktivierung der Funktion HttpOnly in der webanwendungsproxy-Anwendung ermöglicht der Remotedesktopverbindung Client (mstsc. exe) das Verwenden des webanwendungsproxy-Cookies, das über den Browser abgerufen wird.

    Die Authentifizierung beim RD-Webzugriff Server verwendet weiterhin die RD-Webzugriff Formular Anmeldung. Dies bietet die geringste Anzahl von Eingabe Aufforderungen für die Benutzerauthentifizierung, da das RD-Webzugriff Anmeldeformular einen Client seitigen Anmelde Informationsspeicher erstellt, der dann von Remotedesktopverbindung Client (mstsc. exe) für alle nachfolgenden Remote-App-Starts verwendet werden kann.

2.  Erstellen Sie zunächst eine manuelle Vertrauensstellung der vertrauenden Seite in AD FS so, als ob Sie eine Ansprüche unterstützende App veröffentlichen. Dies bedeutet, dass Sie eine Dummy-Vertrauensstellung der vertrauenden Seite erstellen müssen, um die Vorauthentifizierung zu erzwingen, damit Sie die Vorauthentifizierung ohne eingeschränkte Kerberos-Delegierung für den veröffentlichten Server erhalten. Nachdem sich ein Benutzer authentifiziert hat, wird alles andere weitergeleitet.

    > [!WARNING]
    > Möglicherweise ist die Verwendung der Delegierung vorzuziehen, aber Sie löst die mstsc-SSO-Anforderungen nicht vollständig aus, und es gibt Probleme bei der Delegierung an das/RPC-Verzeichnis, da der Client erwartet, dass die RD-Gateway Authentifizierung selbst verarbeitet wird.

3.  Führen Sie die Schritte in der AD FS Management Console aus, um eine manuelle Vertrauensstellung der vertrauenden Seite zu erstellen:

    1.  Verwenden des Assistenten zur Vertrauensstellung der **vertrauenden Seite hinzufügen**

    2.  Wählen Sie **die Option Daten über die vertrauende Seite manuell eingeben**aus.

    3.  Akzeptieren Sie alle Standardeinstellungen.

    4.  Geben Sie für den Bezeichner der vertrauenden Seite den externen voll qualifizierten Namen ein, den Sie für den RDG-Zugriff verwenden möchten, z. b. https://rdg.contoso.com/.

        Dies ist die Vertrauensstellung der vertrauenden Seite, die Sie beim Veröffentlichen der APP im webanwendungsproxy verwenden.

4.  Veröffentlichen Sie den Stamm der Site (z. b. https://rdg.contoso.com/) im webanwendungsproxy. Legen Sie die Vorauthentifizierung auf AD FS fest, und verwenden Sie die zuvor erstellte Vertrauensstellung der vertrauenden Seite. Dies ermöglicht/RDWeb und/RPC, das gleiche webanwendungsproxy-Authentifizierungs Cookie zu verwenden.

    Es ist möglich,/RDWeb und/RPC als separate Anwendungen zu veröffentlichen und sogar andere veröffentlichte Server zu verwenden. Sie müssen lediglich sicherstellen, dass Sie beide mit derselben Vertrauensstellung der vertrauenden Seite veröffentlichen, da das webanwendungsproxy-Token für die Vertrauensstellung der vertrauenden Seite ausgegeben wird

5.  Wenn sich der externe und interne voll qualifizierte Dateityp unterscheiden, sollten Sie die Übersetzung der Anforderungs Kopfzeile für die RDWeb-Veröffentlichungs Regel nicht deaktivieren. Dies kann durch Ausführen des folgenden PowerShell-Skripts auf dem webanwendungsproxy-Server erreicht werden, sollte jedoch standardmäßig aktiviert sein:

    ```PowerShell
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false
    ```

6.  Deaktivieren Sie die HttpOnly-Cookie-Eigenschaft im webanwendungsproxy für die veröffentlichte RDG-Anwendung. Um dem RDG-ActiveX-Steuerelement Zugriff auf das webanwendungsproxy-Authentifizierungs Cookie zu ermöglichen, müssen Sie die HttpOnly-Eigenschaft im webanwendungsproxy-Cookie deaktivieren.

    Hierfür müssen Sie das Updaterollup vom [November 2014 für Windows RT 8,1, Windows 8.1 und Windows Server 2012 R2 (KB3000850)](https://support.microsoft.com/kb/3000850)installieren.

    Führen Sie nach der Installation des Hotfixes das folgende PowerShell-Skript auf dem webanwendungsproxy-Server aus, und geben Sie den entsprechenden Anwendungsnamen

    ```PowerShell
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableHttpOnlyCookieProtection:$true
    ```

    Das Deaktivieren von HttpOnly ermöglicht dem RDG-ActiveX-Steuerelement den Zugriff auf das webanwendungsproxy-Authentifizierungs Cookie

7.  Konfigurieren Sie die relevante RDG-Sammlung auf dem Sammlungs Server so, dass der Remotedesktopverbindung Client (mstsc. exe) weiß, dass die Vorauthentifizierung in der RDP-Datei erforderlich ist.

    -   In Windows Server 2012 und Windows Server 2012 R2 kann dies erreicht werden, indem Sie auf dem RDG-Sammlungs Server das folgende PowerShell-Cmdlet ausführen:

        ```PowerShell
        Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s: <https://externalfqdn/rdweb/>`nrequire pre-authentication:i:1"
        ```

        Stellen Sie sicher, dass Sie die < und > Klammern entfernen, wenn Sie durch ihre eigenen Werte ersetzen, z. b.:

        ```PowerShell
        Set-RDSessionCollectionConfiguration -CollectionName "MyAppCollection" -CustomRdpProperty "pre-authentication server address:s: https://rdg.contoso.com/rdweb/`nrequire pre-authentication:i:1"
        ```

    -   In Windows Server 2008 R2:

        1.  Melden Sie sich auf dem Terminal Server mit einem Konto an, das über Administrator Rechte verfügt.

        2.  Wechseln Sie zu **Start** >**Verwaltungs Tools** > **Terminal Dienste** > **TS RemoteApp-Manager.**

        3.  Klicken Sie im Bereich **Übersicht** von TS RemoteApp-Manager neben RDP-Einstellungen auf **ändern**.

        4.  Geben Sie auf der Registerkarte **Benutzerdefinierte RDP-Einstellungen** die folgenden RDP-Einstellungen in das Feld Benutzerdefinierte RDP-Einstellungen ein:

            `pre-authentication server address: s: https://externalfqdn/rdweb/`

            `require pre-authentication:i:1`

        5.  Wenn Sie dies abgeschlossen haben, **Klicken Sie**auf übernehmen.

            Dadurch wird der Sammlungs Server aufgefordert, die benutzerdefinierten RDP-Eigenschaften in die RDP-Dateien einzuschließen, die an Clients gesendet werden. Diese weisen den Client an, dass eine Vorauthentifizierung erforderlich ist, und dass die Cookies für die Server Adresse der Vorauthentifizierung an den Remotedesktopverbindung-Client (mstsc. exe) übergeben werden. In Verbindung mit der Deaktivierung von HttpOnly in der webanwendungsproxy-Anwendung ermöglicht es dem Remotedesktopverbindung Client (mstsc. exe), das über den Browser erhaltene webanwendungsproxy-Authentifizierungs Cookie zu verwenden.

            Weitere Informationen zu RDP finden Sie unter [Konfigurieren des TS-Gateway-OTP-Szenarios](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731249(v=ws.10)).

## <a name="BKMK_Links"></a>Siehe auch

- [Planen der Veröffentlichung von Anwendungen mit webanwendungsproxy](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11))

- [Problembehandlung: Webanwendungsproxy](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))

- [Leitfaden für webanwendungsproxy](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))
