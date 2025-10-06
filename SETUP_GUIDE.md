# Setup Guide - Vacaciones y Licencias

## Google OAuth Setup Instructions

### Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click on the project dropdown at the top
3. Click "New Project"
4. Enter project name: "Vacaciones y Licencias"
5. Click "Create"

### Step 2: Enable Google+ API

1. In the left sidebar, go to "APIs & Services" > "Library"
2. Search for "Google+ API"
3. Click on it and press "Enable"

### Step 3: Configure OAuth Consent Screen

1. Go to "APIs & Services" > "OAuth consent screen"
2. Select "Internal" (for organization use only)
3. Click "Create"
4. Fill in:
   - App name: Vacaciones y Licencias
   - User support email: Your email
   - Developer contact: Your email
5. Click "Save and Continue"
6. Skip the Scopes section (click "Save and Continue")
7. Click "Back to Dashboard"

### Step 4: Create OAuth Credentials

1. Go to "APIs & Services" > "Credentials"
2. Click "+ CREATE CREDENTIALS" at the top
3. Select "OAuth client ID"
4. Application type: "Web application"
5. Name: "Vacaciones y Licencias Web Client"
6. Under "Authorized JavaScript origins", add:
   - `http://localhost:3000` (for development)
   - Your production URL when ready
7. Under "Authorized redirect URIs", add:
   - `http://localhost:3000/api/auth/callback/google` (for development)
   - Your production callback URL when ready (e.g., `https://yourdomain.com/api/auth/callback/google`)
8. Click "Create"
9. Copy the Client ID and Client Secret

### Step 5: Configure Environment Variables

1. In your project directory, copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and add your credentials:
   ```env
   NEXTAUTH_URL=http://localhost:3000
   NEXTAUTH_SECRET=your-generated-secret
   GOOGLE_CLIENT_ID=your-client-id-from-step-4
   GOOGLE_CLIENT_SECRET=your-client-secret-from-step-4
   ```

3. Generate a secure NEXTAUTH_SECRET:
   ```bash
   openssl rand -base64 32
   ```
   Or use: https://generate-secret.vercel.app/32

### Step 6: Install and Run

1. Install dependencies:
   ```bash
   npm install
   ```

2. Run the development server:
   ```bash
   npm run dev
   ```

3. Open [http://localhost:3000](http://localhost:3000) in your browser

4. Click "Iniciar sesión con Google"

5. Sign in with your Google account

6. You'll be redirected to the dashboard!

## Troubleshooting

### "Access blocked: This app's request is invalid"
- Make sure you added the correct redirect URI in Google Cloud Console
- The URI must exactly match: `http://localhost:3000/api/auth/callback/google`

### "Error: Invalid client"
- Double-check your Client ID and Client Secret in `.env`
- Make sure there are no extra spaces or quotes

### Redirect to login page after authentication
- Check that NEXTAUTH_URL matches your current URL
- Verify NEXTAUTH_SECRET is set and not empty

### Session not persisting
- Clear your browser cookies
- Make sure NEXTAUTH_SECRET is a strong, random string
- Check browser console for errors

## Deployment to Production

When deploying to production (e.g., Vercel, Netlify):

1. Add production environment variables in your hosting platform
2. Update NEXTAUTH_URL to your production domain
3. Add production redirect URI in Google Cloud Console
4. Ensure NEXTAUTH_SECRET is different from development

## Security Notes

- Never commit `.env` file to version control (it's in `.gitignore`)
- Use different credentials for development and production
- Regularly rotate your NEXTAUTH_SECRET
- For production, consider restricting OAuth consent screen to specific domains
