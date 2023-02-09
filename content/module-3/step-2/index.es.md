---
title: 'Configuración'
weight: 52
---

:::alert{header="Importante" type="warning"}
Sigue las instrucciones de esta página solo si estás ejecutando este taller en tu propia cuenta. Para saltar estas instrucciones [haz clic aquí](../step-3).
:::

- Haz clic en el enlace "Lanzar" en cualquiera de las regiones de la tabla a continuación para iniciar la implementación.
  | Región | Lanzar pila |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-3&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_3.yml) |
  | **Europe (Irlanda)** eu-west-1 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-3&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_3.yml) |
  | **Asia Pacific (Singapur)** ap-southeast-1 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-3&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_3.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-3&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_3.yml) |

- La ubicación de la plantilla de CloudFormation se rellenará automáticamente en el campo "URL de Amazon S3" como se muestra en el diagrama a continuación. Haz clic en "Siguiente".  
  ![CloudFormation specify template](/static/img/es/setup/setup-cloudformation-specify-template.png)
- En la página _Detalles de la pila_, el _Nombre de la pila_ se rellenará automáticamente con "SFW-Module-3". Puedes especificar un nombre diferente si lo deseas.  
  ![CloudFormation stack name](/static/img/es/setup/setup-cloudformation-stack-name.png)
- Haz clic en _Siguiente_ dos veces y en la última página de `Revisar`, desplázate hacia abajo. Marca la casilla `si se muestra` y luego haz clic en `Enviar`.  
  ![CloudFormation create stack](/static/img/es/setup/setup-cloudformation-create-stack.png)
- Espera hasta que la pila muestre el estado `CREATE_COMPLETE`.  
  ![CloudFormation stack complete](/static/img/es/setup/setup-cloudformation-create-complete.png)
