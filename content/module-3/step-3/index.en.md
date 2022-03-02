---
title: 'Modify definition'
weight: 53
---

Now we'll modify the ASL definition to implement sync polling. Click the Edit button and navigate to the Definition editor. Add the `.sync` method to the end of the Resource definition.

![Module 3 Workflow](/static/img/module-3/module3-sync.png)

Save your state machine.

To see a list of what integrated services support waiting for sync polling (`.sync`), see [Optimized integrations for Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html).
