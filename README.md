# Python Chat App (LAN)

A local real-time chat app using `socket`, `threading` and `Tkinter`.

## Files
| File | Purpose |
|---|---|
| `server.py` | Socket server, one thread per client, logging, commands |
| `client.py` | Tkinter chat window |
| `test_two_users.py` | Automated 2-user test (Alice & Bob) |
| `chat_log.txt` | Server log (join/leave/messages/commands) |
| `test_output.txt` | What each test user saw |

## How to run
1. **Server** (one machine): `python server.py` (default port 5000)
2. **Clients** (same or other machines on the LAN): `python client.py`
   - Same machine: IP `127.0.0.1`
   - Other machines: the server's LAN IP (`ipconfig` on Windows / `ifconfig` on Linux/Mac)
3. Open two client windows with different names and chat.
4. Automated check: `python test_two_users.py`

## Commands
- `/exit` - leave the chat
- `/mute` - toggle muting incoming chat messages (join/leave notices still show)
- `/users` - list who is online

## How it maps to the mini guide
1. **Socket server** - `server.py` `main()` binds, listens, accepts.
2. **Multiple clients** - `threading.Thread` per connection in `handle_client()`.
3. **Chat UI** - `client.py` uses a read-only `ScrolledText` plus an `Entry` and Send button; a receiver thread feeds a `queue` that the UI polls.
4. **Join/leave events** - server broadcasts `SYSTEM:` messages.
5. **Logs** - `log()` appends timestamped lines to `chat_log.txt`.
6. **Commands** - parsed in `handle_client()`.

## Notes
- If other computers can't connect, allow Python/port 5000 through the firewall.
- Protocol is plain text, one line per message, so it is not encrypted.
