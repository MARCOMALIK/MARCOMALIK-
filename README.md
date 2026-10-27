# Marco Malik WhatsApp Mini Bot

**Node.js 20+ • WhatsApp Cloud API • Railway • Vercel • 646 منفرد command files**

یہ archive آپ کے فراہم کردہ menu text کو نئی branding کے ساتھ ایک editable bot/website starter میں بدلتا ہے۔ source menu کے header میں 681 commands لکھے ہیں؛ اس text میں 678 command entries ملیں، جن میں repeated names کے بعد 646 منفرد command names ہیں۔ ہر منفرد نام کی الگ JavaScript file ہے، جبکہ `data/source-menu.json` اصل category occurrences کو محفوظ کرتا ہے۔

## پہلے یہ حدود جان لیں

یہ اصل WhatsApp Cloud API کے لیے deployable starter ہے، پہلے سے آپ کے Meta account سے connected live service نہیں۔ حقیقی webhook کے لیے آپ کو اپنا Meta app/WhatsApp Business sender بنانا اور Railway یا Vercel میں secrets set کرنا ہوں گے۔ API کی اصل compatibility اور account approval Meta کے اختیار میں ہیں۔

Official Cloud API عام WhatsApp Groups/Channels کو manage نہیں کرتی، linked-device pairing/session code نہیں دیتی، اور کسی message کو حقیقی forwarded بنا کر نہیں دکھاتی۔ اس لیے group/admin/owner-setting اور pairing commands disabled یا preview ہیں۔ AI/download/media tools کو بھی provider APIs/credentials کے بغیر fake output نہیں دیا جاتا۔ NSFW، bulk/forwarding یا action commands فعال نہیں۔ یہ limits website اور bot menu میں واضح ہیں۔

## تصویر اور landing page

`public/hero-marko.svg` اس bundle کی اصل MM vector artwork ہے۔ اس پیغام میں آپ کی الگ تصویر attach نہیں ہوئی؛ اپنی تصویر شامل کرنے کے لیے اسی file کو اپنی image سے بدلیں اور `public/index.html` میں `hero-marko.svg` کا path update کریں۔ Title میں animated “Marco Malik WhatsApp Mini Bot” ticker ہے، ساتھ repository, Railway, Vercel اور WhatsApp channel buttons ہیں۔

`public/site-config.json` میں اپنی GitHub repo اور WhatsApp channel/contact کے حقیقی HTTPS links درج کریں۔ Repository/channel buttons link خالی ہونے پر disabled رہتے ہیں؛ کوئی فرضی URL نہیں لگایا گیا۔ Railway/Vercel buttons platform project pages کھولتے ہیں—یہ آپ کی app کو آپ کے account میں deploy نہیں کرتے جب تک GitHub repo import اور variables مکمل نہ ہوں۔

## GitHub میں upload

1. ZIP extract کریں۔
2. اندرونی `marco-malik-whatsapp-mini-bot` folder کے contents (جیسے `package.json`, `src/`, `public/`, `README-ur.md`) کو اپنی نئی GitHub repository کے root میں upload کریں۔
3. `.env`، tokens اور secrets upload نہ کریں؛ `.gitignore` پہلے سے `.env` کو خارج کرتا ہے۔
4. GitHub repository URL کو `public/site-config.json` میں `repositoryUrl` کے طور پر درج کریں؛ WhatsApp channel/contact links بھی اسی config میں ڈالیں۔

## Railway

1. Railway میں **New Project → Deploy from GitHub Repo** منتخب کرکے repository جوڑیں۔
2. Root directory پر `railway.json` build/start commands خودکار طور پر `npm install` اور `npm start` چلاتے ہیں۔
3. Service Variables میں نیچے کے variables درج کریں۔
4. Networking settings سے public domain بنائیں؛ `https://YOUR-DOMAIN/api/health` کو کھول کر service health دیکھیں۔
5. Meta Developers میں webhook callback `https://YOUR-DOMAIN/webhook`، وہی `VERIFY_TOKEN`، اور `messages` subscription درج کریں۔

## Vercel

1. Vercel میں GitHub repository import کرکے deploy کریں؛ `vercel.json` API handler route کرتا ہے۔
2. Project Settings → Environment Variables میں وہی WhatsApp variables شامل کرکے redeploy کریں۔
3. Vercel domain کے ساتھ Meta webhook URL `https://YOUR-DOMAIN/webhook` رکھیں۔
4. `/api/health` چیک کریں۔ Vercel serverless runtime میں in-memory opt-out state مستقل نہیں رہتی؛ حقیقی business use کے لیے persistent store شامل کریں۔

## Replit

1. Replit میں **Import from GitHub** منتخب کرکے اپنی repository import کریں۔
2. اگر Run configuration خودکار طور پر تیار نہ ہو تو Run command `npm start` رکھیں اور Shell میں `npm install` چلائیں۔
3. Replit Secrets میں Meta کے variables درج کریں؛ انہیں `.env` یا GitHub میں commit نہ کریں۔
4. اپنے Replit deployment سے ملنے والا public HTTPS URL Meta webhook کے طور پر استعمال کریں اور `/api/health` چیک کریں۔

## Meta variables

- `WHATSAPP_TOKEN` — Meta access token، secret
- `PHONE_NUMBER_ID` — WhatsApp Business sender Phone Number ID
- `META_APP_SECRET` — webhook signature verify کرنے کے لیے، secret
- `VERIFY_TOKEN` — آپ کا خود منتخب کردہ webhook verification string
- `OWNER_NAME` — default `Marco Malik`
- `OWNER_NUMBER` — بین الاقوامی format میں owner number؛ اسے hosting Variables میں رکھیں
- `BOT_PREFIX` — default `.`؛ مثلاً `.menu`
- `WHATSAPP_GRAPH_VERSION` — supported Graph API version؛ default `v23.0`، Meta docs کے مطابق اسے update کریں
- `PORT` — Railway خود مہیا کرتا ہے، local default `3000`

## Local run اور tests

```bash
npm install
cp .env.example .env
# .env میں local test values درج کریں؛ کبھی commit نہ کریں
npm test
npm start
```

Dashboard `http://localhost:3000` پر، command API `/api/commands` پر، status `/api/health` پر ہے۔

## Command status

`src/commands/` میں 646 الگ module files ہیں۔ Website/`COMMANDS.json` ہر entry کو `ready`, `preview`, `setup-required` یا `disabled` کے طور پر دکھاتی ہے۔ `.menu` categories دکھاتا ہے، مثلاً `.menu group` یا `.menu fun`; category لمبی ہو تو `.menu ai 2` جیسا page number دیں۔

- Ready: menu/help/ping/time/uptime/owner، caption، URL format check، چھوٹا unit convert.
- Preview: groups, admin, pairing, settings, forwarding اور fictional fun results.
- Setup-required: AI/media/download/search/religious data tools جن کے official providers ابھی configure نہیں.
- Disabled: NSFW، mass/action یا session-style functions.

## Security

Webhook POST پر `META_APP_SECRET` signature لازم ہے۔ API/UI کبھی token value واپس نہیں کرتے؛ logs میں صرف redacted status جاتا ہے۔ APK/media download یا arbitrary group messages فعال نہیں۔ Production سے پہلے opt-out persistence، message retention اور Meta business policies کا جائزہ لیں۔

