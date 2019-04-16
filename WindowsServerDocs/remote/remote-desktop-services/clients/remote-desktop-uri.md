---
title: Remotedesktopclients URI-Schema
description: Enthält Informationen Sie zu den URI-Schema für Remotedesktop-clients
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2934fed43c8f4feec2f321d684cc3593933eb5d
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297469"
---
# Remotedesktopclient Universal Resource Identifier (URI)-Schema unterstützen

>Gilt für: WindowsServer, Version 1803, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Ein Uniform Resource Identifier (URI)-Schema aktivieren ermöglicht es IT-Experten und Entwickler, die Features der Remotedesktopclients über Plattformen hinweg integrieren und verbessert die benutzerfreundlichkeit, indem zugelassen wird: 

- Drittanbieter-Anwendungen zu Microsoft-Remotedesktop und Sie starten Remotesitzungen mit vordefinierten Einstellungen (als Teil der URI-Zeichenfolge bereitgestellt).
- Endbenutzer Remoteverbindungen mit vorkonfigurierten URLs zu starten.

>[!NOTE]
> Mithilfe eines URI Verbindung zu den Remotedesktopclient wird für Windows-Betriebssystemen nicht unterstützt: Verwenden Sie den URI mit MacOS, iOS und Android-Geräte.

Microsoft-Remotedesktop verwendet das URI-Schema Rdp://query_string vorkonfigurierten Attribut Einstellungen zu speichern, die verwendet werden, wenn den Client zu starten. Die Abfragezeichenfolgen Single und RDP-Attribute, die zur Verfügung gestellt, in der URL dargestellt werden. 

Die RDP-Attribute werden durch das kaufmännische und-Zeichen (&) getrennt. Bei der Verbindung mit einem PC ist z. B. die Zeichenfolge:

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

Diese Tabelle enthält eine vollständige Liste der unterstützten Attribute, die mit der iOS-, Mac- und Android Remotedesktopclients verwendet werden kann. (Ein "X" in der Spalte "Plattform" gibt an, dass das Attribut unterstützt wird. Die Werte gekennzeichnet durch ausgeblendete (<>) stellen die Werte, die von den Remotedesktop-Clients unterstützt werden.)

| **RDP-Attribut**                                           | **Android** | **Mac** | **iOS** |
|---------------------------------------------------------|---------|-----|-----|
| Zulassen von desktop-Komposition = i:&lt;0 oder 1&gt;                    | x       | x   | x   |
| Schriftart Glätten zulassen = I:<0 oder 1&gt;                         | x       | x   | x   |
| alternativen Shell = s:&lt;Zeichenfolge&gt;                              | x       | x   | x   |
| [Audiomode = i:&lt;0, 1 oder 2&gt;](https://technet.microsoft.com/library/ff393707.aspx)                                | x       | x   | x   |
| [Authentifizierungsebene = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393709.aspx)                         | x       | x   | x   |
| Verbindung zur Konsole = i:&lt;0 oder 1&gt;                           | x       | x   | x   |
| Cursor-Einstellungen deaktivieren = i:&lt;0 oder 1&gt;                      | x       | x   | x   |
| Deaktivieren des Fensterinhalts = i:&lt;0 oder 1&gt;                     | x       | x   | x   |
| Deaktivieren Sie im Menü Anims = i:&lt;0 oder 1&gt;                           | x       | x   | x   |
| Designs deaktivieren = i:&lt;0 oder 1&gt;                               | x       | x   | x   |
| Hintergrundbild deaktivieren = i:&lt;0 oder 1&gt;                            | x       | x   | x   |
| [Drivestoredirect = s: *](https://technet.microsoft.com/library/ff393728(v=ws.10).aspx) (Dies ist der einzige unterstützte Wert) | x       | x   |     |
| [Desktopheight = i:&lt;Wert in Pixel&gt;](https://technet.microsoft.com/library/ff393702.aspx)                       |         | x   |     |
| [Desktopwidth = i:&lt;Wert in Pixel&gt;](https://technet.microsoft.com/library/ff393697.aspx)                        |         | x   |     |
| [Domäne = s:&lt;Zeichenfolge&gt;](https://technet.microsoft.com/library/ff393673.aspx)                           | x | x | x |
| [vollständige Adresse = s:&lt;Zeichenfolge&gt;](https://technet.microsoft.com/library/ff393661.aspx)                     | x | x | x |
| Gatewayhostname = s:&lt;Zeichenfolge&gt;                  | x | x | x |
| [Gatewayusagemethod = i:&lt;1 oder 2&gt;](https://msdn.microsoft.com/aa381329.aspx)               | x | x | x |
| [Aufforderung zur Eingabe der Anmeldeinformationen auf Client = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393660(v=ws.10).aspx) |   | x |   |
| [Loadbalanceinfo = s:&lt;Zeichenfolge&gt;](https://technet.microsoft.com/library/ff393684.aspx)                  | x | x | x |
| [Redirectprinters = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393671(v=ws.10).aspx)                 |   | x |   |
| Remoteapplicationcmdline = s:&lt;Zeichenfolge&gt;         | x | x | x |
| Remoteapplicationmode = i:&lt;0 oder 1&gt;            | x | x | x |
| Remoteapplicationprogram = s:&lt;Zeichenfolge&gt;         | x | x | x |
| Shell-Arbeitsverzeichnis = s:&lt;Zeichenfolge&gt;          | x | x | x |
| Verwendung Umleitung Servername = i:&lt;0 oder 1&gt;      | x | x | x |
| [Benutzername = s:&lt;Zeichenfolge&gt;](https://technet.microsoft.com/library/ff393678.aspx)                         | x | x | x |
| [Bildschirm Mode Id = i:&lt;1 oder 2&gt;](https://technet.microsoft.com/library/ff393692.aspx)                   |   | x |   |
| [Sitzung Bpp = i:&lt;8, 15, 16, 24 oder 32&gt;](https://technet.microsoft.com/library/ff393680.aspx)        |   | x |   |
| [Verwenden Sie Multimon = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393695(v=ws.10).aspx)          |   | x |   |