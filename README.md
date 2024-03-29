# Linux Service Account Manager (LSAM)


## Description

Make a new linux user account which can be used as general purpose service account.  
(Mainly targeted for `RHEL`-derivatives, may also work on `Debian`-derivatives)  
  
Users created by this script will have:
- User systemd functions (with `loginctl enable-linger` and `export XDG_RUNTIME_DIR`)
- Ports opened for the account (in `firewalld`)
  - If `firewalld` is not installed on the system, [port] parameters are ignored.


## Usage

```
usage: lsam <MODE> [args...]

  <MODE>
   - add:     create a new LSAM service account
                 $ lsam add <account-name> [port-1] [port-2] ...
   - ls:      list all LSAM service accounts
                 $ lsam ls
   - detail:  print details of an LSAM service account
                 $ lsam detail <account-name>
   - rm:      remove an LSAM service account
                 $ lsam rm <account-name> [force]
   - help:    print help message
                 $ lsam help
```


## Remarks
Check below to utilize the script conveniently (Optional).

- To print manual for this command on ssh login:  
  1. Place `lsam` script to `$PATH` (or just place the script in the directory `~/bin` if your shell supports it by default),  
  2. Then add below to the file `~/.ssh/rc`:
     ```shell
     printf "\n
     ================[ LSAM service account list ]===============
     %s
     ============================================================
     
     
     =======================[ LSAM usage ]=======================
     * Create or manage service accounts with the command 'lsam'.
     - %s
     ============================================================
     
     \n" "$(lsam ls | tr '\n' '\t')" "$(lsam help)"
     ```
     ![ssh login help message](readme-asset/ssh-login-help-msg.png)
