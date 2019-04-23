---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: Konfigurieren eines Computers für die Verbundserverproxy-Rolle
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2a89bab2fd1af1a1d7234da29f2025b4b12d6774
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861801"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>Konfigurieren eines Computers für die Verbundserverproxy-Rolle

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie einen Computer mit den erforderlichen Zertifikaten konfiguriert und die Verbunddienstproxy-Rollendienst installiert haben, können Sie den Computer ein Verbundserverproxy konfigurieren. Sie können die folgende Prozedur verwenden, um den Computer für die Verbundserverproxy-Rolle einzurichten.  
  
> [!IMPORTANT]  
> Bevor Sie dieses Verfahren zum Konfigurieren der Verbundserverproxy-Computer verwenden, stellen Sie sicher, dass Sie alle Schritte ausgeführt haben [Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md) in der Reihenfolge, in der sie aufgelistet sind. Stellen Sie sicher, dass mindestens ein Verbundserver bereitgestellt wurde und alle erforderlichen Anmeldeinformationen für die Autorisierung einer Verbundserverproxy-Konfiguration implementiert sind. Außerdem müssen Sie Secure Sockets Layer konfigurieren \(SSL\) Bindungen an die Standardwebsite oder mit diesem Assistenten werden nicht gestartet werden. Alle genannten Aufgaben müssen abgeschlossen sein, damit dieser Verbundserverproxy ordnungsgemäß verwendet werden kann.  
  
Wenn Sie das Einrichten des Computers fertig gestellt haben, überprüfen Sie, ob die Funktionsweise des Verbundserverproxys den Erwartungen entspricht. Weitere Informationen finden Sie unter [Überprüfen der Betriebsbereitschaft eines Verbundserverproxys](Verify-That-a-Federation-Server-Proxy-Is-Operational.md).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>So konfigurieren Sie einen Computer für die Verbundserverproxy-Rolle  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Konfigurations-Assistenten zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Auf der **starten** geben**Konfigurations-Assistenten von AD FS Federation Server Proxy**, und drücken Sie dann die EINGABETASTE.  
  
    -   Jederzeit nach der Setup-Assistent abgeschlossen wurde, öffnen ein Windows-Explorer ist, navigieren Sie zu der **C:\\Windows\\ADFS** Ordner, und klicken Sie dann Double\-klicken Sie auf **FspConfigWizard.exe**.  
  
2.  Starten Sie den Assistenten mit einer dieser Methoden, und klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
3.  Geben Sie auf der Seite **Angeben eines Verbunddienstnamens** unter **Verbunddienstname** den Namen für den Verbunddienst ein, für den dieser Computer in der Proxyrolle agieren wird.  
  
4.  Legen Sie basierend auf Ihren bestimmten Netzwerkanforderungen fest, ob Sie einen HTTP-Proxyserver verwenden müssen, um Anforderungen an den Verbunddienst weiterzuleiten. Falls ja, aktivieren Sie das Kontrollkästchen zum **Verwenden eines HTTP-Proxyservers beim Senden von Andorderungen an diesen Verbunddienst**, geben Sie unter **HTTP-Proxyserveradresse** die Adresse des Proxyservers ein, klicken Sie auf **Verbindung testen**, um die Konnektivität zu prüfen, und klicken Sie dann auf **Weiter**.  
  
5.  Wenn Sie dazu aufgefordert werden, geben Sie die zum Einrichten einer Vertrauensstellung zwischen diesem Verbundserverproxy und dem Verbunddienst erforderlichen Anmeldeinformationen an.  
  
    Standardmäßig wird nur das Dienstkonto ein, die den Verbunddienst oder ein Mitglied der lokalen "Vordefiniert"\\Gruppe "Administratoren" kann einen Verbundserverproxy autorisieren.  
  
6.  Überprüfen Sie die Details auf der Seite **Bereit zum Anwenden der Einstellungen**. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter**, um die Konfiguration dieses Computer mit diesen Proxyeinstellungen zu beginnen.  
  
7.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
    Es ist kein Microsoft Management Console \(MMC\) ausrichten\-in zum Verwalten von Verbund-Server-Proxys. Verwenden Sie Windows PowerShell-Cmdlets, um Einstellungen für die einzelnen Proxys die Verbund-Server in Ihrer Organisation zu konfigurieren.  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>Konfigurieren einer alternativen TCP\/IP-Port für den Proxybetrieb  
Standardmäßig ist der Verbundserverproxy-Dienst konfiguriert, um TCP-Port 443 für HTTPS-Datenverkehr und Port 80 für HTTP-Datenverkehr für die Kommunikation mit dem Verbundserver zu verwenden. Wenn Sie andere Ports, beispielsweise TCP-Port 444 für HTTPS und Port 81 für HTTP, konfigurieren möchten, müssen Sie die folgenden Aufgaben durchführen.  
  
> [!NOTE]  
> Wenn Sie beabsichtigen, die Bereitstellung von AD FS Betrieb unter alternativen TCP anfänglich\/IP-Ports, sollten Sie zunächst die Ports ändern, in Ihrer IIS-protokollbindungen für HTTP und HTTPS auf dem Verbundserver und Verbundserverproxy-Computer. Dies sollte erfolgen, bevor Sie die AD FS-Konfigurations-Assistenten für die Erstkonfiguration ausgeführt. Wenn Sie Internet Information Services konfigurieren \(IIS\) zuerst Ihre alternativen TCP\/IP-Port-Einstellungen werden ermittelt, wenn der Assistent\-je Konfiguration, die in AD FS auftritt und das folgende Verfahren ist nicht erforderlich. Wenn Sie die Porteinstellungen später ändern möchten, aktualisieren Sie zuerst die IIS-Protokollbindungen, und verwenden Sie dann das folgende Verfahren, um die Porteinstellungen entsprechend zu aktualisieren. Weitere Informationen zum Bearbeiten von IIS-Bindungen finden Sie unter [Artikel 149605](https://go.microsoft.com/fwlink/?LinkId=190275) in der Microsoft Knowledge Base.  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>So konfigurieren Sie alternative TCP\/IP-Ports für den Verbundserverproxy verwenden  
  
1.  Konfigurieren Sie den Verbundserver zur Verwendung der Nichtstandardports.  
  
    Zu diesem Zweck legen Sie den nicht standardmäßigen Portnummer, einschließlich von mit der *HttpsPort* und *HttpPort* Optionen als Teil der **festgelegt\-ADFSProperties** Cmdlet. Verwenden Sie die folgenden Befehle in der Windows PowerShell-Sitzung auf dem verbundservercomputer z. B. zum Konfigurieren dieser Ports:  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  Konfigurieren des Verbundserverproxys, um die Verwendung der nichtstandardports.  
  
    Zu diesem Zweck legen Sie den nicht standardmäßigen Portnummer, einschließlich von mit der *HttpsPort* und *HttpPort* Optionen als Teil der **festgelegt\-ADFSProxyProperties** -Cmdlet. Verwenden Sie die folgenden Befehle in der Windows PowerShell-Sitzung auf dem verbundservercomputer z. B. zum Konfigurieren dieser Ports:  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > Endpunkt-URLs sind nicht für die Verbundserverproxy-Dienst standardmäßig aktiviert. Wenn Sie eine Neuinstallation des Verbund-Server konfigurieren, müssen Sie zuerst Federation Server Proxy-Dienstendpunkte aktivieren. Z. B. davon aus, dass für alle Endpunkte, die auf das Beispiel in diesem Verfahren bezieht Sie sie für den Proxy aktiviert haben durch Auswahl in der AD FS-Verwaltungs-Snap\-in auswählen und dann **auf Proxy aktivieren**.  
  
3.  Aktualisieren Sie die IIS-Installation auf dem Verbundserverproxy also diese Security Assertion Markup Language \(SAML\) und WS\-vertrauen Endpunkte werden konfiguriert, um die aktualisierte Portnummer widerspiegeln. Zu diesem Zweck können Sie Notepad Folgendes in der Datei "Web.config" ändern in SystemDrive%\\Inetpub\\Adfs\\ls\\ für die Verbundserverproxy-Computer. Z. B. vorausgesetzt, Sie einen Verbundserver mit dem Namen sts1.contoso.com haben und ist die neue Portnummer 444, navigieren Sie zu, und öffnen Sie die Datei Web.config in Editor, für die Verbundserverproxy-Computer, suchen Sie den folgenden Abschnitt, ändern Sie die Portnummer wie Im folgenden aufgeführt, und speichern und beenden Sie den Editor.  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  Hinzufügen des Federation Server Proxy-Dienstbenutzerkontos an die Access Control List \(ACL\) für den entsprechenden Endpunkt-URLs. Für die Portnummer beispielsweise 1234 und das Benutzerkonto, mit dem die AD-FSfederation Proxys für den Server ausgeführt, wird-Dienst unter den integrierten\-im NETZWERKDIENST-Konto, geben Sie den folgenden Befehl an einer Eingabeaufforderung:  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    Die vorherigen Befehle müssen auf dem Verbundserver und die Verbundserverproxy-Computer ausgeführt werden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Das Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

