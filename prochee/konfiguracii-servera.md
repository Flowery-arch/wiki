---
description: Конфигурация сервера
icon: desktop
---

# Конфигурации сервера

**Конфигурация сервера**

Наш сервер работает на производительном оборудовании, чтобы обеспечивать стабильную работу даже при высоком онлайне.

**Процессор:** AMD Ryzen 9 9950x3D

**Оперативная память:** 64 ГБ.

**Хранилище:** 2 x 476.9 ГБ NVMe SSD от Samsung&#x20;

**Операционная система:** Ubuntu 22.04.5 LTS.

**Ядро Linux:** 5.15.0-164-generic.

**Ядро сервера**

Мы используем **Purpur**. Это даёт хорошую производительность, совместимость с плагинами и гибкую настройку поведения сервера.&#x20;

bukkit.yml

```yml
spawn-limits:
  monsters: 35
  animals: 8
  water-animals: 15
  water-ambient: 5
  water-underground-creature: 5
  axolotls: 5
  ambient: 15
ticks-per:
  monster-spawns: 6
  animal-spawns: 400
  water-spawns: 12
  water-ambient-spawns: 12
  water-underground-creature-spawns: 12
  axolotl-spawns: 12
  ambient-spawns: 12
```

Ограничения по мобам Используются `per-player mob spawns`, то есть спавн масштабируется на игрока, а не только на мир целиком. Это даёт более честное распределение мобов между игроками, но при большом онлайне эффективность отдельных ферм может отличаться от “одиночной” ванили.

spigot.yml

```yml
world-settings:
  default:
    hanging-tick-frequency: 1200
    arrow-despawn-rate: 1200
    trident-despawn-rate: 1200
    mob-spawn-range: 3
    entity-activation-range:
      animals: 32
      monsters: 32
      raiders: 12
      misc: 16
      water: 16
      villagers: 32
      flying-monsters: 32
      wake-up-inactive:
        animals-max-per-tick: 4
        animals-every: 1200
        animals-for: 100
        monsters-max-per-tick: 8
        monsters-every: 400
        monsters-for: 100
        villagers-max-per-tick: 4
        villagers-every: 600
        villagers-for: 100
        flying-monsters-max-per-tick: 8
        flying-monsters-every: 200
        flying-monsters-for: 100
      villagers-work-immunity-after: 100
      villagers-work-immunity-for: 20
      villagers-active-for-panic: true
      tick-inactive-villagers: true
    entity-tracking-range:
      players: 48
      animals: 48
      monsters: 48
      misc: 32
      display: 128
      other: 64
    ticks-per:
      hopper-transfer: 8
      hopper-check: 1
    hopper-amount: 1
    hopper-can-load-chunks: false
```

paper-global.yml

```yml
chunk-loading-basic:
  player-max-chunk-load-rate: 100.0
  player-max-chunk-send-rate: 75.0
chunk-system:
  io-threads: -1
  worker-threads: -1
item-validation:
  book-size:
    page-max: 2560
proxies:
  proxy-protocol: true
unsupported-settings:
  allow-headless-pistons: true
  allow-permanent-block-break-exploits: true
  allow-piston-duplication: true
  perform-username-validation: true
```

paper-world-defaults.yml

```yml
entities:
  spawning:
    alt-item-despawn-rate:
      enabled: true
      items:
        andesite: 600
        beetroot_seeds: 600
        black_wool: 600
        blue_wool: 600
        bone: 600
        brown_wool: 600
        carrot: 600
        cobbled_deepslate: 600
        cobblestone: 600
        cyan_wool: 600
        diorite: 600
        dirt: 600
        egg: 600
        feather: 600
        golden_sword: 600
        granite: 600
        gravel: 600
        gray_wool: 600
        green_wool: 600
        gunpowder: 600
        ink_sac: 600
        leather: 600
        light_blue_wool: 600
        light_gray_wool: 600
        lime_wool: 600
        magenta_wool: 600
        melon_seeds: 600
        nether_wart: 600
        netherrack: 600
        orange_wool: 600
        pink_wool: 600
        potato: 600
        pumpkin_seeds: 600
        purple_wool: 600
        red_wool: 600
        rotten_flesh: 600
        spider_eye: 600
        string: 600
        wheat_seeds: 600
        white_wool: 600
        yellow_wool: 600
    despawn-range-shape: ELLIPSOID
    despawn-ranges:
      ambient:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
      axolotls:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
      creature:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
      misc:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
      monster:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
      underground_water_creature:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
      water_ambient:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
      water_creature:
        hard:
          horizontal: 56
          vertical: 128
        soft: 32
    per-player-mob-spawns: true
    duplicate-uuid:
      mode: SAFE_REGEN
      safe-regen-delete-range: 32
    iron-golems-can-spawn-in-air: false
hopper:
  cooldown-when-full: true
tick-rates:
  behavior:
    villager:
      acquirepoi: 120
      validatenearbypoi: 60
  container-update: 1
  dry-farmland: 1
  grass-spread: 8
  mob-spawner: 4
  sensor:
    villager:
      nearestbedsensor: 80
      nearestlivingentitysensor: 40
      playersensor: 40
      secondarypoisensor: 80
      villagerbabiessensor: 40
  wet-farmland: 1
misc:
  redstone-implementation: VANILLA
  update-pathfinding-on-block-update: true
```

Дополнительно для Нижнего мира:

```yml
entities:
  spawning:
    alt-item-despawn-rate:
      enabled: true
      items:
        golden_sword: 600
        rotten_flesh: 600
        netherrack: 600
```

Механика спавна и деспавна мобов Сервер использует ванильную механику спавна с изменённым hard despawn. Основные значения сейчас такие:

* в радиусе до 24 блоков мобы не спавнятся;
* с 24 блоков начинается зона возможного спавна;
* soft despawn начинается после 32 блоков;
* hard despawn настроен как `56 блоков по горизонтали` и `128 по вертикали`;
* форма деспавна: `ELLIPSOID`.

Что это значит на практике:

* мобы рядом с игроком работают почти как обычно;
* далеко стоящие мобы очищаются быстрее, чем в стандартной ванили;
* это уменьшает нагрузку при большом онлайне и большом количестве одновременно загруженных территорий.

Почему фермы из старых версий могут работать хуже Начиная с новых версий Minecraft, мир стал выше и глубже, поэтому движок проверяет больше позиций для спавна. Из-за этого старые фермы, особенно построенные высоко или без зачистки окружающих спавн-площадок, работают хуже, чем раньше.

Рекомендации по фермам:

* стройте фермы как можно ниже, если механика фермы это позволяет;
* очищайте доступные точки спавна вокруг;
* учитывайте, что при `per-player-mob-spawns: true` эффективность зависит от количества игроков рядом и от общего онлайна;
* фермы в Незере лучше располагать под крышей мира;
* эндермен-фермы и другие вертикально чувствительные фермы лучше проектировать с учётом новой высоты мира.
