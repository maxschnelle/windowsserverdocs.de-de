---
title: Erste Schritte mit dem Windows-Desktopclient
description: Grundlegende Informationen zum Windows-Desktopclient.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 09/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: c864ba0e51054a553bfd53f845bd4d1c9ff3c8ba
ms.sourcegitcommit: 61767c405da44507bd3433967543644e760b20aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988238"
---
# <a name="get-started-with-the-windows-desktop-client"></a>Erste Schritte mit dem Windows-Desktopclient

>Gilt für: Windows 10 und Windows 7

Du kannst den Remotedesktopclient für Windows-Desktop verwenden, um Windows-Apps und -Desktops über ein anderes Windows-Gerät per Remotezugriff zu nutzen.

> [!NOTE]
> - Diese Dokumentation bezieht sich nicht auf den Remotedesktopverbindungs-Client (MSTSC), der mit Windows geliefert wird. Sie bezieht sich auf den neuen Remotedesktopclient (MSRDC).
> - Dieser Client unterstützt derzeit nur den Zugriff auf Remote-Apps und -Desktops aus dem [virtuellen Windows-Desktop](https://aka.ms/wvd).
> - Möchtest du mehr über die neuen Versionen für den Windows-Desktopclient erfahren? [Neuigkeiten im Windows-Desktopclient](windowsdesktop-whatsnew.md) ansehen

## <a name="install-the-client"></a>Installieren des Clients

Derzeit kannst du den Client für Windows 64-Bit herunterladen. Wir aktualisieren diese Liste, sobald der Client für weitere Versionen von Windows verfügbar wird.

- [Windows 64-Bit-Client](https://go.microsoft.com/fwlink/?linkid=2068602)

Du kannst den Client für den aktuellen Benutzer installieren – dafür sind keine Administratorrechte erforderlich –, oder dein Administrator kann den Client installieren und ihn so konfigurieren, dass alle Benutzer des Geräts darauf zugreifen können.

Nach der Installation kann der Client aus dem Startmenü gestartet werden, der Suchbegriff dazu ist **Remotedesktop**.

## <a name="feeds"></a>Feeds

Rufe die Liste der verwalteten Ressourcen ab, auf die du Zugriff hast, wie etwa Apps und Desktops, indem du den Feed abonnierst, den dir dein Administrator bereitgestellt hat. Wenn du abonnierst, werden die Ressourcen auf deinem lokalen PC verfügbar. Der Windows-Desktopclient unterstützt aktuell Ressourcen, die vom virtuellen Windows-Desktop veröffentlicht wurden.

### <a name="subscribe-to-a-feed"></a>Abonnieren eines Feeds

1. Tippe auf der Hauptseite des Clients, die auch als Connection Center bezeichnet wird, auf **Abonnieren**.
2. Melde dich bei entsprechender Aufforderung mit deinem Benutzerkonto an.
3. Die Ressourcen werden im Connection Center nach Arbeitsbereich gruppiert angezeigt.

Du kannst Ressourcen mit einer der folgenden Methoden starten:

- Wechsle zum Connection Center, und doppelklicke auf eine Ressource, um sie zu starten.
- Alternativ kannst du zum Startmenü navigieren und nach einem Ordner mit dem Namen des Arbeitsbereichs suchen oder den Namen der Ressource in die Suchleiste eingeben.

### <a name="workspace-details"></a>Arbeitsbereichsdetails

Nach dem Abonnieren kannst du weitere Informationen zu einem Arbeitsbereich im Bereich „Details“ anzeigen:

- Den Namen des Arbeitsbereichs
- Die zum Abonnieren verwendete URL und den Benutzernamen
- Die Anzahl der Apps und Desktops
- Datum/Uhrzeit der letzten Aktualisierung
- Den Status der letzten Aktualisierung

Zugriff auf den Bereich „Details“:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben dem Arbeitsbereich.
2. Wähle im Dropdownmenü **Details** aus.
3. Der Bereich „Details“ wird auf der rechten Seite des Clients angezeigt.

Nachdem du abonniert hast, wird der Arbeitsbereich automatisch regelmäßig aktualisiert. Da bei können Ressourcen hinzugefügt, geändert oder entfernt werden, basierend auf Änderungen, die von deinem Administrator vorgenommen werden.

Du kannst bei Bedarf auch manuell nach Aktualisierungen suchen, indem du im Detailbereich **Jetzt aktualisieren** auswählst.

### <a name="unsubscribe-from-a-feed"></a>Kündigen des Abonnements eines Feeds

In diesem Abschnitt erfährst du, wie du das Abonnement eines Feeds beendest. Du kannst das Abonnement beenden, um entweder erneut mit einem anderen Konto zu abonnieren oder um deine Ressourcen vom System zu entfernen.

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben dem Arbeitsbereich.
2. Wähle im Dropdownmenü **Abonnement kündigen** aus.
3. Überprüfe das Dialogfeld, und wähle **Fortfahren** aus.

## <a name="update-the-client"></a>Update des Clients

Wenn dies nicht von deinem Administrator deaktiviert wurde, wirst du benachrichtigt, wenn eine neue Version des Clients verfügbar ist. Diese Benachrichtigung wird entweder direkt im Connection Center oder im Windows Action Center angezeigt. Wähle die Benachrichtigung aus, um den Updatevorgang zu starten.

Du kannst außerdem manuell nach neuen Updates für den Client suchen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) in der Befehlsleiste am oberen Rand des Clients.
2. Wähle im Dropdownmenü **Info** aus.
3. Tippe auf **Nach Updates suchen**.
4. Wenn ein Update verfügbar ist, tippe auf **Update installieren**, um ein Update des Clients auszuführen.

## <a name="providing-feedback"></a>Abgeben von Feedback

Hast du einen Vorschlag für eine Funktion, oder möchtest du ein Problem melden? Teile es uns über den [Feedback-Hub](feedback-hub://?tabid=2&contextid=883) mit, auf den du auch vom Client aus zugreifen kannst:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) in der Befehlsleiste am oberen Rand des Clients.
2. Wähle im Dropdownmenü **Feedback** aus, um den Feedback-Hub zu öffnen.
