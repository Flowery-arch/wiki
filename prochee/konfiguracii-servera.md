---
icon: desktop
---

# Конфигурации сервера

### ▌Конфигурация выделенного сервера <a href="#konfiguraciya-vydelennogo-servera" id="konfiguraciya-vydelennogo-servera"></a>

> **CPU** _(Процессор)_: Ryzen 7 1700X\
> **RAM** _(Оперативная память)_: 64gb DDR4 \
> **SSD** _(Накопитель)_: 1000 NVMe \
> **Сеть:** 1000 Мбит/сек \
> **Стоимость:** 6.600₽/мес \
> **Местоположение:** Германия\
> **ОС:** Ubuntu 22.04.1 LTS

### ▌Ядро наших сервера  <a href="#yadro-nashikh-serverov-zw6-zwpremium-i-ostalnykh" id="yadro-nashikh-serverov-zw6-zwpremium-i-ostalnykh"></a>

> На наших всех серверах стоит ядро [Paper](https://papermc.io/) 1.21.11

### ▌Ограничения мобов <a href="#ogranicheniya-mobov" id="ogranicheniya-mobov"></a>

| Сущность                           | Кол-во на чанк |
| ---------------------------------- | -------------- |
| Житель                             | 5 штук         |
| Лодки, вагонетки, стойки для брони | 8 штук         |
| Прочие сущности                    | 10 штук        |

{% hint style="info" %}
Мы обращаем внимание на ограничения, если в зоне прогрузки находится более 150 сущностей, поэтому не превышайте это количество. При этом сложные фермы (с множеством механизмов) могут уменьшить этот порог в некоторых случаях.
{% endhint %}

### ▌spigot.yml <a href="#spigot.yml" id="spigot.yml"></a>

```
world-settings:
  default:
    mob-spawn-range: 8 # Радиус в чанках от игрока, где будут спавнится мобы
    entity-activation-range: # Радиус в котором ентити будут активничать
      animals: 32
      monsters: 32
      raiders: 64
      misc: 16
      water: 16
      villagers: 32
      flying-monsters: 32
```
