---
title: Fehler-und Ereignismeldungen der QoS-Richtlinie
description: Dieses Thema enthält eine Liste der Fehler-und Ereignismeldungen für Quality of Service (QoS)-Richtlinie in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d0eb137716795c324afcf1a708fff00c2f7266d6
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315566"
---
# <a name="qos-policy-error-and-event-messages"></a>Fehler-und Ereignismeldungen der QoS-Richtlinie

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Im folgenden finden Sie die Fehler-und Ereignismeldungen, die der QoS-Richtlinie zugeordnet sind.  
  
## <a name="informational-messages"></a>Informationsnachrichten  

Im folgenden finden Sie eine Liste von Informationsmeldungen zur QoS-Richtlinie.

|||  
|-|-|  
|**MessageId**|16500|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Computer-QoS-Richtlinien wurden erfolgreich aktualisiert. Es wurden keine Änderungen erkannt.|  
  
|||  
|-|-|  
|**MessageId**|16501|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Computer-QoS-Richtlinien wurden erfolgreich aktualisiert. Richtlinien Änderungen wurden erkannt.|  
  
|||  
|-|-|  
|**MessageId**|16502|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**Sprache**|Deutsch|  
|**Nachricht**|Benutzer-QoS-Richtlinien wurden erfolgreich aktualisiert. Es wurden keine Änderungen erkannt.|  
  
|||  
|-|-|  
|**MessageId**|16503|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**Sprache**|Deutsch|  
|**Nachricht**|Benutzer-QoS-Richtlinien wurden erfolgreich aktualisiert. Richtlinien Änderungen wurden erkannt.|  
  
|||  
|-|-|  
|**MessageId**|16504|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Einstellungs Wert wird nicht durch eine QoS-Richtlinie angegeben. Der Standardwert des lokalen Computers wird angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16505|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 0 (minimaler Durchsatz).|  
  
|||  
|-|-|  
|**MessageId**|16506|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 1.|  
  
|||  
|-|-|  
|**MessageId**|16507|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 2.|  
  
|||  
|-|-|  
|**MessageId**|16508|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 3 (maximaler Durchsatz).|  
  
|||  
|-|-|  
|**MessageId**|16509|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die DSCP-Markierung wurde erfolgreich aktualisiert. Der Einstellungs Wert ist nicht angegeben. Anwendungen können DSCP-Werte unabhängig von QoS-Richtlinien festlegen.|  
  
|||  
|-|-|  
|**MessageId**|16510|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die DSCP-Markierung wurde erfolgreich aktualisiert. Anwendungs-DSCP-Markierungs Anforderungen werden ignoriert. Nur QoS-Richtlinien können DSCP-Werte festlegen.|  
  
|||  
|-|-|  
|**MessageId**|16511|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für die DSCP-Markierung wurde erfolgreich aktualisiert. Anwendungen können DSCP-Werte unabhängig von QoS-Richtlinien festlegen.|  
  
|||  
|-|-|  
|**MessageId**|16512|  
|**Zunehmen**|Informationswarnungen|  
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die selektive Anwendung von QoS-Richtlinien, die auf der Domänen Netzwerk Kategorie basieren, wurde deaktiviert. QoS-Richtlinien werden auf alle Netzwerkschnittstellen angewendet.|  
  
## <a name="warning-messages"></a>Warnmeldungen

Im folgenden finden Sie eine Liste der Warnmeldungen der QoS-Richtlinie.

|||  
|-|-|  
|**MessageId**|16600|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|  
|**Sprache**|Deutsch|  
|**Nachricht**|EQoS: * * * Testen\*\*\*[, mit einer Zeichenfolge] "%2".|  
  
|||  
|-|-|  
|**MessageId**|16601|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|  
|**Sprache**|Deutsch|  
|**Nachricht**|EQoS: * * * Testen von\*\*\*[, mit zwei Zeichen folgen, Zeichenfolge1 ist] "%2" [, Zeichenfolge2 ist] "%3".|  
  
|||  
|-|-|  
|**MessageId**|16602|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Computer-QoS-Richtlinie "%2" weist eine ungültige Versionsnummer auf. Diese Richtlinie wird nicht angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16603|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Benutzer-QoS-Richtlinie "%2" weist eine ungültige Versionsnummer auf. Diese Richtlinie wird nicht angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16604|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**Sprache**|Deutsch|  
|**Nachricht**|In der Computer-QoS-Richtlinie "%2" ist kein DSCP-Wert oder eine Drosselungs Rate angegeben. Diese Richtlinie wird nicht angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16605|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**Sprache**|Deutsch|  
|**Nachricht**|In der Benutzer-QoS-Richtlinie "%2" ist kein DSCP-Wert oder eine Drosselungs Rate angegeben. Diese Richtlinie wird nicht angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16606|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die maximale Anzahl von QoS-Richtlinien für Computer wurde überschritten. Die QoS-Richtlinie "%2" und die nachfolgenden Computer-QoS-Richtlinien werden nicht angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16607|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die maximale Anzahl von Benutzer-QoS-Richtlinien wurde überschritten. Die QoS-Richtlinie "%2" und die nachfolgenden Benutzer-QoS-Richtlinien werden nicht angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16608|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Computer-QoS-Richtlinie "%2" steht potenziell in Konflikt mit anderen QoS-Richtlinien. Regeln zur Anwendung der Richtlinie finden Sie in der Dokumentation.|  
  
|||  
|-|-|  
|**MessageId**|16609|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Benutzer-QoS-Richtlinie "%2" steht potenziell in Konflikt mit anderen QoS-Richtlinien. Regeln zur Anwendung der Richtlinie finden Sie in der Dokumentation.|  
  
|||  
|-|-|  
|**MessageId**|16610|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Computer-QoS-Richtlinie "%2" wurde ignoriert, da der Anwendungspfad nicht verarbeitet werden kann. Der Anwendungspfad ist möglicherweise ungültig, enthält einen ungültigen Laufwerk Buchstaben oder enthält ein zugeordnetes Netzwerklaufwerk.|  
  
|||  
|-|-|  
|**MessageId**|16611|  
|**Zunehmen**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**Sprache**|Deutsch|  
|**Nachricht**|Die Benutzer-QoS-Richtlinie "%2" wurde ignoriert, da der Anwendungspfad nicht verarbeitet werden kann. Der Anwendungspfad ist möglicherweise ungültig, enthält einen ungültigen Laufwerk Buchstaben oder enthält ein zugeordnetes Netzwerklaufwerk.|  
  
## <a name="error-messages"></a>Fehlermeldungen  

Im folgenden finden Sie eine Liste der QoS-Richtlinien-Fehlermeldungen.

|||  
|-|-|  
|**MessageId**|16700|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**Sprache**|Deutsch|  
|**Nachricht**|Fehler beim Aktualisieren der QoS-Richtlinien des Computers. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16701|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**Sprache**|Deutsch|  
|**Nachricht**|Fehler beim Aktualisieren der Benutzer-QoS-Richtlinien. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16702|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte den Stamm Schlüssel auf Computer Ebene für QoS-Richtlinien nicht öffnen. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16703|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte den Stamm Schlüssel auf Benutzerebene für QoS-Richtlinien nicht öffnen. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16704|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**Sprache**|Deutsch|  
|**Nachricht**|Eine Computer-QoS-Richtlinie überschreitet die maximal zulässige namens Länge. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Computer Ebene mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16705|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**Sprache**|Deutsch|  
|**Nachricht**|Eine Benutzer-QoS-Richtlinie überschreitet die maximal zulässige namens Länge. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Benutzerebene mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16706|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**Sprache**|Deutsch|  
|**Nachricht**|Eine Computer-QoS-Richtlinie hat einen Namen mit der Länge Null. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Computer Ebene mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16707|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**Sprache**|Deutsch|  
|**Nachricht**|Eine Benutzer-QoS-Richtlinie hat einen Namen mit der Länge Null. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Benutzerebene mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16708|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte den Registrierungs Unterschlüssel für eine Computer-QoS-Richtlinie nicht öffnen. Die Richtlinie wird unter dem Schlüssel der QoS-Richtlinie auf Computer Ebene mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16709|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte den Registrierungs Unterschlüssel für eine Benutzer-QoS-Richtlinie nicht öffnen. Die Richtlinie wird unter dem Schlüssel der QoS-Richtlinie auf Benutzerebene mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16710|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte das Feld "%2" für die Computer-QoS-Richtlinie "%3" nicht lesen oder überprüfen.|  
  
|||  
|-|-|  
|**MessageId**|16711|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte das Feld "%2" für die Benutzer-QoS-Richtlinie "%3" nicht lesen oder überprüfen.|  
  
|||  
|-|-|  
|**MessageId**|16712|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte die eingehende TCP-Durchsatz Ebene nicht lesen oder festlegen. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16713|  
|**Zunehmen**|Error|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**Sprache**|Deutsch|  
|**Nachricht**|QoS konnte die Außerkraftsetzungs Einstellung der DSCP-Markierung nicht lesen oder festlegen. Fehlercode: "%2".|  

Das nächste Thema dieses Handbuchs finden Sie unter [häufig gestellte Fragen zur QoS-Richtlinie](qos-policy-faq.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
