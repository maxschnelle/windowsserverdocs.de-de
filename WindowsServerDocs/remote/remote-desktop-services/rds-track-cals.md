---
title: Nachverfolgen deiner Remotedesktopdienste-Clientzugriffslizenzen (RDS-CALs)
description: Erfahren Sie, wie Sie Clientzugriffslizenzen (CALs) in Ihrer RDS-Bereitstellung verfolgen können.
ms.topic: article
ms.assetid: 80d82d30-3ad0-4a8c-9a9b-2773c47eee19
author: lizap
ms.author: elizapo
ms.date: 05/11/2017
manager: dongill
ms.openlocfilehash: 7804b0339a9c086a6e68dd83d63b0da5ff292665
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954817"
---
# <a name="track-your-remote-desktop-services-client-access-licenses-rds-cals"></a>Nachverfolgen deiner Remotedesktopdienste-Clientzugriffslizenzen (RDS-CALs)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Sie können mit dem Remotedesktoplizenzierungs-Manager Berichte erstellen, um die Pro Benutzer-Clientzugriffslizenzen für Remotedesktopdienste (Pro Benutzer-RDS-CALs) zu verfolgen, die von einem Remotedesktop-Lizenzserver ausgegeben wurden.

> [!NOTE]
>  Wenn Sie Azure AD Domain Services in Ihrer Umgebung verwenden, funktioniert das Remotedesktoplizenzierungs-Manager-Tool nicht, um Clientzugriffslizenzen pro Benutzer zu erhalten. Stattdessen müssen Sie die Lizenzierung manuell verfolgen, entweder durch Anmeldeereignisse, das Abrufen aktiver Remotedesktopverbindungen über den Verbindungsbroker oder einen anderen Mechanismus, der für Sie geeignet ist.

Führen Sie die folgenden Schritte aus, um einen Bericht für die Clientzugriffslizenz vom Typ „Pro Benutzer“ zu erstellen:

1. Klicken Sie im Remotedesktoplizenzierungs-Manager mit der rechten Maustaste auf den Lizenzserver, klicken Sie auf **Bericht erstellen** und dann auf **Verwendung der Clientzugriffslizenz pro Benutzer**.
2. Legen Sie den Bereich für den Bericht fest. Wählen Sie eine der folgenden Optionen aus:
   - Gesamte Domäne – die Domäne, in der der Lizenzserver Mitglied ist.
   - Organisationseinheit – jede Organisationseinheit innerhalb der Domäne, in der der Lizenzserver Mitglied ist.
   - Gesamte Domäne und alle vertrauenswürdigen Domänen – kann Domänen in anderen Gesamtstrukturen einbeziehen. Die Auswahl dieser Option kann die Zeit bis zur Erstellung des Berichts verlängern.

   Ihre Auswahl bestimmt, welche Benutzerkonten in AD DS nach Informationen zur „Pro Benutzer“-Clientzugriffslizenz für Remotedesktopdienste durchsucht werden, um den Bericht zu erstellen.
3. Klicken Sie auf **Bericht erstellen**. Der Bericht wird erstellt und es wird eine Nachricht angezeigt, die bestätigt, dass der Bericht erfolgreich erstellt wurde. Klicken Sie auf **OK**, um die Meldung zu schließen.

Der von Ihnen erstellte Bericht wird im Abschnitt „Berichte“ unter dem Knoten für den Lizenzserver angezeigt. Der Bericht liefert die folgenden Informationen:

- Datum und Uhrzeit der Erstellung des Berichts
- Der Gültigkeitsbereich des Berichts (z. B. „Domäne“, „OU=Vertrieb“ oder „Alle vertrauenswürdigen Domänen“)
- Die Anzahl der „Pro Benutzer“-RDS-CALs, die auf dem Lizenzserver installiert sind
- Die Anzahl der „Pro Benutzer“-RDS-CALs, die vom Lizenzserver ausgegeben wurden, die für den Gültigkeitsbereich des Berichts spezifisch sind

Sie können den Bericht auch als CSV-Datei in einem Ordner auf dem Computer speichern. Um den Bericht zu speichern, klicken Sie mit der rechten Maustaste auf den Bericht, den Sie speichern möchten, klicken Sie auf „Speichern unter“, und geben Sie dann den Dateinamen und den Speicherort zum Speichern des Berichts an.

Von Ihnen erstellte Berichte werden im Knoten „Berichte“ unter dem Knoten für den Lizenzserver im Remotedesktoplizenzierungs-Manager aufgelistet. Wenn Sie einen Bericht nicht mehr benötigen, können Sie ihn löschen.
