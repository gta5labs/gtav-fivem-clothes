<div align="center">

# FiveLabs · GTA V / FiveM Clothing Database

### A fast, developer-friendly collection of pre-rendered GTA V clothing previews for FiveM projects.

**Browse the database · Use direct image links · Integrate with NUI / websites · Self-hosted with GitHub Pages**

[🌐 Open Web Viewer](https://gta5labs.github.io/gtav-fivem-clothes/) ·
[📦 Repository](https://github.com/gta5labs/gtav-fivem-clothes) ·
[⬆️ Original Project](https://github.com/Reizenkun/gtav-fivem-clothes)

</div>

---

## Overview

This repository contains a large collection of **pre-rendered GTA V clothing previews** for male and female freemode characters.

It is useful for:

- FiveM clothing shops
- Character creators
- Inventory systems
- Outfit editors
- Web-based clothing databases
- NUI preview grids
- Developer tools
- Discord bots
- Any project that needs GTA V clothing thumbnails

The repository is published through **GitHub Pages**, so every image can also be accessed directly through a normal HTTPS URL.

---

## Live Viewer

Open the hosted browser here:

**https://gta5labs.github.io/gtav-fivem-clothes/**

---

## Direct Image URLs

The hosted image format is:

```text
https://gta5labs.github.io/gtav-fivem-clothes/renders/{gender}/{part}/{drawableId}_{textureId}.webp
```

### Example

```text
https://gta5labs.github.io/gtav-fivem-clothes/renders/male/accs/0_0.webp
```

Meaning:

| Value | Description |
|---|---|
| `male` | Character gender |
| `accs` | GTA clothing component |
| `0` | Drawable ID |
| `0` | Texture ID |
| `.webp` | Preview image format |

### Trimmed images

Some assets may also include a trimmed version:

```text
https://gta5labs.github.io/gtav-fivem-clothes/renders/{gender}/{part}/trimmed/{drawableId}_{textureId}.webp
```

Example:

```text
https://gta5labs.github.io/gtav-fivem-clothes/renders/male/accs/trimmed/0_0.webp
```

---

## Supported Clothing Parts

The database contains the standard GTA V freemode clothing component and prop groups.

| Part | Typical use |
|---|---|
| `head` | Head / face-related component |
| `berd` | Beard / mask-related component |
| `hair` | Hair |
| `uppr` | Upper body |
| `lowr` | Legs / lower body |
| `hand` | Bags / parachute / hand slot |
| `feet` | Shoes |
| `teef` | Accessories / neck |
| `accs` | Undershirts / accessories |
| `task` | Armor / task slot |
| `decl` | Decals / overlays |
| `jbib` | Tops / jackets |
| `p_head` | Hats / helmets |
| `p_eyes` | Glasses |
| `p_ears` | Ear accessories |
| `p_lwrist` | Left wrist |
| `p_rwrist` | Right wrist |

> GTA component naming can look unusual because these are the internal drawable slot names commonly used by GTA/FiveM tooling.

---

## Quick Start

### HTML

```html
<img
  src="https://gta5labs.github.io/gtav-fivem-clothes/renders/male/jbib/15_0.webp"
  alt="GTA V clothing preview"
/>
```

---

### JavaScript

```js
const CLOTHING_BASE_URL =
  "https://gta5labs.github.io/gtav-fivem-clothes/renders";

function getClothingImage(gender, part, drawable, texture = 0) {
  return `${CLOTHING_BASE_URL}/${gender}/${part}/${drawable}_${texture}.webp`;
}

const imageUrl = getClothingImage("male", "jbib", 15, 0);

console.log(imageUrl);
```

Result:

```text
https://gta5labs.github.io/gtav-fivem-clothes/renders/male/jbib/15_0.webp
```

---

## FiveM NUI Example

You can generate preview images directly from your clothing data instead of manually storing thousands of URLs.

```js
const BASE_URL =
  "https://gta5labs.github.io/gtav-fivem-clothes/renders";

function getPreviewUrl(item) {
  return `${BASE_URL}/${item.gender}/${item.component}/${item.drawable}_${item.texture}.webp`;
}

const clothingItem = {
  gender: "male",
  component: "jbib",
  drawable: 15,
  texture: 0
};

document.querySelector("#preview").src = getPreviewUrl(clothingItem);
```

HTML:

```html
<img id="preview" alt="Clothing preview">
```

---

## React Example

```jsx
const BASE_URL =
  "https://gta5labs.github.io/gtav-fivem-clothes/renders";

function ClothingPreview({
  gender,
  part,
  drawable,
  texture = 0
}) {
  const src =
    `${BASE_URL}/${gender}/${part}/${drawable}_${texture}.webp`;

  return (
    <img
      src={src}
      alt={`${part} ${drawable}:${texture}`}
      loading="lazy"
    />
  );
}
```

Usage:

```jsx
<ClothingPreview
  gender="male"
  part="jbib"
  drawable={15}
  texture={0}
/>
```

---

## Recommended Database Format

You do **not** need to save the complete image URL for every item.

Store only the clothing information:

```json
{
  "gender": "male",
  "part": "jbib",
  "drawable": 15,
  "texture": 0
}
```

Then generate the image URL in your frontend:

```js
function buildImageUrl(item) {
  return `https://gta5labs.github.io/gtav-fivem-clothes/renders/${item.gender}/${item.part}/${item.drawable}_${item.texture}.webp`;
}
```

This keeps your own database much smaller and easier to maintain.

---

## Handling Missing Images

Not every possible GTA combination is guaranteed to have a valid preview.

For websites or FiveM NUI projects, add a fallback:

```html
<img
  src="https://gta5labs.github.io/gtav-fivem-clothes/renders/male/jbib/15_0.webp"
  onerror="this.style.display='none'"
  alt="Clothing preview"
/>
```

Or in JavaScript:

```js
image.onerror = () => {
  image.src = "./assets/placeholder.webp";
};
```

For large clothing menus, using `loading="lazy"` is strongly recommended.

---

## Example Clothing Card

```html
<div class="clothing-card">
  <img
    src="https://gta5labs.github.io/gtav-fivem-clothes/renders/male/jbib/15_0.webp"
    loading="lazy"
    alt="JBIB 15 / Texture 0"
  >

  <div>
    <strong>JBIB 15</strong>
    <span>Texture 0</span>
  </div>
</div>
```

You can use the same approach for thousands of entries without hardcoding every individual URL.

---

## Repository Structure

```text
gtav-fivem-clothes/
│
├── renders/
│   ├── male/
│   │   ├── accs/
│   │   ├── feet/
│   │   ├── hair/
│   │   ├── jbib/
│   │   ├── lowr/
│   │   └── ...
│   │
│   └── female/
│       ├── accs/
│       ├── feet/
│       ├── hair/
│       ├── jbib/
│       ├── lowr/
│       └── ...
│
├── index.html
└── README.md
```

---

## Using This Repository With Your Own Website

You can use this repository purely as an image host.

For example, your website can live at:

```text
https://your-domain.com/
```

while clothing images are loaded from:

```text
https://gta5labs.github.io/gtav-fivem-clothes/renders/...
```

Example:

```js
const item = {
  name: "Black Jacket",
  gender: "male",
  part: "jbib",
  drawable: 15,
  texture: 0
};

item.preview =
  `https://gta5labs.github.io/gtav-fivem-clothes/renders/` +
  `${item.gender}/${item.part}/${item.drawable}_${item.texture}.webp`;
```

---

## Hosting Your Own Fork With GitHub Pages

If you fork this repository and want your own hosted image endpoint:

1. Open your fork on GitHub.
2. Go to **Settings**.
3. Open **Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select your main branch, such as `master`.
6. Select `/(root)`.
7. Save the configuration.
8. Wait for the GitHub Pages deployment to finish.

Your site will then normally be available at:

```text
https://YOUR-USERNAME.github.io/gtav-fivem-clothes/
```

And an image can be accessed using:

```text
https://YOUR-USERNAME.github.io/gtav-fivem-clothes/renders/male/accs/0_0.webp
```

---

## Performance Tips

When displaying hundreds or thousands of clothing items:

```html
<img loading="lazy" ...>
```

Also consider:

- rendering only visible cards
- using pagination or virtual scrolling
- caching generated URLs
- loading thumbnails on demand
- avoiding thousands of DOM elements at once
- using a placeholder when an image cannot be found

These changes make large FiveM clothing menus significantly smoother.

---

## Known Limitations

Some rendered items can contain visual or texture issues.

The upstream project specifically notes that certain items, such as some night-vision-related `p_head` assets, may not render perfectly.

The collection also represents the assets available when the source renders were generated, so newer GTA updates may contain clothing that is not yet present.

---

## Credits

This repository is a FiveLabs fork of:

**Reizenkun / gtav-fivem-clothes**  
https://github.com/Reizenkun/gtav-fivem-clothes

Original rendering/database work belongs to the respective upstream contributors.

FiveLabs maintains this fork and its GitHub Pages endpoint for use in FiveM development projects.

---

## Disclaimer

This is an unofficial community/developer resource.

Grand Theft Auto V, GTA Online and related assets are trademarks and intellectual property of their respective owners. This repository is not affiliated with or endorsed by Rockstar Games or Take-Two Interactive.

---

<div align="center">

### FiveLabs

Built for FiveM developers.

**https://gta5labs.github.io/gtav-fivem-clothes/**

</div>
