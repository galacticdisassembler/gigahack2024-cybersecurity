# gigahack2024-cybersecurity

## Taskboard

✅ - Yes
❌ - No
❔- IDK

| Clue                                                                                | Investigated? | Decoy? | Description                                                                                                                                                               | Conclusion                                                                                                | Next Steps                                                                                                   |
| ----------------------------------------------------------------------------------- | ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **USB drive**                                                                       | ✅             | ❌      | Generic USB drive, designed by Germanese and produced in China.                                                                                                           | Yielded `EXFAT Volume` and `EXT4 Volume`.                                                                 | Forensic analysis of drive metadata (e.g., manufacturer details, timestamps).                                |
| **EXFAT Volume**                                                                    | ✅             | ❌      | 12GB volume, visible in Windows, contains images and validator binaries.                                                                                                  | Yielded `Folder: "Source"`, `Validator binary (target: Linux)`, and `Validator binary (target: Windows)`. | Analyze images for metadata (EXIF, timestamps, origin). Investigate validators' behavior in sandbox.         |
| **EXT4 Volume**                                                                     | ✅             | ❌      | 4GB volume, invisible in Windows, contains images, public, and private keys.                                                                                              | Yielded `Private Key`, `Public Key "byron@cordano"`, `Folder: "KeyPass"`, `Folder: "Remote"`.             | Use private key to attempt a connection. Explore `KeyPass` for encrypted credentials or key storage details. |
| **Validator C# Windows (target: `windows`)**                                        | ❌             | ❌      | C# validator for Windows. If the `ADA` environment variable is set to `Lovelace`, calculates file hash, compares with filename, and deems file valid based on comparison. | Used for file validation in a likely Cardano-related workflow.                                            | Reverse engineer binary to understand exact validation mechanism and purpose in Cardano blockchain context.  |
| **Validator C# Linux (target: `.net`)**                                             | ❌             | ❌      | C# validator for Linux. Same behavior as the Windows variant.                                                                                                             | Used for file validation in a likely Cardano-related workflow.                                            | Reverse engineer Linux binary. Test using a controlled environment to explore its functionality.             |
| **Folder: `Source`**                                                                | ❌             | ❌      | Contains 27 original images with filenames equal to their file hashes.                                                                                                    | Yielded `Private Key Password "Cardano"`.                                                                 | Analyze images for signs of tampering, and check if hashes are linked to any known assets in the blockchain. |
| **Private Key**                                                                     | ✅             | ❌      | OpenSSH private key, potentially for connecting to a remote server.                                                                                                       | Yielded `Public Key "serj@GWS-HOME"`.                                                                     | Attempt to establish a secure connection using the private key. Examine logs from SSH servers, if possible.  |
| **Public Key `byron@cordano`**                                                      | ✅             | ❌      | Public key derived from private key, with a possibly manually altered user@host field.                                                                                    | Used to validate private key connection in an unknown workflow.                                           | Investigate connections made using this public key. Look for signs of keypair usage in blockchain nodes.     |
| **Folder: `KeyPass`**                                                               | ✅             | ❌      | Contains 7 identical images to those in `Source`, with minor changes (1 hex byte) in filenames.                                                                           | Yielded password `Cardano`.                                                                               | Check for password-protected files and decrypt using `Cardano`. Compare hex byte changes to the originals.   |
| **Public Key `serj@GWS-HOME`**                                                      | ❌             | ❔      | Public key derived using the password `Cardano`.                                                                                                                          | ❔                                                                                                         | Check remote servers and logs for connections involving this public key.                                     |
| **Username `serj`**                                                                 | ❌             | ❌      | Likely username for Byron’s account on the connected system.                                                                                                              | Yielded `Remote Username`.                                                                                | Search for the username `serj` on systems connected to the Cardano node. Investigate related SSH logs.       |
| **Hostname `GWS-HOME`**                                                             | ❌             | ❌      | Likely hostname of Byron’s machine.                                                                                                                                       | Yielded `Remote Hostname`.                                                                                | Perform DNS/host lookups for `GWS-HOME`. Check if the machine has been active on the Cardano network.        |
| **Folder: `Remote`**                                                                | ✅             | ❌      | Indexed images with slight hex differences.                                                                                                                               | Yielded `Cardano Node IP`.                                                                                | Investigate connections between `Remote` folder images and any associated blockchain or network activity.    |
| **125.251.180.194**                                                                 | ✅             | ✅      | IP address of a Cardano node connected by Serj.                                                                                                                           | Yielded location `Korea`.                                                                                 | Perform network traffic analysis to confirm whether the node is still active. Consider contacting the host.  |
| **Cardano node location `Korea`, `Seoul`**                                          | ✅             | ✅      | IP lookup indicates the node is hosted in Korea.                                                                                                                          | Cardano node connected to Byron was hosted in Seoul.                                                      | Investigate further connections originating from this node. Look into possible Korean hosting services used. |
| **Cardano pool address `44d7fba88039561837d64773c1e7728c34f1c300edc9fa280263cc7f`** | ✅             | ✅      | Unknown address. Possibly linked to a Cardano staking pool or transaction.                                                                                                | Wrong direction, halt investigation.                                                                                                         | Research Cardano pool databases for information on this address. Investigate for any unusual activity.       |

## Disclaimer

The information presented in this document is based on the assumption that the communication with the agent was interrupted, as noted in the condition: **"Unfortunately, communication with the agent was interrupted, but a package was delivered to the division office..."**. Given these circumstances, it is plausible to assume that the criminal group involved may have been aware of surveillance activities and took deliberate actions to mislead our investigation. This conclusion is speculative and should be treated with caution, as no definitive proof of the group's awareness or intentions has been confirmed.

## Investigation

1. **USB Flash Drive**: 
   - **Producer**: TrekStor, Model: Leo
   - **Capacity**: 16GB split into two volumes:
     - **EXFAT Volume** (12GB, Windows-visible): Contains images and validator binaries.
     - **EXT4 Volume** (4GB, Linux-only): Holds sensitive data like private/public keys and images.

2. **Volumes Investigation**:

   - **EXFAT Volume**:
     - **Folder: Source**: Contains 27 images with filenames matching file hashes.
     - **Validator Binaries**:
       - Windows Validator: A C# program that verifies file integrity if the `ADA` environment variable is set to `Lovelace`.
       - Linux Validator: Similar to Windows but for Linux (.NET-based).
     - **Key Findings**: The validator binaries could be linked to a specific Cardano workflow to validate files.

   - **EXT4 Volume**:
     - **Private Key**: OpenSSH private key found, potentially for remote machine access.
     - **Public Key `byron@cordano`**: Public key derived from the private key, but the user@host field (`byron@cordano`) appears to be manually changed.
     - **Folder: KeyPass**: Contains images slightly modified from the `Source` folder (1 hex byte difference).
     - **Folder: Remote**: Indexed images with two hex bytes difference, potentially used to obfuscate or encode data.
     - **Key Findings**: Sensitive cryptographic data (public/private keys) found, suggesting potential access to external systems.

3. **Validator Binaries**:
   - **Windows Validator** (C#): Checks if the `ADA` environment variable is set to `Lovelace` and validates files based on their hash.
   - **Linux Validator** (.NET): Similar functionality, but built for Linux.
   - **Key Findings**: These validators seem to be part of a custom file validation system, possibly for a blockchain-related application (Cardano). All images under `Source` folder are `Valid`. All images under `KeyPass` and `Remote` folders are `Invalid`

4. **Folder: KeyPass**

   - **Contents**:  
     - Each image in this folder has slight hexadecimal modifications when compared to the original images in the Source folder. The modifications are minimal and analyzed for differences using `exif_comp.py`. Hash comparisons reveal small, deliberate alterations between the images.

   - **Hexadecimal Comparison Example**:
     - Images are compared by their hashes, highlighting small changes in specific hexadecimal characters. Here's a sample comparison:

         ```text
         Comparing two images:
         4376887a860d2634b48a0a766128261cc69f63cb3d00f5793e399e3b2d2111fb
         5876887a860d2634b48a0a766128261cc69f63cb3d00f5793e399e3b2d2111fb
         Differences: 4->5, 3->8
         ```

   - **Python Script (`exif_comp.py`)**:
     - This Python script compares the hashes of images stored in two folders and highlights hexadecimal differences between them.

      ```python
      import re

      regex = r"[<>] ======== \.\.\/vol\d+\/[^\/]+\/([a-f0-9]{64})\.jpg"

      def diff_characters(str1, str2):
          diff = []
          for c1, c2 in zip(str1, str2):
              if c1 != c2:
                  diff.append(f"{c1}->{c2}")
          return ', '.join(diff)

      with open('a.txt', 'r') as file:
          test_str = file.read()

      matches = list(re.finditer(regex, test_str, re.MULTILINE))

      for i in range(0, len(matches), 2):
          match1 = matches[i]
          match2 = matches[i + 1]
          
          group1 = match1.group(1)
          group2 = match2.group(1)
          
          print(f"Comparing:\n{group1}\n{group2}")
          print(f"Differences: {diff_characters(group1, group2)}")
          print("-" * 50)
      ```

   - **Script Run Results**:
     - The output below demonstrates hexadecimal changes between the original and modified images, indicating intentional minor adjustments:

         ```text
         Comparing:
         4376887a860d2634b48a0a766128261cc69f63cb3d00f5793e399e3b2d2111fb
         5876887a860d2634b48a0a766128261cc69f63cb3d00f5793e399e3b2d2111fb
         Differences: 4->5, 3->8
         --------------------------------------------------
         Comparing:
         6a613a24bc0556cec9499192866c0b597aa0427599c8d3280b1f65ecefab35a6
         6a7e3a24bc0556cec9499192866c0b597aa0427599c8d3280b1f65ecefab35a6
         Differences: 6->7, 1->e
         --------------------------------------------------
         Comparing:
         75ee720170bcf182f0ef6d766723a8a553d7d529f8b949eaadc53bb90dacf8b6
         75ee0d0170bcf182f0ef6d766723a8a553d7d529f8b949eaadc53bb90dacf8b6
         Differences: 7->0, 2->d
         --------------------------------------------------
         Comparing:
         82e2e864557ddc3163e2943a2b3e9741006cf43a46812408f056ab45afaff5cd
         82e2e85d557ddc3163e2943a2b3e9741006cf43a46812408f056ab45afaff5cd
         Differences: 6->5, 4->d
         --------------------------------------------------
         Comparing:
         970c6c3f61bec951907c5c0bcd2252d18e60dd9745adf0d3955534dc89e2f500
         970c6c3ff2bec951907c5c0bcd2252d18e60dd9745adf0d3955534dc89e2f500
         Differences: 6->f, 1->2
         --------------------------------------------------
         Comparing:
         97f952b96f6e267656cf482f8d584a3c0b0eaf8bf237eb01573d84b126fe2684
         97f952b96f9d267656cf482f8d584a3c0b0eaf8bf237eb01573d84b126fe2684
         Differences: 6->9, e->d
         --------------------------------------------------
         Comparing:
         9d954ed4c8a66f40b993418b336ae4becce513ce31ac6edaffe97ae7d0ddaab5
         9d954ed4c8a6ba40b993418b336ae4becce513ce31ac6edaffe97ae7d0ddaab5
         Differences: 6->b, f->a
         --------------------------------------------------
         Comparing:
         007db8b4e3fe6e97917c6cf40d89b1507f9350f0de9d58ff6a0a0a28311ce22a
         1092b8b4e3fe6e97917c6cf40d89b1507f9350f0de9d58ff6a0a0a28311ce22a
         Differences: 0->1, 0->0, 7->9, d->2
         --------------------------------------------------
         Comparing:
         01fb4a28284240c1d85268fb1c2baaa462caf761f0969da17a0c93ea2e8b29d1
         1dc84a28284240c1d85268fb1c2baaa462caf761f0969da17a0c93ea2e8b29d1
         Differences: 0->1, 1->d, f->c, b->8
         --------------------------------------------------
         Comparing:
         02b421415a263025ff0456b582fd8710965639fc84f63d68c23349e780fcb4ec
         eda921415a263025ff0456b582fd8710965639fc84f63d68c23349e780fcb4ec
         Differences: 0->e, 2->d, b->a, 4->9
         --------------------------------------------------
         Comparing:
         03c2c5805b9834280d2465ec0784964e07cb39dff426c0257f06729994300071
         f22cc5805b9834280d2465ec0784964e07cb39dff426c0257f06729994300071
         Differences: 0->f, 3->2, c->2, 2->c
         --------------------------------------------------
         ```

   - **Hexadecimal to ASCII Conversion**:
     - By converting the hexadecimal values to ASCII, patterns in the differences were discovered. For example:
       - `43 -> C`
       - `61 -> a`
       - `72 -> r`
       - `64 -> d`
       - `6e -> n`
       - `6f -> o`
     - These differences suggest the changes may correspond to specific readable data in the images.

5. **Connections to Remote Machine**:
   - **Private Key**: SSH private key suggests access to a remote machine.
   - **Public Key `serj@GWS-HOME`**: Derivable from the private key using password `Cardano`. Perhaps, a windows machine, due to hostname pattern.
   - **Key Findings**: The key data and public/private key pairs suggest that `serj` may have access to a remote Cardano node.

6. **Folder: Remote**:
   - Contains indexed images with slight variations (two hex bytes differences), potentially used for obfuscation or encoding purposes.
   - **Key Findings**: This folder likely contains further clues about the data transmission methods used by `serj` and could hide additional files or instructions.

7. **Public Key `byron@cordano`**:
   - A public key derived from the private key, but the user@host field (`byron@cordano`) is suspiciously altered.
   - **Key Findings**: Likely an intentional modification to hide the true identity of the machine `serj` is connecting to.

8. **Cardano Node IP and Location (Mistaken Direction)**:
   - IP Address: 125.251.180.194
   - Location: Seoul, South Korea
   - Important Note:
      - Error: This IP was incorrectly derived from the Remote folder, leading to an unintended result.
      - Misstep: The IP traced to South Korea was a false lead and does not align with the intended investigation.
   - Key Findings: Although linked to a Cardano node, this is not relevant to the actual investigation and should be disregarded.

---

## Conclusion

   `#TODO`

---

## Draft ideas

Source
58
7e
0d
5d
f2
9d
ba
1092  16 || 146
1dc8  29 || 200
eda9 237 || 169
f22c 242 || 44

KeyPass
43  C
61  a
72  r
64  d
61  a
6e  n
6f  o
Remote
007d  125 || 215
01fb  251 || 191
02b4  180 || 75
03c2 194 || 44

125.251.180.194

215.191.75.44

16.29.237.242

130.4.75.61

7.31.43.60

007d01fb02b403c2

10, 92, 1d, c8, ed, a9, f2, 2c, 00, 7d, 01, fb, 02, b4, 03, c2
1, 0, 9, 2, 1, d, c, 8, e, d, a, 9, f, 2, 2, c, 0, 0, 7, d, 0, 1, f, b, 0, 2, b, 4, 0, 3, c, 2
