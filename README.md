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
