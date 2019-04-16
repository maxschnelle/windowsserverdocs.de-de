---
title: Zugriff auf den Remotedesktop-Webclient
description: Beschreibt, wie der Remotedesktop-Webclient anmelden.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/20/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: f4433ad592219d6ed15b28fd0514790b078525fd
ms.sourcegitcommit: d5f10c0c98a9976a86be9f4fa8866650c7fcfc1a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "9065857"
---
# Zugriff auf den Remotedesktop-Webclient

Der Remotedesktop-Webclient können Sie einen kompatible Webbrowser Ihrer Organisation remote Zugriff auf Ressourcen (apps und Desktops) veröffentlicht, die Sie von Ihrem Administrator. Sie sehen möglicherweise von für die Interaktion mit der remote-apps und Desktops, wie Sie mit einem lokalen PC unabhängig davon, wo Sie sind ohne zu einem anderen desktop-PC zu wechseln. Nachdem Ihr Administrator die remote-Ressourcen einrichtet wird, Sie müssen, lediglich sind, Ihre Domäne, Benutzername und Kennwort, die vom Administrator gesendet, die Sie, einen unterstützten Web-Browser-URL, und Sie sind startklar.

>[!NOTE]
>Mehr über die neuen Versionen für WebClient? Sehen Sie sich [Neues für Remotedesktop-Webclient?](web-client-whatsnew.md)

## Was müssen Sie der Web-Client

* Für den WebClient benötigen Sie einen PC mit Windows, MacOS, Linux oder ChromeOS. Mobile Geräte werden zu diesem Zeitpunkt nicht unterstützt.
* Einem modernen Browser wie Microsoft Edge, Internet Explorer 11, Google Chrome, Safari oder Mozilla Firefox (v55.0 und höher).
* Die URL der Administrator hat Ihnen gesendet.

>[!NOTE]
>Die Internet Explorer-Version des Webclients Audio zu diesem Zeitpunkt keinen.
>Safari möglicherweise einen grauen Bildschirm angezeigt, wenn der Browser die Größe geändert wird oder Vollbild mehrmals eingibt.

## Verwenden des Remotedesktop-Clients

Sie gesendet haben, melden Sie sich an den Client, gehen auf die URL den Administrator. Geben Sie auf der Anmeldeseite Ihrer Domäne und Benutzername im Format ```DOMAIN\username```, geben Sie Ihr Kennwort ein, und wählen Sie dann **Anmelden**.

>[!NOTE]
>Durch Anmeldung bei des Webclients, bestätigen Sie, dass Ihr PC Sicherheitsrichtlinie Ihrer Organisation entspricht.

Nachdem Sie sich anmelden, der Client gelangen Sie zum der Registerkarte " **Alle Ressourcen** " enthält alle Elemente, die Ihnen unter einer oder mehreren reduzierbares Gruppen, z. B. die Gruppe "Arbeitsressourcen" veröffentlicht. Sehen Sie mehrere Symbole für die apps, Desktops, oder Ordner mit mehr apps oder Desktops, die der Administrator für der Arbeitsgruppe verfügbar gemacht wurde. Sie können auf dieser Registerkarte zu einem beliebigen Zeitpunkt, um zusätzliche Ressourcen zu starten zurückkehren.

Um mit einer app oder den Desktop, wählen Sie das Element, das Sie verwenden möchten, geben Sie die gleichen Benutzername und Kennwort, die Sie verwendet haben, melden Sie sich an den Webclient, wenn Sie dazu aufgefordert werden, und wählen Sie dann **übermitteln**. Sie können auch ein Zustimmungsdialogfeld Zugriff auf lokale Ressourcen, z. B. Zwischenablage und Drucker angezeigt werden. Sie können auch nicht einer der beider umgeleitet, oder wählen **Zulassen** , um die Standardeinstellungen zu verwenden. Warten Sie, bis des Webclients zum Herstellen der Verbindung, und starten Sie dann mit der Ressource wie gewohnt.

Wenn Sie fertig sind, können Sie Ihre Sitzung beenden Sie die Schaltfläche " **Abmelden** " in der Symbolleiste am oberen Bildschirmrand auswählen oder im Browser-Fenster zu schließen.

## Das Drucken über den Remotedesktop-Webclient

In der Webclient druckt, gehen Sie wie folgt vor:

1. Starten Sie den Druckvorgang wie gewohnt für die app, die Sie verwenden aus drucken möchten.
2. Wenn aufgefordert, einen Drucker auszuwählen, wählen Sie **Remote Desktop virtuellen Drucker**.
3. Wählen Sie nach dem auswählen die Voreinstellungen **Drucken**.
4. Browser wird eine PDF-Datei mit den Druckauftrag generiert.
5. Sie können entweder die PDF-Datei zu öffnen und seinen Inhalt auf dem lokalen Drucker drucken oder auf Ihrem PC zur späteren Verwendung speichern.

## Kopieren und Einfügen aus der Remotedesktop-Webclient

Der Webclient unterstützt derzeit kopieren und Einfügen von Text. Dateien nicht kopiert oder in und aus dem Webclient eingefügt. Darüber hinaus können Sie nur verwenden **STRG + C** und **STRG + V** kopieren und Einfügen von Text.

## Erhalten Sie Hilfe mit dem Webclient

Wenn Sie ein Problem festgestellt haben, die von den Informationen in diesem Artikel gelöst werden kann, erhalten Sie Hilfe mit dem Webclient per e-Mail die Adresse auf der Webclient Seite "Info".