---
title: Verfolgen Sie Ihre Remote Desktop Services-Clientzugriffslizenzen (TS CALs)
description: Erfahren Sie, wie Clientzugriffslizenzen für Ihre RDS-Bereitstellung zu verfolgen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80d82d30-3ad0-4a8c-9a9b-2773c47eee19
author: lizap
ms.author: elizapo
ms.date: 05/11/2017
manager: dongill
ms.openlocfilehash: ed7490b2b61eb516d43b280b67fcefaeedb3e225
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890621"
---
# <a name="track-your-remote-desktop-services-client-access-licenses-rds-cals"></a>Verfolgen Sie Ihre Remote Desktop Services-Clientzugriffslizenzen (TS CALs)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können den Remotedesktoplizenzierungs-Manager-Tool verwenden, erstellen Sie Berichte zum Nachverfolgen von RDS pro Benutzer-CALs, die von einem Remotedesktop-Lizenzserver ausgestellt wurden.

> [!NOTE]
>  Wenn Sie Azure AD Domain Services in Ihrer Umgebung verwenden, funktionieren nicht den Remotedesktoplizenzierungs-Manager-Tool zum Abrufen von Clientzugriffslizenzen pro Benutzer. Stattdessen müssen Sie zum Nachverfolgen der Lizenzierung manuell entweder über das Logon-Ereignissen, Abruf aktive Verbindungen mit Remote Desktop über den Verbindungsbroker oder einen anderen Mechanismus, der für Sie geeignet. 

Verwenden Sie die folgenden Schritte aus, um das Generieren einer pro-Benutzer-CALs Bericht:

1. In den Remotedesktoplizenzierungs-Manager den Lizenzserver, klicken Sie auf **Bericht erstellen**, und klicken Sie dann auf **pro Benutzer-Clientzugriffslizenz-Verwendung**.
2. Festlegen des Gültigkeitsbereichs für den Bericht – wählen Sie eine der folgenden:
   - Gesamte Domäne – der Domäne, in der der Lizenzserver Mitglied ist.
   - Organisationseinheit - eine beliebige Organisationseinheit innerhalb der Domäne, in der der Lizenzserver Mitglied ist.
   - Gesamte Domäne und alle vertrauenswürdigen Domänen - können Domänen in anderen Gesamtstrukturen enthalten. Nach Auswahl dieser Option kann die Zeit verlängern, die zum Erstellen des Berichts benötigt.

   Die Auswahl, die Sie vornehmen bestimmt, welche Benutzerkonten in AD DS für RDS-CAL pro Benutzer Informationen zum Erstellen des Berichts durchsucht werden.
3. Klicken Sie auf **erstellen Berichts**. Der Bericht wird erstellt, und eine Meldung angezeigt wird, um sicherzustellen, dass der Bericht wurde erfolgreich erstellt wurde. Klicken Sie auf **OK**, um die Meldung zu schließen.

Der Bericht, den Sie erstellt haben, wird im Abschnitt "Berichte" unter dem Knoten für den Lizenzserver. Der Bericht enthält die folgende Informationen an:

- Datum und Uhrzeit der Erstellung des Berichts
- Der Geltungsbereich des Berichts (z. B. die Domäne, OU = wird, Vertrieb oder alle vertrauenswürdigen Domänen)
- Die Anzahl von RDS Clientzugriffslizenzen pro Benutzer, die auf dem Lizenzserver installiert sind
- Die Anzahl von RDS Clientzugriffslizenzen pro Benutzer, die auf den Bereich des Berichts durch den bestimmten Lizenzserver ausgestellt wurden

Sie können den Bericht auch als CSV-Datei in einem Ordner auf dem Computer speichern. Um den Bericht speichern möchten, klicken Sie den Bericht, den Sie speichern, klicken Sie auf Speichern unter, und geben Sie dann den Dateinamen und Speicherort für den Bericht speichern möchten.

Von Ihnen erstellten Berichte werden im Knoten "Berichte" unter dem Knoten für den Lizenzserver im Remotedesktoplizenzierungs-Manager aufgeführt. Wenn Sie einen Bericht nicht mehr benötigen, können Sie es löschen.
