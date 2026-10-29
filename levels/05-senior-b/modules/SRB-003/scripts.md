# SRB-003 · Distributed data — Lecture scripts

**Video:** 86 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-003-L01 · Replication strategies (12 min)
**Goal:** compare leader-based, multi-leader, and leaderless replication by how they fail.

**Key points**
- Leader-based: one writer, followers copy; failover can lose recent writes if replication is asynchronous.
- Multi-leader: several writers across regions; fast local writes but conflicts must be resolved.
- Leaderless: any replica accepts writes; quorums and repair keep copies close.
- Synchronous replication costs latency; asynchronous costs durability on failure.

**Show:** a table with three columns (leader-based, multi-leader, leaderless) and rows: write path, conflict handling, failover behavior, typical systems. Verify product examples before recording.

**Check:** What can be lost in async leader failover? *(Recent writes not yet copied to the promoted follower.)*

---

## SRB-003-L02 · Consensus and Raft (14 min)
**Goal:** explain Raft well enough to judge systems that rely on it.

**Key points**
- Consensus makes a group agree on one ordered log despite failures.
- Raft: leader election by term, log replication, commit when a majority has the entry.
- A majority (quorum) is needed, so 3 nodes tolerate 1 failure, 5 tolerate 2.
- Without a majority the system stops accepting writes rather than diverge; that is a choice for consistency.

**Show:** a timeline of a 3-node cluster: leader N1 fails, N2 times out, requests votes in term 2, wins with N3, continues the log; a diagram of an entry committed once on 2 of 3 nodes.

**Check:** How many failures does a 5-node Raft group tolerate? *(Two, since a majority of three must remain.)*

---

## SRB-003-L03 · Quorums (10 min)
**Goal:** use read and write quorums to tune consistency.

**Key points**
- With N replicas, write to W and read from R; if R + W > N, reads overlap the latest write.
- Lower W or R gives speed and availability but weaker guarantees.
- Quorum overlap alone does not give linearizability under failures, concurrent writes, or sloppy quorums.
- Always walk through a failure scenario, not only the arithmetic.

**Show:** N=3 examples: W=2,R=2 overlaps; W=1,R=1 may read stale; then a scenario where a node is slow and a hinted handoff leaves a stale read.

**Check:** With N=3, W=2, R=2, do reads overlap writes? *(Yes, since 2 + 2 > 3, subject to caveats under failure.)*

---

## SRB-003-L04 · Consistency models, revisited (10 min)
**Goal:** place real guarantees on the consistency spectrum.

**Key points**
- Linearizable: behaves like one copy, ordered by real time.
- Sequential, causal, read-your-writes, monotonic reads, eventual: progressively weaker, cheaper.
- Choose per operation: stock reservations need strong; a product view count does not.
- CAP is about behavior during a partition: choose consistency or availability then; PACELC adds latency in normal operation.

**Show:** a ladder diagram from linearizable down to eventual, with FulfillCo examples attached to each rung: stock reservation, order status page, search index.

**Check:** Which operation needs the strongest model: stock reservation or view count? *(Stock reservation.)*

---

## SRB-003-L05 · Reading a Jepsen report (10 min)
**Goal:** use published analyses to test a vendor's claims.

**Key points**
- Jepsen tests databases under partitions and failures and checks histories against models.
- Read: version tested, configuration used, anomalies found, what was fixed.
- Results apply to that version and configuration; verify the current state before relying on them.
- No report is not proof of safety; combine with your own experiment.

**Show:** an annotated skim of a report: abstract, test setup, a lost-update finding, vendor response, and a checklist of what to note for our decision.

**Check:** Why check the tested version? *(Findings may be fixed or newly introduced in other versions.)*

---

## SRB-003-L06 · Demo: partitioning a three-node cluster and watching it choose (15 min)
**Goal:** observe a quorum-based store during a network partition.

**Steps**
1. Start a three-node cluster in containers (verify version before recording) and write a key.
2. Isolate one node and show writes still commit on the majority side.
3. Read from the isolated node and show it refuses or returns stale data depending on settings.
4. **Planned mistake:** isolate two nodes and expect writes to continue; fix by explaining that no majority means no commits.
5. Heal the partition and show the follower catching up.

Prepares SRB-003-LAB1.

---

## SRB-003-L07 · Demo: a quorum read returning stale data, explained (15 min)
**Goal:** trace how a read can be stale although R + W > N appears satisfied.

**Steps**
1. Set up N=3, W=2, R=2 and write a stock value of 10.
2. Introduce a slow replica and a sloppy-quorum or hinted-handoff write.
3. Show the read returning the old stock value of 12.
4. **Planned mistake:** blame the client for the stale read; fix by tracing which replicas formed each quorum.
5. Choose a remedy: strict quorums, read repair, or a different store for stock.

Prepares SRB-003-LAB1.

---
