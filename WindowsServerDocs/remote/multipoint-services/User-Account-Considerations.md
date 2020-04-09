---
title: Überlegungen zu Benutzerkonten
description: Bietet Überlegungen zu Benutzerkonto, Benutzername und Kennwort für Multipoint Services
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: e225900b-cee9-48c9-b21c-394dc5e72b78
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 732100a79adbdd7d9fbe4ade742c43084d6b54f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820573"
---
# <a name="user-account-considerations"></a>Überlegungen zu Benutzerkonten
In diesem Thema werden Probleme beschrieben, die von Ihnen als Administrator beim Erstellen und Verwalten von Benutzerkonten berücksichtigt werden sollten. Sie verwalten Benutzerkonten auf der Registerkarte Benutzer im Multipoint-Manager. Weitere Informationen finden Sie unter [Verwalten von Benutzerkonten](Manage-User-Accounts.md).  
  
## <a name="user-account-types"></a>Typen von Benutzerkonten  
Bei einem Benutzerkonto handelt es sich um eine Sammlung von Informationen, die Multipoint Services mitteilt, auf welche Dateien und Ordner ein Benutzer zugreifen kann, welche Änderungen Sie an dem Multipoint Services-System vornehmen können und welche Einstellungen für jeden Benutzer, wie z. b. Desktop Hintergrund. Jede Person greift mit einem eindeutigen Benutzernamen und einem Kennwort auf ihr eigenes Benutzerkonto zu. Multipoint Services unterstützt drei Arten von Benutzerkonten:  
  
-   Administrator **Konten** sind für Personen gedacht, die den Multipoint-Manager verwenden, um das Multipoint Services-System zu verwenden und zu verwalten. Weitere Informationen finden Sie unter [Erstellen eines Administratorkontos](Create-an-Administrative-User-Account.md).  
  
-   **Standardbenutzerkonten** sind für Personen gedacht, die regelmäßig auf Stationen zugreifen, das System aber nicht verwalten. Normalerweise werden für die meisten Benutzer des MultiPoint Services-Systems Standardbenutzerkonten erstellt. Weitere Informationen finden Sie unter [Erstellen eines Standardbenutzerkontos](Create-a-Standard-User-Account.md).  
  
-   **MultiPoint-Dashboardbenutzerkonten** sind für Personen gedacht, die Sitzungen von Standardbenutzern über das MultiPoint-Dashboard verwalten und die sich über jede Station anmelden können. Weitere Informationen finden Sie unter [Erstellen eines Kontos für MultiPoint-Dashboardbenutzer](Create-a-MultiPoint-Dashboard-User-Account.md).  
  
## <a name="user-name-and-password-considerations"></a>Überlegungen zu Benutzernamen und Kennwörtern  
Administratoren können Aufgaben ausführen, die sich auf alle anderen Benutzer des MultiPoint Services-Systems auswirken, wie z.B. die Installation von Software oder die Änderung von Sicherheitseinstellungen. Aus diesem Grund sollten Administratoren über eindeutige Benutzernamen und Kennwörter verfügen, die nur ihnen bekannt sind.  
  
Ein wichtiger Aspekt von Benutzerkonten ist, dass jedem Benutzerkonto eine eindeutige **Dokumente**-Bibliothek in Windows-Explorer zugeordnet wird, die den Ordner **Eigene Dokumente** umfasst. Wenn die Standardbenutzer Ihres MultiPoint Services-Systems private Dokumente in ihrer jeweiligen **Dokumente**-Bibliothek in Windows-Explorer speichern, sollten sie sich beim MultiPoint Services-System ebenfalls mit einem eindeutigen Benutzernamen und Kennwort anmelden, das nur ihnen bekannt ist. Weitere Informationen zum Speichern von Dokumenten in Windows-Explorer finden Sie im Thema [Verwalten von Benutzerdateien](Manage-User-Files.md).  
  
> [!TIP]  
> Um die Systemsicherheit zu verstärken, sollten alle Benutzer Kennwörter sichere Kenn Wörter sein. Ein sicheres Kennwort ist ein sicheres Kennwort, das nicht leicht erraten oder geknackt werden kann, mindestens acht Zeichen lang ist, den Kontonamen des Benutzers nicht ganz oder teilweise enthält und mindestens drei der vier folgenden Zeichen Kategorien enthält: Großbuchstaben, Kleinbuchstaben, Ziffern und Symbole, die auf einer Tastatur gefunden werden (z. b.!, @, #).  
  
## <a name="see-also"></a>Weitere Informationen  
[Erstellen eines Administratorkontos](Create-an-Administrative-User-Account.md)  
[Erstellen eines Standardbenutzerkontos](Create-a-Standard-User-Account.md)  
[Verwalten von Benutzer Dateien](Manage-User-Files.md)
[Verwalten von Benutzerkonten](Manage-User-Accounts.md)