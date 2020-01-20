---
title: Windows-Desktopclient für Administratoren
description: Informationen zum Windows-Desktopclient sind hauptsächlich für Administratoren nützlich.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 09/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2195c3bafaa01a1b1c16c17889d5e04d7213a5b6
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919708"
---
# <a name="windows-desktop-client-for-admins"></a>Windows-Desktopclient für Administratoren

>Gilt für: Windows 10 und Windows 7

Dieses Thema enthält weitere Informationen zum Windows-Desktopclient, die für Administratoren nützlich sind. Grundlegende Informationen zur Verwendung findest du unter [Erste Schritte mit dem Windows-Desktopclient](windowsdesktop.md).

## <a name="installation-options"></a>Installationsoptions

Obwohl deine Benutzer den Client direkt nach dem Herunterladen installieren können, möchtest du ihn den Benutzern möglicherweise auf andere Weise bereitstellen, wenn du den Client auf mehreren Geräten bereitstellst. Erfolgt die Bereitstellung über Gruppenrichtlinien oder den System Center Configuration Manager, kann das Installationsprogramm im Hintergrund über eine Befehlszeile ausgeführt werden. Führ die folgenden Befehle aus, um den Client pro Gerät oder pro Benutzer bereitzustellen.

### <a name="per-device-installation"></a>Installation pro Gerät

```
msiexec.exe /I <path to the MSI> /qn ALLUSERS=1
```

### <a name="per-user-installation"></a>Installation pro Benutzer

```
msiexec.exe /i `<path to the MSI>` /qn ALLUSERS=2 MSIINSTALLPERUSER=1
```

## <a name="configuration-options"></a>Konfigurationsoptionen

In diesem Abschnitt sind die neuen Konfigurationsoptionen für diesen Client beschrieben.

### <a name="configure-update-notifications"></a>Konfigurieren von Updatebenachrichtigungen

Standardmäßig wirst du vom Client jedes Mal benachrichtigt, wenn ein Update vorliegt. Um Benachrichtigungen zu deaktivieren, müssen die folgenden Registrierungsinformationen festgelegt werden:

- **Schlüssel:** HKLM\Software\Microsoft\MSRDC\Policies
- **Typ:** REG_DWORD
- **Name:** AutomaticUpdates
- **Daten:** 0 = Benachrichtigungen deaktivieren. 1 = Benachrichtigungen anzeigen.

### <a name="configure-user-groups"></a>Konfigurieren von Benutzergruppen

Du kannst den Client für einen der folgenden Typen von Benutzergruppen konfigurieren. Dadurch ist bestimmt, wann der Client Updates empfängt.

#### <a name="insider-group"></a>Gruppe „Insider“

Die Gruppe „Insider“ ist für die frühe Überprüfung vorgesehen und besteht aus Administratoren und deen ausgewählten Benutzern. Die Gruppe „Insider“ fungiert als Testlauf, um im Update jegliche Probleme, die sich auf die Leistung auswirken können, zu erkennen, bevor es für die Gruppe „Öffentlich“ freigegeben wird.

> [!NOTE]
> Es empfiehlt sich, dass jede Organisation einige Benutzer in der Gruppe „Insider“ hat, um Updates zu testen und Probleme frühzeitig aufzuspüren.

In der Gruppe „Insider“ wird den Benutzern am zweiten Dienstag jedes Monats eine neue Version des Clients zur frühen Überprüfung zur Verfügung gestellt. Gibt es keine Probleme mit dem Update, wird das Update zwei Wochen später für die Gruppe „Öffentlich“ freigegeben. Benutzer in der Gruppe „Insider“ erhalten automatisch Updatebenachrichtigungen, sobald Updates bereit sind. Ausführlichere Informationen zu Änderungen am Client findest du unter [Neuigkeiten im Windows-Desktopclient](windowsdesktop-whatsnew.md).

Um den Client für die Gruppe „Insider“ zu konfigurieren, legst du die folgenden Registrierungsinformationen fest:

- **Schlüssel:** HKLM\Software\Microsoft\MSRDC\Policies
- **Typ:** REG_SZ
- **Name:** ReleaseRing
- **Daten:** insider

#### <a name="public-group"></a>Gruppe „Öffentlich“

Diese Gruppe gilt für alle Benutzer und ist die stabilste Version. Es sind keinerlei Aktionen erforderlich, um diese Gruppe zu konfigurieren.

Die Gruppe „Öffentlich“ empfängt an jedem vierten Dienstag jedes Monats die Version des Clients, die von der Gruppe „Insider“ getestet wurde. Alle Benutzer in der Gruppe „Öffentlich“ erhalten eine Updatebenachrichtigung, wenn diese Einstellung aktiviert ist.
