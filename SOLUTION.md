# CTF Steganography Challenge - Hidden Whispers Solution

## Challenge Description
- **Name**: Hidden Whispers
- **Points**: 150
- **Hint**: "Sometimes secrets aren't locked too tightly — you just need the right word to open the door."

## Files Provided
- `wall.jpg` - A JPEG image file (124KB, 540x360 pixels)

## Solution Process

### 1. Initial Analysis
- Examined the JPEG file metadata using `exiftool` - no suspicious metadata found
- Used `binwalk` to check for embedded files - only standard JPEG structure detected
- Searched for readable strings in the file - no obvious flag patterns found

### 2. Steganography Analysis
The hint suggested that secrets aren't "locked too tightly", implying weak security or simple passwords.

Used `steghide` (a steganography tool for JPEG/BMP files) to attempt data extraction:

```bash
steghide extract -sf wall.jpg -p "123456"
```

### 3. Password Discovery
After trying various passwords based on the challenge theme:
- `whispers`, `hidden`, `door`, `secrets`, `word`, `flag`, `ctf` - all failed
- `123456` - **SUCCESS!** 

The password "123456" aligns perfectly with the hint about secrets not being "locked too tightly" - it's one of the most common weak passwords.

### 4. Flag Extraction
The steghide extraction created a file `hidden.txt` containing:
```
flag{E4SY_ST3G_UNL0CK3D}
```

## Final Answer
**FLAG**: `flag{E4SY_ST3G_UNL0CK3D}`

## Tools Used
- `steghide` - For steganography extraction
- `exiftool` - For metadata analysis  
- `binwalk` - For embedded file detection
- `strings` - For text analysis

## Key Learning
The challenge demonstrates that even when steganography is used to hide data, weak passwords make the protection ineffective. The hint was crucial in guiding towards trying common weak passwords rather than complex ones.