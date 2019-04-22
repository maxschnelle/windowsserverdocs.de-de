---
title: ksetup:delkdc
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e2fa065ca60338b04cc8718e199805cc494c908
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814561"
---
# <a name="ksetupdelkdc"></a>ksetup:delkdc



Löscht die Instanzen der Schlüsselverteilungscenter (Key Distribution Center, KDC)-Namen für die Kerberos-Bereich. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delkdc <RealmName> <KDCName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "Contoso.com", und es wird als den Standardbereich aufgeführt beim **Ksetup** ausgeführt wird. Es ist in diesem Bereich aus der Sie versuchen, das andere KDC zu löschen.|
|\<KDCName>|Der KDC-Name wird als Groß-/Kleinschreibung, den vollqualifizierten Domänennamen, z. B. mitkdc.contoso.com angegeben.|

## <a name="remarks"></a>Hinweise

Diese Zuordnungen werden in der Registrierung gespeichert **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**. Um Konfigurationsdaten Bereich von mehreren Computern zu entfernen, verwenden Sie die Vorlage für die Sicherheitskonfiguration-Snap-in und richtlinienverteilung anstelle von **Ksetup** explizit auf einzelnen Computern.

Auf Computern unter Windows 2000 Server mit Service Pack 1 (SP1) und früheren Versionen muss der Computer neu gestartet werden, bevor die Einstellungskonfiguration geänderten Bereich verwendet wird.

Führen Sie den Standardnamen der Bereich für den Computer zu überprüfen oder zu überprüfen, ob dieser Befehl funktioniert wie vorgesehen, **Ksetup** an der Eingabeaufforderung, und stellen Sie sicher, dass das KDC, der entfernt wurde, nicht in der Liste vorhanden ist.

## <a name="BKMK_Examples"></a>Beispiele für

Die sicherheitsanforderungen für diesen Computer wurden geändert, damit die Verknüpfung zwischen der Windows-Bereich und dem nicht-Windows-Bereich entfernt werden muss. Bestimmen Sie zunächst, dem die Zuordnung entfernen und die Ausgabe der vorhandenen Zuordnungen generiert:
```
ksetup
```
Entfernen Sie die Zuordnung mit dem folgenden Befehl ein:
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)