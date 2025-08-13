# confuzyld

⚠️ This is an outline of a prototype. The code does not exist yet; alternatively, it may only be partially existent on
Zynth1a's laptop.

`confuzyld` is a work-in-progress rewrite of Geneva (censorship.ai) in Go; it is a network fuzzer primarily aimed at
censorship circumvention. It may be usable for other purposes like penetration testing, but such purposes were not the
primary motivation for writing it.

`confuzyld` targets both nation-state censorship (such as the Great Firewall of China) and school censorship (often
euphemistically referred to as “student safety software”). Like it or not, open-source censorship circumvention tools
will be appropriated by students to bypass school web filters, so we may as well state this use case up front instead
of trying to deny it. This allows students to make useful contributions and encourages them to consider the risks of
getting caught (see "Caveats").

## Explanation

Most anti-censorship solutions require assistance from outside of the censored network. For instance, VPN software
requires a VPN server outside of the censored network which censored clients then connect to. `confuzyld` can run on only
one side of the connection, though running `confuzyld` on both sides of a connection is also possible and may assist with
development of obfuscated tunneling protocols.

The idea behind `confuzyld` is that censors tend to have bugs in them, meaning it is possible to tamper with packet
streams to confuse the censor without impacting the client-to-server communication. `confuzyld` is likely to be effective
against most types of in-network censorship, but it cannot be used against IP-blocking censorship. This idea has been
confirmed to work by Geneva (censorship.ai) as a proof of concept, but their implementation of it is slow and
platform-specific.

`confuzyld` contains two components: a genetic algorithm, used to evolve new network strategies, and a strategy engine,
used to run a strategy on top of a TCP connection.

## Caveats

- Running `confuzyld` requires root access to your local device, as root access is required to craft arbitrary TCP
  packets. This means you cannot use `confuzyld` on school-provided laptops, only on BYOD ones.
- `confuzyld` developers are not responsible for any negative consequences that may arise from being caught using
  `confuzyld`. In schools this could include suspension or revocation of computer privileges; in censored nation-states
  this could include termination of internet service, arrest, or imprisonment.
- `confuzyld` is a noisy circumvention tool and requires testing against a live censor. Use of `confuzyld`, particularly in
  the training phase, will trigger censorship many times and generate clearly anomalous traffic. This may or may not be
  dangerous depending on how much network-level monitoring is done for circumvention-related traffic.
- `confuzyld` currently only works on TCP connections. This is motivated by the idea that most internet traffic can work
  over TCP. If DNS is censored on your network, you can enable DNS over HTTPS (DoH) and use `confuzyld` to unblock the
  DoH server.
- `confuzyld` may cause chaos if deployed against a censor like Linewize that uses rapidly-iterating ML techniques,
  because `confuzyld` itself uses rapidly-iterating ML techniques.
