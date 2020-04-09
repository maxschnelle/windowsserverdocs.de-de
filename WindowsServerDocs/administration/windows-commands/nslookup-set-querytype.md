---
title: nslookup set querytype
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c066277a22325e5db8383f58cda31038aa656e0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838433"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Ressourcen Daten Satz für die Abfrage.
## <a name="syntax"></a>Syntax
```
set querytype=<ResourceRecordtype>
```
### <a name="parameters"></a>Parameter
<ResourceRecordtype> gibt einen DNS-Ressourcen eingabentyp an. Der Standard Ressourcen Daten Satz-Typ ist. In der folgenden Tabelle sind die gültigen Werte für diesen Befehl aufgeführt.

| Wert |                                                   Beschreibung                                                   |
|-------|-----------------------------------------------------------------------------------------------------------------|
|   A   |                                      Gibt die IP&#39;-Adresse des Computers an.                                      |
|  Irgendeiner  |                                     Gibt die IP&#39;-Adresse des Computers an.                                      |
| CNAME |                                    Gibt einen kanonischen Namen für einen Alias an.                                     |
|  Ü  |                                  Gibt einen Gruppen Bezeichner eines Gruppennamens an.                                  |
| Hinfo |                          Gibt die CPU&#39;und den Typ des Betriebssystems des Computers an.                           |
|  MB   |                                        Gibt einen Post Fach Domänen Namen an.                                         |
|  MG   |                                         Gibt ein e-Mail-Gruppenmitglied an.                                          |
| MINFO |                                   Gibt Postfach-oder e-Mail-Listen Informationen an.                                   |
|  MR   |                                     Gibt den Namen der Umbenennungs Domäne an.                                      |
|  MX   |                                          Gibt den e-Mail-Austausch an                                          |
|  NS   |                                 Gibt einen DNS-Namen Server für die benannte Zone an.                                 |
|  PTR  | Gibt einen Computernamen an, wenn die Abfrage eine IP-Adresse ist. Andernfalls gibt den Zeiger auf andere Informationen an. |
|  SOA  |                                Gibt den Autorisierungs Anfang für eine DNS-Zone an.                                 |
|  TXT  |                                         Gibt die Textinformationen an.                                         |
|  UID  |                                         Gibt die Benutzer-ID an.                                          |
| Uinfo |                                         Gibt die Benutzerinformationen an.                                         |
|  Wert  |                                         Beschreibt einen bekannten Dienst.                                         |
| {Hilfe |                                                       ?}                                                        |

Zeigt eine kurze Zusammenfassung der <strong>nslookup</strong> -Unterbefehle an.
## <a name="remarks"></a>Hinweise
- Der <strong>Set Type</strong> -Befehl führt dieselbe Funktion aus wie der <strong>Set QueryType</strong> -Befehl.
- Weitere Informationen zu Ressourcen Daten Satz Typen finden Sie unter Request for Comment (RFC) 1035.
  ## <a name="additional-references"></a>Weitere Verweise
  < einen href = Command-Line-Syntax-Key.MD Data-RAW-Source =- [Command-Line-Syntax Schlüssel](command-line-syntax-key.md)> Befehlszeilen-Syntax Schlüssel</a> < a href = nslookup-Set-Type.MD Data-RAW-Source =[nslookup Set Type](nslookup-set-type.md)> nslookup Set Type</a>
