---
title: Behandeln von Problemen mit Aktivierungsfehlercodes
description: Hier erfährst du, wie du Probleme mit Aktivierungsfehlercodes behandelst.
ms.topic: article
ms.date: 07/22/2019
ms.technology: server-general
ms.assetid: ''
author: kaushika-msft
ms.author: kaushika-msft; v-tea
ms.localizationpriority: medium
ms.openlocfilehash: 506aa5969228a17fe64581ec2a7143537b1fa05a
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68658871"
---
# <a name="troubleshooting-activation-error-codes"></a>Behandeln von Problemen mit Aktivierungsfehlercodes

> **Privatbenutzer**  
> Dieser Artikel ist für Supportmitarbeiter und IT-Spezialisten gedacht. Weitere Informationen zu Fehlermeldungen im Zusammenhang mit der Aktivierung von Windows finden Sie unter [Hilfe für Fehler bei der Aktivierung von Windows](https://support.microsoft.com/help/10738/windows-10-get-help-with-activation-errors).  

Dieser Artikel bietet Informationen zur Fehlerbehandlung bei Fehlermeldungen, die Sie möglicherweise erhalten, wenn Sie Mehrfachaktivierungsschlüssel (Multiple Activation Key, MAK) oder den Schlüsselverwaltungsdienst (Key Management Service, KMS) für eine Volumenaktivierung auf einem oder mehreren Windows-basierten Computern zu verwenden versuchen. Suchen Sie in der folgenden Tabelle nach dem Fehlercode, und klicken Sie dann auf den Link, um weitere Informationen zu diesem Fehlercode und der entsprechenden Lösung anzuzeigen.

Weitere Informationen zur Volumenaktivierung finden Sie unter [Planen für die Volumenaktivierung](https://docs.microsoft.com/en-us/windows/deployment/volume-activation/plan-for-volume-activation-client).

Weitere Informationen zur Volumenaktivierung für neuere und aktuelle Versionen von Windows finden Sie unter [Volumenaktivierung für Windows 10](https://docs.microsoft.com/windows/deployment/volume-activation/volume-activation-windows-10).

Weitere Informationen zur Volumenaktivierung für ältere Versionen von Windows finden Sie im KB-Artikel 929712,  [Volume Activation information for Windows Vista, Windows Server 2008, Windows Server 2008 R2 and Windows 7](https://support.microsoft.com/en-us/help/929712/volume-activation-information-for-windows-vista-windows-server-2008-wi) (Informationen zur Volumenaktivierung für Windows Vista, Windows Server 2008, Windows Server 2008 R2 und Windows 7, in englischer Sprache).

## <a name="summary-of-error-codes"></a>Übersicht über die Fehlercodes

|Fehlercode |Fehlermeldung |Aktivierungstyp |
|-----------|--------------|----------------|
|[0xC004C001](#0xc004c001-the-activation-server-determined-the-specified-product-key-is-invalid) |Der Aktivierungsserver hat festgestellt, dass der Product Key ungültig ist. |MAK|
|[0xC004C003](#0xc004c003-the-activation-server-determined-the-specified-product-key-is-blocked) |Der Aktivierungsserver hat festgestellt, dass der Product Key blockiert ist. |MAK |
|[0xC004C008](#0xc004c008-the-activation-server-determined-that-the-specified-product-key-could-not-be-used) |Der Aktivierungsserver hat festgestellt, dass der Product Key nicht verwendet werden konnte. |KMS |
|[0xC004B100](#0xc004b100-the-activation-server-determined-that-the-computer-could-not-be-activated) |Der Aktivierungsserver hat festgestellt, dass der Computer nicht aktiviert werden konnte. |MAK |
|[0xC004C020](#0xc004c020-the-activation-server-reported-that-the-multiple-activation-key-has-exceeded-its-limit) |Der Aktivierungsserver hat berichtet, dass die DMAK-Grenze überschritten wurde. |MAK |
|[0xC004C021](#0xc004c021-the-activation-server-reported-that-the-multiple-activation-key-extension-limit-has-been-exceeded) |Der Aktivierungsserver hat berichtet, dass die DMAK-Erweiterungsgrenze überschritten wurde. |MAK |
|[0xC004F009](#0xc004f009-the-software-protection-service-reported-that-the-grace-period-expired) |Vom Softwareschutzdienst wurde gemeldet, dass der Zeitraum bis zur Aktivierung abgelaufen ist. |MAK |
|[0xC004F00F](#0xc004f00f-the-software-licensing-server-reported-that-the-hardware-id-binding-is-beyond-level-of-tolerance) |Vom Softwarelizenzierungsdienst wurde gemeldet, dass bei der Hardware-ID-Bindung die Toleranzschwelle überschritten wurde. |MAK/KMS-Client/KMS-Host |
|[0xC004F014](#0xc004f014-the-software-protection-service-reported-that-the-product-key-is-not-available) |Vom Softwareschutzdienst wurde gemeldet, dass der Product Key nicht verfügbar ist. |MAK/KMS-Client |
|[0xC004F02C](#0xc004f02c-the-software-protection-service-reported-that-the-format-for-the-offline-activation-data-is-incorrect) |Vom Softwareschutzdienst wurde gemeldet, dass das Format für die Offlineaktivierung falsch ist. |MAK/KMS-Client |
|[0xC004F035](#0xc004f035-invalid-volume-license-key) |Dieser Fehlercode entspricht dem Fehler „Vom Softwarelizenzierungsdienst wurde gemeldet, dass der Computer nicht mit dem Volumenlizenz-Product Key aktiviert werden konnte...“. Der Fehlertext ist zwar korrekt, aber nicht eindeutig. Dieser Fehler deutet darauf hin, dass im BIOS des Computers ein Windows-Marker fehlt. Ein solcher Marker wird bei OEM-Systemen angegeben, um Computer zu kennzeichnen, die mit qualifizierenden Editionen von Windows ausgeliefert werden (eine Voraussetzung für die KMS-Clientaktivierung). Fehler: Ungültiger Volumen-Lizenzschlüssel Sie müssen Ihren Product Key in einen gültigen Mehrfachaktivierungsschlüssel (Multi Activation Key, MAK) oder einen Verkaufsschlüssel ändern. Sie benötigen eine qualifizierende Lizenz für das Betriebssystem sowie eine Upgradelizenz der Windows 7-Volumen-Lizenzierung oder eine Lizenz für eine Windows 7-Vollversion aus dem Handel. ANDERE INSTALLATIONEN DIESER SOFTWARE STELLEN EINE VERLETZUNG DER LIZENZBESTIMMUNGEN UND GELTENDER URHEBERRECHTSGESETZE DAR. |KMS-Client/KMS-Host |
|[0xC004F038](#0xc004f038-the-count-reported-by-your-key-management-service-kms-is-insufficient) |Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Die vom Schlüsselverwaltungsdienst (Key Management Service, KMS) gemeldete Anzahl ist nicht ausreichend. Wenden Sie sich an den Systemadministrator. |KMS-Client |
|[0xC004F039](#0xc004f039-the-key-management-service-kms-is-not-enabled) |Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Der Schlüsselverwaltungsdienst (Key Management Service, KMS) ist nicht aktiviert. |KMS-Client |
|[0xC004F041](#0xc004f041-the-software-protection-service-determined-that-the-key-management-server-kms-is-not-activated) |Vom Softwarelizenzierungsdienst wurde festgestellt, dass der Schlüsselverwaltungsserver (Key Management Server, KMS) nicht aktiviert ist. Der KMS muss aktiviert werden.  |KMS-Client |
|[0xC004F042](#0xc004f042-the-software-protection-service-determined-that-the-specified-key-management-service-kms-cannot-be-used) |Der Softwareschutzdienst hat festgestellt, dass der angegebene Schlüsselverwaltungsdienst (KMS) nicht verwendet werden kann. |KMS-Client |
|[0xC004F050](#0xc004f050-the-software-protection-service-reported-that-the-product-key-is-invalid) |Vom Softwareschutzdienst wurde ein ungültiger Product Key gemeldet. |KMS, KMS-Client, MAK |
|[0xC004F051](#0xc004f051-the-software-protection-service-reported-that-the-product-key-is-blocked) |Vom Softwareschutzdienst wurde ein gesperrter Product Key gemeldet. |MAK/KMS |
|[0xC004F064](#0xc004f064-the-software-protection-service-reported-that-the-non-genuine-grace-period-expired) |Vom Softwarelizenzierungsdienst wurde gemeldet, dass der nicht-authentische Aktivierungszeitraum abgelaufen ist. |MAK |
|[0xC004F065](#0xc004f065-the-software-protection-service-reported-that-the-application-is-running-within-the-valid-non-genuine-period) |Vom Softwarelizenzierungsdienst wurde gemeldet, dass die Anwendung innerhalb des gültigen, nicht-authentischen Aktivierungszeitraums ausgeführt wird. |MAK/KMS-Client |
|[0xC004F06C](#0xc004f06c-the-request-timestamp-is-invalid) |Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Vom Schlüsselverwaltungsdienst (KMS) wurde festgestellt, dass der Zeitstempel der Anforderung ungültig ist.  |KMS-Client |
|[0x80070005](#0x80070005-access-denied) |Zugriff verweigert: Die angeforderte Aktion erfordert erhöhte Rechte. |KMS-Client/MAK/KMS-Host |
|[0x8007232A](#0x8007232a-dns-server-failure) |DNS-Server Fehler  |KMS-Host  |
|[0x8007232B](#0x8007232b-dns-name-does-not-exist) |Der DNS-Name ist nicht vorhanden. |KMS-Client |
|[0x800706BA](#0x800706ba-the-rpc-server-is-unavailable) |Der RPC-Server ist nicht verfügbar. |KMS-Client |
|[0x8007251D](#0x8007251d-no-records-found-for-dns-query) |Bei der DNS-Abfrage wurden keine Einträge gefunden. |KMS-Client |
|[0xC004F074](#0xc004f074-no-key-management-service-kms-could-be-contacted) |Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Es konnte kein Schlüsselverwaltungsdienst (Key Management Service, KMS) erreicht werden. Weitere Informationen finden Sie im Anwendungsereignisprotokoll.  |KMS-Client |
|[0x8004FE21](#0x8004fe21-this-computer-is-not-running-genuine-windows) |Auf diesem Computer wird keine Originalversion von Windows ausgeführt.  |MAK/KMS-Client |
|[0x80092328](#0x80092328-dns-name-does-not-exist) |0x80092328 Der DNS-Name ist nicht vorhanden.  |KMS-Client |
|[0x8007007b](#0x8007007b-dns-name-does-not-exist) |0x8007007b Der DNS-Name ist nicht vorhanden. |KMS-Client |
|[0x80070490](#0x80070490-the-product-key-you-entered-didnt-work) |Der eingegebene Product Key funktioniert nicht. Überprüfen Sie den Product Key, und versuchen Sie es noch einmal, oder geben Sie einen anderen Product Key ein. |MAK |

## <a name="causes-and-resolutions"></a>Ursachen und Lösungen

### <a name="0xc004c001-the-activation-server-determined-the-specified-product-key-is-invalid"></a>0xC004C001 Der Aktivierungsserver hat festgestellt, dass der Product Key ungültig ist.

#### <a name="possible-cause"></a>Mögliche Ursache

Der eingegebene MAK ist ungültig.

#### <a name="resolution"></a>Auflösung

Überprüfen Sie, ob es sich um den von Microsoft bereitgestellten MAK handelt. Wenn Sie Hilfe benötigen, wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers).

### <a name="0xc004c003-the-activation-server-determined-the-specified-product-key-is-blocked"></a>0xC004C003 Der Aktivierungsserver hat festgestellt, dass der Product Key blockiert ist.

#### <a name="possible-cause"></a>Mögliche Ursache

Der MAK ist auf dem Aktivierungsserver gesperrt.

#### <a name="resolution"></a>Auflösung

Wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers), um einen neuen MAK zu erhalten. Nachdem Sie den neuen MAK erhalten haben, versuchen Sie erneut, Windows zu installieren und zu aktivieren.  

### <a name="0xc004c008-the-activation-server-determined-that-the-specified-product-key-could-not-be-used"></a>0xC004C008 Der Aktivierungsserver hat festgestellt, dass der Product Key nicht verwendet werden konnte.

#### <a name="possible-cause"></a>Mögliche Ursache

Das Aktivierungslimit des KMS-Schlüssels ist überschritten. Ein KMS-Hostschlüssel kann bis zu zehnmal auf bis zu sechs verschiedenen Computern aktiviert werden.  

#### <a name="resolution"></a>Auflösung

Wenn Sie weitere Aktivierungen benötigen, wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers).  

### <a name="0xc004b100-the-activation-server-determined-that-the-computer-could-not-be-activated"></a>0xC004B100 Der Aktivierungsserver hat festgestellt, dass der Computer nicht aktiviert werden konnte.

#### <a name="possible-cause"></a>Mögliche Ursache

Der MAK wird nicht unterstützt.  

#### <a name="resolution"></a>Auflösung

Vergewissern Sie sich zur Behandlung dieses Problems, dass der von Ihnen verwendete MAK von Microsoft bereitgestellt wurde. Wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers), um die Gültigkeit des MAK zu überprüfen.

### <a name="0xc004c020-the-activation-server-reported-that-the-multiple-activation-key-has-exceeded-its-limit"></a>0xC004C020 Der Aktivierungsserver hat berichtet, dass die DMAK-Grenze überschritten wurde.

#### <a name="possible-cause"></a>Mögliche Ursache

Das Aktivierungslimit des MAK ist überschritten. Für die Anzahl der MAK-Aktivierungen wurde ein Limit festgelegt.

#### <a name="resolution"></a>Auflösung

Wenn Sie weitere Aktivierungen benötigen, wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers).

### <a name="0xc004c021-the-activation-server-reported-that-the-multiple-activation-key-extension-limit-has-been-exceeded"></a>0xC004C021 Der Aktivierungsserver hat berichtet, dass die DMAK-Erweiterungsgrenze überschritten wurde.

#### <a name="possible-cause"></a>Mögliche Ursache

Das Aktivierungslimit des MAK ist überschritten. Für die Anzahl der MAK-Aktivierungen wurde ein Limit festgelegt.

#### <a name="resolution"></a>Auflösung

Wenn Sie weitere Aktivierungen benötigen, wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers).

### <a name="0xc004f009-the-software-protection-service-reported-that-the-grace-period-expired"></a>0xC004F009 Vom Softwareschutzdienst wurde gemeldet, dass der Zeitraum bis zur Aktivierung abgelaufen ist.

#### <a name="possible-cause"></a>Mögliche Ursache

Der Aktivierungszeitraum ist abgelaufen, bevor das System aktiviert wurde. Das System hat jetzt den Status %%amp;quot;Benachrichtigungen%%amp;quot;.  

#### <a name="resolution"></a>Auflösung

Wenn Sie Hilfe benötigen, wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers).

### <a name="0xc004f00f-the-software-licensing-server-reported-that-the-hardware-id-binding-is-beyond-level-of-tolerance"></a>0xC004F00F Vom Softwarelizenzierungsdienst wurde gemeldet, dass bei der Hardware-ID-Bindung die Toleranzschwelle überschritten wurde.

#### <a name="possible-cause"></a>Mögliche Ursache

Die Hardware wurde geändert, oder die Treiber auf dem System wurden aktualisiert.  

#### <a name="resolution"></a>Auflösung

Wenn Sie die MAK-Aktivierung verwenden, aktivieren Sie das System innerhalb des OOT-Verlängerungszeitraums mit der Onlineaktivierung oder telefonischen Aktivierung erneut.  

Wenn Sie die KMS-Aktivierung verwenden, starten Sie Windows neu, oder führen Sie **slmgr.vsb /ato** aus.

### <a name="0xc004f014-the-software-protection-service-reported-that-the-product-key-is-not-available"></a>0xC004F014 Vom Softwareschutzdienst wurde gemeldet, dass der Product Key nicht verfügbar ist.

#### <a name="possible-cause"></a>Mögliche Ursache

Auf dem System sind keine Product Keys installiert.  

#### <a name="resolution"></a>Auflösung

Wenn Sie die MAK-Aktivierung verwenden, installieren Sie einen MAK-Product Key. 

Wenn Sie die KMS-Aktivierung verwenden, überprüfen Sie die Datei „Pid.txt“ (auf dem Installationsmedium im Ordner „\sources“) auf einen KMS-Setupschlüssel. Installieren Sie den Schlüssel.

### <a name="0xc004f02c-the-software-protection-service-reported-that-the-format-for-the-offline-activation-data-is-incorrect"></a>0xC004F02C Vom Softwareschutzdienst wurde gemeldet, dass das Format für die Offlineaktivierung falsch ist.

#### <a name="possible-cause"></a>Mögliche Ursache

Vom System wurde erkannt, dass die bei der telefonischen Aktivierung eingegebenen Daten nicht gültig sind.  

#### <a name="resolution"></a>Auflösung

Überprüfen Sie, ob Sie die CID richtig eingegeben haben.  

### <a name="0xc004f035-invalid-volume-license-key"></a>0xC004F035 Ungültiger Volumen-Lizenzschlüssel

Der vollständige Text dieser Fehlermeldung lautet wie folgt:

> Fehler: Ungültiger Volumen-Lizenzschlüssel. Sie müssen Ihren Product Key in einen gültigen Mehrfachaktivierungsschlüssel (Multi Activation Key, MAK) oder einen Verkaufsschlüssel ändern. Sie benötigen eine qualifizierende Lizenz für das Betriebssystem sowie eine Upgradelizenz der Windows 7-Volumen-Lizenzierung oder eine Lizenz für eine Windows 7-Vollversion aus dem Handel. ANDERE INSTALLATIONEN DIESER SOFTWARE STELLEN EINE VERLETZUNG DER LIZENZBESTIMMUNGEN UND GELTENDER URHEBERRECHTSGESETZE DAR.  

#### <a name="possible-cause"></a>Mögliche Ursache

Volumeneditionen von Windows 7 sind nur für Upgrades lizenziert. Von Microsoft wird das Installieren eines Volumenbetriebssystems auf einem Computer, auf dem kein qualifizierendes Betriebssystem installiert ist, nicht unterstützt.  

Dieser Fehlercode bedeutet Folgendes: „Vom Softwarelizenzierungsdienst wurde gemeldet, dass der Computer nicht mit dem Volumenlizenz-Product Key aktiviert werden konnte...“ Der Fehlertext ist zwar korrekt, aber nicht eindeutig. Dieser Fehler bedeutet, dass im BIOS des Computers ein Windows-Marker fehlt. Dieser Marker wird auf OEM-Systemen angezeigt, um Computer anzugeben, die mit den qualifizierenden Editionen von Windows ausgeliefert werden. Der Marker ist für die KMS-Clientaktivierung erforderlich.  

#### <a name="resolution"></a>Auflösung

Installieren Sie eine qualifizierende Version eines Microsoft-Betriebssystems, und aktivieren Sie sie mithilfe eines MAK.

### <a name="0xc004f038-the-count-reported-by-your-key-management-service-kms-is-insufficient"></a>0xC004F038 Die vom Schlüsselverwaltungsdienst (Key Management Service, KMS) gemeldete Anzahl ist nicht ausreichend.

Der vollständige Text dieser Fehlermeldung lautet wie folgt:

> Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Die vom Schlüsselverwaltungsdienst (Key Management Service, KMS) gemeldete Anzahl ist nicht ausreichend. Wenden Sie sich an den Systemadministrator.  

#### <a name="possible-cause"></a>Mögliche Ursache

Die Anzahl auf dem KMS-Host ist nicht hoch genug. Für Windows Server muss die KMS-Anzahl größer oder gleich 5 sein. Für Windows (Client) muss die KMS-Anzahl größer oder gleich 25 sein.  

#### <a name="resolution"></a>Auflösung
Bevor Sie Windows mithilfe von KMS aktivieren können, müssen Sie über weitere Computer im KMS-Pool verfügen. Führen Sie **Slmgr.vbs /dli** aus, um die aktuelle Anzahl auf dem KMS-Host abzurufen.  

### <a name="0xc004f039-the-key-management-service-kms-is-not-enabled"></a>0xC004F039 Der Schlüsselverwaltungsdienst (Key Management Service, KMS) ist nicht aktiviert.

Der vollständige Text dieser Fehlermeldung lautet wie folgt:

> Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Der Schlüsselverwaltungsdienst (Key Management Service, KMS) ist nicht aktiviert.  

#### <a name="possible-cause"></a>Mögliche Ursache

KMS hat nicht auf die KMS-Anforderung geantwortet.

#### <a name="resolution"></a>Auflösung

Führen Sie eine Problembehandlung für die Netzwerkverbindung zwischen dem KMS-Host und dem Client aus. Stellen Sie sicher, dass TCP-Port 1688 (Standard) nicht durch eine Firewall blockiert oder anderweitig gefiltert wird.

### <a name="0xc004f041-the-software-protection-service-determined-that-the-key-management-server-kms-is-not-activated"></a>0xC004F041 Vom Softwarelizenzierungsdienst wurde festgestellt, dass der Schlüsselverwaltungsserver (Key Management Server, KMS) nicht aktiviert ist.

Der vollständige Text dieser Fehlermeldung lautet wie folgt:

> Vom Softwarelizenzierungsdienst wurde festgestellt, dass der Schlüsselverwaltungsserver (Key Management Server, KMS) nicht aktiviert ist. Der KMS muss aktiviert werden.  

#### <a name="possible-cause"></a>Mögliche Ursache

Der KMS-Host ist nicht aktiviert.  

#### <a name="resolution"></a>Auflösung

Aktivieren Sie den KMS-Host online oder telefonisch.  

### <a name="0xc004f042-the-software-protection-service-determined-that-the-specified-key-management-service-kms-cannot-be-used"></a>0xC004F042 Der Softwareschutzdienst hat festgestellt, dass der angegebene Schlüsselverwaltungsdienst (KMS) nicht verwendet werden kann.

#### <a name="possible-cause"></a>Mögliche Ursache

Dieser Fehler tritt auf, wenn der KMS-Client Kontakt zu einem KMS-Host aufgenommen hat, von dem die Clientsoftware nicht aktiviert werden konnte. Dies kann beispielsweise häufig in gemischten Umgebungen mit anwendungsspezifischen und betriebssystemspezifischen KMS-Hosts auftreten.  

#### <a name="resolution"></a>Auflösung

Stellen Sie sicher, dass die KMS-Clients eine Verbindung mit den richtigen Hosts herstellen, wenn Sie bestimmte KMS-Hosts zum Aktivieren bestimmter Anwendungen oder Betriebssysteme verwenden.

### <a name="0xc004f050-the-software-protection-service-reported-that-the-product-key-is-invalid"></a>0xC004F050 Vom Softwareschutzdienst wurde ein ungültiger Product Key gemeldet.

#### <a name="possible-cause"></a>Mögliche Ursache

Dies kann durch einen Tippfehler im KMS-Schlüssel oder durch die Eingabe eines Schlüssels für eine Betaversion in einer endgültigen Version des Betriebssystems verursacht werden.  

#### <a name="resolution"></a>Auflösung

Installieren Sie den richtigen KMS-Schlüssel in der entsprechenden Version von Windows. Überprüfen Sie die Schreibweise. Wenn Sie den Schlüssel kopieren und einfügen, stellen Sie sicher, dass die Bindestriche im Schlüssel nicht durch Gedankenstriche ersetzt wurden.  

### <a name="0xc004f051-the-software-protection-service-reported-that-the-product-key-is-blocked"></a>0xC004F051 Vom Softwareschutzdienst wurde ein gesperrter Product Key gemeldet.

#### <a name="possible-cause"></a>Mögliche Ursache

Vom Aktivierungsserver wurde festgestellt, dass der Product Key von Microsoft gesperrt wurde.  

#### <a name="resolution"></a>Auflösung

Besorgen Sie sich einen neuen MAK- oder KMS-Schlüssel, installieren Sie diesen auf dem System, und führen Sie die Aktivierung durch.

### <a name="0xc004f064-the-software-protection-service-reported-that-the-non-genuine-grace-period-expired"></a>0xC004F064 Vom Softwarelizenzierungsdienst wurde gemeldet, dass der nicht-authentische Aktivierungszeitraum abgelaufen ist.

#### <a name="possible-cause"></a>Mögliche Ursache

Von den Windows-Aktivierungstools (WAT) wurde festgestellt, dass das System nicht authentisch ist.  

#### <a name="resolution"></a>Auflösung

Wenn Sie Hilfe benötigen, wenden Sie sich an die [Microsoft Licensing Activation Centers](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers).

### <a name="0xc004f065-the-software-protection-service-reported-that-the-application-is-running-within-the-valid-non-genuine-period"></a>0xC004F065 Vom Softwarelizenzierungsdienst wurde gemeldet, dass die Anwendung innerhalb des gültigen, nicht-authentischen Aktivierungszeitraums ausgeführt wird.

#### <a name="possible-cause"></a>Mögliche Ursache

Von den Windows-Aktivierungstools wurde festgestellt, dass das System nicht authentisch ist. Das System wird während des nicht-authentischen Aktivierungszeitraums weiter ausgeführt.  

#### <a name="resolution"></a>Auflösung

Fordern Sie einen Original-Product Key an, installieren Sie ihn, und aktivieren Sie das System während des Aktivierungszeitraums. Andernfalls wechselt das System am Ende des Aktivierungszeitraums in den Zustand „Benachrichtigungen“.

### <a name="0xc004f06c-the-request-timestamp-is-invalid"></a>0xC004F06C Der Anforderungszeitstempel ist ungültig.

Der vollständige Text dieser Fehlermeldung lautet wie folgt:

> Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Vom Schlüsselverwaltungsdienst (KMS) wurde festgestellt, dass der Zeitstempel der Anforderung ungültig ist.  

#### <a name="possible-cause"></a>Mögliche Ursache

Die Systemzeit des Clientcomputers weicht zu stark von der Uhrzeit auf dem KMS-Host ab. Die Zeitsynchronisierung ist aus verschiedenen Gründen für die System- und Netzwerksicherheit wichtig.  

#### <a name="resolution"></a>Auflösung

Beheben Sie das Problem, indem Sie die Systemzeit des Clients so ändern, dass diese mit dem KMS-Host synchronisiert ist. Für die Zeitsynchronisierung wird die Verwendung einer NTP-Zeitquelle (Network Time Protocol) oder die Verwendung von Active Directory Domain Services empfohlen. Bei diesem Problem wird unabhängig von der ausgewählten Zeitzone die UTP-Zeit verwendet.  

### <a name="0x80070005-access-denied"></a>0x80070005 Zugriff verweigert

Der vollständige Text dieser Fehlermeldung lautet wie folgt:

> Zugriff verweigert: Die angeforderte Aktion erfordert erhöhte Rechte.

#### <a name="possible-cause"></a>Mögliche Ursache

Die Ausführung von Aktivierungsprozessen an einem Eingabeaufforderungsfenster ohne erhöhte Rechte wird durch die Benutzerkontensteuerung (User Account Control, UAC) verhindert.  

#### <a name="resolution"></a>Auflösung

Führen Sie **slmgr.vbs** an einer Eingabeaufforderung mit erhöhten Rechten aus. Klicken Sie hierfür im **Startmenü** mit der rechten Maustaste auf **cmd.exe**, und wählen Sie dann **Als Administrator ausführen** aus.  

### <a name="0x8007232a-dns-server-failure"></a>0x8007232A DNS-Server Fehler

#### <a name="possible-cause"></a>Mögliche Ursache

Auf dem System liegen Netzwerkprobleme oder DNS-Probleme vor.

#### <a name="resolution"></a>Auflösung

Führen Sie eine Problembehandlung für das Netzwerk und für DNS aus.  

### <a name="0x8007232b-dns-name-does-not-exist"></a>0x8007232B Der DNS-Name ist nicht vorhanden.

#### <a name="possible-cause"></a>Mögliche Ursache

Vom KMS-Client können in DNS keine KMS-Serverresourceneinträge (SRV RRs) gefunden werden.  

#### <a name="resolution"></a>Auflösung

Überprüfen Sie, ob ein KMS-Host installiert ist und die DNS-Veröffentlichung aktiviert ist (Standard). Wenn DNS nicht verfügbar ist, verweisen Sie den KMS-Client auf den KMS-Host. Verwenden Sie dazu **slmgr.vbs /skms <*KMS-Hostname*>** .  

Wenn Sie über keinen KMS-Host verfügen, rufen Sie einen MAK ab, und installieren Sie ihn. Aktivieren Sie dann das System.

Weitere Informationen zur Behandlung solcher DNS-Probleme finden Sie unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).  

### <a name="0x800706ba-the-rpc-server-is-unavailable"></a>0x800706BA Der RPC-Server ist nicht verfügbar.

#### <a name="possible-cause"></a>Mögliche Ursache

Die Firewalleinstellungen auf dem KMS-Host sind nicht konfiguriert, oder die DNS SRV-Einträge sind veraltet.  

#### <a name="resolution"></a>Auflösung

Vergewissern Sie sich, dass auf dem KMS-Host eine Firewallausnahme für den Schlüsselverwaltungsdienst aktiviert ist (TCP-Port 1688).

Stellen Sie sicher, dass die DNS-SRV-Einträge auf einen gültigen KMS-Host zeigen. 

Führen Sie eine Problembehandlung für die Netzwerkverbindungen aus.  

Weitere Informationen zur Behandlung solcher DNS-Probleme finden Sie unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).  

### <a name="0x8007251d-no-records-found-for-dns-query"></a>0x8007251D Bei der DNS-Abfrage wurden keine Einträge gefunden.

#### <a name="possible-cause"></a>Mögliche Ursache

Vom KMS-Client können in DNS keine KMS-SRV-Einträge gefunden werden.

#### <a name="resolution"></a>Auflösung

Führen Sie eine Problembehandlung für die Netzwerkverbindungen und für DNS aus. Weitere Informationen zur Behandlung solcher DNS-Probleme finden Sie unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).  

### <a name="0xc004f074-no-key-management-service-kms-could-be-contacted"></a>0xC004F074 Es konnte kein Schlüsselverwaltungsdienst (Key Management Service, KMS) erreicht werden.

Der vollständige Text dieser Fehlermeldung lautet wie folgt:

> Vom Softwareschutzdienst wurde gemeldet, dass der Computer nicht aktiviert werden konnte. Es konnte kein Schlüsselverwaltungsdienst (Key Management Service, KMS) erreicht werden. Weitere Informationen finden Sie im Anwendungsereignisprotokoll.  

#### <a name="possible-cause"></a>Mögliche Ursache

Von allen KMS-Hostsystemen wurde ein Fehler zurückgegeben.  

#### <a name="resolution"></a>Auflösung

Identifizieren Sie im Anwendungsereignisprotokoll jedes Ereignis mit der Ereignis-ID 12288, das dem Aktivierungsversuch zugeordnet ist. Beheben Sie die Fehler dieser Ereignisse.

Weitere Informationen zur Behandlung von DNS-Problemen finden Sie unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).  

### <a name="0x8004fe21-this-computer-is-not-running-genuine-windows"></a>0x8004FE21 Auf diesem Computer wird keine Originalversion von Windows ausgeführt.  

#### <a name="possible-cause"></a>Mögliche Ursache

Dieses Problem kann verschiedene Ursachen haben. Am wahrscheinlichsten ist, dass Language Packs (MUI) auf Computern mit Windows-Editionen installiert wurden, die nicht für zusätzliche Sprachpakete lizenziert sind.  

> [!NOTE]
> Dieses Problem muss nicht unbedingt auf eine Manipulation hindeuten. Von einigen Anwendungen wird unter Umständen eine Unterstützung für mehrere Sprachen installiert, obwohl diese Edition von Windows nicht für die Language Packs lizenziert ist.  

Dieses Problem kann auch auftreten, wenn Windows durch Schadsoftware geändert wurde, um die Installation zusätzlicher Features zuzulassen. Darüber hinaus kann dieses Problem auftreten, wenn bestimmte Systemdateien beschädigt sind.  

#### <a name="resolution"></a>Auflösung

Zur Behebung dieses Problems muss das Betriebssystem neu installiert werden.  

### <a name="0x80092328-dns-name-does-not-exist"></a>0x80092328 Der DNS-Name ist nicht vorhanden.

#### <a name="possible-cause"></a>Mögliche Ursache

Dieses Problem kann auftreten, wenn der KMS-Client die KMS-Ressourceneinträge für Dienste (SRV) in DNS nicht findet. 

#### <a name="resolution"></a>Auflösung

Weitere Informationen zur Behandlung solcher DNS-Probleme finden Sie unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).  

### <a name="0x8007007b-dns-name-does-not-exist"></a>0x8007007b Der DNS-Name ist nicht vorhanden.

#### <a name="possible-cause"></a>Mögliche Ursache

Dieses Problem kann auftreten, wenn der KMS-Client die KMS-Ressourceneinträge für Dienste (SRV) in DNS nicht findet.  

#### <a name="resolution"></a>Auflösung

Weitere Informationen zur Behandlung solcher DNS-Probleme finden Sie unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).  

### <a name="0x80070490-the-product-key-you-entered-didnt-work"></a>0x80070490 Der eingegebene Product Key funktioniert nicht.

Der vollständige Text dieser Fehlermeldung lautet wie folgt:
> Der eingegebene Product Key funktioniert nicht. Überprüfen Sie den Product Key, und versuchen Sie es noch einmal, oder geben Sie einen anderen Product Key ein.  

#### <a name="possible-cause"></a>Mögliche Ursache

Dieses Problem ist auf die Eingabe eines ungültigen MAK oder auf ein bekanntes Problem in Windows Server 2019 zurückzuführen.  

#### <a name="resolution"></a>Auflösung

Um dieses Problem zu umgehen und den Computer zu aktivieren, führen Sie an einer Eingabeaufforderung mit erhöhten Rechten den Befehl **slmgr -ipk <5x5 key>** aus.
