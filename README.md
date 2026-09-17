# Mi panel financiero — deploy a Firebase Hosting

## Qué es esto
- `public/index.html` — la app completa (login + Deudas/Cuentas/Tarjeta/Stats), conectada a tu proyecto de Supabase.
- `firebase.json` / `.firebaserc` — configuración de Firebase Hosting.
- `.github/workflows/firebase-hosting-merge.yml` — despliega solo con hacer push a `main`.

## Pasos para dejarlo funcionando

1. **Crea el proyecto en Firebase** (console.firebase.google.com) si no tienes uno, y anota el Project ID.
2. Reemplaza `TU-PROJECT-ID-DE-FIREBASE` en `.firebaserc` y en el workflow por ese ID.
3. **Genera una service account key**:
   ```
   firebase init hosting:github
   ```
   (te lo hace todo: crea el secret `FIREBASE_SERVICE_ACCOUNT` en tu repo de GitHub automáticamente)
   — o hazlo a mano desde Firebase Console > Project Settings > Service Accounts > Generate new private key, y pega el JSON completo como secret `FIREBASE_SERVICE_ACCOUNT` en GitHub (Settings > Secrets > Actions).
4. Sube este repo a GitHub, en la rama `main`.
5. Cada push a `main` va a desplegar solo, gracias al workflow.

## Nota sobre Supabase
La URL y la llave pública (anon key) ya están en el HTML — eso es normal y seguro en Supabase: la seguridad real la dan las políticas RLS que ya configuramos (Row Level Security), no el secreto de la llave.
