---
title: 'Configuración'
weight: 111
---

:::alert{header="Importante" type="warning"}
Siga las instrucciones de esta página solo si está ejecutando este taller en su propia cuenta. Para saltar estas instrucciones [haga clic aquí](../step-3).
:::

- Haga clic en el enlace "Lanzar" contra cualquiera de las regiones de la tabla a continuación para iniciar la implementación.
  | Región | Desplegar pila |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Desplegar](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-9&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_9.yml) |
  | **Europe (Irlanda)** eu-west-1 | [Desplegar](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-9&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_9.yml) |
  | **Asia Pacific (Singapur)** ap-southeast-1 | [Desplegar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-9&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_9.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Desplegar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-9&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_9.yml) |

- La ubicación de la plantilla de CloudFormation se rellenará automáticamente en el campo "URL de Amazon S3" como se muestra en el diagrama a continuación. Haga clic en "Siguiente"
  ![CloudFormation specify template](/static/img/setup/setup-cloudformation-specify-template.png)
- En la página _Detalles de la pila_, el _Nombre de la pila_ se rellenará automáticamente con "SFW-Module-9". Puede especificar un nombre diferente si lo desea.
  ![CloudFormation stack name](/static/img/setup/setup-cloudformation-stack-name.png)
- Haga clic en _Siguiente_ dos veces y en la última página de `Revisar`, desplácese hacia abajo. Marque la casilla `si se muestra` y luego haga clic en `Enviar`.
  ![CloudFormation create stack](/static/img/setup/setup-cloudformation-create-stack.png)
- Espere hasta que la pila muestre el estado `CREATE_COMPLETE`.
  ![CloudFormation stack complete](/static/img/setup/setup-cloudformation-create-complete.png)
