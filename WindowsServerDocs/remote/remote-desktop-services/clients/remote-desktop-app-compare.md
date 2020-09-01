---
title: Remote Desktop – Die Client-Apps im Vergleich
description: Erfahren Sie, wie die verschiedenen Remotedesktop-Apps in Bezug auf die unterstützten Features und Funktionen im Vergleich abschneiden.
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: a44926d50fae9dea38e3f5c46db423991a414a87
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941510"
---
# <a name="compare-the-clients"></a>Vergleichen der Clients

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Wir werden häufig gefragt, wie die verschiedenen Remotedesktopclients im Vergleich abschneiden. Erfüllen Sie alle die gleichen Aufgaben? Hier finden Sie die Antworten auf diese Fragen.

## <a name="redirection-support"></a>Umleitungsunterstützung

Die folgenden Tabellen enthalten einen Vergleich der Unterstützung für Geräte- und andere Umleitungen über die verschiedenen Clients hinweg. In diesen Tabellen werden die Umleitungen aufgeführt, auf die Sie in einer Remotesitzung zugreifen können.

Wenn Sie remote auf Ihren persönlichen Desktop zugreifen, stehen zusätzliche Umleitungen zur Verfügung, die Sie in den **Zusätzlichen Einstellungen** für die Sitzung konfigurieren können. Wenn Ihr Remotedesktop oder Ihre Apps von Ihrer Organisation verwaltet werden, kann Ihr Administrator die Umleitungen über Gruppenrichtlinien- oder RDP-Einstellungen aktivieren oder deaktivieren.

### <a name="input-redirection"></a>Eingabeumleitung

| Umleitung | Windows-Posteingang</br>(MSTSC) | Windows Desktop</br>(MSRDC) | Windows Store | Android | iOS | macOS | Webclient    |
|-------------|---------------------------|-----------------------------|---------------|---------|-----|-------|---------------|
| Tastatur    | X                         | X                           | X             | X       | X   | X     | X             |
| Maus       | X                         | X                           | X             | X       | X\* | X     | X             |
| Touch       | X                         | X                           | X             | X       | X   |       | X (außer IE) |
| Stift         | X                         | X                           |               | X (als Touch) |  X (als Touch)  |       |               |

*Sehen Sie sich die Liste der [unterstützten Eingabegeräte](remote-desktop-ios.md#supported-input-devices) für den Remotedesktopclient für iOS an.

### <a name="port-redirection"></a>Anschlussumleitung

| Umleitung | Windows-Posteingang</br>(MSTSC) | Windows Desktop</br>(MSRDC) | Windows Store | Android | iOS | macOS | Webclient |
|-------------|---------------------------|-----------------------------|---------------|---------|-----|-------|------------|
| Serieller Anschluss | X                         | X                           |               |         |     |       |            |
| USB         | X                         | X                           |               |         |     |       |            |

Wenn Sie die USB-Anschlussumleitung aktivieren, werden alle am USB-Anschluss angeschlossenen USB-Geräte automatisch in der Remotesitzung erkannt.

### <a name="other-redirection-devices-etc"></a>Andere Umleitung (Geräte usw.)

| Umleitung         | Windows-Posteingang</br>(MSTSC) | Windows Desktop</br>(MSRDC) | Windows Store | Android | iOS         | macOS                           | Webclient    |
|---------------------|---------------------------|-----------------------------|---------------|---------|-------------|---------------------------------|---------------|
| Kameras             | X                         | X                           |               |     X    |   X         | X                               |               |
| Zwischenablage           | X                         | X                           | X             | Text    | Text, Bilder | X                               | Text          |
| Lokales Laufwerk/lokaler Speicher | X                         | X                           |               | X       |   X        | X                               |               |
| Speicherort            | X                         | X                           |               |         |             |                                 |               |
| Mikrofone         | X                         | X                           | X             |         |  X          | X                               |               |
| Drucker            | X                         | X                           |               |         |             | X (nur CUPS)                   | PDF-Ausgabe     |
| Scanner            | X                         | X                           |               |         |             |                                 |               |
| Smart Cards         | X                         | X                           |               |         |             | X (Windows-Anmeldung wird nicht unterstützt) |               |
| Speakers            | X                         | X                           | X             | X       | X           | X                               | X (außer IE) |

*Druckerumleitung: Die macOS-App unterstützt standardmäßig den Druckertreiber Publisher Imagesetter. Die Umleitung nativer Druckertreiber wird nicht unterstützt.
