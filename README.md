# LumiPluginThemeManager

📖 English | [中文版](README_zh.md)

ThemeManager plugin: creates and registers `ThemeProviding`, persisting the user's selected theme to the plugin data directory. Theme packs ([LumiPluginThemePack](https://github.com/CofficLab/LumiPluginThemePack)) only register themes here.

## Features

- Creates `DefaultThemeProviding` and registers it as a host provider (the Kernel can stop and restart)
- Persists theme selection to `pluginDataDirectory(for: id)`
- Compatible with injected legacy `ThemeProviding`, preserving its themes and selection state
- Data migration for three historical directory layouts (each with an independent guard):
  - Between version directories: `db_*_vN/ThemeManager` → `db_*_vM/<pluginID>`
  - Within the same version root: `db_*_v6/ThemeManager` (early Lumi 6.0.0 layout)
  - Non-versioned: `<Application Support>/<bundleID>/ThemeManager` (early Kuzee layout)

## Dependencies

- [LumiKernel](https://github.com/CofficLab/LumiKernel) — `KernelCore`
- [LumiProviders](https://github.com/CofficLab/LumiProviders) — `ProviderStorage` / `ProviderTheme`
- [LumiLogging](https://github.com/CofficLab/LumiLogging) — `LumiLoggingKit`
- [LumiLocalization](https://github.com/CofficLab/LumiLocalization) — `LumiLocalizationKit`

## Usage

```swift
import PluginThemeManager

// Default ID (Lumi)
kernel.boot(ThemeManagerPlugin())

// Host custom ID (the persistence directory switches accordingly)
kernel.boot(ThemeManagerPlugin(id: "com.coffic.kuzee.plugin.theme-manager"))
```

## Tests

```bash
swift test
```
