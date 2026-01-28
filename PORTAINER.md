# Portainer-deploy (Docker Stack) – djsnabu.com

## Ennen kuin aloitat
- **Älä tallenna tunnel tokenia Git-repoon.** Käytä Portainerin Env Vars -kenttää.
- Cloudflare Zero Trustissa hostnamet (`djsnabu.com`, `www.djsnabu.com`) tulee routata tähän tunneliin ja serviceksi `http://astro-site:3000`.

## Vaihtoehto A (suositus): Portainer Stack “Git repository”
1. Portainer → **Stacks** → **Add stack**
2. Valitse **Repository**
3. Täytä:
   - **Repository URL**: (sun repo URL)
   - **Repository reference**: `main` (tai branch)
   - **Compose path**: `docker-compose.yml`
4. **Environment variables**:
   - `TUNNEL_TOKEN` = (Cloudflare tunnel token)
   - (valinnainen) `PUBLIC_INSTAGRAM_API_URL` = (Behold.so JSON endpoint)
5. Klikkaa **Deploy the stack**

## Vaihtoehto B: Portainer Stack “Web editor”
1. Portainer → **Stacks** → **Add stack**
2. Valitse **Web editor**
3. Liitä `docker-compose.yml` sisällöt
4. Lisää **Environment variables** kuten yllä
5. **Deploy the stack**

## Tarkistus / debug
- Portainer → Stack → **Logs**
  - `tunnel`: pitäisi näkyä “Connected / Registered tunnel”
  - `astro-site`: build + serve

Jos domain ei aukea:
1. Cloudflare Zero Trust → Tunnel → varmista että hostnamet osoittavat serviceen `http://astro-site:3000`
2. Varmista että stack on **running**
3. Katso `tunnel`-containerin logit (token / DNS / hostname route -virheet näkyy siellä)

