# Nexus UI Library

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
![Version](https://img.shields.io/badge/version-1.0.0-purple)
![Roblox Supported](https://img.shields.io/badge/Roblox-✅-success)

Nexus UI is a modern, feature-rich Roblox UI library inspired by Microsoft's Fluent Design System and Linoria's clean aesthetics. Built with performance, customization, and developer experience in mind.

**Scripted by sk and rxzoa**

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Components](#components)
- [Theming](#theming)
- [Advanced Usage](#advanced-usage)
- [API Reference](#api-reference)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

Nexus UI provides a comprehensive set of customizable UI components with smooth animations, intuitive APIs, and robust theming. Designed specifically for Roblox development, it bridges the gap between professional design systems and game-appropriate interfaces.

```lua
-- Clean, readable syntax that doesn't look auto-generated
local Nexus = require(ReplicatedStorage.NexusUI)
local Theme = require(ReplicatedStorage.NexusUI.Theme)

local ui = Nexus:CreateInterface({
    Name = "PlayerMenu",
    Theme = Theme.Dark
})

local window = ui:CreateWindow({
    Title = "Inventory",
    Size = {400, 300}
})
```

## ✨ Features

- **🎨 Fluent Design Inspired**: Depth, motion, and scale effects
- **🎭 Complete Theme System**: Light, dark, and custom themes
- **⚡ Performance Optimized**: Minimal overhead, efficient rendering
- **📱 Responsive Components**: Adaptive to screen sizes
- **🔌 Plugin Support**: Built-in tools for Studio plugins
- **🔄 State Management**: Reactive data binding
- **🎮 Gamepad Support**: Full controller navigation
- **📦 Modular Architecture**: Import only what you need
- **🔧 Type Checking**: Optional Luau type definitions

## 📥 Installation

### Method 1: Roblox Library
1. Get the [Nexus UI Model](https://www.roblox.com/library/0000000000)
2. Insert into your game's ReplicatedStorage
3. Require the main module:

```lua
local Nexus = require(ReplicatedStorage:WaitForChild("NexusUI"))
```

### Method 2: Manual Setup
1. Download the latest release from GitHub
2. Place the `NexusUI` folder in ReplicatedStorage
3. Initialize in your script:

```lua
local Nexus = require(ReplicatedStorage.NexusUI)

-- Optional: Set default theme
Nexus:SetGlobalTheme("Dark")
```

### Method 3: Wally Package Manager
Add to your `wally.toml`:
```toml
[dependencies]
NexusUI = "skrxzoa/nexus-ui@1.0.0"
```

## 🚀 Quick Start

```lua
-- Basic interface setup
local Nexus = require(ReplicatedStorage.NexusUI)

-- Create a new interface instance
local interface = Nexus:CreateInterface({
    Name = "SettingsPanel",
    Theme = "Dark",
    AccentColor = Color3.fromRGB(0, 120, 215)
})

-- Create a window
local mainWindow = interface:CreateWindow({
    Title = "Game Settings",
    Position = {100, 100},
    Size = {350, 400},
    Resizable = true,
    Minimizable = true
})

-- Add a tab container
local tabContainer = mainWindow:CreateTabContainer()

-- Create tabs
local videoTab = tabContainer:AddTab("Video", "rbxassetid://10709845678")
local audioTab = tabContainer:AddTab("Audio", "rbxassetid://10709845679")

-- Add components to video tab
videoTab:AddLabel("Graphics Quality")
local qualitySlider = videoTab:AddSlider({
    Text = "Render Quality",
    Min = 1,
    Max = 10,
    Default = 7,
    Callback = function(value)
        settings().Rendering.QualityLevel = value
    end
})

-- Show the window
mainWindow:Show()
```

## 🧩 Components

### Window
```lua
local window = interface:CreateWindow({
    Title = "Character Customization",
    Position = UDim2.new(0.5, -200, 0.5, -150),
    Size = {400, 300},
    Style = "Modern", -- "Modern", "Classic", "Compact"
    ShowClose = true,
    ShowMinimize = true
})
```

### Button
```lua
local button = container:AddButton({
    Text = "Equip Item",
    Style = "Primary", -- "Primary", "Secondary", "Danger", "Success"
    Size = {120, 36},
    Callback = function()
        print("Item equipped!")
    end
})

-- Disabled state
button:SetEnabled(false)

-- Loading state
button:SetLoading(true)
```

### Toggle
```lua
local toggle = container:AddToggle({
    Text = "Enable Shadows",
    Default = true,
    Callback = function(state)
        lighting.GlobalShadows = state
    end
})
```

### Slider
```lua
local slider = container:AddSlider({
    Text = "Field of View",
    Min = 70,
    Max = 120,
    Default = 90,
    Decimals = 0,
    Callback = function(value)
        camera.FieldOfView = value
    end
})
```

### Dropdown
```lua
local dropdown = container:AddDropdown({
    Text = "Weapon Type",
    Options = {"Sword", "Axe", "Bow", "Staff"},
    Default = "Sword",
    MultiSelect = false,
    Callback = function(selected)
        print("Selected:", selected)
    end
})

-- Update options dynamically
dropdown:UpdateOptions({"Sword", "Axe", "Bow", "Staff", "Dagger"})
```

### Input
```lua
local input = container:AddInput({
    Text = "Player Name",
    Placeholder = "Enter username...",
    Default = "",
    ClearTextOnFocus = true,
    Callback = function(text)
        print("Input changed:", text)
    end
})
```

### Color Picker
```lua
local colorPicker = container:AddColorPicker({
    Text = "Team Color",
    Default = Color3.new(1, 0, 0),
    Callback = function(color)
        print("Color selected:", color)
    end
})
```

### Keybind
```lua
local keybind = container:AddKeybind({
    Text = "Sprint Key",
    Default = Enum.KeyCode.LeftShift,
    Callback = function(key)
        print("Keybind pressed:", key.Name)
    end
})
```

### Notification
```lua
interface:Notify({
    Title = "Item Collected",
    Text = "You found a rare sword!",
    Duration = 5,
    Type = "Success" -- "Info", "Success", "Warning", "Error"
})
```

## 🎨 Theming

### Built-in Themes
```lua
-- Apply theme globally
Nexus:SetGlobalTheme("Dark") -- "Dark", "Light", "Midnight"

-- Or per interface
local interface = Nexus:CreateInterface({
    Theme = "Light",
    AccentColor = Color3.fromRGB(0, 120, 215)
})
```

### Custom Themes
```lua
local customTheme = {
    Name = "Cyberpunk",
    Background = Color3.fromRGB(10, 10, 20),
    Surface = Color3.fromRGB(20, 20, 40),
    SurfaceAlt = Color3.fromRGB(30, 30, 60),
    Text = Color3.fromRGB(220, 220, 255),
    TextSecondary = Color3.fromRGB(180, 180, 220),
    Accent = Color3.fromRGB(0, 255, 200),
    Success = Color3.fromRGB(0, 255, 100),
    Warning = Color3.fromRGB(255, 200, 0),
    Error = Color3.fromRGB(255, 50, 50)
}

local interface = Nexus:CreateInterface({
    Theme = customTheme
})
```

### Dynamic Theme Switching
```lua
-- Switch themes at runtime
interface:SetTheme("Light")

-- Or toggle between light/dark
interface:ToggleTheme()

-- Listen for theme changes
interface.ThemeChanged:Connect(function(themeName)
    print("Theme changed to:", themeName)
end)
```

## 🔧 Advanced Usage

### Component Styling
```lua
local button = container:AddButton({
    Text = "Custom Button",
    Style = "Primary",
    CustomProperties = {
        CornerRadius = UDim.new(0, 12),
        BorderColor = Color3.new(1, 1, 1),
        BorderSize = 2,
        Font = Enum.Font.GothamBold,
        TextSize = 14
    }
})
```

### Animation Configuration
```lua
local interface = Nexus:CreateInterface({
    AnimationConfig = {
        Enable = true,
        Duration = 0.2,
        EasingStyle = Enum.EasingStyle.Quad,
        EasingDirection = Enum.EasingDirection.Out
    }
})
```

### State Management
```lua
-- Create a reactive state
local playerData = interface:CreateState({
    Health = 100,
    Level = 1,
    Inventory = {}
})

-- Subscribe to changes
playerData:Watch("Health", function(newHealth, oldHealth)
    print("Health changed:", oldHealth, "->", newHealth)
end)

-- Update state (triggers watchers)
playerData:Update({
    Health = 85,
    Level = 2
})
```

### Plugin Development
```lua
-- Nexus UI includes special tools for Roblox Studio plugins
local pluginUI = Nexus:CreatePluginInterface({
    Plugin = plugin,
    Name = "MyPlugin",
    Theme = "StudioDark" -- Special theme matching Roblox Studio
})

-- Toolbar integration
local toolbar = pluginUI:CreateToolbar("My Tools")
local button = toolbar:CreateButton("Generate", "Generate Terrain", "rbxassetid://10709845678")
```

### Mobile Optimization
```lua
local interface = Nexus:CreateInterface({
    MobileOptimized = true,
    TouchConfig = {
        ButtonMinSize = {44, 44}, -- Minimum touch target size
        SwipeNavigation = true,
        LongPressDelay = 0.5
    }
})
```

## 📚 API Reference

### Core Methods
| Method | Description | Returns |
|--------|-------------|---------|
| `Nexus:CreateInterface(options)` | Creates new UI interface | `Interface` |
| `Nexus:SetGlobalTheme(theme)` | Sets default theme for all new interfaces | `void` |
| `Nexus:GetVersion()` | Returns library version | `string` |

### Interface Methods
| Method | Description |
|--------|-------------|
| `interface:CreateWindow(options)` | Creates new window |
| `interface:Notify(options)` | Shows notification |
| `interface:SetTheme(theme)` | Changes interface theme |
| `interface:Destroy()` | Cleans up all UI elements |

### Component Methods (Common)
| Method | Description |
|--------|-------------|
| `component:SetVisible(visible)` | Shows/hides component |
| `component:SetEnabled(enabled)` | Enables/disables component |
| `component:Destroy()` | Removes component |
| `component:GetValue()` | Returns current value |

## 📖 Examples

### Settings Menu
```lua
local settingsWindow = interface:CreateWindow({
    Title = "Settings",
    Size = {450, 500}
})

local tabs = settingsWindow:CreateTabContainer()

-- Video Settings
local videoTab = tabs:AddTab("Video", "🎮")
videoTab:AddLabel("Graphics", {Font = Enum.Font.GothamBold, TextSize = 18})

videoTab:AddToggle({
    Text = "High Quality Graphics",
    Default = UserSettings().GameSettings.SavedQualityLevel == Enum.SavedQualitySetting.QualityLevel10,
    Callback = function(value)
        settings().Rendering.QualityLevel = value and 10 or 1
    end
})

videoTab:AddSlider({
    Text = "Render Distance",
    Min = 100,
    Max = 10000,
    Default = 5000,
    Callback = function(value)
        -- Set render distance
    end
})

-- Audio Settings
local audioTab = tabs:AddTab("Audio", "🔊")
audioTab:AddSlider({
    Text = "Master Volume",
    Min = 0,
    Max = 100,
    Default = 70,
    Callback = function(value)
        -- Set volume
    end
})
```

### Inventory System
```lua
local inventory = interface:CreateWindow({
    Title = "Inventory",
    Size = {600, 400}
})

-- Grid layout for items
local grid = inventory:CreateGridLayout({
    CellSize = {80, 80},
    CellPadding = {5, 5},
    MaxColumns = 6
})

for _, item in pairs(playerInventory) do
    local itemFrame = grid:AddCell()
    
    itemFrame:AddImage({
        Image = item.Icon,
        Size = {60, 60}
    })
    
    itemFrame:AddLabel({
        Text = item.Name,
        Position = {0, 60},
        Size = {80, 20}
    })
end
```

## 🤝 Contributing

We welcome contributions! Here's how to help:

1. **Fork** the repository
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit changes**: `git commit -m 'Add amazing feature'`
4. **Push to branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Development Setup
```bash
# Clone the repository
git clone https://github.com/skrxzoa/nexus-ui.git

# Navigate to project
cd nexus-ui

# Install testing dependencies
rojo serve
```

### Coding Standards
- Use descriptive variable names
- Include Luau type annotations
- Add comments for complex logic
- Follow existing code style
- Write tests for new features

## 📄 License

Nexus UI is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Credits

**Developed by:**
- **sk** - Core architecture, component system
- **rxzoa** - Design system, animations, theming

**Inspired by:**
- Microsoft Fluent Design System
- Linoria UI Library
- Roblox Studio UI patterns

**Special Thanks:**
- Contributors and testers
- Roblox developer community

---

## 🔗 Links

- [GitHub Repository](https://github.com/skrxzoa/nexus-ui)
- [Bug Reports](https://github.com/skrxzoa/nexus-ui/issues)
- [Discord Community](https://discord.gg/nexusui)
- [Roblox Group](https://www.roblox.com/groups/0000000000)

## 📞 Support

Having trouble? Check these resources:
1. Read the documentation carefully
2. Search existing issues
3. Join our Discord community
4. Create a new issue with reproduction steps

---

*Last updated: November 2023 | Version 1.0.0*

*Crafted with precision by sk and rxzoa. Built for Roblox developers who care about quality.*
