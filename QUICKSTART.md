# ⚡ QUICK START - Wrangler Deploy

## Deploy in 3 Commands

```bash
# 1. Install
npm install

# 2. Login to Cloudflare
npx wrangler login

# 3. Deploy!
npm run deploy
```

Your site will be live at: `https://st-augustine-academy.pages.dev`

## Add Your API Key

```bash
npx wrangler pages secret put VITE_GEMINI_API_KEY
# Paste your Gemini API key when prompted
```

Get API key: https://makersuite.google.com/app/apikey

## What Was Fixed?

✅ Wrong package name (`@google/genai` → `@google/generative-ai`)
✅ Wrong API class (`GoogleGenAI` → `GoogleGenerativeAI`)
✅ Wrong model name (`gemini-3-flash-preview` → `gemini-1.5-flash`)
✅ React 19 → React 18 (stable)
✅ Environment variables fixed
✅ Proper project structure
✅ SPA routing configured
✅ Wrangler setup included

## Local Development

```bash
# Run dev server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Update & Redeploy

```bash
# Make changes, then:
npm run deploy
```

## Default Login

**Student**: student / password
**Admin**: admin / password

Change in `src/constants.tsx`

## Troubleshooting

**Build fails?**
```bash
rm -rf node_modules package-lock.json
npm install
```

**Not logged in?**
```bash
npx wrangler login
```

**API not working?**
```bash
# Check your secret is set
npx wrangler pages secret list

# Add if missing
npx wrangler pages secret put VITE_GEMINI_API_KEY
```

## Full Documentation

See `README.md` for complete guide with:
- Custom domains
- Environment management
- Advanced features
- Monitoring & analytics
- Security best practices

That's it! Your site is production-ready. 🚀
