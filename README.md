# 🏛️ Proyecto Final Semillero: Mesa de ayuda IA con agentes especializados para el área Legal

**Agentes con LangChain + Gemini**

## 👥 Integrantes del Grupo
* **JUAN JOSE NAVAS VILLAGRAN** — CI: 1723656995 — Correo: jjnavas@netlife.net.ec
* **BERNY JOAO CAMPUZANO SIGCHO** — CI: 1720967510 — Correo: bcampuzano@netlife.net.ec
* **MARIO DAVID CARRERA CASA** — CI: 1718756065 — Correo: mdcarrera@netlife.net.ec

---

## 🎥 Link del Video del Proyecto
👉 [Ver video explicativo y demostrativo en YouTube](https://youtu.be/OKj27hbeaIA?si=nif9MgO4RzYuxrCe)

---

## ⚙️ Instrucciones de Ejecución Paso a Paso

### Paso A: Carga de librerías oficiales
Lo primero será cargar los stacks oficiales tanto de LangChain, LLM, embeddings y la base vectorial. Para ello, ejecuta el código ubicado debajo de:
* `[0. Instalación de librerías]` 
> *Si todo está bien, aparecerá el mensaje: `Instalacion completa.`*

### Paso B: Configuración del modelo y credenciales
Se debe llamar al modelo LLM (`gemini-3.1-flash-lite`) y al embedding (`gemini-embedding-2-preview`). Para ello se solicitará una API Key:
1. Ingresar a: [Google AI Studio API Keys](https://aistudio.google.com/api-keys)
2. Crear una cuenta gratuita (para pruebas).
3. Hacer clic en **"Crear clave de API"**.
4. Copiar la clave generada.
5. Ir a la sección `[1. Conexión a Google Gemini]`.
6. Colocar la clave en el código sustituyendo donde dice: `(colocar aquí TU: API_KEY)`.
7. Ejecuta el programa para verificar la conexión. *Si todo está bien, aparecerá: `Gemini conectado`*.

---

## 🤖 Ejercitación y Estructura del Programa

### Paso C: Creación de las Bases de Conocimiento (Documentación Legal)
Ejecuta la celda de programación ubicada debajo de `(2. Las bases de conocimiento: Documentación del Departamento Legal)`. 
En este paso definimos la "fuente de verdad" para evitar alucinaciones, creando tres documentos oficiales en formato `.txt` con las directrices del Departamento Legal:
* **01_Clausulas_Contractuales.txt:** Manual de cláusulas estandarizadas, tipos de contrato y cláusulas mínimas obligatorias.
* **02_Proteccion_Datos.txt:** Política de protección de datos personales, consentimiento informado y derechos de los titulares.
* **03_Cumplimiento_Etica.txt:** Guía de cumplimiento normativo, prevención de conflictos de interés y código de ética corporativo.

### Paso D: Chunking + Embeddings + Chroma (Indexación)
Ejecuta la celda ubicada debajo de `(3. Chunking + Embeddings + Chroma — indexar los documentos legales)`.
* **Chunking:** Se divide cada archivo en fragmentos por cada sección numerada para respetar su unidad semántica.
* **Embeddings:** Se convierten los chunks en vectores usando `GoogleGenerativeAIEmbeddings` (`models/text-embedding-004`).
* **Almacenamiento en ChromaDB:** Se guardan en colecciones independientes (`chroma_contratos`, `chroma_proteccion_datos` y `chroma_cumplimiento_etica`) para búsquedas semánticas eficientes.

### Paso E: Agentes de Conocimiento (RAG)
Ejecuta la celda ubicada debajo de `(4. Agentes de Conocimiento (RAG))`. Cada agente recupera los fragmentos relevantes y responde estrictamente con ese contexto:
* **4.1 Agente de Contratos:** Responde sobre cláusulas estándar, plazos y procesos de firma.
* **4.2 Agente de Protección de Datos:** Responde sobre tratamiento de datos personales, consentimiento y retención.
* **4.3 Agente de Cumplimiento Normativo y Código de Ética:** Responde sobre obligaciones regulatorias y prevención de conflictos de interés.

### Paso F: Agente Multimodal de Imagen
Ejecuta la celda ubicada debajo de `(5. Agente Multimodal de Imagen)`. Procesa capturas de pantalla o escaneos de contratos (formatos válidos: PNG, JPG o JPEG), extrayendo texto y validando elementos clave. Toma automáticamente la última imagen cargada en el sistema.

### Paso G: Acción (Registro) con Sistema de Control
Ejecuta la celda ubicada debajo de `(6. Acción (registro) con sistema de control)`. Agente en LangChain que escribe solicitudes en `registro_solicitudes_legal.txt`. 
* **Sistema de control:** Valida obligatoriamente tipo de contrato, datos del proveedor, objeto/servicio, plazo, monto y si trata datos personales. Si falta algo, solicita los campos antes de guardar.

### Paso H: El Orquestador
Ejecuta la celda ubicada debajo de `(7. El Orquestador — agente LangChain que coordina las capacidades legales)`. Coordina todas las herramientas como un equipo (RAGs, multimodal y registros) e integra memoria (`InMemorySaver + thread_id`) para recordar el hilo de la conversación en múltiples mensajes.

### Paso I: Modo Interactivo
Ejecuta la celda final para escribir tus peticiones directamente en el cuadro de texto. El asistente enrutará inteligentemente al agente adecuado. Para terminar la sesión, escribe `salir`.

---

## ⚠️ Riesgos, Limitaciones y Mejoras Futuras
1. Crear un agente con permisos seguros para borrar datos y mantener la base de registros limpia y actualizada.
2. Desarrollar un agente de imágenes capaz de analizar archivos mediante enlaces web directos.
3. Implementar un agente evaluador que analice cláusulas para sugerir automáticamente la viabilidad de firma de contratos.
4. Controlar y gestionar de forma estricta los límites de tokens por consulta del modelo.
5. Administrar de manera segura la protección y el uso de la API Key.
