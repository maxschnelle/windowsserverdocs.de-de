---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: Attributspeicher hinzufügen
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e092cab5a1911c2e710e6f3a9677bf9df987609b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942692"
---
# <a name="add-an-attribute-store"></a>Attributspeicher hinzufügen


Benutzerkonten und Computer Konten, die Zugriff auf eine Ressource benötigen, die durch Active Directory-Verbunddienste (AD FS) \( AD FS geschützt ist \) , werden in einem Attribut Speicher wie Active Directory Domain Services \( AD DS gespeichert \) . Das Anspruchs Ausstellungs Modul verwendet Attribut Speicher, um Daten zu sammeln, die zum Ausstellen von Ansprüchen erforderlich sind. Daten aus den Attribut speichern werden dann als Ansprüche projiziert.

Sie können das folgende Verfahren verwenden, um dem Verbunddienst einen Attribut Speicher hinzuzufügen.

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

#### <a name="to-add-an-attribute-store"></a>So fügen Sie einen Attribut Speicher hinzu

1.  Öffnen Sie **AD FS-Verwaltung**.

2.  Klicken Sie unter **Aktionen** auf **Attribut Speicher hinzufügen**.

![Attribut Speicher hinzufügen](media/Add-an-Attribute-Store/addstore1.PNG)

3. Konfigurieren Sie im Dialogfeld " **Attribut Speicher hinzufügen** " die folgenden Eigenschaften für den Attribut Speicher, die Sie hinzufügen möchten:

   -   Geben Sie unter **Anzeige Name**den Namen ein, den Sie zum Identifizieren des Attribut Speicher verwenden möchten.

   -   Wählen Sie unter **Attribut Speichertypen**einen unterstützten Attribut Speicher aus, entweder **Active Directory**, **LDAP**oder **SQL**.

   -   Wenn Sie in der **Verbindungs Zeichenfolge**entweder einen LDAP-Speicher für das Lightweight Directory Access-Protokoll \( \) oder einen strukturierte Abfragesprache SQL-Speicher ausgewählt haben \( \) , geben Sie die Zeichenfolge ein, die Sie zum Herstellen einer Verbindung mit dem Attribut Speicher verwendet haben. Für Active Directory-Attribut Speicher ist keine Verbindungs Zeichenfolge erforderlich. Daher ist dieses Feld deaktiviert.

       > [!NOTE]
       > AD FS erstellt standardmäßig automatisch einen Active Directory-Attributspeicher.

![Attribut Speicher hinzufügen](media/Add-an-Attribute-Store/addstore2.PNG)

4. Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

[AD FS-Vorgänge](../ad-fs-operations.md)

[Die Rolle von Attribut speichern](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)
