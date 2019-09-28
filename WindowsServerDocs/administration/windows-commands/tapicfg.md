---
title: tapicfg
description: Erfahren Sie, wie Sie eine TAPI-Anwendungsverzeichnis Partition verwalten.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0e642ce-5d98-4edb-9a65-1dff09aef4e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5e9e113f0679034a4cd135cad6e7c546dc59c5c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383666"
---
# <a name="tapicfg"></a>tapicfg

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt, entfernt oder zeigt eine TAPI-Anwendungsverzeichnis Partition an oder legt eine standardmäßige TAPI-Anwendungsverzeichnis Partition fest. TAPI 3,1-Clients können die Informationen in dieser Anwendungsverzeichnis Partition mit dem Verzeichnisdienst-Serverlocatorpunkt-Dienst verwenden, um TAPI-Verzeichnisse zu suchen und mit Ihnen zu kommunizieren. Sie können auch " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen, die TAPI-Clients ermöglichen, die TAPI-Anwendungsverzeichnis Partitionen in einer Domäne effizient zu finden. Weitere Informationen finden Sie unter "Hinweise". Um die Befehlssyntax anzuzeigen, klicken Sie auf einen Befehl. 
-   [tapicfg-Installation](#BKMK_install)
-   [tapicfg entfernen](#BKMK_remove)
-   [tapicfg publishscp](#BKMK_publishscp)
-   [tapicfg removescp](#BKMK_removescp)
-   [tapicfg anzeigen](#BKMK_show)
-   [tapicfg MakeDefault](#BKMK_makedefault)

## <a name="BKMK_install"></a>tapicfg-Installation
Erstellt eine TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg install /directory:<PartitionName> [/server:<DCName>] [/forcedefault]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Installieren von/Directory: \<partitionname >|Erforderlich. Gibt den DNS-Namen der zu erstellenden TAPI-Anwendungsverzeichnis Partition an. Dieser Name muss ein voll qualifizierter Domänen Name sein.|
|/Server \<dcname >|Gibt den DNS-Namen des Domänen Controllers an, auf dem die TAPI-Anwendungsverzeichnis Partition erstellt wird. Wenn der Domänen Controller Name nicht angegeben ist, wird der Name des lokalen Computers verwendet.|
|/forcedefault|Gibt an, dass dieses Verzeichnis die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne ist. Es können mehrere TAPI-Anwendungsverzeichnis Partitionen in einer Domäne vorhanden sein.<br /><br />Wenn dieses Verzeichnis die erste TAPI-Anwendungsverzeichnis Partition ist, die in der Domäne erstellt wurde, wird es automatisch als Standard festgelegt, unabhängig davon, ob Sie die Option **/forcedefault** verwenden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_remove"></a>tapicfg entfernen
Entfernt eine TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg remove /directory:<PartitionName>
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Remove/Directory: \<partitionname >|Erforderlich. Gibt den DNS-Namen der zu entfernenden TAPI-Anwendungsverzeichnis Partition an. Beachten Sie, dass dieser Name ein voll qualifizierter Domänen Name sein muss.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_publishscp"></a>tapicfg publishscp
Erstellt einen Dienst Verbindungspunkt zum Veröffentlichen einer TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg publishscp /directory:<PartitionName> [/domain:<DomainName>] [/forcedefault]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|publishscp/Directory: \<partitionname >|Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, die vom Dienst Verbindungspunkt veröffentlicht wird.|
|/Domain: \<domainname >|Gibt den DNS-Namen der Domäne an, in der der Dienst Verbindungspunkt erstellt wird. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/forcedefault|Gibt an, dass dieses Verzeichnis die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne ist. Es können mehrere TAPI-Anwendungsverzeichnis Partitionen in einer Domäne vorhanden sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_removescp"></a>tapicfg removescp
Entfernt einen Dienst Verbindungspunkt für eine TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg removescp /directory:<PartitionName> [/domain:<DomainName>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|removescp/Directory: \<partitionname >|Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, für die ein Dienst Verbindungspunkt entfernt wird.|
|/Domain \<domainname >|Gibt den DNS-Namen der Domäne an, aus der der Dienst Verbindungspunkt entfernt wird. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_show"></a>tapicfg anzeigen
Zeigt die Namen und Speicherorte der TAPI-Anwendungsverzeichnis Partitionen in der Domäne an.

### <a name="syntax"></a>Syntax
```
tapicfg show [/defaultonly][ /domain:<DomainName>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/defaultonly|Zeigt die Namen und Speicherorte der standardmäßigen TAPI-Anwendungsverzeichnis Partition in der Domäne an.|
|/Domain \<domainname >|Gibt den DNS-Namen der Domäne an, für die die TAPI-Anwendungsverzeichnis Partitionen angezeigt werden. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_makedefault"></a>tapicfg MakeDefault
Legt die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne fest.

### <a name="syntax"></a>Syntax
```
tapicfg makedefault /directory:<PartitionName> [/domain:<DomainName>]  
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|MakeDefault/Directory: \<partitionname >|Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, die als Standard Partition für die Domäne festgelegt ist. Beachten Sie, dass dieser Name ein voll qualifizierter Domänen Name sein muss. Gibt den DNS-Namen der Domäne an, für die die TAPI-Anwendungsverzeichnis Partition als Standard festgelegt ist. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
Sie müssen Mitglied der Gruppe "Organisations-Admins" in Active Directory sein, um entweder die Installation von " **tapicfg** " (zum Erstellen einer TAPI-Anwendungsverzeichnis Partition) oder " **tapicfg Remove** " (zum Entfernen einer TAPI-Anwendungsverzeichnis Partition) auszuführen.

Dieses Befehlszeilen Tool kann auf einem beliebigen Computer ausgeführt werden, der Mitglied der Domäne ist.

Vom Benutzer bereitgestellter Text (z. b. die Namen von TAPI-Anwendungsverzeichnis Partitionen, Servern und Domänen) mit internationalen oder Unicode-Zeichen werden nur ordnungsgemäß angezeigt, wenn entsprechende Schriftarten und Sprachunterstützung installiert ist.

Sie können weiterhin Internet Locator Service (ILS)-Server in Ihrer Organisation verwenden, wenn für die Unterstützung bestimmter Anwendungen ILS benötigt wird, da TAPI-Clients unter Windows XP oder Windows Server 2003 Betriebssystem entweder ILS-Server oder TAPI-Anwendungen Abfragen können. Verzeichnis Partitionen.

Sie können " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen. Wenn die TAPI-Anwendungsverzeichnis Partition aus irgendeinem Grund umbenannt wird (z. b. Wenn Sie die Domäne umbenennen, in der Sie sich befindet), müssen Sie den vorhandenen Dienst Verbindungspunkt entfernen und einen neuen erstellen, der den neuen DNS-Namen des TAPI-Anwendungs Verzeichnisses enthält. die Partition, die veröffentlicht werden soll. Andernfalls sind TAPI-Clients nicht in der Lage, die TAPI-Anwendungsverzeichnis Partition zu finden und darauf zuzugreifen. Sie können einen Dienst Verbindungspunkt auch zu Wartungs-oder Sicherheitszwecken entfernen (z. b. Wenn Sie TAPI-Daten nicht für eine bestimmte TAPI-Anwendungsverzeichnis Partition verfügbar machen möchten).

## <a name="examples"></a>Beispiele
Wenn Sie eine TAPI-Anwendungsverzeichnis Partition namens tapifiction.testDom.Microsoft.com auf einem Server mit dem Namen testdc.testDom.Microsoft.com erstellen und diese dann als standardmäßige TAPI-Anwendungsverzeichnis Partition für die neue Domäne festlegen möchten, geben Sie Folgendes ein:
```
tapicfg install /directory:tapifiction.testdom.microsoft.com /server:testdc.testdom.microsoft.com /forcedefault
```
Wenn Sie den Namen der standardmäßigen TAPI-Anwendungsverzeichnis Partition für die neue Domäne anzeigen möchten, geben Sie Folgendes ein:
```
tapicfg show /defaultonly
```
## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
