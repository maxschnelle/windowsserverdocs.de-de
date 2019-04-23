---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: Anhang für vereinfachte Verwaltung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 36cdacec27e64586c359146b858a9d68750e5026
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858261"
---
# <a name="simplified-administration-appendix"></a>Anhang für vereinfachte Verwaltung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
-   [Server-Manager hinzufügen, Dialogfeld "Server" (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)  
  
-   [Server-Manager Remote-Serverstatus](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)  
  
-   [Windows PowerShell-Modul laden](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)  
  
-   [RID-Ausstellung Hotfixes für frühere Betriebssysteme](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)  
  
-   [Ntdsutil.exe Install from Media Changes](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)  
  
## <a name="BKMK_AddServers"></a>Server-Manager hinzufügen, Dialogfeld "Server" (Active Directory)  

Die **Hinzufügen von Servern** Dialogfeld ermöglicht das Durchsuchen von Active Directory bei Servern, vom Betriebssystem mithilfe von Platzhaltern, und nach Standort. Im Dialogfeld können auch mithilfe von DNS-Abfragen durch vollständig qualifizierten Domänennamen oder den Präfixnamen. Diese Suchvorgänge verwenden systemeigene DNS- und LDAP-Protokolle implementiert, die über .NET nicht AD Windows PowerShell für das AD Management Gateway, über SOAP - Dies bedeutet, dass die Domänencontroller kontaktiert vom Server-Manager auch Windows Server 2003 ausgeführt werden können. Sie können auch eine Datei mit dem Namen der Server für die Bereitstellung zu importieren.  
  
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
Server-Manager überprüft die remote-Server-Zugriff, die über Address Routing Protocol. Alle Server reagiert nicht auf ARP-Anfragen sind nicht aufgeführt, auch wenn sie im Pool sind.  
  
Wenn ARP antwortet, klicken Sie dann DCOM- und WMI-Verbindungen mit dem Server erfolgen Statusinformationen zurückgeben. Wenn der RPC-, DCOM- und WMI nicht erreichbar sind, kann nicht den Server von Server-Manager vollständig verwalten.  
  
## <a name="BKMK_PSLoadModule"></a>Windows PowerShell-Modul laden  
Windows PowerShell 3.0 implementiert, dynamisches Modul geladen wird. Mithilfe der **Import-Module** Cmdlet ist in der Regel nicht mehr erforderlich; stattdessen wird das Modul einfach im Aufrufen der Cmdlets, Alias oder Funktion automatisch geladen.  
  
Um geladenen Module anzuzeigen, verwenden die **Get-Module** Cmdlet.  
  
```  
Get-Module  
  
```  
  
![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)  
  
Um alle installierten Module mit ihren exportierten Funktionen und Cmdlets anzuzeigen, verwenden Sie:  
  
```  
Get-Module -ListAvailable  
  
```  
  
Die wichtigsten Argumente für die Verwendung der **Import-Module** Befehl ist, wenn Sie den Zugriff auf die "AD:" Windows PowerShell-Laufwerk und nichts anderes hat bereits das Modul geladen. Verwenden Sie beispielsweise die folgenden Befehle ein:  
  
```  
import-module activedirectory  
cd ad:  
dir  
  
```  
  
## <a name="BKMK_Rid"></a>RID-Ausstellung Hotfixes für frühere Betriebssysteme  
Finden Sie unter [ein Update ist verfügbar, um zu erkennen und zu verhindern, dass zu viel Ressourcenverbrauch des globalen RID-Pools auf einem Domänencontroller, auf denen Windows Server 2008 R2 ausgeführt wird](https://support.microsoft.com/kb/2618669).  
  
## <a name="BKMK_IFM"></a>Ntdsutil.exe Install from Media Changes  
Windows Server 2012 fügt zwei zusätzliche Optionen für das Befehlszeilenprogramm "Ntdsutil.exe" für die **IFM (IFM-Medien-Erstellung)** Menü. Diese können Sie IFM-Speicher zu erstellen, ohne zunächst eine Offlinedefragmentierung der exportierten Datei NTDS ausgeführt. DIT-Datei. Wenn Speicherplatz nicht Premium ist, speichert dieser Zeit mit der Erstellung der IFM.  
  
Die folgende Tabelle beschreibt die zwei neuen Menüelemente an:  
  
|||  
|-|-|  
|Menüelement|Erläuterung|  
|Erstellen Sie vollständige NoDefrag %s|Erstellen von IFM-Medien ohne für eine vollständige Active Directory-Domänencontroller oder AD/LDS-Instanz in den Ordner "%s" Defragmentierung|  
|Erstellen der Sysvol-voll-NoDefrag %s|Erstellen von IFM-Medien mit SYSVOL und ohne Defragmentieren für einen vollständigen AD-DC in Ordner "%s"|  
  
![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)  
  
![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)  
  


