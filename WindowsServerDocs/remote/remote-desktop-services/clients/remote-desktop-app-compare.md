---
title: Remote Desktop – Die Clients im Vergleich
description: Erfahren Sie, wie die verschiedenen Remotedesktopclients in Bezug auf die unterstützten Features und Funktionen im Vergleich abschneiden.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 03/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 11c91ac951db27915d9313f7f98e5e2cfc56b726
ms.sourcegitcommit: 78c00944b6990702d28bdcc4a9215927ca901bfb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80440373"
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
| Stift         | X                         | X                           |               |         |     |       |               |

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
| Kameras             | X                         | X                           |               |         |             | X                               |               |
| Zwischenablage           | X                         | X                           | X             | Text    | Text, Bild | X                               | Text          |
| Lokales Laufwerk/lokaler Speicher | X                         | X                           |               | X       |             | X                               |               |
| Speicherort            | X                         | X                           |               |         |             |                                 |               |
| Mikrofone         | X                         | X                           | X             |         |             | X                               |               |
| Drucker            | X                         | X                           |               |         |             | X (nur CUPS)                   | PDF-Ausgabe     |
| Scanner            | X                         | X                           |               |         |             |                                 |               |
| Smart Cards         | X                         | X                           |               |         |             | X (Windows-Anmeldung wird nicht unterstützt) |               |
| Speakers            | X                         | X                           | X             | X       | X           | X                               | X (außer IE) |

*Druckerumleitung: Die macOS-App unterstützt standardmäßig den Druckertreiber Publisher Imagesetter. Die Umleitung nativer Druckertreiber wird nicht unterstützt.
