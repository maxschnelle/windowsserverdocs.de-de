---
title: Public Key Authentication für Geräte in einer Domäne
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
author: justinha
ms.author: Justinha
ms.date: 08/18/2017
ms.openlocfilehash: d9603cde90ca4a689d6d5993c8e131ba5a2e7d40
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077597"
---
# <a name="domain-joined-device-public-key-authentication"></a>Public Key Authentication für Geräte in einer Domäne

>Gilt für: Windows Server 2016, Windows 10

Kerberos hat die Unterstützung von in die Domäne eingebundenen Geräten zum Anmelden mit einem Zertifikat ab Windows Server 2012 und Windows 8 hinzugefügt. Diese Änderung ermöglicht Drittanbietern das Erstellen von Lösungen zum Bereitstellen und Initialisieren von Zertifikaten für in die Domäne eingebundenen Geräten, die für die Domänen Authentifizierung verwendet werden sollen.

## <a name="automatic-public-key-provisioning"></a>Automatische Bereitstellung öffentlicher Schlüssel

Ab Windows 10, Version 1507 und Windows Server 2016, stellen in die Domäne eingebundene Geräte automatisch einen gebundenen öffentlichen Schlüssel für einen Windows Server 2016-Domänen Controller (DC) bereit. Nachdem ein Schlüssel bereitgestellt wurde, kann Windows die Authentifizierung mit öffentlichem Schlüssel für die Domäne verwenden.

### <a name="key-generation"></a>Schlüsselgenerierung
Wenn auf dem Gerät Credential Guard ausgeführt wird, wird ein öffentliches/privates Schlüsselpaar erstellt, das durch Credential Guard geschützt wird.

Wenn Credential Guard nicht verfügbar ist und ein TPM ist, wird ein öffentliches/privates Schlüsselpaar durch das TPM geschützt.

Wenn keines von beiden verfügbar ist, wird kein Schlüsselpaar generiert, und das Gerät kann sich nur mit einem Kennwort authentifizieren.

### <a name="provisioning-computer-account-public-key"></a>Öffentlicher Schlüssel für das Bereitstellen des Computer Kontos
Wenn Windows gestartet wird, wird überprüft, ob ein öffentlicher Schlüssel für sein Computer Konto bereitgestellt wurde. Wenn dies nicht der Fall ist, wird ein gebundener öffentlicher Schlüssel generiert und mit einem DC mit Windows Server 2016 oder höher für sein Konto konfiguriert. Wenn alle Domänen Controller auf eine Unterebene festgelegt sind, wird kein Schlüssel bereitgestellt.

### <a name="configuring-device-to-only-use-public-key"></a>Konfigurieren des Geräts für die Verwendung des öffentlichen Schlüssels
Wenn das Gruppenrichtlinie festlegen der **Unterstützung für die Geräte Authentifizierung mithilfe des Zertifikats** auf **Force**festgelegt ist, muss das Gerät einen Domänen Controller finden, auf dem Windows Server 2016 oder höher ausgeführt wird, um sich zu authentifizieren. Die Einstellung befindet sich unter Administrative Vorlagen > System > Kerberos.

### <a name="configuring-device-to-only-use-password"></a>Konfigurieren des Geräts für die Verwendung von Kennwort
Wenn die Unterstützung der Gruppenrichtlinie Einstellung **für die Geräte Authentifizierung mithilfe des Zertifikats** deaktiviert ist, wird immer das Kennwort verwendet. Die Einstellung befindet sich unter Administrative Vorlagen > System > Kerberos.

## <a name="domain-joined-device-authentication-using-public-key"></a>In die Domäne eingebundener Geräte Authentifizierung mit öffentlichem Schlüssel
Wenn Windows über ein Zertifikat für das in die Domäne eingebundenen Gerät verfügt, wird Kerberos zuerst mithilfe des Zertifikats und bei Wiederholungs versuchen mit Kennwort authentifiziert. Dadurch kann sich das Gerät gegenüber DCS authentifizieren.

Da die automatisch bereitgestellten öffentlichen Schlüssel über ein selbst signiertes Zertifikat verfügen, schlägt die Zertifikat Überprüfung auf Domänen Controllern fehl, die die Zuordnung von Schlüssel Vertrauens Konten nicht unterstützen. Standardmäßig wird von Windows die Authentifizierung mit dem Domänen Kennwort des Geräts erneut versucht.


