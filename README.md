# navCSP RMS Task Constraints

```
class Task { stage : 1-1 reference, characteristics : 1-* reference}
class Stage { machines : 0-* reference}
class Task { characteristics : 1-* reference}
class Characteristics {}

context Task inv SameCharacteristic:
  Machine.AllInstances()->select(m | m.characteristics->includesAll(self.characteristics))
    ->includesAll(self.var(stage).var(machines))


context Task inv Precedence:
  self.prev.stage =< self.stage
```
## Compilation & exécution
```bash
# build
./gradlew build

# run
./gradlew run
```


## OCL Refactor
This also demonstraits our refactoring around annotations, the original charachteristics constraint being:
```
context Task inv SameCharacteristic:
  self.var(stage).var(machines).forall(m | m.characteristics->includesAll(self.characteristics))
```
in the refactor, we determine candidates and constraint the variable query `self.var(stage).var(machines) to be among them.
