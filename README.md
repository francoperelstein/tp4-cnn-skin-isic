# TP4 - Redes convolucionales para clasificar lesiones de piel (ISIC)

Trabajo práctico de **Redes Neuronales en Bioingeniería** (ITBA). Clasificación de 9 clases de lesiones de piel (dataset ISIC, 844 imágenes sin duplicados) comparando una MLP con una CNN, decisiones de arquitectura y data augmentation.

## Cómo reproducirlo
1. Abrir TP4_CNN_en_Skin_Dataset.ipynb en Google Colab con GPU (T4).
2. El notebook ya incluye la primera celda que clona el repo de la cátedra (https://github.com/cselmo/CNN-en-Skin-Dataset.git) para obtener los datos, que no están en este repo.
3. Ejecutar todas las celdas en orden. Tarda aproximadamente [el tiempo que te mostró Colab] minutos. Probado con torch 2.14.1+cu130.

## Constantes
No se modificó ninguna constante de la sección 0 (semilla del split 42, 3 semillas por experimento, 5 en la evaluación final).

## Resultados principales
- Split estratificado 60/20/20: 506 / 169 / 169 imágenes (se eliminaron 34 duplicados de 878).
- CNN contra MLP en test (5 semillas): 0.683 ± 0.026 contra 0.504 ± 0.053; CNN con 269.521 parámetros contra 6.358.793.
- La CNN final (3 bloques, 8 filtros, kernel 3, 64 px, flips+rot90+color) dio 0.641 ± 0.042 en validación; ninguna variante de arquitectura o augmentation superó claramente el ruido entre semillas.
- Melanoma es la clase más difícil (recall 0.30, semilla 0).

## Limitaciones
Dataset chico, una sola partición, 3 semillas, GPU no determinista (≈1.4 puntos entre corridas), atajos por resolución y color, posible fuga por pacientes o lesiones repetidas.

## Uso de IA
Usé Claude (Anthropic) como asistente para entender el código del notebook, revisar la coherencia entre los resultados y los textos. Ejecuté el notebook completo en Google Colab con GPU, sin modificar las constantes. Verifiqué a mano los cálculos de parámetros y de campo receptivo contra la tabla.
