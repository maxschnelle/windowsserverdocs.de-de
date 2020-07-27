---
title: Remotedesktop-URI-Schema
description: Lerne das Uniform Resource Identifier-Schema für Remotedesktopclients kennen.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 06/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: 50eb7aaa9b8d4d8826f74f2a5338c93dee5d1053
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954072"
---
# <a name="remote-desktop-uri-scheme"></a>Remotedesktop-URI-Schema

> Gilt für: Windows Server, Version 1803, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

In diesem Dokument wird das Format von URIs (Uniform Resource Identifier) für Remotedesktop definiert. Mithilfe dieser URI-Schemas können Remotedesktopclients mit verschiedenen Befehlen aufgerufen werden.

## <a name="ms-rd-uri-scheme"></a>ms-rd-URI-Schema

>[!NOTE]
> Das ms-rd-URI-Schema wird derzeit nur für den Windows-Desktopclient (MSRDC) unterstützt.

Der ms-rd-URI bietet die Option, einen Befehl für den Client und eine Reihe von Parametern anzugeben, die für den Befehl spezifisch sind. Dabei wird folgendes Format verwendet:

```
ms-rd:command?parameters
```

Parameter verwenden das Abfragezeichenfolgen-Format des Schlüssel=Wert-Paars, durch & getrennt, um zusätzliche Informationen für den angegebenen Befehl bereitzustellen:

```
param1=value1&param2=value2&…
```

### <a name="commands-and-parameters"></a>Befehle und Parameter

Hier findest du eine Liste der derzeit unterstützten Befehle und der entsprechenden Parameter.

Bei Verwendung von `ms-rd:` ohne Befehle wird der Client gestartet.

#### <a name="subscribe"></a>Subscribe

Dieser Befehl startet den Client und den Abonnementprozess.

**Befehlsname:** subscribe

**Befehlsparameter:**

| Parameter | Beschreibung                  | Werte |
|-----------|------------------------------|--------|
| URL       | Gibt die Arbeitsbereichs-URL an. | Eine gültige URL, z. B. <https://contoso.com>. |

**Beispiel:** ms-rd:subscribe?url=https://contoso.com

## <a name="legacy-rdp-uri-scheme"></a>Legacy rdp-URI-Schema

>[!NOTE]
> Das folgende URI-Schema wird nur für die Clients für macOS-, iOS- und Android-Geräte unterstützt. Es wird durch den oben stehenden neuen ms-rd-URI ersetzt.

Microsoft-Remotedesktop verwendet das URI-Schema „rdp://Abfragezeichenfolge“ zum Speichern vorkonfigurierter Attributeinstellungen, die beim Starten des Clients verwendet werden. Die Abfragezeichenfolgen stellen ein oder mehrere RDP-Attribute dar, die in der URL bereitgestellt werden.

Die RDP-Attribute werden durch das kaufmännische Und-Zeichen (&) getrennt. Bei einer Verbindung mit einem PC lautet die Zeichenfolge zum Beispiel wie folgt:

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

Diese Tabelle enthält eine vollständige Liste der unterstützten Attribute, die mit dem iOS, Mac und Android Remotedesktopclients verwendet werden kann. (Ein „X“ in der Spalte mit der Plattform gibt an, dass das Attribut unterstützt wird. Die in spitzen Klammern (<>) eingeschlossenen Werte sind die von den Remotedesktopclients unterstützten Werte.)

| RDP-Attribut                                           | Android | Mac | iOS |
|---------------------------------------------------------|---------|-----|-----|
| allow desktop composition=i:&lt;0 oder 1&gt;              | x       | x   | x   |
| allow font smoothing=i:<0 oder 1&gt;                      | x       | x   | x   |
| alternate shell=s:&lt;Zeichenfolge&gt;                        | x       | x   | x   |
| [audiomode=i:&lt;0, 1 oder 2&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393707(v=ws.10)) | x       | x   | x   |
| [authentication level=i:&lt;0 oder 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393709(v=ws.10)) | x       | x   | x   |
| connect to console=i:&lt;0 oder 1&gt;                     | x       | x   | x   |
| disable cursor settings=i:&lt;0 oder 1&gt;                | x       | x   | x   |
| disable full window drag=i:&lt;0 oder 1&gt;               | x       | x   | x   |
| disable menu anims=i:&lt;0 oder 1&gt;                     | x       | x   | x   |
| disable themes=i:&lt;0 oder 1&gt;                         | x       | x   | x   |
| disable wallpaper=i:&lt;0 oder 1&gt;                      | x       | x   | x   |
| [drivestoredirect=s:*](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393728(v=ws.10)) (Dies ist der einzige unterstützte Wert) | x       | x   |     |
| [desktopheight=i:&lt;Wert in Pixeln&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393702(v=ws.10)) |         | x   |     |
| [desktopwidth=i:&lt;Wert in Pixeln&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393697(v=ws.10))  |         | x   |     |
| [domain=s:&lt;Zeichenfolge&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393673(v=ws.10))                 | x | x | x |
| [full address=s:&lt;Zeichenfolge&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393661(v=ws.10))           | x | x | x |
| gatewayhostname=s:&lt;Zeichenfolge&gt;                  | x | x | x |
| [gatewayusagemethod=i:&lt;1 oder 2&gt;](/windows/win32/termserv/imsrdpclienttransportsettings-gatewayusagemethod)                | x | x | x |
| [prompt for credentials on client=i:&lt;0 oder 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393660(v=ws.10)) |   | x |   |
| [loadbalanceinfo=s:&lt;Zeichenfolge&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393684(v=ws.10))                  | x | x | x |
| [redirectprinters=i:&lt;0 oder 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393671(v=ws.10))                 |   | x |   |
| remoteapplicationcmdline=s:&lt;Zeichenfolge&gt;         | x | x | x |
| remoteapplicationmode=i:&lt;0 oder 1&gt;            | x | x | x |
| remoteapplicationprogram=s:&lt;Zeichenfolge&gt;         | x | x | x |
| shell working directory=s:&lt;Zeichenfolge&gt;          | x | x | x |
| Use redirection server name=i:&lt;0 oder 1&gt;      | x | x | x |
| [username=s:&lt;Zeichenfolge&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393678(v=ws.10))                  | x | x | x |
| [screen mode id=i:&lt;1 oder 2&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393692(v=ws.10))            |   | x |   |
| [session bpp=i:&lt;8, 15, 16, 24 oder 32&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393680(v=ws.10)) |   | x |   |
| [use multimon=i:&lt;0 oder 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393695(v=ws.10))              |   | x |   |
