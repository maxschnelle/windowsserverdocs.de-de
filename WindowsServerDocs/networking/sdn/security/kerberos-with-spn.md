---
title: Kerberos mit Dienstprinzipalname (SPN)
description: Netzwerkcontroller unterstützt mehrere Authentifizierungsmethoden für die Kommunikation mit Verwaltungsclients. Können Sie Kerberos-basierten Authentifizierung, X509 zertifikatbasierte Authentifizierung. Sie haben auch die Möglichkeit, keine Authentifizierung für testbereitstellungen verwenden.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 2459cfa8dfec3de4aa23da7aba192d6eeed7f8ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828971"
---
# <a name="kerberos-with-service-principal-name-spn"></a>Kerberos mit Dienstprinzipalname (SPN)

>Gilt für: Windows Server 2019

Netzwerkcontroller unterstützt mehrere Authentifizierungsmethoden für die Kommunikation mit Verwaltungsclients. Können Sie Kerberos-basierten Authentifizierung, X509 zertifikatbasierte Authentifizierung. Sie haben auch die Möglichkeit, keine Authentifizierung für testbereitstellungen verwenden.

System Center Virtual Machine Manager wird die Kerberos-Authentifizierung verwendet. Wenn Sie Kerberos-Authentifizierung verwenden, müssen Sie einen Namen (SPN) für den Netzwerkcontroller in Active Directory konfigurieren. Der SPN ist ein eindeutiger Bezeichner für die Netzwerkcontroller-Dienstinstanz, die durch die Kerberos-Authentifizierung verwendet wird, ein Dienstkonto für die Anmeldung eine Dienstinstanz zugeordnet werden soll. Weitere Informationen finden Sie unter [Service Principal Names](https://docs.microsoft.com/windows/desktop/ad/service-principal-names).

## <a name="configure-service-principal-names-spn"></a>Konfigurieren von Dienstprinzipalnamen (SPN)

Der Netzwerkcontroller konfiguriert automatisch den SPN an. Alles, was Sie tun müssen ist, erteilen Sie Berechtigungen für die Netzwerkcontroller-Computer den SPN zu registrieren.

1.  Starten Sie auf dem Computer des Domänencontrollers, **Active Directory-Benutzer und-Computer**.

2.  Wählen Sie **Ansicht \> erweiterte**.

3.  Klicken Sie unter **Computer**, suchen Sie für den Netzwerkcontroller-Computerkonten, und klicken Sie dann mit der rechten Maustaste und wählen Sie **Eigenschaften**.

4.  Wählen Sie die **Sicherheit** Registerkarte, und klicken Sie auf **erweitert**.

5.  In der Liste aus, wenn die Netzwerkcontroller-Computerkonten oder eine Sicherheits-müssen alle Computerkonten der Netzwerkcontroller ist nicht aufgeführt Gruppe, klicken Sie auf **hinzufügen** hinzugefügt.

6.  Für jedes Netzwerk-Controller-Computerkonto oder einer Sicherheitsgruppe, die die Netzwerkcontroller-Computerkonten enthält:

    a.  Wählen Sie das Konto oder Gruppe aus, und klicken Sie auf **bearbeiten**.

    b.  Unter "Berechtigungen auswählen" **überprüfen schreiben ServicePrincipalName**.

    d.  Führen Sie einen Bildlauf nach unten, und klicken Sie unter **Eigenschaften** auswählen:

       -  **ServicePrincipalName lesen**

       -  **Schreibzugriff für servicePrincipalName**

    e.  Klicken Sie zweimal auf **OK** .

7.  Wiederholen Sie Schritt 3 bis 6 für jeden Computer für den Netzwerkcontroller aus.

8.  Schließen Sie **Active Directory-Benutzer und -Computer**.

## <a name="failure-to-provide-permissions-for-spn-registrationmodification"></a>Fehler beim Bereitstellen von Berechtigungen für die SPN-Registrierung/Änderung

Auf einem **neu** 2019 für Windows Server-Bereitstellung, wenn Sie Kerberos, für die REST-Client-Authentifizierung auswählen, und Sie keinen über die Berechtigung für den Netzwerkcontroller-Knoten gewähren, den SPN zu registrieren, den REST-Vorgänge auf dem Netzwerkcontroller schlägt fehl. verhindert, dass Verwalten von Sdn Emuliert.

Für ein Upgrade von Windows Server 2016, Windows Server-2019, und Sie Kerberos für die REST-Client-Authentifizierung ausgewählt haben, werden REST-Vorgänge nicht blockiert erhalten Transparenz für vorhandene Bereitstellungen in der Produktion sicherzustellen. 

Wenn der SPN nicht registriert ist, verwendet REST-Client-Authentifizierung NTLM, weniger sicher. Sie erhalten auch ein kritisches Ereignis im adminkanal von **NetworkController-Framework** ereigniskanal, die Sie auffordert, geben Sie die Berechtigungen für die Netzwerkcontroller-Knoten zum SPN zu registrieren. Nachdem Sie die Berechtigung angeben, Netzwerkcontroller wird den SPN automatisch registriert, und alle Clientvorgänge Kerberos verwenden.


>[!TIP]
>In der Regel können Sie den Netzwerkcontroller, um eine IP-Adresse oder DNS-Namen für die REST-basierte Vorgänge verwenden konfigurieren. Wenn Sie Kerberos konfigurieren, können nicht Sie jedoch eine IP-Adresse für REST-Abfragen für den Netzwerkcontroller verwenden. Beispielsweise können Sie \< https://networkcontroller.consotso.com\>, aber Sie können keine \< https://192.34.21.3\>. Service Principal Names, die funktioniert nicht, wenn die IP-Adressen verwendet werden.
>
>Wenn Sie die IP-Adresse für REST-Vorgänge zusammen mit Kerberos-Authentifizierung in Windows Server 2016 verwendet haben, hätten für die Kommunikation über NTLM-Authentifizierung. In solch einer Bereitstellung sind nach dem upgrade auf Windows Server-2019, weiterhin NTLM-basierte Authentifizierung zu verwenden. Um auf Kerberos basierende Authentifizierung verschieben, müssen Sie Network Controller DNS-Namen für die REST-Vorgänge verwenden, und Erteilen von Berechtigungen für den Netzwerkcontroller-Knoten, um den SPN zu registrieren.

---