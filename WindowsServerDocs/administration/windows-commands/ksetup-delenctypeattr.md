---
title: 'Ksetup: Delta Type'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2908cc0a095a6985c11f7885766926b7f0354ab0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724706"
---
# <a name="ksetupdelenctypeattr"></a>Ksetup: Delta Type



Entfernt das Verschlüsselungstyp Attribut für die Domäne.

## <a name="syntax"></a>Syntax

```
ksetup /delenctypeattr <DomainName> 
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Domain Name>|Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. Corp.contoso.com oder Configuration Manager.|

## <a name="remarks"></a>Bemerkungen

Um den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzuzeigen, führen Sie den Befehl **klist** aus, und zeigen Sie die Ausgabe an.

Bei erfolgreicher oder fehlgeschlagener Ausführung wird eine Statusmeldung angezeigt.

Um die Domäne festzulegen, mit der Sie eine Verbindung herstellen und verwenden möchten, führen Sie den Befehl **Ksetup/Domain \<Domainname>** aus.

## <a name="examples"></a>Beispiele

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

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)