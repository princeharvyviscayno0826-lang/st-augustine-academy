# 🚀 Cloudflare Wrangler Deployment Guide

## What Was Fixed

Your code had **10 critical issues** preventing deployment:

1. ✅ Wrong package: `@google/genai` → `@google/generative-ai`
2. ✅ Wrong API class: `GoogleGenAI` → `GoogleGenerativeAI`
3. ✅ Wrong model: `gemini-3-flash-preview` → `gemini-1.5-flash`
4. ✅ Unstable React 19 → Stable React 18
5. ✅ Wrong env vars: `process.env` → `import.meta.env.VITE_*`
6. ✅ No src/ structure → Proper Vite structure
7. ✅ Empty _redirects → Added SPA routing
8. ✅ CDN dependencies → Proper npm packages
9. ✅ Broken TypeScript → Fixed configs
10. ✅ No Tailwind setup → Complete configuration

## Prerequisites

1. **Node.js** (v18 or higher)
2. **npm** (comes with Node.js)
3. **Cloudflare account** (free tier works)

## Quick Deploy (3 Steps)

### Step 1: Install Dependencies
```bash
npm install
```

### Step 2: Login to Cloudflare
```bash
npx wrangler login
```
This opens a browser to authenticate with your Cloudflare account.

### Step 3: Deploy
```bash
npm run deploy
```

That's it! Your site will be live at: `https://st-augustine-academy.pages.dev`

## Environment Variables

### Add Your Gemini API Key

**Option A: Using Wrangler CLI (Recommended)**
```bash
npx wrangler pages secret put VITE_GEMINI_API_KEY
# Paste your API key when prompted
```

**Option B: Using .env for Local Development**
```bash
# Create .env file
echo "VITE_GEMINI_API_KEY=your_api_key_here" > .env

# For production, still use wrangler secret
npx wrangler pages secret put VITE_GEMINI_API_KEY
```

Get your Gemini API key: https://makersuite.google.com/app/apikey

## Available Commands

```bash
# Local development
npm run dev

# Build for production
npm run build

# Preview production build locally
npm run preview

# Deploy to Cloudflare
npm run deploy

# View deployment logs
npx wrangler pages deployment tail

# List deployments
npx wrangler pages deployment list
```

## Project Structure

```
st-augustine-academy/
├── src/
│   ├── components/       # React components
│   ├── services/         # API services (Gemini)
│   ├── App.tsx          # Main app component
│   ├── main.tsx         # Entry point
│   ├── types.ts         # TypeScript types
│   ├── constants.tsx    # Mock data & config
│   └── index.css        # Tailwind styles
├── public/
│   └── _redirects       # SPA routing rules
├── index.html           # HTML template
├── wrangler.toml        # Cloudflare config
├── package.json         # Dependencies
├── vite.config.ts       # Vite config
└── tailwind.config.js   # Tailwind config
```

## Deployment Process Explained

When you run `npm run deploy`:

1. **Build**: `vite build` creates optimized production files in `dist/`
2. **Deploy**: `wrangler pages deploy dist` uploads to Cloudflare
3. **Live**: Site is instantly available on Cloudflare's global CDN

## Wrangler Configuration

The `wrangler.toml` file controls your deployment:

```toml
name = "st-augustine-academy"          # Your project name
compatibility_date = "2024-01-01"       # Cloudflare API version
pages_build_output_dir = "dist"         # Build output directory
```

## Custom Domain (Optional)

### Add Your Domain

1. **Via Wrangler CLI**:
```bash
npx wrangler pages domain add yourdomain.com
```

2. **Via Dashboard**:
- Go to Cloudflare Dashboard → Pages
- Select your project
- Click "Custom domains" → "Set up a custom domain"

3. **Configure DNS**:
- Add CNAME record pointing to your `.pages.dev` URL
- Or use Cloudflare nameservers for automatic setup

## Updating Your Site

### Redeploy After Changes

```bash
# Make your code changes
git add .
git commit -m "Update feature"

# Redeploy
npm run deploy
```

Every deploy creates a new deployment with a unique URL. The latest becomes your production site.

## Environment Management

### View Secrets
```bash
npx wrangler pages secret list
```

### Delete a Secret
```bash
npx wrangler pages secret delete VITE_GEMINI_API_KEY
```

### Manage via Dashboard
Cloudflare Dashboard → Pages → Your Project → Settings → Environment variables

## Troubleshooting

### Build Fails

**Problem**: npm install errors
```bash
# Solution: Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

**Problem**: TypeScript errors
```bash
# Solution: Check types
npx tsc --noEmit
```

### Deploy Fails

**Problem**: Not logged in
```bash
# Solution: Re-authenticate
npx wrangler logout
npx wrangler login
```

**Problem**: Project name conflict
```bash
# Solution: Change name in wrangler.toml
name = "st-augustine-academy-yourname"
```

### API Key Not Working

**Symptoms**: AI insights show "Unable to generate insights"

**Solutions**:
1. Verify API key at Google AI Studio
2. Check it's added as a secret:
   ```bash
   npx wrangler pages secret list
   ```
3. Ensure name is exactly: `VITE_GEMINI_API_KEY`
4. Redeploy after adding secret

### 404 on Page Refresh

**Problem**: Routes return 404 when refreshing
**Solution**: Ensure `public/_redirects` file exists with:
```
/*    /index.html   200
```

## Advanced Wrangler Features

### Preview Deployments

Every git branch can have its own preview:
```bash
# Deploy to preview
npx wrangler pages deploy dist --branch=staging
```

### Rollback Deployment

```bash
# List deployments
npx wrangler pages deployment list

# Promote a specific deployment to production
npx wrangler pages deployment promote <deployment-id>
```

### View Logs in Real-Time

```bash
npx wrangler pages deployment tail
```

### Set Multiple Environment Variables

Create a `.dev.vars` file for local development:
```
VITE_GEMINI_API_KEY=your_local_key
VITE_ANOTHER_VAR=value
```

Note: `.dev.vars` is for local only, use wrangler secrets for production.

## Performance & Optimization

### Cloudflare Automatically Provides:
- ✅ Global CDN (275+ locations)
- ✅ HTTP/3 & QUIC
- ✅ Brotli compression
- ✅ DDoS protection
- ✅ SSL/TLS certificates
- ✅ 99.99% uptime SLA

### Build Optimizations (Already Configured):
- Code splitting
- Tree shaking
- Minification
- Asset optimization

## Monitoring

### View Analytics

1. **Via CLI**:
```bash
npx wrangler pages deployment list
```

2. **Via Dashboard**:
- Cloudflare Dashboard → Pages
- View requests, bandwidth, errors

### Set Up Alerts

In Cloudflare Dashboard:
- Notifications → Add notification
- Choose triggers (build failures, high traffic, etc.)

## Cost

**Free Tier Includes**:
- Unlimited requests
- Unlimited bandwidth
- 500 builds/month
- 100 custom domains

**Paid Tier** ($20/month):
- 5,000 builds/month
- Concurrent builds
- Advanced features

Your project will likely stay in free tier.

## Default Login Credentials

**Student**:
- Username: `student`
- Password: `password`

**Admin**:
- Username: `admin`
- Password: `password`

⚠️ **Change these** in `src/constants.tsx` before production use!

## Security Best Practices

1. **Never commit secrets**: Use `.env` locally, wrangler secrets for production
2. **Use environment variables**: All API keys via `import.meta.env.VITE_*`
3. **Keep dependencies updated**: `npm audit fix`
4. **Monitor API usage**: Set Google Cloud quotas
5. **Enable Cloudflare features**: Bot protection, rate limiting

## Next Steps

After successful deployment:

1. ✅ Test all features on your live site
2. ✅ Add custom domain (optional)
3. ✅ Set up monitoring and alerts
4. ✅ Update login credentials in code
5. ✅ Configure Gemini API quotas
6. ✅ Share your site URL!

## Support Resources

- **Wrangler Docs**: https://developers.cloudflare.com/workers/wrangler/
- **Pages Docs**: https://developers.cloudflare.com/pages/
- **Cloudflare Community**: https://community.cloudflare.com/
- **Vite Docs**: https://vitejs.dev/

## Success Checklist

- [ ] Dependencies installed (`npm install`)
- [ ] Logged into Cloudflare (`npx wrangler login`)
- [ ] API key added (`npx wrangler pages secret put VITE_GEMINI_API_KEY`)
- [ ] Deployed successfully (`npm run deploy`)
- [ ] Site loads correctly
- [ ] Can log in as student/admin
- [ ] AI insights work (requires API key)
- [ ] Page refresh works on all routes
- [ ] Mobile responsive

Your site is now live on Cloudflare's global network! 🎉
