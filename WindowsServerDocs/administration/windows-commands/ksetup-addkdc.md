---
title: ksetup addkdc
description: Referenz Artikel für den Befehl "Ksetup addkdc", der eine Schlüsselverteilungscenter (KDC)-Adresse für den angegebenen Kerberos-Bereich anzeigen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32839c0f8c1e408cfa6ab1e067c250551ee7b490
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925569"
---
# <a name="ksetup-addkdc"></a>ksetup addkdc

Fügt eine Schlüsselverteilungscenter (KDC)-Adresse für den angegebenen Kerberos-Bereich hinzu.

Die Zuordnung wird in der Registrierung unter **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains** gespeichert, und der Computer muss neu gestartet werden, bevor die neue Bereichseinstellung verwendet wird.

> [!NOTE]
> Wenn Sie Kerberos-Bereichs Konfigurationsdaten auf mehreren Computern bereitstellen möchten, müssen Sie das Snap-in für **Sicherheits Konfigurations Vorlagen** und die Richtlinien Verteilung explizit auf einzelnen Computern verwenden. Dieser Befehl kann nicht verwendet werden.

## <a name="syntax"></a>Syntax

```
ksetup /addkdc <realmname> [<KDCname>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com. Dieser Wert wird auch als Standardbereich angezeigt, wenn **Ksetup** ausgeführt wird, und ist der Bereich, dem Sie den anderen KDC hinzufügen möchten. |
| `<KDCname>` | Gibt den voll qualifizierten Domänen Namen der Groß-/Kleinschreibung an, z. b. mitkdc.contoso.com. Wenn der KDC-Name ausgelassen wird, sucht DNS nach KDCs. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen nicht-Windows-KDC-Server und den von der Arbeitsstation zu verwendenden Bereich zu konfigurieren:

```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

Geben Sie Folgendes ein, um das Kennwort für das lokale Computer Konto p@sswrd1 auf dem gleichen Computer wie im vorherigen Beispiel auf% festzulegen und den Computer anschließend neu zu starten:

```
ksetup /setcomputerpassword p@sswrd1%
```

Geben Sie Folgendes ein, um den Standard Bereichs Namen des Computers zu überprüfen oder um zu überprüfen, ob dieser Befehl wie beabsichtigt funktioniert:

```
ksetup
```
Überprüfen Sie die Registrierung, um sicherzustellen, dass die Zuordnung wie beabsichtigt erfolgt ist.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Befehl "setcomputerpassword"](ksetup-setcomputerpassword.md)
