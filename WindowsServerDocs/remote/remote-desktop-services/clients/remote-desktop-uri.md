---
title: URI-Schema des Remotedesktopclients
description: Weitere Informationen Sie zu den Uniform Resource Identifier-Schema für Remotedesktopclients
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
ms.openlocfilehash: 86de6468e2fa45c976711aef43a1a274e04498d3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870501"
---
# <a name="remote-desktop-client-universal-resource-identifier-uri-scheme-support"></a>Remotedesktopclient Universal Resource Identifier (URI)-Schema unterstützen.

>Gilt für: Windows Server, Version 1803, Windows Server 2016, Windows Server 2012 R2

Durch Aktivierung eines URI-Schemas (Uniform Resource Identifier) können IT-Experten und Entwickler Features der Remotedesktopclients über Plattformen hinweg integrieren und die Benutzerfreundlichkeit verbessern, da diese Integration Folgendes ermöglicht: 

- Anwendungen von Drittanbietern können Microsoft Remotedesktop starten und Remotesitzungen mit vordefinierten Einstellungen (die als Teil der URI-Zeichenfolge bereitgestellt werden) einrichten.
- Endbenutzer können Remoteverbindungen über vorkonfigurierte URLs starten.

>[!NOTE]
> Mithilfe eines URI für den Remotedesktop-Client die Verbindung wird für Windows-Betriebssystemen nicht unterstützt – verwenden Sie den URI mit MacOS, iOS und Android-Geräte.

Microsoft Remotedesktop verwendet das URI-Schema-Rdp://query_string zum Speichern von vorkonfigurierter attributeinstellungen, die beim Starten des Clients verwendet werden. Die Abfragezeichenfolgen stellen ein oder mehrere RDP-Attribute dar, die in der URL bereitgestellt werden. 

Die RDP-Attribute werden durch das kaufmännische Und-Zeichen (&) getrennt. Bei einer Verbindung mit einem PC lautet die Zeichenfolge zum Beispiel wie folgt:

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

Diese Tabelle enthält eine vollständige Liste der unterstützten Attribute, die mit dem iOS, Mac und Android Remotedesktopclients verwendet werden kann. (Ein "X" in der Spalte mit der Plattform gibt an, dass das Attribut unterstützt wird. Die in spitzen Klammern (<>) eingeschlossenen Werte sind die von den Remotedesktopclients unterstützten Werte.)

| **RDP-Attribut**                                           | **Android** | **Mac** | **iOS** |
|---------------------------------------------------------|---------|-----|-----|
| desktopgestaltung zulassen = i:&lt;0 oder 1&gt;                    | x       | x   | x   |
| schriftartglättung zulassen = i: < 0 oder 1&gt;                         | x       | x   | x   |
| Alternative Shell = s:&lt;Zeichenfolge&gt;                              | x       | x   | x   |
| [audiomode=i:&lt;0, 1, or 2&gt;](https://technet.microsoft.com/library/ff393707.aspx)                                | x       | x   | x   |
| [Authentication Level = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393709.aspx)                         | x       | x   | x   |
| mit Konsole verbinden = i:&lt;0 oder 1&gt;                           | x       | x   | x   |
| Deaktivieren Cursor Settings = i:&lt;0 oder 1&gt;                      | x       | x   | x   |
| Deaktivieren des Fensterinhalts = i:&lt;0 oder 1&gt;                     | x       | x   | x   |
| Deaktivieren Sie im Menü Anims = i:&lt;0 oder 1&gt;                           | x       | x   | x   |
| Deaktivieren von Themes = i:&lt;0 oder 1&gt;                               | x       | x   | x   |
| Deaktivieren Wallpaper = i:&lt;0 oder 1&gt;                            | x       | x   | x   |
| [drivestoredirect=s:*](https://technet.microsoft.com/library/ff393728(v=ws.10).aspx) (Dies ist der einzige unterstützte Wert) | x       | x   |     |
| [Desktopheight = i:&lt;Wert in Pixel&gt;](https://technet.microsoft.com/library/ff393702.aspx)                       |         | x   |     |
| [desktopwidth=i:&lt;value in pixels&gt;](https://technet.microsoft.com/library/ff393697.aspx)                        |         | x   |     |
| [domain=s:&lt;string&gt;](https://technet.microsoft.com/library/ff393673.aspx)                           | x | x | x |
| [vollständige Adresse = s:&lt;Zeichenfolge&gt;](https://technet.microsoft.com/library/ff393661.aspx)                     | x | x | x |
| gatewayhostname=s:&lt;string&gt;                  | x | x | x |
| [gatewayusagemethod=i:&lt;1 or 2&gt;](https://msdn.microsoft.com/aa381329.aspx)               | x | x | x |
| [Eingabeaufforderung zu Anmeldeinformationen auf dem Client = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393660(v=ws.10).aspx) |   | x |   |
| [loadbalanceinfo=s:&lt;string&gt;](https://technet.microsoft.com/library/ff393684.aspx)                  | x | x | x |
| [Redirectprinters = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393671(v=ws.10).aspx)                 |   | x |   |
| remoteapplicationcmdline=s:&lt;string&gt;         | x | x | x |
| remoteapplicationmode=i:&lt;0 or 1&gt;            | x | x | x |
| remoteapplicationprogram=s:&lt;string&gt;         | x | x | x |
| Arbeitsverzeichnis für die Shell = s:&lt;Zeichenfolge&gt;          | x | x | x |
| Verwenden Redirection Servername = i:&lt;0 oder 1&gt;      | x | x | x |
| [username=s:&lt;string&gt;](https://technet.microsoft.com/library/ff393678.aspx)                         | x | x | x |
| [Anzeige-Modus-Id = i:&lt;1 oder 2&gt;](https://technet.microsoft.com/library/ff393692.aspx)                   |   | x |   |
| [Session Bpp = i:&lt;8, 15, 16, 24 oder 32&gt;](https://technet.microsoft.com/library/ff393680.aspx)        |   | x |   |
| [Verwenden Sie Multimon = i:&lt;0 oder 1&gt;](https://technet.microsoft.com/library/ff393695(v=ws.10).aspx)          |   | x |   |