---
title: 'Ksetup: Delta Controller'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63b264da227d51b6f47f982c66828536bd677920
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841693"
---
# <a name="ksetupdelkdc"></a>Ksetup: Delta Controller



Löscht Instanzen von Schlüsselverteilungscenter Namen (KDC) für den Kerberos-Bereich. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delkdc <RealmName> <KDCName>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und es wird als Standardbereich aufgeführt, wenn **Ksetup** ausgeführt wird. In diesem Bereich versuchen Sie, den anderen KDC zu löschen.|
|\<kdcname >|Der KDC-Name wird als voll qualifizierter Domänen Name, wie z. b. mitkdc.contoso.com, als voll qualifizierter Domänen Name angegeben.|

## <a name="remarks"></a>Hinweise

Diese Zuordnungen werden in der Registrierung in **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**gespeichert. Um Bereichs Konfigurationsdaten von mehreren Computern zu entfernen, verwenden Sie das Snap-in "Sicherheits Konfigurations Vorlage" und die Richtlinien Verteilung, anstatt **Ksetup** explizit auf einzelnen Computern zu verwenden.

Auf Computern, auf denen Windows 2000 Server mit Service Pack 1 (SP1) und früher ausgeführt wird, muss der Computer neu gestartet werden, bevor die geänderte Bereichs Einstellungs Konfiguration verwendet wird.

Um den Standard Bereichs Namen für den Computer zu überprüfen oder um zu überprüfen, ob dieser Befehl wie beabsichtigt funktioniert, führen Sie **Ksetup** an der Eingabeaufforderung aus, und vergewissern Sie sich, dass der entfernte KDC nicht in der Liste vorhanden ist.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Die Sicherheitsanforderungen für diesen Computer wurden geändert, sodass die Verknüpfung zwischen dem Windows-Bereich und dem nicht-Windows-Bereich entfernt werden muss. Legen Sie zunächst fest, welche Zuordnung entfernt werden soll, und führen Sie die Ausgabe vorhandener Zuordnungen aus:
```
ksetup
```
Entfernen Sie die Zuordnung, indem Sie den folgenden Befehl verwenden:
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)