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
ms.openlocfilehash: 4fb647b723586202e2bd88f1ab4c8943e305a73a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436494"
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

| Wert |                                                   Beschreibung                                                   |
|-------|-----------------------------------------------------------------------------------------------------------------|
|   A   |                                      Bezeichnet einen Computer&#39;IP-Adresse                                      |
|  ALLE  |                                     Bezeichnet einen Computer&#39;IP-Adresse.                                      |
| CNAME |                                    Gibt einen kanonischen Namen für einen Alias.                                     |
|  GID  |                                  Gibt eine Gruppen-ID, der einen Gruppennamen an.                                  |
| HINFO |                          Bezeichnet einen Computer&#39;s CPU und der Typ des Betriebssystems.                           |
|  MB   |                                        Gibt den Postfach-Domänennamen an.                                         |
|  MG   |                                         Gibt einen e-Mail-Group-Member.                                          |
| MINFO |                                   Gibt die Mailbox- oder e-Mail-Informationen an.                                   |
|  MR   |                                     Gibt an, der Domänenname der e-Mail-umbenennen.                                      |
|  MX   |                                          Gibt an, die Mail-Exchanger.                                          |
|  NS   |                                 Gibt eine DNS-Namenserver für die benannte Zone an.                                 |
|  PTR  | Bezeichnet einen Computer nennen, wenn die Abfrage eine IP-Adresse ist. andernfalls gibt Sie den Zeiger auf andere Informationen. |
|  SOA  |                                Gibt an, der Start of Authority für eine DNS-Zone.                                 |
|  TXT  |                                         Gibt an, die Textinformationen.                                         |
|  UID  |                                         Gibt die Benutzer-ID an.                                          |
| UINFO |                                         Gibt die Benutzerinformationen an.                                         |
|  WKS  |                                         Beschreibt einen bekannten Dienst.                                         |
| {Hilfe |                                                       ?}                                                        |

Zeigt eine kurze Zusammenfassung der <strong>Nslookup</strong> Unterbefehle
## <a name="remarks"></a>Hinweise
- Die <strong>resultsettyps</strong> Befehl führt die gleiche Funktion wie der <strong>festgelegt Querytype</strong> Befehl.
- Weitere Informationen zu Resource Record-Typen finden Sie in der Anforderung für Kommentar (Rfc) 1035.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  <a href="command-line-syntax-key.md" data-raw-source="[Command-Line Syntax Key](command-line-syntax-key.md)">Befehlszeilen-Syntaxschlüssel</a>
  <a href="nslookup-set-querytype.md" data-raw-source="[nslookup set querytype](nslookup-set-querytype.md)">Nslookup festgelegt Querytype</a>
