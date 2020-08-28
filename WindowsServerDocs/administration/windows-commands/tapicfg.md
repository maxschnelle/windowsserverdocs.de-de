---
title: tapicfg
description: Erfahren Sie, wie Sie eine TAPI-Anwendungsverzeichnis Partition verwalten.
ms.topic: reference
ms.assetid: c0e642ce-5d98-4edb-9a65-1dff09aef4e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: a6f340713e0510b2766124c7a0106f5f9ff9aa8c
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027188"
---
# <a name="tapicfg"></a>tapicfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt, entfernt oder zeigt eine TAPI-Anwendungsverzeichnis Partition an oder legt eine standardmäßige TAPI-Anwendungsverzeichnis Partition fest. TAPI 3,1-Clients können die Informationen in dieser Anwendungsverzeichnis Partition mit dem Verzeichnisdienst-Serverlocatorpunkt-Dienst verwenden, um TAPI-Verzeichnisse zu suchen und mit Ihnen zu kommunizieren. Sie können auch " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen, die TAPI-Clients ermöglichen, die TAPI-Anwendungsverzeichnis Partitionen in einer Domäne effizient zu finden. Weitere Informationen finden Sie unter "Hinweise". Um die Befehlssyntax anzuzeigen, klicken Sie auf einen Befehl.
-   [tapicfg-Installation](#BKMK_install)
-   [tapicfg entfernen](#BKMK_remove)
-   [tapicfg publishscp](#BKMK_publishscp)
-   [tapicfg removescp](#BKMK_removescp)
-   [tapicfg anzeigen](#BKMK_show)
-   [tapicfg MakeDefault](#BKMK_makedefault)

## <a name="tapicfg-install"></a><a name="BKMK_install"></a>tapicfg-Installation
Erstellt eine TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg install /directory:<PartitionName> [/server:<DCName>] [/forcedefault]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Installieren von/Directory:\<PartitionName>|Erforderlich. Gibt den DNS-Namen der zu erstellenden TAPI-Anwendungsverzeichnis Partition an. Dieser Name muss ein voll qualifizierter Domänen Name sein.|
|/Server \<DCName>|Gibt den DNS-Namen des Domänen Controllers an, auf dem die TAPI-Anwendungsverzeichnis Partition erstellt wird. Wenn der Domänen Controller Name nicht angegeben ist, wird der Name des lokalen Computers verwendet.|
|/forcedefault|Gibt an, dass dieses Verzeichnis die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne ist. Es können mehrere TAPI-Anwendungsverzeichnis Partitionen in einer Domäne vorhanden sein.<p>Wenn dieses Verzeichnis die erste TAPI-Anwendungsverzeichnis Partition ist, die in der Domäne erstellt wurde, wird es automatisch als Standard festgelegt, unabhängig davon, ob Sie die Option **/forcedefault** verwenden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="tapicfg-remove"></a><a name="BKMK_remove"></a>tapicfg entfernen
Entfernt eine TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg remove /directory:<PartitionName>
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Directory entfernen:\<PartitionName>|Erforderlich. Gibt den DNS-Namen der zu entfernenden TAPI-Anwendungsverzeichnis Partition an. Beachten Sie, dass dieser Name ein voll qualifizierter Domänen Name sein muss.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="tapicfg-publishscp"></a><a name="BKMK_publishscp"></a>tapicfg publishscp
Erstellt einen Dienst Verbindungspunkt zum Veröffentlichen einer TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg publishscp /directory:<PartitionName> [/domain:<DomainName>] [/forcedefault]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|publishscp/Directory:\<PartitionName>|Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, die vom Dienst Verbindungspunkt veröffentlicht wird.|
|/Domain\<DomainName>|Gibt den DNS-Namen der Domäne an, in der der Dienst Verbindungspunkt erstellt wird. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/forcedefault|Gibt an, dass dieses Verzeichnis die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne ist. Es können mehrere TAPI-Anwendungsverzeichnis Partitionen in einer Domäne vorhanden sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="tapicfg-removescp"></a><a name="BKMK_removescp"></a>tapicfg removescp
Entfernt einen Dienst Verbindungspunkt für eine TAPI-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax
```
tapicfg removescp /directory:<PartitionName> [/domain:<DomainName>]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|removescp/Directory:\<PartitionName>|Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, für die ein Dienst Verbindungspunkt entfernt wird.|
|/Domain \<DomainName>|Gibt den DNS-Namen der Domäne an, aus der der Dienst Verbindungspunkt entfernt wird. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="tapicfg-show"></a><a name="BKMK_show"></a>tapicfg anzeigen
Zeigt die Namen und Speicherorte der TAPI-Anwendungsverzeichnis Partitionen in der Domäne an.

### <a name="syntax"></a>Syntax
```
tapicfg show [/defaultonly][ /domain:<DomainName>]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/defaultonly|Zeigt die Namen und Speicherorte der standardmäßigen TAPI-Anwendungsverzeichnis Partition in der Domäne an.|
|/Domain \<DomainName>|Gibt den DNS-Namen der Domäne an, für die die TAPI-Anwendungsverzeichnis Partitionen angezeigt werden. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="tapicfg-makedefault"></a><a name="BKMK_makedefault"></a>tapicfg MakeDefault
Legt die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne fest.

### <a name="syntax"></a>Syntax
```
tapicfg makedefault /directory:<PartitionName> [/domain:<DomainName>]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|MakeDefault/Directory:\<PartitionName>|Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, die als Standard Partition für die Domäne festgelegt ist. Beachten Sie, dass dieser Name ein voll qualifizierter Domänen Name sein muss. Gibt den DNS-Namen der Domäne an, für die die TAPI-Anwendungsverzeichnis Partition als Standard festgelegt ist. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen
Sie müssen Mitglied der Gruppe "Organisations-Admins" in Active Directory sein, um entweder die Installation von " **tapicfg** " (zum Erstellen einer TAPI-Anwendungsverzeichnis Partition) oder " **tapicfg Remove** " (zum Entfernen einer TAPI-Anwendungsverzeichnis Partition) auszuführen.

Dieses Befehlszeilen Tool kann auf einem beliebigen Computer ausgeführt werden, der Mitglied der Domäne ist.

Vom Benutzer bereitgestellter Text (z. b. die Namen von TAPI-Anwendungsverzeichnis Partitionen, Servern und Domänen) mit internationalen oder Unicode-Zeichen werden nur ordnungsgemäß angezeigt, wenn entsprechende Schriftarten und Sprachunterstützung installiert ist.

Sie können weiterhin Internet Locator Service (ILS)-Server in Ihrer Organisation verwenden, wenn ILS zur Unterstützung bestimmter Anwendungen benötigt wird, da TAPI-Clients unter Windows XP oder Windows Server 2003 Betriebssystem entweder ILS-Server oder TAPI-Anwendungsverzeichnis Partitionen Abfragen können.

Sie können " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen. Wenn die TAPI-Anwendungsverzeichnis Partition aus irgendeinem Grund umbenannt wird (z. b. Wenn Sie die Domäne umbenennen, in der Sie sich befindet), müssen Sie den vorhandenen Dienst Verbindungspunkt entfernen und einen neuen erstellen, der den neuen DNS-Namen der zu veröffentlichenden TAPI-Anwendungsverzeichnis Partition enthält. Andernfalls sind TAPI-Clients nicht in der Lage, die TAPI-Anwendungsverzeichnis Partition zu finden und darauf zuzugreifen. Sie können einen Dienst Verbindungspunkt auch zu Wartungs-oder Sicherheitszwecken entfernen (z. b. Wenn Sie TAPI-Daten nicht für eine bestimmte TAPI-Anwendungsverzeichnis Partition verfügbar machen möchten).

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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
