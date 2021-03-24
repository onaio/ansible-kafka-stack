# Canopy Kafka Service Stack

## What it does

This playbook brings up a Kafka cluster of `B` brokers (communicating via `Z` zookeepers),.  It also (optionally) can provision:

* A distributed (Confluent) Schema Registry service, used to make flows more efficient with Avro
* A distributed Kafka Connect service, used to allow hosting of stateful flow logic
    * (requires Schema Registry)
* A Kafka backup/restore service which runs continuously and can be hooked to make `time interval` snapshots of topics
    * (requires standalone Kafka Connect and Schema Registry)

A lot of the deployment logic comes from the [cp-ansible](https://github.com/confluentinc/cp-ansible) project - this isn't packaged in a super-friendly way but we do our best.

See: `./examples/example_inventory.yml` for how to build your inventory.  For production systems it's recommended to have separate zookeeper, kafka broker, and backup/restore hosts.

## Canopy Kafka Variables and Roles

Configurable variables for the Canopy Kafka stack are prefixed with `canopy_kafka`_.   Inside the stack playbooks themselves the prefix is removed (and vars are defaulted, etc.), since they no longer will conflict with other inventory variables.

There are a few stack-specific roles - these are always imported as relative directories.  If they become more generally useful they could be promoted out of the stack?