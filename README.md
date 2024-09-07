# NATS CLI Documentation

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Basic Commands](#basic-commands)
4. [Managing Streams](#managing-streams)
5. [Working with Contexts](#working-with-contexts)
6. [Configuring File-Based Contexts](#configuring-file-based-contexts)
7. [Managing Multiple File-Based Configurations](#managing-multiple-file-based-configurations)
8. [Example Context File](#example-context-file)
9. [Helpful Commands](#helpful-commands)

---

## Introduction

This document provides an overview of the NATS CLI, covering installation, basic commands, managing streams, working with contexts, and more.

---

## Installation

To install the NATS CLI, follow the steps below:

1. Download the latest release from the [NATS CLI GitHub repository](https://github.com/nats-io/natscli).
2. Extract the downloaded file.
3. Add the extracted binary to your system's PATH.

---

## Basic Commands

### Connecting to a NATS Server
```bash
nats server run
```

### Checking the Server Status
```bash
nats server info
```

### Publishing a Message
```bash
nats pub <subject> <message>
```

### Subscribing to a Subject
```bash
nats sub <subject>
```

### Request-Reply
```bash
nats req <subject> <message>
```

---

## Managing Streams

### Creating a Stream
```bash
nats stream add <stream_name> --subjects <subject>
```

### Listing Streams
```bash
nats stream ls
```

### Deleting a Stream
```bash
nats stream rm <stream_name>
```

### Purging a Stream
```bash
nats stream purge <stream_name>
```

### Deleting a Specific Message
```bash
nats stream rm-msg <stream_name> --seq <sequence_number>
```

---

## Working with Contexts

### Adding a Context
```bash
nats context add <context_name> --server <server_url>
```

### Switching Contexts
```bash
nats context select <context_name>
```

### Listing Contexts
```bash
nats context ls
```

### Removing a Context
```bash
nats context rm <context_name>
```

---

## Configuring File-Based Contexts

File-based contexts allow you to manage NATS configurations through a configuration file.

### Example File-Based Context

Create a file named `nats-context.conf`:

```ini
# NATS Context Configuration
name = "production-context"
description = "NATS context for the production environment"

[nats]
  url = "nats://localhost:4222"
  username = "user"
  password = "password"
  token = "mysecrettoken"

[jetstream]
  account = "JSAccount"
  domain = "my_domain"

[tls]
  cert_file = "/path/to/certificate.crt"
  key_file = "/path/to/private.key"
  ca_file = "/path/to/ca_certificate.crt"

[auth]
  creds = "/path/to/creds/file.creds"
```

### Loading a File-Based Context
```bash
nats context import <context_name> --file nats-context.conf
```

---

## Managing Multiple File-Based Configurations

### Adding Multiple Configurations

You can manage multiple environments (e.g., production, development) by creating separate context files:

1. `nats-prod.conf` for production.
2. `nats-dev.conf` for development.

### Switching Between Configurations

Switch between configurations by loading the appropriate context file:

```bash
nats context import <context_name> --file <config_file>
```

### Example Usage
```bash
nats context import prod --file nats-prod.conf
nats context import dev --file nats-dev.conf
```

---

## Helpful Commands

- **Creating a Stream**:
  ```bash
  nats stream add <stream_name> --subjects <subject>
  ```

- **Listing Streams**:
  ```bash
  nats stream ls
  ```

- **Deleting a Stream**:
  ```bash
  nats stream rm <stream_name>
  ```

- **Purging a Stream**:
  ```bash
  nats stream purge <stream_name>
  ```

- **Deleting a Specific Message**:
  ```bash
  nats stream rm-msg <stream_name> --seq <sequence_number>
  ```

- **Adding a Context**:
  ```bash
  nats context add <context_name> --server <server_url>
  ```

- **Switching Contexts**:
  ```bash
  nats context select <context_name>
  ```

- **Listing Contexts**:
  ```bash
  nats context ls
  ```

- **Removing a Context**:
  ```bash
  nats context rm <context_name>
  ```

- **Loading a File-Based Context**:
  ```bash
  nats context import <context_name> --file nats-context.conf
  ```

---

## Example Context File

### File Name: `nats-context.conf`

### Example Context File (`nats-context.conf`):

```ini
# NATS Context Configuration
name = "production-context"
description = "NATS context for the production environment"

[nats]
  url = "nats://localhost:4222"
  username = "user"
  password = "password"
  token = "mysecrettoken"

[jetstream]
  account = "JSAccount"
  domain = "my_domain"

[tls]
  cert_file = "/path/to/certificate.crt"
  key_file = "/path/to/private.key"
  ca_file = "/path/to/ca_certificate.crt"

[auth]
  creds = "/path/to/creds/file.creds"
```

