---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: "Anhangfür vereinfachte Verwaltung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5de7431d0f3fe9a078432b11a63ce996d3abe447
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="simplified-administration-appendix"></a>Anhangfür vereinfachte Verwaltung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

  
-   [Server-Manager hinzufügen Dialogfeld Server (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)  
  
-   [Server-Manager Remote-Serverstatus](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)  
  
-   [Windows PowerShell-Modul laden](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)  
  
-   [RID-Ausstellung Hotfixes für frühere Betriebssysteme](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)  
  
-   [Installieren Sie Ntdsutil.exe from Media Changes](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)  
  
## <a name="BKMK_AddServers"></a>Server-Manager hinzufügen Dialogfeld Server (Active Directory)  

Die **Hinzufügen von Servern** Dialogfeld ermöglicht das Suchen in Active Directory für Server, vom Betriebssystem, mit Platzhaltern, und nach Standort. Im Dialogfeld können auch mithilfe von DNS-Abfragen nach vollqualifizierten Domänennamen oder Präfixnamen an. Diese suchen verwenden systemeigene DNS- und LDAP-Protokolle implementiert über .NET nicht Active Directory Windows PowerShell für AD-Management-Gateway über SOAP - bedeutet, dass der Domänencontroller kontaktiert vom Server-Manager auch Windows Server2003 ausgeführt werden können. Sie können auch eine Datei mit dem Namen der Server für die Bereitstellung importieren.  
  
Die Active Directory-Suche verwendet die folgenden LDAP-Filter:  
  
```  
(&(ObjectCategory=computer)  
  
(&(ObjectCategory=computer)(cn=dc*)(OperatingSystemVersion=6.2*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.1*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.0*))  
  
(&(ObjectCategory=computer)(|(OperatingSystemVersion=5.2*)(OperatingSystemVersion=5.1*)))  
  
```  
  
Die Active Directory-Suche gibt die folgenden Attribute:  
  
```  
( dnsHostName )( operatingSystem )( cn )  
  
```  
  
## <a name="BKMK_ServerMgrStatus"></a>Server-Manager Remote-Serverstatus  
Server-Manager überprüft Remoteserver Eingabehilfen Address Routing-Protokoll verwenden. Alle Server reagiert nicht auf ARP-Anfragen werden nicht aufgelistet, auch wenn sie im Pool sind.  
  
ARP reagiert, sind dann DCOM- und WMI-Verbindungen mit dem Server versucht, Statusinformationen zurückzugeben. Wenn RPC-, DCOM- und WMI nicht erreichbar sind, kann nicht in Server-Manager vollständig den Server verwalten.  
  
## <a name="BKMK_PSLoadModule"></a>Windows PowerShell-Modul laden  
Windows PowerShell 3.0 implementiert dynamisches Modul geladen. Mithilfe der **Import-Module** Cmdlet ist in der Regel nicht mehr erforderlich. In diesem Fall lädt der Aufruf einfach das Cmdlet, den Alias oder die Funktion automatisch das Modul.  
  
Verwenden Sie zum Anzeigen der geladenen Module der **Get-Module** Cmdlet.  
  
```  
Get-Module  
  
```  
  
![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)  
  
Um alle installierten Module mit exportierten Funktionen und Cmdlets anzuzeigen, verwenden Sie Folgendes:  
  
```  
Get-Module -ListAvailable  
  
```  
  
Die wichtigsten Groß-/Kleinschreibung für die Verwendung der **Import-Module** Befehl ist, wenn Sie den Zugriff auf die "AD:" virtuelle Windows PowerShell-Laufwerk und sonst nichts bereits das Modul geladen. Verwenden beispielsweise die folgenden Befehle ein:  
  
```  
import-module activedirectory  
cd ad:  
dir  
  
```  
  
## <a name="BKMK_Rid"></a>RID-Ausstellung Hotfixes für frühere Betriebssysteme  
Weitere Informationen finden Sie unter [ist ein Update verfügbar ist, zu erkennen und zu verhindern, dass zu viel Verbrauch des globalen RID-Pools auf einem Domänencontroller, auf denen Windows Server2008 R2 ausgeführt wird](https://support.microsoft.com/kb/2618669).  
  
## <a name="BKMK_IFM"></a>Ntdsutil.exe Install from Media Changes  
Windows Server2012 fügt zwei zusätzliche Optionen für das Befehlszeilenprogramm "Ntdsutil.exe" für die **Medium (IFM-Medien erstellen)** Menü. Damit können Sie IFM-Speicher zu erstellen, ohne zunächst eine Offlinedefragmentierung der die exportierten NTDS.DIT-Datenbankdatei. Wenn Speicherplatz keine Premium ist, speichert diese Zeit mit der Erstellung der IFM.  
  
In der folgende Tabelle werden die beiden neuen Menüelemente beschrieben:  
  
|||  
|-|-|  
|Menüelement|Erläuterung|  
|Erstellen Sie vollständige NoDefrag %s|Erstellen von IFM-Medien ohne Defragmentierung für einen vollständigen Active Directory-Domänencontroller oder AD LDS /-Instanz in Ordner %s|  
|Erstellen der Sysvol-Full NoDefrag %s|Erstellen von IFM-Medien mit SYSVOL und ohne Defragmentieren für einen vollständigen Active Directory-Domänencontroller in Ordner %s|  
  
![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)  
  
![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)  
  


