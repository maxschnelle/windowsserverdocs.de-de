---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: "TPM-Schlüsselnachweis"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d08efe825e10d526763a1654c7e090427719c51
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="tpm-key-attestation"></a>TPM-Schlüsselnachweis

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

**"Author"**: Justin Turner, Senior Support Escalation Engineer mit der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wird von Microsoft Customer Support-Mitarbeiter geschrieben und richtet erfahrene Administratoren und Systemarchitekten, die als Themen auf TechNet finden Sie in der Regel einen tieferen technischen Einblick Funktionen und Lösungen in Windows Server 2012 R2 suchen. Allerdings hat es nicht die gleichen linguistischen damit einige der Sprache möglicherweise weniger glänzend als was in der Regel auf TechNet-Website gefunden wird.  
  
## <a name="overview"></a>(Übersicht)  
Dank der Unterstützung für TPM-geschützten Schlüsseln ist seit Windows8 gab es keine Mechanismen für Zertifizierungsstellen mit dem kryptografisch bestätigt, dass der private Schlüssel der Zertifikatanforderung tatsächlich durch ein Trusted Platform Module (TPM) geschützt ist. Dieses Update ermöglicht eine Zertifizierungsstelle, Nachweis ausführen und eine Rechnung zu tragen, Nachweis in das ausgestellte Zertifikat.  
  
> [!NOTE]  
> In diesem Artikel wird davon ausgegangen, dass der Leser mit Zertifikat Vorlage Konzept vertraut ist (Referenz, finden Sie unter [Zertifikatvorlagen](https://technet.microsoft.com/library/cc730705.aspx)). Es wird vorausgesetzt, dass der Leser mit der Vorgehensweise beim Konfigurieren von Unternehmens-ZS zum Ausstellen von Zertifikaten basierend auf Zertifikatvorlagen vertraut ist (Referenz, finden Sie unter [Prüfliste: Konfigurieren von Zertifizierungsstellen zum Ausstellen und Verwalten von Zertifikaten](https://technet.microsoft.com/library/cc771533.aspx)).  
  
### <a name="terminology"></a>Terminologie  
  
|Begriff|Definition|  
|--------|--------------|  
|EK|Endorsement Key. Dies ist eine asymmetrische Schlüssel im TPM (zum Zeitpunkt der Herstellung eingefügt) enthalten. Der EK für jedes TPM eindeutig ist und sie identifizieren. Der EK kann nicht geändert oder entfernt werden.|  
|EKpub|Bezieht sich auf den öffentlichen Schlüssel des den EK.|  
|EKPriv|Bezieht sich auf den privaten Schlüssel von den EK.|  
|EKCert|EK-Zertifikat. Ein TPM-Hersteller ausgestelltes-Zertifikat für EKPub. Nicht alle TPMs verfügen EKCert.|  
|TPM|Trusted Platform Module. Ein TPM dient zum Hardware-basierten sicherheitsbezogene Funktionen bereitzustellen. Ein TPM-Chip ist ein sicherer Krypto-Prozessor, der kryptografischer Vorgänge ausgelegt ist. Der Chip umfasst mehrere physische Sicherheitsmechanismen, die ihn manipulationssicher machen, und Schadsoftware ist nicht die Sicherheitsfunktionen des TPMS zu manipulieren.|  
  
### <a name="background"></a>Hintergrund  
Ab Windows8, kann ein Trusted Platform Module (TPM) verwendet werden, um private Schlüssel des Zertifikats zu schützen. Der Microsoft Plattform Krypto-Anbieter Schlüsselspeicheranbieter (KSP) können mithilfe dieser Funktion. Gab es zwei Probleme bei der Implementierung:  

-   Es wurde keine Garantie, dass ein Schlüssel tatsächlich durch ein TPM geschützt ist (eine Person kann problemlos eine Software-KSP als eine TPM-KSP mit lokalen Administratorrechten spoofen).

-   Es war nicht möglich, die Liste des TPMs zu beschränken, die zum Schutz von Unternehmen, die ausgestellte Zertifikate (die die PKI-Administrator die Arten von Geräten zu steuern, die Abrufen von Zertifikaten in der Umgebung verwendet werden kann möchte) zulässig sind.  

### <a name="tpm-key-attestation"></a>TPM-Schlüsselnachweis  
TPM-Schlüsselnachweis ist die Möglichkeit der Entität, die ein Zertifikat anfordern, kryptografisch eine Zertifizierungsstelle bestätigt, dass die RSA-Schlüssel in der Zertifikatanforderung durch "a" oder "das" TPM geschützt ist, der die Zertifizierungsstelle vertraut. Das TPM-Vertrauensmodell stark mehr der [Bereitstellungsübersicht](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview) weiter unten in diesem Thema.  
  
### <a name="why-is-tpm-key-attestation-important"></a>Warum ist die TPM-Schlüsselnachweis wichtig?  
Ein Benutzerzertifikat mit einem TPM-nachgewiesen Schlüssel bietet höhere Sicherheit anmeldedateneingabe, nicht exportiert, Anti-Hammering und Isolation von Schlüsseln, die vom TPM bereitgestellt.  
  
Mit TPM-Schlüsselnachweis, ein neues Management Paradigma ist jetzt möglich: ein Administrator kann den Satz von Geräten, das Benutzern den Zugriff auf Unternehmensressourcen (z.B. VPN- oder drahtlosen Zugriffspunkt) und haben definieren **starken** wird sichergestellt, dass keine anderen Geräte zum zugreifen darauf verwendet werden können. Ist dieses neue Steuerelement Paradigma für den Zugriff **starken**, da es, um gebunden ist eine *Hardware gebunden* Benutzeridentität, das sicherer als ein Software-basierten Anmeldeinformationen ist.
  
### <a name="how-does-tpm-key-attestation-work"></a>Wie funktioniert die TPM-Schlüsselnachweis?  
Im Allgemeinen basieren auf den folgenden Säulen TPM-Schlüsselnachweis:  
  
1.  Jedes TPM enthält einen eindeutigen asymmetrische Schlüssel bezeichnet die *Endorsement Key* (EK), die vom Hersteller gebrannt. Wir bezeichnen der öffentliche Teil eines dieser Schlüssel als *EKPub* und den zugehörigen privaten Schlüssel als *EKPriv*. Einige TPM-Chips verfügen außerdem über ein EK-Zertifikat, das vom Hersteller für die EKPub ausgestellt wird. Wir bezeichnen diese Zertifikat als *EKCert*.  
  
2.  Eine Zertifizierungsstelle wird das Vertrauen in das TPM, entweder über die EKPub oder EKCert hergestellt.  
  
3.  Ein Benutzer bewiesen, dass die Zertifizierungsstelle, dass die RSA-Schlüssel für den Anforderung des Zertifikats der EKPub kryptografisch verknüpft ist und der Benutzer die EKpriv besitzt.  
  
4.  Die Zertifizierungsstelle ein Zertifikat mit einem speziellen Ausstellungsrichtlinie OID darauf hin, dass der Schlüssel jetzt als Nachweis verwendet wird, die durch ein TPM geschützt werden.  
  
## <a name="BKMK_DeploymentOverview"></a>Übersicht über die Bereitstellung  
In dieser Bereitstellung wird davon ausgegangen, dass eine Windows Server2012 R2-Unternehmenszertifizierungsstelle eingerichtet ist. Das Zertifikat auch Clients (Windows8.1) konfiguriert sind, dass die Unternehmenszertifizierungsstelle mit registrieren Vorlagen. 

Es gibt drei Schrittezum Bereitstellen von TPM-Schlüsselnachweis:  
  
1.  **Planen der TPM-Vertrauensmodell:** im ersten Schrittentscheiden, welche TPM-Vertrauensmodell verwendet wird. Es gibt 3 unterstützten Möglichkeiten hierzu:  
  
    -   **Vertrauensstellung auf der Grundlage von Benutzeranmeldeinformationen:** Unternehmenszertifizierungsstelle vertraut der vom Benutzer bereitgestellte EKPub im Rahmen der Zertifikatanforderung und keine Überprüfung ausgeführt wird als Anmeldeinformationen für die Domäne des Benutzers.  
  
    -   **Vertrauensstellung basierend auf EKCert:** Unternehmenszertifizierungsstelle überprüft die EKCert-Zertifikatkette, die im Rahmen der Zertifikatanforderung, mit einer Liste vom Administrator verwaltet bereitgestellt wird *akzeptabel EK-Zertifikat Ketten*. Die zulässigen Ketten sind pro Hersteller definiert und werden die über zwei benutzerdefinierte Zertifikatspeicher auf der ausstellenden Zertifizierungsstelle (einen Store für die mittlere) und eine für die Stamm-Zertifizierungsstellenzertifikate ausgedrückt werden. Dieser vertrauensstellungsmodus bedeutet, dass **alle** TPMs von einem bestimmten Hersteller vertrauenswürdig sind. Beachten Sie, dass in diesem Modus TPMs in der Umgebung verwendeten EKCerts enthalten müssen.
  
    -   **Vertrauensstellung basierend auf EKPub:** Unternehmenszertifizierungsstelle überprüft, dass die EKPub als Teil der Zertifikatanforderung in einer vom Administrator verwaltet angezeigt wird bereitgestellt EKPubs zulässig. Diese Liste wird als ein Verzeichnis mit Dateien ausgedrückt, in denen die Namen der einzelnen Dateien in dieses Verzeichnis der SHA-2 Hash der zulässigen EKPub ist. Diese Option bietet die höchstmögliche Sicherheit jedoch erfordert mehr Verwaltungsaufwand, da jedes Gerät einzeln identifiziert wird. In diesem Modell Vertrauensstellung dürfen nur die Geräte, auf denen ihr TPM-EKPub hinzugefügt, um die Liste der zulässigen EKPubs Registrierung für ein Zertifikat als TPM-Nachweis verwendet.  
  
    Je nachdem, welche Methode verwendet wird wird die Zertifizierungsstelle eine unterschiedliche Ausstellungsrichtlinie OID auf das ausgestellte Zertifikat angewendet. Weitere Informationen zu Ausstellungsrichtlinie OIDs, finden Sie unter der Tabelle Ausstellung Richtlinie OIDs in der [Konfigurieren einer Zertifikatvorlage](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate) in diesem Thema.  
  
    Beachten Sie, dass es möglich ist, wählen Sie eine Kombination aus TPM Trust Modelle. In diesem Fall wird die Zertifizierungsstelle akzeptiert den Nachweis Methoden und die Ausstellungsrichtlinie, die OIDs alle Nachweis Methoden wiedergibt, die erfolgreich ausgeführt werden.  
  
2.  **Konfigurieren der Zertifikatvorlage:** Konfigurieren der Zertifikatvorlage wird beschrieben, der [Bereitstellungsdetails](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails) in diesem Thema. In diesem Artikel nicht behandelt, wie diese Zertifikatvorlage die Unternehmenszertifizierungsstelle zugewiesen ist oder wie registrieren erhält Zugriff auf eine Gruppe von Benutzern. Weitere Informationen finden Sie unter [Prüfliste: Konfigurieren von Zertifizierungsstellen zum Ausstellen und Verwalten von Zertifikaten](https://technet.microsoft.com/library/cc771533.aspx).  
  
3.  **Konfigurieren Sie die Zertifizierungsstelle für das TPM-Vertrauensmodell**  
  
    1.  **Vertrauensstellung auf der Grundlage von Benutzeranmeldeinformationen:** keine spezielle Konfiguration erforderlich ist.  
  
    2.  **Vertrauensstellung basierend auf EKCert:** der Administrator die EKCert-Zertifikatkette Zertifikate von TPM-Hersteller erhalten muss, und importieren Sie sie in zwei neue Zertifikatspeicher, erstellt der Administrator auf der Zertifizierungsstelle, die TPM-Schlüsselnachweis ausführen. Weitere Informationen finden Sie in der [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    3.  **Vertrauensstellung basierend auf EKPub:** der Administrator muss die EKPub für jedes Gerät, die als TPM-Nachweis verwendet Zertifikate erforderlich und fügen sie der Liste der zulässigen EKPubs erhalten. Weitere Informationen finden Sie in der [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    > [!NOTE]  
    > -   Dieses Feature erfordert Windows8.1 / Windows Server2012 R2.  
    > -   TPM-Schlüsselnachweis für Drittanbieter-Smartcard-Schlüsselspeicheranbieter (KSPs) wird nicht unterstützt. Microsoft-Plattform-KSP. Krypto-Anbieter muss verwendet werden.  
    > -   TPM-Schlüsselnachweis funktioniert nur für RSA-Schlüssel.  
    > -   TPM-Schlüsselnachweis wird für eine eigenständige Zertifizierungsstelle nicht unterstützt.  
    > -   TPM-Schlüsselnachweis unterstützt keine [nicht persistente Zertifikat Verarbeitung](https://technet.microsoft.com/library/ff934598).  
  
## <a name="BKMK_DeploymentDetails"></a>Bereitstellungsdetails  
  
### <a name="BKMK_ConfigCertTemplate"></a>Konfigurieren einer Zertifikatvorlage  
Führen Sie die folgenden Konfigurationsschritte aus, um die Zertifikatvorlage für TPM-Schlüsselnachweise konfigurieren:  
  
1.  **Kompatibilität** Registerkarte  
  
    In der **Kompatibilitätseinstellungen** Abschnitt:  
  
    -   Stellen Sie sicher **Windows Server2012 R2** ausgewählt ist, für die **Zertifizierungsstelle**.  
  
    -   Stellen Sie sicher **Windows8.1 / Windows Server2012 R2** ausgewählt ist, für die **Zertifikatsempfänger**.  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **Kryptografie** Registerkarte  
  
    Stellen Sie sicher **Key Storage Provider** ausgewählt ist, für die **Anbieterkategorie** und **RSA** ausgewählt ist, für die **Name des Algorithmus**. Stellen Sie sicher **Anforderungen müssen einer der folgenden Anbieter verwenden** ausgewählt ist und die **Microsoft-Plattform-Kryptografieanbieter** ausgewählt ist unter **Anbieter**.  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **Schlüsselnachweis** Registerkarte  
  
    Dies ist eine neue Registerkarte für Windows Server2012 R2:  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    Wählen Sie eine nachweismodus aus drei möglichen Optionen.  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **Keine:** setzt voraus, dass Schlüsselnachweis nicht verwendet werden dürfen  
  
    -   **Erforderlich, wenn der Client kann:** ermöglicht Benutzern das auf einem Gerät, das keine TPM Schlüssel Nachweis zum Registrieren für das Zertifikat weiterhin. Nachweis ausführen, können Benutzer werden mit einer speziellen Ausstellungsrichtlinie OID unterschieden werden. Einige Geräte sind möglicherweise nicht in der Nachweis aufgrund einer alten TPM ausführen, die den Schlüsselnachweis nutzen, oder das Gerät nicht auf allen über ein TPM nicht unterstützt.
  
    -   **Erforderlich:** Client *müssen* TPM-Schlüsselnachweis ausführen, andernfalls schlägt die Anforderung fehl.  
  
    Wählen Sie dann das TPM-Vertrauensmodell. Erneut stehen drei Optionen:  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **Benutzeranmeldeinformationen:** ein authentifizierenden Benutzer für eine gültige TPM Bürgen durch Angabe der Anmeldeinformationen für die Domäne.  
  
    -   **Endorsement-Zertifikat:** der EKCert des Geräts muss über vom Administrator verwaltet TPM Zwischenzertifizierungsstellen-Zertifikate auf einer vom Administrator verwaltet Stammzertifizierungsstellen-Zertifikat überprüfen. Wenn Sie diese Option auswählen, müssen Sie einrichten EKCA und EKRoot Zertifikatspeichern auf der ausstellenden Zertifizierungsstelle wie unter dem [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    -   **Endorsement Key:** der EKPub des Geräts muss angezeigt werden, in der Liste für die PKI-Administrator verwaltet. Diese Option bietet die höchstmögliche Sicherheit jedoch weitere Verwaltungsaufwand erfordert. Wenn Sie diese Option auswählen, müssen Sie Einrichten einer EKPub-Liste auf der ausstellenden Zertifizierungsstelle wie unter dem [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    Legen Sie die Ausstellungsrichtlinie in das ausgestellte Zertifikat angezeigt. Jeder Erzwingungstyp verfügt standardmäßig über einen zugeordneten Objektbezeichner (OID), der in das Zertifikat eingefügt wird, wenn er dieses Typs Erzwingung übergeben, wie in der folgenden Tabelle beschrieben. Beachten Sie, dass es möglich ist, wählen Sie eine Kombination von Methoden. In diesem Fall die Zertifizierungsstelle akzeptiert der Nachweis Methoden, und die Ausstellungsrichtlinie OID entsprechen den alle Nachweis-Methoden, die erfolgreich war.  
  
    **Ausstellung Richtlinie OIDs**  
  
    |OID|Schlüsselnachweis Typ|Beschreibung|Sicherheitsstufe|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|"EK überprüft": Liste vom Administrator verwaltet, der EK|Hoch|  
    |1.3.6.1.4.1.311.21.31|Endorsement-Zertifikat|"EK-Zertifikat überprüft": Wenn EK-Zertifikatkette überprüft wird|Mittel|  
    |1.3.6.1.4.1.311.21.32|Benutzeranmeldeinformationen|"Bei der Verwendung als EK vertrauenswürdig": für Benutzer nachgewiesen EK|Niedrig|  
  
    Die OIDs werden in das ausgestellte Zertifikat eingefügt werden, wenn **Ausstellungsrichtlinien enthalten** ist aktiviert (Standardeinstellung).  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > Eine mögliche Verwendung Probleme OID das Zertifikat ist das Beschränken des Zugriffs auf VPN oder Drahtlosnetzwerke für bestimmte Geräte. Ihre Zugriffsrichtlinie kann z.B. Verbindung (oder den Zugriff auf ein anderes VLAN) zulassen, wenn OID 1.3.6.1.4.1.311.21.30 im Zertifikat vorhanden ist. Dadurch können Sie den Zugriff auf Geräte beschränken, deren TPM EK in der EKPUB-Liste vorhanden ist.  
  
### <a name="BKMK_CAConfig"></a>Konfiguration der Zertifizierungsstelle  
  
1.  **Setup-EKCA und EKROOT Zertifikatspeicher auf eine ausstellende Zertifizierungsstelle**  
  
    Wenn Sie gewählt haben **Endorsement-Zertifikat** für die Einstellungen für Vorlagen, führen Sie die folgenden Konfigurationsschritte aus:  
  
    1.  Verwenden Sie Windows PowerShell, um zwei neue Zertifikatspeicher auf den Server der Zertifizierungsstelle (CA) zu erstellen, die TPM-Schlüsselnachweis ausgeführt werden.  
  
    2.  Abrufen der fortgeschrittene und Stamm-Zertifizierungsstellenzertifikate von Herstellern, die Sie in Ihrer Umgebung zulassen möchten. Diese Zertifikate müssen in der zuvor erstellten Zertifikatspeicher (EKCA und EKROOT) nach Bedarf importiert werden.  
  
    Das folgende Windows PowerShell-Skript führt beide der folgenden Schritteaus. Im folgenden Beispiel hat Fabrikam die TPM-Hersteller bereitgestellt, ein Stammzertifikat *FabrikamRoot.cer* und eines Zertifizierungsstellenzertifikats der ausstellenden *Fabrikamca.cer*.  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **Einrichten der EKPUB-Liste EK Nachweis verwenden**  
  
    Wenn Sie gewählt haben **Endorsement Key** in den Vorlageneinstellungen für die, die nächsten Konfigurationsschritte zum Erstellen und konfigurieren einen Ordner auf der ausstellenden Zertifizierungsstelle, die mit 0-Byte-Dateien, jeweils mit dem Namen für den Hash SHA-2 eine zulässige EK. In diesem Ordner dient als eine "Liste zugelassener Websites" von Geräten, die berechtigt sind, die TPM-Key nachgewiesen Zertifikate abrufen. Da die EKPUB für jedes Gerät manuell hinzufügen müssen, die eine nachgewiesene Zertifikat erfordert bietet es Unternehmen bei der Geräte, die berechtigt sind, die TPM-nachgewiesene Zertifikate zu erhalten. Konfigurieren von einer Zertifizierungsstelle für diesen Modus sind zwei Schritteerforderlich:  
  
    1.  **Erstellen Sie den Registrierungseintrag EndorsementKeyListDirectories:** verwenden Sie das Befehlszeilentool "Certutil" So konfigurieren Sie die Speicherorte, in dem vertrauenswürdigen EKpubs definiert werden, wie in der folgenden Tabelle beschrieben.  
  
        |Vorgang|Syntax des Befehls|  
        |-------------|------------------|  
        |Hinzufügen von Ordnern|Certutil.exe - Setreg CA\EndorsementKeyListDirectories + "<folder>"|  
        |Entfernen von Ordnern|Certutil.exe - Setreg CA\EndorsementKeyListDirectories-"<folder>"|  
  
        Die EndorsementKeyListDirectories im Certutil-Befehl ist eine Einstellung in der Registrierung in der folgenden Tabelle beschrieben.  
  
        |Wertname|Typ|Daten|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< lokaler oder UNC-Pfad zum EKPUB können Listen ><br /><br />Beispiel:<br /><br />*\\\blueCA.contoso.com\ekpub*<br /><br />*\\\bluecluster1.contoso.com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration\\<CA Sanitized Name>  
  
        *EndorsementKeyListDirectories* enthält eine Liste der UNC- oder lokale System Dateipfade, die jeweils auf einen Ordner, der die Zertifizierungsstelle über Lesezugriff verfügt. Jeder Ordner kann 0 (null) enthalten oder mehr zulassen Listeneinträge, steht für jeden Eintrag eine Datei mit einem Namen, der die SHA-2 Hash von einer vertrauenswürdigen EKpub, keine Erweiterung. 
        Erstellen oder Bearbeiten von dieser Konfiguration der Registrierung Schlüssel erfordert einen Neustart der Zertifizierungsstelle, wie vorhandene Configuration Registrierungseinstellungen der Zertifizierungsstelle. Jedoch Änderungen an der Konfigurationseinstellung werden sofort wirksam und die Zertifizierungsstelle neu gestartet werden, ist nicht erforderlich.  
  
        > [!IMPORTANT]  
        > Sichern Sie die Ordner in der Liste vor Manipulation und nicht autorisierten Zugriff durch die Berechtigungen so konfigurieren, dass nur autorisierte Administratoren verfügen über Lese- und Schreibzugriff. Das Computerkonto der Zertifizierungsstelle ist nur Lesezugriff erforderlich.  
  
    2.  **Auffüllen die EKPUB-Liste:** verwenden Sie das folgende Windows PowerShell-Cmdlet, um Hash für öffentliche Schlüssel von den EK TPM abrufen, indem Sie mithilfe von Windows PowerShell auf jedem Gerät und öffentlichen Schlüssel, der die Zertifizierungsstelle Hashwert, und speichern Sie sie auf den Ordner EKPubList senden.  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublickKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>Problembehandlung  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>Schlüsselnachweis Felder sind nicht verfügbar für eine Zertifikatvorlage  
Die Schlüsselnachweis Felder sind nicht verfügbar, wenn die Vorlageneinstellungen die Anforderungen für den Nachweis nicht erfüllen. Häufige Ursachen sind:  
  
1.  Die Kompatibilitätseinstellungen sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass sie wie folgt konfiguriert werden:  
  
    1.  **Zertifizierungsstelle**: **Windows Server2012 R2**  
  
    2.  **Zertifikat Empfänger**: **Windows8.1 / Windows Server2012 R2**  
  
2.  Die Kryptografieeinstellungen sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass sie wie folgt konfiguriert werden:  
  
    1.  **Anbieterkategorie**: **Key Storage Provider**  
  
    2.  **Name des Algorithmus**: **RSA**  
  
    3.  **Anbieter**: **Kryptografieanbieter für Microsoft-Plattform**  
  
3.  Die Anforderung Behandlung Einstellungen sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass sie wie folgt konfiguriert werden:  
  
    1.  Die **Exportieren von privatem Schlüssel zulassen** Option muss nicht ausgewählt werden.  
  
    2.  Die **privaten Schlüssel des Antragstellers Verschlüsselung archivieren** Option muss nicht ausgewählt werden.  
  
### <a name="verification-of-tpm-device-for-attestation"></a>Überprüfung der TPM-Gerät für den Nachweis  
Verwenden Sie das Windows PowerShell-Cmdlet **bestätigen CAEndorsementKeyInfo**, um sicherzustellen, dass ein bestimmtes TPM-Gerät für den Nachweis von Zertifizierungsstellen als vertrauenswürdig eingestuft wird. Es gibt zwei Optionen: eine für die Überprüfung der EKCert und die andere für die Überprüfung einer EKPub. Das Cmdlet ist entweder lokal auf einer Zertifizierungsstelle oder auf Remote-Zertifizierungsstellen ausgeführt werden mithilfe von Windows PowerShell-Remoting.  
  
1.  Führen Sie für die Überprüfung der Vertrauenswürdigkeit auf eine EKPub die folgenden beiden Schritteaus:  
  
    1.  **Extrahieren Sie die EKPub vom Clientcomputer:** der EKPub extrahiert werden können, von einem Clientcomputer über **Get TpmEndorsementKeyInfo**. Führen Sie eine Eingabeaufforderung mit erhöhten Rechten Folgendes ein:  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **Vergewissern Sie sich auf eine EKCert auf einem Zertifizierungsstellencomputer vertrauen:** kopieren Sie die extrahierte Zeichenfolge (der SHA-2 Hash der EKPub) auf den Server (z.B. per E-Mail), und übergeben Sie es an das Cmdlet bestätigen CAEndorsementKeyInfo. Beachten Sie, dass dieser Parameter 64 Zeichen lang sein muss.  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  Führen Sie für die Überprüfung der Vertrauenswürdigkeit auf eine EKCert die folgenden beiden Schritteaus:  
  
    1.  **Extrahieren Sie die EKCert vom Clientcomputer:** der EKCert extrahiert werden können, von einem Clientcomputer über **Get TpmEndorsementKeyInfo**. Führen Sie eine Eingabeaufforderung mit erhöhten Rechten Folgendes ein:  
  
        ```  
        PS C:>\$a= Get- TpmEndorsementKeyInfo  
        PS C:>\$a.manufacturerCertificates|Export-Certificate c:\myEkcert.cer  
        ```  
  
    2.  **Vergewissern Sie sich auf eine KCert auf einem Zertifizierungsstellencomputer vertrauen:** kopieren Sie die extrahierten EKCert-(EkCert.cer) an die Zertifizierungsstelle (z.B. per E-Mail oder Xcopy). Beispiel: Wenn Sie die Zertifikatdatei des Ordners "c:\Diagnose" auf dem Zertifizierungsstellenserver kopieren, führen Sie Folgendes ein, um die Überprüfung abzuschließen:  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>Siehe auch  
[Trusted Platform Module – Technologieübersicht](https://technet.microsoft.com/library/jj131725.aspx)  
[Externe Ressource: Trusted Platform Module](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)  
  


