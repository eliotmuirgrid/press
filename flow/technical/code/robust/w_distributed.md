# Distributed resilient replication

This would be a neat idea for high availability and also do something which I thought would
make sense for a long time.  Rather than cover the landscape with data centers which are never
as cool as they look in the movies, instead leverage that fact that we all have computers.

So it would make it a lot easier for folks that want a website just to run their Flow instance
**most** of the time.  If you don't run it at all eventually your 'site' disappears.  But
basically it become a very resilient infra-structure that would be helpful for disaster recovery
scenarios.

The key would be to make it exceptionally [simple to use](/system/extreme) so that people who want
to have websites could just run a binary and get straight to talking about what ever they want to.

1. **Startup:**
   - Attempt to discover bootstrap peers (via DHT or hard-coded addresses).
   - Attempt to open ports via UPnP/NAT-PMP/PCP.
   - Start STUN-based NAT traversal if direct connections fail.

2. **Peer Discovery:**
   - Use DHT for lookup and advertisement.

3. **Secure Session Establishment:**
   - Exchange keys (ECDH, then encrypt).

4. **Participation:**
   - Maintain DHT entries, forward messages as needed.
   - Optionally relay traffic for those with unreachable NATs (if permitted).

| Protocol Area      | Protocol(s)                   | Purpose/Benefit                                      |
|--------------------|-------------------------------|------------------------------------------------------|
| Peer Discovery     | Kademlia DHT, mDNS            | Find peers without central server                    |
| NAT Traversal      | UPnP, NAT-PMP, PCP, STUN, ICE | Allow P2P through routers/NATs                       |
| Encryption         | TLS/DTLS, libsodium           | Keep all communications private                      |
| Transport          | QUIC, WebRTC, TCP             | Efficient, robust messaging between nodes            |
| Multiplexing       | QUIC, WebRTC, libp2p muxers   | Run multiple logical channels per connection         |

