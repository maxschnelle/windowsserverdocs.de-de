---
title: 'AD FS Problembehandlung: Anspruchs Ausstellung'
description: In diesem Dokument wird beschrieben, wie Probleme bei der Tokenausstellung mit AD FS behoben werden.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ea0e6112f00f9cace6a0c580661a5319b5adaea5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366238"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>AD FS Problembehandlung: Anspruchs Ausstellung
Ein Anspruch ist eine-Anweisung, die ein Subjekt über sich selbst oder einen anderen Betreff trifft.  Ansprüche werden von einer vertrauenden Seite ausgegeben, und Sie erhalten einen oder mehrere Werte und werden dann in Sicherheits Token verpackt, die vom AD FS Server ausgestellt werden.  Da in diesem Prozess mehrere bewegliche Teile vorhanden sind, kann die Anspruchs Ausstellung in diese wichtigen Teile aufgeteilt werden.

>[!NOTE]  
>Sie können [claimsxray](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) auf der [ADFS-Hilfe](https://adfshelp.microsoft.com) Website verwenden, um die Behandlung von Anspruchs Problemen zu unterstützen.   

## <a name="token-request"></a>Tokenanforderung
Wenn Sie zu einer vertrauenden Seite wechseln, werden Sie mit einer Tokenanforderung an AD FS umgeleitet.  Probleme können mit der Anforderung auftreten.  Insbesondere:

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>Die Anforderungs Formatierung mit Drittanbietern (insbesondere SAML)

### <a name="pre-formated-urls-that-have-typos"></a>Vorformatierte URLs mit Tippfehler
Beim Ausgeben eines Tokens von WS-federaion-vertrauenden Seiten, die die Tokenanforderung mit URL-Abfrage Zeichenfolgen-Parametern ergibt.  Wenn die vertrauende Seite die richtigen Parameter in dieser URL nicht angibt, wenn Sie die Umleitung zu AD FS, kann dies ein Problem mit der Anforderung verursachen.


Zur Überprüfung des Tokenformats kann ein webdebugger-Tool verwendet werden.


## <a name="token-response"></a>Tokenantwort

## <a name="authentication"></a>Authentifizierung

## <a name="claim-rule-processing"></a>Verarbeitung von Anspruchs Regeln