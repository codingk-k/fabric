# peer snapshot

The `peer snapshot` command allows administrators to perform snapshot related
operations on a peer, such as submit a snapshot request, cancel a snapshot request
and list pending requests. Once a snapshot request is submitted for a specified
block number, the snapshot will be automatically generated when the block number is
committed on the channel.

## Syntax

The `peer snapshot` command has the following subcommands:

  * cancelrequest
  * listpending
  * submitrequest

## peer snapshot cancelrequest
```
Cancel a request for a snapshot at the specified block.

Usage:
  peer snapshot cancelrequest [flags]

Flags:
  -b, --blockNumber uint         The block number for which a snapshot will be generated
  -C, --channelID string         The channel on which this command should be executed
  -h, --help                     help for cancelrequest
      --peerAddress string       The address of the peer to connect to
      --tlsRootCertFile string   The path to the TLS root cert file of the peer to connect to, required if TLS is enabled and ignored if TLS is disabled.
```


## peer snapshot listpending
```
List pending requests for snapshots.

Usage:
  peer snapshot listpending [flags]

Flags:
  -C, --channelID string         The channel on which this command should be executed
  -h, --help                     help for listpending
      --peerAddress string       The address of the peer to connect to
      --tlsRootCertFile string   The path to the TLS root cert file of the peer to connect to, required if TLS is enabled and ignored if TLS is disabled.
```


## peer snapshot submitrequest
```
Submit a request for a snapshot at the specified block. When the blockNumber parameter is set to 0 or not provided, it will submit a request for the last committed block.

Usage:
  peer snapshot submitrequest [flags]

Flags:
  -b, --blockNumber uint         The block number for which a snapshot will be generated
  -C, --channelID string         The channel on which this command should be executed
  -h, --help                     help for submitrequest
      --peerAddress string       The address of the peer to connect to
      --tlsRootCertFile string   The path to the TLS root cert file of the peer to connect to, required if TLS is enabled and ignored if TLS is disabled.
```

## Example Usage

### peer snapshot cancelrequest example

Here is an example of the `peer snapshot cancelrequest` command.

  * Cancel a snapshot request for block number 1000 on channel `mychannel`
    for `peer0.org1.example.com:7051`:

    ```
    peer snapshot cancelrequest -C mychannel -b 1000 --peerAddress peer0.org1.example.com:7051

    Snapshot request cancelled successfully

    ```

    A successful response indicates that the snapshot request for block number 1000 has been removed from `mychannel`.
    If there is no pending snapshot request for block number 1000, the command will return an error.

  * Use the `--tlsRootCertFile` flag in a network with TLS enabled

### peer snapshot listpending example

Here is an example of the `peer snapshot listpending` command.
If a snapshot is already generated, the corresponding block number will be removed from the pending list.

  * List pending snapshot requests on channel `mychannel`
    for `peer0.org1.example.com:7051`:

    ```
    peer snapshot listpending -C mychannel --peerAddress peer0.org1.example.com:7051

    Successfully got pending snapshot requests: [1000 5000]

    ```

    You can see that the command returns a list of block numbers for the pending snapshot requests.

  * Use the `--tlsRootCertFile` flag in a network with TLS enabled

### peer snapshot submitrequest example

Here is an example of the `peer snapshot submitrequest` command.

  * Submit a snapshot request for block number 1000 on channel `mychannel`
    for `peer0.org1.example.com:7051`:

    ```
    peer snapshot submitrequest -C mychannel -b 1000 --peerAddress peer0.org1.example.com:7051

    Snapshot request submitted successfully

    ```

    You can see that the snapshot request is successfully submitted on channel `mychannel`.
    A snapshot will be automatically generated after the block number 1000 is committed on the channel.

    The specified block number must be at or above the last block number on the channel.
    Otherwise, the command will return an error.

  * Use the `--tlsRootCertFile` flag in a network with TLS enabled

