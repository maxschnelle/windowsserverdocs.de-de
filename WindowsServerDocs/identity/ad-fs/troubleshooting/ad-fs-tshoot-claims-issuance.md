---
title: 'AD FS Problembehandlung: Anspruchs Ausstellung'
description: In diesem Dokument wird beschrieben, wie Probleme bei der Tokenausstellung mit AD FS behoben werden.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 9eb5ce1ee92e828cc1fd6ceb40ddddec453afe87
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954186"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>AD FS Problembehandlung: Anspruchs Ausstellung
Ein Anspruch ist eine-Anweisung, die ein Subjekt über sich selbst oder einen anderen Betreff trifft.  Ansprüche werden von einer vertrauenden Seite ausgegeben, und Sie erhalten einen oder mehrere Werte und werden dann in Sicherheits Token verpackt, die vom AD FS Server ausgestellt werden.  Da in diesem Prozess mehrere bewegliche Teile vorhanden sind, kann die Anspruchs Ausstellung in diese wichtigen Teile aufgeteilt werden.

>[!NOTE]
>Sie können [claimsxray](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) auf der [ADFS-Hilfe](https://adfshelp.microsoft.com) Website verwenden, um die Behandlung von Anspruchs Problemen zu unterstützen.

## <a name="token-request"></a>Tokenanforderung
Wenn Sie zu einer vertrauenden Seite wechseln, werden Sie mit einer Tokenanforderung an AD FS umgeleitet.  Probleme können mit der Anforderung auftreten.  Dies gilt insbesondere für Folgendes:

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>Die Anforderungs Formatierung mit Drittanbietern (insbesondere SAML)

### <a name="pre-formated-urls-that-have-typos"></a>Vorformatierte URLs mit Tippfehler
Beim Ausgeben eines Tokens von WS-federaion-vertrauenden Seiten, die die Tokenanforderung mit URL-Abfrage Zeichenfolgen-Parametern ergibt.  Wenn die vertrauende Seite die richtigen Parameter in dieser URL nicht angibt, wenn Sie die Umleitung zu AD FS, kann dies ein Problem mit der Anforderung verursachen.


Zur Überprüfung des Tokenformats kann ein webdebugger-Tool verwendet werden.


## <a name="token-response"></a>Tokenantwort

## <a name="authentication"></a>Authentifizierung

## <a name="claim-rule-processing"></a>Verarbeitung von Anspruchs Regeln