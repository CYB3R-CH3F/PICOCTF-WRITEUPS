# Number Bases & Encoding — PicoCTF Write-Up

Category:General Skills & Cryptography  
Difficulty: 🟢 Easy  
Challenges: 5  
Author: CYB3R_CH3F  

> 📄 [Download PDF write-up](./CYB3R_CH3F_Number_PicoCTF_Bases_And_Encoding.pdf)

## Challenges Covered

| # | Challenge | Category | Flag |
|---|-----------|----------|------|
| 1 | Mod 26 (ROT13) | Cryptography | `picoCTF{next_time_I'll_try_2_rounds_of_rot13_45559abd}` |
| 2 | Warmed Up | General Skills | `picoCTF{61}` |
| 3 | 2warm | General Skills | `picoCTF{101010}` |
| 4 | Bases | General Skills | `picoCTF{l3arn_th3_r0p35}` |
| 5 | Warm | General Skills | `picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}` |



## Challenge 1 — Mod 26 (ROT13)

### What's the challenge asking?

Decode a ROT13-encoded string from a file called `values.txt` to find the flag.

### Concept: What is ROT13?

ROT13 stands for **Rotate by 13**. Every letter in the alphabet shifts 13 places forward. Since the alphabet has 26 letters, applying ROT13 twice brings you back to the original — the same operation both encodes and decodes.

It is not real encryption. Anyone can reverse it instantly. In cybersecurity it is called a **substitution cipher** — one character is swapped for another based on a fixed rule.

### Encoded Text

```
cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_45559noq}
```

### Command Used

```bash
cat values.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

**Breaking it down:**
- `cat values.txt` — print the file contents
- `|` — pipe the output into the next command
- `tr 'A-Za-z' 'N-ZA-Mn-za-m'` — translate every letter by shifting 13 places (ROT13)

### 🎯 Flag

```
picoCTF{next_time_I'll_try_2_rounds_of_rot13_45559abd}
```

### Key Takeaways

- ROT13 = substitution cipher. Every letter shifts 13 places.
- Encoding ≠ Encryption. ROT13 has no key — anyone can reverse it.
- The `tr` command translates characters in Linux — useful for simple ciphers.

---

## Challenge 2 — Warmed Up (Hex → Decimal)

### What's the challenge asking?

Convert **0x3D** from hexadecimal (base 16) to decimal (base 10).

### Concept: What is Hexadecimal?

Hex uses 16 digits: 0–9 and A–F, where A=10, B=11, C=12, D=13, E=14, F=15. The `0x` prefix just means the number is in hex. You will see hex constantly in cybersecurity — memory addresses, byte values, color codes.

### Working It Out

```
0x3D = 3D in hex

3  x  16  =  48
D  =  13
48 + 13  =  61
```

No terminal needed — pure math.

### 🎯 Flag

```
picoCTF{61}
```

### Key Takeaway

- `0x` prefix = hexadecimal. Always.
- D in hex = 13 in decimal. Memorise A–F values.

---

## Challenge 3 — 2warm (Decimal → Binary)

### What's the challenge asking?

Convert **42** from decimal (base 10) to binary (base 2).

### Concept: What is Binary?

Binary uses only two digits: 0 and 1. Every piece of data in a computer is stored as binary. To convert decimal to binary, keep dividing by 2 and read the remainders from bottom to top.

### Working It Out

```
42 / 2 = 21  remainder 0
21 / 2 = 10  remainder 1
10 / 2 =  5  remainder 0
 5 / 2 =  2  remainder 1
 2 / 2 =  1  remainder 0
 1 / 2 =  0  remainder 1

Read bottom to top: 101010
```

### 🎯 Flag

```
picoCTF{101010}
```

### Key Takeaway

- Binary = base 2. Only 0s and 1s.
- Always read remainders from **bottom to top**.

---

## Challenge 4 — Bases (Base64)

### What's the challenge asking?

Decode the string `bDNhcm5fdGdgzX3lwcDM1` — it has something to do with bases.

### Concept: What is Base64?

Base64 encodes binary data into readable text using 64 characters (A–Z, a–z, 0–9, +, /). It is not encryption — anyone can decode it with no key needed. You will see it in web tokens, email attachments, and CTF challenges constantly.

### Command Used

```bash
echo "bDNhcm5fdGdgzX3lwcDM1" | base64 -d
```

**Breaking it down:**
- `echo` — prints the string to the terminal
- `|` — pipes the output into the next command
- `base64 -d` — decode from Base64 (`-d` = decode)

### Output

```
l3arn_th3_r0p35
```

### 🎯 Flag

```
picoCTF{l3arn_th3_r0p35}
```

### Key Takeaway

- Base64 = encoding, not encryption. No key needed to reverse it.
- `echo "string" | base64 -d` — remember this command.

---

## Challenge 5 — Warm (Help Flags)

### What's the challenge asking?

Download a binary called `warm`, make it executable, and pass it a help flag to reveal the hidden flag.

### Steps

```bash
# Step 1 — Download the file
wget <URL from challenge page>

# Step 2 — Make it executable
chmod +x warm

# Step 3 — Run it to see what it wants
./warm
# Output: Hello user! Pass me a -h to learn what I can do!

# Step 4 — Pass the help flag
./warm -h
```

### Mistake I Made (So You Don't)

```bash
# WRONG — these are not standalone commands
$ -h
-h: command not found

$ -- help
--: command not found
```

`-h` is not a command on its own. It is a flag you pass **to** the program:

```bash
# CORRECT
./warm -h
```

### 🎯 Flag

```
picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
```

### Key Takeaways

- `wget` downloads files from the internet directly in the terminal.
- `chmod +x` makes a file executable — without it the OS will not run it.
- `./` means run this file from the current directory.
- `-h` and `--help` are flags you pass **to** a program, not standalone commands.
- Always read error messages — they tell you exactly what went wrong.

---

## Concepts Summary

| Concept | What it is | Challenge |
|---------|-----------|-----------|
| ROT13 | Shift every letter by 13 places | Mod 26 |
| Hexadecimal | Base 16 number system (0–9, A–F) | Warmed Up |
| Binary | Base 2 number system (0 and 1) | 2warm |
| Base64 | Encoding binary data as readable text | Bases |
| chmod +x | Make a file executable in Linux | Warm |
| wget | Download files from the internet | Warm |
| -h / --help | Pass a help flag to a program | Warm |

---

*— CYB3R_CH3F*
