---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: Anhang für vereinfachte Verwaltung
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 3cef76347bcd5a341b96a71fed58d2fe0085a46c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953406"
---
# <a name="simplified-administration-appendix"></a>Anhang für vereinfachte Verwaltung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

-   [Dialog Server-Manager "Server hinzufügen" (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)

-   [Status des Remote Servers Server-Manager](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)

-   [Laden von Windows PowerShell-Modulen](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)

-   [Hotfixes für die RID-Ausstellung für vorherige Betriebssysteme](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)

-   [Ntdsutil.exe Installation von Medien Änderungen](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)

## <a name="server-manager-add-servers-dialog-active-directory"></a><a name="BKMK_AddServers"></a>Dialog Server-Manager "Server hinzufügen" (Active Directory)

Im Dialogfeld **Server hinzufügen können Sie** Active Directory nach Servern, nach Betriebssystem, unter Verwendung von Platzhaltern und nach Standort suchen. Im Dialogfeld können DNS-Abfragen auch mit einem voll qualifizierten Domänen Namen oder Präfix Namen verwendet werden. Diese Suchvorgänge verwenden systemeigene DNS-und LDAP-Protokolle, die über .NET implementiert werden, nicht AD Windows PowerShell für das AD-Verwaltungs Gateway über SOAP. Dies bedeutet, dass die von Server-Manager verbundenen Domänen Controller sogar Windows Server 2003 ausführen können. Sie können auch eine Datei mit Servernamen zu Bereitstellungs Zwecken importieren.

Bei der Active Directory Suche werden die folgenden LDAP-Filter verwendet:

```
(&(ObjectCategory=computer)

(&(ObjectCategory=computer)(cn=dc*)(OperatingSystemVersion=6.2*))

(&(ObjectCategory=computer)(OperatingSystemVersion=6.1*))

(&(ObjectCategory=computer)(OperatingSystemVersion=6.0*))

(&(ObjectCategory=computer)(|(OperatingSystemVersion=5.2*)(OperatingSystemVersion=5.1*)))

```

Die Active Directory Suche gibt die folgenden Attribute zurück:

```
( dnsHostName )( operatingSystem )( cn )

```

## <a name="server-manager-remote-server-status"></a><a name="BKMK_ServerMgrStatus"></a>Status des Remote Servers Server-Manager
Server-Manager testet die Barrierefreiheit des Remote Servers mithilfe des Adress Routing Protokolls. Alle Server, die nicht auf ARP-Anforderungen reagieren, werden nicht aufgeführt, auch wenn Sie sich im Pool befinden.

Wenn ARP antwortet, werden DCOM-und WMI-Verbindungen zum Server hergestellt, um Statusinformationen zurückzugeben. Wenn RPC, DCOM und WMI nicht erreichbar sind, kann der Server von Server-Manager nicht vollständig verwaltet werden.

## <a name="windows-powershell-module-loading"></a><a name="BKMK_PSLoadModule"></a>Laden von Windows PowerShell-Modulen
Windows PowerShell 3,0 implementiert dynamisches Laden von Modulen. Die Verwendung des **Import-Module-** Cmdlets ist in der Regel nicht mehr erforderlich. Stattdessen wird das Modul durch einfaches Aufrufen des Cmdlets, des Alias oder der Funktion automatisch geladen.

Verwenden Sie das Cmdlet **Get-Module** , um geladene Module anzuzeigen.

```
Get-Module

```

![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)

Um alle installierten Module mit ihren exportierten Funktionen und Cmdlets anzuzeigen, verwenden Sie Folgendes:

```
Get-Module -ListAvailable

```

Der Hauptgrund für die Verwendung des **Import-Module-** Befehls ist, wenn Sie auf das virtuelle Windows PowerShell-Laufwerk "AD:" zugreifen müssen und das Modul noch nicht geladen wurde. Verwenden Sie beispielsweise die folgenden Befehle:

```
import-module activedirectory
cd ad:
dir

```

## <a name="rid-issuance-hotfixes-for-previous-operating-systems"></a><a name="BKMK_Rid"></a>Hotfixes für die RID-Ausstellung für vorherige Betriebssysteme
Weitere Informationen finden [Sie unter ein Update ist verfügbar, um zu viel Verbrauch des globalen RID-Pools auf einem Domänen Controller mit Windows Server 2008 R2 zu erkennen und zu vermeiden](https://support.microsoft.com/kb/2618669).

## <a name="ntdsutilexe-install-from-media-changes"></a><a name="BKMK_IFM"></a>Ntdsutil.exe Installation von Medien Änderungen
Windows Server 2012 fügt dem Befehlszeilen Tool "Ntdsutil.exe" für das **IFM-Menü (IFM-Medien Erstellung)** zwei zusätzliche Optionen hinzu. Diese ermöglichen es Ihnen, IFM-Speicher zu erstellen, ohne zuvor eine Offline-decofragmentierung der exportierten NTDS auszuführen. DIT-Datenbankdatei. Wenn der Speicherplatz kein Premium-Speicherplatz ist, spart das Erstellen der IFM Zeit.

In der folgenden Tabelle werden die zwei neuen Menü Elemente beschrieben:

|Menübefehl|Erklärung|
|--|--|
|Vollständige NoDebug-% s erstellen|Erstellen Sie IFM-Medien ohne die Fragmentierung für einen vollständigen AD DC oder eine AD/LDS-Instanz in den Ordner "% s".|
|Create SYSVOL Full Node Frag% s|Erstellen von IFM-Medien mit SYSVOL und ohne decofragmentierung eines vollständigen AD-Domänen Controllers in den Ordner "% s"|

![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)

![Vereinfachte Verwaltung](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)
