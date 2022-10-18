# Change Proposal: Record license exceptions

## Owner

- Alexios Zavras
	- alexios.zavras@intel.com
	- http://github.com/zvr

## Issue statement
*Provide a concise statement of the problem or issue that you want to solve, new use case you wish to cover, etc. Optionally include any issues that you would consider to be out of scope for your proposal.    
Briefly describe why existing capabilities of SPDX don’t effectively address this problem or issue.*

In many cases in real-world projects, the actual license that a piece of software is under is a "standard" license with an additional "exception". These exceptions grant an exception to a license condition or additional permissions beyond those granted in a license; they are not stand-alone licenses.

The SPDX Project maintains a [list of license exceptions](https://spdx.org/licenses/exceptions-index.html). These can be used in SPDX License Expressions with the `WITH` operator.

The current specification does not allow for recording exceptions found that these additional texts standalone, but only as parts of a license. The latest [guideline](https://spdx.github.io/spdx-spec/v2.3/SPDX-license-expressions/#d44-exception-with-operator) is to "use a single LicenseRef- to represent the entire license terms, including the exception."

## Proposed solution
*Provide a proposed resolution to solve this problem or issue.*

The proposed solution is to amend the specification, so that any additional text to a given license can be recorded like regular license text and be referenced by using the new prefix syntax `ExceptionRef-`.

Such additions will be able to be used in SPDX License Expressions in the right-hand side of the `WITH` operator.

### Example

```
ExceptionID: ExceptionRef-1
ExtractedText: <text> ... </text>
```


## Benefit to SPDX and its ecosystem
*Describe the audience in the SPDX ecosystem this proposal serves.
Include a statement as to how this fits into the overall mission/vision of SPDX.*
    
The proposed change allows recording and expressing more accurate licensing information, which closely aligns with the SPDX project mission and vision.


## Scope of impact
*Indicate which existing parts of the SPDX project are impacted.*

The **Specification** will be updated to introduce the new syntax.

Obviously, an updated syntax in the specification will impact the **SPDX language libraries** as well, since they will have to be updated to support the new syntax.

The **Ontology** in its current state will not be affected, since it does not include information on the content of a `LicenseException`, the same way that it does not distinguish between licenses in the SPDX License List and licenses defined with `LicenseRef`.


## Additional information
*Include any additional information that is relevant or may be helpful to understand the context and/or use case for this change proposal. Also include here links to any related, existing issue or discussions.*

### Previous discussions
The topic has been discussed in the past a number of times, almost as soon as the Exceptions were introduced in the SPDX License List.

The most recent discussion was in [issue 153 of spdx-spec repo](https://github.com/spdx/spdx-spec/issues/153).

### Alternatives considered

##### Not introducing new prefix
The current specification allows any license to be named and referenced with the prefix `LicenseRef-`.  If the definition were extended for this to refer to any legal text, even partial, there will be no need for introducing a new syntax convention.

However, this would result in an impossibility to distinguish between Licenses and Exceptions, therefore a construct like `LicenseRef-1 WITH LicenseRef-2` might be valid (if it were similar to `Apache-2.0 WITH LLVM-exception`) or not (if it were similar to `Apache-2.0 WITH BSD-3-Clause`).
