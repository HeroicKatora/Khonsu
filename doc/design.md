# Major objectives

* Decentral
* Plain
* Minimal
* Explicit
* Compatible

## Decentral

Everyone should be able to operate or contact a service under her own control
without the need for a central register. In case of opportunity, resist the urge
to create an easy central component and build a reusable and decentral
replacement instead.

## Plain

Avoid binary(-like) formats that can only be read or interpreted with special
purpose programs with small user basis. As a sanity check, ensure that a major
usecase outside this binary exists. Only deviate from this for established
solutions in the domain of calendar apps. This is aimed to ensure that other
developers can work with and alongside the application, so widespread developer
tools or languages (e.g. git, python, …) do count as plaintext.

## Minimal

Keep your assumptions about sensible behaviour in check. Resist the urge to
perform additional work without explicit requests (see Compatible). This also
includes such things as user-tracking, metrics, beacons, etc.. Screw that.

## Explicit

Hide unconnected complexity but keep all operations explicit. That is, it is
fine to group actions or rename them for the sake of usability but keep the
amount of automatically performed system interactions at a minimum. This should
prevent operating poorly in the face of adjusted or extended environments. One
example for this behaviour is deferring changes made on the ui to an explicit
acknowledgement but nevertheless rechecking consistency with the state the user
assumes they are applied to.

## Compatible

Keep it open and well-documented, such that the produced data is usable without
executing this/these binaries, and without reading their sources. Try to limit
the amount of conversion to special purpose formats for imports but supply
explicit converters on request where possible.

