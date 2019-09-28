---
title: Verwalten von Transport Layer Security (TLS)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: a4ac1ea5b0648dbb80f103c146ad3df23fc04ab7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402343"
---
# <a name="manage-transport-layer-security-tls"></a>Verwalten von Transport Layer Security (TLS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

## <a name="configuring-tls-cipher-suite-order"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungs Sammlungen

Unterschiedliche Windows-Versionen unterstützen verschiedene TLS-Verschlüsselungs Sammlungen und Prioritäts Reihenfolge. Weitere Informationen finden Sie unter Verschlüsselungs Sammlungen [in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx) für die Standard Reihenfolge, die vom Microsoft SChannel-Anbieter in verschiedenen Windows-Versionen unterstützt wird.

> [!NOTE] 
> Sie können auch die Liste der Verschlüsselungs Sammlungen mithilfe von CNG-Funktionen ändern. Weitere Informationen finden Sie unter [Priorisieren von SChannel Chiffre Suites](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx) .

Änderungen an der Reihenfolge der TLS-Verschlüsselungs Sammlungen werden beim nächsten Start wirksam. Bis zum Neustart oder zum Herunterfahren wird die vorhandene Bestellung wirksam.

> [!WARNING] 
> Das Aktualisieren der Registrierungs Einstellungen für die Standard Reihenfolge der Priorität wird nicht unterstützt und kann mit Wartungsupdates zurückgesetzt werden. 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungs Sammlung mithilfe von Gruppenrichtlinie

Sie können die Reihenfolge Gruppenrichtlinie Einstellungen der SSL-Verschlüsselungs Sammlung verwenden, um die Standard Reihenfolge der TLS-Verschlüsselungs Sammlung zu konfigurieren.

1. Wechseln Sie in der Gruppenrichtlinien-Verwaltungskonsole zu **Computer Konfiguration** > **Administrative Vorlagen** > **Netzwerke** > **SSL-Konfigurationseinstellungen**.
2. Doppelklicken Sie auf die **Reihenfolge der SSL**-Verschlüsselungs Sammlungen, und klicken Sie dann auf die Option **aktiviert** .
3. Klicken Sie mit der rechten Maustaste auf das Feld **SSL** -Verschlüsselungs Sammlungen, und wählen Sie im Popupmenü die Option **Alle auswählen** aus.

   ![Gruppenrichtlinieneinstellung](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4. Klicken Sie mit der rechten Maustaste auf den ausgewählten Text, und wählen Sie im Popup Menü **Kopieren** aus.
5. Fügen Sie den Text in einen Texteditor ein, z. b. "Notepad. exe", und aktualisieren Sie ihn mit der neuen Liste der Verschlüsselungs Sammlungen.

   > [!NOTE]
   > Die Reihen folgen Liste der TLS-Verschlüsselungs Sammlung muss ein strenges Komma getrenntes Format aufweisen. Jede Chiffre Zeichenfolge endet mit einem Komma (,) auf der rechten Seite. 
   > 
   > Außerdem ist die Liste der Verschlüsselungs Sammlungen auf 1.023 Zeichen beschränkt.

6. Ersetzen Sie die Liste in den **SSL** -Verschlüsselungs Sammlungen durch die aktualisierte geordnete Liste.
7. Klicken Sie auf **OK** oder **Übernehmen**.

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungs Sammlungen mithilfe von MDM

Der Windows 10 Policy CSP unterstützt die Konfiguration der TLS-Verschlüsselungs Sammlungen. Weitere Informationen finden Sie unter [Cryptography/tlsciphersuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites) .

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungs Sammlungen mithilfe von TLS-PowerShell-Cmdlets

Das TLS-PowerShell-Modul unterstützt das erhalten der geordneten Liste von TLS-Verschlüsselungs Sammlungen, das Deaktivieren einer Verschlüsselungs Sammlung und das Aktivieren einer Verschlüsselungs Sammlung. Weitere Informationen finden Sie unter [TLS-Modul](https://technet.microsoft.com/itpro/powershell/windows/tls/tls) .

## <a name="configuring-tls-ecc-curve-order"></a>Konfigurieren der TLS ECC-Kurven Reihenfolge 

Ab Windows 10 & Windows Server 2016 kann die ECC-Kurven Reihenfolge unabhängig von der Reihenfolge der Verschlüsselungs Sammlungen konfiguriert werden. Wenn die Reihen folgen Liste der TLS-Verschlüsselungs Sammlungen elliptische Kurven Suffixe aufweist, werden Sie bei Aktivierung durch die neue Priorität der elliptischen Kurven Priorität überschrieben. Dies ermöglicht es Organisationen, mithilfe eines Gruppenrichtlinie Objekts verschiedene Versionen von Windows mit der gleichen Chiffre Reihenfolge zu konfigurieren.

> [!NOTE]
> Vor Windows 10 wurden Chiffre Sammlungs Zeichenfolgen mit der elliptischen Kurve angehängt, um die Kurven Priorität zu bestimmen.

### <a name="managing-windows-ecc-curves-using-certutil"></a>Verwalten von Windows ECC-Kurven mithilfe von certutil

Ab Windows 10 und Windows Server 2016 bietet Windows eine elliptische Kurven Parameter Verwaltung über das Befehlszeilen-Hilfsprogramm certutil. exe. Parameter der elliptischen Kurve werden in der Datei "bcryptprimitives. dll" gespeichert. Mithilfe von certutil. exe können Administratoren Kurven Parameter zu bzw. aus Windows hinzufügen bzw. daraus entfernen. Certutil. exe speichert die Kurven Parameter sicher in der Registrierung. Windows kann die Kurven Parameter mit dem Namen verwenden, der mit der Kurve verknüpft ist.    

#### <a name="displaying-registered-curves"></a>Anzeigen von registrierten Kurven

Verwenden Sie den folgenden certutil. exe-Befehl, um eine Liste der Kurven anzuzeigen, die für den aktuellen Computer registriert sind.

```powershell
certutil.exe –displayEccCurve
```

![Certutil-Anzeige Kurven](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*Abbildung 1: die Ausgabe von "Certutil. exe", um die Liste der registrierten Kurven anzuzeigen.*

#### <a name="adding-a-new-curve"></a>Hinzufügen einer neuen Kurve

Organisationen können Kurven Parameter erstellen und verwenden, die von anderen vertrauenswürdigen Entitäten erforscht werden.  
Administratoren, die diese neuen Kurven in Windows verwenden möchten, müssen die Kurve hinzufügen.  
Verwenden Sie den folgenden certutil. exe-Befehl, um dem aktuellen Computer eine Kurve hinzuzufügen:

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- Das **Cursor** Name-Argument stellt den Namen der Kurve dar, in der die Kurven Parameter hinzugefügt wurden.
- Das Argument " **currveparameters** " stellt den Dateinamen eines Zertifikats dar, das die Parameter der Kurven enthält, die Sie hinzufügen möchten.
- Das Argument " **currveoid** " stellt einen Dateinamen eines Zertifikats dar, das die OID der Kurven Parameter enthält, die Sie hinzufügen möchten (optional).
- Das **Cursor Type** -Argument stellt einen Dezimalwert der benannten Kurve aus dem [EC](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8) (optional) dar.

![Certutil-Kurven hinzufügen](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*Abbildung 2: Hinzufügen einer Kurve mithilfe von "Certutil. exe".*

#### <a name="removing-a-previously-added-curve"></a>Entfernen einer zuvor hinzugefügten Kurve

Administratoren können eine zuvor hinzugefügte Kurve mit dem folgenden certutil. exe-Befehl entfernen:

```powershell
Certutil.exe –deleteEccCurve curveName
```

Eine benannte Kurve kann nicht verwendet werden, nachdem ein Administrator die Kurve vom Computer entfernt hat.

## <a name="managing-windows-ecc-curves-using-group-policy"></a>Verwalten von Windows ECC-Kurven mithilfe von Gruppenrichtlinie

Organisationen können Kurven Parameter mithilfe von Gruppenrichtlinie und der Registrierungs Erweiterung Gruppenrichtlinie Einstellungen an Enterprise, in eine Domäne eingebundenen Computer verteilen.  
Der Prozess zum Verteilen einer Kurve ist:

1.  Verwenden Sie unter Windows 10 und Windows Server 2016 " **certutil. exe** ", um Windows eine neue registrierte benannte Kurve hinzuzufügen.
2.  Öffnen Sie auf demselben Computer die Gruppenrichtlinien-Verwaltungskonsole (GPMC), erstellen Sie ein neues Gruppenrichtlinie Objekt, und bearbeiten Sie es.
3.  Navigieren Sie zu **Computer Konfiguration | Einstellungen | Windows-Einstellungen | Registrierung**.  Klicken mit der rechten Maustaste auf **Registrierung**. Zeigen Sie auf **neu** , und wählen Sie **Sammel Element**aus. Benennen Sie das Sammel Element so um, dass es dem Namen der Kurve entspricht. Sie erstellen ein Registrierungs Sammel Element für jeden Registrierungsschlüssel unter *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters*.
4.  Konfigurieren Sie die neu erstellte Gruppenrichtlinie Einstellungs Registrierungs Sammlung, indem Sie ein neues **Registrierungs Element** für jeden Registrierungs Wert hinzufügen, der unter *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters @ no__t-2currvename]* aufgeführt ist. .
5.  Stellen Sie das Gruppenrichtlinie Objekt, das Gruppenrichtlinie Registrierungs Sammel Element enthält, für Windows 10-und Windows Server 2016-Computer bereit, die die neuen benannten Kurven erhalten sollen.

    ![Kurven der GPP-Verteilung](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *Abbildung 3 Verwenden von Gruppenrichtlinie Einstellungen zum Verteilen von Kurven*

## <a name="managing-tls-ecc-order"></a>Verwalten der TLS ECC-Reihenfolge

Ab Windows 10 und Windows Server 2016 können die Gruppenrichtlinien Einstellungen für die ECC-Kurven Sortierung verwendet werden, um die standardmäßige TLS ECC-Kurven Reihenfolge zu konfigurieren. Mithilfe der generischen ECC und dieser Einstellung können Organisationen ihre eigenen vertrauenswürdigen benannten Kurven (die für die Verwendung mit TLS genehmigt werden) dem Betriebssystem hinzufügen und diese benannten Kurven dann der Einstellung für die Kurven Priorität Gruppenrichtlinie hinzufügen, um sicherzustellen, dass Sie in zukünftigen TLS verwendet werden. Handshakes. Neue Kurven Prioritäts Listen werden beim nächsten Neustart nach dem Empfang der Richtlinien Einstellungen aktiv.     

![Kurven der GPP-Verteilung](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*Abbildung 4 Verwalten der TLS-Kurven Priorität mithilfe Gruppenrichtlinie*


