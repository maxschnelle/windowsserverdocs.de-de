---
title: ksetup:addkdc
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3e0d38bdec11618561ee4acaa32ffdd06695fab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868531"
---
# <a name="ksetupaddkdc"></a>ksetup:addkdc



Fügt ein Schlüsselverteilungscenter (Key Distribution Center, KDC)-Adresse für den angegebenen Kerberos-Bereich hinzu. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "Contoso.com", und es wird als den Standardbereich aufgeführt beim **Ksetup** ausgeführt wird. Es ist in diesem Bereich, die Sie andere KDC hinzufügen möchten.|
|\<KDCName>|Der KDC-Name wird als Groß-und Kleinschreibung den vollqualifizierten Domänennamen, z. B. mitkdc.microsoft.com angegeben. Wenn der KDC-Name fehlt, wird DNS KDCs suchen.|

## <a name="remarks"></a>Hinweise

Diese Zuordnungen werden gespeichert, in der Registrierung unter **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**. Um die Konfigurationsdaten für Kerberos-Bereich auf mehreren Computern bereitstellen, verwenden Sie die Vorlage für die Sicherheitskonfiguration-Snap-in und richtlinienverteilung anstelle von **Ksetup** explizit auf einzelnen Computern.

Der Computer muss neu gestartet werden, bevor die neue Einstellung für den Bereich verwendet wird.

Führen Sie den Standardnamen der Bereich für den Computer zu überprüfen oder zu überprüfen, ob dieser Befehl funktioniert wie vorgesehen, **Ksetup** an der Eingabeaufforderung, und überprüfen Sie die Ausgabe für den hinzugefügten KDC.

## <a name="BKMK_Examples"></a>Beispiele für

Konfigurieren Sie einen nicht - Windows-KDC-Server und dem Bereich, den die Arbeitsstation verwendet werden soll:
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
Führen Sie das Ksetup-Tool in der Befehlszeile aus dem gleichen Computer wie der vorhergehende Befehl legen Sie das Kennwort des lokalen Computerkontos auf "p@sswrd1%?. Klicken Sie dann starten Sie den Computer neu.
```
Ksetup /setcomputerpassword p@sswrd1%
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)