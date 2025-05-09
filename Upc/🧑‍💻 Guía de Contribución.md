Este repositorio sigue un flujo de trabajo estándar con Git y GitHub. Sigue estos pasos para contribuir correctamente al proyecto.

---

## ⚙️ 0. Configurar Git (usuario y correo)

Antes de comenzar, configura tu nombre de usuario y correo globalmente:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@example.com"
```

Puedes verificar la configuración actual con:

```bash
git config --list
```

---

## 🔐 1. Crear clave SSH y agregarla a GitHub

1. Genera una nueva clave (si no tienes una):
    
    ```bash
    ssh-keygen -t ed25519 -C "tu_correo@example.com"
    ```
    

2. Copia la clave pública:
    
    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```
    
3. Ve a [https://github.com/settings/keys](https://github.com/settings/keys), haz clic en **"New SSH key"** y pega tu clave.
    

---

## 📥 2. Clonar el repositorio

```bash
git clone git@github.com:JotaFab/Compression_Upc.git
cd Compression_Upc
```

---

## 🌱 3. Crear tu propia rama de trabajo

Antes de realizar cualquier cambio:

```bash
git checkout -b feature/nombre-descriptivo
```

Ejemplo:

```bash
git checkout -b feature/algoritmo-huffman
```

---

## 💾 4. Realizar cambios y crear commit

Haz tus cambios en el código y luego guarda el snapshot:

```bash
git add archivo_modificado.go
git commit -m "Agrega algoritmo de compresión Huffman"
```

---

## 🚀 5. Subir tus cambios a GitHub

```bash
git push origin feature/nombre-descriptivo
```

---

## 🔄 6. Crear Pull Request

1. Ve al repositorio en GitHub.
    
2. Haz clic en **"Compare & pull request"**.
    
3. Describe brevemente los cambios.
    
4. Espera revisión o aprobación.
    

---

## 🔃 7. Mantener sincronización con `main`

Antes de seguir trabajando:

```bash
git checkout main
git pull origin main
git checkout feature/nombre-descriptivo
git merge main
```

---

## 📌 Notas

- Siempre trabaja en ramas, nunca en `main`.
    
- Commits deben ser claros y concisos.
    
- Sincronízate frecuentemente para evitar conflictos.
    

---