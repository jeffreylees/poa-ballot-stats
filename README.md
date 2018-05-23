# POA Ballot Stats

POA Ballot Stats is a command line tool that displays voting statistics for the [POA Network](https://poa.network/). The purpose of this tool is to provide visibility into ballot statistics for token holders on the POA Network. The tool will indicate each Validator and the amount of ballots they have been able to vote on versus the amount they have missed.

This will further provide insight into the responsibilities of Validators, the fulfillment of those responsibilities, and into how successful the current ballot procedures are. The initial requirements for this tool were described in [RFC9 "Statistics of ballots"](https://github.com/poanetwork/RFC/issues/9).

## Installation and Setup

* Usage of the Ballot Stats tool requires a recent version of [Rust](https://www.rust-lang.org/).
* The Ballot Stats tool needs to communicate with a fully synchronized node that is connected to the POA Network (you can follow the [POA Installation Guide](https://github.com/poanetwork/wiki/wiki/POA-Installation) to set up a node if you have not done so already). 
* The tool needs access to the full logs of the POA Network, so you must run the node with the option `--pruning=archive --no-warp`. 

## Basic Usage

The Ballot Stats tool can be run with default arguments successfully. However, more customization may be required at times. To this end, there are several arguments which customize the behavior of the tool, allowing a custom endpoint, a verbose mode, custom contract maps, or a time-based filter on results.

### Usage Arguments

Arguments can be supplied when running the Ballot Stats tool with the following syntax:

```bash
$ cargo run -- [argument] [value]
```

See the table below for a listing of currently available arguments.

| Argument | Value | Description |
| --- | --- | --- |
| `-h` | N/A | View the command line options. |
| N/A | string | This argument does not have a short argument, but is simply a URL value for the JSON-RPC endpoint. A usage example would be `cargo run -- https://sokol.poa.network`. Defaults to `http://127.0.0.1:8545` |
| `-v` | N/A | Runs the tool in verbose mode, and shows the completed list of collected events. |
| `-c` | string | Takes as a value a map with the POA contracts' addresses, in JSON format. The current maps for the main and test networks can be found in the `contracts` folder. By default, the value is `contracts/core.json` for the main network. |
| `-p` | string | Takes as a value a [time interval](https://docs.rs/parse_duration/1.0.1/parse_duration/#units) in hours, days, weeks, months, etc. This value refers to the date of ballot creation. For instance, `-p "10 weeks"` will return statistics for ballots that were created within the last ten weeks. |

### Usage Examples

The tool can be run without any arguments at all:

```bash
$ cargo run
```

With a single parameter:

```bash
$ cargo run -- -v
$ cargo run -- -c contracts/sokol.json
```

Or with multiple parameters:

```bash
$ cargo run -- -c contracts/sokol.json https://sokol.poa.network -v
```

## Screenshots

![Screenshot](screenshot.png)
