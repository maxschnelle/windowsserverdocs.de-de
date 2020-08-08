---
title: Vorbereiten der Datei „CAPolicy.inf“
description: Die Datei CAPolicy. inf enthält verschiedene Einstellungen, die bei der Installation des Active Directory Zertifizierungs Dienstanbieter (AD CS) oder beim Erneuern des Zertifizierungsstellen Zertifikats verwendet werden.
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 83e2acbc9edfd9ca236f01b1fef3474ffe1bbb51
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949454"
---
# <a name="capolicyinf-syntax"></a>CAPolicy. inf-Syntax
>   Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die Datei "capolicy. inf" ist eine Konfigurationsdatei, die Erweiterungen, Einschränkungen und andere Konfigurationseinstellungen definiert, die auf ein Zertifikat der Stamm Zertifizierungsstelle und alle von der Stamm Zertifizierungsstelle ausgestellten Zertifikate angewendet werden. Die Datei CAPolicy. inf muss auf einem Host Server installiert werden, bevor die Setup Routine für die Stamm Zertifizierungsstelle beginnt. Wenn die Sicherheitseinschränkungen für eine Stamm Zertifizierungsstelle geändert werden sollen, muss das Stamm Zertifikat erneuert und eine aktualisierte CAPolicy. inf-Datei auf dem Server installiert werden, bevor der Erneuerungs Vorgang beginnt.

"Capolicy. inf" ist:

-   Erstellt und manuell von einem Administrator definiert

-   Während der Erstellung von Stamm-und untergeordneten Zertifizierungsstellen Zertifikaten verwendet

-   Definiert in der Signatur Zertifizierungsstelle, an der Sie das Zertifikat signieren und ausstellen (nicht die Zertifizierungsstelle, an der die Anforderung erteilt wurde)

Nachdem Sie die Datei CAPolicy. inf erstellt haben, müssen Sie Sie in den Ordner **% systemroot%** des Servers kopieren, bevor Sie ADCs installieren oder das Zertifizierungsstellen Zertifikat erneuern.

Die CAPolicy. inf ermöglicht es, eine Vielzahl von ZS-Attributen und-Optionen anzugeben und zu konfigurieren. Im folgenden Abschnitt werden alle Optionen beschrieben, mit denen Sie eine INF-Datei erstellen können, die auf Ihre spezifischen Anforderungen zugeschnitten ist.

## <a name="capolicyinf-file-structure"></a>Struktur der CAPolicy. inf-Datei

Die folgenden Begriffe werden verwendet, um die INF-Dateistruktur zu beschreiben:

-   _Abschnitt_ – ist ein Bereich der Datei, in der eine logische Gruppe von Schlüsseln behandelt wird. Abschnittsnamen in INF-Dateien werden identifiziert, indem Sie in Klammern angezeigt werden. Viele, aber nicht alle Abschnitte werden zum Konfigurieren von Zertifikat Erweiterungen verwendet.

-   _Key_ – ist der Name eines Eintrags und wird links neben dem Gleichheitszeichen angezeigt.

-   _Value_ – ist der Parameter und wird rechts neben dem Gleichheitszeichen angezeigt.

Im folgenden Beispiel ist **[Version]** der-Abschnitt, **Signature** ist der Schlüssel, und **" \$ Windows NT \$ "** ist der Wert.

Beispiel:

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>Version

Identifiziert die Datei als INF-Datei. Die Version ist der einzige erforderliche Abschnitt und muss am Anfang der Datei "capolicy. inf" vorliegen.

###  <a name="policystatementextension"></a>Policystatus-TExtension

Listet die von der Organisation definierten Richtlinien auf und ob Sie optional oder obligatorisch sind. Mehrere Richtlinien werden durch Kommas getrennt. Die Namen haben eine Bedeutung im Kontext einer bestimmten Bereitstellung oder in Bezug auf benutzerdefinierte Anwendungen, die überprüfen, ob diese Richtlinien vorhanden sind.

Für jede definierte Richtlinie muss ein Abschnitt vorhanden sein, der die Einstellungen für diese bestimmte Richtlinie definiert. Für jede Richtlinie müssen Sie einen benutzerdefinierten Objekt Bezeichner (OID) und entweder den Text, der als Richtlinien Anweisung angezeigt werden soll, oder einen URL-Zeiger auf die Richtlinien Anweisung angeben. Die URL kann in Form einer HTTP-, FTP-oder LDAP-URL vorliegen.

Wenn Sie in der Policy-Anweisung beschreibenden Text haben werden, sehen die nächsten drei Zeilen der CAPolicy. inf wie folgt aus:

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

Wenn Sie eine URL zum Hosten der ZS-Richtlinien Anweisung verwenden, sehen die nächsten drei Zeilen stattdessen wie folgt aus:

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
```

Berücksichtigen Sie zudem Folgendes:

-   Mehrere URL-und Hinweis Schlüssel werden unterstützt.

-   Beachten Sie, dass die URL-Schlüssel im gleichen Richtlinien Abschnitt unterstützt werden.

-   URLs, die Leerzeichen oder Text mit Leerzeichen enthalten, müssen in Anführungszeichen eingeschlossen werden. Dies gilt für den **URL** -Schlüssel, unabhängig von dem Abschnitt, in dem er angezeigt wird.

Ein Beispiel für mehrere Hinweise und URLs in einem Richtlinien Abschnitt sieht wie folgt aus:

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

Sie können CRL-Verteilungs Punkte (CDPs) für ein Zertifikat der Stamm Zertifizierungsstelle in der Datei "capolicy. inf" angeben.  Nach der Installation der Zertifizierungsstelle können Sie die CDP-URLs konfigurieren, die in den einzelnen ausgestellten Zertifikaten enthalten sind. Das Zertifikat der Stamm Zertifizierungsstelle zeigt die URLs an, die in diesem Abschnitt der Datei "capolicy. inf" angegeben sind.

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

Weitere Informationen zu diesem Abschnitt:
-   Unterstützt:
    - HTTP
    - Datei-URLs
    - LDAP-URLs
    - Mehrere URLs

    >[!IMPORTANT]
    >HTTPS-URLs werden von nicht unterstützt.

-   Anführungszeichen müssen URLs mit Leerzeichen umschließen.

-   Wenn keine URLs angegeben werden – d. h., wenn der Abschnitt **[CRLDistributionPoint]** in der Datei vorhanden ist, aber leer ist – wird die CRL-Verteilungs Punkt Erweiterung aus dem Zertifikat der Stamm Zertifizierungsstelle ausgelassen. Dies ist in der Regel vorzuziehen, wenn Sie eine Stamm Zertifizierungsstelle einrichten. Windows führt keine Sperr Überprüfung für ein Zertifikat der Stamm Zertifizierungsstelle aus, sodass die CDP-Erweiterung in einem Zertifikat der Stamm Zertifizierungsstelle überflüssig ist.

-    Die Zertifizierungsstelle kann in der Datei "UNC" veröffentlichen, z. b. in einer Freigabe, die den Ordner einer Website darstellt, in der ein Client über HTTP abruft.

-   Verwenden Sie diesen Abschnitt nur, wenn Sie eine Stamm Zertifizierungsstelle einrichten oder das Zertifikat der Stamm Zertifizierungsstelle erneuern. Die Zertifizierungsstelle bestimmt die CDP-Erweiterungen der untergeordneten Zertifizierungsstelle.


### <a name="authorityinformationaccess"></a>Autorityinformationaccess

Sie können in der Datei "capolicy. inf" für das Zertifikat der Stamm Zertifizierungsstelle die Zugriffspunkte für die Zertifizierungsstelle angeben.

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

Weitere Hinweise zum Abschnitt "Autoritäts Informations Zugriff":

-   Es werden mehrere URLs unterstützt.

-   HTTP-, FTP-, LDAP-und Datei-URLs werden unterstützt. HTTPS-URLs werden nicht unterstützt.

-   Dieser Abschnitt wird nur verwendet, wenn Sie eine Stamm Zertifizierungsstelle einrichten oder das Zertifikat der Stamm Zertifizierungsstelle erneuern. Untergeordnete ZS-AIA-Erweiterungen werden von der Zertifizierungsstelle bestimmt, die das Zertifikat der untergeordneten Zertifizierungsstelle ausgestellt hat

-   URLs mit Leerzeichen müssen in Anführungszeichen eingeschlossen werden.

-   Wenn keine URLs angegeben werden – d. h., wenn der Abschnitt **[autorityinformationaccess]** in der Datei vorhanden ist, aber leer ist – wird die Erweiterung des Zertifizierungsstellen Informations Zugriffs im Zertifikat der Stamm Zertifizierungsstelle ausgelassen. Dies wäre wiederum die bevorzugte Einstellung im Fall eines Zertifikats der Stamm Zertifizierungsstelle, da keine Zertifizierungsstelle vorhanden ist, auf die durch einen Link zum Zertifikat verwiesen werden muss.

### <a name="certsrv_server"></a>certsrv_Server

Ein weiterer Optionaler Abschnitt der Datei "capolicy. inf" ist [Certsrv_Server], mit der die Länge des Erneuerungs Schlüssels, der Erneuerungs Gültigkeitsdauer und die Zertifikat Sperr Listen-Gültigkeitsdauer für eine Zertifizierungsstelle angegeben werden, die erneuert oder installiert wird. Keiner der Schlüssel in diesem Abschnitt ist erforderlich. Viele dieser Einstellungen verfügen über Standardwerte, die für die meisten Anforderungen ausreichend sind und in der Datei CAPolicy. inf weggelassen werden können. Alternativ können viele dieser Einstellungen geändert werden, nachdem die Zertifizierungsstelle installiert wurde.

Ein Beispiel sieht wie folgt aus:

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

**RenewalKeyLength** legt die Schlüsselgröße nur für die Erneuerung fest. Dies wird nur verwendet, wenn während der Zertifizierungsstellen-Zertifikat Erneuerung ein neues Schlüsselpaar generiert wird. Die Schlüsselgröße für das anfängliche Zertifizierungsstellen Zertifikat wird bei der Installation der Zertifizierungsstelle festgelegt.

Wenn Sie ein Zertifizierungsstellen Zertifikat mit einem neuen Schlüsselpaar erneuern, kann die Schlüssellänge entweder erweitert oder verringert werden. Wenn Sie z. b. eine Stamm-ZS-Schlüsselgröße von 4096 Bytes oder höher festgelegt haben und dann feststellen, dass Sie über Java-Apps oder Netzwerkgeräte verfügen, die nur Schlüsselgrößen von 2048 Bytes unterstützen können. Unabhängig davon, ob Sie die Größe vergrößern oder verringern, müssen Sie alle von dieser Zertifizierungsstelle ausgestellten Zertifikate neu ausstellen.

Bei erneutem erneuern des Zertifikats der Stamm Zertifizierungsstelle wird die **Gültigkeits** Dauer des neuen Zertifikats der Stamm Zertifizierungsstelle durch Erneuern von erneuert und **erneuert** . Dies gilt nur für eine Stamm Zertifizierungsstelle. Die Zertifikats Lebensdauer einer untergeordneten Zertifizierungsstelle wird durch die übergeordnete Zertifizierungsstelle festgelegt. Die folgenden Werte sind für RenewalValidityPeriod möglich: Stunden, Tage, Wochen, Monate und Jahre.

**CRLPeriod** und **CRLPeriodUnits** legen den Gültigkeits Zeitraum für die Basis-CRL fest. **CRLPeriod** kann die folgenden Werte aufweisen: Stunden, Tage, Wochen, Monate und Jahre.

**CRLDeltaPeriod** und **CRLDeltaPeriodUnits** legen den Gültigkeits Zeitraum der Delta-CRL fest. **CRLDelta period** kann die folgenden Werte aufweisen: Stunden, Tage, Wochen, Monate und Jahre.

Jede dieser Einstellungen kann nach der Installation der Zertifizierungsstelle konfiguriert werden:

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

Denken Sie daran, Active Directory Zertifikat Dienste neu zu starten, damit die Änderungen wirksam werden.

**Loaddefaulttemplates** ist nur während der Installation einer Unternehmens Zertifizierungsstelle anwendbar. Diese Einstellung, entweder true oder false (oder 1 oder 0), gibt an, ob die Zertifizierungsstelle mit einer der Standardvorlagen konfiguriert ist.

Bei einer Standardinstallation der Zertifizierungsstelle wird dem Ordner Zertifikat Vorlagen im Snap-In Zertifizierungsstelle eine Teilmenge der Standard Zertifikat Vorlagen hinzugefügt. Dies bedeutet, dass ein Benutzer oder ein Computer mit ausreichenden Berechtigungen sofort für ein Zertifikat registriert werden kann, sobald der AD CS-Dienst gestartet wird, nachdem die Rolle installiert wurde.

Möglicherweise möchten Sie nicht sofort nach der Installation einer Zertifizierungsstelle Zertifikate ausstellen. Sie können daher die Einstellung loaddefaulttemplates verwenden, um zu verhindern, dass die Standardvorlagen der Unternehmens Zertifizierungsstelle hinzugefügt werden. Wenn keine Vorlagen auf der Zertifizierungsstelle konfiguriert sind, können keine Zertifikate ausgestellt werden.

Die Zertifizierungsstelle wird von " **Alternativen** Dienstanbieter" so konfiguriert, dass das PKCS \# 1 v 2.1-Signatur Format sowohl für das Zertifizierungsstellen Zertifikat als auch für die Zertifikat Anforderungen unterstützt wird. Wenn für eine Stamm Zertifizierungsstelle der Wert 1 festgelegt wird, enthält das Zertifizierungsstellen Zertifikat das PKCS \# 1 v 2.1-Signatur Format. Wenn die untergeordnete Zertifizierungsstelle auf eine untergeordnete Zertifizierungsstelle festgelegt ist, wird eine Zertifikat Anforderung erstellt, die das PKCS \# 1 v 2.1-Signatur Format enthält.

**ForceUTF8** ändert die Standard Codierung relativer definierter Namen (rDNS) in Antragsteller-und Aussteller definierter Namen in UTF-8. Nur die RDNs, die UTF-8 unterstützen, z. b. solche, die durch eine RFC als Verzeichnis Zeichen folgen Typen definiert sind, sind betroffen. Beispielsweise unterstützt der RDN für Domänen Komponenten (DC) die Codierung entweder als IA5 oder UTF-8, während das Land RDN (C) nur die Codierung als Druck Bare Zeichenfolge unterstützt. Die ForceUTF8-Direktive wirkt sich daher auf eine DC-RDN aus, wirkt sich aber nicht auf eine C RDN aus.

**Enablekeycounting** konfiguriert die Zertifizierungsstelle so, dass ein Zähler jedes Mal erhöht wird, wenn der Signatur Schlüssel der Zertifizierungsstelle verwendet wird. Aktivieren Sie diese Einstellung nur, wenn Sie über ein Hardware Sicherheitsmodul (HSM) und den zugehörigen Kryptografiedienstanbieter (CSP) verfügen, der die Schlüssel Zählung unterstützt. Weder der starke Microsoft-CSP noch der Microsoft-Software Schlüsselspeicher-Anbieter (KSP) unterstützen die Schlüssel Zählung.

## <a name="create-the-capolicyinf-file"></a>Erstellen der Datei "capolicy. inf"

Vor der Installation von AD CS konfigurieren Sie die Datei CAPolicy. inf mit spezifischen Einstellungen für die Bereitstellung.

**Voraussetzung:** Sie müssen Mitglied der Gruppe "Administratoren" sein.

1. Öffnen Sie auf dem Computer, auf dem Sie AD CS installieren möchten, Windows PowerShell, geben Sie **Editor c:\Capolicy.inf** ein, und drücken Sie die EINGABETASTE.

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
4. Klicken Sie auf **Datei**und dann auf **Speichern**unter.

5. Navigieren Sie zum Ordner% SystemRoot%.

6. Stellen Sie Folgendes sicher:

   -   **Dateiname** ist auf **CAPolicy.inf**

   -   **Dateityp** ist auf **Alle Dateien** gesetzt.

   -   Die **Codierung** ist **ANSI**.

7. Klicken Sie auf **Speichern**.

8. Klicken Sie auf **Ja**, wenn Sie zum Überschreiben der Datei aufgefordert werden.

   ![Speichern als Speicherort für die Datei "capolicy. inf"](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

   > [!CAUTION]
   >   Vergewissern Sie sich, dass die Datei %%amp;quot;CAPolicy.inf%%amp;quot; mit der Dateierweiterung INF gespeichert wurde. Wenn Sie am Ende des Dateinamens nicht ausdrücklich **.inf** eingeben und die beschriebenen Optionen auswählen, wird die Datei als Textdatei gespeichert und nicht während der Zertifizierungsstelleninstallation verwendet.

9. Schließen Sie den Editor.

> [!IMPORTANT]
>   In der CAPolicy. inf sehen Sie, dass eine Zeile die URL angibt https://pki.corp.contoso.com/pki/cps.txt . Der Abschnitt der Datei %%amp;quot;CAPolicy.inf%%amp;quot; zu den internen Richtlinien dient lediglich als Beispiel dafür, wie Sie den Speicherort einer Zertifikatverwendungserklärung (Certificate Practice Statement, CPS) angeben können. In diesem Handbuch werden Sie nicht aufgefordert, die CPS (Certificate Practice Statement) zu erstellen.
