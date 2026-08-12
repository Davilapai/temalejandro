# Tea Leaves

**A deep, dark mug of green tea with hints of chai and a view of the ocean.**

Tema para VS Code con dos variantes:

- **Teamalejandro** — oscuro, con soporte completo para C/C++, Python y Java.
- **Tea Leaves Light** — variante clara con la misma identidad de paleta.

## Instalación desde el repositorio

1. Clona o descarga el repositorio:

   ```sh
   git clone https://github.com/Davilapai/temalejandro.git
   ```

2. Abre VS Code y desde la vista **Extensiones** (Ctrl+Shift+X) abre el menú `...` y elige **Instalar desde VSIX...**, seleccionando el archivo `temalejandro-0.2.0.vsix` de la raíz del repositorio.

   Alternativamente, desde la terminal dentro de la carpeta del repositorio:

   ```sh
   code --install-extension temalejandro-0.2.1.vsix
   ```

3. Activa el tema: **Ctrl+K Ctrl+T** → elige **Teamalejandro** (oscuro) o **Tea Leaves Light** (claro).

## Recompilar el .vsix

Si modificas los temas y quieres regenerar el paquete:

```sh
npm install -g @vscode/vsce
vsce package
```

Esto genera un nuevo `temalejandro-<versión>.vsix` instalable desde la raíz del repositorio.
