---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: Attributspeicher hinzufügen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 103ee707c88f4e88b231a833f739cf75b6503e18
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190100"
---
# <a name="add-an-attribute-store"></a>Attributspeicher hinzufügen


Benutzerkonten und Computerkonten, die Zugriff auf eine Ressource, die von Active Directory Federation Services geschützt ist, erfordern \(AD FS\) befinden sich in einem Attributspeicher, z. B. Active Directory Domain Services \(AD DS \). Die anspruchsausstellungs-Engine verwendet Attributspeicher zum Sammeln von Daten, die zum Ausstellen von Ansprüchen erforderlich ist. Daten aus dem Attributspeicher projiziert werden dann als Ansprüche.  
  
Sie können das folgende Verfahren verwenden, einen Attributspeicher für den Verbunddienst hinzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-an-attribute-store"></a>Hinzufügen von einem Attributspeicher  
  
1.  Open **AD FS-Verwaltung**.  
  
2.  Klicken Sie unter **Aktionen** klicken Sie auf **Attributspeicher hinzufügen**.  

![Attributspeicher hinzufügen](media/Add-an-Attribute-Store/addstore1.PNG)
  
3.  In der **Attributspeicher hinzufügen** Dialogfeld konfigurieren Sie die folgenden Eigenschaften für den Attributspeicher, die Sie hinzufügen möchten:  
  
    -   In **Anzeigenamen**, geben Sie den Namen, die Sie verwenden, um den Attributspeicher identifizieren möchten.  
  
    -   In **Store Attributtyp**, wählen Sie einen unterstützten Attributspeicher Speicher, entweder **Active Directory**, **LDAP**, oder **SQL**.  
  
    -   In **Verbindungszeichenfolge**, wenn Sie entweder ein Lightweight Directory Access Protocol ausgewählt haben \(LDAP\) Store oder eine strukturierte Abfragesprache \(SQL\) speichern, geben Sie die Zeichenfolge die Sie zum Herstellen einer Verbindung mit dem Attributspeicher verwendet. Für Active Directory-Attributspeicher ist keine Verbindungszeichenfolge erforderlich. aus diesem Grund wird dieses Feld deaktiviert.  
  
        > [!NOTE]  
        > AD FS erstellt standardmäßig automatisch einen Active Directory-Attributspeicher.  
 
![Attributspeicher hinzufügen](media/Add-an-Attribute-Store/addstore2.PNG) 

4.  Klicken Sie auf **OK**.  
  
## <a name="additional-references"></a>Weitere Verweise  

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
  
[Die Rolle des Attributspeichers](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
