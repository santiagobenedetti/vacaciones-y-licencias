# Vacaciones y Licencias

Sistema de gestión de vacaciones y licencias con autenticación Google SSO.

## Características

- 🔐 Autenticación con Google SSO
- 📊 Dashboard con información de usuario
- 🏖️ Visualización de días de vacaciones disponibles
- 📱 Diseño responsive con Tailwind CSS
- ⚡ Construido con Next.js 15 y TypeScript

## Requisitos Previos

- Node.js 18+ instalado
- Cuenta de Google Cloud Platform
- Credenciales OAuth 2.0 de Google

## Configuración de Google OAuth

1. Ve a [Google Cloud Console](https://console.cloud.google.com/)
2. Crea un nuevo proyecto o selecciona uno existente
3. Navega a "APIs & Services" > "Credentials"
4. Haz clic en "Create Credentials" > "OAuth client ID"
5. Selecciona "Web application"
6. Agrega las URIs de redirección autorizadas:
   - `http://localhost:3000/api/auth/callback/google` (desarrollo)
   - Tu URL de producción cuando despliegues
7. Copia el Client ID y Client Secret

## Instalación

1. Clona el repositorio:
```bash
git clone https://github.com/santiagobenedetti/vacaciones-y-licencias.git
cd vacaciones-y-licencias
```

2. Instala las dependencias:
```bash
npm install
```

3. Crea un archivo `.env` basado en `.env.example`:
```bash
cp .env.example .env
```

4. Edita el archivo `.env` y agrega tus credenciales:
```env
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=genera-una-clave-secreta-aleatoria
GOOGLE_CLIENT_ID=tu-google-client-id
GOOGLE_CLIENT_SECRET=tu-google-client-secret
```

Para generar un `NEXTAUTH_SECRET`, puedes usar:
```bash
openssl rand -base64 32
```

## Ejecución en Desarrollo

```bash
npm run dev
```

Abre [http://localhost:3000](http://localhost:3000) en tu navegador.

## Construcción para Producción

```bash
npm run build
npm start
```

## Estructura del Proyecto

```
vacaciones-y-licencias/
├── app/
│   ├── api/
│   │   └── auth/
│   │       └── [...nextauth]/
│   │           └── route.ts      # Configuración de NextAuth
│   ├── dashboard/
│   │   └── page.tsx              # Dashboard protegido
│   ├── globals.css               # Estilos globales
│   ├── layout.tsx                # Layout principal
│   └── page.tsx                  # Página de login
├── components/
│   └── Providers.tsx             # Provider de sesión
└── ...
```

## Tecnologías Utilizadas

- **Next.js 15**: Framework de React
- **TypeScript**: Tipado estático
- **NextAuth.js**: Autenticación
- **Tailwind CSS**: Estilos
- **Google OAuth**: Proveedor de autenticación

## Próximas Funcionalidades

- [ ] Solicitud de días de vacaciones
- [ ] Historial de vacaciones
- [ ] Calendario de equipo
- [ ] Notificaciones por email
- [ ] Panel de administración

## Licencia

ISC
