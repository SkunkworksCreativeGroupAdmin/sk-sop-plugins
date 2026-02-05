# Skunkworks S.O.P. Plugins Configuration

This repository contains [the centralized configuration](https://github.com/SkunkworksCreativeGroupAdmin/sk-sop-plugins/blob/main/plugins-config.json) for the **Skunkworks S.O.P. Plugins** MU-plugin. It dictates which plugins are activated or deactivated across different site environments (Staging, Production, and Archive).

## 🚀 How it Works

The WordPress MU-plugin fetches `plugins-config.json` every 12 hours (or on-demand) and ensures the site matches the environment rules defined here.

- **Always Active:** Managed plugins that must exist on every environment.
- **Staging Only:** Plugins active only on URLs containing `staging` or `skunk.ws`.
- **Production Only:** Plugins active only on live sites (not staging, backup, or archive).
- **Auto-Deactivation:** If a plugin is listed in a category that does not match the current environment, the MU-plugin will automatically deactivate it.

## 🛠 Management Instructions

### Adding/Editing Plugins
Edit `plugins-config.json` directly. The format is:
`"plugin-folder/main-file.php": "WordPress.org URL"`

1. **The Key:** Must be the internal WordPress plugin path (e.g., `cloudflare/cloudflare.php`).
2. **The Value:** The official WordPress.org URL. If provided, the MU-plugin will show a native installation popup if the plugin is missing.

### Forcing a Sync
If you make a change here and need it to reflect on a site immediately:
1. Go to the WordPress Dashboard of that site.
2. Navigate to **Plugins > Must-Use**.
3. Click **Force GitHub refresh** or **Recheck** on a missing plugin alert.

## 📂 JSON Schema Example

```json
{
  "always_active": {
    "cloudflare/cloudflare.php": "[https://wordpress.org/plugins/cloudflare/](https://wordpress.org/plugins/cloudflare/)"
  },
  "staging_only": {
    "password-protected/password-protected.php": ""
  },
  "production_only": {
    "broken-link-checker/broken-link-checker.php": "[https://wordpress.org/plugins/broken-link-checker/](https://wordpress.org/plugins/broken-link-checker/)"
  }
}
