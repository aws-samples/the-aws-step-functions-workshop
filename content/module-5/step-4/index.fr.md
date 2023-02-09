---
title: "Localisez vos ressources et configurez votre machine à états"
weight: 74
---

### Localisez vos ressources

Accédez aux services ci-dessous dans la console AWS pour vous familiariser avec les ressources. Assurez-vous d'être dans la bonne région. Copiez l'ARN de la rubrique SNS (Amazon Resource Name) dans un bloc-notes. Vous aurez besoin de cette valeur plus tard dans le module.

- [Amazon DynamoDB](https://console.aws.amazon.com/dynamodbv2/home) - trouvez **MapStateTable**

### Afficher votre machine à état

1. Accédez à [Step Functions](https://console.aws.amazon.com/states/home) dans la console AWS.

2. Localisez la machine à états qui contient **MapStateStateMachine** dans son nom. Cliquez dessus, puis cliquez sur **Modifier** dans le coin supérieur droit.

![Modifier la machine à états](/static/img-fr/module-5/map-state-definition-edit.png)

3. Ouvrez **MapStateStateMachine** dans Workflow Studio en cliquant sur le bouton Workflow Studio sur le côté droit de l'écran.
![EDIT](/static/img/module-5/workflow-studio-button.png)

![EDIT](/static/img-fr/module-5/module5-workflowstudio.png)

4. Cliquez sur l'état `Map` "Iterate Over Input Array" et notez les détails de la configuration.
   1. **Mode de traitement : Inline** - Il s'agit du mode de traitement des entrées et des sources de données relativement plus petites. Si vous souhaitez en savoir plus sur la façon de traiter des ensembles de données plus volumineux tels que ceux venant de S3, consultez le module `Map distribuée` plus tard dans l'atelier !
   2. **Source de l'élément - Fournir un chemin d'accès au tableau d'éléments** - Ce paramètre est utilisé pour pointer l'état `Map` vers le tableau spécifique dans l'entrée JSON.
   3. **Nombre maximal de simultanéités** - Ce paramètre est utilisé pour définir le nombre d'éléments que nous voulons traiter en parallèle. La valeur par défaut est 0, ce qui signifie que nous traiterons les données de manière séquentielle, un élément à la fois. Nous explorerons ce paramètre dans le module.
   :::expand{header="Capture d'écran de la configuration de l'état `Map` (Cliquez pour agrandir)" defaultExpanded=false}
   ![Configuration de l'état Map](/static/img-fr/module-5/map-state-configuration.png)
   ::::
1. Sélectionnez l'état `Map` "Priority Filter" et affichez les `Choice Rules` que nous avons définies dans la machine à état.
   1. **Rule #1** : $.priority == "LOW". Dans chaque élément du tableau, nous vérifierons la priorité et Step Functions enverra l'élément vers l'état défini pour cette règle. Dans ce cas, les éléments de priorité "LOW" sont envoyé vers un état de success "Low Priority Order Detected", ils ne sont pas écrits dans la table DynamoDB.
   2. **Rule #2** : $.priority == "HIGH". Dans ce cas, les éléments de priorité "HIGH" sont envoyé à "Insert High Priority Order" et sont écrits dans la table DynamoDB.
   3. Lorsque vous travaillez avec des états `Choice` dans vos propres machines à état, utilisez Workshop Studio et le bouton "Ajouter une nouvelle règle de choix" pour créer rapidement la logique dont vous avez besoin pour acheminer vos données.
  ::::expand{header="Capture d'écran de configuration de l'état de choix (Cliquez pour agrandir)" defaultExpanded=false}
  ![Configuration de l'état de choix](/static/img-fr/module-5/choice-state-configuration.png)
  ::::
