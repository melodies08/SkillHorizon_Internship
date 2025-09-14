# Step 3: HTTP Enumeration (Dirb)

**Objective:** To discover hidden or common directories and files on the target web server using brute-force techniques.

**Target:** `http://testfire.net/`

-----

### Command Used

```bash
dirb http://testfire.net /usr/share/wordlists/dirb/common.txt
```

-----

### Findings

The scan used the `common.txt` wordlist, which contains 4612 words. It discovered 15 directories and files on the server.

```
+ http://testfire.net/admin (CODE:302|SIZE:0)
+ http://testfire.net/aux (CODE:200|SIZE:0)
+ http://testfire.net/bank (CODE:302|SIZE:0)
+ http://testfire.net/com1 (CODE:200|SIZE:0)
+ http://testfire.net/com2 (CODE:200|SIZE:0)
+ http://testfire.net/com3 (CODE:200|SIZE:0)
+ http://testfire.net/con (CODE:200|SIZE:0)
+ http://testfire.net/images (CODE:302|SIZE:0)
+ http://testfire.net/lpt1 (CODE:200|SIZE:0)
+ http://testfire.net/lpt2 (CODE:200|SIZE:0)
+ http://testfire.net/nul (CODE:200|SIZE:0)
+ http://testfire.net/pr (CODE:302|SIZE:0)
+ http://testfire.net/prn (CODE:200|SIZE:0)
+ http://testfire.net/static (CODE:302|SIZE:0)
+ http://testfire.net/util (CODE:302|SIZE:0)
```

**Key Discovered Paths:**

  * `/admin`: Found with a 302 Redirect, which confirms its existence and likely points to a login page.
  * `/bank`: Also a 302 Redirect, indicating a primary application path.
  * `/images`, `/static`, `/util`: Directories that likely contain static content and utilities.
  * `/aux`, `/con`, `/nul`, `/prn`: The discovery of these paths, which are reserved filenames in Windows, is interesting and may indicate the underlying OS or a misconfiguration.

