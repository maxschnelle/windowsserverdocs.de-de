---
title: 'Ksetup: getenctypeattr'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8363113d4fbb310d98b40d852b36a00f20320e6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724635"
---
# <a name="ksetupgetenctypeattr"></a>Ksetup: getenctypeattr



Ruft das Verschlüsselungstyp Attribut für die Domäne ab.

## <a name="syntax"></a>Syntax

```
ksetup /getenctypeattr <DomainName> 
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Domain Name>|Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. Corp.contoso.com oder Configuration Manager.|

## <a name="remarks"></a>Bemerkungen

Um den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzuzeigen, führen Sie den Befehl **klist** aus, und zeigen Sie die Ausgabe an.

Wenn der Befehl erfolgreich ausgeführt wird oder fehlschlägt, wird bei erfolgreicher oder fehlgeschlagener Ausführung eine Statusmeldung angezeigt.

Um die Domäne festzulegen, mit der Sie eine Verbindung herstellen und verwenden möchten, führen Sie den Befehl **Ksetup/Domain \<Domainname>** aus.

## <a name="examples"></a>Beispiele

Überprüfen Sie das Attribut für den Verschlüsselungstyp für die Domäne:
```
ksetup /getenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)