import random

class Character:
    def __init__(self, name, health, base_attack, base_defense):
        self.name = name
        self.health = health
        self.base_attack = base_attack
        self.base_defense = base_defense

    def attack(self):
        return self.base_attack

    def defend(self):
        return self.base_defense

    def is_alive(self):
        return self.health > 0

    def __str__(self):
        return f"{self.name} (Vida: {self.health})"


class Hero(Character):
    def __init__(self, name, health, base_attack, base_defense):
        super().__init__(name, health, base_attack, base_defense)
        self.level = 1
        self.experience = 0

    def attack(self):
        if random.random() < 0.2:
            return self.use_magic()
        else:
            bonus = random.randint(0, 10)
            damage = self.base_attack + bonus
            print(f"{self.name} ataca com força total ({damage} de dano).")
            return damage

    def use_magic(self):
        spells = {
            "Bola de Fogo": random.randint(25, 40),
            "Raio de Gelo": random.randint(20, 35),
            "Golpe Divino": random.randint(30, 45)
        }
        spell_name, damage = random.choice(list(spells.items()))
        print(f"{self.name} usa {spell_name}! ({damage} de dano mágico).")
        return damage

    def defend(self):
        block = random.choice([True, False])
        defense = self.base_defense + 10 if block else self.base_defense
        if block:
            print(f"{self.name} bloqueou parte do ataque.")
        return defense

    def gain_experience(self, xp):
        self.experience += xp
        print(f"{self.name} ganhou {xp} XP (Total: {self.experience}).")
        while self.experience >= 100:
            self.level += 1
            self.experience -= 100
            self.health += 20
            self.base_attack += 5
            self.base_defense += 3
            print(f"{self.name} subiu para o nível {self.level}!")
            print(f"Atributos melhorados: Vida {self.health}, Ataque {self.base_attack}, Defesa {self.base_defense}.")


class Enemy(Character):
    def attack(self):
        variation = random.randint(-5, 15)
        damage = self.base_attack + variation
        print(f"{self.name} ataca ({damage} de dano).")
        return damage

    def defend(self):
        resistance = random.randint(0, 5)
        return self.base_defense + resistance


class Orc(Enemy):
    def attack(self):
        variation = random.randint(0, 8)
        damage = self.base_attack + variation
        print(f"{self.name} (Orc) ataca ({damage} de dano).")
        return damage


class Goblin(Enemy):
    def attack(self):
        variation = random.randint(-3, 6)
        damage = self.base_attack + variation
        print(f"{self.name} (Goblin) ataca ({damage} de dano).")
        return damage


def battle(heroes, enemies):
    print("A BATALHA COMEÇA!\n")
    round_number = 1
    turn_limit = 20

    while any(h.is_alive() for h in heroes) and any(e.is_alive() for e in enemies) and round_number <= turn_limit:
        print(f"\n--- RODADA {round_number} ---")
        attacker_type = random.choice(["hero", "enemy"])

        if attacker_type == "hero":
            attacker = random.choice([h for h in heroes if h.is_alive()])
            defender = random.choice([e for e in enemies if e.is_alive()])
        else:
            attacker = random.choice([e for e in enemies if e.is_alive()])
            defender = random.choice([h for h in heroes if h.is_alive()])

        print(f"{attacker.name} está atacando {defender.name}.")
        attack_value = attacker.attack()
        defense_value = defender.defend()
        final_damage = max(1, attack_value - defense_value)
        defender.health -= final_damage
        print(f"{defender.name} recebeu {final_damage} de dano. Vida restante: {defender.health}")

        if not defender.is_alive():
            print(f"{defender.name} foi derrotado!")
            if isinstance(attacker, Hero):
                attacker.gain_experience(random.randint(40, 70))

        round_number += 1

    print("\nFIM DA BATALHA!")
    if any(h.is_alive() for h in heroes):
        print("Os heróis venceram!")
    elif any(e.is_alive() for e in enemies):
        print("Os inimigos venceram!")
    else:
        print("A batalha terminou empatada!")


if __name__ == "__main__":
    heroes = [
        Hero("Aragorn", 100, 20, 10),
        Hero("Legolas", 80, 18, 8)
    ]

    enemies = [
        Orc("Gorgul", 90, 15, 5),
        Goblin("Snark", 60, 12, 3)
    ]

    battle(heroes, enemies)
