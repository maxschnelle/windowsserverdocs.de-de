---
title: Clients können keine Verbindung herstellen und erhalten den Fehler „Klasse nicht registriert“
description: Beheben des Fehlers „Klasse nicht registriert“ bei der Remotedesktopverbindung.
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7a98e894f3eaf47e257ab39c640e93101fd76fc8
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265902"
---
# <a name="clients-cant-connect-and-get-the-class-not-registered-error"></a>Clients können keine Verbindung herstellen und erhalten den Fehler „Klasse nicht registriert“

Wenn Sie versuchen, eine Verbindung mit einem Remotecomputer mithilfe eines Clients herzustellen, auf dem Windows 10, Version 1709 oder höher, ausgeführt wird, stellt der Client möglicherweise keine Verbindung her, während der Remotedesktop-Sitzungshostserver eine Meldung ausgibt, die den Fehlercode „Klasse nicht registriert (0x80040154)“ enthält.

Dieses Problem tritt auf, wenn der Benutzer, der die Verbindung herzustellen versucht, über ein obligatorisches Benutzerprofil verfügt. Um dieses Problem zu beheben, installieren Sie das Windows 10-Update vom [24. Juli 2018—KB4338817 (Betriebssystembuild 16299.579)](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817).
