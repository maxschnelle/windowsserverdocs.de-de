---
title: Remotedesktop - vergleichen Sie die Client-apps
description: Erfahren Sie, wie die verschiedenen RD-apps vergleichen, bei unterstützten Features und Funktionen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 79a6b264c38b4b843c2887c6a3eb6f236480243d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828961"
---
# <a name="compare-the-client-apps"></a>Vergleichen Sie die Client-apps

>Gilt für: Windows 10, Windows 8.1, Windows Server 2012 R2, WindowsServer 2016

Wir häufig gefragt, wie die anderen Remotedesktop-Client-apps miteinander verglichen werden soll. Machen sie alle dasselbe? Hier sind die Antworten auf diese Fragen.

## <a name="redirection-support"></a>-Umleitung

Die folgenden Tabellen vergleichen die Unterstützung für Geräte und andere umleitungen auf das Remote Desktop Connection-app, Universal-app, Android-app, iOS-app, MacOS-app und die Web-Client. Diese Tabellen beziehen sich die umleitungen, die Sie einmal in einer Remotesitzung zugreifen können. 

Wenn Sie eine Remoteverbindung mit Ihrem persönlichen Desktop, stehen zusätzliche umleitungen, die Sie, in konfigurieren können der **zusätzliche Einstellungen** für die Sitzung. Wenn Ihre Remotedesktop oder apps, die von Ihrer Organisation verwaltet werden, kann Ihr Administrator die Funktionen aktivieren oder Deaktivieren von umleitungen, die über gruppenrichtlinieneinstellungen bereitstellen.

### <a name="input-redirection"></a>Geben Sie die Umleitung

| Umleitung | Remotedesktop<br> Verbindung | Universelle | Android | iOS | MacOS | WebClient |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| Tastatur    | X                             | X         | X       | X   | X     | X          |
| Maus       | X                             | X         | X       | X*    | X     | X          |
| Touch       | X                             | X         | X       | X   |       |            |
| Andere       | Stift                           |           |         |     |       |            |
* Anzeigen der [Liste von unterstützten Geräten für die Eingabe für den Remotedesktop-iOS-Beta-Client](remote-desktop-ios.md#supported-input-devices).

### <a name="port-redirection"></a>Portweiterleitung   

| Umleitung | Remotedesktop <br>Verbindung | Universelle | Android | iOS | MacOS | WebClient |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| Seriellen Anschluss | X                             |           |         |     |       |            |
| USB         | X                             |           |         |     |       |            |

Wenn Sie USB-Anschluss-Umleitung aktivieren, werden alle USB-Geräte an den USB-Anschluss automatisch in der Remotesitzung erkannt.

### <a name="other-redirection-devices-etc"></a>Anderen umleitungen (Geräte usw.)



| Umleitung         | Remotedesktopverbindung | Universelle   | Android | iOS         | MacOS                                    | WebClient    |
|---------------------|---------------------------|-------------|---------|-------------|------------------------------------------|---------------|
| Kameras             | X                         |             |         |             |                                          |               |
| Zwischenablage           | X                         | Text, image | Text    | Text, image | X                                        | Text          |
| Lokales Laufwerk/Speicher | X                         |             | X       |             | x                                        |               |
| Pfad            | X                         |             |         |             |                                          |               |
| Mikrofonen         | X                         |X            |         |             | X                                        |               |
| Drucker            | X                         |             |         |             | X (nur CUPS)                            | PDF-Datei drucken     |
| Scanner            | X                         |             |         |             |                                          |               |
| Smartcards         | X                         |             |         |             | X (Windows-Authentifizierung nicht unterstützt) |               |
| Lautsprecher            | X                         | X           | X       | X           | X                                        | X (mit Ausnahme von Internet Explorer) |

* Für die druckerumleitung - unterstützt die MacOS-app den Druckertreiber Verleger Belichter standardmäßig. Sie unterstützen keine systemeigenen Druckertreiber umleiten.
