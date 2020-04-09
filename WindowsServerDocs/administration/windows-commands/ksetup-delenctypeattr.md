---
title: 'Ksetup: Delta Type'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c650b973ac34e28394d5b6ec38142a058ad76338
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841763"
---
# <a name="ksetupdelenctypeattr"></a>Ksetup: Delta Type



Entfernt das Verschlüsselungstyp Attribut für die Domäne. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delenctypeattr <DomainName> 
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Domainname >|Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. Corp.contoso.com oder Configuration Manager.|

## <a name="remarks"></a>Hinweise

Um den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzuzeigen, führen Sie den Befehl **klist** aus, und zeigen Sie die Ausgabe an.

Bei erfolgreicher oder fehlgeschlagener Ausführung wird eine Statusmeldung angezeigt.

Um die Domäne festzulegen, mit der Sie eine Verbindung herstellen und verwenden möchten, führen Sie den Befehl **Ksetup/Domain \<Domainname >** aus.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Bestimmen Sie die aktuellen Verschlüsselungstypen, die auf diesem Computer festgelegt sind:
```
klist
```
Legen Sie die Domäne auf mit.contoso.com fest:
```
ksetup /domain mit.contoso.com
```
Überprüfen Sie das Verschlüsselungstyp Attribut für die Domäne:
```
ksetup /getenctypeattr mit.contoso.com
```
Entfernen Sie das Set encryption type-Attribut für die Domäne mit.contoso.com:
```
ksetup /delenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)