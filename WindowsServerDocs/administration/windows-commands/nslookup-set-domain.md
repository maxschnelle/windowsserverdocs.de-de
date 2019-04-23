---
title: nslookup set domain
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9019893d92201079fb60b820a14dda3763bafd6b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886641"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Standarddomänennamen des Domain Name System (DNS) in den angegebenen Namen.
## <a name="syntax"></a>Syntax
```
set domain=<DomainName>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<DomainName>|Gibt einen neuen Namen für den standardmäßigen DNS-Domänennamen an. Der standardmäßige Domänenname ist der Hostname.|
|{help &#124; ?}|Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.|
## <a name="remarks"></a>Hinweise
-   Der Standard-DNS-Domänenname wird an eine suchanforderung, abhängig vom Zustand angefügt der **Defname** und **Suche** Optionen. Die Suchliste für DNS-Domäne enthält die übergeordneten Elementen von DNS-Standarddomäne, verfügt er über mindestens zwei Komponenten in ihrem Namen. Beispielsweise ist der DNS-Standarddomäne mfg.widgets.com, die Suchliste sowohl mfg.widgets.com und widgets.com heißt. Verwenden der **festgelegt Srchlist** Befehl, um eine andere Liste anzugeben und die **alle festlegen** Befehl aus, um die Liste anzuzeigen.
## <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Nslookup festgelegt Srchlist](nslookup-set-srchlist.md)
[Nslookup alle festlegen](nslookup-set-all.md)
