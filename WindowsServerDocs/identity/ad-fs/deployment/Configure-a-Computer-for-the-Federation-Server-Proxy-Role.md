---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: Konfigurieren eines Computers für die Verbundserverproxy-Rolle
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 06bccb135963d5b5bc754e895843a4d75153c120
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963121"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>Konfigurieren eines Computers für die Verbundserverproxy-Rolle

Nachdem Sie einen Computer mit den erforderlichen Zertifikaten konfiguriert und den Verbunddienstproxy-Rollen Dienst installiert haben, können Sie den Computer als Verbund Server Proxy konfigurieren. Sie können die folgende Prozedur verwenden, um den Computer für die Verbundserverproxy-Rolle einzurichten.

> [!IMPORTANT]
> Bevor Sie dieses Verfahren zum Konfigurieren des Verbund Server Proxy-Computers verwenden, stellen Sie sicher, dass Sie alle Schritte in Prüfliste [: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md) in der angegebenen Reihenfolge ausgeführt haben. Stellen Sie sicher, dass mindestens ein Verbundserver bereitgestellt wurde und alle erforderlichen Anmeldeinformationen für die Autorisierung einer Verbundserverproxy-Konfiguration implementiert sind. Sie müssen auch Secure Sockets Layer \( SSL- \) Bindungen auf der Standard Website konfigurieren, oder dieser Assistent wird nicht gestartet. Alle genannten Aufgaben müssen abgeschlossen sein, damit dieser Verbundserverproxy ordnungsgemäß verwendet werden kann.

Wenn Sie das Einrichten des Computers fertig gestellt haben, überprüfen Sie, ob die Funktionsweise des Verbundserverproxys den Erwartungen entspricht. Weitere Informationen finden Sie unter [Überprüfen der Betriebsbereitschaft eines Verbundserverproxys](Verify-That-a-Federation-Server-Proxy-Is-Operational.md).

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>So konfigurieren Sie einen Computer für die Verbundserverproxy-Rolle

1.  Es gibt zwei Möglichkeiten, den AD FS-Assistenten für die Konfiguration des Verbundservers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:

    -   Geben Sie auf dem **Start** Bildschirm**AD FS Assistenten für die Konfiguration eines Verbund Server Proxys**ein, und drücken Sie die EINGABETASTE

    -   Öffnen Sie nach Abschluss des Setup-Assistenten Windows-Explorer, navigieren Sie zum Ordner **C: \\ Windows \\ ADFS** , und doppelklicken Sie dann auf \- **FspConfigWizard.exe**.

2.  Starten Sie den Assistenten mit einer der beiden Methoden, und klicken Sie dann auf der Seite **Willkommen** auf **Weiter**.

3.  Geben Sie auf der Seite **Verbunddienstname angeben** unter **Verbunddienstname** den Namen ein, der den Verbunddienst darstellt, für den dieser Computer die Proxyrolle übernimmt.

4.  Legen Sie basierend auf Ihren bestimmten Netzwerkanforderungen fest, ob Sie einen HTTP-Proxyserver verwenden müssen, um Anforderungen an den Verbunddienst weiterzuleiten. Wenn dies der Fall ist, aktivieren Sie das Kontrollkästchen **HTTP-Proxyserver beim Senden von Anforderungen an diesen Verbunddienst verwenden**, geben Sie unter **Adresse des HTTP-Proxyservers** die Adresse des Proxyservers ein, klicken Sie auf **Verbindung testen**, um die Verbindung zu überprüfen, und klicken Sie dann auf **Weiter**.

5.  Wenn Sie dazu aufgefordert werden, geben Sie die zum Einrichten einer Vertrauensstellung zwischen diesem Verbundserverproxy und dem Verbunddienst erforderlichen Anmeldeinformationen an.

    Standardmäßig kann nur das vom Verbunddienst verwendete Dienst Konto oder ein Mitglied der lokalen Gruppe "Builtin \\ Administrators" einen Verbund Server Proxy autorisieren.

6.  Überprüfen Sie auf der Seite **Bereit zum Übernehmen der Einstellungen** die Details. Wenn die Einstellungen richtig sind, klicken Sie auf **Weiter**, um diesen Computer mit diesen Proxyeinstellungen zu konfigurieren.

7.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.

    Es gibt kein MMC-Snap-in Microsoft Management Console \( \) , das \- zum Verwalten von Verbund Server Proxys verwendet werden kann. Verwenden Sie Windows PowerShell-Cmdlets, um die Einstellungen für die einzelnen Verbund Server Proxys in Ihrer Organisation zu konfigurieren.

## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>Konfigurieren eines alternativen TCP \/ -IP-Ports für Proxy Vorgänge
Standardmäßig ist der Verbund Server Proxy-Dienst für die Verwendung von TCP-Port 443 für HTTPS-Datenverkehr und Port 80 für HTTP-Datenverkehr für die Kommunikation mit dem Verbund Server konfiguriert. Wenn Sie andere Ports, beispielsweise TCP-Port 444 für HTTPS und Port 81 für HTTP, konfigurieren möchten, müssen Sie die folgenden Aufgaben durchführen.

> [!NOTE]
> Wenn Sie beabsichtigen, AD FS für den Betrieb unter Alternativen TCP \/ -IP-Ports bereitzustellen, sollten Sie zuerst die Ports in den IIS-Protokoll Bindungen für http und HTTPS auf dem Verbund Server und den Verbund Server Proxy-Computern ändern. Dies sollte eintreten, bevor Sie die AD FS Konfigurationsassistenten für die Erstkonfiguration ausführen. Wenn Sie Internetinformationsdienste \( IIS \) zuerst konfigurieren, \/ werden die Einstellungen für den alternativen TCP-IP-Port erkannt, wenn \- die Assistenten basierte Konfiguration in AD FS erfolgt. das folgende Verfahren ist nicht erforderlich. Wenn Sie die Porteinstellungen später ändern möchten, aktualisieren Sie zuerst die IIS-Protokollbindungen, und verwenden Sie dann das folgende Verfahren, um die Porteinstellungen entsprechend zu aktualisieren. Weitere Informationen zum Bearbeiten von IIS-Bindungen finden Sie im [Artikel 149605](https://go.microsoft.com/fwlink/?LinkId=190275) in der Microsoft Knowledge Base.

#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>So konfigurieren Sie alternative TCP \/ -IP-Ports für die Verwendung durch den Verbund Server Proxy

1.  Konfigurieren Sie den Verbundserver zur Verwendung der Nichtstandardports.

    Geben Sie hierzu die nicht standardmäßige Portnummer an, indem Sie Sie als Teil des Cmdlets **Set \- adfsproperties** mit den Optionen *httpsport* und *HTTPPort* einschließen. Verwenden Sie zum Konfigurieren dieser Ports beispielsweise die folgenden Befehle in der Windows PowerShell-Sitzung auf dem Verbund Server Computer:

    ```
    Set-ADFSProperties -HttpsPort 444
    Set-ADFSProperties -HttpPort 81
    ```

2.  Konfigurieren Sie den Verbund Server Proxy so, dass er den nicht Standardport verwendet.

    Geben Sie hierzu die nicht standardmäßige Portnummer an, indem Sie diese mit den Optionen *httpsport* und *HTTPPort* als Teil des Cmdlets **Set \- adfsproxyproperties** einschließen. Verwenden Sie zum Konfigurieren dieser Ports beispielsweise die folgenden Befehle in der Windows PowerShell-Sitzung auf dem Verbund Server Computer:

    ```
    Set-ADFSProxyProperties -HttpsPort 444
    Set-ADFSProxyProperties -HttpPort 81
    ```

    > [!NOTE]
    > Endpunkt-URLs sind für den Verbund Server Proxy-Dienst standardmäßig nicht aktiviert. Wenn Sie eine neue Verbund Server Installation konfigurieren, müssen Sie zunächst die Verbund Server Proxy-Dienst Endpunkte aktivieren. Beispielsweise wird angenommen, dass Sie für alle Endpunkte, auf die sich das Beispiel in diesem Verfahren bezieht, Sie für den Proxy aktiviert haben, indem Sie diese im Snap \- -in AD FS Verwaltung auswählen und dann **auf Proxy aktivieren**auswählen.

3.  Aktualisieren Sie die IIS-Installation auf dem Verbund Server Proxy, damit Security Assertion Markup Language \( SAML \) -und WS \- Trust-Endpunkte so konfiguriert sind, dass Sie die aktualisierte Portnummer widerspiegeln. Zu diesem Zweck können Sie mithilfe von Editor Folgendes in der Web.config-Datei ändern, die sich auf dem Verbund Server Proxy-Computer unter Systemlaufwerk% \\ Inetpub \\ ADFS \\ ls befindet \\ . Wenn Sie z. b. einen Verbund Server mit dem Namen sts1.contoso.com haben und die neue Portnummer 444 lautet, navigieren Sie zu, und öffnen Sie die Datei Web.config im Editor auf dem Verbund Server Proxy-Computer. Suchen Sie den folgenden Abschnitt, ändern Sie die Portnummer wie unten gezeigt, und speichern und beenden Sie dann den Editor.

    ```
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />
    ```

4.  Fügen Sie das Benutzerkonto des Verbund Server Proxy-Dienstanbieter der Zugriffs Steuerungs Listen- \( ACL \) für die zugehörigen Endpunkt-URLs hinzu. Wenn beispielsweise die Portnummer 1234 und das Benutzerkonto, unter dem der AD fsfederation-Server Proxy Dienst ausgeführt wird, das integrierte \- Netzwerkdienst Konto ist, geben Sie an einer Eingabeaufforderung den folgenden Befehl ein:

    ```
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"

    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"
    ```

    Die vorherigen Befehle müssen auf dem Verbund Server und den Verbund Server Proxy-Computern ausgeführt werden.

## <a name="additional-references"></a>Weitere Verweise
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)


