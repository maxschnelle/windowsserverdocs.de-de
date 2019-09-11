---
title: Kerberos mit Dienstprinzipalname (SPN)
description: Der Netzwerk Controller unterstützt mehrere Authentifizierungsmethoden für die Kommunikation mit Verwaltungs Clients. Sie können die Kerberos-basierte Authentifizierung, die auf X509-Zertifikaten basierende Authentifizierung verwenden. Sie haben auch die Möglichkeit, keine Authentifizierung für Test Bereitstellungen zu verwenden.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 8c8c5367eeda576f87ac5de20b7885a1a29aeb4d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869915"
---
# <a name="kerberos-with-service-principal-name-spn"></a>Kerberos mit Dienstprinzipalname (SPN)

>Gilt für: Windows Server 2019

Der Netzwerk Controller unterstützt mehrere Authentifizierungsmethoden für die Kommunikation mit Verwaltungs Clients. Sie können die Kerberos-basierte Authentifizierung, die auf X509-Zertifikaten basierende Authentifizierung verwenden. Sie haben auch die Möglichkeit, keine Authentifizierung für Test Bereitstellungen zu verwenden.

System Center Virtual Machine Manager verwendet die Kerberos-basierte Authentifizierung. Wenn Sie die Kerberos-basierte Authentifizierung verwenden, müssen Sie einen Dienst Prinzipal Namen (Service Principal Name, SPN) für den Netzwerk Controller in Active Directory konfigurieren. Der SPN ist ein eindeutiger Bezeichner für die Netzwerk Controller-Dienst Instanz, die von der Kerberos-Authentifizierung zum Zuordnen einer Dienst Instanz zu einem Dienst Anmelde Konto verwendet wird. Weitere Informationen finden Sie unter [Dienst Prinzipal Namen](https://docs.microsoft.com/windows/desktop/ad/service-principal-names).

## <a name="configure-service-principal-names-spn"></a>Konfigurieren von Dienst Prinzipal Namen (SPN)

Der SPN wird vom Netzwerk Controller automatisch konfiguriert. Sie müssen lediglich Berechtigungen für die Netzwerk Controller Computer bereitstellen, um den SPN zu registrieren und zu ändern.

1.  Starten Sie auf dem Domänen Controller Computer **Active Directory Benutzer und Computer**.

2.  Wählen **Sie \> Ansicht erweitert**aus.

3.  Suchen Sie unter Computer nach einem der Netzwerk Controller- **Computer**Konten, klicken Sie mit der rechten Maustaste, und wählen Sie **Eigenschaften**aus.

4.  Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **erweitert**.

5.  Klicken Sie in der Liste auf **Hinzufügen** , wenn alle Netzwerk Controller-Computer Konten oder eine Sicherheitsgruppe mit allen Netzwerk Controller-Computer Konten nicht aufgeführt sind.

6.  Für jedes Netzwerk Controller-Computer Konto oder eine einzelne Sicherheitsgruppe, die die Computer Konten des Netzwerk Controllers enthält:

    a.  Wählen Sie das Konto oder die Gruppe, und klicken Sie auf **Bearbeiten**.

    b.  Wählen Sie unter Berechtigungen die Option überprüfen **Schreibdienst Prinzipal Name**aus.

    d.  Scrollen Sie nach unten, und wählen Sie unter **Eigenschaften** Folgendes:

       -  **ServicePrincipalName lesen**

       -  **ServicePrincipalName schreiben**

    e.  Klicken Sie zweimal auf **OK** .

7.  Wiederholen Sie Schritt 3-6 für jeden Netzwerk Controller Computer.

8.  Schließen Sie **Active Directory-Benutzer und -Computer**.

## <a name="failure-to-provide-permissions-for-spn-registrationmodification"></a>Fehler beim Bereitstellen von Berechtigungen für die SPN-Registrierung/-Änderung

Wenn Sie bei einer **neuen** Windows Server 2019-Bereitstellung Kerberos für die Rest-Client Authentifizierung ausgewählt haben und keine Berechtigung für Netzwerk Controller Knoten erteilen, um den SPN zu registrieren oder zu ändern, können Rest-Vorgänge auf dem Netzwerk Controller die Verwaltung von nicht verhindern. der Sdn.

Bei einem Upgrade von Windows Server 2016 auf Windows Server 2019 und bei der Auswahl von Kerberos für die Rest-Client Authentifizierung werden Rest-Vorgänge nicht blockiert. Dadurch wird die Transparenz für vorhandene Produktions Bereitstellungen sichergestellt. 

Wenn der SPN nicht registriert ist, verwendet die Rest-Client Authentifizierung NTLM, das weniger sicher ist. Außerdem erhalten Sie ein kritisches Ereignis im Admin-Kanal des Network **Controller-Framework-** Ereignis Kanals, in dem Sie aufgefordert werden, Berechtigungen für die Netzwerk Controller Knoten zum Registrieren des SPN bereitzustellen. Nachdem Sie die Berechtigung erteilt haben, registriert der Netzwerk Controller den SPN automatisch, und alle Client Vorgänge verwenden Kerberos.


>[!TIP]
>In der Regel können Sie den Netzwerk Controller so konfigurieren, dass er eine IP-Adresse oder einen DNS-Namen für Rest-basierte Vorgänge verwendet. Wenn Sie Kerberos konfigurieren, können Sie jedoch keine IP-Adresse für Rest-Abfragen an den Netzwerk Controller verwenden. Beispiels \<Weise können Sie verwenden https://networkcontroller.consotso.com\>, aber Sie können nicht verwenden \< https://192.34.21.3\>. Dienst Prinzipal Namen können nicht funktionieren, wenn IP-Adressen verwendet werden.
>
>Wenn Sie die IP-Adresse für Rest-Vorgänge zusammen mit der Kerberos-Authentifizierung in Windows Server 2016 verwendet haben, wäre die tatsächliche Kommunikation über die NTLM-Authentifizierung erfolgt. Wenn Sie in einer solchen Bereitstellung ein Upgrade auf Windows Server 2019 durchführen, verwenden Sie die NTLM-basierte Authentifizierung. Wenn Sie zur Kerberos-basierten Authentifizierung wechseln möchten, müssen Sie den DNS-Namen des Netzwerk Controllers für Rest-Vorgänge verwenden und die Berechtigung für Netzwerk Controller Knoten zum Registrieren des SPN angeben.

---