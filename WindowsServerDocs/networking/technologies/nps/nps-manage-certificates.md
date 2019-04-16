---
title: Verwalten von mit NPS verwendeten Zertifikaten
description: Dieses Thema enthält Informationen zur Verwendung von Serverzertifikaten mit dem Netzwerkrichtlinienserver in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 204a4ef4-9d78-4a62-9940-43cc0e1c39d0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2044cf30cc90c1673e05a1948ac9196d05940d1f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="manage-certificates-used-with-nps"></a>Verwalten von mit NPS verwendeten Zertifikaten

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Wenn Sie eine zertifikatbasierte Authentifizierung-Methode, z. B. Extensible Authentication Protocol\-Transport Layer Security \(EAP\-TLS\) Protected Extensible Authentication Protocol\-Transport Layer Security \(PEAP\-TLS\) und PEAP\-Microsoft Challenge Handshake Authentication Protocol Version 2 Bereitstellen \ (MS\ CHAP v2\), müssen Sie ein Serverzertifikat für alle Ihre NPS-Server registrieren. Das Serverzertifikat muss:

- Die Mindestanforderungen für Serverzertifikate erfüllen, wie unter [Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen](nps-manage-cert-requirements.md)

- Von einer Zertifizierungsstelle ausgestellt werden \(CA\), die von Clientcomputern als vertrauenswürdig eingestuft wird. Eine Zertifizierungsstelle ist vertrauenswürdig, wenn ihr Zertifikat im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für den aktuellen Benutzer und den lokalen Computer vorhanden ist.

Die folgenden Anweisungen bei der Verwaltung von NPS-Serverzertifikate in Bereitstellungen, bei denen die vertrauenswürdige Stamm-CA ist von einer Drittanbieter-Zertifizierungsstelle wie Verisign, oder eine Zertifizierungsstelle, die Sie für Ihre public Key-Infrastruktur bereitgestellt haben \(PKI\) mithilfe von Active Directory Certificate Services \(AD CS\).

## <a name="change-the-cached-tls-handle-expiry"></a>Ändern der Ablauf der zwischengespeicherten TLS-Handle

Während der anfänglichen Authentifizierungsprozesse für EAP\-TLS, PEAP\-TLS und PEAP\-MS\-CHAP v2 speichert der NPS-Server einen Teil der Eigenschaften für die Verbindung des Clients TLS-Verbindung. Der Client wird auch einen Teil der Eigenschaften für den NPS-Server TLS-Verbindung zwischengespeichert.

Jede einzelne Sammlung dieser Eigenschaften der TLS-Verbindung wird einen TLS-Handle aufgerufen.

Clientcomputer können die TLS-Handles für mehrere Authentifikatoren zwischenspeichern, während der NPS-Server die TLS-Handles von vielen Clientcomputern zwischengespeichert werden können.

Zwischengespeicherte TLS-Handles auf dem Client und Server, dass die erneute Authentifizierung Prozess schneller ausgeführt. Z. B. bei ein drahtlosen Computer mit einem NPS-Server cloudserverfunktion, der NPS-Server kann die TLS-Handle für den drahtlosen Client überprüfen und kann schnell feststellen, dass der Client wird. Der NPS-Server wird die Verbindung ohne vollständige Authentifizierung autorisiert.

Entsprechend der Client überprüft das TLS-Handle für den NPS-Server, legt fest, dass sie eine erneute Verbindung, und muss nicht zum Ausführen von Server-Authentifizierung.

Auf Computern unter Windows 10 und Windows Server 2016 ist standardmäßig TLS-Handle Ablauf 10 Stunden.

In einigen Fällen empfiehlt es sich zum Vergrößern oder verkleinern die Ablaufzeit des TLS-Handle.

Sie möchten z. B. verringern die Ablaufzeit des TLS-Handle in Situationen, in dem Zertifikat des Benutzers wird durch den Administrator widerrufen, und das Zertifikat ist abgelaufen. In diesem Szenario kann der Benutzer weiterhin mit dem Netzwerk verbinden, wenn ein NPS-Server einen zwischengespeicherten TLS-Handle verfügt, der noch nicht abgelaufen ist. Reduzieren die TLS möglicherweise Handle Ablauf verhindern, dass diese Benutzer mit gesperrten Zertifikaten weiterhin.

>[!NOTE]
>Die beste Lösung für dieses Szenario ist das Benutzerkonto in Active Directory zu deaktivieren oder das Benutzerkonto aus Active Directory-Gruppe zu entfernen, die Berechtigung zum Verbinden mit dem Netzwerk in der Netzwerkrichtlinie erteilt wurde. Die Weitergabe dieser Änderungen auf allen Domänencontrollern kann auch, jedoch aufgrund der Replikationswartezeit verzögert werden. 

## <a name="configure-the-tls-handle-expiry-time-on-client-computers"></a>Konfigurieren Sie die Ablaufzeit des TLS-Handle auf Clientcomputern

Dieses Verfahrens können Sie um den Zeitraum zu ändern, dass Clientcomputer das TLS-Handle des NPS-Server zwischengespeichert. Nach einer erfolgreichen Authentifizierung eines NPS-Servers cache Clientcomputern Eigenschaften der TLS-Verbindung des NPS-Servers als ein Handle TLS. Das TLS-Handle verfügt standardmäßig über die Dauer \(36,000,000 milliseconds\) 10 Stunden. Sie können erhöhen oder verringern die Ablaufzeit des TLS-Handle mithilfe des folgenden Verfahrens.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

>[!IMPORTANT]
>Dieses Verfahren muss auf einem NPS-Server nicht auf einem Clientcomputer ausgeführt werden.

### <a name="to-configure-the-tls-handle-expiry-time-on-client-computers"></a>Behandeln zum Konfigurieren der TLS Ablaufzeit auf Clientcomputern

1. Öffnen Sie auf einem NPS-Server Registrierungs-Editor.

2. Navigieren Sie zum Registrierungsschlüssel **HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. Auf der **bearbeiten** Menü klicken Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.

4. Typ **ClientCacheTime**, und drücken Sie dann die EINGABETASTE.

5. Mit der rechten Maustaste **ClientCacheTime**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)**.

6. Geben Sie die Zeitdauer in Millisekunden an, die Clientcomputer das TLS-Handle des NPS-Server zwischengespeichert, nachdem die erste Authentifizierung erfolgreiche vom NPS-Server versucht werden soll.

## <a name="configure-the-tls-handle-expiry-time-on-nps-servers"></a>Konfigurieren Sie die Ablaufzeit des TLS-Handle auf NPS-Servern

Verwenden Sie dieses Verfahren, den Zeitraum zu ändern, dass NPS-Server das TLS-Handle des Clientcomputer zwischengespeichert. Nach einer erfolgreichen Authentifizierung eines Clients Zugriff cache NPS-Server TLS-Verbindungseigenschaften des Client-Computers als Handle TLS. Das TLS-Handle verfügt standardmäßig über die Dauer \(36,000,000 milliseconds\) 10 Stunden. Sie können erhöhen oder verringern die Ablaufzeit des TLS-Handle mithilfe des folgenden Verfahrens.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

>[!IMPORTANT]
>Dieses Verfahren muss auf einem NPS-Server nicht auf einem Clientcomputer ausgeführt werden.

### <a name="to-configure-the-tls-handle-expiry-time-on-nps-servers"></a>Zum Konfigurieren von behandeln das TLS Ablaufzeit auf NPS-Servern

1. Öffnen Sie auf einem NPS-Server Registrierungs-Editor.

2. Navigieren Sie zum Registrierungsschlüssel **HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. Auf der **bearbeiten** Menü klicken Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.

4. Typ **"servercachetime"**, und drücken Sie dann die EINGABETASTE.

5. Mit der rechten Maustaste **"servercachetime"**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)**.

6. Geben Sie die Zeitdauer in Millisekunden an, die NPS-Server das TLS-Handle eines Clientcomputers zwischengespeichert, nachdem die erste Authentifizierung erfolgreiche vom Client versucht werden soll.

## <a name="obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>Abrufen des SHA-1-Hashs eines vertrauenswürdigen Stamm-CA-Zertifikats

Verwenden Sie dieses Verfahren, um die Secure Hash Algorithm (SHA-1) Hash von einer vertrauenswürdigen Stammzertifizierungsstelle (CA) aus einem Zertifikat abzurufen, die auf dem lokalen Computer installiert ist. In einigen Fällen z. B. wenn die Gruppenrichtlinie bereitstellen, ein Zertifikat angeben, mit dem SHA-1-Hash des Zertifikats erforderlich ist.

Wenn Sie Gruppenrichtlinien verwenden, können Sie eine oder mehrere vertrauenswürdige Stammzertifizierungsstellen-Zertifikate festlegen, die Clients verwenden müssen, um die NPS-Server bei der gegenseitigen Authentifizierung mit EAP oder PEAP authentifizieren. Um ein Zertifikat einer vertrauenswürdigen Stammzertifizierungsstelle festzulegen, die Clients zum Überprüfen des Serverzertifikats verwenden müssen, können Sie den SHA-1-Hash des Zertifikats eingeben.

Dieses Verfahren veranschaulicht, wie Sie den SHA-1-Hash des Zertifikat einer vertrauenswürdigen Stammzertifizierungsstelle abrufen, indem Sie mit dem Zertifikate Microsoft Management Console (MMC)-Snap-in. 

Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Benutzer** Gruppe auf dem lokalen Computer.

### <a name="to-obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>Den SHA-1-Hash des einen vertrauenswürdigen Stamm-CA-Zertifikat abrufen

1. Geben Sie im Dialogfeld Ausführen oder Windows PowerShell, **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console \(MMC\) wird geöffnet. Klicken Sie in der MMC auf **Datei**, klicken Sie dann auf **hinzufügen/entfernen Snap\in**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.

2. In **hinzufügen oder Entfernen von Snap-Ins**im **Verfügbare Snap-Ins**, doppelklicken Sie auf **Zertifikate**. Das Zertifikate-Snap-in-Assistent wird geöffnet. Klicken Sie auf **Computerkonto**, und klicken Sie dann auf **Weiter**.

3. In **Computer auswählen**, stellen Sie sicher, dass **lokalen Computer (Computer, auf diese Konsole ausgeführt wird)** ist ausgewählt haben, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.

4. Doppelklicken Sie im linken Bereich auf **Zertifikate (lokaler Computer)**, und doppelklicken Sie dann auf die **vertrauenswürdige Stammzertifizierungsstellen** Ordner.

5. Die **Zertifikate** ist ein Unterordner des der **vertrauenswürdige Stammzertifizierungsstellen** Ordner. Klicken Sie auf die **Zertifikate** Ordner.

6. Navigieren Sie im Detailbereich auf das Zertifikat für die vertrauenswürdige Stammzertifizierungsstelle. Doppelklicken Sie auf das Zertifikat. Die **Zertifikat** Dialogfeld wird geöffnet.

7. In der **Zertifikat** Dialogfeld, klicken Sie auf die **Details** Registerkarte.

8. In der Liste der Felder, scrollen Sie zu, und wählen Sie **Fingerabdruck**.

9. Im unteren Bereich wird die Hexadezimalzeichenfolge, die den SHA-1-Hash des Zertifikats wird angezeigt. Wählen Sie den SHA-1-Hash, und drücken Sie dann die Windows-Tastenkombination für die Kopie der Befehl \(CTRL\+C\) den Hash auf die Windows-Zwischenablage kopieren.

10. Öffnen Sie den Speicherort an, Sie fügen Sie den SHA-1-Hash, richtig suchen den Cursor, und drücken dann die Windows-Tastenkombination für das einfügen möchten Befehl \(CTRL\+V\). 

Weitere Informationen zu Zertifikaten und NPS, finden Sie unter [Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen](nps-manage-cert-requirements.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
