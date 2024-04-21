![](Aspose.Words.3caa8bf7-2718-4cf0-99c8-0f67c5a23c9f.001.jpeg)

**UNIVERSIDAD PERUANA DE CIENCIAS APLICADAS**


TÓPICOS DE CIENCIAS DE LA COMPUTACIÓN - CC58

Tarea Académica 01




**INTEGRANTES**

Humbser Meza, Diego Fernando		u202012711

Llaguento De La Cruz, Marlon Omar		u20201b055

Quispe Palacin, Diego Eloy			u202012453


**SECCIÓN**

CC82



**DOCENTE**

Luis Martin Canaval Sanchez





**CICLO 2024-01**

**Engine Plant Scheduling**

We run a plant which produces engines. We have a package of orders for different engines. Each engine consists of components. A component may also consist of other components. For producing an engine/component, all components of which it consists should be available. Producing an engine/component consumes some resources during a certain time. Our factory is working 24/24 hours. However, it closes for the weekend (from 5:00PM on Friday to 9:00AM on Monday). An operation cannot be interrupted for the weekend break. So, the data for the problem is the following. For each order we know the ordered engine type and the due date. For each resource we know its capacity. For each engine or component we know the list of required (preceding) components, the list of required resources together with the resource consumption, and its duration (in hours).

The problem consists in scheduling operations for producing components. The objective is to minimize to maximum tardiness (maximum difference between the due date and engine production date among all orders). The data will be sent directly to groups which choose this project.

**Project aim.** Model this problem as a CSP and solve it using a solver of your choice.

**INTRODUCCIÓN**

La programación eficiente de operaciones en plantas manufactureras es crucial para cumplir con los plazos de producción, optimizar la utilización de recursos y garantizar la satisfacción del cliente. En este proyecto, proponemos un modelo de Constraint Satisfaction Problem (CSP) para abordar los desafíos de programación que enfrenta una planta de fabricación de motores. El modelo tiene como objetivo minimizar la tardanza máxima de los pedidos al programar la producción de componentes teniendo en cuenta dependencias, restricciones de recursos y operaciones no interrumpibles.

**PROBLEMA**

La planta de fabricación de motores tiene la tarea de cumplir con pedidos de varios tipos de motores dentro de fechas de vencimiento especificadas. Cada motor consta de múltiples componentes, y la producción de cada componente requiere recursos y tiempo específicos. Además, los componentes pueden depender de otros componentes, lo que significa que todos los componentes anteriores deben estar disponibles antes de que se pueda producir un componente. La planta opera las 24 horas del día, excepto los fines de semana, cuando cierra desde las 5:00 p.m. del viernes hasta las 9:00 a.m. del lunes. Las operaciones no pueden interrumpirse durante el fin de semana.

El problema se puede resumir de la siguiente manera:

- Programar la producción de componentes para cumplir con los pedidos minimizando la tardanza máxima.
- Asegurar que se satisfagan todas las dependencias entre componentes.
- Respetar las capacidades de recursos y las restricciones de tiempo para cada operación.
- Evitar interrupciones durante el descanso de fin de semana mientras se asegura que las operaciones programadas antes del fin de semana se completen.



**MOTIVACIÓN**

La programación eficiente es esencial para la competitividad y el éxito de las plantas manufactureras. Al implementar un modelo de CSP para la programación de plantas de motores, se pueden lograr varios beneficios: la utilización optimizada de recursos garantiza una asignación eficiente sin sobre reserva ni subutilización, la mejora en la entrega puntual aumenta la satisfacción del cliente al cumplir con los plazos de los pedidos, las operaciones optimizadas mediante un enfoque estructurado en la programación reducen los tiempos de entrega, y la adaptabilidad a condiciones cambiantes permite que el modelo se ajuste de manera flexible a cambios en las prioridades de los pedidos, la disponibilidad de recursos y las restricciones de producción, contribuyendo en última instancia a mejorar la productividad y la rentabilidad.

**TÉCNICA PROPUESTA**

Se usará la programación restrictiva debido a su alta flexibilidad a la hora de encontrar soluciones en la planificación de horarios. Además, las condiciones establecerán para alcanzar el objetivo indicado.


**OBJETIVOS** 

- Minimizar al máximo la tardanza (máxima diferencia entre la fecha de vencimiento y la fecha de producción del motor entre todos los pedidos).


**MARCO TEÓRICO**

En la programación con restricciones se plantean problemas de tal manera que se satisfacen ciertas condiciones o restricciones para su resolución. Este enfoque se centra en describir las restricciones o reglas que debe satisfacer cualquier decisión válida, no en cómo llegar a esa solución (Rossi, et al., 2006). También, “el objetivo puede ser reducir un conjunto muy grande de soluciones posibles a un subconjunto más manejable agregando restricciones al problema (Google OR-Tools, 2024)”.

Este paradigma de la computación tiene los siguientes componentes principales:

1. **Variables:** Elementos que necesitan ser determinados.
1. **Dominios:** Conjunto de valores posibles que cada variable puede tomar.
1. **Restricciones:** Condiciones que deben cumplirse para que una asignación de valores a las variables sea considerada válida.

Su aplicación abarca distintos ámbitos donde el conjunto de soluciones para un problema es muy grande, por ejemplo, para los juegos o puzzles como Sudoku, también en la planificación de horarios de trabajo, configuración de sistemas, etc. 

Las ventajas que nos ofrece la CP (constraint programming) son su flexibilidad para modelar problemas complejos pero uno de sus problemas es a la hora de querer usar restricciones con un alto nivel de complejidad. Esto hace que la resolución del problema no llegue a darse o se tarde mucho en poder encontrarla.





**PLANTEAMIENTO**

**Variable y Dominio:**

Según el problema, la variable será cada motor/componente, de la siguiente manera Componente (0 - 104). En donde el dominio de la variable puede llegar a tomar las horas entre 0 a 104 horas. Siendo 0 el inicio de la apertura de la fábrica de motores (Lunes 9 am) y las 104 el cierre de esta (Viernes 17 pm). Es decir, el dominio será la hora de producción de cada motor/componente.

**Restricciones**

- La producción de un motor/componente deriva de la producción de otros componentes. Por lo que no puede ser terminado hasta que posea todos sus componentes listos. Esto se debe a su precedencia de componentes.
- Cada motor/componente posee un total de horas de producción que necesitará usar los recursos.
- Los recursos son limitados. Se podría sugerir un ejemplo de datos como el siguiente: {r1: 10, r2:8, r3:10, r4:6}. Siendo estos recursos, en nuestro caso, máquinas y su capacidad.
- La fecha de producción de un motor/componente no puede superar la fecha de vencimiento.

**Función Objetivo**

La función objetivo es minimizar al máximo el retraso entre la fecha de entrega y la fecha de producción del motor para todos los pedidos. En otras palabras, queremos minimizar la diferencia máxima entre la fecha de entrega esperada de cada motor y la fecha en que realmente se produjo ese motor.

La función objetivo se define de la siguiente manera:

1. Definimos una variable para cada motor que represente su fecha de entrega esperada.
1. Definimos una variable para cada motor que represente su fecha de producción real.
1. La diferencia entre la fecha de entrega esperada y la fecha de producción real de cada motor representa el retraso para ese motor.
1. Nuestra función objetivo consiste en minimizar la diferencia máxima entre la fecha de entrega y la fecha de producción de todos los motores.


**Referencias bibliográficas**
Francesca Rossi, Peter van Beek, and Toby Walsh. 2006. Handbook of Constraint Programming. Elsevier Science Inc., USA.

Google for developers(2024, 13 de marzo) Constraint Optimization. Google OR-Tools. Recuperado el 19 de abril del 2024, de [https://developers.google.com/optimization/cp](https://developers.google.com/optimization/cp)



