---
title: Erste Schritte mit dem Webclient
description: Hier wird beschrieben, wie du dich beim Remotedesktop-Webclient anmeldest.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 08/27/2019
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 6c37c28fded08ba68e46a10a534ee0269c714938
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "74189470"
---
# <a name="get-started-with-the-web-client"></a>Erste Schritte mit dem Webclient

Der Remotedesktop-Webclient ermöglicht dir, mit einem kompatiblen Webbrowser auf die Remoteressourcen (Apps und Desktops) deiner Organisation zuzugreifen, die dir von deinem Administrator zur Verfügung gestellt werden. Egal wo du dich befindest, kannst du mit den Remote-Apps und -desktops wie mit einem lokalen PC interagieren, ohne zu einem anderen Desktop-PC wechseln zu müssen. Sobald dein Administrator deine Remoteressourcen eingerichtet hat, benötigst du nur noch deine Domäne, deinen Benutzernamen, dein Kennwort, die URL, die dir dein Administrator geschickt hat, und einen unterstützten Webbrowser, und schon kannst du loslegen.

>[!NOTE]
>Möchtest du mehr über die neuen Versionen für den Webclient erfahren? Lies [Neues beim Remotedesktop-Webclient](web-client-whatsnew.md).

## <a name="what-youll-need-to-use-the-web-client"></a>Voraussetzungen für die Verwendung des Webclients

* Für den Webclient benötigst du einen Windows-, macOS-, ChromeOS- oder Linux-PC. Mobile Geräte werden derzeit nicht unterstützt.
* Ein moderner Browser wie Microsoft Edge, Internet Explorer 11, Google Chrome, Safari oder Mozilla Firefox (v55.0 und höher).
* Die URL, die dein Administrator dir gesendet hat.

>[!NOTE]
>Die Internet Explorer-Version des Webclients bietet zu diesem Zeitpunkt keine Audiounterstützung.
>Safari zeigt möglicherweise einen grauen Bildschirm an, wenn der Browser angepasst wird oder mehrmals in den Vollbildmodus wechselt.

## <a name="start-using-the-remote-desktop-client"></a>Erste Schritte bei der Verwendung des Remotedesktopclients

Um dich beim Client anzumelden, öffnest du die URL, die dein Administrator dir gesendet hat. Gib auf der Anmeldeseite deine Domäne und deinen Benutzernamen im Format ```DOMAIN\username``` ein, gib dein Kennwort ein, und wähle dann **Anmelden** aus.

>[!NOTE]
>Indem du dich beim Webclient anmeldest, stimmst du zu, dass dein PC der Sicherheitsrichtlinie deiner Organisation entspricht.

Nachdem du dich angemeldet hast, führt der Client dich zur Registerkarte **Alle Ressourcen**, die unter einer oder mehreren reduzierbaren Gruppen alle für dich veröffentlichten Elemente enthält, z.B. die Gruppe „Arbeit“. Es werden mehrere Symbole angezeigt, die die Apps, Desktops oder Ordner mit weiteren Apps oder Desktops darstellen, die der Administrator der Arbeitsgruppe zur Verfügung gestellt hat. Du kannst jederzeit auf diese Registerkarte zurückgreifen, um zusätzliche Ressourcen zu starten.

Um mit der Verwendung einer App oder eines Desktops zu beginnen, wählst du das Element aus, das du verwenden möchtest, gibst bei Aufforderung den gleichen Benutzernamen und das gleiche Kennwort ein, mit denen du dich beim Webclient angemeldet haben, und wählst dann **Senden** aus. Möglicherweise wird dir auch ein Zustimmungsdialogfeld angezeigt, um auf lokale Ressourcen wie Zwischenablage und Drucker zuzugreifen. Du kannst wählen, nichts davon umzuleiten, oder **Zulassen** auswählen, um die Standardeinstellungen zu verwenden. Warte, bis der Webclient die Verbindung hergestellt hat, und beginne dann mit der Nutzung der Ressource, wie du es normalerweise tun würdest.

Wenn du fertig bist, kannst du deine Sitzung beenden, indem du entweder die Schaltfläche **Abmelden** in der Symbolleiste oben auf deinem Bildschirm auswählst oder das Browserfenster schließt.

## <a name="printing-from-the-remote-desktop-web-client"></a>Drucken über den Remotedesktop-Webclient

So druckst du über den Webclient:

1. Starte wie gewohnt den Druckvorgang für die App, aus der du drucken möchtest.
2. Wähle bei Aufforderung zum Auswählen eines Druckers **Virtueller Remote Desktopdrucker** aus.
3. Wähle nach der Auswahl deiner Einstellungen **Drucken** aus.
4. Dein Browser generiert eine PDF-Datei des Druckauftrags.
5. Du kannst wählen, ob du die PDF-Datei öffnen und ihren Inhalt auf deinem lokalen Drucker ausdrucken oder sie zur späteren Verwendung auf deinem PC speichern möchtest.

## <a name="copy-and-paste-from-the-remote-desktop-web-client"></a>Kopieren und Einfügen über den Remotedesktop-Webclient

Der Webclient unterstützt derzeit nur das Kopieren und Einfügen von Text. Dateien können über den Webclient nicht kopiert oder eingefügt werden. Außerdem kannst du nur mit **STRG+C** und **STRG+V** Text kopieren und einfügen.

## <a name="use-an-input-method-editor-ime-in-the-remote-session"></a>Verwenden eines Eingabemethoden-Editors in der Remotesitzung

Zur Verwendung eines Eingabemethoden-Editors (IME), um komplexe Zeichen in der Remotesitzung einzugeben, klicken Sie auf das Zahnradsymbol in der Navigationsleiste, um die Seitenleiste **Einstellungen** zu öffnen, und legen Sie die Option **Enable Input Method Editor** (Eingabemethoden-Editor aktivieren) auf **Ein** fest. Sie müssen den Eingabemethoden-Editor in der Remotesitzung installiert und aktiviert haben. 

## <a name="get-help-with-the-web-client"></a>Anfordern von Hilfe zum Webclient

Wenn ein Problem aufgetreten ist, das mit den Informationen in diesem Artikel nicht behoben werden kann, kannst du Hilfe zum Webclient erhalten, indem du eine E-Mail an die Adresse auf der Info-Seite des Webclients sendest.
