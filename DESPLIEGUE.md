# Despliegue de Progress+

Tiempo estimado: 10 minutos. Hacen falta dos cuentas: GitHub (con acceso a este repo) y [Vercel](https://vercel.com) (se puede entrar con GitHub). No hace falta base de datos: la app es un solo `index.html` y guarda los datos en el navegador.

## 0. Antes de empezar

- Los cambios de la corrección están en la rama `correccion-spec`. Tienen que estar unidos a `main` en GitHub antes del paso 2, porque Vercel publica `main`.
- La spec recomienda renombrar el repo (hoy se llama `IMV`) a algo como `progress-plus`. Si lo hacen, háganlo antes de importarlo en Vercel: **Settings** → **Repository name** en GitHub.

## 1. Probarlo en la computadora (opcional)

Abran `index.html` con un servidor local, no con doble clic (el registro usa funciones del navegador que solo andan en `localhost` o `https`):

```bash
python3 -m http.server 8000
```

y entren a `http://localhost:8000`.

## 2. Publicar en Vercel

1. En Vercel: **Add New…** → **Project** → importen este repo desde GitHub.
2. En **Framework Preset** elijan **Other**. No completen comandos de build ni carpeta de salida.
3. **Deploy** y copien la dirección (`https://progress-plus-xxxx.vercel.app`).

No hay variables de entorno que cargar.

## 3. Recorrido de verificación

1. Creen una cuenta. Antes de entrar, la app pide edad, peso, altura, sexo, actividad y objetivo. Se ven los avisos de datos en el dispositivo y de que no reemplaza a un nutricionista.
2. Prueben una edad de 5 o un peso de 400: muestra el error y no deja seguir.
3. Al entrar, la meta de calorías y de agua salen de sus datos. En **Entreno** → **Peso** hay un solo registro: el del alta.
4. **Perfil**: se ve el IMC con su categoría. Editen la altura y miren que cambia. Con edad menor a 18 se ve el número sin categoría.
5. **Nutrición**: hay una sugerencia por franja y la suma queda cerca de la meta. Toquen **Registrar** en una y aparece en "Registrado hoy". **Otra opción** cambia la sugerencia.
6. Carguen una comida después de las 21:00: cuenta para ese mismo día.
7. **Agua**: activen **Recordatorios** y acepten las notificaciones. Con la pestaña abierta, llega un aviso cada 1 a 4 horas si no llegaron a la meta.
8. Registren un peso nuevo: se desbloquea "Punto de partida".
9. En **Perfil** → engranaje se lee dónde se guardan los datos.

## Notas

- **Datos en el navegador.** Cada cuenta y sus registros viven solo en el navegador donde se crearon. Otro dispositivo, una ventana de incógnito o borrar los datos del sitio empiezan de cero.
- **Recordatorios.** Llegan solo mientras la app está abierta. Si el navegador no permite notificaciones, el aviso aparece dentro de la app.
- **Menores de 18.** El objetivo "Bajar de peso" usa la meta de mantenimiento y sugiere consultar a un profesional. El IMC se muestra sin categoría.
- **Catálogo de ejemplo.** Los 42 alimentos y las combinaciones del plan son datos de ejemplo con valores aproximados. El grupo los revisa en `FOOD_CATALOG` y `PLAN_COMBOS` dentro de `index.html`.
- **Cuentas de la versión anterior.** Quien se registró antes de esta corrección tenía un perfil inventado (70 kg). Al entrar, la app le pide sus datos de nuevo y conserva sus comidas, agua y entrenamientos.

## Problemas comunes

| Síntoma | Causa y solución |
|---|---|
| Página en blanco al abrir `index.html` con doble clic | Ábranla con un servidor local o desde Vercel. |
| Página en blanco en Vercel | La app carga React desde internet. Revisen la conexión o que no haya un bloqueador de scripts. |
| Vercel pide un comando de build o falla el deploy | En **Settings** → **Build and Deployment** pongan **Framework Preset: Other** y dejen vacíos los comandos. |
| No llegan los recordatorios | La pestaña tiene que estar abierta, y el navegador tiene que tener permitidas las notificaciones para el sitio. |
| "No encontramos una cuenta con ese email" en otro dispositivo | Es lo esperado: las cuentas no se comparten entre dispositivos. |
