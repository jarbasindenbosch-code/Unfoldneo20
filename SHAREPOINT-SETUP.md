# SharePoint-koppeling — instructie voor ICT

De Unfold Neo-app leest én schrijft de leerling-voortgang naar één SharePoint-lijst
via Microsoft Graph. Aanmelden gebeurt in de browser met Entra ID (MSAL, PKCE).

## 1. App registration (Entra ID)
In de bestaande App registration:
- **Authentication → Add a platform → Single-page application (SPA)**.
- Redirect URI = de exacte URL waarop de app draait, bijvoorbeeld:
  `https://<gebruiker>.github.io/<repo>/`
  (de app toont de juiste URI ook zelf onder het koppelscherm — kopieer die).
- **API permissions → Microsoft Graph → Delegated → `Sites.ReadWrite.All`**
  → daarna **Grant admin consent**. (Standaard-scopes openid/profile/offline_access
  voegt MSAL zelf toe.) Type is **Delegated**, niet Application.

Waarden die de gebruiker in de app invult: **Client ID**, **Tenant ID**
(GUID of `contoso.onmicrosoft.com`), **site-URL**, **lijstnaam**.

## 2. SharePoint-lijst
Maak in de site een lijst (bijv. "Neo Voortgang") met deze kolommen.
Let op: SharePoint heeft gereserveerde kolomnamen (o.a. `Type`), daarom hebben
alle eigen kolommen de prefix **`Neo`**. Neem de namen exact zo over.

| Kolom            | Type                     |
|------------------|--------------------------|
| Title            | (bestaat standaard) — bevat het record-id, uniek |
| NeoLeerlingNaam  | Eén regel tekst          |
| NeoLeerlingKlas  | Eén regel tekst          |
| NeoThema         | Eén regel tekst          |
| NeoThemaLabel    | Eén regel tekst          |
| NeoNiveau        | Eén regel tekst          |
| NeoXP            | Getal                    |
| NeoType          | Eén regel tekst          |
| NeoChallengeType | Eén regel tekst          |
| NeoCategorie     | Eén regel tekst          |
| NeoAfgerond      | Ja/nee                   |
| NeoAfgerondOp    | Datum en tijd            |
| NeoVoortgang     | Getal                    |
| NeoRubricScore   | Getal                    |
| NeoReflectie     | Meerdere regels tekst    |
| NeoData          | Meerdere regels tekst    |

`NeoData` bevat het volledige record als JSON, zodat **alle** NEO-velden bewaard
blijven, ook als er later velden bijkomen. De losse kolommen zijn voor filteren/
rapporteren in SharePoint zelf.

Tip: geef de kolom bij het aanmaken meteen deze naam als weergavenaam en zonder
spaties, dan is de interne naam gelijk aan bovenstaande (Graph gebruikt de
interne naam).

## 3. Gebruik
Admin → Integraties → **SharePoint-koppeling**: velden invullen →
**Verbinding testen** (controleert site, lijst en kolommen) →
**Nu synchroniseren** (leest eerst uit SharePoint, voegt samen, schrijft terug).

## Let op
- Werkt alleen via **https** (de gehoste site), niet met `file://`.
- Bij ontbrekende kolommen meldt "Verbinding testen" precies welke; die velden
  worden dan overgeslagen tot ze bestaan.
