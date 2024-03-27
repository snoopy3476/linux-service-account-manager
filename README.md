# Linux Service Account Manager (SAMAN)


## Description

Make a new linux user account which can be used as general purpose service account.  
(Mainly targeted for `RHEL`-derivatives, may also work on `Debian`-derivatives)  
  
Users created by this script will have:
- User systemd functions (with `loginctl enable-linger` and `export XDG_RUNTIME_DIR`)
- Ports opened for the account (in `firewalld`)
  - If `firewalld` is not installed on the system, [port] parameters are ignored.


## Usage

```
usage: saman <MODE> [args...]

  <MODE>
   - add:     create a new SAMAN service account
                 $ saman add <account-name> [port-1] [port-2] ...
   - ls:      list all SAMAN service accounts
                 $ saman ls
   - detail:  print details of an SAMAN service account
                 $ saman detail <account-name>
   - rm:      remove an SAMAN service account
                 $ saman rm <account-name> [force]
   - help:    print help message
                 $ saman help
```


## Remarks
Check below to utilize the script conveniently (Optional).

- To print manual for this command on ssh login:  
  1. Place `saman` script to `$PATH` (or just place the script in the directory `~/bin` if your shell supports it by default),  
  2. Then add below to the file `~/.ssh/rc`:
     ```shell
     printf "\n
     ===============[ SAMAN service account list ]===============
     %s
     ============================================================
     
     
     =======================[ SAMAN usage ]======================
     * Create or manage service accounts with the command 'saman'
     - %s
     ============================================================
     
     \n" "$(saman ls | tr '\n' '\t')" "$(saman help)"
     ```
     ![ssh login help message](readme-asset/ssh-login-help-msg.png)
