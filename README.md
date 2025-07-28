# NordPVE

A **[Nordic](https://www.nordtheme.com/)**-inspired light & dark CSS theme for Proxmox VE’s web UI.  
Automatically switches to dark mode whenever Proxmox’s `theme-proxmox-dark.css` is loaded.

---

## Screenshots

- Coming soon

## Features

- **Light** (Nordic Polar Day) by default  
- **Dark** (Nordic Polar Night) when Proxmox’s dark stylesheet is present  
- No JS-framework dependencies—just vanilla CSS & a tiny inline script  
- Easy to install and override via Proxmox’s `index.html.tpl`

---

## Installation

1. **Copy the CSS**  
   Place `nord.css` into your Proxmox server’s static‐assets folder.  
   By default this is:  
```

/usr/share/pve-manager/images/nord.css

```

2. **Patch the Proxmox template**  
Edit (or better: override) Proxmox’s `index.html.tpl`—usually at:  
```

/usr/share/pve-manager/index.html.tpl

````
and add *before* the existing `</head>` the following snippet:

```html
<script>
  document.addEventListener('DOMContentLoaded', () => {
    // Detect if Proxmox’s dark stylesheet is loaded
    const darkLink = document.querySelector(
      'link[href*="theme-proxmox-dark.css"]'
    );
    if (darkLink) {
      document.body.classList.add('proxmox-theme-dark');
    }
  });
</script>

<link rel="stylesheet" href="/pve2/images/nord.css">
````
(An example index.html.tpl ships in this repo, see the `Example` folder)

3. **Clear browser cache**
   After restarting the PVE manager service, do a hard-refresh (Ctrl+F5) so your new CSS and script take effect.

4. **Restart Proxmox GUI**

   ```bash
   systemctl restart pveproxy
   ```

---

## How It Works

* **Light mode**
  All rules scoped under `body:not(.proxmox-theme-dark)` apply Nordic Polar Day defaults.

* **Dark mode**
  When Proxmox itself loads its `theme-proxmox-dark.css`, our small `<script>` adds `.proxmox-theme-dark` to `<body>` and you can write complementary CSS rules (e.g. under `body.proxmox-theme-dark`) for Nordic Polar Night.

---

## Customization

* Feel free to edit any of the `--baseXX` or `--accent` variables at the top of `nord.css` to tweak colors.
* To add new dark-mode overrides, target:

  ```css
  body.proxmox-theme-dark .your-selector {
    /* dark-mode styles here */
  }
  ```

---

## Contributing

1. Fork this repo
2. Create a feature branch (`git checkout -b my-tweak`)
3. Commit your changes (`git commit -am 'Add foo'`)
4. Push and open a Pull Request

Bug reports and PRs for improved selectors, additional components, or accessibility tweaks are very welcome!

---

## License

This repo is licensed under **CC BY-NC 4.0**.

* ✅ Free to use, modify & share for **non-commercial** purposes (with attribution).
* ❗️ For commercial use please see the license file

---

Enjoy a Nordic-themed Proxmox UI! 🚀


