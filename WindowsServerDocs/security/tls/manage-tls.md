---
title: Verwalten von Transport Layer Security (TLS)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 06/05/2017
ms.openlocfilehash: e26d1f833dbb7219251947f1cb3cb09def958aea
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-transport-layer-security-tls"></a>Verwalten von Transport Layer Security (TLS)

## <a name="configuring-tls-cipher-suite-order"></a>Konfigurieren von Reihenfolge der TLS-Verschlüsselungssammlungen

Verschiedene Versionen von Windows unterstützen unterschiedliche TLS-Verschlüsselungssammlungen und Reihenfolge ihrer Priorität aufgelistet. Finden Sie unter [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx) für die Standardreihenfolge vom Microsoft Schannel-Provider in verschiedenen Windows-Versionen unterstützt.

> [!NOTE] 
> Sie können auch das Ändern der Liste der Verschlüsselungssammlungen mit CNG-Funktionen, finden Sie unter [Verschlüsselungssammlungen priorisieren](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx) Details.

Änderungen an der Reihenfolge der TLS-Verschlüsselungssammlungen werden beim nächsten Start wirksam. Bis zum Neustarten oder Herunterfahren wird die vorhandene Reihenfolge in Kraft sein.

> [!WARNING] 
> Aktualisieren die registrierungseinstellungen für die Priorität Standardreihenfolge wird nicht unterstützt und kann mit Wartungsupdates zurückgesetzt werden. 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungssammlungen mithilfe von Gruppenrichtlinien

Die SSL-Verschlüsselung Suite Reihenfolge-gruppenrichtlinieneinstellungen können so konfigurieren Sie die Standardreihenfolge TLS-Verschlüsselung Suite.

1.  Die Gruppenrichtlinien-Verwaltungskonsole, wechseln Sie zu **Computerkonfiguration** > **Administrative Vorlagen** > **Netzwerke** > **SSL-Konfigurationseinstellungen**.
2.  Doppelklicken Sie auf **Reihenfolge der SSL-Verschlüsselungssammlungen**, und klicken Sie dann auf die **aktiviert** Option.
3.  Mit der rechten Maustaste **SSL-Verschlüsselungssammlungen** und wählen Sie **wählen Sie alle** aus dem Popupmenü.

    ![Gruppenrichtlinieneinstellung](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4.  Mit der rechten Maustaste in des markierten Texts, und wählen Sie **Kopie** aus dem Popupmenü.
5.  Fügen Sie den Text in einem Text-Editor wie z. B. notepad.exe und mit der neuen Cipher Suite Liste aktualisieren.

    > [!NOTE]
    > Die TLS-Verschlüsselung Suite Liste muss strikte durch Trennzeichen getrennte Format aufweisen. Jede Cipher Suite-Zeichenfolge wird durch ein Komma (,) auf der rechten Seite des beendet. 

    > Darüber hinaus ist die Liste der Verschlüsselungssammlungen auf 1023 Zeichen begrenzt.

6.  Ersetzen der Liste in der **SSL-Verschlüsselungssammlungen** mit der aktualisierten sortierte Liste.
7.  Klicken Sie auf **OK** oder **gelten**.

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungssammlungen mit MDM

Windows 10 Policy CSP unterstützt die Konfiguration der Verschlüsselungssammlungen, TLS. Finden Sie unter [Kryptografie/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites) Weitere Informationen.

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungssammlungen mithilfe von TLS-PowerShell-Cmdlets

Das TLS-PowerShell-Modul unterstützt das Abrufen der sortierten Liste der TLS-Verschlüsselungssammlungen, eine Verschlüsselungssammlung zu deaktivieren und eine Verschlüsselungssammlung zu aktivieren. Finden Sie unter [TLS-Modul](https://technet.microsoft.com/itpro/powershell/windows/tls/tls) Weitere Informationen.

## <a name="configuring-tls-ecc-curve-order"></a>Konfigurieren von TLS ECC Kurve Reihenfolge 

Ab Windows 10 und Windows Server 2016, kann ECC Kurve Reihenfolge unabhängig von der Reihenfolge der Verschlüsselungssammlungen konfiguriert werden. Wenn die TLS dieses Feld enthält die Reihenfolge der, dass die Liste Elliptische Kurve Suffixe sind, werden sie durch die neue Elliptische Kurve Prioritätsreihenfolge überschrieben werden, wenn aktiviert. Dadurch können Organisationen ein Gruppenrichtlinienobjekt zu verwenden, um verschiedene Versionen von Windows mit der gleichen Reihenfolge der Cipher Suites konfigurieren.

> [!NOTE]
> Vor Windows 10 wurden Verschlüsselungssammlungen Suite Zeichenfolgen Elliptische Kurve die Priorität der Kurve bestimmt angefügt.

### <a name="managing-windows-ecc-curves-using-certutil"></a>Verwalten von Windows-ECC-Kurven verwenden von CertUtil

Ab Windows 10 und Windows Server 2016, sorgt Windows Elliptische Kurve Parameter Management über die Befehlszeile Dienstprogramm certuil.exe. Elliptische Kurvenzugparameter sind in der bcryptprimitives.dll gespeichert. Verwenden certutil.exe, können Administratoren hinzufügen und entfernen kurvenparametern zu und von Windows, bzw.. Certutil.exe speichert die Kurvenzugparameter sicher in der Registrierung. Windows kann die Verwendung der Kurvenzugparameter mit dem Namen der Kurve zugeordnet beginnen.    

#### <a name="displaying-registered-curves"></a>Anzeigen von registrierten Kurven

Verwenden Sie den folgenden certutil.exe-Befehl, um eine Liste der für den aktuellen Computer registrierten Kurven anzuzeigen.

```powershell
certutil.exe –displayEccCurve
```

![Certutil Anzeige Kurven](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*Abbildung 1 Certutil.exe Ausgabe in die Liste der registrierten Kurven anzuzeigen.*

#### <a name="adding-a-new-curve"></a>Hinzufügen einer neuen Kurve

Organisationen können erstellen und Verwenden von anderen vertrauenswürdigen Entitäten Recherchen kurvenparametern.  
Administratoren, die diese neue Kurven in Windows verwenden, müssen die Kurve hinzufügen.  
Verwenden Sie den folgenden certutil.exe-Befehl, um eine Kurve mit aktuellen Computer hinzufügen:

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- Die **partiell** Argument stellt den Namen der Kurve, unter dem die Kurvenzugparameter hinzugefügt wurden.
- Die **CurveParameters** Argument stellt den Dateinamen eines Zertifikats mit den Parametern der Kurven hinzugefügt werden soll.
- Die **CurveOid** Argument stellt einen Dateinamen eines Zertifikats, das die OID der Kurvenzugparameter enthält (optional) hinzufügen möchten.
- Die **CurveType** Argument stellt einen Dezimalwert für die benannte Kurve aus der [EG namens Kurve Registrierung](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8) (optional).

![Certutil Kurven hinzufügen](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*Abbildung 2 eine Kurve mit certutil.exe hinzufügen.*

#### <a name="removing-a-previously-added-curve"></a>Entfernen eine zuvor hinzugefügte Kurve

Administratoren können eine zuvor hinzugefügte Kurve mit dem folgenden Befehl mit certutil.exe entfernen:

```powershell
Certutil.exe –deleteEccCurve curveName
```

Eine benannte Kurve kann nicht verwendet werden, nachdem ein Administrator die Kurve vom Computer entfernt.

## <a name="managing-windows-ecc-curves-using-group-policy"></a>Verwalten von Windows-ECC-Kurven, die mithilfe von Gruppenrichtlinien

Organisationen können kurvenparametern für Unternehmen, Domäne, Computer mithilfe von Gruppenrichtlinien und der Registrierungseinstellungen für Gruppenrichtlinieneinstellungen Erweiterung verteilen.  
Der Prozess zum Verteilen einer Kurve ist:

1.  Auf Windows 10 und Windows Server 2016 verwenden **certutil.exe** registrierte neue benannte Kurven zu Windows hinzufügen.
2.  Öffnen Sie auf dem gleichen Computer die Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC), erstellen Sie ein neues Gruppenrichtlinienobjekt zu und bearbeiten.
3.  Navigieren Sie zu **Computerkonfiguration | Einstellungen | Windows-Einstellungen | Registrierung**.  Mit der rechten Maustaste **Registrierung**. Zeigen Sie auf **neu** , und wählen Sie **Auflistungselement**. Benennen Sie die Sammlungselement, um den Namen der Kurve entsprechen. Erstellen Sie eine Registrierung Auflistungselement für jeden Registrierungsschlüssel unter *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters*.
4.  Konfigurieren Sie die neu erstellte Einstellung Registrierung Erfassung von Gruppenrichtlinien durch Hinzufügen eines neuen **Registrierungselement** für jeden Registrierungswert unter aufgeführten *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters\ [partiell]*.
5.  Stellen Sie das Gruppenrichtlinienobjekt mit Registrierung Erfassung von Gruppenrichtlinien Artikel für Windows 10 und Windows Server 2016-Computer, die die neuen benannten Kurven erhalten sollen, bereit.

    ![GPP verteilen Kurven](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *Abbildung 3 mithilfe von Voreinstellungen für Gruppenrichtlinien zur Verteilung von Kurven*

## <a name="managing-tls-ecc-order"></a>Verwalten von TLS ECC-Auftrag

Ab Windows 10 und Windows Server 2016, ECC Kurve Reihenfolge Konfiguration einer Gruppenrichtlinie Einstellungen verwendet werden, können standardmäßig TLS ECC Kurve Reihenfolge. Generische ECC und diese Einstellung, die Organisationen können eigene vertrauenswürdige mit dem Namen Kurven (die für die Verwendung mit TLS genehmigt wurden) für das Betriebssystem hinzufügen und dann fügen diesen benannten Kurven der Kurve Priorität Gruppenrichtlinien-Einstellung, um sicherzustellen, dass sie in zukünftigen TLS-Handshakes verwendet werden. Neue Kurve Priorität Listen werden beim nächsten Neustart nach Erhalt der Richtlinieneinstellungen aktiviert.     

![GPP verteilen Kurven](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*Abbildung 4 Verwalten von TLS Kurve Priorität mithilfe von Gruppenrichtlinien*


