---
title: "Domäne eingebundenen Geräteauthentifizierung des öffentlichen Schlüssels"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 8/18/2017
ms.openlocfilehash: 65f39f4900fcd99ef90b160d3db7099edb73bc1c
ms.sourcegitcommit: e94838df702ff0135ebe7c179b228aa67b772d35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
# <a name="domain-joined-device-public-key-authentication"></a>Domäne eingebundenen Geräteauthentifizierung des öffentlichen Schlüssels

>Gilt für: Windows Server2016, Windows10

Kerberos zusätzliche Unterstützung für Geräte in einer Domäne anmelden mit Windows Server2012 und Windows8 ein Zertifikat ab. Diese Änderung kann 3. Anbietern zum Erstellen von Lösungen zum Bereitstellen und Initialisieren von Zertifikaten für die Domäne eingebundene Geräte für die Domänenauthentifizierung verwenden. 

## <a name="automatic-public-key-provisioning"></a>Automatische public Key-Bereitstellung

Ab Windows10, Version 1507 und Windows Server2016, Bereitstellen Geräte in einer Domäne automatisch einen gebundenen öffentlichen Schlüssel zu einem Windows Server2016-Domänencontroller (DC). Wenn ein Schlüssel bereitgestellt wird, und klicken Sie dann Windows Authentifizierung mit öffentlichen Schlüsseln zur Domäne verwendet werden kann.

### <a name="public-key-generation"></a>Erstellung von öffentlichen Schlüsseln
Wenn das Gerät Credential Guard ausgeführt wird, wird ein öffentlicher Schlüssel durch Credential Guard geschützt erstellt. 

Wenn Credential Guard nicht verfügbar ist, und ein TPM ist, wird ein öffentlicher Schlüssel durch das TPM erstellt. 

Wenn keiner verfügbar ist, ein Schlüssel wird nicht generiert, und das Gerät kann nur authentifizieren Kennwort verwenden.

### <a name="provisioning-computer-account-public-key"></a>Computer-Konto public Key-Bereitstellung
Wenn Windows gestartet wird, überprüft, ob ein öffentlicher Schlüssel für das Konto "Computer" bereitgestellt wird. Wenn dies nicht der Fall, anschließend einen gebundenen öffentlichen Schlüssel generiert und in AD mit einem Windows Server2016 oder höher Domänencontroller für sein Konto konfiguriert. Wenn alle Domänencontroller kompatible sind, wird kein Schlüssel bereitgestellt.

### <a name="configuring-device-to-only-use-public-key"></a>Konfigurieren des Geräts nur öffentlichen Schlüssel verwenden
Wenn die Gruppenrichtlinieneinstellung **Unterstützung für Geräte mit Zertifikat** festgelegt ist **Force**, und klicken Sie dann das Gerät muss auf einen Domänencontroller zu suchen, die Windows Server2016 ausgeführt wird oder höher zum Authentifizieren. Die Einstellung befindet sich unter Administrative Vorlagen > System > Kerberos.

### <a name="configuring-device-to-only-use-password"></a>Konfigurieren von Gerät nur Kennwort verwenden
Wenn die Gruppenrichtlinieneinstellung **Unterstützung für Geräte mit Zertifikat** deaktiviert ist, und klicken Sie dann Kennwort immer verwendet wird. Die Einstellung befindet sich unter Administrative Vorlagen > System > Kerberos.

## <a name="domain-joined-device-authentication-using-public-key"></a>Domäne Geräteauthentifizierung mit öffentlichen Schlüssel
Wenn Windows ein Zertifikat für die Domäne eingebundenen Gerät ist, mithilfe des Zertifikats zuerst Kerberos authentifiziert und auf Fehler bei der Wiederholungen mit Kennwort. Dadurch wird das Gerät für die Authentifizierung bei älteren DCs.

Da die automatisch bereitgestellten öffentlichen Schlüssel ein selbst signiertes Zertifikat aufweisen, bei der Validierung von Zertifikat auf Domänencontrollern, auf denen Schlüssel vertrauen Kontenzuordnung nicht unterstützen. Standardmäßig versucht Windows Authentifizierung unter Verwendung des Geräts Domänenkennwort ein.


