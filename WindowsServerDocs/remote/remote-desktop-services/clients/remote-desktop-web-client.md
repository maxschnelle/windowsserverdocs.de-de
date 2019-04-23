---
title: Zugriff auf den Remotedesktop-Webclient
description: Beschreibt, wie Sie sich an den WebClient Remote Desktop angemeldet.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/20/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: f4433ad592219d6ed15b28fd0514790b078525fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849371"
---
# <a name="access-the-remote-desktop-web-client"></a>Zugriff auf den Remotedesktop-Webclient

Der Webclient Remotedesktop können Sie einen kompatiblen Webbrowser Ihres Unternehmens (apps und Desktops) veröffentlicht, die Sie von Ihrem Administrator den Zugriff auf Remoteressourcen Sie werden möglicherweise von für die Interaktion mit dem remote-apps und Desktops, wie Sie mit einem lokalen PC unabhängig davon, wo Sie sind ohne zu einem anderen desktop-PC zu wechseln. Sobald Ihr Administrator die Remoteressourcen eingerichtet hat, wird alles, was, die Sie benötigen, werden, Ihre Domäne, Benutzername, Kennwort, die URL Ihren Administrator gesendet, Sie und einen unterstützten Webbrowser, und Sie können alles in Ordnung.

>[!NOTE]
>Möchten Sie wissen zu den neuen Versionen für den WebClient? Sehen Sie sich [Neuigkeiten für Remote Desktop WebClient?](web-client-whatsnew.md)

## <a name="what-youll-need-to-use-the-web-client"></a>Was Sie benötigen, verwenden Sie den WebClient

* Für den WebClient benötigen Sie einen PC unter Windows, MacOS, ChromeOS oder Linux. Mobile Geräte werden zurzeit nicht unterstützt.
* Einem modernen Browser wie Microsoft Edge, Internet Explorer 11, Google Chrome, Mozilla Firefox oder Safari (v55.0 und höher).
* Die URL Ihr Administrator hat Ihnen gesendet.

>[!NOTE]
>Die Internet Explorer-Version des Webclients Audio zu diesem Zeitpunkt keinen.
>Safari möglicherweise einen grauen Bildschirm angezeigt, wenn der Browser angepasst wird, oder geben Sie im Vollbildmodus mehrmals.

## <a name="start-using-the-remote-desktop-client"></a>Starten Sie mit dem Remotedesktop-client

Melden Sie sich an den Client, öffnen die URL Ihren Administrator, die Sie gesendet. Geben Sie auf der Anmeldeseite Ihrer Domäne und den Namen im Format ```DOMAIN\username```, geben Sie Ihr Kennwort ein, und wählen Sie dann **Anmeldung**.

>[!NOTE]
>Indem Sie sich anmelden, an den Webclient, stimmen Sie zu, dass Ihr PC mit der Sicherheitsrichtlinie Ihrer Organisation entspricht.

Nachdem Sie sich angemeldet haben, der Client gelangen Sie auf die **alle Ressourcen** Registerkarte, die alle Elemente enthält, die Ihnen unter einer oder mehreren reduzierbare Gruppen, z. B. die Gruppe "Arbeit" veröffentlicht. Sie werden sehen, dass mehrere Symbolen zur Darstellung der apps, Desktops oder Ordner, die mehr apps oder -Desktops, die der Administrator der Gruppe "Arbeit" zur Verfügung gestellt hat. Sie können auf dieser Registerkarte zu einem beliebigen Zeitpunkt aus, um zusätzliche Ressourcen starten zurückkehren.

Nutzen Sie eine app oder den Desktop, wählen Sie das Element, das Sie verwenden möchten, geben den gleichen Benutzernamen und Kennwort für die Anmeldung an den Webclient, wenn Sie aufgefordert werden, und wählen Sie dann **senden**. Sie können auch ein Zustimmungsdialogfeld Zugriff auf lokale Ressourcen, z. B. Clipboard "und" Drucker angezeigt werden. Sie können nicht eines dieser umleiten, oder wählen Sie auch **zulassen** auf die Standardeinstellungen verwenden. Warten Sie, bis des Webclients zum Herstellen der Verbindung, und starten Sie dann mit der Ressource, wie gewohnt.

Wenn Sie fertig sind, können Sie die Sitzung beenden, durch Drücken der **Abmelden** Schaltfläche auf der Symbolleiste am oberen Rand den Bildschirm oder das Browserfenster schließen.

## <a name="printing-from-the-remote-desktop-web-client"></a>Drucken über den Remotedesktopclient für web

So drucken Sie vom WebClient, gehen Sie wie folgt vor:

1. Starten Sie den Druckvorgang, wie gewohnt für die app verwenden, die Sie drucken möchten.
2. Wählen Sie bei Aufforderung zum Auswählen eines Druckers **Remote Desktop virtuellen Drucker**.
3. Wählen Sie nach der Auswahl Ihrer Einstellungen **Drucken**.
4. Ihr Browser wird eine PDF-Datei des Druckauftrags generiert.
5. Sie können auswählen, die PDF-Datei zu öffnen und seinen Inhalt auf dem lokalen Drucker drucken oder speichern Sie es auf Ihrem PC für die spätere Verwendung.

## <a name="copy-and-paste-from-the-remote-desktop-web-client"></a>Kopieren Sie aus der Remotedesktop-Webclient

Der Webclient unterstützt derzeit kopieren und Einfügen von nur-Text. Dateien nicht kopiert oder eingefügt, und vom WebClient. Darüber hinaus können Sie nur **STRG + C** und **STRG + V** kopieren und Einfügen von Text.

## <a name="get-help-with-the-web-client"></a>Hilfe bei der WebClient

Wenn Sie ein Problem aufgetreten ist, die von den Informationen in diesem Artikel nicht gelöst werden kann, erhalten Sie Hilfe mit dem Webclient per e-Mail an die Adresse auf der Seite "Info" des Webclients.