# Change Proposal: Extended Modifier Support
## Owners
- Karsten Klein
  - karsten.klein@metaeffekt.com
  - https://github.com/karsten-klein

## Issue Statement

Currently, SPDX supports on exceptions as modifiers to licenses. On various occasions 
it was observed that the current options are too limited to model different license/modifier
constellations. 

The limitation has already produces various bloomers:

| Full Name                                          | Identifier | Alternative Expression              |
|----------------------------------------------------| --- |-------------------------------------|
| ANTLR Software Rights Notice with license fallback | ANTLR-PD-fallback | ANTLR-PD WITH PD-fallback           |
| n.a.                                               | LicenseRef-Apache-2.0-with-Commons-Clause | Apache-2.0 WITH CCL-Condition-1.0   |
| BSD-2-Clause Plus Patent License | BSD-2-Clause-Patent | BSD-2-Clause WITH Patent-Clause-1.0 |
| BSD 3-Clause No Military License | BSD-3-Clause-No-Military-License | BSD-3-Clause WITH Military-Use-Restriction | 

Thus, this change proposal suggests a greater conceptional change to the approach SPDX is 
currently modelling licenses.

Out of scope of this change proposal is how SPDX deals with license application or usage. 
These can be observed when SPDX includes modifiers on the level of an SPDX license id:
* -only/-or-later constructs
* -invariants/-no-invariants
* -RFN/-no-RFN 
* combinatorics of the above; such as -only-no-invariants.

In theory the proposal could be extended to also capture the license usage context / 
license application as a modifier or another concept. But at this level it is only 
meant to ignite further conceptual thoughts. 

## Proposed Solution

The solution anticipates that there is already a WITH operator for SPDX license expressions. 
As such, one can currently combine a license A with an exception E:
  
    A WITH E

where A is an SPDX license identifier and E is an SPDX exception identifier.

### Part 1

We understand that exceptions are a specific type of modifiers, while also other modifiers 
are possible. The following categories can already be observed:

* Exceptions (see https://spdx.org/licenses/exceptions-index.html) - Exceptions relax the
  existing obligations of a license. They usually do not reduce or modify grants.
* Restrictions (not yet available) - Restrictions may reduce the applicability of a license; 
  e.g. not for military use constructs or other domain restrictions. The above Commons Clause 
  Condition can be also be considered a restriction. Restrictions impair on the grants.
* Extensions (or Addons) - Extension provide additional grants or increase applicability of
  licenses.
* Other - The category other is applicable, when a modification cannot be clearly assigned.

Please note that a patent clause can be a restriction (in case a patent claim restricts 
applicability of provided grants), an extension (if a patent license is implicitly granted) or
it could also be both (moving the modifier to the other category)

### Part 2

The SPDX expression grammar is changed such that the WITH operator can be used with the
different modifiers:

    A WITH M

where A is a license id and M is a modifier. Please note, that support for exceptions is 
implicitly retained.  

## Describe the benefit to SPDX and its ecosystem

SPDX is enabled by the concept to model different combinations of licenses and modifiers 
providing an added-value to the SPDX community. Custom licenses and custom modifier can be
established benefiting from the extended expression capabilities. SPDX can significantly 
contribute to the consolidation and proliferation.

## Scope of impact

The change impacts
* license and modifier (currently exception) inclusion principles - initially the inclusion
  principles would be reviewed to capture the change. For the new modifier categories initially
  rather strict inclusion principles are provided to harness the initial impact.
* Existing licenses and exceptions - not immediately from the start, but as a midterm objective 
  the existing licenses and exceptions need to be revised, whether these can be replaced by a 
  modifier construct. This would imply deprecation of existing license/exception ids.
* SPDX expression grammar - The grammar needs to be extended to capture the change. The different 
  types (license, modifier types) must be distinguished to manage the degree of freedom.
* The organisation and management of exception extending the above modifier categories - This
  includes managing the different new categories and adapting current processes.

## Additional information

TBD