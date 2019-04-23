---
title: Überlegungen zu Benutzerkonten
description: Bietet Benutzerkonto, Benutzername und Überlegungen zu Kennwörtern für MultiPoint Services
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e225900b-cee9-48c9-b21c-394dc5e72b78
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 00fb5e83921ba0b8ad86a6f75bdfd7bf16419b73
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850791"
---
# <a name="user-account-considerations"></a>Überlegungen zu Benutzerkonten
Dieses Thema beschreibt die Probleme, die Sie als Administrator beim Erstellen und Verwalten von Benutzerkonten berücksichtigen sollten. Sie verwalten die Benutzerkonten in der Registerkarte "Benutzer" im MultiPoint-Manager. Weitere Informationen finden Sie unter [Verwalten von Benutzerkonten](Manage-User-Accounts.md).  
  
## <a name="user-account-types"></a>Typen von Benutzerkonten  
Ein Benutzerkonto ist eine Sammlung von Informationen, anhand derer MultiPoint Services ermittelt, auf welche Dateien und Ordner ein Benutzer zugreifen und welche Änderungen der Benutzer am MultiPoint Services-System vornehmen darf. Außerdem umfassen diese Informationen die Einstellungen der einzelnen Benutzer (z.B. den Desktophintergrund). Jede Person greift mit einem eindeutigen Benutzernamen und einem Kennwort auf ihr eigenes Benutzerkonto zu. MultiPoint Services unterstützt drei Typen von Benutzerkonten:  
  
-   **Administratorkonten** sind für Personen, die MultiPoint-Manager verwenden und Verwalten von MultiPoint Services-System verwendet wird. Weitere Informationen finden Sie unter [Erstellen eines Administratorkontos](Create-an-Administrative-User-Account.md).  
  
-   **Standardbenutzerkonten** sind für Personen gedacht, die regelmäßig auf Stationen zugreifen, das System aber nicht verwalten. Normalerweise werden für die meisten Benutzer des MultiPoint Services-Systems Standardbenutzerkonten erstellt. Weitere Informationen finden Sie unter [Erstellen eines Standardbenutzerkontos](Create-a-Standard-User-Account.md).  
  
-   **MultiPoint-Dashboardbenutzerkonten** sind für Personen gedacht, die Sitzungen von Standardbenutzern über das MultiPoint-Dashboard verwalten und die sich über jede Station anmelden können. Weitere Informationen finden Sie unter [Erstellen eines Kontos für MultiPoint-Dashboardbenutzer](Create-a-MultiPoint-Dashboard-User-Account.md).  
  
## <a name="user-name-and-password-considerations"></a>Überlegungen zu Benutzernamen und Kennwörtern  
Administratoren können Aufgaben ausführen, die sich auf alle anderen Benutzer des MultiPoint Services-Systems auswirken, wie z.B. die Installation von Software oder die Änderung von Sicherheitseinstellungen. Aus diesem Grund sollten Administratoren über eindeutige Benutzernamen und Kennwörter verfügen, die nur ihnen bekannt sind.  
  
Ein wichtiger Aspekt von Benutzerkonten ist, dass jedem Benutzerkonto eine eindeutige **Dokumente**-Bibliothek in Windows-Explorer zugeordnet wird, die den Ordner **Eigene Dokumente** umfasst. Wenn die Standardbenutzer Ihres MultiPoint Services-Systems private Dokumente in ihrer jeweiligen **Dokumente**-Bibliothek in Windows-Explorer speichern, sollten sie sich beim MultiPoint Services-System ebenfalls mit einem eindeutigen Benutzernamen und Kennwort anmelden, das nur ihnen bekannt ist. Weitere Informationen zum Speichern von Dokumenten in Windows-Explorer finden Sie im Thema [Verwalten von Benutzerdateien](Manage-User-Files.md).  
  
> [!TIP]  
> Zur Erhöhung der Systemsicherheit sollten die Kennwörter aller Benutzer sichere Kennwörter sein. Ein sicheres Kennwort ist ein, der nicht leicht erraten werden kann oder geknackt wird, mindestens acht Zeichen lang sein, enthält keine vollständig oder teilweise Kontonamen des Benutzers und enthält mindestens drei der vier folgenden Zeichenkategorien: Großbuchstaben, Kleinbuchstaben Zeichen, Zahlen und Symbole auf einer Tastatur (wie z. B.!, @, #).  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen eines Administratorkontos](Create-an-Administrative-User-Account.md)  
[Erstellen Sie ein Standardbenutzerkonto](Create-a-Standard-User-Account.md)  
[Verwalten von Benutzerdateien](Manage-User-Files.md)
[Verwalten von Benutzerkonten](Manage-User-Accounts.md)