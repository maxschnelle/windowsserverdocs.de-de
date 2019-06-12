---
title: Vorbereiten der Datei „CAPolicy.inf“
description: Die Datei "CAPolicy.inf" enthält verschiedene Einstellungen, die Wenn es sich bei dem Dienst Active Directory-Zertifizierung (AD CS) installieren oder Erneuern des Zertifizierungsstellenzertifikats verwendet werden.
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 19a87df7c4f165d3b0e6c5add4bc40ff97cc87cb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446460"
---
# <a name="capolicyinf-syntax"></a>CAPolicy.inf-Syntax
>   Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die Datei "CAPolicy.inf" handelt es sich um eine Konfigurationsdatei, die definiert, die Erweiterungen, Einschränkungen und andere Konfigurationseinstellungen, die ein Zertifikat einer Stammzertifizierungsstelle und alle von der Stamm-ZS ausgestellten Zertifikate angewendet werden. Die CAPolicy.inf-Datei muss auf einem Hostserver, bevor Sie die Setuproutine für den Stamm installiert werden, bei der Zertifizierungsstelle beginnt. Wenn die sicherheitseinschränkungen beim Stamm-ZS sind geändert werden, muss das Stammzertifikat erneuert werden, und eine aktualisierte Datei "CAPolicy.inf"-Datei muss auf dem Server installiert werden, bevor die Verlängerung durchführen beginnt.

Die Datei "CAPolicy.inf" ist:

-   Erstellt und manuell von einem Administrator definiert

-   Verwendet während der Erstellung der Stamm und untergeordnete ZS-Zertifikate

-   Definiert, die für die Signierung Zertifizierungsstelle, in dem Sie sich anmelden, und stellen Sie das Zertifikat (nicht die Zertifizierungsstelle, in dem die Anforderung nicht gewährt wird)

Nachdem Sie die Datei "CAPolicy.inf" erstellt haben, müssen Sie kopieren Sie ihn in die **%SystemRoot%** Ordner des Servers vor der Installation von AD CS und das ZS-Zertifikat zu erneuern.

Die Datei "CAPolicy.inf" ermöglicht das angeben und konfigurieren eine Vielzahl von Optionen und CA-Attribute. Der folgende Abschnitt beschreibt alle Optionen für Sie erstellen eine INF-Datei, die auf Ihre speziellen Anforderungen zugeschnitten sind.

## <a name="capolicyinf-file-structure"></a>Struktur der Datei "CAPolicy.inf"

Die folgenden Begriffe werden verwendet, um die INF-Datei-Struktur zu beschreiben:

-   _Abschnitt_ – ist ein Bereich der Datei, die eine logische Gruppe von Schlüsseln behandelt. Abschnittsnamen in INF-Dateien werden in Klammern angezeigt werden identifiziert. Viele, aber nicht alle Abschnitte dienen zum zertifikaterweiterungen zu konfigurieren.

-   _Schlüssel_ – ist der Name eines Eintrags und auf der linken Seite des Gleichheitszeichens wird angezeigt.

-   _Wert_ – ist der Parameter und rechts neben dem Gleichzeichen wird angezeigt.

Im folgenden Beispiel wird **[Version]** ist der Bereich, **Signatur** ist der Schlüssel, und **"\$Windows NT\$"** ist der Wert.

Beispiel:

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>Version

Gibt die Datei als INF-Datei an. Version ist der einzige Abschnitt erforderlich und muss am Anfang der Datei "CAPolicy.inf" sein.

###  <a name="policystatementextension"></a>PolicyStatementExtension

Enthält die Richtlinien, die von der Organisation definiert wurden und ob diese optional oder obligatorisch sind. Mehrere Richtlinien werden durch Kommas getrennt. Die Namen haben Bedeutung im Kontext einer bestimmten Bereitstellung oder in Bezug auf benutzerdefinierte Anwendungen, die das Vorhandensein dieser Richtlinien überprüft.

Für jede Richtlinie definiert wird muss ein Abschnitt, der die Einstellungen für diese bestimmte Richtlinie definiert sein. Für jede Richtlinie müssen Sie einen benutzerdefinierten Objektbezeichner (OID) angeben, und entweder den Text, angezeigt werden sollen als die Policy-Anweisung oder ein URL-Zeiger auf die richtlinienanweisung. Die URL kann in Form einer HTTP, FTP oder LDAP-URL sein.

Wenn Sie beabsichtigen, die beschreibenden Text in einer richtlinienanweisung haben, würde die nächsten drei Zeilen der Datei CAPolicy.inf wie aussehen:

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

Wenn Sie beabsichtigen, eine URL zu verwenden, um die richtlinienanweisung für die Zertifizierungsstelle zu hosten, würde nächsten drei Zeilen stattdessen wie aussehen:

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
```

Beachten Sie auch Folgendes:

-   Mehrere URL, und beachten Sie, dass Schlüssel werden unterstützt.

-   Beachten Sie, dass und URL-Schlüssel in der gleichen Richtlinienabschnitt werden unterstützt.

-   URLs mit Leerzeichen oder eine SMS mit Leerzeichen muss in Anführungszeichen gesetzt werden. Dies gilt für die **URL** drücken, unabhängig von den Abschnitt, in dem er angezeigt wird.

Ein Beispiel für mehrere Hinweise und URLs in einem Richtlinienabschnitt würde wie aussehen:

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

Sie können die Zertifikatsperrlisten-Verteilungspunkte (CDPs) für ein Stammzertifizierungsstellen-Zertifikat in der Datei "CAPolicy.inf" angeben.  Nach der Installation der Zertifizierungsstelle können Sie die CDP-URLs konfigurieren, die die Zertifizierungsstelle in jeder ausgestelltes Zertifikat enthält. Das Zertifikat der Stammzertifizierungsstelle zeigt die URLs, die in diesem Abschnitt der Datei "CAPolicy.inf" angegeben. 

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

Einige zusätzliche Informationen in diesem Abschnitt:
-   unterstützt:
    - HTTP 
    - Datei-URLs
    - LDAP-URLs 
    - Mehrere URLs
   
    >[!IMPORTANT]
    >HTTPS-URLs unterstützt nicht.

-   Anführungszeichen müssen URLs mit Leerzeichen setzen.

-   Wenn keine URLs – d. h. Wenn angegeben sind die **[CRLDistributionPoint]** Abschnitt in der Datei vorhanden ist, ist jedoch leer: die Zugriff auf Stelleninformationen-Erweiterung aus dem Stamm-CA-Zertifikat fehlt. Dies ist in der Regel besser, bei der Einrichtung einer Stamm-ZS. Windows führt keine sperrüberprüfung auf ein Stammzertifizierungsstellen-Zertifikat, damit die CDP-Erweiterung im Zertifikat einer Stammzertifizierungsstelle überflüssig ist.

-    ZS kann in UNC-Datei, z. B. auf eine Freigabe veröffentlichen, die den Ordner einer Website darstellt, in denen ein Client über HTTP abgerufen.

-   Verwenden Sie diesen Abschnitt nur, wenn Sie zum Einrichten einer Stamm-ZS oder erneuern das Zertifikat der Stammzertifizierungsstelle. Die Zertifizierungsstelle bestimmt, die untergeordneten Zertifizierungsstelle CDP-Erweiterungen.
   

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

Sie können die Autorität für die Informationen Zugriffspunkte in der Datei "CAPolicy.inf" für das Zertifikat der Stammzertifizierungsstelle angeben.

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

Einige Weitere Hinweise auf die Autorität für die Informationen zugreifen, Abschnitt:

-   Mehrere URLs werden unterstützt.

-   HTTP, FTP, LDAP und Datei-URLs werden unterstützt. HTTPS-URLs werden nicht unterstützt.

-   In diesem Abschnitt wird nur verwendet, wenn Sie zum Einrichten einer Stamm-ZS, oder das Zertifikat der Stammzertifizierungsstelle erneuern. Untergeordnete Zertifizierungsstelle AIA-Erweiterungen werden von der Zertifizierungsstelle bestimmt, die der untergeordnete ZS-Zertifikat ausgestellt hat.

-   URLs mit Leerzeichen müssen in Anführungszeichen gesetzt werden.

-   Wenn keine URLs – d. h. Wenn angegeben sind die **[AuthorityInformationAccess]** Abschnitt in der Datei vorhanden ist, ist jedoch leer: die Erweiterung der CRL-Verteilungspunkt aus dem Stamm-CA-Zertifikat fehlt. In diesem Fall wäre dies die bevorzugte Einstellung im Fall von Zertifizierungsstellen-Stammzertifikat, wie es ist keine Autorität, die höher als Stamm-ZS, die einen Link zu das Zertifikat verwiesen werden muss.

### <a name="certsrvserver"></a>certsrv_Server

Optionaler die Datei "CAPolicy.inf" den Abschnitt ist [Certsrv_server], womit Erneuerung Schlüssellänge, die Gültigkeitsdauer der Erneuerung und die Gültigkeitszeitraum der Zertifikatssperrliste (CRL) für eine Zertifizierungsstelle angeben, die erneuert oder installiert. Keine der Schlüssel in diesem Abschnitt sind erforderlich. Viele dieser Einstellungen haben Standardwerte, die sind ausreichend für die häufigsten Anforderungen, und können einfach aus der Datei "CAPolicy.inf" ausgelassen werden. Alternativ können viele dieser Einstellungen geändert werden, nach der Installation der Zertifizierungsstelle.

Ein Beispiel würde wie aussehen:

```
[certsrv_server]
RenewalKeyLength=2048
RenewalValidityPeriod=Years
RenewalValidityPeriodUnits=5
CRLPeriod=Days
CRLPeriodUnits=2
CRLDeltaPeriod=Hours
CRLDeltaPeriodUnits=4
ClockSkewMinutes=20
LoadDefaultTemplates=True
AlternateSignatureAlgorithm=0
ForceUTF8=0
EnableKeyCounting=0
```

**RenewalKeyLength** legt die Größe des Schlüssels für die Erneuerung. Dies wird nur verwendet, wenn während der Erneuerung eines Zertifikats ein neues Schlüsselpaar generiert wird. Die Größe des Schlüssels für das erste Zertifikat der Zertifizierungsstelle wird festgelegt, wenn die Zertifizierungsstelle installiert ist.

Beim erneuern ein Zertifikat mit einem neuen Schlüsselpaar, kann die Länge des Schlüssels entweder erhöht oder verringert werden. Wenn Sie einen Stamm-CA-Schlüsselgröße von 4096 Bytes oder höher festgelegt haben, und klicken Sie dann zu ermitteln, müssen Sie z. B. Java-apps oder Geräte, die nur Schlüssellängen von 2048 Bytes unterstützen können. Ob Sie vergrößern oder verkleinern, müssen Sie alle von dieser Zertifizierungsstelle ausgestellten Zertifikate neu ausstellen.

**RenewalValidityPeriod** und **RenewalValidityPeriodUnits** die Lebensdauer des neuen Stamm-CA-Zertifikats herzustellen, wenn das alte Stamm-CA-Zertifikat zu erneuern. Sie gilt nur für ein Stamm-ZS zu finden. Die Gültigkeitsdauer des Zertifikats von einer untergeordneten Zertifizierungsstelle richtet sich nach dem übergeordneten. RenewalValidityPeriod kann die folgenden Werte aufweisen: Stunden, Tagen, Wochen, Monate und Jahre.

**CRLPeriod** und **CRLPeriodUnits** richten Sie die Gültigkeitsdauer für die Basis-CRL. **CRLPeriod** können die folgenden Werte aufweisen: Stunden, Tagen, Wochen, Monate und Jahre.

**CRLDeltaPeriod** und **CRLDeltaPeriodUnits** die Gültigkeitsdauer der Delta-CRL herzustellen. **CRLDeltaPeriod** können die folgenden Werte aufweisen: Stunden, Tagen, Wochen, Monate und Jahre.

Jede dieser Einstellungen kann konfiguriert werden, nach der Installation der Zertifizierungsstelle:

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

Denken Sie daran, Active Directory Certificate Services für die Änderungen wirksam werden neu gestartet.

**LoadDefaultTemplates** gilt nur während der Installation von einer Unternehmenszertifizierungsstelle. Diese Einstellung entweder "true" oder "false" (oder 1 oder 0), schreibt vor, wenn die Zertifizierungsstelle mit einem der Standardvorlagen konfiguriert ist.

Eine Teilmenge der Standardzertifikatvorlagen wird in einer Standardinstallation der Zertifizierungsstelle das Zertifikatvorlagen-Ordner, in das Zertifizierungsstelle-Snap-in hinzugefügt. Dies bedeutet, dass, sobald der AD CS-Dienst gestartet wird, nach der Installation der Rolle einen Benutzer oder Computer mit ausreichenden Berechtigungen sofort für ein Zertifikat registrieren kann.

Möglicherweise möchten Sie keine Zertifikate ausstellen, sofort nach der Installation einer Zertifizierungsstelle, damit Sie die Einstellung LoadDefaultTemplates verwenden können, um zu verhindern, dass die Standardvorlagen Unternehmenszertifizierungsstelle hinzugefügt wird. Wenn es keine Vorlagen, die auf der Zertifizierungsstelle konfiguriert sind, können sie keine Zertifikate ausgeben.

**AlternateSignatureAlgorithm** konfiguriert die Zertifizierungsstelle so unterstützen das PKCS\#1 v2. 1-Signatur-Format für das Zertifizierungsstellenzertifikat und den zertifikatanforderungen. Bei Festlegung auf 1 auf einer Stamm-ZS das Zertifikat der Zertifizierungsstelle das PKCS enthält\#1 v2. 1-Signatur-Format. Bei Festlegung auf eine untergeordnete Zertifizierungsstelle, die untergeordnete Zertifizierungsstelle eine zertifikatanforderung erstellen, das der PKCS enthält\#1 v2. 1-Signatur-Format.

**ForceUTF8** ändert den Standard-Codierung des relativen definierten Namen (RDNs) in den Antragsteller und Aussteller-distinguished Names in UTF-8. Nur diese RDNs, die UTF-8, z. B. zu unterstützen, die definiert sind, als Verzeichnis Zeichenfolgen-Datentypen von einer RFC betroffen sind. Beispielsweise unterstützt der RDN für Domain-Komponente (DC) als IA5 oder UTF-8-Codierung während der Country RDN (C) nur unterstützt, wie eine druckbare Zeichenfolge codiert. Die Direktive ForceUTF8 wirkt sich daher auf einem DC RDN, jedoch wirkt sich nicht auf eine C-RDN.

**EnableKeyCounting** konfiguriert die Zertifizierungsstelle, um einen Zähler zu erhöhen, jedes Mal, wenn der ZS-Signaturschlüssel verwendet wird. Aktivieren Sie diese Einstellung nicht, es sei denn, Sie verfügen über ein Hardwaresicherheitsmodul (HSM) und die zugehörigen Kryptografiedienstanbieter (CSP), die wichtigsten zählen unterstützt. Microsoft starker CSP weder die Microsoft Software Schlüsselspeicheranbieter (KSP) Unterstützung für wichtige zählen.


## <a name="create-the-capolicyinf-file"></a>Erstellen Sie die Datei "CAPolicy.inf"

Bevor Sie AD CS installieren, konfigurieren Sie die CAPolicy.inf-Datei mit spezifischen Einstellungen für die Bereitstellung.

**Voraussetzung:** Sie müssen Mitglied der Gruppe "Administratoren" sein.

1. Geben Sie auf dem Computer, in dem Sie planen, installieren Sie AD CS, öffnen Sie Windows PowerShell, **Editor c:\CAPolicy.inf** und drücken Sie EINGABETASTE.

2. Klicken Sie auf **Ja**, wenn Sie zum Erstellen einer neuen Datei aufgefordert werden.

3. Geben Sie folgenden Dateiinhalt an:
   ```
   [Version]  
   Signature="$Windows NT$"  
   [PolicyStatementExtension]  
   Policies=InternalPolicy  
   [InternalPolicy]  
   OID=1.2.3.4.1455.67.89.5  
   Notice="Legal Policy Statement"  
   URL=https://pki.corp.contoso.com/pki/cps.txt  
   [Certsrv_Server]  
   RenewalKeyLength=2048  
   RenewalValidityPeriod=Years  
   RenewalValidityPeriodUnits=5  
   CRLPeriod=weeks  
   CRLPeriodUnits=1  
   LoadDefaultTemplates=0  
   AlternateSignatureAlgorithm=1  
   [CRLDistributionPoint]  
   [AuthorityInformationAccess]
   ```
4. Klicken Sie auf **Datei**, und klicken Sie dann auf **speichern**.

5. Navigieren Sie zum Ordner "% SystemRoot%".

6. Vergewissern Sie sich, dass folgende Bedingungen erfüllt sind:

   -   **Dateiname** ist auf **CAPolicy.inf**

   -   **Dateityp** ist auf **Alle Dateien** gesetzt.

   -   Die **Codierung** ist **ANSI**.

7. Klicken Sie auf **Speichern**.

8. Klicken Sie auf **Ja**, wenn Sie zum Überschreiben der Datei aufgefordert werden.

   ![Speichern Sie als Speicherort für die Datei "CAPolicy.inf"](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

   > [!CAUTION]
   >   Vergewissern Sie sich, dass die Datei %%amp;quot;CAPolicy.inf%%amp;quot; mit der Dateierweiterung INF gespeichert wurde. Wenn Sie am Ende des Dateinamens nicht ausdrücklich **.inf** eingeben und die beschriebenen Optionen auswählen, wird die Datei als Textdatei gespeichert und nicht während der Zertifizierungsstelleninstallation verwendet.

9. Schließen Sie Editor.

> [!IMPORTANT]
>   In der Datei "CAPolicy.inf", können Sie sehen, es gibt eine Zeile, in der URL https://pki.corp.contoso.com/pki/cps.txt. Der Abschnitt der Datei %%amp;quot;CAPolicy.inf%%amp;quot; zu den internen Richtlinien dient lediglich als Beispiel dafür, wie Sie den Speicherort einer Zertifikatverwendungserklärung (Certificate Practice Statement, CPS) angeben können. In diesem Handbuch werden Sie nicht angewiesen, um die praktischen Certificate-Anweisung (CPS) zu erstellen.
