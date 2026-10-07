# Week 5 lab — Programmable Data Planes (P4)

Two P4 software switches (BMv2) in a Mininet network, both running `tunnel.p4`. You'll
watch a P4 pipeline forward IPv4, change its tables at run time, then finish a custom
tunnel header — and see what happens when the parser, the ingress and the deparser
disagree.

**The full step-by-step instructions are in the Lab tab of Week 5 on the course website.**

## Start

This repository is meant to be opened in **GitHub Codespaces** (Code → Codespaces →
Create codespace). The first start takes a few minutes while the lab image downloads.
Then, in the terminal:

```bash
python3 topo.py
```

That compiles `tunnel.p4`, starts the network, fills the switches' tables and opens the
`mininet>` prompt. Type `exit` to stop it; run it again after every change to `tunnel.p4`.

## Files

| File | What it is |
|---|---|
| `tunnel.p4` | The P4 program both switches run. You edit this. |
| `topo.py` | Builds the network: h1 — s1 — s2 — h2, h3. |
| `s1-commands.txt`, `s2-commands.txt` | Table entries loaded into each switch at start. |
| `send.py` | Sends one test packet, optionally tunnelled (run it on h1). |
| `receive.py` | Started automatically on h2 and h3; output in `logs/h2.txt`, `logs/h3.txt`. |
| `p4cli` | Sends one command to a switch's runtime CLI, e.g. `./p4cli s2 table_dump MyIngress.ipv4_lpm`. |
| `logs/s1.txt`, `logs/s2.txt` | What each switch did with every packet: parser states, tables, actions. |

## If something goes wrong

- **Mininet complains that interfaces already exist** (after a crash): run `mn -c`, then `python3 topo.py` again.
- **Compilation failed**: the message gives the line number in `tunnel.p4`. Check for a missing `;` or `}`.
- **The codespace stopped**: codespaces stop after 30 minutes idle. Restart it from github.com/codespaces; your edits are kept.
- **When you've finished the lab**, delete the codespace at github.com/codespaces so it stops using your storage quota.
