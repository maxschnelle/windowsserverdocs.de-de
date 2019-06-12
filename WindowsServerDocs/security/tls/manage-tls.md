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
ms.date: 05/16/2018
ms.openlocfilehash: 872647f09898bf8ae08ee69f28b717d28abf7c78
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447304"
---
# <a name="manage-transport-layer-security-tls"></a>Verwalten von Transport Layer Security (TLS)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

## <a name="configuring-tls-cipher-suite-order"></a>Konfigurieren von Reihenfolge der TLS-Verschlüsselungssammlungen

Verschiedene Windows-Versionen unterstützen verschiedene TLS-Verschlüsselungssammlungen und die Reihenfolge ihrer Priorität. Finden Sie unter [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx) für die Standardreihenfolge, die von der Microsoft-Schannel-Provider in verschiedenen Windows-Versionen unterstützt.

> [!NOTE] 
> Sie können auch die Liste ändern von Verschlüsselungssammlungen mit CNG-Funktionen finden Sie unter [Priorisieren von Schannel Cipher Suites](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx) Details.

Änderungen an der Reihenfolge der TLS-Verschlüsselungssammlungen werden auf den nächsten Systemstart wirksam. Bis zum Neustarten oder Herunterfahren wird die vorhandene Reihenfolge aktiviert sein.

> [!WARNING] 
> Aktualisieren die registrierungseinstellungen für die Priorität Standardreihenfolge wird nicht unterstützt und für die Verarbeitung der Updates zurückgesetzt werden. 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungssammlungen mithilfe einer Gruppenrichtlinie

Sie können die SSL Cipher Suite Order-gruppenrichtlinieneinstellungen verwenden, so konfigurieren Sie die Standardreihenfolge TLS Cipher Suite.

1. Die Gruppenrichtlinien-Verwaltungskonsole, navigieren Sie zu **Computerkonfiguration** > **Administrative Vorlagen** > **Netzwerke**  >  **SSL-Konfigurationseinstellungen**.
2. Doppelklicken Sie auf **Reihenfolge der SSL-Verschlüsselungssammlungen**, und klicken Sie dann auf die **aktiviert** Option.
3. Mit der rechten Maustaste **SSL-Verschlüsselungssammlungen** und wählen Sie **wählen Sie alle** aus dem Popupmenü.

   ![Gruppenrichtlinieneinstellung](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4. Mit der rechten Maustaste in des ausgewählten Texts, und wählen **Kopie** aus dem Popupmenü.
5. Fügen Sie den Text in einem Text-Editor wie notepad.exe und Update mit der neuen Cipher Suite Liste aus.

   > [!NOTE]
   > Der TLS-Verschlüsselungsverfahren Suite Bestellliste muss strenge durch Trennzeichen getrennten Format aufweisen. Jede Cipher Suite Zeichenfolge endet mit einem Komma (,), auf die rechte Seite des Zertifikats. 
   > 
   > Darüber hinaus ist die Liste der Verschlüsselungssammlungen maximal 1.023 Zeichen.

6. Ersetzen Sie die Liste in der **SSL-Verschlüsselungssammlungen** mit der aktualisierten sortierten Liste.
7. Klicken Sie auf **OK** oder **Übernehmen**.

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungssammlungen mithilfe von MDM

Die Windows 10 Policy, CSP unterstützt die Konfiguration der Verschlüsselungssammlungen, TLS. Finden Sie unter [Kryptografie/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites) für Weitere Informationen.

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>Konfigurieren der Reihenfolge der TLS-Verschlüsselungssammlungen mithilfe von TLS-PowerShell-Cmdlets

Das TLS-PowerShell-Modul unterstützt die geordnete Liste der TLS-Verschlüsselungssammlungen abrufen, eine Verschlüsselungssammlung zu deaktivieren und eine Verschlüsselungssammlung zu aktivieren. Finden Sie unter [TLS-Modul](https://technet.microsoft.com/itpro/powershell/windows/tls/tls) für Weitere Informationen.

## <a name="configuring-tls-ecc-curve-order"></a>Konfigurieren die Reihenfolge der TLS-ECC-Kurve 

Ab Windows 10 und Windows Server 2016 kann ECC-Kurve Reihenfolge unabhängig von der Reihenfolge der Verschlüsselungssammlungen konfiguriert werden. Wenn TLS dieses Feld enthält die Reihenfolge der, dass Liste Elliptische Kurve Suffixe aufweist, wird von der Reihenfolge ihrer Priorität von neuen Elliptische Kurve überschrieben werden bei Aktivierung. Dadurch können Organisationen ein Gruppenrichtlinienobjekt zu verwenden, um verschiedene Versionen von Windows mit der gleichen Reihenfolge der Cipher Suites konfigurieren zu können.

> [!NOTE]
> Vor Windows 10 wurden die Elliptische Kurve zum Festlegen der Priorität der Kurve Cipher Suite Zeichenfolgen angefügt.

### <a name="managing-windows-ecc-curves-using-certutil"></a>Verwalten von Windows-ECC-Kurven, die das Verwenden von CertUtil

Ab Windows 10 und Windows Server 2016 bietet Windows parameterverwaltung für Elliptische Kurve über die Befehlszeile Hilfsprogramm certutil.exe. Elliptische Kurve-Parameter werden in der bcryptprimitives.dll gespeichert. Verwenden certutil.exe, können Administratoren hinzufügen und entfernen Kurvenparameter zu und von Windows, bzw. Die Kurvenparameter wird von Certutil.exe sicher in der Registrierung gespeichert. Windows kann beginnen mit den Parametern für die Kurve und der Name der Kurve zugeordnet.    

#### <a name="displaying-registered-curves"></a>Anzeigen von registrierten Kurven

Verwenden Sie den folgenden certutil.exe-Befehl, um eine Liste von Kurven, die für den aktuellen Computer registrierten anzuzeigen.

```powershell
certutil.exe –displayEccCurve
```

![Certutil-Anzeige-Kurven](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*Abbildung 1-Certutil.exe ausgeben, um die Liste der registrierten Kurven anzuzeigen.*

#### <a name="adding-a-new-curve"></a>Hinzufügen einer neuen Kurve

Organisationen können erstellen und Verwenden von Kurvenparameter, die von anderen vertrauenswürdigen Entitäten untersucht.  
Administratoren, die diese neuen Kurven in Windows verwenden möchten, müssen die Kurve hinzufügen.  
Verwenden Sie den folgenden certutil.exe-Befehl, eine Kurve aktuellen Computer hinzu:

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- Die **partiell** Argument darstellt, den Namen der Kurve, die unter dem die Kurvenparameter hinzugefügt wurden.
- Die **CurveParameters** Argument darstellt, den Dateinamen eines Zertifikats mit den Parametern der Kurven hinzugefügt werden soll.
- Die **CurveOid** Argument darstellt, einen Dateinamen eines Zertifikats, das die OID der Kurvenparameter enthält (optional) hinzufügen möchten.
- Die **CurveType** Argument stellt einen Dezimalwert aus der benannten Kurve dar. die [EC benannte Kurve Registrierung](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8) (optional).

![Certutil hinzufügen Kurven](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*Abbildung 2: Hinzufügen einer Kurve mit certutil.exe.*

#### <a name="removing-a-previously-added-curve"></a>Entfernt eine zuvor hinzugefügte Kurve

Administratoren können eine zuvor hinzugefügte Kurve, die mit dem folgenden certutil.exe-Befehl entfernen:

```powershell
Certutil.exe –deleteEccCurve curveName
```

Windows kann nicht auf eine benannte Kurve verwenden, nachdem ein Administrator die Kurve vom Computer entfernt.

## <a name="managing-windows-ecc-curves-using-group-policy"></a>Verwalten von Windows-ECC-Kurven, die mithilfe von Gruppenrichtlinien

Organisationen können Kurvenparameter, Enterprise, Domäne eingebundene Computer mithilfe von Gruppenrichtlinien und der Registrierungseinstellungen für Gruppenrichtlinieneinstellungen-Erweiterung verteilen.  
Der Prozess für die Verteilung der Kurve ist:

1.  Verwenden Sie auf Windows 10 und Windows Server 2016, **certutil.exe** Windows eine neue registrierten benannte Kurve hinzu.
2.  Öffnen Sie von demselben Computer die Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC), erstellen Sie ein neues Gruppenrichtlinienobjekt und bearbeiten.
3.  Navigieren Sie zu **Computerkonfiguration | Einstellungen | Windows-Einstellungen | Registrierung**.  Mit der rechten Maustaste **Registrierung**. Zeigen Sie auf **neu** , und wählen Sie **Sammelelement**. Benennen Sie das sammelelement entsprechend den Namen der Kurve. Erstellen Sie eine Registrierung sammelelement für jeden Registrierungsschlüssel unter *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters*.
4.  Konfigurieren Sie die neu erstellte Einstellung Registrierung Erfassung von Gruppenrichtlinien durch Hinzufügen eines neuen **Registrierungselement** für jeden Registrierungswert unter aufgeführten *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ ECCParameters\[partiell]* .
5.  Stellen Sie das Gruppenrichtlinienobjekt mit Registrierung Erfassung von Gruppenrichtlinien-Element für Windows 10 und Windows Server 2016-Computer, die die neuen benannten Kurven erhalten soll.

    ![GPP Verteilen von Kurven](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *Abbildung 3 Using Group Policy Preferences zum Verteilen von Kurven*

## <a name="managing-tls-ecc-order"></a>Verwalten von TLS ECC-Reihenfolge

Ab Windows 10 und Windows Server 2016 können ECC-Kurve Reihenfolge der Gruppenrichtlinie die Einstellungen verwendet werden können konfigurieren die Standardeinstellung für die TLS ECC-Kurve Reihenfolge. Mithilfe von generischen ECC und diese Einstellung, die Organisationen kann ihre eigenen vertrauenswürdigen benannter Kurven (die für die Verwendung mit TLS genehmigt wurden) an das Betriebssystem hinzufügen und dann diese benannten Kurven hinzufügen, auf die Kurve Priorität Gruppenrichtlinien-Einstellung, um sicherzustellen, dass sie in zukünftigen TLS verwendet werden SSL-Handshakes. Neue Kurve Priorität Listen werden beim nächsten Neustart nach Erhalt der Richtlinieneinstellungen aktiv.     

![GPP Verteilen von Kurven](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*Abbildung 4 Verwalten von TLS-Kurve Priorität, die mithilfe von Gruppenrichtlinien*


