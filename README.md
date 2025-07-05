# Clicker Guardians – Game Design Document
V0.1

---

## Table des matières

1. [Présentation générale](#1-présentation-générale)
2. [Gameplay de base](#2-gameplay-de-base)
   2.1 [Dégâts de clic](#21-dégâts-de-clic-cd)
   2.2 [DPS passif](#22-dps-passif)
   2.3 [Combo & auto-clics](#23-combo--auto-clics)
3. [Monnaies](#3-monnaies)
4. [Boosts temporaires](#4-boosts-temporaires)
5. [Progression](#5-progression)
   5.1 [Rangs](#51-rangs)
   5.2 [Prestige](#52-prestige)
6. [Gardiens](#6-gardiens)
   6.1 [Déblocage & slots](#61-déblocage--slots)
   6.2 [Capacités](#62-capacités)
7. [Système de combat](#7-système-de-combat)
   7.1 [Vagues & Boss](#71-vagues--boss)
   7.2 [Méga-Boss](#72-méga-boss)
8. [Équipement joueur](#8-équipement-joueur)
   8.1 [Épées](#81-épées)
   8.2 [Armures](#82-armures)
9. [Compétences](#9-compétences)
10. [Quêtes](#10-quêtes)

---

## 1. Présentation générale

Clicker Guardians est un *idle‑RPG clicker* où le joueur progresse en éliminant des vagues d’ennemis, recrute des gardiens et réinitialise régulièrement sa partie (« Prestige ») pour obtenir des bonus permanents.

---

## 2. Gameplay de base

### 2.1 Dégâts de clic (CD)

`CD = BaseClick × (1 + ΣSwordDMG) × (1 + ComboMult) × PotionMult × PrestigeMult`

| Variable         | Description                                                                |
| ---------------- | -------------------------------------------------------------------------- |
| **BaseClick**    | 1 au départ                                                                |
| **ΣSwordDMG**    | Somme des multiplicateurs de toutes les épées équipées (joueur + gardiens) |
| **ComboMult**    | Bonus issu du combo (voir 2.3)                                             |
| **PotionMult**   | Boost actif (x2 DMG, etc.)                                                 |
| **PrestigeMult** | `1 + 0,02 × PrestigePoints` — voir 5.2                                     |

### 2.2 DPS passif

`PassiveDPS = GuardianBaseDPS × GuardianUpgradeMult × GuardianSwordMult × PotionMult × PrestigeMult`

Tous les multiplicateurs sont appliqués de façon **multiplicative**. `GuardianSwordMult` combine les bonus d’épées propres aux gardiens.

### 2.3 Combo & auto‑clics

*Fenêtre de combo :* **2 s**

| Type          | Stacks max | Bonus / stack |   Auto‑click | Remarques                 |
| ------------- | ---------: | ------------: | -----------: | ------------------------- |
| **Gratuit**   |        250 |       +0,25 % | 1,5 s / clic | Reste dans la fenêtre     |
| **Game Pass** |        500 |        +0,5 % | 0,5 s / clic | Empile le combo plus vite |

*Max bonus DMG :* 62,5 % (gratuit) / 250 % (Game Pass) – valeurs à équilibrer.

---

## 3. Monnaies

| Monnaie              | Source principale                                                      | Utilisation                                   |
| -------------------- | ---------------------------------------------------------------------- | --------------------------------------------- |
| **Gold**             | Tous les monstres                                                      | Achat & amélioration de gardiens / équipement |
| **Gemmes**           | Donjon « Gem Dungeon » (10 waves) — clé : 0,2 % Boss / 0,5 % Méga‑Boss | Contenu premium (slots, épées supérieures)    |
| **Potion Fragments** | « Potion Raid » (structure identique)                                  | Craft des potions                             |

`GoldDrop = MobGoldValue × GoldMult × PrestigeMult × GamePassMult`

`GoldMult` peut être amélioré via les compétences (*cf.* section 9).

---

## 4. Boosts temporaires

| Objet              | Effet                                | Durée  | Obtention                                          |
| ------------------ | ------------------------------------ | ------ | -------------------------------------------------- |
| Potion **×2 DMG**  | ×2 CD & DPS                          | 5 min  | Craft (Fragments) ou Shop                          |
| Potion **×2 Gold** | ×2 Gold                              | 5 min  | Craft / Shop                                       |
| **Server Boost**   | ×1,5 (effet potion) *serveur entier* | 20 min | 150 Robux — un seul actif, file d’attente possible |
| **Global Boost**   | ×2 (potion) *tous serveurs*          | 1 h    | 999 Robux — exclusivité globale                    |

---

## 5. Progression

### 5.1 Rangs

* Déblocage : +1 rang tous les **100 waves**, puis **+50 waves** supplémentaires par rang
* Bonus : **+10 %** DMG & DPS (multiplicatif) par rang
* Coût : `RankCost = 1 000 000 × 10^(Rank − 1)`
* 1 Skill Point / rang

### 5.2 Prestige

* Déverrouillé à la **wave 2500**
* **Reset** : niveaux, or, gardiens, progression carte
* **Conserve** : équipement, achats Robux / Game Pass, Skill Points non dépensés
* **Prestige Points (PP)** : 1 PP / 100 waves au‑delà de 2500 → **+2 %** DMG & DPS / PP (multiplicatif)

---

## 6. Gardiens

### 6.1 Déblocage & slots

* Slots achetés : d’abord Gold, puis Gemmes
* Recrutement via **jetons** (drop Boss / Méga‑Boss)

| Slot   | Niveau | Coût          |
| ------ | -----: | ------------- |
| Épée   |     50 | X gemmes      |
| Armure |    150 | 4 × coût épée |
| Passif |    500 | Gold + Gemmes |

### 6.2 Capacités

Talents déverrouillés aux **niveaux 25, 50, 100, 250**, etc.

---

## 7. Système de combat

### 7.1 Vagues & Boss

* **Wave** : 10 mobs — *45 s*
* **Boss** : toutes les **5 waves** — *60 s*, HP = 5 × HP wave
* Échec ⇒ retour à la wave précédente

### 7.2 Méga‑Boss

* Tous les **10 Boss** (wave 50, 100, 150, …)
* Timer : **5 min** — HP ≈ **20 ×** Boss normal
* AoE continu sur gardiens
* **Récompenses** : 5 × Gold Boss • 3 fragments garantis • \~20 % jeton gardien

---

## 8. Équipement joueur

### 8.1 Épées

* Rareté : Commun → Mythique
* Formule : `SwordDMG = BaseDamage × TierMult × (1 + 0,1 × UpgradeLvl)`
* Upgrades max : +10 (ou +20)

### 8.2 Armures

* Défense % + bonus DPS passif possible
* Même système d’upgrade que les épées

---

## 9. Compétences

* **3 arbres** : Attaque • Utilitaire • Économie
* 1 Skill Point / rang +1 / Prestige
* Respec gratuit au Prestige ou payant (Robux)

---

## 10. Quêtes

| Type                  | Fréquence | Exemple                         | Récompense               |
| --------------------- | --------- | ------------------------------- | ------------------------ |
| **Quotidiennes**      | 24 h      | Tuer 500 mobs, 5 Boss…          | Gold, Fragments, Potions |
| **Hebdomadaires**     | 7 j       | Chaîne : 5 Méga‑Boss, 50 waves… | Monnaie hebdo            |
| **Guide progression** | Unique    | Wave 10, premier gardien, etc.  | Boost ponctuel           |

---

