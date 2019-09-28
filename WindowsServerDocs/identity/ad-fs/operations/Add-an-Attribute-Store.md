---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: Attributspeicher hinzufügen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0f5c9d3b0f856ab72a16930ddb5c50686d747ecc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358389"
---
# <a name="add-an-attribute-store"></a>Attributspeicher hinzufügen


Benutzerkonten und Computer Konten, die Zugriff auf eine Ressource benötigen, die durch Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 geschützt ist, werden in einem Attribut Speicher wie Active Directory Domain Services \(AD DS @ no__t-3 gespeichert. Das Anspruchs Ausstellungs Modul verwendet Attribut Speicher, um Daten zu sammeln, die zum Ausstellen von Ansprüchen erforderlich sind. Daten aus den Attribut speichern werden dann als Ansprüche projiziert.  
  
Sie können das folgende Verfahren verwenden, um dem Verbunddienst einen Attribut Speicher hinzuzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-an-attribute-store"></a>So fügen Sie einen Attribut Speicher hinzu  
  
1.  Öffnen Sie **AD FS-Verwaltung**.  
  
2.  Klicken Sie unter **Aktionen** auf **Attribut Speicher hinzufügen**.  

![Attribut Speicher hinzufügen](media/Add-an-Attribute-Store/addstore1.PNG)
  
3. Konfigurieren Sie im Dialogfeld " **Attribut Speicher hinzufügen** " die folgenden Eigenschaften für den Attribut Speicher, die Sie hinzufügen möchten:  
  
   -   Geben Sie unter **Anzeige Name**den Namen ein, den Sie zum Identifizieren des Attribut Speicher verwenden möchten.  
  
   -   Wählen Sie unter **Attribut Speichertypen**einen unterstützten Attribut Speicher aus, entweder **Active Directory**, **LDAP**oder **SQL**.  
  
   -   Wenn Sie in der **Verbindungs Zeichenfolge**entweder ein Lightweight Directory Access-Protokoll \(ldap @ no__t-2-Speicher oder einen strukturierte Abfragesprache \(sql @ no__t-4-Speicher ausgewählt haben, geben Sie die Zeichenfolge ein, die Sie zum Herstellen einer Verbindung mit dem Attribut verwendet haben. Speicher. Für Active Directory-Attribut Speicher ist keine Verbindungs Zeichenfolge erforderlich. Daher ist dieses Feld deaktiviert.  
  
       > [!NOTE]  
       > AD FS erstellt standardmäßig automatisch einen Active Directory-Attributspeicher.  
 
![Attribut Speicher hinzufügen](media/Add-an-Attribute-Store/addstore2.PNG) 

4. Klicken Sie auf **OK**.  
  
## <a name="additional-references"></a>Weitere Verweise  

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
  
[Die Rolle von Attribut speichern](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
