---
title: Remote Desktop – Die Client-Apps im Vergleich
description: Erfahren Sie, wie die verschiedenen Remotedesktop-Apps in Bezug auf die unterstützten Features und Funktionen im Vergleich abschneiden.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 237bb79fae6460bc3b31fb1753e2d679c8d67512
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404165"
---
# <a name="compare-the-client-apps"></a>Die Client-Apps im Vergleich

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Wir werden häufig gefragt, wie die verschiedenen Remotedesktopclient-Apps im Vergleich abschneiden. Erfüllen Sie alle die gleichen Aufgaben? Hier finden Sie die Antworten auf diese Fragen.

## <a name="redirection-support"></a>Umleitungsunterstützung

In den folgenden Tabellen wird die Unterstützung für Geräte und andere Umleitungen von den folgenden Komponenten verglichen: Remotedesktopverbindungs-App, universelle App, Android-App, iOS-App, macOS-App und Webclient. In diesen Tabellen werden die Umleitungen aufgeführt, auf die Sie in einer Remotesitzung zugreifen können. 

Wenn Sie remote auf Ihren persönlichen Desktop zugreifen, stehen zusätzliche Umleitungen zur Verfügung, die Sie in den **Zusätzlichen Einstellungen** für die Sitzung konfigurieren können. Wenn Ihr Remotedesktop oder Ihre Apps von Ihrer Organisation verwaltet werden, kann Ihr Administrator die Umleitungen über Gruppenrichtlinieneinstellungen aktivieren oder deaktivieren.

### <a name="input-redirection"></a>Eingabeumleitung

| Umleitung | Remotedesktop<br> Verbindung | Universelle | Android | iOS | macOS |          Webclient           |
|-------------|-------------------------------|-----------|---------|-----|-------|-------------------------------|
|  Tastatur   |               X               |     X     |    X    |  X  |   X   |               X               |
|    Maus    |               X               |     X     |    X    | X\* |   X   |               X               |
|    Touch    |               X               |     X     |    X    |  X  |       | X (Edge und IE werden nicht unterstützt.) |
|    Andere    |              Stift              |           |         |     |       |                               |

*Sehen Sie sich die Liste der [unterstützten Eingabegeräte](remote-desktop-ios.md#supported-input-devices) für den Remotedesktop-Beta-Client für iOS an.

### <a name="port-redirection"></a>Anschlussumleitung   

| Umleitung | Remotedesktop <br>Verbindung | Universelle | Android | iOS | macOS | Webclient |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| Serieller Anschluss | X                             |           |         |     |       |            |
| USB         | X                             |           |         |     |       |            |

Wenn Sie die USB-Anschlussumleitung aktivieren, werden alle am USB-Anschluss angeschlossenen USB-Geräte automatisch in der Remotesitzung erkannt.

### <a name="other-redirection-devices-etc"></a>Andere Umleitung (Geräte usw.)



| Umleitung         | Remotedesktopverbindung | Universelle   | Android | iOS         | macOS                                    | Webclient    |
|---------------------|---------------------------|-------------|---------|-------------|------------------------------------------|---------------|
| Kameras             | X                         |             |         |             |                                          |               |
| Zwischenablage           | X                         | Text, Bild | Text    | Text, Bild | X                                        | Text          |
| Lokales Laufwerk/lokaler Speicher | X                         |             | X       |             | x                                        |               |
| Pfad            | X                         |             |         |             |                                          |               |
| Mikrofone         | X                         |X            |         |             | X                                        |               |
| Drucker            | X                         |             |         |             | X (nur CUPS)                            | PDF-Ausgabe     |
| Scanner            | X                         |             |         |             |                                          |               |
| Smartcards         | X                         |             |         |             | X (Windows-Authentifizierung wird nicht unterstützt.) |               |
| Lautsprecher            | X                         | X           | X       | X           | X                                        | X (außer IE) |

*Druckerumleitung: Die macOS-App unterstützt standardmäßig den Druckertreiber Publisher Imagesetter. Die Umleitung nativer Druckertreiber wird nicht unterstützt.
