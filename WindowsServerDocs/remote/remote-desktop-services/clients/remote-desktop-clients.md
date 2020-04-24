---
title: Remotedesktopclients
description: Hier erfährst du mehr über die verschiedenen Remotedesktopclients, die für deine Geräte verfügbar sind.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: b7d8158c-aee1-4c60-8a46-40ce5595b8e8
author: HeidiLohr
manager: lizross
ms.author: helohr
ms.date: 01/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 711fa87fe697ae616d9bd8c696d29fabf1586055
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80856043"
---
# <a name="remote-desktop-clients"></a>Remotedesktopclients

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Mit dem Microsoft-Remotedesktopclient kannst du praktisch von überall aus und mit fast jedem Gerät eine Verbindung mit einem Remote-PC und deinen Arbeitsressourcen herstellen. Sie können eine Verbindung mit Ihrem Arbeits-PC herstellen und haben Zugriff auf alle Ihre Apps, Dateien und Netzwerkressourcen, als säßen Sie direkt an Ihrem Schreibtisch. Sie können Apps am Arbeitsplatz geöffnet lassen und dann zu Hause über den Remotedesktopclient dieselben Apps nutzen.

Bevor du beginnst, lies den Artikel [unterstützte Konfiguration](remote-desktop-supported-config.md), der die PCs aufführt, mit denen du über Remotedesktopclients eine Verbindung herstellen kannst. Sieh dir ebenfalls die [Client-FAQ](remote-desktop-client-faq.md) an.

Die folgenden Client-Apps sind verfügbar:

| Gerät          | Abrufen der App                                                                                                  | Setupanleitung                                                                |
|-----------------|-----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| Windows Desktop | [Windows Desktop-Client](windowsdesktop.md#install-the-client)                                               | [Erste Schritte mit dem Windows-Desktop-Client](windowsdesktop.md) |
| Windows Store   | [Windows 10-Client im Microsoft Store](https://go.microsoft.com/fwlink/?LinkID=616709)                   | [Erste Schritte mit dem Windows Store-Client](windows.md)          |
| Android         | [Android-Client in Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)     | [Erste Schritte mit dem Android-Client](remote-desktop-android.md) |
| iOS             | [iOS-Client im iTunes Store](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)     | [Erste Schritte mit dem iOS-Client](remote-desktop-ios.md)         |
| macOS           | [macOS-Client im iTunes Store](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12) | [Erste Schritte mit dem macOS-Client](remote-desktop-mac.md)       |

## <a name="configuring-the-remote-pc"></a>Konfigurieren des Remote-PC

Um deinen Remotecomputer vor dem Remotezugriff zu konfigurieren [lass den Zugriff auf deinen PC zu](remote-desktop-allow-access.md).

## <a name="remote-desktop-client-uri-scheme"></a>Remotedesktopclient-URI Schema

Du kannst Features von Remotedesktopclients plattformübergreifend integrieren, indem du ein URI-Schema (Uniform Resource Identifier) aktivierst. Sieh dir die [unterstützten URI-Attribute](remote-desktop-uri.md) an, die du mit den iOS-, Mac- und Android-Clients verwenden kannst.
