# [Deprecated] uint384-cairo

CAUTION: This repo is decrecated. A working uint384 library is contained in the repo `research-384bit-prime-field-arithmetic`(https://github.com/NethermindEth/research-384bit-prime-field-arithmetic-cairo). 

For more context: originally `research-uint384` and `research-384bit-prime-field-arithmetic` were separate libraries. However the latter library makes extensive use of the former, and due to Cairo's non-importability of custom libraries (as of July 2022), we ended up copying `research-uint384` inside `research-384bit-prime-field-arithmetic`. Subsequently we made tiny improvements to the `research-uint384` library version inside the field arithmetic library, and this caused the present repo to become outdated.



--------------


Cairo implementation of basic operations between unsigned 384-bit integers. Some operations are also supported for signed 384-bit integers.  (Note that Cairo's native "integer" is of 251 bits)

**NOTE**: All hints were whitelisted on Cairo v0.9.1 (20 Jul 2022). 

The library follows and extends Cairo's common library `uint256`. The usage and logic is almost the same as in `uint256`. All operations from `uint256` are implemented here for 384 bits. 

Recall that in `uint256`, 256-bit integers are represented by the struct:

    # Represents an integer in the range [0, 2^384)
    struct Uint256:
        # The low 128 bits of the value.
        member low : felt
        # The high 128 bits of the value.
        member high : felt
    end

We extend this to 384 bits by defining the struct

    # Represents an integer in the range [0, 2^384)
    struct Uint384:
        # The low 128 bits of the value.
        member d0 : felt
        # The middle 128 bits of the value.
        member d1 : felt    
        # The high 128 bits of the value.
        member d1 : felt
    end

**NOTE**: All operations here expect each member of `Uint384` to be a felt smaller than 2**128. Similarly, all the returned instances of `Uint384` satisfy this condition. Using this library without meeting this requirement can result in unexpected behavior.

## Namespace

We use a namespace so that all library functions can be imported at once with `from <library directory>.uint384 import uint384` and functions can be called with the syntax `uint384.<function_name>` (this differs from the original `uint256`)

## Testing

We include a simple StarkNet contract and a pytest test for every library function (except some auxiliary functions that are used within other functions). The project is structured following Nile's framework.

## Contributors

[0xNonCents](https://github.com/0xNonCents), [albert_g](https://github.com/albert-garreta)
