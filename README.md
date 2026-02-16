# MYTHICAL-WORLD-KNOWLEDGE-ENGINE
Prolog
/* ===============================
   MYTHICAL WORLD KNOWLEDGE ENGINE
   =============================== */

/* ---------- ELEMENT TYPES ---------- */

element(fire).
element(water).
element(earth).
element(air).
element(light).
element(darkness).
element(ether).

/* ---------- CREATURE TYPES ---------- */

creature(dragon).
creature(phoenix).
creature(leviathan).
creature(griffin).
creature(titan).
creature(angel).
creature(demon).
creature(hydra).
creature(serpent).

/* ---------- ELEMENT CONTROL ---------- */

controls(dragon, fire).
controls(phoenix, fire).
controls(phoenix, light).
controls(leviathan, water).
controls(griffin, air).
controls(titan, earth).
controls(angel, light).
controls(demon, darkness).
controls(hydra, water).
controls(serpent, ether).

/* ---------- POWER LEVELS ---------- */

power(dragon, 900).
power(phoenix, 850).
power(leviathan, 920).
power(griffin, 700).
power(titan, 880).
power(angel, 950).
power(demon, 940).
power(hydra, 870).
power(serpent, 800).

/* ---------- ELEMENT ADVANTAGE RULES ---------- */

strong_against(fire, earth).
strong_against(water, fire).
strong_against(earth, air).
strong_against(air, water).
strong_against(light, darkness).
strong_against(darkness, light).
strong_against(ether, fire).

/* ---------- WEAKNESS RULE ---------- */

weak_against(X,Y) :- strong_against(Y,X).

/* ---------- HYBRID CREATURE ---------- */

hybrid(X,Y,hybrid_xy) :-
    creature(X),
    creature(Y),
    X \= Y.

/* ---------- BATTLE RESULT ---------- */

battle(C1, C2, C1) :-
    power(C1, P1),
    power(C2, P2),
    P1 > P2.

battle(C1, C2, C2) :-
    power(C1, P1),
    power(C2, P2),
    P2 > P1.

battle(C1, C2, draw) :-
    power(C1, P),
    power(C2, P).

/* ---------- ELEMENT BATTLE ---------- */

element_battle(E1, E2, winner(E1)) :-
    strong_against(E1, E2).

element_battle(E1, E2, winner(E2)) :-
    strong_against(E2, E1).

element_battle(E1, E2, neutral) :-
    \+ strong_against(E1, E2),
    \+ strong_against(E2, E1).

/* ---------- DESTINY SYSTEM ---------- */

destiny(Creature, conqueror) :-
    power(Creature, P),
    P > 930.

destiny(Creature, guardian) :-
    controls(Creature, light).

destiny(Creature, destroyer) :-
    controls(Creature, darkness).

destiny(Creature, neutral) :-
    \+ destiny(Creature, conqueror),
    \+ destiny(Creature, guardian),
    \+ destiny(Creature, destroyer).

/* ---------- ENERGY COMPATIBILITY ---------- */

compatible(C1, C2) :-
    controls(C1, E),
    controls(C2, E),
    C1 \= C2.

incompatible(C1, C2) :-
    controls(C1, E1),
    controls(C2, E2),
    strong_against(E1, E2).

/* ---------- EVOLUTION RULE ---------- */

evolves(dragon, ancient_dragon).
evolves(phoenix, eternal_phoenix).
evolves(angel, archangel).
evolves(demon, overlord).
evolves(titan, primordial_titan).

/* ---------- PROPHECY SYSTEM ---------- */

prophecy(world_end) :-
    power(demon, P1),
    power(angel, P2),
    P1 > 900,
    P2 > 900.

prophecy(balance_restored) :-
    compatible(angel, dragon).

prophecy(elemental_chaos) :-
    strong_against(fire, air),
    strong_against(water, earth).

/* ---------- ANCIENT RELIC SYSTEM ---------- */

relic(flame_sword, fire).
relic(trident_of_depths, water).
relic(earth_hammer, earth).
relic(wings_of_tempest, air).
relic(holy_crown, light).
relic(abyss_orb, darkness).

wields(dragon, flame_sword).
wields(leviathan, trident_of_depths).
wields(titan, earth_hammer).
wields(griffin, wings_of_tempest).
wields(angel, holy_crown).
wields(demon, abyss_orb).

/* ---------- TOTAL DOMINANCE CHECK ---------- */

total_dominance(Creature) :-
    destiny(Creature, conqueror),
    evolves(Creature, _),
    wields(Creature, _).

/* ===============================
   END OF SYSTEM
   =============================== */
   #OUTPUT
   
