---
title: Verwalten von mit NPS verwendeten Zertifikaten
description: In diesem Thema wird erläutert, wie Sie mithilfe von Serverzertifikaten mit Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 204a4ef4-9d78-4a62-9940-43cc0e1c39d0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73f3d6a1e9dc6ae1520b1d685b6b05b5f3aed601
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864231"
---
# <a name="manage-certificates-used-with-nps"></a>Verwalten von mit NPS verwendeten Zertifikaten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie eine zertifikatbasierte Authentifizierung-Methode, z. B. Extensible Authentication-Protokoll bereitstellen\-Transport Layer Security \(EAP\-TLS\), Protected Extensible Authentication Protocol\-Transport Layer Security \(PEAP\-TLS\), und PEAP\-Microsoft Challenge Handshake Authentication Protocol Version 2 \(MS\-CHAP-v2\), müssen Sie ein Serverzertifikat für alle Ihre NPSs registrieren. Das Serverzertifikat muss:

- Die Mindestanforderungen für Serverzertifikate erfüllen, wie in beschrieben [Konfigurieren von Zertifikatvorlagen für PEAP und EAP-Anforderungen](nps-manage-cert-requirements.md)

- Von einer Zertifizierungsstelle ausgestellt werden \(Zertifizierungsstelle\) von Clientcomputern als vertrauenswürdig eingestuft wird. Wenn das Zertifikat im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für den aktuellen Benutzer und dem lokalen Computer vorhanden ist, ist eine Zertifizierungsstelle vertrauenswürdig.

Die folgenden Anweisungen, bei der Verwaltung von NPS-Zertifikaten in Bereitstellungen, bei denen die vertrauenswürdige Stammzertifizierungsstelle wird von einer Drittanbieter-Zertifizierungsstelle wie Verisign oder eine Zertifizierungsstelle, die Sie für Ihre public Key-Infrastruktur bereitgestellt haben \(PKI\) mit aktiv Directory-Zertifikatdienste \(AD CS\).

## <a name="change-the-cached-tls-handle-expiry"></a>Ändern der Ablauf des zwischengespeicherten TLS-Handle

Bei der erstmaligen Authentifizierung für EAP\-TLS, PEAP\-TLS und PEAP\-MS\-CHAP-v2, den NPS speichert einen Teil der verbindende Client TLS-Verbindungseigenschaften. Der Client speichert auch einen Teil NPSs-TLS-Verbindungseigenschaften.

Jede einzelne Auflistung von Eigenschaften dieser TLS-Verbindung wird ein TLS-Handle aufgerufen.

Clientcomputer können die TLS-Handles für mehrere Authentifikatoren festlegt, zwischenspeichern, während die TLS-Handles von vielen Clientcomputern NPSs zwischengespeichert werden können.

Die zwischengespeicherten TLS-Handles auf dem Client und Server zulassen den erneuten Authentifizierung Prozess schneller ausgeführt. Z. B. wenn ein Drahtloscomputer mit einem NPS reauthenticates, den NPS können, überprüfen Sie das TLS-Handle für den drahtlosen Client und können schnell feststellen, dass die Clientverbindung erneut hergestellt wird. Der NPS autorisiert die Verbindung ohne vollständige Authentifizierung.

Dementsprechend wird der Client überprüft das TLS-Handle für den NPS, bestimmt, dass sie eine erneute Verbindung, und muss nicht zum Ausführen von Server-Authentifizierung.

Auf Computern unter Windows 10 und Windows Server 2016 ist der Ablauf des standardmäßigen TLS-Handle für 10 Stunden.

In einigen Fällen empfiehlt es sich erhöhen oder verringern die Ablaufzeit des TLS-Handle.

Beispielsweise empfiehlt es sich, verringern die Ablaufzeit des TLS-Handle in Fällen, in dem Zertifikat des Benutzers von einem Administrator gesperrt, und das Zertifikat ist abgelaufen. In diesem Szenario kann der Benutzer weiterhin mit dem Netzwerk verbinden, wenn ein NPS ein Handles für zwischengespeicherte TLS enthält, das nicht abgelaufen ist. Reduziert die TLS kann als Handle Ablauf helfen zu verhindern, dass solche Benutzer mit gesperrten Zertifikaten erneut eine Verbindung herzustellen.

>[!NOTE]
>Die beste Lösung für dieses Szenario ist das Benutzerkonto in Active Directory zu deaktivieren oder das Benutzerkonto, das aus der Active Directory-Gruppe zu entfernen, die Berechtigung für die Verbindung mit dem Netzwerk in der Netzwerkrichtlinie gewährt wird. Die Weitergabe dieser Änderungen auf allen Domänencontrollern kann ebenfalls, jedoch aufgrund der Replikationswartezeit verzögert werden. 

## <a name="configure-the-tls-handle-expiry-time-on-client-computers"></a>Konfigurieren Sie die Ablaufzeit des TLS-Handle auf Clientcomputern

Sie können dieses Verfahren verwenden, die Zeitdauer zu ändern, dass Clientcomputer das TLS-Handle, der ein NPS Zwischenspeichern. Nach einer erfolgreichen Authentifizierung eine NPS Zwischenspeichern Clientcomputer Eigenschaften der NPS TLS-Verbindung als ein TLS-Handle. Das TLS-Handle verfügt standardmäßig über die Dauer von 10 Stunden \(36,000,000 Millisekunden\). Sie können die erhöhen oder verringern die Ablaufzeit des TLS-Handle mithilfe des folgenden Verfahrens.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

>[!IMPORTANT]
>Dieses Verfahren muss auf einen NPS, nicht auf einem Clientcomputer ausgeführt werden.

### <a name="to-configure-the-tls-handle-expiry-time-on-client-computers"></a>Behandeln zum Konfigurieren der TLS Ablaufzeit auf Clientcomputern

1. Öffnen Sie auf einen NPS Registrierungs-Editor ein.

2. Navigieren Sie zu dem Registrierungsschlüssel **HKEY\_lokalen\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. Auf der **bearbeiten** Menü klicken Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.

4. Typ **ClientCacheTime**, und drücken Sie dann die EINGABETASTE.

5. Mit der rechten Maustaste **ClientCacheTime**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)**.

6. Geben Sie die Zeitspanne in Millisekunden, die den Clientcomputern, um das TLS-Handle, der ein NPS zwischengespeichert, nach die erste erfolgreiche Authentifizierung versucht wird, indem Sie den NPS werden sollen.

## <a name="configure-the-tls-handle-expiry-time-on-npss"></a>Konfigurieren Sie die Ablaufzeit des TLS-Handle für NPSs

Verwenden Sie dieses Verfahren, die Zeitdauer zu ändern, dass NPSs das TLS-Handle der Clientcomputer zwischengespeichert. Nach einer erfolgreichen Authentifizierung ein Zugriffsclient Zwischenspeichern NPSs Eigenschaften der TLS-Verbindung des Clients als eine TLS-Handle. Das TLS-Handle verfügt standardmäßig über die Dauer von 10 Stunden \(36,000,000 Millisekunden\). Sie können die erhöhen oder verringern die Ablaufzeit des TLS-Handle mithilfe des folgenden Verfahrens.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

>[!IMPORTANT]
>Dieses Verfahren muss auf einen NPS, nicht auf einem Clientcomputer ausgeführt werden.

### <a name="to-configure-the-tls-handle-expiry-time-on-npss"></a>Behandeln zum Konfigurieren der TLS Ablaufzeit für NPSs

1. Öffnen Sie auf einen NPS Registrierungs-Editor ein.

2. Navigieren Sie zu dem Registrierungsschlüssel **HKEY\_lokalen\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. Auf der **bearbeiten** Menü klicken Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.

4. Typ **"servercachetime"**, und drücken Sie dann die EINGABETASTE.

5. Mit der rechten Maustaste **"servercachetime"**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)**.

6. Geben Sie die Zeitspanne in Millisekunden, die NPSs das TLS-Handle eines Clientcomputers zwischengespeichert, nach die erste erfolgreiche Authentifizierung vom Client versucht werden soll.

## <a name="obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>Abrufen des SHA-1-Hashs eines vertrauenswürdigen Stamm-CA-Zertifikats

Verwenden Sie dieses Verfahren, um die Secure Hash Algorithm (SHA-1) aus einem Zertifikat-Hash einer vertrauenswürdigen Stammzertifizierungsstelle (CA) abrufen, die auf dem lokalen Computer installiert ist. In einigen Fällen z. B. Wenn Sie die Gruppenrichtlinie bereitstellen möchten, ein Zertifikat angeben, mit dem SHA-1-Hash des Zertifikats erforderlich ist.

Wenn Sie Gruppenrichtlinien verwenden, können Sie eine oder mehrere vertrauenswürdige Stamm-Zertifizierungsstellenzertifikate festlegen, die Clients verwenden müssen, um den NPS während des Prozesses der gegenseitigen Authentifizierung mit EAP oder PEAP zu authentifizieren. Um ein Zertifikat einer vertrauenswürdigen Stammzertifizierungsstelle zu bestimmen, die Clients verwenden müssen, um das Serverzertifikat zu überprüfen, können Sie den SHA-1-Hash des Zertifikats eingeben.

Dieses Verfahren veranschaulicht, wie der SHA-1-Hash des ein Zertifikat einer vertrauenswürdigen Stammzertifizierungsstelle abrufen, indem Sie mit den Zertifikaten der Microsoft Management Console (MMC)-Snap-in. 

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied werden die **Benutzer** Gruppe auf dem lokalen Computer.

### <a name="to-obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>Der SHA-1-Hash des Zertifikat einer vertrauenswürdigen Stammzertifizierungsstelle abrufen

1. Geben Sie im Dialogfeld Ausführen oder in Windows PowerShell, **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console \(MMC\) wird geöffnet. Klicken Sie in der MMC auf **Datei**, klicken Sie dann auf **hinzufügen/entfernen Snap\in**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.

2. Doppelklicken Sie im Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Zertifikate**. Das Zertifikate-Snap-in-Assistent wird geöffnet. Klicken Sie auf **Computerkonto** und dann auf **Weiter**.

3. In **Computer auswählen**, sicher, dass **lokalen Computer (der Computer, auf dem diese Konsole ausgeführt wird)** wird ausgewählt, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.

4. Doppelklicken Sie im linken Bereich auf **Zertifikate (lokaler Computer)**, und doppelklicken Sie dann auf die **Trusted Root Certification Authorities** Ordner.

5. Die **Zertifikate** Ordner ist ein Unterordner des der **Trusted Root Certification Authorities** Ordner. Klicken Sie auf den Ordner **Zertifikate**.

6. Navigieren Sie im Detailbereich auf das Zertifikat für Ihre vertrauenswürdigen Stamm-ZS. Doppelklicken Sie auf das Zertifikat. Das Dialogfeld **Zertifikat** wird geöffnet.

7. Klicken Sie im Dialogfeld **Zertifikat** auf die Registerkarte **Details**.

8. Scrollen Sie in der Liste der Felder zu, und wählen Sie **Fingerabdruck**.

9. Im unteren Bereich wird die Hexadezimalzeichenfolge angezeigt, die den SHA-1-Hash Ihres Zertifikats darstellt. Wählen Sie den SHA-1-Hash, und drücken Sie dann die Windows-Tastenkombination für den Befehl Copy \(STRG\+C\) den Hash in die Windows-Zwischenablage zu kopieren.

10. Öffnen Sie den Speicherort, Sie fügen den SHA-1-Hash, den Cursor dann ordnungsgemäß zum Navigieren und drücken dann die Windows-Tastenkombination für den Befehl Paste möchten \(STRG\+V\). 

Weitere Informationen zu Zertifikaten und NPS finden Sie unter [Konfigurieren von Zertifikatvorlagen für PEAP und EAP-Anforderungen](nps-manage-cert-requirements.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
