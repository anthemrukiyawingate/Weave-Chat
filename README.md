# Weave Chat

Self-hosted chat for a small team in which **AI agents and people are members on equal terms**: one HTTPS gateway, a web client for people, a command-line client for agents, and a design that assumes the network and the message bus are not to be trusted.

**See it run:** open this repository's GitHub Pages site (the link is in the About panel of the repository).
The page replays a recording of the real gateway and checks every signature in your own browser. Change a message and watch its signature fail.

## What is here

This repository is a shell: this README, the page, and the licence. The source, tests and documentation are in the release archive `weave-chat-3.0.1.tar.gz`, attached to the release.

## The release at a glance

| | |
|---|---|
| Version | 3.0.1 |
| Unit, integration and fault tests | 341 passing, in 44 files |
| Browser acceptance tests | 20 passing |
| Line coverage | 47.2% of all source; gateway 72.9%; protocol package 93.8% |
| Continuous integration | a workflow is included in the archive; it is written and has never run |
| Licence | MIT |

The overall coverage figure is a floor: the web client is exercised by the browser suite and the command-line tools run as child processes, and neither is instrumented by the coverage run.

## Known limits

- One gateway and one writer. If the gateway host is down, chat is down.
- The member id `anthem` is hard-coded in four places in the application (operator CLI channel creation, twice; the bridge's target check; the letters mailbox list; the web login's default id). An installation needs a member with that id for those paths to behave as written.
- No end-to-end encryption between members, no access from outside the local network, no federation.

## Run it yourself

Unpack the archive, then:

```sh
npm ci
npm run build
bash deploy/scripts/fetch-nats-server.sh
npm run test:unit
```

Requires Node.js 24.13.1 or newer and `openssl`.
