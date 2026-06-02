[ssh-netcat-README.md](https://github.com/user-attachments/files/28507308/ssh-netcat-README.md)
# SSH & Netcat — PicoCTF Write-Up

**Category:** General Skills  
**Difficulty:** 🟢 Easy  
**Author:** CYB3R_CH3F  

> 📄 [Download PDF write-up](./writeup.pdf)

---

## Challenge 1 — Secure Shell (SSH)

### What's the challenge asking?

Connect to a remote server using SSH with a custom port, username, and password. Once connected, the flag is printed in the session output.

### Concepts you need to know first

**SSH (Secure Shell)** is an encrypted protocol for remote login. Think of it as a locked tunnel into another computer — everything you send is encrypted so nobody can intercept it. The default port is 22, but servers can run SSH on any port.

### Connection Details

| Field    | Value                  |
|----------|------------------------|
| Host     | titan.picoctf.net      |
| Port     | 60126                  |
| Username | ctf-player             |
| Password | 84b12bae               |

### Command Used

```bash
ssh -p 60126 ctf-player@titan.picoctf.net
```

**Breaking it down:**
- `ssh` — the SSH client
- `-p 60126` — custom port (default is 22, always use `-p` when it's different)
- `ctf-player@titan.picoctf.net` — username @ hostname

**What happened:**
1. Got a fingerprint warning — typed `yes` to accept it
2. Entered the password when prompted
3. Flag appeared in the welcome message

### 🎯 Flag

```
picoCTF{s3cur3_c0nn3ct10n_07a987ac}
```

### Key Takeaways

- SSH = encrypted remote login. Nothing travels in plaintext.
- Always use `-p` when the port is not the default 22.
- The fingerprint prompt is SSH protecting you from man-in-the-middle attacks.

---

## Challenge 2 — what's a netcat?

### What's the challenge asking?

Connect to a server using Netcat at a given host and port. The server sends the flag back — just read it.

### Concepts you need to know first

**Netcat (nc)** is called the Swiss Army knife of networking. It opens a raw TCP or UDP connection — no encryption, no login. Whatever the server sends, you see it. In CTFs, `nc` is used constantly to interact with challenge servers.

### Connection Details

| Field | Value                        |
|-------|------------------------------|
| Host  | fickle-tempest.picoctf.net   |
| Port  | 59546                        |

### Mistake I Made (So You Don't)

I copied the challenge description text directly and pasted it as a command. The description said *"at port 59546"* in plain English, so those words ended up in my terminal:

```bash
# WRONG — copied natural language into the terminal
$ nc fickle-tempest.picoctf.net at port 59546
invalid port at
```

The words `at port` are **not** part of the command. Netcat just takes the host then the port number directly.

### Command Used

```bash
# CORRECT
nc fickle-tempest.picoctf.net 59546
```

**Breaking it down:**
- `nc` — netcat utility
- `fickle-tempest.picoctf.net` — the server to connect to
- `59546` — port number only, nothing else

### 🎯 Flag

```
picoCTF{nEtCat_Mast3ry_5c7cC1a9}
```

### Key Takeaways

- Netcat syntax: `nc <host> <port>` — port is just the number, no extra words.
- Unlike SSH, no encryption and no login. Raw and direct.
- **Read the actual command syntax, not the plain English description.**

---

## SSH vs Netcat — Quick Comparison

|              | SSH                        | Netcat (nc)           |
|--------------|----------------------------|-----------------------|
| Encryption   | ✅ Yes                     | ❌ No                 |
| Auth         | Username + Password / Key  | None                  |
| Syntax       | `ssh -p PORT user@host`    | `nc host PORT`        |
| CTF use      | Log into remote machines   | Talk to challenge servers |
| Traffic      | Encrypted tunnel           | Raw plaintext         |

---

*— CYB3R_CH3F*
