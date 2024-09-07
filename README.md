
# NATS CLI Documentation

## Table of Contents
- [Installation](#installation)
- [Configuration](#configuration)
  - [Adding Context](#adding-context)
  - [Managing Multiple Connections](#managing-multiple-connections)
- [Stream Management](#stream-management)
  - [Creating a Stream](#creating-a-stream)
  - [Viewing Stream Information](#viewing-stream-information)
  - [Purging a Stream](#purging-a-stream)
  - [Deleting a Stream](#deleting-a-stream)
- [Message Management](#message-management)
  - [Deleting a Specific Message](#deleting-a-specific-message)
  - [Removing a Deleted Message](#removing-a-deleted-message)
- [Helpful Commands](#helpful-commands)

## Installation

To install the NATS CLI, download the appropriate binary for your operating system from the [NATS GitHub Releases](https://github.com/nats-io/natscli/releases) page. Extract the binary and place it in your system's PATH.

Alternatively, if you are on macOS, you can use Homebrew:

```sh
brew install nats-io/nats-tools/nats
```

Verify the installation by running:

```sh
nats --version
```

## Configuration

### Adding Context

Contexts are a way to manage different NATS environments. A context is a combination of NATS servers, credentials, and other connection settings.

To add a new context:

```sh
nats context add <context_name> --server <nats_server_url> --user <username> --password <password>
```

For example:

```sh
nats context add mycontext --server nats://localhost:4222 --user myuser --password mypass
```

To list all contexts:

```sh
nats context ls
```

To use a specific context:

```sh
nats context select <context_name>
```

### Managing Multiple Connections

You can manage multiple connections by creating multiple contexts and switching between them as needed.

To add multiple contexts:

```sh
nats context add context1 --server nats://server1:4222 --user user1 --password pass1
nats context add context2 --server nats://server2:4222 --user user2 --password pass2
```

Switch between contexts:

```sh
nats context select context1
nats context select context2
```

## Stream Management

### Creating a Stream

To create a stream:

```sh
nats stream add <stream_name> --subjects <subject_name> --storage <file_or_memory> --retention <policy>
```

Example:

```sh
nats stream add mystream --subjects "foo.>" --storage file --retention limits
```

### Viewing Stream Information

To view information about a stream:

```sh
nats stream info <stream_name>
```

### Purging a Stream

To purge a stream:

```sh
nats stream purge <stream_name>
```

To purge a stream but keep the stream configuration:

```sh
nats stream purge <stream_name> --keep
```

### Deleting a Stream

To delete a stream:

```sh
nats stream rm <stream_name>
```

## Message Management

### Deleting a Specific Message

To delete a specific message from a stream by sequence number:

```sh
nats stream delmsg <stream_name> --seq <sequence_number>
```

Example:

```sh
nats stream delmsg mystream --seq 10
```

### Removing a Deleted Message

After a message is deleted, you can compact the stream:

```sh
nats stream compact <stream_name>
```

## Helpful Commands

- **List All Streams**:
  ```sh
  nats stream ls
  ```

- **List All Messages in a Stream**:
  ```sh
  nats stream view <stream_name>
  ```

- **List All Consumers**:
  ```sh
  nats consumer ls <stream_name>
  ```

- **Viewing a Specific Message**:
  ```sh
  nats stream get <stream_name> --seq <sequence_number>
  ```

- **Viewing Stream Configuration**:
  ```sh
  nats stream info <stream_name> --json
  ```

This documentation should cover the most common tasks you'll need to perform with NATS using the CLI. For more advanced features or updates, refer to the [official NATS documentation](https://docs.nats.io) or the [NATS CLI GitHub repository](https://github.com/nats-io/natscli).

## Helpful Commands

- **List All Streams**:
  ```sh
  nats stream ls
  ```

- **List All Messages in a Stream**:
  ```sh
  nats stream view <stream_name>
  ```

- **List All Consumers**:
  ```sh
  nats consumer ls <stream_name>
  ```

- **Viewing a Specific Message**:
  ```sh
  nats stream get <stream_name> --seq <sequence_number>
  ```

- **Viewing Stream Configuration**:
  ```sh
  nats stream info <stream_name> --json
  ```

- **List All Contexts**:
  ```sh
  nats context ls
  ```

- **Delete a Specific Context**:
  ```sh
  nats context rm <context_name>
  ```

- **Switch to a Different Context**:
  ```sh
  nats context select <context_name>
  ```

- **View Current Context Details**:
  ```sh
  nats context
  ```

- **Add a New Stream**:
  ```sh
  nats stream add <stream_name>
  ```

- **Update an Existing Stream**:
  ```sh
  nats stream update <stream_name>
  ```

- **Delete a Stream**:
  ```sh
  nats stream rm <stream_name>
  ```

- **Purge a Stream**:
  ```sh
  nats stream purge <stream_name>
  ```

- **Compact a Stream**:
  ```sh
  nats stream compact <stream_name>
  ```

- **View a Specific Message by Sequence**:
  ```sh
  nats stream get <stream_name> --seq <sequence_number>
  ```

- **Delete a Specific Message by Sequence**:
  ```sh
  nats stream delmsg <stream_name> --seq <sequence_number>
  ```

- **List All Consumers for a Stream**:
  ```sh
  nats consumer ls <stream_name>
  ```

- **View Details of a Consumer**:
  ```sh
  nats consumer info <stream_name> <consumer_name>
  ```

- **Create a New Consumer**:
  ```sh
  nats consumer add <stream_name> <consumer_name>
  ```

- **Delete a Consumer**:
  ```sh
  nats consumer rm <stream_name> <consumer_name>
  ```

- **Pause a Consumer**:
  ```sh
  nats consumer pause <stream_name> <consumer_name>
  ```

- **Resume a Paused Consumer**:
  ```sh
  nats consumer resume <stream_name> <consumer_name>
  ```

- **Get the Last Message for a Subject**:
  ```sh
  nats stream last <stream_name> --subject <subject_name>
  ```

- **Check JetStream Account Information**:
  ```sh
  nats account info
  ```

- **Check Server Status**:
  ```sh
  nats server report jetstream
  ```

- **Monitor Server Connections**:
  ```sh
  nats server report connections
  ```

- **Monitor Stream Statistics**:
  ```sh
  nats server report stats
  ```
