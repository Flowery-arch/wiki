---
icon: desktop
---

# Конфигурации сервера

Наш сервер работает на мощном оборудовании, чтобы обеспечить стабильную производительность даже при большом количестве игроков (за сезон нас посетило более 3500 человек!).

* **Процессор**: AMD R9 7950X3D.
* **Оперативная память**: 32 ГБ.
* **Хранилище**: 500 Гб NVMe SSD от Samsung.
* **Операционная система**: Debian 11.
* **Местоположение**: Германия

***

**Ядро сервера**\
Используем Purpur. Настройки ниже применяются ко всем мирам, если не переопределены отдельно в `world*/paper-world.yml`.

**Ограничения по мобам**\
Используются **per‑player mob caps** (на игрока), а не лимиты по чанкам.\
Если строите фермы — следите, чтобы не копить большие стаки мобов в одном чанке.

**Жители и lobotomize**\
Встроенный `lobotomize` в Purpur **выключен**, чтобы жители нормально паниковали от зомби и работали голем‑фермы.\
Для торговых залов используем плагин **VillagerLobotimizer**: он лоботомизирует “зажатых” жителей, но торговля работает.

***

**bukkit.yml**

```yaml
spawn-limits:
  monsters: 20
  animals: 5
  water-animals: 2
  water-ambient: 2
  water-underground-creature: 3
  axolotls: 3
  ambient: 1
ticks-per:
  animal-spawns: 400
  monster-spawns: 10
  water-spawns: 100
  water-ambient-spawns: 400
  water-underground-creature-spawns: 400
  axolotl-spawns: 400
  ambient-spawns: 400
```

**spigot.yml**

```yaml
world-settings:
  default:
    hanging-tick-frequency: 1200
    arrow-despawn-rate: 300
    trident-despawn-rate: 1200
    mob-spawn-range: 3
    entity-activation-range:
      animals: 24
      monsters: 24
      raiders: 48
      misc: 8
      water: 8
      villagers: 32
      flying-monsters: 48
      wake-up-inactive:
        animals-max-per-tick: 2
        animals-every: 4000
        animals-for: 40
        monsters-max-per-tick: 4
        monsters-every: 400
        monsters-for: 60
        villagers-max-per-tick: 4
        villagers-every: 600
        villagers-for: 100
        flying-monsters-max-per-tick: 2
        flying-monsters-every: 200
        flying-monsters-for: 60
      villagers-work-immunity-after: 100
      villagers-work-immunity-for: 20
      villagers-active-for-panic: true
      tick-inactive-villagers: true
    entity-tracking-range:
      players: 128
      animals: 48
      monsters: 48
      misc: 32
      display: 64
      other: 64
```

**paper-global.yml**

```yaml
item-validation:
  book-size:
    page-max: 1280
unsupported-settings:
  allow-headless-pistons: true
  allow-permanent-block-break-exploits: true
  allow-piston-duplication: true
  perform-username-validation: true
```

**paper-world-defaults.yml**

```yaml
chunks:
  auto-save-interval: 6000
  delay-chunk-unloads-by: 10s
  entity-per-chunk-save-limit:
    area_effect_cloud: 8
    arrow: 16
    dragon_fireball: 3
    egg: 8
    ender_pearl: 8
    experience_bottle: 3
    experience_orb: 16
    eye_of_ender: 8
    fireball: 8
    firework_rocket: 8
    llama_spit: 3
    potion: 8
    shulker_bullet: 8
    small_fireball: 8
    snowball: 8
    spectral_arrow: 16
    trident: 16
    wither_skull: 4
  max-auto-save-chunks-per-tick: 8
  prevent-moving-into-unloaded-chunks: true
collisions:
  max-entity-collisions: 4
entities:
  behavior:
    pillager-patrols:
      disable: true
  spawning:
    creative-arrow-despawn-rate: 400
    despawn-ranges:
      ambient: { hard: 54, soft: 32 }
      axolotls: { hard: 54, soft: 32 }
      creature: { hard: 54, soft: 32 }
      misc: { hard: 54, soft: 32 }
      monster: { hard: 54, soft: 32 }
      underground_water_creature: { hard: 54, soft: 32 }
      water_ambient: { hard: 54, soft: 32 }
      water_creature: { hard: 54, soft: 32 }
    duplicate-uuid:
      mode: SAFE_REGEN
      safe-regen-delete-range: 32
    iron-golems-can-spawn-in-air: false
    non-player-arrow-despawn-rate: 400
    per-player-mob-spawns: true
  spawning:
    alt-item-despawn-rate:
      enabled: true
      items:
        andesite: 1200
        cobbled_deepslate: 1200
        cobblestone: 1200
        diorite: 1200
        dirt: 1200
        granite: 1200
        gravel: 1200
        netherrack: 1200
        egg: 600
        feather: 600
        wheat_seeds: 600
        pumpkin_seeds: 600
        melon_seeds: 600
        beetroot_seeds: 600
fixes:
  disable-unloaded-chunk-enderpearl-exploit: true
  fix-curing-zombie-villager-discount-exploit: true
hopper:
  cooldown-when-full: true
misc:
  redstone-implementation: ALTERNATE_CURRENT
  update-pathfinding-on-block-update: false
spawn:
  keep-spawn-loaded: false
tick-rates:
  behavior:
    villager:
      validatenearbypoi: -1
  container-update: 1
  grass-spread: 4
  mob-spawner: 2
  sensor:
    villager:
      secondarypoisensor: 40
unsupported-settings:
  fix-invulnerable-end-crystal-exploit: true
```

**world\_nether/paper-world.yml (только АД)**

```yaml
spawning:
  alt-item-despawn-rate:
    enabled: true
    items:
      golden_sword: 600
      rotten_flesh: 600
```

***

**Механика спавна и деспавна мобов**\
Мы используем ванильную механику спавна мобов с одним изменением: **Hard Despawn уменьшен с 128 до 54 блоков**. Это снижает нагрузку и улучшает стабильность.

Как работает спавн мобов:

* Красная зона `24–54` блока: зона появления мобов.
* Зеленая зона `до 24` блоков: мобы не появляются.
* Цилиндр `до 32` блоков: мобы активны и взаимодействуют с миром.
* `32–54` блока: мобы тикают медленнее.
* Дальше `54`: мобы исчезают.

**Почему фермы из старых версий работают медленнее?**\
После 1.19 высота мира изменилась (с `Y0–Y265` на `Y-64–Y320`). Игра проверяет больше блоков для спавна, поэтому старые фермы дают меньше мобов.

Решения:

* Стройте фермы на `Y-64`.
* Очищайте периметр `Y-64` → `Y0`.
* Учитывайте, что на серверах с `per-player-mob-spawns` эффективность ниже.

Рекомендации:

* Большой периметр вокруг фермы.
* Эндермен‑фермы — только `Y-64`.
* Фермы в Нижнем мире — под крышей, чтобы не было лишнего спавна вне платформы.

***

Если хочешь, могу сделать второй вариант — более короткий, без механики спавна и сжатый до 1 страницы.

<figure><img src="https://docs.vanillasquad.com/~gitbook/image?url=https%3A%2F%2F1639357051-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-Md61sIy9355-Dt4QFTm%252Fuploads%252FKQCsirha2UkoCDfR4dLN%252Fimage.png%3Falt%3Dmedia%26token%3Df631d4b6-a2be-4dc9-af7a-3694c6a966a8&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=f8edb0e5&#x26;sv=2" alt=""><figcaption></figcaption></figure>

**Почему фермы из старых версий работают медленнее?**

После обновления до версии 1.19 высота мира изменилась (с Y0–Y265 на Y-64–Y320). Это повлияло на спавн мобов, так как игра теперь проверяет больше блоков для спавна. Фермы, построенные на высоте Y0, стали менее эффективными из-за дополнительных 64 блоков ниже.

**Решения проблемы:**

1. **Перестройте ферму** на высоте Y-64 (самый низкий уровень мира).
2. **Очистите периметр** от Y-64 до Y0, оставив только воздух.
3. Примите, что спавн мобов на многопользовательских серверах менее эффективен из-за механики **per-player-mob-spawns**.

**Рекомендации для ферм:**

* **Большой периметр**: очищайте все возможные места спавна вокруг фермы.
* **Фермы эндерменов**: стройте на Y-64 для максимальной эффективности.
* **Фермы в Нижнем мире**: располагайте под крышей Нижнего мира, чтобы минимизировать спавн мобов вне платформы.
