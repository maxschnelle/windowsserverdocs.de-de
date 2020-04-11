---
title: Clients können keine Verbindung herstellen und erhalten den Fehler „Klasse nicht registriert“
description: Beheben des Fehlers „Klasse nicht registriert“ bei der Remotedesktopverbindung.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 52e696bd4229b947ea63a379211192b8664a9f93
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857183"
---
# <a name="clients-cant-connect-and-get-the-class-not-registered-error"></a>Clients können keine Verbindung herstellen und erhalten den Fehler „Klasse nicht registriert“

Wenn Sie versuchen, eine Verbindung mit einem Remotecomputer mithilfe eines Clients herzustellen, auf dem Windows 10, Version 1709 oder höher, ausgeführt wird, stellt der Client möglicherweise keine Verbindung her, während der Remotedesktop-Sitzungshostserver eine Meldung ausgibt, die den Fehlercode „Klasse nicht registriert (0x80040154)“ enthält.

Dieses Problem tritt auf, wenn der Benutzer, der die Verbindung herzustellen versucht, über ein obligatorisches Benutzerprofil verfügt. Um dieses Problem zu beheben, installieren Sie das Windows 10-Update vom [24. Juli 2018—KB4338817 (Betriebssystembuild 16299.579)](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817).
