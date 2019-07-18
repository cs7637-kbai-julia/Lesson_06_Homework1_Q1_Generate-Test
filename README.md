### Homework 1 - Question 1: Rey, Kylo, Snoke transportation problem

Rey has managed to capture Snoke and Kylo Ren on the planet Quesh. Quesh has a poisonous atmosphere, however, and so Rey, Snoke, and Kylo Ren will have to be kept together in quarantine for two weeks upon arriving back on the orbiting ship.

Only one shuttle is available to transfer individuals back and forth between Quesh and the orbiting ship, and that shuttle can only seat one person. The shuttle has an autopilot, though, so it can fly without anyone in it.

Leia, in the orbiting ship, refuses to let Rey be alone with Snoke (without Kylo) either on the planet or in quarantine, knowing that Snoke will turn Rey to the dark side. Snoke would rather stay and die than let Rey be alone with Kylo Ren, knowing that she will turn Kylo to the light side. Leia wants Snoke alive, and therefore agrees to his demand that Kylo and Rey never be alone together (without Snoke) either on the planet or in quarantine. It is okay, however, for Kylo & Rey or Rey & Snoke to be together if the shuttle is with them, as long as one of them departs on the shuttle.

In simple terms: the goal is to move Rey, Snoke, and Kylo from the planet to the ship. Only one can move at a time, and the shuttle can move without a passenger. Rey and Kylo can never be alone together without the shuttle, and Rey and Snoke can never be alone together without the shuttle. (If you do are unfamiliar with Star Wars, know that this paragraph contains everything you need to know to solve this problem.)

First, construct a semantic network representing this problem. This should take approximately half a page, including a figure of two states with a transition between them. Make sure to include all components of the state, and an operator indicating how we transition from one state to another.

Second, apply generate & test to this semantic network in order to solve the problem. In applying generate & test, your generator should be smart enough to only make valid moves (e.g. it will not try to move two people at once or make consecutive planet-to-ship moves without the transport ship coming back), but it should not be smart enough to only make moves that result in valid states (e.g. it should still try to move Kylo first, even though that move results in an invalid state). Your tester, in turn, should check each generated state to see if (a) it follows the rules, and (b) if it has met the goal. You may decide whether identifying states that have already been visited is the responsibility of the generator or the tester.

Include the entire semantic network that solves this problem. Clearly indicate which states are failed, and why. The semantic network should explore the entire problem space: every state should be either ruled out or have its following states explored.

transfer: from planet Quesh -> to orbiting ship with Leia

vehicle: one shuttle - max 1 passenger only - autopilot

passengers: Ray, Kylo, Snoke

can be kept together: Rey+Kylo+shuttle, Rey+Snoke+shuttle

can't be kept together: Rey+Snoke w/o Kylo, Rey+Kylo w/o Snoke

Start state: Quesh(Ray, Kylo, Snoke, shuttle), Ship()

End state: Quesh(), Ship(Ray, Kylo, Snoke, shuttle)

### Output
`parent   Planet        shuttle     Ship
====== ==============  =======  =================
       --------------  Step:0   -----------------
  ->.1 Rey Kylo Snoke     <-                         VALID
       --------------  Step:1   -----------------
.1->.1     Kylo Snoke     ->     Rey                 VALID
.1->.2 Rey      Snoke     ->         Kylo            illegal
.1->.3 Rey Kylo           ->              Snoke      illegal
.1->.4 Rey Kylo Snoke     ->                         empty shuttle to empty place
       --------------  Step:2   -----------------
.1->.1 Rey Kylo Snoke     <-                         loop
.1->.2     Kylo Snoke     <-     Rey                 VALID
       --------------  Step:3   -----------------
.2->.1          Snoke     ->     Rey Kylo            VALID
.2->.2     Kylo           ->     Rey      Snoke      VALID
.2->.3     Kylo Snoke     ->     Rey                 loop
       --------------  Step:4   -----------------
.1->.1 Rey      Snoke     <-         Kylo            VALID
.1->.2     Kylo Snoke     <-     Rey                 loop
.1->.3          Snoke     <-     Rey Kylo            illegal
.2->.4 Rey Kylo           <-              Snoke      VALID
.2->.5     Kylo Snoke     <-     Rey                 loop
.2->.6     Kylo           <-     Rey      Snoke      illegal
       --------------  Step:5   -----------------
.1->.1          Snoke     ->     Rey Kylo            loop
.1->.2 Rey                ->         Kylo Snoke      VALID
.1->.3 Rey      Snoke     ->         Kylo            illegal
.4->.4     Kylo           ->     Rey      Snoke      loop
.4->.5 Rey                ->         Kylo Snoke      repeat occurrence within step
.4->.6 Rey Kylo           ->              Snoke      illegal
       --------------  Step:6   -----------------
.2->.1 Rey Kylo           <-              Snoke      VALID
.2->.2 Rey      Snoke     <-         Kylo            loop
.2->.3 Rey                <-         Kylo Snoke      VALID
       --------------  Step:7   -----------------
.1->.1     Kylo           ->     Rey      Snoke      VALID
.1->.2 Rey                ->         Kylo Snoke      loop
.1->.3 Rey Kylo           ->              Snoke      illegal
.3->.4                    ->     Rey Kylo Snoke      REACHED GOAL
.3->.5 Rey                ->         Kylo Snoke      loop
                    ---- END ----`
