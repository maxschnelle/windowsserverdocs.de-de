---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: "Attributspeicher hinzufügen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11baba5bfdb699f120a506feb8361db21d26cff1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-an-attribute-store"></a>Attributspeicher hinzufügen

>Gilt für: Windows Server 2016, Windows Server2012 R2

Benutzerkonten und Computerkonten, die Zugriff auf eine Ressource erforderlich ist, die durch Active Directory Federation Services \(AD FS\) geschützt ist, werden in einem Attributspeicher, z.B. Active Directory-Domänendienste \(AD DS\) gespeichert. Das anspruchsausstellungsmodul verwendet Attributspeicher zum Sammeln von Daten, die zum Ausstellen von Ansprüchen erforderlich ist. Daten aus dem Attributspeicher werden dann als Ansprüche projiziert.  
  
Das folgende Verfahren können einem Attributspeicher an den Verbunddienst hinzu.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-an-attribute-store"></a>Hinzufügen ein Attributspeichers  
  
1.  Öffnen **AD FS-Verwaltungs**.  
  
2.  Klicken Sie unter **Aktionen** klicken Sie auf **Attributspeicher hinzufügen**.  

![Attributspeicher hinzufügen](media/Add-an-Attribute-Store/addstore1.PNG)
  
3.  In der **Attributspeicher hinzufügen** Dialogfeld konfigurieren Sie die folgenden Eigenschaften für den Attributspeicher, die Sie hinzufügen möchten:  
  
    -   In **Anzeigenamen**, geben Sie den Namen, die Sie verwenden, um den Attributspeicher identifizieren möchten.  
  
    -   In **Store Attributtyp**, wählen Sie entweder einen unterstützten Store Attributtyp **Active Directory**, **LDAP**, oder **SQL**.  
  
    -   In **Verbindungszeichenfolge**, wenn Sie, entweder eine Lightweight Directory Access Protocol \(LDAP\) oder ein Speicher Structured Query Language \(SQL\) ausgewählt haben Geben Sie die Zeichenfolge, die Sie zum Herstellen einer Verbindung mit dem Attributspeicher verwendet. Für Active Directory-Attributspeicher ist keine Verbindungszeichenfolge erforderlich. Daher ist dieses Feld deaktiviert.  
  
        > [!NOTE]  
        > AD FS erstellt standardmäßig automatisch einen Active Directory-Attributspeicher.  
 
![Attributspeicher hinzufügen](media/Add-an-Attribute-Store/addstore2.PNG) 

4.  Klicken Sie auf **OK**.  
  
## <a name="additional-references"></a>Weitere Verweise  

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
  
[Die Rolle des Attributspeichers](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
