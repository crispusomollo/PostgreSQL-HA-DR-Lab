# PostgreSQL HA + DR Lab

A hands-on lab for **PostgreSQL High Availability and Disaster Recovery**, featuring:

- Primary ↔ Replica replication
- Automatic failover and promotion
- WAL archiving
- pg_rewind rejoin
- Chaos testing & RTO/RPO measurements

---

## Features

- **Automated setup**: `install.sh` builds primary & replica clusters
- **Verification**: `verify.sh` checks replication, writes test data
- **Chaos simulation**: `chaos.sh` kills primary to simulate failure
- **Failover automation**: `failover.sh` promotes standby
- **Rejoin automation**: `rejoin.sh` uses `pg_rewind` for old node
- **Monitoring**: `monitor.sh` shows node status and replication lag
- **Cleanup**: `cleanup.sh` removes clusters safely
- **Demo scripts**: `demo/demo.sh` with sample-data.sql

---

## Directory Structure

```
systemd/
├─ postgres-ha-primary.service
├─ postgres-ha-replica.service

config/
├─ primary.conf
├─ replica.conf
├─ archive.conf

docs/
├─ architecture.md
├─ failover-walkthrough.md
├─ disaster-recovery-playbook.md
├─ screenshots/

demo/
├─ demo.sh
├─ sample-data.sql
```

---

## Getting Started

### Prerequisites

- PostgreSQL 16 installed
- Linux environment (WSL, Ubuntu recommended)
- `sudo` privileges

### Setup

```bash
sudo ./install.sh
```

- Installs primary (port 5436) and replica (port 5437)
- Configures replication and WAL archiving
- Starts clusters and verifies replication

### Verify

```bash
./verify.sh
```

- Checks primary/replica connectivity
- Verifies replication status
- Performs a write-test

### Failover & Chaos

```bash
./chaos.sh
./failover.sh
./rejoin.sh
```

- Simulates primary failure
- Promotes standby
- Rejoins old primary using `pg_rewind`

---

## Monitoring

```bash
./monitor.sh
```

- Displays current role (PRIMARY/STANDBY)
- Shows replication lag
- Tracks WAL receiver and sender status

---

## Cleanup

```bash
sudo ./cleanup.sh
```

- Stops clusters
- Removes cluster data safely

---

## Documentation

- `docs/architecture.md` — HA & DR architecture diagram
- `docs/failover-walkthrough.md` — step-by-step failover demo
- `docs/disaster-recovery-playbook.md` — emergency recovery checklist
- `docs/screenshots/` — sample screenshots of lab

---

## Notes

- This lab is for **learning and testing purposes only**.
- Original data from previous clusters is **not preserved**.
- Best practice: always backup
