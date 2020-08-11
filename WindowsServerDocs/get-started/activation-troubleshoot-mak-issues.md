---
title: 'MAK-Aktivierung: bekannte Probleme'
description: Beschreibt häufige Probleme, die während des MAK-Aktivierungsvorgangs auftreten können, und bietet Lösungen und Anleitungen.
ms.topic: troubleshooting
ms.date: 10/3/2019
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: ed9be4f46dccb525d4207378e1695d12a0c648ed
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972347"
---
# <a name="mak-activation-known-issues"></a>MAK-Aktivierung: bekannte Probleme

In diesem Artikel werden häufige Probleme beschrieben, die bei der Aktivierung mittels Mehrfachaktivierungsschlüssel (MAK) auftreten können, sowie Anleitungen zur Behebung dieser Probleme.

## <a name="how-can-i-tell-whether-my-computer-is-activated"></a>Woran kann ich erkennen, ob mein Computer aktiviert ist?

Öffne auf dem Computer die **Systemsteuerung**, und suche nach **Windows ist aktiviert**. Führe alternativ „Slmgr.vbs“ aus, und verwende die Befehlszeilenoption **/dli**.

## <a name="the-computer-does-not-activate-over-the-internet"></a>Der Computer wird über das Internet nicht aktiviert.

Stelle sicher, dass die erforderlichen Ports in der Firewall geöffnet sind. Eine Liste der Ports findest du im [Bereitstellungshandbuch zur Volumenaktivierung](https://go.microsoft.com/fwlink/?linkid=150083).

## <a name="internet-and-telephone-activation-fail"></a>Fehler bei der Internet- und Telefonaktivierung

Wende dich an ein Microsoft Activation Center vor Ort. Die weltweiten Telefonnummern der Microsoft Activation Center findest du unter [Microsoft Licensing Activation Center –Telefonnummern weltweit](https://www.microsoft.com/Licensing/existing-customer/activation-centers). Stelle sicher, dass du die Informationen zum Volumenlizenzvertrag und den Kaufnachweis bereitstellen kannst, wenn du anrufst.

## <a name="slmgrvbs-ato-returns-an-error-code"></a>„Slmgr.vbs /ato“ gibt einen Fehlercode zurück.

Wenn „Slmgr.vbs“ einen hexadezimalen Fehlercode zurückgibt, ermittelst du die zugehörige Fehlermeldung, indem du das folgende Skript ausführst:

```cmd
slui.exe 0x2a 0x <ErrorCode>
```

Weitere Informationen zu bestimmten Fehlercodes und deren Behebung findest du unter [Auflösen von gängigen Aktivierungsfehlercodes](activation-error-codes.md).
