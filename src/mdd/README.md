# MdD

> [Glosario](glosario.md)

## Diagramas 

### Iteración "cero"

||||
|:-:|:-:|:-:|
|![](/images/modelosUML/src/mdd/000-DdC-000.svg)|![](/images/modelosUML/src/mdd/000-DdC-001.svg)|![](/images/modelosUML/src/mdd/000-DdC-002.svg)|

### Primera iteración

<div align=center>

|![](/images/modelosUML/src/mdd/001-DdC.svg)|![](/images/modelosUML/src/mdd/001-DdO.svg)|
|:-:|:-:|
|DdC|DdO|

</div>

---

<div align=center>

|![](/images/modelosUML/src/mdd/001-DdE-Ascensor.svg)|![](/images/modelosUML/src/mdd/001-DdE-Persona.svg)|
|:-:|:-:|
|Ascensor|Persona|

</div>

---

<div align=center>

|||
|-|:-:|
||![](/images/modelosUML/src/mdd/001-DdCol-001-PersonaEdificio.svg)
||![](/images/modelosUML/src/mdd/001-DdCol-002-PersonaAscensor.svg)
||![](/images/modelosUML/src/mdd/001-DdCol-003-EdificioAscensor.svg)|

</div>

---

<div align=center>

|![](/images/modelosUML/src/mdd/001-DdS-UsoDeAscensor.svg)|
|-|

</div>

### Segunda iteración

<div align=center>

|![](/images/modelosUML/src/mdd/002-DdC.svg)|
|:-:|
|DdC|

---

|![](/images/modelosUML/src/mdd/002-DdO.svg)|![](/images/modelosUML/src/mdd/002-DdO-002.svg)|
|:-:|:-:|
|DdO|DdO II|

</div>

### Tercera iteración

<div align=center>

|![](/images/modelosUML/src/mdd/003-DdC.svg)|![](/images/modelosUML/src/mdd/003-DdO.svg)|
|:-:|:-:|
|DdC|DdO|

</div>

### Cuarta iteración

Intención de uso de ascensor

<div align=center>

|![](/images/modelosUML/src/mdd/004-DdC.svg)|![](/images/modelosUML/src/mdd/004-DdO.svg)|
|:-:|:-:|
|DdC|DdO|

</div>

### Quinta iteración


<div align=center>

|![](/images/modelosUML/src/mdd/005-CdU.svg)|
|:-:|
|CdU|

</div>

#### Considerandos

- **Manejo de errores**
  - No consideraremos ascensores que se descomponen u otros tipos de errores del sistema.
  - El sistema funcionará en condiciones ideales.
- **Concurrencia**
  - No implementaremos concurrencia en el sentido estricto de programación paralela o multihilo.
  - En su lugar, el sistema funcionará con un modelo de simulación por pasos, donde cada paso representa un minuto.
- **Modelo de simulación**
  - El sistema itera minuto a minuto.
  - En cada iteración (minuto), se actualiza el estado de todas las entidades.

Para reflejar este enfoque en nuestro diseño, podríamos considerar añadir una clase o componente de Simulación que se encargue de manejar estas iteraciones por minuto. Esta clase podría tener un método como "avanzarMinuto()" que se encargaría de actualizar el estado de todas las entidades en el sistema.

¿Sería una clase nueva o podríamos dejarlo dentro de "Universidad"? 

||Universidad|Clase Nueva|
|-|-|-|
|***Pros***|**Simplicidad**: Evita añadir una nueva clase al diseño, manteniendo el modelo más simple.|**Responsabilidad única**: Cumple mejor con el principio de responsabilidad única.
||**Centralización**: Universidad ya es la clase de nivel más alto en nuestra jerarquía, por lo que tiene sentido que controle la simulación.|**Flexibilidad**: Permite modificar o reemplazar la lógica de simulación sin afectar a la clase Universidad.
||**Acceso directo**: Universidad ya tiene acceso a todos los elementos necesarios para la simulación (edificios, ascensores, personas).|**Reutilización**: La lógica de simulación podría reutilizarse más fácilmente en otros contextos o proyectos.
||**Coherencia conceptual**: La Universidad es el "mundo" de nuestro sistema, por lo que podría ser natural que maneje el paso del tiempo.|**Claridad**: Hace que el propósito y la funcionalidad de la simulación sean más explícitos en el diseño.
|***Contras***|**Responsabilidad única**: Podría violar el principio de responsabilidad única, ya que Universidad tendría dos responsabilidades distintas: representar la universidad y manejar la simulación.|**Complejidad adicional**: Añade una nueva clase al diseño, lo que podría complicar ligeramente el modelo.
||**Acoplamiento**: Podría crear un acoplamiento fuerte entre la lógica de simulación y la representación de la universidad.|**Necesidad de coordinación**: Requiere establecer una relación clara entre Simulación y Universidad.
||**Flexibilidad limitada**: Si en el futuro queremos cambiar el mecanismo de simulación, tendríamos que modificar la clase Universidad.|
||**Reutilización**: Si quisiéramos usar la lógica de simulación en otro contexto, sería más difícil extraerla.|
