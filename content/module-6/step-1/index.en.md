---
title: 'Overview of the concept'
weight: 81
---

A Step Functions execution receives JSON text as input and passes that input to the first state in the workflow. Individual states receive JSON as input and usually pass JSON as output to the next state. Understanding how this information flows from state to state, and learning how to filter and manipulate this data, is key to effectively designing and implementing workflows in AWS Step Functions.

In the Amazon States Language, these fields filter and control the flow of JSON from state to state:

`InputPath`

`OutputPath`

`ResultPath`

`Parameters`

`ResultSelector`
