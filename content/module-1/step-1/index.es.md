---
title: 'Configuración'
weight: 31
---

:::alert{header="Importante" type="warning"}
Sigue las instrucciones de esta página solamente si estás ejecutando el laboratorio en tu propia cuenta de AWS. Para saltarte estas instrucciones [haz click aquí](../step-2).
:::

- Haz clic en el enlace "Lanzar" en cualquiera de las regiones de la tabla a continuación para iniciar la implementación.
  | Región | Lanzar pila |
  | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
  | **US East (N. Virginia)** us-east-1 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |
  | **Europe (Ireland)** eu-west-1 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |
  | **Asia Pacific (Singapore)** ap-southeast-1 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |
  | **Asia Pacific (Sydney)** ap-southeast-2 | [Lanzar](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/template?stackName=SFW-Module-1&templateURL=https://serverless-stepfunctions-artifacts-17oiei2i27urc.s3.amazonaws.com/resources/module_1.yml) |

- La localización de la plantilla de CloudFormation se auto-completará en el campo `Amazon S3 URL` como muestra la siguiente imagen. Haz click en `Siguiente`.  
  ![CloudFormation specify template](/static/img/es/setup/setup-cloudformation-specify-template.png)
- En la sección _Especificar los detalles de la pila_, _Nomber de la pila_ debería autocompletarse con `SFW-Module-1`. Puedes especificar otro nombre si te parece apropiado.  
  ![CloudFormation stack name](/static/img/es/setup/setup-cloudformation-stack-name.png)
- Haz clic en _Siguiente_ dos veces y en la pagína de `Revisar`, ve al final. Marca las casillas de verificación `si aparecen` y luego haz click en `Enviar`.  
  ![CloudFormation create stack](/static/img/es/setup/setup-cloudformation-create-stack.png)
- Espera hasta que la pila muestre el estado `CREATE_COMPLETE`.  
  ![CloudFormation stack complete](/static/img/es/setup/setup-cloudformation-create-complete.png)
