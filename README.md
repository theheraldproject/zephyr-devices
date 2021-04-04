# zephyr-devices

A set of utility and driver classes to support IC peripherals in Zephyr RTOS. 

Adopts the same layout structure as the main Zephyr repository here: 
https://github.com/zephyrproject-rtos/zephyr

## Background

The devices contained within this library have been used in the design
of the Herald Hardware project's wearable and bluetooth beacons for
eHealth and Digital Contact Tracing. They are provided here for wider
community benefit.

Information on the hardware designs can be found here:-
https://github.com/theheraldproject/herald-hardware

## Zephyr board definitions

We are providing board definitions for the latest bleeding edge board
designs we are working on here. We will contribute back to Zephyr once
each hardware design is ratified and physically tested.

The 'main' branch here is release quality, but the definitions may not
have made it into Zephyr upstream yet. The 'develop' branch is bleeding
edge but where each merged commit has been tested as per our contributing
guide. (See CONTRIBUTING.md)

## License and Copyright

All files are copyright 2021 Herald Project Contributors and
are provided under the Apache 2.0 license.

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache2.0-yellow.svg)](https://opensource.org/licenses/Apache-2.0)

See LICENSE.txt and NOTICE.txt for details.

