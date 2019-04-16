---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: Configure a Computer for the Federation Server Proxy Role
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2a89bab2fd1af1a1d7234da29f2025b4b12d6774
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>Configure a Computer for the Federation Server Proxy Role

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie einen Computer mit den erforderlichen Zertifikaten konfiguriert und den Verbunddienstproxy-Rollendienst installiert haben, können Sie so konfigurieren Sie den Computer, um einen Verbundserverproxy verwendet werden. Sie können das folgende Verfahren, damit der Computer in der Verbundserverproxy-Rolle verwendet wird.  
  
> [!IMPORTANT]  
> Bevor Sie dieses Verfahren verwenden, um die Verbundserverproxy-Computer konfigurieren, stellen Sie sicher, dass Sie alle Schrittebefolgt haben [Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md) in der Reihenfolge, in der sie aufgelistet sind. Stellen Sie sicher, dass die mindestens ein Verbundserver bereitgestellt wurde und dass alle erforderlichen Anmeldeinformationen für die Autorisierung einer Verbundserverproxy-Konfigurations implementiert sind. Außerdem müssen Sie Secure Sockets Layer \(SSL\) Bindungen konfigurieren, auf der Standardwebsite oder dieser Assistent wird nicht gestartet. Alle diese Aufgaben müssen abgeschlossen sein, bevor dieser Verbundserverproxy ordnungsgemäß kann.  
  
Nachdem Sie das Einrichten des Computers abgeschlossen haben, stellen Sie sicher, dass der Verbundserverproxy wie erwartet funktioniert. Weitere Informationen finden Sie unter [überprüfen Sie, ob ein Verbundserver Betriebsbereitschaft](Verify-That-a-Federation-Server-Proxy-Is-Operational.md).  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>Konfigurieren eines Computers für die Verbundserverproxy-Rolle  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Federation Server-Konfigurations-Assistenten zu starten. Um den Assistenten zu starten, führen Sie eine der folgenden:  
  
    -   Auf der **starten** geben**AD FS-Konfigurationsassistenten für den Verbundserverproxy**, und drücken Sie dann die EINGABETASTE.  
  
    -   Jederzeit nach Abschluss des Setup-Assistenten öffnen Windows Explorer, navigieren Sie zu der **C:\\Windows\\ADFS** Ordner, und klicken Sie dann Variablenname klicken **FspConfigWizard.exe**.  
  
2.  Mit einer dieser Methoden, starten Sie den Assistenten, und klicken Sie auf die **Willkommen** auf **Weiter**.  
  
3.  Auf der **angeben eines Verbunddienstnamens** Seite unter **verbunddienstname**, geben Sie den Namen, die den Verbunddienst darstellt, für die diese Computer die Proxyrolle fungiert.  
  
4.  Basierend auf Ihren bestimmten Netzwerkanforderungen, bestimmen Sie, ob Sie einen HTTP-Proxyserver zu verwenden, um die Anforderungen an den Verbunddienst weiterleiten müssen. Wenn dies der Fall ist, wählen Sie die **einen HTTP-Proxyserver verwenden, beim Senden von Anfragen an diesen Verbunddienst** Kontrollkästchen unter **HTTP-Proxyserveradresse** Geben Sie die Adresse des Proxyservers ein, klicken Sie auf **Testverbindung** überprüfen die Verbindung, und klicken Sie dann auf **Weiter**.  
  
5.  Wenn Sie aufgefordert werden, geben Sie die Anmeldeinformationen, die zum Herstellen einer Vertrauensstellung zwischen diesem Verbundserverproxy und den Verbunddienst erforderlich sind.  
  
    Standardmäßig kann nur die von den Verbunddienst oder ein Mitglied der lokalen Prinzipalobjekt verwendete Dienstkonto einen Verbundserverproxy autorisieren.  
  
6.  Auf der **bereit zum Anwenden der Einstellungen** Seite, überprüfen Sie die Detail. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter** um Konfiguration dieses Computer mit diesen Proxyeinstellungen zu beginnen.  
  
7.  Auf der **Konfigurationsergebnisse** Seite, überprüfen Sie die Ergebnisse. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
    Es gibt keine \(MMC\) snap\ Microsoft Management Console-in für die Verwaltung von Federation Server Proxys verwenden. Verwenden Sie Windows PowerShell-Cmdlets, um Einstellungen für die Proxys Federation Server in Ihrer Organisation zu konfigurieren.  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>Konfigurieren einen alternativen TCP/IP TCP/IP-Port für den Proxybetrieb  
Standardmäßig ist der Verbundserverproxy-Dienst so konfiguriert, dass TCP-Port 443 für HTTPS-Datenverkehr und Port 80 für HTTP-Datenverkehr für die Kommunikation mit dem Verbundserver verwendet werden. Die folgenden Aufgaben müssen abgeschlossen werden, um andere Ports, z.B. TCP-Port 444 für HTTPS und Port 81 für HTTP, konfigurieren.  
  
> [!NOTE]  
> Wenn Sie AD FS für den Betrieb unter alternativen TCP/IP TCP/IP-Ports anfänglich bereitstellen möchten, sollten Sie zunächst Ports in Ihren IIS-protokollbindungen für HTTP und HTTPS auf dem Verbundserver und die Verbundserverproxy-Computer ändern. Dies sollte vor dem Ausführen der AD FS-Konfigurations-Assistenten für die Erstkonfiguration auftreten. Wenn Sie Internetinformationsdienste \(IIS\) zuerst konfigurieren, werden Ihre alternativen TCP/IP TCP/IP-Porteinstellungen erkannt, wenn Wizard\-basierten Konfiguration in AD FS auftritt und das folgende Verfahren nicht erforderlich ist. Wenn Sie die Porteinstellungen später ändern möchten, aktualisieren Sie die IIS-protokollbindungen zuerst, und klicken Sie dann mithilfe des folgenden Verfahrens zum Aktualisieren von Port-Einstellungen entsprechend. Weitere Informationen zum Bearbeiten von IIS-Bindungen finden Sie unter [Artikel 149605](https://go.microsoft.com/fwlink/?LinkId=190275) in der Microsoft Knowledge Base.  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>So konfigurieren Sie alternative TCP/IP TCP/IP-Ports für die Verbundserverproxys verwenden  
  
1.  Konfigurieren Sie den Verbundserver zur Verwendung der nichtstandardports.  
  
    Legen Sie dazu die nicht standardmäßige Portnummer an, einschließlich mit der *HttpsPort* und *HttpPort* Optionen als Teil der **Set-ADFSProperties** Cmdlet. Verwenden Sie folgenden Ports konfigurieren, z.B. die folgenden Befehle in der Windows PowerShell-Sitzung auf dem Verbundservercomputer:  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  Konfigurieren des Verbundserverproxys zur Verwendung der nichtstandardports.  
  
    Legen Sie dazu die nicht standardmäßige Portnummer an, einschließlich mit der *HttpsPort* und *HttpPort* Optionen als Teil der **Set-ADFSProxyProperties** Cmdlet. Verwenden Sie folgenden Ports konfigurieren, z.B. die folgenden Befehle in der Windows PowerShell-Sitzung auf dem Verbundservercomputer:  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > Endpunkt-URLs sind nicht für die Verbundserverproxy-Dienst standardmäßig aktiviert. Wenn Sie eine neue Installation von Federation Server konfigurieren, müssen Sie zunächst Federation Server Proxy-Endpunkte aktivieren. Angenommen, es wird vorausgesetzt, die für alle Endpunkte, die auf das Beispiel in diesem Verfahren werden für Proxy durch Auswahl in AD FS-Verwaltungs-Snap-In, und wählen Sie dann aktiviert ist **auf Proxy aktivieren**.  
  
3.  Aktualisieren Sie die IIS-Installation auf dem Verbundserverproxy, sodass Security Assertion Markup Language \(SAML\) und WS-Trust-Endpunkte konfiguriert sind, um die aktualisierte Portnummer widerspiegeln. Editor können Sie dazu um Folgendes in der Datei "Web.config" zu ändern, die auf systemdrive%\\inetpub\\adfs\\ls\\ auf der Verbundserverproxy-Computer befindet. Zum Beispiel angenommen, Sie einen Verbundserver mit dem Namen sts1.contoso.com haben und die neue Portnummer 444 ist, suchen Sie und öffnen Sie die Datei "Web.config" im Editor auf der Verbundserverproxy-Computer, suchen den folgenden Abschnitt, ändern die Portnummer wie unten markiert, und klicken Sie dann speichern und schließen Sie Editor.  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  Hinzufügen von Federation Server Proxybenutzerkonto für den die Steuerung des Zugriffs Liste \(ACL\) für die entsprechenden Endpunkt-URLs. Z.B. Geben Sie die Portnummer 1234 ist und das Benutzerkonto, mit dem Ausführen der AD-FSfederation-Dienst unter, dem integrierten Netzwerkdienstkonto ist, dann an einer Eingabeaufforderung den folgenden Befehl ein:  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    Die vorherigen Befehle müssen auf dem Verbundserver und die Verbundserverproxy-Computer ausgeführt werden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

