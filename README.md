# EALC (Enchainement Astra Loop Chain)
```
import os
import google.generativeai as genai

# Configuración de la clave API
os.environ["API_KEY"] = ""  # Tu clave de API de Google

# Configurar la API de Google Generative AI
genai.configure(api_key=os.environ["API_KEY"])

# Configuración del modelo
generation_config = {
    "temperature": 0.7,
    "top_p": 0.95,
    "top_k": 64,
    "max_output_tokens": 65536,
    "response_mime_type": "text/plain",
}

# Modelo de generación de texto
model = genai.GenerativeModel(
    model_name="gemini-2.0-flash-thinking-exp-01-21",
    generation_config=generation_config,
)

# Función principal para el Enchantment Loop + Chain of Astra + Chain of Thought
def enchainment_then_astra(input_text, enchainment_loops, astra_iterations):
    chat_session = model.start_chat(history=[])

    # Enchantment Loop: Mejorar la pregunta antes de responder
    improved_question = input_text
    for loop in range(enchainment_loops):
        print(f"\n--- Enchantment Loop Iteration {loop+1} ---")
        response = chat_session.send_message(f"Mejora esta pregunta para hacerla más clara y detallada solo pon la pregunta: {improved_question}")
        improved_question = response.text
        print(f" {improved_question}")

    # Procesar la pregunta mejorada con el modelo base
    print("\n--- Procesando la respuesta final del Enchantment Loop con el modelo base ---")
    base_response = chat_session.send_message(f"Procesa y responde esta pregunta final: {improved_question}")
    print(f"Respuesta del modelo base: {base_response.text}")

    # Chain of Astra: Mejorar la respuesta generada
    final_response = base_response.text
    for i in range(astra_iterations):
        print(f"\n  --- Iteración Chain of Astra {i+1} ---")
        response = chat_session.send_message(f"Mejora esta respuesta agregando más detalles e información: {final_response}")
        final_response = response.text
        print(f"{final_response}")

    print("\n--- Resultado final después de todo el proceso ---")
    print(final_response)

# Input inicial
input_text = "Si tienes 3 velas con diferentes longitudes y las enciendes al mismo tiempo, y las vas apagando aleatoriamente, y al final del experimento las velas quedan asi: 1.--- , 2.----- , 3.- , cual apagaste primero"
# Número de mejoras en el Enchantment Loop
enchainment_loops = int(input("¿Cuántas veces quieres mejorar la pregunta con Enchantment Loop? "))
# Número de mejoras en Chain of Thought
astra_iterations = int(input("¿Cuántas veces quieres mejorar la respuesta con Chain of Astra? "))

# Ejecutar el proceso
enchainment_then_astra(input_text, enchainment_loops, astra_iterations)
```
