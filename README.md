

[![Minecraft](https://img.shields.io/badge/MINECRAFT-26.2%20%7C%201.21.X-44CC11?style=for-the-badge)](https://www.minecraft.net/)
[![Tested On](https://img.shields.io/badge/TESTED%20ON-PAPER%2026.2-007EC6?style=for-the-badge)](https://papermc.io/)
[![Java](https://img.shields.io/badge/JAVA-21%20%2F%2026%20%2B-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Economy](https://img.shields.io/badge/ECONOMY-VAULT%20API-EAB308?style=for-the-badge)](https://www.spigotmc.org/resources/vault.34315/)
[![License](https://img.shields.io/badge/LICENSE-NON--COMMERCIAL-E05D44?style=for-the-badge)](LICENSE)

</div>

# SellMulti

SellMulti is an advanced, high-performance economy plugin built for Minecraft 1.21+ servers running Paper or Purpur. It provides an end-to-end dynamic market economy, 9-category progression multipliers, drop-in auto-sell containers, a real-time Action Bar HUD, and an interactive Admin Price Editor GUI.

---

##

<img width="692" height="358" alt="image" src="https://github.com/user-attachments/assets/7a7356f4-ccae-41ab-bec9-f8a8af7729b0" />
<img width="688" height="293" alt="image" src="https://github.com/user-attachments/assets/6cb79035-6efd-4c5b-8ccb-49d24fa727ee" />
<img width="987" height="340" alt="image" src="https://github.com/user-attachments/assets/758e41c9-dfe9-423d-8de8-baef386e02b7" />
<img width="696" height="496" alt="image" src="https://github.com/user-attachments/assets/b4fe1715-cc11-4533-9bac-3a8db51fa473" />
<img width="699" height="309" alt="image" src="https://github.com/user-attachments/assets/10d6668c-c511-4b7c-8ce8-c619a5518a5f" />
<img width="986" height="217" alt="image" src="https://github.com/user-attachments/assets/9cc9977b-a473-4b68-b5f4-89278b31c969" />
<img width="802" height="501" alt="image" src="https://github.com/user-attachments/assets/2e5ecaa5-e130-4d97-a7fc-69a094b99676" />
<img width="1254" height="284" alt="image" src="https://github.com/user-attachments/assets/c134d01e-3bac-46c5-867e-b97a7e0c83b2" />



## Dependencies & Requirements

### Required Dependencies
1. **Server Platform**: Paper or Purpur **1.21.x** (Running on **Java 21** or newer)
2. **Vault**: Economy abstraction layer API ([Download Vault](https://www.spigotmc.org/resources/vault.34315/))
3. **Economy Provider**: Any Vault-compatible economy plugin, such as:
   - EssentialsX (Recommended)
   - CMI
   - Treasury
   - CoinsEngine

### Recommended Plugins
- **LuckPerms**: Permission management for player and administrative access.
- **PlaceholderAPI**: Placeholder expansion support for Scoreboards, TAB, and chat formatting.
- **DecentHolograms / FancyHolograms**: For displaying top seller leaderboards.

---

## Features

### 1. Drop-In Sell Container (/sell)
- Clean, 4-row (36 slots) virtual chest container.
- Drop items directly into the inventory.
- **ESC Auto-Sell**: Closing the container or pressing `ESC` automatically calculates payouts, credits player balance, updates multiplier EXP, and sends a single-line summary message.
- **Automatic Item Refund**: Unsellable items and protected containers are immediately returned to the player.

### 2. 9-Category Multiplier Progression (/sellmulti)
Categorizes over 1,300+ Minecraft 1.21 items into 9 distinct categories:
- **CROPS**: Agricultural harvests, seeds, fruits, and farming crops.
- **MINERALS**: Raw ores, ingots, gems, diamonds, and netherite materials.
- **MOB_DROPS**: Monster loot, boss drops, mob materials, and mob meats.
- **EQUIPMENT**: Weapons, armor, tools, bows, shields, and gear.
- **NATURAL**: Raw environmental blocks, dirt, stone, sand, logs, and leaves.
- **FISHING**: Fish species, nautilus shells, kelp, and aquatic catches.
- **ENCHANTED**: Enchanted books, golden apples, and enhanced consumable items.
- **ALCHEMY**: Potions, brewing ingredients, and chemical components.
- **MISC**: Decorative blocks, glass, wool, terracotta, and construction blocks.

- **Exponential Scaling Curve**: Progression requirement scales exponentially, particularly from `2.0x` to `3.0x` (ranging from billions up to 1.5 Trillion currency).
- **Hard Multiplier Ceiling**: Multiplier strictly caps at `3.0x (MAX LEVEL)`.

### 3. 30-Day Dynamic Market Cycles
- Every 30 days, the market engine automatically applies randomized market factors (between `0.8x` and `1.5x`) to all items.
- Staged prices configured by administrators via `/selladmin` automatically take effect during the next 30-day market reset cycle.

### 4. Real-Time Action Bar Live Price HUD
- Displays instant unit price, active category multiplier, and stack total payout above the hotbar when switching to or holding any sellable item:
  - Single item: `Sell: 1.5 [Currency] (1x)`
  - Stack (>1): `Sell: 1.5 [Currency] (1x) | Total: +96 [Currency]`
- **100% Vanilla NBT Purity**: Does not alter physical item lore, ensuring flawless block stacking, crafting recipes, and hopper sorting compatibility.

### 5. Interactive Admin Price Editor GUI (/selladmin)
- Overview menu displaying all 9 categories with total registered items.
- Paginated category editor sorted by staged price descending.
- **Configured Item Highlighting**: Configured items display in bold green with `(Configured)` status.
- **Search System**: Built-in search dialog to filter items by keyword, with right-click to clear filter.
- **Administrative Action Controls**: Dedicated buttons to reset all staged prices across all categories to 1.0 currency or apply staged prices and reroll market factors immediately.

### 6. Security & Anti-Exploit Invariants
- **Atomic Session Locks**: Prevents race conditions, double-processing, and packet spam exploits during batch transactions.
- **Shulker Box & Bundle Protection**: Strictly prohibits selling Shulker Boxes and Bundles, preventing accidental loss of container contents.
- **Named & Enchanted Item Safety**: The `/sell all` command automatically excludes custom-named items and enchanted gear.
- **Numeric Overflow Guard**: Rejects non-positive prices and caps values at 1 Trillion to prevent 64-bit integer and double memory overflow.

---

## Commands & Permissions

| Command | Permission | Description |
|---|---|---|
| `/sell` | `sell.use` | Open 4-row drop-in sell container (Auto-sells on close) |
| `/sell hand` | `sell.use` | Sell item currently held in main hand |
| `/sell all` | `sell.use` | Sell all valid items in inventory (Protects shulkers and enchanted gear) |
| `/sellmulti` | `sell.use` | Open Multiplier Overview GUI and Category Price Lists |
| `/selladmin` | `sell.admin` | Open Interactive Admin Price Editor GUI |
| `/selladmin reroll` | `sell.admin` | Apply staged prices and reroll 30-day market factors immediately |
| `/selladmin reload` | `sell.admin` | Reload configuration files and item catalog |
| `/selladmin reset` | `sell.admin` | Reset all staged prices across all categories to 1.0 currency |
| `/selladmin setmulti <player> <category> <multiplier>` | `sell.admin` | Set specific player multiplier for a category |
| `/selladmin resetplayer <player>` | `sell.admin` | Reset all multipliers and EXP for a specific player |

---

## Configuration (config.yml)

```yaml
# Prefix and Currency Symbol
prefix: "&8[&6✦ &e&lSell&8]&r "
currency_symbol: "⛃"

# Market Reroll Interval in Seconds (2592000 = 30 Days)
market_reroll_interval: 2592000

# Action Bar HUD Display
hud:
  enabled: true

# Multiplier Progression Settings
multiplier:
  max: 3.0
  increment: 0.1
  levels:
    1: 1000000          # 1.0M  -> 1.1x
    2: 3000000          # 3.0M  -> 1.2x
    3: 8000000          # 8.0M  -> 1.3x
    4: 20000000         # 20M   -> 1.4x
    5: 50000000         # 50M   -> 1.5x
    6: 100000000        # 100M  -> 1.6x
    7: 200000000        # 200M  -> 1.7x
    8: 350000000        # 350M  -> 1.8x
    9: 550000000        # 550M  -> 1.9x
    10: 800000000       # 800M  -> 2.0x
    11: 2500000000      # 2.5B  -> 2.1x
    12: 6000000000      # 6.0B  -> 2.2x
    13: 15000000000     # 15B   -> 2.3x
    14: 35000000000     # 35B   -> 2.4x
    15: 75000000000     # 75B   -> 2.5x
    16: 150000000000    # 150B  -> 2.6x
    17: 280000000000    # 280B  -> 2.7x
    18: 500000000000    # 500B  -> 2.8x
    19: 850000000000    # 850B  -> 2.9x
    20: 1500000000000   # 1.5T  -> 3.0x (MAX LEVEL)
```

---

## Building from Source

### Prerequisites
- **Java Development Kit (JDK) 21** or newer
- **Apache Maven 3.8+**

```bash
# 1. Clone the repository
git clone https://github.com/egade369/sellmulti.git

# 2. Navigate into project directory
cd sellmulti

# 3. Build the JAR file
mvn clean package
```

The compiled JAR file will be generated at `target/sellmulti-1.0.0.jar`.

---

## Author & License

- **Author**: **egade369**
- **Repository**: [https://github.com/egade369/sellmulti](https://github.com/egade369/sellmulti)
- **License**: Custom Non-Commercial License (Free for private server use. Commercial resale or paid redistribution is strictly prohibited. See [LICENSE](LICENSE) for details.)
