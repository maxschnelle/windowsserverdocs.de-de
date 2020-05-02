---
title: 'Ksetup: Delta Controller'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19ebe322d414d1ae9007275772ccd747f6f0ff8d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724658"
---
# <a name="ksetupdelkdc"></a>Ksetup: Delta Controller



Löscht Instanzen von Schlüsselverteilungscenter Namen (KDC) für den Kerberos-Bereich.

## <a name="syntax"></a>Syntax

```
ksetup /delkdc <RealmName> <KDCName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Realmname->|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und es wird als Standardbereich aufgeführt, wenn **Ksetup** ausgeführt wird. In diesem Bereich versuchen Sie, den anderen KDC zu löschen.|
|\<Kdcname->|Der KDC-Name wird als voll qualifizierter Domänen Name, wie z. b. mitkdc.contoso.com, als voll qualifizierter Domänen Name angegeben.|

## <a name="remarks"></a>Bemerkungen

Diese Zuordnungen werden in der Registrierung in **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**gespeichert. Um Bereichs Konfigurationsdaten von mehreren Computern zu entfernen, verwenden Sie das Snap-in "Sicherheits Konfigurations Vorlage" und die Richtlinien Verteilung, anstatt **Ksetup** explizit auf einzelnen Computern zu verwenden.

Auf Computern, auf denen Windows 2000 Server mit Service Pack 1 (SP1) und früher ausgeführt wird, muss der Computer neu gestartet werden, bevor die geänderte Bereichs Einstellungs Konfiguration verwendet wird.

Um den Standard Bereichs Namen für den Computer zu überprüfen oder um zu überprüfen, ob dieser Befehl wie beabsichtigt funktioniert, führen Sie **Ksetup** an der Eingabeaufforderung aus, und vergewissern Sie sich, dass der entfernte KDC nicht in der Liste vorhanden ist.

## <a name="examples"></a>Beispiele

Die Sicherheitsanforderungen für diesen Computer wurden geändert, sodass die Verknüpfung zwischen dem Windows-Bereich und dem nicht-Windows-Bereich entfernt werden muss. Legen Sie zunächst fest, welche Zuordnung entfernt werden soll, und führen Sie die Ausgabe vorhandener Zuordnungen aus:
```
ksetup
```
Entfernen Sie die Zuordnung, indem Sie den folgenden Befehl verwenden:
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)