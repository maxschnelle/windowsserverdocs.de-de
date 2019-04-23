---
title: Von Windows Server Essentials Best Practices Analyzer (BPA) verwendete Regeln
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850691"
---
# <a name="rules-used-by-the-windows-server-essentials-best-practices-analyzer-bpa-tool"></a>Von Windows Server Essentials Best Practices Analyzer (BPA) verwendete Regeln

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieser Artikel beschreibt die Wartung von der Windows Server Essentials Best Practices Analyzer (BPA) verwendeten Regeln. Der BPA überprüft einen Server, der Windows Server Essentials ausgeführt wird, und zeigt einen Bericht, der problembeschreibungen und Empfehlungen zur Fehlerbehebung. Die Empfehlungen werden von der Product Supportorganisation für Windows Server Essentials entwickelt.  
  
## <a name="using-the-tool"></a>Verwenden des Tools  
 Es ist eine standardmäßige Vorgehensweise, bei der Migration zu Windows Server Essentials in Windows Server 2011 Essentials, Windows Small Business Server 2011 Essentials oder Windows Home Server 2011 zum Ausführen von Best Practices Analyzer auf dem Zielserver nach Abschluss der Migration Ihrer Einstellungen und Daten. Sie können das Tool jederzeit über das Dashboard ausführen.  
  
#### <a name="to-run-the--windows-server-essentials-bpa-on-the-server"></a>Zum Ausführen von BPA für Windows Server Essentials auf dem server  
  
1.  Melden Sie sich als Administrator beim Server an, und öffnen Sie dann das Dashboard.  
  
2.  Klicken Sie im Dashboard auf die Registerkarte **Geräte**.  
  
3.  Klicken Sie im Bereich **Servertasks** auf **Best Practices Analyzer**.  
  
4.  Überprüfen Sie jede BPA-Meldung und befolgen Sie die Anweisungen, um ggf. Probleme zu lösen.  
  
## <a name="rules-used-by-the-best-practices-analyzer"></a>Von Best Practices Analyzer verwendete Regeln  
  
### <a name="disable-ip-filtering"></a>IP-Filterung deaktivieren  
 **Problem:** Die IP-Filterung ist aktuell auf dem Server aktiviert. Sie müssen die IP-Filterung deaktivieren.  
  
 **Auswirkung:** Wenn die IP-Filterung aktiviert ist, kann der Netzwerkverkehr blockiert werden.  
  
 **Lösung:**  
  
##### <a name="to-disable-ip-filtering"></a>So deaktivieren Sie die IP-Filterung  
  
1.  Öffnen Sie "regedit.exe" auf dem Server.  
  
2.  Navigieren Sie zu "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters".  
  
3.  Klicken Sie mit der rechten Maustaste auf **EnableSecurityFilters**, und klicken Sie dann auf **Ändern**.  
  
4.  Legen Sie im Fenster **DWORD-Wert (32-Bit) bearbeiten** das Feld **Wertdaten** auf 0 (null), und klicken Sie dann auf **OK**.  
  
5.  Starten Sie den Server neu, um die Änderungen zu übernehmen.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-set-to-start-automatically-by-default"></a>Der MSDTC-Dienst (Distributed Transaction Coordinator) sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:** Der MSDTC-Dienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** Der MSDTC-Dienst wird beim Start des Servers möglicherweise nicht automatisch gestartet. Wenn der Dienst beendet wird, können bestimmte SQL Server- oder COM-Funktionen fehlschlagen. Anwendungen, die Microsoft SQL Server- oder COM-Funktionen verwenden, funktionieren daher möglicherweise nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-msdtc-service-to-start-automatically"></a>So konfigurieren Sie den MSDTC-Diensts für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Distributed Transaction Coordinator**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch (Verzögerter Start)**, und klicken Sie dann auf **OK**.  
  
### <a name="the-netlogon-service-should-be-configured-to-start-automatically-by-default"></a>Der Anmeldedienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:** Der Anmeldedienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  Der Anmeldedienst wird beim Start des Servers möglicherweise nicht automatisch gestartet. Wenn der Dienst beendet wird, authentifiziert der Server Benutzer und Dienste möglicherweise nicht.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-netlogon-service-to-start-automatically"></a>So konfigurieren Sie den Anmeldedienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Netlogon**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-dns-client-service-should-be-configured-to-start-automatically-by-default"></a>Der DNS-Clientdienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:**  Der DNS-Clientdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  Der DNS-Clientdienst wird beim Start des Servers möglicherweise nicht automatisch gestartet. Wenn dieser Dienst beendet wurde, kann der Server DNS-Namen möglicherweise nicht auflösen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dns-client-service-to-start-automatically"></a>So konfigurieren Sie den DNS-Clientdienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DNS-Client**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-dns-server-service-should-be-configured-to-start-automatically-by-default"></a>Der DNS-Serverdienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:**  Der DNS-Serverdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  Der DNS-Serverdienst wird beim Start des Servers möglicherweise nicht automatisch gestartet. Wenn dieser Dienst beendet wurde, erfolgen keine DNS-Aktualisierungen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dns-server-service-to-start-automatically"></a>So konfigurieren Sie den DNS-Serverdienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DNS-Server**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="active-directory-web-services-is-not-set-to-the-default-start-mode"></a>Für die Active Directory-Webdienste ist nicht der Standardstartmodus festgelegt  
 **Problem:**  Für die Active Directory-Webdienste ist nicht der Standardstartmodus "Automatisch" festgelegt.  
  
 **Auswirkung:**  Für die Active Directory-Webdienste (ADWS) ist nicht der Standardstartmodus "Automatisch" festgelegt. Wenn ADWS auf dem Server beendet oder deaktiviert wurde, können Clientanwendungen wie das Active Directory-Modul für Windows PowerShell oder das Active Directory-Verwaltungscenter nicht auf Verzeichnisdienstinstanzen zugreifen oder diese verwalten, die auf diesem Server ausgeführt werden. Weitere Informationen finden Sie unter [Neuigkeiten in AD DS: Active Directory-Webdienste](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in der technischen Bibliothek für Windows Server.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-active-directory-web-services-service-to-start-automatically"></a>So konfigurieren Sie die Active Directory-Webdienste für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Active Directory-Webdienste**, und klicken Sie dann auf**Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-dhcp-client-service-should-be-configured-to-start-automatically-by-default"></a>Der DHCP-Clientdienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:**  Der DHCP-Clientdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  Der DHCP-Clientdienst wird beim Start des Servers nicht automatisch gestartet. Wenn dieser Dienst beendet wurde, können Clientcomputer keine IP-Adresse vom Server empfangen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dhcp-client-service-to-start-automatically"></a>So konfigurieren Sie den DHCP-Clientdienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DHCP-Client**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-iis-admin-service-should-be-configured-to-start-automatically-by-default"></a>Der IIS-Verwaltungsdienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:** Der IIS-Verwaltungsdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:** Der IIS-Verwaltungsdienst wird beim Start des Servers nicht automatisch gestartet. Wenn dieser Dienst beendet wurde, können Sie möglicherweise nicht auf Websites zugreifen, die auf dem Server ausgeführt werden, z. B. Remotewebzugriff.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-iis-admin-service-to-start-automatically"></a>So konfigurieren Sie den IIS-Verwaltungsdienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **IIS-Verwaltungsdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-world-wide-web-publishing-service-should-be-configured-to-start-automatically-by-default"></a>Der WWW-Publishingdienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:**  Der WWW-Publishingdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  Der WWW-Publishingdienst wird beim Start des Servers möglicherweise nicht automatisch gestartet. Wenn dieser Dienst beendet wurde, können Sie möglicherweise nicht auf Websites zugreifen, die auf dem Server ausgeführt werden, z. B. Remotewebzugriff.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-world-wide-web-publishing-service-to-start-automatically"></a>So konfigurieren Sie den WWW-Publishingdienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **WWW-Publishingdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-remote-registry-service-should-be-configured-to-start-automatically-by-default"></a>Der Remoteregistrierungsdienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:**  Der Remoteregistrierungsdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  
  
 Der Remoteregistrierungsdienst wird beim Start des Servers möglicherweise nicht automatisch gestartet. Wenn dieser Dienst beendet wurde, können Sie möglicherweise einige Netzwerkvorgänge nicht mehr von einem Remotestandort aus ausführen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-remote-registry-service-to-start-automatically"></a>So konfigurieren Sie den Remoteregistrierungsdienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Remoteregistrierung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-remote-desktop-gateway-service-should-be-configured-to-start-automatically-by-default"></a>Der Remotedesktopgateway-Dienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:**  Der Remotedesktopgateway-Dienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  Wenn dieser Dienst beendet wurde, können Benutzer nicht mit Remotewebzugriff auf Computer zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-remote-desktop-gateway-service-to-start-automatically"></a>So konfigurieren Sie den Remotedesktopgateway-Dienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Remotedesktopgateway**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch (Verzögerter Start)**, und klicken Sie dann auf **OK**.  
  
### <a name="the-windows-time-service-should-be-configured-to-start-automatically-by-default"></a>Der Windows-Zeitdienst sollte standardmäßig für den automatischen Start konfiguriert sein  
 **Problem:**  Der Windows-Zeitdienst ist nicht für den automatischen Start konfiguriert.  
  
 **Auswirkung:**  Wenn dieser Dienst beendet wurde, sind Zeit- und Datumssynchronisierung nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-windows-time-service-to-start-automatically"></a>So konfigurieren Sie den Windows-Zeitdienst für den automatischen Start  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Windows-Zeitgeber**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-started"></a>Der MSDTC-Dienst (Distributed Transaction Coordinator) sollte gestartet werden  
 **Problem:**  Der MSDTC-Dienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn der Dienst beendet wird, können bestimmte SQL Server- oder COM-Funktionen fehlschlagen. Anwendungen, die Microsoft SQL Server- oder COM-Funktionen verwenden, funktionieren daher möglicherweise nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-start-the-distributed-transaction-coordinator-service"></a>So starten Sie den Distributed Transaction Coordinator-Dienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Distributed Transaction Coordinator**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-netlogon-service-should-be-started"></a>Der Anmeldedienst sollte gestartet werden  
 **Problem:**  Der Anmeldedienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn der Dienst nicht gestartet wird, authentifiziert der Server Benutzer und Dienste möglicherweise nicht.  
  
 **Lösung:**  
  
##### <a name="to-start-the-netlogon-service"></a>So starten Sie den Anmeldedienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Netlogon**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-dns-client-service-should-be-started"></a>Der DNS-Clientdienst sollte gestartet werden  
 **Problem:**  Der DNS-Clientdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn dieser Dienst nicht gestartet wurde, kann der Server DNS-Namen möglicherweise nicht auflösen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dns-client-service"></a>So starten Sie den DNS-Clientdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DNS-Client**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-dns-server-service-should-be-started"></a>Der DNS-Serverdienst sollte gestartet werden  
 **Problem:**  Der DNS-Serverdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn der DNS-Serverdienst nicht gestartet wurde, erfolgen möglicherweise keine DNS-Aktualisierungen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dns-server-service"></a>So starten Sie den DNS-Serverdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DNS-Server**, und klicken Sie dann auf **Starten**.  
  
### <a name="active-directory-web-services-is-not-started"></a>Die Active Directory-Webdienste wurden nicht gestartet  
 **Problem:**  Die Active Directory-Webdienste wurden nicht gestartet.  
  
 **Auswirkung:**  Die Active Directory-Webdienste (ADWS) wurden nicht gestartet. Wenn ADWS auf dem Server beendet oder deaktiviert wurde, können Clientanwendungen wie das Active Directory-Modul für Windows PowerShell oder das Active Directory-Verwaltungscenter nicht auf Verzeichnisdienstinstanzen zugreifen oder diese verwalten, die auf diesem Server ausgeführt werden. Weitere Informationen finden Sie unter [Neuigkeiten in AD DS: Active Directory-Webdienste](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in der technischen Bibliothek für Windows Server.  
  
 **Lösung:**  
  
##### <a name="to-start-the-active-directory-web-services-service"></a>So starten Sie den Dienst "Active Directory-Webdienste"  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Active Directory-Webdienste**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-dhcp-client-service-should-be-started"></a>Der DHCP-Clientdienst sollte gestartet werden  
 **Problem:**  Der DHCP-Clientdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn dieser Dienst beendet wurde, können Clientcomputer keine IP-Adresse vom Server empfangen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dhcp-client-service"></a>So starten Sie den DHCP-Clientdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DHCP-Client**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-iis-admin-service-should-be-started"></a>IIS-Verwaltungsdienst sollte gestartet werden  
 **Problem:**  Der IIS-Verwaltungsdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn dieser Dienst beendet wurde, können Sie möglicherweise nicht auf Websites zugreifen, die auf dem Server ausgeführt werden, z. B. Remotewebzugriff.  
  
 **Lösung:**  
  
##### <a name="to-start-the-iis-admin-service"></a>So starten Sie den IIS-Verwaltungsdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **IIS-Verwaltungsdienst**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-world-wide-web-publishing-service-should-be-started"></a>Der WWW-Publishingdienst sollte gestartet werden  
 **Problem:**  Der WWW-Publishingdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn dieser Dienst beendet wurde, können Sie möglicherweise nicht auf Websites zugreifen, die auf dem Server ausgeführt werden, z. B. Remotewebzugriff.  
  
 **Lösung:**  
  
##### <a name="to-start-the-world-wide-web-publishing-service"></a>So starten Sie den WWW-Publishingdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **WWW-Publishingdienst**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-remote-desktop-gateway-service-should-be-started"></a>Der Remotedesktopgateway-Dienst sollte gestartet werden  
 **Problem:**  Der Remotedesktopgateway-Dienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn dieser Dienst beendet wurde, können Benutzer nicht mit Remotewebzugriff auf Computer zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-start-the-remote-desktop-gateway-service"></a>Starten Sie den Remotedesktopgateway-Diensts  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Remotedesktopgateway**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-windows-time-service-should-be-started"></a>Der Windows-Zeitdienst sollte gestartet werden  
 **Problem:**  Der Windows-Zeitdienst wird auf dem Server nicht ausgeführt.  
  
 **Auswirkung:**  Wenn dieser Dienst beendet wurde, sind Zeit- und Datumssynchronisierung nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-start-the-windows-time-service"></a>Der Windows-Zeitdienst starten  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Windows-Zeitgeber**, und klicken Sie dann auf **Starten**.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-logon-account-should-be-nt-authoritynetwork-service"></a>Das Anmeldekonto für den MSDTC-Dienst (Distributed Transaction Coordinator) sollte "NT AUTORITÄT\Netzwerkdienst" sein  
 **Problem:**  Das Standardanmeldekonto für den MSDTC-Diensts (Distributed Transaction Coordinator) wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Anwendungen, die SQL Server- oder COM-Funktionen verwenden, funktionieren daher möglicherweise nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-change-the-logon-account-for-the-service"></a>So ändern Sie das Anmeldekonto für den Dienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Distributed Transaction Coordinator**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Dieses Konto** aus, geben Sie **NT AUTORITÄT\Netzwerkdienst** ein, und klicken Sie auf **OK**.  
  
### <a name="the-netlogon-service-should-use-the-local-system-account-as-its-logon-account"></a>Der Anmeldedienst sollte das lokale Systemkonto als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den Anmeldedienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Daher authentifiziert der Server Benutzer und Dienste möglicherweise nicht.  
  
 **Lösung:**  
  
##### <a name="to-change-the-netlogon-service-logon-account"></a>So ändern Sie das Anmeldekonto für den Anmeldedienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Netlogon**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Lokales Systemkonto** aus.  
  
### <a name="the-dns-client-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Der DNS-Clientdienst sollte das Konto "NT AUTORITÄT\Netzwerkdienst" als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den DNS-Clientdienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Daher kann der Server möglicherweise keine DNS-Namen auflösen.  
  
 **Lösung:**  
  
##### <a name="to-change-the-dns-client-service-logon-account"></a>So ändern Sie das Anmeldekonto für den DNS-Clientdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DNS-Client**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Dieses Konto** aus, und geben Sie dann **NT AUTORITÄT\Netzwerkdienst** ein.  
  
### <a name="the-dns-server-service-should-use-the-local-system-account-as-its-logon-account"></a>Der DNS-Serverdienst sollte das lokale Systemkonto als Anmeldekonto verwenden.  
 **Problem:**  Das Standardanmeldekonto für den DNS-Serverdienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Daher erfolgen möglicherweise keine DNS-Aktualisierungen.  
  
 **Lösung:**  
  
##### <a name="to-change-the-dns-server-service-logon-account"></a>So ändern Sie das Anmeldekonto für den DNS-Serverdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DNS-Server**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Lokales Systemkonto** aus.  
  
### <a name="active-directory-web-services-is-not-the-default-logon-account"></a>Die Active Directory-Webdienste sind nicht das Standardanmeldekonto  
 **Problem:**  Die Active Directory-Webdienste sind nicht das Standardanmeldekonto. Standardmäßig wird für das Anmeldekonto das **Lokale Systemkonto** festgelegt.  
  
 **Auswirkung:**  Die Active Directory-Webdienste (ADWS) wurden nicht gestartet. Wenn ADWS auf dem Server beendet oder deaktiviert wurde, können Clientanwendungen wie das Active Directory-Modul für Windows PowerShell oder das Active Directory-Verwaltungscenter nicht auf Verzeichnisdienstinstanzen zugreifen oder diese verwalten, die auf diesem Server ausgeführt werden. Weitere Informationen finden Sie unter [Neuigkeiten in AD DS: Active Directory-Webdienste](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in der technischen Bibliothek für Windows Server.  
  
 **Lösung:**  
  
##### <a name="to-change-the-active-directory-web-services-logon-account"></a>So ändern Sie das Anmeldekonto von "Active Directory-Webdienste"  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Active Directory-Webdienste**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Ändern Sie die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie in "Active Directory-Webdienste" unter **Eigenschaften** auf die Registerkarte **Anmelden**.  
  
5.  Wählen Sie die Option **Lokales Systemkonto** aus, und klicken Sie dann auf **OK**.  
  
### <a name="the-windows-update-service-should-use-the-local-system-account-as-its-logon-account"></a>Der Windows Update-Dienst sollte das lokale Systemkonto als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den Dienst für Automatische Updates wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Daher kann der Server möglicherweise keine automatischen Updates empfangen.  
  
 **Lösung:**  
  
##### <a name="to-change-the-windows-update-service-logon-account"></a>So ändern Sie das Anmeldekonto für den Windows Update-Dienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Windows Update**, und klicken Sie dann auf "Eigenschaften".  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Lokales Systemkonto** aus.  
  
### <a name="the-dhcp-client-service-should-use-the-nt-authoritylocalservice-account-as-its-logon-account"></a>Der DHCP-Clientdienst sollte das Konto "NT AUTORITÄT\LocalService" als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den DHCP-Clientdienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Daher empfängt der Client keine IP-Adressen vom Server.  
  
 **Lösung:**  
  
##### <a name="to-change-the-dhcp-client-service-logon-account"></a>So ändern Sie das Anmeldekonto für den DHCP-Clientdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **DHCP-Client**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Dieses Konto** aus, und geben Sie dann **NT AUTHORITY\Local Service** ein.  
  
### <a name="the-iis-admin-service-should-use-the-local-system-account-as-its-logon-account"></a>Der IIS-Verwaltungsdienst sollte das lokale Systemkonto als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den IIS-Verwaltungsdienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Daher können Sie möglicherweise nicht auf Websites zugreifen, die auf dem Server ausgeführt werden, z. B. Remotewebzugriff.  
  
 **Lösung:**  
  
##### <a name="to-change-the-service-logon-account"></a>So ändern Sie das Anmeldekonto für den Dienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **IIS-Verwaltungsdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Lokales Systemkonto** aus.  
  
### <a name="the-world-wide-web-publishing-service-should-use-the-local-system-account-as-its-logon-account"></a>Der WWW-Publishingdienst sollte das lokale Systemkonto als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den WWW-Publishingdienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die Berechtigungen, die für einen erwartungsgemäßen Betrieb erforderlich sind. Daher können Sie möglicherweise nicht auf Websites zugreifen, die auf dem Server ausgeführt werden, z. B. Remotewebzugriff.  
  
 **Lösung:**  
  
##### <a name="to-change-the-world-wide-web-publishing-service-logon-account"></a>So ändern Sie das Anmeldekonto für den WWW-Publishingdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf **WWW-Publishingdienst**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Lokales Systemkonto** aus.  
  
### <a name="the-remote-desktop-gateway-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Der Remotedesktopgateway-Dienst sollte das Konto "NT AUTORITÄT\Netzwerkdienst" als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den Remotedesktopgateway-Dienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die geeigneten Berechtigungen für einen erwartungsgemäßen Betrieb. Daher können Benutzer möglicherweise nicht mit Remotewebzugriff auf Computer zugreifen .  
  
 **Lösung:**  
  
##### <a name="to-change-the-remote-desktop-gateway-service-logon-account"></a>So ändern Sie das Anmeldekonto für den Remotedesktopgateway-Dienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Remotedesktopgateway**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Dieses Konto** aus, und geben Sie dann **NT AUTORITÄT\Netzwerkdienst** ein.  
  
### <a name="the-windows-time-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Der Windows-Zeitdienst sollte das Konto "NT AUTORITÄT\Netzwerkdienst" als Anmeldekonto verwenden  
 **Problem:**  Das Standardanmeldekonto für den Windows-Zeitdienst wurde geändert.  
  
 **Auswirkung:**  Der Dienst verfügt möglicherweise nicht über die geeigneten Berechtigungen für einen erwartungsgemäßen Betrieb. Daher ist die Synchronisierung von Datum und Uhrzeit möglicherweise nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-change-the-windows-time-service-logon-account"></a>So ändern Sie das Anmeldekonto für den Windows-Zeitdienst  
  
1.  Öffnen Sie "services.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Dienst **Windows-Zeitgeber**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Dieses Konto** aus, und geben Sie dann **NT AUTHORITY\Local Service** ein.  
  
### <a name="the-built-in-administrators-group-does-not-have-the-right-to-log-on-as-batch-job"></a>Die integrierte Gruppe "Administratoren" verfügt nicht über die Berechtigung zum Anmelden als Batchauftrag  
 **Problem:**  Die integrierte Gruppe "Administratoren" verfügt nicht über die Berechtigung zur Anmeldung als Batchauftrag.  
  
 **Auswirkung:**  Wenn der Administrator eine Warnung erstellt und diese so konfiguriert, dass sie ausgeführt wird, wenn der Administrator nicht angemeldet ist, schlägt die Warnung mit Fehlercode 2147943785 fehl.  
  
 **Lösung:**  Weitere Informationen zur Verwendung der integrierten Administratorgruppennamen Gruppe die Berechtigung zum Anmelden als Batchauftrag erteilen, finden Sie unter [der integrierten Administratorengruppe das Recht zum Anmelden als Batchauftrag erteilen](https://technet.microsoft.com/library/jj635076) (https://technet.microsoft.com/library/jj635076).  
  
### <a name="the-windows-firewall-is-turned-off"></a>Die Windows-Firewall ist deaktiviert  
 **Problem:**  Die Windows-Firewall ist deaktiviert. Der Standardwert ist "Ein".  
  
 **Auswirkung:**  Abhängig von Ihren Firewalleinstellungen kann die Windows-Firewall Ihren Server und das Netzwerk vor bösartigen Aktivitäten schützen, indem einige Informationen blockiert und nicht durch den Server übergeben werden.  
  
 **Lösung:**  
  
##### <a name="to-turn-on-windows-firewall-on-the-server"></a>So schalten Sie die Windows-Firewall auf dem Server ein  
  
1.  Öffnen Sie die Systemsteuerung auf dem Server.  
  
2.  Klicken Sie in der Systemsteuerung auf **System und Sicherheit** und dann auf **Windows-Firewall**.  
  
3.  Klicken Sie in der Windows-Firewall auf **Windows-Firewall ein- oder ausschalten**, wählen Sie **Windows-Firewall aktivieren** aus, und klicken Sie dann auf **OK**.  
  
### <a name="the-internal-network-adapter-is-not-configured-to-register-ip-address-in-dns"></a>Der interne Netzwerkadapter ist nicht für die Registrierung seiner IP-Adresse im DNS konfiguriert  
 **Problem:**  Der interne Netzwerkadapter ist nicht für die Registrierung seiner IP-Adresse im DNS konfiguriert.  
  
 **Auswirkung:**  Wenn die IP-Adresse des internen Netzwerkadapters nicht in DNS registriert ist, es möglich, die Zugriff auf den Server mit den Namen des Servers s möglicherweise nicht.  
  
 **Lösung:**  Vergewissern Sie sich, dass der interne Netzwerkadapter so konfiguriert ist, dass er in DNS registriert wird.  
  
### <a name="dns-the-values-for-the-dns-forwardingtimeout-and-recursiontimeout-registry-key-are-identical"></a>DNS: Die Werte für die DNS-Registrierungsschlüssel "ForwardingTimeout" und "RecursionTimeout" sind identisch  
 **Problem:**  Der Wert des DNS-Registrierungsschlüssels "ForwardingTimeout" muss sich vom Wert für "RecursionTimeout" unterscheiden.  
  
 **Auswirkung:**  Sie können möglicherweise nicht über den Namen auf Internetressourcen zugreifen.  
  
 **Lösung:**  Der Wert für den Registrierungsschlüssels "RecursionTimeout" muss größer als der Wert des Schlüssels "ForwardingTimeout" in der Registrierung unter "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters" sein.  
  
### <a name="the-forward-dns-zone-for-your-active-directory-domain-does-not-allow-secure-updates"></a>Die Forward-DNS-Zone für die Active Directory-Domäne lässt keine sicheren Updates zu  
 **Problem:**  Sie sollten die Forward-Lookupzone so konfigurieren, dass nur sichere dynamische Updates zulässig sind.  
  
 **Auswirkung:**  Wenn Sie sichere dynamische Updates aktivieren, können Änderungen an Datensätzen nur von autorisierten Benutzern und Hosts vorgenommen werden.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-forward-lookup-zone-for-your-active-directory-domain"></a>So konfigurieren Sie die Forward-Lookupzone für Ihre Active Directory-Domäne  
  
1.  Öffnen Sie "dnsmgmt.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Forward-Lookupzone für Ihre Active Directory-Domäne, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie in der Dropdown-Liste **Dynamische Updates** die Option **Nur sichere** aus, und klicken Sie dann auf **OK**.  
  
### <a name="the-forward-dns-zone-does-not-allow-secure-updates"></a>Die Forward-DNS-Zone lässt keine sicheren Updates zu  
 **Problem:**  Sie sollten die Forward-Lookupzone für die Zone "_msdcs.*" so konfigurieren, dass nur sichere dynamische Updates zulässig sind.  
  
 **Auswirkung:**  Wenn Sie sichere dynamische Updates aktivieren, können Änderungen an Datensätzen in der Zone "_msdcs.*" nur von autorisierten Benutzern und Hosts vorgenommen werden.  
  
 **Lösung:**  
  
##### <a name="to-allow-secure-updates-in-the-msdcs-zone"></a>So erlauben Sie sichere Updates in der _msdcs-Zone  
  
1.  Öffnen Sie "dnsmgmt.msc" auf dem Server.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Forward-Lookupzone für die "_msdcs"-Zone, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie in der Dropdown-Liste **Dynamische Updates** die Option **Nur sichere** aus, und klicken Sie dann auf **OK**.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Die verstärkte Sicherheitskonfiguration für Internet Explorer ist nicht aktiviert  
 **Problem:**  Internet Explorer Enhanced Security Configuration (IE ESC) ist derzeit nicht für die Gruppe "Administratoren" aktiviert.  
  
 **Auswirkung:**  Wenn die verstärkte Sicherheitskonfiguration für Internet Explorer für die Gruppe "Administratoren" nicht aktiviert ist, sind Ihr Server und Internet Explorer in erhöhtem Maße bösartigen Angriffen durch Webinhalt und Anwendungsskripts ausgesetzt.  
  
 **Lösung:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>So aktivieren Sie die verstärkte Sicherheitskonfiguration für Internet Explorer  
  
1.  Öffnen Sie **Server-Manager** auf dem Server, und klicken Sie dann auf **Lokaler Server**.  
  
2.  Ändern Sie im **Eigenschaftenbereich** die Einstellung für **Verstärkte Sicherheitskonfiguration für IE** in **Ein**, und klicken Sie dann auf **OK**.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Die verstärkte Sicherheitskonfiguration für Internet Explorer ist nicht aktiviert  
 **Problem:**  Internet Explorer Enhanced Security Configuration (IE ESC) ist derzeit nicht für die Gruppe Benutzer aktiviert.  
  
 **Auswirkung:**  Wenn die verstärkte Sicherheitskonfiguration für Internet Explorer für die Benutzergruppe nicht aktiviert ist, sind Ihr Server und Internet Explorer in erhöhtem Maße bösartigen Angriffen durch Webinhalt und Anwendungsskripts ausgesetzt.  
  
 **Lösung:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>So aktivieren Sie die verstärkte Sicherheitskonfiguration für Internet Explorer  
  
1.  Öffnen Sie **Server-Manager**, und klicken Sie dann auf **Lokaler Server**.  
  
2.  Ändern Sie im **Eigenschaftenbereich** die Einstellung für **Verstärkte Sicherheitskonfiguration für IE** in **Ein**, und klicken Sie dann auf **OK**.  
  
### <a name="the-source-server-remains-in-active-directory-sites-and-services"></a>Der Quellserver verbleibt in "Active Directory-Standorte und -Dienste"  
 **Problem:**  Der Quellserver, auf dem Windows Small Business Server ausgeführt wird, ist in "Active Directory-Standorte und-Dienste" unter "Standardname-des-ersten-Standorts" weiterhin vorhanden.  
  
 **Auswirkung:**  Wenn der Quellserver in Active Directory-Standorte und-Dienste bleibt, können Connectivity Problems auf Clientcomputern auftreten: s.  
  
 **Lösung:**  Sie sollten den Quellserver tiefer stufen, ihn aus der Domäne entfernen und dann aus "Active Directory-Standorte und Dienste" und "Active Directory-Benutzer und -Computer" löschen.  
  
### <a name="source-server-remains-in-sbscomputer-ou"></a>Der Quellserver verbleibt in der Organisationseinheit "SBSComputer"  
 **Problem:**  Der Quellserver, auf dem Windows Small Business Server ausgeführt wird, ist in "Active Directory-Benutzer und-Computer" weiterhin vorhanden.  
  
 **Auswirkung:**  Wenn der Quellserver in Active Directory-Benutzer und-Computer bleibt, können Connectivity Problems auf Clientcomputern auftreten: s.  
  
 **Lösung:**  Sie sollten den Quellserver tiefer stufen, ihn aus der Domäne entfernen und dann aus "Active Directory-Standorte und Dienste" und "Active Directory-Benutzer und -Computer" löschen.  
  
### <a name="a-group-policy-is-missing"></a>Eine Gruppenrichtlinie fehlt  
 **Problem:**  Die Gruppenrichtlinie "Standarddomänenrichtlinie" fehlt.  
  
 **Auswirkung:**  Die Standarddomänenrichtlinie ist für ordnungsgemäße Domänenfunktionen erforderlich.  
  
 **Lösung:**  
  
##### <a name="to-restore-a-missing-group-policy"></a>So stellen Sie eine fehlende Gruppenrichtlinie wieder her  
  
1.  Öffnen Sie "gpmc.msc" auf dem Server.  
  
2.  Erweitern Sie im Gruppenrichtlinien-Manager die Domänengesamtstruktur, und suchen Sie die Konsolenstruktur für das Gruppenrichtlinienobjekt **Standarddomänenrichtlinie**.  
  
3.  Wenn die Richtlinie in der Struktur nicht angezeigt wird, stellen Sie sie aus einer Systemstatussicherung wieder her.  
  
### <a name="no-dns-name-server-resource-records"></a>Keine DNS-Namenserver-Ressourceneinträge  
 **Problem:**  In der Forward-Lookupzone für Ihren Server sind keine DNS-Namenserver-Ressourceneinträge enthalten.  
  
 **Auswirkung:**  Wenn kein DNS-Namenserver-Ressourceneintrag in der Forward-Lookupzone für die Active Directory-Domäne vorhanden ist, können Benutzern möglicherweise nicht auf Ressourcen im Netzwerk oder im Internet zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-restore-missing-dns-name-server-resource-records"></a>So stellen Sie fehlende DNS-Namenserver-Ressourceneinträge wieder her  
  
1.  Öffnen Sie "dnsmgmt.msc" auf dem Server.  
  
2.  Klicken Sie im DNS-Manager mit der rechten Maustaste auf die Forward-Lookupzone für die Active Directory-Domäne, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Vergewissern Sie sich auf der Registerkarte **Namenserver**, dass die Einstellungen richtig sind.  
  
4.  Nehmen Sie die erforderlichen Änderungen vor, und klicken Sie dann auf **OK**, um die Einstellungen zu speichern.  
  
### <a name="no-dns-name-server-records"></a>Keine DNS-Namenservereinträge  
 **Problem:**  Es sind für Ihren Server keine DNS-Namenserver-Ressourceneinträge in der Zone "_msdcs" enthalten (Beispiel: "_msdcs.contoso.local").  
  
 **Auswirkung:**  Wenn kein DNS-Namenserver-Ressourceneintrag in der Zone "_msdcs" für die Active Directory-Domäne vorhanden ist, können Benutzern möglicherweise nicht auf Ressourcen im Netzwerk oder im Internet zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-restore-missing-dns-name-server-records"></a>So stellen Sie fehlende DNS-Namenserver-Einträge wieder her  
  
1.  Öffnen Sie "dnsmgmt.msc" auf dem Server.  
  
2.  Klicken Sie im DNS-Manager mit der rechten Maustaste auf die Forward-Lookupzone für die "_msdcs"-Zone, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Vergewissern Sie sich auf der Registerkarte **Namenserver**, dass die Einstellungen richtig sind.  
  
4.  Nehmen Sie die erforderlichen Änderungen vor, und klicken Sie dann auf **OK**, um die Einstellungen zu speichern.  
  
### <a name="no-dns-name-server-records"></a>Keine DNS-Namenservereinträge  
 **Problem:**  Es sind für die Forward-Lookupzone "delegated _msdcs" keine DNS-Namenserver-Ressourceneinträge enthalten.  
  
 **Auswirkung:**  Wenn kein DNS-Namenserver-Ressourceneintrag für die Forward-Lookupzone "delegated _msdcs" vorhanden ist, kann der DNS-Serverdienst die DNS-Ressourceneinträge für die Domäne nicht auflösen und wird nicht gestartet.  
  
 **Lösung:**  
  
##### <a name="to-reconfigure-missing-dns-name-server-records"></a>So konfigurieren Sie fehlende DNS-Namenserver-Einträge neu  
  
1.  Öffnen Sie "dnsmgmt.msc" auf dem Server.  
  
2.  Erweitern Sie im DNS-Manager den Namen Ihres Servers, und klicken Sie dann auf **Forward-Lookupzonen**.  
  
3.  Klicken Sie auf die Forward-Lookupzone für Ihre Active Directory-Domäne (z. B. "contoso.local").  
  
4.  Die Zone "delegated _msdcs" wird als abgeblendeter Ordner angezeigt. Klicken Sie mit der rechten Maustaste auf die Zone "_msdcs", und klicken Sie dann auf **Eigenschaften**.  
  
5.  Vergewissern Sie sich auf der Registerkarte **Namenserver**, dass die Einstellungen richtig sind.  
  
6.  Nehmen Sie die erforderlichen Änderungen vor, und klicken Sie dann auf **OK**, um die Einstellungen zu speichern.  
  
### <a name="authenticated-users-not-a-member-of-the-pre-windows-2000-compatible-access-group"></a>"Authentifizierte Benutzer" ist kein Mitglied der Gruppe "Prä-Windows 2000 kompatibler Zugriff"  
 **Problem:**  Die Gruppe "Authentifizierte Benutzer" ist kein Mitglied der Gruppe "Prä-Windows 2000 kompatibler Zugriff"  
  
 **Auswirkung:**  Ist die integrierte Gruppe "Authentifizierte Benutzer" kein Mitglied der Gruppe "Prä-Windows 2000 kompatibler Zugriff", können bei Netzwerkbenutzern "Zugriff verweigert"-Fehler auftreten.  
  
 **Lösung:**  
  
##### <a name="to-add-authenticated-users-to-the-pre-windows-2000-compatible-access-group"></a>So fügen Sie die Gruppe "Authentifizierte Benutzer" zur Gruppe "Prä-Windows 2000 kompatibler Zugriff" hinzu  
  
1.  Öffnen Sie "dsa.msc" auf dem Server.  
  
2.  Klicken Sie im Ordner **Builtin** mit der rechten Maustaste auf **Prä-Windows 2000 kompatibler Zugriff**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Hinzufügen**, geben Sie **Authentifizierte Benutzer** ein, und klicken Sie dann zweimal auf **OK**.  
  
### <a name="dns-client-not-configured"></a>Der DNS-Client ist nicht konfiguriert  
 **Problem:**  Der DNS-Client ist nicht so konfiguriert, dass er nur auf die interne IP-Adresse des Servers verweist.  
  
 **Auswirkung:**  Wenn der DNS-Client nicht so konfiguriert ist, dass er nur auf die interne IP-Adresse des Servers verweist, kann ein Fehler bei der DNS-Namensauflösung auftreten.  
  
 **Lösung:**  
  
##### <a name="to-configure-dns-to-point-only-to-the-server-s-internal-ip-address"></a>So konfigurieren Sie DNS, um nur für den Server s interne IP-Adresse verweisen.  
  
1.  Öffnen Sie auf dem Clientcomputer die Seite **Eigenschaften** für die Netzwerkverbindung.  
  
2.  Stellen Sie sicher, dass der DNS-Client so konfiguriert ist, dass er nur auf die interne IP-Adresse des Servers verweist.  
  
### <a name="default-application-pool-value-changed"></a>Der Standardwert für den Anwendungspool wurde geändert  
 **Problem:**  Die maximale Anzahl von Arbeitsprozessen für den Anwendungspool "DefaultAppPool" ist nicht auf den Standardwert "1" festgelegt.  
  
 **Auswirkung:**  Benutzer können möglicherweise keine Verbindung mit webbasierten Windows Small Business Server-Diensten herstellen.  
  
 **Lösung:**  
  
##### <a name="to-reset-maximum-worker-processes-for-the-default-application-pool"></a>So setzen Sie die maximale Anzahl von Arbeitsprozessen für den Standardanwendungspool zurück  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Anwendungspools**.  
  
3.  Klicken Sie in **Anwendungspools** mit der rechten Maustaste auf **DefaultAppPool**, und klicken Sie dann auf **Erweiterte Einstellungen**.  
  
4.  Ändern Sie in **Erweiterte Einstellungen** den Wert für **Maximale Anzahl von Arbeitsprozessen** auf "1", und klicken Sie dann auf **OK**.  
  
5.  Schließen Sie **Erweiterte Einstellungen**, klicken Sie mit der rechten Maustaste auf **DefaultAppPool**, beenden Sie den Anwendungspool, und starten Sie ihn anschließend neu.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-account"></a>Der Anwendungspool für Remotewebzugriff verwendet nicht das Standardkonto  
 **Problem:**  Der Anwendungspool "RemoteAppPool" wird nicht mit dem Standardkonto ausgeführt.  
  
 **Auswirkung:**  Netzwerkbenutzer können möglicherweise nicht auf die Website für Remotewebzugriff zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-reset-the-remote-application-pool-to-use-the-default-account"></a>So setzen Sie den Remoteanwendungspool zurück, damit er das Standardkonto verwendet  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Anwendungspools**.  
  
3.  Klicken Sie in **Anwendungspools** mit der rechten Maustaste auf **RemoteAppPool**, und klicken Sie dann auf **Erweiterte Einstellungen**.  
  
4.  Ändern Sie die **Identität** in **Erweiterte Einstellungen** auf **NetworkService**, und klicken Sie dann auf**OK**.  
  
5.  Schließen Sie **Erweiterte Einstellungen**, klicken Sie mit der rechten Maustaste auf **RemoteAppPool**, beenden Sie den Anwendungspool, und starten Sie ihn anschließend neu.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-net-framework-version"></a>Der Anwendungspool für Remotewebzugriff verwendet nicht die .NET Framework-Standardversion  
 **Problem:**  Der Anwendungspool "RemoteAppPool" wird nicht mit der Standardversion von Microsoft .NET Framework ausgeführt.  
  
 **Auswirkung:**  Netzwerkbenutzer können möglicherweise nicht auf die Website für Remotewebzugriff zugreifen.  
  
 **Lösung:**  
  
##### <a name="to-change-the-net-framework-version-used-by-the-remoteapppool"></a>So ändern Sie die von "RemoteAppPool" verwendete .NET Framework-Version  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Anwendungspools**.  
  
3.  Klicken Sie in **Anwendungspools** mit der rechten Maustaste auf **RemoteAppPool**, und klicken Sie dann auf **Erweiterte Einstellungen**.  
  
4.  Ändern Sie in **Erweiterte Einstellungen**, die **.NET Framework-Version** in "v4.0", und klicken Sie dann auf **OK**.  
  
5.  Schließen Sie **Erweiterte Einstellungen**, klicken Sie mit der rechten Maustaste auf **RemoteAppPool**, beenden Sie den Anwendungspool, und starten Sie ihn anschließend neu.  
  
### <a name="the-remoteaccesslog-file-is-larger-than-1-gb-in-size"></a>Die Datei "RemoteAccess.log" ist größer als 1 GB  
 **Problem:**  Wenn die Größe der Datei "Remoteaccess.log" 1 GB überschreitet, können Probleme aufgrund von wenig Speicherplatz auf dem Systemlaufwerk auftreten.  
  
 **Auswirkung:**  Wenn die Datei "Remoteaccess.log" zu groß ist, kann dies Speicherplatz Problem: s auf Laufwerk "c:".  
  
 **Lösung:**  Nach dem Sichern des Servers können Sie die Datei "Remoteaccess.log" aus dem Ordner "%ProgramData%\Microsoft\Windows Server\Logs\WebApps" löschen.  
  
### <a name="default-web-sites-log-directory-is-over-1-gb-in-size"></a>Protokollverzeichnis der Standardwebsite ist größer als 1 GB  
 **Problem:**  Wenn die Größe der Protokollordner der Standardwebsite 1 GB überschreitet, können Sie Fehler von wenig Speicherplatz auf dem Systemlaufwerk auftreten.  
  
 **Auswirkung:**  Wenn der Protokollordner der Standardwebsite zu groß ist, kann dies Speicherplatz Problem: s auf Laufwerk C:  
  
 **Lösung:**  Nachdem Sie den Server gesichert haben und während die Standardwebsite angehalten wurde, können Sie die Protokolldateien im Ordner "C:\inetpub\logs\LogFiles\W3SVC1" löschen. Starten Sie anschließend die Standardwebsite.  
  
### <a name="no-binding-for-ssl-on-all-ip-addresses"></a>Keine Bindung für SSL an allen IP-Adressen  
 **Problem:**  Es erfolgt keine Bindung für Secure Sockets Layer (SSL) an allen IP-Adressen auf dem Server.  
  
 **Auswirkung:**  Wenn SSL nicht an alle IP-Adressen auf dem Server gebunden ist, sind einige Websites für Benutzer nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-bind-ssl-to-all-ip-addresses-on-the-server"></a>So binden Sie SSL an alle IP-Adressen auf dem Server  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager im Bereich **Verbindungen** Ihren Server und **Sites**, klicken Sie mit der rechten Maustaste auf **Standardwebsite**, und klicken Sie anschließend auf **Bindungen bearbeiten**.  
  
3.  Klicken Sie in **Sitebindungen** auf **Hinzufügen**, und wählen Sie dann die folgenden Einstellungen aus:  
  
    -   **Typ** = **Https**  
  
    -   **IP-Adresse** = **alle nicht zugewiesenen**  
  
    -   **Port** = 443  
  
4.  Wählen Sie ein SSL-Zertifikat aus, und klicken Sie dann zum Speichern der Änderungen auf **OK**.  
  
### <a name="no-binding-for-ssl-on-the-default-web-site"></a>Keine Bindung für SSL an der Standardwebsite  
 **Problem:**  Es erfolgt keine Bindung für SSL an der Standardwebsite.  
  
 **Auswirkung:**  Wenn SSL nicht an die Standardwebsite gebunden ist, sind manche Websites möglicherweise für Benutzer nicht verfügbar.  
  
 **Lösung:**  
  
##### <a name="to-bind-ssl-to-the-default-website"></a>So binden Sie SSL an die Standardwebsite  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager im Bereich **Verbindungen** Ihren Server und **Sites**, klicken Sie mit der rechten Maustaste auf **Standardwebsite**, und klicken Sie anschließend auf **Bindungen bearbeiten**.  
  
3.  Klicken Sie in **Sitebindungen** auf **Hinzufügen**, und wählen Sie dann die folgenden Optionen aus:  
  
    -   **Typ** = **Https**  
  
    -   **IP-Adresse** = **alle nicht zugewiesenen**  
  
    -   **Port** = 443  
  
    > [!NOTE]
    >  Wenn für eine bestimmte IP-Adresse eine HTTPS-Bindung für Port 443 vorhanden ist, ändern Sie das Attribut **IP-Adresse** für diese Bindung in **Keine zugewiesen**. Hierbei stellt die IP-Adresse 127.0.0.1 eine Ausnahme dar. Ändern Sie die Bindung für 127.0.0.1 nicht.  
  
4.  Wählen Sie ein SSL-Zertifikat aus, und klicken Sie dann zum Speichern der Änderungen auf **OK**.  
  
### <a name="a-certificate-expires-within-30-days"></a>Ein Zertifikat läuft innerhalb von 30 Tagen ab  
 **Problem:**  Ihr Serverzertifikat läuft innerhalb von 30 Tagen ab.  
  
 **Auswirkung:**  Der Server kann kein abgelaufenes Zertifikat verwenden. Wenn das Zertifikat abläuft, können Benutzer möglicherweise keine "Zugriff überall"-Funktionen verwenden.  
  
 **Lösung:**  Um zu verhindern, dass das Zertifikat abläuft, erneuern Sie es bei der vertrauenswürdigen Zertifizierungsstelle.  
  
### <a name="certificate-subject-does-not-match-the-name-configured-by-domain-name-wizard"></a>Der Zertifikatantragsteller stimmt nicht mit dem vom Domänennamen-Assistenten konfigurierten Namen überein  
 **Problem:**  Der Zertifikatantragsteller stimmt nicht mit dem Namen überein, der vom Domänennamen-Assistenten konfiguriert wurde.  
  
 **Auswirkung:**  Wenn der Zertifikatantragsteller nicht mit dem Namen übereinstimmt, der vom Domänennamen-Assistenten konfiguriert wurde, werden einige Websites nicht initialisiert. Andere Websites zeigen den Fehler "Es ist ein Problem mit dem Sicherheitszertifikat der Website."  
  
 **Lösung:**  Um dieses Problem zu beheben:, führen Sie die Set up Zugriff überall Wizard erneut aus, und geben Sie den richtigen Domänennamen für das Zertifikat, oder erwerben Sie ein neues Zertifikat, das den Domänennamen entspricht, die Sie verwenden möchten.  
  
### <a name="one-or-more-user-accounts-have-duplicate-cn-names"></a>Mindestens ein Benutzerkonto weist einen doppelten CN-Namen auf  
 **Problem:**  Eine oder mehrere Benutzerkonten weist einen doppelten CN-Namen: {0}.  
  
 **Auswirkung:**  Wenn Benutzerkonten doppelte CN-Namen aufweisen, können sich Benutzer möglicherweise nicht am Netzwerk anmelden. Außerdem können Suchvorgänge von Active Directory nach Benutzern zu falschen Werten führen.  
  
 **Lösung:**  Um dieses Problem zu beheben:, stellen Sie sicher, dass Netzwerkbenutzerkonten keine doppelten "CN =" Namen. Sie können Active Directory-Inhalte zur Überprüfung in eine Textdatei exportieren, um diesen Vorgang zu vereinfachen. Informationen hierzu finden Sie unter [Verwenden von LDIFDE zum Importieren und Exportieren von Verzeichnisobjekten in Active Directory (Knowledge Base-Artikel 237677)](https://support.microsoft.com/kb/237677) (https://support.microsoft.com/kb/237677).  
  
### <a name="nt-backup-is-installed"></a>NT Backup ist installiert  
 **Problem:**  Das Windows NT Backup-Programm ist auf dem Server installiert.  
  
 **Auswirkung:**   Windows Server Essentials wird Windows Server-Sicherung verwendet. Wenn das Windows NT Backup-Programm ebenfalls installiert ist, können Konflikte zwischen den beiden Sicherungsprogrammen auftreten. Dies kann zu einem Fehler bei der Windows Server-Sicherung führen. Möglicherweise können Sie auch keine Sicherung zum Wiederherstellen des Servers verwenden.  
  
 **Lösung:** Um dieses Problem zu beheben:, deinstallieren Sie das NT Backup-Programm auf dem Server.  
  
### <a name="iis-does-not-own-port-80-000080-or-port-443-0000443"></a>Port 80 (0.0.0.0:80) oder Port 443 (0.0.0.0:443) sind nicht im Besitz von IIS  
 **Problem:**  Port 80 (0.0.0.0:80) oder Port 443 sind nicht im Besitz von Internetinformationsdienste (IIS). Diese Ports sind derzeit an andere Anwendungen gebunden.  
  
 **Auswirkung:**   Windows Server Essentials-Webanwendungen erfordern die Verwendung von Port 80 und Port 443, um die Dienste für Benutzer verfügbar machen. Wenn Sie einen anderen Prozess oder eine Anwendung bereits Port 80 oder Port 443 verwendet wird, können nicht die Windows Server Essentials-Webanwendungen ausgeführt. In einem solchen Fall stehen Benutzern Remotewebzugriff und andere Anwendungen nicht zur Verfügung.  
  
 **Lösung:**  Um dieses Problem zu beheben:, deinstallieren Sie die Anwendung, die bereits mithilfe von Port 80 oder Port 443 ist, oder diese Anwendung an einen anderen Port zuweisen.  
  
### <a name="the-default-website-is-not-running"></a>Die Standardwebsite ist nicht aktiv  
 **Problem:**  Die Standard-Website wird nicht in Ihrer Windows Server Essentials-Umgebung ausgeführt werden.  
  
 **Auswirkung:**   Windows Server Essentials-Webanwendungen erfordern die Verwendung der Standardwebsite. Wenn die Standardwebsite nicht aktiv ist, stehen Benutzern Remotewebzugriff und andere Anwendungen nicht zur Verfügung.  
  
 **Lösung:**  
  
##### <a name="to-start-the-default-website"></a>So starten Sie die Standardwebsite  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Sites**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Standardwebsite**, zeigen Sie auf **Website verwalten**, und klicken Sie dann auf **Starten**.  
  
### <a name="read-and-script-permissions-for-the-remote-virtual-directory-are-incorrect"></a>Die Lese- und Skriptberechtigungen für das virtuelle Verzeichnis "/Remote" sind ungültig  
 **Problem:**  Dem virtuellen Verzeichnis "/Remote" sind keine Lese- und Skriptberechtigungen zugewiesen.  
  
 **Auswirkung:**  Wenn die Lese- und Skriptberechtigungen für das virtuelle Verzeichnis "/Remote" ungültig sind, können Benutzer den Remotewebzugriff nicht verwenden. Wenn sie versuchen, die Remote Web Access verwenden, um das Internet zu durchsuchen, können sie den Fehler "HTTP-Fehler 403.1-verboten". auftreten.  
  
 **Lösung:**  
  
##### <a name="to-assign-read-and-script-permissions-to-the-remote-directory"></a>So weisen Sie dem Verzeichnis "/Remote" Lese- und Skriptberechtigungen zu  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Sites**.  
  
3.  Erweitern Sie **Standardwebsite** und dann **Remote**.  
  
4.  Doppelklicken Sie in der Ansicht **Features** auf **Handlerzuordnungen**.  
  
5.  Klicken Sie im Bereich **Aktionen** auf **Featureberechtigungen bearbeiten**.  
  
6.  Aktivieren Sie die Kontrollkästchen **Lesen** und **Skript**, und klicken Sie dann auf **OK**.  
  
### <a name="http-redirect-is-either-set-or-inherited-on-the-remote-virtual-directory"></a>Die HTTP-Umleitung wird im virtuellen Verzeichnis "/Remote" festgelegt oder vererbt  
 **Problem:**  Das Attribut für die HTTP-Umleitung wurde im virtuellen Verzeichnis "/Remote" unerwartet festgelegt oder vererbt.  
  
 **Auswirkung:**  Wenn das Attribut für die HTTP-Umleitung im virtuellen Verzeichnis "/Remote" festgelegt wurde, funktioniert Remote-Webarbeitsplatz möglicherweise nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-remove-the-http-redirect-attribute"></a>So entfernen Sie das Attribut "HTTP-Umleitung"  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Sites**.  
  
3.  Erweitern Sie **Standardwebsite** und dann **Remote**.  
  
4.  Doppelklicken Sie in der Ansicht **Features** auf **HTTP-Umleitung**.  
  
5.  Deaktivieren Sie das Kontrollkästchen **Anforderungen zu diesem Ziel umleiten**, und klicken Sie dann im Bereich **Aktionen** auf **Übernehmen**.  
  
### <a name="a-host-name-exists-for-port-80-on-the-default-website"></a>Es ist ein Hostname für Port 80 auf der Standardwebsite vorhanden  
 **Problem:**  Ein Hostname wird für Port 80 auf der Standardwebsite zugewiesen.  
  
 **Auswirkung:**  Wenn ein Hostname für Port 80 auf der Standardwebsite zugewiesen ist, können Sie mit einigen Windows Server Essentials-Webanwendungen herstellen nicht. Ein Hostname ist nicht erforderlich, und er wird in dieser Situation auch nicht empfohlen.  
  
 **Lösung:**  
  
##### <a name="to-clear-the-host-name-entry-for-port-80-on-the-default-website"></a>So löschen Sie den Hostnameneintrag für Port 80 auf der Standardwebsite  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Sites**.  
  
3.  Klicken Sie in der Ansicht **Features** mit der rechten Maustaste auf **Standardwebsite**, und klicken Sie dann auf **Bindungen**.  
  
4.  Wählen Sie **Sitebindungen** die Einstellung **HTTP für Port 80** aus, und klicken Sie dann auf **Bearbeiten**.  
  
5.  Löschen Sie unter **Sitebindung bearbeiten** den **Hostnameneintrag**, und klicken Sie dann auf **OK**.  
  
### <a name="backup-does-not-succeed-because-of-a-hidden-partition"></a>Sicherung ist aufgrund einer verborgenen Partition nicht erfolgreich  
 **Problem:**  Eine Partition, die keine NTFS-Partition ist, ist für eine Sicherung durch die Windows Server-Sicherung geplant.  
  
 **Auswirkung:**  Die Windows Server-Sicherung kann nur als NTFS formatierte Partitionen sichern.  
  
 **Lösung:**  Konfigurieren Sie die Windows Server-Sicherung nicht für die Sicherung nicht unterstützter Partitionen. Weitere Informationen finden Sie unter [Ereignis-IDs 12290 und 16387 werden protokolliert, wenn die Sicherung des Systemstatus auf einem Windows Server 2008-basierte Computer (Knowledge Base-Artikel 968128) schlägt fehl,](https://support.microsoft.com/kb/968128) (https://support.microsoft.com/kb/968128).  
  
### <a name="the-most-recent-backup-did-not-succeed"></a>Die aktuelle Sicherung war nicht erfolgreich  
 **Problem:**  Die aktuelle versuchte Sicherung wurde nicht erfolgreich abgeschlossen.  
  
 **Auswirkung:**  Der Sicherungsstatus für das System ist falsch.  
  
 **Lösung:**  Überprüfen Sie die Ereignis- und Sicherungsprotokolle auf Fehler während der letzten Sicherung.  
  
### <a name="the-startup-type-for-the-file-replication-service-is-not-set-to-automatic"></a>Der Starttyp für den Dateireplikationsdienst ist nicht auf "Automatisch" festgelegt  
 **Problem:**  Der Dateireplikationsdienst (FRS) wird möglicherweise nicht gestartet, wenn der Starttyp nicht auf den Standardwert "Automatisch" festgelegt ist.  
  
 **Auswirkung:**  Wenn der Dateireplikationsdienst nicht ausgeführt wird, kündigt der Domänencontroller möglicherweise seine Dienste nicht mehr an. Dies kann zu weiteren Problemen führen, z. B. zu Anmeldefehlern und Gruppenrichtlinienfehlern.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-file-replication-service-for-automatic-startup"></a>So konfigurieren Sie den Dateireplikationsdienst für den automatischen Start  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Dateireplikation**.  
  
3.  Wählen Sie für **Starttyp** die Option **Automatisch** aus, und klicken Sie dann auf **Übernehmen**.  
  
### <a name="the-file-replication-service-is-not-running"></a>Der Dateireplikationsdienst wird nicht ausgeführt  
 **Problem:**  Der Dateireplikationsdienst wird nicht ausgeführt.  
  
 **Auswirkung:**  Wenn der Dateireplikationsdienst nicht ausgeführt wird, kündigt der Domänencontroller möglicherweise seine Dienste nicht mehr an. Dieses Verhalten kann zu weiteren Problemen führen, z. B. zu Anmeldefehlern und Gruppenrichtlinienfehlern.  
  
 **Lösung:**  
  
##### <a name="to-start-the-file-replication-service"></a>So starten Sie den Dateireplikationsdienst  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Dateireplikationsdienst**.  
  
3.  Klicken Sie auf **Start**.  
  
### <a name="the-logon-account-for-the-file-replication-service-is-not-set-to-use-the-local-system-account"></a>Das Anmeldekonto für den Dateireplikationsdienst ist nicht auf die Verwendung des lokalen Systemkontos festgelegt  
 **Problem:**  Der Dateireplikationsdienst ist nicht für die Verwendung des lokalen Systemkontos als Standardanmeldekonto konfiguriert.  
  
 **Auswirkung:**  Wenn der Dateireplikationsdienst nicht "Lokales System" als Standardanmeldekonto verwendet, können Fehler in Bezug auf Berechtigungen auftreten. Diese Fehler können andere Fehler auslösen und letztendlich dazu führen, dass der Domänencontroller seine Dienste nicht mehr ankündigt.  
  
 **Lösung:**  
  
##### <a name="to-configure-local-system-as-the-default-logon-account-for-file-replication"></a>So konfigurieren Sie "Lokales System" als Standardanmeldekonto für die Dateireplikation  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Dateireplikation**.  
  
3.  Klicken Sie auf der Seite **Diensteigenschaften** auf die Registerkarte **Anmelden**.  
  
4.  Wählen Sie die Option **Lokales Systemkonto** aus, und klicken Sie dann auf **Übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-startup-type-for-the-dfs-replication-service-is-not-set-to-automatic"></a>Der Starttyp für den DFS-Replikationsdienst ist nicht auf "Automatisch" festgelegt  
 **Problem:**  Der DFS-Replikationsdienst wird möglicherweise nicht gestartet, wenn der Starttyp nicht auf den Standardwert "Automatisch" festgelegt ist.  
  
 **Auswirkung:**  Wenn der DFS-Replikationsdienst nicht ausgeführt wird, kündigt der Domänencontroller möglicherweise seine Dienste nicht mehr an. Dies kann zu weiteren Problemen führen, z. B. zu Anmeldefehlern und Gruppenrichtlinienfehlern.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-dfs-replication-service-for-automatic-startup"></a>So konfigurieren Sie den DFS-Replikationsdienst für den automatischen Start  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **DFS-Replikation**.  
  
3.  Wählen Sie für **Starttyp** die Option **Automatisch** aus, und klicken Sie dann auf **Übernehmen**.  
  
### <a name="the-dfs-replication-service-is-not-running"></a>Der DFS-Replikationsdienst wird nicht ausgeführt  
 **Problem:**  Der DFS-Replikationsdienst wird aktuell nicht ausgeführt.  
  
 **Auswirkung:**  Wenn der DFS-Replikationsdienst nicht ausgeführt wird, kündigt der Domänencontroller möglicherweise seine Dienste nicht mehr an. Dieses Verhalten kann zu weiteren Problemen führen, z. B. zu Anmeldefehlern und Gruppenrichtlinienfehlern.  
  
 **Lösung:**  
  
##### <a name="to-start-the-dfs-replication-service"></a>So starten Sie den DFS-Replikationsdienst  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **DFS-Replikation**.  
  
3.  Klicken Sie auf **Start**.  
  
### <a name="the-dfs-replication-service-is-not-is-not-set-to-use-the-local-system-account"></a>Der DFS-Replikationsdienst ist nicht auf die Verwendung des lokalen Systemkontos festgelegt  
 **Problem:**  Der DFS-Replikationsdienst ist nicht auf die Verwendung des lokalen Systemkontos als Standardanmeldekonto festgelegt.  
  
 **Auswirkung:**  Wenn der DFS-Replikationsdienst nicht "Lokales System" als Standardanmeldekonto verwendet, können Fehler in Bezug auf Berechtigungen auftreten. Diese Fehler können andere Fehler auslösen und letztendlich dazu führen, dass der Domänencontroller seine Dienste nicht mehr ankündigt.  
  
 **Lösung:**  
  
##### <a name="to-configure-dfs-replication-to-use-local-system-as-the-default-logon-account"></a>So konfigurieren Sie "Lokales System" als Standardanmeldekonto für die DFS-Replikation  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **DFS-Replikation**.  
  
3.  Klicken Sie auf der Seite **Diensteigenschaften** auf die Registerkarte **Anmelden**.  
  
4.  Wählen Sie die Option **Lokales Systemkonto** aus, und klicken Sie dann auf **Übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-set-to-use-the-local-system-account"></a>Der Windows Server Office 365-Integrationsdienst ist nicht auf die Verwendung des lokalen Systemkontos festgelegt  
 **Problem:**  Der Windows Server Office 365-Integrationsdienst ist nicht auf die Verwendung des lokalen Systemkontos als Standardanmeldekonto festgelegt.  
  
 **Auswirkung:**  Wenn der Windows Server Office 365-Integrationsdienst nicht "Lokales System" als das Standardanmeldekonto verwendet, funktionieren einige Features von Office 365 möglicherweise nicht ordnungsgemäß. Es können zudem Fehler in Bezug auf Berechtigungen auftreten.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-office-365-integration-service-to-use-local-system-as-the-default-logon-account"></a>So konfigurieren Sie "Lokales System" als Standardanmeldekonto für den Office 365-Integrationsdienst  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Windows Server Office 365-Integrationsdienst**.  
  
3.  Klicken Sie auf der Seite **Diensteigenschaften** auf die Registerkarte **Anmelden**.  
  
4.  Wählen Sie die Option **Lokales Systemkonto** aus, und klicken Sie dann auf **Übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-running"></a>Der Windows Server Office 365-Integrationsdienst wird nicht ausgeführt  
 **Problem:**  Der Windows Server Office 365-Integrationsdienst wird aktuell nicht ausgeführt.  
  
 **Auswirkung:**  Wenn der Windows Server Office 365-Integrationsdienst nicht ausgeführt wird, stehen die cloudbasierten Features von Office 365 nicht zur Verfügung.  
  
 **Lösung:**  
  
##### <a name="to-start-the-windows-server-office-365-integration-service"></a>So starten Sie den Windows Server Office 365-Integrationsdienst  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Windows Server Office 365-Integrationsdienst**.  
  
3.  Klicken Sie auf **Start**.  
  
### <a name="the-startup-type-for-the-windows-server-office-365-integration-service-is-not-set-to-automatic"></a>Der Starttyp für den Windows Server Office 365-Integrationsdienst ist nicht auf "Automatisch" festgelegt  
 **Problem:**  Der Windows Server Office 365-Integrationsdienst wird möglicherweise nicht gestartet, wenn der Starttyp nicht auf den Standardwert "Automatisch" festgelegt ist.  
  
 **Auswirkung:**  Wenn der Windows Server Office 365-Integrationsdienst nicht ausgeführt wird, stehen die cloudbasierten Features von Office 365 nicht zur Verfügung.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-office-365-integration-service-for-automatic-startup"></a>So konfigurieren Sie den Office 365-Integrationsdienst für den automatischen Start  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Windows Server Office 365-Integrationsdienst**.  
  
3.  Wählen Sie für **Starttyp** die Option **Automatisch** aus, und klicken Sie dann auf **Übernehmen**.  
  
### <a name="a-registry-value-is-missing-or-set-incorrectly"></a>Ein Registrierungswert fehlt oder wurde nicht ordnungsgemäß festgelegt  
 **Problem:**  Ein Registrierungswert unter "HKEY_LOCAL_MACHINE \Software\Microsoft\Rpc\RpcProxy" enthält entweder einen falschen Wert oder ist nicht vorhanden.  
  
 **Auswirkung:**  Wenn der RPCProxy-Registrierungsschlüssel falsch festgelegt ist, wird möglicherweise eine Fehlermeldung angezeigt, die der folgenden ähnelt: "Der Computer kann keine Verbindung mit dem Remotecomputer herstellen, da der Remotedesktop-Gatewayserver derzeit nicht verfügbar ist. Versuchen Sie später, die Verbindung wiederherzustellen, oder wenden Sie sich an den Netzwerkadministrator, um Hilfe zu erhalten."  
  
 **Lösung:**  
  
##### <a name="to-correct-the-registry-setting"></a>So korrigieren Sie die Registrierungseinstellung  
  
1.  Öffnen Sie den Registrierungs-Editor.  
  
2.  Navigieren Sie zu folgendem Registrierungsschlüssel:  
  
     HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy  
  
3.  Stellen Sie sicher, dass die Zeichenfolge, die mit dem Namen "Website" den Wert eines Datentyps der Default Web Site verfügt:  
  
    -   Wenn der Wert falsch ist, ändern Sie die Zeichenfolge so, dass der richtige Wert verwendet wird.  
  
    -   Wenn die Zeichenfolge nicht vorhanden ist, erstellen Sie eine neue Zeichenfolge, die mit dem Namen "Website", und legen Sie den Wert Default Web Site."  
  
### <a name="the-startup-type-for-the-block-level-backup-engine-service-is-not-set-to-manual"></a>Der Starttyp für das Blockebenen-Sicherungsmodul ist nicht auf "Manuell" festgelegt  
 **Problem:**  Das Blockebenen-Sicherungsmodul verwendet nicht den Standardstarttyp "Manuell".  
  
 **Auswirkung:**  Der Blockebenen-Sicherungsmoduldienst wird möglicherweise nicht gestartet, wenn der Starttyp auf nicht auf "Manuell" festgelegt ist. Dieses Problem: kann dazu führen, dass Aufträge von Windows Server-Sicherung fehlschlagen.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-for-manual-startup"></a>So konfigurieren Sie den Blockebenen-Sicherungsmoduldienst den manuellen Start  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Blockebenen-Sicherungsmoduldienst**.  
  
3.  Wählen Sie für **Starttyp** die Option **Manuell** aus, und klicken Sie dann auf **Übernehmen**.  
  
### <a name="the-logon-account-for-the-block-level-backup-engine-service-is-not-set-to-use-the-local-system-account"></a>Das Anmeldekonto für den Blockebenen-Sicherungsmoduldienst ist nicht auf die Verwendung des lokalen Systemkontos festgelegt  
 **Problem:**  Der Blockebenen-Sicherungsmoduldienst ist nicht auf die Verwendung des lokalen Systemkontos als Standardanmeldekonto festgelegt.  
  
 **Auswirkung:**  Wenn der Blockebenen-Sicherungsmoduldienst nicht "Lokales System" als Standardanmeldekonto verwendet, können Fehler in Bezug auf Berechtigungen auftreten. Diese Fehler können verhindern, dass Aufträge von der Windows Server-Sicherung erfolgreich abgeschlossen werden.  
  
 **Lösung:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-to-use-local-system-as-the-default-logon-account"></a>So konfigurieren Sie den Blockebenen-Sicherungsmoduldienst für die Verwendung von "Lokales System" als Standardanmeldekonto  
  
1.  Öffnen Sie die Konsole "Dienste".  
  
2.  Doppelklicken Sie in der Liste der Dienste auf **Blockebenen-Sicherungsmoduldienst**.  
  
3.  Klicken Sie auf der Seite **Diensteigenschaften** auf die Registerkarte **Anmelden**.  
  
4.  Wählen Sie die Option **Lokales Systemkonto** aus, und klicken Sie dann auf **Übernehmen**.  
  
5.  Starten Sie den Dienst neu.  
  
### <a name="the-common-name-on-the-certificate-that-is-bound-to-the-wss-certificate-web-service-website-does-not-match-the-server-name"></a>Der allgemeine Name für das Zertifikat, das an die Website des Webdiensts für WSS-Zertifikate gebunden ist, stimmt nicht mit dem Servernamen überein  
 **Problem:**  Ein ungültiges Zertifikat ist an die Website des Webdiensts für WSS-Zertifikate in IIS gebunden. Der allgemeine Name für dieses Zertifikat stimmt nicht mit dem Servernamen überein.  
  
 **Auswirkung:**  Wenn Sie ein ungültiges Zertifikate an die Website des Webdiensts für WSS-Zertifikate binden, funktioniert der Verbindungs-Assistent möglicherweise nicht ordnungsgemäß.  
  
 **Lösung:**  
  
##### <a name="to-configure-a-valid-certificate-for-the-wss-certificate-web-service"></a>So konfigurieren Sie ein gültiges Zertifikat für den Webdienst für WSS-Zertifikate  
  
1.  Öffnen Sie auf dem Server den Internetinformationsdienste-Manager (IIS)  
  
2.  Erweitern Sie im IIS-Manager den Namen des Servers, und klicken Sie dann auf **Sites**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Webdienst für WSS-Zertifikate**, und klicken Sie dann auf **Bindungen bearbeiten**.  
  
4.  Klicken Sie in **Sitebindungen** auf **HTTPS**, und klicken Sie dann auf **Bearbeiten**.  
  
5.  Wählen Sie in **Sitebindung bearbeiten** für **SSL-Zertifikat** das Zertifikat aus, das denselben Namen wie der Server aufweist.  
  
6.  Wenn mehrere Zertifikateinträge denselben Namen wie der Server aufweisen, klicken Sie auf **Anzeigen**, um herauszufinden, welches Zertifikat gültig ist, und wählen Sie dann das entsprechende Zertifikat aus.  
  
### <a name="there-appears-to-be-a-problem-with-the-certificate-binding-for-the-remote-desktop-gateway-service"></a>Mit der Zertifikatbindung für den Remotedesktopgateway-Dienst scheint ein Problem zu bestehen  
 **Problem:**  Das Zertifikat für den Remotedesktopgateway-Dienst scheint nicht ordnungsgemäß gebunden zu sein.  
  
 **Auswirkung:**  Wenn das Zertifikat für den Remotedesktopgateway-Dienst nicht richtig konfiguriert ist, können Benutzer keine Verbindung mit Remotewebzugriff herstellen.  
  
 **Lösung:**  
  
##### <a name="to-fix-the-binding-for-the-remote-desktop-gateway-service"></a>So korrigieren Sie die Bindung für den Remotedesktopgateway-Dienst  
  
-   Öffnen Sie eine Eingabeaufforderung als Administrator, und geben Sie den folgende Befehle ein:  
  
    ```  
    REG ADD HKLM\SYSTEM\CurrentControlSet\services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443  /v DefaultFlags /t REG_DWORD /d 1 /f  
    net stop tsgateway  
    net start tsgateway  
    ```  
  
     Weitere Informationen finden Sie unter [so verwalten Sie den Remotedesktopgateway-Diensts in Windows Server Essentials (Knowledge Base-Artikel 2472211)](https://support.microsoft.com/kb/2472211) (https://support.microsoft.com/kb/2472211).
