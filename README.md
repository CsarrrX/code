# 📓 Guía Universal: Neovim + Jupyter + Conda (Python/R)

## 🛠️ 1. Configuración del Entorno (Conda)
Prepara cualquier entorno para que sea compatible con el flujo de notas.

1. Activar el entorno deseado:
conda activate NOMBRE_DE_TU_ENV

2. Instalar motores de ejecución y sincronización:
conda install -c conda-forge jupyterlab jupytext ipykernel -y

3. (Opcional) Soporte para lenguaje R:
conda install -c conda-forge r-base r-irkernel -y


## 🏗️ 2. Gestión de Kernels (Vincular Entornos a Jupyter)
Para que el navegador "vea" tu entorno de Conda, debes registrar el Kernel.

### Instalar Kernel
- Para Python:
  python -m ipykernel install --user --name NOMBRE_DE_ENV --display-name "Python (NOMBRE)"
- Para R:
  Rscript -e "IRkernel::installspec(user = FALSE, name = 'NOMBRE_R', displayname = 'R (NOMBRE)')"

### Eliminar Kernels (Limpieza)
Si borraste un entorno de Conda pero sigue apareciendo en Jupyter, elimínalo así:
1. Listar kernels instalados: 
   jupyter kernelspec list
2. Borrar el kernel deseado: 
   jupyter kernelspec uninstall NOMBRE_DEL_KERNEL


## 📦 3. Instalación de Paquetes de R
A diferencia de Python, en R puedes instalar paquetes de dos formas:

### A. Vía Conda (Recomendado para evitar errores de compilación)
conda install -c conda-forge r-ggplot2 r-dplyr r-scipy -y

### B. Vía Consola de R (Si no están en Conda)
# Entra a R y ejecuta:
install.packages('nombre_del_paquete', repos='https://cloud.r-project.org')

*Nota: Si da error de permisos en Fedora, usa: install.packages('pkg', lib='~/R/library')*


## 🔗 4. Sincronización de Archivos (Jupytext)
Vincula tu script de Neovim con el Notebook del navegador. Solo una vez por archivo.

# Para Python
jupytext --set-formats ipynb,py:hydrogen --sync archivo.py

# Para R
jupytext --set-formats ipynb,R:hydrogen --sync archivo.R


## 🚀 5. Flujo de Trabajo Diario

1. Servidor (Terminal 1): 
   conda activate NOMBRE_ENV && jupyter lab --no-browser
   (Abre el link en tu navegador).

2. Editor (Terminal 2): 
   nvim archivo.py o nvim archivo.R
   (Usa "# %%" para crear celdas y guarda con ":w").

3. Visualizador (Navegador): 
   Abre el .ipynb generado y selecciona el Kernel correspondiente arriba a la derecha.


## 💡 Marcadores de Celda Rápidos
# %%            -> Celda de Código.
# %% [markdown]  -> Celda de Texto / LaTeX.
