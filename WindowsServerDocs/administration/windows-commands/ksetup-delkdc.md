---
title: 'Ksetup: Delta Controller'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b918f8c2fa0ec09c2aae77517a0ee2c9e77ce2dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375140"
---
# <a name="ksetupdelkdc"></a>Ksetup: Delta Controller



Löscht Instanzen von Schlüsselverteilungscenter Namen (KDC) für den Kerberos-Bereich. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delkdc <RealmName> <KDCName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und es wird als Standardbereich aufgeführt, wenn **Ksetup** ausgeführt wird. In diesem Bereich versuchen Sie, den anderen KDC zu löschen.|
|\<kdcname >|Der KDC-Name wird als voll qualifizierter Domänen Name, wie z. b. mitkdc.contoso.com, als voll qualifizierter Domänen Name angegeben.|

## <a name="remarks"></a>Hinweise

Diese Zuordnungen werden in der Registrierung in **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**gespeichert. Um Bereichs Konfigurationsdaten von mehreren Computern zu entfernen, verwenden Sie das Snap-in "Sicherheits Konfigurations Vorlage" und die Richtlinien Verteilung, anstatt **Ksetup** explizit auf einzelnen Computern zu verwenden.

Auf Computern, auf denen Windows 2000 Server mit Service Pack 1 (SP1) und früher ausgeführt wird, muss der Computer neu gestartet werden, bevor die geänderte Bereichs Einstellungs Konfiguration verwendet wird.

Um den Standard Bereichs Namen für den Computer zu überprüfen oder um zu überprüfen, ob dieser Befehl wie beabsichtigt funktioniert, führen Sie **Ksetup** an der Eingabeaufforderung aus, und vergewissern Sie sich, dass der entfernte KDC nicht in der Liste vorhanden ist.

## <a name="BKMK_Examples"></a>Beispiele

Die Sicherheitsanforderungen für diesen Computer wurden geändert, sodass die Verknüpfung zwischen dem Windows-Bereich und dem nicht-Windows-Bereich entfernt werden muss. Legen Sie zunächst fest, welche Zuordnung entfernt werden soll, und führen Sie die Ausgabe vorhandener Zuordnungen aus:
```
ksetup
```
Entfernen Sie die Zuordnung, indem Sie den folgenden Befehl verwenden:
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)