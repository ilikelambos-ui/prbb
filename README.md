const db = globalThis.__B44_DB__ || { auth:{ isAuthenticated: async()=>false, me: async()=>null }, entities:new Proxy({}, { get:()=>({ filter:async()=>[], get:async()=>null, create:async()=>({}), update:async()=>({}), delete:async()=>({}) }) }), integrations:{ Core:{ UploadFile:async()=>({ file_url:'' }) } } };

# Welcome to PRBB - Base44 Project

## About

This is a modern React + Vite application configured for deployment to **Cloudflare Pages**.

View and Edit your app on [db.com](http://db.com) 

This project contains everything you need to run your app locally and deploy it to production.

## Prerequisites

1. **Node.js** 18+ installed
2. **npm** or **yarn** package manager
3. **Git** for version control

## Local Setup

### 1. Clone the Repository
```bash
git clone https://github.com/ilikelambos-ui/prbb.git
cd prbb
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Create Environment Configuration
Copy `.env.example` to `.env.local` and fill in your values:

```bash
cp .env.example .env.local
```

Update `.env.local`:
```
VITE_BASE44_APP_ID=your_app_id
VITE_BASE44_APP_BASE_URL=your_backend_url
```

### 4. Run Development Server
```bash
npm run dev
```

The app will be available at `http://localhost:3000`

## Build & Deployment

### Local Build
```bash
npm run build
```

Output will be in the `dist/` directory.

### Deploy to Cloudflare Pages

#### Option 1: Direct Git Integration (Recommended)
1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Navigate to **Pages** → **Create a project**
3. Select **Connect to Git**
4. Authorize GitHub and select `ilikelambos-ui/prbb`
5. Configure build settings:
   - **Framework preset:** `Vite (React)`
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
6. Add environment variables:
   - `VITE_BASE44_APP_ID`
   - `VITE_BASE44_APP_BASE_URL`
7. Click **Deploy**

#### Option 2: Using Wrangler CLI
```bash
# Install wrangler globally
npm install -g wrangler

# Authenticate
wrangler login

# Deploy
wrangler pages deploy dist --project-name=prbb
```

#### Option 3: GitHub Actions (Automated)
The repository includes a GitHub Actions workflow (`.github/workflows/deploy-cloudflare.yml`) that automatically deploys on push to `main`.

**Setup required secrets in GitHub:**
1. Go to repository **Settings** → **Secrets and variables** → **Actions**
2. Add these secrets:
   - `CLOUDFLARE_API_TOKEN` - [Get from Cloudflare](https://dash.cloudflare.com/profile/api-tokens)
   - `CLOUDFLARE_ACCOUNT_ID` - Your Cloudflare account ID
   - `VITE_BASE44_APP_ID` - Your Base44 app ID
   - `VITE_BASE44_APP_BASE_URL` - Your Base44 backend URL

### Connect Custom Domain

1. In Cloudflare Pages project settings
2. Go to **Custom domains**
3. Add your domain
4. Update DNS records as shown

## Available Scripts

```bash
npm run dev        # Start development server
npm run build      # Build for production
npm run preview    # Preview production build locally
npm run lint       # Run ESLint
npm run lint:fix   # Fix linting issues
npm run typecheck  # Run TypeScript type checking
```

## Project Structure

```
prbb/
├── src/
│   ├── components/     # React components
│   ├── pages/          # Page components
│   ├── lib/            # Utilities
│   ├── hooks/          # Custom React hooks
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── dist/               # Build output (generated)
├── public/             # Static assets
├── vite.config.js      # Vite configuration
├── tailwind.config.js  # Tailwind CSS config
├── postcss.config.js   # PostCSS config
├── eslint.config.js    # ESLint config
├── jsconfig.json       # JS compiler options
├── wrangler.toml       # Cloudflare configuration
└── package.json
```

## Tech Stack

- **React 18** - UI framework
- **Vite** - Build tool & dev server
- **Tailwind CSS** - Styling
- **Radix UI** - Accessible components
- **React Router** - Client-side routing
- **React Hook Form** - Form handling
- **TanStack Query** - Data fetching
- **Stripe** - Payment processing
- **Base44 SDK** - Backend integration

## Docs & Support

- **Documentation:** [Base44 Docs](https://docs.db.com/Integrations/Using-GitHub)
- **Support:** [db.com Support](https://app.db.com/support)
- **Cloudflare Pages Docs:** [Pages Documentation](https://developers.cloudflare.com/pages/)

## Troubleshooting

### Build fails locally
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Environment variables not loading
- Ensure `.env.local` is in the root directory
- Restart dev server after changing env vars
- Verify variables are prefixed with `VITE_` for frontend access

### Cloudflare deployment fails
- Check build logs in Cloudflare Dashboard
- Verify `dist/` directory is generated
- Ensure all required secrets are set in GitHub/Cloudflare

## Next Steps

1. ✅ Set up local development environment
2. ✅ Connect to Cloudflare Pages
3. ✅ Configure custom domain (if needed)
4. 📝 Publish changes to production
5. 📊 Monitor deployments in Cloudflare Dashboard
