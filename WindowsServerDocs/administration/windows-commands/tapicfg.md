---
title: tapicfg
description: Erfahren Sie, wie eine TAPI-Anwendungsverzeichnispartition zu verwalten.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6e89b1e3d7638fbcbe0140658d2d2a9af1ccd852
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886511"
---
# <a name="tapicfg"></a>tapicfg

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erstellt, entfernt, oder zeigt eine TAPI-Anwendungsverzeichnispartition, oder legt eine standardanwendungsverzeichnispartition TAPI. TAPI 3.1-Clients können die Informationen in dieser Anwendungsverzeichnispartition mit dem Service Locator-Verzeichnisdienst zum Suchen und mit TAPI-Verzeichnissen zu kommunizieren. Sie können auch **Tapicfg** erstellen oder Entfernen von Dienstverbindungspunkten, mit denen TAPI-Clients, um effizient TAPI-Anwendungsverzeichnispartitionen in einer Domäne suchen können. Weitere Informationen finden Sie unter "Hinweise". Klicken Sie auf einen Befehl, um die Befehlssyntax anzuzeigen. 
-   [Tapicfg installieren](#BKMK_install)
-   [Tapicfg entfernen](#BKMK_remove)
-   [tapicfg publishscp](#BKMK_publishscp)
-   [Tapicfg removescp](#BKMK_removescp)
-   [Tapicfg anzeigen](#BKMK_show)
-   [Tapicfg makedefault](#BKMK_makedefault)

## <a name="BKMK_install"></a>Tapicfg installieren
Erstellt eine TAPI-Anwendungsverzeichnispartition.

### <a name="syntax"></a>Syntax
```
tapicfg install /directory:<PartitionName> [/server:<DCName>] [/forcedefault]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Installieren von Directory:\<PartitionName >|Erforderlich. Gibt den DNS-Namen die TAPI-Anwendungsverzeichnispartition erstellt werden. Dieser Name muss es sich um einen vollständig qualifizierten Domänennamen sein.|
|/ Server: \<DCName>|Gibt den DNS-Namen des Domänencontrollers, auf dem die TAPI-Anwendungsverzeichnispartition erstellt wird. Wenn der Name des Domänencontrollers nicht angegeben ist, wird der Name des lokalen Computers verwendet.|
|/forcedefault|Gibt an, dass das Verzeichnis der Standard-TAPI-Anwendungsverzeichnispartition für die Domäne ist. Es kann mehrere TAPI-Anwendungsverzeichnispartitionen in einer Domäne sein.<br /><br />Wenn dieses Verzeichnis die erste TAPI-Anwendungsverzeichnispartition erstellt, in der Domäne ist, wird es automatisch festgelegt als Standard verwendet, unabhängig davon, ob Sie die **forcedefault** Option.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_remove"></a>Tapicfg entfernen
Entfernt eine TAPI-Anwendungsverzeichnispartition.

### <a name="syntax"></a>Syntax
```
tapicfg remove /directory:<PartitionName>
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Directory entfernen:\<PartitionName >|Erforderlich. Gibt den DNS-Namen die TAPI-Anwendungsverzeichnispartition entfernt werden soll. Beachten Sie, dass dieser Name muss einen vollständig qualifizierten Domänennamen sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_publishscp"></a>Tapicfg publishscp
Erstellt einen Dienstverbindungspunkt, um eine TAPI-Anwendungsverzeichnispartition zu veröffentlichen.

### <a name="syntax"></a>Syntax
```
tapicfg publishscp /directory:<PartitionName> [/domain:<DomainName>] [/forcedefault]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|publishscp /directory:\<PartitionName>|Erforderlich. Gibt an, dass der DNS-Name, der den Dienstverbindungspunkt TAPI-Anwendungsverzeichnispartition veröffentlicht werden sollen.|
|/ Domain:\<DomainName >|Gibt an, der DNS-Namen der Domäne, in dem der Dienstverbindungspunkt, erstellt wird. Wenn der Domänenname nicht angegeben ist, wird der Name der lokalen Domäne verwendet.|
|/forcedefault|Gibt an, dass das Verzeichnis der Standard-TAPI-Anwendungsverzeichnispartition für die Domäne ist. Es kann mehrere TAPI-Anwendungsverzeichnispartitionen in einer Domäne sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_removescp"></a>Tapicfg removescp
Entfernt einen Dienstverbindungspunkt für ein TAPI-Anwendungsverzeichnispartition.

### <a name="syntax"></a>Syntax
```
tapicfg removescp /directory:<PartitionName> [/domain:<DomainName>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Removescp Directory:\<PartitionName >|Erforderlich. Gibt den DNS-Namen die TAPI-Anwendungsverzeichnispartition für die Service Connection Point entfernt wird.|
|/ Domain: \<DomainName>|Gibt den DNS-Namen der Domäne aus der der Dienstverbindungspunkt entfernt wird. Wenn der Domänenname nicht angegeben ist, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_show"></a>Tapicfg anzeigen
Zeigt die Namen und Speicherorte der TAPI-Anwendungsverzeichnispartitionen in der Domäne an.

### <a name="syntax"></a>Syntax
```
tapicfg show [/defaultonly][ /domain:<DomainName>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/defaultonly|Zeigt die Namen und Speicherorte der nur die standardmäßigen TAPI Anwendungsverzeichnispartition in der Domäne an.|
|/ Domain: \<DomainName>|Gibt den DNS-Namen der Domäne für die die TAPI-Anwendungsverzeichnispartitionen angezeigt werden. Wenn der Domänenname nicht angegeben ist, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_makedefault"></a>Tapicfg makedefault
Legt die Standard-TAPI-Anwendungsverzeichnispartition für die Domäne fest.

### <a name="syntax"></a>Syntax
```
tapicfg makedefault /directory:<PartitionName> [/domain:<DomainName>]  
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Makedefault Directory:\<PartitionName >|Erforderlich. Gibt den DNS-Namen die TAPI-Anwendungsverzeichnispartition, legen Sie als die Standardpartition für die Domäne an. Beachten Sie, dass dieser Name muss einen vollständig qualifizierten Domänennamen sein. Gibt den DNS-Namen der Domäne für die die TAPI-Anwendungsverzeichnispartition als Standard festgelegt ist. Wenn der Domänenname nicht angegeben ist, wird der Name der lokalen Domäne verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
Sie müssen Mitglied der Gruppe "Organisations-Admins" in active Directory ausgeführt werden **Tapicfg installieren** (um eine TAPI-Anwendungsverzeichnispartition erstellen) oder **Tapicfg entfernen** (So entfernen Sie eine TAPI-Anwendung die Verzeichnispartition).

Dieses Befehlszeilentool kann auf jedem Computer ausgeführt werden, die ein Mitglied der Domäne ist.

Benutzer bereitgestellten Text (z. B. die Namen von TAPI-Anwendungsverzeichnispartitionen, Servern und Domänen) mit International oder Unicode-Zeichen werden nur angezeigt, ordnungsgemäß Wenn entsprechenden Schriftarten und Unterstützung für Sprachen installiert sind.

Weiterhin Internet Locator-Dienst (ILS) Server können in Ihrer Organisation gegebenenfalls ILS zur Unterstützung bestimmter Anwendungen erfolgen, da TAPI-Clients unter Windows XP oder eine Windows Server 2003-Betriebssystem entweder ILS-Server oder TAPI-Anwendung abgefragt werden können Verzeichnispartitionen.

Sie können **Tapicfg** erstellen oder Entfernen von Dienstverbindungspunkten. Wenn die TAPI-Anwendungsverzeichnispartition aus irgendeinem Grund (z. B., wenn Sie die Domäne umbenennen, in der er sich befindet) umbenannt wird, müssen Sie den vorhandenen Dienstverbindungspunkt zu entfernen und eine neue, die den neuen DNS-Namen des Anwendungsverzeichnisses TAPI enthält die Partition, die veröffentlicht werden. Andernfalls sind die TAPI-Clients nicht finden, und die TAPI-Anwendungsverzeichnispartition zugreifen. Sie können auch einen Dienstverbindungspunkt im Wartungszwecken oder Sicherheit entfernen, (beispielsweise, wenn Sie nicht, TAPI-Daten in einer bestimmten TAPI-Anwendungsverzeichnispartition verfügbar zu machen möchten).

## <a name="examples"></a>Beispiele
Um eine TAPI-Anwendungsverzeichnispartition benannte tapifiction.testdom.microsoft.com auf einem Server mit dem Namen testdc.testdom.microsoft.com, und legen Sie diese dann als die standardmäßige TAPI-Anwendungsverzeichnispartition für die neue Domäne zu erstellen, geben Sie Folgendes ein:
```
tapicfg install /directory:tapifiction.testdom.microsoft.com /server:testdc.testdom.microsoft.com /forcedefault
```
Um den Namen der standardmäßigen TAPI-Anwendungsverzeichnispartition für die neue Domäne anzuzeigen, geben Sie Folgendes ein:
```
tapicfg show /defaultonly
```
## <a name="additional-references"></a>Weitere Verweise
-   [Befehlszeilensyntax](command-line-syntax-key.md)
