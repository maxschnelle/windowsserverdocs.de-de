---
title: Problembehandlung für AD FS - Ausstellung von Ansprüchen
description: In diesem Dokument wird beschrieben, wie tokenausstellungs-Problembehandlung mit AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fdf8851fe9b35f82191458ba3313fda2dc3ee4cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839661"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>Problembehandlung für AD FS - Ausstellung von Ansprüchen
Ein Anspruch ist eine Anweisung, ein Subjekt macht über sich selbst oder einen anderen Antragsteller.  Ansprüche werden durch eine vertrauende Seite ausgestellt, und sie erhalten Sie einen oder mehrere Werte sind, und klicken Sie dann in Sicherheitstoken, die von AD FS-Servers ausgestellt werden verpackt.  Da in diesen Prozess mehrere Variable Komponenten vorhanden sind, kann Ausstellung von Ansprüchen in diese wichtige Teile unterteilt werden.

>[!NOTE]  
>Können Sie [ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) auf die [AD FS-Hilfe](https://adfshelp.microsoft.com) Site zur Problembehandlung behauptet Probleme.   

## <a name="token-request"></a>Anforderung eines Zugriffstokens
Wenn Sie zu einer vertrauenden leitet es Sie AD FS mit einer token-Anforderung.  Probleme können mit der Anforderung auftreten.  Insbesondere:

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>Die Anforderung, die Formatierung mit 3. Parteien (insbesondere SAML)

### <a name="pre-formated-urls-that-have-typos"></a>Pre-formatiertes URLs, die von Tippfehlern
Wenn Sie ein Token von WS-Federaion vertrauende Seiten, Sicherheitstoken-Anforderung ausgeben mit URL-Abfragezeichenfolgenparametern geht auf.  Wenn die vertrauende Seite angeben und nicht die richtigen Parameter in diese URL wird die Umleitung zu AD FS kann dies ein Problem mit der Anforderung führen.


Damit auf Verifiy das tokenformat kann ein Web Debugger-Tool verwendet werden


## <a name="token-response"></a>Tokenantwort

## <a name="authentication"></a>Authentifizierung

## <a name="claim-rule-processing"></a>Anspruch Regelverarbeitung