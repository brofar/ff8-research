# c0m000.dat-c0m199.dat monster AI as pseudocode (section 8)

**Variable names.** Each monster's local variables (raw `varA`..`varI`, ids 220-228 in `ENEMY_AI_SCRIPTS.md`) are renamed, with a key under each heading. 
*named* = picked by reading that monster's script). It's not something the code proves, just an interpretation.  
*auto* = a generic name from the usage pattern (`defeated`, `turn_counter`, `hit_counter`, `once_turn`, `phase`, ...; rules in `auto_var_names`). 
Unknown variables are in the format `varX`.


## 1: GIM52A

Variables: `hit_counter` = varA (named), `unused` = varB (named)


### Init

```
hit_counter = 0
unused = 0
return
```

### Turn

```
if (status(self) has Aura) {
    Strength multiplier = 200%
    Magic multiplier = 200%
} else {
    Strength multiplier = 100%
    Magic multiplier = 100%
}
if (random(0..2) == 0) {
    return
}
if (alive(entity 88)) {
    hit_counter = 1
} else {
    if (hit_counter == 1) {
        hit_counter = 0
        if (random(0..2) == 0) {
            target all enemies
            use Ray Bomb
            return
        } else {
            target random enemy
            use one of Physical attack, Micro Missiles, Thundara/Thundaga
            return
        }
    }
}
if (hit_counter >= 5) {
    hit_counter = 1
    target all enemies
    use Ray Bomb
    return
}
target random enemy
use one of Physical attack, Physical attack, Micro Missiles
return
```

### Counter

```
if (group_level(enemy team) >= 1) {
    hit_counter += 1
}
return
```

## 2: Blobra

Variables: `phase` = varA (auto)


### Init

```
if (combat_scene == 76 /*Blobra+Blood Soul*/) {
    elemDmgMod 006400
    phase = 0
    return
} else {
    if (combat_scene == 77 /*Blobra*/) {
        elemDmgMod 006400
        phase = 0
        return
    }
}
if (group_level(enemy team) == 0) {
    if (random(0..2) == 0) {
        elemDmgMod 006400
        phase = 0
    } else {
        if (random(0..1) == 0) {
            elemDmgMod 016400
            phase = 1
        } else {
            elemDmgMod 026400
            phase = 2
        }
    }
} else {
    if (group_level(enemy team) == 1) {
        if (random(0..5) == 0) {
            elemDmgMod 006400
            phase = 0
        } else {
            if (random(0..4) == 0) {
                elemDmgMod 016400
                phase = 1
            } else {
                if (random(0..3) == 0) {
                    elemDmgMod 026400
                    phase = 2
                } else {
                    if (random(0..2) == 0) {
                        elemDmgMod 036400
                        phase = 3
                    } else {
                        if (random(0..1) == 0) {
                            elemDmgMod 046400
                            phase = 4
                        } else {
                            elemDmgMod 056400
                            phase = 5
                        }
                    }
                }
            }
        }
    } else {
        if (random(0..8) == 0) {
            elemDmgMod 006400
            phase = 0
        } else {
            if (random(0..7) == 0) {
                elemDmgMod 016400
                phase = 1
            } else {
                if (random(0..6) == 0) {
                    elemDmgMod 026400
                    phase = 2
                } else {
                    if (random(0..5) == 0) {
                        elemDmgMod 036400
                        phase = 3
                    } else {
                        if (random(0..4) == 0) {
                            elemDmgMod 046400
                            phase = 4
                        } else {
                            if (random(0..3) == 0) {
                                elemDmgMod 056400
                                phase = 5
                            } else {
                                if (random(0..2) == 0) {
                                    elemDmgMod 066400
                                    phase = 6
                                } else {
                                    if (random(0..1) == 0) {
                                        elemDmgMod 076400
                                        phase = 7
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
return
```

### Turn

```
if (random(0..2) == 0) {
    return
} else {
    if (status(self) has Confuse) {
        target random enemy
        use one of Esuna, Cure/Cura/Curaga, Slow/Stop
        return
    }
    target random enemy
    use one of Physical attack, Physical attack, Physical attack/Sticky Icky
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
} else {
    if (status(self) has Berserk) {
        return
    }
}
if (random(0..2) != 0) {
    return
}
if (last_command == Magic) {
    if (phase == 0) {
        if (last_element == Fire) {
            if (random(0..1) == 0) {
                target last attacker
                use one of Silence, Silence, Berserk
            }
        }
    } else {
        if (phase == 1) {
            if (last_element == Ice) {
                if (random(0..1) == 0) {
                    target last attacker
                    use one of Silence, Silence, Berserk
                }
            }
        } else {
            if (phase == 2) {
                if (last_element == Thunder) {
                    if (random(0..1) == 0) {
                        target last attacker
                        use one of Silence, Silence, Berserk
                    }
                }
            } else {
                if (phase == 3) {
                    if (last_element == Earth) {
                        if (random(0..1) == 0) {
                            target last attacker
                            use one of Silence, Silence, Berserk
                        }
                    }
                } else {
                    if (phase == 4) {
                        if (last_element == Poison) {
                            if (random(0..1) == 0) {
                                target last attacker
                                use one of Silence, Silence, Berserk
                            }
                        }
                    } else {
                        if (phase == 5) {
                            if (last_element == Wind) {
                                if (random(0..1) == 0) {
                                    target last attacker
                                    use one of Silence, Silence, Berserk
                                }
                            }
                        } else {
                            if (phase == 6) {
                                if (last_element == Water) {
                                    if (random(0..1) == 0) {
                                        target last attacker
                                        use one of Silence, Silence, Berserk
                                    }
                                }
                            } else {
                                if (phase == 7) {
                                    if (last_element == Holy) {
                                        if (random(0..1) == 0) {
                                            target last attacker
                                            use one of Silence, Silence, Berserk
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
return
```

## 3: Thrustaevis


### Init

```
if (group_level(enemy team) == 1) {
    elemDmgMod 058403
} else {
    if (group_level(enemy team) == 2) {
        elemDmgMod 05e803
    }
}
if (save.tutorial_irvine_shot_seen == 0) {
    if (battle.tutorial_shown_this_battle == 0) {
        if (alive(entity 2)) {
            battle.tutorial_shown_this_battle = 1
            save.tutorial_irvine_shot_seen = 1
            print+lock '{Irvine} “Oh, I forgot to tell you...”'
            print+lock '“For my Limit Break, Shot,”'
            print+lock '“pull the trigger with the {R1}.”'
            print+lock '“Got it?”'
            waitText 04
        }
    }
}
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use null (Thrustaevis Attack)
    return
}
if (HP%(self) < 30) {
    if (random(0..2) == 1) {
        target all enemies
        use Wind Blast
    } else {
        target random enemy
        use one of null (Thrustaevis Attack), Physical attack, Physical attack
    }
} else {
    target random enemy
    use one of null (Thrustaevis Attack), null (Thrustaevis Attack), Physical attack
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (random(0..2) == 0) {
    if (last_command == Draw) {
        target last attacker
        use Physical attack
    }
}
return
```

## 4: Geezard


### Turn

```
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (random(0..2) == 0) {
    if (random(0..2) != 0) {
        target random enemy
        use Fire/Fira
    } else {
        target all enemies
        use Bad Breath
    }
} else {
    if (random(0..2) == 0) {
        return
    } else {
        target random enemy
        use one of Physical attack, Physical attack, null
    }
}
return
```

## 5: Belhelmel


### Init

```
varA = 1
set_scan_text '(no text 255)'
set_scan_text "It's laughing!"
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (varA == 0) {
    target random enemy
    use Physical attack
} else {
    target random enemy
    use one of Thunder/Thundara/Thundaga, Thunder/Thundara/Thundaga, Sleep/Confuse/Berserk
}
return
```

### Counter

```
if (random(0..2) != 0) {
    return
}
if (status(self) has Confuse) {
    return
}
if (varA == 0) {
    if (last_damage == physical) {
        target last attacker
        use Counter Slice
    } else {
        varA = 1
        set_scan_text "It's laughing!"
        target self
        use null
        print 'Belhelmel laughed!'
    }
} else {
    if (last_damage == magical) {
        target last attacker
        use Counter Laser Eye
    } else {
        varA = 0
        set_scan_text "It's scowling!"
        target self
        use null
        print 'Belhelmel is furious!'
    }
}
return
```

## 6: Glacial Eye

Variables: `magic_hit_pending` = varA (named), `silence_target` = varB (named)


### Init

```
magic_hit_pending = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (HP%(self) <= 100) {
    if (random(0..2) != 0) {
        target random enemy
        use Vampire
        return
    }
}
if (magic_hit_pending == 1) {
    if (random(0..2) != 0) {
        if (status(self) lacks Reflect) {
            magic_hit_pending = 0
            target self
            use Physical attack/Reflect
            return
        }
    }
}
if (magic_hit_pending == 1) {
    if (random(0..2) != 0) {
        magic_hit_pending = 0
        target silence_target
        use Physical attack/Silence
        return
    }
}
target random enemy
use one of Physical attack, Physical attack/Blizzara/Blizzaga, Physical attack/Petrify Stare
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (group_level(enemy team) >= 1) {
    if (last_damage == magical) {
        magic_hit_pending = 1
        silence_target = 203
    }
}
return
```

## 7: SAM08G

Variables: `charging` = varA (named), `charge_turns` = varB (named)


### Init

```
charging = 0
charge_turns = 0
return
```

### Turn

```
if (alive(entity 87)) {
    if (alive(entity 88)) {
        if (alive(entity 124)) {
            if (charging == 1) {
                charging = 0
                charge_turns = 0
                target random enemy
                use Cannon Blow
                return
            } else {
                target random enemy
                use one of Shoulder Charge, Physical attack, Gatling Gun
                return
            }
        }
    }
}
if (charging != 0) {
    charge_turns += 1
    if (charge_turns >= 3) {
        charging = 0
        charge_turns = 0
        target all enemies
        use Wild Cannon Blow
    } else {
        if (charge_turns == 2) {
            if (random(0..1) == 0) {
                charging = 0
                charge_turns = 0
                target random enemy
                use Cannon Blow
            }
        }
    }
} else {
    charging = 1
    charge_turns = 0
    target self
    use Store
}
return
```

## 8: GIM47N


### Turn

```
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (random(0..2) == 0) {
    return
} else {
    if (group_level(enemy team) == 0) {
        target random enemy
        use one of Physical attack, Physical attack, Snipe Laser
    } else {
        if (group_level(enemy team) == 1) {
            if (random(0..1) == 0) {
                target all enemies
                use Chaingun
            } else {
                target random enemy
                use one of Physical attack, Physical attack, Snipe Laser
            }
        } else {
            if (random(0..2) == 0) {
                if (status(self) lacks Reflect) {
                    target self
                    use Reflect
                }
            } else {
                if (random(0..1) == 0) {
                    target all enemies
                    use Chaingun
                } else {
                    target random enemy
                    use one of Physical attack, Physical attack, Snipe Laser
                }
            }
        }
    }
}
return
```

## 9: Mesmerize

Variables: `once_pre_hit` = varA (auto)


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (once_pre_hit == 0) {
    if (random(0..2) == 0) {
        target random enemy
        use Blade Shot
    } else {
        target random enemy
        use one of Physical attack, Blade Slice, Blade Slice
    }
} else {
    target random enemy
    use one of Physical attack, Physical attack, Hind Kick
}
return
```

### Counter

```
if (status(self) has Confuse) {
    if (once_pre_hit == 0) {
    } else {
        if (varB == 1) {
            print 'The horn broke off!'
            varB = 0
        }
    }
} else {
    if (once_pre_hit == 0) {
        if (last_damage == magical) {
            target last attacker
            use Blade Shot
            return
        }
    } else {
        if (varB == 1) {
            print 'The horn broke off!'
            varB = 0
        }
    }
}
return
```

### Pre-hit

```
if (once_pre_hit == 0) {
    if (last_damage == physical) {
        if (status(self) lacks Petrify) {
            if (status(self) lacks Stop) {
                if (random(0..2) == 0) {
                    once_pre_hit = 1
                    varB = 1
                    setHitAnim 12
                }
            }
        }
    }
}
return
```

## 10: Buel


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (group_level(enemy team) >= 1) {
    if (status(self) has Reflect) {
        if (group_level(enemy team) == 2) {
            if (random(0..2) == 0) {
                if (status(ally team) has Reflect) {
                    targetStatus 00c90017
                    use one of Fire/Fira/Firaga, Fire/Fira/Firaga, Thunder/Thundara/Thundaga
                } else {
                    target random enemy
                    use one of Physical attack, Fire/Fira/Firaga, Thunder/Thundara/Thundaga
                }
            } else {
                target random enemy
                use one of Physical attack, Fire/Fira/Firaga, Thunder/Thundara/Thundaga
            }
        } else {
            target random enemy
            use one of Physical attack, Fire/Fira/Firaga, Thunder/Thundara/Thundaga
        }
    } else {
        if (random(0..2) == 0) {
            target self
            use Reflect
        } else {
            target random enemy
            use one of Physical attack, Fire/Fira/Firaga, Thunder/Thundara/Thundaga
        }
    }
} else {
    target random enemy
    use one of Physical attack, Fire/Fira/Firaga, Thunder/Thundara/Thundaga
}
return
```

### Death

```
if (status(self) lacks Confuse) {
    if (status(self) lacks Petrify) {
        if (status(self) lacks Sleep) {
            if (status(self) lacks Stop) {
                if (status(self) lacks Berserk) {
                    if (last_command == Attack) {
                        if (group_level(enemy team) == 2) {
                            if (random(0..2) == 0) {
                                target last attacker
                                use Death
                            }
                        }
                    }
                }
            }
        }
    }
}
die
return
```

## 11: Sphinxaur


### Turn

```
if (random(0..2) == 0) {
    return
} else {
    target random enemy
    use one of Firaga, Thundaga, Blizzaga
}
return
```

### Death

```
prepare summon
target monster c0m012 (Sphinxara)
use null
leave 200
return
```

## 12: Sphinxara

Variables: `once_turn` = varA (auto), `defeated` = varB (auto), `phase` = varD (auto)


### Turn

```
if (defeated != 0) {
    return
}
if (once_turn == 0) {
    if (random(0..2) == 0) {
        return
    } else {
        if (alive_count(ally team) == 1) {
            if (phase == 0) {
                phase = 1
                activate
                enable 2
                once_turn = 1
                target self
                use ??
            } else {
                if (phase == 1) {
                    phase = 2
                    activate
                    enable 3
                    once_turn = 1
                    target self
                    use ??
                } else {
                    if (phase == 2) {
                        phase = 3
                        activate
                        enable 4
                        once_turn = 1
                        target self
                        use ??
                    } else {
                        if (status(enemy team) lacks Doom) {
                            targetStatus 00c8031a
                            use Doom
                        } else {
                            target random enemy
                            use one of Slow, Sleep, Zombie
                        }
                    }
                }
            }
        } else {
            if (status(enemy team) lacks Doom) {
                targetStatus 00c8031a
                use Doom
            } else {
                target random enemy
                use one of Slow, Sleep, Zombie
            }
        }
    }
}
return
```

### Counter

```
if (once_turn == 1) {
    prepare summon
    target new ally
    use Magic Summon
    activate
    loadAndTargetable 209
    once_turn = 0
}
return
```

### Death

```
if (alive_count(ally team) != 1) {
    leave 0
    leave 2
    leave 3
}
if (defeated == 0) {
    defeated = 1
    target self
    use null
    leave 200
}
return
```

## 13: Snow Lion


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use null
    return
}
if (group_level(enemy team) >= 1) {
    if (random(0..2) == 0) {
        target all enemies
        use Ice Breath
    } else {
        target random enemy
        use one of null, Physical attack, Physical attack
    }
} else {
    target random enemy
    use one of null, Physical attack, Physical attack
}
return
```

### Counter

```
if (random(0..2) == 0) {
    return
} else {
    if (status(self) has Confuse) {
        return
    } else {
        if (group_level(enemy team) >= 1) {
            if (last_command == Magic) {
                if (last_element == Fire) {
                    target all enemies
                    use Ice Breath
                }
            }
        }
    }
}
return
```

## 14: Anacondaur

Variables: `target_slot` = varA (auto)


### Init

```
target_slot = 240
if (combat_scene == 20 /*Anacondaur*/) {
    if (alive_count(enemy team) != 1) {
        if (alive(entity 6)) {
            print+lock 'Seifer “Listen up!”'
            print+lock '“The finishing blow determines”'
            print+lock '“the EXP.  Save it for me!”'
            waitText 03
        }
    }
}
return
```

### Turn

```
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (target_slot != 240) {
    if (random(0..1) == 0) {
        target target_slot
        use Squeeze
        target_slot = 240
    } else {
        target_slot = 240
        if (HP%(self) < 50) {
            if (random(0..2) == 0) {
                target random enemy
                use Dark Mist/Poison Mist
            } else {
                target random enemy
                use Physical attack
            }
        } else {
            target random enemy
            use one of Physical attack, Physical attack, line 253
        }
    }
} else {
    if (HP%(self) < 50) {
        if (random(0..2) == 0) {
            target random enemy
            use Dark Mist/Poison Mist
        } else {
            target random enemy
            use Physical attack
        }
    } else {
        target random enemy
        use one of Physical attack, Physical attack, line 253
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (last_damage == physical) {
    target_slot = 203
}
return
```

## 15: Grat


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (random(0..2) == 0) {
    target random enemy
    use one of Physical attack, Vampire, Gastric Juice
} else {
    target random enemy
    use Physical attack
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (random(0..7) == 0) {
    target all enemies
    use Sleeping Gas
}
return
```

## 16: Cockatrice


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use null (Cockatrice Pecks)
    return
}
if (alive_count(ally team) == 1) {
    if (group_level(enemy team) == 0) {
        if (random(0..2) == 0) {
            target random enemy
            use Upward Kick
        } else {
            target all enemies
            use Electric Discharge
        }
    } else {
        if (random(0..2) == 0) {
            target all enemies
            use Electric Discharge
        } else {
            target random enemy
            use one of Petrify Stare, Petrify Stare, Upward Kick
        }
    }
} else {
    target random enemy
    use one of null (Cockatrice Pecks), null (Cockatrice Pecks), Upward Kick
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
} else {
    if (status(self) has Berserk) {
        return
    }
}
if (last_command == Magic) {
    if (group_level(enemy team) >= 1) {
        if (random(0..2) == 0) {
            target random enemy
            use Petrify Stare
            return
        }
    }
}
return
```

### Death

```
if (status(self) lacks Confuse) {
    if (status(self) lacks Petrify) {
        if (status(self) lacks Sleep) {
            if (status(self) lacks Stop) {
                if (status(self) lacks Berserk) {
                    if (last_element == Fire) {
                        if (random(0..2) == 0) {
                            target all enemies
                            use Electric Discharge
                        }
                    }
                }
            }
        }
    }
}
die
return
```

## 17: Caterchipillar

Variables: `first_web_done` = varA (named)


### Init

```
first_web_done = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (HP%(self) < 50) {
    if (group_level(enemy team) >= 1) {
        if (random(0..2) == 0) {
            if (first_web_done == 0) {
                first_web_done = 1
                targetStatus 00c800d1
                use Sticky Web
            } else {
                target random enemy
                use Sticky Web
            }
        } else {
            if (random(0..2) == 0) {
                target all enemies
                use Ultra Waves
            } else {
                target random enemy
                use one of Physical attack, Physical attack, null
            }
        }
    } else {
        if (random(0..2) == 0) {
            target all enemies
            use Ultra Waves
        } else {
            target random enemy
            use one of Physical attack, Physical attack, null
        }
    }
} else {
    target random enemy
    use one of Physical attack, Physical attack, null
}
return
```

## 18: Red Bat


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random enemy
    use Physical attack/Vampire
    return
}
if (HP%(self) < 50) {
    target random enemy
    use one of Physical attack, Physical attack/Vampire, Ultrasonic Waves
} else {
    target random enemy
    use one of Physical attack, Physical attack, line 253
}
return
```

## 19: Blitz

Variables: `once_on_hit` = varA (auto)


### Turn

```
if (random(0..2) == 0) {
    return
}
if (random(0..2) == 0) {
    target self
    use Thunder/Thundara/Thundaga
} else {
    if (once_on_hit == 0) {
        target random enemy
        use one of Physical attack, Physical attack, Thunder/Thundara/Thundaga
    } else {
        target random enemy
        use one of null, null, Thunder/Thundara/Thundaga
    }
}
return
```

### Counter

```
if (once_on_hit == 0) {
    if (last_element == Thunder) {
        once_on_hit = 1
        autoStatus 2601
        print 'Blitz charged itself up!'
        set_scan_text 'Charging...'
    }
}
return
```

### Pre-hit

```
if (status(self) lacks Petrify) {
    if (status(self) lacks Stop) {
        if (last_damage == physical) {
            if (last_element == Thunder) {
                setHitAnim 15
            }
        } else {
            if (last_damage == magical) {
                if (last_element == Thunder) {
                    setHitAnim 16
                }
            }
        }
    }
}
return
```

## 20: Fastitocalon

Variables: `once_turn` = varA (auto)


### Init

```
once_turn = 0
Vitality multiplier = 300%
Spirit multiplier = 300%
return
```

### Turn

```
if (status(self) has Confuse) {
    target random non-self ally
    if (once_turn == 0) {
        target self
        use null (Fastitocalon Reveal)
        once_turn = 1
        elemDmgMod 038403
        Vitality multiplier = 100%
        Spirit multiplier = 100%
    } else {
        target random non-self ally
        use null (Fastitocalon Bite)
    }
    return
}
if (once_turn == 0) {
    target random enemy
    use Physical attack
} else {
    if (random(0..2) == 0) {
        target all enemies
        use Sand Storm
    } else {
        target random enemy
        use null (Fastitocalon Bite)
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (last_command == Magic) {
    if (last_element == Thunder) {
        if (once_turn == 0) {
            target self
            use null (Fastitocalon Reveal)
            once_turn = 1
            elemDmgMod 038403
            Vitality multiplier = 100%
            Spirit multiplier = 100%
        }
    } else {
        if (HP%(self) <= 50) {
            if (once_turn == 0) {
                target self
                use null (Fastitocalon Reveal)
                once_turn = 1
                elemDmgMod 038403
                Vitality multiplier = 100%
                Spirit multiplier = 100%
            }
        } else {
            if (random(0..2) == 0) {
                if (once_turn == 0) {
                    target self
                    use null (Fastitocalon Reveal)
                    once_turn = 1
                    elemDmgMod 038403
                    Vitality multiplier = 100%
                    Spirit multiplier = 100%
                }
            }
        }
    }
} else {
    if (HP%(self) <= 50) {
        if (once_turn == 0) {
            target self
            use null (Fastitocalon Reveal)
            once_turn = 1
            elemDmgMod 038403
            Vitality multiplier = 100%
            Spirit multiplier = 100%
        }
    } else {
        if (random(0..2) == 0) {
            if (once_turn == 0) {
                target self
                use null (Fastitocalon Reveal)
                once_turn = 1
                elemDmgMod 038403
                Vitality multiplier = 100%
                Spirit multiplier = 100%
            }
        }
    }
}
return
```

## 21: Fastitocalon

Variables: `once_turn` = varA (auto)


### Init

```
once_turn = 0
Vitality multiplier = 300%
Spirit multiplier = 300%
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    if (once_turn == 0) {
        target self
        use null (Fastitocalon-F Reveal)
        once_turn = 1
        elemDmgMod 038403
        Vitality multiplier = 100%
        Spirit multiplier = 100%
    } else {
        target random non-self ally
        use null (Fastitocalon-F Bite)
    }
    return
}
if (once_turn == 0) {
    target random enemy
    use Physical attack
} else {
    target random enemy
    use null (Fastitocalon-F Bite)
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (last_command == Magic) {
    if (last_element == Thunder) {
        if (once_turn == 0) {
            target self
            use null (Fastitocalon-F Reveal)
            once_turn = 1
            elemDmgMod 038403
            Vitality multiplier = 100%
            Spirit multiplier = 100%
        }
    } else {
        if (HP%(self) <= 50) {
            if (once_turn == 0) {
                target self
                use null (Fastitocalon-F Reveal)
                once_turn = 1
                elemDmgMod 038403
                Vitality multiplier = 100%
                Spirit multiplier = 100%
            }
        } else {
            if (random(0..2) == 0) {
                if (once_turn == 0) {
                    target self
                    use null (Fastitocalon-F Reveal)
                    once_turn = 1
                    elemDmgMod 038403
                    Vitality multiplier = 100%
                    Spirit multiplier = 100%
                }
            }
        }
    }
} else {
    if (HP%(self) <= 50) {
        if (once_turn == 0) {
            target self
            use null (Fastitocalon-F Reveal)
            once_turn = 1
            elemDmgMod 038403
            Vitality multiplier = 100%
            Spirit multiplier = 100%
        }
    } else {
        if (random(0..2) == 0) {
            if (once_turn == 0) {
                target self
                use null (Fastitocalon-F Reveal)
                once_turn = 1
                elemDmgMod 038403
                Vitality multiplier = 100%
                Spirit multiplier = 100%
            }
        }
    }
}
return
```

## 22: Gesper


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    if (random(0..3) == 0) {
        if (random(0..2) == 0) {
            target random enemy
        } else {
            target random non-self ally
        }
        if (random(0..2) == 0) {
            use one of Cure/Cura, Shell, Protect
        } else {
            if (random(0..1) == 0) {
                use one of Confuse, Berserk, Slow/Stop
            } else {
                use one of Blind, Silence, Float
            }
        }
    } else {
        if (random(0..2) == 0) {
            target random enemy
        } else {
            if (alive_count(ally team) == 1) {
                target random enemy
            } else {
                target random non-self ally
            }
        }
        use one of Physical attack, Physical attack, line 253
    }
}
if (random(0..3) == 0) {
    if (random(0..2) == 0) {
        if (alive_count(ally team) == 1) {
            target random enemy
        } else {
            target random non-self ally
        }
    } else {
        target random enemy
    }
    if (random(0..2) == 0) {
        use one of Cure/Cura, Shell, Protect
    } else {
        if (random(0..1) == 0) {
            use one of Confuse, Berserk, Slow/Stop
        } else {
            use one of Blind, Silence, Float
        }
    }
} else {
    if (random(0..2) == 0) {
        if (alive_count(ally team) == 1) {
            target random enemy
        } else {
            target random non-self ally
        }
        use one of Physical attack, Physical attack, line 253
    } else {
        if (alive_count(enemy team) == 1) {
            target random enemy
            use one of Physical attack, Physical attack, Telekinesis
        } else {
            target random enemy
            use one of Physical attack, Physical attack/Degenerator, Telekinesis
        }
    }
}
return
```

## 23: Creeps

Variables: `once_turn` = varA (auto)


### Init

```
once_turn = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random enemy
    use Protect
    return
}
if (status(enemy team) has Invocation-pending) {
    targetStatus 00c8002f
    use Physical attack
} else {
    if (once_turn == 0) {
        if (random(0..4) == 0) {
            once_turn = 1
            target random enemy
            use Heartbreak
        } else {
            target random enemy
            use one of Physical attack, Physical attack, Thunder/Thundara/Thundaga
        }
    } else {
        target random enemy
        use one of Physical attack, Physical attack, Thunder/Thundara/Thundaga
    }
}
return
```

### Death

```
if (status(self) lacks Confuse) {
    if (status(self) lacks Petrify) {
        if (status(self) lacks Sleep) {
            if (status(self) lacks Stop) {
                if (status(self) lacks Berserk) {
                    if (last_damage == magical) {
                        if (random(0..2) == 0) {
                            target random enemy
                            use Thundara/Thundaga
                        }
                    }
                }
            }
        }
    }
}
die
return
```

## 24: Hexadragon


### Turn

```
if (group_level(enemy team) >= 1) {
    if (HP%(self) < 30) {
        if (random(0..2) == 0) {
            target all enemies
            use Melt-Eye
        } else {
            if (random(0..2) == 0) {
                target random enemy
                use one of Firaga, Firaga, Breath
            } else {
                target random enemy
                use Physical attack
            }
        }
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use one of Firaga, Firaga, Breath
        } else {
            target random enemy
            use Physical attack
        }
    }
} else {
    if (random(0..2) == 0) {
        target random enemy
        use one of Fira, Fira, Breath
    } else {
        target random enemy
        use Physical attack
    }
}
return
```

## 25: Blood Soul


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (group_level(enemy team) >= 1) {
    if (random(0..2) == 0) {
        if (status(enemy team) has Zombie) {
            targetStatus 00c80006
            use one of Cura, Curaga, Regen
        } else {
            if (status(enemy team) has Reflect) {
                targetStatus 00c80017
                use Dispel
            } else {
                target random enemy
                use one of Silence, Zombie, Zombie
            }
        }
    } else {
        if (random(0..1) == 0) {
            target random enemy
            use one of Physical attack, Breath of Death, Disease Breath
        } else {
            target random enemy
            use one of Zombie, Blind, Sleep
        }
    }
} else {
    if (random(0..1) == 0) {
        target random enemy
        use one of Physical attack, Physical attack, Breath of Death
    } else {
        target random enemy
        use one of Berserk, Blind, Sleep
    }
}
return
```

## 26: Elastoid

Variables: `low_hp_mode` = varA (named)


### Init

```
low_hp_mode = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (low_hp_mode == 0) {
    if (group_level(enemy team) == 2) {
        if (random(0..2) != 0) {
            target random enemy
            use one of Physical attack, Beam Laser, Beam Laser
        } else {
            if (random(0..1) == 0) {
                target random ally
                use one of Shell, Protect, Haste
            } else {
                target random enemy
                use one of Dispel, Stop, Sleep
            }
        }
    } else {
        if (group_level(enemy team) == 1) {
            if (random(0..1) == 0) {
                target random enemy
                use one of Physical attack, Beam Laser, Beam Laser
            } else {
                target random ally
                use one of Shell, Protect, Haste
            }
        } else {
            target random enemy
            use Physical attack
        }
    }
} else {
    target all enemies
    use Reflect Beam
}
return
```

### Counter

```
if (low_hp_mode == 0) {
    if (HP%(self) < 30) {
        low_hp_mode = 1
        target self
        use null
    }
} else {
    if (HP%(self) > 30) {
        low_hp_mode = 0
        target self
        use null
    }
}
return
```

## 27: Armadodo

Variables: `once_pre_hit` = varA (auto)


### Init

```
once_pre_hit = 0
varB = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (once_pre_hit == 1) {
    if (status(self) has Float) {
        return
    } else {
        if (group_level(enemy team) >= 1) {
            if (random(0..3) == 0) {
                once_pre_hit = 0
                target self
                Vitality multiplier = 100%
                use null
                print 'Armadodo got up!'
            }
        } else {
            if (random(0..5) == 0) {
                once_pre_hit = 0
                target self
                Vitality multiplier = 100%
                use null
                print 'Armadodo got up!'
            }
        }
    }
} else {
    if (status(self) has Confuse) {
        target random non-self ally
        use Physical attack
        return
    } else {
        if (group_level(enemy team) >= 1) {
            if (random(0..3) == 0) {
                target all enemies
                use Earthquake
            } else {
                target random enemy
                use one of Physical attack, Physical attack, null
            }
        } else {
            target random enemy
            use one of Physical attack, Physical attack, null
        }
    }
}
return
```

### Counter

```
if (varB == 1) {
    varB = 0
    print 'Armadodo fell over!'
}
return
```

### Death

```
if (status(self) lacks Confuse) {
    if (status(self) lacks Petrify) {
        if (status(self) lacks Sleep) {
            if (status(self) lacks Stop) {
                if (status(self) lacks Berserk) {
                    if (status(self) lacks Float) {
                        if (once_pre_hit == 0) {
                            if (random(0..2) == 0) {
                                target all enemies
                                use Earthquake
                            }
                        }
                    }
                }
            }
        }
    }
}
die
return
```

### Pre-hit

```
if (last_damage == physical) {
    if (status(self) lacks Float) {
        if (status(self) lacks Petrify) {
            if (status(self) lacks Stop) {
                if (once_pre_hit == 0) {
                    if (random(0..4) == 0) {
                        once_pre_hit = 1
                        setHitAnim 15
                        Vitality multiplier = 20%
                        varB = 1
                    }
                }
            }
        }
    }
}
return
```

## 28: Bite Bug

Variables: `turn_counter` = varA (auto)


### Init

```
if (save.tutorial_bite_bug_seen == 0) {
    if (battle.tutorial_shown_this_battle == 0) {
        if (alive_count(enemy team) == 2) {
            if (status(enemy team) lacks Death) {
                if (alive(entity 0)) {
                    if (alive(entity 3)) {
                        battle.tutorial_shown_this_battle = 1
                        save.tutorial_bite_bug_seen = 1
                        print+lock '{Quistis} “{Squall}, you still remember?”'
                        print+lock '“The {R1} is the trigger.”'
                        print+lock '“Pull it just as you strike.”'
                        print+lock '“Same for the Renzokuken!”'
                        waitText 04
                    }
                }
            }
        }
    }
}
turn_counter = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
} else {
    if (group_level(enemy team) >= 1) {
        turn_counter += 1
    }
}
if (turn_counter == 3) {
    if (random(0..2) == 0) {
        target random enemy
        use one of Physical attack/Needle, Physical attack/Fart, Physical attack/Fart
        turn_counter = 0
        return
    }
} else {
    if (turn_counter == 4) {
        if (random(0..1) == 0) {
            target random enemy
            use one of Physical attack/Needle, Physical attack/Fart, Physical attack/Fart
            turn_counter = 0
            return
        }
    } else {
        if (turn_counter >= 5) {
            if (random(0..2) != 0) {
                target random enemy
                use one of Physical attack/Needle, Physical attack/Fart, Physical attack/Fart
                turn_counter = 0
                return
            }
        }
    }
}
target random enemy
use one of Physical attack, Physical attack, Physical attack/Needle
return
```

## 29: Jelleye

Variables: `phase` = varA (auto), `hit_counter` = varB (auto), `phase_2` = varC (auto)


### Init

```
phase = 0
hit_counter = 0
if (random(0..2) == 0) {
    return
}
if (random(0..2) == 0) {
    phase_2 = 0
} else {
    if (random(0..1) == 0) {
        phase_2 = 1
    } else {
        phase_2 = 2
    }
}
return
```

### Turn

```
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (hit_counter >= 2) {
    if (phase == 0) {
        if (random(0..2) == 0) {
            phase = 1
            hit_counter = 0
            varD = 1
            set_scan_text 'Complete Defense Morph'
            Strength multiplier = 100%
            Magic multiplier = 100%
            Vitality multiplier = 400%
            Spirit multiplier = 400%
            target self
            use Morph
        } else {
            if (random(0..1) == 0) {
                phase = 2
                hit_counter = 0
                varD = 1
                set_scan_text 'Magic Defense Morph'
                Strength multiplier = 50%
                Magic multiplier = 200%
                Vitality multiplier = 30%
                Spirit multiplier = 1000%
                target self
                use Morph
            } else {
                phase = 3
                hit_counter = 0
                varD = 1
                set_scan_text 'Physical Defense Morph'
                Strength multiplier = 200%
                Magic multiplier = 50%
                Vitality multiplier = 1000%
                Spirit multiplier = 30%
                target self
                use Morph
            }
        }
    } else {
        if (phase == 1) {
            if (random(0..2) == 0) {
                phase = 0
                hit_counter = 0
                varD = 1
                set_scan_text 'Normal Defense Morph'
                Strength multiplier = 100%
                Magic multiplier = 100%
                Vitality multiplier = 100%
                Spirit multiplier = 100%
                target self
                use Morph
            } else {
                if (random(0..1) == 0) {
                    phase = 2
                    hit_counter = 0
                    varD = 1
                    set_scan_text 'Magic Defense Morph'
                    Strength multiplier = 50%
                    Magic multiplier = 200%
                    Vitality multiplier = 30%
                    Spirit multiplier = 1000%
                    target self
                    use Morph
                } else {
                    phase = 3
                    hit_counter = 0
                    varD = 1
                    set_scan_text 'Physical Defense Morph'
                    Strength multiplier = 200%
                    Magic multiplier = 50%
                    Vitality multiplier = 1000%
                    Spirit multiplier = 30%
                    target self
                    use Morph
                }
            }
        } else {
            if (phase == 2) {
                if (random(0..2) == 0) {
                    phase = 0
                    hit_counter = 0
                    varD = 1
                    set_scan_text 'Normal Defense Morph'
                    Strength multiplier = 100%
                    Magic multiplier = 100%
                    Vitality multiplier = 100%
                    Spirit multiplier = 100%
                    target self
                    use Morph
                } else {
                    if (random(0..1) == 0) {
                        phase = 1
                        hit_counter = 0
                        varD = 1
                        set_scan_text 'Complete Defense Morph'
                        Strength multiplier = 100%
                        Magic multiplier = 100%
                        Vitality multiplier = 400%
                        Spirit multiplier = 400%
                        target self
                        use Morph
                    } else {
                        phase = 3
                        hit_counter = 0
                        varD = 1
                        set_scan_text 'Physical Defense Morph'
                        Strength multiplier = 200%
                        Magic multiplier = 50%
                        Vitality multiplier = 1000%
                        Spirit multiplier = 30%
                        target self
                        use Morph
                    }
                }
            } else {
                if (random(0..2) == 0) {
                    phase = 0
                    hit_counter = 0
                    varD = 1
                    set_scan_text 'Normal Defense Morph'
                    Strength multiplier = 100%
                    Magic multiplier = 100%
                    Vitality multiplier = 100%
                    Spirit multiplier = 100%
                    target self
                    use Morph
                } else {
                    if (random(0..1) == 0) {
                        phase = 1
                        hit_counter = 0
                        varD = 1
                        set_scan_text 'Complete Defense Morph'
                        Strength multiplier = 100%
                        Magic multiplier = 100%
                        Vitality multiplier = 400%
                        Spirit multiplier = 400%
                        target self
                        use Morph
                    } else {
                        phase = 2
                        hit_counter = 0
                        varD = 1
                        set_scan_text 'Magic Defense Morph'
                        Strength multiplier = 50%
                        Magic multiplier = 200%
                        Vitality multiplier = 30%
                        Spirit multiplier = 1000%
                        target self
                        use Morph
                    }
                }
            }
        }
    }
} else {
    if (phase == 0) {
        target random enemy
        if (random(0..2) == 0) {
            use Physical attack
        } else {
            if (phase_2 == 0) {
                use Fire/Fira/Firaga
            } else {
                if (phase_2 == 1) {
                    use Thunder/Thundara/Thundaga
                } else {
                    use Blizzard/Blizzara/Blizzaga
                }
            }
        }
    } else {
        if (phase == 1) {
            if (random(0..2) != 0) {
                return
            } else {
                target random enemy
                if (random(0..2) != 0) {
                    use Physical attack
                } else {
                    if (phase_2 == 0) {
                        use Fire/Fira/Firaga
                    } else {
                        if (phase_2 == 1) {
                            use Thunder/Thundara/Thundaga
                        } else {
                            use Blizzard/Blizzara/Blizzaga
                        }
                    }
                }
            }
        } else {
            if (phase == 2) {
                target random enemy
                if (phase_2 == 0) {
                    use Fire/Fira/Firaga
                } else {
                    if (phase_2 == 1) {
                        use Thunder/Thundara/Thundaga
                    } else {
                        use Blizzard/Blizzara/Blizzaga
                    }
                }
            } else {
                target random enemy
                use Physical attack
            }
        }
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (varD == 1) {
    varD = 0
    return
}
if (random(0..2) == 0) {
    return
}
if (phase == 3) {
    if (last_damage == physical) {
        target last attacker
        use Physical attack
    } else {
        hit_counter += 1
    }
} else {
    if (phase == 2) {
        if (last_damage == magical) {
            target last attacker
            if (phase_2 == 0) {
                target last attacker
                use Fire/Fira/Firaga
            } else {
                if (phase_2 == 1) {
                    target last attacker
                    use Thunder/Thundara/Thundaga
                } else {
                    target last attacker
                    use Blizzard/Blizzara/Blizzaga
                }
            }
        } else {
            hit_counter += 1
        }
    } else {
        if (phase == 1) {
            if (last_damage == physical) {
                target last attacker
                use Physical attack
            } else {
                if (phase_2 == 0) {
                    target last attacker
                    use Fire/Fira/Firaga
                } else {
                    if (phase_2 == 1) {
                        target last attacker
                        use Thunder/Thundara/Thundaga
                    } else {
                        target last attacker
                        use Blizzard/Blizzara/Blizzaga
                    }
                }
            }
            hit_counter += 1
        } else {
            hit_counter += 1
        }
    }
}
return
```

## 30: Tri-Point

Variables: `once_on_hit` = varA (auto), `turn_counter` = varB (auto), `phase` = varC (auto)


### Init

```
once_on_hit = 0
turn_counter = 0
phase = 0
elemDmgMod 00f401
elemDmgMod 012003
print+lock '“USING ELEMENTAL ATTACKS.”'
print+lock "“WHATEVER I DON'T USE, I DON'T LIKE.”"
waitText 02
return
```

### Turn

```
unless (random(0..2) == 0) goto L12
return
goto L12
L12: turn_counter += 1
unless (turn_counter == 1) goto L32
target random enemy
use one of Physical attack, Physical attack, line 253
goto L448
L32: unless (turn_counter == 2) goto L49
target random enemy
use one of Physical attack, Physical attack, line 253
goto L448
L49: unless (turn_counter == 3) goto L241
L57: unless (random(0..5) == 0) goto L89
unless (alive(entity 0)) goto L83
target battle slot 0
use Scan
phase = 0
goto L86
L83: goto L57
L86: goto L238
L89: unless (random(0..4) == 0) goto L121
unless (alive(entity 1)) goto L115
target battle slot 1
use Scan
phase = 1
goto L118
L115: goto L57
L118: goto L238
L121: unless (random(0..3) == 0) goto L153
unless (alive(entity 2)) goto L147
target battle slot 2
use Scan
phase = 2
goto L150
L147: goto L57
L150: goto L238
L153: unless (random(0..2) == 0) goto L185
unless (alive(entity 3)) goto L179
target battle slot 3
use Scan
phase = 3
goto L182
L179: goto L57
L182: goto L238
L185: unless (random(0..1) == 0) goto L217
unless (alive(entity 4)) goto L211
target battle slot 4
use Scan
phase = 4
goto L214
L211: goto L57
L214: goto L238
L217: unless (alive(entity 5)) goto L235
target battle slot 5
use Scan
phase = 5
goto L238
L235: goto L57
L238: goto L448
L241: unless (turn_counter == 5) goto L433
unless (phase == 0) goto L281
unless (alive(entity 0)) goto L272
target battle slot 0
use Onrush
goto L278
L272: turn_counter = 3
goto L57
L278: goto L430
L281: unless (phase == 1) goto L313
unless (alive(entity 1)) goto L304
target battle slot 1
use Onrush
goto L310
L304: turn_counter = 3
goto L57
L310: goto L430
L313: unless (phase == 2) goto L345
unless (alive(entity 2)) goto L336
target battle slot 2
use Onrush
goto L342
L336: turn_counter = 3
goto L57
L342: goto L430
L345: unless (phase == 3) goto L377
unless (alive(entity 3)) goto L368
target battle slot 3
use Onrush
goto L374
L368: turn_counter = 3
goto L57
L374: goto L430
L377: unless (phase == 4) goto L409
unless (alive(entity 4)) goto L400
target battle slot 4
use Onrush
goto L406
L400: turn_counter = 3
goto L57
L406: goto L430
L409: unless (alive(entity 5)) goto L424
target battle slot 5
use Onrush
goto L430
L424: turn_counter = 3
goto L57
L430: goto L448
L433: unless (turn_counter == 6) goto L447
turn_counter = 0
goto L448
L447: return
```

### Counter

```
if (last_command == Magic) {
    if (last_action_id == 50) {
        return
    }
}
if (once_on_hit == 0) {
    if (last_element == Fire) {
        once_on_hit = 1
        elemDmgMod 002003
        elemDmgMod 01f401
    } else {
        target all enemies
        use Mega Spark
    }
} else {
    if (last_element == Ice) {
        once_on_hit = 0
        elemDmgMod 00f401
        elemDmgMod 012003
    } else {
        target all enemies
        use Mega Spark
    }
}
return
```

### Death

```
target self
use null
leave 200
return
```

## 31: Turtapod

Variables: `once_on_hit` = varA (auto)


### Init

```
once_on_hit = 0
return
```

### Turn

```
if (status(self) has Confuse) {
    if (once_on_hit == 0) {
        target random non-self ally
        use Physical attack
    }
    return
}
if (once_on_hit == 0) {
    target random enemy
    use one of Physical attack, Physical attack, line 3
} else {
    if (random(0..3) == 0) {
        target self
        use Do Nothing?
        Vitality multiplier = 100%
        Spirit multiplier = 100%
        once_on_hit = 0
    }
}
return
```

### Counter

```
if (group_level(enemy team) >= 1) {
    if (once_on_hit == 0) {
        if (random(0..2) == 0) {
            target self
            use Do Nothing?
            Vitality multiplier = 500%
            Spirit multiplier = 500%
            once_on_hit = 1
        }
    }
}
return
```

## 32: Wendigo


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (group_level(enemy team) == 2) {
    if (random(0..2) != 0) {
        if (random(0..1) == 0) {
            target random enemy
            use one of Power Bomb, Power Bomb, Dribble
        } else {
            target random enemy
            use one of Physical attack, Physical attack, Arm Hug
        }
    }
    if (alive_count(enemy team) == 3) {
        target all enemies
        use Shoot
    } else {
        if (status(enemy team) has Invocation-pending) {
            targetStatus 00c8002f
            use Dribble
        } else {
            if (random(0..1) == 0) {
                target random enemy
                use one of Power Bomb, Power Bomb, Dribble
            } else {
                target random enemy
                use one of Physical attack, Physical attack, Arm Hug
            }
        }
    }
} else {
    if (group_level(enemy team) == 1) {
        if (random(0..2) == 0) {
            targetStatus 00c800cc
            use Dribble
        } else {
            target random enemy
            use one of Physical attack, Arm Hug, Power Bomb
        }
    } else {
        target random enemy
        use one of Physical attack, Physical attack, Arm Hug
    }
}
return
```

## 33: Gayla


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(enemy team) lacks Sleep) {
    if (group_level(enemy team) == 1) {
        if (random(0..2) == 0) {
            targetStatus 00c80310
            use Hypnotize
            return
        }
    } else {
        if (group_level(enemy team) == 2) {
            if (random(0..2) != 0) {
                targetStatus 00c80310
                use Hypnotize
                return
            }
        }
    }
}
target random enemy
use one of Physical attack, Physical attack/Gastric Juice, null
return
```

## 34: Gerogero

Variables: `attack_cycle` = varA (named), `opening_line_done` = varB (named)


### Init

```
attack_cycle = 0
fill ATB
return
```

### Turn

```
attack_cycle += 1
if (opening_line_done == 0) {
    if (alive(entity 0)) {
        attack_cycle += 1
        print+lock '{Squall} “What the...?”'
    } else {
        if (alive(entity 1)) {
            attack_cycle += 1
            print+lock '{Zell} “...The hell is this!?”'
        } else {
            if (alive(entity 5)) {
                attack_cycle += 1
                print+lock '{Selphie} “Ewww!  Nasty!”'
            }
        }
    }
    opening_line_done = 1
} else {
    if (random(0..3) == 0) {
        return
    }
    if (attack_cycle == 1) {
        target random enemy
        use Physical attack
    } else {
        if (attack_cycle == 2) {
            if (random(0..2) == 0) {
                if (status(enemy team) lacks Berserk) {
                    if (alive_count(enemy team) == 1) {
                        target random enemy
                        use Sleep
                    } else {
                        target random enemy
                        use Berserk
                    }
                } else {
                    target random enemy
                    use Dispel
                }
            } else {
                target random enemy
                use Silence
            }
        } else {
            if (attack_cycle == 2) {
                target random enemy
                use Physical attack
            } else {
                attack_cycle = 0
                target random enemy
                use "Brrawghh!"
            }
        }
    }
}
return
```

## 35: Death Claw

Variables: `hit_counter` = varA (auto)


### Init

```
hit_counter = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (random(0..2) == 0) {
    return
} else {
    if (random(0..2) == 0) {
        target random enemy
        use one of Death Claw, Death Claw, Bear Hug
    } else {
        target random enemy
        use Physical attack
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (random(0..3) == 0) {
    hit_counter += 1
    if (hit_counter >= 3) {
        if (group_level(enemy team) == 2) {
            hit_counter = 0
            target all enemies
            use Explosion
        } else {
            if (group_level(enemy team) == 1) {
                hit_counter = 0
                target all enemies
                use Explosion
            } else {
                hit_counter = 0
                target all enemies
                use Explosion
            }
        }
    } else {
        target all enemies
        use Gas
    }
}
return
```

## 36: Tri-Face


### Turn

```
if (random(0..2) == 0) {
    return
}
if (alive_count(enemy team) == 1) {
    target random enemy
    use Bite
    return
} else {
    if (status(self) has HP<25%) {
        target random enemy
        use Acid
        return
    } else {
        if (random(0..4) == 0) {
            target all enemies
            use Poison Gas
        } else {
            target random enemy
            use one of Physical attack, Physical attack, Bite
        }
    }
}
return
```

### Death

```
if (last_element == Fire) {
    if (status(self) lacks Confuse) {
        if (status(self) lacks Petrify) {
            if (status(self) lacks Sleep) {
                if (status(self) lacks Stop) {
                    if (status(self) lacks Berserk) {
                        if (random(0..2) == 0) {
                            target all enemies
                            use Poison Gas
                        }
                    }
                }
            }
        }
    }
}
die
return
```

## 37: Grand Mantis


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (random(0..2) == 0) {
    target random enemy
    use one of Super Arm, Super Arm, Melting Bubble
} else {
    target random enemy
    use Physical attack
}
return
```

## 38: Krysta


### Init

```
print+lock '“SHOW ME WHAT YOU GOT!”'
print+lock "“YOU'LL REGRET FIGHTING ME!”"
waitText 02
return
```

### Turn

```
if (random(0..2) == 0) {
    target random enemy
    use one of Physical attack, Physical attack, Charge
}
return
```

### Counter

```
if (last_command == Magic) {
    if (last_action_id == 50) {
        return
    }
}
if (last_command == GF) {
    return
}
if (last_command == Item) {
    return
}
if (last_command == Attack) {
    target last attacker
    use null
} else {
    target last attacker
    use null
}
return
```

### Death

```
target all enemies
use Ultima
target self
use null
leave 200
return
```

## 39: Lefty

Variables: `once_death` = varA (auto)


### Turn

```
if (random(0..2) == 0) {
    return
}
if (group_level(enemy team) == 2) {
    if (random(0..2) == 0) {
        if (status(ally team) has Poison) {
            targetStatus 00c90001
            use Esuna
            return
        }
        if (status(ally team) has Berserk) {
            targetStatus 00c90005
            use Esuna
            return
        }
        if (status(ally team) has Silence) {
            targetStatus 00c90004
            use Esuna
            return
        }
        if (status(ally team) lacks Reflect) {
            targetStatus 00c90317
            use Reflect
            return
        }
        if (status(self) lacks Silence) {
            if (status(enemy team) has Has-Magic) {
                targetStatus 00c8002e
                use Draw
                draw magic
                cast drawn magic
            }
        } else {
            return
        }
    } else {
        if (status(enemy team) has Reflect) {
            if (status(ally team) lacks Reflect) {
                target self
                use Regen
            } else {
                targetStatus 00c90017
                use one of Thunder/Thundara/Thundaga, Demi, Bio
            }
        } else {
            if (random(0..2) == 0) {
                target random enemy each hit
                use Meteor
            } else {
                target all enemies
                use Quake
            }
        }
    }
} else {
    if (group_level(enemy team) == 1) {
        if (random(0..2) == 0) {
            if (status(self) lacks Silence) {
                if (status(enemy team) has Has-Magic) {
                    targetStatus 00c8002e
                    use Draw
                    draw magic
                    cast drawn magic
                }
            } else {
                return
            }
        } else {
            target random enemy
            use one of Stop, Drain, Blind
        }
    } else {
        target random enemy
        use one of Thunder/Thundara/Thundaga, Thunder/Thundara/Thundaga, Slow
    }
}
return
```

### Death

```
if (once_death == 0) {
    once_death = 1
    if (combat_scene == 180 /*Funguar*/) {
        if (battle.scene180_trio_death_count == 2) {
            die
            activate
            enter 3
        } else {
            battle.scene180_trio_death_count += 1
            die
        }
    } else {
        die
    }
}
return
```

## 40: Righty

Variables: `once_death` = varA (auto)


### Turn

```
if (random(0..2) == 0) {
    return
} else {
    target random enemy
    use one of Physical attack, Physical attack, null
}
return
```

### Death

```
if (once_death == 0) {
    once_death = 1
    if (combat_scene == 180 /*Funguar*/) {
        if (battle.scene180_trio_death_count == 2) {
            die
            activate
            enter 3
        } else {
            battle.scene180_trio_death_count += 1
            die
        }
    } else {
        die
    }
}
return
```

## 41: Blue Dragon

Variables: `target_slot` = varA (auto), `hit_counter` = varB (auto)


### Init

```
target_slot = 240
hit_counter = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (hit_counter >= 3) {
    hit_counter = 0
    if (random(0..2) == 0) {
        if (status(self) lacks Reflect) {
            target self
            use Reflect
            return
        } else {
            target all enemies
            use Breath
            return
        }
    } else {
        target all enemies
        use Breath
        return
    }
} else {
    if (target_slot != 240) {
        if (random(0..1) == 0) {
            target target_slot
            use Grab Punch
            target_slot = 240
            return
        }
    }
}
target random enemy
if (random(0..2) == 0) {
    use one of Bio/Death, Blind/Break, Drain
} else {
    use one of Physical attack, Physical attack, null
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (last_damage == physical) {
    target_slot = 203
} else {
    hit_counter += 1
}
return
```

## 42: Forbidden

Variables: `once_turn` = varA (auto)


### Init

```
once_turn = 0
varB = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (once_turn == 0) {
    if (HP%(self) < 20) {
        target self
        use null (Forbidden Iai Blow Stance)
        once_turn = 1
        varB = 0
    } else {
        if (random(0..2) == 0) {
            if (random(0..2) == 0) {
                target random enemy
                use one of Blind, Blind, Silence
            } else {
                if (random(0..1) == 0) {
                    target random enemy
                    use Slow/Stop
                } else {
                    target random enemy
                    use Sleep/Death
                }
            }
        } else {
            if (random(0..2) == 0) {
                target random enemy
                use one of Physical attack, Double Sword, Thrust
            } else {
                target random enemy
                use Physical attack
            }
        }
    }
} else {
    target random enemy
    use one of Iai Blow, line 253, line 253
}
return
```

### Counter

```
if (last_damage == physical) {
    if (once_turn == 1) {
        target last attacker
        use Iai Blow
    }
}
return
```

## 43: Bomb

Variables: `hits_taken` = varA (named)


### Init

```
if (save.tutorial_bomb_seen == 0) {
    if (battle.tutorial_shown_this_battle == 0) {
        if (alive_count(enemy team) == 2) {
            if (status(enemy team) lacks Death) {
                if (alive(entity 0)) {
                    if (alive(entity 3)) {
                        battle.tutorial_shown_this_battle = 1
                        save.tutorial_bomb_seen = 1
                        print+lock '{Quistis} “Bomb... An elemental monster.”'
                        print+lock '“Use an ice attack for these.”'
                        print+lock "“Check the monster's weakness with Scan.”"
                        waitText 03
                    }
                }
            }
        }
    }
}
hits_taken = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use one of Fire, Fire, line 253
    return
}
target random enemy
use one of Physical attack, Fire, line 253
return
```

### Counter

```
if (group_level(enemy team) >= 1) {
    hits_taken += 1
    if (hits_taken == 1) {
        target self
        use null (Bomb Expand 1)
        Strength multiplier = 150%
        return
    } else {
        if (hits_taken == 2) {
            target self
            use null (Bomb Expand 1)
            Strength multiplier = 200%
            return
        } else {
            target random enemy
            use Suicide
            leave 200
            return
        }
    }
}
return
```

## 44: Abyss Worm

Variables: `once_on_hit` = varA (auto), `hit_counter` = varB (auto)


### Init

```
once_on_hit = 0
hit_counter = 0
Vitality multiplier = 200%
Spirit multiplier = 200%
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (once_on_hit == 0) {
    if (random(0..2) == 0) {
        target self
        use one of Protect, Shell, line 8
        return
    } else {
        if (random(0..1) == 0) {
            target all enemies
            use Sand Shake
            return
        } else {
            return
        }
    }
} else {
    if (group_level(enemy team) == 2) {
        if (random(0..1) == 0) {
            target random enemy
            use one of Saliva, Aero, Aero
        } else {
            target all enemies
            use Physical attack
        }
    } else {
        if (random(0..1) == 0) {
            target random enemy
            use Saliva
        } else {
            target all enemies
            use Physical attack
        }
    }
}
return
```

### Counter

```
if (once_on_hit == 0) {
    hit_counter += 1
    if (group_level(enemy team) == 2) {
        if (random(0..2) == 0) {
            target all enemies
            use Sand Shake
        }
    }
    if (hit_counter >= 3) {
        if (random(0..2) == 0) {
            once_on_hit = 1
            hit_counter = 0
            Vitality multiplier = 100%
            Spirit multiplier = 100%
            target self
            use null
        }
    }
} else {
    if (last_damage == magical) {
        hit_counter += 1
        if (hit_counter >= 4) {
            once_on_hit = 0
            hit_counter = 0
            Vitality multiplier = 200%
            Spirit multiplier = 200%
            target self
            use null
        }
    }
}
return
```

## 45: Ochu

Variables: `hit_counter` = varA (auto), `once_turn` = varB (auto)


### Init

```
hit_counter = 0
hit_counter = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (group_level(enemy team) >= 1) {
    if (once_turn == 0) {
        once_turn = 1
        target all enemies
        use Ochu Dance
    } else {
        if (hit_counter >= 5) {
            hit_counter = 0
            target all enemies
            use Earthquake
        } else {
            if (random(0..2) == 0) {
                if (random(0..1) == 0) {
                    target random enemy
                    use one of Blind, Blind, Dispel
                } else {
                    target all enemies
                    use Ochu Dance
                }
            } else {
                if (random(0..1) == 0) {
                    target random enemy
                    use Physical attack
                } else {
                    target random enemy
                    use null (Ochu Poison Attack)
                }
            }
        }
    }
} else {
    if (hit_counter >= 5) {
        hit_counter = 0
        target all enemies
        use Ochu Dance
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use one of Sleep, Blind, Dispel
        } else {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
hit_counter += 1
if (group_level(enemy team) >= 1) {
    if (last_damage == magical) {
        if (status(enemy team) has Has-Magic) {
            targetStatus 00c8002e
            use Drink Magic
            draw magic
        }
    }
}
return
```

## 46: Adamantoise


### Turn

```
if (status(self) has Confuse) {
    target self
    use one of Shell, Protect, line 253
    return
}
if (random(0..1) == 0) {
    return
} else {
    if (group_level(enemy team) == 2) {
        if (random(0..3) == 0) {
            target all enemies
            use Sand Storm
            return
        } else {
            if (random(0..2) == 0) {
                if (status(ally team) lacks Shell) {
                    targetStatus 00c90316
                    use Shell
                    return
                } else {
                    if (status(ally team) lacks Protect) {
                        targetStatus 00c90315
                        use Protect
                        return
                    } else {
                        target random enemy
                        use Berserk
                        return
                    }
                }
            }
        }
    } else {
        if (group_level(enemy team) == 1) {
            if (random(0..3) == 0) {
                target all enemies
                use Sand Storm
                return
            } else {
                if (random(0..2) == 0) {
                    if (status(ally team) lacks Shell) {
                        targetStatus 00c90316
                        use Shell
                        return
                    } else {
                        if (status(ally team) lacks Protect) {
                            targetStatus 00c90315
                            use Protect
                            return
                        } else {
                            target random enemy
                            use Berserk
                            return
                        }
                    }
                }
            }
        }
    }
    if (random(0..2) == 0) {
        target all allies
        use White Wind
    } else {
        target random enemy
        use one of Physical attack, Physical attack, null
    }
}
return
```

## 47: Chimera


### Turn

```
if (random(0..2) == 0) {
    return
}
if (random(0..3) == 0) {
    target random enemy
    use Physical attack
} else {
    if (random(0..2) == 0) {
        target all enemies
        use Aqua Breath
    } else {
        if (random(0..1) == 0) {
            target random enemy
            use one of Break/Berserk/Confuse, Stop, Dispel
        } else {
            if (group_level(enemy team) == 2) {
                if (random(0..1) == 0) {
                    target random enemy
                    use Thundara/Thundaga
                } else {
                    target all enemies
                    use Aero/Tornado
                }
            } else {
                if (random(0..1) == 0) {
                    target random enemy
                    use Thundara/Thundaga
                } else {
                    target random enemy
                    use Aero/Tornado
                }
            }
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    if (group_level(enemy team) == 2) {
        if (random(0..2) == 0) {
            target last attacker
            use Physical attack
        }
    }
}
return
```

## 48: Malboro

Variables: `once_turn` = varA (auto)


### Init

```
once_turn = 0
return
```

### Turn

```
if (once_turn == 0) {
    once_turn = 1
    target all enemies
    use Bad Breath
} else {
    if (random(0..2) != 0) {
        return
    } else {
        if (group_level(enemy team) >= 1) {
            if (status(enemy team) has Poison) {
                if (status(enemy team) has Slow) {
                    if (random(0..2) == 0) {
                        target all enemies
                        use Eerie Sound Wave
                    } else {
                        target random enemy
                        use Dissolving Acid
                    }
                } else {
                    if (random(0..2) == 0) {
                        target all enemies
                        use Bad Breath
                    } else {
                        if (random(0..2) == 0) {
                            target all enemies
                            use Eerie Sound Wave
                        } else {
                            target random enemy
                            use Dissolving Acid
                        }
                    }
                }
            } else {
                if (random(0..2) == 0) {
                    target all enemies
                    use Bad Breath
                } else {
                    if (random(0..2) == 0) {
                        target all enemies
                        use Eerie Sound Wave
                    } else {
                        target random enemy
                        use Dissolving Acid
                    }
                }
            }
        } else {
            if (random(0..2) == 0) {
                target all enemies
                use Eerie Sound Wave
            } else {
                target random enemy
                use Dissolving Acid
            }
        }
    }
}
return
```

## 49: Iron Giant

Variables: `once_turn` = varA (auto)


### Init

```
once_turn = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (once_turn == 0) {
    if (HP%(self) < 50) {
        if (group_level(enemy team) == 2) {
            once_turn = 1
            target self
            use Mighty Guard
        } else {
            if (random(0..2) == 0) {
                target all enemies
                use Grand Sword
            } else {
                target random enemy
                use null
            }
        }
    } else {
        if (group_level(enemy team) >= 1) {
            if (random(0..2) == 0) {
                target all enemies
                use Grand Sword
            } else {
                target random enemy
                use null
            }
        } else {
            target random enemy
            use null
        }
    }
} else {
    if (group_level(enemy team) >= 1) {
        if (random(0..2) == 0) {
            target all enemies
            use Grand Sword
        } else {
            target random enemy
            use null
        }
    } else {
        target random enemy
        use null
    }
}
return
```

## 50: Behemoth

Variables: `once_turn` = varA (auto)


### Turn

```
if (random(0..2) == 0) {
    return
}
if (group_level(enemy team) == 0) {
    if (random(0..2) == 0) {
        if (random(0..2) == 0) {
            target all enemies
            use Tornado
        } else {
            target random enemy
            use Thundaga
        }
    } else {
        target random enemy
        use Physical attack
    }
} else {
    if (HP%(self) < 30) {
        if (once_turn == 0) {
            once_turn = 1
            target all allies
            use Mighty Guard
            return
        }
    }
    if (random(0..2) == 0) {
        target all enemies
        use Tornado
    } else {
        target random enemy
        use one of Physical attack, Physical attack, Assault Horn
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (last_damage == physical) {
    if (group_level(enemy team) >= 1) {
        if (random(0..2) == 0) {
            target random enemy each hit
            use Meteor
        }
    }
}
return
```

### Death

```
if (status(self) lacks Confuse) {
    if (status(self) lacks Petrify) {
        if (status(self) lacks Sleep) {
            if (status(self) lacks Stop) {
                if (status(self) lacks Berserk) {
                    if (group_level(enemy team) == 2) {
                        if (random(0..2) == 0) {
                            target random enemy
                            use Flare
                        }
                    }
                }
            }
        }
    }
}
die
return
```

## 51: T-Rexaur

Variables: `opening_roar_done` = varA (named)


### Init

```
if (save.tutorial_t_rexaur_seen == 0) {
    if (battle.tutorial_shown_this_battle == 0) {
        if (alive_count(enemy team) == 2) {
            if (status(enemy team) lacks Death) {
                if (alive(entity 0)) {
                    if (alive(entity 3)) {
                        battle.tutorial_shown_this_battle = 1
                        save.tutorial_t_rexaur_seen = 1
                        print+lock '{Quistis} “T-Rexaur!!!”'
                        print+lock '“{Squall}, be careful!”'
                        print+lock "“Sometimes it's better to run!”"
                        waitText 03
                    }
                }
            }
        }
    }
}
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (opening_roar_done == 0) {
    target all enemies
    use null
    opening_roar_done = 1
} else {
    if (random(0..2) == 0) {
        if (group_level(enemy team) >= 1) {
            target all enemies
            use null
        }
    } else {
        target random enemy
        use Physical attack
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (last_damage == magical) {
    if (group_level(enemy team) == 2) {
        target last attacker
        use null
    }
}
return
```

## 52: Ruby Dragon


### Turn

```
if (random(0..2) == 0) {
    return
}
if (alive_count(enemy team) == 3) {
    if (group_level(enemy team) == 2) {
        if (random(0..2) == 0) {
            target all enemies
            use Breath
        } else {
            if (random(0..1) == 0) {
                target random enemy each hit
                use Meteor
            } else {
                target random enemy
                use Firaga
            }
        }
    } else {
        if (group_level(enemy team) == 1) {
            if (random(0..2) == 0) {
                target all enemies
                use Breath
            } else {
                target random enemy
                use one of Physical attack, Physical attack, Fira
            }
        } else {
            target random enemy
            use one of Physical attack, Physical attack, Fira
        }
    }
} else {
    if (group_level(enemy team) == 2) {
        if (status(enemy team) has Reflect) {
            if (status(ally team) has Reflect) {
                targetStatus 00c90017
                use one of Firaga, Flare, Demi
            } else {
                target self
                use Reflect
            }
        } else {
            target random enemy
            use one of Physical attack, Fira, Aero
        }
    } else {
        if (group_level(enemy team) == 2) {
            target random enemy
            use one of Physical attack, Physical attack, Fira
        } else {
            target random enemy
            use Physical attack
        }
    }
}
return
```

## 53: Grendel


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (alive_count(ally team) == 1) {
    if (random(0..2) == 0) {
        target random enemy
        use Tail Blade
    } else {
        if (group_level(enemy team) >= 1) {
            target all enemies
            use Breath
        } else {
            target random enemy
            use one of Tail Blade, Thunder, Thunder
        }
    }
} else {
    target random enemy
    use one of Physical attack, Physical attack, null
}
return
```

### Counter

```
if (status(self) has Confuse) {
    if (random(0..2) == 0) {
        target last attacker
        use null
    }
}
return
```

## 54: Vysage

Variables: `once_death` = varA (auto)


### Turn

```
if (random(0..2) == 0) {
    return
}
if (alive(entity 55)) {
    if (alive(entity 56)) {
        if (group_level(enemy team) == 2) {
            if (random(0..1) == 0) {
                target random enemy
                use Curse
                return
            } else {
                if (random(0..1) == 0) {
                    target random enemy
                    use null
                    return
                }
            }
        } else {
            if (group_level(enemy team) >= 1) {
                if (random(0..1) == 0) {
                    target random enemy
                    use null
                    return
                }
            }
        }
    }
}
if (status(enemy team) has Protect) {
    if (random(0..2) == 0) {
        targetStatus 00c80015
        use Dispel
        return
    }
}
if (status(enemy team) has Shell) {
    if (random(0..2) == 0) {
        targetStatus 00c80016
        use Dispel
        return
    }
}
if (alive(entity 55)) {
    if (status(tgt55) has Silence) {
        if (group_level(enemy team) >= 1) {
            targetStatus 00370004
            use Esuna
            return
        }
    }
}
if (group_level(enemy team) >= 1) {
    if (random(0..1) == 0) {
        if (alive(entity 56)) {
            if (status(tgt56) lacks Protect) {
                targetStatus 00380315
                use Protect
                return
            } else {
                if (status(tgt56) lacks Shell) {
                    targetStatus 00380316
                    use Shell
                    return
                }
            }
        }
    }
}
if (group_level(enemy team) >= 1) {
    if (random(0..1) == 0) {
        if (alive(entity 55)) {
            if (status(tgt55) lacks Protect) {
                targetStatus 00370315
                use Protect
                return
            } else {
                if (status(tgt55) lacks Shell) {
                    targetStatus 00370316
                    use Shell
                    return
                }
            }
        }
    }
}
if (random(0..2) == 0) {
    target random enemy
    use Stare
} else {
    if (random(0..1) == 0) {
        target all enemies
        use Sigh
    } else {
        if (group_level(enemy team) == 2) {
            target all enemies
            use Tornado
        } else {
            if (group_level(enemy team) == 1) {
                target random enemy
                use Aero
            }
        }
    }
}
return
```

### Death

```
if (once_death == 0) {
    once_death = 1
    if (combat_scene == 180 /*Funguar*/) {
        if (battle.scene180_trio_death_count == 2) {
            die
            activate
            enter 3
        } else {
            battle.scene180_trio_death_count += 1
            die
        }
    } else {
        die
    }
}
return
```

## 55: Cactuar


### Turn

```
if (random(0..2) != 0) {
    target self
    use null
    print 'Escaped...'
} else {
    if (random(0..1) == 0) {
        return
    } else {
        target random enemy
        use one of Physical attack, 1000 Needles, line 253
    }
}
return
```

## 56: Tonberry

Variables: `turn_counter` = varA (auto)


### Init

```
turn_counter = 0
return
```

### Turn

```
if (turn_counter <= 4) {
    if (random(0..2) == 0) {
        return
    } else {
        turn_counter += 1
        target self
        use null
    }
} else {
    if (random(0..2) == 0) {
        return
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use null
            print 'Tonberry fell over...'
        } else {
            target random enemy
            use Chef's Knife
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    if (turn_counter <= 1) {
        if (random(0..2) == 0) {
            target last attacker
            use Everyone's Grudge
        }
    }
} else {
    if (last_damage == magical) {
        if (turn_counter <= 1) {
            if (random(0..2) == 0) {
                target last attacker
                use Everyone's Grudge
            }
        }
    }
}
return
```

### Death

```
save.tonberry_kill_count += 1
die
if (combat_scene == 236 /*Tonberry*/) {
    if (save.tonberry_kill_count >= 20) {
        if (save.tonberry_king_defeated == 0) {
            activate
            enter 0
            return
        }
    }
}
if (combat_scene == 237 /*Tonberry*/) {
    if (save.tonberry_kill_count >= 50) {
        if (save.tonberry_king_defeated == 0) {
            activate
            enter 0
            return
        }
    }
}
return
```

## 57: Torama

Variables: `once_turn` = varA (auto)


### Init

```
once_turn = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (once_turn == 0) {
    if (group_level(enemy team) >= 1) {
        if (HP%(self) < 50) {
            target self
            use null
            once_turn = 1
        } else {
            if (group_level(enemy team) == 2) {
                if (status(ally team) has Blind) {
                    targetStatus 00c90003
                    use Esuna
                } else {
                    if (status(ally team) has Stop) {
                        targetStatus 00c90013
                        use Esuna
                    } else {
                        if (random(0..2) == 0) {
                            target random enemy each hit
                            use Meteor
                        } else {
                            if (random(0..1) == 0) {
                                target random enemy
                                use Holy
                            } else {
                                target all enemies
                                use LV5 Death
                            }
                        }
                    }
                }
            } else {
                target random enemy
                use one of Demi, Aero, Death
            }
        }
    } else {
        target random enemy
        use one of Confuse, Thunder, Bio
    }
} else {
    if (random(0..1) == 0) {
        if (status(enemy team) lacks HP<50%) {
            if (random(0..1) == 0) {
                target random enemy
                use Blaster
            } else {
                target random enemy
                use Blaster
            }
        } else {
            target random enemy
            use Physical attack
        }
    } else {
        target random enemy
        use Physical attack
    }
}
return
```

## 58: Funguar

Variables: `turn_counter` = varA (auto)


### Turn

```
if (random(0..2) == 0) {
    return
}
turn_counter = 0
if (status(self) has Confuse) {
    target random non-self ally
    use Confuse
    return
}
if (any_enemy_gender == male) {
    turn_counter += 1
}
if (any_enemy_gender == female) {
    turn_counter += 2
}
if (turn_counter == 1) {
    target random enemy
    use one of Sleep, Fire/Demi, Fire/Bio
} else {
    if (turn_counter == 2) {
        target random enemy
        use null (Funguar Laser)
    } else {
        if (random(0..1) == 0) {
            targetStatus 00c800c8
            use one of Sleep, Sleep, line 253
        } else {
            targetStatus 00c800c9
            use null (Funguar Laser)
        }
    }
}
return
```

## 59: Imp

Variables: `once_turn` = varA (auto), `turn_counter` = varB (auto)


### Init

```
once_turn = 0
turn_counter = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(enemy team) has Reflect) {
    if (random(0..2) == 0) {
        targetStatus 00c80017
        use Dispel
        return
    }
}
if (status(enemy team) has Protect) {
    if (random(0..2) == 0) {
        targetStatus 00c80015
        use Dispel
        return
    }
}
if (status(enemy team) has Shell) {
    if (random(0..2) == 0) {
        targetStatus 00c80016
        use Dispel
        return
    }
}
if (once_turn == 0) {
    if (turn_counter >= 2) {
        if (random(0..1) == 0) {
            once_turn = 1
            target self
            use null
        }
    }
}
if (once_turn == 0) {
    if (random(0..2) == 0) {
        turn_counter += 1
        target random enemy
        use Berserk
    } else {
        if (random(0..1) == 0) {
            target random enemy
            use one of Confuse, Silence, Blind
        } else {
            target random enemy
            use one of Thundaga, Firaga, Blizzaga
        }
    }
} else {
    if (random(0..1) == 0) {
        target random enemy
        use one of Physical attack, Berserk, Blind
    } else {
        if (random(0..2) == 0) {
            target random enemy each hit
            use Meteor
        } else {
            target all enemies
            use one of Tornado, Tornado, Quake
        }
    }
}
return
```

### Death

```
if (group_level(enemy team) >= 1) {
    if (random(0..2) == 0) {
        target last attacker
        use Holy
    }
}
die
return
```

## 60: PuPu

Variables: `hit_counter` = varB (auto), `phase` = varC (auto)


### Init

```
varA = 0
hit_counter = 0
phase = 0
return
```

### Turn

```
if (phase == 0) {
    phase = 1
    target self
    use null
} else {
    if (phase == 1) {
        phase = 2
    } else {
        phase = 0
    }
}
return
```

### Counter

```
if (varA == 1) {
    varA = 0
    hit_counter += 1
    if (hit_counter >= 5) {
        add card drop PuPu
        target self
        use null
        die
    } else {
        target self
        use null
    }
}
return
```

### Death

```
add item drop Accelerator (non-battle-item, cross-confirmed via mngrp+mwepon)
die
return
```

### Pre-hit

```
if (last_command == Item) {
    if (last_action_id == 9) {
        varA = 1
    }
}
return
```

## 61: Ifrit

Variables: `hits_taken` = varA (named), `fire_ineffective_line_done` = varB (named), `half_hp_line_done` = varC (named), `shiva_reaction_done` = varD (named), `strong_punch_done` = varE (named)


### Init

```
hits_taken = 0
fire_ineffective_line_done = 0
half_hp_line_done = 0
shiva_reaction_done = 0
return
```

### Turn

```
if (HP%(self) < 50) {
    if (half_hp_line_done == 0) {
        half_hp_line_done = 1
        target self
        use Ifrit HP < 50%
        return
    }
}
if (hits_taken >= 5) {
    hits_taken = 0
    target random enemy
    if (strong_punch_done != 0) {
        use Ifrit Weak Punch
    } else {
        strong_punch_done = 1
        print '“Impudent humans!”'
        use Ifrit Strong Punch
    }
} else {
    target random enemy
    use one of Fire, Fire, line 253
}
return
```

### Counter

```
hits_taken += 1
if (last_command == GF) {
    if (last_action_id == 65) {
        if (shiva_reaction_done == 0) {
            shiva_reaction_done = 1
            target self
            use Ifrit Shiva Summoned 1st time
            return
        }
    }
}
if (last_command == Magic) {
    if (last_element == Fire) {
        if (fire_ineffective_line_done == 0) {
            fire_ineffective_line_done = 1
            if (attacker(left=1) == 0) {
                print+lock '{Squall} “Fire magic ineffective?”'
            } else {
                print+lock "{Quistis} “Fire won't work.”"
            }
        }
    }
}
return
```

### Death

```
if (last_action_id == 65) {
    target self
    use Ifrit Defeated by Shiva
} else {
    target self
    use Ifrit Death
}
die
return
```

## 62: Minotaur

Variables: `defeated` = varA (named)


### Turn

```
if (defeated != 0) {
    return
}
if (status(self) lacks Float) {
    target self
    use Minotaur Earth Regen
}
if (alive_count(ally team) == 1) {
    if (random(0..2) == 0) {
        target random enemy
        use Physical attack
    } else {
        target all enemies
        use Mower
    }
} else {
    if (random(0..2) == 0) {
        target all enemies
        use Mower
    } else {
        target random enemy
        use Physical attack
    }
}
return
```

### Counter

```
if (alive_count(ally team) == 1) {
} else {
    battle_var[96] += 1
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    if (alive_count(ally team) == 1) {
        target self
        use Minotaur Death v2
    } else {
        battle_var[96] = 0
        target self
        use Minotaur Death v1
    }
}
return
```

## 63: Sacred

Variables: `defeated` = varA (named)


### Init

```
battle_var[96] = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (status(self) lacks Float) {
    target self
    use Sacred Earth Regen
}
if (random(0..2) == 0) {
    return
}
if (combat_scene == 189 /*Sacred*/) {
    if (HP%(self) < 50) {
        target self
        use Sacred Death (1st Battle)
    } else {
        if (random(0..2) == 0) {
            return
        } else {
            target random enemy
            use Physical attack
        }
    }
} else {
    if (battle_var[96] >= 11) {
        battle_var[96] = 0
        target all enemies
        use Mad Cow Special
    } else {
        if (random(0..2) == 0) {
            return
        } else {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
if (alive_count(ally team) == 1) {
} else {
    battle_var[96] += 1
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    if (combat_scene == 189 /*Sacred*/) {
        target self
        use Sacred Death (1st Battle)
    } else {
        if (alive_count(ally team) == 1) {
            target self
            use Sacred Death v2 (2nd battle)
        } else {
            battle_var[96] = 0
            target self
            use Sacred Death v1 (2nd battle)
        }
    }
}
return
```

## 64: Base Leader

Variables: `taunt_message_done` = varA (named), `double_attack_step` = varB (named)


### Init

```
battle_var[96] = 0
battle_var[97] = 0
battle_var[98] = 0
battle_var[99] = 0
taunt_message_done = 0
double_attack_step = 0
print+lock '“Time for us to get serious!”'
waitText 01
return
```

### Turn

```
if (battle_var[96] == 1) {
    battle_var[96] = 0
    target self
    use Base Leader Message 1
    target random enemy
    use Arm Slash
    return
}
if (battle_var[97] == 1) {
    if (double_attack_step == 0) {
        double_attack_step = 1
        targetStatus 00c800cc
        use Physical attack
        return
    } else {
        battle_var[97] = 0
        double_attack_step = 0
        targetStatus 00c800cc
        use Physical attack
        return
    }
} else {
    if (battle_var[97] == 2) {
        battle_var[97] = 0
        target random enemy
        use Thundara
        return
    } else {
        if (alive_count(ally team) != 1) {
            if (random(0..2) == 0) {
                if (taunt_message_done == 0) {
                    taunt_message_done = 1
                    target self
                    use Base Leader Message 2
                    return
                } else {
                    if (random(0..1) == 0) {
                        battle_var[97] = 1
                        target self
                        use Base Leader Message 3
                        targetStatus 00c800cc
                        use Physical attack
                        return
                    } else {
                        battle_var[97] = 2
                        target self
                        use Base Leader Message 4
                        target random enemy
                        use Thundara
                        return
                    }
                }
            }
        }
    }
}
if (status(ally team) has Confuse) {
    if (random(0..1) == 0) {
        targetStatus 00c9001e
        use Remedy
        return
    }
}
if (status(ally team) has Silence) {
    if (random(0..1) == 0) {
        targetStatus 00c90004
        use Remedy
        return
    }
}
if (random(0..2) == 0) {
    if (status(ally team) has HP<50%) {
        targetStatus 00c90009
        use one of Cura, Protect, Shell
        return
    }
}
target random enemy
use one of Physical attack, Physical attack, Confuse
return
```

### Death

```
battle_var[99] = 1
die
return
```

## 65: Cerberus

Variables: `triple_active` = varA (named), `triple_cast_pending` = varB (named), `low_hp_line_done` = varC (named)


### Init

```
triple_active = 0
triple_cast_pending = 0
low_hp_line_done = 0
if (alive(entity 3)) {
    print+lock "{Quistis} “I don't think G Garden uses GF.”"
    if (alive(entity 0)) {
        print+lock "{Squall} “Ahh... Let's just take it.”"
    } else {
        if (alive(entity 1)) {
            print+lock "{Zell} “This baby's ours!”"
        } else {
            if (alive(entity 5)) {
                print+lock "{Selphie} “We're gonna take it...!”"
            } else {
                if (alive(entity 2)) {
                    print+lock '{Irvine} “We should just take it.”'
                } else {
                    if (alive(entity 4)) {
                        print+lock '{Rinoa} “Mr. GF, give us your power!”'
                    }
                }
            }
        }
    }
} else {
    if (alive(entity 1)) {
        print+lock '{Zell} “Do people here know GF?”'
        if (alive(entity 0)) {
            print+lock "{Squall} “Ahh... Let's just take it.”"
        } else {
            if (alive(entity 3)) {
                print+lock "{Quistis} “Let's take it!”"
            } else {
                if (alive(entity 5)) {
                    print+lock "{Selphie} “We're gonna take it...!”"
                } else {
                    if (alive(entity 2)) {
                        print+lock '{Irvine} “We should just take it.”'
                    } else {
                        if (alive(entity 4)) {
                            print+lock '{Rinoa} “Mr. GF, give us your power!”'
                        }
                    }
                }
            }
        }
    } else {
        if (alive(entity 5)) {
            print+lock '{Selphie} “Is this a GF!?”'
            if (alive(entity 0)) {
                print+lock "{Squall} “Ahh... Let's just take it.”"
            } else {
                if (alive(entity 3)) {
                    print+lock "{Quistis} “Let's take it!”"
                } else {
                    if (alive(entity 1)) {
                        print+lock "{Zell} “This baby's ours!”"
                    } else {
                        if (alive(entity 2)) {
                            print+lock '{Irvine} “We should just take it.”'
                        } else {
                            if (alive(entity 4)) {
                                print+lock '{Rinoa} “Mr. GF, give us your power!”'
                            }
                        }
                    }
                }
            }
        } else {
            if (alive(entity 2)) {
                print+lock '{Irvine} “Never knew about this one.”'
                if (alive(entity 0)) {
                    print+lock "{Squall} “Ahh... Let's just take it.”"
                } else {
                    if (alive(entity 3)) {
                        print+lock "{Quistis} “Let's take it!”"
                    } else {
                        if (alive(entity 1)) {
                            print+lock "{Zell} “This baby's ours!”"
                        } else {
                            if (alive(entity 5)) {
                                print+lock "{Selphie} “We're gonna take it...!”"
                            } else {
                                if (alive(entity 4)) {
                                    print+lock '{Rinoa} “Mr. GF, give us your power!”'
                                }
                            }
                        }
                    }
                }
            } else {
                if (alive(entity 0)) {
                    print+lock '{Squall} “G Garden uses GF, too?”'
                    if (alive(entity 3)) {
                        print+lock "{Quistis} “Let's take it!”"
                    } else {
                        if (alive(entity 1)) {
                            print+lock "{Zell} “This baby's ours!”"
                        } else {
                            if (alive(entity 5)) {
                                print+lock "{Selphie} “We're gonna take it...!”"
                            } else {
                                if (alive(entity 2)) {
                                    print+lock '{Irvine} “We should just take it.”'
                                } else {
                                    if (alive(entity 4)) {
                                        print+lock '{Rinoa} “Mr. GF, give us your power!”'
                                    }
                                }
                            }
                        }
                    }
                } else {
                    print+lock '{Rinoa} “Could this be a GF?”'
                    if (alive(entity 0)) {
                        print+lock "{Squall} “Ahh... Let's just take it.”"
                    } else {
                        if (alive(entity 3)) {
                            print+lock "{Quistis} “Let's take it!”"
                        } else {
                            if (alive(entity 1)) {
                                print+lock "{Zell} “This baby's ours!”"
                            } else {
                                if (alive(entity 5)) {
                                    print+lock "{Selphie} “We're gonna take it...!”"
                                } else {
                                    if (alive(entity 2)) {
                                        print+lock '{Irvine} “We should just take it.”'
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
print+lock 'Cerberus “...PRETTY CONFIDENT.”'
print+lock "Cerberus “LET'S SEE HOW YOU DO.”"
waitText 04
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (triple_active == 0) {
    if (random(0..2) == 0) {
        target random enemy
        use Physical attack
    } else {
        if (random(0..2) != 0) {
            if (random(0..2) == 0) {
                target all enemies
                use Quake
            } else {
                if (random(0..1) == 0) {
                    target all enemies
                    use Tornado
                } else {
                    target random enemy
                    use Berserk
                }
            }
        } else {
            target self
            use Triple
            triple_cast_pending = 1
        }
    }
} else {
    if (all(enemy team) have Reflect) {
        if (random(0..2) == 0) {
            target random enemy
            use null
            return
        } else {
            target random enemy
            use Dispel
            if (alive_count(enemy team) != 0) {
                target random enemy
                use Dispel
            }
            if (alive_count(enemy team) != 0) {
                target random enemy
                use Dispel
            }
            return
        }
    }
    if (random(0..3) == 0) {
        if (random(0..2) == 0) {
            target random enemy
            use Dispel
            if (alive_count(enemy team) != 0) {
                target random enemy
                use Dispel
            }
            if (alive_count(enemy team) != 0) {
                target random enemy
                use Dispel
            }
            return
        } else {
            if (random(0..1) == 0) {
                target random enemy
                use Silence
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Silence
                }
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Silence
                }
            } else {
                target random enemy
                use Blind
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Blind
                }
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Blind
                }
            }
        }
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use null
        } else {
            if (random(0..2) == 0) {
                target random enemy
                use Aero
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Aero
                }
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Aero
                }
            } else {
                target random enemy
                use Thundaga
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Thundaga
                }
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Thundaga
                }
            }
        }
    }
}
return
```

### Counter

```
if (last_command == Magic) {
    if (last_action_id == 34) {
        if (triple_active != 1) {
            target self
            use Cerberus Counter 1
            triple_active = 1
        }
    } else {
        if (last_action_id == 28) {
            target self
            use Cerberus Counter 2
            triple_active = 0
        }
    }
} else {
    if (triple_cast_pending == 1) {
        target self
        use Cerberus Counter 1
        triple_active = 1
        triple_cast_pending = 0
    }
}
if (HP%(self) < 20) {
    if (low_hp_line_done == 0) {
        low_hp_line_done = 1
        target self
        use null
    }
}
return
```

### Death

```
target self
use null
return
```

## 66: Diablos


### Init

```
print+lock '“Who dares disturb my sleep?”'
waitText 01
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (HP%(self) < 50) {
    if (random(0..2) != 0) {
        target random enemy
        use Physical attack
    } else {
        target all enemies
        use Gravija
    }
} else {
    if (random(0..3) != 0) {
        target random enemy
        use one of Physical attack, Demi, Demi
    } else {
        target all enemies
        use Gravija
    }
}
return
```

### Counter

```
if (last_command == Magic) {
    if (last_action_id == 13) {
        target last attacker
        use Curaga
    } else {
        if (last_action_id == 50) {
            return
        } else {
            target last attacker
            use Demi
        }
    }
}
return
```

### Death

```
print+lock '“Too much sleep... Too weak...”'
give GF 5
die
return
```

## 67: Bahamut

Variables: `turn_counter` = varA (named), `unused` = varB (named), `intro_dialog_done` = varC (named)


### Init

```
turn_counter = 0
unused = 0
intro_dialog_done = 0
fill ATB
return
```

### Turn

```
if (intro_dialog_done == 0) {
    intro_dialog_done = 1
    if (alive(entity 0)) {
        target self
        use Bahamut / Squall Dialog
    } else {
        if (alive(entity 1)) {
            target self
            use Bahamut / Zell Dialog
        } else {
            if (alive(entity 3)) {
                target self
                use Bahamut / Quistis Dialog
            } else {
                if (alive(entity 5)) {
                    target self
                    use Bahamut / Selphie Dialog
                } else {
                    if (alive(entity 2)) {
                        target self
                        use Bahamut / Irvine Dialog
                    } else {
                        if (alive(entity 4)) {
                            target self
                            use Bahamut / Rinoa Dialog
                        }
                    }
                }
            }
        }
    }
    return
}
if (turn_counter <= 30) {
    turn_counter += 1
}
if (random(0..2) == 0) {
    return
}
if (turn_counter >= 25) {
    if (status(enemy team) lacks Stop) {
        if (random(0..2) == 0) {
            targetStatus 00c80313
            use Stop
            return
        }
    }
}
if (turn_counter <= 3) {
    if (random(0..2) == 0) {
        target random enemy
        use Physical attack
    } else {
        targetStatus 00c800cc
        use Physical attack
    }
} else {
    if (turn_counter <= 6) {
        if (random(0..1) == 0) {
            if (random(0..2) == 0) {
                target random enemy
                use Physical attack
            } else {
                targetStatus 00c800cc
                use Physical attack
            }
        } else {
            targetStatus 00c800e7
            use Thundaga
        }
    } else {
        if (random(0..2) == 0) {
            targetStatus 00c800d6
            use Physical attack
        } else {
            if (random(0..2) == 0) {
                target all enemies
                use Mega Flare
            } else {
                if (random(0..1) == 0) {
                    target all enemies
                    use Tornado
                } else {
                    targetStatus 00c800e7
                    use Thundaga
                }
            }
        }
    }
}
return
```

### Death

```
target self
use Bahamut Death
return
```

## 68: NORG Pod

Variables: `turn_counter` = varA (named), `bujuru_line_done` = varB (named), `pod_opened` = varC (named)


### Init

```
print 'NORG “BLUE-YELLOW-RED.”'
print 'NORG “LOTS-OF-MAGIC-WHEN-RED!”'
print 'NORG “AS-LONG-AS-COLOR-STAYS,”'
print 'NORG “I-WILL-ATTACK-SeeD-WITH-MAGIC!”'
waitText 04
return
```

### Turn

```
if (pod_opened != 0) {
    return
}
if (pod_opened == 0) {
    turn_counter += 1
    if (bujuru_line_done == 0) {
        if (turn_counter == 3) {
            print 'NORG “Bujurururu...”'
            bujuru_line_done = 1
        }
    }
} else {
    if (battle_var[96] == 1) {
        die
    }
    fill ATB
}
return
```

### Death

```
if (pod_opened == 0) {
    pod_opened = 1
    target self
    use NORG Pod Opening
    become untargetable
    recover to full HP
    fill ATB
}
return
```

## 69: Garden Faculty


### Init

```
if (combat_scene == 65 /*Geezard*/) {
    print '“Seize them!”'
    target self
    use Do Nothing?
    return
}
if (combat_scene == 66 /*Geezard*/) {
    print '“NORG is the true ruler of the Garden!”'
    target self
    use Do Nothing?
    return
}
if (combat_scene == 67 /*Blood Soul*/) {
    print '“Now, attack!”'
    target self
    use Do Nothing?
    return
}
if (combat_scene == 68 /*Buel+Blood Soul*/) {
    print '“Stall them.”'
    target self
    use Do Nothing?
    return
}
if (combat_scene == 69 /*Geezard*/) {
    print '“This Garden belongs to NORG!”'
    target self
    use Do Nothing?
    return
}
if (combat_scene == 70 /*Buel*/) {
    print '“More SeeDs here!?”'
    target self
    use Do Nothing?
    return
}
if (combat_scene == 71 /*Tri-Face*/) {
    print "“You're siding with the headmaster!?”"
    target self
    use Do Nothing?
    return
}
if (combat_scene == 72 /*Geezard+Blood Soul*/) {
    print '“Those opposed to NORG must die!”'
    target self
    use Do Nothing?
    return
}
if (combat_scene == 73 /*Blood Soul+Buel*/) {
    print '“Face the wrath of this monster!”'
    target self
    use Do Nothing?
    return
}
return
```

## 70: Odin

Variables: `defeated` = varA (named)


### Init

```
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (countdown == 0) {
    target all enemies
    use Zantetsuken
} else {
    fill ATB
}
return
```

### Counter

```
if (countdown == 0) {
    target all enemies
    use Zantetsuken
} else {
    fill ATB
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
}
return
```

## 71: G-Soldier


### Init

```
if (combat_scene == 164 /*BGH251F2*/) {
    if (battle_var[97] == 0) {
        battle_var[97] = 1
        enter 2
    } else {
        target self
        specialAction 248
    }
} else {
    battle_var[96] = 0
    if (combat_scene == 1 /*G-Soldier*/) {
        if (battle_var[96] == 0) {
            print "“They're Dollet reinforcements?”"
            battle_var[96] = 1
        }
    }
}
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
battle_var[96] += 1
if (combat_scene != 4 /*G-Soldier*/) {
    target random enemy
    use one of Physical attack, Physical attack, Fire/Fira
} else {
    if (battle_var[96] == 1) {
        print "“Look out, it's SeeD!”"
    } else {
        if (battle_var[96] == 3) {
            print '“They still look like kids!”'
        } else {
            if (battle_var[96] == 4) {
                print '“Elite forces from Garden?”'
            } else {
                target random enemy
                use one of Physical attack, Physical attack, Fire/Fira
            }
        }
    }
}
return
```

## 72: Elite Soldier

Variables: `entry_anim_done` = varA (named)


### Init

```
if (combat_scene == 164 /*BGH251F2*/) {
    enter 3
    fill ATB
} else {
    if (combat_scene == 161 /*GIM52A+Elite Soldier*/) {
        print+lock "“You're not goin' anywhere!”"
        Vitality multiplier = 200%
        Spirit multiplier = 200%
        Speed multiplier = 150%
    }
}
return
```

### Turn

```
if (combat_scene == 164 /*BGH251F2*/) {
    if (entry_anim_done == 0) {
        if (alive_count(ally team) == 3) {
            entry_anim_done = 1
            target self
            use null (Elite Soldier BGH251F2 ?)
            return
        }
    }
}
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (alive(entity 23)) {
    if (status(enemy team) lacks VIT0) {
        targetStatus 00c80328
        use Meltdown
        return
    }
}
if (alive(entity 17)) {
    if (alive(entity 87)) {
        target random enemy
        use one of Physical attack, Physical attack, Arm Slash
    } else {
        if (HP%(tgt87) < 50) {
            targetStatus 00570009
            use one of Cure/Cura/Curaga, Cure/Cura/Curaga, Protect/Shell/Reflect
        } else {
            target random enemy
            use one of Physical attack, Physical attack, Arm Slash
        }
    }
} else {
    if (random(0..2) == 0) {
        if (status(enemy team) lacks VIT0) {
            targetStatus 00c80328
            use Meltdown
        } else {
            target random enemy
            use Physical attack
        }
    } else {
        if (random(0..2) != 0) {
            if (status(tgt17) lacks Aura) {
                targetStatus 00110318
                use Aura
                return
            }
        }
        if (random(0..1) == 0) {
            if (status(tgt17) lacks Shell) {
                targetStatus 00110316
                use Shell
                return
            }
        }
        if (random(0..1) == 0) {
            if (status(tgt17) lacks Protect) {
                targetStatus 00110315
                use Protect
                return
            }
        }
        target random ally
        use Cure/Cura/Curaga
    }
}
return
```

## 73: Wedge


### Init

```
doNothing 01
target self
use Wedge Enter Battle
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
target random enemy
use one of Physical attack, Physical attack, Fire
return
```

### Death

```
if (battle_var[98] == 0) {
    battle_var[98] = 1
    target all allies
    specialAction 110
    leave 0
    leave 1
    enter 2
}
return
```

## 74: Biggs

Variables: `first_heal_done` = varA (named)


### Init

```
doNothing 01
print 'Biggs “Prepare for the worst, you brats!”'
first_heal_done = 0
battle_var[96] = 0
battle_var[98] = 0
return
```

### Turn

```
if (turn_count == 4) {
    if (battle_var[96] == 0) {
        enterWithAnim 1 0
        battle_var[96] = 1
        battle_var[96] = 1
    }
} else {
    if (HP%(tgt89) < 50) {
        if (first_heal_done == 0) {
            target self
            use null (Biggs before healing Wedge 1)
            target monster c0m073 (Wedge)
            use Cure
            first_heal_done = 1
        } else {
            if (random(0..2) == 0) {
                target self
                use Cure
            } else {
                target random enemy
                use one of Arm Slash, Physical attack, Physical attack
            }
        }
    } else {
        target random enemy
        use one of Thunder, Physical attack, Physical attack
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
} else {
    if (random(0..3) == 0) {
        if (attacker(left=203) != 200) {
            target last attacker
            use Arm Slash
        }
    }
}
return
```

### Death

```
if (battle_var[96] == 0) {
    battle_var[96] = 1
    enterWithAnim 1 0
    battle_var[96] = 1
    recover to full HP
} else {
    if (battle_var[98] == 0) {
        battle_var[98] = 1
        target all allies
        specialAction 110
        leave 0
        leave 1
        enter 2
    }
}
return
```

## 75: Fake President

Variables: `turn_counter` = varA (named), `amused_line_done` = varB (named), `death_handled` = varC (named), `defeated` = varD (named)


### Init

```
turn_counter = 0
amused_line_done = 0
print+lock '“YOu...fEll...FOr...iT”'
waitText 01
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
turn_counter += 1
if (turn_counter == 5) {
    print+lock '“kiLL...thE...REsisTanCE...”'
    waitText 01
} else {
    target random enemy
    use one of Physical attack, Physical attack, line 253
}
return
```

### Counter

```
if (turn_counter >= 3) {
    if (amused_line_done == 0) {
        amused_line_done = 1
        print+lock '“aMusINg... tHIs iS AmuSinG!”'
        waitText 01
    }
}
return
```

### Death

```
if (death_handled == 0) {
    death_handled = 1
    defeated = 1
    target self
    use Fake President Death
    leave 200
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 76: Guard


### Init

```
if (battle_var[96] == 0) {
    if (save.prison_biggs_fought == 0) {
        if (random(0..2) == 0) {
            battle_var[96] = 1
            print+lock '“Hey!  What are you doing!?”'
        } else {
            battle_var[96] = 1
            print+lock "“Who's there!?”"
        }
    } else {
        if (random(0..2) == 0) {
            battle_var[96] = 1
            print+lock '“SeeDs have escaped!”'
        } else {
            if (random(0..1) == 0) {
                battle_var[96] = 1
                print+lock '“Yo, I found the SeeDs!”'
            } else {
                battle_var[96] = 1
                print+lock "“SeeDs, you ain't gettin' away!”"
            }
        }
    }
}
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
target random enemy
if (save.prison_biggs_fought == 0) {
    use one of Physical attack, Physical attack, line 253
} else {
    use one of Physical attack, Physical attack, Sleep
}
return
```

## 77: NORG

Variables: `move_cycle_step` = varA (named), `tutorial_done` = varB (named), `defeated` = varC (named)


### Init

```
move_cycle_step = 0
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (tutorial_done == 0) {
    tutorial_done = 1
    target self
    use NORG Tutorial?
    return
}
move_cycle_step += 1
if (random(0..2) == 0) {
    return
} else {
    if (move_cycle_step == 1) {
        if (gf_not_yet_stolen) {
            if (random(0..2) != 0) {
                target self
                use one of Shell, Protect, line 253
            } else {
                return
            }
        } else {
            target random enemy
            use Water
        }
    } else {
        if (move_cycle_step == 2) {
            if (gf_not_yet_stolen) {
                target random enemy
                use Blizzara
            } else {
                target random enemy
                use Water
            }
        } else {
            if (move_cycle_step == 3) {
                if (gf_not_yet_stolen) {
                    target random enemy
                    use one of Slow, Silence, line 253
                } else {
                    target random enemy
                    use Water
                }
            } else {
                move_cycle_step = 0
                target random enemy
                use Psycho Blast
            }
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use NORG Death
}
return
```

## 78: Esthar Soldier


### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
target random enemy
use one of Physical attack, Physical attack, Shotgun
return
```

## 79: Esthar Soldier

Variables: `boomerang_used` = varA (named)


### Turn

```
if (random(0..2) == 0) {
    return
}
if (boomerang_used == 1) {
    target random enemy
    use Punch (Esthar Soldier)
} else {
    if (group_level(enemy team) >= 1) {
        if (random(0..4) == 0) {
            boomerang_used = 1
            Speed multiplier = 200%
            target all enemies
            use Boomerang Sword
            return
        } else {
            target random enemy
            use one of Physical attack, Shotgun, Blizzara/Demi/Death
        }
    } else {
        target random enemy
        use one of Physical attack, Shotgun, Blizzara/Demi/Death
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    if (boomerang_used == 1) {
        if (random(0..2) == 0) {
            target last attacker
            use Punch (Esthar Soldier)
        }
    }
}
return
```

### Death

```
if (combat_scene == 233 /*Esthar Soldier*/) {
    if (battle_var[96] == 1) {
        if (alive(entity 9)) {
            if (HP%(tgt9) >= 10) {
                target battle slot 9
                use Soul Crush
            }
        }
        if (alive(entity 10)) {
            if (HP%(tgt10) >= 10) {
                target battle slot 10
                use Soul Crush
            }
        }
    } else {
        battle_var[96] = 1
    }
}
die
return
```

## 80: Right Orb

Variables: `open_stage` = varA (named), `just_opened` = varB (named), `skip_next_turn` = varC (named)


### Init

```
open_stage = 0
just_opened = 0
skip_next_turn = 0
return
```

### Turn

```
recover to full HP
if (skip_next_turn == 0) {
    if (open_stage == 0) {
        if (random(0..1) == 0) {
            open_stage = 1
            just_opened = 1
            skip_next_turn = 1
            target self
            use Do Nothing?
        }
    } else {
        if (open_stage == 1) {
            if (random(0..2) == 0) {
                open_stage = 2
                just_opened = 1
                skip_next_turn = 1
                target self
                use Do Nothing?
            }
        } else {
            if (random(0..2) == 0) {
                if (status(enemy team) has Reflect) {
                    targetStatus 00c80017
                    use Dispel
                } else {
                    target random enemy
                    use one of Dispel, Silence, Slow
                }
            }
        }
    }
} else {
    skip_next_turn = 0
}
return
```

### Counter

```
recover to full HP
return
```

### Death

```
recover to full HP
return
```

### Pre-hit

```
if (just_opened == 0) {
    if (last_damage == physical) {
        if (open_stage == 2) {
            if (random(0..1) == 0) {
                setHitAnim 14
                open_stage = 1
                skip_next_turn = 1
            } else {
                setHitAnim 16
                open_stage = 0
                skip_next_turn = 1
            }
        } else {
            if (open_stage == 1) {
                setHitAnim 15
                open_stage = 0
                skip_next_turn = 1
            }
        }
    }
} else {
    just_opened = 0
}
return
```

## 81: Left Orb

Variables: `open_stage` = varA (named), `just_opened` = varB (named), `skip_next_turn` = varC (named)


### Init

```
open_stage = 0
just_opened = 0
skip_next_turn = 0
return
```

### Turn

```
recover to full HP
if (skip_next_turn == 0) {
    if (open_stage == 0) {
        if (random(0..1) == 0) {
            open_stage = 1
            just_opened = 1
            skip_next_turn = 1
            target self
            use Do Nothing?
        }
    } else {
        if (open_stage == 1) {
            if (random(0..2) == 0) {
                open_stage = 2
                just_opened = 1
                skip_next_turn = 1
                target self
                use Do Nothing?
            }
        } else {
            if (random(0..2) == 0) {
                if (random(0..2) == 0) {
                    target all enemies
                    use Tornado
                } else {
                    target random enemy
                    use one of Thundara, Fira, Bio
                }
            }
        }
    }
} else {
    skip_next_turn = 0
}
return
```

### Counter

```
recover to full HP
return
```

### Death

```
recover to full HP
return
```

### Pre-hit

```
if (just_opened == 0) {
    if (last_damage == physical) {
        if (open_stage == 2) {
            if (random(0..1) == 0) {
                setHitAnim 14
                open_stage = 1
                skip_next_turn = 1
            } else {
                setHitAnim 16
                open_stage = 0
                skip_next_turn = 1
            }
        } else {
            if (open_stage == 1) {
                setHitAnim 15
                open_stage = 0
                skip_next_turn = 1
            } else {
                return
            }
        }
    }
} else {
    just_opened = 0
}
return
```

## 83: Tonberry King

Variables: `hit_counter` = varB (auto), `defeated` = varC (auto)


### Init

```
varA = 0
hit_counter = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (random(0..2) == 0) {
    return
}
if (hit_counter >= 5) {
    hit_counter = 0
    target all enemies
    use Junk
    return
}
target random enemy
use one of Physical attack, Physical attack, It's sharp!
return
```

### Counter

```
if (last_damage == physical) {
    hit_counter += 1
} else {
    if (last_damage == magical) {
        hit_counter += 1
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    save.tonberry_king_defeated = 1
    give GF 14
    target self
    use Tonberry King Death
    print 'Tonberry joined your party!'
}
return
```

## 84: Jumbo Cactuar

Variables: `hit_counter` = varA (named), `hesitating` = varB (named)


### Init

```
hit_counter = 0
hesitating = 0
return
```

### Turn

```
if (hesitating == 0) {
    if (HP%(self) < 10) {
        hesitating = 1
        print 'Jumbo Cactuar is hesitating...'
        return
    }
}
if (random(0..2) != 0) {
    return
} else {
    if (random(0..2) == 0) {
        target all enemies
        use Ker Plunk
    } else {
        target random enemy
        use null
    }
}
return
```

### Counter

```
if (hesitating == 1) {
    if (random(0..7) == 0) {
        target self
        use null
        return
    }
}
hit_counter += 1
if (hit_counter >= 5) {
    if (random(0..2) == 0) {
        hit_counter = 0
        target last attacker
        use 10.000 Needles
    }
}
return
```

### Death

```
give GF 13
die
return
```

## 85: Seifer

Variables: `turn_counter` = varA (named), `half_hp_line_done` = varB (named), `squall_low_hp_line_done` = varC (named)


### Init

```
turn_counter = 0
half_hp_line_done = 0
squall_low_hp_line_done = 0
print+lock "Seifer “{Squall}, you're mine!”"
return
```

### Turn

```
turn_counter += 1
if (turn_counter == 4) {
    target self
    use null
    target random enemy
    use null
} else {
    if (squall_low_hp_line_done == 0) {
        if (HP%(tgt0) < 50) {
            squall_low_hp_line_done = 1
            target self
            use null
            target random enemy
            use null
        } else {
            if (random(0..2) == 0) {
                return
            } else {
                target random enemy
                use one of Seifer Physical Attack, Seifer Physical Attack, Fira
            }
        }
    } else {
        if (random(0..2) == 0) {
            return
        } else {
            target random enemy
            use one of Seifer Physical Attack, Seifer Physical Attack, Fira
        }
    }
}
return
```

### Counter

```
if (half_hp_line_done == 0) {
    if (HP%(self) < 50) {
        half_hp_line_done = 1
        target self
        use null
    }
}
return
```

### Death

```
target self
use null
return
```

## 86: Seifer

Variables: `defeated` = varA (named), `demon_slice_line_done` = varB (named), `hp40_line_done` = varC (named), `taunt_turn_counter` = varD (named)


### Init

```
print "Seifer “Let's go after them monsters!”"
defeated = 0
demon_slice_line_done = 0
hp40_line_done = 0
taunt_turn_counter = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (random(0..2) == 0) {
    return
}
if (HP%(self) < 30) {
    if (demon_slice_line_done == 1) {
        if (random(0..2) == 0) {
            if (random(0..2) == 0) {
                targetStatus 00c800e5
                use Firaga
            } else {
                target random enemy
                use Seifer Physical Attack
            }
        } else {
            if (random(0..1) == 0) {
                target random enemy
                use Demon Slice
            } else {
                if (random(0..2) != 0) {
                    target self
                    use Hi-Potion
                } else {
                    if (status(self) has Poison) {
                        if (random(0..1) == 0) {
                            target self
                            use Remedy
                            return
                        }
                    }
                    if (status(self) has Blind) {
                        if (random(0..2) == 0) {
                            target self
                            use Remedy
                            return
                        }
                    }
                    if (status(self) has Silence) {
                        if (random(0..2) == 0) {
                            target self
                            use Remedy
                            return
                        }
                    }
                    target self
                    use Hi-Potion
                }
            }
        }
    } else {
        if (random(0..2) == 0) {
            if (random(0..2) == 0) {
                targetStatus 00c800e5
                use Fira
            } else {
                target random enemy
                use Seifer Physical Attack
            }
        } else {
            if (random(0..1) == 0) {
                if (random(0..2) != 0) {
                    target self
                    use Hi-Potion
                } else {
                    if (status(self) has Poison) {
                        if (random(0..1) == 0) {
                            target self
                            use Remedy
                            return
                        }
                    }
                    if (status(self) has Blind) {
                        if (random(0..2) == 0) {
                            target self
                            use Remedy
                            return
                        }
                    }
                    if (status(self) has Silence) {
                        if (random(0..2) == 0) {
                            target self
                            use Remedy
                            return
                        }
                    }
                    target self
                    use Hi-Potion
                }
            } else {
                target random enemy
                use Demon Slice
            }
        }
    }
} else {
    if (HP%(self) < 60) {
        if (random(0..1) == 0) {
            if (status(self) has Poison) {
                if (random(0..1) == 0) {
                    target self
                    use Remedy
                    return
                }
            }
            if (status(self) has Blind) {
                if (random(0..2) == 0) {
                    target self
                    use Remedy
                    return
                }
            }
            if (status(self) has Silence) {
                if (random(0..2) == 0) {
                    target self
                    use Remedy
                    return
                }
            }
        }
        if (demon_slice_line_done == 0) {
            if (alive(entity 0)) {
                demon_slice_line_done = 1
                target self
                use null
                target battle slot 0
                use Demon Slice
                return
            }
        }
        if (random(0..2) != 0) {
            target random enemy
            use Seifer Physical Attack
        } else {
            if (random(0..2) == 0) {
                target random enemy
                use Demon Slice
            } else {
                targetStatus 00c800e5
                use Fira
            }
        }
    } else {
        if (taunt_turn_counter <= 3) {
            taunt_turn_counter += 1
            if (taunt_turn_counter == 3) {
                taunt_turn_counter += 2
                target self
                use null
            }
        }
        if (random(0..1) == 0) {
            if (status(self) has Poison) {
                if (random(0..1) == 0) {
                    target self
                    use Remedy
                    return
                }
            }
            if (status(self) has Blind) {
                if (random(0..2) == 0) {
                    target self
                    use Remedy
                    return
                }
            }
            if (status(self) has Silence) {
                if (random(0..2) == 0) {
                    target self
                    use Remedy
                    return
                }
            }
        }
        target random enemy
        use one of Seifer Physical Attack, Seifer Physical Attack, Fira
    }
}
return
```

### Counter

```
if (hp40_line_done == 0) {
    if (HP%(self) < 40) {
        hp40_line_done = 1
        target self
        use null
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 36
    }
}
return
```

## 87: Seifer

Variables: `defeated` = varA (named), `turn_counter` = varB (named)


### Init

```
defeated = 0
turn_counter = 0
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
turn_counter += 1
if (turn_counter == 1) {
    target self
    use null
} else {
    if (turn_counter == 4) {
        target self
        use null
    } else {
        if (status(self) has Silence) {
            if (random(0..2) == 0) {
                return
            } else {
                target random enemy
                use Seifer Physical Attack
            }
        } else {
            if (random(0..2) == 0) {
                return
            } else {
                target random enemy
                use one of Seifer Physical Attack, Seifer Physical Attack, Fira
            }
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
    targetableSlot 5
    vanish (silent remove)
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
    }
} else {
    setHitAnim 49
}
return
```

## 88: Edea

Variables: `opening_done` = varA (named), `two_left_line_done` = varB (named)


### Init

```
opening_done = 0
two_left_line_done = 0
return
```

### Turn

```
if (opening_done == 0) {
    opening_done = 1
    target self
    use null
    targetStatus 00c800cb
    use Thundaga
    return
}
if (two_left_line_done == 0) {
    if (alive_count(enemy team) <= 2) {
        two_left_line_done = 1
        target self
        use null
        return
    }
}
if (HP%(tgt0) < 100) {
    if (alive_count(enemy team) <= 2) {
        target self
        use null
        return
    }
}
if (random(0..2) == 0) {
    return
}
if (status(enemy team) has Reflect) {
    targetStatus 00c80017
    if (random(0..3) != 0) {
        use Dispel
    } else {
        use Astral Punch
    }
} else {
    if (alive_count(enemy team) == 1) {
        if (HP%(tgt0) <= 30) {
            target battle slot 0
            use Blizzaga
        } else {
            target battle slot 0
            use one of Firaga, Thundaga, Blizzaga
        }
    } else {
        if (HP%(tgt0) <= 50) {
            if (random(0..1) == 0) {
                if (alive(entity 2)) {
                    target battle slot 2
                    use one of Firaga, Thundaga, Blizzaga
                } else {
                    if (random(0..1) == 0) {
                        if (status(self) lacks Shell) {
                            target self
                            use Shell
                        } else {
                            if (status(self) lacks Protect) {
                                target self
                                use Protect
                            } else {
                                target random enemy
                                use one of Firaga, Thundaga, Blizzaga
                            }
                        }
                    } else {
                        target random enemy
                        use one of Firaga, Thundaga, Blizzaga
                    }
                }
            } else {
                if (alive(entity 4)) {
                    target battle slot 4
                    use one of Firaga, Thundaga, Blizzaga
                } else {
                    if (random(0..1) == 0) {
                        if (status(self) lacks Shell) {
                            target self
                            use Shell
                        } else {
                            if (status(self) lacks Protect) {
                                target self
                                use Protect
                            } else {
                                target random enemy
                                use one of Firaga, Thundaga, Blizzaga
                            }
                        }
                    } else {
                        target random enemy
                        use one of Firaga, Thundaga, Blizzaga
                    }
                }
            }
        } else {
            target random enemy
            use one of Firaga, Thundaga, Blizzaga
        }
    }
}
return
```

### Death

```
target self
use null
return
```

## 89: Propagator

Variables: `physical_hits_taken` = varA (named), `magic_hits_taken` = varB (named)


### Init

```
physical_hits_taken = 0
magic_hits_taken = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (physical_hits_taken >= 3) {
    physical_hits_taken = 0
    if (any_enemy_gender == female) {
        targetStatus 00c800c9
        use BiteBite
    } else {
        target random enemy
        use BiteBite
    }
} else {
    if (magic_hits_taken >= 3) {
        magic_hits_taken = 0
        if (any_enemy_gender == male) {
            targetStatus 00c800c8
            use BiteBite
        } else {
            target random enemy
            use BiteBite
        }
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use one of Silence, Blind, Thundaga
        } else {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    physical_hits_taken += 1
} else {
    if (last_damage == magical) {
        magic_hits_taken += 1
    }
}
return
```

## 90: Ultima Weapon

Variables: `defeated` = varA (named), `attack_cycle` = varB (named)


### Init

```
defeated = 0
attack_cycle = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
attack_cycle += 1
if (random(0..3) == 0) {
    return
}
if (attack_cycle == 6) {
    attack_cycle = 0
    target random enemy
    use one of Physical attack, Physical attack, Light Pillar
} else {
    if (attack_cycle == 5) {
        target random enemy each hit
        use Meteor
    } else {
        if (attack_cycle == 4) {
            target all enemies
            use Quake
        } else {
            if (attack_cycle == 3) {
                target all enemies
                use Gravija
            } else {
                target random enemy
                use one of Physical attack, Physical attack, Light Pillar
            }
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use Ultima Weapon Death
    leave 200
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 91: Elvoret

Variables: `turn_counter` = varA (auto)


### Init

```
turn_counter = 0
target self
prepareAnim 0f
specialAction 17
if (alive(entity 1)) {
    print+lock '{Zell} “What the hell is it?”'
} else {
    if (alive(entity 0)) {
        print+lock '{Squall} “What the...!?”'
    } else {
        print+lock '{Selphie} “Huh?  What is it?”'
    }
}
return
```

### Turn

```
turn_counter += 1
if (turn_counter == 4) {
    target all enemies
    use Storm Breath
    turn_counter = 0
} else {
    if (turn_counter == 2) {
        target random enemy
        use one of Physical attack, Physical attack, Thunder
    } else {
        if (turn_counter == 1) {
            target random enemy
            use one of Physical attack, Physical attack, Fire
        }
    }
}
return
```

### Death

```
add item drop Weapons Mon Mar (non-battle-item, cross-confirmed via mngrp+mwepon)
target self
prepareAnim 10
specialAction 18
vanish (silent remove)
return
```

### Pre-hit

```
if (status(self) has Death) {
    setHitAnim 3
}
return
```

## 92: X-ATM092

Variables: `downed` = varA (named), `repair_turn_counter` = varB (named), `attack_cycle` = varC (named), `times_downed` = varD (named), `recovery_line_index` = varE (named)


### Init

```
downed = 0
repair_turn_counter = 0
attack_cycle = 0
times_downed = 0
recovery_line_index = 0
return
```

### Turn

```
if (downed == 1) {
    if (repair_turn_counter < 4) {
        repair_turn_counter += 1
        if (repair_turn_counter == 1) {
            print 'Repairing... 20%'
        } else {
            if (repair_turn_counter == 2) {
                print 'Repairing... 40%'
            } else {
                if (repair_turn_counter == 3) {
                    print 'Repairing... 60%'
                } else {
                    print 'Repairing... 80%'
                }
            }
        }
    } else {
        recover to full HP
        target self
        use Do Nothing?
        downed = 0
        repair_turn_counter = 0
        block_escape = True
        if (recovery_line_index == 0) {
            if (alive(entity 1)) {
                print+lock '{Zell} “Huh, is it repairing itself!?”'
                recovery_line_index = 1
            } else {
                if (alive(entity 0)) {
                    print+lock '{Squall} “A self-repair mechanism?”'
                    recovery_line_index = 1
                } else {
                    print+lock "{Selphie} “What's goin' on here!?”"
                    recovery_line_index = 1
                }
            }
        } else {
            if (recovery_line_index == 2) {
                recovery_line_index += 1
                if (alive(entity 0)) {
                    print+lock "{Squall} “There's no end to this...”"
                } else {
                    if (alive(entity 5)) {
                        print+lock '{Selphie} “No more!”'
                    } else {
                        print+lock '{Zell} “Geez, not again!!!”'
                    }
                }
            } else {
                if (recovery_line_index == 3) {
                    recovery_line_index += 1
                    if (alive(entity 1)) {
                        print+lock '{Zell} “Geez, not again!!!”'
                    } else {
                        if (alive(entity 0)) {
                            print+lock "{Squall} “There's no end to this...”"
                        } else {
                            print+lock '{Selphie} “No more!”'
                        }
                    }
                } else {
                    recovery_line_index += 1
                    if (alive(entity 5)) {
                        print+lock '{Selphie} “No more!”'
                    } else {
                        if (alive(entity 1)) {
                            print+lock '{Zell} “Geez, not again!!!”'
                        } else {
                            print+lock "{Squall} “There's no end to this...”"
                        }
                    }
                }
            }
        }
    }
} else {
    attack_cycle += 1
    if (attack_cycle == 5) {
        target all enemies
        use Clash
        attack_cycle = 0
    } else {
        if (attack_cycle == 4) {
            target random enemy
            use Physical attack
        } else {
            if (attack_cycle == 3) {
                target all enemies
                use Ray Bomb
            } else {
                if (attack_cycle == 2) {
                    target random enemy
                    use one of Physical attack, Arm Crush, Arm Crush
                } else {
                    if (random(0..2) == 0) {
                        target all enemies
                        use Clash
                    } else {
                        target random enemy
                        use Physical attack
                    }
                }
            }
        }
    }
}
return
```

### Counter

```
if (times_downed <= 4) {
    if (downed == 0) {
        if (HP%(self) < 80) {
            target self
            use Do Nothing?
            block_escape = False
            downed = 1
            if (combat_scene != 26 /*X-ATM092*/) {
                times_downed += 1
            }
            if (alive(entity 1)) {
                print "{Zell} “Let's get the hell outta here!”"
            } else {
                if (alive(entity 5)) {
                    print '{Selphie} “Hurry to the rendezvous!”'
                } else {
                    print '{Squall} “Alright, withdraw.”'
                }
            }
            print '{L2}, {R2} buttons to escape.'
            waitText 02
        }
    }
}
return
```

### Death

```
if (times_downed <= 4) {
    block_escape = True
    recover to full HP
    target self
    use Do Nothing?
    downed = 0
    repair_turn_counter = 0
    if (combat_scene != 26 /*X-ATM092*/) {
        times_downed += 1
    }
    if (alive(entity 1)) {
        print '{Zell} “Huh, is it repairing itself!?”'
        recovery_line_index = 1
    } else {
        if (alive(entity 0)) {
            print '{Squall} “A self-repair mechanism?”'
            recovery_line_index = 1
        } else {
            print "{Selphie} “What's goin' on here!?”"
            recovery_line_index = 1
        }
    }
} else {
    if (random(0..3) == 0) {
        add item drop Power Wrist (non-battle-item, cross-confirmed via mngrp+mwepon)
    } else {
        if (random(0..2) == 0) {
            add item drop Orihalcon (non-battle-item, cross-confirmed via mngrp+mwepon)
        } else {
            if (random(0..1) == 0) {
                add item drop Force Armlet (non-battle-item, cross-confirmed via mngrp+mwepon)
            } else {
                add item drop Hypno Crown (non-battle-item, cross-confirmed via mngrp+mwepon)
            }
        }
    }
    target self
    use X-ATM092 Death
    leave 200
}
return
```

## 93: Iguion


### Init

```
battle_var[96] = 3
if (battle_var[97] == 0) {
    if (save.tutorial_irvine_shot_seen == 0) {
        battle_var[97] = 1
        save.tutorial_irvine_shot_seen = 1
        print+lock '{Irvine} “Oh, I forgot to tell you...”'
        print+lock '“For my Limit Break, Shot,”'
        print+lock '“pull the trigger with the {R1}.”'
        print+lock '“Got it?”'
        waitText 04
    } else {
        battle_var[97] = 1
        print '{Irvine} “We have to save {Rinoa}!”'
    }
}
return
```

### Turn

```
if (gf_not_yet_stolen) {
    autoStatus 1700
}
if (random(0..2) == 0) {
    return
}
if (alive_count(enemy team) == 1) {
    target random enemy
    use one of Physical attack, Physical attack, line 253
} else {
    if (battle_var[96] >= 6) {
        if (alive_count(ally team) == 2) {
            target all enemies
            use Resonance
            battle_var[96] = 0
        } else {
            target random enemy
            use one of Physical attack, Physical attack, Magma Breath
        }
    } else {
        target random enemy
        use one of Physical attack, Physical attack, Magma Breath
    }
}
return
```

### Counter

```
if (gf_not_yet_stolen) {
    autoStatus 1700
}
battle_var[96] += 1
return
```

## 94: Gargantua

Variables: `once_turn` = varA (auto)


### Init

```
target self
use null
return
```

### Turn

```
if (once_turn == 0) {
    once_turn = 1
    target all enemies
    use Evil-Eye
    return
}
if (random(0..2) == 0) {
    return
}
if (random(0..1) == 0) {
    if (random(0..2) != 0) {
        target random enemy
        use null
    } else {
        target all enemies
        use Evil-Eye
    }
} else {
    if (status(enemy team) lacks Berserk) {
        if (random(0..1) == 0) {
            targetStatus 00c80305
            use Berserk
        } else {
            if (random(0..2) == 0) {
                target all enemies
                use Quake
            } else {
                target random enemy
                use one of Demi, Demi, Silence
            }
        }
    } else {
        if (random(0..2) == 0) {
            target all enemies
            use Quake
        } else {
            target random enemy
            use one of Demi, Demi, Silence
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    target last attacker
    use Counter Twist
}
return
```

### Death

```
target self
use null
leave 200
return
```

## 95: Granaldo


### Turn

```
if (random(0..2) == 0) {
    return
}
if (combat_scene == 62 /*Granaldo+Raldo*/) {
    if (alive(entity 112)) {
        if (random(0..2) == 0) {
            if (alive(battle_slot 1)) {
                target random enemy
                if (random(0..1) == 0) {
                    use null
                } else {
                    use null
                }
            } else {
                if (alive(battle_slot 2)) {
                    target random enemy
                    if (random(0..1) == 0) {
                        use null
                    } else {
                        use null
                    }
                } else {
                    if (random(0..1) == 0) {
                        use null
                    } else {
                        use null
                    }
                }
            }
        } else {
            if (random(0..1) == 0) {
                if (alive(battle_slot 2)) {
                    target random enemy
                    if (random(0..1) == 0) {
                        use null
                    } else {
                        use null
                    }
                } else {
                    if (alive(battle_slot 3)) {
                        target random enemy
                        if (random(0..1) == 0) {
                            use null
                        } else {
                            use null
                        }
                    } else {
                        if (random(0..1) == 0) {
                            use null
                        } else {
                            use null
                        }
                    }
                }
            } else {
                if (alive(battle_slot 3)) {
                    target random enemy
                    if (random(0..1) == 0) {
                        use null
                    } else {
                        use null
                    }
                } else {
                    if (alive(battle_slot 1)) {
                        target random enemy
                        if (random(0..1) == 0) {
                            use null
                        } else {
                            use null
                        }
                    } else {
                        if (random(0..1) == 0) {
                            use null
                        } else {
                            use null
                        }
                    }
                }
            }
        }
    } else {
        target random enemy
        use Physical attack
    }
} else {
    target random enemy
    use one of Physical attack, Physical attack, line 253
}
return
```

## 96: Raldo


### Turn

```
if (random(0..2) == 0) {
    return
}
if (combat_scene == 62 /*Granaldo+Raldo*/) {
    if (alive(entity 111)) {
        Vitality multiplier = 200%
        Spirit multiplier = 200%
    } else {
        Vitality multiplier = 100%
        Spirit multiplier = 100%
        target random enemy
        use Physical attack
    }
} else {
    target random enemy
    use one of Physical attack, Physical attack, line 253
}
return
```

## 97: Propagator

Variables: `physical_hits_taken` = varA (named), `magic_hits_taken` = varB (named)


### Init

```
physical_hits_taken = 0
magic_hits_taken = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (physical_hits_taken >= 3) {
    physical_hits_taken = 0
    if (any_enemy_gender == female) {
        targetStatus 00c800c9
        use BiteBite
    } else {
        target random enemy
        use BiteBite
    }
} else {
    if (magic_hits_taken >= 3) {
        magic_hits_taken = 0
        if (any_enemy_gender == male) {
            targetStatus 00c800c8
            use BiteBite
        } else {
            target random enemy
            use BiteBite
        }
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use one of Silence, Blind, Thundaga
        } else {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    physical_hits_taken += 1
} else {
    if (last_damage == magical) {
        magic_hits_taken += 1
    }
}
return
```

## 98: Propagator

Variables: `physical_hits_taken` = varA (named), `magic_hits_taken` = varB (named)


### Init

```
physical_hits_taken = 0
magic_hits_taken = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (physical_hits_taken >= 3) {
    physical_hits_taken = 0
    if (any_enemy_gender == female) {
        targetStatus 00c800c9
        use BiteBite
    } else {
        target random enemy
        use BiteBite
    }
} else {
    if (magic_hits_taken >= 3) {
        magic_hits_taken = 0
        if (any_enemy_gender == male) {
            targetStatus 00c800c8
            use BiteBite
        } else {
            target random enemy
            use BiteBite
        }
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use one of Silence, Blind, Thundaga
        } else {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    physical_hits_taken += 1
} else {
    if (last_damage == magical) {
        magic_hits_taken += 1
    }
}
return
```

## 99: Oilboyle


### Turn

```
if (random(0..2) == 0) {
    return
}
if (random(0..7) == 0) {
    target all enemies
    use Sonic Wave
} else {
    if (random(0..1) == 0) {
        target random enemy
        use Physical attack
    } else {
        target random enemy
        use Oil Shot
    }
}
return
```

### Counter

```
if (HP%(self) < 50) {
    if (random(0..2) == 0) {
        target last attacker
        use Oil Blast
    }
}
return
```

## 100: Edea

Variables: `defeated` = varA (named), `maelstrom_opener_done` = varB (named)


### Init

```
become untargetable
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (alive_count(ally team) != 1) {
    fill ATB
} else {
    if (maelstrom_opener_done == 0) {
        maelstrom_opener_done = 1
        activate
        target self
        use null
        target all enemies
        use Maelstrom
    } else {
        if (all(enemy team) have Reflect) {
            if (random(0..1) == 0) {
                target random enemy
                use Dispel
            } else {
                if (status(self) has Reflect) {
                    target self
                    use one of Blizzaga, Blizzaga, Silence
                } else {
                    target self
                    use Reflect
                }
            }
        } else {
            if (random(0..2) == 0) {
                targetStatus 00c80317
                use one of Silence, Death, Slow
            } else {
                if (random(0..1) == 0) {
                    if (random(0..1) == 0) {
                        targetStatus 00c80317
                        use one of Blizzaga, Fira, Thundara
                    } else {
                        targetStatus 00c80317
                        use Blizzaga
                    }
                } else {
                    if (random(0..2) == 0) {
                        if (status(self) lacks Reflect) {
                            target self
                            use Reflect
                        } else {
                            targetStatus 00c80317
                            use Blizzaga
                        }
                    } else {
                        if (random(0..1) == 0) {
                            target random enemy
                            use Dispel
                        } else {
                            target all enemies
                            use Maelstrom
                        }
                    }
                }
            }
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 101: BGH251F2

Variables: `beam_cannon_only` = varA (named), `turret1_exploded` = varB (named), `turret2_exploded` = varC (named), `turret3_exploded` = varD (named), `turret4_exploded` = varE (named), `attack_cycle` = varF (named), `standby_line_done` = varG (named)


### Init

```
beam_cannon_only = 0
turret1_exploded = 0
turret2_exploded = 0
turret3_exploded = 0
turret4_exploded = 0
attack_cycle = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (beam_cannon_only == 1) {
    target random enemy
    use Beam Cannon
} else {
    attack_cycle += 1
    if (attack_cycle == 1) {
        target random enemy
        use BGH251F2 Gatling Gun
    } else {
        if (attack_cycle == 2) {
            target random enemy
            use BGH251F2 Gatling Gun
        } else {
            if (attack_cycle == 3) {
                target random enemy
                use BGH251F2 Gatling Gun
            } else {
                if (attack_cycle == 4) {
                    if (standby_line_done == 0) {
                        print+lock 'Captain “Stand by for beam cannon!”'
                        print+lock 'Private 1 “Yes, sir!”'
                        waitText 02
                        standby_line_done = 1
                    } else {
                        if (random(0..2) == 0) {
                            print+lock 'Private 2 “Setting target!”'
                            waitText 01
                        } else {
                            if (random(0..1) == 0) {
                                print+lock 'Captain “Stand by for beam cannon!”'
                                print+lock 'Private 1 “Yes, sir!”'
                                waitText 02
                            } else {
                                print+lock "Captain “Shoot'em again!”"
                                waitText 01
                            }
                        }
                    }
                } else {
                    target random enemy
                    use Beam Cannon
                    attack_cycle = 0
                }
            }
        }
    }
}
return
```

### Counter

```
if (HP%(self) < 20) {
    if (turret1_exploded == 0) {
        turret1_exploded = 1
        target self
        use BGH251F2 1st Turret Exploding
    }
    if (turret2_exploded == 0) {
        turret2_exploded = 1
        target self
        use BGH251F2 2nd Turret Exploding
    }
    if (turret3_exploded == 0) {
        turret3_exploded = 1
        target self
        use BGH251F2 3rd Turret Exploding
        target self
        use null
    }
    if (turret4_exploded == 0) {
        turret4_exploded = 1
        target self
        use BGH251F2 4th Turret Exploding
    }
    target self
    use null
    add item drop Weapons Mon Jun (non-battle-item, cross-confirmed via mngrp+mwepon)
    target self
    use BGH251F2 Death
    enter 1
    leave 200
} else {
    if (HP%(self) < 40) {
        beam_cannon_only = 1
        if (turret1_exploded == 0) {
            turret1_exploded = 1
            target self
            use BGH251F2 1st Turret Exploding
        }
        if (turret2_exploded == 0) {
            turret2_exploded = 1
            target self
            use BGH251F2 2nd Turret Exploding
        }
        if (turret3_exploded == 0) {
            turret3_exploded = 1
            target self
            use BGH251F2 3rd Turret Exploding
            target self
            use null
        }
        if (turret4_exploded == 0) {
            turret4_exploded = 1
            target self
            use BGH251F2 4th Turret Exploding
            print+lock 'Captain “Keep attacking anyway!”'
            print+lock 'Private 1 “Yes, sir!”'
            waitText 02
        }
    } else {
        if (HP%(self) < 60) {
            if (turret1_exploded == 0) {
                turret1_exploded = 1
                target self
                use BGH251F2 1st Turret Exploding
            }
            if (turret2_exploded == 0) {
                turret2_exploded = 1
                target self
                use BGH251F2 2nd Turret Exploding
            }
            if (turret3_exploded == 0) {
                turret3_exploded = 1
                target self
                use BGH251F2 3rd Turret Exploding
                target self
                use null
            }
        } else {
            if (HP%(self) < 70) {
                if (turret1_exploded == 0) {
                    turret1_exploded = 1
                    target self
                    use BGH251F2 1st Turret Exploding
                }
                if (turret2_exploded == 0) {
                    turret2_exploded = 1
                    target self
                    use BGH251F2 2nd Turret Exploding
                }
            } else {
                if (HP%(self) < 80) {
                    if (turret1_exploded == 0) {
                        turret1_exploded = 1
                        target self
                        use BGH251F2 1st Turret Exploding
                        print+lock 'Private 2 “AHHH!  Captain!”'
                        print+lock "Captain “It's only 1, don't worry!”"
                        waitText 02
                    }
                }
            }
        }
    }
}
return
```

### Death

```
if (turret1_exploded == 0) {
    turret1_exploded = 1
    target self
    use BGH251F2 1st Turret Exploding
}
if (turret2_exploded == 0) {
    turret2_exploded = 1
    target self
    use BGH251F2 2nd Turret Exploding
}
if (turret3_exploded == 0) {
    turret3_exploded = 1
    target self
    use BGH251F2 3rd Turret Exploding
    target self
    use null
}
if (turret4_exploded == 0) {
    turret4_exploded = 1
    target self
    use BGH251F2 4th Turret Exploding
}
target self
use null
add item drop Weapons Mon Jun (non-battle-item, cross-confirmed via mngrp+mwepon)
target self
use BGH251F2 Death
enter 1
leave 200
return
```

## 102: BGH251F2


### Init

```
if (alive(entity 1)) {
    print+lock '{Zell} “We got a big one on our hands!”'
} else {
    if (alive(entity 3)) {
        print+lock "{Quistis} “Galbadia's latest weapon.”"
    } else {
        if (alive(entity 2)) {
            print+lock '{Irvine} “Here comes their latest invention!”'
        } else {
            if (alive(entity 4)) {
                print+lock "{Rinoa} “It's here!”"
            }
        }
    }
}
if (alive(entity 0)) {
    print+lock "{Squall} “Let's destroy this thing!”"
}
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (random(0..2) == 0) {
    if (status(enemy team) has HP<50%) {
        targetStatus 00c80009
        use Beam Cannon
    } else {
        target random enemy
        use null
    }
} else {
    target random enemy
    use one of null, null, line 3
}
return
```

### Death

```
target self
use null
die
return
```

## 103: Abadon

Variables: `defense_up` = varA (named), `turn_counter` = varB (named), `defeated` = varC (named)


### Init

```
defense_up = 0
turn_counter = 0
if (alive(entity 0)) {
    print+lock '{Squall} “An undead monster...”'
    print+lock '“Use recovery-related magic and items.”'
    waitText 02
}
return
```

### Turn

```
if (defeated != 0) {
    return
}
turn_counter += 1
if (turn_counter >= 5) {
    if (defense_up == 0) {
        defense_up = 1
        turn_counter = 0
        Vitality multiplier = 500%
        Spirit multiplier = 500%
        target self
        use null
    } else {
        defense_up = 0
        turn_counter = 0
        Vitality multiplier = 100%
        Spirit multiplier = 100%
        target self
        use null
    }
} else {
    if (defense_up == 0) {
        target random enemy
        use one of null, null, null
    } else {
        if (random(0..4) == 0) {
            return
        } else {
            if (status(self) has VIT0) {
                if (random(0..1) == 0) {
                    target self
                    use Esuna
                } else {
                    if (random(0..1) == 0) {
                        target random enemy
                        use Confuse
                    } else {
                        target random enemy
                        use one of Silence, Blind, Dispel
                    }
                }
            } else {
                if (random(0..1) == 0) {
                    target random enemy
                    use Confuse
                } else {
                    target random enemy
                    use one of Silence, Blind, Dispel
                }
            }
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
    leave 0
    leave 1
}
return
```

## 105: Mobile Type 8

Variables: `mobile_turn_counter` = varA (named), `skip_next_counter` = varB (named)


### Init

```
print+lock 'Mobile weaponry attack mode ON'
print+lock 'Support weaponry attack mode OFF'
waitText 02
fill ATB
return
```

### Turn

```
if (battle_var[96] == 0) {
    skip_next_counter = 0
    mobile_turn_counter += 1
    if (mobile_turn_counter <= 6) {
        if (random(0..1) == 0) {
            target random enemy
            use Physical attack
        }
    } else {
        target self
        use Do Nothing?
        battle_var[96] = 1
        mobile_turn_counter = 0
        print+lock 'Mobile weaponry attack mode OFF'
        print+lock 'Support weaponry attack mode ON'
        waitText 02
    }
} else {
    battle_var[98] += 1
    if (battle_var[98] == 1) {
        target all enemies
        use Corona
    } else {
        if (battle_var[98] == 5) {
            target all enemies
            use Megiddo Flame
            battle_var[96] = 0
            battle_var[98] = 0
            skip_next_counter = 1
            target self
            use Do Nothing?
            print+lock 'Mobile weaponry attack mode ON'
            print+lock 'Support weaponry attack mode OFF'
            waitText 02
            fill ATB
        }
    }
}
return
```

### Counter

```
if (battle_var[96] == 0) {
    if (last_command == Draw) {
    } else {
        if (last_command == Magic) {
            if (last_action_id == 50) {
                return
            }
        }
        if (skip_next_counter == 0) {
            target last attacker
            use Twin Homing Laser
        } else {
            skip_next_counter = 0
        }
    }
}
return
```

### Death

```
if (battle_var[96] == 0) {
    target self
    use Do Nothing?
}
battle_var[97] = 1
target self
use null
leave 1
leave 2
leave 200
return
```

## 106: Left Probe

Variables: `counter_disabled` = varA (named)


### Init

```
fill ATB
return
```

### Turn

```
recover to full HP
if (battle_var[96] == 1) {
    if (battle_var[98] == 2) {
        target random enemy
        use Physical attack
    } else {
        if (battle_var[98] == 4) {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
recover to full HP
if (counter_disabled == 1) {
} else {
    if (battle_var[96] == 1) {
        if (last_command == Magic) {
            if (last_action_id == 50) {
                return
            }
        }
        target last attacker
        use Homing Laser
    }
}
return
```

### Death

```
if (battle_var[97] == 0) {
    recover to full HP
}
return
```

## 107: Right Probe

Variables: `counter_disabled` = varA (named)


### Init

```
fill ATB
return
```

### Turn

```
recover to full HP
if (battle_var[96] == 1) {
    if (battle_var[98] == 3) {
        target random enemy
        use Physical attack
    } else {
        if (battle_var[98] == 5) {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
recover to full HP
if (counter_disabled == 1) {
} else {
    if (battle_var[96] == 1) {
        if (last_command == Magic) {
            if (last_action_id == 50) {
                return
            }
        }
        target last attacker
        use Homing Laser
    }
}
return
```

### Death

```
if (battle_var[97] == 0) {
    recover to full HP
}
return
```

## 108: Paratrooper


### Init

```
if (combat_scene == 7 /*Paratrooper*/) {
    if (battle_var[96] == 0) {
        battle_var[96] = 1
        print+lock '“Dispose of this Garden as planned!”'
        if (alive(entity 2)) {
            print+lock '{Irvine} “Dispose!?”'
        } else {
            if (alive(entity 5)) {
                print+lock '{Selphie} “NO WAY!”'
            } else {
                if (alive(entity 0)) {
                    print+lock '{Squall} “Not a chance!”'
                } else {
                    if (alive(entity 3)) {
                        print+lock "{Quistis} “There's no way we'll let you!”"
                    }
                }
            }
        }
        print+lock '“You little SeeD twerps!”'
        waitText 03
    }
}
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (random(0..2) == 0) {
    target random enemy
    use Physical attack
} else {
    target random enemy
    use one of Silence, Demi, Slow
}
return
```

## 109: Trauma

Variables: `phase` = varB (auto), `phase_2` = varC (auto), `turn_counter` = varD (auto), `defeated` = varE (auto)


### Init

```
varA = 0
phase = 0
phase_2 = 0
turn_counter = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (random(0..3) == 0) {
    return
}
if (phase == 0) {
    phase = 1
    phase_2 = 1
    enable 0
    varA = 1
    target self
    use ??
    return
} else {
    if (phase == 1) {
        phase = 2
        phase_2 = 2
        enable 2
        varA = 1
        target self
        use ??
        return
    }
}
if (phase_2 == 2) {
    if (alive_count(ally team) == 1) {
        phase_2 = 0
        turn_counter = 1
    }
}
if (turn_counter >= 5) {
    turn_counter = 0
    target all enemies
    use Mega Pulse Cannon
    return
} else {
    if (turn_counter == 1) {
        turn_counter += 1
        target all enemies
        use Mega Pulse Cannon
        return
    } else {
        if (turn_counter != 0) {
            turn_counter += 1
            target random enemy
            use Physical attack
            return
        }
    }
}
if (phase_2 == 0) {
    phase_2 = 1
    enable 0
    varA = 1
    target self
    use ??
    return
} else {
    if (phase_2 == 1) {
        phase_2 = 2
        enable 2
        varA = 1
        target self
        use ??
        return
    }
}
return
```

### Counter

```
if (varA == 1) {
    prepare summon
    target new ally
    use null
    activate
    loadAndTargetable 209
    varA = 0
}
return
```

### Death

```
if (alive_count(ally team) == 1) {
    if (defeated == 0) {
        defeated = 1
        target self
        use null
        leave 200
    }
} else {
    target random non-self ally
    use Drain
}
return
```

## 110: Droma


### Turn

```
if (random(0..4) == 0) {
    return
}
target random enemy
use one of Physical attack, Physical attack, Mini Pulse Cannon
return
```

## 111: Propagator

Variables: `physical_hits_taken` = varA (named), `magic_hits_taken` = varB (named)


### Init

```
physical_hits_taken = 0
magic_hits_taken = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (physical_hits_taken >= 3) {
    physical_hits_taken = 0
    if (any_enemy_gender == female) {
        targetStatus 00c800c9
        use BiteBite
    } else {
        target random enemy
        use BiteBite
    }
} else {
    if (magic_hits_taken >= 3) {
        magic_hits_taken = 0
        if (any_enemy_gender == male) {
            targetStatus 00c800c8
            use BiteBite
        } else {
            target random enemy
            use BiteBite
        }
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use one of Silence, Blind, Thundaga
        } else {
            target random enemy
            use Physical attack
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    physical_hits_taken += 1
} else {
    if (last_damage == magical) {
        magic_hits_taken += 1
    }
}
return
```

## 112: Adel

Variables: `defeated` = varA (named), `attack_cycle` = varB (named), `opening_done` = varC (named)


### Init

```
defeated = 0
attack_cycle = 0
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (opening_done == 0) {
    opening_done = 1
    if (alive(entity 1)) {
        target self
        use null
    } else {
        if (alive(entity 5)) {
            target self
            use null
        } else {
            if (alive(entity 3)) {
                target self
                use null
            }
        }
    }
    target battle slot 0
    use null
    return
}
if (random(0..2) == 0) {
    return
}
attack_cycle += 1
if (attack_cycle == 8) {
    attack_cycle = 0
    battle_var[96] = 1
    target random non-self ally
    use Adel's Drain?
    if (random(0..2) != 0) {
        target random enemy
        use Engery Bomber
    } else {
        target random enemy
        use one of Holy, Flare, Flare
    }
} else {
    if (attack_cycle == 7) {
        target all enemies
        use Ultima
        battle_var[97] = 0
    } else {
        if (attack_cycle == 6) {
            return
        } else {
            if (attack_cycle == 5) {
                print+lock 'Magical powers are concentrated on Adel!'
                battle_var[97] = 1
                target self
                use Do Nothing?
            } else {
                if (attack_cycle == 4) {
                    battle_var[96] = 1
                    target random non-self ally
                    use Adel's Drain?
                    if (random(0..2) == 0) {
                    } else {
                        target all enemies
                        use Quake
                    }
                } else {
                    if (attack_cycle == 3) {
                        battle_var[96] = 1
                        target random non-self ally
                        use Adel's Drain?
                        if (random(0..2) == 0) {
                            target random enemy
                            use one of Holy, Holy, Flare
                        } else {
                            target random enemy
                            use Engery Bomber
                        }
                    } else {
                        if (attack_cycle == 2) {
                            battle_var[96] = 1
                            target random non-self ally
                            use Adel's Drain?
                            if (random(0..2) == 0) {
                                target random enemy
                                use one of Holy, Holy, Flare
                            } else {
                                target random enemy
                                use Engery Bomber
                            }
                        } else {
                            battle_var[96] = 1
                            target random non-self ally
                            use Adel's Drain?
                            target random enemy each hit
                            use Meteor
                        }
                    }
                }
            }
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use Adel Death
    leave 0
    leave 1
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 113: {Rinoa}

Variables: `hit_reaction_done` = varA (named)


### Init

```
hit_reaction_done = 0
return
```

### Counter

```
if (last_command == Magic) {
    if (last_action_id == 46) {
        return
    }
}
if (last_command == Magic) {
    if (last_action_id == 47) {
        return
    }
}
if (last_command == Magic) {
    if (last_action_id == 50) {
        return
    }
}
if (last_command == Magic) {
    if (last_action_id >= 21) {
        if (last_action_id <= 41) {
            return
        }
    }
}
if (battle_var[96] == 0) {
    if (hit_reaction_done == 0) {
        hit_reaction_done = 1
        target self
        use null
    }
} else {
    battle_var[96] = 0
}
return
```

### Death

```
print '{Rinoa}...'
force GAME OVER
return
```

## 114: Omega Weapon

Variables: `defeated` = varA (auto), `turn_counter` = varB (auto), `once_turn` = varC (auto)


### Init

```
defeated = 0
turn_counter = 0
once_turn = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (varD == 1) {
    varD = 0
    return
}
if (random(0..2) == 0) {
    return
}
if (random(0..2) == 0) {
    target random enemy
    use Physical attack
} else {
    turn_counter += 1
    if (turn_counter == 1) {
        if (once_turn == 0) {
            once_turn = 1
            target all enemies
            use LV5 Death
        } else {
            target random enemy
            use Light Pillar
        }
    } else {
        if (turn_counter == 2) {
            target random enemy each hit
            use Meteor
        } else {
            if (turn_counter == 3) {
                target all enemies
                use Megiddo Flame
            } else {
                if (turn_counter == 4) {
                    target all enemies
                    use Gravija
                } else {
                    if (turn_counter == 5) {
                        target random enemy each hit
                        use Terra Break
                    } else {
                        if (turn_counter == 6) {
                            target all enemies
                            use Ultima
                            turn_counter = 0
                        }
                    }
                }
            }
        }
    }
}
return
```

### Counter

```
if (last_command == Item) {
    if (last_action_id == 1) {
        varD = 1
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    give Proof of Omega
    target self
    use Ultima Weapon Death
    leave 200
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 115: “Sorceress”

Variables: `spell_set` = varA (named), `spawn_variant` = varB (named)


### Init

```
if (battle_var[96] != 0) {
    battle_var[96] += 1
    if (battle_var[98] == 0) {
        battle_var[98] = 1
    } else {
        battle_var[98] = 2
    }
    target self
    use "Sorceress" Spawn
    if (battle_var[96] == 2) {
        spell_set = 2
    }
    if (battle_var[96] == 3) {
        spell_set = 3
    }
    if (battle_var[96] == 4) {
        spell_set = 4
    }
    if (battle_var[96] == 5) {
        spell_set = 5
    }
    if (battle_var[96] == 6) {
        spell_set = 6
    }
    if (battle_var[97] == 3) {
        battle_var[97] = 0
        spawn_variant = 3
    } else {
        battle_var[97] = 0
        spawn_variant = 6
    }
} else {
    battle_var[96] += 1
    battle_var[98] = 1
    battle_var[99] = 0
    spell_set = 1
    spawn_variant = 3
    target self
    use Do Nothing?
}
return
```

### Turn

```
if (battle_var[96] >= 10) {
} else {
    if (random(0..1) == 0) {
        if (battle_var[98] == 1) {
            if (spawn_variant == 3) {
                if (battle_var[96] >= 6) {
                    battle_var[97] = 4
                    activate
                    enter 1
                    return
                } else {
                    battle_var[97] = 6
                    activate
                    enter 3
                    return
                }
            } else {
                if (spawn_variant == 6) {
                    if (battle_var[96] >= 6) {
                        battle_var[97] = 5
                        activate
                        enter 2
                        return
                    } else {
                        battle_var[97] = 3
                        activate
                        enter 0
                        return
                    }
                }
            }
        }
    }
}
if (random(0..2) == 0) {
    return
}
if (random(0..2) == 0) {
    target random enemy
    use null
    return
}
if (spell_set == 1) {
    if (all(enemy team) have Reflect) {
        if (status(ally team) has Reflect) {
            targetStatus 00c90017
            use Fire
            return
        } else {
            target random ally
            use Reflect
            return
        }
    } else {
        targetStatus 00c80317
        use Fire
        return
    }
}
if (spell_set == 2) {
    if (alive_count(enemy team) == 1) {
        if (all(enemy team) have Reflect) {
            target random enemy
            use null
            return
        }
    } else {
        target random enemy
        use Thunder
        return
    }
}
if (spell_set == 3) {
    if (alive_count(enemy team) == 1) {
        if (all(enemy team) have Reflect) {
            target random enemy
            use null
            return
        }
    } else {
        target random enemy
        use Fira
        return
    }
}
if (spell_set == 4) {
    if (all(enemy team) have Reflect) {
        if (status(ally team) has Reflect) {
            targetStatus 00c90017
            use Blizzara
            return
        } else {
            target random ally
            use Reflect
            return
        }
    } else {
        target random enemy
        use Blizzara
        return
    }
}
if (spell_set == 5) {
    if (status(ally team) has Silence) {
        targetStatus 00c90004
        use Esuna
        return
    } else {
        if (all(enemy team) have Reflect) {
            if (alive_count(enemy team) == 1) {
                target random enemy
                use null
                return
            } else {
                target random enemy
                use Dispel
                return
            }
        } else {
            target random enemy
            use Thundara
            return
        }
    }
}
if (spell_set == 6) {
    if (all(enemy team) have Reflect) {
        if (alive_count(enemy team) == 1) {
            target random enemy
            use null
            return
        } else {
            target random enemy
            use Dispel
            return
        }
    } else {
        target random enemy
        use Aero
        return
    }
}
return
```

### Death

```
if (battle_var[99] >= 9) {
    die
    activate
    enter 4
} else {
    if (battle_var[98] == 1) {
        battle_var[98] = 0
        battle_var[99] += 1
        die
        if (spawn_variant == 3) {
            if (battle_var[96] >= 6) {
                battle_var[97] = 4
                activate
                enter 1
            } else {
                battle_var[97] = 6
                activate
                enter 3
            }
        } else {
            if (spawn_variant == 6) {
                if (battle_var[96] >= 6) {
                    battle_var[97] = 5
                    activate
                    enter 2
                } else {
                    battle_var[97] = 3
                    activate
                    enter 0
                }
            }
        }
    } else {
        battle_var[98] = 1
        battle_var[99] += 1
        die
    }
}
return
```

## 116: “Sorceress”

Variables: `phase` = varA (auto)


### Init

```
battle_var[96] += 1
if (battle_var[98] == 0) {
    battle_var[98] = 1
} else {
    battle_var[98] = 2
}
target self
use "Sorceress" Spawn
if (battle_var[96] == 7) {
    phase = 7
}
if (battle_var[96] == 8) {
    phase = 8
}
if (battle_var[96] == 9) {
    phase = 9
}
if (battle_var[96] == 10) {
    phase = 10
}
if (battle_var[97] == 4) {
    battle_var[97] = 0
    varB = 4
} else {
    battle_var[97] = 0
    varB = 5
}
return
```

### Turn

```
if (battle_var[96] >= 10) {
} else {
    if (random(0..1) == 0) {
        if (battle_var[98] == 1) {
            if (varB == 4) {
                battle_var[97] = 5
                activate
                enter 2
                return
            } else {
                if (varB == 5) {
                    battle_var[97] = 4
                    activate
                    enter 1
                    return
                }
            }
        }
    }
}
if (random(0..2) == 0) {
    return
}
if (alive_count(enemy team) == 1) {
    if (random(0..2) == 0) {
        target random enemy
        use one of null, Thundaga, Esuna
        return
    } else {
        return
    }
}
if (random(0..2) == 0) {
    target random enemy
    use null
    return
}
if (phase == 7) {
    if (status(self) lacks Reflect) {
        if (status(self) lacks Double) {
            if (random(0..1) == 0) {
                target self
                use Double
                return
            }
        }
    }
    if (status(self) has Double) {
        target random enemy
        use Thundaga
        if (alive_count(enemy team) != 0) {
            target random enemy
            use Thundaga
        }
    } else {
        target random enemy
        use Thundaga
    }
    return
}
if (phase == 8) {
    if (random(0..1) == 0) {
        target all enemies
        use Quake
        return
    } else {
        target random enemy
        use Meltdown
        return
    }
}
if (phase == 9) {
    target random enemy each hit
    use Meteor
    return
}
if (phase == 10) {
    if (status(self) lacks Reflect) {
        if (status(self) lacks Double) {
            if (random(0..1) == 0) {
                target self
                use Double
                return
            }
        }
    }
    if (status(self) has Double) {
        target random enemy
        use Flare
        if (alive_count(enemy team) != 0) {
            target random enemy
            use Flare
        }
    } else {
        target random enemy
        use Flare
    }
    return
}
return
```

### Death

```
if (battle_var[99] >= 9) {
    die
    activate
    enter 4
} else {
    if (battle_var[98] == 1) {
        battle_var[98] = 0
        battle_var[99] += 1
        die
        if (varB == 4) {
            battle_var[97] = 5
            activate
            enter 2
            return
        } else {
            if (varB == 5) {
                battle_var[97] = 4
                activate
                enter 1
                return
            }
        }
    } else {
        battle_var[98] = 1
        battle_var[99] += 1
        die
    }
}
return
```

## 117: “Sorceress”

Variables: `defeated` = varA (auto), `turn_counter` = varB (auto)


### Init

```
defeated = 0
turn_counter = 0
target self
use "Sorceress" Spawn
target self
use Do Nothing?
return
```

### Turn

```
if (defeated != 0) {
    return
}
turn_counter += 1
if (turn_counter == 3) {
    print '5'
    varC = 1
    target self
    use Do Nothing?
} else {
    if (turn_counter == 4) {
        print '4'
    } else {
        if (turn_counter == 5) {
            print '3'
            varC = 1
            target self
            use Do Nothing?
        } else {
            if (turn_counter == 6) {
                print '2'
            } else {
                if (turn_counter == 7) {
                    print '1'
                    varC = 1
                    target self
                    use Do Nothing?
                } else {
                    if (turn_counter >= 8) {
                        turn_counter = 0
                        target all enemies
                        use Ultima
                        varC = 1
                        target self
                        use Do Nothing?
                    }
                }
            }
        }
    }
}
return
```

### Counter

```
if (varC == 1) {
    varC = 0
} else {
    if (turn_counter <= 2) {
        target last attacker
        use null
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use Final "Sorceress" Death
    leave 200
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 118: UFO?

Variables: `defeated` = varA (auto)


### Death

```
if (defeated == 0) {
    defeated = 1
    save.ufo_defeated = 1
    target self
    use null
    leave 200
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 119: Fujin

Variables: `tornado_opener_done` = varA (named), `turn_counter` = varB (named), `defeated` = varC (named), `turn4_line_done` = varD (named)


### Init

```
tornado_opener_done = 0
turn_counter = 0
turn4_line_done = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
turn_counter += 1
if (turn_counter == 4) {
    if (turn4_line_done == 0) {
        turn4_line_done = 1
        target self
        use null
        return
    }
}
if (gf_not_yet_stolen) {
    if (HP%(self) < 50) {
        if (random(0..3) == 0) {
            if (status(ally team) has Blind) {
                targetStatus 00c90003
                use Remedy
            } else {
                target random ally
                use null
            }
        } else {
            target random enemy
            use one of Zan, Zan, Sai
        }
    } else {
        target random enemy
        use Zan
    }
} else {
    if (tornado_opener_done == 0) {
        tornado_opener_done = 1
        target all enemies
        use Tornado
    } else {
        if (status(enemy team) lacks HP<50%) {
            if (random(0..2) == 0) {
                target all enemies
                use Tornado
            } else {
                target random enemy
                use Aero
            }
        } else {
            target random enemy
            use Aero
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    if (alive_count(ally team) == 1) {
        target self
        use null
    } else {
        target self
        use null
    }
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 120: Raijin

Variables: `no_male_line_done` = varA (named), `heal_line_done` = varB (named), `defeated` = varC (named)


### Init

```
if (defeated != 0) {
    return
}
no_male_line_done = 0
heal_line_done = 0
if (combat_scene == 83 /*G-Soldier+Raijin*/) {
    print+lock "{Zell} “You'll pay for this, Raijin!”"
} else {
    print+lock 'Raijin “Time to get serious, ya know!?”'
    waitText 01
}
return
```

### Turn

```
if (combat_scene == 83 /*G-Soldier+Raijin*/) {
    if (any_enemy_gender != male) {
        if (alive_count(ally team) != 1) {
            if (no_male_line_done == 0) {
                no_male_line_done = 1
                target self
                use null
                return
            } else {
                return
            }
        }
    }
    if (alive_count(ally team) != 1) {
        if (HP%(tgt87) < 50) {
            if (random(0..2) == 0) {
                targetStatus 00570009
                use Hi-Potion
            } else {
                targetStatus 00c800c8
                use Physical attack
            }
        } else {
            targetStatus 00c800c8
            use Physical attack
        }
    } else {
        target random enemy
        use Physical attack
    }
} else {
    if (any_enemy_gender != male) {
        if (alive_count(ally team) != 1) {
            if (no_male_line_done == 0) {
                no_male_line_done = 1
                target self
                use null
                return
            } else {
                if (HP%(tgt135) < 50) {
                    target random non-self ally
                    use Hi-Potion
                } else {
                    return
                }
            }
        } else {
            target random enemy
            use Physical attack
        }
    } else {
        targetStatus 00c800c8
        use one of Physical attack, Physical attack, Raijin Special
    }
}
return
```

### Counter

```
if (combat_scene == 84 /*Raijin+Fujin*/) {
    if (HP%(self) < 100) {
        if (heal_line_done == 0) {
            heal_line_done = 1
            target self
            use null
            target self
            use Hi-Potion
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    if (combat_scene == 83 /*G-Soldier+Raijin*/) {
        target self
        use null
    } else {
        add item drop Combat King 002 (non-battle-item, cross-confirmed via mngrp+mwepon)
        if (alive_count(ally team) == 1) {
            target self
            use null
        } else {
            target self
            use null
        }
    }
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 121: Ultimecia

Variables: `defeated` = varA (named), `alternate_turn` = varB (named), `ko_seen_once` = varC (named)


### Init

```
defeated = 0
alternate_turn = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (alternate_turn == 0) {
    alternate_turn = 1
    if (status(enemy team) has Death) {
        if (ko_seen_once == 0) {
            ko_seen_once = 1
        } else {
            if (random(0..2) != 0) {
                targetStatus 00c80000
                use Absorbed into time...
                print+lock 'Absorbed into time...'
                ko_seen_once = 0
            }
        }
    } else {
        ko_seen_once = 0
    }
    return
} else {
    alternate_turn = 0
    if (random(0..3) == 0) {
        return
    }
    if (all(enemy team) have Reflect) {
        if (random(0..1) == 0) {
            if (random(0..2) == 0) {
                target random enemy
                use Vacuum Wave
                return
            } else {
                target random enemy
                use Dispel
                if (status(self) has Double) {
                    target random enemy
                    use Dispel
                }
                return
            }
        }
    }
    if (random(0..4) == 0) {
        target all enemies
        use Maelstrom
        return
    }
    if (random(0..6) == 0) {
        target random enemy
        use Bio
        if (status(self) has Double) {
            if (alive_count(enemy team) != 0) {
                target random enemy
                use Bio
            }
        }
        return
    }
    if (random(0..1) == 0) {
        if (random(0..3) == 0) {
            targetStatus 00c800e6
            use Blizzaga
            if (status(self) has Double) {
                if (alive_count(enemy team) != 0) {
                    targetStatus 00c800e6
                    use Blizzaga
                }
            }
            return
        }
        if (random(0..2) == 0) {
            targetStatus 00c800e7
            use Thundaga
            if (status(self) has Double) {
                if (alive_count(enemy team) != 0) {
                    targetStatus 00c800e6
                    use Thundaga
                }
            }
            return
        }
        alternate_turn = 0
        if (status(self) lacks Double) {
            if (random(0..2) == 0) {
                target self
                use Double
                return
            }
        }
        targetStatus 00c800ec
        use Holy
        if (status(self) has Double) {
            if (alive_count(enemy team) != 0) {
                targetStatus 00c800ec
                use Holy
            }
        }
        return
    } else {
        if (random(0..5) == 0) {
            target random enemy
            use Dispel
            if (status(self) has Double) {
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Dispel
                }
            }
            return
        }
        if (random(0..2) == 0) {
            target all enemies
            use Tornado
            if (status(self) has Double) {
                if (alive_count(enemy team) != 0) {
                    target all enemies
                    use Tornado
                }
            }
            return
        }
        if (random(0..2) == 0) {
            target random enemy
            use Meltdown
            if (status(self) has Double) {
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Meltdown
                }
            }
            return
        }
        if (random(0..2) == 0) {
            target all enemies
            use Quake
            if (status(self) has Double) {
                if (alive_count(enemy team) != 0) {
                    target all enemies
                    use Quake
                }
            }
            return
        }
        if (random(0..2) == 0) {
            target random enemy
            use Stop
            if (status(self) has Double) {
                if (alive_count(enemy team) != 0) {
                    target random enemy
                    use Stop
                }
            }
            return
        }
        target all enemies
        use Maelstrom
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use Ultimecia First Death
    leave 200
    activate
    enter 2
}
return
```

## 122: {Griever}

Variables: `alternate_turn` = varA (named), `turn_counter` = varB (named), `pulsar_line_done` = varC (named), `defeated` = varD (named), `pulsar_charge_done` = varE (named), `ko_seen_once` = varF (named)


### Init

```
alternate_turn = 0
turn_counter = 0
pulsar_line_done = 0
target self
use Griever Summon
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (alternate_turn == 1) {
    alternate_turn = 0
    if (turn_counter >= 4) {
        if (turn_counter <= 6) {
            return
        }
    }
    if (status(enemy team) has Death) {
        if (ko_seen_once == 0) {
            ko_seen_once = 1
        } else {
            if (random(0..2) != 0) {
                targetStatus 00c80000
                use Absorbed into time...
                print+lock 'Absorbed into time...'
                ko_seen_once = 0
                return
            }
        }
    } else {
        ko_seen_once = 0
    }
    if (random(0..2) == 0) {
        if (status(enemy team) has Has-Magic) {
            targetStatus 00c8002e
            use Ultimecia Blow Away Magic
            blow away target magic
            return
        }
    }
} else {
    alternate_turn = 1
    if (random(0..3) == 0) {
        return
    }
    turn_counter += 1
    if (turn_counter == 4) {
        alternate_turn = 0
        pulsar_charge_done = 1
        target self
        use Do Nothing?
        return
    }
    if (turn_counter == 5) {
        return
    }
    if (turn_counter == 6) {
        if (pulsar_line_done == 0) {
            pulsar_line_done = 1
            target self
            use null
        }
        target all enemies
        use Shockwave Pulsar
        return
    }
    if (turn_counter == 8) {
        turn_counter = 0
        target random enemy
        use ??
        return
    }
    if (random(0..2) == 0) {
        if (random(0..1) == 0) {
            if (status(enemy team) has Has-Magic) {
                targetStatus 00c8002e
                use Draw
                draw magic
                cast drawn magic
                return
            } else {
                target random enemy
                use ??
                return
            }
        } else {
            if (random(0..1) == 0) {
                target random enemy
                use ??
                return
            } else {
                target all enemies
                use Gravija
                return
            }
        }
    }
    if (random(0..2) == 0) {
        if (status(enemy team) lacks Doom) {
            targetStatus 00c8031a
            use Doom
            return
        }
    }
    if (random(0..3) == 0) {
        if (status(self) lacks Triple) {
            if (status(self) lacks Reflect) {
                target self
                use Triple
                return
            } else {
                if (status(enemy team) has Reflect) {
                    targetStatus 00c80017
                    use Triple
                    return
                } else {
                    target random enemy
                    use ??
                    return
                }
            }
        }
    }
    if (random(0..2) == 0) {
        if (all(enemy team) have Reflect) {
            if (status(self) has Reflect) {
                target self
                use Pain
                if (status(self) has Triple) {
                    if (alive_count(enemy team) != 0) {
                        target self
                        use Pain
                    }
                    if (alive_count(enemy team) != 0) {
                        target self
                        use Pain
                    }
                }
                return
            } else {
                if (random(0..2) == 0) {
                    target random enemy
                    use Dispel
                    if (status(self) has Triple) {
                        if (alive_count(enemy team) != 0) {
                            target random enemy
                            use Dispel
                        }
                        if (alive_count(enemy team) != 0) {
                            target random enemy
                            use Dispel
                        }
                    }
                    return
                } else {
                    if (random(0..2) == 0) {
                        target self
                        use Reflect
                        return
                    } else {
                        target random enemy
                        use ??
                        return
                    }
                }
            }
        } else {
            targetStatus 00c80317
            use Pain
            if (status(self) has Triple) {
                if (alive_count(enemy team) != 0) {
                    targetStatus 00c80317
                    use Pain
                }
                if (alive_count(enemy team) != 0) {
                    targetStatus 00c80317
                    use Pain
                }
            }
            return
        }
    }
    if (random(0..2) == 0) {
        if (all(enemy team) have Reflect) {
            if (status(self) has Reflect) {
                target self
                use Flare
                if (status(self) has Triple) {
                    if (alive_count(enemy team) != 0) {
                        target self
                        use Flare
                    }
                    if (alive_count(enemy team) != 0) {
                        target self
                        use Flare
                    }
                }
                return
            } else {
                if (random(0..2) == 0) {
                    target random enemy
                    use Dispel
                    if (status(self) has Triple) {
                        if (alive_count(enemy team) != 0) {
                            target random enemy
                            use Dispel
                        }
                        if (alive_count(enemy team) != 0) {
                            target random enemy
                            use Dispel
                        }
                    }
                    return
                } else {
                    if (random(0..2) == 0) {
                        target self
                        use Reflect
                        return
                    } else {
                        target random enemy
                        use ??
                        return
                    }
                }
            }
        } else {
            targetStatus 00c80317
            use Flare
            if (status(self) has Triple) {
                if (alive_count(enemy team) != 0) {
                    targetStatus 00c80317
                    use Flare
                }
                if (alive_count(enemy team) != 0) {
                    targetStatus 00c80317
                    use Flare
                }
            }
            return
        }
    }
    if (random(0..2) == 0) {
        if (status(enemy team) has Has-Magic) {
            if (all(enemy team) have Reflect) {
                target random enemy
                use ??
                return
            } else {
                targetStatus 00c8002e
                use Draw
                draw magic
                cast drawn magic
                return
            }
        } else {
            target random enemy
            use ??
            return
        }
    } else {
        if (random(0..1) == 0) {
            target all enemies
            use Gravija
            return
        } else {
            target random enemy
            use ??
            return
        }
    }
}
```

### Death

```
if (defeated == 0) {
    if (pulsar_line_done == 0) {
        if (pulsar_charge_done == 0) {
            pulsar_charge_done = 1
            target self
            use Do Nothing?
        }
        target self
        use null
        target all enemies
        use Shockwave Pulsar
        pulsar_line_done = 1
    }
    if (alive_count(enemy team) != 0) {
        defeated = 1
        prepare summon
        target monster c0m123 (unnamed)
        use Griever Death
        leave 200
        enter 3
        loadAndTargetable 4
    }
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        if (pulsar_line_done == 0) {
            return
        } else {
            setHitAnim 3
        }
    }
}
return
```

## 123:  


### Init

```
become untargetable
target self
use Do Nothing?
target monster c0m124 (Ultimecia)
use Ultimecia Junctioning to Griever
leave 200
return
```

## 124: Ultimecia

Variables: `tail_fallen` = varA (named), `turn_phase` = varB (named), `part_spawn_step` = varC (named), `great_attractor_step` = varD (named), `defeated` = varE (named), `tail_fell_pending` = varF (named), `big_spell_cooldown` = varG (named), `ko_seen_once` = varH (named)


### Init

```
defeated = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (tail_fell_pending == 1) {
    battle_var[97] = 1
    tail_fell_pending = 0
    if (alive(battle_slot 1)) {
        targetBattleSlot 4
        use null
    }
    if (alive(battle_slot 2)) {
        targetBattleSlot 5
        use null
    }
}
if (turn_phase == 0) {
    turn_phase = 1
    if (great_attractor_step == 0) {
        if (status(enemy team) has Death) {
            if (ko_seen_once == 0) {
                ko_seen_once = 1
            } else {
                if (random(0..2) != 0) {
                    targetStatus 00c80000
                    use Absorbed into time...
                    print+lock 'Absorbed into time...'
                    ko_seen_once = 0
                    return
                }
            }
        } else {
            ko_seen_once = 0
        }
        if (alive(entity 0)) {
            if (status(tgt0) lacks Invincible) {
                if (status(tgt0) has Invocation-pending) {
                    target battle slot 0
                    use null
                    print+lock 'GF defense has been destroyed.'
                    return
                }
            }
        }
        if (alive(entity 1)) {
            if (status(tgt1) lacks Invincible) {
                if (status(tgt1) has Invocation-pending) {
                    target battle slot 1
                    use null
                    print+lock 'GF defense has been destroyed.'
                    return
                }
            }
        }
        if (alive(entity 2)) {
            if (status(tgt2) lacks Invincible) {
                if (status(tgt2) has Invocation-pending) {
                    target battle slot 2
                    use null
                    print+lock 'GF defense has been destroyed.'
                    return
                }
            }
        }
        if (alive(entity 3)) {
            if (status(tgt3) lacks Invincible) {
                if (status(tgt3) has Invocation-pending) {
                    target battle slot 3
                    use null
                    print+lock 'GF defense has been destroyed.'
                    return
                }
            }
        }
        if (alive(entity 4)) {
            if (status(tgt4) lacks Invincible) {
                if (status(tgt4) has Invocation-pending) {
                    target battle slot 4
                    use null
                    print+lock 'GF defense has been destroyed.'
                    return
                }
            }
        }
        if (alive(entity 5)) {
            if (status(tgt5) lacks Invincible) {
                if (status(tgt5) has Invocation-pending) {
                    target battle slot 5
                    use null
                    print+lock 'GF defense has been destroyed.'
                    return
                }
            }
        }
    }
} else {
    if (tail_fallen == 0) {
        turn_phase = 0
        if (random(0..3) == 0) {
            return
        }
        if (part_spawn_step == 0) {
            part_spawn_step = 1
            if (all(enemy team) have Reflect) {
                if (random(0..11) == 0) {
                    target random enemy
                    use Dispel
                } else {
                    target all enemies
                    use one of Quake, Ultima, Tornado
                }
            } else {
                if (random(0..1) == 0) {
                    if (random(0..2) == 0) {
                        if (random(0..11) == 0) {
                            target random enemy
                            use Dispel
                        } else {
                            target random enemy each hit
                            use Meteor
                        }
                    } else {
                        if (random(0..11) == 0) {
                            target random enemy
                            use Dispel
                        } else {
                            target all enemies
                            use one of Quake, Ultima, Tornado
                        }
                    }
                } else {
                    if (random(0..11) == 0) {
                        target random enemy
                        use Dispel
                    } else {
                        targetStatus 00c80317
                        use Holy
                    }
                }
            }
            return
        } else {
            if (part_spawn_step == 1) {
                part_spawn_step = 2
                assignSlot 4 4
                return
            } else {
                if (part_spawn_step == 2) {
                    part_spawn_step = 3
                    if (all(enemy team) have Reflect) {
                        if (random(0..11) == 0) {
                            target random enemy
                            use Dispel
                        } else {
                            target all enemies
                            use one of Quake, Ultima, Tornado
                        }
                    } else {
                        if (random(0..2) == 0) {
                            if (random(0..11) == 0) {
                                target random enemy
                                use Dispel
                            } else {
                                if (random(0..2) == 0) {
                                    target random enemy each hit
                                    use Meteor
                                } else {
                                    target all enemies
                                    use one of Quake, Ultima, Tornado
                                }
                            }
                        } else {
                            if (random(0..11) == 0) {
                                target random enemy
                                use Dispel
                            } else {
                                targetStatus 00c80317
                                use Holy
                            }
                        }
                    }
                    return
                } else {
                    if (part_spawn_step == 3) {
                        part_spawn_step = 4
                        assignSlot 5 5
                        return
                    }
                }
            }
        }
        if (great_attractor_step == 0) {
            great_attractor_step = 1
            if (all(enemy team) have Reflect) {
                if (random(0..11) == 0) {
                    target random enemy
                    use Dispel
                } else {
                    target all enemies
                    use one of Quake, Ultima, Tornado
                }
            } else {
                if (random(0..2) == 0) {
                    if (random(0..2) == 0) {
                        if (random(0..11) == 0) {
                            target random enemy
                            use Dispel
                        } else {
                            target random enemy each hit
                            use Meteor
                        }
                    } else {
                        if (random(0..11) == 0) {
                            target random enemy
                            use Dispel
                        } else {
                            target all enemies
                            use one of Quake, Ultima, Tornado
                        }
                    }
                } else {
                    if (random(0..11) == 0) {
                        target random enemy
                        use Dispel
                    } else {
                        targetStatus 00c80317
                        use Holy
                    }
                }
            }
        } else {
            if (alive(battle_slot 1)) {
                assignSlot 4 4
                return
            }
            if (alive(battle_slot 2)) {
                assignSlot 5 5
                return
            }
            if (great_attractor_step == 1) {
                great_attractor_step = 2
                target self
                use Do Nothing?
                target self
                use null
            } else {
                great_attractor_step = 0
                target all enemies
                use Great Attractor
            }
        }
    } else {
        great_attractor_step = 0
        if (turn_phase == 1) {
            turn_phase = 2
        } else {
            turn_phase = 0
        }
        if (random(0..3) == 0) {
            return
        }
        if (big_spell_cooldown == 0) {
            Speed multiplier = 300%
            if (random(0..2) != 0) {
                target random enemy
                use null
            } else {
                big_spell_cooldown = 1
                if (random(0..15) == 0) {
                    target random enemy
                    use Dispel
                } else {
                    target all enemies
                    use one of Quake, Ultima, Tornado
                }
            }
        } else {
            big_spell_cooldown = 0
        }
    }
}
return
```

### Counter

```
if (tail_fallen == 0) {
    if (HP%(self) < 40) {
        target self
        use Griever Tail Falling Off
        tail_fallen = 1
        tail_fell_pending = 1
        fill ATB
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    if (tail_fallen == 0) {
        if (HP%(self) < 40) {
            tail_fallen = 1
            battle_var[97] = 1
            target self
            use Griever Tail Falling Off
        }
    }
    target self
    use Griever + Ultimecia Death
    leave 1
    leave 2
    leave 200
    activate
    assignSlot 6 5
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (tail_fallen == 0) {
        if (HP%(self) < 40) {
            setHitAnim 15
        }
    } else {
        if (status(self) has Death) {
            setHitAnim 3
        }
    }
}
return
```

## 125: Helix

Variables: `hit_anim_flag` = varA (named)


### Init

```
target self
use null
return
```

### Counter

```
if (battle_var[97] == 1) {
    die
} else {
    if (last_command == Magic) {
        if (last_action_id == 50) {
            return
        }
    } else {
        if (random(0..2) == 0) {
            if (last_damage == physical) {
                target last attacker
                use null
            } else {
                if (last_damage == magical) {
                    target last attacker
                    use null
                }
            }
        }
    }
}
return
```

### Pre-hit

```
if (hit_anim_flag == 0) {
    setHitAnim 13
} else {
    setHitAnim 12
}
return
```

## 126: Ultimecia

Variables: `attack_cycle_step` = varA (named), `alternate_turn` = varB (named), `cycle_count` = varC (named), `death_speech_step` = varE (named), `defeated` = varF (named), `apocalypse_step` = varG (named), `ko_seen_once` = varH (named)


### Init

```
target self
use Ultimecia Final Form Spawn
assignSlot 7 6
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (alternate_turn == 1) {
    alternate_turn = 0
    if (status(enemy team) has Death) {
        if (ko_seen_once == 0) {
            ko_seen_once = 1
        } else {
            if (random(0..2) != 0) {
                targetStatus 00c80000
                use Absorbed into time...
                print+lock 'Absorbed into time...'
                ko_seen_once = 0
                return
            }
        }
    } else {
        ko_seen_once = 0
    }
    if (alive(entity 0)) {
        if (status(tgt0) lacks Invincible) {
            if (status(tgt0) has Invocation-pending) {
                target battle slot 0
                use null
                print+lock 'GF defense has been destroyed.'
                return
            }
        }
    }
    if (alive(entity 1)) {
        if (status(tgt1) lacks Invincible) {
            if (status(tgt1) has Invocation-pending) {
                target battle slot 1
                use null
                print+lock 'GF defense has been destroyed.'
                return
            }
        }
    }
    if (alive(entity 2)) {
        if (status(tgt2) lacks Invincible) {
            if (status(tgt2) has Invocation-pending) {
                target battle slot 2
                use null
                print+lock 'GF defense has been destroyed.'
                return
            }
        }
    }
    if (alive(entity 3)) {
        if (status(tgt3) lacks Invincible) {
            if (status(tgt3) has Invocation-pending) {
                target battle slot 3
                use null
                print+lock 'GF defense has been destroyed.'
                return
            }
        }
    }
    if (alive(entity 4)) {
        if (status(tgt4) lacks Invincible) {
            if (status(tgt4) has Invocation-pending) {
                target battle slot 4
                use null
                print+lock 'GF defense has been destroyed.'
                return
            }
        }
    }
    if (alive(entity 5)) {
        if (status(tgt5) lacks Invincible) {
            if (status(tgt5) has Invocation-pending) {
                target battle slot 5
                use null
                print+lock 'GF defense has been destroyed.'
                return
            }
        }
    }
    if (random(0..2) == 0) {
        if (status(enemy team) has Has-Magic) {
            targetStatus 00c8002e
            use Ultimecia Blow Away Magic
            blow away target magic
            return
        }
    }
} else {
    alternate_turn = 1
    if (HP%(self) > 30) {
        if (cycle_count <= 1) {
            if (attack_cycle_step == 0) {
                attack_cycle_step = 1
                target all enemies
                use Hell's Judgement
                return
            } else {
                if (attack_cycle_step == 1) {
                    attack_cycle_step = 2
                    return
                } else {
                    if (attack_cycle_step == 2) {
                        attack_cycle_step = 3
                        target all enemies
                        use Hell's Judgement
                        return
                    } else {
                        if (attack_cycle_step == 3) {
                            attack_cycle_step = 4
                            return
                        } else {
                            if (attack_cycle_step <= 6) {
                                attack_cycle_step += 1
                                if (random(0..2) == 0) {
                                    target random enemy
                                    use ??
                                } else {
                                    if (random(0..2) == 0) {
                                        target random enemy
                                        use Dispel
                                    } else {
                                        if (all(enemy team) have Reflect) {
                                            if (status(self) has Reflect) {
                                                target self
                                                use one of Flare, Holy, Holy
                                                return
                                            } else {
                                                target self
                                                use Reflect
                                                return
                                            }
                                        } else {
                                            targetStatus 00c80317
                                            use one of Flare, Holy, Holy
                                            return
                                        }
                                    }
                                }
                                return
                            } else {
                                attack_cycle_step = 0
                                cycle_count += 1
                                return
                            }
                        }
                    }
                }
            }
        }
        if (attack_cycle_step == 0) {
            attack_cycle_step = 1
            target all enemies
            use Hell's Judgement
            return
        } else {
            if (attack_cycle_step == 1) {
                attack_cycle_step = 2
                return
            } else {
                if (attack_cycle_step == 2) {
                    attack_cycle_step = 3
                    if (random(0..2) == 0) {
                        target random enemy
                        use ??
                    } else {
                        if (all(enemy team) have Reflect) {
                            target all enemies
                            use Ultima
                            return
                        } else {
                            targetStatus 00c80317
                            use one of Flare, Holy, Holy
                            return
                        }
                    }
                } else {
                    attack_cycle_step = 0
                    if (all(enemy team) have Reflect) {
                        if (status(self) has Reflect) {
                            target self
                            use one of Flare, Holy, Holy
                            return
                        } else {
                            target self
                            use Reflect
                            return
                        }
                    } else {
                        targetStatus 00c80317
                        use one of Flare, Holy, Holy
                        return
                    }
                }
            }
        }
    } else {
        if (alive(entity 143)) {
            if (apocalypse_step == 0) {
                apocalypse_step = 1
                target all enemies
                use Hell's Judgement
                targetableSlot 6
                return
            } else {
                if (apocalypse_step == 1) {
                    apocalypse_step = 2
                    target random non-self ally
                    use Draw Apocalypse
                    targetableSlot 6
                } else {
                    if (apocalypse_step == 2) {
                        apocalypse_step = 3
                        target all enemies
                        use Apocalypse
                        targetableSlot 6
                    } else {
                        apocalypse_step = 0
                        return
                    }
                }
            }
        } else {
            if (random(0..2) == 0) {
                target all enemies
                use Hell's Judgement
            } else {
                if (random(0..1) == 0) {
                    if (random(0..1) == 0) {
                        target all enemies
                        use Ultima
                    } else {
                        target random enemy each hit
                        use Meteor
                    }
                } else {
                    if (all(enemy team) have Reflect) {
                        if (status(self) has Reflect) {
                            target self
                            use one of Flare, Holy, Holy
                            return
                        } else {
                            target self
                            use Reflect
                            return
                        }
                    } else {
                        targetStatus 00c80317
                        use one of Holy, Holy, Flare
                    }
                }
            }
        }
    }
}
return
```

### Counter

```
if (last_command == Magic) {
    if (last_action_id == 28) {
        target last attacker
        use null
    }
}
return
```

### Death

```
if (death_speech_step == 5) {
    if (defeated == 0) {
        defeated = 1
        target self
        use Ultimecia Final Form Death
        leave 2
        leave 3
    }
} else {
    if (death_speech_step == 4) {
        death_speech_step = 5
        print+lock '“And...”'
        waitText 01
        addCurrentHP 64
        return
    } else {
        if (death_speech_step == 3) {
            death_speech_step = 4
            print+lock '“No matter...”'
            print+lock '“...how hard you hold on.”'
            print+lock '“It escapes you...”'
            waitText 03
            addCurrentHP 64
            return
        } else {
            if (death_speech_step == 2) {
                death_speech_step = 3
                print+lock '“Time...”'
                print+lock '“It will not wait...”'
                waitText 02
                addCurrentHP 64
                return
            } else {
                if (death_speech_step == 1) {
                    death_speech_step = 2
                    print+lock '“Your sensation...”'
                    print+lock '“Your words...”'
                    print+lock '“Your emotions...”'
                    waitText 03
                    addCurrentHP 64
                    return
                } else {
                    death_speech_step = 1
                    print+lock '“Reflect on your...”'
                    print+lock '“Childhood...”'
                    waitText 02
                    addCurrentHP 64
                    return
                }
            }
        }
    }
}
```

### Pre-hit

```
if (death_speech_step == 5) {
    if (defeated == 0) {
        if (status(self) has Death) {
            setHitAnim 3
        }
    }
}
return
```

## 127: Ultimecia


### Init

```
become untargetable
return
```

### Death

```
become untargetable
vanish (silent remove)
return
```

## 128: Seifer

Variables: `defeated` = varA (named), `turn_counter` = varB (named), `turn15_line_done` = varC (named)


### Init

```
defeated = 0
turn_counter = 0
turn15_line_done = 0
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
turn_counter += 1
if (turn_counter == 1) {
    if (odin_obtained == 1) {
        target self
        use Zantetsuken
        target self
        use null
        return
    } else {
        return
    }
}
if (turn_counter == 15) {
    if (odin_obtained == 1) {
        turn15_line_done = 1
        target self
        use null
        return
    }
}
if (random(0..2) != 0) {
    target random enemy
    use Seifer Physical Attack
} else {
    if (random(0..1) == 0) {
        if (HP%(self) < 50) {
            target all enemies
            use Bloodfest
        } else {
            target random enemy
            use null
        }
    } else {
        target random enemy
        use one of Firaga, Flare, null
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    if (odin_obtained == 1) {
        if (turn15_line_done == 0) {
            target self
            use null
        }
        leave 0
        leave 1
        unlock Gilgamesh
    } else {
        target self
        use null
    }
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        if (odin_obtained == 1) {
            return
        } else {
            setHitAnim 59
        }
    }
}
return
```

## 129: Slapper

Variables: `once_turn` = varA (auto)


### Init

```
battle_var[96] = 0
battle_var[97] = 0
once_turn = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (battle_var[96] != 0) {
    battle_var[96] += 1
    target random enemy
    use Physical attack
    if (battle_var[96] >= 7) {
        battle_var[96] = 0
    }
} else {
    if (battle_var[97] != 0) {
        battle_var[97] += 1
        target random enemy
        use Blizzara
        if (battle_var[97] >= 4) {
            battle_var[97] = 0
        }
    } else {
        if (once_turn == 0) {
            once_turn = 1
            if (random(0..4) == 0) {
                if (random(0..2) == 0) {
                    print+lock '“We have heart!  Go, Galbadia!”'
                    Strength multiplier = 200%
                    target random enemy
                    use null
                    Strength multiplier = 100%
                } else {
                    if (random(0..1) == 0) {
                        print+lock '“Formation G!  Go!!!”'
                        print+lock '“Roger!”'
                        waitText 02
                        battle_var[96] = 1
                    } else {
                        print+lock '“Formation M!  Go!!!”'
                        waitText 01
                        battle_var[97] = 1
                    }
                }
            } else {
                target random enemy
                use Physical attack
            }
        } else {
            once_turn = 0
        }
    }
}
return
```

## 130: Red Giant

Variables: `once_pre_hit` = varA (auto), `defeated` = varB (auto)


### Init

```
once_pre_hit = 0
return
```

### Turn

```
if (random(0..2) == 0) {
    return
}
if (once_pre_hit == 0) {
    if (random(0..2) == 0) {
        target all enemies
        use Gigantic Sword
    } else {
        target random enemy
        use null
    }
} else {
    target random enemy
    use null
}
return
```

### Counter

```
if (status(self) has VIT0) {
    return
} else {
    if (last_command == Attack) {
        print+lock '“GWahaHA!  PHysical attacKS?  USeleSS!”'
        return
    }
    if (last_command == Magic) {
        if (last_action_id == 13) {
            print+lock '“Urgh!  N-NO more DEMI, pleaSE...!!!”'
            return
        } else {
            if (last_action_id == 50) {
                return
            } else {
                print+lock '“THat magic is useleSS!”'
                return
            }
        }
    }
    if (last_command == GF) {
        if (last_action_id == 69) {
            print+lock '“{Diablos}!  Defeat is immineNT!”'
            return
        } else {
            print+lock '“THat GF is a waste of tiME!”'
            return
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
    leave 200
}
return
```

### Pre-hit

```
if (status(self) has Death) {
    if (defeated == 0) {
        setHitAnim 3
    }
} else {
    if (once_pre_hit == 0) {
        if (last_damage == physical) {
            if (HP%(self) < 30) {
                once_pre_hit = 1
                setHitAnim 16
            }
        } else {
            if (last_damage == magical) {
                if (HP%(self) < 30) {
                    once_pre_hit = 1
                    setHitAnim 16
                }
            }
        }
    }
}
return
```

## 131: Elnoyle

Variables: `turn_counter` = varA (auto)


### Init

```
turn_counter = 0
return
```

### Turn

```
if (varB != 0) {
    return
}
if (random(0..2) == 0) {
    return
}
turn_counter += 1
if (turn_counter == 6) {
    turn_counter = 0
    target random enemy
    use Death
} else {
    if (turn_counter == 5) {
        target all enemies
        use Storm Breath
    } else {
        if (turn_counter == 4) {
            target random enemy
            use one of Pain, Dispel, Pain
        } else {
            if (turn_counter == 3) {
                target random enemy
                use Physical attack/Tail Needle
            } else {
                if (turn_counter == 2) {
                    target random enemy
                    if (random(0..2) == 0) {
                        target random enemy each hit
                        use Meteor
                    } else {
                        if (random(0..1) == 0) {
                            if (status(enemy team) has Reflect) {
                                targetStatus 00c80017
                                use Dispel
                            } else {
                                target random enemy
                                use Dispel
                            }
                        } else {
                            target random enemy
                            use Holy
                        }
                    }
                } else {
                    target random enemy
                    use Physical attack
                }
            }
        }
    }
}
return
```

### Counter

```
if (last_damage == physical) {
    if (group_level(enemy team) == 2) {
        if (random(0..2) == 0) {
            return
        } else {
            target last attacker
            use Physical attack
        }
    }
}
return
```

## 132: Tiamat

Variables: `defeated` = varA (auto), `turn_counter` = varB (auto)


### Init

```
turn_counter = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
turn_counter += 1
if (turn_counter == 1) {
    print 'D         '
} else {
    if (turn_counter == 2) {
        print 'Da        '
    } else {
        if (turn_counter == 3) {
            print 'Dar       '
        } else {
            if (turn_counter == 4) {
                print 'Dark F    '
            } else {
                if (turn_counter == 5) {
                    print 'Dark Fla  '
                } else {
                    turn_counter = 0
                    target all enemies
                    use Dark Flare
                }
            }
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
    leave 200
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 133: Catoblepas

Variables: `turn_counter` = varA (auto), `defeated` = varB (auto)


### Init

```
turn_counter = 0
print+lock '“I am Catoblepas.”'
print+lock '“What do you humans plan to do...”'
print+lock '“Against the likes of me...?”'
waitText 03
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (random(0..2) == 0) {
    return
}
if (turn_counter >= 3) {
    if (random(0..2) == 0) {
        turn_counter = 0
        target all enemies
        use Thunder Summon
    }
} else {
    if (random(0..1) == 0) {
        if (random(0..1) == 0) {
            turn_counter += 1
            targetStatus 00c800e7
            use Thundaga
        } else {
            turn_counter += 1
            target random enemy
            use Thundaga
        }
    } else {
        if (random(0..2) != 0) {
            target random enemy
            use Physical attack
        } else {
            target random enemy
            use Deadly Horn
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    Magic multiplier = 200%
    target random enemy each hit
    use Meteor
    target self
    use null
    die
}
return
```

## 134: Wedge

Variables: `enraged` = varA (named), `ouch_line_done` = varB (named), `ally_hit_line_done` = varC (named)


### Turn

```
if (battle_var[96] == 0) {
    return
}
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use Physical attack
    return
}
if (HP%(self) < 100) {
    if (enraged == 0) {
        enraged = 1
        Strength multiplier = 200%
        Magic multiplier = 200%
        print "Wedge “I don't wanna be demoted!”"
        target random enemy
        use Physical attack
        print 'Wedge is pissed!'
        set_scan_text 'Pissed...'
    } else {
        target random enemy
        use one of Physical attack, Physical attack, Fire
    }
} else {
    target random enemy
    use one of Physical attack, Physical attack, Fire
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (attacker(left=1) == 151) {
    if (battle_var[98] == 1) {
        battle_var[98] = 0
    } else {
        if (ally_hit_line_done == 0) {
            ally_hit_line_done = 1
            print+lock "Wedge “Stop pickin' on us!”"
        }
    }
} else {
    if (last_command == Magic) {
        if (last_action_id == 46) {
            return
        }
    }
    if (last_command == Magic) {
        if (last_action_id == 47) {
            return
        }
    }
    if (last_command == Magic) {
        if (last_action_id == 50) {
            return
        }
    }
    if (last_command == Magic) {
        if (last_action_id >= 21) {
            if (last_action_id <= 41) {
                return
            }
        }
    }
    if (ouch_line_done == 0) {
        if (last_damage == physical) {
            ouch_line_done = 1
            print+lock 'Wedge “O-Ouch!”'
            print+lock "Wedge “They're always trouble...”"
        } else {
            if (last_damage == magical) {
                ouch_line_done = 1
                print+lock 'Wedge “O-Ouch!”'
                print+lock "Wedge “They're always trouble...”"
            }
        }
    }
}
return
```

### Death

```
print 'Wedge “W-Why...?”'
die
return
```

## 135: Biggs

Variables: `half_hp_line_done` = varA (named)


### Init

```
print+lock 'Biggs “I was demoted because of you!”'
print+lock "Biggs “I'm only a lieutenant now!”"
print+lock "Biggs “I'll get my revenge!”"
waitText 03
return
```

### Turn

```
save.prison_biggs_fought = 1
battle_var[96] = 1
if (random(0..2) == 0) {
    return
}
if (status(self) has Confuse) {
    target random non-self ally
    use null
    return
}
if (HP%(self) < 50) {
    if (half_hp_line_done == 0) {
        half_hp_line_done = 1
        print+lock "Biggs “We're just getting started!”"
    } else {
        if (random(0..2) == 0) {
            target random enemy
            use Physical attack
        } else {
            if (random(0..1) == 0) {
                target random enemy
                use one of Thundara, Slow, Slow
            } else {
                battle_var[98] = 1
                target random ally
                use one of Cure, Haste, Regen
            }
        }
    }
} else {
    target random enemy
    use Physical attack
}
return
```

### Counter

```
battle_var[98] = 0
if (status(self) has Confuse) {
    return
}
if (attacker(left=1) == 150) {
    print 'Biggs “You idiot!  What are you doing!”'
    target random non-self ally
    use null
    print+lock 'Wedge “Yikes, what was I doing!?”'
}
return
```

### Death

```
print "Biggs “What's below lieutenant...?”"
die
return
```

## 136: Fujin

Variables: `defeated` = varA (named), `turn_counter` = varB (named)


### Init

```
defeated = 0
turn_counter = 0
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (random(0..3) == 0) {
    return
}
if (turn_counter <= 2) {
    turn_counter += 1
    if (random(0..2) == 0) {
        target random enemy
        use Zan
    } else {
        if (random(0..1) == 0) {
            target random enemy
            use one of Slow, Confuse, Blind
        } else {
            target random ally
            use Haste
        }
    }
} else {
    if (turn_counter == 3) {
        turn_counter += 1
        target self
        use null
        target random enemy each hit
        use Meteor
    } else {
        if (random(0..1) == 0) {
            if (random(0..2) == 0) {
                target all enemies
                use Metsu
            } else {
                target random enemy
                use one of Zan, Zan, Sai
            }
        } else {
            if (random(0..2) == 0) {
                target random ally
                use Regen
            } else {
                if (random(0..2) == 0) {
                    target all enemies
                    use Tornado
                } else {
                    target random enemy
                    use one of Slow, Pain, Pain
                }
            }
        }
    }
}
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 137: Raijin

Variables: `defeated` = varA (named), `attack_counter` = varB (named), `half_hp_line_done` = varC (named), `targets_anyone` = varD (named), `opening_line_done` = varE (named)


### Init

```
defeated = 0
attack_counter = 0
half_hp_line_done = 0
targets_anyone = 0
fill ATB
return
```

### Turn

```
if (defeated != 0) {
    return
}
if (opening_line_done == 0) {
    opening_line_done = 1
    target self
    use null
    return
}
if (status(self) has Aura) {
    Strength multiplier = 150%
    Magic multiplier = 150%
} else {
    Strength multiplier = 100%
    Magic multiplier = 100%
}
if (random(0..2) == 0) {
    return
}
if (targets_anyone == 0) {
    if (any_enemy_gender != male) {
        targets_anyone = 1
        target self
        use null
        target random enemy
        use Physical attack
        return
    }
}
if (attack_counter <= 5) {
    attack_counter += 1
    if (targets_anyone == 0) {
        targetStatus 00c800c8
    } else {
        target random enemy
    }
    use Physical attack
} else {
    if (attack_counter == 6) {
        attack_counter += 1
        target self
        use null
        target self
        use Aura
        if (status(self) has Aura) {
            Strength multiplier = 150%
            Magic multiplier = 150%
        }
        target self
        use null
        if (targets_anyone == 0) {
            targetStatus 00c800c8
        } else {
            target random enemy
        }
        use Raijin Special
    } else {
        if (targets_anyone == 0) {
            targetStatus 00c800c8
        } else {
            target random enemy
        }
        use one of Physical attack, Raijin Special, null
    }
}
return
```

### Counter

```
if (HP%(self) < 50) {
    if (half_hp_line_done == 0) {
        half_hp_line_done = 1
        if (attacker(left=1) == 0) {
            target self
            use null
        } else {
            target self
            use null
        }
    }
}
return
```

### Death

```
if (defeated == 0) {
    defeated = 1
    target self
    use null
}
return
```

### Pre-hit

```
if (defeated == 0) {
    if (status(self) has Death) {
        setHitAnim 3
    }
}
return
```

## 138: UFO?


### Init

```
fill ATB
return
```

### Turn

```
die
return
```

## 139: UFO?


### Init

```
fill ATB
return
```

### Turn

```
die
return
```

## 140: UFO?


### Init

```
fill ATB
return
```

### Turn

```
die
return
```

## 141: UFO?


### Init

```
fill ATB
return
```

### Turn

```
die
return
```

## 142: Gunblade

Variables: `attack_cycle` = varA (named), `intro_line_done` = varB (named)


### Init

```
attack_cycle = 0
fill ATB
return
```

### Turn

```
attack_cycle += 1
if (intro_line_done == 0) {
    if (alive(entity 0)) {
        attack_cycle += 1
        print+lock '{Squall} “What the...?”'
    } else {
        if (alive(entity 1)) {
            attack_cycle += 1
            print+lock '{Zell} “...The hell is this!?”'
        } else {
            if (alive(entity 5)) {
                attack_cycle += 1
                print+lock '{Selphie} “Ewww!  Nasty!”'
            }
        }
    }
    intro_line_done = 1
} else {
    if (random(0..3) == 0) {
        return
    }
    if (attack_cycle == 1) {
        target random enemy
        use Physical attack
    } else {
        if (attack_cycle == 2) {
            if (random(0..2) == 0) {
                if (status(enemy team) lacks Berserk) {
                    if (alive_count(enemy team) == 1) {
                        target random enemy
                        use Sleep
                    } else {
                        target random enemy
                        use Berserk
                    }
                } else {
                    target random enemy
                    use Dispel
                }
            } else {
                target random enemy
                use Silence
            }
        } else {
            if (attack_cycle == 2) {
                target random enemy
                use Physical attack
            } else {
                attack_cycle = 0
                target random enemy
                use "Brrawghh!"
            }
        }
    }
}
return
```

## 143: Base Soldier


### Init

```
if (combat_scene == 179 /*Base Soldier*/) {
    print+lock '“How dare you mess up our plan!”'
    waitText 01
}
return
```

### Turn

```
if (battle_var[97] == 1) {
    targetStatus 00c800cc
    use Physical attack
    return
} else {
    if (battle_var[97] == 2) {
        target random enemy
        use Blizzara
        return
    }
}
if (status(ally team) has Confuse) {
    if (random(0..3) == 0) {
        targetStatus 00c9001e
        use Remedy
        return
    }
}
if (status(ally team) has Silence) {
    if (random(0..3) == 0) {
        targetStatus 00c90004
        use Remedy
        return
    }
}
if (combat_scene == 175 /*Base Soldier+Base Leader*/) {
    if (battle_var[99] == 0) {
        if (HP%(self) < 50) {
            battle_var[99] = 1
            target self
            use null
            return
        }
    }
}
target random enemy
use Physical attack
return
```

### Counter

```
if (status(self) has Confuse) {
    return
}
if (last_damage == physical) {
    if (random(0..5) == 0) {
        target self
        use Potion
    }
} else {
    if (last_damage == magical) {
        if (random(0..5) == 0) {
            target self
            use Potion
        }
    }
}
return
```

### Death

```
if (combat_scene == 179 /*Base Soldier*/) {
    print "“You're all going down!”"
} else {
    if (battle_var[98] == 0) {
        battle_var[96] = 1
        battle_var[98] = 1
        print '“Ughhhh!”'
    } else {
        battle_var[96] = 1
        print '“C-Captain...”'
    }
}
die
return
```
