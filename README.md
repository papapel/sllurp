# sllurp

This repository began in August 2013 as a snapshot of the dormant
[LLRPyC project][]'s [code][] on SourceForge.  It has been violently updated to
work with Impinj Speedway readers (and probably still other readers), and to
provide a simple callback-based API to clients.

[LLRPyC project]: http://wiki.enneenne.com/index.php/LLRPyC
[code]: http://sourceforge.net/projects/llrpyc/.

## Quick Start

To connect to a reader and perform EPC Gen 2 inventory for 10 seconds:

1. Figure out your reader's IP address `ip.add.re.ss`
2. `./simple_inventory.py ip.add.re.ss`

Run `./simple_inventory.py -h` to see options.

## Reader API

Interactions with the reader are brokered by a `llrp.LLRPReaderThread` object;
see `simple_inventory.py` for an example.  This class provides a simple API to
expose interesting events to programs.

 * `addCallback(eventType, func)`: Every time the reader receives an LLRP
   message of type `eventType` (e.g., `RO_ACCESS_REPORT` reports tag reads),
   call the function `func` with the representative `LLRPMessage` object as its
   argument.
 * `start_inventory()`: Starts the reader performing inventory.
 * `stop_inventory()`: Cleanly stops the active inventory operation.