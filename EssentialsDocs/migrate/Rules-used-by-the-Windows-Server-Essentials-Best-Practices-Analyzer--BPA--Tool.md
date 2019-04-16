---
title: Mit dem Tool Windows Server Essentials Best Practices Analyzer (BPA) verwendete Regeln
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37e1dae7-586c-4dd7-bf83-7e14a9567c8f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c205bc8ff75bf64d4a13a7d799988c9d1ebe1a22
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="rules-used-by-the-windows-server-essentials-best-practices-analyzer-bpa-tool"></a>Mit dem Tool Windows Server Essentials Best Practices Analyzer (BPA) verwendete Regeln

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieser Artikel beschreibt die Wartung von der Windows Server Essentials Best Practices Analyzer (BPA) verwendeten Regeln. Der BPA überprüft einen Server, der Windows Server Essentials ausgeführt wird, und zeigt einen Bericht, der mit problembeschreibungen und Empfehlungen zur Fehlerbehebung. Die Empfehlungen werden von der Product Supportorganisation für Windows Server Essentials entwickelt.  
  
## <a name="using-the-tool"></a>Mithilfe des Tools  
 Es ist eine standardmäßige Vorgehensweise, wenn Sie zum Windows Server Essentials aus Windows Server2011 Essentials, Windows Small Business Server2011 Essentials oder Windows Home Server2011, führen Sie den BPA auf dem Zielserver nach Abschluss der Migration Ihrer Einstellungen und Daten migrieren. Sie können das Tool jederzeit über das Dashboard ausführen.  
  
#### <a name="to-run-the--windows-server-essentials-bpa-on-the-server"></a>Zum Ausführen von BPA für Windows Server Essentials auf dem Server  
  
1.  Melden Sie sich an den Server als Administrator, und öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf dem Dashboard auf der **Geräte** Registerkarte.  
  
3.  Auf der **Servertasks** Bereich, klicken Sie auf **Best Practices Analyzer**.  
  
4.  Überprüfen Sie jede BPA-Meldung, und folgen Sie die Anweisungen, um Probleme zu beheben, falls erforderlich.  
  
## <a name="rules-used-by-the-best-practices-analyzer"></a>Von der Best Practices Analyzer verwendete Regeln  
  
### <a name="disable-ip-filtering"></a>IP-Filterung deaktivieren  
 **Problem:** IP-Filterung ist zurzeit auf dem Server aktiviert. Sie müssen das IP-Filterung deaktivieren.  
  
 **Auswirkung:** Wenn IP-Filterung aktiviert ist, kann der Netzwerkverkehr blockiert werden.  
  
 **Lösung:**  
  
##### <a name="to-disable-ip-filtering"></a>So deaktivieren Sie die IP-Filterung  
  
1.  Öffnen Sie regedit.exe auf dem Server.  
  
2.  Navigieren Sie zu "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters".  
  
3.  Mit der rechten Maustaste **EnableSecurityFilters**, und klicken Sie dann auf **ändern**.  
  
4.  In der **DWORD-Wert bearbeiten (32-Bit) Wert** ändern die **Wert** 0 (null) ein, und klicken Sie dann auf **OK**.  
  
5.  Starten Sie den Server neu, um die Änderung zu übernehmen.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-set-to-start-automatically-by-default"></a>Der Dienst Distributed Transaction Coordinator (MSDTC) sollte für den automatischen Start standardmäßig festgelegt werden  
 **Problem:** der MSDTC-Dienst ist nicht für den automatischen Start konfiguriert  
  
 **Auswirkung:** der MSDTC-Dienst möglicherweise nicht automatisch starten beim Starten des Servers. Wenn der Dienst beendet wird, können bestimmte SQL Server- oder COM-Funktionen fehlschlagen. Daher können die Anwendungen mit Microsoft SQL Server- oder COM-Funktionen nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-msdtc-service-to-start-automatically"></a>So konfigurieren Sie den MSDTC-Dienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Distributed Transaction Coordinator** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatisch (verzögerter Start)**, und klicken Sie dann auf **OK**.  
  
### <a name="the-netlogon-service-should-be-configured-to-start-automatically-by-default"></a>Der Netlogon-Dienst sollte so konfiguriert werden, dass standardmäßig automatisch starten  
 **Problem:** der Netlogon-Dienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** der Netlogon-Dienst möglicherweise nicht automatisch starten beim Starten des Servers. Wenn der Dienst beendet wird, kann der Server nicht authentifiziert Benutzer und Dienste.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-netlogon-service-to-start-automatically"></a>So konfigurieren Sie den Netlogon-Dienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Netlogon** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-dns-client-service-should-be-configured-to-start-automatically-by-default"></a>Der DNS-Clientdienst sollte so konfiguriert werden, dass standardmäßig automatisch starten  
 **Problem:** der DNS-Clientdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** der DNS-Clientdienst möglicherweise nicht automatisch starten beim Starten des Servers. Wenn dieser Dienst beendet wird, der Server zum Auflösen von DNS-Namen möglicherweise nicht.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dns-client-service-to-start-automatically"></a>So konfigurieren Sie den DNS-Clientdienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DNS-Client** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-dns-server-service-should-be-configured-to-start-automatically-by-default"></a>Der DNS-Serverdienst sollte so konfiguriert werden, dass standardmäßig automatisch starten  
 **Problem:** der DNS-Serverdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** der DNS-Serverdienst kann nicht gestartet werden automatisch beim Starten des Servers. Wenn dieser Dienst beendet wird, werden die DNS-Updates nicht ausgeführt.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dns-server-service-to-start-automatically"></a>So konfigurieren Sie den DNS-Serverdienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DNS-Server** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="active-directory-web-services-is-not-set-to-the-default-start-mode"></a>Active Directory-Webdienste ist nicht der Standardstartmodus festgelegt.  
 **Problem:** Active Directory-Webdienste ist nicht auf der Standardstartmodus automatisch festgelegt.  
  
 **Auswirkung:** Active Directory-Webdienste (ADWS) ist nicht der Standardstartmodus automatisch festgelegt. Wenn ADWS auf dem Server beendet oder deaktiviert, Clientanwendungen wie z.B. Active Directory-Modul für Windows PowerShell oder das Active Directory-Verwaltungscenter nicht zugreifen oder Verwalten von Verzeichnisdienstinstanzen, die auf diesem Server ausgeführt werden. Weitere Informationen finden Sie unter [What's New in AD DS: Active Directory-Webdienste](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in der technischen Bibliothek für Windows Server.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-active-directory-web-services-service-to-start-automatically"></a>So konfigurieren Sie die Active Directory-Webdienste-Dienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Active Directory-Webdienste** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-dhcp-client-service-should-be-configured-to-start-automatically-by-default"></a>Der DHCP-Clientdienst sollte so konfiguriert werden, dass standardmäßig automatisch starten  
 **Problem:** der DHCP-Clientdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** der DHCP-Clientdienst wird nicht automatisch starten beim Starten des Servers. Wenn dieser Dienst beendet wird, können nicht Clientcomputer eine IP-Adresse vom Server empfangen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dhcp-client-service-to-start-automatically"></a>So konfigurieren Sie den DHCP-Clientdienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DHCP-Client** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-iis-admin-service-should-be-configured-to-start-automatically-by-default"></a>Der IIS-Verwaltungsdienst sollte so konfiguriert werden, dass standardmäßig automatisch gestartet  
 **Problem:** der IIS-Verwaltungsdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** der IIS-Verwaltungsdienst wird nicht automatisch starten beim Starten des Servers. Wenn dieser Dienst beendet wird, können Sie nicht auf Websites, die auf dem Server, z.B. Remotewebzugriff zugreifen sein.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-iis-admin-service-to-start-automatically"></a>So konfigurieren Sie IIS-Verwaltungsdienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **IIS-Verwaltungsdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-world-wide-web-publishing-service-should-be-configured-to-start-automatically-by-default"></a>Der WWW-Publishingdienst sollte für den automatischen Start standardmäßig konfiguriert werden  
 **Problem:** der WWW-Publishingdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** der WWW-Publishingdienst kann nicht gestartet werden automatisch beim Starten des Servers. Wenn dieser Dienst beendet wird, können Sie nicht auf Websites, die auf dem Server, z.B. Remotewebzugriff zugreifen sein.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-world-wide-web-publishing-service-to-start-automatically"></a>Der WWW-Publishingdienst für den automatischen Start konfigurieren.  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **WWW-Publishingdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-remote-registry-service-should-be-configured-to-start-automatically-by-default"></a>Der Remoteregistrierungsdienst sollte so konfiguriert werden, dass standardmäßig automatisch gestartet  
 **Problem:** der Remoteregistrierungsdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  
  
 Der Remoteregistrierungsdienst wird möglicherweise nicht automatisch gestartet, wenn der Server startet. Wenn dieser Dienst beendet wird, möglicherweise einige Netzwerkvorgänge Remote ausführen möglich.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-remote-registry-service-to-start-automatically"></a>So konfigurieren Sie den Remoteregistrierungsdienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Remoteregistrierung** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-remote-desktop-gateway-service-should-be-configured-to-start-automatically-by-default"></a>Der Remotedesktopgateway-Dienst sollte für den automatischen Start standardmäßig konfiguriert werden  
 **Problem:** der Remotedesktopgateway-Dienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, Benutzer können möglicherweise nicht auf Computern mit Remote Web Access zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-remote-desktop-gateway-service-to-start-automatically"></a>So konfigurieren Sie den Remotedesktopgateway-Dienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Remotedesktopgateway** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatisch (verzögerter Start)**, und klicken Sie dann auf **OK**.  
  
### <a name="the-windows-time-service-should-be-configured-to-start-automatically-by-default"></a>Windows-Zeitdienst sollte so konfiguriert werden, dass standardmäßig automatisch gestartet  
 **Problem:** Windows-Zeitdienst wird nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, sind Zeit- und datumssynchronisierung nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-windows-time-service-to-start-automatically"></a>So konfigurieren Sie die Windows-Zeitdienst für den automatischen Start  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Windows-Zeitdienst** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **allgemeine** Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-started"></a>Der Distributed Transaction Coordinator (MSDTC)-Dienst sollte gestartet werden  
 **Problem:** der MSDTC-Dienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, können bestimmte SQL Server- oder COM-Funktionen fehlschlagen. Daher können die Anwendungen mit Microsoft SQL Server- oder COM-Funktionen nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-start-the-distributed-transaction-coordinator-service"></a>Den Distributed Transaction Coordinator-Dienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Distributed Transaction Coordinator** Dienstes, und klicken Sie dann auf **starten**.  
  
### <a name="the-netlogon-service-should-be-started"></a>Der Netlogon-Dienst sollte gestartet werden  
 **Problem:** der Netlogon-Dienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst nicht gestartet wird, authentifiziert der Server möglicherweise nicht Benutzern und Diensten.  
  
 **Lösung:**  
  
##### <a name="to-start-the-netlogon-service"></a>Den Netlogon-Dienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Netlogon** Dienstes, und klicken Sie dann auf **starten**.  
  
### <a name="the-dns-client-service-should-be-started"></a>Der DNS-Clientdienst sollte gestartet werden  
 **Problem:** der DNS-Clientdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst nicht gestartet wurde, der Server ist möglicherweise keine DNS-Namen auflösen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dns-client-service"></a>Den DNS-Clientdienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DNS-Client** Dienstes, und klicken Sie dann auf **starten**.  
  
### <a name="the-dns-server-service-should-be-started"></a>Der DNS-Serverdienst sollte gestartet werden  
 **Problem:** der DNS-Serverdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn der DNS-Serverdienst nicht gestartet wurde, wird DNS-Updates möglicherweise nicht ausgeführt.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dns-server-service"></a>Den DNS-Serverdienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DNS-Server** Dienstes, und klicken Sie dann auf **starten**.  
  
### <a name="active-directory-web-services-is-not-started"></a>Active Directory-Webdienste wurden nicht gestartet.  
 **Problem:** Active Directory-Webdienste wurden nicht gestartet.  
  
 **Auswirkung:** Active Directory-Webdienste (ADWS) wurde nicht gestartet. Wenn ADWS auf dem Server beendet oder deaktiviert, Clientanwendungen wie z.B. Active Directory-Modul für Windows PowerShell oder das Active Directory-Verwaltungscenter nicht zugreifen oder Verwalten von Verzeichnisdienstinstanzen, die auf diesem Server ausgeführt werden. Weitere Informationen finden Sie unter [What's New in AD DS: Active Directory-Webdienste](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in der technischen Bibliothek für Windows Server.  
  
 **Lösung:**  
  
##### <a name="to-start-the-active-directory-web-services-service"></a>Um den Active Directory-Webdienste-Dienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **Active Directory-Webdienste**, und klicken Sie dann auf **starten**.  
  
### <a name="the-dhcp-client-service-should-be-started"></a>Der DHCP-Clientdienst sollte gestartet werden  
 **Problem:** der DHCP-Clientdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, können keine Clientcomputer eine IP-Adresse vom Server empfangen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dhcp-client-service"></a>Den DHCP-Clientdienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DHCP-Client** Dienstes, und klicken Sie dann auf **starten**.  
  
### <a name="the-iis-admin-service-should-be-started"></a>Der IIS-Verwaltungsdienst sollte gestartet werden  
 **Problem:** der IIS-Verwaltungsdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, ist Sie möglicherweise nicht auf Websites, die auf dem Server, z.B. Remotewebzugriff zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-iis-admin-service"></a>Der IIS-Verwaltungsdienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **IIS-Verwaltungsdienst**, und klicken Sie dann auf **starten**.  
  
### <a name="the-world-wide-web-publishing-service-should-be-started"></a>Der WWW-Publishingdienst sollte gestartet werden  
 **Problem:** der WWW-Publishingdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, ist Sie möglicherweise nicht auf Websites, die auf dem Server, z.B. Remotewebzugriff zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-world-wide-web-publishing-service"></a>Starten Sie den WWW-Publishingdienst.  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **WWW-Publishingdienst**, und klicken Sie dann auf **starten**.  
  
### <a name="the-remote-desktop-gateway-service-should-be-started"></a>Der Remotedesktopgateway-Dienst sollte gestartet werden  
 **Problem:** der Remotedesktopgateway-Dienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, Benutzer können möglicherweise nicht auf Computern mit Remote Web Access zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-remote-desktop-gateway-service"></a>Starten Sie den Remotedesktopgateway-Diensts  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Remotedesktopgateway** Dienstes, und klicken Sie dann auf **starten**.  
  
### <a name="the-windows-time-service-should-be-started"></a>Windows-Zeitdienst sollte gestartet werden  
 **Problem:** Windows-Zeitdienst wird nicht auf dem Server ausgeführt.  
  
 **Auswirkung:** Wenn dieser Dienst beendet wird, Zeit- und datumssynchronisierung werden nicht zur Verfügung stehen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-windows-time-service"></a>Der Windows-Zeitdienst starten  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Windows-Zeitdienst** Dienstes, und klicken Sie dann auf **starten**.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-logon-account-should-be-nt-authoritynetwork-service"></a>Das Anmeldekonto für den Distributed Transaction Coordinator (MSDTC) sollte "NT-Autorität\netzwerkdienst" sein.  
 **Problem:** das Standardanmeldekonto für den Dienst Distributed Transaction Coordinator (MSDTC) geändert wird.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die Berechtigungen, die erforderlich sind, wie erwartet. Anwendungen, die SQL Server- oder COM-Funktionen verwenden, funktionieren daher möglicherweise nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-change-the-logon-account-for-the-service"></a>So ändern Sie das Anmeldekonto für den Dienst  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Distributed Transaction Coordinator** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **dieses Konto**, Typ **NT-Autorität\netzwerkdienst**, und klicken Sie dann auf **OK**.  
  
### <a name="the-netlogon-service-should-use-the-local-system-account-as-its-logon-account"></a>Der Netlogon-Dienst sollte das lokale Systemkonto als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den Anmeldedienst wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die Berechtigungen, die erforderlich sind, wie erwartet. Daher kann der Server nicht authentifiziert Benutzer und Dienste.  
  
 **Lösung:**  
  
##### <a name="to-change-the-netlogon-service-logon-account"></a>So ändern Sie das Anmeldekonto der Netlogon-Dienst  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Netlogon** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **lokales Systemkonto**.  
  
### <a name="the-dns-client-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Der DNS-Clientdienst sollte das Konto "NT-Autorität\netzwerkdienst" als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den DNS-Clientdienst wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die Berechtigungen, die erforderlich sind, wie erwartet. Daher kann der Server keine DNS-Namen auflösen können.  
  
 **Lösung:**  
  
##### <a name="to-change-the-dns-client-service-logon-account"></a>So ändern Sie das Anmeldekonto für den DNS-Client  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DNS-Client** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **dieses Konto**, und geben Sie dann **NT-Autorität\netzwerkdienst**.  
  
### <a name="the-dns-server-service-should-use-the-local-system-account-as-its-logon-account"></a>Der DNS-Serverdienst sollte das lokale Systemkonto als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den DNS-Serverdienst wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die Berechtigungen, die erforderlich sind, wie erwartet. Daher können der DNS-Updates nicht auftreten.  
  
 **Lösung:**  
  
##### <a name="to-change-the-dns-server-service-logon-account"></a>So ändern Sie das Anmeldekonto für DNS-Server-Dienst  
  
1.  Öffnen Sie Services.msc auf dem Server  
  
2.  Mit der rechten Maustaste die **DNS-Server** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **lokales Systemkonto**.  
  
### <a name="active-directory-web-services-is-not-the-default-logon-account"></a>Active Directory-Webdienste ist nicht das Standardanmeldekonto  
 **Problem:** Active Directory-Webdienste ist nicht das Standardanmeldekonto. Wird standardmäßig das Anmeldekonto festgelegt ist, um **lokales Systemkonto**.  
  
 **Auswirkung:** Active Directory-Webdienste (ADWS) wurde nicht gestartet. Wenn ADWS auf dem Server beendet oder deaktiviert, Clientanwendungen wie z.B. Active Directory-Modul für Windows PowerShell oder das Active Directory-Verwaltungscenter nicht zugreifen oder Verwalten von Verzeichnisdienstinstanzen, die auf diesem Server ausgeführt werden. Weitere Informationen finden Sie unter [What's New in AD DS: Active Directory-Webdienste](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in der technischen Bibliothek für Windows Server.  
  
 **Lösung:**  
  
##### <a name="to-change-the-active-directory-web-services-logon-account"></a>So ändern Sie das Anmeldekonto für den Active Directory-Webdienste  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **Active Directory-Webdienste**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern der **Starttyp** auf **automatische**, und klicken Sie dann auf **OK**.  
  
4.  In Active Directory-Webdiensten **Eigenschaften**, klicken Sie auf die **anmelden** Registerkarte.  
  
5.  Wählen Sie die **lokales Systemkonto** aus, und klicken Sie dann auf **OK**.  
  
### <a name="the-windows-update-service-should-use-the-local-system-account-as-its-logon-account"></a>Der Windows Update-Dienst sollte das lokale Systemkonto als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den Dienst für automatische Updates wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die Berechtigungen, die erforderlich sind, wie erwartet. Daher kann der Server keine automatischen Updates empfangen.  
  
 **Lösung:**  
  
##### <a name="to-change-the-windows-update-service-logon-account"></a>So ändern Sie das Anmeldekonto für Windows Update-Dienst  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Windows Update** Service, und klicken Sie dann auf Eigenschaften.  
  
3.  Auf der **anmelden** Registerkarte **lokales Systemkonto**.  
  
### <a name="the-dhcp-client-service-should-use-the-nt-authoritylocalservice-account-as-its-logon-account"></a>Der DHCP-Clientdienst sollte das Konto "NT AUTORITÄT\LocalService" als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den DHCP-Clientdienst wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die Berechtigungen, die erforderlich sind, wie erwartet. Daher erhalten der Clientcomputer keine IP-Adressen vom Server.  
  
 **Lösung:**  
  
##### <a name="to-change-the-dhcp-client-service-logon-account"></a>So ändern Sie das Anmeldekonto für den DHCP-Client  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **DHCP-Client** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **dieses Konto**, und geben Sie dann **NT-Autorität\Lokaler Dienst**.  
  
### <a name="the-iis-admin-service-should-use-the-local-system-account-as-its-logon-account"></a>IIS-Verwaltungsdienst sollte das lokale Systemkonto als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den IIS-Verwaltungsdienst wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht über die erforderlichen Berechtigungen, die erwartungsgemäß erforderlich sind. Sie können daher nicht auf Websites, die auf dem Server, z.B. Remotewebzugriff zugreifen sein.  
  
 **Lösung:**  
  
##### <a name="to-change-the-service-logon-account"></a>So ändern Sie das Anmeldekonto  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **IIS-Verwaltungsdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **lokales Systemkonto**.  
  
### <a name="the-world-wide-web-publishing-service-should-use-the-local-system-account-as-its-logon-account"></a>Der WWW-Publishingdienst sollte das lokale Systemkonto als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den WWW-Publishingdienst wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die Berechtigungen, die erforderlich sind, wie erwartet. Sie können daher nicht auf Websites, die auf dem Server, z.B. Remotewebzugriff zugreifen sein.  
  
 **Lösung:**  
  
##### <a name="to-change-the-world-wide-web-publishing-service-logon-account"></a>So ändern Sie das Anmeldekonto für den WWW-Publishingdienst.  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste **WWW-Publishingdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **lokales Systemkonto**.  
  
### <a name="the-remote-desktop-gateway-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Der Remotedesktopgateway-Dienst sollte das Konto NT-Autorität\netzwerkdienst als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den Remotedesktopgateway-Dienst geändert wird.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die entsprechenden Berechtigungen wie erwartet. Daher können Benutzer können auf Computern mit Remote Web Access nicht.  
  
 **Lösung:**  
  
##### <a name="to-change-the-remote-desktop-gateway-service-logon-account"></a>So ändern Sie das Anmeldekonto für den Remotedesktop-Gatewayserver  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Remotedesktopgateway** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **dieses Konto**, und geben Sie dann **NT-Autorität\netzwerkdienst**.  
  
### <a name="the-windows-time-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Windows-Zeitdienst sollte das Konto NT-Autorität\netzwerkdienst als Anmeldekonto verwenden.  
 **Problem:** das Standardanmeldekonto für den Windows-Zeitdienst wurde geändert.  
  
 **Auswirkung:** der Dienst möglicherweise nicht die entsprechenden Berechtigungen wie erwartet. Daher Synchronisierung von Datum und Uhrzeit möglicherweise nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-change-the-windows-time-service-logon-account"></a>So ändern Sie das Anmeldekonto für den Windows-Zeitdienst  
  
1.  Öffnen Sie Services.msc auf dem Server.  
  
2.  Mit der rechten Maustaste die **Windows-Zeitdienst** Dienstes, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **anmelden** Registerkarte **dieses Konto**, und geben Sie dann **NT-Autorität\Lokaler Dienst**.  
  
### <a name="the-built-in-administrators-group-does-not-have-the-right-to-log-on-as-batch-job"></a>Die integrierte Administratorengruppe das Recht zum Anmelden als Stapelverarbeitungsauftrag keinen  
 **Problem:** der integrierten Gruppe "Administratoren" verfügt nicht über das Recht zum Anmelden als Stapelverarbeitungsauftrag.  
  
 **Auswirkung:**, wenn der Administrator eine Warnung erstellt und so konfiguriert, dass ausgeführt werden, wenn der Administrator nicht angemeldet ist, die Warnung mit Fehlercode 2147943785 fehl.  
  
 **Lösung:** Informationen dazu, wie Sie die integrierten Administratoren Gruppe die Berechtigung zum Anmelden als Batchauftrag erteilen, finden Sie unter [der integrierten Gruppe "Administratoren" das Recht zum Anmelden als Batchauftrag erteilen](https://technet.microsoft.com/library/jj635076) (https://technet.microsoft.com/library/jj635076).  
  
### <a name="the-windows-firewall-is-turned-off"></a>Die Windows-Firewall ist deaktiviert  
 **Problem:** Windows-Firewall ist deaktiviert. Der Standardwert ist auf.  
  
 **Auswirkung:** abhängig von Ihren Firewalleinstellungen Windows-Firewall helfen Ihres Servers und Netzwerks vor bösartigen Aktivitäten schützen, indem Sie einige Informationen über den Server übergeben blockiert.  
  
 **Lösung:**  
  
##### <a name="to-turn-on-windows-firewall-on-the-server"></a>So aktivieren Sie Windows-Firewall auf dem Server  
  
1.  Öffnen Sie die Systemsteuerung auf dem Server.  
  
2.  Klicken Sie in der Systemsteuerung auf **System und Sicherheit**, und klicken Sie dann auf **Windows-Firewall**.  
  
3.  Klicken Sie in der Windows-Firewall auf **Windows-Firewall ein- oder ausschalten**, wählen die **Windows-Firewall aktivieren** aus, und klicken Sie dann auf **OK**.  
  
### <a name="the-internal-network-adapter-is-not-configured-to-register-ip-address-in-dns"></a>Der interne Netzwerkadapter ist nicht so konfiguriert, dass die IP-Adresse in DNS registriert werden.  
 **Problem:** der interne Netzwerkadapter ist nicht so konfiguriert, dass die IP-Adresse in DNS registriert werden.  
  
 **Auswirkung:**, wenn die IP-Adresse des internen Netzwerkadapters nicht in DNS registriert ist, möglicherweise nicht möglich, den Zugriff auf den Server mit den Computernamen des Servers.  
  
 **Lösung:** überprüfen, ob der interne Netzwerkadapter so konfiguriert ist, dass in DNS registriert werden.  
  
### <a name="dns-the-values-for-the-dns-forwardingtimeout-and-recursiontimeout-registry-key-are-identical"></a>DNS: Die Werte für den Registrierungsschlüssel DNS-Registrierungsschlüssel "ForwardingTimeout" und "RecursionTimeout" sind identisch  
 **Problem:** der Wert des Registrierungsschlüssels DNS-Registrierungsschlüssel "ForwardingTimeout" sollten nicht den Wert des Registrierungsschlüssels "RecursionTimeout" muss identisch sein.  
  
 **Auswirkung:** Sie möglicherweise nicht den Namen Internetressourcen zugreifen.  
  
 **Lösung:** legen Sie den Wert des Registrierungsschlüssels "RecursionTimeout" muss größer sein als der Wert des Schlüssels "ForwardingTimeout" muss, befindet sich in der Registrierung unter "hkey_local_machine\System\currentcontrolset\services\dns\Parameters" sein.  
  
### <a name="the-forward-dns-zone-for-your-active-directory-domain-does-not-allow-secure-updates"></a>Die forward DNS-Zone für die Active Directory-Domäne ist nicht sichere Updates zulässig.  
 **Problem:** sollten Sie die Forward-Lookupzone nur sichere dynamische Updates zulassen konfigurieren.  
  
 **Auswirkung:** Wenn Sie sichere dynamische Updates aktivieren Sie nur autorisierte Benutzer und Hosts können Änderungen vornehmen, um die Datensätze.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-forward-lookup-zone-for-your-active-directory-domain"></a>So konfigurieren Sie die Forward-Lookupzone für Ihre Active Directory-Domäne  
  
1.  Öffnen Sie dnsmgmt.msc auf dem Server.  
  
2.  Maustaste auf die Forward-Lookupzone für Ihre Active Directory-Domäne, und klicken Sie dann auf **Eigenschaften**.  
  
3.  In der **dynamische Updates** Dropdownliste **nur sichere**, und klicken Sie dann auf **OK**.  
  
### <a name="the-forward-dns-zone-does-not-allow-secure-updates"></a>Die Forward-DNS-Zone keine sicheren lässt Updates  
 **Problem:** sollten Sie die Forward-Lookupzone für die Zone "_msdcs" nur sichere dynamische Updates zulassen konfigurieren.  
  
 **Auswirkung:** Wenn Sie sichere dynamische Updates aktivieren Sie nur autorisierte Benutzer und Hosts können Änderungen an Datensätzen in der _msdcs-Zone vornehmen.  
  
 **Lösung:**  
  
##### <a name="to-allow-secure-updates-in-the-msdcs-zone"></a>So ermöglichen Sie sichere Updates in der Zone "_msdcs"  
  
1.  Öffnen Sie dnsmgmt.msc auf dem Server.  
  
2.  Maustaste auf die Forward-Lookupzone für die Zone "_msdcs", und klicken Sie dann auf **Eigenschaften**.  
  
3.  In der **dynamische Updates** Dropdownliste **nur sichere**, und klicken Sie dann auf **OK**.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Verstärkte Sicherheitskonfiguration für Internet Explorer ist nicht aktiviert.  
 **Problem:** Internet Explorer Enhanced Security Configuration (IE ESC) ist momentan für die Gruppe "Administratoren" nicht aktiviert.  
  
 **Auswirkung:** Wenn die verstärkte Sicherheitskonfiguration für Internet Explorer für die Gruppe "Administratoren" nicht aktiviert ist, Ihr Server und Internet Explorer haben erhöhte Risiko böswilliger Angriffe, die über Web-Inhalte auftreten können und Anwendungsskripts.  
  
 **Lösung:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>So aktivieren Sie die verstärkte Sicherheitskonfiguration für Internet Explorer  
  
1.  Öffnen **Server-Manager** auf dem Server, und klicken Sie dann auf **lokalen Server**.  
  
2.  Auf der **Eigenschaften** Bereich, ändern Sie die Einstellung für **verstärkte Sicherheitskonfiguration für IE** auf **auf**, und klicken Sie dann auf **OK**.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Verstärkte Sicherheitskonfiguration für Internet Explorer ist nicht aktiviert.  
 **Problem:** Internet Explorer Enhanced Security Configuration (IE ESC) ist momentan nicht für die Gruppe "Benutzer" aktiviert.  
  
 **Auswirkung:** Wenn die verstärkte Sicherheitskonfiguration für Internet Explorer für die Gruppe "Benutzer" nicht aktiviert ist, Ihr Server und Internet Explorer haben erhöhte Risiko böswilliger Angriffe, die über Web-Inhalte auftreten können und Anwendungsskripts.  
  
 **Lösung:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>So aktivieren Sie die verstärkte Sicherheitskonfiguration für Internet Explorer  
  
1.  Öffnen **Server-Manager**, und klicken Sie dann auf **lokalen Server**.  
  
2.  Auf der **Eigenschaften** Bereich, ändern Sie die Einstellung für **verstärkte Sicherheitskonfiguration für IE** auf **auf**, und klicken Sie dann auf **OK**.  
  
### <a name="the-source-server-remains-in-active-directory-sites-and-services"></a>Der Quellserver verbleibt in Active Directory-Standorte und -Dienste  
 **Problem:** der Quellserver, auf dem Windows Small Business Server ausgeführt wird, die noch in Active Directory-Standorte und -Dienste vorhanden ist in den Default-First-Site-Name.  
  
 **Auswirkung:**, wenn der Quellserver in Active Directory-Standorte und -Dienste verbleibt, können Clientcomputer Konnektivität Problem auftreten: s.  
  
 **Lösung:** sollten Sie den Quellserver tiefer stufen, aus der Domäne entfernen und löschen Sie dann den Quellserver aus Active Directory-Standorte und Dienste und Active Directory-Benutzer und Computer.  
  
### <a name="source-server-remains-in-sbscomputer-ou"></a>Quellserver verbleibt in SBSComputer OU  
 **Problem:** der Quellserver, auf dem Windows Small Business Server ausgeführt wird, die noch in Active Directory-Benutzer und -Computer vorhanden ist.  
  
 **Auswirkung:**, wenn der Quellserver in Active Directory-Benutzer und -Computer verbleibt, können Clientcomputer Konnektivität Problem auftreten: s.  
  
 **Lösung:** sollten Sie den Quellserver tiefer stufen, aus der Domäne entfernen und löschen Sie dann den Quellserver aus Active Directory-Standorte und Dienste und Active Directory-Benutzer und Computer.  
  
### <a name="a-group-policy-is-missing"></a>Eine Gruppenrichtlinie fehlt.  
 **Problem:** die Gruppenrichtlinie Standarddomänenrichtlinie ist nicht vorhanden.  
  
 **Auswirkung:** der Standarddomänenrichtlinie ist für ordnungsgemäße Domänenfunktionen erforderlich.  
  
 **Lösung:**  
  
##### <a name="to-restore-a-missing-group-policy"></a>So stellen Sie eine fehlende Gruppenrichtlinie wieder her  
  
1.  Öffnen Sie gpmc.msc auf dem Server.  
  
2.  Im Gruppenrichtlinien-Manager, erweitern Sie die Domänengesamtstruktur, und suchen Sie die Konsolenstruktur für die **Default Domain Policy** Gruppenrichtlinienobjekt.  
  
3.  Wenn die Richtlinie nicht in der Struktur angezeigt wird, stellen sie eine Sicherung des Systemstatus wieder her.  
  
### <a name="no-dns-name-server-resource-records"></a>Keine DNS-Namenserver-Ressourceneinträge  
 **Problem:** stehen keine DNS-Namenserver-Ressourceneinträge in der Forward-Lookupzone für Ihren Server.  
  
 **Auswirkung:** Wenn kein DNS-Namenserver-Ressourceneintrag in der Forward-Lookupzone für die Active Directory-Domäne vorhanden ist, Benutzer möglicherweise nicht auf Ressourcen im Netzwerk oder im Internet zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-restore-missing-dns-name-server-resource-records"></a>Zum Wiederherstellen fehlender DNS-Namenserver-Ressourceneinträge  
  
1.  Öffnen Sie dnsmgmt.msc auf dem Server.  
  
2.  Im DNS-Manager mit der rechten Maustaste die Forward-Lookupzone für die Active Directory-Domäne, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **Namenserver** Registerkarte, stellen Sie sicher, dass die Einstellungen richtig sind.  
  
4.  Stellen Sie alle notwendigen Änderungen vor, und klicken Sie dann auf **OK** zum Speichern der Einstellungen.  
  
### <a name="no-dns-name-server-records"></a>Keine DNS-Namenserver-Einträge  
 **Problem:** es sind keine DNS-Namenserver-Ressourceneintrag (NS) Ressourceneinträge in der _msdcs-Zone für den Server (z.B.: "_msdcs.contoso.Local").  
  
 **Auswirkung:** Wenn kein DNS-Namenserver-Ressourceneintrag in der Zone "_msdcs" für die Active Directory-Domäne vorhanden ist, Benutzer möglicherweise nicht den Zugriff auf Ressourcen im Netzwerk oder im Internet.  
  
 **Lösung:**  
  
##### <a name="to-restore-missing-dns-name-server-records"></a>So stellen Sie fehlende DNS-Namenserver-Einträge wieder her  
  
1.  Öffnen Sie dnsmgmt.msc auf dem Server.  
  
2.  Im DNS-Manager mit der rechten Maustaste die Forward-Lookupzone für die Zone "_msdcs", und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **Namenserver** Registerkarte, stellen Sie sicher, dass die Einstellungen richtig sind.  
  
4.  Stellen Sie alle notwendigen Änderungen vor, und klicken Sie dann auf **OK** zum Speichern der Einstellungen.  
  
### <a name="no-dns-name-server-records"></a>Keine DNS-Namenserver-Einträge  
 **Problem:** es sind keine DNS-Namenserver-Ressourceneintrag (NS) Ressourceneinträge für die "delegated _msdcs"-Lookupzone weiterleiten.  
  
 **Auswirkung:** Wenn kein DNS-Namenserver-Ressourceneintrag vorhanden ist, für die "delegated _msdcs"-Lookupzone weiterleiten, wird der DNS-Serverdienst die DNS-Ressourceneinträge für die Domäne kann nicht aufgelöst werden und kann nicht gestartet.  
  
 **Lösung:**  
  
##### <a name="to-reconfigure-missing-dns-name-server-records"></a>So konfigurieren Sie fehlende DNS-Namenserver-Einträge neu  
  
1.  Öffnen Sie dnsmgmt.msc auf dem Server.  
  
2.  Im DNS-Manager, erweitern Sie den Servernamen, und klicken Sie dann **Forward-Lookupzonen**.  
  
3.  Klicken Sie auf die Forward-Lookupzone für Ihre Active Directory-Domäne (z.B.: "contoso.Local").  
  
4.  Die Zone "delegated _msdcs" wird als abgeblendeter Ordner angezeigt. Mit der rechten Maustaste in der _msdcs-Zone, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Auf der **Namenserver** Registerkarte, stellen Sie sicher, dass die Einstellungen richtig sind.  
  
6.  Stellen Sie alle notwendigen Änderungen vor, und klicken Sie dann auf **OK** zum Speichern der Einstellungen.  
  
### <a name="authenticated-users-not-a-member-of-the-pre-windows-2000-compatible-access-group"></a>Authentifizierte Benutzer kein Mitglied der Gruppe "Prä-Windows2000 kompatibler Zugriff"  
 **Problem:** die Gruppe Authentifizierte Benutzer ist kein Mitglied der Gruppe "Prä-Windows2000 kompatibler Zugriff".  
  
 **Auswirkung:** ist die integrierte Gruppe Authentifizierte Benutzer nicht Mitglied der Gruppe "Prä-Windows2000 kompatibler Zugriff", können Benutzer im Netzwerk "Zugriff verweigert"-Fehler auftreten.  
  
 **Lösung:**  
  
##### <a name="to-add-authenticated-users-to-the-pre-windows-2000-compatible-access-group"></a>Der Gruppe "Prä-Windows2000 kompatibler Zugriff" Authentifizierte Benutzer hinzu  
  
1.  Öffnen Sie dsa.msc auf dem Server.  
  
2.  In der **vordefiniert** Ordner mit der rechten Maustaste **Prä-Windows2000 kompatibler Zugriff**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **hinzufügen**, Typ **authentifizierte Benutzer**, und klicken Sie dann auf **OK** zwei Mal.  
  
### <a name="dns-client-not-configured"></a>DNS-Client nicht konfiguriert  
 **Problem:** der DNS-Client ist nicht so konfiguriert, dass nur auf die interne IP-Adresse des Servers verweist.  
  
 **Auswirkung:** DNS-Namensauflösung kann fehlschlagen, wenn der DNS-Client nur auf die interne IP-Adresse des Servers nicht konfiguriert ist.  
  
 **Lösung:**  
  
##### <a name="to-configure-dns-to-point-only-to-the-server-s-internal-ip-address"></a>Zum Konfigurieren von DNS nur auf dem Server s interne IP-Adresse  
  
1.  Öffnen Sie auf dem Clientcomputer die **Eigenschaften** Seite für die Netzwerkverbindung.  
  
2.  Stellen Sie sicher, dass DNS konfiguriert ist, dass nur auf die interne IP-Adresse des Servers verweist.  
  
### <a name="default-application-pool-value-changed"></a>Standard-Anwendungspool-Wert wurde geändert.  
 **Problem:** die Anzahl der maximale Anzahl von Arbeitsprozessen für den Anwendungspool "DefaultAppPool" ist nicht auf den Standardwert von 1 festgelegt.  
  
 **Auswirkung:** Benutzer möglicherweise nicht mit Windows Small Business Server webbasierten Diensten herstellen.  
  
 **Lösung:**  
  
##### <a name="to-reset-maximum-worker-processes-for-the-default-application-pool"></a>So setzen Sie die maximale Anzahl von Arbeitsprozessen für den Standardanwendungspool zurück  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Anwendungspools**.  
  
3.  In **Anwendungspools**, mit der rechten Maustaste **DefaultAppPool**, und klicken Sie dann auf **Erweiterte Einstellungen**.  
  
4.  In **Erweiterte Einstellungen**, ändern Sie den Wert für **maximale Anzahl von Arbeitsprozessen** auf 1 fest, und klicken Sie dann auf **OK**.  
  
5.  Schließen **Erweiterte Einstellungen**, mit der rechten Maustaste **DefaultAppPool**, beenden und anschließend den Anwendungspool neu starten.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-account"></a>Anwendungspool für Remotewebzugriff verwendet nicht das Standardkonto  
 **Problem:** der Anwendungspool "RemoteAppPool" wird nicht mit dem Standardkonto ausgeführt.  
  
 **Auswirkung:** Benutzer im Netzwerk möglicherweise nicht auf die Remotewebzugriff-Website zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-reset-the-remote-application-pool-to-use-the-default-account"></a>So setzen Sie den Remoteanwendungspool, um das Standardkonto zurück  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Anwendungspools**.  
  
3.  In **Anwendungspools**, mit der rechten Maustaste **RemoteAppPool**, und klicken Sie dann auf **Erweiterte Einstellungen**.  
  
4.  In **Erweiterte Einstellungen**, ändern Sie die **Identität** auf **"NetworkService"**, und klicken Sie dann auf **OK**.  
  
5.  Schließen **Erweiterte Einstellungen**, mit der rechten Maustaste **RemoteAppPool**, beenden und anschließend den Anwendungspool neu starten.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-net-framework-version"></a>Anwendungspool für Remotewebzugriff verwendet nicht die .NET Framework-Standardversion  
 **Problem:** der Anwendungspool "RemoteAppPool" wird nicht mit der Standardversion von Microsoft .NET Framework ausgeführt.  
  
 **Auswirkung:** Benutzer im Netzwerk möglicherweise nicht auf die Remotewebzugriff-Website zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-change-the-net-framework-version-used-by-the-remoteapppool"></a>So ändern Sie die von "RemoteAppPool" verwendete .NET Framework-Version  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Anwendungspools**.  
  
3.  In **Anwendungspools**, mit der rechten Maustaste **RemoteAppPool**, und klicken Sie dann auf **Erweiterte Einstellungen**.  
  
4.  In **Erweiterte Einstellungen**, ändern Sie die **.NET Framework-Version** v4. 0, und klicken Sie dann auf **OK**.  
  
5.  Schließen **Erweiterte Einstellungen**, mit der rechten Maustaste **RemoteAppPool**, beenden und anschließend den Anwendungspool neu starten.  
  
### <a name="the-remoteaccesslog-file-is-larger-than-1-gb-in-size"></a>Die RemoteAccess.log Datei ist größer als 1GB groß  
 **Problem:**, wenn die Größe der Datei Remoteaccess.log 1GB überschreitet, Sie können Fehler auftreten, wenig Speicherplatz auf dem Systemlaufwerk.  
  
 **Auswirkung:** Remoteaccess.log-Datei zu groß ist, kann dies Speicherplatz Problem: s auf Laufwerk C:.  
  
 **Lösung:** nach dem Sichern des Servers können, löschen Sie die Remoteaccess.log-Datei, die sich im Ordner "%ProgramData%\Microsoft\Windows Server\Logs\WebApps" befindet.  
  
### <a name="default-web-sites-log-directory-is-over-1-gb-in-size"></a>Protokollverzeichnis der Standardwebsite ist als 1GB  
 **Problem:**, wenn die Größe des Protokollordners der Standardwebsite 1GB überschreitet, Sie können Fehler auftreten, wenig Speicherplatz auf dem Systemlaufwerk.  
  
 **Auswirkung:** Protokollordner der Standardwebsite zu groß ist, kann dies Speicherplatz Problem: s auf Laufwerk C:  
  
 **Lösung:** nach dem Sichern des Servers, und während die Standardwebsite beendet wird, können Sie die Protokolldateien im Ordner "C:\inetpub\logs\LogFiles\W3SVC1" löschen. Starten Sie die Standardwebsite.  
  
### <a name="no-binding-for-ssl-on-all-ip-addresses"></a>Keine Bindung für SSL an alle IP-Adressen  
 **Problem:** es erfolgt keine Bindung für Secure Sockets Layer (SSL) für alle IP-Adressen auf dem Server.  
  
 **Auswirkung:** Wenn SSL nicht an alle IP-Adressen auf dem Server gebunden ist, einige Websites nicht für Benutzer verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-bind-ssl-to-all-ip-addresses-on-the-server"></a>So binden Sie SSL an alle IP-Adressen auf dem Server  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager auf den **Verbindungen** Bereich, erweitern Sie den Server, erweitern Sie **Sites**, mit der rechten Maustaste **Standardwebsite**, und klicken Sie dann auf **Bindungen bearbeiten**.  
  
3.  In **Sitebindungen**, klicken Sie auf **hinzufügen**, und wählen Sie dann die folgenden Einstellungen:  
  
    -   **Typ** = **Https**  
  
    -   **IP-Adresse** = **alle nicht zugewiesenen**  
  
    -   **Port** = 443  
  
4.  Wählen Sie ein SSL-Zertifikat, und klicken Sie dann auf **OK** um Ihre Änderungen zu speichern.  
  
### <a name="no-binding-for-ssl-on-the-default-web-site"></a>Keine Bindung für SSL auf der Standardwebsite  
 **Problem:** es erfolgt keine Bindung für SSL auf der Standardwebsite.  
  
 **Auswirkung:** Wenn SSL nicht an die Standardwebsite gebunden ist, einige Websites möglicherweise nicht für Benutzer verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-bind-ssl-to-the-default-website"></a>So binden Sie SSL an die Standardwebsite  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager auf den **Verbindungen** Bereich, erweitern Sie den Server, erweitern Sie **Sites**, mit der rechten Maustaste **Standardwebsite**, und klicken Sie dann auf **Bindungen bearbeiten**.  
  
3.  In **Sitebindungen**, klicken Sie auf **hinzufügen**, und wählen Sie dann die folgenden Optionen:  
  
    -   **Typ** = **Https**  
  
    -   **IP-Adresse** = **alle nicht zugewiesenen**  
  
    -   **Port** = 443  
  
    > [!NOTE]
    >  Wenn eine HTTPS-Bindung für Port 443 für eine bestimmte IP-Adresse vorhanden ist, ändern Sie die **IP-Adresse** -Attribut für diese Bindung in **alle nicht zugewiesenen**. Die einzige Ausnahme ist für die IP-Adresse 127.0.0.1. Ändern Sie die Bindung für 127.0.0.1 nicht.  
  
4.  Wählen Sie ein SSL-Zertifikat, und klicken Sie dann auf **OK** um Ihre Änderungen zu speichern.  
  
### <a name="a-certificate-expires-within-30-days"></a>Ein Zertifikat läuft innerhalb von 30Tagen ab.  
 **Problem:** Ihr Serverzertifikat läuft innerhalb von 30Tagen.  
  
 **Auswirkung:** der Server kann kein abgelaufenes Zertifikat verwenden. Wenn das Zertifikat abläuft, können Benutzer nicht "Zugriff überall"-Funktionen verwenden können.  
  
 **Lösung:** soll das Zertifikat abläuft, erneuern Sie das Zertifikat mit der vertrauenswürdigen Zertifizierungsstelle.  
  
### <a name="certificate-subject-does-not-match-the-name-configured-by-domain-name-wizard"></a>Antragsteller des Zertifikats entspricht nicht dem Namen, der vom Domänennamen-Assistenten konfiguriert  
 **Problem:** der Antragsteller des Zertifikats entspricht nicht den Namen, der vom Domänennamen-Assistenten konfiguriert wurde.  
  
 **Auswirkung:**, wenn der Antragsteller des Zertifikats nicht dem Namen entsprechen, der vom Domänennamen-Assistenten konfiguriert wurde, haben einige Websites nicht initialisiert werden. Andere Websites zeigen den Fehler "Es besteht ein Problem mit dem Sicherheitszertifikat dieser Website."  
  
 **Lösung:** zum Beheben dieses Problems:, führen Sie erneut die überall den Assistenten zum Einrichten und den richtigen Domänennamen für das Zertifikat bereitstellen, oder erwerben Sie ein neues Zertifikat an, die Namen der Domäne entspricht, die Sie verwenden möchten.  
  
### <a name="one-or-more-user-accounts-have-duplicate-cn-names"></a>Ein oder mehrere Benutzerkonten weist einen doppelten CN-Namen  
 **Problem:** ein oder mehrere Benutzerkonten weist einen doppelten CN-Namen: {0}.  
  
 **Auswirkung:** Wenn Benutzerkonten doppelte CN-Namen haben, Benutzer möglicherweise nicht mit dem Netzwerk anmelden. Darüber hinaus können Suchvorgänge von Active Directory für Benutzer falschen Werten führen.  
  
 **Lösung:** zum Beheben dieses Problems:, stellen Sie sicher, dass Netzwerkbenutzerkonten keine doppelten "CN =" Namen. Um dies zu vereinfachen, sollten Sie in der Active Directory-Inhalte in einer Datei zur Überprüfung exportieren. Informationen hierzu finden Sie unter [Verwenden von LDIFDE zum Importieren und Exportieren von Verzeichnisobjekten in Active Directory (Knowledge Base-Artikel 237677)](https://support.microsoft.com/kb/237677) (https://support.microsoft.com/kb/237677).  
  
### <a name="nt-backup-is-installed"></a>NT Backup ist installiert.  
 **Problem:** das Windows NT Backup-Programm auf dem Server installiert ist.  
  
 **Auswirkung:** Windows Server Essentials wird Windows Server-Sicherung verwendet. Wenn Windows NT Backup-Programm ebenfalls installiert ist, können Konflikte zwischen den beiden Sicherungsprogramme vorhanden sind. Dadurch kann Windows Server-Sicherung beim Prozess Fehler auf. Die Konflikte auch verhindert möglicherweise mithilfe einer Sicherung zum Wiederherstellen des Servers.  
  
 **Lösung:** zum Beheben dieses Problems:, das NT Backup-Programm auf dem Server deinstalliert.  
  
### <a name="iis-does-not-own-port-80-000080-or-port-443-0000443"></a>IIS über keinen Port 80 (0.0.0.0:80) oder Port 443 (0.0.0.0: 443) verfügt.  
 **Problem:** Port 80 (0.0.0.0:80) oder Port 443 (Internet Information Services, IIS) nicht besitzt. Diese Ports sind derzeit an andere Anwendungen gebunden.  
  
 **Auswirkung:** Web-Apps für Windows Server Essentials erfordert die Verwendung von Port 80 und Port 443, um die Dienste verfügbar zu machen. Wenn Sie einen anderen Prozess oder diese Anwendung bereits Port 80 oder Port 443 verwendet wird, können nicht der Windows Server Essentials-Web-Apps ausgeführt. In diesem Fall sind Remotewebzugriff und andere Anwendungen nicht für Benutzer verfügbar.  
  
 **Lösung:** zum Beheben dieses Problems:, deinstallieren Sie die Anwendung, die bereits mithilfe von Port 80 oder Port 443 ist, oder diese Anwendung in einen anderen Port zuweisen.  
  
### <a name="the-default-website-is-not-running"></a>Die Standardwebsite wird nicht ausgeführt.  
 **Problem:** die Standardwebsite nicht in der Windows Server Essentials-Umgebung ausgeführt wird.  
  
 **Auswirkung:** Windows Server Essentials-Web-Apps die Verwendung der Standardwebsite erfordern. Wenn die Standardwebsite nicht ausgeführt wird, sind Remotewebzugriff und andere Anwendungen nicht für Benutzer verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-start-the-default-website"></a>Starten Sie die Standardwebsite  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Sites**.  
  
3.  Mit der rechten Maustaste **Standardwebsite**, zeigen Sie auf **Website verwalten**, und klicken Sie dann auf **starten**.  
  
### <a name="read-and-script-permissions-for-the-remote-virtual-directory-are-incorrect"></a>Lese- und Berechtigungen für das virtuelle Verzeichnis /Remote sind falsch  
 **Problem:** Lese- und nicht auf das virtuelle Verzeichnis /Remote zugewiesen werden.  
  
 **Auswirkung:** Wenn die Berechtigungen Lesen und Skripts für das virtuelle Verzeichnis /Remote fehlerhaft sind, können keine Benutzer Remote Web Access verwenden. Wenn sie versuchen, den Remotewebzugriff zu verwenden, um im Internet zu surfen, können sie den Fehler "HTTP-Fehler 403.1 verboten." auftreten.  
  
 **Lösung:**  
  
##### <a name="to-assign-read-and-script-permissions-to-the-remote-directory"></a>Zuweisen von Berechtigungen zum Lesen und Skripts in das Verzeichnis /Remote  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Sites**.  
  
3.  Erweitern Sie **Standardwebsite**, und erweitern Sie dann **Remote**.  
  
4.  In **Ansicht "Features"**, doppelklicken Sie auf **Handlerzuordnungen**.  
  
5.  Auf der **Aktionen** Bereich, klicken Sie auf **Featureberechtigungen bearbeiten**.  
  
6.  Wählen Sie die **lesen** und **Skript** Kontrollkästchen, und klicken Sie dann auf **OK**.  
  
### <a name="http-redirect-is-either-set-or-inherited-on-the-remote-virtual-directory"></a>HTTP-Umleitung festgelegt oder geerbt für das virtuelle Verzeichnis /Remote  
 **Problem:** Attributs HTTP-Umleitung unerwartet festgelegt oder geerbt für das virtuelle Verzeichnis /Remote.  
  
 **Auswirkung:** Wenn das HTTP-Umleitung-Attribut für das virtuelle Verzeichnis /Remote festgelegt ist, Remote-Webarbeitsplatz nicht ordnungsgemäß funktioniert.  
  
 **Lösung:**  
  
##### <a name="to-remove-the-http-redirect-attribute"></a>So entfernen Sie das Attribut HTTP-Umleitung  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Sites**.  
  
3.  Erweitern Sie **Standardwebsite**, und erweitern Sie dann **Remote**.  
  
4.  In **Ansicht "Features"**, doppelklicken Sie auf **HTTP-Umleitung**.  
  
5.  Deaktivieren der **Anfragen zu diesem Ziel umleiten**, und klicken Sie dann auf **übernehmen** auf die **Aktionen** Bereich.  
  
### <a name="a-host-name-exists-for-port-80-on-the-default-website"></a>Ein Hostname für Port 80 auf der Standardwebsite vorhanden ist  
 **Problem:** ein Hostname für Port 80 auf der Standardwebsite zugewiesen ist.  
  
 **Auswirkung:** Wenn ein Hostname für Port 80 auf der Standardwebsite zugewiesen ist, Sie möglicherweise nicht zur Verbindung mit einigen Windows Server Essentials-Web-Apps. Ein Hostname ist nicht erforderlich und sollte nicht in dieser situation  
  
 **Lösung:**  
  
##### <a name="to-clear-the-host-name-entry-for-port-80-on-the-default-website"></a>So löschen Sie die Hostnameneintrag für Port 80 auf der Standardwebsite  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Sites**.  
  
3.  In **Ansicht "Features"**, mit der rechten Maustaste **Standardwebsite**, und klicken Sie dann auf **Bindungen**.  
  
4.  In **Sitebindungen**, wählen die **http für Port 80** festlegen, und klicken Sie dann auf **bearbeiten**.  
  
5.  In **Sitebindung bearbeiten**Kontrollkästchen die **Hostnamen** Eintrag, und klicken Sie dann auf **OK**.  
  
### <a name="backup-does-not-succeed-because-of-a-hidden-partition"></a>Sicherung ist aufgrund einer verborgenen Partition nicht erfolgreich.  
 **Problem:** eine Nicht-NTFS-Partition für die Sicherung von Windows Server-Sicherung geplant ist.  
  
 **Auswirkung:** Windows Server-Sicherung können nur eine Sicherungskopie von Partitionen, die als NTFS formatiert sind.  
  
 **Lösung:** Windows Server-Sicherung zum Sichern von Nicht-NTFS-Partitionen nicht konfigurieren. Weitere Informationen finden Sie unter [Ereignis-IDs 12290 und 16387 werden protokolliert, wenn keine Sicherung des Systemstatus auf einem Windows Server2008-basierten Computer (Knowledge Base-Artikel 968128)](https://support.microsoft.com/kb/968128) (https://support.microsoft.com/kb/968128).  
  
### <a name="the-most-recent-backup-did-not-succeed"></a>Die aktuelle Sicherung war nicht erfolgreich.  
 **Problem:** die aktuelle versuchte Sicherung wurde nicht erfolgreich abgeschlossen.  
  
 **Auswirkung:** der Sicherungsstatus für das System ist nicht korrekt.  
  
 **Lösung:** überprüfen Sie die Ereignisprotokolle und Sicherungsprotokolle auf Fehler, die während der letzten Sicherung aufgetreten ist.  
  
### <a name="the-startup-type-for-the-file-replication-service-is-not-set-to-automatic"></a>Der Starttyp für den Dateireplikationsdienst ist nicht automatisch festgelegt.  
 **Problem:** (File Replication Service, FRS) möglicherweise nicht gestartet, wenn der Starttyp nicht auf den Standardwert automatisch festgelegt wird.  
  
 **Auswirkung:**, wenn der Dateireplikationsdienst nicht ausgeführt wird, der Domänencontroller möglicherweise seine Dienste anzukündigen. Dies kann zu weiteren Problemen wie z.B. Anmeldefehlern und Gruppenrichtlinienfehlern führen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-file-replication-service-for-automatic-startup"></a>So konfigurieren Sie den Dateireplikationsdienst für den automatischen Start  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Dateireplikation**.  
  
3.  Für **Starttyp**Option **automatische**, und klicken Sie dann auf **übernehmen**.  
  
### <a name="the-file-replication-service-is-not-running"></a>Der Dateireplikationsdienst wird nicht ausgeführt.  
 **Problem:** der Dateireplikationsdienst wird nicht ausgeführt.  
  
 **Auswirkung:**, wenn der Dateireplikationsdienst nicht ausgeführt wird, der Domänencontroller möglicherweise seine Dienste anzukündigen. Dieses Verhalten kann zu weiteren Problemen wie z.B. Anmeldefehlern und Gruppenrichtlinienfehlern führen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-file-replication-service"></a>Der Dateireplikationsdienst starten  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Dateireplikationsdienst**.  
  
3.  Klicken Sie auf **starten**.  
  
### <a name="the-logon-account-for-the-file-replication-service-is-not-set-to-use-the-local-system-account"></a>Das Anmeldekonto für den Dateireplikationsdienst ist nicht festgelegt, das lokale Systemkonto verwenden.  
 **Problem:** der Dateireplikationsdienst ist nicht Verwendung des lokalen Systemkontos als Standardanmeldekonto konfiguriert.  
  
 **Auswirkung:**, wenn der Dateireplikationsdienst nicht lokalen System als Standardanmeldekonto verwendet, können Sie Fehler in Bezug auf Berechtigungen auftreten. Diese Fehler können andere Fehler auslösen, und Sie können dazu führen, dass den Domänencontroller kündigt seine Dienste nicht mehr.  
  
 **Lösung:**  
  
##### <a name="to-configure-local-system-as-the-default-logon-account-for-file-replication"></a>So konfigurieren Sie Lokales System als das Standardanmeldekonto für die Dateireplikation  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Dateireplikation**.  
  
3.  Auf der **Diensteigenschaften** auf die **anmelden** Registerkarte.  
  
4.  Wählen Sie die **lokales Systemkonto** aus, und klicken Sie dann auf **übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-startup-type-for-the-dfs-replication-service-is-not-set-to-automatic"></a>Der Starttyp für den DFS-Replikationsdienst wird nicht automatisch festgelegt.  
 **Problem:** der DFS-Replikationsdienst möglicherweise nicht gestartet, wenn der Starttyp nicht auf den Standardwert automatisch festgelegt wird.  
  
 **Auswirkung:**, wenn der DFS-Replikationsdienst nicht ausgeführt wird, der Domänencontroller möglicherweise seine Dienste anzukündigen. Dies kann zu weiteren Problemen wie z.B. Anmeldefehlern und Gruppenrichtlinienfehlern führen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dfs-replication-service-for-automatic-startup"></a>So konfigurieren Sie den DFS-Replikationsdienst für den automatischen Start  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **DFS-Replikation**.  
  
3.  Für **Starttyp**Option **automatische**, und klicken Sie dann auf **übernehmen**.  
  
### <a name="the-dfs-replication-service-is-not-running"></a>Der DFS-Replikationsdienst wird nicht ausgeführt.  
 **Problem:** der DFS-Replikationsdienst wird aktuell nicht ausgeführt.  
  
 **Auswirkung:**, wenn der DFS-Replikationsdienst nicht ausgeführt wird, der Domänencontroller möglicherweise seine Dienste anzukündigen. Dieses Verhalten kann zu weiteren Problemen wie z.B. Anmeldefehlern und Gruppenrichtlinienfehlern führen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dfs-replication-service"></a>Den DFS-Replikationsdienst starten  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **DFS-Replikation**.  
  
3.  Klicken Sie auf **starten**.  
  
### <a name="the-dfs-replication-service-is-not-is-not-set-to-use-the-local-system-account"></a>Der DFS-Replikation ist der Dienst ist nicht festgelegt, das lokale Systemkonto verwenden  
 **Problem:** der DFS-Replikationsdienst ist nicht auf das Verwenden des lokalen Systemkontos als Standardanmeldekonto festgelegt.  
  
 **Auswirkung:**, wenn der DFS-Replikationsdienst nicht lokalen System als Standardanmeldekonto verwendet, können Sie Fehler in Bezug auf Berechtigungen auftreten. Diese Fehler können andere Fehler auslösen, und Sie können dazu führen, dass den Domänencontroller kündigt seine Dienste nicht mehr.  
  
 **Lösung:**  
  
##### <a name="to-configure-dfs-replication-to-use-local-system-as-the-default-logon-account"></a>Zum Konfigurieren der DFS-Replikation zum lokalen System als Standardanmeldekonto verwendet  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **DFS-Replikation**.  
  
3.  Auf der **Diensteigenschaften** auf die **anmelden** Registerkarte.  
  
4.  Wählen Sie die **lokales Systemkonto** aus, und klicken Sie dann auf **übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-set-to-use-the-local-system-account"></a>Windows Server Office365-Integrationsdienst ist nicht festgelegt, das lokale Systemkonto verwenden.  
 **Problem:** der Windows Server Office365-Integrationsdienst ist nicht auf das Verwenden des lokalen Systemkontos als Standardanmeldekonto festgelegt.  
  
 **Auswirkung:** Wenn Windows Server Office365-Integrationsdienst nicht lokalen System als Standardanmeldekonto verwendet, einige Features von Office365 möglicherweise nicht ordnungsgemäß. Sie können auch Fehler in Bezug auf Berechtigungen auftreten.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-office-365-integration-service-to-use-local-system-as-the-default-logon-account"></a>So konfigurieren Sie die Office365-Integrationsdienst zum lokalen System als Standardanmeldekonto verwendet  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Windows Server Office365-Integrationsdienst**.  
  
3.  Auf der **Diensteigenschaften** auf die **anmelden** Registerkarte.  
  
4.  Wählen Sie die **lokales Systemkonto** aus, und klicken Sie dann auf **übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-running"></a>Windows Server Office365-Integrationsdienst wird nicht ausgeführt.  
 **Problem:** der Windows Server Office365-Integrationsdienst wird aktuell nicht ausgeführt.  
  
 **Auswirkung:**, wenn der Windows Server Office365-Integrationsdienst nicht ausgeführt wird, sind die cloudbasierten Features von Office365 nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-start-the-windows-server-office-365-integration-service"></a>Zum Starten der Windows Server Office365-Integrationsdienst  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Windows Server Office365-Integrationsdienst**.  
  
3.  Klicken Sie auf **starten**.  
  
### <a name="the-startup-type-for-the-windows-server-office-365-integration-service-is-not-set-to-automatic"></a>Der Starttyp für den Windows Server Office365-Integrationsdienst ist nicht automatisch festgelegt.  
 **Problem:** der Windows Server Office365-Integrationsdienst wird möglicherweise nicht gestartet, wenn der Starttyp nicht auf den Standardwert automatisch festgelegt ist.  
  
 **Auswirkung:**, wenn der Windows Server Office365-Integrationsdienst nicht ausgeführt wird, sind die cloudbasierten Features von Office365 nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-office-365-integration-service-for-automatic-startup"></a>So konfigurieren Sie die Office365-Integrationsdienst für den automatischen Start  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Windows Server Office365-Integrationsdienst**.  
  
3.  Für **Starttyp**Option **automatische**, und klicken Sie dann auf **übernehmen**.  
  
### <a name="a-registry-value-is-missing-or-set-incorrectly"></a>Ein Registrierungswert ist nicht vorhanden oder wurde nicht ordnungsgemäß festgelegt  
 **Problem:** ein Registrierungswert unter HKEY_LOCAL_MACHINE \Software\Microsoft\Rpc\RpcProxy falsche Werte enthält oder nicht vorhanden ist.  
  
 **Auswirkung:** Wenn der RPCProxy-Registrierungsschlüssel falsch festgelegt ist, möglicherweise eine Fehlermeldung angezeigt, die der folgenden ähnelt: "kann nicht verbinden Sie Ihren Computer an den Remotecomputer, da der Remotedesktop-Gatewayserver vorübergehend nicht verfügbar ist. Versuchen Sie es später, oder wenden Sie sich an den Netzwerkadministrator, um Unterstützung zu erhalten."  
  
 **Lösung:**  
  
##### <a name="to-correct-the-registry-setting"></a>So korrigieren Sie die Einstellung in der Registrierung  
  
1.  Registrierungs-Editor zu öffnen.  
  
2.  Navigieren Sie zu dem folgenden Registrierungsschlüssel:  
  
     HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy  
  
3.  Stellen Sie sicher, dass die Zeichenfolge mit dem Namen "Website" Datenwert Standardwebsite verfügt:  
  
    -   Wenn der Wert falsch ist, ändern Sie die Zeichenfolge, um den richtigen Wert zu verwenden.  
  
    -   Wenn die Zeichenfolge nicht vorhanden ist, erstellen Sie eine neue Zeichenfolge mit dem Namen "Website", und legen Sie den Wert auf der Standardwebsite."  
  
### <a name="the-startup-type-for-the-block-level-backup-engine-service-is-not-set-to-manual"></a>Der Starttyp für den Block-Sicherungsmoduldienst ist nicht auf manuell gesetzt.  
 **Problem:** der Block-Sicherungsmoduldienst ist nicht der Standardstarttyp des Handbuchs verwenden.  
  
 **Auswirkung:** der Block-Sicherungsmodul möglicherweise nicht gestartet, wenn der Starttyp nicht auf manuell festgelegt ist. Dieses Problem: kann dazu führen, dass Aufträge von Windows Server-Sicherung fehlschlagen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-for-manual-startup"></a>So konfigurieren Sie die Block-Sicherungsmoduldienst für manuellen Start  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Block-Sicherungsmodul**.  
  
3.  Für **Starttyp**Option **manuell**, und klicken Sie dann auf **übernehmen**.  
  
### <a name="the-logon-account-for-the-block-level-backup-engine-service-is-not-set-to-use-the-local-system-account"></a>Das Anmeldekonto für den Block-Sicherungsmoduldienst ist nicht festgelegt, das lokale Systemkonto verwenden.  
 **Problem:** der Block-Sicherungsmoduldienst ist nicht auf Verwenden des lokalen Systemkontos als Standardanmeldekonto festgelegt.  
  
 **Auswirkung:** Wenn Block-Sicherungsmodul Lokales System nicht als Standardanmeldekonto verwendet, können Sie Fehler in Bezug auf Berechtigungen auftreten. Diese Fehler können verhindern, dass Aufträge von Windows Server-Sicherung nicht erfolgreich abgeschlossen werden.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-to-use-local-system-as-the-default-logon-account"></a>So konfigurieren Sie die Block-Sicherungsmodul zum lokalen System als Standardanmeldekonto verwendet  
  
1.  Öffnen Sie Dienste.  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Block-Sicherungsmodul**.  
  
3.  Auf der **Diensteigenschaften** auf die **anmelden** Registerkarte.  
  
4.  Wählen Sie die **lokales Systemkonto** aus, und klicken Sie dann auf **übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-common-name-on-the-certificate-that-is-bound-to-the-wss-certificate-web-service-website-does-not-match-the-server-name"></a>Der allgemeine Name für das Zertifikat, das an die Website des Webdiensts für WSS-Zertifikate gebunden ist, entspricht nicht den Namen des Servers  
 **Problem:** ein ungültiges Zertifikat an den Webdienst für WSS-Zertifikate Website in IIS gebunden ist. Der allgemeine Name für dieses Zertifikat stimmt nicht mit den Servernamen überein.  
  
 **Auswirkung:** Wenn Sie ein ungültiges Zertifikat an die Website des Webdiensts für WSS-Zertifikate binden, der Verbindungs-Assistent möglicherweise nicht ordnungsgemäß ausgeführt.  
  
 **Lösung:**  
  
##### <a name="to-configure-a-valid-certificate-for-the-wss-certificate-web-service"></a>So konfigurieren Sie ein gültiges Zertifikat für den Webdienst für WSS-Zertifikat  
  
1.  Öffnen Sie Internet Information Services (IIS) Manager auf dem Server.  
  
2.  Im IIS-Manager, erweitern Sie den Server, und klicken Sie dann auf **Sites**.  
  
3.  Mit der rechten Maustaste **Webdienst für WSS-Zertifikate**, und klicken Sie dann auf **Bindungen bearbeiten**.  
  
4.  In **Sitebindungen**, klicken Sie auf **HTTPS**, und klicken Sie dann auf **bearbeiten**.  
  
5.  In **Sitebindung bearbeiten**, für **SSL-Zertifikat**, wählen Sie das Zertifikat, das den gleichen Namen wie der Server hat.  
  
6.  Wenn mehr als ein Zertifikateintrag den gleichen Namen wie der Server hat, klicken Sie auf **Ansicht** zu bestimmen, welches Zertifikat gültig ist, und wählen Sie dann das entsprechende Zertifikat.  
  
### <a name="there-appears-to-be-a-problem-with-the-certificate-binding-for-the-remote-desktop-gateway-service"></a>Es scheint ein Problem mit der zertifikatbindung für den Remotedesktopgateway-Dienst  
 **Problem:** des Zertifikats für den Remotedesktopgateway-Dienst scheint nicht ordnungsgemäß gebunden werden.  
  
 **Auswirkung:**, wenn das Zertifikat für den Remotedesktopgateway-Dienst nicht ordnungsgemäß konfiguriert ist, keine Benutzer Remotewebzugriff herstellen.  
  
 **Lösung:**  
  
##### <a name="to-fix-the-binding-for-the-remote-desktop-gateway-service"></a>Um die Bindung für den Remotedesktopgateway-Dienst zu beheben.  
  
-   Öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie die folgenden Befehle:  
  
    ```  
    REG ADD HKLM\SYSTEM\CurrentControlSet\services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443  /v DefaultFlags /t REG_DWORD /d 1 /f  
    net stop tsgateway  
    net start tsgateway  
    ```  
  
     Weitere Informationen finden Sie unter [zum Verwalten der Remotedesktopgateway-Diensts in Windows Server Essentials (Knowledge Base-Artikel 2472211)](https://support.microsoft.com/kb/2472211) (https://support.microsoft.com/kb/2472211).
