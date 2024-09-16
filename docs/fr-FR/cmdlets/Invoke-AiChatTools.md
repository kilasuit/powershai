﻿---
external help file: powershai-help.xml
schema: 2.0.0
powershai: true
---

# Invoke-AiChatTools

## SYNOPSIS <!--!= @#Synop !-->
Envoie un message à un LLM, avec la prise en charge des appels d'outils, et exécutez les outils demandés par le modèle en tant que commandes Powershell.

## DESCRIPTION <!--!= @#Desc !-->
Il s'agit d'une fonction auxiliaire pour faciliter le traitement des outils avec Powershell.
Elle gère le traitement des "Outils", en les exécutant lorsque le modèle le demande !

Vous devez transmettre les outils dans un format spécifique, documenté dans le sujet about_Powershai_Chats.
Ce format mappe correctement les fonctions et les commandes Powershell vers le schéma acceptable par OpenAI (OpenAPI Schema).

Cette commande encapsule toute la logique qui identifie quand le modèle veut invoquer la fonction, l'exécution de ces fonctions et l'envoi de cette réponse au modèle.
Elle reste dans cette boucle jusqu'à ce que le modèle cesse de décider d'invoquer plus de fonctions, ou que la limite d'interactions (oui, ici on appelle ça des interactions, et non des itérations) avec le modèle soit terminée.

Le concept d'interaction est simple : chaque fois que la fonction envoie un prompt au modèle, cela compte comme une interaction.
Voici un flux typique qui peut se produire :

Vous pouvez obtenir plus de détails sur le fonctionnement en consultant le sujet about_Powershai_Chats.

## SYNTAX <!--!= @#Syntax !-->

```
Invoke-AiChatTools [[-prompt] <Object>] [[-Tools] <Object>] [[-PrevContext] <Object>] [[-MaxTokens] <Object>] [[-MaxInteractions] <Object>] [[-MaxSeqErrors] <Object>] 
[[-temperature] <Object>] [[-model] <Object>] [[-on] <Object>] [-Json] [[-RawParams] <Object>] [-Stream] [<CommonParameters>]
```

## PARAMETERS <!--!= @#Params !-->

### -prompt

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 1
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -Tools
Tableau d'outils, comme expliqué dans la doc de cette commande.
Utilisez le résultat de Get-OpenaiTool* pour générer les valeurs possibles.
Vous pouvez transmettre un tableau d'objets de type OpenaiTool.
Si une même fonction est définie dans plusieurs outils, la première trouvée dans l'ordre défini sera utilisée !

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 2
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -PrevContext

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 3
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -MaxTokens
Sortie max !

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 4
Default Value: 500
Accept pipeline input: false
Accept wildcard characters: false
```

### -MaxInteractions
Au total, autoriser au maximum 5 itérations !

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 5
Default Value: 10
Accept pipeline input: false
Accept wildcard characters: false
```

### -MaxSeqErrors
Quantité maximale d'erreurs consécutives que votre fonction peut générer avant qu'elle ne se termine.

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 6
Default Value: 2
Accept pipeline input: false
Accept wildcard characters: false
```

### -temperature

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 7
Default Value: 0.6
Accept pipeline input: false
Accept wildcard characters: false
```

### -model

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 8
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -on
Gestionnaire d'événements.
Chaque clé est un événement qui sera déclenché à un moment donné par cette commande !
événements :
answer : déclenché après avoir obtenu la réponse du modèle (ou lorsqu'une réponse devient disponible en utilisant le flux).
func : déclenché avant de commencer l'exécution d'un outil demandé par le modèle.
	exec : déclenché après que le modèle ait exécuté la fonction.
	error : déclenché lorsque la fonction exécutée génère une erreur.
	stream : déclenché lorsqu'une réponse a été envoyée (par le flux) et -DifferentStreamEvent
	beforeAnswer : Déclenché après toutes les réponses. Utile lorsqu'il est utilisé en flux !
	afterAnswer : Déclenché avant de commencer les réponses. Utile lorsqu'il est utilisé en flux !

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 9
Default Value: @{}
Accept pipeline input: false
Accept wildcard characters: false
```

### -Json
Envoie response_format = "json", forçant le modèle à renvoyer un json.

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```

### -RawParams
Ajouter des paramètres personnalisés directement dans l'appel (remplacera les paramètres définis automatiquement).

```yml
Parameter Set: (All)
Type: Object
Aliases: 
Accepted Values: 
Required: false
Position: 10
Default Value: 
Accept pipeline input: false
Accept wildcard characters: false
```

### -Stream

```yml
Parameter Set: (All)
Type: SwitchParameter
Aliases: 
Accepted Values: 
Required: false
Position: named
Default Value: False
Accept pipeline input: false
Accept wildcard characters: false
```



<!--PowershaiAiDocBlockStart-->
_Traduit automatiquement à l'aide de PowershAI et IA. 
_
<!--PowershaiAiDocBlockEnd-->