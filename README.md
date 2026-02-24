# Nix Web App Manager

A nix flake that declares web applications.

## Installation

### Using Flakes (Recommended)

1. Add this flake to your Home Manager configuration:

```nix
  inputs = {
    nix-webapps.url = "github:AniviaFlome/nix-webapps";
  };
```

## Usage

### Example Configuration

```nix
{
 imports = [ inputs.nix-webapps.homeManagerModules.default ];

 programs.nix-webapps = {
  enable = true;
  browser = "brave";  # Set your preferred browser

  apps = {
    # Icon will be automatically fetched from Gmail's favicon
    # Uses browser (brave)
    gmail = {
      url = "https://mail.google.com";
      icon = null;
      comment = "Gmail Web App";
    };

    # Or specify a custom icon URL and override browser for this app
    github = {
      url = "https://github.com";
      icon = "https://github.githubassets.com/favicons/favicon.png";
      sha = "sha256-";
      browser = "chromium-browser";  # Override browser just for this app
      comment = "GitHub";
    };
  };
 };
}
```

## Configuration Options

### Module Options

- **`enable`**: Enable the webapp manager module
- **`browser`**: Default browser to use for all web apps
- **`apps`**: Attribute set of web applications

### Per-App Options

- **`url`** (required): The URL of the web application
- **`icon`** (optional): Icon URL (will be downloaded) or local file path. If not specified, automatically fetches from `<url>/favicon.ico`
- **`browser`** (optional): Browser to use for this specific app. Overrides `browser`.
- **`exec`** (optional): Custom exec command. If specified, overrides the browser setting
- **`comment`** (optional): Description shown in app launcher
- **`mimeTypes`** (optional): List of MIME types for protocol handling