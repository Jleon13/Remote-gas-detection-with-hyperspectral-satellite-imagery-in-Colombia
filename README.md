# Gas Detection in Hyperspectral Satellite Imagery

## 🚀 Resumen del proyecto

Este repositorio contiene código para la detección de gases (CH₄, H₂O, CO₂) en imágenes hiperespectrales satelitales (SWIR).  
El flujo principal es:

1. **Modelado espectral** de cada gas usando la ley de Beer–Lambert y datos de HITRAN → firmas de gas (`t_vec`) a la resolución de tus 133 bandas SWIR.  
2. **Preprocesado**: carga de la imagen (`data`, `hdr['wavelength']`), alineación de bandas y generación de un vector columna de firma.  
3. **Clustering** en espacio Mahalanobis (whitening + K-Means con inicialización extrema en PC1) para filtrar “clutter” y dividir la escena en K clases.  
4. **Matched Filter (SLF)**: cálculo píxel-a-píxel de la puntuación  
   \[
     \mathrm{SLF}(x_{ij}) \;=\; 
     \frac{(x_{ij} - \mu_k)^\top \Sigma_k^{-1} \, t}
          {t^\top \Sigma_k^{-1} \, t}
   \]  
   sin ningún suavizado espacial, solo espectral.  
5. **Validación** con píxeles sintéticos y comparación opcional con clustering en espacio PCA.  

## 🔧 Instalación

1. **Clona el repositorio**  
   ```bash
   git clone https://github.com/tu_usuario/gas-detection-hyperspectral.git
   cd gas-detection-hyperspectral
   
2. **Crea y activa un entorno virtual**
  ```bash
    python3 -m venv venv
    source venv/bin/activate
