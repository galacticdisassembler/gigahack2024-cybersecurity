# gigahack2024-cybersecurity

## Taskboard

✅ - Yes
❌ - No
❔- IDK

| Clue                                                                            | Investigated? | Decoy? | Description                                                                                     | Conclusion                                                |
| ------------------------------------------------------------------------------- | ------------- | ------ | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Validator C# Windows (target: `windows`)                                        | ❌             | ❔      | ❔                                                                                               | ❔                                                         |
| Validator C# Linux (target: `.net`)                                             | ❌             | ❔      | ❔                                                                                               | ❔                                                         |
| Folder: `Source`                                                                | ❌             | ❌      | Folder containing original 27 images with filename equal to filehash                            | Yeild `Private key Password "Cardano"`                    |
| Private Key                                                                     | ✅             | ❌      | Openssh private key used to connect to a remote machine                                         | Yeild `Publick key "serj@GWS-HOME"`                       |
| Public Key `bayron@cordano`                                                     | ✅             | ❌      | Public key, derivated from private, with, supposedly, manually changed user@host field          | ❔                                                         |
| Folder: `KeyPass`                                                               | ✅             | ❌      | Contains 7 identic images to the ones from `Source` with slight derivation (1 hex byte) in name | Yeild Password `Cardano`                                  |
| Public Key `serj@GWS-HOME`                                                      | ❌             | ❔      | Public key, derivated from private using password `Cardano`                                    | ❔                                                         |
| Username `serj`                                                                 | ❌             | ❌      | Supposedly, Byron's username                                                                    | Yeild `Remote Username`                                                         |
| Hostname `GWS-HOME`                                                             | ❌             | ❔      | ❔                                                                                               | ❔                                                         |
| Remote                                                                          | ✅             | ❌      | Indexed images with hex byte difference                                                         | Yeild `Cardano Node IP`                                   |
| 125.251.180.194                                                                 | ✅             | ❌      | Cardano node IP Serj connected to                                                               | Yeild Location `Korea`                                    |
| Cardano node location `Korea`, `Seoul`                                          | ✅             | ❌      | IP lookup showed that IP was in Korea                                                           | Cardano Node Serj connected to was hosted in Korea, Seoul |
| Cardano pool address `44d7fba88039561837d64773c1e7728c34f1c300edc9fa280263cc7f` | ❌             | ❔      | ❔                                                                                               |                                                           |

## Disclaimer

- As explained in the condition **"Unfortunately, communication with the agent was interrupted, but a package was delivered to the division office..."**, the next assumption could be valid that criminal group knew about spying and made some actions to lead us astray.

## Investigation

- Double check the flash drive
  
  - Producer - TrekStor
  
  - Mark - Leo
  
  - Form factor - Flat as my ex
  
  - Designed in Germany
  
  - Made in China
  
  - Sold in Poland [Trekstor Leo SMARTKEY - pamięć USB - 16GB - dodatkowa opcja dla Twojego Leo Smartkey - Pendrive - Morele.net](https://www.morele.net/pendrive-trekstor-leo-smartkey-pamiec-usb-16gb-dodatkowa-opcja-dla-twojego-leo-smartkey-7424826/) <u>as an addition to a smartkey</u>.
  
  - Sold on spanish amazon <https://www.amazon.es/Leo-Memoria-para-Insertar-Smartkey/dp/B00LA1DVZE>
  
  - Weight, according to amazon - 798gr
  
  - Actual weight - light as fuck
  
  - On amazon since - july 2014
  
  - ASIN - B00LA1DVZE
  
  - Space - 16 GB
  
  - Actual space - two volumes (EXFAT 12GB, EXT4 4GB)

- Who the fuck are we hunting?
  
  - The name is `serj`.
  
  - Workstation name is `GWS-HOME`.
  
  - Wrote a program in <u>C# for linux </u>and <u>C# for windows</u>?
  
  - Likes `Astrologic imagery`?
  
  - Likes `Lord of the rings`?
  
  - Needs `a wallpaper`?
  
  - Has `Adobe Photoshop` installed?
  
  - ---
  
  - ### General Observations

    1. **File Details:**

       - The images have varied file sizes, ranging from 1650 KiB to 12 MiB, with different dimensions and megapixels, indicating that they were likely captured by different devices or under varying settings.
       - The images show diverse resolutions, with some images being smaller (1080x2340) and others significantly larger (9600x6400), which suggests different contexts—possibly mobile devices for smaller images and high-end cameras for larger ones.

    2. **Image Metadata:**

       - Some of the images are associated with metadata comments like "GoodFon.ru" and "CREATOR: gd-jpeg," indicating that some of these files may have been processed by specific software, potentially pointing to post-processing or compression techniques.
       - The large resolution images (9600x6400, 9000x6000) point to either professional photography or high-resolution digital art.

    3. **Editing/Processing Software:**

       - Mentions of the sRGB IEC61966-2.1 color profile in one of the images indicate that the file might have been processed using tools that manage color spaces accurately, suggesting that the creator could have professional or semi-professional expertise in image editing.

    ### Inferences

    1. **Possible Devices Used:**

       - The presence of images with a width of 1080px (likely from a mobile device) along with high-resolution images of 9600px width (from a DSLR or advanced digital camera) suggests that the person might use both mobile photography and professional cameras.
       - The varied resolutions hint at different use cases for the images—perhaps some for casual or social media use (e.g., mobile phone images) and others for high-quality purposes such as prints or professional work.

    2. **Photography or Visual Media Interest:**

       - Given the wide range of image sizes and resolutions, the person might have an interest in photography or visual media production. The high-resolution images are suggestive of potential professional or hobbyist-level work.

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
