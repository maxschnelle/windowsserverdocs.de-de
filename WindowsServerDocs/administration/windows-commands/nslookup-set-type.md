---
title: nslookup set type
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5248e314-fac1-413e-81dc-bbe0a0873ba5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: accf8ccbe147a831ee306dd670384b90844ff4fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835951"
---
# <a name="nslookup-set-type"></a>nslookup set type

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Typ des Ressourcendatensatzes für die Abfrage an.
## <a name="syntax"></a>Syntax
```
set type=<ResourceRecordtype>
```
## <a name="parameters"></a>Parameter
<ResourceRecordtype> Gibt einen DNS-Datensatz Ressourcentyp an. Die Standard-Ressourceneintragstyp ist a? Die folgende Tabelle enthält die gültigen Werte für diesen Befehl.
|Wert|Beschreibung|
|-----|--------|
|A|Gibt an, die IP-Adresse eines Computers|
|ALLE|Gibt die IP-Adresse eines Computers an.|
|CNAME|Gibt einen kanonischen Namen für einen Alias.|
|GID|Gibt eine Gruppen-ID, der einen Gruppennamen an.|
|HINFO|Gibt an, CPU und den Typ des Betriebssystems eines Computers.|
|MB|Gibt den Postfach-Domänennamen an.|
|MG|Gibt einen e-Mail-Group-Member.|
|MINFO|Gibt die Mailbox- oder e-Mail-Informationen an.|
|MR|Gibt an, der Domänenname der e-Mail-umbenennen.|
|MX|Gibt an, die Mail-Exchanger.|
|NS|Gibt eine DNS-Namenserver für die benannte Zone an.|
|PTR|Bezeichnet einen Computer nennen, wenn die Abfrage eine IP-Adresse ist. andernfalls gibt Sie den Zeiger auf andere Informationen.|
|SOA|Gibt an, der Start of Authority für eine DNS-Zone.|
|TXT|Gibt an, die Textinformationen.|
|UID|Gibt die Benutzer-ID an.|
|UINFO|Gibt die Benutzerinformationen an.|
|WKS|Beschreibt einen bekannten Dienst.|
{Hilfe | ?}
Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle
## <a name="remarks"></a>Hinweise
-   Die **resultsettyps** Befehl führt die gleiche Funktion wie der **festgelegt Querytype** Befehl.
-   Weitere Informationen zu Resource Record-Typen finden Sie in der Anforderung für Kommentar (Rfc) 1035.
## <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Nslookup festgelegt Querytype](nslookup-set-querytype.md)
