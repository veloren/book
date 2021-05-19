# Wiring

## General system overview

Shallow definitions:
* *Circuit* component is a backbone of whole system. It stores information about from where and to where data has to be passed.
* *Wire* is part of *Circuit* (one circuit can have many wires) it stores data from what entity and under what field name value has to be passed to what entity and field name.
* *Wiring* component is a "worker" it knows what data it has and what has to be performed when executing it.
* *OutputFormula* takes inputs (and own config) and produces output.

> If something can't be calculated, but given place has to result in some value - it will result in f32 0.

Each wiring component has 3 informations.
1. Inputs (data injected by *Circuit*)
2. Outputs (information of _how_ to compute output)
3. Actions (information about what should happen if inputs are in given state)

Each wiring tick has 3 stages:
1. Compute (take each *Wiring* component, feed inputs into output formulas, produce outputs)
2. Transport (get outputs of previous step and using *Circuit* pass them around)
3. Dispatch (get inputs (note that we are using _modified_ state by transport) and dispatch logic)

### Compute

* Take all wiring components and map them
* Calculate each outputs output formula
* Construct outputs with type `HashMap<E, Hashmap<F, V>>` where:
    * *E* is an `specs::Entity` that holds certain wiring component.
    * *F* is a `String` representing field name.
    * *V* is a resulting value of OutputFormula. (atm all results are `f32`)

### Transport

* Take circuits and for each circuit take attached wires *
* Take every wire and for each wire *
* Get `from what entity`, `from what field`, `to what entity` and `to what field` from wire.
* Perform something like `to what entity`.inputs[`to what field`] = `from what entity`[`from what field`] **
> \* It is basically "take every wire" in loaded server data
>
> \*\* Keep in mind that we are using product of Compute step as right hand of this simplification.

### Dispatch

* For each action in every wiring component
* If wiring action formula output* is more or equal to action threshold...
* Dispatch each effect attached to the wiring action
> \* Calculated using inputs

## Output formulas

### Constant
Outputs constant value.

### Input
Outputs value of input field under given name.

### Logic
Allows composing output formulas. It takes `left` and `right` output formulas which are calculated, and then performs logic on them.

Available logic kinds (I refer to `left` and `right` output as *side*):
* Min - return value of lower side.
* Max - return value of higher side.
* Sub - return value of `left - right`.
* Sum - return value of `left + right`.
* Mul - return value of `left * right`.

### Sine wave (not implemented)
Takes server time and returns sine of it.

### OnCollide
If physics captures collision for attached entity (`touching_entities`) returns given value.

### OnInteract (not implemented)
If something interacts (e.g. player is "pulling" lever) returns given value.

### OnDeath
Returns `value * count of entities that died in last tick in given radius`.

## Actions

### Spawn projectile
Spawns projectile using projectile constructor.

### Set block collidability (not implemented)
Modifies properties of block on certain coordinates.

### Set light
Changes `LightEmitter` properties of attached entity.
